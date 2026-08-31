<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>⚠️ WARNING: CRITICAL SYSTEM OVERRIDE</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: #020202;
            color: #00ff66;
            font-family: 'Courier New', Courier, monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 15px;
            overflow-x: hidden;
        }

        /* تأثير خطوط الشاشة CRT */
        body::before {
            content: " ";
            display: block;
            position: fixed;
            top: 0; left: 0; bottom: 0; right: 0;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.4) 50%), 
                        linear-gradient(90deg, rgba(255, 0, 0, 0.03), rgba(0, 255, 0, 0.01), rgba(0, 0, 255, 0.03));
            z-index: 10;
            background-size: 100% 3px, 3px 100%;
            pointer-events: none;
        }

        .card {
            border: 1px solid #00ff66;
            padding: 20px;
            border-radius: 8px;
            background-color: rgba(0, 10, 0, 0.9);
            box-shadow: 0 0 30px rgba(0, 255, 102, 0.3);
            max-width: 520px;
            width: 100%;
            text-align: right;
            position: relative;
            z-index: 1;
        }

        .header {
            color: #ff3333;
            font-size: 17px;
            font-weight: bold;
            margin-bottom: 15px;
            text-shadow: 0 0 10px #ff3333;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid #ff3333;
            padding-bottom: 8px;
        }

        .blink {
            animation: blinker 0.8s linear infinite;
        }

        @keyframes blinker {
            50% { opacity: 0; }
        }

        .typing-text {
            font-size: 15px;
            line-height: 1.5;
            min-height: 60px;
            margin-bottom: 15px;
            color: #00ff66;
        }

        /* لوحة بيانات الجهاز */
        .device-info-box {
            border: 1px dashed #00ff66;
            padding: 12px;
            margin-bottom: 15px;
            border-radius: 4px;
            background: rgba(0, 25, 0, 0.6);
            font-size: 12px;
        }

        .device-info-title {
            color: #ffff33;
            margin-bottom: 8px;
            font-weight: bold;
            font-size: 13px;
        }

        .info-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 4px;
        }

        .info-item {
            display: flex;
            justify-content: space-between;
            border-bottom: 1px dotted rgba(0, 255, 102, 0.2);
            padding-bottom: 2px;
            direction: ltr;
        }

        .info-item span:first-child {
            color: #aaa;
        }

        .info-item span:last-child {
            color: #00ff66;
            font-weight: bold;
        }

        /* شريط التقدم */
        .progress-box {
            margin-top: 15px;
        }

        .progress-label {
            font-size: 13px;
            margin-bottom: 5px;
            color: #aaa;
        }

        .progress-bar {
            width: 100%;
            height: 16px;
            background: #111;
            border: 1px solid #00ff66;
            border-radius: 3px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            width: 0%;
            background: #00ff66;
            box-shadow: 0 0 12px #00ff66;
            transition: width 0.1s linear;
        }

        .status-logs {
            font-size: 11px;
            color: #777;
            margin-top: 10px;
            height: 55px;
            overflow: hidden;
            direction: ltr;
            text-align: left;
            background: #000;
            padding: 5px;
            border: 1px solid #113311;
        }
    </style>
