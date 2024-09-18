# dont<span id="task-text"></span><span id="text"></span> 😌

## Hey <span id="name"></span> 👋

Quiet your mind.

Let go of the constant urge to do.

Just stop, and **don’t**.

## You’ve doing great for <span id="counter">0</span> seconds ⏳

This timer tracks the time you've chosen not to act. No chasing goals, no distractions, no tasks calling for attention. It's a space where stopping is the point—away from the endless stream of things to do.

<br>**Breathe** <span id="breathing-box"></span><span id="breathing-state"></span>

### You were most still for <span id="most-dont-time">0</span> seconds ⏱️

<script>
    let idleTime = 0, mostIdleTime = 0, idleInterval;
    let exclamations = 0, maxExclamations = 4, mouseTimeout;

    const text = document.getElementById('text');
    const counterElem = document.getElementById("counter");
    const maxDontTimeElem = document.getElementById("most-dont-time");
    const nameElem = document.getElementById('name');
    const taskTextElem = document.getElementById('task-text');

    let breatheLines = 0, breatheState = 0;
    const maxBreatheLines = 16;
    const breathingBox = document.getElementById('breathing-box');
    const breathingState = document.getElementById('breathing-state');
    const breathingLabels = ["Inhale", "Hold", "Exhale"];
    let breathingInterval;

    function getQueryParameter(name) {
        const urlParams = new URLSearchParams(window.location.search);
        return urlParams.get(name);
    }

    function updateMaxTime() {
        if (idleTime > mostIdleTime) {
            mostIdleTime = idleTime;
            maxDontTimeElem.textContent = mostIdleTime;
        }
    }

    function resetCounter() {
        updateMaxTime();
        idleTime = 0;
        counterElem.textContent = idleTime;
    }

    function updateText() {
        text.textContent = `${'!'.repeat(exclamations)}`;
    }

    const scheduleRemoval = () => {
        if (exclamations > 0) {
            setTimeout(() => {
                exclamations--;
                updateText();
                if (exclamations > 0) scheduleRemoval();
            }, 2000);
        }
    };

    function startIdleTimer() {
        idleInterval = setInterval(() => {
            idleTime++;
            counterElem.textContent = idleTime;
            updateMaxTime();
        }, 1000);
    }

    const updateBreathingBox = () => {
        const boxContent = "+".repeat(breatheLines) + "-".repeat(maxBreatheLines - breatheLines);
        breathingBox.textContent = `[${boxContent}] ${breathingLabels[breatheState]}`;
    };

    const startInhale = () => {
        breatheState = 0;
        breatheLines = 0;
        breathingInterval = setInterval(() => {
            if (breatheLines < maxBreatheLines) {
                breatheLines++;
                updateBreathingBox();
            } else {
                clearInterval(breathingInterval);
                startHold();
            }
        }, 250);
    };

    const startHold = () => {
        breatheState = 1;
        let isBold = false, holdTime = 0;
        updateBreathingBox();
        breathingInterval = setInterval(() => {
            breathingBox.style.fontWeight = isBold ? 'bold' : 'normal';
            isBold = !isBold;
            holdTime++;
            if (holdTime >= 8) {
                clearInterval(breathingInterval);
                startExhale();
            }
        }, 500);
    };

    const startExhale = () => {
        breatheState = 2;
        breathingInterval = setInterval(() => {
            if (breatheLines > 0) {
                breatheLines--;
                updateBreathingBox();
            } else {
                clearInterval(breathingInterval);
                startInhale();
            }
        }, 400);
    };

    document.onclick = () => {
        resetCounter();
        if (exclamations < maxExclamations) {
            exclamations++;
            updateText();
        }
    };

    document.onmousemove = () => {
        clearTimeout(mouseTimeout);
        resetCounter();
        if (exclamations === 0) {
            exclamations++;
            updateText();
        }
        mouseTimeout = setTimeout(() => {
            exclamations--;
            updateText();
            if (exclamations > 0) scheduleRemoval();
        }, 2000);
    };

    window.onload = function() {
        startIdleTimer();
        startInhale();

        // Get and apply query parameters
        const nameParam = getQueryParameter('name');
        const taskParam = getQueryParameter('task');

        if (nameParam) {
            nameElem.textContent = nameParam;
        } else {
            nameElem.textContent = "there";
        }

        if (taskParam) {
            taskTextElem.textContent = ` ${taskParam}`;
        } else {
            taskTextElem.textContent = "";
        }
    };

</script>
