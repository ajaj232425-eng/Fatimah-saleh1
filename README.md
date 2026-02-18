# Fatimah-saleh1<<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>حساب عمر الطفل</title>

<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@600&display=swap" rel="stylesheet">

<style>
body{
font-family:'Cairo',sans-serif;
text-align:center;
margin:0;
color:#fff;
background: linear-gradient(270deg,#ff9de6,#bfa6ff,#8ed6ff);
background-size:600% 600%;
animation: gradientMove 8s ease infinite;
}

/* تموج الخلفية */
@keyframes gradientMove{
0%{background-position:0% 50%}
50%{background-position:100% 50%}
100%{background-position:0% 50%}
}

/* زخارف أزهار */
body::before{
content:"🌸 🌼 🌺 🌸 🌼 🌺";
font-size:40px;
position:fixed;
top:10px;
left:10px;
opacity:0.25;
}

/* الترويسة */
.header{
background:white;
color:#6a5acd;
padding:12px;
font-size:20px;
font-weight:bold;
}

.header img{
width:60px;
vertical-align:middle;
}

.container{
background:white;
color:#333;
margin:40px auto;
padding:30px;
border-radius:25px;
width:50%;
box-shadow:0 10px 25px rgba(0,0,0,0.2);
}

input,button{
padding:12px;
font-size:18px;
border-radius:12px;
border:none;
margin-top:10px;
}

button{
background:#ff7ad9;
color:white;
cursor:pointer;
}

button:hover{
background:#ff4ec7;
}

.result{
margin-top:20px;
font-size:22px;
color:#6a5acd;
}

.print-btn{
background:#6a5acd;
margin-top:15px;
}

footer{
margin-top:40px;
font-size:18px;
}
</style>
</head>

<body>

<div class="header">
<img src="https://upload.wikimedia.org/wikipedia/ar/thumb/0/02/Ministry_of_Education_Saudi_Arabia_Logo.svg/512px-Ministry_of_Education_Saudi_Arabia_Logo.svg.png">
وزارة التعليم – منطقة نجران
</div>

<div class="container">
<h2>🎈 حساب عمر الطفل 🎈</h2>

<input type="date" id="birthdate"><br>
<button onclick="calculateAge()">احسب العمر</button>

<div class="result" id="result"></div>
<div class="result" id="hijri"></div>

<button class="print-btn" onclick="window.print()">🖨️ طباعة النتيجة</button>
</div>

<footer>
مديره الروضه ومصممه الموقع :<br>
<strong>فاطمه صالح ال بحري</strong>
</footer>

<audio id="sound">
<source src="https://www.soundjay.com/human/sounds/applause-8.mp3">
</audio>

<script>
function calculateAge(){
const birthdate=document.getElementById("birthdate").value;
if(!birthdate){ alert("اختاري تاريخ الميلاد"); return; }

const birth=new Date(birthdate);
const today=new Date();

let years=today.getFullYear()-birth.getFullYear();
let months=today.getMonth()-birth.getMonth();
let days=today.getDate()-birth.getDate();

if(days<0){
months--;
days+=30;
}
if(months<0){
years--;
months+=12;
}

document.getElementById("result").innerHTML=
"العمر: "+years+" سنة و "+months+" شهر و "+days+" يوم 🎉";

// التاريخ الهجري
const hijri=new Intl.DateTimeFormat('ar-SA-u-ca-islamic',{
day:'numeric',month:'long',year:'numeric'
}).format(birth);

document.getElementById("hijri").innerHTML=
"تاريخ الميلاد هجري: "+hijri;

document.getElementById("sound").play();
}
</script>

</body>
</html>