</head>
<body>

    <div class="card">
        <div class="header">
            <span>🔴 SYSTEM PENETRATION ACTIVE</span>
            <span class="blink">● LIVE</span>
        </div>
        
        <div class="typing-text" id="typewriter"></div>

        <!-- لوحة عرض بيانات الجهاز الشاملة -->
        <div class="device-info-box">
            <div class="device-info-title">💻 TARGET HARDWARE TELEMETRY:</div>
            <div class="info-grid">
                <div class="info-item"><span>[IP Address]</span><span id="ip-val">Fetching...</span></div>
                <div class="info-item"><span>[Location]</span><span id="loc-val">Locating...</span></div>
                <div class="info-item"><span>[OS / Platform]</span><span id="os-val">Detecting...</span></div>
                <div class="info-item"><span>[Browser Engine]</span><span id="browser-val">Detecting...</span></div>
                <div class="info-item"><span>[Battery Status]</span><span id="battery-val">Reading...</span></div>
                <div class="info-item"><span>[CPU Cores]</span><span id="cpu-val">Counting...</span></div>
                <div class="info-item"><span>[Device Memory]</span><span id="ram-val">Estimating...</span></div>
                <div class="info-item"><span>[Screen Resolution]</span><span id="screen-val">Measuring...</span></div>
                <div class="info-item"><span>[Network Connection]</span><span id="net-val">Checking...</span></div>
                <div class="info-item"><span>[System Language]</span><span id="lang-val">Reading...</span></div>
                <div class="info-item"><span>[Local Timezone]</span><span id="time-val">Syncing...</span></div>
            </div>
        </div>

        <div class="progress-box">
            <div class="progress-label" id="progress-text">Initializing exploit payload... 0%</div>
            <div class="progress-bar">
                <div class="progress-fill" id="fill"></div>
            </div>
        </div>

        <div class="status-logs" id="logs"></div>
    </div>

    <script>
        const text = "جاري فحص جميع المكونات والخصائص البرمجية للجهاز الحالي لإظهارها على الشاشة...";
        let index = 0;
        const speed = 35;

        // توليد نغمات تنبيه إلكترونية (Beep)
        function playBeep(freq = 400, duration = 0.08) {
            try {
                const ctx = new (window.AudioContext || window.webkitAudioContext)();
                const osc = ctx.createOscillator();
                const gain = ctx.createGain();
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(freq, ctx.currentTime);
                gain.gain.setValueAtTime(0.05, ctx.currentTime);
                osc.connect(gain);
                gain.connect(ctx.destination);
                osc.start();
                osc.stop(ctx.currentTime + duration);
            } catch(e) {}
        }

        // جلب وقراءة بيانات الجهاز
        async function fetchSystemData() {
            const ua = navigator.userAgent;

            // 1. نظام التشغيل
            let os = "Unknown OS";
            if (ua.includes("Android")) os = "Android OS";
            else if (ua.includes("iPhone") || ua.includes("iPad")) os = "iOS (Apple)";
            else if (ua.includes("Windows")) os = "Windows OS";
            else if (ua.includes("Mac")) os = "macOS (Apple)";
            else if (ua.includes("Linux")) os = "Linux OS";
            document.getElementById("os-val").innerText = os;

            // 2. المتصفح
            let browser = "Web Browser";
            if (ua.includes("Chrome") && !ua.includes("Edg")) browser = "Google Chrome";
            else if (ua.includes("Firefox")) browser = "Mozilla Firefox";
            else if (ua.includes("Safari") && !ua.includes("Chrome")) browser = "Apple Safari";
            else if (ua.includes("Edg")) browser = "Microsoft Edge";
            document.getElementById("browser-val").innerText = browser;

            // 3. أبعاد الشاشة ودقتها
            document.getElementById("screen-val").innerText = `${window.screen.width} x ${window.screen.height} (Depth: ${window.screen.colorDepth}-bit)`;

            // 4. أنوية المعالج
            document.getElementById("cpu-val").innerText = navigator.hardwareConcurrency ? `${navigator.hardwareConcurrency} Cores` : "N/A";

            // 5. حجم الرام المقدر
            document.getElementById("ram-val").innerText = navigator.deviceMemory ? `~${navigator.deviceMemory} GB` : "Standard";

            // 6. اللغة
            document.getElementById("lang-val").innerText = navigator.language || "ar-SA";

            // 7. المنطقة الزمنية والتوقيت
            const tz = Intl.DateTimeFormat().resolvedOptions().timeZone;
            document.getElementById("time-val").innerText = tz || "Local System Time";

            // 8. نوع الاتصال
            const connection = navigator.connection || navigator.mozConnection || navigator.webkitConnection;
            if (connection) {
                document.getElementById("net-val").innerText = `${connection.effectiveType || 'Online'} (${connection.downlink || '?'} Mbps)`;
            } else {
                document.getElementById("net-val").innerText = navigator.onLine ? "Online (Active)" : "Offline";
            }

            // 9. مستوى البطارية والشاحن
            if (navigator.getBattery) {
                try {
                    const battery = await navigator.getBattery();
                    const updateBattery = () => {
                        const level = Math.round(battery.level * 100);
                        const charging = battery.charging ? "⚡ Charging" : "🔋 Discharging";
                        document.getElementById("battery-val").innerText = `${level}% [${charging}]`;
                    };
                    updateBattery();
                    battery.addEventListener('levelchange', updateBattery);
                    battery.addEventListener('chargingchange', updateBattery);
                } catch(e) {
                    document.getElementById("battery-val").innerText = "Access Restricted";
                }
            } else {
                document.getElementById("battery-val").innerText = "Not Supported";
            }

            // 10. عنوان IP والدولة (عبر API عام وشفاف)
            try {
                const res = await fetch('https://ipapi.co/json/');
                if (res.ok) {
                    const data = await res.json();
                    document.getElementById("ip-val").innerText = data.ip || "Hidden";
                    document.getElementById("loc-val").innerText = `${data.city || ''}, ${data.country_name || ''}`;
                } else {
                    document.getElementById("ip-val").innerText = "Protected IP";
                    document.getElementById("loc-val").innerText = "Protected Location";
                }
            } catch(e) {
                document.getElementById("ip-val").innerText = "127.0.0.1 (Local)";
                document.getElementById("loc-val").innerText = "Unavailable";
            }
        }

        // كتابة النص الهيدر تلقائياً
        function typeWriter() {
            if (index < text.length) {
                document.getElementById("typewriter").innerHTML += text.charAt(index);
                index++;
                setTimeout(typeWriter, speed);
            } else {
                startProgress();
            }
        }

        // شريط التقدم والسجلات
        function startProgress() {
            let width = 0;
            const fill = document.getElementById("fill");
            const label = document.getElementById("progress-text");
            const logs = document.getElementById("logs");

            const logMessages = [
                "> Probing hardware registers...",
                "> Mapping network sockets...",
                "> Querying IP API geolocation...",
                "> Analyzing screen geometry...",
                "> Inspecting power state...",
                "> Telemetry aggregation complete."
            ];

            let logIndex = 0;

            const interval = setInterval(() => {
                if (width >= 100) {
                    clearInterval(interval);
                    label.innerHTML = "<span style='color:#00ff66;'>تم عرض التقرير كاملاً بنجاح ✔️</span>";
                    playBeep(800, 0.2);
                } else {
                    width += 1;
                    fill.style.width = width + '%';
                    label.innerText = `Analyzing system telemetry... ${width}%`;
                    
                    if(width % 16 === 0 && logIndex < logMessages.length) {
                        logs.innerHTML += logMessages[logIndex] + "<br>";
                        logs.scrollTop = logs.scrollHeight;
                        logIndex++;
                        playBeep(450 + (width * 3), 0.05);
                    }
                }
            }, 50);
        }

        window.onload = () => {
            fetchSystemData();
            playBeep(300, 0.1);
            typeWriter();
        };
    </script>
</body>
</html>
