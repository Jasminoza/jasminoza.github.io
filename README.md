555
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>UUID v4 Generator</title>
  <script src="https://an.yandex.ru/system/context.js"></script>
  <style>
    html { width: 100%; height: 100%; margin: 0; padding: 0; }

    body {
      min-height: 100vh;
      max-width: 1400px; /* ← ШИРЕ для всех экранов */
      margin: 0 auto;
      background: linear-gradient(135deg, #0f0f23 0%, #1a1a2e 50%, #16213e 100%);
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      color: #f8fafc;
      padding: 40px 24px; /* ← Больше padding */
      gap: 24px;
      box-sizing: border-box;
      overflow-x: hidden;
    }

    :root {
      --glass-bg: rgba(255, 255, 255, 0.05);
      --glass-border: rgba(255, 255, 255, 0.1);
      --accent: linear-gradient(135deg, #3b82f6 0%, #8b5cf6 50%, #ec4899 100%);
      --shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
      --app-to-ads-gap: 80px; /* ← Еще больше отступ */
    }

    .main-app {
      flex-shrink: 0;
      width: 100%;
      max-width: 600px; /* ← ШИРЕ приложение */
      display: flex;
      flex-direction: column;
      align-items: center;
      margin: 0 auto;
    }

    .container {
      background: var(--glass-bg);
      backdrop-filter: blur(25px);
      border: 1px solid var(--glass-border);
      border-radius: 24px;
      padding: 48px 40px; /* ← ШИРЕ padding */
      width: 100%;
      box-shadow: var(--shadow);
      text-align: center;
      animation: slideIn 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
      box-sizing: border-box;
    }

    @keyframes slideIn {
      from { opacity: 0; transform: translateY(30px); }
      to { opacity: 1; transform: translateY(0); }
    }

    h1 {
      font-size: clamp(2rem, 5vw, 3rem); /* ← КРУПНЕЕ */
      font-weight: 800;
      background: var(--accent);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 12px;
      letter-spacing: -0.03em;
    }

    .subtitle {
      color: #cbd5e1;
      font-size: 1.2rem; /* ← КРУПНЕЕ */
      margin-bottom: 40px;
      font-weight: 400;
      line-height: 1.5;
      max-width: 500px; /* ← Не растягивается */
      margin-left: auto;
      margin-right: auto;
    }

    /* ✅ UUID: ПОЛНОЕ ПРОСТРАНСТВО */
    #uuid {
      background: var(--glass-bg);
      backdrop-filter: blur(15px);
      border: 2px solid var(--glass-border);
      border-radius: 16px;
      padding: 24px 32px; /* ← ОЧЕНЬ много места */
      margin-bottom: 32px;
      font-size: 1.35rem; /* ← КРУПНЕЕ шрифт */
      font-family: 'SF Mono', Monaco, 'Cascadia Code', monospace;
      font-weight: 500;
      color: #f8fafc;
      width: 100%;
      max-width: 520px; /* ← Шире поле */
      min-width: 360px;
      height: 72px; /* ← Фиксированная высота */
      text-align: center;
      letter-spacing: 0.03em;
      line-height: 1.3;
      transition: all 0.3s ease;
      box-sizing: border-box;
      text-overflow: ellipsis;
      overflow: hidden;
      white-space: nowrap;
      -webkit-appearance: textfield;
      appearance: textfield;
    }

    #uuid:focus {
      outline: none;
      border-color: #3b82f6;
      box-shadow: 0 0 0 4px rgba(59, 130, 246, 0.15);
    }

    button {
      background: var(--accent);
      border: none;
      border-radius: 16px;
      padding: 24px 64px; /* ← КРУПНАЯ кнопка */
      font-size: 1.2rem;
      font-weight: 700;
      color: white;
      cursor: pointer;
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      box-shadow: var(--shadow);
      min-height: 72px;
      width: 100%;
      max-width: 380px;
      box-sizing: border-box;
    }

    button:hover { 
      transform: translateY(-4px); 
      box-shadow: 0 35px 60px -12px rgba(0,0,0,0.4); 
    }
    button:active { transform: translateY(-2px); }

    #status {
      margin-top: 16px;
      font-size: 1.1rem;
      font-weight: 600;
      opacity: 0;
      transform: translateY(10px);
      transition: all 0.4s ease;
      min-height: 28px; /* ← Место для текста */
    }

    #status.show { opacity: 1; transform: translateY(0); }

    .spacer {
      height: var(--app-to-ads-gap); /* ← 80px */
      width: 100%;
      max-width: 600px;
      flex-shrink: 0;
    }

    .ads-section {
      width: 100%;
      max-width: 1200px; /* ← Шире ads */
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 24px;
      margin: 0 auto;
    }

    .ads-container {
      display: flex;
      gap: 32px; /* ← Больше gap между баннерами */
      justify-content: center;
      flex-wrap: wrap;
      width: 100%;
    }

    .ad-slot {
      background: var(--glass-bg) !important;
      backdrop-filter: blur(15px) !important;
      border: 1px solid var(--glass-border) !important;
      border-radius: 16px !important;
      padding: 16px !important;
      box-shadow: var(--shadow) !important;
      overflow: hidden;
      box-sizing: border-box;
    }

    .ad-slot.wide { 
      min-width: 728px; 
      max-width: 728px; 
      height: 90px; 
      flex: 0 0 auto;
    }
    .ad-slot.medium { 
      min-width: 300px; 
      max-width: 300px; 
      height: 250px; 
      flex: 0 0 auto;
    }

    .ad-placeholder {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 8px;
      height: 100%;
      color: #cbd5e1;
      font-weight: 600;
      font-size: 1rem;
    }

    @media (max-width: 768px) {
      body { padding: 24px 16px; gap: 20px; }
      .spacer { height: 60px; }
      .container { padding: 32px 24px; }
      #uuid { 
        font-size: 1.2rem; 
        padding: 20px 28px; 
        height: 64px;
        min-width: unset;
      }
      button { padding: 20px 48px; min-height: 64px; }
      .ads-section, .ads-container { gap: 20px; flex-direction: column; align-items: center; }
      .ad-slot.wide { max-width: 100%; height: 70px; }
      .ad-slot.medium { height: 200px; }
    }
  </style>
