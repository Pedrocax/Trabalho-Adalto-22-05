<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<title>Cabo de Guerra</title>

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
user-select:none;
}

body{
font-family:Arial,sans-serif;
background:
radial-gradient(circle at top,#1e293b,#020617 70%);
color:white;
overflow-x:hidden;
overflow-y:auto;
-webkit-overflow-scrolling:touch;
touch-action:pan-y;
min-height:100vh;
}

#startScreen{
position:fixed;
inset:0;
background:linear-gradient(180deg,#0f172a,#020617);
display:flex;
align-items:center;
justify-content:center;
z-index:2000;
}

.startBox{
width:90%;
max-width:420px;
background:rgba(255,255,255,0.08);
padding:30px;
border-radius:30px;
text-align:center;
border:2px solid rgba(255,255,255,0.08);
box-shadow:0 0 30px rgba(59,130,246,0.25);
}

.startBox h2{
font-size:34px;
margin-bottom:20px;
color:#facc15;
}

.startBox input{
width:100%;
height:60px;
border:none;
border-radius:16px;
margin:10px 0;
padding:10px;
font-size:20px;
text-align:center;
}

.startBox button{
margin-top:15px;
padding:15px 30px;
border:none;
border-radius:18px;
background:#facc15;
font-size:22px;
font-weight:900;
}

body::before{
content:"";
position:fixed;
inset:0;
background:
radial-gradient(circle at 20% 20%,rgba(59,130,246,0.15),transparent 30%),
radial-gradient(circle at 80% 30%,rgba(250,204,21,0.15),transparent 30%),
radial-gradient(circle at 50% 80%,rgba(239,68,68,0.12),transparent 30%);
pointer-events:none;
}

h1{
text-align:center;
margin-top:15px;
font-size:40px;
color:#facc15;
text-shadow:0 0 20px rgba(250,204,21,0.7);
}

#score,#timer,#question,#msg{
text-align:center;
margin-top:10px;
}

#question{
font-size:34px;
font-weight:900;
color:#38bdf8;
padding:0 10px;
}

#timer{
font-size:32px;
font-weight:bold;
}

#powerContainer{
width:92%;
height:28px;
margin:15px auto;
background:#111827;
border-radius:30px;
overflow:hidden;
border:2px solid rgba(255,255,255,0.08);
box-shadow:0 0 18px rgba(59,130,246,0.2);
}

#powerBar{
width:50%;
height:100%;
background:linear-gradient(90deg,#2563eb,#facc15,#dc2626);
transition:0.35s;
}

#arena{
position:relative;
width:95%;
height:220px;
margin:auto;
margin-top:15px;
background:linear-gradient(180deg,#111827,#0f172a);
border-radius:30px;
overflow:hidden;
border:2px solid rgba(255,255,255,0.1);
box-shadow:0 0 35px rgba(59,130,246,0.25);
}

#center{
position:absolute;
left:50%;
width:5px;
height:100%;
background:#facc15;
transform:translateX(-50%);
}

#rope{
position:absolute;
top:105px;
left:50%;
transform:translateX(-50%);
width:650px;
height:24px;
background:repeating-linear-gradient(
90deg,
#8b5a2b 0px,
#d97706 18px,
#92400e 36px
);
border-radius:30px;
transition:0.35s;
animation:ropeFloat 3s ease-in-out infinite;
box-shadow:0 0 20px rgba(245,158,11,0.6);
}

#flag{
position:absolute;
left:50%;
top:-45px;
transform:translateX(-50%);
font-size:55px;
}

.team{
position:absolute;
top:60px;
font-size:60px;
transition:0.35s;
display:flex;
gap:0px;
alignment-baseline:middle;
animation:pullLoop 1s infinite alternate;

position:absolute;
top:35px;
font-size:60px;
transition:0.35s;
}

#blueTeam{left:120px;}
#redTeam{right:120px;}

.container{
display:flex;
justify-content:space-between;
gap:10px;
width:95%;
margin:auto;
margin-top:15px;
}

.player{
width:49%;
}

.box{
overflow:visible;
background:rgba(255,255,255,0.08);
padding:12px;
border-radius:25px;
border:2px solid rgba(255,255,255,0.08);
}

