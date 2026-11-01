<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>JUBA STUDIOS // Digital Engineering & Media</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,300..800;1,300..800&family=Syne:wght@700;800&display=swap" rel="stylesheet">

  <style>
    :root {
      --bg: #09090b;
      --bg-2: #111214;
      --surface: rgba(18, 18, 22, 0.8);
      --surface-strong: #121216;
      --surface-border: rgba(255,255,255,0.09);
      --text: #f4f4f5;
      --muted: #a1a1aa;
      --accent: #22c55e;
      --accent-2: #7ef0ae;
      --accent-dim: rgba(34, 197, 94, 0.12);
      --shadow: 0 20px 60px rgba(0,0,0,0.35);
      --radius: 20px;
      --font-display: 'Syne', sans-serif;
      --font-mono: 'JetBrains Mono', monospace;
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    html { scroll-behavior: smooth; }

    body {
      background:
        radial-gradient(circle at top left, rgba(34,197,94,0.10), transparent 22%),
        radial-gradient(circle at right center, rgba(34,197,94,0.07), transparent 25%),
        var(--bg);
      color: var(--text);
      font-family: var(--font-mono);
      line-height: 1.5;
      padding: 0 1.25rem;
      -webkit-font-smoothing: antialiased;
      overflow-x: hidden;
    }

    body::before {
      content: "";
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(255,255,255,0.022) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,255,255,0.022) 1px, transparent 1px);
      background-size: 38px 38px;
      mask-image: radial-gradient(circle at center, black 55%, transparent 100%);
      pointer-events: none;
      z-index: 0;
    }

    a { color: var(--accent); text-decoration: none; }
    a:hover { text-decoration: underline; }

    h1, h2, h3 {
      font-family: var(--font-display);
      font-weight: 800;
      letter-spacing: -0.05em;
      line-height: 0.98;
      text-transform: uppercase;
    }

    .container {
      position: relative;
      z-index: 1;
      max-width: 1100px;
      margin: 0 auto;
      padding: 2rem 0 5rem;
    }

    .page-section {
      display: none;
      opacity: 0;
      transform: translateY(18px);
      transition: opacity .4s ease, transform .4s ease;
      padding: 1.5rem 0 2.75rem;
    }

    .page-section.active {
      display: block;
      opacity: 1;
      transform: translateY(0);
    }

    .reveal {
      opacity: 0;
      transform: translateY(20px) scale(0.98);
      transition: opacity .7s ease, transform .7s ease;
    }

    .reveal.visible {
      opacity: 1;
      transform: translateY(0) scale(1);
    }

    .floating-orb {
      position: fixed;
      border-radius: 50%;
      filter: blur(24px);
      opacity: 0.18;
      pointer-events: none;
      z-index: 0;
      animation: floatOrb 12s ease-in-out infinite alternate;
    }

    .orb-one { width: 260px; height: 260px; background: #22c55e; top: 10%; left: 8%; }
    .orb-two { width: 360px; height: 360px; background: #14532d; right: 9%; top: 25%; animation-delay: 1.5s; }
    .orb-three { width: 200px; height: 200px; background: #84cc16; bottom: 8%; left: 18%; animation-delay: 3s; }

    @keyframes floatOrb {
      0% { transform: translate3d(0, 0, 0) scale(1); }
      50% { transform: translate3d(28px, -18px, 0) scale(1.08); }
      100% { transform: translate3d(-20px, 18px, 0) scale(0.96); }
    }

    header {
      position: sticky;
      top: 0;
      z-index: 40;
      backdrop-filter: blur(10px);
      background: rgba(9, 9, 11, 0.7);
      border-bottom: 1px solid var(--surface-border);
      max-width: 1100px;
      margin: 0 auto;
    }

    .header-inner {
      max-width: 1100px;
      margin: 0 auto;
      padding: 1.1rem 0.5rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 1rem;
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 0.6rem;
      font-family: var(--font-display);
      font-size: clamp(1rem, 2vw, 1.5rem);
      font-weight: 800;
      letter-spacing: -0.06em;
      color: #fff;
    }

    .logo span {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      background: var(--accent);
      color: #000;
      padding: 0.18rem 0.5rem;
      font-size: 0.72rem;
      font-family: var(--font-mono);
      letter-spacing: 0.05em;
      font-weight: 700;
    }

    .menu-toggle {
      border: 1px solid var(--surface-border);
      background: rgba(255,255,255,0.01);
      color: var(--text);
      padding: 0.7rem 0.9rem;
      cursor: pointer;
      font-family: var(--font-mono);
      font-size: 0.8rem;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      transition: transform 0.2s ease, border-color 0.2s ease, background 0.2s ease;
    }

    .menu-toggle:hover {
      transform: translateY(-1px);
      border-color: var(--accent);
      background: rgba(34,197,94,0.06);
    }

    .nav-menu {
      position: fixed;
      top: 0;
      right: -100%;
      width: min(340px, 100vw);
      height: 100vh;
      background: rgba(18, 18, 22, 0.96);
      border-left: 1px solid var(--surface-border);
      box-shadow: var(--shadow);
      padding: 5rem 1.2rem 1.5rem;
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
      transition: right 0.25s cubic-bezier(.22,1,.36,1);
      z-index: 60;
    }

    .nav-menu.open { right: 0; }

    .nav-menu button {
      background: transparent;
      border: 1px solid transparent;
      color: var(--muted);
      text-align: left;
      padding: 0.9rem 1rem;
      font-family: var(--font-mono);
      font-size: 0.88rem;
      text-transform: uppercase;
      cursor: pointer;
      transition: all 0.15s ease;
      letter-spacing: 0.03em;
    }

    .nav-menu button:hover {
      color: var(--text);
      border-color: var(--surface-border);
      background: rgba(255,255,255,0.02);
    }

    .nav-menu button.active {
      background: var(--accent-dim);
      border-color: rgba(34,197,94,0.45);
      color: var(--accent-2);
      box-shadow: inset 0 0 0 1px rgba(34,197,94,0.15);
    }

    .nav-menu .back-btn {
      margin-top: auto;
      text-align: center;
      border-color: var(--surface-border) !important;
      color: var(--text) !important;
    }

    .overlay {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.75);
      backdrop-filter: blur(3px);
      opacity: 0;
      pointer-events: none;
      transition: opacity .2s ease;
      z-index: 50;
    }

    .overlay.active { opacity: 1; pointer-events: auto; }

    .hero {
      padding-top: 2rem;
      padding-bottom: 1rem;
    }

    .eyebrow {
      display: inline-flex;
      align-items: center;
      gap: 0.65rem;
      border: 1px solid var(--surface-border);
      background: rgba(18,18,22,0.7);
      padding: 0.55rem 0.9rem;
      font-size: 0.74rem;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      color: var(--text);
      margin-bottom: 1.5rem;
      box-shadow: inset 0 0 0 1px rgba(255,255,255,0.02);
    }

    .status-dot {
      width: 9px;
      height: 9px;
      border-radius: 50%;
      background: var(--accent);
      box-shadow: 0 0 10px rgba(34,197,94,0.9);
      animation: pulse 2s ease-in-out infinite;
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); opacity: 1; }
      50% { transform: scale(1.5); opacity: 0.7; }
    }

    .hero h1 {
      max-width: 760px;
      font-size: clamp(2.8rem, 7vw, 5.4rem);
      margin-bottom: 1.2rem;
      color: #fff;
      text-shadow: 0 0 32px rgba(34,197,94,0.07);
    }

    .hero p {
      max-width: 660px;
      color: var(--muted);
      font-size: 1.04rem;
      margin-bottom: 1.5rem;
    }

    .hero-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 1rem;
      margin-top: 2.3rem;
    }

    .hero-link-card {
      position: relative;
      background: linear-gradient(180deg, rgba(18,18,22,0.95), rgba(13,13,16,0.95));
      border: 1px solid var(--surface-border);
      padding: 1.5rem 1.25rem;
      border-radius: var(--radius);
      cursor: pointer;
      transition: transform 0.2s ease, border-color 0.2s ease, box-shadow 0.2s ease;
      overflow: hidden;
      min-height: 190px;
    }

    .hero-link-card::before {
      content: "";
      position: absolute;
      inset: 0;
      background: linear-gradient(135deg, rgba(34,197,94,0.10), transparent 50%);
      opacity: 0;
      transition: opacity 0.2s ease;
    }

    .hero-link-card:hover {
      transform: translateY(-4px);
      border-color: rgba(34,197,94,0.5);
      box-shadow: 0 20px 35px rgba(0,0,0,0.18);
    }

    .hero-link-card:hover::before { opacity: 1; }

    .hero-link-card h3 {
      position: relative;
      z-index: 1;
      font-size: 1.15rem;
      margin-bottom: 0.6rem;
      color: #fff;
    }

    .hero-link-card p {
      position: relative;
      z-index: 1;
      margin: 0 0 1.2rem;
      font-size: 0.83rem;
      color: var(--muted);
      max-width: 90%;
    }

    .hero-link-card span {
      position: relative;
      z-index: 1;
      font-size: 0.74rem;
      color: var(--accent-2);
      text-transform: uppercase;
      letter-spacing: 0.08em;
    }

    .primary-box {
      background: linear-gradient(180deg, rgba(18,18,22,0.92), rgba(12,16,12,0.98));
      border: 1px solid rgba(34,197,94,0.28);
      border-radius: var(--radius);
      padding: 1.6rem 1.4rem;
      margin: 2.3rem 0 1rem;
      box-shadow: 0 20px 50px rgba(0,0,0,0.18);
    }

    .primary-box h3 {
      font-size: 1.1rem;
      margin-bottom: 0.5rem;
      color: var(--text);
    }

    .primary-box p {
      color: var(--muted);
      font-size: 0.9rem;
    }

    h2 {
      margin: 3rem 0 1.25rem;
      font-size: clamp(1.25rem, 2.8vw, 2rem);
      color: #fff;
      border-left: 3px solid var(--accent);
      padding-left: 0.8rem;
    }

    .cards-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
      gap: 1rem;
      margin-top: 1.2rem;
    }

    .card {
      position: relative;
      background: linear-gradient(180deg, rgba(18,18,22,0.9), rgba(12,12,16,0.96));
      border: 1px solid var(--surface-border);
      border-radius: var(--radius);
      padding: 1.3rem 1.2rem;
      box-shadow: var(--shadow);
      overflow: hidden;
      transition: transform 0.2s ease, border-color 0.2s ease;
    }

    .card:hover {
      transform: translateY(-4px);
      border-color: rgba(34,197,94,0.4);
    }

    .card h3 {
      font-size: 1.1rem;
      color: white;
      margin-bottom: 0.5rem;
    }

    .price {
      display: flex;
      align-items: baseline;
      gap: 0.2rem;
      font-family: var(--font-display);
      font-weight: 800;
      color: var(--accent);
      font-size: clamp(1.6rem, 3vw, 2.2rem);
      margin: 1rem 0;
    }

    .price small {
      font-size: 0.75rem;
      font-family: var(--font-mono);
      color: var(--muted);
      letter-spacing: 0.05em;
    }

    .card ul {
      list-style: none;
      margin-top: 0.4rem;
    }

    .card ul li {
      color: var(--muted);
      border-bottom: 1px dashed rgba(255,255,255,0.08);
      padding: 0.5rem 0;
      font-size: 0.82rem;
    }

    .card ul li:last-child { border-bottom: none; }

    .card strong { color: var(--text); }

    .card.custom-plan {
      background: linear-gradient(180deg, rgba(15,26,18,0.96), rgba(10,16,11,0.96));
      border-color: rgba(34,197,94,0.45);
    }

    .service-list {
      list-style: none;
      background: rgba(18,18,22,0.85);
      border: 1px solid var(--surface-border);
      border-radius: var(--radius);
      overflow: hidden;
      margin-top: 1rem;
    }

    .service-list li {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 1rem;
      padding: 0.9rem 1rem;
      border-bottom: 1px solid var(--surface-border);
      font-size: 0.88rem;
      color: var(--text);
    }

    .service-list li:last-child { border-bottom: none; }

    .service-list li span:last-child {
      color: var(--accent-2);
      font-weight: 700;
      white-space: nowrap;
    }

    .note {
      color: var(--muted);
      font-size: 0.78rem;
      margin-top: 0.7rem;
      line-height: 1.6;
    }

    .method-list {
      list-style: none;
      margin-top: 1rem;
      background: rgba(18,18,22,0.75);
      border: 1px solid var(--surface-border);
      border-radius: var(--radius);
      overflow: hidden;
    }

    .method-list li {
      position: relative;
      padding: 0.9rem 1rem 0.9rem 2.1rem;
      border-bottom: 1px solid var(--surface-border);
      color: var(--muted);
      font-size: 0.9rem;
    }

    .method-list li:last-child { border-bottom: none; }

    .method-list li::before {
      content: ">";
      position: absolute;
      left: 0.9rem;
      top: 0.9rem;
      color: var(--accent);
      font-weight: 700;
    }

    .samples-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 1.2rem;
      margin-top: 1.2rem;
    }

    .sample-card {
      background: rgba(18,18,22,0.88);
      border: 1px solid var(--surface-border);
      border-radius: var(--radius);
      overflow: hidden;
      box-shadow: var(--shadow);
      transition: transform 0.2s ease, border-color 0.2s ease;
    }

    .sample-card:hover {
      transform: translateY(-4px);
      border-color: rgba(34,197,94,0.45);
    }

    .sample-card img {
      width: 100%;
      height: 220px;
      object-fit: cover;
      display: block;
      background: linear-gradient(135deg, rgba(34,197,94,0.09), rgba(255,255,255,0.02));
    }

    .sample-body {
      padding: 1rem 1rem 1.15rem;
    }

    .sample-body h3 {
      font-size: 1rem;
      color: white;
      margin-bottom: 0.4rem;
    }

    .sample-body p {
      color: var(--muted);
      font-size: 0.8rem;
      margin-bottom: 0.8rem;
    }

    .sample-url {
      display: inline-block;
      background: rgba(34,197,94,0.06);
      border: 1px solid rgba(34,197,94,0.25);
      color: var(--accent-2);
      padding: 0.6rem 0.8rem;
      font-size: 0.72rem;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      transition: all 0.2s ease;
    }

    .sample-url:hover {
      background: rgba(34,197,94,0.10);
      text-decoration: none;
      transform: translateY(-1px);
    }

    .contact-box {
      background:
        linear-gradient(135deg, rgba(18,18,22,0.9), rgba(12,16,11,0.9)),
        rgba(16,16,21,0.95);
      border: 1px solid rgba(34,197,94,0.3);
      border-radius: var(--radius);
      padding: 2rem 1.3rem;
      text-align: center;
      margin: 2.5rem 0 1rem;
      box-shadow: 0 20px 40px rgba(0,0,0,0.2);
    }

    .contact-box h3 {
      font-size: clamp(1.2rem, 2vw, 1.8rem);
      color: #fff;
      margin-bottom: 0.6rem;
    }

    .contact-box p {
      color: var(--muted);
      font-size: 0.87rem;
      line-height: 1.7;
    }

    .contact-box strong {
      color: var(--accent-2);
      font-weight: 700;
    }

    footer {
      border-top: 1px solid var(--surface-border);
      padding: 2rem 0 2.5rem;
      text-align: center;
      color: var(--muted);
      font-size: 0.76rem;
      letter-spacing: 0.06em;
      text-transform: uppercase;
    }

    @media (max-width: 600px) {
      body { padding: 0 0.9rem; }
      .nav-menu { width: 100%; }
      .service-list li { flex-direction: column; align-items: flex-start; }
      .sample-card img { height: 200px; }
    }
  </style>
