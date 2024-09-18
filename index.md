<h1 id="text">dont</h1>

<script>
    let exclamations = 0, max = 4, mouseTimeout;
    const text = document.getElementById('text');

    // Function to update the displayed text with the correct number of exclamations
    const updateText = () => text.textContent = `don't${'!'.repeat(exclamations)}`;

    // Function to remove one exclamation mark after a delay (used for both click and mouse movement)
    const scheduleRemoval = () => {
        if (exclamations > 0) {
            setTimeout(() => {
                exclamations--;
                updateText();
                if (exclamations > 0) scheduleRemoval(); // Recursively call to remove all exclamations
            }, 2000);
        }
    };

    // Handle click anywhere on the page
    document.onclick = () => {
        if (exclamations < max) {
            exclamations++;
            updateText();
        }
    };

    // Handle mouse movement and add exclamation mark if none are present
    document.onmousemove = () => {
        clearTimeout(mouseTimeout); // Clear any previous mouse inactivity timeout
        if (exclamations === 0) {
            exclamations++;
            updateText();
        }
        // Set a timeout to remove the exclamation after 4 seconds of inactivity
        mouseTimeout = setTimeout(() => {
            exclamations--;
            updateText();
            if (exclamations > 0) scheduleRemoval(); // Start the removal process if first exclamation
        }, 2000);
    };
</script>