.btn{
background:linear-gradient(180deg,#ffffff,#dbeafe);
min-height:100px;
font-size:34px;
margin:20px 0;
border:4px solid rgba(255,255,255,0.4);
color:#0f172a;
min-height:65px;
margin:10px 0;
border-radius:18px;
display:flex;
align-items:center;
justify-content:center;
font-size:22px;
font-weight:900;
cursor:pointer;
transition:0.2s;
box-shadow:0 8px 18px rgba(0,0,0,0.25);
}

.btn:hover{
transform:scale(1.03);
}

.correct{
background:#22c55e !important;
color:white;
}

.wrong{
background:#ef4444 !important;
color:white;
}

#miniBattle{
position:fixed;
inset:0;
display:none;
align-items:center;
justify-content:center;
font-size:90px;
z-index:998;
pointer-events:none;
background:rgba(0,0,0,0.4);
}

.throwLeft{
animation:throwLeft 1s forwards;
}

.throwRight{
animation:throwRight 1s forwards;
}

@keyframes throwLeft{
0%{transform:translateX(0) rotate(0deg) scale(1);opacity:1;}
100%{transform:translateX(-600px) rotate(-720deg) scale(0.5);opacity:0;}
}

@keyframes throwRight{
0%{transform:translateX(0) rotate(0deg) scale(1);opacity:1;}
100%{transform:translateX(600px) rotate(720deg) scale(0.5);opacity:0;}
}

#treasureGame{
position:fixed;
inset:0;
background:linear-gradient(180deg,#111827,#020617);
display:none;
overflow:hidden;
z-index:999;
}

#treasureTitle{
text-align:center;
margin-top:20px;
font-size:42px;
font-weight:900;
color:#facc15;
text-shadow:0 0 20px rgba(250,204,21,0.7);
}

#treasureTimer{
text-align:center;
font-size:34px;
margin-top:10px;
font-weight:bold;
}

#treasureScore{
text-align:center;
font-size:32px;
margin-top:10px;
font-weight:bold;
}

.item{
position:absolute;
font-size:80px;
padding:20px;
font-size:48px;
cursor:pointer;
filter:drop-shadow(0 0 12px rgba(255,255,255,0.5));
animation:fall linear forwards;
transition:0.15s;
}



@keyframes fall{
from{
transform:translateY(-120px) rotate(0deg);
}

to{
transform:translateY(120vh) rotate(360deg);
}
}

#win{
position:fixed;
inset:0;
background:rgba(0,0,0,0.95);
display:none;
justify-content:center;
align-items:center;
flex-direction:column;
font-size:42px;
text-align:center;
z-index:1000;
}

#restartBtn{
margin-top:25px;
padding:16px 30px;
border:none;
border-radius:18px;
font-size:24px;
font-weight:900;
background:#facc15;
}

@keyframes pullLoop{
0%{
transform:translateY(0px);
}
100%{
transform:translateY(8px);
}
}

@keyframes ropeFloat{
0%{
transform:translateX(-50%) translateY(0px);
}
50%{
transform:translateX(-50%) translateY(-8px);
}
100%{
transform:translateX(-50%) translateY(0px);
}
}
100%{transform:translateY(8px);}
}

.eventBox{
position:fixed;
top:20px;
left:50%;
transform:translateX(-50%);
padding:16px 28px;
background:rgba(250,204,21,0.15);
border:2px solid rgba(250,204,21,0.5);
border-radius:20px;
font-size:28px;
font-weight:900;
color:#facc15;
backdrop-filter:blur(10px);
z-index:1200;
animation:eventAnim 3s forwards;
}

@keyframes eventAnim{
0%{opacity:0;transform:translateX(-50%) translateY(-50px);}
15%{opacity:1;transform:translateX(-50%) translateY(0px);}
85%{opacity:1;transform:translateX(-50%) translateY(0px);}
100%{opacity:0;transform:translateX(-50%) translateY(-50px);}
}

