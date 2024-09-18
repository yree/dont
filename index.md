# Dont

Hey there,

Quiet your mind.<br>
Let go of the constant urge to do.<br>
Just stop, and don’t.

## You’ve been idle for **<span id="counter">0</span> seconds**

This timer tracks the time you've chosen not to act. No chasing goals, no distractions, no tasks calling for attention. It's a space where stopping is the point—away from the endless stream of things to do.

Stay as long as you like or move on. There’s no goal here, just the simple act of stopping. Sometimes, the most meaningful choice is to stop everything and simply let yourself be still.

<div class="stats">
    <p>Most Don't Time: <span id="most-dont-time">0</span> seconds</p>
    <p>Last Don't Time: <span id="last-dont-time">0</span> seconds</p>
</div>

<div class="button-group">
    <button onclick="resetStats()">Reset Stats</button>
</div>

<div id="message" class="message"></div>

<script>
    let idleTime = 0;
    let lastIdleTime = 0;
    let mostIdleTime = 0;
    let idleInterval;

    function resetCounter() {
        lastIdleTime = idleTime;
        document.getElementById("last-dont-time").textContent = lastIdleTime;

        if (lastIdleTime > mostIdleTime) {
            mostIdleTime = lastIdleTime;
            document.getElementById("most-dont-time").textContent = mostIdleTime;
        }

        idleTime = 0;
        document.getElementById("counter").textContent = idleTime;
    }

    function startIdleTimer() {
        idleInterval = setInterval(() => {
            idleTime++;
            document.getElementById("counter").textContent = idleTime;
        }, 1000);
    }

    function resetStats() {
        idleTime = 0;
        lastIdleTime = 0;
        mostIdleTime = 0;
        document.getElementById("counter").textContent = 0;
        document.getElementById("last-dont-time").textContent = 0;
        document.getElementById("most-dont-time").textContent = 0;
        document.getElementById("message").textContent = '';
    }

    function displayMessage(message) {
        document.getElementById("message").textContent = message;
    }

    document.addEventListener("mousemove", function() {
        resetCounter();
        displayMessage("don't");
    });

    document.addEventListener("click", function() {
        resetCounter();
        displayMessage("don't click");
    });

    window.onload = function() {
        startIdleTimer();
    };
</script>
