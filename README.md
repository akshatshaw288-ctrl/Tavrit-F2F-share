<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Tavrit F2F Share</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="style.css">
</head>

<body>

<div class="page active" id="page1">
  <h1>Tavrit F2F Share</h1>
  <input type="text" id="username" placeholder="Enter your name">
  <button onclick="goNext()">Next</button>
</div>

<div class="page" id="page2">
  <div class="top">
    <div class="logo" id="logo"></div>
    <h2 id="welcome"></h2>
  </div>

  <div class="codes">
    <p>Your Code</p>
    <div id="myCode" class="code-box"></div>

    <p>Enter Friend Code</p>
    <input type="text" id="friendCode" maxlength="5" oninput="connectCheck()">
    <p id="connectMsg"></p>
  </div>

  <div class="files">
    <input type="file" multiple id="files" max="7">
    <button onclick="sendFiles()">Send Files</button>
  </div>

  <div id="progress"></div>
</div>

<script src="app.js"></script>
</body>
</html>
