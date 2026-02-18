# Fatimah-saleh1<<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>حاسبة عمر الطفل</title>

<style>
body {
    font-family: "Tahoma", Arial;
    text-align: center;
    direction: rtl;
    margin: 0;
    min-height: 100vh;
    overflow-x: hidden;

    /* خلفية تموجات ملونة */
    background: linear-gradient(-45deg, #c77dff, #ffafcc, #90dbf4, #b8c0ff);
    background-size: 400% 400%;
    animation: gradientBG 5s ease infinite; /* تموج أسرع */
    position: relative;
}

/* التموجات الخلفية */
@keyframes gradientBG {
    0% {background-position: 0% 50%;}
    50% {background-position: 100% 50%;}
    100% {background-position: 0% 50%;}
}

/* صور أزهار فوق الخلفية */
body::before {
    content: "";
    position: absolute;
    top:0;
    left:0;
    width:100%;
    height:100%;
    background: url('https://i.ibb.co/W6f8KQh/flower-transparent.png') repeat;
    opacity: 0.15; /* شفافية الأزهار */
    pointer-events: none;
    z-index: 0;
}

/* الترويسة */
.header {
    background: white;
    padding: 15px;
    border-bottom: 3px solid #0a7c66;
    position: relative;
    z-index: 1;
}

.header img {
    width: 80px;
    vertical-align: middle;
}

.header-text {
    display: inline-block;
    text-align: right;
    margin-right: 10px;
    font-size: 18px;
    color: #0a7c66;
    font-weight: bold;
}

/* زخارف */
.decor {
    font-size: 48px;
    margin-top: 10px;
    position: relative;
    z-index: 1;
}

.container {
    background: white;
    padding: 30px;
    margin: 25px auto;
    width: 50%; /* نصف الصفحة */
    min-width: 320px;
    border-radius: 25px;
    box-shadow: 0 0 20px rgba(0,0,0,0.3);
    position: relative;
    z-index: 1;
}

h1 {
    color: #d63384;
    font-size: 28px;
}

.subtitle {
    color: #555;
    margin-bottom: 15px;
    font-size: 18px;
}

input {
    padding: 12px;
    border-radius: 10px;
    border: 1px solid #ccc;
    width: 90%;
    margin-bottom: 15px;
    text-align: center;
    font-size: 18px;
}

button {
    background-color: #d63384;
    color: white;
    padding: 12px 20px;
    border: none;
    border-radius: 12px;
    font-size: 18px;
    cursor: pointer;
}

button:hover {
    background-color: #ad2168;
}

.result {
    margin-top: 25px;
    font-size: 22px;
    color: #333;
    background: #f0fbff;
    padding: 20px;
    border-radius: 15px;
    line-height: 1.5;
}

.footer {
    margin-top: 25px;
    font-size: 16px;
    color: #333;
    padding: 15px;
}
</style>
</head>

<body>

<!-- الترويسة -->
<div class="header">
    <img src="https://upload.wikimedia.org/wikipedia/ar/thumb/0/02/Ministry_of_Education_Saudi_Arabia_Logo.svg/512px-Ministry_of_Education_Saudi_Arabia_Logo.svg.png">
    <div class="header-text">
        وزارة التعليم<br>
        الإدارة العامة للتعليم بمنطقة نجران
    </div>
</div>

<div class="decor">🌸 🌼 🌺 🎈✨</div>

<div class="container">
<h1>🌟 حاسبة عمر الطفل 🌟</h1>
<div class="subtitle">مرحلة رياض الأطفال</div>

<input type="text" id="childName" placeholder="اسم الطفل">
<br>
<input type="date" id="birthDate">
<br><br>

<button onclick="calculateAge()">احسبي العمر</button>

<div class="result" id="result"></div>

<div class="footer">
🌼 مديرة الروضة ومصممة الموقع 🌼<br>
<strong>فاطمه صالح ال بحري</strong>
</div>
</div>

<script>
// أصوات احتفالية متعددة
const sounds = [
    new Audio('https://www.soundjay.com/buttons/sounds/button-3.mp3'),
    new Audio('https://www.soundjay.com/misc/sounds/bell-ringing-01.mp3'),
    new Audio('https://www.soundjay.com/button/sounds/button-16.mp3')
];

function playRandomSound() {
    const sound = sounds[Math.floor(Math.random() * sounds.length)];
    sound.play();
}

// تحويل الميلادي إلى هجري تقريبي
function toHijri(date) {
    const jd = Math.floor((date / 86400000) - (date.getTimezoneOffset()/1440) + 2440587.5);
    const islamic = Math.floor((jd - 1948440 + 10632) / 10631);
    const year = islamic;
    const month = Math.min(Math.floor((jd - 1948440) % 354 / 29.5) + 1, 12);
    const day = Math.min((jd - 1948440) % 354 % 29.5 + 1, 30);
    return {year, month, day};
}

function calculateAge() {
    const name = document.getElementById("childName").value;
    const birthDate = new Date(document.getElementById("birthDate").value);
    const today = new Date();

    if (!birthDate.getTime()) {
        document.getElementById("result").innerHTML = "الرجاء إدخال تاريخ ميلاد صحيح";
        return;
    }

    let years = today.getFullYear() - birthDate.getFullYear();
    let months = today.getMonth() - birthDate.getMonth();
    let days = today.getDate() - birthDate.getDate();

    if (days < 0) {
        months--;
        days += 30;
    }

    if (months < 0) {
        years--;
        months += 12;
    }

    const hijri = toHijri(birthDate);

    document.getElementById("result").innerHTML =
        `🎈 عمر الطفل <strong>${name}</strong> هو:<br>
        <strong>${years} سنة و ${months} شهر و ${days} يوم</strong><br><br>
        📅 الميلادي: ${birthDate.getDate()}/${birthDate.getMonth()+1}/${birthDate.getFullYear()}<br>
        📅 الهجري (تقريبي): ${hijri.day}/${hijri.month}/${hijri.year}`;

    // تشغيل صوت عشوائي
    playRandomSound();
}
</script>

</body>
</html>