.transitionScreen{
position:fixed;
inset:0;
display:flex;
align-items:center;
justify-content:center;
font-size:70px;
font-weight:900;
background:rgba(0,0,0,0.75);
backdrop-filter:blur(10px);
z-index:1500;
opacity:0;
pointer-events:none;
transition:0.4s;
}

html,body{
height:100%;
}

.container{
padding-bottom:40px;
}

@media(max-width:900px){

.container{
flex-direction:row;
align-items:flex-start;
gap:20px;
}

.player{
width:50%;
}

.box{
min-height:520px;
}

#rope{
width:340px;
}

.team{
font-size:40px;
}

#question{
font-size:24px;
}

.btn{
font-size:18px;
}
}
</style>
</head>
<body>

<div id="startScreen">
<div class="startBox">
<h2>⚔️ CABO DE GUERRA ⚔️</h2>
<input id="blueNameInput" placeholder="Nome da equipe azul">
<input id="redNameInput" placeholder="Nome da equipe vermelha">
<button id="startBtn" type="button">🎮 Começar</button>
</div>
</div>

<div style="display:flex;justify-content:center;margin-top:10px;gap:15px;">
<button onclick="openFullscreen()" style="padding:14px 24px;border:none;border-radius:16px;background:#facc15;font-size:22px;font-weight:900;cursor:pointer;">📺 Tela Cheia</button>
</div>

<h1>⚔️ CABO DE GUERRA ⚔️</h1>

<div id="score" style="display:flex;justify-content:space-between;width:92%;margin:auto;margin-top:10px;font-size:24px;font-weight:900;">
<div id="blueScore">🔵 Azul: 0</div>
<div id="redScore">🔴 Vermelho: 0</div>
</div>
<div id="timer">⏱️ 20</div>
<div id="round" style="text-align:center;margin-top:8px;font-size:24px;font-weight:bold;color:#facc15;">🏆 Rodada 1 / 10</div>
<div id="question"></div>
<div id="msg"></div>

<div id="powerContainer">
<div id="powerBar"></div>
</div>

<div id="arena">
<div id="center"></div>

<div id="rope">
<div id="flag">🚩</div>
</div>

<div class="team" id="blueTeam">🧍‍♂️🧍‍♂️🧍‍♂️</div>
<div class="team" id="redTeam">🧍‍♀️🧍‍♀️🧍‍♀️</div>
</div>

<div class="container">
<div class="player">
<div class="box" id="blue"></div>
</div>

<div class="player">
<div class="box" id="red"></div>
</div>
</div>

<div id="miniBattle"></div>

<div id="treasureGame">
<div id="treasureTitle">💰 CAÇA AO TESOURO 💰</div>
<div id="treasureTimer">⏱️ 6</div>
<div id="treasureScore">⭐ 0</div>
</div>

<div id="transition" class="transitionScreen">⚡ MINI GAME ⚡</div>

<div id="win"></div>

<script>

