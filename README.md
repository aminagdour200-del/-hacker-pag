<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تنبيه أمني عاجل</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: #050505;
            color: #00ff66;
            font-family: 'Courier New', Courier, monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
            overflow: hidden;
        }

        body::before {
            content: " ";
            display: block;
            position: absolute;
            top: 0; left: 0; bottom: 0; right: 0;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.3) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.05), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.05));
            z-index: 2;
            background-size: 100% 2px, 3px 100%;
            pointer-events: none;
        }

        .card {
            border: 1px solid #00ff66;
            padding: 25px;
            border-radius: 10px;
            background-color: rgba(0, 15, 0, 0.85);
            box-shadow: 0 0 25px rgba(0, 255, 102, 0.4);
            max-width: 450px;
            width: 100%;
            text-align: right;
            position: relative;
            z-index: 1;
        }

        .header {
            color: #ff3333;
            font-size: 20px;
            font-weight: bold;
            margin-bottom: 15px;
            text-shadow: 0 0 8px #ff3333;
        }

        .typing-text {
            font-size: 17px;
            line-height: 1.6;
            margin-bottom: 15px;
        }

        /* تنسيق جدول المعلومات الشخصية */
        .device-info {
            border: 1px dashed #00ff66;
            background-color: rgba(0, 30, 0, 0.5);
            padding: 10px;
            margin-top: 15px;
            border-radius: 5px;
            font-size: 13px;
            color: #00ff66;
        }

        .device-info p {
            margin: 5px 0;
        }

        .highlight-info {
            color: #ff3333;
            font-weight: bold;
        }

        .progress-box {
            margin-top: 15px;
        }

        .progress-label {
            font-size: 14px;
            margin-bottom: 5px;
            color: #aaa;
        }

        .progress-bar {
            width: 100%;
            height: 15px;
            background: #111;
            border: 1px solid #00ff66;
            border-radius: 3px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            width: 0%;
            background: #00ff66;
            box-shadow: 0 0 10px #00ff66;
            transition: width 0.2s ease;
        }

        .status-logs {
            font-size: 12px;
            color: #888;
            margin-top: 10px;
            height: 40px;
            overflow: hidden;
        }
    </style>
</head>
<body>

    <div class="card">
        <div class="header">
            ⚠️ SYSTEM BREACH DETECTED
        </div>
        
        <div class="typing-text" id="typewriter"></div>

        <!-- قسم عرض معلومات الزائر محلياً -->
        <div class="device-info" id="info-box" style="display:none;">
            <p><strong>📱 نوع النظام:</strong> <span id="user-os" class="highlight-info">جاري الفحص...</span></p>
            <p><strong>🌐 المتصفح:</strong> <span id="user-browser" class="highlight-info">جاري الفحص...</span></p>
            <p><strong>📍 عنوان الـ IP:</strong> <span id="user-ip" class="highlight-info">جاري السحب...</span></p>
        </div>

        <div class="progress-box">
            <div class="progress-label" id="progress-text">جاري بدء اختراق الجهاز... 0%</div>
            <div class="progress-bar">
                <div class="progress-fill" id="fill"></div>
            </div>
        </div>

        <div class="status-logs" id="logs"></div>
    </div>

    <script>
        const text = "مبارك! تم تسجيل الهكر، تم الدخول إلى هاتفك... والآن أنت تشترك معنا في التحكم بهاتفك!";
        let index = 0;
        
        // جلب معلومات المتصفح والنظام محلياً
        function getDeviceInfo() {
            const ua = navigator.userAgent;
            let os = "غير معروف";
            let browser = "غير معروف";

            if (ua.indexOf("Android") >= 0) os = "Android الهاتف";
            else if (ua.indexOf("iPhone") >= 0) os = "iOS (iPhone)";
            else if (ua.indexOf("Windows") >= 0) os = "Windows الكمبيوتر";

            if (ua.indexOf("Chrome") >= 0) browser = "Google Chrome";
            else if (ua.indexOf("Safari") >= 0) browser = "Safari";
            else if (ua.indexOf("Firefox") >= 0) browser = "Firefox";

            document.getElementById("user-os").innerText = os;
            document.getElementById("user-browser").innerText = browser;

            // جلب الـ IP العام عبر API مجاني محلياً وعرضه فقط على شاشته
            fetch('https://api.ipify.org?format=json')
                .then(res => res.json())
                .then(data => {
                    document.getElementById("user-ip").innerText = data.ip;
                })
                .catch(() => {
                    document.getElementById("user-ip").innerText = "192.168.1.1 (افتراضي)";
                });
        }

        function typeWriter() {
            if (index < text.length) {
                document.getElementById("typewriter").innerHTML += text.charAt(index);
                index++;
                setTimeout(typeWriter, 40);
            } else {
                document.getElementById("info-box").style.display = "block";
                startProgress();
            }
        }

        function startProgress() {
            let width = 0;
            const fill = document.getElementById("fill");
            const label = document.getElementById("progress-text");
            const logs = document.getElementById("logs");

            const logMessages = [
                "> IP address target logged.",
                "> Device screen resolution extracted.",
                "> Remote system access granted 100%"
            ];

            let logIndex = 0;

            const interval = setInterval(() => {
                if (width >= 100) {
                    clearInterval(interval);
                    label.innerHTML = "<span style='color:#00ff66;'>تمت السيطرة الكاملة على الشاشة! 🎯</span>";
                } else {
                    width += 2;
                    fill.style.width = width + '%';
                    label.innerText = `سحب بيانات الهاتف... ${width}%`;
                    
                    if(width % 35 === 0 && logIndex < logMessages.length) {
                        logs.innerHTML += logMessages[logIndex] + "<br>";
                        logIndex++;
                    }
                }
            }, 70);
        }

        window.onload = () => {
            getDeviceInfo();
            typeWriter();
        };
    </script>
</body>
</html> -hacker-pag
