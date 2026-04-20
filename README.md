[ecotrack (5).html](https://github.com/user-attachments/files/26899523/ecotrack.5.html)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <!-- ✅ FIX #1: Viewport meta tag for mobile responsiveness -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>EcoTrack – Smart Plastic Waste Management</title>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet" />
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet" />

  <style>
    /* =============================================
       CSS VARIABLES & RESET
    ============================================= */
    :root {
      --green-dark:   #0a5c3a;
      --green-main:   #16a34a;
      --green-mid:    #22c55e;
      --green-light:  #bbf7d0;
      --green-pale:   #f0fdf4;
      --accent:       #84cc16;
      --amber:        #f59e0b;
      --red:          #ef4444;
      --blue:         #3b82f6;
      --text-dark:    #0f172a;
      --text-mid:     #334155;
      --text-muted:   #64748b;
      --bg:           #f8fafc;
      --card:         #ffffff;
      --border:       #e2e8f0;
      --shadow-sm:    0 1px 3px rgba(0,0,0,.08);
      --shadow-md:    0 4px 16px rgba(0,0,0,.10);
      --shadow-lg:    0 8px 32px rgba(0,0,0,.14);
      --radius:       14px;
      --radius-sm:    8px;
      --nav-h:        64px;
      --sidebar-w:    240px;
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    html, body {
      height: 100%;
      font-family: 'Plus Jakarta Sans', sans-serif;
      background: var(--bg);
      color: var(--text-dark);
      overflow-x: hidden;
    }

    a { text-decoration: none; color: inherit; }
    ul { list-style: none; }
    button { cursor: pointer; font-family: inherit; border: none; outline: none; }
    input, textarea, select { font-family: inherit; outline: none; border: none; }

    /* =============================================
       ✅ FIX #2: AUTH SCREEN
    ============================================= */
    #auth-screen {
      position: fixed;
      inset: 0;
      background: linear-gradient(135deg, #064e2c 0%, #0a5c3a 40%, #16a34a 100%);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 9999;
      padding: 20px;
    }

    .auth-box {
      background: rgba(255,255,255,.97);
      border-radius: 24px;
      padding: 44px 40px;
      width: 100%;
      max-width: 420px;
      box-shadow: 0 24px 64px rgba(0,0,0,.25);
    }

    .auth-logo {
      display: flex;
      align-items: center;
      gap: 10px;
      justify-content: center;
      margin-bottom: 8px;
    }
    .auth-logo i { font-size: 28px; color: var(--green-main); }
    .auth-logo span { font-size: 24px; font-weight: 800; color: var(--green-dark); }

    .auth-tagline {
      text-align: center;
      color: var(--text-muted);
      font-size: 13px;
      margin-bottom: 32px;
    }

    .auth-tabs {
      display: flex;
      border-radius: var(--radius-sm);
      background: var(--bg);
      padding: 4px;
      margin-bottom: 28px;
    }
    .auth-tab {
      flex: 1;
      padding: 10px;
      border-radius: 6px;
      font-size: 14px;
      font-weight: 600;
      background: transparent;
      color: var(--text-muted);
      transition: all .2s;
    }
    .auth-tab.active { background: var(--green-main); color: #fff; }

    .form-group { margin-bottom: 16px; }
    .form-group label { display: block; font-size: 13px; font-weight: 600; color: var(--text-mid); margin-bottom: 6px; }
    .form-group input {
      width: 100%;
      padding: 12px 14px;
      border: 1.5px solid var(--border);
      border-radius: var(--radius-sm);
      font-size: 14px;
      transition: border-color .2s;
    }
    .form-group input:focus { border-color: var(--green-main); }

    .form-error { font-size: 12px; color: var(--red); margin-top: 4px; display: none; }
    .form-error.show { display: block; }

    .btn-auth {
      width: 100%;
      padding: 14px;
      background: linear-gradient(135deg, var(--green-main), var(--green-dark));
      color: #fff;
      border-radius: var(--radius-sm);
      font-size: 15px;
      font-weight: 700;
      letter-spacing: .3px;
      transition: opacity .2s, transform .1s;
      margin-top: 8px;
    }
    .btn-auth:hover { opacity: .92; transform: translateY(-1px); }
    .btn-auth:active { transform: translateY(0); }

    /* =============================================
       ✅ FIX #3: APP SHELL
    ============================================= */
    #app {
      display: none;
      height: 100vh;
      overflow: hidden;
    }
    #app.visible { display: flex; flex-direction: column; }

    /* TOP NAV BAR */
    .topbar {
      height: var(--nav-h);
      background: var(--green-dark);
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 20px;
      position: sticky;
      top: 0;
      z-index: 100;
      flex-shrink: 0;
    }
    .topbar-logo { display: flex; align-items: center; gap: 8px; color: #fff; font-size: 18px; font-weight: 800; }
    .topbar-logo i { color: var(--green-mid); font-size: 22px; }
    .topbar-right { display: flex; align-items: center; gap: 12px; }
    .topbar-icon { color: rgba(255,255,255,.8); font-size: 18px; cursor: pointer; transition: color .2s; }
    .topbar-icon:hover { color: #fff; }
    .topbar-avatar {
      width: 34px; height: 34px;
      border-radius: 50%;
      background: var(--green-mid);
      display: flex; align-items: center; justify-content: center;
      color: var(--green-dark);
      font-weight: 700;
      font-size: 13px;
      cursor: pointer;
    }

    /* HAMBURGER (mobile) */
    .hamburger { display: none; flex-direction: column; gap: 5px; cursor: pointer; padding: 4px; }
    .hamburger span { display: block; width: 22px; height: 2px; background: #fff; border-radius: 2px; transition: all .3s; }

    /* BODY AREA: SIDEBAR + CONTENT */
    .app-body {
      display: flex;
      flex: 1;
      overflow: hidden;
    }

    /* SIDEBAR */
    .sidebar {
      width: var(--sidebar-w);
      background: #fff;
      border-right: 1px solid var(--border);
      display: flex;
      flex-direction: column;
      flex-shrink: 0;
      overflow-y: auto;
      transition: transform .3s;
    }

    .nav-menu { padding: 12px 10px; flex: 1; }
    .nav-item {
      display: flex;
      align-items: center;
      gap: 12px;
      padding: 11px 14px;
      border-radius: var(--radius-sm);
      font-size: 14px;
      font-weight: 500;
      color: var(--text-mid);
      cursor: pointer;
      transition: all .18s;
      margin-bottom: 2px;
      white-space: nowrap;
    }
    .nav-item i { width: 18px; text-align: center; font-size: 15px; color: var(--text-muted); flex-shrink: 0; }
    .nav-item:hover { background: var(--green-pale); color: var(--green-dark); }
    .nav-item:hover i { color: var(--green-main); }
    .nav-item.active { background: var(--green-pale); color: var(--green-dark); font-weight: 700; }
    .nav-item.active i { color: var(--green-main); }
    .nav-item.active::before {
      content: '';
      position: absolute;
      right: 0;
      width: 3px;
      height: 100%;
      background: var(--green-main);
      border-radius: 3px 0 0 3px;
    }
    .nav-item { position: relative; }

    .sidebar-footer {
      padding: 14px 12px;
      border-top: 1px solid var(--border);
    }
    .eco-tip {
      background: var(--green-pale);
      border-radius: var(--radius-sm);
      padding: 12px;
      font-size: 12px;
      color: var(--green-dark);
      line-height: 1.5;
    }
    .eco-tip strong { display: block; margin-bottom: 4px; color: var(--green-main); }

    /* MAIN CONTENT */
    .main-content {
      flex: 1;
      overflow-y: auto;
      overflow-x: hidden;
      background: var(--bg);
    }

    /* =============================================
       ✅ FIX #4: SECTION SYSTEM – no overlapping
    ============================================= */
    .section {
      display: none;         /* ALL hidden by default */
      padding: 28px 24px;
      min-height: 100%;
      animation: fadeIn .25s ease;
    }
    .section.active-section {
      display: block;        /* Only active one shows */
    }

    @keyframes fadeIn { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: translateY(0); } }

    /* =============================================
       SHARED COMPONENT STYLES
    ============================================= */
    .page-header { margin-bottom: 24px; }
    .page-title { font-size: 22px; font-weight: 800; color: var(--text-dark); }
    .page-sub { font-size: 13px; color: var(--text-muted); margin-top: 4px; }

    .card {
      background: var(--card);
      border-radius: var(--radius);
      padding: 20px;
      box-shadow: var(--shadow-sm);
      border: 1px solid var(--border);
    }
    .card-title { font-size: 15px; font-weight: 700; margin-bottom: 14px; color: var(--text-dark); }

    .btn {
      display: inline-flex;
      align-items: center;
      gap: 7px;
      padding: 10px 18px;
      border-radius: var(--radius-sm);
      font-size: 14px;
      font-weight: 600;
      transition: all .18s;
    }
    .btn-primary { background: var(--green-main); color: #fff; }
    .btn-primary:hover { background: var(--green-dark); }
    .btn-outline { border: 1.5px solid var(--green-main); color: var(--green-main); background: transparent; }
    .btn-outline:hover { background: var(--green-pale); }
    .btn-sm { padding: 7px 14px; font-size: 13px; }
    .btn-danger { background: var(--red); color: #fff; }

    .badge {
      display: inline-block;
      padding: 3px 10px;
      border-radius: 99px;
      font-size: 11px;
      font-weight: 700;
    }
    .badge-green { background: var(--green-light); color: var(--green-dark); }
    .badge-amber { background: #fef3c7; color: #92400e; }
    .badge-blue  { background: #dbeafe; color: #1e40af; }

    .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
    .grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; }
    .grid-4 { display: grid; grid-template-columns: repeat(4, 1fr); gap: 16px; }

    /* =============================================
       HOME SECTION
    ============================================= */
    .hero-banner {
      background: linear-gradient(135deg, var(--green-dark) 0%, var(--green-main) 100%);
      border-radius: var(--radius);
      padding: 28px;
      color: #fff;
      margin-bottom: 24px;
      position: relative;
      overflow: hidden;
    }
    .hero-banner::after {
      content: '♻';
      position: absolute;
      right: 20px;
      top: 50%;
      transform: translateY(-50%);
      font-size: 80px;
      opacity: .12;
    }
    .hero-banner h2 { font-size: 22px; font-weight: 800; margin-bottom: 8px; }
    .hero-banner p  { font-size: 13px; opacity: .85; line-height: 1.6; max-width: 420px; }
    .hero-banner .btn { margin-top: 16px; background: #fff; color: var(--green-dark); }
    .hero-banner .btn:hover { background: var(--green-light); }

    .stat-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(130px, 1fr)); gap: 14px; margin-bottom: 24px; }
    .stat-card {
      background: var(--card);
      border-radius: var(--radius);
      padding: 18px 16px;
      border: 1px solid var(--border);
      box-shadow: var(--shadow-sm);
      display: flex;
      flex-direction: column;
      gap: 6px;
    }
    .stat-icon { width: 36px; height: 36px; border-radius: 8px; display: flex; align-items: center; justify-content: center; font-size: 16px; margin-bottom: 4px; }
    .stat-value { font-size: 24px; font-weight: 800; color: var(--text-dark); font-family: 'DM Mono', monospace; }
    .stat-label { font-size: 12px; color: var(--text-muted); font-weight: 500; }
    .stat-delta { font-size: 11px; font-weight: 600; }
    .stat-delta.up { color: var(--green-main); }

    .home-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }

    .activity-list { display: flex; flex-direction: column; gap: 12px; }
    .activity-item { display: flex; align-items: center; gap: 12px; }
    .act-icon { width: 36px; height: 36px; border-radius: 8px; background: var(--green-pale); display: flex; align-items: center; justify-content: center; color: var(--green-main); font-size: 15px; flex-shrink: 0; }
    .act-info { flex: 1; }
    .act-title { font-size: 13px; font-weight: 600; }
    .act-sub   { font-size: 12px; color: var(--text-muted); }
    .act-pts   { font-size: 13px; font-weight: 700; color: var(--green-main); font-family: 'DM Mono', monospace; }

    /* =============================================
       DASHBOARD SECTION
    ============================================= */
    .progress-bar-wrap { background: var(--border); border-radius: 99px; height: 10px; overflow: hidden; margin-top: 8px; }
    .progress-bar { height: 100%; border-radius: 99px; background: linear-gradient(90deg, var(--green-main), var(--accent)); transition: width .6s ease; }

    .chart-placeholder {
      background: var(--green-pale);
      border-radius: var(--radius-sm);
      height: 160px;
      display: flex;
      align-items: flex-end;
      justify-content: space-around;
      padding: 16px 12px 28px;
      position: relative;
    }
    .bar-wrap { display: flex; flex-direction: column; align-items: center; gap: 6px; flex: 1; }
    .bar {
      width: 28px;
      background: linear-gradient(180deg, var(--green-mid), var(--green-main));
      border-radius: 4px 4px 0 0;
      transition: height .6s ease;
    }
    .bar-label { font-size: 10px; color: var(--text-muted); font-weight: 600; }

    /* =============================================
       SCAN SECTION
    ============================================= */
    .scan-area {
      background: var(--card);
      border-radius: var(--radius);
      padding: 32px 24px;
      text-align: center;
      border: 2px dashed var(--border);
      margin-bottom: 20px;
    }
    .scan-icon-big { font-size: 56px; color: var(--green-light); margin-bottom: 12px; }
    .scan-area h3 { font-size: 18px; font-weight: 700; margin-bottom: 8px; }
    .scan-area p { font-size: 13px; color: var(--text-muted); margin-bottom: 20px; }

    .scan-types { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin-top: 20px; }
    .scan-type { background: var(--green-pale); border-radius: var(--radius-sm); padding: 14px 10px; text-align: center; cursor: pointer; border: 1.5px solid transparent; transition: all .18s; }
    .scan-type:hover, .scan-type.selected { border-color: var(--green-main); background: #dcfce7; }
    .scan-type i  { font-size: 22px; color: var(--green-main); display: block; margin-bottom: 6px; }
    .scan-type span { font-size: 12px; font-weight: 600; color: var(--text-mid); }

    /* =============================================
       ✅ FIX #5: CAMERA MODAL – full screen
    ============================================= */
    #camera-modal {
      display: none;
      position: fixed;
      inset: 0;
      background: #000;
      z-index: 10000;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }
    #camera-modal.open { display: flex; }
    #camera-video {
      width: 100%;
      height: 100%;
      object-fit: cover;
      position: absolute;
      inset: 0;
    }
    .camera-overlay {
      position: relative;
      z-index: 1;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: space-between;
      width: 100%;
      height: 100%;
      padding: 32px 24px;
    }
    .camera-top { display: flex; align-items: center; justify-content: space-between; width: 100%; }
    .camera-title { color: #fff; font-size: 16px; font-weight: 700; text-shadow: 0 1px 6px rgba(0,0,0,.5); }
    .btn-close-cam {
      background: rgba(255,255,255,.18);
      border: 1.5px solid rgba(255,255,255,.35);
      color: #fff;
      border-radius: 50%;
      width: 42px; height: 42px;
      display: flex; align-items: center; justify-content: center;
      font-size: 18px;
      backdrop-filter: blur(6px);
      transition: background .2s;
    }
    .btn-close-cam:hover { background: rgba(255,255,255,.3); }
    .scan-frame {
      width: min(280px, 70vw); height: min(280px, 70vw);
      border: 2px solid rgba(255,255,255,.6);
      border-radius: 16px;
      box-shadow: 0 0 0 4000px rgba(0,0,0,.45);
      position: relative;
    }
    .scan-frame::before, .scan-frame::after,
    .scan-frame .corner-tr, .scan-frame .corner-bl, .scan-frame .corner-br {
      content: '';
      position: absolute;
      width: 22px; height: 22px;
      border-color: var(--green-mid);
      border-style: solid;
    }
    .scan-frame::before  { top: -2px; left: -2px; border-width: 3px 0 0 3px; border-radius: 4px 0 0 0; }
    .scan-frame::after   { top: -2px; right: -2px; border-width: 3px 3px 0 0; border-radius: 0 4px 0 0; }
    .scan-frame .corner-bl { bottom: -2px; left: -2px; border-width: 0 0 3px 3px; border-radius: 0 0 0 4px; }
    .scan-frame .corner-br { bottom: -2px; right: -2px; border-width: 0 3px 3px 0; border-radius: 0 0 4px 0; }
    .scan-line {
      position: absolute;
      left: 0; right: 0;
      height: 2px;
      background: linear-gradient(90deg, transparent, var(--green-mid), transparent);
      animation: scanLine 2s ease-in-out infinite;
    }
    @keyframes scanLine { 0%,100% { top: 8px; } 50% { top: calc(100% - 10px); } }
    .camera-bottom { display: flex; flex-direction: column; align-items: center; gap: 16px; }
    .camera-hint { color: rgba(255,255,255,.75); font-size: 13px; text-align: center; }
    .btn-capture {
      width: 64px; height: 64px;
      border-radius: 50%;
      background: #fff;
      border: 4px solid rgba(255,255,255,.4);
      display: flex; align-items: center; justify-content: center;
      font-size: 24px; color: var(--green-dark);
      transition: transform .15s;
    }
    .btn-capture:hover { transform: scale(1.08); }

    /* Camera permission error */
    #cam-error { color: #fff; text-align: center; font-size: 14px; padding: 20px; display: none; }

    /* =============================================
       REWARDS SECTION
    ============================================= */
    .credits-hero {
      background: linear-gradient(135deg, #065f46, var(--green-main));
      border-radius: var(--radius);
      padding: 24px;
      color: #fff;
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 20px;
    }
    .credits-hero h3 { font-size: 14px; opacity: .8; margin-bottom: 4px; }
    .credits-hero .big-num { font-size: 42px; font-weight: 800; font-family: 'DM Mono', monospace; }
    .credits-hero .sub { font-size: 12px; opacity: .75; }
    .credits-icon { font-size: 52px; opacity: .25; }

    .reward-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 14px; }
    .reward-card {
      background: var(--card);
      border-radius: var(--radius);
      padding: 18px;
      border: 1px solid var(--border);
      text-align: center;
      cursor: pointer;
      transition: all .2s;
    }
    .reward-card:hover { border-color: var(--green-main); transform: translateY(-2px); box-shadow: var(--shadow-md); }
    .reward-card i  { font-size: 32px; margin-bottom: 10px; display: block; }
    .reward-card h4 { font-size: 14px; font-weight: 700; margin-bottom: 6px; }
    .reward-card p  { font-size: 12px; color: var(--text-muted); margin-bottom: 12px; }
    .reward-cost    { font-size: 13px; font-weight: 700; color: var(--green-main); font-family: 'DM Mono', monospace; }

    /* =============================================
       MAP SECTION
    ============================================= */
    .map-placeholder {
      background: #d1fae5;
      border-radius: var(--radius);
      height: 340px;
      position: relative;
      overflow: hidden;
      margin-bottom: 16px;
    }
    .map-placeholder svg { width: 100%; height: 100%; }
    .map-pin {
      position: absolute;
      font-size: 26px;
      cursor: pointer;
      filter: drop-shadow(0 2px 4px rgba(0,0,0,.25));
      transition: transform .2s;
    }
    .map-pin:hover { transform: scale(1.25); }

    .dustbin-list { display: flex; flex-direction: column; gap: 10px; }
    .dustbin-item {
      background: var(--card);
      border-radius: var(--radius-sm);
      padding: 14px 16px;
      border: 1px solid var(--border);
      display: flex;
      align-items: center;
      gap: 14px;
    }
    .dustbin-icon { font-size: 22px; width: 44px; height: 44px; border-radius: 10px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
    .dustbin-icon.full  { background: #fee2e2; }
    .dustbin-icon.half  { background: #fef9c3; }
    .dustbin-icon.empty { background: #dcfce7; }
    .dustbin-info { flex: 1; }
    .dustbin-name { font-size: 14px; font-weight: 600; }
    .dustbin-addr { font-size: 12px; color: var(--text-muted); }
    .fill-bar-wrap { display: flex; align-items: center; gap: 8px; margin-top: 4px; }
    .fill-bar { flex: 1; height: 6px; background: var(--border); border-radius: 99px; overflow: hidden; }
    .fill-inner { height: 100%; border-radius: 99px; }
    .fill-inner.full  { background: var(--red); }
    .fill-inner.half  { background: var(--amber); }
    .fill-inner.empty { background: var(--green-main); }
    .fill-pct { font-size: 11px; font-weight: 700; color: var(--text-muted); width: 30px; text-align: right; font-family: 'DM Mono', monospace; }

    /* =============================================
       SMART DUSTBIN SECTION
    ============================================= */
    .sensor-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); gap: 14px; margin-bottom: 20px; }
    .sensor-card {
      background: var(--card);
      border-radius: var(--radius);
      padding: 16px;
      border: 1px solid var(--border);
      text-align: center;
    }
    .sensor-val { font-size: 28px; font-weight: 800; font-family: 'DM Mono', monospace; margin: 8px 0 4px; }
    .sensor-lbl { font-size: 12px; color: var(--text-muted); }

    .bin-visual {
      width: 100%; max-width: 200px;
      margin: 0 auto 20px;
      position: relative;
    }
    .bin-body {
      width: 120px; height: 180px;
      background: #e2e8f0;
      border-radius: 8px 8px 14px 14px;
      margin: 0 auto;
      position: relative;
      overflow: hidden;
      border: 2px solid #cbd5e1;
    }
    .bin-fill {
      position: absolute;
      bottom: 0; left: 0; right: 0;
      background: linear-gradient(0deg, var(--green-main), var(--accent));
      transition: height .8s ease;
      border-radius: 0 0 12px 12px;
    }
    .bin-pct-label {
      position: absolute;
      top: 50%; left: 50%; transform: translate(-50%,-50%);
      font-size: 18px; font-weight: 800;
      color: #fff;
      text-shadow: 0 1px 4px rgba(0,0,0,.3);
      z-index: 1;
    }
    .bin-lid {
      width: 130px; height: 20px;
      background: #94a3b8;
      border-radius: 4px;
      margin: 0 auto 4px;
      border: 2px solid #64748b;
    }

    /* =============================================
       LEADERBOARD SECTION
    ============================================= */
    .podium { display: flex; align-items: flex-end; justify-content: center; gap: 12px; margin-bottom: 24px; }
    .podium-block { display: flex; flex-direction: column; align-items: center; gap: 8px; }
    .podium-avatar {
      width: 48px; height: 48px; border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      font-size: 18px; font-weight: 800; color: #fff;
    }
    .podium-platform {
      border-radius: 8px 8px 0 0;
      width: 80px;
      display: flex; flex-direction: column; align-items: center; justify-content: flex-end;
      padding-bottom: 8px;
    }
    .podium-rank { font-size: 11px; font-weight: 700; color: rgba(255,255,255,.8); }
    .podium-name { font-size: 12px; font-weight: 700; }
    .podium-pts  { font-size: 11px; color: var(--text-muted); font-family: 'DM Mono', monospace; }
    .p-1 .podium-platform { height: 90px; background: linear-gradient(180deg, #fbbf24, #f59e0b); }
    .p-2 .podium-platform { height: 70px; background: linear-gradient(180deg, #94a3b8, #64748b); }
    .p-3 .podium-platform { height: 55px; background: linear-gradient(180deg, #a78bfa, #7c3aed); }
    .p-1 .podium-avatar { background: #f59e0b; }
    .p-2 .podium-avatar { background: #64748b; }
    .p-3 .podium-avatar { background: #7c3aed; }

    .lb-table { width: 100%; border-collapse: collapse; }
    .lb-table th { text-align: left; font-size: 12px; color: var(--text-muted); font-weight: 600; padding: 8px 12px; border-bottom: 1px solid var(--border); }
    .lb-table td { padding: 12px 12px; font-size: 14px; border-bottom: 1px solid var(--border); }
    .lb-table tr:last-child td { border-bottom: none; }
    .lb-rank { font-weight: 700; font-family: 'DM Mono', monospace; color: var(--text-muted); }
    .lb-user { display: flex; align-items: center; gap: 10px; }
    .lb-avatar { width: 32px; height: 32px; border-radius: 50%; background: var(--green-light); display: flex; align-items: center; justify-content: center; font-weight: 700; font-size: 12px; color: var(--green-dark); }
    .lb-pts { font-family: 'DM Mono', monospace; font-weight: 700; color: var(--green-main); }

    /* =============================================
       PROFILE SECTION
    ============================================= */
    .profile-top {
      background: linear-gradient(135deg, var(--green-dark), var(--green-main));
      border-radius: var(--radius);
      padding: 28px;
      color: #fff;
      display: flex;
      align-items: center;
      gap: 20px;
      margin-bottom: 20px;
    }
    .profile-avatar {
      width: 72px; height: 72px;
      border-radius: 50%;
      background: rgba(255,255,255,.2);
      border: 3px solid rgba(255,255,255,.4);
      display: flex; align-items: center; justify-content: center;
      font-size: 28px; font-weight: 800;
      flex-shrink: 0;
    }
    .profile-name { font-size: 20px; font-weight: 800; }
    .profile-email { font-size: 13px; opacity: .8; margin-bottom: 8px; }
    .profile-badge { display: inline-block; background: rgba(255,255,255,.2); padding: 4px 12px; border-radius: 99px; font-size: 12px; font-weight: 600; }

    .profile-stats { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin-bottom: 20px; text-align: center; }
    .pstat-val { font-size: 22px; font-weight: 800; font-family: 'DM Mono', monospace; color: var(--green-main); }
    .pstat-lbl { font-size: 11px; color: var(--text-muted); }

    .setting-list { display: flex; flex-direction: column; gap: 2px; }
    .setting-item {
      display: flex; align-items: center; gap: 14px;
      padding: 14px 16px;
      border-radius: var(--radius-sm);
      cursor: pointer;
      transition: background .15s;
    }
    .setting-item:hover { background: var(--bg); }
    .setting-item i { width: 20px; color: var(--text-muted); }
    .setting-item span { flex: 1; font-size: 14px; }
    .setting-item .arrow { color: var(--text-muted); font-size: 12px; }

    /* =============================================
       CONTACT SECTION
    ============================================= */
    .contact-form { display: flex; flex-direction: column; gap: 14px; }
    .input-row { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
    .form-field label { display: block; font-size: 13px; font-weight: 600; margin-bottom: 6px; color: var(--text-mid); }
    .form-field input,
    .form-field textarea,
    .form-field select {
      width: 100%; padding: 12px 14px;
      border: 1.5px solid var(--border);
      border-radius: var(--radius-sm);
      font-size: 14px;
      background: var(--card);
      transition: border-color .2s;
    }
    .form-field input:focus,
    .form-field textarea:focus { border-color: var(--green-main); }
    .form-field textarea { resize: vertical; min-height: 110px; }
    .contact-info-list { display: flex; flex-direction: column; gap: 12px; }
    .ci-item { display: flex; align-items: center; gap: 12px; font-size: 14px; }
    .ci-item i { color: var(--green-main); width: 18px; }

    /* =============================================
       PLASTIC CREDIT ECONOMY WIDGET
    ============================================= */
    .credit-economy {
      background: linear-gradient(135deg, #064e2c 0%, #0f766e 100%);
      border-radius: var(--radius);
      padding: 20px;
      color: #fff;
    }
    .credit-economy h3 { font-size: 15px; font-weight: 700; margin-bottom: 6px; }
    .credit-economy p  { font-size: 12px; opacity: .8; line-height: 1.5; margin-bottom: 14px; }
    .credit-flow { display: flex; align-items: center; justify-content: space-between; gap: 4px; flex-wrap: wrap; }
    .cf-step { display: flex; flex-direction: column; align-items: center; gap: 4px; }
    .cf-icon { width: 38px; height: 38px; border-radius: 8px; background: rgba(255,255,255,.15); display: flex; align-items: center; justify-content: center; font-size: 16px; }
    .cf-label { font-size: 10px; font-weight: 600; opacity: .8; text-align: center; max-width: 60px; }
    .cf-arrow { color: var(--green-mid); font-size: 16px; padding-bottom: 16px; }

    /* =============================================
       MOBILE BOTTOM NAV
    ============================================= */
    .bottom-nav {
      display: none;
      position: fixed;
      bottom: 0; left: 0; right: 0;
      background: var(--card);
      border-top: 1px solid var(--border);
      padding: 6px 0 env(safe-area-inset-bottom, 6px);
      z-index: 200;
      justify-content: space-around;
    }
    .bn-item {
      display: flex; flex-direction: column; align-items: center; gap: 3px;
      padding: 6px 8px;
      border-radius: var(--radius-sm);
      cursor: pointer;
      color: var(--text-muted);
      font-size: 10px;
      font-weight: 600;
      flex: 1;
      min-width: 0;
      transition: color .15s;
    }
    .bn-item i { font-size: 18px; }
    .bn-item.active { color: var(--green-main); }

    /* =============================================
       OVERLAY (mobile sidebar)
    ============================================= */
    #sidebar-overlay {
      display: none;
      position: fixed; inset: 0;
      background: rgba(0,0,0,.4);
      z-index: 50;
    }

    /* =============================================
       TOAST NOTIFICATION
    ============================================= */
    #toast {
      position: fixed;
      bottom: 80px; left: 50%; transform: translateX(-50%) translateY(20px);
      background: var(--green-dark);
      color: #fff;
      padding: 11px 22px;
      border-radius: 99px;
      font-size: 13px;
      font-weight: 600;
      opacity: 0;
      pointer-events: none;
      transition: all .3s;
      z-index: 9000;
      white-space: nowrap;
    }
    #toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }

    /* =============================================
       ✅ FIX #6: RESPONSIVE BREAKPOINTS
    ============================================= */
    @media (max-width: 900px) {
      .grid-4 { grid-template-columns: repeat(2, 1fr); }
      .home-row { grid-template-columns: 1fr; }
    }

    @media (max-width: 768px) {
      :root { --sidebar-w: 260px; }

      /* Sidebar becomes drawer on mobile */
      .sidebar {
        position: fixed;
        top: var(--nav-h); bottom: 0; left: 0;
        z-index: 100;
        transform: translateX(-100%);
      }
      .sidebar.open { transform: translateX(0); }
      #sidebar-overlay.open { display: block; }

      .hamburger { display: flex; }
      .bottom-nav { display: flex; }
      .main-content { padding-bottom: 70px; }

      .section { padding: 16px 14px; }
      .grid-2, .grid-3 { grid-template-columns: 1fr; }
      .grid-4 { grid-template-columns: 1fr 1fr; }
      .reward-grid { grid-template-columns: 1fr 1fr; }
      .scan-types { grid-template-columns: repeat(3, 1fr); }
      .input-row { grid-template-columns: 1fr; }
      .profile-stats { grid-template-columns: repeat(3, 1fr); }

      .auth-box { padding: 32px 24px; }
      .credits-hero { flex-direction: column; text-align: center; gap: 10px; }
      .credits-hero .credits-icon { display: none; }
    }

    @media (max-width: 480px) {
      .stat-grid { grid-template-columns: repeat(2, 1fr); }
      .reward-grid { grid-template-columns: 1fr; }
      .scan-types { grid-template-columns: repeat(2, 1fr); }
      .hero-banner h2 { font-size: 18px; }
      .podium { gap: 6px; }
      .podium-platform { width: 64px; }
    }
  </style>
</head>
<body>

  <!-- =========================================
       AUTH SCREEN
  ========================================= -->
  <div id="auth-screen">
    <div class="auth-box">
      <div class="auth-logo">
        <i class="fas fa-recycle"></i>
        <span>EcoTrack</span>
      </div>
      <p class="auth-tagline">Smart Plastic Waste Management System</p>

      <div class="auth-tabs">
        <button class="auth-tab active" id="tab-login" onclick="switchAuthTab('login')">Login</button>
        <button class="auth-tab" id="tab-signup" onclick="switchAuthTab('signup')">Sign Up</button>
      </div>

      <!-- Login Form -->
      <div id="login-form">
        <div class="form-group">
          <label>Email Address</label>
          <input type="email" id="login-email" placeholder="you@example.com" />
          <div class="form-error" id="login-email-err">Please enter a valid email.</div>
        </div>
        <div class="form-group">
          <label>Password</label>
          <input type="password" id="login-pass" placeholder="••••••••" />
          <div class="form-error" id="login-pass-err">Password must be at least 6 characters.</div>
        </div>
        <button class="btn-auth" onclick="doLogin()">
          <i class="fas fa-leaf" style="margin-right:6px"></i>Login to EcoTrack
        </button>
        <p style="text-align:center; font-size:12px; color:var(--text-muted); margin-top:12px;">
          Demo: use any email + 6+ char password
        </p>
      </div>

      <!-- Signup Form -->
      <div id="signup-form" style="display:none">
        <div class="form-group">
          <label>Full Name</label>
          <input type="text" id="signup-name" placeholder="Arjun Sharma" />
          <div class="form-error" id="signup-name-err">Please enter your name.</div>
        </div>
        <div class="form-group">
          <label>Email Address</label>
          <input type="email" id="signup-email" placeholder="you@example.com" />
          <div class="form-error" id="signup-email-err">Please enter a valid email.</div>
        </div>
        <div class="form-group">
          <label>Password</label>
          <input type="password" id="signup-pass" placeholder="Min. 6 characters" />
          <div class="form-error" id="signup-pass-err">Password must be at least 6 characters.</div>
        </div>
        <button class="btn-auth" onclick="doSignup()">
          <i class="fas fa-seedling" style="margin-right:6px"></i>Create EcoTrack Account
        </button>
      </div>
    </div>
  </div>

  <!-- =========================================
       MAIN APP
  ========================================= -->
  <div id="app">

    <!-- TOP BAR -->
    <header class="topbar">
      <div style="display:flex; align-items:center; gap:12px;">
        <div class="hamburger" onclick="toggleSidebar()" aria-label="Menu">
          <span></span><span></span><span></span>
        </div>
        <div class="topbar-logo">
          <i class="fas fa-recycle"></i>
          <span>EcoTrack</span>
        </div>
      </div>
      <div class="topbar-right">
        <i class="fas fa-bell topbar-icon" onclick="showToast('🔔 No new notifications')"></i>
        <div class="topbar-avatar" id="user-avatar" onclick="showSection('profile')">A</div>
      </div>
    </header>

    <!-- SIDEBAR OVERLAY (mobile) -->
    <div id="sidebar-overlay" onclick="closeSidebar()"></div>

    <!-- APP BODY -->
    <div class="app-body">

      <!-- SIDEBAR NAV -->
      <nav class="sidebar" id="sidebar">
        <ul class="nav-menu">
          <li class="nav-item active" onclick="showSection('home')"    id="nav-home">    <i class="fas fa-home"></i>         Home</li>
          <li class="nav-item"        onclick="showSection('dashboard')"id="nav-dashboard"><i class="fas fa-chart-bar"></i>    Dashboard</li>
          <li class="nav-item"        onclick="showSection('scan')"    id="nav-scan">    <i class="fas fa-camera"></i>       Scan Waste</li>
          <li class="nav-item"        onclick="showSection('rewards')" id="nav-rewards"> <i class="fas fa-gift"></i>         Rewards</li>
          <li class="nav-item"        onclick="showSection('map')"     id="nav-map">     <i class="fas fa-map-marker-alt"></i>Map</li>
          <li class="nav-item"        onclick="showSection('dustbin')" id="nav-dustbin"> <i class="fas fa-trash-alt"></i>    Smart Dustbin</li>
          <li class="nav-item"        onclick="showSection('leaderboard')"id="nav-leaderboard"><i class="fas fa-trophy"></i> Leaderboard</li>
          <li class="nav-item"        onclick="showSection('profile')" id="nav-profile"> <i class="fas fa-user"></i>         Profile</li>
          <li class="nav-item"        onclick="showSection('contact')" id="nav-contact"> <i class="fas fa-envelope"></i>     Contact</li>
        </ul>
        <div class="sidebar-footer">
          <div class="eco-tip">
            <strong>🌱 Eco Tip</strong>
            One plastic bottle takes 450 years to decompose. Scan &amp; recycle today!
          </div>
        </div>
      </nav>

      <!-- MAIN CONTENT AREA -->
      <main class="main-content" id="main-content">

        <!-- ===== HOME ===== -->
        <section class="section active-section" id="sec-home">
          <div class="page-header">
            <div class="page-title">Welcome back, Arjun! 👋</div>
            <div class="page-sub">Here's your environmental impact summary</div>
          </div>

          <div class="hero-banner">
            <div>
              <h2>♻️ Plastic Credit Economy</h2>
              <p>Every piece of plastic you recycle earns Plastic Credits (PCs). Redeem them for real rewards – discounts, coupons, and eco-products!</p>
              <button class="btn" onclick="showSection('scan')"><i class="fas fa-camera"></i> Scan &amp; Earn Now</button>
            </div>
          </div>

          <div class="stat-grid">
            <div class="stat-card">
              <div class="stat-icon" style="background:#dcfce7"><i class="fas fa-recycle" style="color:var(--green-main)"></i></div>
              <div class="stat-value">142</div>
              <div class="stat-label">Items Recycled</div>
              <div class="stat-delta up">↑ 12 this week</div>
            </div>
            <div class="stat-card">
              <div class="stat-icon" style="background:#dbeafe"><i class="fas fa-coins" style="color:#3b82f6"></i></div>
              <div class="stat-value">2,840</div>
              <div class="stat-label">Plastic Credits</div>
              <div class="stat-delta up">↑ 320 earned</div>
            </div>
            <div class="stat-card">
              <div class="stat-icon" style="background:#fef9c3"><i class="fas fa-leaf" style="color:#ca8a04"></i></div>
              <div class="stat-value">8.4</div>
              <div class="stat-label">CO₂ Saved (kg)</div>
              <div class="stat-delta up">↑ Great impact</div>
            </div>
            <div class="stat-card">
              <div class="stat-icon" style="background:#ede9fe"><i class="fas fa-trophy" style="color:#7c3aed"></i></div>
              <div class="stat-value">#7</div>
              <div class="stat-label">City Rank</div>
              <div class="stat-delta up">↑ 3 spots up</div>
            </div>
          </div>

          <div class="home-row">
            <div class="card">
              <div class="card-title">Recent Activity</div>
              <div class="activity-list">
                <div class="activity-item">
                  <div class="act-icon"><i class="fas fa-wine-bottle"></i></div>
                  <div class="act-info"><div class="act-title">PET Bottle Scanned</div><div class="act-sub">2 hours ago · Sector 14</div></div>
                  <div class="act-pts">+40 PC</div>
                </div>
                <div class="activity-item">
                  <div class="act-icon"><i class="fas fa-shopping-bag"></i></div>
                  <div class="act-info"><div class="act-title">Plastic Bag Dropped</div><div class="act-sub">Yesterday · Smart Bin #3</div></div>
                  <div class="act-pts">+20 PC</div>
                </div>
                <div class="activity-item">
                  <div class="act-icon"><i class="fas fa-gift"></i></div>
                  <div class="act-info"><div class="act-title">Reward Redeemed</div><div class="act-sub">3 days ago · Eco-Bag</div></div>
                  <div class="act-pts">-150 PC</div>
                </div>
                <div class="activity-item">
                  <div class="act-icon"><i class="fas fa-box"></i></div>
                  <div class="act-info"><div class="act-title">Packaging Recycled</div><div class="act-sub">4 days ago · Drop Point</div></div>
                  <div class="act-pts">+60 PC</div>
                </div>
              </div>
            </div>

            <div class="card">
              <div class="card-title">Plastic Credit Economy</div>
              <div class="credit-economy">
                <h3>🌍 How It Works</h3>
                <p>Recycle plastic → Earn Credits → Redeem Rewards → Reduce Waste. Your actions drive a circular economy.</p>
                <div class="credit-flow">
                  <div class="cf-step"><div class="cf-icon">♻️</div><div class="cf-label">Recycle</div></div>
                  <div class="cf-arrow">›</div>
                  <div class="cf-step"><div class="cf-icon">🪙</div><div class="cf-label">Earn PCs</div></div>
                  <div class="cf-arrow">›</div>
                  <div class="cf-step"><div class="cf-icon">🎁</div><div class="cf-label">Redeem</div></div>
                  <div class="cf-arrow">›</div>
                  <div class="cf-step"><div class="cf-icon">🌱</div><div class="cf-label">Planet Wins</div></div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <!-- ===== DASHBOARD ===== -->
        <section class="section" id="sec-dashboard">
          <div class="page-header">
            <div class="page-title">Dashboard</div>
            <div class="page-sub">Your recycling performance overview</div>
          </div>

          <div class="grid-2" style="margin-bottom:20px">
            <div class="card">
              <div class="card-title">Monthly Recycling Progress</div>
              <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:6px">
                <span style="font-size:13px; color:var(--text-muted)">Goal: 200 items</span>
                <span style="font-size:13px; font-weight:700; color:var(--green-main)">142 / 200</span>
              </div>
              <div class="progress-bar-wrap"><div class="progress-bar" style="width:71%"></div></div>
              <p style="font-size:12px; color:var(--text-muted); margin-top:10px">71% of monthly goal reached. Keep it up!</p>
            </div>
            <div class="card">
              <div class="card-title">Carbon Footprint Saved</div>
              <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:6px">
                <span style="font-size:13px; color:var(--text-muted)">Target: 15 kg CO₂</span>
                <span style="font-size:13px; font-weight:700; color:var(--green-main)">8.4 / 15 kg</span>
              </div>
              <div class="progress-bar-wrap"><div class="progress-bar" style="width:56%"></div></div>
              <p style="font-size:12px; color:var(--text-muted); margin-top:10px">Every kg of CO₂ saved = 1 tree's daily work.</p>
            </div>
          </div>

          <div class="card" style="margin-bottom:20px">
            <div class="card-title">Weekly Recycling Activity</div>
            <div class="chart-placeholder">
              <div class="bar-wrap"><div class="bar" style="height:55px"></div><div class="bar-label">Mon</div></div>
              <div class="bar-wrap"><div class="bar" style="height:80px"></div><div class="bar-label">Tue</div></div>
              <div class="bar-wrap"><div class="bar" style="height:40px"></div><div class="bar-label">Wed</div></div>
              <div class="bar-wrap"><div class="bar" style="height:100px"></div><div class="bar-label">Thu</div></div>
              <div class="bar-wrap"><div class="bar" style="height:65px"></div><div class="bar-label">Fri</div></div>
              <div class="bar-wrap"><div class="bar" style="height:90px"></div><div class="bar-label">Sat</div></div>
              <div class="bar-wrap"><div class="bar" style="height:30px"></div><div class="bar-label">Sun</div></div>
            </div>
          </div>

          <div class="grid-3">
            <div class="card" style="text-align:center">
              <div style="font-size:32px; margin-bottom:8px">🥤</div>
              <div style="font-size:20px; font-weight:800; font-family:'DM Mono',monospace; color:var(--green-main)">68</div>
              <div style="font-size:12px; color:var(--text-muted)">PET Bottles</div>
            </div>
            <div class="card" style="text-align:center">
              <div style="font-size:32px; margin-bottom:8px">🛍️</div>
              <div style="font-size:20px; font-weight:800; font-family:'DM Mono',monospace; color:var(--green-main)">34</div>
              <div style="font-size:12px; color:var(--text-muted)">Carry Bags</div>
            </div>
            <div class="card" style="text-align:center">
              <div style="font-size:32px; margin-bottom:8px">📦</div>
              <div style="font-size:20px; font-weight:800; font-family:'DM Mono',monospace; color:var(--green-main)">40</div>
              <div style="font-size:12px; color:var(--text-muted)">Packaging</div>
            </div>
          </div>
        </section>

        <!-- ===== SCAN ===== -->
        <section class="section" id="sec-scan">
          <div class="page-header">
            <div class="page-title">Scan Plastic Waste</div>
            <div class="page-sub">Identify plastic type and earn Plastic Credits</div>
          </div>

          <div class="scan-area">
            <div class="scan-icon-big">♻️</div>
            <h3>Ready to Scan</h3>
            <p>Point your camera at a plastic item to identify it and earn credits automatically.</p>
            <button class="btn btn-primary" onclick="openCamera()">
              <i class="fas fa-camera"></i> Open Camera
            </button>
          </div>

          <div class="card" style="margin-bottom:16px">
            <div class="card-title">Choose Plastic Type</div>
            <div class="scan-types">
              <div class="scan-type selected" onclick="selectScanType(this)">
                <i class="fas fa-wine-bottle"></i>
                <span>PET Bottle<br><small style="color:var(--text-muted)">+40 PC</small></span>
              </div>
              <div class="scan-type" onclick="selectScanType(this)">
                <i class="fas fa-shopping-bag"></i>
                <span>Plastic Bag<br><small style="color:var(--text-muted)">+20 PC</small></span>
              </div>
              <div class="scan-type" onclick="selectScanType(this)">
                <i class="fas fa-box"></i>
                <span>Packaging<br><small style="color:var(--text-muted)">+60 PC</small></span>
              </div>
              <div class="scan-type" onclick="selectScanType(this)">
                <i class="fas fa-cup-straw"></i>
                <span>Cup/Straw<br><small style="color:var(--text-muted)">+15 PC</small></span>
              </div>
              <div class="scan-type" onclick="selectScanType(this)">
                <i class="fas fa-container-storage"></i>
                <span>Container<br><small style="color:var(--text-muted)">+50 PC</small></span>
              </div>
              <div class="scan-type" onclick="selectScanType(this)">
                <i class="fas fa-question-circle"></i>
                <span>Other<br><small style="color:var(--text-muted)">+10 PC</small></span>
              </div>
            </div>
          </div>

          <div class="card">
            <div class="card-title">Manual Log Entry</div>
            <div style="display:flex; gap:10px; flex-wrap:wrap; align-items:center">
              <select style="flex:1; min-width:140px; padding:10px 12px; border:1.5px solid var(--border); border-radius:var(--radius-sm); font-size:14px; background:#fff">
                <option>PET Bottle (+40 PC)</option>
                <option>Plastic Bag (+20 PC)</option>
                <option>Packaging (+60 PC)</option>
                <option>Cup / Straw (+15 PC)</option>
                <option>Container (+50 PC)</option>
              </select>
              <input type="number" min="1" max="50" value="1" style="width:80px; padding:10px 12px; border:1.5px solid var(--border); border-radius:var(--radius-sm); font-size:14px" />
              <button class="btn btn-primary" onclick="logManual()"><i class="fas fa-plus"></i> Log</button>
            </div>
          </div>
        </section>

        <!-- ===== REWARDS ===== -->
        <section class="section" id="sec-rewards">
          <div class="page-header">
            <div class="page-title">Rewards</div>
            <div class="page-sub">Redeem your Plastic Credits for eco-rewards</div>
          </div>

          <div class="credits-hero">
            <div>
              <h3>Your Plastic Credits</h3>
              <div class="big-num">2,840</div>
              <div class="sub">Earned this month: +320 PC · Lifetime: 12,400 PC</div>
            </div>
            <div class="credits-icon">🪙</div>
          </div>

          <div class="card" style="margin-bottom:20px">
            <div class="card-title">💡 About Plastic Credits</div>
            <p style="font-size:13px; color:var(--text-mid); line-height:1.6">Plastic Credits (PC) are your eco-currency. Every plastic item you scan and recycle adds to your balance. Use them to claim real-world rewards and contribute to a sustainable circular economy.</p>
          </div>

          <div class="card-title" style="margin-bottom:12px">Available Rewards</div>
          <div class="reward-grid">
            <div class="reward-card" onclick="redeemReward(this, 150)">
              <i style="color:#22c55e">🛍️</i>
              <h4>Eco Carry Bag</h4>
              <p>Reusable jute bag – replace 500 plastic bags</p>
              <div class="reward-cost">150 PC</div>
            </div>
            <div class="reward-card" onclick="redeemReward(this, 300)">
              <i style="color:#3b82f6">💧</i>
              <h4>Steel Water Bottle</h4>
              <p>BPA-free, keeps drinks cold for 24 hours</p>
              <div class="reward-cost">300 PC</div>
            </div>
            <div class="reward-card" onclick="redeemReward(this, 500)">
              <i style="color:#f59e0b">🌿</i>
              <h4>Plant a Tree</h4>
              <p>We'll plant a tree in your name locally</p>
              <div class="reward-cost">500 PC</div>
            </div>
            <div class="reward-card" onclick="redeemReward(this, 200)">
              <i style="color:#a855f7">🎫</i>
              <h4>10% Off Coupon</h4>
              <p>Discount at partnered eco-stores</p>
              <div class="reward-cost">200 PC</div>
            </div>
            <div class="reward-card" onclick="redeemReward(this, 1000)">
              <i style="color:#0ea5e9">☀️</i>
              <h4>Solar Charger</h4>
              <p>Portable solar-powered phone charger</p>
              <div class="reward-cost">1,000 PC</div>
            </div>
            <div class="reward-card" onclick="redeemReward(this, 250)">
              <i style="color:#10b981">🌱</i>
              <h4>Seed Kit</h4>
              <p>Grow your own herb garden at home</p>
              <div class="reward-cost">250 PC</div>
            </div>
          </div>
        </section>

        <!-- ===== MAP ===== -->
        <section class="section" id="sec-map">
          <div class="page-header">
            <div class="page-title">Recycling Map</div>
            <div class="page-sub">Find smart dustbins and drop points near you</div>
          </div>

          <!-- Simple SVG Map Placeholder -->
          <div class="map-placeholder">
            <svg viewBox="0 0 600 340" xmlns="http://www.w3.org/2000/svg">
              <rect width="600" height="340" fill="#d1fae5"/>
              <!-- Roads -->
              <line x1="0" y1="170" x2="600" y2="170" stroke="#a7f3d0" stroke-width="12"/>
              <line x1="300" y1="0" x2="300" y2="340" stroke="#a7f3d0" stroke-width="12"/>
              <line x1="0" y1="100" x2="600" y2="100" stroke="#a7f3d0" stroke-width="6"/>
              <line x1="0" y1="240" x2="600" y2="240" stroke="#a7f3d0" stroke-width="6"/>
              <line x1="150" y1="0" x2="150" y2="340" stroke="#a7f3d0" stroke-width="6"/>
              <line x1="450" y1="0" x2="450" y2="340" stroke="#a7f3d0" stroke-width="6"/>
              <!-- Labels -->
              <text x="80" y="60" fill="#059669" font-size="12" font-family="sans-serif">Sector 14</text>
              <text x="330" y="60" fill="#059669" font-size="12" font-family="sans-serif">Market Area</text>
              <text x="80" y="210" fill="#059669" font-size="12" font-family="sans-serif">Park Zone</text>
              <text x="330" y="210" fill="#059669" font-size="12" font-family="sans-serif">City Center</text>
              <text x="470" y="210" fill="#059669" font-size="12" font-family="sans-serif">Station</text>
            </svg>
            <!-- Pins -->
            <div class="map-pin" style="left:18%; top:30%" title="Smart Bin #1 – 30% full" onclick="showToast('📍 Smart Bin #1 – 30% Full')">🟢</div>
            <div class="map-pin" style="left:52%; top:20%" title="Smart Bin #2 – 80% full" onclick="showToast('📍 Smart Bin #2 – 80% Full!')">🔴</div>
            <div class="map-pin" style="left:35%; top:55%" title="Drop Point – Open" onclick="showToast('📍 Drop Point – Open till 8PM')">♻️</div>
            <div class="map-pin" style="left:70%; top:60%" title="Smart Bin #3 – 55% full" onclick="showToast('📍 Smart Bin #3 – 55% Full')">🟡</div>
            <div class="map-pin" style="left:80%; top:25%" title="Collection Centre" onclick="showToast('📍 Collection Centre – Weekdays 9-5')">🏭</div>
          </div>

          <div class="card" style="margin-bottom:16px">
            <div style="display:flex; gap:16px; flex-wrap:wrap; font-size:12px; font-weight:600">
              <span>🟢 Empty (&lt;40%)</span>
              <span>🟡 Half (40–75%)</span>
              <span>🔴 Full (&gt;75%)</span>
              <span>♻️ Drop Point</span>
              <span>🏭 Collection Centre</span>
            </div>
          </div>

          <div class="card">
            <div class="card-title">Nearby Smart Dustbins</div>
            <div class="dustbin-list">
              <div class="dustbin-item">
                <div class="dustbin-icon empty">🗑️</div>
                <div class="dustbin-info">
                  <div class="dustbin-name">Smart Bin #1 – Sector 14</div>
                  <div class="dustbin-addr">Near Gandhi Park Gate, 0.3 km</div>
                  <div class="fill-bar-wrap">
                    <div class="fill-bar"><div class="fill-inner empty" style="width:30%"></div></div>
                    <div class="fill-pct">30%</div>
                  </div>
                </div>
                <span class="badge badge-green">Empty</span>
              </div>
              <div class="dustbin-item">
                <div class="dustbin-icon full">🗑️</div>
                <div class="dustbin-info">
                  <div class="dustbin-name">Smart Bin #2 – Market Area</div>
                  <div class="dustbin-addr">Main Bazar Chowk, 0.7 km</div>
                  <div class="fill-bar-wrap">
                    <div class="fill-bar"><div class="fill-inner full" style="width:82%"></div></div>
                    <div class="fill-pct">82%</div>
                  </div>
                </div>
                <span class="badge badge-amber">Full</span>
              </div>
              <div class="dustbin-item">
                <div class="dustbin-icon half">🗑️</div>
                <div class="dustbin-info">
                  <div class="dustbin-name">Smart Bin #3 – City Center</div>
                  <div class="dustbin-addr">Opp. Metro Station, 1.2 km</div>
                  <div class="fill-bar-wrap">
                    <div class="fill-bar"><div class="fill-inner half" style="width:55%"></div></div>
                    <div class="fill-pct">55%</div>
                  </div>
                </div>
                <span class="badge badge-blue">Half</span>
              </div>
            </div>
          </div>
        </section>

        <!-- ===== SMART DUSTBIN ===== -->
        <section class="section" id="sec-dustbin">
          <div class="page-header">
            <div class="page-title">Smart Dustbin</div>
            <div class="page-sub">Real-time IoT bin monitoring</div>
          </div>

          <div class="sensor-grid">
            <div class="sensor-card">
              <div style="font-size:22px">📊</div>
              <div class="sensor-val" style="color:var(--amber)">62%</div>
              <div class="sensor-lbl">Fill Level</div>
            </div>
            <div class="sensor-card">
              <div style="font-size:22px">🌡️</div>
              <div class="sensor-val" style="color:var(--red)">38°C</div>
              <div class="sensor-lbl">Temperature</div>
            </div>
            <div class="sensor-card">
              <div style="font-size:22px">💧</div>
              <div class="sensor-val" style="color:var(--blue)">45%</div>
              <div class="sensor-lbl">Humidity</div>
            </div>
            <div class="sensor-card">
              <div style="font-size:22px">⚖️</div>
              <div class="sensor-val" style="color:var(--green-main)">2.4kg</div>
              <div class="sensor-lbl">Weight</div>
            </div>
          </div>

          <div class="grid-2">
            <div class="card" style="text-align:center">
              <div class="card-title">Bin Fill Visualizer</div>
              <div class="bin-visual">
                <div class="bin-lid"></div>
                <div class="bin-body">
                  <div class="bin-fill" style="height:62%">
                    <div class="bin-pct-label">62%</div>
                  </div>
                </div>
              </div>
              <p style="font-size:12px; color:var(--amber); font-weight:600">⚠️ Collection recommended soon</p>
            </div>

            <div class="card">
              <div class="card-title">Bin Status</div>
              <div style="display:flex; flex-direction:column; gap:10px">
                <div style="display:flex; justify-content:space-between; font-size:13px">
                  <span style="color:var(--text-muted)">Bin ID</span>
                  <strong>SB-007</strong>
                </div>
                <div style="display:flex; justify-content:space-between; font-size:13px">
                  <span style="color:var(--text-muted)">Location</span>
                  <strong>Sector 14, Gate 2</strong>
                </div>
                <div style="display:flex; justify-content:space-between; font-size:13px">
                  <span style="color:var(--text-muted)">Last Emptied</span>
                  <strong>Today, 08:30 AM</strong>
                </div>
                <div style="display:flex; justify-content:space-between; font-size:13px">
                  <span style="color:var(--text-muted)">Connectivity</span>
                  <span class="badge badge-green">Online</span>
                </div>
                <div style="display:flex; justify-content:space-between; font-size:13px">
                  <span style="color:var(--text-muted)">Battery</span>
                  <strong style="color:var(--green-main)">87%</strong>
                </div>
                <div style="display:flex; justify-content:space-between; font-size:13px">
                  <span style="color:var(--text-muted)">Alert Status</span>
                  <span class="badge badge-amber">Moderate</span>
                </div>
              </div>
            </div>
          </div>

          <div class="card" style="margin-top:16px">
            <div class="card-title">Bin Actions</div>
            <div style="display:flex; gap:10px; flex-wrap:wrap">
              <button class="btn btn-primary btn-sm" onclick="showToast('📤 Collection request sent!')">
                <i class="fas fa-truck"></i> Request Collection
              </button>
              <button class="btn btn-outline btn-sm" onclick="showToast('🔄 Sensor data refreshed!')">
                <i class="fas fa-sync"></i> Refresh Sensors
              </button>
              <button class="btn btn-outline btn-sm" onclick="showToast('📊 Report generated!')">
                <i class="fas fa-file-alt"></i> View Report
              </button>
            </div>
          </div>
        </section>

        <!-- ===== LEADERBOARD ===== -->
        <section class="section" id="sec-leaderboard">
          <div class="page-header">
            <div class="page-title">Leaderboard</div>
            <div class="page-sub">Top recyclers in your city this month</div>
          </div>

          <div class="card" style="margin-bottom:20px">
            <div class="card-title">🏆 Top 3 Champions</div>
            <div class="podium">
              <div class="podium-block p-2">
                <div class="podium-name">Priya S.</div>
                <div class="podium-pts">3,820 PC</div>
                <div class="podium-avatar">P</div>
                <div class="podium-platform"><div class="podium-rank">🥈 #2</div></div>
              </div>
              <div class="podium-block p-1">
                <div class="podium-name">Rahul K.</div>
                <div class="podium-pts">5,210 PC</div>
                <div class="podium-avatar">R</div>
                <div class="podium-platform"><div class="podium-rank">🥇 #1</div></div>
              </div>
              <div class="podium-block p-3">
                <div class="podium-name">Sneha M.</div>
                <div class="podium-pts">2,990 PC</div>
                <div class="podium-avatar">S</div>
                <div class="podium-platform"><div class="podium-rank">🥉 #3</div></div>
              </div>
            </div>
          </div>

          <div class="card">
            <div class="card-title">Full Rankings</div>
            <table class="lb-table">
              <thead>
                <tr>
                  <th>Rank</th>
                  <th>User</th>
                  <th>Items</th>
                  <th>Credits</th>
                </tr>
              </thead>
              <tbody>
                <tr><td class="lb-rank">1</td><td><div class="lb-user"><div class="lb-avatar" style="background:#fef3c7;color:#92400e">R</div>Rahul K.</div></td><td>260</td><td class="lb-pts">5,210</td></tr>
                <tr><td class="lb-rank">2</td><td><div class="lb-user"><div class="lb-avatar" style="background:#dbeafe;color:#1e40af">P</div>Priya S.</div></td><td>191</td><td class="lb-pts">3,820</td></tr>
                <tr><td class="lb-rank">3</td><td><div class="lb-user"><div class="lb-avatar" style="background:#ede9fe;color:#6d28d9">S</div>Sneha M.</div></td><td>149</td><td class="lb-pts">2,990</td></tr>
                <tr><td class="lb-rank">4</td><td><div class="lb-user"><div class="lb-avatar" style="background:#fce7f3;color:#9d174d">A</div>Amit V.</div></td><td>138</td><td class="lb-pts">2,760</td></tr>
                <tr><td class="lb-rank">5</td><td><div class="lb-user"><div class="lb-avatar" style="background:#d1fae5;color:#065f46">K</div>Kavita R.</div></td><td>130</td><td class="lb-pts">2,600</td></tr>
                <tr><td class="lb-rank">6</td><td><div class="lb-user"><div class="lb-avatar" style="background:#fee2e2;color:#991b1b">N</div>Nikhil J.</div></td><td>122</td><td class="lb-pts">2,440</td></tr>
                <tr style="background:var(--green-pale)"><td class="lb-rank" style="color:var(--green-main)">7</td><td><div class="lb-user"><div class="lb-avatar">A</div><strong>Arjun (You)</strong></div></td><td><strong>142</strong></td><td class="lb-pts"><strong>2,840</strong></td></tr>
                <tr><td class="lb-rank">8</td><td><div class="lb-user"><div class="lb-avatar">M</div>Megha T.</div></td><td>118</td><td class="lb-pts">2,360</td></tr>
                <tr><td class="lb-rank">9</td><td><div class="lb-user"><div class="lb-avatar">V</div>Vikas B.</div></td><td>110</td><td class="lb-pts">2,200</td></tr>
                <tr><td class="lb-rank">10</td><td><div class="lb-user"><div class="lb-avatar">D</div>Deepa N.</div></td><td>104</td><td class="lb-pts">2,080</td></tr>
              </tbody>
            </table>
          </div>
        </section>

        <!-- ===== PROFILE ===== -->
        <section class="section" id="sec-profile">
          <div class="page-header">
            <div class="page-title">My Profile</div>
            <div class="page-sub">Manage your EcoTrack account</div>
          </div>

          <div class="profile-top">
            <div class="profile-avatar" id="profile-av">A</div>
            <div>
              <div class="profile-name" id="profile-name">Arjun Sharma</div>
              <div class="profile-email" id="profile-email">arjun@example.com</div>
              <span class="profile-badge">🌿 Eco Warrior</span>
            </div>
          </div>

          <div class="grid-2" style="margin-bottom:20px">
            <div class="card">
              <div class="profile-stats">
                <div><div class="pstat-val">142</div><div class="pstat-lbl">Recycled</div></div>
                <div><div class="pstat-val">2,840</div><div class="pstat-lbl">Credits</div></div>
                <div><div class="pstat-val">#7</div><div class="pstat-lbl">City Rank</div></div>
              </div>
            </div>
            <div class="card">
              <div class="card-title">Eco Level</div>
              <div style="margin-bottom:8px">
                <div style="display:flex; justify-content:space-between; font-size:12px; color:var(--text-muted); margin-bottom:4px">
                  <span>Eco Warrior</span><span>1,400 XP / 2,000 XP</span>
                </div>
                <div class="progress-bar-wrap"><div class="progress-bar" style="width:70%"></div></div>
              </div>
              <p style="font-size:12px; color:var(--text-muted)">600 XP more to reach <strong>Eco Champion</strong>!</p>
            </div>
          </div>

          <div class="card">
            <div class="card-title">Settings</div>
            <div class="setting-list">
              <div class="setting-item" onclick="showToast('✏️ Edit Profile – Coming soon')">
                <i class="fas fa-user-edit"></i><span>Edit Profile</span><i class="fas fa-chevron-right arrow"></i>
              </div>
              <div class="setting-item" onclick="showToast('🔔 Notifications – Coming soon')">
                <i class="fas fa-bell"></i><span>Notifications</span><i class="fas fa-chevron-right arrow"></i>
              </div>
              <div class="setting-item" onclick="showToast('🔒 Privacy – Coming soon')">
                <i class="fas fa-shield-alt"></i><span>Privacy &amp; Security</span><i class="fas fa-chevron-right arrow"></i>
              </div>
              <div class="setting-item" onclick="showToast('🌍 Language – Coming soon')">
                <i class="fas fa-globe"></i><span>Language</span><i class="fas fa-chevron-right arrow"></i>
              </div>
              <div class="setting-item" onclick="showToast('📊 Export Data – Coming soon')">
                <i class="fas fa-download"></i><span>Export My Data</span><i class="fas fa-chevron-right arrow"></i>
              </div>
              <div class="setting-item" onclick="doLogout()" style="color:var(--red)">
                <i class="fas fa-sign-out-alt" style="color:var(--red)"></i><span style="color:var(--red)">Logout</span><i class="fas fa-chevron-right arrow"></i>
              </div>
            </div>
          </div>
        </section>

        <!-- ===== CONTACT ===== -->
        <section class="section" id="sec-contact">
          <div class="page-header">
            <div class="page-title">Contact Us</div>
            <div class="page-sub">Get in touch with the EcoTrack team</div>
          </div>

          <div class="grid-2">
            <div class="card">
              <div class="card-title">Send a Message</div>
              <div class="contact-form">
                <div class="input-row">
                  <div class="form-field">
                    <label>Your Name</label>
                    <input type="text" id="ct-name" placeholder="Arjun Sharma" />
                  </div>
                  <div class="form-field">
                    <label>Email</label>
                    <input type="email" id="ct-email" placeholder="you@example.com" />
                  </div>
                </div>
                <div class="form-field">
                  <label>Subject</label>
                  <select id="ct-subject">
                    <option>General Inquiry</option>
                    <option>Report a Dustbin Issue</option>
                    <option>Credits/Rewards Problem</option>
                    <option>App Bug Report</option>
                    <option>Partnership</option>
                  </select>
                </div>
                <div class="form-field">
                  <label>Message</label>
                  <textarea id="ct-msg" placeholder="Describe your query or issue in detail…"></textarea>
                </div>
                <button class="btn btn-primary" onclick="sendContact()">
                  <i class="fas fa-paper-plane"></i> Send Message
                </button>
              </div>
            </div>

            <div style="display:flex; flex-direction:column; gap:16px">
              <div class="card">
                <div class="card-title">Contact Information</div>
                <div class="contact-info-list">
                  <div class="ci-item"><i class="fas fa-envelope"></i><span>support@ecotrack.in</span></div>
                  <div class="ci-item"><i class="fas fa-phone"></i><span>+91 98765 43210</span></div>
                  <div class="ci-item"><i class="fas fa-map-marker-alt"></i><span>Jaipur, Rajasthan, India</span></div>
                  <div class="ci-item"><i class="fas fa-clock"></i><span>Mon–Fri, 9 AM – 6 PM IST</span></div>
                </div>
              </div>
              <div class="card">
                <div class="card-title">🌱 Our Mission</div>
                <p style="font-size:13px; color:var(--text-mid); line-height:1.6">EcoTrack empowers citizens to actively participate in plastic waste reduction through technology, incentives, and community action. Together we can make our cities plastic-free.</p>
              </div>
              <div class="card" style="background:var(--green-pale); border-color:var(--green-light)">
                <div style="font-size:13px; color:var(--green-dark); font-weight:600; margin-bottom:4px">🌍 Did You Know?</div>
                <p style="font-size:12px; color:var(--green-dark); line-height:1.5">India generates ~3.5 million tonnes of plastic waste per year. EcoTrack users have collectively recycled over <strong>12 tonnes</strong> this year!</p>
              </div>
            </div>
          </div>
        </section>

      </main><!-- end .main-content -->
    </div><!-- end .app-body -->

    <!-- BOTTOM NAV (mobile only) -->
    <nav class="bottom-nav" id="bottom-nav">
      <div class="bn-item active" id="bn-home"    onclick="showSection('home')">        <i class="fas fa-home"></i>Home</div>
      <div class="bn-item"        id="bn-dashboard" onclick="showSection('dashboard')"> <i class="fas fa-chart-bar"></i>Stats</div>
      <div class="bn-item"        id="bn-scan"    onclick="showSection('scan')">        <i class="fas fa-camera"></i>Scan</div>
      <div class="bn-item"        id="bn-rewards" onclick="showSection('rewards')">     <i class="fas fa-gift"></i>Rewards</div>
      <div class="bn-item"        id="bn-profile" onclick="showSection('profile')">     <i class="fas fa-user"></i>Profile</div>
    </nav>

  </div><!-- end #app -->

  <!-- =========================================
       ✅ FIX #5: CAMERA MODAL – full screen
  ========================================= -->
  <div id="camera-modal">
    <video id="camera-video" autoplay playsinline muted></video>
    <div id="cam-error">
      <i class="fas fa-exclamation-triangle" style="font-size:32px; margin-bottom:12px; display:block; color:#ef4444"></i>
      Camera access denied or not available.<br>Please allow camera permission and try again.
    </div>
    <div class="camera-overlay">
      <div class="camera-top">
        <div class="camera-title"><i class="fas fa-recycle" style="margin-right:6px; color:var(--green-mid)"></i>EcoTrack Scanner</div>
        <button class="btn-close-cam" onclick="closeCamera()" aria-label="Close Camera">
          <i class="fas fa-times"></i>
        </button>
      </div>
      <div class="scan-frame">
        <div class="scan-line"></div>
        <div class="corner-bl"></div>
        <div class="corner-br"></div>
      </div>
      <div class="camera-bottom">
        <div class="camera-hint">Align plastic item within the frame</div>
        <button class="btn-capture" onclick="captureItem()" aria-label="Scan item">
          <i class="fas fa-recycle"></i>
        </button>
        <button class="btn btn-danger btn-sm" onclick="closeCamera()">
          <i class="fas fa-times"></i> Close Camera
        </button>
      </div>
    </div>
  </div>

  <!-- TOAST -->
  <div id="toast"></div>

  <!-- =========================================
       JAVASCRIPT
  ========================================= -->
  <script>
    /* ============================================
       ✅ SECTION NAVIGATION – FIX #1, #2, #3
    ============================================ */
    /**
     * showSection(id) – hides all sections, shows only the selected one.
     * Also updates sidebar nav, bottom nav, and closes mobile drawer.
     */
    function showSection(id) {
      // 1. Hide ALL sections
      document.querySelectorAll('.section').forEach(sec => {
        sec.classList.remove('active-section');
      });

      // 2. Remove active from sidebar nav items
      document.querySelectorAll('.nav-item').forEach(item => {
        item.classList.remove('active');
      });

      // 3. Remove active from bottom nav items
      document.querySelectorAll('.bn-item').forEach(item => {
        item.classList.remove('active');
      });

      // 4. Show SELECTED section
      const target = document.getElementById('sec-' + id);
      if (target) target.classList.add('active-section');

      // 5. Highlight sidebar nav item
      const navEl = document.getElementById('nav-' + id);
      if (navEl) navEl.classList.add('active');

      // 6. Highlight bottom nav if applicable
      const bnEl = document.getElementById('bn-' + id);
      if (bnEl) bnEl.classList.add('active');

      // 7. Scroll main content to top
      document.getElementById('main-content').scrollTop = 0;

      // 8. Close mobile sidebar
      closeSidebar();
    }

    // ✅ Default section = Home on page load
    document.addEventListener('DOMContentLoaded', () => {
      showSection('home');
    });

    /* ============================================
       SIDEBAR (MOBILE DRAWER)
    ============================================ */
    function toggleSidebar() {
      document.getElementById('sidebar').classList.toggle('open');
      document.getElementById('sidebar-overlay').classList.toggle('open');
    }
    function closeSidebar() {
      document.getElementById('sidebar').classList.remove('open');
      document.getElementById('sidebar-overlay').classList.remove('open');
    }

    /* ============================================
       AUTH SYSTEM – LOGIN / SIGNUP
    ============================================ */
    function switchAuthTab(tab) {
      document.getElementById('tab-login').classList.toggle('active', tab === 'login');
      document.getElementById('tab-signup').classList.toggle('active', tab === 'signup');
      document.getElementById('login-form').style.display  = tab === 'login'  ? 'block' : 'none';
      document.getElementById('signup-form').style.display = tab === 'signup' ? 'block' : 'none';
    }

    function showError(id, show) {
      document.getElementById(id).classList.toggle('show', show);
    }

    function doLogin() {
      const email = document.getElementById('login-email').value.trim();
      const pass  = document.getElementById('login-pass').value;
      let valid = true;

      if (!email || !email.includes('@')) { showError('login-email-err', true); valid = false; }
      else { showError('login-email-err', false); }

      if (pass.length < 6) { showError('login-pass-err', true); valid = false; }
      else { showError('login-pass-err', false); }

      if (!valid) return;

      // Extract username from email
      const uname = email.split('@')[0];
      const initials = uname.charAt(0).toUpperCase();
      setUserInfo(uname.charAt(0).toUpperCase() + uname.slice(1), email, initials);
      launchApp();
    }

    function doSignup() {
      const name  = document.getElementById('signup-name').value.trim();
      const email = document.getElementById('signup-email').value.trim();
      const pass  = document.getElementById('signup-pass').value;
      let valid = true;

      if (!name) { showError('signup-name-err', true); valid = false; }
      else { showError('signup-name-err', false); }

      if (!email || !email.includes('@')) { showError('signup-email-err', true); valid = false; }
      else { showError('signup-email-err', false); }

      if (pass.length < 6) { showError('signup-pass-err', true); valid = false; }
      else { showError('signup-pass-err', false); }

      if (!valid) return;

      const initials = name.charAt(0).toUpperCase();
      setUserInfo(name, email, initials);
      launchApp();
    }

    function setUserInfo(name, email, initials) {
      document.getElementById('profile-name').textContent  = name;
      document.getElementById('profile-email').textContent = email;
      document.getElementById('profile-av').textContent    = initials;
      document.getElementById('user-avatar').textContent   = initials;
    }

    function launchApp() {
      document.getElementById('auth-screen').style.display = 'none';
      const app = document.getElementById('app');
      app.classList.add('visible');
      showSection('home');
    }

    function doLogout() {
      document.getElementById('app').classList.remove('visible');
      document.getElementById('auth-screen').style.display = 'flex';
      // Clear inputs
      ['login-email','login-pass'].forEach(id => document.getElementById(id).value = '');
    }

    /* ============================================
       ✅ CAMERA – FIX #5: Full screen modal
    ============================================ */
    let cameraStream = null;

    async function openCamera() {
      const modal = document.getElementById('camera-modal');
      const video = document.getElementById('camera-video');
      const errEl = document.getElementById('cam-error');
      errEl.style.display = 'none';
      video.style.display = 'block';
      modal.classList.add('open');

      try {
        cameraStream = await navigator.mediaDevices.getUserMedia({
          video: { facingMode: { ideal: 'environment' }, width: { ideal: 1920 }, height: { ideal: 1080 } },
          audio: false
        });
        video.srcObject = cameraStream;
      } catch (err) {
        // Camera not available / permission denied
        video.style.display = 'none';
        errEl.style.display = 'block';
        console.warn('Camera error:', err);
      }
    }

    function closeCamera() {
      // Stop all camera tracks
      if (cameraStream) {
        cameraStream.getTracks().forEach(track => track.stop());
        cameraStream = null;
      }
      const video = document.getElementById('camera-video');
      video.srcObject = null;
      document.getElementById('camera-modal').classList.remove('open');
    }

    function captureItem() {
      closeCamera();
      showToast('✅ Item scanned! +40 Plastic Credits earned 🎉');
    }

    /* ============================================
       SCAN SECTION – type selector
    ============================================ */
    function selectScanType(el) {
      document.querySelectorAll('.scan-type').forEach(t => t.classList.remove('selected'));
      el.classList.add('selected');
    }

    function logManual() {
      showToast('✅ Plastic logged successfully! Credits added 🌿');
    }

    /* ============================================
       REWARDS
    ============================================ */
    function redeemReward(el, cost) {
      const credits = 2840;
      if (cost > credits) {
        showToast('❌ Not enough Plastic Credits!');
        return;
      }
      const name = el.querySelector('h4').textContent;
      showToast('🎁 ' + name + ' redeemed for ' + cost + ' PC!');
    }

    /* ============================================
       CONTACT FORM
    ============================================ */
    function sendContact() {
      const name = document.getElementById('ct-name').value.trim();
      const email = document.getElementById('ct-email').value.trim();
      const msg = document.getElementById('ct-msg').value.trim();
      if (!name || !email || !msg) {
        showToast('⚠️ Please fill in all required fields');
        return;
      }
      showToast('✉️ Message sent! We\'ll reply within 24 hours.');
      document.getElementById('ct-name').value = '';
      document.getElementById('ct-email').value = '';
      document.getElementById('ct-msg').value = '';
    }

    /* ============================================
       TOAST NOTIFICATION
    ============================================ */
    let toastTimer = null;
    function showToast(msg) {
      const t = document.getElementById('toast');
      t.textContent = msg;
      t.classList.add('show');
      if (toastTimer) clearTimeout(toastTimer);
      toastTimer = setTimeout(() => t.classList.remove('show'), 3000);
    }

    /* ============================================
       KEYBOARD – close camera on Escape
    ============================================ */
    document.addEventListener('keydown', e => {
      if (e.key === 'Escape') closeCamera();
    });
  </script>

</body>
</html>
