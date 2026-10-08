<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">

<title>Samjhao AI</title>

<style>
*{
  box-sizing:border-box;
  margin:0;
  padding:0;
  font-family:Arial,sans-serif;
}

body{
  background:#f5f7ff;
  color:#111827;
  height:100vh;
}

.app{
  max-width:600px;
  height:100vh;
  margin:auto;
  display:flex;
  flex-direction:column;
  background:#fff;
}

/* HEADER */

header{
  padding:18px;
  display:flex;
  justify-content:space-between;
  align-items:center;
  border-bottom:1px solid #eee;
}

.logo{
  font-size:25px;
  font-weight:800;
}

.logo span{
  color:#635bff;
}

.menu{
  border:0;
  background:#f1f2f6;
  padding:10px;
  border-radius:12px;
  font-size:18px;
}

/* HOME */

.home{
  padding:22px;
  flex:1;
  overflow:auto;
}

.greeting{
  margin-top:25px;
}

.greeting h1{
  font-size:28px;
}

.greeting p{
  margin-top:8px;
  color:#6b7280;
}

/* MODE */

.modes{
  display:flex;
  gap:8px;
  margin:22px 0;
}

.mode{
  flex:1;
  padding:11px;
  border:0;
  border-radius:12px;
  background:#f1f2f6;
}

.mode.active{
  background:#635bff;
  color:white;
}

/* SUGGESTIONS */

.suggestions{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:12px;
}

.suggestion{
  padding:18px;
  background:#f8f8ff;
  border:1px solid #eee;
  border-radius:17px;
  text-align:left;
}

/* CHAT */

.chat{
  display:none;
  flex:1;
  overflow:auto;
  padding:18px;
}

.message{
  max-width:85%;
  padding:13px 15px;
  margin-bottom:12px;
  border-radius:17px;
  line-height:1.5;
}

.user{
  margin-left:auto;
  background:#635bff;
  color:white;
  border-bottom-right-radius:5px;
}

.ai{
  background:#f1f2f6;
  border-bottom-left-radius:5px;
}

/* INPUT */

.input-area{
  padding:12px;
  border-top:1px solid #eee;
}

.input-box{
  display:flex;
  align-items:center;
  gap:7px;
  background:#f5f6fa;
  padding:7px;
  border-radius:18px;
}

textarea{
  flex:1;
  border:0;
  outline:0;
  background:transparent;
  resize:none;
  padding:10px;
  font-size:15px;
}

.icon{
  border:0;
  background:white;
  width:42px;
  height:42px;
  border-radius:13px;
  font-size:18px;
}

.send{
  background:#635bff;
  color:white;
}

/* HISTORY */

.history{
  display:none;
  padding:20px;
  flex:1;
  overflow:auto;
}

.history-item{
  padding:15px;
  background:#f5f6fa;
  border-radius:14px;
  margin-bottom:10px;
}

/* SETTINGS */

.settings{
  display:none;
  padding:20px;
  flex:1;
}

.setting{
  padding:17px;
  background:#f5f6fa;
  border-radius:15px;
  margin-bottom:12px;
}

.dark{
  background:#111827;
  color:white;
}

.dark .app{
  background:#111827;
}

.dark .input-box,
.dark .setting,
.dark .history-item,
.dark .ai,
.dark .suggestion{
  background:#1f2937;
  color:white;
}
</style>
</head>

<body>

<div class="app">

<header>
  <div class="logo">Sam<span>jhao</span> 🧠</div>

  <button class="menu" onclick="openSettings()">
    ⚙️
  </button>
</header>


<!-- HOME -->

<section class="home" id="home">

  <div class="greeting">

    <h1>Heyy 👋</h1>

    <p>
      Kya samajhna hai aaj?
    </p>

  </div>


  <div class="modes">

    <button class="mode active">
      🌱 Basic
    </button>

    <button class="mode">
      📚 JEE
    </button>

    <button class="mode">
      🚀 Advanced
    </button>

  </div>


  <div class="suggestions">

    <button class="suggestion"
      onclick="ask('Newton ka first law simple language mein samjhao')">

      ⚡ Physics<br>
      Newton's Laws

    </button>


    <button class="suggestion"
      onclick="ask('Quadratic equation basic se samjhao')">

      📐 Maths<br>
      Quadratic Equation

    </button>


    <button class="suggestion"
      onclick="ask('Chemical bonding samjhao')">

      🧪 Chemistry<br>
      Chemical Bonding

    </button>


    <button class="suggestion"
      onclick="ask('Photosynthesis samjhao')">

      🌱 Biology<br>
      Photosynthesis

    </button>

  </div>

</section>


<!-- CHAT -->

<section class="chat" id="chat"></section>


<!-- HISTORY -->

<section class="history" id="history">

  <h2>📚 History</h2>

  <br>

  <div id="historyList"></div>

</section>


<!-- SETTINGS -->

<section class="settings" id="settings">

  <h2>⚙️ Settings</h2>

  <br>

  <div class="setting">
    👤 Profile
    <br>
    <small>Samjhao user</small>
  </div>

  <div class="setting"
       onclick="toggleDark()">

    🌙 Dark Mode

  </div>

  <div class="setting"
       onclick="clearHistory()">

    🗑️ Clear History

  </div>

  <div class="setting">

    ℹ️ About Samjhao
    <br>
    <small>Learn anything from basic to advanced.</small>

  </div>

