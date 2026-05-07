<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>GazeBridge: Neural Trainer v2</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;900&display=swap');
        body {
            font-family: 'Orbitron', sans-serif;
            background-color: #020617;
            color: #00d2ff;
            overflow: hidden;
            touch-action: none;
        }
        #target {
            width: 80px; height: 80px;
            position: absolute;
            border: 2px solid #00d2ff;
            border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            transition: transform 0.1s linear, filter 0.3s ease;
            box-shadow: 0 0 20px rgba(0, 210, 255, 0.2);
            left: 0; top: 0;
        }
        .locked {
            border-color: #ff0055 !important;
            box-shadow: 0 0 40px #ff0055 !important;
            transform: scale(1.2) !important;
        }
        .progress-ring {
            transition: stroke-dashoffset 0.1s linear;
            transform: rotate(-90deg);
            transform-origin: 50% 50%;
        }
        #debug-panel {
            font-family: monospace;
            font-size: 10px;
            color: rgba(0, 210, 255, 0.5);
        }
    </style>
</head>
<body class="flex flex-col h-screen p-6">

    <div class="flex justify-between items-start mb-4">
        <div>
            <div class="text-[0.6rem] opacity-50 uppercase tracking-widest">Pilot</div>
            <div class="font-black text-xl">DANI_01</div>
        </div>
        <div class="text-right">
            <div class="text-[0.6rem] opacity-50 uppercase tracking-widest">Status</div>
            <div id="state-label" class="font-black text-xl italic text-cyan-400">WAITING</div>
        </div>
    </div>

    <div id="debug-panel" class="mb-4 bg-black/40 p-2 rounded border border-white/5">
        > SENSORS: <span id="sensor-status">OFFLINE</span><br>
        > DELTA: <span id="delta-val">0.00</span>
    </div>

    <div id="field" class="flex-grow relative border border-white/10 rounded-3xl overflow-hidden bg-white/[0.02]">
        <div id="target">
            <div class="absolute w-6 h-[2px] bg-[#00d2ff]"></div>
            <div class="absolute w-[2px] h-6 bg-[#00d2ff]"></div>
            <svg class="absolute" width="100" height="100" viewBox="0 0 100 100">
                <circle id="timer-ring" class="progress-ring" stroke="#ff0055" stroke-width="5" fill="transparent" r="45" cx="50" cy="50" stroke-dasharray="282.7" stroke-dashoffset="282.7"/>
            </svg>
        </div>
        
        <!-- Simulation Button (Hidden by default) -->
        <div id="sim-box" class="hidden absolute inset-0 bg-black/80 flex flex-col items-center justify-center p-10 text-center z-[100]">
            <p class="text-sm mb-6 text-white">Датчики заблокированы браузером.<br>Запустите симуляцию для проверки логики.</p>
            <button onclick="startSimulation()" class="px-8 py-4 bg-pink-600 text-white font-bold rounded-full">ЗАПУСТИТЬ СИМУЛЯЦИЮ</button>
        </div>
    </div>

    <div class="mt-6 flex flex-col gap-4">
        <div class="flex justify-between items-end">
            <div class="flex-grow mr-4">
                <div class="text-[0.5rem] uppercase mb-1 opacity-50">Stability Link</div>
                <div class="w-full h-2 bg-gray-900 rounded-full overflow-hidden">
                    <div id="stability-fill" class="h-full bg-cyan-400 w-0 transition-all duration-200"></div>
                </div>
            </div>
            <div id="score" class="text-3xl font-black italic">0000</div>
        </div>
        
        <button id="initBtn" class="w-full py-4 bg-white text-black font-black text-sm uppercase tracking-widest rounded-xl shadow-xl active:scale-95 transition-transform">
            Initialize Link
        </button>
    </div>

    <script>
        const target = document.getElementById('target');
        const field = document.getElementById('field');
        const initBtn = document.getElementById('initBtn');
        const stabilityFill = document.getElementById('stability-fill');
        const scoreVal = document.getElementById('score');
        const timerRing = document.getElementById('timer-ring');
        const stateLabel = document.getElementById('state-label');
        const sensorStatus = document.getElementById('sensor-status');
        const deltaDisplay = document.getElementById('delta-val');
        const simBox = document.getElementById('sim-box');

        let score = 0;
        let isRunning = false;
        let isSimulating = false;
        let stability = 0;
        let lockProgress = 0;
        let lastRot = 0;
        let lastUpdate = Date.now();
        
        const LOCK_THRESHOLD = 92; 
        const LOCK_TIME = 800; // 800ms per Stein

        let targetX = 100, targetY = 100;
        let velX = 2, velY = 2;

        function animate() {
            if (!isRunning) return;
            const now = Date.now();
            const dt = now - lastUpdate;
            lastUpdate = now;

            if (stability < LOCK_THRESHOLD) {
                // ДВИЖЕНИЕ (Поиск)
                targetX += velX; targetY += velY;
                if (targetX <= 0 || targetX >= field.clientWidth - 80) velX *= -1;
                if (targetY <= 0 || targetY >= field.clientHeight - 80) velY *= -1;
                
                target.style.transform = `translate(${targetX}px, ${targetY}px)`;
                target.classList.remove('locked');
                target.style.filter = "blur(10px)";
                lockProgress = 0;
                timerRing.style.strokeDashoffset = 282.7;
                stateLabel.textContent = "SEARCHING";
                stateLabel.style.color = "#22d3ee";
            } else {
                // ЗАХВАТ (Покой)
                target.classList.add('locked');
                target.style.filter = "blur(0px)";
                lockProgress += dt;
                stateLabel.textContent = "LOCKING...";
                stateLabel.style.color = "#f43f5e";
                
                const offset = 282.7 - (Math.min(lockProgress / LOCK_TIME, 1) * 282.7);
                timerRing.style.strokeDashoffset = offset;

                if (lockProgress >= LOCK_TIME) {
                    onSuccess();
                }
            }
            requestAnimationFrame(animate);
        }

        function onSuccess() {
            score += 100;
            scoreVal.textContent = score.toString().padStart(4, '0');
            targetX = Math.random() * (field.clientWidth - 80);
            targetY = Math.random() * (field.clientHeight - 80);
            lockProgress = 0;
            stability = 0; 
            if (navigator.vibrate) navigator.vibrate([50, 30, 50]);
            stateLabel.textContent = "ACQUIRED!";
        }

        async function init() {
            initBtn.style.display = 'none';
            // Проверка на iOS
            if (typeof DeviceOrientationEvent !== 'undefined' && typeof DeviceOrientationEvent.requestPermission === 'function') {
                try {
                    const permission = await DeviceOrientationEvent.requestPermission();
                    if (permission === 'granted') start();
                    else alert("Нужен доступ к датчикам.");
                } catch (e) { start(); }
            } else {
                start();
            }

            // Если через 3 сек данных нет - предлагаем симуляцию
            setTimeout(() => {
                if (stability === 0 && !isSimulating) {
                    simBox.classList.remove('hidden');
                }
            }, 3000);
        }

        function start() {
            isRunning = true;
            sensorStatus.textContent = "ACTIVE";
            window.addEventListener('deviceorientation', (e) => {
                if (isSimulating) return;
                let total = Math.abs(e.beta || 0) + Math.abs(e.gamma || 0);
                let delta = Math.abs(total - lastRot);
                lastRot = total;
                deltaDisplay.textContent = delta.toFixed(2);

                let currentStab = Math.max(0, 100 - (delta * 25));
                stability = (stability * 0.7) + (currentStab * 0.3);
                stabilityFill.style.width = `${stability}%`;
            });
            animate();
        }

        function startSimulation() {
            isSimulating = true;
            isRunning = true;
            simBox.classList.add('hidden');
            sensorStatus.textContent = "EMULATED";
            // Цикл симуляции: 2 сек движение, 2 сек покой
            setInterval(() => {
                stability = (Math.random() > 0.5) ? 98 : 40;
                stabilityFill.style.width = `${stability}%`;
            }, 2000);
            animate();
        }

        initBtn.addEventListener('click', init);
    </script>
</body>
</html>
