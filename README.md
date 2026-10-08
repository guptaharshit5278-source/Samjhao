<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Samjhao</title>

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial,sans-serif;
}

body{
    background:linear-gradient(135deg,#eef2ff,#f8fafc);
    min-height:100vh;
    color:#111827;
}

.header{
    padding:25px 20px 15px;
}

.logo{
    font-size:30px;
    font-weight:800;
}

.logo span{
    color:#6366f1;
}

.subtitle{
    color:#6b7280;
    margin-top:6px;
}

.container{
    padding:20px;
    max-width:600px;
    margin:auto;
}

.card{
    background:white;
    border-radius:24px;
    padding:20px;
    box-shadow:0 10px 30px rgba(0,0,0,.08);
}

textarea{
    width:100%;
    height:130px;
    border:2px solid #e5e7eb;
    border-radius:18px;
    padding:15px;
    font-size:16px;
    resize:none;
    outline:none;
}

textarea:focus{
    border-color:#6366f1;
}

.buttons{
    display:flex;
    gap:10px;
    margin-top:12px;
}

.small-btn{
    flex:1;
    padding:13px;
    border:none;
    border-radius:14px;
    background:#f3f4f6;
    font-size:15px;
    cursor:pointer;
}

.explain{
    width:100%;
    margin-top:12px;
    padding:15px;
    border:none;
    border-radius:16px;
    background:#6366f1;
    color:white;
    font-size:17px;
    font-weight:bold;
    cursor:pointer;
}

.result{
    margin-top:20px;
    padding:18px;
    background:#f8fafc;
    border-radius:18px;
    display:none;
    line-height:1.7;
}

.result h3{
    color:#4f46e5;
    margin-bottom:10px;
}

.history{
    margin-top:25px;
}

.history h3{
    margin-bottom:10px;
}

.history-item{
    background:white;
    padding:12px;
    border-radius:12px;
    margin-bottom:8px;
    box-shadow:0 3px 10px rgba(0,0,0,.05);
}
</style>
</head>

<body>

<div class="header">
    <div class="logo">Sam<span>jhao</span> 🧠</div>
    <div class="subtitle">
        Kisi bhi topic ko simple language mein samjho
    </div>
</div>

<div class="container">

    <div class="card">

        <textarea id="question"
        placeholder="Example: Newton's First Law kya hai?"></textarea>

        <div class="buttons">
            <button class="small-btn" onclick="startVoice()">🎤 Mic</button>

            <button class="small-btn"
            onclick="document.getElementById('imageInput').click()">
            📷 Photo
            </button>

            <input type="file"
            id="imageInput"
            accept="image/*"
            style="display:none">
        </div>

        <button class="explain" onclick="explainTopic()">
            ✨ Samjhao
        </button>

        <div class="result" id="result">
            <h3>Explanation</h3>
            <p id="answer"></p>
        </div>

    </div>

    <div class="history">
        <h3>📚 Recent History</h3>
        <div id="historyList"></div>
    </div>

</div>

<script>

function explainTopic(){

    let question =
    document.getElementById("question").value.trim();

    if(question === ""){
        alert("Pehle koi topic ya question likho.");
        return;
    }

    let answer =
    "Tumne poocha: <b>" + question + "</b><br><br>" +

    "Is topic ko simple language mein samajhne ke liye " +
    "pehle iska basic concept samjho. " +
    "Ye Samjhao app ka demo explanation hai. " +
    "Agla version AI ki madad se tumhare question ka " +
    "proper answer generate karega.";

    document.getElementById("answer").innerHTML = answer;

    document.getElementById("result").style.display = "block";

    saveHistory(question);
}


function saveHistory(question){

    let history =
    JSON.parse(localStorage.getItem("history")) || [];

    history.unshift(question);

    history = history.slice(0,5);

    localStorage.setItem(
        "history",
        JSON.stringify(history)
    );

    showHistory();
}


function showHistory(){

    let history =
    JSON.parse(localStorage.getItem("history")) || [];

    let list =
    document.getElementById("historyList");

    list.innerHTML = "";

    history.forEach(function(item){

        let div =
        document.createElement("div");

        div.className = "history-item";

        div.innerHTML = "🔹 " + item;

        list.appendChild(div);

    });
}


function startVoice(){

    if(!("webkitSpeechRecognition" in window)){

        alert("Is browser mein voice input support nahi hai.");

        return;
    }

    let recognition =
    new webkitSpeechRecognition();

    recognition.lang = "hi-IN";

    recognition.start();

    recognition.onresult = function(event){

        let text =
        event.results[0][0].transcript;

        document.getElementById("question").value = text;
    };
}


showHistory();

</script>

</body>
</html>