</section>


<!-- INPUT -->

<div class="input-area">

  <div class="input-box">

    <button class="icon"
      onclick="startVoice()">
      🎤
    </button>


    <textarea
      id="input"
      rows="1"
      placeholder="Kuch bhi poochho...">
    </textarea>


    <button class="icon"
      onclick="chooseImage()">
      📷
    </button>


    <button class="icon send"
      onclick="sendMessage()">
      ➤
    </button>

  </div>

</div>


<input
  type="file"
  id="image"
  accept="image/*"
  style="display:none">

</div>


<script>

/* -------------------------
   NAVIGATION
------------------------- */

function showOnly(id){

  document.getElementById("home").style.display="none";

  document.getElementById("chat").style.display="none";

  document.getElementById("history").style.display="none";

  document.getElementById("settings").style.display="none";

  document.getElementById(id).style.display="block";
}


function openSettings(){

  showOnly("settings");

}


/* -------------------------
   ASK
------------------------- */

function ask(text){

  document.getElementById("input").value=text;

  sendMessage();

}


/* -------------------------
   SEND MESSAGE
------------------------- */

function sendMessage(){

  let input=document.getElementById("input");

  let text=input.value.trim();

  if(!text)return;


  showOnly("chat");


  addMessage(text,"user");


  input.value="";


  saveHistory(text);


  setTimeout(()=>{

    let answer=generateDemoAnswer(text);

    addMessage(answer,"ai");

  },700);

}


/* -------------------------
   MESSAGE
------------------------- */

function addMessage(text,type){

  let chat=document.getElementById("chat");

  let div=document.createElement("div");

  div.className="message "+type;

  div.innerHTML=text;

  chat.appendChild(div);

  chat.scrollTop=chat.scrollHeight;

}


/* -------------------------
   DEMO AI
------------------------- */

function generateDemoAnswer(question){

  let q=question.toLowerCase();


  if(q.includes("newton")){

    return `
    <b>Newton's First Law</b><br><br>

    Kisi object par net external force zero ho,
    to object apni current state ko maintain karta hai.

    <br><br>

    👉 Agar object rest mein hai → rest mein rahega.<br>
    👉 Agar motion mein hai → same velocity se chalega.

    <br><br>

    <b>Example:</b><br>
    Bus suddenly brake lagati hai to body aage
    ki taraf jhukti hai. Ye inertia ki wajah se hota hai.
    `;

  }


  if(q.includes("quadratic")){

    return `
    <b>Quadratic Equation</b><br><br>

    General form:

    <br><br>

    ax² + bx + c = 0

    <br><br>

    Jahan a ≠ 0.

    <br><br>

    Iske roots nikalne ke liye:

    <br><br>

    x = (-b ± √(b² - 4ac)) / 2a
    `;

  }


  return `
  <b>Samjhao AI</b> 🧠<br><br>

  Tumne poocha:<br>
  <b>${question}</b>

  <br><br>

  Iska detailed AI explanation agle version
  mein connect kiya jayega.

  <br><br>

  Main tumhe concept ko:
  <br>1️⃣ Basic
  <br>2️⃣ Example
  <br>3️⃣ Diagram
  <br>4️⃣ JEE level
  <br>5️⃣ Advanced
  <br>
  mein samjha sakta hoon.
  `;

}


/* -------------------------
   VOICE
------------------------- */

function startVoice(){

  if(!("webkitSpeechRecognition" in window)){

    alert("Voice recognition is not supported.");

    return;

  }


  let recognition=
    new webkitSpeechRecognition();


  recognition.lang="hi-IN";

  recognition.start();


  recognition.onresult=function(event){

    document.getElementById("input").value=
      event.results[0][0].transcript;

  };

}


/* -------------------------
   IMAGE
------------------------- */

function chooseImage(){

  document.getElementById("image").click();

}


/* -------------------------
   HISTORY
------------------------- */

function saveHistory(text){

  let history=
    JSON.parse(localStorage.getItem("samjhaoHistory")) || [];


  history.unshift(text);

  history=history.slice(0,20);


  localStorage.setItem(
    "samjhaoHistory",
    JSON.stringify(history)
  );

}


function showHistory(){

  let history=
    JSON.parse(localStorage.getItem("samjhaoHistory")) || [];


  let list=
    document.getElementById("historyList");


  list.innerHTML="";


  history.forEach(item=>{

    let div=document.createElement("div");

    div.className="history-item";

    div.innerHTML="🧠 "+item;

    list.appendChild(div);

  });

}


/* -------------------------
   CLEAR HISTORY
------------------------- */

function clearHistory(){

  localStorage.removeItem("samjhaoHistory");

  showHistory();

  alert("History clear ho gayi.");

}


/* -------------------------
   DARK MODE
------------------------- */

function toggleDark(){

  document.body.classList.toggle("dark");

}


/* INITIAL */

showHistory();

</script>

</body>
</html>
