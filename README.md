# Fatimah-saleh1<script>
// صوت احتفالي عند الحساب
const celebrationAudio = new Audio('https://www.soundjay.com/buttons/sounds/button-3.mp3');

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

    document.getElementById("result").innerHTML =
        `🎈 عمر الطفل <strong>${name}</strong> هو:<br>
        <strong>${years} سنة و ${months} شهر و ${days} يوم</strong>`;

    // تشغيل الصوت الاحتفالي
    celebrationAudio.play();
}
</script>