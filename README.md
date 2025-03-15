<!DOCTYPE html>
<html>

<head>
    <title>Stopwatch</title>
    <style>
        body {
            font-family: sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            /*  Set height to full viewport for Notion embed */
            margin: 0;
            background-color: #000000;
            /* Light background */
        }

        #display {
            font-size: 6em;
            margin-bottom: 20px;
            padding: 10px;
            border: 2px solid #c20000;
            border-radius: 5px;
            background-color: #ac9191;
            /* White background */
        }

        .controls {
            display: flex;
            gap: 10px;
        }

        button {
            padding: 10px 20px;
            font-size: 1em;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background-color: #4CAF50;
            /* Green */
            color: rgb(161, 0, 0);
        }

        button:hover {
            opacity: 0.8;
        }

        button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
    </style>
</head>

<body>

    <div id="display">00:00:00</div>

    <div class="controls">
        <button id="startStopBtn">Start</button>
        <button id="resetBtn">Reset</button>
    </div>

    <script>
        let timerInterval;
        let startTime;
        let elapsedTime = 0;
        let isRunning = false;

        const display = document.getElementById('display');
        const startStopBtn = document.getElementById('startStopBtn');
        const resetBtn = document.getElementById('resetBtn');

        function timeToString(time) {
            let diffInHrs = time / 3600000;
            let hh = Math.floor(diffInHrs);

            let diffInMin = (diffInHrs - hh) * 60;
            let mm = Math.floor(diffInMin);

            let diffInSec = (diffInMin - mm) * 60;
            let ss = Math.floor(diffInSec);

            let formattedHH = hh.toString().padStart(2, '0');
            let formattedMM = mm.toString().padStart(2, '0');
            let formattedSS = ss.toString().padStart(2, '0');

            return `${formattedHH}:${formattedMM}:${formattedSS}`;
        }


        function updateDisplay() {
            display.innerText = timeToString(elapsedTime);
        }

        function startStop() {
            if (!isRunning) {
                startTime = Date.now() - elapsedTime;
                timerInterval = setInterval(function printTime() {
                    elapsedTime = Date.now() - startTime;
                    updateDisplay();
                }, 10); // Update every 10 milliseconds for smoother timing.
                startStopBtn.innerText = 'Stop';
                isRunning = true;
            } else {
                clearInterval(timerInterval);
                startStopBtn.innerText = 'Start';
                isRunning = false;
            }
        }

        function reset() {
            clearInterval(timerInterval);
            elapsedTime = 0;
            updateDisplay();
            startStopBtn.innerText = 'Start';
            isRunning = false;
        }


        startStopBtn.addEventListener('click', startStop);
        resetBtn.addEventListener('click', reset);
    </script>

</body>

</html>
