# Assignment-05
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Debounce and Throttle Demo</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      height: 2000px; /* Add height to allow scrolling */
      background-color: #f0f4f8;
    }
    h1 {
      margin-bottom: 30px;
    }
    .section {
      margin-bottom: 50px;
    }
    .box {
      padding: 10px;
      margin-top: 10px;
      border: 1px solid #ccc;
      background-color: #fff;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    }
    input {
      padding: 8px;
      width: 300px;
      font-size: 16px;
    }
  </style>
</head>
<body>

  <h1>Debounce and Throttle Example</h1>

  <!-- Debounce Section -->
  <div class="section">
    <h2>Debounce Example</h2>
    <input type="text" id="debounceInput" placeholder="Start typing..." />
    <div class="box" id="debounceResult">Debounced result will appear here.</div>
  </div>

  <!-- Throttle Section -->
  <div class="section">
    <h2>Throttle Example</h2>
    <div class="box" id="throttleResult">Scroll down to see throttled scroll position.</div>
  </div>

  <script>
    // Debounce Function
    function debounce(func, delay) {
      let timeoutId;
      return function (...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => {
          func.apply(this, args);
        }, delay);
      };
    }

    // Throttle Function
    function throttle(func, interval) {
      let lastTime = 0;
      return function (...args) {
        const now = Date.now();
        if (now - lastTime >= interval) {
          lastTime = now;
          func.apply(this, args);
        }
      };
    }

    // Debounce Implementation
    const debounceInput = document.getElementById('debounceInput');
    const debounceResult = document.getElementById('debounceResult');

    const showDebounceResult = debounce(function(event) {
      debounceResult.textContent = 'Debounced Input: ' + event.target.value;
    }, 500);

    debounceInput.addEventListener('input', showDebounceResult);

    // Throttle Implementation
    const throttleResult = document.getElementById('throttleResult');

    const showThrottleResult = throttle(function() {
      throttleResult.textContent = 'Scroll Y Position (throttled): ' + window.scrollY;
    }, 500);

    window.addEventListener('scroll', showThrottleResult);
  </script>

</body>
</html>
