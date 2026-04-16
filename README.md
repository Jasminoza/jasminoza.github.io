<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>UUID v4 Generator</title>
  <script src="https://an.yandex.ru/system/context.js"></script>
  <style>
    :root {
      --bg-primary: linear-gradient(135deg, #0f0f23 0%, #1a1a2e 50%, #16213e 100%);
      --glass-bg: rgba(255, 255, 255, 0.05);
      --glass-border: rgba(255, 255, 255, 0.1);
      --text-primary: #f8fafc;
      --text-secondary: #cbd5e1;
      --accent: linear-gradient(135deg, #3b82f6 0%, #8b5cf6 50%, #ec4899 100%);
      --success: #10b981;
      --error: #ef4444;
      --shadow: 0 20px 40px -12px rgba(0, 0, 0, 0.25);
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      min-height: 100vh; /* ← Полная высота viewport */
      background: var(--bg-primary);
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      color: var(--text-primary);
      padding: 20px; /* ← Минимальные отступы */
      gap: 16px; /* ← Уменьшенный gap */
      overflow-x: hidden;
    }

    .container {
      background: var(--glass-bg);
      backdrop-filter: blur(20px);
      border: 1px solid var(--glass-border);
      border-radius: 20px;
      padding: 32px 28px; /* ← Уменьшены отступы: 32px сверху/снизу, 28px слева/справа */
      max-width: 480px; /* ← Немного уже */
      width: 100%;
      box-shadow: var(--shadow);
      text-align: center;
      animation: slideIn 0.6s ease-out;
    }

    @keyframes slideIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    h1 {
      font-size: clamp(1.6rem, 3.5vw, 2.2rem); /* ← Уменьшен размер */
      font-weight: 800;
      background: var(--accent);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 8px; /* ← Меньше отступ */
      letter-spacing: -0.02em;
    }

    .subtitle {
      color: var(--text-secondary);
      font-size: 1rem; /* ← Уменьшен */
      margin-bottom: 28px; /* ← Уменьшен */
      font-weight: 400;
      line-height: 1.4;
    }

    #uuid {
      background: var(--glass-bg);
      backdrop-filter: blur(10px);
      border: 2px solid var(--glass-border);
      border-radius: 12px;
      padding: 18px; /* ← Уменьшен padding */
      margin-bottom: 24px;
      font-size: 1.15rem; /* ← Немного меньше */
      font-family: 'SF Mono', Monaco, 'Cascadia Code', monospace;
      font-weight: 500;
      color: var(--text-primary);
      width: 100%;
      text-align: center;
      letter-spacing: 0.02em;
      transition: all 0.3s ease;
    }

    #uuid:focus {
      outline: none;
      border-color: #3b82f6;
      box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
    }

    button {
      background: var(--accent);
      border: none;
      border-radius: 14px;
      padding: 16px 36px; /* ← Уменьшен: 16px высота, 36px ширина */
      font-size: 1rem;
      font-weight: 600;
      color: white;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: var(--shadow);
      min-height: 56px; /* ← Меньше высота */
    }

    button:hover { transform: translateY(-2px); box-shadow: 0 25px 50px -12px rgba(0,0,0,0.35); }
    button:active { transform: translateY(0); }

    #status {
      margin-top: 12px; /* ← Меньше отступ */
      font-size: 0.95rem;
      font-weight: 500;
      opacity: 0;
      transform: translateY(8px);
      transition: all 0.3s ease;
    }

    #status.show { opacity: 1; transform: translateY(0); }

    /* ===== РЕКЛАМА: Компактная версия ===== */
    .ads-container {
      display: flex;
      gap: 16px; /* ← Уменьшен gap */
      justify-content: center;
      margin-bottom: 12px; /* ← Минимальный отступ снизу */
      max-width: 1000px; /* ← Шире для экранов */
      flex-wrap: wrap;
    }

    .ad-slot {
      background: var(--glass-bg) !important;
      backdrop-filter: blur(10px) !important;
      border: 1px solid var(--glass-border) !important;
      border-radius: 12px !important;
      padding: 8px !important; /* ← Минимальный padding */
      box-shadow: var(--shadow) !important;
      overflow: hidden;
    }

    .ad-slot.wide {
      min-width: 728px;
      max-width: 728px;
      height: 80px; /* ← Фиксированная компактная высота */
    }
    .ad-slot.medium {
      min-width: 300px;
      max-width: 300px;
      height: 200px; /* ← Уменьшена высота */
    }

    .ad-placeholder {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 4px;
      height: 100%;
      color: var(--text-secondary);
      font-weight: 500;
      font-size: 0.85rem;
    }

    .ad-slot iframe {
      border-radius: 10px !important;
      box-shadow: 0 8px 25px rgba(0,0,0,0.3) !important;
      width: 100% !important;
      height: 100% !important;
    }

    @media (max-width: 768px) {
      body { padding: 12px; gap: 12px; }
      .container { padding: 24px 20px; margin: 0; }
      .ads-container { 
        flex-direction: column; 
        align-items: center; 
        gap: 12px; 
        width: 100%; 
      }
      .ad-slot.wide { 
        max-width: 100%; 
        height: 60px; /* ← Еще компактнее на мобиле */
      }
      .ad-slot.medium { height: 160px; }
    }

    @media (max-width: 480px) {
      .ads-container { gap: 8px; }
      h1 { font-size: 1.8rem; }
      .subtitle { font-size: 0.95rem; margin-bottom: 20px; }
    }
  </style>
