<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>UUID v4 Generator</title>
  <style>
    html { width: 100%; height: 100%; margin: 0; padding: 0; }

    body {
      min-height: 100vh;
      max-width: 1400px;
      margin: 0 auto;
      background: linear-gradient(135deg, #0f0f23 0%, #1a1a2e 50%, #16213e 100%);
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      color: #f8fafc;
      padding: 40px 24px;
      gap: 24px;
      box-sizing: border-box;
      overflow-x: hidden;
    }

    :root {
      --glass-bg: rgba(255, 255, 255, 0.05);
      --glass-border: rgba(255, 255, 255, 0.1);
      --accent: linear-gradient(135deg, #3b82f6 0%, #8b5cf6 50%, #ec4899 100%);
      --shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
    }

    .main-app {
      flex-shrink: 0;
      width: 100%;
      max-width: 600px;
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
      padding: 48px 40px;
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
      font-size: clamp(2rem, 5vw, 3rem);
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
      font-size: 1.2rem;
      margin-bottom: 40px;
      font-weight: 400;
      line-height: 1.5;
      max-width: 500px;
      margin-left: auto;
      margin-right: auto;
    }

    #uuid {
      background: var(--glass-bg);
      backdrop-filter: blur(15px);
      border: 2px solid var(--glass-border);
      border-radius: 16px;
      padding: 20px 5px;
      margin-bottom: 32px;
      font-size: 1.3rem;
      font-family: 'SF Mono', Monaco, 'Cascadia Code', monospace !important;
      font-weight: 500;
      color: #f8fafc;
      width: 100%;
      max-width: 580px;
      height: 80px;
      text-align: center;
      letter-spacing: 0.02em;
      line-height: 1.4;
      transition: all 0.3s ease;
      box-sizing: border-box;
      text-overflow: clip !important;
      overflow: visible !important;
      white-space: normal !important;
      -webkit-appearance: none;
      appearance: none;
      border: none;
    }

    #uuid::placeholder {
      color: #94a3b8;
      opacity: 0.8;
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
      padding: 24px 24px;
      font-size: 1.2rem;
      font-weight: 700;
      color: white;
      cursor: pointer;
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      box-shadow: var(--shadow);
      min-height: 72px;
      width: 100%;
      max-width: 420px;
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
      min-height: 28px;
    }

    #status.show { opacity: 1; transform: translateY(0); }

    /* 🔥 ПОЛНАЯ МОБИЛЬНАЯ АДАПТИВНОСТЬ */

    /* Планшеты (768px - 1024px) */
    @media (max-width: 1024px) and (min-width: 769px) {
      .container { padding: 40px 32px; }
      #uuid { max-width: 500px; }
      button { max-width: 360px; }
    }

    /* Мобильные устройства (≤768px) */
    @media (max-width: 768px) {
      body {
        padding: 20px 16px;
        gap: 20px;
      }

      .container {
        padding: 32px 20px;
        border-radius: 20px;
        margin-bottom: 20px;
      }

      h1 {
        font-size: clamp(1.75rem, 8vw, 2.25rem);
        margin-bottom: 8px;
      }

      .subtitle {
        font-size: 1.1rem;
        margin-bottom: 28px;
        line-height: 1.4;
      }

      #uuid {
        font-size: clamp(1.1rem, 5vw, 1.25rem);
        padding: 20px 28px;
        height: clamp(68px, 12vw, 72px);
        margin-bottom: 24px;
        letter-spacing: 0.01em;
        border-radius: 14px;
      }

      button {
        padding: 20px 32px;
        min-height: clamp(64px, 12vw, 68px);
        max-width: 100%;
        font-size: clamp(1.1rem, 4.5vw, 1.2rem);
        border-radius: 14px;
      }
    }

    /* Маленькие мобильные (≤480px) */
    @media (max-width: 480px) {
      body { padding: 16px 12px; gap: 16px; }

      .container { padding: 28px 16px; }

      #uuid {
        padding: 18px 24px;
        font-size: 1.1rem;
      }

      button { padding: 18px 28px; }

    }

    /* Очень маленькие экраны (≤360px) */
    @media (max-width: 360px) {
      .container { padding: 24px 12px; }
      #uuid { padding: 16px 20px; }
      button { padding: 16px 24px; }
    }

    /* Ландшафтный режим мобильных */
    @media (max-height: 500px) and (orientation: landscape) {
      body { padding: 16px 12px; gap: 12px; }
      .container { padding: 24px 20px; }
      #uuid { height: 60px; padding: 16px 24px; }
      button { min-height: 56px; padding: 16px 24px; }
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
           maxlength="38" size="42">

    <button onclick="generateAndCopy()">✨ Сгенерировать & Копировать</button>

    <div id="status"></div>
  </div>
</div>

<script>
  async function generateAndCopy() {
    const uuid = crypto.randomUUID();
    const uuidInput = document.getElementById('uuid');

    uuidInput.value = uuid;
    uuidInput.setAttribute('value', uuid);

    console.log('UUID length:', uuid.length, uuid);

    const status = document.getElementById('status');
    const button = document.querySelector('button');

    button.textContent = '✅ Скопировано!';

    try {
      await navigator.clipboard.writeText(uuid);
      status.innerHTML = `✅ <strong>${uuid.length} символов</strong> → скопировано!`;
      status.className = 'success show';
    } catch {
      status.innerHTML = '❌ Ctrl+C';
      status.className = 'error show';
    }

    setTimeout(() => {
      button.textContent = '✨ Сгенерировать & Копировать';
      status.classList.remove('show');
    }, 3000);
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
  generateAndCopy();
</script>
</body>
</html>