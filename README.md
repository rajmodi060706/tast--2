<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Stopwatch App</title>

<style>
    body {
        font-family: Arial, sans-serif;
        text-align: center;
        background: #f3f3f3;
        margin: 0;
        padding: 50px;
    }

    h1 {
        margin-bottom: 20px;
    }

    .stopwatch {
        font-size: 50px;
        background: white;
        padding: 20px 40px;
        border-radius: 10px;
        display: inline-block;
        box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        margin-bottom: 30px;
    }

    .buttons button {
        padding: 12px 20px;
        margin: 10px;
        font-size: 18px;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        transition: 0.3s;
    }

    #startBtn { background: #4caf50; color: white; }
    #pauseBtn { background: #ff9800; color: white; }
    #resetBtn { background: #f44336; color: white; }
    #lapBtn   { background: #2196f3; color: white; }

    button:hover {
        opacity: 0.8;
    }

    .laps {
        margin-top: 30px;
        text-align: left;
        max-width: 400px;
        margin-left: auto;
        margin-right: auto;
    }

    .lap-item {
        background: #fff;
        padding: 10px;
        margin: 5px 0;
        border-radius: 6px;
        box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }
</style>

</head>
<body>

<h1>Stopwatch Application</h1>

<div class="stopwatch" id="display">00:00:00</div>

<div class="buttons">
    <button id="startBtn">Start</button>
    <button id="pauseBtn">Pause</button>
    <button id="resetBtn">Reset</button>
    <button id="lapBtn">Lap</button>
</div>

<h2>Laps</h2>
<div class="laps" id="lapsList"></div>

<script>
    let startTime = 0;
    let elapsedTime = 0;
    let interval;

    const display = document.getElementById("display");
    const lapsList = document.getElementById("lapsList");

    function formatTime(ms) {
        let totalSeconds = Math.floor(ms / 1000);
        let hours = Math.floor(totalSeconds / 3600);
        let minutes = Math.floor((totalSeconds % 3600) / 60);
        let seconds = totalSeconds % 60;

        return (
            (hours < 10 ? "0" : "") + hours + ":" +
            (minutes < 10 ? "0" : "") + minutes + ":" +
            (seconds < 10 ? "0" : "") + seconds
        );
    }

    document.getElementById("startBtn").addEventListener("click", function () {
        if (!interval) {
            startTime = Date.now() - elapsedTime;
            interval = setInterval(function () {
                elapsedTime = Date.now() - startTime;
                display.textContent = formatTime(elapsedTime);
            }, 100);
        }
    });

    document.getElementById("pauseBtn").addEventListener("click", function () {
        clearInterval(interval);
        interval = null;
    });

    document.getElementById("resetBtn").addEventListener("click", function () {
        clearInterval(interval);
        interval = null;
        elapsedTime = 0;
        display.textContent = "00:00:00";
        lapsList.innerHTML = "";
    });

    document.getElementById("lapBtn").addEventListener("click", function () {
        if (elapsedTime > 0) {
            const lapItem = document.createElement("div");
            lapItem.className = "lap-item";
            lapItem.textContent = "Lap: " + formatTime(elapsedTime);
            lapsList.appendChild(lapItem);
        }
    });
</script>

</body>
</html>
