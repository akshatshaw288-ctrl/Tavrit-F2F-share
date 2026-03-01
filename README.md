<div class="app">

  <!-- PAGE 1 -->
  <div id="page1" class="page">
    <h1 class="title">Tavrit F2F Share</h1>
    <p class="subtitle">Fast • Secure • Browser Based</p>

    <input id="userName" placeholder="ENTER YOUR NAME" />
    <button class="primary" onclick="goNext()">NEXT</button>
  </div>

  <!-- PAGE 2 -->
  <div id="page2" class="page hidden">

    <div id="avatar" class="avatar"></div>

    <div class="codeBox">
      <span>Your Code</span>
      <div id="myCode" class="code">ABCDE</div>
    </div>

    <input id="friendCode" maxlength="5" placeholder="ENTER FRIEND CODE" />
    <p id="status" class="status">Waiting for connection...</p>

    <input type="file" id="fileInput" multiple />
    <button class="primary" onclick="sendFiles()">SEND FILES</button>

    <!-- Progress -->
    <div id="progressBox" class="progress hidden">
      <progress id="progressBar" value="0" max="100"></progress>
      <span>Sending...</span>
    </div>

    <div id="successMsg" class="success hidden">
      ✔ Files Sent Successfully
    </div>

    <!-- VOICE -->
    <button id="voiceBtn" class="primary hidden" onclick="startVoice()">
      🎙️ START VOICE
    </button>
    <button id="endVoiceBtn" class="primary danger hidden" onclick="endVoice()">
      ❌ END CALL
    </button>

  </div>
</div>


*{
  box-sizing:border-box;
  font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto;
}

body{
  margin:0;
  height:100vh;
  display:flex;
  align-items:center;
  justify-content:center;
  background:linear-gradient(135deg,#0f172a,#020617);
  color:#fff;
}

.app{
  width:100%;
  max-width:360px;
  background:#020617;
  border-radius:18px;
  padding:24px;
  box-shadow:0 20px 60px rgba(0,0,0,.6);
}

.page{text-align:center}
.hidden{display:none}

.title{font-size:26px;margin-bottom:4px}
.subtitle{font-size:13px;opacity:.6;margin-bottom:20px}

input{
  width:100%;
  padding:14px;
  margin:10px 0;
  border-radius:10px;
  border:none;
  outline:none;
  font-size:14px;
  text-transform:uppercase;
}

.primary{
  width:100%;
  padding:14px;
  border:none;
  border-radius:12px;
  background:#2563eb;
  color:#fff;
  font-size:15px;
  font-weight:600;
  cursor:pointer;
  margin-top:8px;
}

.primary:active{transform:scale(.98)}
.danger{background:#dc2626}

.avatar{
  width:70px;
  height:70px;
  background:#22c55e;
  border-radius:50%;
  margin:0 auto 14px;
  display:flex;
  align-items:center;
  justify-content:center;
  font-size:30px;
  font-weight:700;
}

.codeBox span{font-size:12px;opacity:.6}
.code{font-size:24px;letter-spacing:4px;margin-top:4px}
.status{font-size:13px;opacity:.7;margin:8px 0}

.progress{margin-top:12px}
progress{width:100%;height:14px}

.success{
  margin-top:10px;
  color:#22c55e;
  font-weight:600;
}






let connected = false;

let localStream = null;

// Page 1 → Page 2
function goNext(){
  const name = userName.value.trim();
  if(!name){
    alert("Enter your name");
    return;
  }

  page1.classList.add("hidden");
  page2.classList.remove("hidden");

  avatar.innerText = name[0].toUpperCase();

  const code = Math.random().toString(36).substring(2,7).toUpperCase();
  myCode.innerText = code;
}

// Fake connect (demo)
friendCode.addEventListener("input", e=>{
  if(e.target.value.length === 5){
    status.innerText = "Connected";
    connected = true;
    voiceBtn.classList.remove("hidden");
  }
});

// Multiple file send (demo)
function sendFiles(){
  if(!connected){
    alert("Not connected");
    return;
  }

  const files = fileInput.files;
  if(files.length === 0){
    alert("Select files");
    return;
  }

  if(files.length > 7){
    alert("Max 7 files allowed");
    return;
  }

  progressBox.classList.remove("hidden");
  successMsg.classList.add("hidden");
  progressBar.value = 0;

  let p = 0;
  const timer = setInterval(()=>{
    p += 10;
    progressBar.value = p;

    if(p >= 100){
      clearInterval(timer);
      progressBox.classList.add("hidden");
      successMsg.classList.remove("hidden");
    }
  },200);
}

// Voice (local mic demo)
async function startVoice(){
  voiceBtn.classList.add("hidden");
  endVoiceBtn.classList.remove("hidden");

  localStream = await navigator.mediaDevices.getUserMedia({audio:true});
  alert("Microphone ON (demo)");
}

function endVoice(){
  if(localStream){
    localStream.getTracks().forEach(t=>t.stop());
  }
  endVoiceBtn.classList.add("hidden");
  voiceBtn.classList.remove("hidden");
  alert("Voice stopped");
}
