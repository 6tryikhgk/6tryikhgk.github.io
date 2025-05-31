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

  // القسم الأول: نظام التشغيل والمتصفح
  const section1 = addSection("🎯 القسم الأول: نظام التشغيل والمتصفح");
  addRow(section1, "navigator.userAgent", navigator.userAgent, "نوع النظام والمتصفح");
  addRow(section1, "navigator.platform", navigator.platform, "يحدد ويندوز، لينوكس، إلخ");
  addRow(section1, "navigator.vendor", navigator.vendor, "تلميح عن المتصفح الحقيقي");
  addRow(section1, "navigator.appVersion", navigator.appVersion, "إصدار المتصفح");
  addRow(section1, "navigator.hardwareConcurrency", navigator.hardwareConcurrency || "غير مدعوم", "عدد أنوية المعالج");
  addRow(section1, "navigator.deviceMemory", navigator.deviceMemory || "غير مدعوم", "حجم الذاكرة العشوائية (RAM) بالجيجابايت");

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
  addRow(section1, "Canvas Fingerprint (Base64)", `<textarea style="width:100%;height:50px;">${getCanvasFingerprint()}</textarea>`, "بصمة رسومية فريدة");

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
          const data = buffer.getChannelData(0);
          for (let i = 4500; i < 5000; i++) fingerprint += Math.abs(data[i]);
          resolve(fingerprint.toString());
        }).catch(() => resolve("خطأ"));
      });
    } catch {
      return Promise.resolve("خطأ");
    }
  }
  addRow(section1, "Audio Fingerprint", "جارٍ التحميل...", "بصمة صوتية فريدة (بدون صوت مسموع)");

  // القسم الثاني: شاشة العرض والجرافيكس
  const section2 = addSection("🖼️ القسم الثاني: شاشة العرض والجرافيكس");
  addRow(section2, "screen.width", screen.width, "عرض شاشة العرض");
  addRow(section2, "screen.height", screen.height, "ارتفاع شاشة العرض");
  addRow(section2, "screen.colorDepth", screen.colorDepth, "عمق ألوان الشاشة");
  addRow(section2, "window.devicePixelRatio", window.devicePixelRatio, "معدل بيكسل الجهاز");
  addRow(section2, "screen.availWidth", screen.availWidth, "العرض المتاح");
  addRow(section2, "screen.availHeight", screen.availHeight, "الارتفاع المتاح");
  addRow(section2, "screen.orientation.type", (screen.orientation && screen.orientation.type) || "غير مدعوم", "اتجاه الجهاز");

  // WebGL Parameters
  addRow(section2, "WebGL Vendor", webglInfo.vendor, "بصمة GPU دقيقة");
  addRow(section2, "WebGL Renderer", webglInfo.renderer, "بصمة GPU دقيقة");

  // القسم الثالث: قدرات النظام والمستعرض
  const section3 = addSection("🧪 القسم الثالث: قدرات النظام والمستعرض");
  addRow(section3, "دعم WebGL", !!webglInfo.vendor, "هل يدعم WebGL");
  addRow(section3, "دعم WebRTC", !!(window.RTCPeerConnection || window.webkitRTCPeerConnection), "هل يدعم WebRTC");
  addRow(section3, "دعم AudioContext", !!(window.AudioContext || window.webkitAudioContext), "هل يدعم AudioContext");
  addRow(section3, "دعم canvas", !!document.createElement("canvas").getContext("2d"), "هل يدعم canvas");
  addRow(section3, "دعم IndexedDB", !!window.indexedDB, "هل يدعم IndexedDB");
  addRow(section3, "دعم touch screen", "ontouchstart" in window, "هل الجهاز يعمل باللمس");
  addRow(section3, "دعم Battery API", !!navigator.getBattery, "هل يدعم بطارية API");

  // القسم الرابع: الشبكة والموقع (IP + Geo)
  const section4 = addSection("🌐 القسم الرابع: الشبكة والموقع");
  async function getIPInfo() {
    try {
      const res = await fetch("https://ipapi.co/json/");
      if (!res.ok) throw new Error("فشل جلب IP");
      const data = await res.json();
      return data;
    } catch {
      return null;
    }
  }
  const ipData = await getIPInfo();
  addRow(section4, "IP Address", ipData?.ip || "غير متوفر", "عنوان IP");
  addRow(section4, "Country", ipData?.country_name || "غير متوفر", "الدولة");
  addRow(section4, "Region", ipData?.region || "غير متوفر", "المنطقة");
  addRow(section4, "City", ipData?.city || "غير متوفر", "المدينة");
  addRow(section4, "ISP", ipData?.org || "غير متوفر", "مزود الخدمة");

  // القسم الخامس: الإعدادات الإقليمية والوقت
  const section5 = addSection("📅 القسم الخامس: الإعدادات الإقليمية والوقت");
  addRow(section5, "navigator.language", navigator.language, "لغة الجهاز");
  addRow(section5, "navigator.languages", navigator.languages.join(", "), "جميع اللغات المفضلة");
  addRow(section5, "Intl.DateTimeFormat().resolvedOptions().timeZone", Intl.DateTimeFormat().resolvedOptions().timeZone, "التوقيت المحلي");
  const offset = new Date().getTimezoneOffset();
  addRow(section5, "UTC Timezone offset (minutes)", offset, "فرق التوقيت عن UTC بالدقائق");
  addRow(section5, "Date.now()", Date.now(), "الوقت الحالي بالنظام (ميلي ثانية منذ 1970)");

  // القسم السادس: الخصوصية والتعقب
  const section6 = addSection("🔥 القسم السادس: الخصوصية والتعقب");
  addRow(section6, "هل المتصفح Headless", navigator.webdriver ? "نعم" : "لا", "هل المتصفح بدون واجهة مستخدم");
  addRow(section6, "هل داخل iframe", window.self !== window.top ? "نعم" : "لا", "هل الصفحة داخل iframe");
  addRow(section6, "FingerprintJS ID", "تحتاج مكتبة FingerprintJS", "معرف فريد لتتبع");

  // القسم السابع: التخزين والتفاعل
  const section7 = addSection("💾 القسم السابع: التخزين والتفاعل");
  if(navigator.storage && navigator.storage.estimate) {
    const storageEstimate = await navigator.storage.estimate();
    addRow(section7, "Storage Quota (بايت)", storageEstimate.quota || "غير متوفر", "حجم التخزين المسموح");
    addRow(section7, "Storage Usage (بايت)", storageEstimate.usage || "غير متوفر", "حجم التخزين المستخدم");
  } else {
    addRow(section7, "Storage API", "غير مدعوم", "");
  }
  addRow(section7, "Cookies Enabled", navigator.cookieEnabled, "هل ملفات الكوكيز مفعلة");
  addRow(section7, "Do Not Track", navigator.doNotTrack || "غير متوفر", "هل المستخدم طلب عدم التتبع");

  // تحميل الـ Audio Fingerprint واستبدال النص
  getAudioFingerprint().then(fp => {
    const rows = document.querySelectorAll("#output section:nth-child(1) tbody tr");
    for (const row of rows) {
      if (row.firstChild.textContent.includes("Audio Fingerprint")) {
        row.children[1].textContent = fp;
        break;
      }
    }
  });

})();
</script>

</body>
</html>
