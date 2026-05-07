<!-- 
  PROJECT: GazeBridge // Mission: Commander Zero
  ARCHITECT: Svetlana Vorobeva
  PURPOSE: OMA Neural Orthotic // Ticker Mode v6
  LOGIC: "Morpheme Slicing" & "Lexend Deceleration"
  SCIENCE: Reducing Visual Crowding via Lexend font and Color-coded chunks.
-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>GazeBridge: Ticker v6</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* LEXEND is the scientific choice for reading fluency */
        @import url('https://fonts.googleapis.com/css2?family=Lexend:wght@400;700;900&family=JetBrains+Mono:wght@500&display=swap');
        
        body {
            font-family: 'Lexend', sans-serif;
            background-color: #020617;
            color: #ffffff;
            overflow: hidden;
            touch-action: none;
        }

        .ticker-container {
            height: 350px;
            display: flex;
            align-items: center;
            overflow: hidden;
            border-top: 1px solid rgba(0, 210, 255, 0.1);
            border-bottom: 1px solid rgba(0, 210, 255, 0.1);
            background: radial-gradient(circle, rgba(0, 210, 255, 0.05) 0%, rgba(0, 0, 0, 0) 80%);
            position: relative;
        }

        #ticker {
            white-space: nowrap;
            font-size: 5rem;
            font-weight: 800;
            padding-left: 100vw;
            will-change: transform;
            /* BIGGER SPACES: to combat visual crowding */
            letter-spacing: 0.15em; 
            word-spacing: 1.5em;
            transition: filter 0.3s ease;
        }

        /* Morpheme Colors */
        .m-1 { color: #00d2ff; text-shadow: 0 0 20px rgba(0, 210, 255, 0.3); } /* Stein Blue */
        .m-2 { color: #e2e8f0; } /* Neutral Signal */
        .m-sep { color: rgba(255, 0, 85, 0.3); font-weight: 400; margin: 0 -0.1em; } /* Visual separator */

        .focus-gate {
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
            width: 2px;
            height: 120%;
            background: #ff0055;
            box-shadow: 0 0 20px #ff0055;
            z-index: 10;
            opacity: 0.5;
        }

        #debug-panel {
            font-family: 'JetBrains Mono', monospace;
            font-size: 10px;
            color: rgba(0, 210, 255, 0.6);
            background: rgba(0, 0, 0, 0.4);
            padding: 12px;
            border-radius: 12px;
            border: 1px solid rgba(255,255,255,0.05);
        }

        input[type=range] {
            -webkit-appearance: none;
            width: 100%;
            background: transparent;
        }
        input[type=range]::-webkit-slider-runnable-track {
            width: 100%; height: 4px; background: rgba(0, 210, 255, 0.2); border-radius: 2px;
        }
        input[type=range]::-webkit-slider-thumb {
            height: 24px; width: 24px; border-radius: 50%; background: #00d2ff;
            cursor: pointer; -webkit-appearance: none; margin-top: -10px;
            box-shadow: 0 0 15px #00d2ff;
        }
    </style>
</head>
<body class="flex flex-col h-screen p-6">

    <!-- Header -->
    <div class="flex justify-between items-start mb-4">
        <div>
            <h1 class="text-2xl font-black tracking-tighter text-[#00d2ff]">GAZEBRIDGE</h1>
            <p class="text-[0.6rem] text-cyan-700 uppercase tracking-[0.3em] font-bold">Morpheme Decoding Mode</p>
        </div>
        <div id="status" class="px-4 py-2 rounded-full border border-gray-800 text-[10px] font-black uppercase tracking-widest text-gray-500">
            OFFLINE
        </div>
    </div>

    <!-- Top Controls: Slower Calibration -->
    <div class="mb-4 bg-white/5 p-4 rounded-2xl border border-white/5">
        <div class="flex justify-between items-center mb-2">
            <span class="text-[10px] uppercase font-bold text-cyan-500 tracking-widest">Flow Speed (Neural Pace)</span>
            <span id="speed-val" class="text-xs font-black text-white">1.0</span>
        </div>
        <input type="range" id="speed-slider" min="0.2" max="4" step="0.2" value="1.0">
    </div>

    <!-- Debug Info -->
    <div id="debug-panel" class="mb-4">
        > LINK: <span id="sensor-state" class="text-white">WAITING...</span><br>
        > FOCUS: <span id="stab-val" class="text-white">0</span>%<br>
        > LOCK TIMER: <span id="lock-timer" class="text-pink-500">0ms</span>
    </div>

    <!-- Ticker Section -->
    <div class="flex-grow flex items-center justify-center relative w-full">
        <div class="w-full ticker-container">
            <div class="focus-gate"></div>
            <div id="ticker">
                <!-- Humpty Dumpty with Morpheme Slicing -->
                <span class="m-1">HUMP</span><span class="m-sep">-</span><span class="m-2">TY</span> 
                <span class="m-1">DUMP</span><span class="m-sep">-</span><span class="m-2">TY</span> 
                SAT ON A WALL... 
                <span class="m-1">HUMP</span><span class="m-sep">-</span><span class="m-2">TY</span> 
                <span class="m-1">DUMP</span><span class="m-sep">-</span><span class="m-2">TY</span> 
                HAD A GREAT FALL... 
                ALL THE KING'S <span class="m-1">HORS</span><span class="m-sep">-</span><span class="m-2">ES</span> 
                AND ALL THE KING'S MEN... 
                <span class="m-1">COULD</span><span class="m-sep">-</span><span class="m-2">N'T</span> 
                PUT <span class="m-1">HUMP</span><span class="m-sep">-</span><span class="m-2">TY</span> 
                <span class="m-1">TO</span><span class="m-sep">-</span><span class="m-2">GETH</span><span class="m-sep">-</span><span class="m-1">ER</span> 
                <span class="m-1">A</span><span class="m-sep">-</span><span class="m-2">GAIN</span>...
            </div>
        </div>
    </div>

    <!-- Bottom Controls -->
    <div class="mt-8 flex flex-col items-center gap-6">
        <div class="w-full h-2 bg-gray-900 rounded-full overflow-hidden">
            <div id="stability-bar" class="h-full bg-[#00d2ff] w-0 transition-all duration-300"></div>
        </div>
        
        <button id="startBtn" class="w-full py-5 bg-white text-black font-black text-sm uppercase tracking-[0.3em] rounded-2xl active:scale-95 transition-transform">
            Connect Neural Link
        </button>

        <button id="simBtn" class="px-6 py-2 border border-pink-500/30 text-pink-500 text-[10px] uppercase font-bold tracking-widest rounded-full hover:bg-pink-500/10">
            Force Demo Mode
        </button>
    </div>

    <script>
        const ticker = document.getElementById('ticker');
        const stabilityBar = document.getElementById('stability-bar');
        const statusBadge = document.getElementById('status');
        const startBtn = document.getElementById('startBtn');
        const simBtn = document.getElementById('simBtn');
        const sensorStateDisplay = document.getElementById('sensor-state');
        const stabValDisplay = document.getElementById('stab-val');
        const timerDisplay = document.getElementById('lock-timer');
        const speedSlider = document.getElementById('speed-slider');
        const speedValDisplay = document.getElementById('speed-val');

        let isRunning = false;
        let isSimulating = false;
        let position = 0;
        let baseSpeed = 1.0; // SLOWER DEFAULT
        let stability = 0;
        let lastRotation = 0;
        let lockTime = 0; 
        const STEIN_THRESHOLD_MS = 800;

        speedSlider.addEventListener('input', (e) => {
            baseSpeed = parseFloat(e.target.value);
            speedValDisplay.textContent = baseSpeed.toFixed(1);
        });

        function update(timestamp) {
            if (isRunning) {
                if (stability > 85) {
                    lockTime += 16; 
                    timerDisplay.textContent = `${Math.min(lockTime, STEIN_THRESHOLD_MS)}ms`;
                } else {
                    lockTime = 0;
                    timerDisplay.textContent = `0ms`;
                }

                if (lockTime >= STEIN_THRESHOLD_MS) {
                    position -= baseSpeed;
                    statusBadge.innerText = "SIGNAL CLEAR";
                    statusBadge.style.borderColor = "#00ff41";
                    statusBadge.style.color = "#00ff41";
                    ticker.style.filter = "blur(0px)";
                } else {
                    statusBadge.innerText = "WAITING FOR STILLNESS";
                    statusBadge.style.borderColor = "#ff3131";
                    statusBadge.style.color = "#ff3131";
                    ticker.style.filter = `blur(${Math.max(2, (90 - stability) / 4)}px)`;
                }

                if (Math.abs(position) > ticker.offsetWidth) {
                    position = window.innerWidth;
                }
                ticker.style.transform = `translateX(${position}px)`;
            }
            requestAnimationFrame(update);
        }

        async function init() {
            startBtn.classList.add('hidden');
            if (typeof DeviceOrientationEvent !== 'undefined' && typeof DeviceOrientationEvent.requestPermission === 'function') {
                try {
                    const permission = await DeviceOrientationEvent.requestPermission();
                    if (permission === 'granted') startSensors();
                    else enableSimulation("PERMISSION DENIED");
                } catch (err) { enableSimulation("BROWSER BLOCK"); }
            } else { startSensors(); }
            setTimeout(() => { if (stability === 0 && !isSimulating) enableSimulation("NO SENSOR"); }, 1500);
        }

        function startSensors() {
            isRunning = true;
            sensorStateDisplay.textContent = "CONNECTED (GYRO)";
            window.addEventListener('deviceorientation', (event) => {
                if (isSimulating) return;
                let total = Math.abs(event.beta || 0) + Math.abs(event.gamma || 0);
                let delta = Math.abs(total - lastRotation);
                lastRotation = total;
                let currentStab = Math.max(0, 100 - (delta * 35));
                stability = (stability * 0.6) + (currentStab * 0.4);
                stabilityBar.style.width = `${stability}%`;
                stabValDisplay.textContent = Math.floor(stability);
            });
            requestAnimationFrame(update);
        }

        function enableSimulation(reason) {
            if (isSimulating) return;
            isSimulating = true;
            isRunning = true;
            sensorStateDisplay.textContent = reason + " -> EMULATED";
            setInterval(() => {
                let isStable = Math.random() > 0.4; 
                stability = isStable ? 98 : 15;
                stabilityBar.style.width = `${stability}%`;
                stabValDisplay.textContent = Math.floor(stability);
            }, 3000);
            requestAnimationFrame(update);
        }

        simBtn.addEventListener('click', () => enableSimulation("MANUAL"));
        startBtn.addEventListener('click', init);
        position = window.innerWidth;
    </script>
</body>
</html>
