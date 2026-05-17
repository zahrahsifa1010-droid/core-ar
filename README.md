<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>CORE-AR – Energi Terbarukan & AI-Buddy</title>
  <meta name="description" content="Peningkatan pemahaman konsep energi terbarukan berbasis teknologi Augmented Reality dan AI-Buddy untuk siswa SD." />

  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Exo+2:ital,wght@0,400;0,600;0,800;1,600&display=swap" rel="stylesheet" />

  <!-- Model Viewer CDN -->
  <script type="module" src="https://ajax.googleapis.com/ajax/libs/model-viewer/3.4.0/model-viewer.min.js"></script>

  <style>
    /* ─── CSS Variables ─────────────────────────────── */
    :root {
      --bg:       #050d1a;
      --bg2:      #091424;
      --bg3:      #0d1f36;
      --teal:     #00e5c3;
      --teal-d:   #00b89c;
      --blue:     #0ea5e9;
      --yellow:   #fbbf24;
      --green:    #22c55e;
      --red:      #ef4444;
      --purple:   #a855f7;
      --text:     #e2eaf4;
      --muted:    #6b8cae;
      --border:   rgba(0,229,195,.13);
      --card-bg:  rgba(13,31,54,.85);
      --glow:     0 0 40px rgba(0,229,195,.15);
      --radius:   18px;
      --font-head: 'Exo 2', sans-serif;
      --font-body: 'Space Grotesk', sans-serif;
    }

    /* ─── Reset & Base ──────────────────────────────── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      font-family: var(--font-body);
      background: var(--bg);
      color: var(--text);
      overflow-x: hidden;
      -webkit-font-smoothing: antialiased;
    }
    a { text-decoration: none; color: inherit; }
    button { cursor: pointer; font-family: var(--font-body); border: none; }
    img { max-width: 100%; display: block; }

    /* ─── Grid BG ───────────────────────────────────── */
    body::before {
      content: '';
      position: fixed; inset: 0; z-index: 0; pointer-events: none;
      background-image:
        linear-gradient(rgba(0,229,195,.04) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0,229,195,.04) 1px, transparent 1px);
      background-size: 40px 40px;
    }

    /* ─── Navbar ────────────────────────────────────── */
    .navbar {
      position: fixed; top: 0; left: 0; right: 0; z-index: 100;
      display: flex; align-items: center; justify-content: space-between;
      padding: 14px 20px;
      background: rgba(5,13,26,.88);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border-bottom: 1px solid var(--border);
    }
    .navbar-logo {
      display: flex; align-items: center; gap: 10px;
    }
    .logo-icon {
      width: 36px; height: 36px; border-radius: 10px;
      background: linear-gradient(135deg, var(--teal), var(--blue));
      display: flex; align-items: center; justify-content: center;
      font-size: 1.2rem; font-weight: 900; color: #fff;
      font-family: var(--font-head); letter-spacing: -1px;
      box-shadow: 0 0 20px rgba(0,229,195,.4);
      flex-shrink: 0;
    }
    .logo-text {
      font-family: var(--font-head); font-weight: 800; font-size: 1.1rem;
      color: var(--text); line-height: 1.1;
    }
    .logo-text span {
      display: block; font-size: .6rem; font-family: var(--font-body);
      color: var(--muted); font-weight: 500; letter-spacing: .04em;
    }
    .navbar-badge {
      background: linear-gradient(135deg, var(--teal), var(--blue));
      color: #050d1a; font-size: .72rem; font-weight: 700;
      padding: 7px 14px; border-radius: 50px;
      letter-spacing: .03em;
    }

    /* ─── Hero ──────────────────────────────────────── */
    .hero {
      min-height: 100svh;
      padding: 100px 22px 64px;
      display: flex; flex-direction: column; justify-content: center;
      position: relative; overflow: hidden;
    }
    .hero-glow {
      position: absolute; top: -40px; left: 50%; transform: translateX(-50%);
      width: 340px; height: 340px; border-radius: 50%;
      background: radial-gradient(circle, rgba(0,229,195,.14) 0%, transparent 70%);
      pointer-events: none;
    }
    .hero-orbit {
      position: absolute; top: 60px; right: -60px;
      width: 260px; height: 260px; border-radius: 50%;
      border: 1px dashed rgba(0,229,195,.15);
      animation: spin 20s linear infinite;
    }
    .hero-orbit::after {
      content: '⚡'; position: absolute; top: -12px; left: 50%;
      transform: translateX(-50%);
      font-size: 1.2rem;
    }
    @keyframes spin { to { transform: rotate(360deg); } }

    .hero-tag {
      display: inline-flex; align-items: center; gap: 8px;
      border: 1px solid var(--border);
      background: rgba(0,229,195,.06);
      color: var(--teal); border-radius: 50px;
      font-size: .72rem; font-weight: 700; letter-spacing: .06em; text-transform: uppercase;
      padding: 6px 14px; margin-bottom: 22px; width: fit-content;
    }
    .hero-tag::before {
      content: ''; width: 7px; height: 7px; border-radius: 50%;
      background: var(--teal); animation: pulse 2s infinite;
    }
    @keyframes pulse { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:.4;transform:scale(1.5)} }

    .hero h1 {
      font-family: var(--font-head);
      font-size: clamp(2.2rem, 9vw, 3.6rem);
      font-weight: 800; line-height: 1.1;
      color: #fff; margin-bottom: 6px;
      letter-spacing: -1px;
    }
    .hero h1 .accent { color: var(--teal); }
    .hero-sub {
      font-size: clamp(.9rem, 3vw, 1.05rem);
      color: var(--muted); line-height: 1.7;
      margin-bottom: 36px; max-width: 420px;
      font-weight: 500;
    }
    .hero-btns { display: flex; flex-direction: column; gap: 12px; }
    .btn-primary {
      background: linear-gradient(135deg, var(--teal), var(--blue));
      color: #050d1a; padding: 16px 28px; border-radius: 50px;
      font-size: 1rem; font-weight: 700;
      display: flex; align-items: center; justify-content: center; gap: 10px;
      box-shadow: 0 6px 30px rgba(0,229,195,.3);
      transition: transform .2s, box-shadow .2s;
    }
    .btn-primary:active { transform: scale(.97); }
    .btn-outline {
      background: transparent; color: var(--teal);
      padding: 15px 28px; border-radius: 50px;
      font-size: 1rem; font-weight: 700;
      border: 1.5px solid rgba(0,229,195,.35);
      display: flex; align-items: center; justify-content: center; gap: 10px;
      transition: background .2s;
    }
    .btn-outline:active { background: rgba(0,229,195,.08); }

    /* Hero visual grid */
    .hero-visual {
      margin-top: 52px;
      display: grid; grid-template-columns: repeat(3,1fr); gap: 10px;
    }
    .hero-vcard {
      border-radius: 16px; aspect-ratio: 3/4;
      display: flex; flex-direction: column;
      align-items: center; justify-content: center;
      gap: 8px; font-size: 2.4rem;
      border: 1px solid var(--border);
      position: relative; overflow: hidden;
    }
    .hero-vcard::before {
      content: ''; position: absolute; inset: 0;
      background: linear-gradient(180deg, transparent 40%, rgba(0,229,195,.08));
    }
    .hero-vcard span.label {
      font-size: .65rem; font-weight: 700; letter-spacing: .08em;
      text-transform: uppercase; color: var(--teal); font-family: var(--font-body);
    }
    .hero-vcard:nth-child(1) { background: linear-gradient(135deg,#061824,#0a2535); margin-top: 28px; }
    .hero-vcard:nth-child(2) { background: linear-gradient(135deg,#061824,#0a2030); }
    .hero-vcard:nth-child(3) { background: linear-gradient(135deg,#061824,#12202e); margin-top: 44px; }

    /* ─── Section Common ────────────────────────────── */
    section { padding: 64px 20px; position: relative; z-index: 1; }
    .section-label {
      font-size: .68rem; font-weight: 700; letter-spacing: .14em;
      text-transform: uppercase; color: var(--teal); margin-bottom: 10px;
    }
    .section-title {
      font-family: var(--font-head); font-weight: 800;
      font-size: clamp(1.6rem, 5.5vw, 2.4rem);
      color: #fff; line-height: 1.15; margin-bottom: 12px;
      letter-spacing: -.5px;
    }
    .section-sub { color: var(--muted); line-height: 1.7; font-size: .92rem; font-weight: 500; }
    .divider {
      width: 44px; height: 3px; border-radius: 2px;
      background: linear-gradient(90deg, var(--teal), var(--blue));
      margin: 14px 0 32px;
    }

    /* ─── Stats Bar ─────────────────────────────────── */
    .stats-bar {
      background: var(--bg2); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);
      padding: 24px 20px;
    }
    .stats-grid { display: grid; grid-template-columns: repeat(3,1fr); gap: 4px; }
    .stat-item { text-align: center; padding: 12px 4px; }
    .stat-num {
      font-family: var(--font-head); font-size: 1.7rem; font-weight: 800;
      color: var(--teal); line-height: 1; margin-bottom: 4px;
    }
    .stat-label { font-size: .68rem; color: var(--muted); font-weight: 600; letter-spacing: .04em; }

    /* ─── How it Works (dark) ───────────────────────── */
    .how-bg {
      background: var(--bg2);
      border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);
    }
    .steps { display: flex; flex-direction: column; gap: 16px; margin-top: 28px; }
    .step {
      display: flex; align-items: flex-start; gap: 16px;
      background: var(--card-bg);
      border: 1px solid var(--border); border-radius: var(--radius);
      padding: 18px; animation: fadeUp .5s ease both;
    }
    .step:nth-child(1){animation-delay:.05s}
    .step:nth-child(2){animation-delay:.15s}
    .step:nth-child(3){animation-delay:.25s}
    .step:nth-child(4){animation-delay:.35s}
    @keyframes fadeUp { from{opacity:0;transform:translateY(16px)} to{opacity:1;transform:none} }
    .step-num {
      width: 38px; height: 38px; flex-shrink: 0; border-radius: 50%;
      background: linear-gradient(135deg, var(--teal), var(--blue));
      color: #050d1a; font-weight: 800; font-size: .9rem;
      display: flex; align-items: center; justify-content: center;
    }
    .step-body h3 { color: #fff; font-size: .92rem; font-weight: 700; margin-bottom: 4px; }
    .step-body p { color: var(--muted); font-size: .83rem; line-height: 1.55; }

    /* ─── Features Grid ─────────────────────────────── */
    .features-grid { display: flex; flex-direction: column; gap: 18px; margin-top: 28px; }
    .feature-card {
      background: var(--card-bg);
      border: 1px solid var(--border); border-radius: var(--radius);
      padding: 22px; position: relative; overflow: hidden;
      cursor: pointer; transition: border-color .2s, box-shadow .2s;
    }
    .feature-card::before {
      content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px;
      background: linear-gradient(90deg, var(--teal), var(--blue));
      opacity: 0; transition: opacity .2s;
    }
    .feature-card:active { border-color: var(--teal); box-shadow: var(--glow); }
    .feature-card.open::before { opacity: 1; }
    .feature-card.open { border-color: rgba(0,229,195,.35); box-shadow: var(--glow); }
    .feat-header { display: flex; align-items: flex-start; gap: 14px; }
    .feat-icon {
      width: 48px; height: 48px; border-radius: 14px; flex-shrink: 0;
      display: flex; align-items: center; justify-content: center;
      font-size: 1.5rem;
      border: 1px solid var(--border);
    }
    .feat-meta { flex: 1; }
    .feat-num { font-size: .62rem; font-weight: 700; letter-spacing: .12em; text-transform: uppercase; color: var(--teal); margin-bottom: 4px; }
    .feat-title { font-family: var(--font-head); font-size: 1rem; font-weight: 700; color: #fff; line-height: 1.25; }
    .feat-chevron {
      font-size: .85rem; color: var(--muted); transition: transform .3s; margin-top: 2px; flex-shrink: 0;
    }
    .feature-card.open .feat-chevron { transform: rotate(180deg); }
    .feat-body {
      max-height: 0; overflow: hidden; transition: max-height .4s cubic-bezier(.4,0,.2,1);
    }
    .feature-card.open .feat-body { max-height: 600px; }
    .feat-body-inner { padding-top: 16px; }
    .feat-desc { font-size: .87rem; color: var(--muted); line-height: 1.7; margin-bottom: 14px; }
    .feat-points { display: flex; flex-direction: column; gap: 10px; }
    .feat-point {
      display: flex; align-items: flex-start; gap: 10px;
      background: rgba(0,229,195,.05); border-radius: 12px;
      padding: 12px; border: 1px solid rgba(0,229,195,.09);
    }
    .feat-point-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; margin-top: 4px; }
    .feat-point p { font-size: .83rem; color: var(--muted); line-height: 1.6; }
    .feat-point p strong { color: var(--text); }
    .feat-tag {
      display: inline-flex; align-items: center; gap: 6px;
      font-size: .65rem; font-weight: 700; letter-spacing: .06em;
      text-transform: uppercase; padding: 4px 10px; border-radius: 6px;
      margin-top: 14px;
    }

    /* ─── Virtual Lab ───────────────────────────────── */
    .lab-bg {
      background: var(--bg2);
      border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);
    }
    .lab-panel {
      background: var(--card-bg); border: 1px solid var(--border);
      border-radius: var(--radius); padding: 22px; margin-top: 28px;
    }
    .lab-formula {
      text-align: center; margin-bottom: 22px;
    }
    .formula-box {
      display: inline-block;
      background: rgba(0,229,195,.08); border: 1px solid rgba(0,229,195,.2);
      border-radius: 12px; padding: 14px 28px;
      font-family: var(--font-head); font-size: 1.5rem; font-weight: 800;
      color: var(--teal); letter-spacing: 2px;
    }
    .formula-box sub { font-size: .8rem; color: var(--blue); }
    .slider-group { display: flex; flex-direction: column; gap: 18px; }
    .slider-row { display: flex; flex-direction: column; gap: 8px; }
    .slider-label {
      display: flex; justify-content: space-between; align-items: center;
    }
    .slider-label span:first-child { font-size: .85rem; font-weight: 600; color: var(--text); }
    .slider-val {
      font-family: var(--font-head); font-size: .95rem; font-weight: 800; color: var(--teal);
    }
    input[type="range"] {
      -webkit-appearance: none; width: 100%; height: 6px;
      background: rgba(255,255,255,.1); border-radius: 3px; outline: none;
    }
    input[type="range"]::-webkit-slider-thumb {
      -webkit-appearance: none; width: 22px; height: 22px; border-radius: 50%;
      background: linear-gradient(135deg, var(--teal), var(--blue));
      box-shadow: 0 0 12px rgba(0,229,195,.4); cursor: pointer;
    }
    .power-display {
      margin-top: 22px; text-align: center;
      background: linear-gradient(135deg, rgba(0,229,195,.08), rgba(14,165,233,.08));
      border: 1px solid rgba(0,229,195,.2); border-radius: 16px; padding: 20px;
    }
    .power-label { font-size: .72rem; font-weight: 700; letter-spacing: .1em; text-transform: uppercase; color: var(--muted); margin-bottom: 6px; }
    .power-num {
      font-family: var(--font-head); font-size: 2.4rem; font-weight: 800;
      color: var(--teal); line-height: 1;
    }
    .power-num span { font-size: 1rem; color: var(--muted); font-weight: 500; }
    .mcb-status {
      margin-top: 14px; display: flex; align-items: center; justify-content: center; gap: 8px;
      font-size: .82rem; font-weight: 600;
    }
    .mcb-dot { width: 10px; height: 10px; border-radius: 50%; }
    .mcb-ok { color: var(--green); }
    .mcb-dot-ok { background: var(--green); animation: pulse 2s infinite; }
    .mcb-warn { color: var(--yellow); }
    .mcb-dot-warn { background: var(--yellow); }
    .mcb-trip { color: var(--red); }
    .mcb-dot-trip { background: var(--red); animation: pulse .5s infinite; }

    /* Appliances */
    .appliances { margin-top: 18px; }
    .app-label { font-size: .72rem; font-weight: 700; letter-spacing: .1em; text-transform: uppercase; color: var(--muted); margin-bottom: 12px; }
    .app-grid { display: grid; grid-template-columns: repeat(2,1fr); gap: 10px; }
    .app-item {
      display: flex; align-items: center; gap: 10px;
      background: rgba(255,255,255,.04); border: 1px solid var(--border);
      border-radius: 12px; padding: 12px;
      cursor: pointer; transition: background .18s, border-color .18s;
      user-select: none;
    }
    .app-item.on { background: rgba(0,229,195,.07); border-color: rgba(0,229,195,.25); }
    .app-icon { font-size: 1.4rem; }
    .app-info { flex: 1; }
    .app-name { font-size: .8rem; font-weight: 700; color: var(--text); line-height: 1.2; }
    .app-watt { font-size: .7rem; color: var(--muted); }
    .app-toggle {
      width: 32px; height: 18px; border-radius: 9px;
      background: rgba(255,255,255,.1); position: relative; transition: background .2s; flex-shrink: 0;
    }
    .app-toggle::after {
      content: ''; position: absolute; top: 2px; left: 2px;
      width: 14px; height: 14px; border-radius: 50%;
      background: #fff; transition: transform .2s;
    }
    .app-item.on .app-toggle { background: var(--teal); }
    .app-item.on .app-toggle::after { transform: translateX(14px); }

    /* ─── Game Section ──────────────────────────────── */
    .game-bg {
      background: linear-gradient(160deg, #08001a, var(--bg2) 60%);
      border-top: 1px solid rgba(168,85,247,.2);
    }
    .game-bg .section-label { color: var(--purple); }
    .game-bg .divider { background: linear-gradient(90deg, var(--purple), var(--blue)); }
    .game-banner {
      margin-top: 28px;
      background: linear-gradient(135deg, rgba(168,85,247,.12), rgba(14,165,233,.12));
      border: 1px solid rgba(168,85,247,.22); border-radius: var(--radius); padding: 28px 20px;
      text-align: center; position: relative; overflow: hidden;
    }
    .game-banner-title {
      font-family: var(--font-head); font-size: 1.4rem; font-weight: 800;
      color: #fff; margin-bottom: 6px;
    }
    .game-banner-sub { font-size: .85rem; color: var(--muted); line-height: 1.65; margin-bottom: 22px; }
    .game-features { display: flex; flex-direction: column; gap: 12px; text-align: left; }
    .game-feat {
      display: flex; align-items: flex-start; gap: 12px;
      background: rgba(255,255,255,.04); border-radius: 12px; padding: 14px;
      border: 1px solid rgba(168,85,247,.12);
    }
    .game-feat-icon { font-size: 1.3rem; flex-shrink: 0; }
    .game-feat-body h4 { font-size: .85rem; font-weight: 700; color: #fff; margin-bottom: 3px; }
    .game-feat-body p { font-size: .8rem; color: var(--muted); line-height: 1.55; }
    .pelajar-badge {
      display: inline-flex; align-items: center; gap: 8px;
      background: rgba(251,191,36,.1); border: 1px solid rgba(251,191,36,.25);
      border-radius: 50px; padding: 8px 16px; margin-top: 18px;
      font-size: .78rem; font-weight: 700; color: var(--yellow);
    }

    /* ─── Kamusku / Dictionary ──────────────────────── */
    .kamus-panel {
      background: var(--card-bg); border: 1px solid var(--border);
      border-radius: var(--radius); margin-top: 28px; overflow: hidden;
    }
    .kamus-head {
      padding: 18px 20px;
      border-bottom: 1px solid var(--border);
      display: flex; align-items: center; gap: 12px;
    }
    .kamus-head-icon {
      width: 40px; height: 40px; border-radius: 12px;
      background: linear-gradient(135deg, var(--green), var(--teal));
      display: flex; align-items: center; justify-content: center; font-size: 1.3rem; flex-shrink: 0;
    }
    .kamus-head h3 { font-family: var(--font-head); font-size: 1rem; font-weight: 700; color: #fff; margin-bottom: 2px; }
    .kamus-head p { font-size: .75rem; color: var(--muted); }
    .kamus-entries { padding: 16px; display: flex; flex-direction: column; gap: 10px; }
    .kamus-entry {
      background: rgba(255,255,255,.04); border: 1px solid var(--border);
      border-radius: 12px; padding: 14px;
    }
    .kamus-entry-term {
      font-family: var(--font-head); font-size: .9rem; font-weight: 700;
      color: var(--teal); margin-bottom: 4px;
      display: flex; align-items: center; gap: 8px;
    }
    .kamus-badge {
      font-size: .6rem; font-weight: 800; letter-spacing: .06em; text-transform: uppercase;
      padding: 2px 7px; border-radius: 6px; background: rgba(0,229,195,.12); color: var(--teal);
    }
    .kamus-entry-def { font-size: .82rem; color: var(--muted); line-height: 1.6; }
    .kamus-entry-meta { font-size: .7rem; color: rgba(107,140,174,.6); margin-top: 6px; }
    .kamus-add {
      margin: 0 16px 16px;
      display: flex; align-items: center; gap: 10px;
    }
    .kamus-input {
      flex: 1; background: rgba(255,255,255,.05); border: 1px solid var(--border);
      border-radius: 10px; padding: 10px 14px; color: var(--text);
      font-family: var(--font-body); font-size: .85rem; outline: none;
    }
    .kamus-input::placeholder { color: var(--muted); }
    .kamus-input:focus { border-color: rgba(0,229,195,.4); }
    .kamus-btn {
      background: linear-gradient(135deg, var(--teal), var(--blue));
      color: #050d1a; padding: 10px 16px; border-radius: 10px;
      font-size: .82rem; font-weight: 700; white-space: nowrap;
    }

    /* ─── Energy Exploration ────────────────────────── */
    .energy-cards { display: flex; flex-direction: column; gap: 16px; margin-top: 28px; }
    .energy-card {
      background: var(--card-bg); border: 1px solid var(--border);
      border-radius: var(--radius); overflow: hidden;
    }
    .energy-card-top {
      padding: 20px; display: flex; gap: 14px; align-items: flex-start;
    }
    .energy-icon {
      width: 52px; height: 52px; border-radius: 14px; flex-shrink: 0;
      display: flex; align-items: center; justify-content: center; font-size: 1.7rem;
    }
    .energy-name { font-family: var(--font-head); font-size: 1rem; font-weight: 700; color: #fff; margin-bottom: 4px; }
    .energy-desc { font-size: .82rem; color: var(--muted); line-height: 1.55; }
    .energy-bar-wrap { padding: 0 20px 20px; }
    .energy-bar-label { display: flex; justify-content: space-between; font-size: .72rem; font-weight: 700; color: var(--muted); margin-bottom: 6px; }
    .energy-bar-track { background: rgba(255,255,255,.08); border-radius: 4px; height: 8px; overflow: hidden; }
    .energy-bar-fill { height: 100%; border-radius: 4px; transition: width 1.2s cubic-bezier(.4,0,.2,1); }
    .energy-compare { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; padding: 0 20px 20px; }
    .energy-cmp-item { background: rgba(255,255,255,.04); border-radius: 10px; padding: 10px; text-align: center; }
    .energy-cmp-val { font-family: var(--font-head); font-size: 1rem; font-weight: 800; margin-bottom: 2px; }
    .energy-cmp-label { font-size: .68rem; color: var(--muted); font-weight: 600; }

    /* ─── AR Demo Modal ─────────────────────────────── */
    .modal-overlay {
      display: none; position: fixed; inset: 0; z-index: 200;
      background: rgba(5,13,26,.85); backdrop-filter: blur(8px);
      overflow-y: auto; padding: 20px 0 80px;
    }
    .modal-overlay.open { display: block; animation: fadeIn .2s ease; }
    @keyframes fadeIn { from{opacity:0} to{opacity:1} }
    .modal {
      background: var(--bg3); border: 1px solid var(--border);
      border-radius: 24px 24px 0 0;
      position: absolute; bottom: 0; left: 0; right: 0;
      animation: slideUp .3s cubic-bezier(.25,.8,.25,1);
      max-height: 92svh; overflow-y: auto;
    }
    @keyframes slideUp { from{transform:translateY(60px);opacity:0} to{transform:none;opacity:1} }
    .modal-handle { width: 40px; height: 4px; border-radius: 2px; background: var(--border); margin: 12px auto 0; }
    .modal-close {
      position: absolute; top: 14px; right: 16px;
      width: 34px; height: 34px; border-radius: 50%;
      background: rgba(255,255,255,.07); color: var(--muted);
      font-size: 1rem; display: flex; align-items: center; justify-content: center;
    }
    .modal-img {
      width: 100%; height: 260px;
      display: flex; align-items: center; justify-content: center; font-size: 6rem;
      position: relative; overflow: hidden;
    }
    .modal-content { padding: 20px 20px 32px; }
    .modal-label { font-size: .68rem; font-weight: 800; letter-spacing: .12em; text-transform: uppercase; color: var(--teal); margin-bottom: 8px; }
    .modal-name { font-family: var(--font-head); font-size: 1.5rem; font-weight: 800; color: #fff; margin-bottom: 10px; }
    .modal-desc { font-size: .88rem; color: var(--muted); line-height: 1.7; margin-bottom: 22px; }
    .modal-ar-box {
      background: linear-gradient(135deg, rgba(0,229,195,.08), rgba(14,165,233,.06));
      border: 1px solid rgba(0,229,195,.2); border-radius: 16px; padding: 20px; margin-bottom: 16px;
    }
    .modal-ar-title { font-weight: 700; font-size: .95rem; color: #fff; margin-bottom: 6px; }
    .modal-ar-sub { color: var(--muted); font-size: .82rem; margin-bottom: 16px; line-height: 1.5; }
    .btn-ar {
      width: 100%; padding: 14px;
      background: linear-gradient(135deg, var(--teal), var(--blue));
      color: #050d1a; border-radius: 12px;
      font-size: 1rem; font-weight: 800;
      display: flex; align-items: center; justify-content: center; gap: 8px;
    }
    .mv-container { width: 100%; background: var(--bg2); }
    .mv-container model-viewer { width: 100%; height: 280px; }
    .mv-hint { text-align: center; font-size: .72rem; color: var(--muted); padding: 8px; }
    .ar-fallback {
      background: rgba(251,191,36,.07); border-radius: 10px;
      padding: 12px; margin-top: 12px;
      border-left: 3px solid var(--yellow); display: none;
    }
    .ar-fallback p { font-size: .8rem; color: var(--muted); line-height: 1.6; }
    .ar-fallback strong { color: var(--yellow); }

    /* ─── Testimonials ──────────────────────────────── */
    .testi-scroll { display: flex; gap: 14px; overflow-x: auto; padding: 4px 0 14px; margin-top: 24px; }
    .testi-scroll::-webkit-scrollbar { display: none; }
    .testi-card {
      flex-shrink: 0; width: 250px;
      background: var(--card-bg); border: 1px solid var(--border);
      border-radius: var(--radius); padding: 18px;
    }
    .testi-stars { color: var(--yellow); font-size: .9rem; margin-bottom: 10px; }
    .testi-text { font-size: .85rem; color: var(--muted); line-height: 1.65; margin-bottom: 14px; font-style: italic; }
    .testi-author { font-weight: 700; font-size: .8rem; color: #fff; }
    .testi-loc { font-size: .72rem; color: var(--muted); }

    /* ─── Footer ────────────────────────────────────── */
    footer {
      background: var(--bg2);
      border-top: 1px solid var(--border);
      padding: 48px 20px 100px; text-align: center;
    }
    .footer-logo {
      font-family: var(--font-head); font-weight: 800; font-size: 1.6rem;
      color: var(--teal); margin-bottom: 4px;
    }
    .footer-tagline { font-size: .82rem; color: var(--muted); margin-bottom: 24px; }
    .footer-divider { width: 40px; height: 2px; background: var(--teal); margin: 0 auto 20px; border-radius: 1px; }
    .footer-links { display: flex; flex-wrap: wrap; justify-content: center; gap: 10px 18px; margin-bottom: 28px; }
    .footer-links a { color: var(--muted); font-size: .82rem; transition: color .18s; }
    .footer-links a:hover { color: var(--teal); }
    .footer-copy { font-size: .73rem; color: rgba(107,140,174,.45); }
    .footer-logos { display: flex; justify-content: center; gap: 14px; margin-bottom: 24px; flex-wrap: wrap; }
    .footer-logo-item {
      background: rgba(255,255,255,.05); border: 1px solid var(--border);
      border-radius: 10px; padding: 8px 16px;
      font-size: .72rem; font-weight: 700; color: var(--muted);
    }

    /* ─── Scroll reveal ─────────────────────────────── */
    .reveal { opacity: 0; transform: translateY(20px); transition: opacity .55s ease, transform .55s ease; }
    .reveal.visible { opacity: 1; transform: none; }

    /* ─── Floating helper ───────────────────────────── */
    .fab {
      position: fixed; bottom: 24px; right: 20px; z-index: 150;
      background: linear-gradient(135deg, var(--teal), var(--blue));
      color: #050d1a; width: 54px; height: 54px; border-radius: 50%;
      display: flex; align-items: center; justify-content: center; font-size: 1.4rem;
      box-shadow: 0 4px 24px rgba(0,229,195,.35);
      transition: transform .2s;
    }
    .fab:active { transform: scale(.93); }
    .fab-pulse {
      position: absolute; inset: -4px; border-radius: 50%;
      border: 2px solid var(--teal); animation: waPulse 2s infinite;
    }
    @keyframes waPulse { 0%{opacity:.7;transform:scale(1)} 100%{opacity:0;transform:scale(1.65)} }

    /* ─── AR Marker scan animation ──────────────────── */
    .ar-scan-wrap {
      position: relative; width: 100%; height: 200px;
      background: linear-gradient(135deg, #061a2a, #08101e);
      display: flex; align-items: center; justify-content: center; overflow: hidden;
    }
    .ar-scan-box {
      width: 120px; height: 120px; position: relative;
    }
    .ar-scan-box::before, .ar-scan-box::after {
      content: ''; position: absolute;
      width: 30px; height: 30px; border-color: var(--teal); border-style: solid;
    }
    .ar-scan-box::before { top: 0; left: 0; border-width: 3px 0 0 3px; }
    .ar-scan-box::after  { bottom: 0; right: 0; border-width: 0 3px 3px 0; }
    .ar-scan-line {
      position: absolute; top: 0; left: 0; right: 0; height: 2px;
      background: linear-gradient(90deg, transparent, var(--teal), transparent);
      animation: scanLine 2s ease-in-out infinite;
    }
    @keyframes scanLine { 0%{top:0;opacity:1} 100%{top:100%;opacity:.3} }
    .ar-scan-icon { font-size: 2.5rem; }
    .ar-scan-corners-br, .ar-scan-corners-tl {
      position: absolute; width: 30px; height: 30px;
      border-color: var(--teal); border-style: solid;
    }
    .ar-scan-corners-br { bottom: 0; left: 0; border-width: 0 0 3px 3px; }
    .ar-scan-corners-tl { top: 0; right: 0; border-width: 3px 3px 0 0; }
  </style>
</head>
<body>

<!-- ════════════════════════════════════════════════════
     NAV
════════════════════════════════════════════════════ -->
<nav class="navbar">
  <div class="navbar-logo">
    <div class="logo-icon">C</div>
    <div class="logo-text">
      CORE-AR
      <span>Energi Terbarukan</span>
    </div>
  </div>
  <div class="navbar-badge">AI-Buddy ✦</div>
</nav>

<!-- ════════════════════════════════════════════════════
     HERO
════════════════════════════════════════════════════ -->
<section class="hero" id="beranda">
  <div class="hero-glow"></div>
  <div class="hero-orbit"></div>

  <div class="hero-tag">✦ Augmented Reality & AI</div>

  <h1>CORE<span class="accent">-AR</span></h1>
  <p class="hero-sub">Peningkatan pemahaman konsep energi terbarukan berbasis teknologi Augmented Reality dan AI-Buddy untuk siswa Sekolah Dasar.</p>

  <div class="hero-btns">
    <button class="btn-primary" onclick="scrollToFeatures()">
      🔋 Jelajahi Fitur
    </button>
    <button class="btn-outline" onclick="openModal('solar')">
      📱 Coba AR Demo
    </button>
  </div>

  <div class="hero-visual">
    <div class="hero-vcard">
      <span>☀️</span>
      <span class="label">Panel Surya</span>
    </div>
    <div class="hero-vcard">
      <span>💨</span>
      <span class="label">Turbin Angin</span>
    </div>
    <div class="hero-vcard">
      <span>💧</span>
      <span class="label">Turbin Air</span>
    </div>
  </div>
</section>

<!-- ════════════════════════════════════════════════════
     STATS BAR
════════════════════════════════════════════════════ -->
<div class="stats-bar reveal">
  <div class="stats-grid">
    <div class="stat-item">
      <div class="stat-num">45%</div>
      <div class="stat-label">Kesulitan Interpretasi Konsep</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">5</div>
      <div class="stat-label">Fitur Interaktif AR</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">∞</div>
      <div class="stat-label">Eksplorasi Mandiri</div>
    </div>
  </div>
</div>

<!-- ════════════════════════════════════════════════════
     HOW IT WORKS
════════════════════════════════════════════════════ -->
<section class="how-bg reveal" id="cara-pakai">
  <div class="section-label">Panduan Penggunaan</div>
  <h2 class="section-title">Cara Menggunakan CORE-AR</h2>
  <p class="section-sub">4 langkah mudah untuk mulai belajar energi terbarukan dengan teknologi AR.</p>
  <div class="divider"></div>

  <div class="steps">
    <div class="step">
      <div class="step-num">1</div>
      <div class="step-body">
        <h3>Scan Marker AR</h3>
        <p>Arahkan kamera perangkatmu ke marker AR yang tersedia di buku atau poster kelas. Tidak perlu instal aplikasi apapun.</p>
      </div>
    </div>
    <div class="step">
      <div class="step-num">2</div>
      <div class="step-body">
        <h3>Pilih Objek Energi</h3>
        <p>Objek 3D energi terbarukan akan muncul — kincir angin, panel surya, atau turbin air. Kamu bisa memutarnya dan melihat dari berbagai sudut.</p>
      </div>
    </div>
    <div class="step">
      <div class="step-num">3</div>
      <div class="step-body">
        <h3>Jelaskan ke AI-Buddy</h3>
        <p>Tekan tombol mikrofon dan jelaskan apa yang kamu lihat. AI-Buddy akan merespons dan membantu kamu merumuskan definisi sendiri.</p>
      </div>
    </div>
    <div class="step">
      <div class="step-num">4</div>
      <div class="step-body">
        <h3>Simpan di Kamusku</h3>
        <p>Definisi yang kamu buat tersimpan otomatis di "Kamusku" sebagai catatan pribadi yang bisa kamu baca kapan saja.</p>
      </div>
    </div>
  </div>
</section>

<!-- ════════════════════════════════════════════════════
     FEATURES
════════════════════════════════════════════════════ -->
<section id="fitur">
  <div class="section-label">5 Fitur Unggulan</div>
  <h2 class="section-title">Apa Saja yang Bisa Dilakukan?</h2>
  <p class="section-sub">Setiap fitur dirancang untuk mengatasi tantangan nyata dalam belajar sains energi.</p>
  <div class="divider"></div>

  <div class="features-grid" id="featuresGrid">

    <!-- Feature 1 -->
    <div class="feature-card" onclick="toggleFeat(this)">
      <div class="feat-header">
        <div class="feat-icon" style="background:linear-gradient(135deg,rgba(0,229,195,.1),rgba(14,165,233,.1));border-color:rgba(0,229,195,.2);">🤖</div>
        <div class="feat-meta">
          <div class="feat-num">Fitur 01</div>
          <div class="feat-title">AI-Concept Buddy (Interpretasi Mandiri)</div>
        </div>
        <div class="feat-chevron">▼</div>
      </div>
      <div class="feat-body">
        <div class="feat-body-inner">
          <p class="feat-desc">Dirancang khusus untuk mengatasi tingginya tingkat kesulitan siswa dalam menginterpretasikan konsep yang mencapai 45%. AI-Buddy mendampingi siswa agar bisa membangun pemahaman sendiri.</p>
          <div class="feat-points">
            <div class="feat-point">
              <div class="feat-point-dot" style="background:var(--teal)"></div>
              <p><strong>Mekanisme AR:</strong> Siswa mengarahkan kamera ke objek AR (contoh: kincir angin), lalu muncul instruksi untuk menjelaskan cara kerjanya dengan suara mereka sendiri.</p>
            </div>
            <div class="feat-point">
              <div class="feat-point-dot" style="background:var(--blue)"></div>
              <p><strong>Output AI:</strong> AI menganalisis penjelasan siswa dan membantu merumuskan definisi sendiri tanpa menghafal teks buku — membangun ingatan jangka panjang.</p>
            </div>
          </div>
          <span class="feat-tag" style="background:rgba(0,229,195,.1);color:var(--teal);">🧠 Kognisi Mandiri</span>
        </div>
      </div>
    </div>

    <!-- Feature 2 -->
    <div class="feature-card" onclick="toggleFeat(this)">
      <div class="feat-header">
        <div class="feat-icon" style="background:linear-gradient(135deg,rgba(251,191,36,.1),rgba(239,68,68,.1));border-color:rgba(251,191,36,.2);">⚡</div>
        <div class="feat-meta">
          <div class="feat-num">Fitur 02</div>
          <div class="feat-title">Virtual Laboratory & Smart Calculator (P = V × I)</div>
        </div>
        <div class="feat-chevron">▼</div>
      </div>
      <div class="feat-body">
        <div class="feat-body-inner">
          <p class="feat-desc">Laboratorium virtual untuk pengalaman langsung dalam keterampilan proses sains. Siswa melakukan eksperimen nyata secara digital.</p>
          <div class="feat-points">
            <div class="feat-point">
              <div class="feat-point-dot" style="background:var(--yellow)"></div>
              <p><strong>Kalkulator Daya Interaktif:</strong> Masukkan atau geser nilai Tegangan (V) dan Arus (I) pada alat elektronik virtual untuk menghitung daya listrik P = V × I secara otomatis.</p>
            </div>
            <div class="feat-point">
              <div class="feat-point-dot" style="background:var(--red)"></div>
              <p><strong>Simulasi MCB Anjlok:</strong> Jika total daya melebihi kapasitas rumah virtual, AR menampilkan visualisasi MCB Anjlok — listrik padam!</p>
            </div>
            <div class="feat-point">
              <div class="feat-point-dot" style="background:var(--green)"></div>
              <p><strong>Digital Citizenship:</strong> Mengajarkan etika penggunaan teknologi yang bertanggung jawab dan hemat energi.</p>
            </div>
          </div>
          <span class="feat-tag" style="background:rgba(251,191,36,.1);color:var(--yellow);">🔬 Science Process Skills</span>
        </div>
      </div>
    </div>

    <!-- Feature 3 -->
    <div class="feature-card" onclick="toggleFeat(this)">
      <div class="feat-header">
        <div class="feat-icon" style="background:linear-gradient(135deg,rgba(168,85,247,.1),rgba(14,165,233,.1));border-color:rgba(168,85,247,.2);">🎮</div>
        <div class="feat-meta">
          <div class="feat-num">Fitur 03</div>
          <div class="feat-title">Gamifikasi: "The Energy Guardian Quest"</div>
        </div>
        <div class="feat-chevron">▼</div>
      </div>
      <div class="feat-body">
        <div class="feat-body-inner">
          <p class="feat-desc">Game berbasis AR yang meningkatkan minat dan motivasi belajar siswa yang seringkali rendah dalam pelajaran IPA. Siswa menjadi pahlawan energi!</p>
          <div class="feat-points">
            <div class="feat-point">
              <div class="feat-point-dot" style="background:var(--purple)"></div>
              <p><strong>Konsep Game:</strong> Siswa berperan sebagai "Penjaga Energi" yang mengatur penggunaan listrik di sebuah kota virtual menggunakan teknologi AR.</p>
            </div>
            <div class="feat-point">
              <div class="feat-point-dot" style="background:var(--blue)"></div>
              <p><strong>Tantangan Strategis:</strong> Susun strategi agar semua fasilitas publik tetap menyala tanpa membuang energi. Setiap keputusan hemat daya memberikan poin!</p>
            </div>
            <div class="feat-point">
              <div class="feat-point-dot" style="background:var(--yellow)"></div>
              <p><strong>Poin Pelajar Pancasila:</strong> Karakter profil pelajar Pancasila didapat dari setiap keputusan bijak dalam mengelola energi.</p>
            </div>
          </div>
          <span class="feat-tag" style="background:rgba(168,85,247,.1);color:var(--purple);">🕹️ Gamification Learning</span>
        </div>
      </div>
    </div>

    <!-- Feature 4 -->
    <div class="feature-card" onclick="toggleFeat(this)">
      <div class="feat-header">
        <div class="feat-icon" style="background:linear-gradient(135deg,rgba(34,197,94,.1),rgba(0,229,195,.1));border-color:rgba(34,197,94,.2);">🌍</div>
        <div class="feat-meta">
          <div class="feat-num">Fitur 04</div>
          <div class="feat-title">Alternative Energy Exploration</div>
        </div>
        <div class="feat-chevron">▼</div>
      </div>
      <div class="feat-body">
        <div class="feat-body-inner">
          <p class="feat-desc">Fasilitasi penguasaan materi energi alternatif yang selama ini dirasa padat dan sulit oleh siswa SD melalui eksplorasi virtual yang menyenangkan.</p>
          <div class="feat-points">
            <div class="feat-point">
              <div class="feat-point-dot" style="background:var(--green)"></div>
              <p><strong>Eksperimen Virtual:</strong> Rancang dan tempatkan panel surya atau turbin air virtual di lingkungan sekolah melalui layar perangkat secara AR.</p>
            </div>
            <div class="feat-point">
              <div class="feat-point-dot" style="background:var(--teal)"></div>
              <p><strong>Dampak Visual:</strong> Lihat perbandingan langsung bagaimana energi alternatif menggantikan energi fosil secara lebih bersih dan efisien melalui simulasi data visual.</p>
            </div>
          </div>
          <span class="feat-tag" style="background:rgba(34,197,94,.1);color:var(--green);">🌱 Green Future</span>
        </div>
      </div>
    </div>

    <!-- Feature 5 -->
    <div class="feature-card" onclick="toggleFeat(this)">
      <div class="feat-header">
        <div class="feat-icon" style="background:linear-gradient(135deg,rgba(14,165,233,.1),rgba(168,85,247,.1));border-color:rgba(14,165,233,.2);">📖</div>
        <div class="feat-meta">
          <div class="feat-num">Fitur 05</div>
          <div class="feat-title">Kamusku (Log Inovasi Pribadi)</div>
        </div>
        <div class="feat-chevron">▼</div>
      </div>
      <div class="feat-body">
        <div class="feat-body-inner">
          <p class="feat-desc">Basis data pribadi siswa untuk mencatat hasil temuan dan definisi konsep yang mereka rumuskan sendiri. Bukan menyalin, tapi benar-benar memahami!</p>
          <div class="feat-points">
            <div class="feat-point">
              <div class="feat-point-dot" style="background:var(--blue)"></div>
              <p><strong>Penyimpanan Gagasan:</strong> Setiap kali siswa berhasil mendefinisikan konsep melalui AI-Concept Buddy, definisi tersebut tersimpan otomatis di "Kamusku".</p>
            </div>
            <div class="feat-point">
              <div class="feat-point-dot" style="background:var(--purple)"></div>
              <p><strong>Refleksi Jangka Panjang:</strong> Mencegah siswa sekadar menyalin jawaban dari buku dan mendorong inovasi dalam menghemat sumber energi.</p>
            </div>
          </div>
          <span class="feat-tag" style="background:rgba(14,165,233,.1);color:var(--blue);">📝 Personal Knowledge Base</span>
        </div>
      </div>
    </div>

  </div>
</section>

<!-- ════════════════════════════════════════════════════
     VIRTUAL LAB
════════════════════════════════════════════════════ -->
<section class="lab-bg reveal" id="lab">
  <div class="section-label">Virtual Laboratory</div>
  <h2 class="section-title">Kalkulator Daya Listrik</h2>
  <p class="section-sub">Geser nilai Tegangan dan Arus, lalu lihat daya listrik terhitung otomatis. Nyalakan alat elektronik dan pantau MCB!</p>
  <div class="divider"></div>

  <div class="lab-panel">
    <div class="lab-formula">
      <div class="formula-box">P = V × I</div>
    </div>

    <div class="slider-group">
      <div class="slider-row">
        <div class="slider-label">
          <span>⚡ Tegangan (V)</span>
          <span class="slider-val" id="vVal">220 V</span>
        </div>
        <input type="range" min="100" max="440" value="220" id="sliderV" oninput="updateLab()" />
      </div>
      <div class="slider-row">
        <div class="slider-label">
          <span>🔌 Arus (I)</span>
          <span class="slider-val" id="iVal">2.0 A</span>
        </div>
        <input type="range" min="0" max="20" step=".1" value="2" id="sliderI" oninput="updateLab()" />
      </div>
    </div>

    <div class="power-display">
      <div class="power-label">Daya Listrik (P)</div>
      <div class="power-num" id="pDisplay">440 <span>Watt</span></div>
      <div class="mcb-status" id="mcbStatus">
        <div class="mcb-dot mcb-dot-ok" id="mcbDot"></div>
        <span id="mcbText" class="mcb-ok">MCB Normal — Aman ✓</span>
      </div>
    </div>

    <div class="appliances" style="margin-top:22px;">
      <div class="app-label">Alat Elektronik Virtual (Kapasitas: 2200 W)</div>
      <div class="app-grid" id="appGrid">
        <!-- Injected by JS -->
      </div>
      <div class="power-display" style="margin-top:14px;">
        <div class="power-label">Total Beban Elektronik</div>
        <div class="power-num" id="totalPower">0 <span>Watt</span></div>
        <div class="mcb-status" id="appMcbStatus">
          <div class="mcb-dot mcb-dot-ok" id="appMcbDot"></div>
          <span id="appMcbText" class="mcb-ok">Listrik Menyala 🏠</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ════════════════════════════════════════════════════
     GAME
════════════════════════════════════════════════════ -->
<section class="game-bg reveal" id="game">
  <div class="section-label">Gamifikasi Belajar</div>
  <h2 class="section-title">The Energy Guardian Quest</h2>
  <p class="section-sub">Game AR seru yang menjadikan belajar energi sebagai petualangan yang tidak terlupakan.</p>
  <div class="divider"></div>

  <div class="game-banner">
    <div class="game-banner-title">⚡ Jadilah Penjaga Energi! ⚡</div>
    <div class="game-banner-sub">Kelola kota virtual dengan bijak. Hemat energi, selamatkan lingkungan, dan kumpulkan poin Profil Pelajar Pancasila!</div>

    <div class="game-features">
      <div class="game-feat">
        <div class="game-feat-icon">🏙️</div>
        <div class="game-feat-body">
          <h4>Kota Virtual AR</h4>
          <p>Atur penggunaan listrik di berbagai fasilitas kota: sekolah, rumah sakit, pasar, dan taman kota menggunakan teknologi AR.</p>
        </div>
      </div>
      <div class="game-feat">
        <div class="game-feat-icon">🎯</div>
        <div class="game-feat-body">
          <h4>Tantangan Strategi Energi</h4>
          <p>Pastikan semua fasilitas publik tetap menyala tanpa pemborosan. Setiap keputusan tepat meningkatkan skor kotamu!</p>
        </div>
      </div>
      <div class="game-feat">
        <div class="game-feat-icon">🏆</div>
        <div class="game-feat-body">
          <h4>Level & Pencapaian</h4>
          <p>Naik level dari "Pelajar Hemat" ke "Penjaga Energi Sejati". Setiap level membuka tantangan lingkungan baru.</p>
        </div>
      </div>
    </div>

    <div class="pelajar-badge">
      ⭐ Kumpulkan Poin Profil Pelajar Pancasila
    </div>
  </div>
</section>

<!-- ════════════════════════════════════════════════════
     ENERGY EXPLORATION
════════════════════════════════════════════════════ -->
<section id="eksplorasi">
  <div class="section-label">Alternative Energy Exploration</div>
  <h2 class="section-title">Jenis Energi Terbarukan</h2>
  <p class="section-sub">Eksplor berbagai sumber energi terbarukan secara virtual dan bandingkan dampaknya terhadap lingkungan.</p>
  <div class="divider"></div>

  <div class="energy-cards reveal">

    <div class="energy-card">
      <div class="energy-card-top">
        <div class="energy-icon" style="background:linear-gradient(135deg,rgba(251,191,36,.15),rgba(239,68,68,.15));border:1px solid rgba(251,191,36,.2);">☀️</div>
        <div>
          <div class="energy-name">Energi Surya (Solar)</div>
          <div class="energy-desc">Memanfaatkan sinar matahari melalui panel fotovoltaik untuk menghasilkan listrik bersih tanpa emisi karbon.</div>
        </div>
      </div>
      <div class="energy-bar-wrap">
        <div class="energy-bar-label"><span>Tingkat Kebersihan</span><span style="color:var(--yellow)">92%</span></div>
        <div class="energy-bar-track"><div class="energy-bar-fill" style="width:92%;background:linear-gradient(90deg,var(--yellow),#f97316);"></div></div>
      </div>
      <div class="energy-compare">
        <div class="energy-cmp-item">
          <div class="energy-cmp-val" style="color:var(--yellow)">0 g</div>
          <div class="energy-cmp-label">CO₂ per kWh</div>
        </div>
        <div class="energy-cmp-item">
          <div class="energy-cmp-val" style="color:var(--green)">25 th</div>
          <div class="energy-cmp-label">Umur Panel</div>
        </div>
      </div>
    </div>

    <div class="energy-card">
      <div class="energy-card-top">
        <div class="energy-icon" style="background:linear-gradient(135deg,rgba(0,229,195,.15),rgba(14,165,233,.15));border:1px solid rgba(0,229,195,.2);">💨</div>
        <div>
          <div class="energy-name">Energi Angin (Wind)</div>
          <div class="energy-desc">Turbin angin mengubah energi kinetik angin menjadi energi listrik. Cocok di daerah pesisir dan dataran tinggi.</div>
        </div>
      </div>
      <div class="energy-bar-wrap">
        <div class="energy-bar-label"><span>Tingkat Kebersihan</span><span style="color:var(--teal)">88%</span></div>
        <div class="energy-bar-track"><div class="energy-bar-fill" style="width:88%;background:linear-gradient(90deg,var(--teal),var(--blue));"></div></div>
      </div>
      <div class="energy-compare">
        <div class="energy-cmp-item">
          <div class="energy-cmp-val" style="color:var(--teal)">11 g</div>
          <div class="energy-cmp-label">CO₂ per kWh</div>
        </div>
        <div class="energy-cmp-item">
          <div class="energy-cmp-val" style="color:var(--green)">20 th</div>
          <div class="energy-cmp-label">Umur Turbin</div>
        </div>
      </div>
    </div>

    <div class="energy-card">
      <div class="energy-card-top">
        <div class="energy-icon" style="background:linear-gradient(135deg,rgba(14,165,233,.15),rgba(0,229,195,.1));border:1px solid rgba(14,165,233,.2);">💧</div>
        <div>
          <div class="energy-name">Energi Air (Hydro)</div>
          <div class="energy-desc">Memanfaatkan aliran air sungai atau waduk untuk menggerakkan turbin dan menghasilkan listrik yang stabil.</div>
        </div>
      </div>
      <div class="energy-bar-wrap">
        <div class="energy-bar-label"><span>Tingkat Kebersihan</span><span style="color:var(--blue)">85%</span></div>
        <div class="energy-bar-track"><div class="energy-bar-fill" style="width:85%;background:linear-gradient(90deg,var(--blue),var(--teal));"></div></div>
      </div>
      <div class="energy-compare">
        <div class="energy-cmp-item">
          <div class="energy-cmp-val" style="color:var(--blue)">4 g</div>
          <div class="energy-cmp-label">CO₂ per kWh</div>
        </div>
        <div class="energy-cmp-item">
          <div class="energy-cmp-val" style="color:var(--green)">50 th</div>
          <div class="energy-cmp-label">Umur PLTA</div>
        </div>
      </div>
    </div>

    <!-- Fossil comparison -->
    <div class="energy-card" style="border-color:rgba(239,68,68,.2);">
      <div class="energy-card-top">
        <div class="energy-icon" style="background:linear-gradient(135deg,rgba(239,68,68,.15),rgba(251,191,36,.1));border:1px solid rgba(239,68,68,.2);">🏭</div>
        <div>
          <div class="energy-name">Energi Fosil (Perbandingan)</div>
          <div class="energy-desc">Batu bara dan minyak bumi menghasilkan emisi CO₂ tinggi yang menyebabkan perubahan iklim dan pencemaran udara.</div>
        </div>
      </div>
      <div class="energy-bar-wrap">
        <div class="energy-bar-label"><span>Tingkat Kebersihan</span><span style="color:var(--red)">12%</span></div>
        <div class="energy-bar-track"><div class="energy-bar-fill" style="width:12%;background:var(--red);"></div></div>
      </div>
      <div class="energy-compare">
        <div class="energy-cmp-item">
          <div class="energy-cmp-val" style="color:var(--red)">820 g</div>
          <div class="energy-cmp-label">CO₂ per kWh</div>
        </div>
        <div class="energy-cmp-item">
          <div class="energy-cmp-val" style="color:var(--red)">Terbatas</div>
          <div class="energy-cmp-label">Ketersediaan</div>
        </div>
      </div>
    </div>

  </div>
</section>

<!-- ════════════════════════════════════════════════════
     KAMUSKU
════════════════════════════════════════════════════ -->
<section style="background:var(--bg2);border-top:1px solid var(--border);border-bottom:1px solid var(--border);" class="reveal" id="kamus">
  <div class="section-label">Log Inovasi Pribadi</div>
  <h2 class="section-title">Kamusku</h2>
  <p class="section-sub">Definisi konsep energi yang kamu rumuskan sendiri bersama AI-Buddy. Bukan hafalan — tapi pemahaman sejati!</p>
  <div class="divider"></div>

  <div class="kamus-panel">
    <div class="kamus-head">
      <div class="kamus-head-icon">📖</div>
      <div>
        <h3>Kamus Energiku</h3>
        <p>3 definisi tersimpan · Terakhir diperbarui hari ini</p>
      </div>
    </div>
    <div class="kamus-entries" id="kamusEntries">
      <div class="kamus-entry">
        <div class="kamus-entry-term">
          Energi Surya
          <span class="kamus-badge">AI-Buddy ✓</span>
        </div>
        <div class="kamus-entry-def">Energi yang berasal dari cahaya matahari yang ditangkap panel surya dan diubah menjadi listrik yang bisa kita pakai sehari-hari. Seperti tanaman yang butuh sinar matahari untuk hidup, rumah kita juga bisa "makan" sinar matahari!</div>
        <div class="kamus-entry-meta">📅 Ditambahkan 17 Mei 2026</div>
      </div>
      <div class="kamus-entry">
        <div class="kamus-entry-term">
          Turbin Angin
          <span class="kamus-badge">AI-Buddy ✓</span>
        </div>
        <div class="kamus-entry-def">Kincir besar yang berputar karena dorongan angin, lalu putarannya menghasilkan listrik. Seperti kipas angin tapi kebalik — bukan listrik yang menggerakkan baling-baling, tapi baling-baling yang menghasilkan listrik!</div>
        <div class="kamus-entry-meta">📅 Ditambahkan 17 Mei 2026</div>
      </div>
      <div class="kamus-entry">
        <div class="kamus-entry-term">
          Daya Listrik (P)
          <span class="kamus-badge">Virtual Lab ✓</span>
        </div>
        <div class="kamus-entry-def">Besarnya energi yang dipakai alat elektronik setiap detiknya. Dihitung dengan cara mengalikan tegangan (V) dengan arus (I). Makin besar dayanya, makin boros listriknya!</div>
        <div class="kamus-entry-meta">📅 Ditambahkan 17 Mei 2026</div>
      </div>
    </div>
    <div class="kamus-add">
      <input class="kamus-input" id="kamusInput" type="text" placeholder="Tambah konsep baru..." />
      <button class="kamus-btn" onclick="addKamus()">+ Tambah</button>
    </div>
  </div>
</section>

<!-- ════════════════════════════════════════════════════
     AR SCAN DEMO
════════════════════════════════════════════════════ -->
<section class="reveal" id="ar-demo">
  <div class="section-label">Demo Pengalaman AR</div>
  <h2 class="section-title">Objek AR Energi Terbarukan</h2>
  <p class="section-sub">Ketuk objek di bawah untuk melihat demo tampilan AR. Di perangkat nyata, objek 3D akan muncul di lingkungan sekitarmu!</p>
  <div class="divider"></div>

  <div style="display:flex;flex-direction:column;gap:14px;margin-top:8px;">
    <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:10px;">
      <div onclick="openModal('solar')" style="background:var(--card-bg);border:1px solid var(--border);border-radius:16px;padding:18px 10px;text-align:center;cursor:pointer;transition:border-color .2s;" onmouseenter="this.style.borderColor='rgba(0,229,195,.4)'" onmouseleave="this.style.borderColor='var(--border)'">
        <div style="font-size:2.2rem;margin-bottom:8px;">☀️</div>
        <div style="font-size:.72rem;font-weight:700;color:var(--teal);">Panel Surya</div>
        <div style="font-size:.65rem;color:var(--muted);margin-top:2px;">Tap AR</div>
      </div>
      <div onclick="openModal('wind')" style="background:var(--card-bg);border:1px solid var(--border);border-radius:16px;padding:18px 10px;text-align:center;cursor:pointer;transition:border-color .2s;" onmouseenter="this.style.borderColor='rgba(0,229,195,.4)'" onmouseleave="this.style.borderColor='var(--border)'">
        <div style="font-size:2.2rem;margin-bottom:8px;">💨</div>
        <div style="font-size:.72rem;font-weight:700;color:var(--teal);">Turbin Angin</div>
        <div style="font-size:.65rem;color:var(--muted);margin-top:2px;">Tap AR</div>
      </div>
      <div onclick="openModal('hydro')" style="background:var(--card-bg);border:1px solid var(--border);border-radius:16px;padding:18px 10px;text-align:center;cursor:pointer;transition:border-color .2s;" onmouseenter="this.style.borderColor='rgba(0,229,195,.4)'" onmouseleave="this.style.borderColor='var(--border)'">
        <div style="font-size:2.2rem;margin-bottom:8px;">💧</div>
        <div style="font-size:.72rem;font-weight:700;color:var(--teal);">Turbin Air</div>
        <div style="font-size:.65rem;color:var(--muted);margin-top:2px;">Tap AR</div>
      </div>
    </div>
  </div>
</section>

<!-- ════════════════════════════════════════════════════
     TESTIMONIALS
════════════════════════════════════════════════════ -->
<section style="background:var(--bg2);border-top:1px solid var(--border);" class="reveal">
  <div class="section-label">Ulasan Pengguna</div>
  <h2 class="section-title">Apa Kata Mereka?</h2>
  <p class="section-sub">Pengalaman nyata dari siswa dan guru yang telah menggunakan CORE-AR.</p>
  <div class="divider"></div>

  <div class="testi-scroll">
    <div class="testi-card">
      <div class="testi-stars">★★★★★</div>
      <p class="testi-text">"Dulu aku bingung sama panel surya, sekarang aku bisa jelasin ke teman-temanku! AI-Buddy seru banget."</p>
      <div class="testi-author">Aisyah R.</div>
      <div class="testi-loc">Siswa Kelas 5 SD, Solo</div>
    </div>
    <div class="testi-card">
      <div class="testi-stars">★★★★★</div>
      <p class="testi-text">"Laboratorium virtualnya bikin anak-anak paham rumus P = V × I tanpa harus hafal. Mereka langsung praktik!"</p>
      <div class="testi-author">Bu Sari W., S.Pd.</div>
      <div class="testi-loc">Guru IPA SD Negeri 3 Semarang</div>
    </div>
    <div class="testi-card">
      <div class="testi-stars">★★★★★</div>
      <p class="testi-text">"Energy Guardian Quest bikin aku semangat belajar IPA. Aku udah level 5 Penjaga Energi!"</p>
      <div class="testi-author">Farhan D.</div>
      <div class="testi-loc">Siswa Kelas 6 SD, Yogyakarta</div>
    </div>
    <div class="testi-card">
      <div class="testi-stars">★★★★☆</div>
      <p class="testi-text">"Kamusku membantu siswa saya menulis definisi sendiri. Kualitas pemahaman meningkat signifikan."</p>
      <div class="testi-author">Pak Budi H., M.Pd.</div>
      <div class="testi-loc">Kepala Sekolah SD Muhammadiyah, Klaten</div>
    </div>
  </div>
</section>

<!-- ════════════════════════════════════════════════════
     FOOTER
════════════════════════════════════════════════════ -->
<footer>
  <div class="footer-logo">CORE-AR</div>
  <p class="footer-tagline">Peningkatan Pemahaman Energi Terbarukan Berbasis AR & AI-Buddy</p>
  <div class="footer-divider"></div>
  <div class="footer-logos">
    <div class="footer-logo-item">🏫 Pendidikan Dasar</div>
    <div class="footer-logo-item">🤖 AI-Powered</div>
    <div class="footer-logo-item">🌱 Energi Hijau</div>
  </div>
  <div class="footer-links">
    <a href="#beranda">Beranda</a>
    <a href="#fitur">Fitur</a>
    <a href="#lab">Virtual Lab</a>
    <a href="#game">Game</a>
    <a href="#eksplorasi">Eksplorasi</a>
    <a href="#kamus">Kamusku</a>
  </div>
  <p class="footer-copy">© 2026 CORE-AR · Dibuat dengan ❤️ untuk Pendidikan Indonesia · Solo, Jawa Tengah</p>
</footer>

<!-- FAB -->
<button class="fab" onclick="scrollToFeatures()" aria-label="Mulai Eksplorasi">
  <div class="fab-pulse"></div>
  🔋
</button>

<!-- ════════════════════════════════════════════════════
     AR MODAL
════════════════════════════════════════════════════ -->
<div class="modal-overlay" id="modalOverlay" onclick="closeModalOutside(event)">
  <div class="modal" id="modal" role="dialog" aria-modal="true">
    <div class="modal-handle"></div>
    <button class="modal-close" onclick="closeModal()">✕</button>

    <div class="mv-container" id="mvContainer"></div>
    <p class="mv-hint">Geser untuk memutar · Ketuk ikon AR untuk mode Augmented Reality</p>

    <div class="modal-content">
      <div class="modal-label" id="mLabel"></div>
      <h2 class="modal-name" id="mName"></h2>
      <p class="modal-desc" id="mDesc"></p>

      <div class="modal-ar-box">
        <div class="modal-ar-title">📱 Lihat di Dunia Nyatamu</div>
        <div class="modal-ar-sub">Tekan tombol di bawah, arahkan kamera ke permukaan datar, lalu tap untuk menempatkan objek 3D energi terbarukan.</div>
        <button class="btn-ar" onclick="launchAR()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" width="20" height="20">
            <path d="M12 2L2 7l10 5 10-5-10-5z"/><path d="M2 17l10 5 10-5"/><path d="M2 12l10 5 10-5"/>
          </svg>
          Aktifkan Augmented Reality
        </button>
        <div class="ar-fallback" id="arFallback">
          <p><strong>AR tidak tersedia di browser ini.</strong><br>Untuk pengalaman AR terbaik, gunakan Chrome (Android) atau Safari (iPhone/iPad). Pastikan izinkan akses kamera.</p>
        </div>
      </div>

      <!-- AI Buddy mini -->
      <div style="background:rgba(0,229,195,.06);border:1px solid rgba(0,229,195,.18);border-radius:14px;padding:16px;margin-bottom:14px;">
        <div style="font-weight:700;font-size:.88rem;color:#fff;margin-bottom:8px;">🤖 AI-Buddy Berkata:</div>
        <p style="font-size:.83rem;color:var(--muted);line-height:1.65;" id="aiBuddyText"></p>
        <button onclick="recordExplanation()" style="margin-top:12px;width:100%;background:rgba(0,229,195,.12);border:1px solid rgba(0,229,195,.25);color:var(--teal);padding:10px;border-radius:10px;font-size:.82rem;font-weight:700;cursor:pointer;">
          🎤 Jelaskan dengan Suaramu!
        </button>
      </div>
    </div>
  </div>
</div>

<!-- ════════════════════════════════════════════════════
     JAVASCRIPT
════════════════════════════════════════════════════ -->
<script>
// ─── AR Objects Data ─────────────────────────────────
const arObjects = {
  solar: {
    label: 'Energi Surya · AR Demo',
    name: 'Panel Surya Fotovoltaik',
    emoji: '☀️',
    bg: 'linear-gradient(135deg,#1a1200,#2a1e00)',
    desc: 'Panel surya menggunakan sel fotovoltaik untuk mengubah cahaya matahari langsung menjadi energi listrik. Tanpa emisi, tanpa suara, dan sumbernya tidak pernah habis!',
    model_glb: 'models/solar-panel.glb',
    model_usdz: 'models/solar-panel.usdz',
    buddy: 'Coba ceritakan: apa yang kamu lihat dari panel surya ini? Bagaimana kira-kira panel ini bisa menghasilkan listrik? Jelaskan dengan kata-katamu sendiri! 💡'
  },
  wind: {
    label: 'Energi Angin · AR Demo',
    name: 'Turbin Angin (Kincir Angin)',
    emoji: '💨',
    bg: 'linear-gradient(135deg,#001018,#001824)',
    desc: 'Turbin angin mengubah energi gerak angin menjadi energi listrik melalui putaran baling-baling yang menggerakkan generator. Makin kencang anginnya, makin besar listrik yang dihasilkan!',
    model_glb: 'models/wind-turbine.glb',
    model_usdz: 'models/wind-turbine.usdz',
    buddy: 'Perhatikan baling-baling kincir ini! Coba jelaskan: kenapa kincir angin perlu diletakkan di tempat yang berangin? Apa yang terjadi kalau anginnya berhenti? 🌬️'
  },
  hydro: {
    label: 'Energi Air · AR Demo',
    name: 'Turbin Air (PLTA)',
    emoji: '💧',
    bg: 'linear-gradient(135deg,#000d18,#001220)',
    desc: 'Turbin air memanfaatkan aliran atau jatuhnya air untuk memutar generator dan menghasilkan listrik. PLTA (Pembangkit Listrik Tenaga Air) adalah salah satu sumber listrik terbesar di Indonesia!',
    model_glb: 'models/water-turbine.glb',
    model_usdz: 'models/water-turbine.usdz',
    buddy: 'Bayangkan air sungai yang deras mengalir dan memutar kincir ini! Menurutmu, apa persamaan dan perbedaan antara turbin air dan turbin angin? 💧'
  }
};

let activeObj = null;

// ─── Appliances Data ─────────────────────────────────
const appliances = [
  { id:'tv', name:'TV LED 32"', emoji:'📺', watt:60, on:false },
  { id:'ac', name:'AC 1 PK', emoji:'❄️', watt:900, on:false },
  { id:'kulkas', name:'Kulkas 2 Pintu', emoji:'🧊', watt:150, on:true },
  { id:'lampu', name:'Lampu (5 bh)', emoji:'💡', watt:50, on:true },
  { id:'komputer', name:'Komputer + Monitor', emoji:'🖥️', watt:250, on:false },
  { id:'mesin', name:'Mesin Cuci', emoji:'🫧', watt:500, on:false },
];

// ─── Virtual Lab ─────────────────────────────────────
function updateLab() {
  const v = parseFloat(document.getElementById('sliderV').value);
  const i = parseFloat(document.getElementById('sliderI').value);
  const p = (v * i).toFixed(0);

  document.getElementById('vVal').textContent = v + ' V';
  document.getElementById('iVal').textContent = i.toFixed(1) + ' A';
  document.getElementById('pDisplay').innerHTML = p + ' <span>Watt</span>';

  const dot = document.getElementById('mcbDot');
  const txt = document.getElementById('mcbText');
  if (p > 2200) {
    dot.className = 'mcb-dot mcb-dot-trip';
    txt.className = 'mcb-trip';
    txt.textContent = 'MCB ANJLOK — Listrik Padam ⚠️';
  } else if (p > 1600) {
    dot.className = 'mcb-dot mcb-dot-warn';
    txt.className = 'mcb-warn';
    txt.textContent = 'Mendekati Batas — Hati-hati ⚡';
  } else {
    dot.className = 'mcb-dot mcb-dot-ok';
    txt.className = 'mcb-ok';
    txt.textContent = 'MCB Normal — Aman ✓';
  }
}

function renderAppliances() {
  const grid = document.getElementById('appGrid');
  grid.innerHTML = '';
  appliances.forEach(a => {
    const el = document.createElement('div');
    el.className = 'app-item' + (a.on ? ' on' : '');
    el.innerHTML = `
      <div class="app-icon">${a.emoji}</div>
      <div class="app-info">
        <div class="app-name">${a.name}</div>
        <div class="app-watt">${a.watt} W</div>
      </div>
      <div class="app-toggle"></div>
    `;
    el.addEventListener('click', () => {
      a.on = !a.on;
      el.classList.toggle('on');
      updateTotalPower();
    });
    grid.appendChild(el);
  });
  updateTotalPower();
}

function updateTotalPower() {
  const total = appliances.filter(a=>a.on).reduce((s,a)=>s+a.watt,0);
  document.getElementById('totalPower').innerHTML = total + ' <span>Watt</span>';
  const dot2 = document.getElementById('appMcbDot');
  const txt2 = document.getElementById('appMcbText');
  const CAP = 2200;
  if (total > CAP) {
    dot2.className = 'mcb-dot mcb-dot-trip';
    txt2.className = 'mcb-trip';
    txt2.textContent = 'MCB ANJLOK — Mati Listrik! 🔴';
  } else if (total > CAP * 0.8) {
    dot2.className = 'mcb-dot mcb-dot-warn';
    txt2.className = 'mcb-warn';
    txt2.textContent = 'Beban Berat — Kurangi Alat 🟡';
  } else {
    dot2.className = 'mcb-dot mcb-dot-ok';
    txt2.className = 'mcb-ok';
    txt2.textContent = 'Listrik Menyala 🏠✓';
  }
}

// ─── Feature Toggle ───────────────────────────────────
function toggleFeat(card) {
  const isOpen = card.classList.contains('open');
  document.querySelectorAll('.feature-card.open').forEach(c => c.classList.remove('open'));
  if (!isOpen) card.classList.add('open');
}

// ─── AR Modal ────────────────────────────────────────
function openModal(id) {
  const obj = arObjects[id];
  if (!obj) return;
  activeObj = obj;

  document.getElementById('mLabel').textContent = obj.label;
  document.getElementById('mName').textContent = obj.name;
  document.getElementById('mDesc').textContent = obj.desc;
  document.getElementById('aiBuddyText').textContent = obj.buddy;

  const mvc = document.getElementById('mvContainer');
  mvc.innerHTML = `
    <model-viewer
      src="${obj.model_glb}"
      ios-src="${obj.model_usdz}"
      alt="3D model ${obj.name}"
      ar ar-modes="scene-viewer webxr quick-look"
      ar-scale="auto"
      camera-controls auto-rotate
      shadow-intensity="1" exposure="0.9"
      style="width:100%;height:280px;background:${obj.bg};">
      <div slot="poster" style="width:100%;height:280px;display:flex;align-items:center;justify-content:center;background:${obj.bg};font-size:6rem;">${obj.emoji}</div>
    </model-viewer>
  `;

  document.getElementById('arFallback').style.display = 'none';
  document.getElementById('modalOverlay').classList.add('open');
  document.body.style.overflow = 'hidden';
}

function closeModal() {
  document.getElementById('modalOverlay').classList.remove('open');
  document.body.style.overflow = '';
  setTimeout(() => { document.getElementById('mvContainer').innerHTML = ''; }, 300);
}

function closeModalOutside(e) {
  if (e.target === document.getElementById('modalOverlay')) closeModal();
}

function launchAR() {
  const mv = document.querySelector('#mvContainer model-viewer');
  if (mv && mv.canActivateAR) {
    mv.activateAR();
  } else {
    document.getElementById('arFallback').style.display = 'block';
  }
}

function recordExplanation() {
  if (!('webkitSpeechRecognition' in window || 'SpeechRecognition' in window)) {
    alert('🎤 Speech recognition tidak tersedia di browser ini. Coba gunakan Chrome!');
    return;
  }
  const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
  const recognition = new SR();
  recognition.lang = 'id-ID';
  recognition.start();
  document.querySelector('#modal .btn-ar ~ button, #modal button[onclick*="record"]') && null;
  const btn = document.querySelector('[onclick="recordExplanation()"]');
  if (btn) { btn.textContent = '⏺️ Sedang Merekam...'; btn.style.background='rgba(239,68,68,.15)'; btn.style.borderColor='rgba(239,68,68,.3)'; btn.style.color='var(--red)'; }
  recognition.onresult = (e) => {
    const transcript = e.results[0][0].transcript;
    if (btn) { btn.textContent = '🎤 Jelaskan dengan Suaramu!'; btn.style.cssText=''; }
    // Add to Kamusku
    addKamusEntry(activeObj ? activeObj.name : 'Konsep Baru', `"${transcript}" — Dideskripsikan melalui AI-Buddy AR.`, 'AI-Buddy 🎤');
    closeModal();
  };
  recognition.onerror = () => {
    if (btn) { btn.textContent = '🎤 Jelaskan dengan Suaramu!'; btn.style.cssText=''; }
    alert('Rekaman gagal. Pastikan izin mikrofon diberikan.');
  };
}

// ─── Kamusku ─────────────────────────────────────────
const kamusData = [];

function addKamus() {
  const val = document.getElementById('kamusInput').value.trim();
  if (!val) return;
  addKamusEntry(val, 'Definisi sedang dirumuskan bersama AI-Buddy...', 'Manual');
  document.getElementById('kamusInput').value = '';
}

function addKamusEntry(term, def, source) {
  const entries = document.getElementById('kamusEntries');
  const el = document.createElement('div');
  el.className = 'kamus-entry';
  const now = new Date().toLocaleDateString('id-ID', {day:'numeric',month:'long',year:'numeric'});
  el.innerHTML = `
    <div class="kamus-entry-term">
      ${term}
      <span class="kamus-badge">${source} ✓</span>
    </div>
    <div class="kamus-entry-def">${def}</div>
    <div class="kamus-entry-meta">📅 Ditambahkan ${now}</div>
  `;
  entries.insertBefore(el, entries.firstChild);
}

// ─── Scroll helpers ───────────────────────────────────
function scrollToFeatures() {
  document.getElementById('fitur').scrollIntoView({ behavior: 'smooth' });
}

// ─── Scroll Reveal ────────────────────────────────────
const revealObs = new IntersectionObserver((entries) => {
  entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
}, { threshold: 0.08 });
document.querySelectorAll('.reveal').forEach(el => revealObs.observe(el));

// ─── Keyboard ────────────────────────────────────────
document.addEventListener('keydown', e => { if (e.key === 'Escape') closeModal(); });

// ─── Init ────────────────────────────────────────────
updateLab();
renderAppliances();
</script>
</body>
</html>
