<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>حساب عمر الطفل - إدارة تعليم نجران</title>
    <style>
        /* إعدادات الخط والخلفية */
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            /* صورة خلفية طفل بحقيبة وأزهار مع طبقة حماية للنصوص */
            background: linear-gradient(rgba(255, 255, 255, 0.7), rgba(255, 255, 255, 0.7)), 
                        url('https://img.freepik.com/free-photo/boy-with-backpack-flowers_23-2148210364.jpg'); 
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            background-repeat: no-repeat;
        }

        .container {
            background-color: rgba(255, 255, 255, 0.95);
            padding: 35px;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            width: 90%;
            max-width: 480px;
            text-align: center;
            border-top: 10px solid #1a5e37; /* لون أخضر رسمي */
        }

        /* تنسيق الرأس الجديد */
        .header {
            border-bottom: 2px solid #f0f0f0;
            margin-bottom: 25px;
            padding-bottom: 15px;
        }
        .header img { 
            width: 130px; 
            margin-bottom: 10px; 
        }
        .header h2 { 
            color: #1a5e37; 
            margin: 5px 0; 
            font-size: 1.4em;
        }
        .header h3 { 
            color: #444; 
            margin: 5px 0; 
            font-size: 1.1em;
            font-weight: normal;
        }

        h1 {
            font-size: 1.6em;
            color: #2c3e50;
            margin-bottom: 20px;
        }

        .input-group {
            background: #f9fbf9;
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 25px;
            border: 1px solid #e0e0e0;
        }
        label { 
            display: block; 
            margin-bottom: 12px; 
            font-weight: bold; 
            color: #333;
        }
        input[type="date"] {
            padding: 12px;
            width: 85%;
            border: 2px solid #cbd5e0;
            border-radius: 10px;
            font-size: 18px;
            text-align: center;
            outline: none;
        }

        .btn-container {
            display: flex;
            gap: 12px;
            justify-content: center;
        }
        button {
            padding: 14px 25px;
            font-size: 17px;
            border-radius: 10px;
            cursor: pointer;
            border: none;
            transition: 0.3s;
            font-weight: bold;
            flex: 1;
        }
        .btn-calc { background-color: #27ae60; color: white; }
        .btn-calc:hover { background-color: #1e8449; }
        .btn-print { background-color: #2980b9; color: white; }
        .btn-print:hover { background-color: #1f6391; }

        #result {
            margin-top: 25px;
            padding: 20px;
            background-color: #e8f5e9;
            border-radius: 12px;
            border-right: 6px solid #27ae60;
            display: none;
            font-size: 1.1em;
            line-height: 1.6;
            color: #1b5e20;
        }

        /* تنسيق التذييل المطلوب */
        .footer {
            margin-top: 35px;
            padding-top: 20px;
            border-top: 1px solid #eee;
            color: #555;
            font-size: 1em;
        }
        .footer strong {
            display: block;
            margin-top: 8px;
            color: #1a5e37;
            font-size: 1.1em;
        }

        @media print {
            body { background: white !important; }
            .container { box-shadow: none; border: 1px solid #ccc; }
            button { display: none; }
        }
    </style>
</head>
<body>

<div class="container">
    <div class="header">
        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/11/Ministry_of_Education_Saudi_Arabia_Logo.svg/512px-Ministry_of_Education_Saudi_Arabia_Logo.svg.png" alt="شعار وزارة التعليم">
        <h2>وزارة التعليم</h2>
        <h3>إدارة التعليم بنجران</h3>
    </div>

    <h1>حساب عمر الطفل</h1>
    
    <div class="input-group">
        <label>يرجى اختيار تاريخ ميلاد الطفل:</label>
        <input type="date" id="birth_date">
    </div>

    <div class="btn-container">
        <button class="btn-calc" onclick="calculateAge()">عرض النتيجة</button>
        <button class="btn-print" onclick="window.print()">🖨️ طباعة</button>
    </div>

    <div id="result"></div>

    <div class="footer">
        المديرة ومصممة الموقع:
        <strong>فاطمه صالح آل بحري</strong>
    </div>
</div>

<script>
    function calculateAge() {
        const birthValue = document.getElementById('birth_date').value;
        const resultDiv = document.getElementById('result');
        
        if (!birthValue) {
            alert("فضلاً، اختر تاريخ ميلاد الطفل");
            return;
        }

        const birthDate = new Date(birthValue);
        const today = new Date();
        
        let years = today.getFullYear() - birthDate.getFullYear();
        let months = today.getMonth() - birthDate.getMonth();

        if (months < 0 || (months === 0 && today.getDate() < birthDate.getDate())) {
            years--;
            months += 12;
        }

        let level = "";
        if (years < 3) level = "دون سن القبول النظامي";
        else if (years == 3) level = "المستوى الأول (روضة 1)";
        else if (years == 4) level = "المستوى الثاني (روضة 2)";
        else if (years == 5) level = "المستوى الثالث (روضة 3)";
        else level = "مؤهل للمرحلة الابتدائية";

        resultDiv.style.display = "block";
        resultDiv.innerHTML = `
            <strong>النتيجة المستخلصة:</strong><br>
            عمر الطفل الآن: ${years} سنوات و ${months} أشهر<br>
            المرحلة المستحقة: ${level}
        `;
    }
</script>

</body>
</html>