const Game = {

maxRounds:10,
currentRound:1,

questions:[
{q:"Goiás",a:"Goiânia",o:["Goiânia","Anápolis","Rio Verde","Catalão"]},
{q:"Bahia",a:"Salvador",o:["Salvador","Ilhéus","Feira de Santana","Porto Seguro"]},
{q:"Paraná",a:"Curitiba",o:["Curitiba","Londrina","Maringá","Foz do Iguaçu"]},
{q:"Amazonas",a:"Manaus",o:["Manaus","Tefé","Coari","Parintins"]},
{q:"São Paulo",a:"São Paulo",o:["São Paulo","Campinas","Santos","Ribeirão Preto"]},
{q:"Pernambuco",a:"Recife",o:["Recife","Olinda","Caruaru","Petrolina"]},
{q:"Acre",a:"Rio Branco",o:["Rio Branco","Cruzeiro do Sul","Tarauacá","Sena Madureira"]},
{q:"Alagoas",a:"Maceió",o:["Maceió","Arapiraca","Penedo","Palmeira dos Índios"]},
{q:"Amapá",a:"Macapá",o:["Macapá","Santana","Oiapoque","Laranjal do Jari"]},
{q:"Ceará",a:"Fortaleza",o:["Fortaleza","Sobral","Juazeiro do Norte","Crato"]},
{q:"Distrito Federal",a:"Brasília",o:["Brasília","Taguatinga","Ceilândia","Gama"]},
{q:"Espírito Santo",a:"Vitória",o:["Vitória","Serra","Vila Velha","Linhares"]},
{q:"Maranhão",a:"São Luís",o:["São Luís","Imperatriz","Caxias","Timon"]},
{q:"Mato Grosso",a:"Cuiabá",o:["Cuiabá","Sinop","Rondonópolis","Cáceres"]},
{q:"Mato Grosso do Sul",a:"Campo Grande",o:["Campo Grande","Corumbá","Dourados","Três Lagoas"]},
{q:"Minas Gerais",a:"Belo Horizonte",o:["Belo Horizonte","Uberlândia","Ouro Preto","Contagem"]},
{q:"Pará",a:"Belém",o:["Belém","Santarém","Marabá","Altamira"]},
{q:"Paraíba",a:"João Pessoa",o:["João Pessoa","Campina Grande","Patos","Sousa"]},
{q:"Piauí",a:"Teresina",o:["Teresina","Parnaíba","Picos","Floriano"]},
{q:"Rio Grande do Norte",a:"Natal",o:["Natal","Mossoró","Caicó","Parnamirim"]},
{q:"Rio Grande do Sul",a:"Porto Alegre",o:["Porto Alegre","Pelotas","Caxias do Sul","Gramado"]},
{q:"Rondônia",a:"Porto Velho",o:["Porto Velho","Ji-Paraná","Vilhena","Ariquemes"]},
{q:"Roraima",a:"Boa Vista",o:["Boa Vista","Pacaraima","Caracaraí","Rorainópolis"]},
{q:"Santa Catarina",a:"Florianópolis",o:["Florianópolis","Joinville","Blumenau","Chapecó"]},
{q:"Sergipe",a:"Aracaju",o:["Aracaju","Lagarto","Itabaiana","Estância"]},
{q:"Tocantins",a:"Palmas",o:["Palmas","Araguaína","Gurupi","Porto Nacional"]}
],

index:0,
ropePos:0,
blueScore:0,
redScore:0,
answered:false,
time:20,
timer:null,
treasureInterval:null,
treasurePoints:0,
clickLock:false,

shuffle(array){
for(let i=array.length-1;i>0;i--){
const j=Math.floor(Math.random()*(i+1));
[array[i],array[j]]=[array[j],array[i]];
}
return array;
},

blueName:"Azul",
redName:"Vermelho",

startGame(){

this.blueName=
document.getElementById("blueNameInput").value || "Azul";

this.redName=
document.getElementById("redNameInput").value || "Vermelho";

const start=document.getElementById("startScreen");

if(start){
start.style.display="none";
}

this.index=0;
this.currentRound=1;
this.ropePos=0;
this.blueScore=0;
this.redScore=0;
this.answered=false;

this.updateScore();
this.updatePowerBar();

this.shuffle(this.questions);

this.load();
},

start(){
this.shuffle(this.questions);
this.updateScore();
this.updatePowerBar();
this.load();
},

startTimer(){

clearInterval(this.timer);

this.time=25;

const timer=document.getElementById("timer");

timer.innerHTML=`⏱️ ${this.time}`;

timer.style.color="#38bdf8";

this.timer=setInterval(()=>{

this.time--;

timer.innerHTML="⏱️ "+this.time;

if(this.time<=5){
timer.style.color="#ef4444";
}

if(this.time<=0){
clearInterval(this.timer);
this.answered=true;
document.getElementById("msg").innerHTML="⏰ Tempo acabou!";
setTimeout(()=>this.next(),1200);
}

},1000);
},

load(){

this.answered=false;

if(this.currentRound>this.maxRounds){

if(this.blueScore>this.redScore){
this.end(`🏆 ${this.blueName} venceu a partida!`);
}
else if(this.redScore>this.blueScore){
this.end(`🏆 ${this.redName} venceu a partida!`);
}
else{
this.end("🤝 Empate!");
}

return;
}

document.getElementById("round")
.innerHTML=`🏆 Rodada ${this.currentRound} / ${this.maxRounds}`;

const data=this.questions[this.index];

document.getElementById("question")
.innerHTML=`🌍 Qual é a capital de <b>${data.q}</b>?`;

this.createButtons("blue",data);
this.createButtons("red",data);

this.startTimer();
},

createButtons(id,data){

const box=document.getElementById(id);

box.innerHTML="";

this.shuffle([...data.o]).forEach(opt=>{

const btn=document.createElement("div");

btn.className="btn";
btn.innerHTML=opt;

btn.onclick=()=>this.answer(opt,data.a,id,btn);

box.appendChild(btn);
});
},

answer(opt,correct,team,button){

if(this.answered) return;

if(this.clickLock) return;

this.clickLock=true;

setTimeout(()=>{
this.clickLock=false;
},250);

this.answered=true;

clearInterval(this.timer);

if(navigator.vibrate){
navigator.vibrate(80);
}

const allBtns=document.querySelectorAll(".btn");

allBtns.forEach(btn=>{
if(btn.innerHTML===correct){
btn.classList.add("correct");
}
});

if(opt!==correct){
button.classList.add("wrong");
document.getElementById("msg").innerHTML="❌ Errou!";
setTimeout(()=>this.next(),1200);
return;
}

document.getElementById("msg").innerHTML=
"✅ ACERTOU! PREPARANDO MINI GAME!";

document.body.style.background=
"linear-gradient(180deg,#14532d,#020617)";

setTimeout(()=>{
document.body.style.background=
"radial-gradient(circle at top,#1e293b,#020617 70%)";
},700);

this.showThrowAnimation(team);
this.showTransition(team);

setTimeout(()=>{
this.startTreasure(team);
},2200);
},

spawnItem(){

const item=document.createElement("div");

item.className="item";

let rand=Math.random();
let value=0;

if(rand<0.45){
item.innerHTML="💰";
value=5;
}
else if(rand<0.75){
item.innerHTML="💎";
value=30;
}
else if(rand<0.93){
item.innerHTML="👑";
value=50;
}
else{
item.innerHTML="💣";
value=-20;
}

item.style.left=Math.random()*90+"%";
item.style.animationDuration=(Math.random()*2+2)+"s";

item.onclick=()=>{

this.treasurePoints+=value;

this.treasurePoints=
Math.max(-100,Math.min(this.treasurePoints,999));

if(navigator.vibrate){
navigator.vibrate(40);
}

item.style.transform="scale(1.5)";

setTimeout(()=>{
item.remove();
},80);

this.updateTreasureScore();
};

document.getElementById("treasureGame")
.appendChild(item);

setTimeout(()=>{
item.remove();
},5000);
},

updateTreasureScore(){

document.getElementById("treasureScore")
.innerHTML=`⭐ ${this.treasurePoints}`;
},

showTransition(team){

const transition=document.getElementById("transition");

let name=
team==="blue"
? this.blueName
: this.redName;

let color=
team==="blue"
? "🔵"
: "🔴";

transition.innerHTML=`
<div>
${color} MINI GAME ${color}<br>

<div style="
font-size:42px;
margin-top:20px;
color:#facc15;
">
${name} vai jogar!
</div>
</div>
`;

transition.style.opacity="1";

setTimeout(()=>{
transition.style.opacity="0";
},1800);
},

showEvent(){

const events=[
"🌧️ CHUVA DE DIAMANTES",
"👑 FEBRE DAS COROAS",
"💣 CAMPO MINADO",
"⚡ MODO TURBO"
];

const div=document.createElement("div");

div.className="eventBox";

div.innerHTML=
events[Math.floor(Math.random()*events.length)];

document.body.appendChild(div);

setTimeout(()=>{
div.remove();
},3000);
},

showThrowAnimation(team){

const battle=document.getElementById("miniBattle");

battle.style.display="flex";

if(team==="blue"){

battle.innerHTML=`
<div class="throwRight">🧍‍♂️💥🧍‍♀️</div>
`;
}
else{

battle.innerHTML=`
<div class="throwLeft">🧍‍♀️💥🧍‍♂️</div>
`;
}

setTimeout(()=>{
battle.style.display="none";
battle.innerHTML="";
},1000);
},

startTreasure(team){

this.showEvent();

this.treasurePoints=0;

let duration=8;

if(this.index>=3) duration=5;
if(this.index>=6) duration=4;

let current=duration;

const game=document.getElementById("treasureGame");

game.style.display="block";

this.updateTreasureScore();

document.getElementById("treasureTimer")
.innerHTML="⏱️ "+current;

this.treasureInterval=setInterval(()=>{
this.spawnItem();
},220);

const countdown=setInterval(()=>{
current--;

document.getElementById("treasureTimer")
.innerHTML="⏱️ "+current;

if(current<=0){
clearInterval(countdown);
}

},1000);

setTimeout(()=>{

clearInterval(this.treasureInterval);

const items=document.querySelectorAll(".item");
items.forEach(el=>el.remove());

game.style.display="none";

if(team==="blue"){
this.ropePos+=this.treasurePoints/4;
this.blueScore+=Math.max(0,Math.floor(this.treasurePoints/10));
}
else{
this.ropePos-=this.treasurePoints/4;
this.redScore+=Math.max(0,Math.floor(this.treasurePoints/10));
}

this.ropePos=Math.max(-260,Math.min(this.ropePos,260));

this.updateRope();
this.updateScore();
this.updatePowerBar();

if(this.ropePos>=250){
this.end(`🔵 ${this.blueName} venceu!`);
return;
}

if(this.ropePos<=-250){
this.end(`🔴 ${this.redName} venceu!`);
return;
}

this.next();

},duration*1000);
},

updatePowerBar(){

const percent=50+(this.ropePos/5);

document.getElementById("powerBar")
.style.width=`${percent}%`;
},

updateRope(){

document.getElementById("rope")
.style.transform=
`translateX(calc(-50% + ${this.ropePos}px))`;

document.getElementById("blueTeam")
.style.transform=`translateX(${this.ropePos}px)`;

document.getElementById("redTeam")
.style.transform=`translateX(${this.ropePos}px)`;
},

updateScore(){

document.getElementById("blueScore")
.innerHTML=`🔵 ${this.blueName}: ${this.blueScore}`;

document.getElementById("redScore")
.innerHTML=`🔴 ${this.redName}: ${this.redScore}`;

},

next(){

this.index++;
this.currentRound++;

if(this.index>=this.questions.length){
this.index=0;
this.shuffle(this.questions);
}

this.load();
},

exitGame(){

clearInterval(this.timer);
clearInterval(this.treasureInterval);

location.reload();
},

reset(){

clearInterval(this.timer);
clearInterval(this.treasureInterval);

this.index=0;
this.ropePos=0;
this.blueScore=0;
this.redScore=0;
this.answered=false;
this.treasurePoints=0;
this.currentRound=1;

this.shuffle(this.questions);

this.updateRope();
this.updateScore();
this.updatePowerBar();

const win=document.getElementById("win");
win.style.display="none";

this.load();
},

end(text){

clearInterval(this.timer);
clearInterval(this.treasureInterval);

const win=document.getElementById("win");

win.style.display="flex";

win.innerHTML=`
<div>${text}</div>

<div style="margin-top:20px;font-size:28px;line-height:1.7;">
🔵 ${this.blueName}: ${this.blueScore}<br>
🔴 ${this.redName}: ${this.redScore}
</div>

<div style="display:flex;gap:18px;justify-content:center;margin-top:25px;flex-wrap:wrap;">
<button id="restartBtn">🔄 Jogar novamente</button>
<button id="exitBtn" style="background:#ef4444;color:white;">🚪 Sair</button>
</div>
`;

document.getElementById("restartBtn")
.onclick=()=>this.reset();

document.getElementById("exitBtn")
.onclick=()=>this.exitGame();
}

};



function openFullscreen(){

const elem=document.documentElement;

if(elem.requestFullscreen){
elem.requestFullscreen();
}
}

window.onload = function(){

const startBtn = document.getElementById("startBtn");

if(startBtn){
startBtn.onclick = function(){
Game.startGame();
};
}

};

</script>
</body>
</html>
