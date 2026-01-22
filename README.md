<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>EstateLink - Connect with Agents</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&family=Roboto:wght@400;500&display=swap" rel="stylesheet">
<style>
body {
  margin:0;
  font-family: 'Roboto', sans-serif;
  background: linear-gradient(to bottom right, rgba(0,0,0,0.6), rgba(25,25,112,0.6)),
              url("https://images.unsplash.com/photo-1560518883-ce09059eeffa") no-repeat center center fixed;
  background-size: cover;
  color:white;
  transition: 0.5s all;
}
header {text-align:center; padding:50px;}
header h1 {font-family: 'Montserrat', sans-serif; font-size:50px; margin:0; letter-spacing:2px; color:#FFD700; text-shadow: 2px 2px 8px #000;}
header p {font-size:22px; color:#f0f0f0; margin-top:10px; text-shadow: 1px 1px 6px #000;}
.container {max-width:1100px; margin:auto; padding:20px;}
.btn {display:inline-block;margin:5px 5px 10px 0;padding:12px 20px;border-radius:12px;font-weight:bold;text-decoration:none;cursor:pointer;transition:0.3s; font-family:'Montserrat',sans-serif;}
.btn:hover {opacity:0.85;}
.whatsapp {background:#25D366;color:black;}
.email {background:#03A9F4;color:black;}
.appointment {background:#FFC107;color:black;}
.subscribe {background:#FF5722;color:black;}
input {width:100%;padding:12px;margin:8px 0;border-radius:8px;border:none;font-size:16px;}
#agentLogin,#agentDashboard,#clientView {
  background: rgba(255,255,255,0.12);
  padding:30px;
  border-radius:20px;
  margin-bottom:30px;
  backdrop-filter:blur(8px);
  box-shadow: 0 8px 20px rgba(0,0,0,0.4);
  transition: 0.5s all;
  display:none; /* hide initially */
}
#agentBtn {
  position:fixed;
  top:30px;
  right:30px;
  background: linear-gradient(45deg, #FF5722, #FF8A65);
  color:white;
  padding:14px 22px;
  border:none;
  border-radius:12px;
  cursor:pointer;
  font-family:'Montserrat',sans-serif;
  font-weight:600;
  z-index:999;
  box-shadow:0 4px 10px rgba(0,0,0,0.4);
  transition:0.3s all;
}
#agentBtn:hover {transform: scale(1.05);}
#assistantBtn {
  position:fixed;
  bottom:20px;
  right:20px;
  background:#25D366;
  color:white;
  padding:16px 22px;
  border:none;
  border-radius:12px;
  cursor:pointer;
  font-family:'Montserrat',sans-serif;
  font-weight:600;
  z-index:999;
  box-shadow:0px 4px 8px rgba(0,0,0,0.3);
}
#assistant {position:fixed;bottom:70px;right:20px;width:350px;background:white;color:black;border-radius:12px;display:none;flex-direction:column;box-shadow:0 4px 8px rgba(0,0,0,0.3);}
#assistant-header {background:#25D366;padding:14px;text-align:center;font-weight:bold;border-top-left-radius:12px;border-top-right-radius:12px;color:white;}
#assistant-body {height:240px;padding:12px;overflow-y:auto;font-size:14px; line-height:1.4;}
#assistant-input {display:flex; margin-top:5px;}
#assistant-input input {flex:1;padding:10px;border:none;border-radius:0 0 0 8px;}
#assistant-input button {padding:10px;background:#25D366;border:none;color:white;border-radius:0 0 8px 0;}
.agent-card {background:rgba(255,255,255,0.18);padding:25px;margin-bottom:20px;border-radius:18px;transition:0.3s;box-shadow:0 8px 15px rgba(0,0,0,0.3);}
.agent-card:hover {background:rgba(255,255,255,0.28);}
.agent-card h4 {margin:0 0 6px 0;font-family:'Montserrat',sans-serif; font-size:20px; color:#FFD700;}
.agent-card p {margin:4px 0; font-size:15px;}
.free-trial {background:#4CAF50;color:white;padding:4px 8px;border-radius:5px;font-size:13px;margin-left:10px;}
</style>
</head>
<body>

<header>
<h1>EstateLink</h1>
<p>Instantly Find & Connect with Verified Real Estate Agents</p>
</header>

<div class="container">

<!-- AGENT LOGIN -->
<div id="agentLogin">
<h3>Agent Login / Profile Setup</h3>
<p>Set up your profile and start your 3-day free trial!</p>
<input type="text" id="agentName" placeholder="Full Name">
<input type="email" id="agentEmail" placeholder="Email">
<input type="text" id="agentWhatsApp" placeholder="WhatsApp Number">
<input type="text" id="agentLocation" placeholder="Location">
<input type="text" id="agentExperience" placeholder="Experience (Years)">
<button class="btn subscribe" onclick="agentLogin()">Save & Login</button>
</div>

<!-- AGENT DASHBOARD -->
<div id="agentDashboard">
<h3>Welcome <span id="dashboardName"></span> <span class="free-trial">3-Day Free Trial</span></h3>
<p>WhatsApp: <span id="dashboardWhatsApp"></span></p>
<p>Email: <span id="dashboardEmail"></span></p>
<p>Location: <span id="dashboardLocation"></span></p>
<p>Experience: <span id="dashboardExperience"></span> years</p>
<p><i>Verified Agent</i></p>
<p><b>Monthly Fee: $50</b></p>
<a class="btn subscribe" href="https://payoneer.com/your-payment-link" target="_blank">Pay Now / Activate Plan</a>
</div>

<!-- CLIENT VIEW -->
<div id="clientView">
<h3>Available Agents</h3>
<input type="text" id="searchAgent" placeholder="Search by location..." onkeyup="filterAgents()">
<div id="clientAgents"></div>
</div>

</div>

<!-- AGENT LOGIN BUTTON -->
<button id="agentBtn" onclick="toggleAgent()">Agent Login</button>

<!-- AI Assistant -->
<button id="assistantBtn" onclick="toggleAssistant()">Ask Assistant</button>
<div id="assistant">
<div id="assistant-header">Virtual Assistant</div>
<div id="assistant-body">
<p><b>Assistant:</b> Hi! How can I help you today?</p>
</div>
<div id="assistant-input">
<input type="text" id="userText" placeholder="Type your question...">
<button onclick="assistantReply()">Send</button>
</div>
</div>

<script>
let agents = [];
let trialDays = 3;

// ---------------- Toggle Agent Login Panel ----------------
function toggleAgent(){
  let panel = document.getElementById("agentLogin");
  let dashboard = document.getElementById("agentDashboard");
  // toggle visibility
  if(panel.style.display === "block"){
    panel.style.display = "none";
  } else {
    panel.style.display = "block";
    dashboard.style.display = "none"; // hide dashboard if login is clicked
  }
}

// ---------------- Agent Login ----------------
function agentLogin(){
  let name=document.getElementById("agentName").value;
  let email=document.getElementById("agentEmail").value;
  let whatsapp=document.getElementById("agentWhatsApp").value;
  let location=document.getElementById("agentLocation").value;
  let experience=document.getElementById("agentExperience").value;

  if(!name || !email){ alert("Enter Name and Email"); return; }

  let agent={name,email,whatsapp,location,experience,loginTime:new Date().getTime()};
  agents.push(agent);
  localStorage.setItem("agents",JSON.stringify(agents));

  document.getElementById("agentLogin").style.display="none";
  document.getElementById("agentDashboard").style.display="block";
  document.getElementById("agentBtn").style.display="none";

  document.getElementById("dashboardName").innerText=name;
  document.getElementById("dashboardEmail").innerText=email;
  document.getElementById("dashboardWhatsApp").innerText=whatsapp;
  document.getElementById("dashboardLocation").innerText=location;
  document.getElementById("dashboardExperience").innerText=experience;

  renderClientAgents();
  alert("You have a 3-Day Free Trial! After that, profile will be hidden unless monthly fee is paid.");
}

// ---------------- Check Trial ----------------
function checkTrial(){
  let storedAgents=JSON.parse(localStorage.getItem("agents")) || [];
  let now = new Date().getTime();
  for(let i=storedAgents.length-1;i>=0;i--){
    if(now - storedAgents[i].loginTime > trialDays*24*60*60*1000){
      storedAgents.splice(i,1);
    }
  }
  localStorage.setItem("agents",JSON.stringify(storedAgents));
}

// ---------------- Render Agents ----------------
function renderClientAgents(){
  checkTrial();
  let container=document.getElementById("clientAgents");
  container.innerHTML="";
  let storedAgents=JSON.parse(localStorage.getItem("agents")) || [];
  storedAgents.forEach(a=>{
    let card=document.createElement("div");
    card.className="agent-card";
    card.innerHTML=`<h4>${a.name}</h4>
    <p>Location: ${a.location}</p>
    <p>Experience: ${a.experience} Years</p>
    <a class="btn whatsapp" href="https://wa.me/${a.whatsapp}" target="_blank">WhatsApp</a>
    <a class="btn email" href="mailto:${a.email}">Email</a>
    <a class="btn appointment" href="mailto:${a.email}?subject=Appointment Request&body=Hi, I want to book an appointment.">Book Appointment</a>`;
    container.appendChild(card);
  });
}

// ---------------- Filter Agents ----------------
function filterAgents(){
  let input=document.getElementById("searchAgent").value.toLowerCase();
  let storedAgents=JSON.parse(localStorage.getItem("agents")) || [];
  let container=document.getElementById("clientAgents");
  container.innerHTML="";
  storedAgents.filter(a=>a.location.toLowerCase().includes(input))
  .forEach(a=>{
    let card=document.createElement("div");
    card.className="agent-card";
    card.innerHTML=`<h4>${a.name}</h4>
    <p>Location: ${a.location}</p>
    <p>Experience: ${a.experience} Years</p>
    <a class="btn whatsapp" href="https://wa.me/${a.whatsapp}" target="_blank">WhatsApp</a>
    <a class="btn email" href="mailto:${a.email}">Email</a>
    <a class="btn appointment" href="mailto:${a.email}?subject=Appointment Request&body=Hi, I want to book an appointment.">Book Appointment</a>`;
    container.appendChild(card);
  });
}

// ---------------- AI Assistant ----------------
function toggleAssistant(){
  let box=document.getElementById("assistant");
  box.style.display=(box.style.display=="flex")?"none":"flex";
}
function assistantReply(){
  let text=document.getElementById("userText").value.toLowerCase();
  let body=document.getElementById("assistant-body");
  body.innerHTML+="<p><b>You:</b> "+text+"</p>";
  let reply="Please select an agent to contact for details.";
  if(text.includes("hi")||text.includes("hello")) reply="Hello! How can I help you today?";
  else if(text.includes("how are you")) reply="I'm a virtual assistant ready to help with real estate queries!";
  else if(text.includes("agent")) reply="Select an agent from the list above to connect.";
  else if(text.includes("where")||text.includes("location")) reply="Search agents by city or region using the search bar above.";
  else if(text.includes("price")||text.includes("rent")||text.includes("buy")) reply="Agents can provide pricing, rental, or property sale info directly.";
  else if(text.includes("appointment")||text.includes("book")) reply="Use the 'Book Appointment' button on the agent card to schedule.";
  else if(text.includes("thanks")||text.includes("thank you")) reply="You're welcome!";
  body.innerHTML+="<p><b>Assistant:</b> "+reply+"</p>";
  document.getElementById("userText").value="";
}

// ---------------- Load ----------------
window.onload=function(){ renderClientAgents(); }
</script>

</body>
</html>
