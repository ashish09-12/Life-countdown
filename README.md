# Life-countdown
A website showing remaining life time
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Life Countdown Clock</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #121212;
      color: #ffffff;
      text-align: center;
      padding: 50px;
    }
    input, button {
      padding: 10px;
      margin: 10px;
      font-size: 18px;
      border-radius: 8px;
      border: none;
    }
    button {
      background-color: #6200ea;
      color: white;
      cursor: pointer;
    }
    #countdown {
      margin-top: 30px;
      font-size: 24px;
    }
  </style>
</head>
<body>

  <h1>Life Countdown Clock</h1>

  <p>Enter your details:</p>

  <input type="number" id="currentAge" placeholder="Your Current Age">
  <input type="number" id="expectedAge" placeholder="Expected Lifespan (Years)">
  <br>
  <button onclick="startCountdown()">Start Countdown</button>

  <div id="countdown"></div>

  <script>
    let interval;

    function startCountdown() {
      clearInterval(interval);
      
      const currentAge = parseInt(document.getElementById('currentAge').value);
      const expectedAge = parseInt(document.getElementById('expectedAge').value);

      if (isNaN(currentAge) || isNaN(expectedAge) || currentAge >= expectedAge) {
        alert('Please enter valid ages.');
        return;
      }

      const now = new Date();
      const yearsLeft = expectedAge - currentAge;
      const endDate = new Date(now.getFullYear() + yearsLeft, now.getMonth(), now.getDate(), now.getHours(), now.getMinutes(), now.getSeconds());

      interval = setInterval(() => {
        const currentTime = new Date();
        const difference = endDate - currentTime;

        if (difference <= 0) {
          document.getElementById('countdown').innerHTML = "Time's up!";
          clearInterval(interval);
          return;
        }

        const seconds = Math.floor((difference / 1000) % 60);
        const minutes = Math.floor((difference / 1000 / 60) % 60);
        const hours = Math.floor((difference / (1000 * 60 * 60)) % 24);
        const days = Math.floor((difference / (1000 * 60 * 60 * 24)) % 365);
        const years = Math.floor(difference / (1000 * 60 * 60 * 24 * 365));

        document.getElementById('countdown').innerHTML =
          `${years} Years, ${days} Days, ${hours} Hours, ${minutes} Minutes, ${seconds} Seconds Left`;
      }, 1000);
    }
  </script>

</body>
</html>
