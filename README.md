[prenatal-phoenix (1).html](https://github.com/user-attachments/files/29270612/prenatal-phoenix.1.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Access to Prenatal Care in the Phoenix Metropolitan Area</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css" />
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600;9..144,700&family=DM+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --indigo:#2c2a4a;        /* dusk sky / primary text */
    --indigo-soft:#4a4368;
    --turquoise:#1f9e92;     /* interactive accent */
    --turquoise-dk:#157a70;
    --saguaro:#5b7f4d;       /* cactus green */
    --coral:#df6c4f;         /* sunset clay */
    --coral-dk:#c6553a;
    --gold:#e9a23b;          /* desert sun */
    --sand:#fbf1e0;          /* page background */
    --sand-2:#f5e6cf;
    --card:#fffaf1;
    --line:#e6d4ba;
    --ink-2:#6b6076;
    --danger:#b23a2e;
    --shadow:0 1px 2px rgba(44,42,74,.06),0 8px 24px rgba(44,42,74,.08);
    --radius:16px;
  }
  *{box-sizing:border-box}
  html{scroll-behavior:smooth}
  body{
    margin:0;background:var(--sand);color:var(--indigo);
    font-family:"DM Sans",system-ui,-apple-system,Segoe UI,Roboto,sans-serif;
    line-height:1.55;-webkit-font-smoothing:antialiased;
  }
  h1,h2,h3,h4{font-family:"Fraunces",Georgia,serif;font-weight:600;line-height:1.12;margin:0}
  a{color:var(--turquoise-dk);text-decoration:none}
  a:hover{text-decoration:underline}
  .wrap{max-width:1120px;margin:0 auto;padding:0 20px}

  /* ---------- Top bar ---------- */
  header.top{
    position:sticky;top:0;z-index:1200;background:rgba(251,241,224,.92);
    backdrop-filter:blur(8px);border-bottom:1px solid var(--line);
  }
  .top-inner{display:flex;align-items:center;justify-content:space-between;gap:16px;height:62px}
  .brand{display:flex;align-items:center;gap:10px;font-family:"Fraunces";font-weight:600;font-size:1.02rem;color:var(--indigo)}
  .brand svg{flex:none}
  .lang{display:inline-flex;border:1.5px solid var(--turquoise);border-radius:999px;overflow:hidden;font-weight:600;font-size:.85rem}
  .lang button{border:0;background:transparent;color:var(--turquoise-dk);padding:7px 16px;cursor:pointer;font-family:inherit;font-weight:600}
  .lang button.active{background:var(--turquoise);color:#fff}

  /* ---------- Hero ---------- */
  .hero{position:relative;overflow:hidden;border-bottom:1px solid var(--line)}
  .hero-sky{position:absolute;inset:0;width:100%;height:100%;display:block}
  .hero-inner{position:relative;z-index:2;padding:54px 0 230px}
  .eyebrow{display:inline-block;font-size:.74rem;letter-spacing:.18em;text-transform:uppercase;font-weight:700;
    color:#fff;background:rgba(44,42,74,.34);border:1px solid rgba(255,255,255,.35);padding:6px 12px;border-radius:999px;backdrop-filter:blur(2px)}
  .hero h1{color:#fff;font-size:clamp(2.1rem,5.4vw,3.5rem);margin:18px 0 12px;max-width:14ch;text-shadow:0 2px 18px rgba(44,42,74,.35)}
  .hero p.lede{color:#fff;font-size:clamp(1rem,2.2vw,1.18rem);max-width:46ch;margin:0;text-shadow:0 1px 12px rgba(44,42,74,.45)}
  @keyframes sunGlow{0%,100%{opacity:.85;transform:scale(1)}50%{opacity:1;transform:scale(1.03)}}
  .sun{transform-origin:center;animation:sunGlow 7s ease-in-out infinite}
  @media (prefers-reduced-motion:reduce){.sun{animation:none}}

  /* ---------- Tabs ---------- */
  nav.tabs{position:sticky;top:62px;z-index:1100;background:var(--sand);border-bottom:1px solid var(--line)}
  .tabs-inner{display:flex;gap:6px;overflow-x:auto;padding:10px 0}
  .tab{flex:none;display:flex;align-items:center;gap:9px;border:1px solid var(--line);background:var(--card);
    color:var(--indigo);padding:11px 18px;border-radius:999px;cursor:pointer;font-family:"DM Sans";font-weight:600;font-size:.96rem}
  .tab:hover{border-color:var(--turquoise)}
  .tab.active{background:var(--indigo);color:#fff;border-color:var(--indigo)}
  .tab.active svg [stroke]{stroke:#fff}
  .tab.active svg [fill]:not([fill="none"]){fill:#fff}

  main{padding:34px 0 60px}
  section.panel{display:none}
  section.panel.active{display:block;animation:fade .35s ease}
  @keyframes fade{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}

  .section-head{display:flex;align-items:flex-end;gap:16px;flex-wrap:wrap;margin-bottom:6px}
  .section-head h2{font-size:clamp(1.6rem,3.6vw,2.3rem)}
  .count-pill{font-size:.8rem;font-weight:700;color:var(--turquoise-dk);background:#e3f3f0;border:1px solid #bfe4de;padding:4px 11px;border-radius:999px}
  .section-sub{color:var(--ink-2);max-width:62ch;margin:6px 0 22px}

  /* horizon divider (signature) */
  .horizon{height:30px;margin:30px 0;background-repeat:repeat-x;background-position:bottom;background-size:auto 100%;opacity:.9}

  /* ---------- Neighborhood pills ---------- */
  .hoods{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:20px}
  .hood{border:1px solid var(--line);background:var(--card);color:var(--indigo-soft);
    padding:8px 15px;border-radius:999px;cursor:pointer;font-weight:600;font-size:.9rem;font-family:inherit}
  .hood:hover{border-color:var(--coral)}
  .hood.active{background:var(--coral);color:#fff;border-color:var(--coral)}
  .hood .n{opacity:.7;font-weight:600}
  .hood.active .n{opacity:.9}

  /* ---------- Cards ---------- */
  .grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(290px,1fr));gap:16px}
  .card{background:var(--card);border:1px solid var(--line);border-radius:var(--radius);padding:18px 18px 16px;box-shadow:var(--shadow);position:relative}
  .card .hoodtag{font-size:.72rem;letter-spacing:.06em;text-transform:uppercase;font-weight:700;color:var(--saguaro)}
  .card h3{font-size:1.12rem;margin:5px 0 8px;line-height:1.2}
  .card .addr{color:var(--ink-2);font-size:.9rem;margin:0 0 12px;display:flex;gap:7px}
  .card .addr svg{flex:none;margin-top:3px}
  .card-actions{display:flex;flex-wrap:wrap;gap:8px;margin-top:4px}
  .btn{display:inline-flex;align-items:center;gap:6px;font-size:.85rem;font-weight:600;padding:8px 13px;border-radius:10px;border:1px solid transparent;cursor:pointer;font-family:inherit}
  .btn-map{background:var(--turquoise);color:#fff}
  .btn-map:hover{background:var(--turquoise-dk);text-decoration:none}
  .btn-call{background:#fff;border-color:var(--line);color:var(--indigo)}
  .btn-call:hover{border-color:var(--turquoise);text-decoration:none}
  .badge{position:absolute;top:14px;right:14px;font-size:.66rem;font-weight:700;letter-spacing:.04em;text-transform:uppercase;padding:4px 9px;border-radius:999px}
  .badge-conf{background:#fbe9e3;color:var(--coral-dk);border:1px solid #f3cabb}
  .badge-preg{background:#fdf0d8;color:#a9742a;border:1px solid #f0d9a8}
  .badge-fqhc{background:#e6f1de;color:#4d6b3c;border:1px solid #cbe0bb}
  .card .note{font-size:.82rem;color:var(--ink-2);margin:10px 0 2px;padding-top:10px;border-top:1px dashed var(--line)}

  /* ---------- Map ---------- */
  .map-card{margin-top:26px;border:1px solid var(--line);border-radius:var(--radius);overflow:hidden;box-shadow:var(--shadow);background:var(--card)}
  .map-head{display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap;padding:14px 18px;border-bottom:1px solid var(--line)}
  .map-head h3{font-size:1.15rem}
  .map-legend{display:flex;gap:14px;flex-wrap:wrap;font-size:.82rem;color:var(--ink-2)}
  .map-legend span{display:inline-flex;align-items:center;gap:6px}
  .dot{width:12px;height:12px;border-radius:50%;display:inline-block;border:2px solid #fff;box-shadow:0 0 0 1px rgba(0,0,0,.15)}
  .leaflet-container{height:460px;width:100%;background:#dfe9e3;font-family:inherit}
  .leaflet-popup-content{margin:12px 14px;font-family:"DM Sans"}
  .pin-name{font-weight:700;font-size:.98rem;color:var(--indigo);font-family:"Fraunces"}
  .pin-addr{color:var(--ink-2);font-size:.84rem;margin:3px 0 8px}
  .pin-link{font-weight:600;font-size:.85rem}

  /* ---------- Disclaimer ---------- */
  .disclaimer{display:flex;gap:12px;background:#fff7e9;border:1px solid #f0dcb4;border-radius:var(--radius);padding:14px 16px;margin-bottom:24px;font-size:.88rem;color:#7a5b22}
  .disclaimer svg{flex:none;margin-top:2px}

  /* ---------- Emergency strip (resources) ---------- */
  .emergency{background:linear-gradient(135deg,#3a2330,#5a2a2a);border-radius:20px;padding:22px;color:#fff;margin-bottom:30px;box-shadow:var(--shadow)}
  .emergency h2{color:#fff;font-size:1.5rem;display:flex;align-items:center;gap:10px}
  .emergency .e-sub{color:#f3d8cf;margin:6px 0 16px;font-size:.92rem}
  .e-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px}
  .e-item{background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.16);border-radius:13px;padding:13px 15px}
  .e-item .lbl{font-size:.78rem;letter-spacing:.05em;text-transform:uppercase;color:#f0c9bd;font-weight:700}
  .e-item .num{font-family:"Fraunces";font-size:1.45rem;font-weight:600;color:#fff;display:block;margin:3px 0 2px}
  .e-item .num a{color:#fff}
  .e-item small{color:#e9cabf;font-size:.78rem}

  /* ---------- Need chooser ---------- */
  .chooser{background:var(--card);border:1px solid var(--line);border-radius:20px;padding:22px;margin-bottom:30px;box-shadow:var(--shadow)}
  .chooser h2{font-size:1.5rem;margin-bottom:4px}
  .chooser p{color:var(--ink-2);margin:0 0 16px;font-size:.92rem}
  .chips{display:flex;flex-wrap:wrap;gap:10px}
  .chip{display:flex;align-items:center;gap:9px;background:var(--sand);border:1px solid var(--line);border-radius:13px;
    padding:12px 15px;cursor:pointer;font-weight:600;font-size:.92rem;color:var(--indigo);text-align:left;font-family:inherit}
  .chip:hover{border-color:var(--turquoise);background:#fff}
  .chip .ic{width:30px;height:30px;border-radius:9px;display:grid;place-items:center;flex:none;color:#fff}

  /* ---------- Resource cards ---------- */
  .res-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(330px,1fr));gap:18px}
  .res{background:var(--card);border:1px solid var(--line);border-radius:var(--radius);padding:20px;box-shadow:var(--shadow);scroll-margin-top:140px;transition:box-shadow .3s,border-color .3s}
  .res.flash{border-color:var(--gold);box-shadow:0 0 0 3px rgba(233,162,59,.35),var(--shadow)}
  .res .rh{display:flex;align-items:center;gap:11px;margin-bottom:10px}
  .res .ric{width:38px;height:38px;border-radius:11px;display:grid;place-items:center;flex:none;color:#fff}
  .res h3{font-size:1.18rem}
  .res p{font-size:.92rem;color:#4b4357;margin:0 0 10px}
  .res ul{margin:0;padding-left:0;list-style:none}
  .res li{font-size:.9rem;padding:7px 0;border-top:1px solid var(--line);display:flex;justify-content:space-between;gap:10px;align-items:baseline}
  .res li:first-child{border-top:0}
  .res li .k{color:var(--indigo);font-weight:600}
  .res li .v{color:var(--turquoise-dk);font-weight:600;white-space:nowrap;text-align:right}
  .res li .v.plain{color:var(--ink-2);font-weight:500}

  /* ---------- Accordion (trimester) ---------- */
  .road{background:var(--card);border:1px solid var(--line);border-radius:var(--radius);box-shadow:var(--shadow);overflow:hidden;margin-top:24px}
  .road-head{padding:18px 20px;border-bottom:1px solid var(--line)}
  .road-head h3{font-size:1.3rem}
  .road-head p{color:var(--ink-2);font-size:.9rem;margin:4px 0 0}
  .acc{border-top:1px solid var(--line)}
  .acc:first-of-type{border-top:0}
  .acc-btn{width:100%;display:flex;align-items:center;gap:14px;background:transparent;border:0;padding:16px 20px;cursor:pointer;font-family:inherit;text-align:left}
  .acc-btn:hover{background:var(--sand)}
  .acc-num{width:34px;height:34px;border-radius:50%;flex:none;display:grid;place-items:center;font-family:"Fraunces";font-weight:700;color:#fff;font-size:.95rem}
  .acc-btn .at{font-family:"Fraunces";font-weight:600;font-size:1.08rem;flex:1}
  .acc-btn .ax{font-size:1.3rem;color:var(--ink-2);transition:transform .25s}
  .acc.open .ax{transform:rotate(45deg)}
  .acc-body{max-height:0;overflow:hidden;transition:max-height .3s ease}
  .acc-body .inner{padding:0 20px 18px 68px;color:#4b4357;font-size:.92rem}
  .acc-body li{margin:6px 0}

  footer{border-top:1px solid var(--line);background:var(--sand-2);padding:30px 0;font-size:.84rem;color:var(--ink-2)}
  footer .wrap>p{margin:6px 0}
  footer strong{color:var(--indigo)}

  .hidden{display:none!important}
  @media (max-width:560px){
    .hero-inner{padding:40px 0 180px}
    .leaflet-container{height:380px}
    .e-grid{grid-template-columns:1fr}
  }
</style>
</head>
<body>

<!-- ============ TOP BAR ============ -->
<header class="top">
  <div class="wrap top-inner">
    <div class="brand">
      <svg width="26" height="26" viewBox="0 0 24 24" fill="none" aria-hidden="true">
        <path d="M12 21s-7-4.5-7-10a7 7 0 0 1 14 0c0 5.5-7 10-7 10Z" fill="#df6c4f"/>
        <circle cx="12" cy="11" r="3.1" fill="#fffaf1"/>
      </svg>
      <span data-i18n="brand">Prenatal Care • Phoenix Metro</span>
    </div>
    <div class="lang" role="group" aria-label="Language">
      <button id="btn-en" class="active" onclick="setLang('en')">EN</button>
      <button id="btn-es" onclick="setLang('es')">ES</button>
    </div>
  </div>
</header>

<!-- ============ HERO ============ -->
<div class="hero">
  <svg class="hero-sky" viewBox="0 0 1200 520" preserveAspectRatio="xMidYMid slice" aria-hidden="true">
    <defs>
      <linearGradient id="sky" x1="0" y1="0" x2="0" y2="1">
        <stop offset="0%" stop-color="#3b3566"/>
        <stop offset="42%" stop-color="#7d4f74"/>
        <stop offset="70%" stop-color="#df6c4f"/>
        <stop offset="100%" stop-color="#e9a23b"/>
      </linearGradient>
      <radialGradient id="sunG" cx="50%" cy="50%" r="50%">
        <stop offset="0%" stop-color="#ffe9b0"/>
        <stop offset="60%" stop-color="#f6b24a"/>
        <stop offset="100%" stop-color="#f6b24a" stop-opacity="0"/>
      </radialGradient>
    </defs>
    <rect width="1200" height="520" fill="url(#sky)"/>
    <circle class="sun" cx="870" cy="300" r="120" fill="url(#sunG)"/>
    <circle cx="870" cy="300" r="62" fill="#ffdf91"/>
    <!-- distant ridge -->
    <path d="M0 360 L180 320 L360 350 L560 312 L780 348 L1000 320 L1200 352 V520 H0 Z" fill="#8a4f5f" opacity=".55"/>
    <!-- mid ground -->
    <path d="M0 410 L220 380 L470 408 L720 378 L980 406 L1200 384 V520 H0 Z" fill="#6e3b46" opacity=".75"/>
    <!-- foreground with saguaros -->
    <g fill="#3a2233">
      <path d="M0 470 L1200 470 V520 H0 Z"/>
      <!-- saguaro 1 -->
      <g transform="translate(120,470)">
        <path d="M-9 0 V-118 a9 9 0 0 1 18 0 V0 Z"/>
        <path d="M-9 -78 q-26 0 -26 26 v14 a8 8 0 0 0 16 0 v-12 q0-12 10-12 Z"/>
        <path d="M9 -92 q26 0 26 26 v22 a8 8 0 0 1 -16 0 v-20 q0-12 -10-12 Z"/>
      </g>
      <!-- saguaro 2 small -->
      <g transform="translate(300,470) scale(.7)">
        <path d="M-9 0 V-110 a9 9 0 0 1 18 0 V0 Z"/>
        <path d="M9 -70 q24 0 24 24 v18 a8 8 0 0 1 -15 0 v-16 q0-11 -9-11 Z"/>
      </g>
      <!-- saguaro 3 -->
      <g transform="translate(1040,470) scale(1.15)">
        <path d="M-9 0 V-120 a9 9 0 0 1 18 0 V0 Z"/>
        <path d="M-9 -84 q-26 0 -26 26 v16 a8 8 0 0 0 16 0 v-14 q0-12 10-12 Z"/>
        <path d="M9 -64 q22 0 22 22 v12 a8 8 0 0 1 -15 0 v-10 q0-10 -7-10 Z"/>
      </g>
      <!-- prickly pear clumps -->
      <g transform="translate(600,470)"><ellipse cx="0" cy="-22" rx="15" ry="20"/><ellipse cx="-18" cy="-34" rx="11" ry="15"/><ellipse cx="17" cy="-30" rx="10" ry="14"/></g>
      <g transform="translate(820,470)"><ellipse cx="0" cy="-16" rx="12" ry="16"/><ellipse cx="15" cy="-26" rx="9" ry="12"/></g>
    </g>
  </svg>
  <div class="wrap hero-inner">
    <span class="eyebrow" data-i18n="eyebrow">A guide for expecting families</span>
    <h1 data-i18n="heroTitle">Access to Prenatal Care in the Phoenix Metropolitan Area</h1>
    <p class="lede" data-i18n="heroLede">Find pregnancy clinics, safe shelter, and the support you need across the Valley — wherever you are, whatever your situation.</p>
  </div>
</div>

<!-- ============ TABS ============ -->
<nav class="tabs">
  <div class="wrap tabs-inner" role="tablist">
    <button class="tab active" data-tab="clinics" onclick="showTab('clinics')">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><path d="M12 7v10M7 12h10" stroke="#1f9e92" stroke-width="2.2" stroke-linecap="round"/><rect x="3.5" y="3.5" width="17" height="17" rx="4" stroke="#1f9e92" stroke-width="2"/></svg>
      <span data-i18n="tabClinics">Pregnancy Clinics</span>
    </button>
    <button class="tab" data-tab="shelters" onclick="showTab('shelters')">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><path d="M4 11 12 4l8 7" stroke="#df6c4f" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/><path d="M6 10v9h12v-9" stroke="#df6c4f" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
      <span data-i18n="tabShelters">Women's Shelters</span>
    </button>
    <button class="tab" data-tab="resources" onclick="showTab('resources')">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none"><path d="M12 21s-7-4.2-7-9.5A7 7 0 0 1 12 4a7 7 0 0 1 7 7.5c0 5.3-7 9.5-7 9.5Z" stroke="#e9a23b" stroke-width="2" stroke-linejoin="round"/><circle cx="12" cy="11" r="2.4" fill="#e9a23b"/></svg>
      <span data-i18n="tabResources">Resources &amp; Support</span>
    </button>
  </div>
</nav>

<main class="wrap">

  <!-- ============ CLINICS ============ -->
  <section id="clinics" class="panel active">
    <div class="section-head">
      <h2 data-i18n="clinicsHead">Pregnancy Clinics</h2>
      <span class="count-pill" id="clinicCount"></span>
    </div>
    <p class="section-sub" data-i18n="clinicsSub">OB-GYN practices, perinatal specialists, and community health centers across the Valley. Choose a neighborhood, then find each location on the map below.</p>

    <div class="disclaimer">
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none"><path d="M12 9v4M12 17h.01" stroke="#b8860b" stroke-width="2" stroke-linecap="round"/><path d="M10.3 3.9 2.5 18a2 2 0 0 0 1.7 3h15.6a2 2 0 0 0 1.7-3L13.7 3.9a2 2 0 0 0-3.4 0Z" stroke="#b8860b" stroke-width="1.8"/></svg>
      <span data-i18n="clinicsDisc">Always call ahead to confirm hours, accepted insurance, and whether they take new prenatal patients. Many centers offer sliding-scale fees and accept AHCCCS (Arizona Medicaid).</span>
    </div>

    <div class="hoods" id="clinicHoods"></div>
    <div class="grid" id="clinicGrid"></div>

    <div class="map-card">
      <div class="map-head">
        <h3 data-i18n="clinicMapTitle">Clinic locations</h3>
        <div class="map-legend"><span><i class="dot" style="background:#1f9e92"></i><span data-i18n="legClinic">Clinic / health center</span></span></div>
      </div>
      <div id="clinicMap" class="leaflet-container"></div>
    </div>
  </section>

  <!-- ============ SHELTERS ============ -->
  <section id="shelters" class="panel">
    <div class="section-head">
      <h2 data-i18n="sheltersHead">Women's Shelters &amp; Safe Housing</h2>
      <span class="count-pill" id="shelterCount"></span>
    </div>
    <p class="section-sub" data-i18n="sheltersSub">Emergency domestic-violence programs, family shelters, and transitional housing. For safety, most domestic-violence shelters keep their addresses private — you reach them by phone, and they arrange a safe place to go.</p>

    <div class="disclaimer" style="background:#fbece6;border-color:#f1c9b8;color:#8a3b26">
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none"><path d="M12 21s-7-4.5-7-10a7 7 0 0 1 14 0c0 5.5-7 10-7 10Z" stroke="#c6553a" stroke-width="1.8"/><path d="M12 8v4M12 15h.01" stroke="#c6553a" stroke-width="2" stroke-linecap="round"/></svg>
      <span data-i18n="sheltersDisc"><strong>In immediate danger, call 911.</strong> Not sure where to start? The Maricopa County shelter line at <a href="tel:14808903039">480-890-3039</a> screens for every domestic-violence shelter in the county. Spots fill quickly — keep calling, and ask to be placed on a list.</span>
    </div>

    <div class="hoods" id="shelterHoods"></div>
    <div class="grid" id="shelterGrid"></div>

    <div class="map-card">
      <div class="map-head">
        <h3 data-i18n="shelterMapTitle">Mapped: shelters with public locations</h3>
        <div class="map-legend">
          <span><i class="dot" style="background:#df6c4f"></i><span data-i18n="legShelter">Shelter / housing</span></span>
          <span><i class="dot" style="background:#e9a23b"></i><span data-i18n="legPreg">For pregnant women</span></span>
        </div>
      </div>
      <div id="shelterMap" class="leaflet-container"></div>
      <p style="margin:0;padding:12px 18px;font-size:.82rem;color:var(--ink-2)" data-i18n="shelterMapNote">Domestic-violence shelters are intentionally not pinned on the map. Call the intake numbers on the cards above — their locations are kept confidential to protect residents.</p>
    </div>
  </section>

  <!-- ============ RESOURCES ============ -->
  <section id="resources" class="panel">
    <div class="section-head">
      <h2 data-i18n="resHead">Resources &amp; Support</h2>
    </div>
    <p class="section-sub" data-i18n="resSub">Everything around getting care: how to pay for it, your rights, a month-by-month roadmap, food and supplies, and someone to talk to. Start with what you need right now.</p>

    <!-- emergency -->
    <div class="emergency">
      <h2><svg width="22" height="22" viewBox="0 0 24 24" fill="none"><circle cx="12" cy="12" r="9" stroke="#fff" stroke-width="2"/><path d="M12 7v6M12 16h.01" stroke="#fff" stroke-width="2.2" stroke-linecap="round"/></svg><span data-i18n="emTitle">If you need help now</span></h2>
      <p class="e-sub" data-i18n="emSub">These lines are free, confidential, and answered around the clock unless noted.</p>
      <div class="e-grid">
        <div class="e-item"><span class="lbl" data-i18n="emDangerL">Immediate danger</span><span class="num"><a href="tel:911">911</a></span><small data-i18n="emDangerS">Call or text. Tell them if you can't speak safely.</small></div>
        <div class="e-item"><span class="lbl" data-i18n="emDvL">Domestic violence</span><span class="num"><a href="tel:18007997233">1-800-799-7233</a></span><small data-i18n="emDvS">National hotline, 24/7. Text START to 88788.</small></div>
        <div class="e-item"><span class="lbl" data-i18n="emMhL">Emotional crisis</span><span class="num"><a href="tel:988">988</a></span><small data-i18n="emMhS">Suicide &amp; Crisis Lifeline. Call or text, 24/7.</small></div>
        <div class="e-item"><span class="lbl" data-i18n="emAnyL">Any resource, 24/7</span><span class="num"><a href="tel:18772118661">2-1-1</a></span><small data-i18n="emAnyS">Arizona 211 connects you to local help.</small></div>
      </div>
    </div>

    <!-- need chooser -->
    <div class="chooser">
      <h2 data-i18n="chTitle">What do you need right now?</h2>
      <p data-i18n="chSub">Tap one and we'll jump you to the right place.</p>
      <div class="chips" id="needChips"></div>
    </div>

    <div class="res-grid" id="resGrid"></div>

    <!-- trimester roadmap -->
    <div class="road">
      <div class="road-head">
        <h3 data-i18n="roadTitle">Your pregnancy roadmap</h3>
        <p data-i18n="roadSub">A simple month-by-month checklist. Tap a stage to open it.</p>
      </div>
      <div id="roadAcc"></div>
    </div>
  </section>

</main>

<footer>
  <div class="wrap">
    <p><strong data-i18n="footTitle">About this guide.</strong> <span data-i18n="footBody">This directory was compiled from public listings in June 2026 to help expecting families in the Phoenix metro area find care. Details change — please call ahead to confirm. This site offers information, not medical or legal advice.</span></p>
    <p data-i18n="footEmerg">In a medical emergency, call 911. An emergency room cannot turn you away when you are in active labor, regardless of your ability to pay or your immigration status.</p>
  </div>
</footer>

<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.js"></script>
<script>
/* =========================================================
   DATA
   ========================================================= */
const CLINIC_HOODS = [
  ["central","Downtown &amp; Central Phoenix","Centro de Phoenix"],
  ["north","North Phoenix","Norte de Phoenix"],
  ["south","South Phoenix","Sur de Phoenix"],
  ["west","West Phoenix / Maryvale","Oeste de Phoenix / Maryvale"],
  ["glendale","Glendale","Glendale"],
  ["scottsdale","Scottsdale","Scottsdale"],
  ["tempe","Tempe","Tempe"],
  ["mesa","Mesa","Mesa"],
  ["chandler","Chandler","Chandler"],
  ["gilbert","Gilbert","Gilbert"]
];

const CLINICS = [
  // Central
  ["Valley Perinatal Services – Phoenix","central","2620 N 3rd St #102, Phoenix, AZ 85004",33.4773884,-112.0697954,"4807566000",null],
  ["Central Phoenix Women's Health Care","central","1313 E Osborn Rd #250, Phoenix, AZ 85012",33.4872072,-112.0542347,"6022659161",null],
  ["Women's Care – Central Phoenix OBGYN","central","4747 N 7th St Ste 150, Phoenix, AZ 85014",33.5072433,-112.063752,"6022402401",null],
  ["Maricopa OB/GYN","central","1661 E Camelback Rd Unit 160, Phoenix, AZ 85016",33.506986,-112.0454946,"6022411671",null],
  ["Arizona Gynecology Consultants – Phoenix","central","1008 E McDowell Rd, Phoenix, AZ 85006",33.4659638,-112.0602947,"6023588588",null],
  ["Planned Parenthood – Central Phoenix","central","4751 N 15th St #3, Phoenix, AZ 85014",33.5071653,-112.0494212,"6022777526",null],
  ["A Woman's Clinic","central","2023 W Bethany Home Rd, Phoenix, AZ 85015",33.5238563,-112.1032241,"6024625559",null],
  // North
  ["Lotus Obstetrics &amp; Gynecology","north","3805 E Bell Rd #4800, Phoenix, AZ 85032",33.6400707,-112.0000357,"6029923162",null],
  ["Phoenix Women's Clinic","north","8326 N 7th St, Phoenix, AZ 85020",33.5594658,-112.0656668,"6023055100",null],
  ["Agave Postpartum Wellness","north","15433 N Tatum Blvd Suite 106, Phoenix, AZ 85032",33.6270905,-111.9774285,"6232088242",null],
  // South
  ["Mountain Park Women's Health – Baseline","south","303 E Baseline Rd, Phoenix, AZ 85042",33.3767753,-112.0700623,"6022437277","fqhc"],
  // West
  ["Life Choices Women's Clinic","west","3516 W McDowell Rd, Phoenix, AZ 85009",33.4661699,-112.1353283,"6023055100",null],
  ["Planned Parenthood – Desert Sky","west","2020 N 75th Ave #11, Phoenix, AZ 85035",33.4698882,-112.2231262,"6022777526",null],
  // Glendale
  ["North Valley Women's Care","glendale","6316 W Union Hills Dr Ste 100, Glendale, AZ 85308",33.6544031,-112.1974651,"6232331300",null],
  ["Glendale Obstetrics and Gynecology","glendale","5605 W Eugie Ave #102, Glendale, AZ 85304",33.6071081,-112.1814908,"6022988977",null],
  ["Valley Perinatal Services – Glendale","glendale","5605 W Eugie Ave #111, Glendale, AZ 85304",33.6070828,-112.1814994,"4807566000",null],
  ["Arizona Maternity &amp; Women's Clinic","glendale","6314 W Union Hills Dr, Glendale, AZ 85308",33.654431,-112.1965265,"6233221800",null],
  ["Planned Parenthood – Glendale","glendale","5771 W Eugie Ave, Glendale, AZ 85304",33.6082944,-112.1835865,"6022777526",null],
  // Scottsdale
  ["Arizona Women's Care","scottsdale","9823 N 95th St #101, Scottsdale, AZ 85258",33.5758481,-111.8744247,"9285697049",null],
  ["Cornerstone Women's Care OBGYN","scottsdale","9377 E Bell Rd Ste 143, Scottsdale, AZ 85260",33.637365,-111.8821036,"6028672690",null],
  ["North Scottsdale Women's Health","scottsdale","9745 N 90th Pl, Scottsdale, AZ 85258",33.573707,-111.885031,"4806611485",null],
  ["Paradise Valley OBGYN","scottsdale","10261 N 92nd St #101, Scottsdale, AZ 85258",33.579002,-111.879076,"4804434437",null],
  // Tempe
  ["Southwest Contemporary Women's Care","tempe","6301 S McClintock Dr Unit 215, Tempe, AZ 85283",33.364717,-111.910624,"4808206657",null],
  // Mesa
  ["Women's Care Arizona – Mesa","mesa","4824 E Baseline Rd Ste 129, Mesa, AZ 85206",33.3799342,-111.7288612,"4806441001",null],
  ["Arizona Gynecology Consultants – Mesa","mesa","1151 N Gilbert Rd, Mesa, AZ 85203",33.4369079,-111.7875306,"6023588588",null],
  // Chandler
  ["Lilac Ob-Gyn","chandler","655 S Dobson Rd Ste 101, Chandler, AZ 85224",33.2946811,-111.8756382,"4804592555",null],
  ["New Horizons Women's Care","chandler","1950 W Frye Rd, Chandler, AZ 85224",33.299085,-111.87535,"4808959555",null],
  ["Valley Perinatal Services – Chandler","chandler","1910 W Frye Rd, Chandler, AZ 85224",33.2989614,-111.8748277,"4807566000",null],
  ["Sun Life Health OB/GYN","chandler","655 S Dobson Rd #201, Chandler, AZ 85224",33.2946179,-111.8756801,"4803079477","fqhc"],
  // Gilbert
  ["WREN Obstetrics, Midwifery &amp; Gynecology","gilbert","3370 Mercy Rd Ste 314, Gilbert, AZ 85297",33.2891522,-111.7494887,"4807820993",null],
  ["Desert Maternal Fetal Medicine – Gilbert","gilbert","3303 S Lindsay Rd Bldg 6 Unit 113, Gilbert, AZ 85297",33.2895401,-111.7732505,"4806841692",null],
  ["Women's Care OBGYN in Gilbert","gilbert","3530 S Val Vista Dr, Gilbert, AZ 85297",33.2863266,-111.7568977,"4806336868",null],
  ["Morning Star OB/GYN","gilbert","3499 Mercy Rd, Gilbert, AZ 85297",33.2851597,-111.7479117,"4803558525",null]
];

const SHELTER_REGIONS = [
  ["cphx","Central &amp; South Phoenix","Phoenix Centro y Sur"],
  ["nphx","North Phoenix","Norte de Phoenix"],
  ["west","West Valley","Valle Oeste"],
  ["mesa","Mesa &amp; East Valley","Mesa y Valle Este"],
  ["chgi","Chandler &amp; Gilbert","Chandler y Gilbert"]
];

// type: 'dv' (confidential, no map), 'family', 'preg'
// fields: name, region, type, address|null, lat|null, lng|null, phone, desc_en, desc_es
const SHELTERS = [
  ["Sojourner Center","cphx","dv",null,null,null,"6022440089",
    "One of the nation's largest domestic-violence shelters. Pet friendly, on-site childcare, Spanish-language services.",
    "Uno de los refugios de violencia doméstica más grandes del país. Admite mascotas, cuidado infantil y servicios en español."],
  ["De Colores (Chicanos Por La Causa)","cphx","dv",null,null,null,"6022691515",
    "Bilingual domestic-violence shelter serving South Phoenix. Spanish-language services, pet friendly.",
    "Refugio bilingüe de violencia doméstica que atiende el sur de Phoenix. Servicios en español, admite mascotas."],
  ["Maggie's Place – Homes for pregnant women","cphx","preg","4001 N 30th St, Phoenix, AZ 85016",33.4935546,-112.0168916,"6022625555",
    "Free residential homes for pregnant women, with support through the baby's first year.",
    "Casas residenciales gratuitas para mujeres embarazadas, con apoyo durante el primer año del bebé."],
  ["Halle Women's Center at UMOM","cphx","family","3424 E Van Buren St, Phoenix, AZ 85008",33.4517119,-112.0080285,"6023625833",
    "Emergency shelter for single women, with meals, laundry, and case management toward housing.",
    "Refugio de emergencia para mujeres solas, con comidas, lavandería y gestión de casos hacia vivienda."],
  ["Central Arizona Shelter Services (CASS)","cphx","family","230 S 12th Ave, Phoenix, AZ 85007",33.4448876,-112.0888167,"6022566945",
    "The Valley's largest emergency shelter campus. Open 24 hours.",
    "El campus de refugio de emergencia más grande del Valle. Abierto las 24 horas."],
  ["Chrysalis","nphx","dv",null,null,null,"6029444999",
    "Domestic-violence shelter and counseling in North Phoenix. Service animals welcome.",
    "Refugio y consejería de violencia doméstica en el norte de Phoenix. Se admiten animales de servicio."],
  ["CASS Family Shelter (Vista Colina)","nphx","family","1050 W Mountain View Rd, Phoenix, AZ 85021",33.5751393,-112.0866044,"6028708778",
    "Townhome-style emergency shelter for families, with childcare and a play area.",
    "Refugio de emergencia tipo casa para familias, con cuidado infantil y área de juegos."],
  ["A New Leaf – Faith House","west","dv",null,null,null,"6239396798",
    "Domestic-violence shelter for singles and families in the West Valley.",
    "Refugio de violencia doméstica para personas solas y familias en el Valle Oeste."],
  ["New Life Center","west","dv",null,null,null,"6239324404",
    "One of Arizona's largest DV shelters, based in the West Valley. Pet friendly.",
    "Uno de los refugios de violencia doméstica más grandes de Arizona, en el Valle Oeste. Admite mascotas."],
  ["Eve's Place","west","dv","10448 W Coggins Dr, Sun City, AZ 85351",33.5996259,-112.2835949,"6235375380",
    "Domestic & sexual violence support, counseling, and advocacy in the West Valley.",
    "Apoyo, consejería y defensa para violencia doméstica y sexual en el Valle Oeste."],
  ["A New Leaf – CAAFA","mesa","dv",null,null,null,"4807732359",
    "Domestic-violence shelter for singles and families (Apache Junction / East Valley).",
    "Refugio de violencia doméstica para personas solas y familias (Apache Junction / Valle Este)."],
  ["House of Refuge","mesa","family","6935 E Williams Field Rd, Mesa, AZ 85212",33.3065272,-111.6830338,"4809889242",
    "Transitional housing for families working toward stability after a crisis.",
    "Vivienda de transición para familias que buscan estabilidad tras una crisis."],
  ["The Olive Press","mesa","family","720 S Mesa Dr, Mesa, AZ 85210",33.4018845,-111.8233456,null,
    "Faith-based transitional shelter for women. Confirm current intake by dialing 2-1-1.",
    "Refugio de transición para mujeres, de base religiosa. Confirme la admisión actual marcando 2-1-1."],
  ["My Sister's Place","chgi","dv",null,null,null,"4808211024",
    "Domestic-violence shelter for singles and families in Chandler. Service animals welcome.",
    "Refugio de violencia doméstica para personas solas y familias en Chandler. Se admiten animales de servicio."]
];

/* =========================================================
   I18N (UI strings)
   ========================================================= */
const I18N = {
  en:{
    brand:"Prenatal Care • Phoenix Metro",
    eyebrow:"A guide for expecting families",
    heroTitle:"Access to Prenatal Care in the Phoenix Metropolitan Area",
    heroLede:"Find pregnancy clinics, safe shelter, and the support you need across the Valley — wherever you are, whatever your situation.",
    tabClinics:"Pregnancy Clinics", tabShelters:"Women's Shelters", tabResources:"Resources & Support",
    clinicsHead:"Pregnancy Clinics",
    clinicsSub:"OB-GYN practices, perinatal specialists, and community health centers across the Valley. Choose a neighborhood, then find each location on the map below.",
    clinicsDisc:"Always call ahead to confirm hours, accepted insurance, and whether they take new prenatal patients. Many centers offer sliding-scale fees and accept AHCCCS (Arizona Medicaid).",
    clinicMapTitle:"Clinic locations", legClinic:"Clinic / health center",
    sheltersHead:"Women's Shelters & Safe Housing",
    sheltersSub:"Emergency domestic-violence programs, family shelters, and transitional housing. For safety, most domestic-violence shelters keep their addresses private — you reach them by phone, and they arrange a safe place to go.",
    shelterMapTitle:"Mapped: shelters with public locations",
    legShelter:"Shelter / housing", legPreg:"For pregnant women",
    shelterMapNote:"Domestic-violence shelters are intentionally not pinned on the map. Call the intake numbers on the cards above — their locations are kept confidential to protect residents.",
    resHead:"Resources & Support",
    resSub:"Everything around getting care: how to pay for it, your rights, a month-by-month roadmap, food and supplies, and someone to talk to. Start with what you need right now.",
    emTitle:"If you need help now", emSub:"These lines are free, confidential, and answered around the clock unless noted.",
    emDangerL:"Immediate danger", emDangerS:"Call or text. Tell them if you can't speak safely.",
    emDvL:"Domestic violence", emDvS:"National hotline, 24/7. Text START to 88788.",
    emMhL:"Emotional crisis", emMhS:"Suicide & Crisis Lifeline. Call or text, 24/7.",
    emAnyL:"Any resource, 24/7", emAnyS:"Arizona 211 connects you to local help.",
    chTitle:"What do you need right now?", chSub:"Tap one and we'll jump you to the right place.",
    roadTitle:"Your pregnancy roadmap", roadSub:"A simple month-by-month checklist. Tap a stage to open it.",
    footTitle:"About this guide.",
    footBody:"This directory was compiled from public listings in June 2026 to help expecting families in the Phoenix metro area find care. Details change — please call ahead to confirm. This site offers information, not medical or legal advice.",
    footEmerg:"In a medical emergency, call 911. An emergency room cannot turn you away when you are in active labor, regardless of your ability to pay or your immigration status.",
    call:"Call", maps:"Open in Maps", confidential:"Confidential — call first",
    forPregnant:"For pregnant women", communityHealth:"Sliding scale",
    clinicsN:"clinics", sheltersN:"programs"
  },
  es:{
    brand:"Cuidado Prenatal • Área de Phoenix",
    eyebrow:"Una guía para familias que esperan un bebé",
    heroTitle:"Acceso al Cuidado Prenatal en el Área Metropolitana de Phoenix",
    heroLede:"Encuentre clínicas de embarazo, refugio seguro y el apoyo que necesita en todo el Valle — donde sea que esté y sea cual sea su situación.",
    tabClinics:"Clínicas de Embarazo", tabShelters:"Refugios para Mujeres", tabResources:"Recursos y Apoyo",
    clinicsHead:"Clínicas de Embarazo",
    clinicsSub:"Consultorios de ginecología y obstetricia, especialistas perinatales y centros de salud comunitarios en todo el Valle. Elija un vecindario y luego ubique cada lugar en el mapa.",
    clinicsDisc:"Llame siempre antes para confirmar horarios, seguros aceptados y si reciben nuevas pacientes prenatales. Muchos centros ofrecen tarifas según ingresos y aceptan AHCCCS (Medicaid de Arizona).",
    clinicMapTitle:"Ubicación de las clínicas", legClinic:"Clínica / centro de salud",
    sheltersHead:"Refugios y Vivienda Segura para Mujeres",
    sheltersSub:"Programas de emergencia para violencia doméstica, refugios familiares y vivienda de transición. Por seguridad, la mayoría de los refugios de violencia doméstica mantienen su dirección en privado — usted los contacta por teléfono y ellos coordinan un lugar seguro.",
    shelterMapTitle:"En el mapa: refugios con ubicación pública",
    legShelter:"Refugio / vivienda", legPreg:"Para embarazadas",
    shelterMapNote:"Los refugios de violencia doméstica no se marcan en el mapa a propósito. Llame a los números de admisión en las tarjetas de arriba — su ubicación es confidencial para proteger a las residentes.",
    resHead:"Recursos y Apoyo",
    resSub:"Todo lo relacionado con recibir atención: cómo pagarla, sus derechos, una guía mes a mes, comida y artículos, y alguien con quien hablar. Empiece con lo que necesita ahora.",
    emTitle:"Si necesita ayuda ahora", emSub:"Estas líneas son gratuitas, confidenciales y atienden las 24 horas, salvo que se indique.",
    emDangerL:"Peligro inmediato", emDangerS:"Llame o envíe un texto. Avise si no puede hablar con seguridad.",
    emDvL:"Violencia doméstica", emDvS:"Línea nacional, 24/7. Envíe START al 88788.",
    emMhL:"Crisis emocional", emMhS:"Línea de Crisis y Suicidio. Llame o envíe un texto, 24/7.",
    emAnyL:"Cualquier recurso, 24/7", emAnyS:"Arizona 211 lo conecta con ayuda local.",
    chTitle:"¿Qué necesita ahora mismo?", chSub:"Toque una opción y lo llevamos al lugar indicado.",
    roadTitle:"Su guía del embarazo", roadSub:"Una lista sencilla mes a mes. Toque una etapa para abrirla.",
    footTitle:"Acerca de esta guía.",
    footBody:"Este directorio se recopiló de listados públicos en junio de 2026 para ayudar a las familias que esperan un bebé en el área de Phoenix a encontrar atención. Los datos cambian — por favor llame antes para confirmar. Este sitio ofrece información, no consejo médico ni legal.",
    footEmerg:"En una emergencia médica, llame al 911. Una sala de emergencias no puede rechazarla cuando está en trabajo de parto activo, sin importar su capacidad de pago ni su estatus migratorio.",
    call:"Llamar", maps:"Abrir en Mapas", confidential:"Confidencial — llame primero",
    forPregnant:"Para embarazadas", communityHealth:"Según ingresos",
    clinicsN:"clínicas", sheltersN:"programas"
  }
};

/* =========================================================
   RESOURCE CARDS + CHOOSER + ROADMAP CONTENT
   ========================================================= */
const RES_ICON = {
  pay:["#1f9e92",'<path d="M3 7h18v10H3z" stroke="#fff" stroke-width="2"/><circle cx="12" cy="12" r="2.4" stroke="#fff" stroke-width="2"/>'],
  food:["#5b7f4d",'<path d="M6 3v8M9 3v8M6 11h3v9H6zM16 3c-2 0-3 3-3 6 0 2 1 3 3 3v8" stroke="#fff" stroke-width="2" stroke-linecap="round"/>'],
  rights:["#2c2a4a",'<path d="M12 3 4 6v6c0 5 8 9 8 9s8-4 8-9V6l-8-3Z" stroke="#fff" stroke-width="2" stroke-linejoin="round"/><path d="m9 12 2 2 4-4" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>'],
  imm:["#df6c4f",'<circle cx="12" cy="12" r="9" stroke="#fff" stroke-width="2"/><path d="M3 12h18M12 3c2.5 2.5 2.5 15 0 18M12 3c-2.5 2.5-2.5 15 0 18" stroke="#fff" stroke-width="1.6"/>'],
  mind:["#7d4f74",'<path d="M9 18h6M10 21h4" stroke="#fff" stroke-width="2" stroke-linecap="round"/><path d="M12 3a6 6 0 0 0-4 10c1 1 1 2 1 3h6c0-1 0-2 1-3a6 6 0 0 0-4-10Z" stroke="#fff" stroke-width="2" stroke-linejoin="round"/>'],
  supply:["#e9a23b",'<path d="M3 8h18l-1.5 11.5a1 1 0 0 1-1 .9H5.5a1 1 0 0 1-1-.9L3 8Z" stroke="#fff" stroke-width="2" stroke-linejoin="round"/><path d="M8 8a4 4 0 0 1 8 0" stroke="#fff" stroke-width="2"/>']
};

function R(en,es){return {en,es};}
const RESOURCES = [
  {
    id:"pay", icon:"pay",
    title:R("Paying for care","Cómo pagar la atención"),
    body:R("Cost should never stop you from getting prenatal care. These programs cover most pregnant Arizonans.",
            "El costo nunca debe impedirle recibir atención prenatal. Estos programas cubren a la mayoría de las embarazadas en Arizona."),
    rows:[
      [R("AHCCCS (Arizona Medicaid)","AHCCCS (Medicaid de Arizona)"), R("Apply anytime","Solicite en cualquier momento"),"https://www.healthearizonaplus.gov"],
      [R("Pregnancy coverage — income-based","Cobertura de embarazo según ingresos"), R("healthearizonaplus.gov",""),"https://www.healthearizonaplus.gov"],
      [R("KidsCare (for your children)","KidsCare (para sus hijos)"), R("azahcccs.gov",""),"https://www.azahcccs.gov/Members/GetCovered/Categories/KidsCare.html"],
      [R("Sliding-scale health centers","Centros de salud según ingresos"), R("Dial 2-1-1","Marque 2-1-1"),"tel:18772118661"],
      [R("Can't be denied emergency care","No le pueden negar atención de emergencia"), R("Federal law","Ley federal"),null]
    ]
  },
  {
    id:"food", icon:"food",
    title:R("Food & nutrition (WIC)","Comida y nutrición (WIC)"),
    body:R("WIC gives pregnant people and children under 5 free healthy food, formula, and breastfeeding support.",
            "WIC ofrece a embarazadas y niños menores de 5 años comida saludable gratis, fórmula y apoyo para amamantar."),
    rows:[
      [R("Find your local WIC clinic","Encuentre su clínica WIC"), R("azwic.gov",""),"https://azdhs.gov/azwic"],
      [R("Apply or ask questions","Solicite o haga preguntas"), R("Dial 2-1-1","Marque 2-1-1"),"tel:18772118661"],
      [R("Free food bank near you","Banco de alimentos cercano"), R("Dial 2-1-1","Marque 2-1-1"),"tel:18772118661"]
    ]
  },
  {
    id:"rights", icon:"rights",
    title:R("Know your rights","Conozca sus derechos"),
    body:R("A few protections worth knowing as you seek care in Arizona.",
            "Algunas protecciones importantes mientras busca atención en Arizona."),
    rows:[
      [R("ERs must help you in active labor","Las salas de emergencia deben atenderla en parto"), R("EMTALA",""),null],
      [R("Care regardless of immigration status","Atención sin importar estatus migratorio"), R("Yes","Sí"),null],
      [R("Emergency Medicaid covers labor & delivery","Medicaid de emergencia cubre el parto"), R("Any status","Cualquier estatus"),null],
      [R("Your medical records are confidential","Su expediente médico es confidencial"), R("HIPAA",""),null],
      [R("Address confidentiality for DV survivors","Dirección confidencial para sobrevivientes"), R("AZ program","Programa AZ"),"https://azsos.gov/services/address-confidentiality-program-acp"]
    ]
  },
  {
    id:"imm", icon:"imm",
    title:R("For immigrant & Spanish-speaking families","Para familias inmigrantes y de habla hispana"),
    body:R("You can get prenatal and emergency care in Arizona no matter your immigration status. Using WIC, emergency Medicaid, or prenatal care is not counted against you in a public-charge review.",
            "Puede recibir atención prenatal y de emergencia en Arizona sin importar su estatus migratorio. Usar WIC, Medicaid de emergencia o atención prenatal no cuenta en su contra en una revisión de carga pública."),
    rows:[
      [R("De Colores — Spanish DV services","De Colores — servicios DV en español"), R("602-269-1515",""),"tel:16022691515"],
      [R("Community centers with Spanish staff","Centros con personal en español"), R("Dial 2-1-1","Marque 2-1-1"),"tel:18772118661"],
      [R("Free immigration legal help","Ayuda legal de inmigración gratuita"), R("Florence Project","Florence Project"),"https://firrp.org"]
    ]
  },
  {
    id:"mind", icon:"mind",
    title:R("Mental & emotional health","Salud mental y emocional"),
    body:R("Pregnancy and new parenthood are a lot. Support is available 24/7, and reaching out is a sign of strength.",
            "El embarazo y la maternidad son mucho. Hay apoyo disponible 24/7, y pedir ayuda es señal de fortaleza."),
    rows:[
      [R("National Maternal Mental Health Hotline","Línea Nacional de Salud Mental Materna"), R("1-833-852-6262",""),"tel:18338526262"],
      [R("Postpartum Support International","Apoyo Posparto Internacional"), R("1-800-944-4773",""),"tel:18009444773"],
      [R("Suicide & Crisis Lifeline","Línea de Crisis y Suicidio"), R("Call or text 988","Llame o texto 988"),"tel:988"]
    ]
  },
  {
    id:"supply", icon:"supply",
    title:R("Free supplies & extra support","Artículos gratis y apoyo adicional"),
    body:R("Diapers, car seats, home visits from a nurse, and people in your corner — at little or no cost.",
            "Pañales, asientos de auto, visitas de enfermeras a domicilio y personas que la apoyan — a bajo costo o gratis."),
    rows:[
      [R("Maggie's Place — homes for pregnant women","Maggie's Place — casas para embarazadas"), R("602-262-5555",""),"tel:16022625555"],
      [R("Healthy Families AZ — free home visits","Healthy Families AZ — visitas gratis"), R("Learn more","Más información"),"https://strongfamiliesaz.com/program/healthy-families/"],
      [R("Diaper Bank of Central Arizona","Banco de Pañales de Arizona Central"), R("diaperbankaz.org",""),"https://diaperbankaz.org"],
      [R("Fresh Start Women's Foundation","Fundación Fresh Start"), R("602-252-8494",""),"tel:16022528494"],
      [R("Hope Women's Center","Hope Women's Center"), R("602-715-0999",""),"tel:16027150999"]
    ]
  }
];

const NEEDS = [
  ["pay","#1f9e92",R("I can't afford care","No puedo pagar la atención")],
  ["imm","#df6c4f",R("No insurance / undocumented","Sin seguro / indocumentada")],
  ["rights","#2c2a4a",R("Will they help me?","¿Me van a atender?")],
  ["food","#5b7f4d",R("I need food or diapers","Necesito comida o pañales")],
  ["mind","#7d4f74",R("I'm struggling emotionally","Me siento agobiada")],
  ["supply","#e9a23b",R("I need baby supplies & support","Necesito artículos y apoyo")]
];

const ROADMAP = [
  ["#5b7f4d", R("Just found out — weeks 1–12","Recién se enteró — semanas 1–12"),
    R("<li>Start a prenatal vitamin with folic acid today.</li><li>Book your first prenatal visit (usually around weeks 8–10).</li><li>Apply for AHCCCS and WIC — don't wait for the first appointment.</li><li>Avoid alcohol, tobacco, and unprescribed meds; ask about anything you're unsure of.</li>",
      "<li>Empiece hoy una vitamina prenatal con ácido fólico.</li><li>Agende su primera consulta prenatal (normalmente entre las semanas 8 y 10).</li><li>Solicite AHCCCS y WIC — no espere a la primera cita.</li><li>Evite alcohol, tabaco y medicamentos sin receta; pregunte ante cualquier duda.</li>")],
  ["#1f9e92", R("Second trimester — weeks 13–27","Segundo trimestre — semanas 13–27"),
    R("<li>Anatomy ultrasound around week 20.</li><li>Glucose screening for gestational diabetes (~weeks 24–28).</li><li>Choose the hospital where you'll give birth.</li><li>This is often the best window to travel or take a class.</li>",
      "<li>Ecografía anatómica alrededor de la semana 20.</li><li>Prueba de glucosa para diabetes gestacional (~semanas 24–28).</li><li>Elija el hospital donde dará a luz.</li><li>Suele ser el mejor momento para viajar o tomar una clase.</li>")],
  ["#e9a23b", R("Third trimester — weeks 28–40","Tercer trimestre — semanas 28–40"),
    R("<li>More frequent visits; Group B strep test around week 36.</li><li>Write a simple birth plan and pack your hospital bag.</li><li>Choose a pediatrician and install your car seat.</li><li>Know the signs of labor and when to call your provider.</li>",
      "<li>Consultas más frecuentes; prueba de estreptococo grupo B hacia la semana 36.</li><li>Escriba un plan de parto sencillo y prepare su maleta.</li><li>Elija un pediatra e instale el asiento de auto.</li><li>Conozca las señales del parto y cuándo llamar a su proveedor.</li>")],
  ["#df6c4f", R("After birth — the fourth trimester","Después del parto — el cuarto trimestre"),
    R("<li>Go to your postpartum checkup (around 6 weeks).</li><li>Ask for a mental-health check — the baby blues vs. postpartum depression.</li><li>Free lactation support is available; call your provider or 2-1-1.</li><li>Keep WIC going — it covers you and baby after birth too.</li>",
      "<li>Acuda a su control posparto (alrededor de las 6 semanas).</li><li>Pida una evaluación de salud mental — diferenciar la tristeza posparto de la depresión.</li><li>Hay apoyo gratuito de lactancia; llame a su proveedor o al 2-1-1.</li><li>Mantenga WIC — también la cubre a usted y al bebé después del parto.</li>")]
];

/* =========================================================
   STATE + HELPERS
   ========================================================= */
let lang = "en";
let clinicHood = "all";
let shelterRegion = "all";
let clinicMap, shelterMap, clinicLayer, shelterLayer;
let mapsReady = {clinics:false, shelters:false};

const t = k => I18N[lang][k];
const tx = o => o[lang];
const fmtPhone = p => p ? p.replace(/^1?(\d{3})(\d{3})(\d{4})$/, "($1) $2-$3") : "";
const gmaps = (name,addr) => "https://www.google.com/maps/search/?api=1&query=" + encodeURIComponent(name.replace(/&amp;/g,"&")+" "+addr);
const hoodLabel = (arr,id) => { const r = arr.find(x=>x[0]===id); return r ? r[lang==="en"?1:2] : id; };

function pinSVG(color){
  return '<svg width="30" height="40" viewBox="0 0 30 40" xmlns="http://www.w3.org/2000/svg">'+
    '<path d="M15 0C7 0 1 6 1 14c0 9 14 26 14 26s14-17 14-26C29 6 23 0 15 0Z" fill="'+color+'" stroke="#fff" stroke-width="2"/>'+
    '<circle cx="15" cy="14" r="5" fill="#fff"/></svg>';
}
function makeIcon(color){
  return L.divIcon({html:pinSVG(color), className:"", iconSize:[30,40], iconAnchor:[15,40], popupAnchor:[0,-36]});
}

/* =========================================================
   RENDERERS
   ========================================================= */
function renderClinicHoods(){
  const wrap = document.getElementById("clinicHoods");
  const counts = {};
  CLINICS.forEach(c=>counts[c[1]]=(counts[c[1]]||0)+1);
  let html = `<button class="hood ${clinicHood==='all'?'active':''}" onclick="setClinicHood('all')">${lang==='en'?'All areas':'Todas las áreas'} <span class="n">(${CLINICS.length})</span></button>`;
  CLINIC_HOODS.forEach(h=>{
    html += `<button class="hood ${clinicHood===h[0]?'active':''}" onclick="setClinicHood('${h[0]}')">${lang==='en'?h[1]:h[2]} <span class="n">(${counts[h[0]]||0})</span></button>`;
  });
  wrap.innerHTML = html;
}
function renderClinics(){
  const grid = document.getElementById("clinicGrid");
  const list = CLINICS.filter(c=>clinicHood==='all'||c[1]===clinicHood);
  document.getElementById("clinicCount").textContent = list.length+" "+t("clinicsN");
  grid.innerHTML = list.map(c=>{
    const [name,hood,addr,lat,lng,phone,flag]=c;
    const badge = flag==='fqhc' ? `<span class="badge badge-fqhc">${t("communityHealth")}</span>` : "";
    return `<div class="card">${badge}
      <div class="hoodtag">${hoodLabel(CLINIC_HOODS,hood)}</div>
      <h3>${name}</h3>
      <p class="addr"><svg width="14" height="14" viewBox="0 0 24 24" fill="none"><path d="M12 21s-7-4.5-7-10a7 7 0 0 1 14 0c0 5.5-7 10-7 10Z" stroke="#9a8" stroke-width="2"/><circle cx="12" cy="11" r="2.5" stroke="#9a8" stroke-width="2"/></svg>${addr}</p>
      <div class="card-actions">
        <a class="btn btn-map" target="_blank" rel="noopener" href="${gmaps(name,addr)}">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none"><path d="M12 21s-7-4.5-7-10a7 7 0 0 1 14 0c0 5.5-7 10-7 10Z" stroke="#fff" stroke-width="2"/><circle cx="12" cy="11" r="2.5" fill="#fff"/></svg>${t("maps")}</a>
        ${phone?`<a class="btn btn-call" href="tel:1${phone}"><svg width="14" height="14" viewBox="0 0 24 24" fill="none"><path d="M5 4h3l2 5-2 1a11 11 0 0 0 5 5l1-2 5 2v3a2 2 0 0 1-2 2A16 16 0 0 1 3 6a2 2 0 0 1 2-2Z" stroke="#2c2a4a" stroke-width="1.8" stroke-linejoin="round"/></svg>${fmtPhone(phone)}</a>`:""}
      </div></div>`;
  }).join("");
  refreshClinicMarkers();
}

function renderShelterHoods(){
  const wrap = document.getElementById("shelterHoods");
  const counts = {};
  SHELTERS.forEach(s=>counts[s[1]]=(counts[s[1]]||0)+1);
  let html = `<button class="hood ${shelterRegion==='all'?'active':''}" onclick="setShelterRegion('all')">${lang==='en'?'All areas':'Todas las áreas'} <span class="n">(${SHELTERS.length})</span></button>`;
  SHELTER_REGIONS.forEach(h=>{
    html += `<button class="hood ${shelterRegion===h[0]?'active':''}" onclick="setShelterRegion('${h[0]}')">${lang==='en'?h[1]:h[2]} <span class="n">(${counts[h[0]]||0})</span></button>`;
  });
  wrap.innerHTML = html;
}
function renderShelters(){
  const grid = document.getElementById("shelterGrid");
  const list = SHELTERS.filter(s=>shelterRegion==='all'||s[1]===shelterRegion);
  document.getElementById("shelterCount").textContent = list.length+" "+t("sheltersN");
  grid.innerHTML = list.map(s=>{
    const [name,region,type,addr,lat,lng,phone,den,des]=s;
    const desc = lang==='en'?den:des;
    let badge="";
    if(type==='dv') badge=`<span class="badge badge-conf">${t("confidential")}</span>`;
    else if(type==='preg') badge=`<span class="badge badge-preg">${t("forPregnant")}</span>`;
    const mapsBtn = addr ? `<a class="btn btn-map" target="_blank" rel="noopener" href="${gmaps(name,addr)}"><svg width="14" height="14" viewBox="0 0 24 24" fill="none"><path d="M12 21s-7-4.5-7-10a7 7 0 0 1 14 0c0 5.5-7 10-7 10Z" stroke="#fff" stroke-width="2"/><circle cx="12" cy="11" r="2.5" fill="#fff"/></svg>${t("maps")}</a>` : "";
    const callBtn = phone ? `<a class="btn btn-call" href="tel:1${phone}"><svg width="14" height="14" viewBox="0 0 24 24" fill="none"><path d="M5 4h3l2 5-2 1a11 11 0 0 0 5 5l1-2 5 2v3a2 2 0 0 1-2 2A16 16 0 0 1 3 6a2 2 0 0 1 2-2Z" stroke="#2c2a4a" stroke-width="1.8" stroke-linejoin="round"/></svg>${fmtPhone(phone)}</a>` : "";
    return `<div class="card">${badge}
      <div class="hoodtag">${hoodLabel(SHELTER_REGIONS,region)}</div>
      <h3>${name}</h3>
      ${addr?`<p class="addr"><svg width="14" height="14" viewBox="0 0 24 24" fill="none"><path d="M12 21s-7-4.5-7-10a7 7 0 0 1 14 0c0 5.5-7 10-7 10Z" stroke="#d9a" stroke-width="2"/><circle cx="12" cy="11" r="2.5" stroke="#d9a" stroke-width="2"/></svg>${addr}</p>`:""}
      <div class="card-actions">${mapsBtn}${callBtn}</div>
      <p class="note">${desc}</p>
    </div>`;
  }).join("");
  refreshShelterMarkers();
}

/* ---- maps ---- */
function initClinicMap(){
  if(mapsReady.clinics) return;
  clinicMap = L.map("clinicMap",{scrollWheelZoom:false}).setView([33.45,-111.95],10);
  L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",{maxZoom:18,attribution:'© OpenStreetMap'}).addTo(clinicMap);
  clinicLayer = L.layerGroup().addTo(clinicMap);
  mapsReady.clinics=true;
  refreshClinicMarkers();
}
function refreshClinicMarkers(){
  if(!mapsReady.clinics) return;
  clinicLayer.clearLayers();
  const list = CLINICS.filter(c=>clinicHood==='all'||c[1]===clinicHood);
  const icon = makeIcon("#1f9e92");
  const bounds=[];
  list.forEach(c=>{
    const [name,hood,addr,lat,lng]=c;
    bounds.push([lat,lng]);
    L.marker([lat,lng],{icon}).addTo(clinicLayer).bindPopup(
      `<div class="pin-name">${name}</div><div class="pin-addr">${addr}</div><a class="pin-link" target="_blank" rel="noopener" href="${gmaps(name,addr)}">${t("maps")} →</a>`
    );
  });
  if(bounds.length) clinicMap.fitBounds(bounds,{padding:[40,40],maxZoom:13});
}
function initShelterMap(){
  if(mapsReady.shelters) return;
  shelterMap = L.map("shelterMap",{scrollWheelZoom:false}).setView([33.45,-111.95],10);
  L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",{maxZoom:18,attribution:'© OpenStreetMap'}).addTo(shelterMap);
  shelterLayer = L.layerGroup().addTo(shelterMap);
  mapsReady.shelters=true;
  refreshShelterMarkers();
}
function refreshShelterMarkers(){
  if(!mapsReady.shelters) return;
  shelterLayer.clearLayers();
  const list = SHELTERS.filter(s=>(shelterRegion==='all'||s[1]===shelterRegion) && s[3]);
  const bounds=[];
  list.forEach(s=>{
    const [name,region,type,addr,lat,lng]=s;
    bounds.push([lat,lng]);
    const icon = makeIcon(type==='preg'?"#e9a23b":"#df6c4f");
    L.marker([lat,lng],{icon}).addTo(shelterLayer).bindPopup(
      `<div class="pin-name">${name}</div><div class="pin-addr">${addr}</div><a class="pin-link" target="_blank" rel="noopener" href="${gmaps(name,addr)}">${t("maps")} →</a>`
    );
  });
  if(bounds.length) shelterMap.fitBounds(bounds,{padding:[40,40],maxZoom:12});
  else shelterMap.setView([33.45,-111.95],10);
}

/* ---- resources ---- */
function renderResources(){
  document.getElementById("resGrid").innerHTML = RESOURCES.map(r=>{
    const [col,path]=RES_ICON[r.icon];
    const rows = r.rows.map(([k,v,href])=>{
      const val = href ? `<a class="v" href="${href}" ${href.startsWith('http')?'target="_blank" rel="noopener"':''}>${tx(v)}</a>` : `<span class="v plain">${tx(v)}</span>`;
      return `<li><span class="k">${tx(k)}</span>${val}</li>`;
    }).join("");
    return `<div class="res" id="res-${r.id}">
      <div class="rh"><div class="ric" style="background:${col}"><svg width="20" height="20" viewBox="0 0 24 24" fill="none">${path}</svg></div><h3>${tx(r.title)}</h3></div>
      <p>${tx(r.body)}</p><ul>${rows}</ul></div>`;
  }).join("");
}
function renderChips(){
  document.getElementById("needChips").innerHTML = NEEDS.map(([id,col,label])=>
    `<button class="chip" onclick="jumpTo('${id}')"><span class="ic" style="background:${col}">●</span>${tx(label)}</button>`
  ).join("");
}
function jumpTo(id){
  const el = document.getElementById("res-"+id);
  el.scrollIntoView({behavior:"smooth",block:"center"});
  el.classList.add("flash");
  setTimeout(()=>el.classList.remove("flash"),1800);
}
function renderRoadmap(){
  document.getElementById("roadAcc").innerHTML = ROADMAP.map((r,i)=>{
    const [col,title,body]=r;
    return `<div class="acc" id="acc-${i}">
      <button class="acc-btn" onclick="toggleAcc(${i})">
        <span class="acc-num" style="background:${col}">${i+1}</span>
        <span class="at">${tx(title)}</span><span class="ax">+</span>
      </button>
      <div class="acc-body"><div class="inner"><ul>${tx(body)}</ul></div></div>
    </div>`;
  }).join("");
}
function toggleAcc(i){
  const acc = document.getElementById("acc-"+i);
  const body = acc.querySelector(".acc-body");
  const open = acc.classList.toggle("open");
  body.style.maxHeight = open ? body.scrollHeight+"px" : null;
}

/* =========================================================
   CONTROLLERS
   ========================================================= */
function setClinicHood(h){ clinicHood=h; renderClinicHoods(); renderClinics(); }
function setShelterRegion(r){ shelterRegion=r; renderShelterHoods(); renderShelters(); }

function showTab(id){
  document.querySelectorAll(".tab").forEach(b=>b.classList.toggle("active",b.dataset.tab===id));
  document.querySelectorAll(".panel").forEach(p=>p.classList.toggle("active",p.id===id));
  if(id==="clinics"){ initClinicMap(); setTimeout(()=>{clinicMap&&clinicMap.invalidateSize(); refreshClinicMarkers();},60); }
  if(id==="shelters"){ initShelterMap(); setTimeout(()=>{shelterMap&&shelterMap.invalidateSize(); refreshShelterMarkers();},60); }
  window.scrollTo({top:document.querySelector("nav.tabs").offsetTop-70,behavior:"smooth"});
}

function applyStaticI18n(){
  document.documentElement.lang = lang;
  document.querySelectorAll("[data-i18n]").forEach(el=>{
    const k = el.getAttribute("data-i18n");
    if(I18N[lang][k]!==undefined) el.innerHTML = I18N[lang][k];
  });
}
function setLang(l){
  lang=l;
  document.getElementById("btn-en").classList.toggle("active",l==="en");
  document.getElementById("btn-es").classList.toggle("active",l==="es");
  applyStaticI18n();
  renderClinicHoods(); renderClinics();
  renderShelterHoods(); renderShelters();
  renderChips(); renderResources(); renderRoadmap();
}

/* init */
applyStaticI18n();
renderClinicHoods(); renderClinics();
renderShelterHoods(); renderShelters();
renderChips(); renderResources(); renderRoadmap();
initClinicMap();
setTimeout(()=>{clinicMap&&clinicMap.invalidateSize(); refreshClinicMarkers();},200);
</script>
</body>
</html>