</head>
<body>

  <div class="floating-orb orb-one"></div>
  <div class="floating-orb orb-two"></div>
  <div class="floating-orb orb-three"></div>

  <div class="overlay" id="overlay"></div>

  <header>
    <div class="header-inner">
      <div class="logo">JUBA <span>// STUDIOS</span></div>
      <button class="menu-toggle" id="menuToggle">[ MENÚ ]</button>
    </div>
  </header>

  <nav class="nav-menu" id="navMenu">
    <button data-section="intro" class="active">// 00. Inicio</button>
    <button data-section="edicion">// 01. Edición y Diseño</button>
    <button data-section="programacion">// 02. Programación Web</button>
    <button data-section="modelado">// 03. Modelado 3D</button>
    <button class="back-btn" onclick="showSection('intro')">← Volver al inicio</button>
  </nav>

  <main class="container">

    <section class="page-section active reveal" id="intro">
      <div class="hero">
        <div class="eyebrow">
          <span class="status-dot"></span>
          <span>Estado: disponible para nuevos proyectos</span>
        </div>

        <h1>Ingeniería digital y contenidos.</h1>
        <p>Desarrollo web frontend, edición de video de alto impacto y modelado 3D estructurado bajo requerimientos estrictos.</p>

        <div class="primary-box">
          <h3>Pasarela de pagos</h3>
          <p>Solo cobramos en USDT. Cobro directo y transacciones claras, sin fricción ni intermediarios.</p>
        </div>

        <div class="contact-box">
          <h3>¿Iniciar un proyecto?</h3>
          <p>
            Escribir por privado a este usuario de Reddit: <strong>LegitimateMistake715</strong>
          </p>
        </div>

        <div class="hero-grid">
          <div class="hero-link-card reveal" onclick="showSection('edicion')">
            <h3>Edición y diseño</h3>
            <p>Reels, shorts, piezas gráficas y packs de producción mensual.</p>
            <span>Ver specs →</span>
          </div>

          <div class="hero-link-card reveal" onclick="showSection('programacion')">
            <h3>Programación web</h3>
            <p>Sitios dinámicos estructurados en HTML, CSS y JavaScript.</p>
            <span>Ver specs →</span>
          </div>

          <div class="hero-link-card reveal" onclick="showSection('modelado')">
            <h3>Modelado 3D</h3>
            <p>Assets y mallas optimizadas para motores y entornos virtuales.</p>
            <span>Ver specs →</span>
          </div>
        </div>
      </div>
    </section>

    <section class="page-section reveal" id="edicion">
      <h1>Edición & Multimedia</h1>
      <p style="color: var(--muted); font-size: 0.9rem; margin-bottom: 1.5rem;">
        Cortes limpios, diseño vectorial y piezas para plataformas de alta retención.
      </p>

      <h2>Servicios unitarios</h2>
      <ul class="service-list">
        <li><span>Post estático / redes</span><span>desde 5 USDT</span></li>
        <li><span>Logo y branding ID</span><span>desde 15 USDT</span></li>
        <li><span>Diseño gráfico genérico</span><span>desde 10 USDT</span></li>
        <li><span>Reel vertical (Instagram)</span><span>desde 10 USDT</span></li>
        <li><span>Short vertical (TikTok / YT)</span><span>desde 12 USDT</span></li>
        <li><span>Edición de video (hasta 3 min)</span><span>desde 7 USDT</span></li>
        <li><span>Edición de video largo (hasta 15 min)</span><span>desde 30 USDT</span></li>
      </ul>
      <p class="note">* El costo final varía según la carga de efectos visuales y requerimientos de subtitulado.</p>

      <h2>Packs de producción mensual</h2>
      <div class="cards-grid">
        <div class="card">
          <h3>Starter</h3>
          <div class="price">15 <small>USDT/m</small></div>
          <ul>
            <li><strong>16 piezas/mes</strong> (4 por semana)</li>
            <li>Cortes y transiciones base</li>
            <li>Subtítulos simples y audio mix</li>
            <li>1 revisión por entrega</li>
          </ul>
        </div>

        <div class="card">
          <h3>Creator</h3>
          <div class="price">35 <small>USDT/m</small></div>
          <ul>
            <li><strong>32 piezas/mes</strong> (8 por semana)</li>
            <li>Subtítulos dinámicos custom</li>
            <li>Sound design & efectos</li>
            <li>1 revisión por entrega</li>
          </ul>
        </div>

        <div class="card">
          <h3>Pro</h3>
          <div class="price">60 <small>USDT/m</small></div>
          <ul>
            <li><strong>48 piezas/mes</strong> (12 por semana)</li>
            <li>Edición avanzada / narrativa</li>
            <li>Motion graphics y branding</li>
            <li>2 revisiones por entrega</li>
          </ul>
        </div>

        <div class="card custom-plan">
          <h3>Custom</h3>
          <div class="price" style="font-size: 1.25rem;">A Medida</div>
          <ul>
            <li>Evaluación técnica previa</li>
            <li>Adaptación multiplataforma</li>
            <li>Frecuencia de entrega flexible</li>
            <li>Uso de material propio o stock</li>
          </ul>
        </div>
      </div>

      <h2>Muestras de diseño</h2>
      <div class="samples-grid">
        <div class="sample-card">
          <img src="assets/edicion/mr-watches.jpg" alt="Mr. Watches">
          <div class="sample-body">
            <h3>Mr. Watches</h3>
            <p>Identidad visual</p>
          </div>
        </div>

        <div class="sample-card">
          <img src="assets/edicion/editor-inc-01.jpg" alt="Editor Inc. collage">
          <div class="sample-body">
            <h3>Editor, Inc.</h3>
            <p>Branding / creatividad editorial</p>
          </div>
        </div>

        <div class="sample-card">
          <img src="assets/edicion/editor-inc-02.jpg" alt="Editor Inc. collage 2">
          <div class="sample-body">
            <h3>Editor, Inc.</h3>
            <p>Concepto visual / composición</p>
          </div>
        </div>
      </div>

      <h2>Muestras de video</h2>
      <div class="samples-grid">
        <div class="sample-card">
          <img src="https://images.unsplash.com/photo-1492691527719-9d1e07e534b4?auto=format&fit=crop&w=900&q=80" alt="Reel publicitario">
          <div class="sample-body">
            <h3>Reel Publicitario</h3>
            <p>Edición comercial de alto ritmo</p>
            <a href="https://canva.link/9orx66qpm7wu654" target="_blank" class="sample-url">Ver video en Canva →</a>
          </div>
        </div>

        <div class="sample-card">
          <img src="https://images.unsplash.com/photo-1498050108023-c5249f4df085?auto=format&fit=crop&w=900&q=80" alt="Showreel">
          <div class="sample-body">
            <h3>Showreel Tiempos</h3>
            <p>Pruebas de efectos y cortes</p>
            <a href="https://canva.link/8zlxv4k30lwtmjf" target="_blank" class="sample-url">Ver video en Canva →</a>
          </div>
        </div>
      </div>
    </section>

    <section class="page-section reveal" id="programacion">
      <h1>Programación Frontend</h1>
      <p style="color: var(--muted); font-size: 0.9rem; margin-bottom: 1.5rem;">Desarrollo puro con HTML, CSS y JavaScript estructurado.</p>

      <div class="card reveal" style="max-width: 420px; margin-bottom: 1.5rem;">
        <h3>Desarrollo Web Base</h3>
        <div class="price">5 <small>USDT</small></div>
        <p style="font-size: 0.85rem; color: var(--muted);">Presupuesto base sujeto a complejidad del layout y lógica JS requerida.</p>
        <p class="note">* No incluye costos de dominio o alojamiento web.</p>
      </div>

      <div class="card reveal" style="border-left: 2px solid var(--accent); margin-bottom: 1.8rem;">
        <h3 style="font-size: 0.96rem; margin-bottom: 0.3rem;">Protocolo de entrega</h3>
        <p style="font-size: 0.85rem; color: var(--muted);">
          Se entrega el código fuente empaquetado (HTML/CSS/JS). La puesta en producción, servidores y DNS corren exclusivamente por cuenta del cliente.
        </p>
      </div>

      <h2>Muestras de código (CodePen)</h2>
      <div class="samples-grid">
        <div class="sample-card reveal">
          <img src="https://images.unsplash.com/photo-1460925895917-afdab827c52f?auto=format&fit=crop&w=900&q=80" alt="Muestra UI 01">
          <div class="sample-body">
            <h3>Muestra UI 01</h3>
            <p>Estructura frontend</p>
            <a href="https://codepen.io/editor/Juan-Pepe-the-scripter/pen/01a19294-aca6-7ad1-95bf-4b580a55688e" target="_blank" class="sample-url">Ver código →</a>
          </div>
        </div>

        <div class="sample-card reveal">
          <img src="https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=900&q=80" alt="Muestra UI 02">
          <div class="sample-body">
            <h3>Muestra UI 02</h3>
            <p>Componentes y lógica</p>
            <a href="https://codepen.io/editor/Juan-Pepe-the-scripter/pen/01a1929c-e2b8-717b-9d02-68a217481964" target="_blank" class="sample-url">Ver código →</a>
          </div>
        </div>
      </div>

      <h2>Condiciones operativas</h2>
      <ul class="method-list reveal">
        <li>Validación técnica previa a la aceptación de cualquier encargo.</li>
        <li>Acuerdo de plazos y características inalterables post-inicio.</li>
        <li>Soporte de comunicación transparente durante todo el ciclo.</li>
      </ul>
    </section>

    <section class="page-section reveal" id="modelado">
      <h1>Modelado 3D</h1>
      <p style="color: var(--muted); font-size: 0.9rem; margin-bottom: 1.5rem;">
        Construcción de assets tridimensionales y mallas optimizadas.
      </p>

      <div class="card reveal" style="max-width: 420px; margin-bottom: 2rem;">
        <h3>Asset 3D Custom</h3>
        <div class="price">20 – 100 <small>USDT</small></div>
        <p style="font-size: 0.85rem; color: var(--muted);">
          Tasación basada en densidad poligonal, texturizado, rigging y motor de destino.
        </p>
      </div>

      <h2>Muestras de assets</h2>
      <div class="samples-grid">
        <div class="sample-card reveal">
          <img src="assets/modelado/model-01.jpg" alt="Asset model 01">
          <div class="sample-body">
            <h3>Asset Model 01</h3>
            <p>Malla y texturas</p>
          </div>
        </div>

        <div class="sample-card reveal">
          <img src="assets/modelado/model-02.jpg" alt="Asset model 02">
          <div class="sample-body">
            <h3>Asset Model 02</h3>
            <p>Malla y texturas</p>
          </div>
        </div>

        <div class="sample-card reveal">
          <img src="assets/modelado/model-03.jpg" alt="Asset model 03">
          <div class="sample-body">
            <h3>Asset Model 03</h3>
            <p>Malla y texturas</p>
          </div>
        </div>

        <div class="sample-card reveal">
          <img src="assets/modelado/model-04.jpg" alt="Asset model 04">
          <div class="sample-body">
            <h3>Asset Model 04</h3>
            <p>Malla y texturas</p>
          </div>
        </div>
      </div>
    </section>

  </main>

  <footer>
    <p>JUBA STUDIOS // INDEPENDENT DIGITAL SERVICES — 2026</p>
    <p style="margin-top: 0.4rem;">transacciones exclusivas en USDT</p>
  </footer>

  <script>
    (function () {
      const menuToggle = document.getElementById('menuToggle');
      const navMenu = document.getElementById('navMenu');
      const overlay = document.getElementById('overlay');
      const navButtons = navMenu.querySelectorAll('button[data-section]');
      const sections = document.querySelectorAll('.page-section');

      function openMenu() {
        navMenu.classList.add('open');
        overlay.classList.add('active');
        document.body.style.overflow = 'hidden';
      }

      function closeMenu() {
        navMenu.classList.remove('open');
        overlay.classList.remove('active');
        document.body.style.overflow = '';
      }

      menuToggle.addEventListener('click', function (e) {
        e.stopPropagation();
        if (navMenu.classList.contains('open')) {
          closeMenu();
        } else {
          openMenu();
        }
      });

      overlay.addEventListener('click', closeMenu);

      document.addEventListener('keydown', function (e) {
        if (e.key === 'Escape' && navMenu.classList.contains('open')) {
          closeMenu();
        }
      });

      window.showSection = function (id) {
        sections.forEach(section => {
          section.classList.remove('active');
        });

        const target = document.getElementById(id);
        if (target) target.classList.add('active');

        navButtons.forEach(button => {
          button.classList.toggle('active', button.dataset.section === id);
        });

        closeMenu();
        window.scrollTo({ top: 0, behavior: 'smooth' });
      };

      navButtons.forEach(button => {
        button.addEventListener('click', function () {
          if (this.dataset.section) {
            showSection(this.dataset.section);
          }
        });
      });

      const revealEls = document.querySelectorAll('.reveal');
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('visible');
          }
        });
      }, { threshold: 0.12 });

      revealEls.forEach(el => observer.observe(el));
    })();
  </script>
</body>
</html>