</head>
<body>
<div class="particles" id="particles"></div>

<div class="main-app">
  <div class="container">
    <h1>UUID v4 Generator</h1>
    <p class="subtitle">Генерируйте и копируйте уникальные идентификаторы одним кликом</p>

    <input type="text" id="uuid" readonly placeholder="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
           maxlength="36" size="36">

    <button onclick="generateAndCopy()">✨ Сгенерировать & Копировать</button>

    <div id="status"></div>
  </div>
</div>

<div class="spacer"></div>

<div class="ads-section">
  <div class="ads-container">
    <div id="yandex_rtb_widget_1" class="ad-slot medium">
      <div class="ad-placeholder">
        📢 300×250<br>Место для рекламы
      </div>
    </div>
    <div id="yandex_rtb_widget_2" class="ad-slot wide">
      <div class="ad-placeholder">
        📢 728×90<br>Место для рекламы
      </div>
    </div>
  </div>
</div>

<script>
  function generateUUIDv4() { return crypto.randomUUID(); }

  async function generateAndCopy() {
    const uuid = generateUUIDv4();
    const uuidInput = document.getElementById('uuid');
    const status = document.getElementById('status');
    const button = document.querySelector('button');

    uuidInput.value = uuid;
    uuidInput.setAttribute('value', uuid);
    uuidInput.scrollLeft = uuidInput.scrollWidth;

    button.textContent = '✅ Скопировано в буфер!';

    try {
      await navigator.clipboard.writeText(uuid);
      status.innerHTML = '✅ <strong>UUID полностью скопирован!</strong> (36 символов)';
      status.className = 'success show';
    } catch {
      status.innerHTML = '❌ Используйте Ctrl+C';
      status.className = 'error show';
    }

    setTimeout(() => {
      button.textContent = '✨ Сгенерировать & Копировать';
      status.classList.remove('show');
    }, 2500);
  }

  function createParticles() {
    const particles = document.getElementById('particles');
    for (let i = 0; i < 20; i++) {
      const particle = document.createElement('div');
      particle.style.cssText = `
        position: fixed; top: 0; left: ${Math.random() * 100}%;
        width: ${Math.random() * 4 + 2}px; height: ${Math.random() * 4 + 2}px;
        background: rgba(255,255,255,0.4); border-radius: 50%;
        animation: float ${Math.random() * 12 + 18}s linear infinite;
        z-index: -1; pointer-events: none;
      `;
      particles.appendChild(particle);
    }
  }

  const style = document.createElement('style');
  style.textContent = `
    @keyframes float {
      0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
      10% { opacity: 1; }
      90% { opacity: 1; }
      100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
    }
    .success { color: #10b981; }
    .error { color: #ef4444; }
  `;
  document.head.appendChild(style);

  createParticles();
</script>
</body>
</html>