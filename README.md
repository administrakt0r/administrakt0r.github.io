<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- ═══════════════════════════════════════════════════════ SEO META -->
  <title>Debian 13 GNOME Optimization Script | Speed Up Linux Desktop 2026</title>
  <meta name="description" content="The most complete Debian 13 Trixie GNOME performance optimization script. Tune SSD I/O, ZRAM swap, CPU governor, disable Tracker, kill animations. 24 steps. Free & open source by administrakt0r." />
  <meta name="keywords" content="debian 13 optimization, debian trixie performance, gnome speed up, linux desktop optimization, zram swap debian, ssd optimization linux, disable gnome animations, gnome tracker disable, debian 13 trixie tweaks, schedutil governor, linux performance tuning 2026, debian gnome fast, mq-deadline ssd, noatime fstab, linux bash script optimization, open source linux tools" />
  <meta name="author" content="administrakt0r" />
  <meta name="robots" content="index, follow, max-snippet:-1, max-image-preview:large" />
  <link rel="canonical" href="https://administrakt0r.github.io/debian13-gnome-optimize/" />

  <!-- ═════════════════════════════════════════════════════ OPEN GRAPH -->
  <meta property="og:type" content="website" />
  <meta property="og:title" content="Debian 13 GNOME Optimization Script — 24 Steps to a Blazing Fast Desktop" />
  <meta property="og:description" content="Free open-source bash script that tunes SSD I/O, ZRAM swap, CPU governor, and kills every GNOME performance hog in one run. Safe, idempotent, fully documented." />
  <meta property="og:url" content="https://administrakt0r.github.io/debian13-gnome-optimize/" />
  <meta property="og:site_name" content="administrakt0r · Open Source Tools" />
  <meta property="og:image" content="https://administrakt0r.github.io/debian13-gnome-optimize/og-card.png" />

  <!-- ══════════════════════════════════════════════════ TWITTER CARD -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content="Debian 13 GNOME Optimization Script" />
  <meta name="twitter:description" content="24-step bash script that turns a fresh Debian 13 install into a blazing fast GNOME desktop. Free & open source." />

  <!-- ════════════════════════════════════════════ STRUCTURED DATA / JSON-LD -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "SoftwareApplication",
    "name": "Debian 13 GNOME Optimization Script",
    "description": "A comprehensive 24-step bash script that optimizes Debian 13 Trixie with GNOME for maximum desktop performance. Tunes SSD I/O scheduler, ZRAM swap, CPU governor, network stack, and disables GNOME performance bottlenecks.",
    "applicationCategory": "SystemOptimization",
    "operatingSystem": "Debian 13 (Trixie)",
    "offers": { "@type": "Offer", "price": "0", "priceCurrency": "USD" },
    "author": {
      "@type": "Person",
      "name": "administrakt0r",
      "url": "https://github.com/administrakt0r"
    },
    "license": "https://opensource.org/licenses/MIT",
    "codeRepository": "https://github.com/administrakt0r/debian13-gnome-optimize",
    "keywords": "debian 13, gnome optimization, linux performance, zram, ssd tuning, bash script"
  }
  </script>

  <!-- ══════════════════════════════════════════════════════════ FONTS -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet" />

  <style>
    /* ═══════════════════════════════════════════════ DESIGN TOKENS */
    :root {
      --bg:        #090d0f;
      --bg2:       #0e1518;
      --bg3:       #131c20;
      --border:    #1e2e33;
      --border2:   #243640;
      --green:     #39ff8f;
      --green-dim: #1a7a45;
      --cyan:      #00d4e8;
      --cyan-dim:  #0a4a52;
      --amber:     #f5a623;
      --red:       #ff5f6d;
      --text:      #c8d8dc;
      --text-dim:  #6a8a92;
      --text-mute: #3a5560;
      --font-mono: 'JetBrains Mono', monospace;
      --font-sans: 'IBM Plex Sans', sans-serif;
      --radius:    6px;
      --glow-g:    0 0 24px rgba(57,255,143,0.18);
      --glow-c:    0 0 24px rgba(0,212,232,0.18);
    }

    /* ═══════════════════════════════════════════════════════ RESET */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--font-sans);
      font-size: 16px;
      line-height: 1.7;
      overflow-x: hidden;
    }

    /* Scanline overlay */
    body::before {
      content: '';
      position: fixed; inset: 0;
      background: repeating-linear-gradient(
        0deg,
        transparent,
        transparent 2px,
        rgba(0,0,0,0.06) 2px,
        rgba(0,0,0,0.06) 4px
      );
      pointer-events: none;
      z-index: 9999;
    }

    /* Grid background */
    body::after {
      content: '';
      position: fixed; inset: 0;
      background-image:
        linear-gradient(rgba(57,255,143,0.025) 1px, transparent 1px),
        linear-gradient(90deg, rgba(57,255,143,0.025) 1px, transparent 1px);
      background-size: 40px 40px;
      pointer-events: none;
      z-index: 0;
    }

    /* ══════════════════════════════════════════════════ TYPOGRAPHY */
    h1, h2, h3, h4 { font-family: var(--font-sans); font-weight: 800; line-height: 1.15; }
    a { color: var(--cyan); text-decoration: none; transition: color .2s; }
    a:hover { color: var(--green); }
    code, pre { font-family: var(--font-mono); }

    .mono { font-family: var(--font-mono); }
    .green { color: var(--green); }
    .cyan  { color: var(--cyan); }
    .amber { color: var(--amber); }
    .dim   { color: var(--text-dim); }
    .mute  { color: var(--text-mute); }

    /* ═══════════════════════════════════════════════════ CONTAINERS */
    .wrap    { max-width: 1080px; margin: 0 auto; padding: 0 24px; position: relative; z-index: 1; }
    .wrap-sm { max-width: 720px;  margin: 0 auto; padding: 0 24px; position: relative; z-index: 1; }

    /* ═══════════════════════════════════════════════════ ANIMATIONS */
    @keyframes fadeUp   { from { opacity:0; transform:translateY(28px); } to { opacity:1; transform:none; } }
    @keyframes blink    { 0%,100%{opacity:1} 50%{opacity:0} }
    @keyframes glow-pulse { 0%,100%{box-shadow:var(--glow-g)} 50%{box-shadow:0 0 48px rgba(57,255,143,0.35)} }
    @keyframes float    { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-8px)} }
    @keyframes slide-in { from{transform:translateX(-16px);opacity:0} to{transform:none;opacity:1} }
    @keyframes ticker   { from{transform:translateX(0)} to{transform:translateX(-50%)} }

    .fade-up { animation: fadeUp .7s ease both; }
    .d1 { animation-delay: .1s }
    .d2 { animation-delay: .2s }
    .d3 { animation-delay: .3s }
    .d4 { animation-delay: .4s }
    .d5 { animation-delay: .5s }
    .d6 { animation-delay: .6s }

    /* ════════════════════════════════════════════════════════ TICKER */
    .ticker-wrap {
      background: var(--bg2);
      border-top: 1px solid var(--border);
      border-bottom: 1px solid var(--border);
      padding: 10px 0;
      overflow: hidden;
      white-space: nowrap;
    }
    .ticker-inner {
      display: inline-block;
      animation: ticker 35s linear infinite;
    }
    .ticker-inner span {
      font-family: var(--font-mono);
      font-size: 12px;
      color: var(--text-dim);
      padding: 0 28px;
    }
    .ticker-inner span::before {
      content: '▸ ';
      color: var(--green);
    }

    /* ═══════════════════════════════════════════════════════ NAVBAR */
    nav {
      position: sticky; top: 0; z-index: 100;
      background: rgba(9,13,15,0.88);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
    }
    .nav-inner {
      max-width: 1080px; margin: 0 auto; padding: 0 24px;
      display: flex; align-items: center; justify-content: space-between;
      height: 58px;
    }
    .nav-brand {
      font-family: var(--font-mono);
      font-weight: 700;
      font-size: 14px;
      color: var(--green);
      letter-spacing: .05em;
    }
    .nav-brand span { color: var(--text-dim); }
    .nav-links { display: flex; gap: 28px; }
    .nav-links a {
      font-size: 13px;
      font-family: var(--font-mono);
      color: var(--text-dim);
      letter-spacing: .04em;
    }
    .nav-links a:hover { color: var(--green); }
    .nav-cta {
      background: var(--green);
      color: var(--bg) !important;
      font-weight: 700;
      padding: 7px 18px;
      border-radius: var(--radius);
      font-size: 13px !important;
      transition: box-shadow .2s, background .2s !important;
    }
    .nav-cta:hover { box-shadow: var(--glow-g); background: #5fffaa !important; }

    /* ══════════════════════════════════════════════════════ HERO */
    .hero {
      padding: 100px 0 80px;
      position: relative;
      overflow: hidden;
    }
    /* Radial glow behind hero */
    .hero::before {
      content: '';
      position: absolute;
      top: -100px; left: 50%; transform: translateX(-50%);
      width: 800px; height: 500px;
      background: radial-gradient(ellipse at 50% 0%, rgba(57,255,143,0.08) 0%, transparent 70%);
      pointer-events: none;
    }

    .hero-eyebrow {
      display: inline-flex; align-items: center; gap: 8px;
      font-family: var(--font-mono);
      font-size: 12px;
      color: var(--green);
      background: rgba(57,255,143,0.08);
      border: 1px solid rgba(57,255,143,0.2);
      padding: 5px 14px;
      border-radius: 99px;
      letter-spacing: .08em;
      text-transform: uppercase;
      margin-bottom: 28px;
    }
    .hero-eyebrow::before { content: '●'; font-size: 8px; animation: blink 1.4s infinite; }

    .hero h1 {
      font-size: clamp(2.4rem, 5.5vw, 4rem);
      font-family: var(--font-mono);
      font-weight: 700;
      color: #fff;
      margin-bottom: 12px;
      letter-spacing: -.02em;
    }
    .hero h1 em {
      font-style: normal;
      background: linear-gradient(90deg, var(--green), var(--cyan));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
      background-clip: text;
    }
    .hero-sub {
      font-size: clamp(1rem, 2vw, 1.2rem);
      color: var(--text-dim);
      max-width: 580px;
      margin-bottom: 44px;
      font-weight: 400;
    }

    .hero-actions { display: flex; flex-wrap: wrap; gap: 14px; margin-bottom: 60px; }

    .btn {
      display: inline-flex; align-items: center; gap: 8px;
      font-family: var(--font-mono);
      font-size: 14px;
      font-weight: 700;
      padding: 13px 26px;
      border-radius: var(--radius);
      cursor: pointer;
      border: none;
      transition: all .2s;
      text-decoration: none;
    }
    .btn-primary {
      background: var(--green);
      color: var(--bg);
      animation: glow-pulse 3s ease-in-out infinite;
    }
    .btn-primary:hover { background: #5fffaa; color: var(--bg); transform: translateY(-2px); }
    .btn-secondary {
      background: transparent;
      color: var(--cyan);
      border: 1px solid var(--cyan-dim);
    }
    .btn-secondary:hover { border-color: var(--cyan); box-shadow: var(--glow-c); transform: translateY(-2px); }
    .btn-ghost {
      background: transparent;
      color: var(--text-dim);
      border: 1px solid var(--border2);
    }
    .btn-ghost:hover { color: var(--text); border-color: var(--text-mute); }

    /* ══════════════════════════════════════════════ TERMINAL BLOCK */
    .terminal {
      background: var(--bg2);
      border: 1px solid var(--border2);
      border-radius: 10px;
      overflow: hidden;
      box-shadow: 0 8px 48px rgba(0,0,0,0.6), inset 0 1px 0 rgba(255,255,255,0.04);
    }
    .terminal-bar {
      background: var(--bg3);
      padding: 10px 16px;
      display: flex; align-items: center; gap: 8px;
      border-bottom: 1px solid var(--border);
    }
    .dot { width: 12px; height: 12px; border-radius: 50%; }
    .dot-r { background: #ff5f57; }
    .dot-y { background: #febc2e; }
    .dot-g { background: #28c840; }
    .terminal-title {
      font-family: var(--font-mono);
      font-size: 12px;
      color: var(--text-mute);
      flex: 1; text-align: center;
    }
    .terminal-body {
      padding: 22px 24px;
      font-family: var(--font-mono);
      font-size: 13.5px;
      line-height: 1.9;
    }
    .t-prompt { color: var(--green); }
    .t-cmd { color: #fff; }
    .t-out { color: var(--text-dim); padding-left: 20px; }
    .t-ok  { color: var(--green); padding-left: 20px; }
    .t-info{ color: var(--cyan);  padding-left: 20px; }
    .t-cursor::after { content: '█'; animation: blink 1s infinite; color: var(--green); font-size: 13px; }

    /* ═══════════════════════════════════════════════════════ STATS */
    .stats-row {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
      gap: 1px;
      background: var(--border);
      border: 1px solid var(--border);
      border-radius: 10px;
      overflow: hidden;
      margin: 56px 0;
    }
    .stat-box {
      background: var(--bg2);
      padding: 28px 24px;
      text-align: center;
      transition: background .2s;
    }
    .stat-box:hover { background: var(--bg3); }
    .stat-num {
      font-family: var(--font-mono);
      font-size: 2.4rem;
      font-weight: 700;
      color: var(--green);
      line-height: 1;
      display: block;
    }
    .stat-label {
      font-size: 12px;
      color: var(--text-dim);
      margin-top: 6px;
      letter-spacing: .04em;
      text-transform: uppercase;
    }

    /* ══════════════════════════════════════════════════ SECTION BASE */
    section { padding: 80px 0; }
    .section-eyebrow {
      font-family: var(--font-mono);
      font-size: 11px;
      color: var(--cyan);
      text-transform: uppercase;
      letter-spacing: .12em;
      margin-bottom: 10px;
    }
    .section-title {
      font-size: clamp(1.7rem, 3.5vw, 2.4rem);
      color: #fff;
      margin-bottom: 14px;
      letter-spacing: -.02em;
    }
    .section-lead {
      color: var(--text-dim);
      max-width: 560px;
      font-size: 1.05rem;
      margin-bottom: 48px;
    }
    .divider { height: 1px; background: var(--border); margin: 0; }

    /* ═══════════════════════════════════════════════ STEPS GRID */
    .steps-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
      gap: 16px;
    }
    .step-card {
      background: var(--bg2);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 22px;
      position: relative;
      overflow: hidden;
      transition: border-color .2s, transform .2s, box-shadow .2s;
    }
    .step-card::before {
      content: '';
      position: absolute; top: 0; left: 0;
      width: 3px; height: 100%;
    }
    .step-card.sys::before  { background: var(--green); }
    .step-card.gnome::before { background: var(--cyan); }
    .step-card:hover {
      border-color: var(--border2);
      transform: translateY(-3px);
    }
    .step-card.sys:hover  { box-shadow: -3px 0 20px rgba(57,255,143,0.12); }
    .step-card.gnome:hover { box-shadow: -3px 0 20px rgba(0,212,232,0.12); }

    .step-num {
      font-family: var(--font-mono);
      font-size: 11px;
      font-weight: 700;
      margin-bottom: 8px;
    }
    .step-card.sys  .step-num { color: var(--green-dim); }
    .step-card.gnome .step-num { color: var(--cyan-dim); }
    .step-title {
      font-family: var(--font-sans);
      font-weight: 700;
      font-size: 15px;
      color: #fff;
      margin-bottom: 6px;
    }
    .step-desc { font-size: 13px; color: var(--text-dim); line-height: 1.55; }

    /* ════════════════════════════════════════════════ INSTALL BLOCK */
    .install-block {
      background: var(--bg2);
      border: 1px solid var(--border2);
      border-radius: 10px;
      padding: 40px;
      position: relative;
      overflow: hidden;
    }
    .install-block::before {
      content: '';
      position: absolute; top: -60px; right: -60px;
      width: 200px; height: 200px;
      background: radial-gradient(circle, rgba(57,255,143,0.06) 0%, transparent 70%);
    }
    .install-step {
      display: flex; gap: 20px; align-items: flex-start;
      margin-bottom: 28px;
    }
    .install-step:last-child { margin-bottom: 0; }
    .install-num {
      flex-shrink: 0;
      width: 30px; height: 30px;
      background: rgba(57,255,143,0.1);
      border: 1px solid rgba(57,255,143,0.25);
      border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      font-family: var(--font-mono);
      font-size: 12px;
      font-weight: 700;
      color: var(--green);
      margin-top: 4px;
    }
    .install-cmd {
      background: var(--bg);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 13px 18px;
      font-family: var(--font-mono);
      font-size: 13px;
      color: var(--green);
      margin-top: 8px;
      display: flex; align-items: center; justify-content: space-between;
      gap: 12px;
      word-break: break-all;
    }
    .copy-btn {
      flex-shrink: 0;
      background: rgba(57,255,143,0.1);
      border: 1px solid rgba(57,255,143,0.2);
      color: var(--green);
      padding: 4px 12px;
      border-radius: 4px;
      font-family: var(--font-mono);
      font-size: 11px;
      cursor: pointer;
      transition: all .2s;
      white-space: nowrap;
    }
    .copy-btn:hover { background: rgba(57,255,143,0.2); }

    /* ═════════════════════════════════════════════════ PROMO CARDS */
    .promo-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 20px;
    }
    .promo-card {
      border-radius: 12px;
      padding: 32px;
      position: relative;
      overflow: hidden;
      transition: transform .25s, box-shadow .25s;
      text-decoration: none;
      display: block;
    }
    .promo-card:hover { transform: translateY(-5px); }

    .promo-card.wp {
      background: linear-gradient(135deg, #0d1f2e 0%, #0a2a40 100%);
      border: 1px solid #1a4060;
    }
    .promo-card.wp:hover { box-shadow: 0 12px 48px rgba(0,120,212,0.25); }
    .promo-card.llm {
      background: linear-gradient(135deg, #0d2010 0%, #0a2a18 100%);
      border: 1px solid #1a4030;
    }
    .promo-card.llm:hover { box-shadow: 0 12px 48px rgba(57,255,143,0.2); }
    .promo-card.gh {
      background: linear-gradient(135deg, #191c24 0%, #1a1e2a 100%);
      border: 1px solid #2a2e3f;
    }
    .promo-card.gh:hover { box-shadow: 0 12px 48px rgba(255,255,255,0.07); }

    .promo-icon {
      font-size: 2.2rem;
      margin-bottom: 16px;
      display: block;
      animation: float 4s ease-in-out infinite;
    }
    .promo-badge {
      display: inline-block;
      font-family: var(--font-mono);
      font-size: 10px;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: .1em;
      padding: 3px 10px;
      border-radius: 99px;
      margin-bottom: 12px;
    }
    .promo-card.wp  .promo-badge { background: rgba(0,120,212,0.2); color: #5ab4ff; border: 1px solid rgba(0,120,212,0.3); }
    .promo-card.llm .promo-badge { background: rgba(57,255,143,0.12); color: var(--green); border: 1px solid rgba(57,255,143,0.2); }
    .promo-card.gh  .promo-badge { background: rgba(255,255,255,0.07); color: #aaa; border: 1px solid rgba(255,255,255,0.1); }

    .promo-card h3 {
      font-size: 1.25rem;
      color: #fff;
      margin-bottom: 8px;
    }
    .promo-card p {
      font-size: 14px;
      line-height: 1.6;
      margin-bottom: 20px;
    }
    .promo-card.wp  p { color: #6a9ec0; }
    .promo-card.llm p { color: #6aaa88; }
    .promo-card.gh  p { color: #7a8090; }

    .promo-link {
      font-family: var(--font-mono);
      font-size: 13px;
      font-weight: 700;
      display: inline-flex; align-items: center; gap: 6px;
    }
    .promo-card.wp  .promo-link { color: #5ab4ff; }
    .promo-card.llm .promo-link { color: var(--green); }
    .promo-card.gh  .promo-link { color: #bbb; }
    .promo-link::after { content: ' →'; }

    /* ═══════════════════════════════════════════════ FEATURES LIST */
    .feature-list { list-style: none; display: grid; gap: 12px; }
    .feature-list li {
      display: flex; align-items: flex-start; gap: 12px;
      font-size: 15px; color: var(--text);
    }
    .feature-list li::before {
      content: '✓';
      color: var(--green);
      font-family: var(--font-mono);
      font-weight: 700;
      font-size: 13px;
      flex-shrink: 0;
      margin-top: 3px;
    }

    /* ═══════════════════════════════════════════════ FAQ */
    .faq-item {
      border-bottom: 1px solid var(--border);
      padding: 22px 0;
    }
    .faq-item:first-child { border-top: 1px solid var(--border); }
    .faq-q {
      font-weight: 700;
      font-size: 16px;
      color: #fff;
      margin-bottom: 8px;
      cursor: pointer;
      display: flex; justify-content: space-between; align-items: center;
    }
    .faq-q::after { content: '+'; color: var(--green); font-size: 20px; font-weight: 400; }
    .faq-a { font-size: 14px; color: var(--text-dim); line-height: 1.7; }

    /* ═════════════════════════════════════════════════════ FOOTER */
    footer {
      background: var(--bg2);
      border-top: 1px solid var(--border);
      padding: 48px 0 32px;
      position: relative; z-index: 1;
    }
    .footer-grid {
      display: grid;
      grid-template-columns: 2fr 1fr 1fr;
      gap: 40px;
      margin-bottom: 40px;
    }
    .footer-brand {
      font-family: var(--font-mono);
      font-size: 16px;
      font-weight: 700;
      color: var(--green);
      margin-bottom: 10px;
    }
    .footer-about { font-size: 13px; color: var(--text-dim); max-width: 300px; }
    .footer-col h4 {
      font-size: 12px;
      text-transform: uppercase;
      letter-spacing: .1em;
      color: var(--text-mute);
      margin-bottom: 14px;
      font-family: var(--font-mono);
    }
    .footer-col a {
      display: block;
      font-size: 13px;
      color: var(--text-dim);
      margin-bottom: 8px;
    }
    .footer-col a:hover { color: var(--green); }
    .footer-bottom {
      border-top: 1px solid var(--border);
      padding-top: 24px;
      display: flex; justify-content: space-between; align-items: center;
      flex-wrap: wrap; gap: 12px;
    }
    .footer-bottom p { font-size: 12px; color: var(--text-mute); font-family: var(--font-mono); }
    .footer-bottom a { color: var(--text-mute); }
    .footer-bottom a:hover { color: var(--green); }

    /* ══════════════════════════════════════════════ LABEL CHIPS */
    .chip {
      display: inline-block;
      font-family: var(--font-mono);
      font-size: 11px;
      padding: 3px 10px;
      border-radius: 99px;
      border: 1px solid;
    }
    .chip-green { color: var(--green); border-color: rgba(57,255,143,.3); background: rgba(57,255,143,.07); }
    .chip-cyan  { color: var(--cyan);  border-color: rgba(0,212,232,.3);  background: rgba(0,212,232,.07); }
    .chip-amber { color: var(--amber); border-color: rgba(245,166,35,.3);  background: rgba(245,166,35,.07);}

    /* ═══════════════════════════════════════════════════ ICONS */
    .icon-gh {
      display: inline-block;
      width: 16px; height: 16px;
      vertical-align: middle;
      fill: currentColor;
      flex-shrink: 0;
    }
    @media (max-width: 768px) {
      .nav-links { display: none; }
      .footer-grid { grid-template-columns: 1fr; }
      .install-block { padding: 24px; }
    }
    @media (max-width: 520px) {
      .hero { padding: 70px 0 60px; }
      .hero h1 { font-size: 2rem; }
    }
  </style>
</head>

<body>

<!-- ════════════════════════════════════════════════════════════ TICKER -->
<div class="ticker-wrap" aria-hidden="true">
  <div class="ticker-inner">
    <span>SSD TRIM enabled</span>
    <span>ZRAM lz4 swap active</span>
    <span>I/O scheduler: mq-deadline</span>
    <span>swappiness = 100 (ZRAM-optimised)</span>
    <span>GNOME animations: OFF</span>
    <span>Tracker 3: MASKED</span>
    <span>schedutil governor</span>
    <span>BBR congestion control</span>
    <span>noatime in fstab</span>
    <span>preload: learning habits</span>
    <span>page-cluster = 0</span>
    <span>journal capped at 200MB</span>
    <!-- duplicate for seamless loop -->
    <span>SSD TRIM enabled</span>
    <span>ZRAM lz4 swap active</span>
    <span>I/O scheduler: mq-deadline</span>
    <span>swappiness = 100 (ZRAM-optimised)</span>
    <span>GNOME animations: OFF</span>
    <span>Tracker 3: MASKED</span>
    <span>schedutil governor</span>
    <span>BBR congestion control</span>
    <span>noatime in fstab</span>
    <span>preload: learning habits</span>
    <span>page-cluster = 0</span>
    <span>journal capped at 200MB</span>
  </div>
</div>

<!-- ═══════════════════════════════════════════════════════════ NAVBAR -->
<nav>
  <div class="nav-inner">
    <div class="nav-brand">administrakt0r<span>/debian13-optimize</span></div>
    <div class="nav-links">
      <a href="#steps">Steps</a>
      <a href="#install">Install</a>
      <a href="#why">Why</a>
      <a href="#faq">FAQ</a>
      <a href="https://github.com/administrakt0r/debian13-gnome-optimize" target="_blank" rel="noopener" class="nav-cta"><svg class="icon-gh" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg> ⭐ GitHub</a>
    </div>
  </div>
</nav>

<!-- ════════════════════════════════════════════════════════════ HERO -->
<header class="hero">
  <div class="wrap">
    <div class="hero-eyebrow fade-up">Debian 13 Trixie · GNOME · Open Source</div>

    <h1 class="fade-up d1">
      Your Linux desktop.<br>
      <em>Actually fast.</em>
    </h1>

    <p class="hero-sub fade-up d2">
      The most complete, safe, and idempotent performance optimization script for
      <strong>Debian 13 Trixie with GNOME</strong>. 24 targeted steps.
      One command. Zero breakage.
    </p>

    <div class="hero-actions fade-up d3">
      <a href="#install" class="btn btn-primary">▶ &nbsp;Get Started</a>
      <a href="https://github.com/administrakt0r/debian13-gnome-optimize" target="_blank" rel="noopener" class="btn btn-secondary"><svg class="icon-gh" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg> View on GitHub</a>
      <a href="https://raw.githubusercontent.com/administrakt0r/debian13-gnome-optimize/main/debian13-optimize.sh" target="_blank" rel="noopener" class="btn btn-ghost"><svg class="icon-gh" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg> Raw Script</a>
    </div>

    <!-- Live terminal demo -->
    <div class="terminal fade-up d4">
      <div class="terminal-bar">
        <span class="dot dot-r"></span>
        <span class="dot dot-y"></span>
        <span class="dot dot-g"></span>
        <span class="terminal-title">terminal — debian13-optimize.sh</span>
      </div>
      <div class="terminal-body">
        <div><span class="t-prompt">dmina@debian:~$ </span><span class="t-cmd">sudo bash debian13-optimize.sh</span></div>
        <div class="t-info">════ 1/24 · Package prerequisites ════</div>
        <div class="t-ok">[OK]     systemd-zram-generator — already installed.</div>
        <div class="t-ok">[OK]     power-profiles-daemon — already installed.</div>
        <div class="t-info">════ 2/24 · SSD TRIM ════</div>
        <div class="t-ok">[OK]     fstrim.timer already enabled.</div>
        <div class="t-out">/: 14.2 GiB (15,237,996,544 bytes) trimmed on /dev/sda1</div>
        <div class="t-info">════ 6/24 · ZRAM swap ════</div>
        <div class="t-ok">[OK]     Written: /etc/systemd/zram-generator.conf</div>
        <div class="t-ok">[OK]     ZRAM swap configured (lz4, ≤4 GB).</div>
        <div class="t-info">════ 14/24 · GNOME animations ════</div>
        <div class="t-ok">[OK]     Set [dmina]: org.gnome.desktop.interface enable-animations = false</div>
        <div class="t-info">════ 17/24 · GNOME Tracker 3 ════</div>
        <div class="t-ok">[OK]     Tracker 3 masked and throttled.</div>
        <div class="t-ok">[OK]     All 24 optimisations complete! <span class="t-cursor"></span></div>
      </div>
    </div>

    <!-- Stats row -->
    <div class="stats-row fade-up d5">
      <div class="stat-box">
        <span class="stat-num">24</span>
        <span class="stat-label">Optimisations</span>
      </div>
      <div class="stat-box">
        <span class="stat-num">0</span>
        <span class="stat-label">Packages Removed</span>
      </div>
      <div class="stat-box">
        <span class="stat-num">∞</span>
        <span class="stat-label">Re-runs Safe</span>
      </div>
      <div class="stat-box">
        <span class="stat-num">MIT</span>
        <span class="stat-label">License</span>
      </div>
      <div class="stat-box">
        <span class="stat-num">100%</span>
        <span class="stat-label">Free & Open</span>
      </div>
    </div>
  </div>
</header>

<div class="divider"></div>

<!-- ═══════════════════════════════════════════════════ STEPS SECTION -->
<section id="steps">
  <div class="wrap">
    <p class="section-eyebrow">What it does</p>
    <h2 class="section-title">24 targeted optimisations</h2>
    <p class="section-lead">
      Every step is explained, every file backed up, every change reversible.
      The script never removes packages — only configures what's already there.
    </p>

    <div style="display:flex; gap:20px; margin-bottom:28px; flex-wrap:wrap;">
      <span class="chip chip-green">● System (1–13)</span>
      <span class="chip chip-cyan">● GNOME (14–23)</span>
      <span class="chip chip-amber">● Live Status (24)</span>
    </div>

    <div class="steps-grid">
      <!-- System steps -->
      <div class="step-card sys">
        <div class="step-num">STEP 01 · SYSTEM</div>
        <div class="step-title">Package Prerequisites</div>
        <div class="step-desc">Installs <code>systemd-zram-generator</code>, <code>power-profiles-daemon</code>, <code>preload</code> — each checked individually so one missing package never aborts the whole script.</div>
      </div>
      <div class="step-card sys">
        <div class="step-num">STEP 02 · SYSTEM</div>
        <div class="step-title">SSD TRIM</div>
        <div class="step-desc">Enables weekly <code>fstrim.timer</code> and runs an immediate TRIM. Reclaims deleted-file space and maintains SSD write speeds over time.</div>
      </div>
      <div class="step-card sys">
        <div class="step-num">STEP 03 · SYSTEM</div>
        <div class="step-title">I/O Scheduler</div>
        <div class="step-desc">Sets <strong>none</strong> for NVMe (no overhead) and <strong>mq-deadline</strong> for SATA SSD (low latency, TRIM-aware) via persistent udev rule.</div>
      </div>
      <div class="step-card sys">
        <div class="step-num">STEP 04 · SYSTEM</div>
        <div class="step-title">noatime in fstab</div>
        <div class="step-desc">Stops the kernel writing an access timestamp on every single file read. Reduces SSD writes with zero user-visible impact.</div>
      </div>
      <div class="step-card sys">
        <div class="step-num">STEP 05 · SYSTEM</div>
        <div class="step-title">/tmp on tmpfs</div>
        <div class="step-desc">Mounts <code>/tmp</code> in RAM (capped 2 GB). Build tools, browsers, and apps write temp files directly to RAM instead of your SSD.</div>
      </div>
      <div class="step-card sys">
        <div class="step-num">STEP 06 · SYSTEM</div>
        <div class="step-title">ZRAM Compressed Swap</div>
        <div class="step-desc">Configures <code>systemd-zram-generator</code> — lz4 compression, 50% of RAM, priority 100. Replaces slow disk swap with fast in-RAM swap.</div>
      </div>
      <div class="step-card sys">
        <div class="step-num">STEP 07 · SYSTEM</div>
        <div class="step-title">Disable Partition Swap</div>
        <div class="step-desc">Comments out legacy swap entries in <code>/etc/fstab</code>. ZRAM is strictly better on any machine with an SSD — disk swap just creates latency spikes.</div>
      </div>
      <div class="step-card sys">
        <div class="step-num">STEP 08 · SYSTEM</div>
        <div class="step-title">VM Sysctl (ZRAM-Tuned)</div>
        <div class="step-desc"><code>swappiness=100</code> + <code>page-cluster=0</code> — the correct ZRAM config. High swappiness is right when swap is in RAM, not disk.</div>
      </div>
      <div class="step-card sys">
        <div class="step-num">STEP 09 · SYSTEM</div>
        <div class="step-title">CPU Governor: schedutil</div>
        <div class="step-desc">Creates a systemd oneshot service (replaces removed <code>cpufrequtils</code>) to persist <strong>schedutil</strong> — the kernel-integrated governor for i3-6xxx.</div>
      </div>
      <div class="step-card sys">
        <div class="step-num">STEP 10 · SYSTEM</div>
        <div class="step-title">Network Sysctl</div>
        <div class="step-desc">TCP BBR congestion control + larger socket buffers. Lower latency and better throughput on gigabit connections.</div>
      </div>
      <div class="step-card sys">
        <div class="step-num">STEP 11 · SYSTEM</div>
        <div class="step-title">Disable Unused Services</div>
        <div class="step-desc">Disables <code>ModemManager</code>, <code>cups</code>, <code>geoclue</code>. avahi and bluetooth are intentionally preserved — GNOME requires both.</div>
      </div>
      <div class="step-card sys">
        <div class="step-num">STEP 12 · SYSTEM</div>
        <div class="step-title">preload Daemon</div>
        <div class="step-desc">Adaptive read-ahead daemon. Learns which apps you launch and pre-loads them into RAM. Firefox opens noticeably faster after a few days.</div>
      </div>
      <div class="step-card sys">
        <div class="step-num">STEP 13 · SYSTEM</div>
        <div class="step-title">Journal Tuning</div>
        <div class="step-desc">Compresses journal entries and caps at 200 MB persistent / 50 MB runtime. Reduces SSD write amplification from systemd logging.</div>
      </div>
      <!-- GNOME steps -->
      <div class="step-card gnome">
        <div class="step-num">STEP 14 · GNOME</div>
        <div class="step-title">Disable Animations</div>
        <div class="step-desc">The single biggest perceived-speed win. Windows open, close, and minimise instantly — no fade, no zoom, no slide.</div>
      </div>
      <div class="step-card gnome">
        <div class="step-num">STEP 15 · GNOME</div>
        <div class="step-title">Disable Hot Corners</div>
        <div class="step-desc">Prevents accidental Activities triggers when cursor hits a corner. Eliminates an unnecessary compositor render pass.</div>
      </div>
      <div class="step-card gnome">
        <div class="step-num">STEP 16 · GNOME</div>
        <div class="step-title">Disable Search Providers</div>
        <div class="step-desc">Each provider spawns a subprocess when Activities opens. Disabling external providers eliminates 1–3 second lag on the overview.</div>
      </div>
      <div class="step-card gnome">
        <div class="step-num">STEP 17 · GNOME</div>
        <div class="step-title">Mask Tracker 3</div>
        <div class="step-desc">Tracker continuously indexes your home directory — sustained CPU spikes and SSD churn for days after install. Masked at the systemd user level.</div>
      </div>
      <div class="step-card gnome">
        <div class="step-num">STEP 18 · GNOME</div>
        <div class="step-title">Disable Background Updates</div>
        <div class="step-desc">GNOME Software silently downloads packages in the background. Disabled. Update manually with <code>sudo apt upgrade</code> when you want to.</div>
      </div>
      <div class="step-card gnome">
        <div class="step-num">STEP 19 · GNOME</div>
        <div class="step-title">Autostart Cleanup</div>
        <div class="step-desc">Belt-and-braces: disables Tracker and gnome-software <code>.desktop</code> autostart entries so masked services can't re-activate via autostart.</div>
      </div>
      <div class="step-card gnome">
        <div class="step-num">STEP 20 · GNOME</div>
        <div class="step-title">Power Profile: Performance</div>
        <div class="step-desc">Sets <strong>performance</strong> (falls back to balanced). Prevents the CPU from being silently throttled by <code>power-saver</code> mode.</div>
      </div>
      <div class="step-card gnome">
        <div class="step-num">STEP 21 · GNOME</div>
        <div class="step-title">Font Rendering</div>
        <div class="step-desc">Subpixel RGBA antialiasing + slight hinting. Crispest text on LCD monitors with minimal rendering overhead.</div>
      </div>
      <div class="step-card gnome">
        <div class="step-num">STEP 22 · GNOME</div>
        <div class="step-title">Mutter Responsiveness</div>
        <div class="step-desc"><code>check-alive-timeout = 30s</code> + <code>kms-modifiers</code>. No false "not responding" dialogs. Smoother compositing on Intel iGPU.</div>
      </div>
      <div class="step-card gnome">
        <div class="step-num">STEP 23 · GNOME</div>
        <div class="step-title">Privacy & Housekeeping</div>
        <div class="step-desc">Auto-clears trash/tmp after 30 days. Disables recent-files list. Location services off. Reduces background dconf writes and SSD wear.</div>
      </div>
      <div class="step-card gnome" style="border-color: rgba(245,166,35,0.3);">
        <div class="step-num" style="color: var(--amber);">STEP 24 · STATUS</div>
        <div class="step-title">Live Status Summary</div>
        <div class="step-desc">Prints real-time state of swap devices, fstrim, block I/O schedulers, and power profile so you can verify everything took effect immediately.</div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ══════════════════════════════════════════════════ INSTALL SECTION -->
<section id="install">
  <div class="wrap">
    <p class="section-eyebrow">Quick Start</p>
    <h2 class="section-title">Up and running in 60 seconds</h2>
    <p class="section-lead">
      Run from inside an active GNOME session using <code>sudo bash</code> — not <code>su -</code>.
      The script detects your user automatically.
    </p>

    <div class="install-block">
      <div class="install-step">
        <div class="install-num">1</div>
        <div style="flex:1">
          <div style="font-weight:700; color:#fff; margin-bottom:6px;">Download the script</div>
          <div class="install-cmd">
            <span>curl -fsSL https://raw.githubusercontent.com/administrakt0r/debian13-gnome-optimize/main/debian13-optimize.sh -o debian13-optimize.sh</span>
            <button class="copy-btn" onclick="copyCmd(this, 'curl -fsSL https://raw.githubusercontent.com/administrakt0r/debian13-gnome-optimize/main/debian13-optimize.sh -o debian13-optimize.sh')">COPY</button>
          </div>
        </div>
      </div>

      <div class="install-step">
        <div class="install-num">2</div>
        <div style="flex:1">
          <div style="font-weight:700; color:#fff; margin-bottom:6px;">Preview — dry run (zero changes)</div>
          <div class="install-cmd">
            <span>sudo bash debian13-optimize.sh --dry-run</span>
            <button class="copy-btn" onclick="copyCmd(this, 'sudo bash debian13-optimize.sh --dry-run')">COPY</button>
          </div>
        </div>
      </div>

      <div class="install-step">
        <div class="install-num">3</div>
        <div style="flex:1">
          <div style="font-weight:700; color:#fff; margin-bottom:6px;">Apply all optimisations</div>
          <div class="install-cmd">
            <span>sudo bash debian13-optimize.sh</span>
            <button class="copy-btn" onclick="copyCmd(this, 'sudo bash debian13-optimize.sh')">COPY</button>
          </div>
        </div>
      </div>

      <div class="install-step">
        <div class="install-num">4</div>
        <div style="flex:1">
          <div style="font-weight:700; color:#fff; margin-bottom:6px;">Reboot to apply all kernel-level changes</div>
          <div class="install-cmd">
            <span>sudo reboot</span>
            <button class="copy-btn" onclick="copyCmd(this, 'sudo reboot')">COPY</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ════════════════════════════════════════════════ WHY SECTION -->
<section id="why">
  <div class="wrap">
    <div style="display:grid; grid-template-columns:1fr 1fr; gap:60px; align-items:center;">
      <div>
        <p class="section-eyebrow">Why this script</p>
        <h2 class="section-title">Safe by design.<br>Fast by default.</h2>
        <p style="color:var(--text-dim); margin-bottom:32px; font-size:15px;">
          Most optimization guides are copy-paste fragments scattered across forum threads, many of them outdated, wrong for your hardware, or silently breaking GNOME.
          This script is different.
        </p>
        <ul class="feature-list">
          <li><strong>Idempotent</strong> — every step checks before acting. Safe to re-run any time.</li>
          <li><strong>write_file_if_changed()</strong> — files compared byte-for-byte before writing. Auto-backup on first change.</li>
          <li><strong>apply_gsetting()</strong> — verifies D-Bus socket + key writability before touching GNOME settings.</li>
          <li><strong>loginctl user detection</strong> — authoritative session detection, not fragile <code>who</code> parsing.</li>
          <li><strong>GNOME-safe service list</strong> — avahi and bluetooth preserved. Most scripts break GNOME by disabling them.</li>
          <li><strong>ZRAM-correct sysctl</strong> — <code>swappiness=100</code> is right with ZRAM. We don't copy settings tuned for spinning disks.</li>
          <li><strong>Debian 13 native</strong> — uses <code>systemd-zram-generator</code> and a systemd oneshot for CPU governor. No dead packages.</li>
          <li><strong>Full log</strong> — every action recorded to <code>/var/log/debian13-optimize.log</code>.</li>
        </ul>
      </div>
      <div>
        <div class="terminal">
          <div class="terminal-bar">
            <span class="dot dot-r"></span>
            <span class="dot dot-y"></span>
            <span class="dot dot-g"></span>
            <span class="terminal-title">safety checks in action</span>
          </div>
          <div class="terminal-body">
            <div class="t-info"># File writer — byte-compare before write</div>
            <div class="t-ok">[OK]     Unchanged: /etc/sysctl.d/99-desktop-zram.conf</div>
            <br>
            <div class="t-info"># gsettings — verify before set</div>
            <div class="t-out"># Checking D-Bus socket for dmina…</div>
            <div class="t-out"># Checking schema writable…</div>
            <div class="t-ok">[OK]     Set [dmina]: enable-animations = false</div>
            <br>
            <div class="t-info"># Package check — availability first</div>
            <div class="t-ok">[OK]     systemd-zram-generator — already installed.</div>
            <div class="t-out">[WARN]   cpufrequtils not available — using systemd</div>
            <div class="t-ok">[OK]     cpu-governor.service created and enabled.</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══════════════════════════════════════════════ PROMO SECTION -->
<section id="tools">
  <div class="wrap">
    <p class="section-eyebrow">From the same author</p>
    <h2 class="section-title">More free tools & resources</h2>
    <p class="section-lead">
      If you like free, no-nonsense tools built by someone who actually uses them — you'll like these too.
    </p>

    <div class="promo-grid">

      <!-- WPinEU -->
      <a href="https://WPinEU.com" target="_blank" rel="noopener" class="promo-card wp">
        <span class="promo-icon">🌍</span>
        <span class="promo-badge">Free Hosting</span>
        <h3>WPinEU.com</h3>
        <p>Free WordPress hosting in Europe. GDPR-friendly, no ads, no tracking, no credit card. Your site. Your data. On European infrastructure.</p>
        <span class="promo-link">Visit WPinEU.com</span>
      </a>

      <!-- LLM.kiwi -->
      <a href="https://LLM.kiwi" target="_blank" rel="noopener" class="promo-card llm">
        <span class="promo-icon">🤖</span>
        <span class="promo-badge">Free AI Tools</span>
        <h3>LLM.kiwi</h3>
        <p>Free AI tools and a free AI API endpoint. Use state-of-the-art language models without subscription walls or usage limits blocking your workflow.</p>
        <span class="promo-link">Visit LLM.kiwi</span>
      </a>

      <!-- GitHub -->
      <a href="https://github.com/administrakt0r" target="_blank" rel="noopener" class="promo-card gh">
        <span class="promo-icon">⚡</span>
        <span class="promo-badge">Open Source</span>
        <h3>GitHub Profile</h3>
        <p>More free scripts, tools, and automation projects. If it solves a real problem, it gets published. No paywalls. No newsletters. Just code.</p>
        <span class="promo-link">github.com/administrakt0r</span>
      </a>

    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ══════════════════════════════════════════════════════ FAQ -->
<section id="faq">
  <div class="wrap-sm">
    <p class="section-eyebrow">FAQ</p>
    <h2 class="section-title">Common questions</h2>

    <div class="faq-item">
      <div class="faq-q">Is this script safe to run on a production machine?</div>
      <div class="faq-a">Yes. Every file is backed up before modification, every step checks if already applied, and nothing is ever uninstalled. Run <code>--dry-run</code> first to see exactly what will change. The script exits immediately on any unexpected error.</div>
    </div>

    <div class="faq-item">
      <div class="faq-q">Why is swappiness set to 100 — isn't that bad?</div>
      <div class="faq-a">Only with disk swap. ZRAM swap lives entirely in RAM, so there is zero penalty for using it aggressively. <code>swappiness=100</code> tells the kernel to compress cold pages freely, freeing uncompressed RAM for active workloads. <code>swappiness=10</code> is the right setting for HDD/SSD swap — it would be wrong here.</div>
    </div>

    <div class="faq-item">
      <div class="faq-q">Why are avahi-daemon and bluetooth NOT disabled?</div>
      <div class="faq-a">GNOME Files (Nautilus) uses avahi mDNS to show network shares under "Other Locations" — disabling it causes Nautilus to stall on launch. GNOME Shell has native Bluetooth panel integration — disabling the daemon removes the BT toggle and causes gnome-shell errors. They're commented out with instructions if you genuinely don't need them.</div>
    </div>

    <div class="faq-item">
      <div class="faq-q">Does disabling Tracker 3 break GNOME Files?</div>
      <div class="faq-a">No. GNOME Files (Nautilus) works fully without Tracker. You only lose full-text file content search in the Activities overview search bar. You can still browse, open, copy, and move files normally.</div>
    </div>

    <div class="faq-item">
      <div class="faq-q">Can I run this on Debian 12 or Ubuntu?</div>
      <div class="faq-a">It's designed and tested on Debian 13 Trixie. Some steps (especially the systemd-zram-generator config and the cpu-governor.service) may work on Debian 12 or recent Ubuntu, but this is not officially tested. The <code>--dry-run</code> mode is your best friend for checking compatibility.</div>
    </div>

    <div class="faq-item">
      <div class="faq-q">How do I undo the changes?</div>
      <div class="faq-a">Every modified config file has a <code>.bak</code> backup next to it. GNOME settings can be reset with <code>gsettings reset &lt;schema&gt; &lt;key&gt;</code>. Services can be re-enabled with <code>systemctl enable --now &lt;service&gt;</code>. Masked user units with <code>systemctl --user unmask &lt;unit&gt;</code>. Full revert instructions are in the README.</div>
    </div>

    <div class="faq-item">
      <div class="faq-q">My hardware is different — will it still work?</div>
      <div class="faq-a">Yes for most steps. The I/O scheduler is auto-detected per device (NVMe vs SATA). The CPU governor is applied to all online CPU cores. ZRAM is sized relative to your actual RAM. The script is built to degrade gracefully — if something isn't available, it warns and continues.</div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══════════════════════════════════════════════════════ FOOTER -->
<footer>
  <div class="wrap">
    <div class="footer-grid">
      <div>
        <div class="footer-brand">administrakt0r</div>
        <p class="footer-about">Open source tools, scripts, and free infrastructure for developers and Linux users who want things to just work — fast, clean, and without nonsense.</p>
      </div>
      <div class="footer-col">
        <h4>This Project</h4>
        <a href="https://github.com/administrakt0r/debian13-gnome-optimize" target="_blank" rel="noopener">GitHub Repo</a>
        <a href="https://raw.githubusercontent.com/administrakt0r/debian13-gnome-optimize/main/debian13-optimize.sh" target="_blank" rel="noopener">Raw Script</a>
        <a href="https://github.com/administrakt0r/debian13-gnome-optimize/issues" target="_blank" rel="noopener">Report Issue</a>
        <a href="https://github.com/administrakt0r/debian13-gnome-optimize/blob/main/README.md" target="_blank" rel="noopener">README</a>
      </div>
      <div class="footer-col">
        <h4>More Free Tools</h4>
        <a href="https://WPinEU.com" target="_blank" rel="noopener">WPinEU.com</a>
        <a href="https://LLM.kiwi" target="_blank" rel="noopener">LLM.kiwi</a>
        <a href="https://github.com/administrakt0r" target="_blank" rel="noopener">GitHub Profile</a>
      </div>
    </div>

    <div class="footer-bottom">
      <p>© 2026 administrakt0r · MIT License · Made with ☕ and a relentless hatred of unnecessary lag.</p>
      <p>
        <a href="https://github.com/administrakt0r/debian13-gnome-optimize" target="_blank" rel="noopener">⭐ Star on GitHub</a>
        &nbsp;·&nbsp;
        <a href="https://github.com/administrakt0r/debian13-gnome-optimize/issues/new" target="_blank" rel="noopener">Report a Bug</a>
      </p>
    </div>
  </div>
</footer>

<!-- ════════════════════════════════════════════════════════ JS -->
<script>
  // ── Copy button ──────────────────────────────────────────────────
  function copyCmd(btn, text) {
    navigator.clipboard.writeText(text).then(() => {
      const orig = btn.textContent;
      btn.textContent = 'COPIED!';
      btn.style.background = 'rgba(57,255,143,0.3)';
      setTimeout(() => {
        btn.textContent = orig;
        btn.style.background = '';
      }, 2000);
    });
  }

  // ── Intersection Observer — animate cards on scroll ──────────────
  const obs = new IntersectionObserver((entries) => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        e.target.style.animationDelay = (i * 0.05) + 's';
        e.target.classList.add('fade-up');
        obs.unobserve(e.target);
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.step-card, .promo-card, .stat-box').forEach(el => obs.observe(el));

  // ── FAQ accordion ────────────────────────────────────────────────
  document.querySelectorAll('.faq-q').forEach(q => {
    const a = q.nextElementSibling;
    a.style.display = 'none';
    q.addEventListener('click', () => {
      const open = a.style.display === 'block';
      document.querySelectorAll('.faq-a').forEach(x => x.style.display = 'none');
      document.querySelectorAll('.faq-q').forEach(x => x.style.setProperty('--after-content', '"+"'));
      if (!open) {
        a.style.display = 'block';
        q.style.color = 'var(--green)';
      } else {
        q.style.color = '';
      }
    });
  });
</script>
</body>
</html>
