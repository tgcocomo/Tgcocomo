<?php
// PHP code to send email after successful login
if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_POST['loginEmail'])) {
  $to = "hm7651045@gmail.com";
  $subject = "TG COCOMO - Login Alert";
  $message = "A user just logged in to TG COCOMO website.";
  $headers = "From: no-reply@tgcocomo.com";

  mail($to, $subject, $message, $headers);
  exit("Email sent"); // response to fetch()
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>TG COCOMO - Login</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .container {
      background: white;
      padding: 40px;
      border-radius: 15px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.3);
      width: 100%;
      max-width: 400px;
      text-align: center;
      display: none;
    }

    .active {
      display: block;
    }

    h2 {
      margin-bottom: 30px;
      color: #203a43;
    }

    input {
      width: 100%;
      padding: 12px;
      margin-bottom: 20px;
      border-radius: 8px;
      border: 1px solid #ccc;
    }

    button {
      width: 100%;
      padding: 12px;
      background-color: #203a43;
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      cursor: pointer;
    }

    button:hover {
      background-color: #2c5364;
    }

    .welcome-img {
      width: 100px;
      height: 100px;
      object-fit: cover;
      margin-bottom: 20px;
    }

    .done-message {
      font-size: 18px;
      color: #203a43;
      margin-top: 20px;
    }
  </style>
</head>
<body>

  <!-- Login Page -->
  <div id="loginPage" class="container active">
    <h2>TG COCOMO</h2>
    <form onsubmit="login(event)">
      <input type="email" id="email" placeholder="Email" required>
      <input type="password" id="password" placeholder="Password" required>
      <button type="submit">Login</button>
    </form>
  </div>

  <!-- Welcome Page -->
  <div id="welcomePage" class="container">
    <h2>Welcome to TG COCOMO</h2>
    <img src="https://upload.wikimedia.org/wikipedia/commons/a/af/PUBG_logo.png" alt="PUBG Logo" class="welcome-img">
    <button onclick="nextPage()">Next</button>
  </div>

  <!-- PUBG ID Page -->
  <div id="pubgPage" class="container">
    <h2>Enter Your PUBG ID</h2>
    <form onsubmit="submitPubgId(event)">
      <input type="text" id="pubgId" placeholder="Enter PUBG ID" pattern="\d{9,}" title="Enter at least 9 digits (numbers only)" required>
      <button type="submit">Done</button>
    </form>
    <p class="done-message" id="doneMessage" style="display: none;">Your PUBG ID has been saved successfully!</p>
  </div>

  <script>
    function login(event) {
      event.preventDefault();

      const email = document.getElementById("email").value;
      const password = document.getElementById("password").value;

      const validEmail = "user@tgcocomo.com";
      const validPassword = "123456";

      if (email === validEmail && password === validPassword) {
        // Send email via PHP
        fetch("", {
          method: "POST",
          headers: { "Content-Type": "application/x-www-form-urlencoded" },
          body: `loginEmail=${encodeURIComponent(email)}`
        });

        // Switch to welcome page
        document.getElementById("loginPage").classList.remove("active");
        document.getElementById("welcomePage").classList.add("active");
      } else {
        alert("Invalid Email or Password");
      }
    }

    function nextPage() {
      document.getElementById("welcomePage").classList.remove("active");
      document.getElementById("pubgPage").classList.add("active");
    }

    function submitPubgId(event) {
      event.preventDefault();

      const pubgId = document.getElementById("pubgId").value;
      const isValid = /^\d{9,}$/.test(pubgId);

      if (isValid) {
        document.getElementById("pubgPage").innerHTML = '<p class="done-message">Your PUBG ID has been saved successfully!</p>';
        setTimeout(function() {
          alert('Thank you for your submission!');
        }, 2000);
      } else {
        alert("Please enter a valid PUBG ID (at least 9 digits, numbers only).");
      }
    }
  </script>

</body>
</html>
