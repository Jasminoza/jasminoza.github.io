<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>UUID v4 Generator</title>

  <!-- ===== ЯНДЕКС РСЯ ЗАГРУЗЧИК (вставьте ваш реальный код) ===== -->
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
      --shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
      --shadow-hover: 0 35px 60px -12px rgba(0, 0, 0, 0.35);
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      margin: -70px !important;
      min-height: 80vh;
      background: var(--bg-primary);
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;  /* ← Прижать к верху */
      gap: 10px;                     /* ← Отступ между элементами */
      color: var(--text-primary);
      overflow-x: hidden;
    }

    .container {
      background: var(--glass-bg);
      backdrop-filter: blur(20px);
      border: 1px solid var(--glass-border);
      border-radius: 24px;
      padding: 48px;
      max-width: 520px;
      width: 100%;
      box-shadow: var(--shadow);
      text-align: center;
      position: relative;
      animation: slideIn 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94);
      margin: 0 !important;         /* ← Убираем лишние отступы */
    }

    @keyframes slideIn {
      from {
        opacity: 0;
        transform: translateY(30px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    h1 {
      font-size: clamp(1.8rem, 4vw, 2.5rem);
      font-weight: 800;
      background: var(--accent);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 12px;
      letter-spacing: -0.02em;
    }

    .subtitle {
      color: var(--text-secondary);
      font-size: 1.1rem;
      margin-bottom: 40px;
      font-weight: 400;
    }

    #uuid {
      background: var(--glass-bg);
      backdrop-filter: blur(10px);
      border: 2px solid var(--glass-border);
      border-radius: 16px;
      padding: 24px;
      margin-bottom: 32px;
      font-size: 1.3rem;
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
      box-shadow: 0 0 0 4px rgba(59, 130, 246, 0.1);
    }

    #uuid::placeholder {
      color: var(--text-secondary);
    }

    button {
      background: var(--accent);
      border: none;
      border-radius: 16px;
      padding: 20px 48px;
      font-size: 1.1rem;
      font-weight: 600;
      color: white;
      cursor: pointer;
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      box-shadow: var(--shadow);
      position: relative;
      overflow: hidden;
      min-height: 64px;
    }

    button::before {
      content: '';
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
      transition: left 0.6s;
    }

    button:hover::before {
      left: 100%;
    }

    button:hover {
      transform: translateY(-4px);
      box-shadow: var(--shadow-hover);
    }

    button:active {
      transform: translateY(-2px);
    }

    #status {
      margin-top: 20px;
      font-size: 1rem;
      font-weight: 500;
      opacity: 0;
      transform: translateY(10px);
      transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    }

    #status.show {
      opacity: 1;
      transform: translateY(0);
    }

    .success { color: var(--success); }
    .error { color: var(--error); }

    /* ===== РЕКЛАМА ===== */
    .ads-container {
      display: flex;
      gap: 24px;
      justify-content: center;
      margin: 0 0 20px 0;          /* ← Только снизу 20px */
      max-width: 1100px;
      flex-wrap: wrap;
    }

    .ad-slot {
      background: var(--glass-bg) !important;
      backdrop-filter: blur(10px) !important;
      border: 1px solid var(--glass-border) !important;
      border-radius: 16px !important;
      padding: 12px !important;
      box-shadow: var(--shadow) !important;
      min-height: 250px;
      position: relative;
      overflow: hidden;
    }

    .ad-slot.wide {
      min-width: 728px;
      max-width: 728px;
      min-height: 90px;
    }
    .ad-slot.medium {
      min-width: 300px;
      max-width: 300px;
      min-height: 250px;
    }

    .ad-placeholder {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 8px;
      height: 100%;
      color: var(--text-secondary);
      font-weight: 500;
      font-size: 0.95rem;
    }

    /* Фикс iframe рекламы */
    .ad-slot iframe {
      border-radius: 12px !important;
      box-shadow: 0 10px 30px rgba(0,0,0,0.3) !important;
      width: 100% !important;
      height: 100% !important;
    }

    @media (max-width: 768px) {
      .container { padding: 32px 24px; margin: 20px; }
      .ads-container { flex-direction: column; align-items: center; gap: 20px; }
      .ad-slot.wide { max-width: 100%; min-height: 90px; }
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

<!-- ===== БЛОКИ РЕКЛАМЫ ===== -->
<div class="ads-container">
  <!-- 300x250 -->
  <div id="yandex_rtb_widget_1" class="ad-slot medium">
    <div class="ad-placeholder">
      📢 Место<br>для рекламы<br>300×250
    </div>
    <!-- ВСТАВЬТЕ КОД РСЯ ЗДЕСЬ:
    <script>Ya.Context.AdvManager.render({blockId: 'R-M-XXXXXX-1', renderTo: 'yandex_rtb_widget_1'});</script>
    -->
  </div>

  <!-- 728x90 -->
  <div id="yandex_rtb_widget_2" class="ad-slot wide">
    <div class="ad-placeholder">
      📢 Место<br>для рекламы<br>728×90
    </div>
    <!-- ВСТАВЬТЕ КОД РСЯ ЗДЕСЬ:
    <script>Ya.Context.AdvManager.render({blockId: 'R-M-XXXXXX-2', renderTo: 'yandex_rtb_widget_2'});</script>
    -->
  </div>
</div>

<script>
  function generateUUIDv4() {
      return crypto.randomUUID();
  }

  async function generateAndCopy() {
      const uuid = generateUUIDv4();
      const uuidInput = document.getElementById('uuid');
      const status = document.getElementById('status');
      const button = document.querySelector('button');

      uuidInput.value = uuid;
      button.textContent = '✅ Скопировано!';

      try {
          await navigator.clipboard.writeText(uuid);
          status.textContent = '✅ UUID скопирован в буфер обмена!';
          status.className = 'success show';
      } catch (err) {
          status.textContent = '❌ Ошибка копирования. Нажмите Ctrl+C';
          status.className = 'error show';
      }

      setTimeout(() => {
          button.textContent = '✨ Сгенерировать & Копировать';
          status.classList.remove('show');
      }, 2000);
  }

  function createParticles() {
      const particles = document.getElementById('particles');
      for (let i = 0; i < 20; i++) {
          const particle = document.createElement('div');
          particle.className = 'particle';
          particle.style.left = Math.random() * 100 + '%';
          particle.style.width = particle.style.height = (Math.random() * 4 + 2) + 'px';
          particle.style.animationDelay = Math.random() * 20 + 's';
          particle.style.animationDuration = (Math.random() * 10 + 15) + 's';
          particles.appendChild(particle);
      }
  }

  // Фикс рекламы
  function fixAdStyles() {
      const ads = document.querySelectorAll('.ad-slot');
      ads.forEach(ad => {
          const observer = new MutationObserver(() => {
              ad.style.background = 'rgba(255,255,255,0.05)';
          });
          observer.observe(ad, { childList: true, subtree: true });
      });
  }

  createParticles();
  window.addEventListener('load', fixAdStyles);
</script>
</body>
</html>