</head>
<body>
<div class="particles" id="particles"></div>

<div class="container">
  <h1>UUID v4 Generator</h1>
  <p class="subtitle">Генерируйте и копируйте уникальные идентификаторы одним кликом</p>

  <input type="text" id="uuid" readonly placeholder="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx">

  <button onclick="generateAndCopy()">
    ✨ Сгенерировать & Копировать
  </button>

  <div id="status"></div>
</div>

<!-- БЛОКИ РЕКЛАМЫ -->
<div class="ads-container">
  <div id="yandex_rtb_widget_1" class="ad-slot medium">
    <div class="ad-placeholder">
      📢 Место<br>для рекламы<br>300×200
    </div>
  </div>

  <div id="yandex_rtb_widget_2" class="ad-slot wide">
    <div class="ad-placeholder">
      📢 Место<br>для рекламы<br>728×80
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
    button.textContent = '✅ Скопировано!';

    try {
      await navigator.clipboard.writeText(uuid);
      status.textContent = '✅ UUID скопирован!';
      status.className = 'success show';
    } catch {
      status.textContent = '❌ Ctrl+C вручную';
      status.className = 'error show';
    }

    setTimeout(() => {
      button.textContent = '✨ Сгенерировать & Копировать';
      status.classList.remove('show');
    }, 1800);
  }

  function createParticles() {
    const particles = document.getElementById('particles');
    for (let i = 0; i < 15; i++) { // ← Меньше частиц
      const particle = document.createElement('div');
      particle.className = 'particle';
      particle.style.cssText = `
        position: fixed; top: 0; left: ${Math.random() * 100}%;
        width: ${Math.random() * 3 + 1}px; height: ${Math.random() * 3 + 1}px;
        background: rgba(255,255,255,0.3); border-radius: 50%;
        animation: float ${Math.random() * 10 + 15}s linear infinite;
        z-index: -1;
      `;
      particles.appendChild(particle);
    }
  }

  const floatStyle = document.createElement('style');
  floatStyle.textContent = `
    @keyframes float {
      0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
      10% { opacity: 1; }
      90% { opacity: 1; }
      100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
    }
    .particle { pointer-events: none; }
  `;
  document.head.appendChild(floatStyle);

  createParticles();
</script>
</body>
</html>
