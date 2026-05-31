<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>AI Dog</title>
<style>
body{
    font-family:Arial,sans-serif;
    text-align:center;
    background:#f5f5f5;
}
#dog{
    width:250px;
    margin-top:20px;
}
#chat{
    width:80%;
    max-width:600px;
    height:300px;
    margin:20px auto;
    border:1px solid #ccc;
    background:white;
    overflow-y:auto;
    padding:10px;
}
button{
    padding:10px 20px;
    font-size:18px;
}
</style>
</head>
<body>

<h1>🐶 AI Dog</h1>

<img id="dog" src="https://images.unsplash.com/photo-1552053831-71594a27632d?w=500" alt="Dog">

<div id="chat"></div>

<button onclick="startListening()">🎤 Talk to Dog</button>

<script>
const chat = document.getElementById("chat");

function addMessage(sender,text){
    chat.innerHTML += "<p><b>"+sender+":</b> "+text+"</p>";
    chat.scrollTop = chat.scrollHeight;
}

function speak(text){
    const utterance = new SpeechSynthesisUtterance(text);
    speechSynthesis.speak(utterance);
}

function dogReply(text){
    text = text.toLowerCase();

    let reply = "Woof! Tell me more.";

    if(text.includes("hello"))
        reply = "Hello human! Nice to see you!";
    else if(text.includes("name"))
        reply = "I am your AI Dog.";
    else if(text.includes("how are you"))
        reply = "I'm feeling pawsome today!";
    else if(text.includes("sad"))
        reply = "I'm sorry. Want a virtual dog hug?";
    else if(text.includes("bye"))
        reply = "Woof woof! See you later!";

    addMessage("Dog",reply);
    speak(reply);
}

function startListening(){
    const SpeechRecognition =
        window.SpeechRecognition ||
        window.webkitSpeechRecognition;

    const recognition = new SpeechRecognition();

    recognition.start();

    recognition.onresult = function(event){
        const text = event.results[0][0].transcript;
        addMessage("You",text);
        dogReply(text);
    };
}
</script>

</body>
</html>
<button onclick="testDog()">Talk to Dog</button>

<script>
function testDog() {
    alert("Button works!");

    const text = "Hello! I am your AI Dog!";

    const speech = new SpeechSynthesisUtterance(text);
    speechSynthesis.speak(speech);
}
</script>
