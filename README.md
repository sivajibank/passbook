
<!DOCTYPE html>
<html lang="ta">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
<meta name="robots" content="noindex, nofollow">
<meta http-equiv="Cache-Control" content="no-cache, must-revalidate">
<meta http-equiv="Pragma" content="no-cache">
<!-- PASSBOOK VIEWER v10 — Latest-gen UI/UX: aurora backdrop, glassmorphic animated
     KPI cards (orbs + sheen + shimmer + count-up, matching main app v183 dashboard),
     scroll-reveal pledge cards, animated unlock sequence, reduced-motion safe.
     ALL v9 logic preserved: LZString fragment payload, PIN gate, tiered/compound
     interest parity, 450-day filter, UPI deep links, WhatsApp UTR confirmation. -->
<title>📘 Customer Passbook</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@400;500;600;700;800&family=DM+Serif+Display&family=Noto+Sans+Tamil:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
  :root{
    --gold:#C9A84C; --gold-lt:#E8C97A; --gold-deep:#9A7A30;
    --ink:#1A1209; --bg:#0F0C06;
    --card:#FFFEFA; --green:#1A7A3C; --red:#C0392B; --amber:#B8860B;
    --blue:#1A4A8C;
    --ease-out:cubic-bezier(.22,1,.36,1);
    --ease-spring:cubic-bezier(.22,.68,0,1.3);
  }
  *{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
  html{scroll-behavior:smooth;}
  body{
    font-family:'Outfit','Noto Sans Tamil','Segoe UI','Nirmala UI',Arial,sans-serif;
    background:#0F0C06;
    min-height:100vh;color:var(--ink);padding:14px 12px 40px;
    position:relative;overflow-x:hidden;
  }
  /* ── Aurora mesh backdrop ── */
  .aurora{position:fixed;inset:0;z-index:0;pointer-events:none;overflow:hidden;}
  .aurora::before,.aurora::after{
    content:'';position:absolute;width:70vmax;height:70vmax;border-radius:50%;
    filter:blur(90px);opacity:.5;will-change:transform;
  }
  .aurora::before{
    background:radial-gradient(circle,rgba(201,168,76,.32) 0%,transparent 62%);
    top:-30vmax;left:-18vmax;animation:drift1 22s ease-in-out infinite alternate;
  }
  .aurora::after{
    background:radial-gradient(circle,rgba(26,74,60,.45) 0%,transparent 62%);
    bottom:-32vmax;right:-20vmax;animation:drift2 26s ease-in-out infinite alternate;
  }
  @keyframes drift1{from{transform:translate(0,0) scale(1)}to{transform:translate(9vmax,7vmax) scale(1.12)}}
  @keyframes drift2{from{transform:translate(0,0) scale(1.05)}to{transform:translate(-8vmax,-6vmax) scale(1)}}
  .wrap{max-width:460px;margin:0 auto;position:relative;z-index:1;}

  /* ── Motion primitives ── */
  @keyframes fadeUp{from{opacity:0;transform:translateY(14px)}to{opacity:1;transform:none}}
  @keyframes cardIn{from{opacity:0;transform:translateY(20px) scale(.96)}to{opacity:1;transform:none}}
  @keyframes kpiIn{from{opacity:0;transform:translateY(22px) scale(.93)}to{opacity:1;transform:none}}
  @keyframes shake{0%,100%{transform:translateX(0)}20%,60%{transform:translateX(-8px)}40%,80%{transform:translateX(8px)}}
  @keyframes popIn{0%{opacity:0;transform:scale(.6)}70%{transform:scale(1.06)}100%{opacity:1;transform:scale(1)}}
  @keyframes pulse{0%{box-shadow:0 0 0 0 rgba(102,187,106,.5)}100%{box-shadow:0 0 0 8px rgba(102,187,106,0)}}
  @keyframes gateOut{to{opacity:0;transform:translateY(-16px) scale(.97);}}
  @keyframes sweep{from{background-position:250% center}to{background-position:-250% center}}
  @keyframes ringDash{from{stroke-dashoffset:var(--ring-c)}to{stroke-dashoffset:var(--ring-off)}}
  @keyframes badgeGlow{0%,100%{box-shadow:0 0 0 0 rgba(192,57,43,.35)}50%{box-shadow:0 0 0 6px rgba(192,57,43,0)}}

  /* ── Header ── */
  .hdr{text-align:center;padding:18px 10px 14px;animation:fadeUp .5s var(--ease-out) both;}
  .hdr .shop{
    font-family:'DM Serif Display','Noto Sans Tamil',serif;
    font-size:22px;font-weight:400;color:var(--gold-lt);letter-spacing:.3px;
    background:linear-gradient(90deg,#E8C97A 0%,#FFF3CE 50%,#C9A84C 100%);
    -webkit-background-clip:text;background-clip:text;-webkit-text-fill-color:transparent;
  }
  .hdr .shopTa{font-family:'Noto Sans Tamil',sans-serif;font-size:14px;font-weight:700;color:rgba(232,201,122,.75);margin-top:2px;}
  .hdr .tag{display:inline-flex;align-items:center;gap:6px;margin-top:9px;font-size:11px;color:rgba(232,201,122,.65);background:rgba(255,255,255,.05);border:1px solid rgba(232,201,122,.2);border-radius:20px;padding:5px 13px;backdrop-filter:blur(6px);-webkit-backdrop-filter:blur(6px);}
  .hdr .tag .dot{width:6px;height:6px;border-radius:50%;background:#66BB6A;animation:pulse 1.8s ease-out infinite;}

  /* ── Language toggle ── */
  .langbar{display:flex;justify-content:center;margin-bottom:10px;animation:fadeUp .4s var(--ease-out) both;}
  .langbar button{background:rgba(255,255,255,.06);border:1px solid rgba(232,201,122,.25);color:rgba(232,201,122,.8);font-family:inherit;font-size:11px;font-weight:700;padding:6px 15px;cursor:pointer;transition:background .2s,color .2s,transform .15s;}
  .langbar button:active{transform:scale(.95);}
  .langbar button:first-child{border-radius:16px 0 0 16px;}
  .langbar button:last-child{border-radius:0 16px 16px 0;border-left:none;}
  .langbar button.on{background:linear-gradient(135deg,var(--gold),var(--gold-deep));color:#1A1209;border-color:var(--gold);box-shadow:0 3px 12px rgba(201,168,76,.35);}

  /* ── PIN gate ── */
  .gate{
    background:linear-gradient(160deg,#FFFEFA 0%,#FBF5E6 100%);
    border-radius:20px;padding:28px 22px;text-align:center;
    box-shadow:0 20px 50px rgba(0,0,0,.5),inset 0 1px 0 rgba(255,255,255,.9);
    animation:cardIn .5s var(--ease-out) both;position:relative;overflow:hidden;
  }
  .gate::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;background:linear-gradient(90deg,var(--gold),#F5E3A8,var(--gold));}
  .gate.leaving{animation:gateOut .38s var(--ease-out) forwards;}
  .gate .lock{font-size:40px;animation:popIn .55s var(--ease-out) .1s both;}
  .gate h2{font-size:16px;font-weight:800;color:#2C1F0A;margin:10px 0 4px;}
  .gate p{font-size:11.5px;color:#8A7350;line-height:1.55;margin-bottom:16px;}
  .gate .cn{font-size:13.5px;font-weight:800;color:var(--blue);margin-bottom:14px;}
  .pinrow{display:flex;gap:8px;justify-content:center;margin-bottom:14px;}
  .pinrow input{width:100%;max-width:200px;text-align:center;font-family:monospace;font-size:24px;font-weight:800;letter-spacing:8px;padding:11px 6px;border:2px solid #E4D8B8;border-radius:13px;background:#FFFDF4;color:#2C1F0A;outline:none;transition:border-color .2s,box-shadow .2s;}
  .pinrow input:focus{border-color:var(--gold);box-shadow:0 0 0 4px rgba(201,168,76,.18);}
  .gate.err .pinrow{animation:shake .4s ease;}
  .gate .errmsg{font-size:11px;color:var(--red);font-weight:700;min-height:16px;margin-bottom:8px;}
  .gate button{width:100%;max-width:220px;padding:13px;border:none;border-radius:13px;background:linear-gradient(135deg,#1A4A8C,#0F2E5E);color:#fff;font-family:inherit;font-size:14px;font-weight:800;cursor:pointer;transition:transform .18s var(--ease-spring),filter .15s,box-shadow .2s;box-shadow:0 8px 22px rgba(26,74,140,.35);}
  .gate button:hover{filter:brightness(1.1);box-shadow:0 12px 28px rgba(26,74,140,.45);}
  .gate button:active{transform:scale(.96);}

  /* ── Passbook body ── */
  .book{display:none;}

  /* ── Summary hero (name + as-of) ── */
  .sumhero{
    background:linear-gradient(135deg,#16331F 0%,#0F1A10 60%,#2C1F0A 100%);
    border:1px solid rgba(232,201,122,.25);border-radius:18px;padding:15px 16px;
    margin-bottom:12px;animation:kpiIn .55s var(--ease-out) both;
    box-shadow:0 12px 36px rgba(0,0,0,.4),inset 0 1px 0 rgba(255,255,255,.08);
    display:flex;align-items:center;gap:12px;position:relative;overflow:hidden;
  }
  .sumhero::before{content:'';position:absolute;top:-55%;right:-14%;width:130px;height:130px;background:rgba(232,201,122,.08);border-radius:50%;pointer-events:none;}
  .sumhero .av{width:46px;height:46px;border-radius:50%;background:linear-gradient(135deg,#C9A84C,#9A7A30);display:flex;align-items:center;justify-content:center;font-weight:800;color:#1A1209;font-size:16px;flex-shrink:0;animation:popIn .5s var(--ease-out) .12s both;box-shadow:0 4px 14px rgba(201,168,76,.4),inset 0 1px 0 rgba(255,255,255,.35);}
  .sumhero .nm{font-size:15.5px;font-weight:800;color:var(--gold-lt);letter-spacing:.2px;}
  .sumhero .asof{font-size:10px;color:rgba(232,201,122,.55);margin-top:2px;}

  /* ── ANIMATED KPI CARDS (main-app v183 dashboard parity) ── */
  .kpigrid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:9px;margin-bottom:14px;}
  .kpi{
    border-radius:16px;padding:13px 11px 12px;color:#fff;position:relative;overflow:hidden;
    user-select:none;cursor:default;border:1px solid rgba(255,255,255,.08);
    transition:transform .22s var(--ease-spring),box-shadow .22s;
    animation:kpiIn .55s var(--ease-out) both;
    backdrop-filter:saturate(150%);-webkit-backdrop-filter:saturate(150%);
  }
  .kpi:nth-child(1){animation-delay:.06s;background:linear-gradient(135deg,#1A7A3C 0%,#0F5C2A 100%);box-shadow:0 10px 26px rgba(15,92,42,.42);}
  .kpi:nth-child(2){animation-delay:.14s;background:linear-gradient(135deg,#C9A84C 0%,#8A6A20 100%);box-shadow:0 10px 26px rgba(154,122,48,.45);}
  .kpi:nth-child(3){animation-delay:.22s;background:linear-gradient(135deg,#1A4A8C 0%,#0F2E5E 100%);box-shadow:0 10px 26px rgba(15,46,94,.45);}
  /* Big decorative orb top-right */
  .kpi::before{content:'';position:absolute;top:-45%;right:-22%;width:92px;height:92px;background:rgba(255,255,255,.10);border-radius:50%;pointer-events:none;transition:transform .45s var(--ease-out);}
  /* Small orb bottom-left */
  .kpi::after{content:'';position:absolute;bottom:-42%;left:-14%;width:66px;height:66px;background:rgba(255,255,255,.06);border-radius:50%;pointer-events:none;transition:transform .45s var(--ease-out);}
  .kpi:hover,.kpi:active{transform:translateY(-5px) scale(1.03);box-shadow:0 18px 40px rgba(0,0,0,.4);}
  .kpi:hover::before{transform:scale(1.4) translate(8px,-8px);}
  .kpi:hover::after{transform:scale(1.5) translate(-6px,6px);}
  /* Glassmorphic sheen */
  .kpi .sheen{position:absolute;inset:0;pointer-events:none;z-index:0;border-radius:inherit;background:linear-gradient(135deg,rgba(255,255,255,.24) 0%,rgba(255,255,255,.06) 38%,rgba(255,255,255,0) 62%);box-shadow:inset 0 1px 0 rgba(255,255,255,.3),inset 0 -14px 22px rgba(0,0,0,.12);}
  .kpi .sheen::before{content:'';position:absolute;top:0;left:9%;right:9%;height:1px;background:linear-gradient(90deg,transparent,rgba(255,255,255,.6),transparent);}
  /* Hover shimmer sweep */
  .kpi .shimmer{position:absolute;inset:0;pointer-events:none;z-index:0;background:linear-gradient(105deg,transparent 35%,rgba(255,255,255,.14) 50%,transparent 65%);background-size:250% 100%;background-position:250% center;opacity:0;transition:opacity .2s;}
  .kpi:hover .shimmer{opacity:1;animation:sweep .55s ease forwards;}
  .kpi>*:not(.sheen):not(.shimmer){position:relative;z-index:1;}
  .kpi .kico{font-size:15px;background:rgba(255,255,255,.16);border:1px solid rgba(255,255,255,.14);width:29px;height:29px;border-radius:9px;display:flex;align-items:center;justify-content:center;margin-bottom:8px;transition:transform .22s var(--ease-out);}
  .kpi:hover .kico{transform:scale(1.16) rotate(-6deg);}
  .kpi .kval{font-size:19px;font-weight:800;letter-spacing:-.5px;line-height:1;font-variant-numeric:tabular-nums;}
  .kpi .klab{font-size:8px;font-weight:700;letter-spacing:.7px;opacity:.8;text-transform:uppercase;margin-top:5px;}

  .stale{background:#FFF3CD;border:1px solid #F5D77E;border-radius:12px;padding:10px 13px;font-size:11px;color:#7A5C00;line-height:1.5;margin-bottom:12px;animation:cardIn .45s var(--ease-out) .05s both;}

  /* ── Pledge cards ── */
  .pcard{
    background:var(--card);border-radius:18px;padding:15px 15px 13px;margin-bottom:12px;
    box-shadow:0 10px 30px rgba(0,0,0,.38),inset 0 1px 0 rgba(255,255,255,.85);
    position:relative;overflow:hidden;
    opacity:0;transform:translateY(22px) scale(.97);
    transition:opacity .55s var(--ease-out),transform .55s var(--ease-out),box-shadow .25s;
  }
  .pcard.vis{opacity:1;transform:none;}
  .pcard:hover{box-shadow:0 16px 40px rgba(0,0,0,.45),inset 0 1px 0 rgba(255,255,255,.85);}
  .pcard::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;background:linear-gradient(90deg,var(--gold),#F5E3A8,var(--gold));background-size:200% 100%;animation:sweep 5s linear infinite;}
  .pcard .top{display:flex;justify-content:space-between;align-items:flex-start;gap:8px;margin-bottom:8px;}
  .pcard .bill{font-size:10px;color:#9A7A30;font-weight:700;letter-spacing:.5px;}
  .pcard .item{font-size:13.5px;font-weight:800;color:#2C1F0A;margin-top:1px;line-height:1.35;}
  .badge{font-size:9px;font-weight:800;border-radius:14px;padding:4px 9px;white-space:nowrap;flex-shrink:0;}
  .badge.ok{background:#EBF7EF;color:var(--green);border:1px solid #BFE3CB;}
  .badge.due{background:#FDECEA;color:var(--red);border:1px solid #F4C2BC;animation:popIn .4s ease both,badgeGlow 2.2s ease-in-out 1s infinite;}
  .kv{display:grid;grid-template-columns:1fr 1fr;gap:6px 10px;font-size:11px;margin-bottom:9px;}
  .kv .k{color:#9A8A60;font-size:9.5px;text-transform:uppercase;letter-spacing:.3px;}
  .kv .v{font-weight:700;color:#3D2B0F;margin-top:1px;}
  .duebar{background:linear-gradient(135deg,#FFF8E1,#FFF3CD);border:1.5px solid #F0DA9A;border-radius:13px;padding:10px 13px;display:flex;justify-content:space-between;align-items:center;margin-bottom:9px;}
  .duebar .l{font-size:10px;color:#8A6D00;font-weight:700;}
  .duebar .v{font-size:17px;font-weight:800;color:#5C4A1E;font-variant-numeric:tabular-nums;}
  .duebar.zero{background:#EBF7EF;border-color:#BFE3CB;}
  .duebar.zero .l{color:var(--green);}
  .duebar.zero .v{color:var(--green);font-size:13px;}
  .mnote{font-size:9.5px;color:#9A8A60;line-height:1.5;margin-bottom:9px;}

  /* Elapsed ring (SVG progress toward due date) */
  .ering{display:flex;align-items:center;gap:6px;}
  .ering svg{width:34px;height:34px;flex-shrink:0;transform:rotate(-90deg);}
  .ering circle{fill:none;stroke-width:3.4;}
  .ering .bgc{stroke:#F0E8D2;}
  .ering .fgc{stroke:var(--gold);stroke-linecap:round;stroke-dasharray:var(--ring-c);stroke-dashoffset:var(--ring-off);animation:ringDash 1.1s var(--ease-out) .3s both;}
  .ering .fgc.hot{stroke:var(--red);}
  .ering .etxt{line-height:1.3;}

  /* pay row */
  .payrow{border-top:1px dashed #E4D8B8;padding-top:10px;margin-top:2px;}
  .payrow .pl{font-size:9.5px;font-weight:800;color:#8A7350;text-transform:uppercase;letter-spacing:.5px;margin-bottom:6px;}
  .payamt{display:flex;align-items:center;gap:7px;margin-bottom:7px;}
  .payamt span{font-size:12px;font-weight:800;color:#5C4A1E;}
  .payamt input{flex:1;min-width:0;padding:8px 10px;border:1.5px solid #E4D8B8;border-radius:10px;font-family:inherit;font-size:14px;font-weight:800;color:#2C1F0A;background:#FFFDF4;outline:none;transition:border-color .2s,box-shadow .2s;}
  .payamt input:focus{border-color:var(--gold);box-shadow:0 0 0 3px rgba(201,168,76,.16);}
  .paybtns{display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:5px;}
  .paybtns a{display:block;text-align:center;text-decoration:none;font-size:9px;font-weight:800;padding:9px 2px;border-radius:10px;border:1px solid #ddd;background:#fff;transition:transform .15s var(--ease-spring),box-shadow .15s;}
  .paybtns a:hover{box-shadow:0 4px 12px rgba(0,0,0,.1);transform:translateY(-2px);}
  .paybtns a:active{transform:scale(.94);}
  .paybtns .gp{color:#1a73e8;} .paybtns .pp{color:#5f259f;} .paybtns .pt{color:#00baf2;} .paybtns .up{color:#3D2B0F;border-color:#E4D8B8;background:#FFF8E8;}

  /* payment history */
  .hist{border-top:1px dashed #E4D8B8;margin-top:10px;padding-top:8px;}
  .hist summary{font-size:10.5px;font-weight:800;color:var(--blue);cursor:pointer;list-style:none;display:flex;align-items:center;gap:5px;user-select:none;}
  .hist summary::before{content:'▸';transition:transform .2s;}
  .hist[open] summary::before{transform:rotate(90deg);}
  .hist table{width:100%;border-collapse:collapse;margin-top:7px;font-size:10.5px;}
  .hist td{padding:5px 4px;border-bottom:1px dotted #EEE4CC;}
  .hist td:last-child{text-align:right;font-weight:800;color:var(--green);}
  .hist .hk{font-size:8.5px;background:#F2ECDC;color:#8A7350;border-radius:8px;padding:1px 6px;font-weight:700;}

  /* closed pledges */
  .sect-title{font-size:11px;font-weight:800;color:rgba(232,201,122,.85);text-transform:uppercase;letter-spacing:.7px;margin:16px 2px 8px;animation:fadeUp .4s var(--ease-out) both;}
  .ccard{background:rgba(255,254,250,.94);border-radius:14px;padding:11px 13px;margin-bottom:8px;display:flex;justify-content:space-between;align-items:center;gap:8px;opacity:0;transform:translateY(16px);transition:opacity .5s var(--ease-out),transform .5s var(--ease-out);}
  .ccard.vis{opacity:1;transform:none;}
  .ccard .ci{min-width:0;}
  .ccard .cb{font-size:9.5px;color:#9A7A30;font-weight:700;}
  .ccard .cn2{font-size:12px;font-weight:800;color:#2C1F0A;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
  .ccard .cd{font-size:9.5px;color:#8A8A8A;margin-top:1px;}
  .ccard .cst{font-size:9px;font-weight:800;border-radius:12px;padding:4px 9px;flex-shrink:0;background:#EBF7EF;color:var(--green);}
  .ccard .cst.fc{background:#FDECEA;color:var(--red);}

  /* footer */
  .foot{text-align:center;margin-top:18px;animation:fadeUp .5s var(--ease-out) both;}
  .callbtn{display:inline-flex;align-items:center;gap:7px;background:rgba(255,255,255,.07);border:1px solid rgba(232,201,122,.3);color:var(--gold-lt);border-radius:24px;padding:10px 21px;font-size:12.5px;font-weight:800;text-decoration:none;transition:transform .18s var(--ease-spring),background .2s;backdrop-filter:blur(6px);-webkit-backdrop-filter:blur(6px);}
  .callbtn:hover{background:rgba(232,201,122,.14);}
  .callbtn:active{transform:scale(.95);}
  .foot .addr{font-size:10px;color:rgba(232,201,122,.5);margin-top:10px;line-height:1.5;}
  .foot .note{font-size:9px;color:rgba(232,201,122,.35);margin-top:12px;line-height:1.6;}
  .badlink{background:var(--card);border-radius:16px;padding:26px 20px;text-align:center;font-size:13px;color:#8A7350;line-height:1.6;box-shadow:0 12px 32px rgba(0,0,0,.4);}

  /* ── Reduced motion ── */
  @media (prefers-reduced-motion: reduce){
    *,*::before,*::after{animation-duration:.001s !important;animation-iteration-count:1 !important;transition-duration:.001s !important;}
    .pcard,.ccard{opacity:1;transform:none;}
  }
</style>
</head>
<body>
<div class="aurora"></div>
<div class="wrap">
  <div class="langbar"><button id="lang-en" class="on" onclick="setLang('en')">English</button><button id="lang-ta" onclick="setLang('ta')">தமிழ்</button></div>
  <div class="hdr">
    <div class="shop" id="h-shop">📘</div>
    <div class="shopTa" id="h-shopta" style="display:none;"></div>
    <div class="tag"><span class="dot"></span><span data-i="live">Live dues — calculated fresh every time you open this</span></div>
  </div>

  <!-- PIN GATE -->
  <div class="gate" id="gate">
    <div class="lock">🔐</div>
    <h2 data-i="gt">Enter your PIN</h2>
    <div class="cn" id="g-cn"></div>
    <p data-i="gp">This passbook is protected. Enter the PIN given to you by the shop.</p>
    <div class="pinrow"><input id="pin" type="password" inputmode="numeric" autocomplete="off" maxlength="12" placeholder="••••" onkeydown="if(event.key==='Enter')unlock()"></div>
    <div class="errmsg" id="g-err"></div>
    <button onclick="unlock()" data-i="gb">🔓 Unlock Passbook</button>
  </div>

  <!-- PASSBOOK -->
  <div class="book" id="book"></div>

  <div class="foot" id="foot" style="display:none;"></div>
</div>

<script>
var LZString=function(){var r=String.fromCharCode,o="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=",n="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+-$",e={};function t(r,o){if(!e[r]){e[r]={};for(var n=0;n<r.length;n++)e[r][r.charAt(n)]=n}return e[r][o]}var i={compressToBase64:function(r){if(null==r)return"";var n=i._compress(r,6,function(r){return o.charAt(r)});switch(n.length%4){default:case 0:return n;case 1:return n+"===";case 2:return n+"==";case 3:return n+"="}},decompressFromBase64:function(r){return null==r?"":""==r?null:i._decompress(r.length,32,function(n){return t(o,r.charAt(n))})},compressToUTF16:function(o){return null==o?"":i._compress(o,15,function(o){return r(o+32)})+" "},decompressFromUTF16:function(r){return null==r?"":""==r?null:i._decompress(r.length,16384,function(o){return r.charCodeAt(o)-32})},compressToUint8Array:function(r){for(var o=i.compress(r),n=new Uint8Array(2*o.length),e=0,t=o.length;e<t;e++){var s=o.charCodeAt(e);n[2*e]=s>>>8,n[2*e+1]=s%256}return n},decompressFromUint8Array:function(o){if(null==o)return i.decompress(o);for(var n=new Array(o.length/2),e=0,t=n.length;e<t;e++)n[e]=256*o[2*e]+o[2*e+1];var s=[];return n.forEach(function(o){s.push(r(o))}),i.decompress(s.join(""))},compressToEncodedURIComponent:function(r){return null==r?"":i._compress(r,6,function(r){return n.charAt(r)})},decompressFromEncodedURIComponent:function(r){return null==r?"":""==r?null:(r=r.replace(/ /g,"+"),i._decompress(r.length,32,function(o){return t(n,r.charAt(o))}))},compress:function(o){return i._compress(o,16,function(o){return r(o)})},_compress:function(r,o,n){if(null==r)return"";var e,t,i,s={},u={},a="",p="",c="",l=2,f=3,h=2,d=[],m=0,v=0;for(i=0;i<r.length;i+=1)if(a=r.charAt(i),Object.prototype.hasOwnProperty.call(s,a)||(s[a]=f++,u[a]=!0),p=c+a,Object.prototype.hasOwnProperty.call(s,p))c=p;else{if(Object.prototype.hasOwnProperty.call(u,c)){if(c.charCodeAt(0)<256){for(e=0;e<h;e++)m<<=1,v==o-1?(v=0,d.push(n(m)),m=0):v++;for(t=c.charCodeAt(0),e=0;e<8;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1}else{for(t=1,e=0;e<h;e++)m=m<<1|t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t=0;for(t=c.charCodeAt(0),e=0;e<16;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1}0==--l&&(l=Math.pow(2,h),h++),delete u[c]}else for(t=s[c],e=0;e<h;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1;0==--l&&(l=Math.pow(2,h),h++),s[p]=f++,c=String(a)}if(""!==c){if(Object.prototype.hasOwnProperty.call(u,c)){if(c.charCodeAt(0)<256){for(e=0;e<h;e++)m<<=1,v==o-1?(v=0,d.push(n(m)),m=0):v++;for(t=c.charCodeAt(0),e=0;e<8;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1}else{for(t=1,e=0;e<h;e++)m=m<<1|t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t=0;for(t=c.charCodeAt(0),e=0;e<16;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1}0==--l&&(l=Math.pow(2,h),h++),delete u[c]}else for(t=s[c],e=0;e<h;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1;0==--l&&(l=Math.pow(2,h),h++)}for(t=2,e=0;e<h;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1;for(;;){if(m<<=1,v==o-1){d.push(n(m));break}v++}return d.join("")},decompress:function(r){return null==r?"":""==r?null:i._decompress(r.length,32768,function(o){return r.charCodeAt(o)})},_decompress:function(o,n,e){var t,i,s,u,a,p,c,l=[],f=4,h=4,d=3,m="",v=[],g={val:e(0),position:n,index:1};for(t=0;t<3;t+=1)l[t]=t;for(s=0,a=Math.pow(2,2),p=1;p!=a;)u=g.val&g.position,g.position>>=1,0==g.position&&(g.position=n,g.val=e(g.index++)),s|=(u>0?1:0)*p,p<<=1;switch(s){case 0:for(s=0,a=Math.pow(2,8),p=1;p!=a;)u=g.val&g.position,g.position>>=1,0==g.position&&(g.position=n,g.val=e(g.index++)),s|=(u>0?1:0)*p,p<<=1;c=r(s);break;case 1:for(s=0,a=Math.pow(2,16),p=1;p!=a;)u=g.val&g.position,g.position>>=1,0==g.position&&(g.position=n,g.val=e(g.index++)),s|=(u>0?1:0)*p,p<<=1;c=r(s);break;case 2:return""}for(l[3]=c,i=c,v.push(c);;){if(g.index>o)return"";for(s=0,a=Math.pow(2,d),p=1;p!=a;)u=g.val&g.position,g.position>>=1,0==g.position&&(g.position=n,g.val=e(g.index++)),s|=(u>0?1:0)*p,p<<=1;switch(c=s){case 0:for(s=0,a=Math.pow(2,8),p=1;p!=a;)u=g.val&g.position,g.position>>=1,0==g.position&&(g.position=n,g.val=e(g.index++)),s|=(u>0?1:0)*p,p<<=1;l[h++]=r(s),c=h-1,f--;break;case 1:for(s=0,a=Math.pow(2,16),p=1;p!=a;)u=g.val&g.position,g.position>>=1,0==g.position&&(g.position=n,g.val=e(g.index++)),s|=(u>0?1:0)*p,p<<=1;l[h++]=r(s),c=h-1,f--;break;case 2:return v.join("")}if(0==f&&(f=Math.pow(2,d),d++),l[c])m=l[c];else{if(c!==h)return null;m=i+i.charAt(0)}v.push(m),l[h++]=i+m.charAt(0),i=m,0==--f&&(f=Math.pow(2,d),d++)}}};return i}();"function"==typeof define&&define.amd?define(function(){return LZString}):"undefined"!=typeof module&&null!=module?module.exports=LZString:"undefined"!=typeof angular&&null!=angular&&angular.module("LZString",[]).factory("LZString",function(){return LZString});
</script>
<script>
'use strict';
// ═══════════════════════════════════════════════════════════════════════════
// Customer Passbook Viewer v10 — Sivaji Bank Pawnshop Manager
// Data arrives compressed in the URL fragment (#...) — nothing is ever sent
// to any server. PIN gate is a privacy speed-bump, matching the app's model.
// Supports payload v1 (active pledges only) and v2 (+ payment history,
// closed pledges, UPI Pay-Now, shop address).
// v10: latest-gen UI — animated KPI cards (count-up + orbs + sheen + shimmer,
// dashboard parity with main app v183), elapsed progress ring, scroll-reveal
// cards, animated unlock. Calculation engine unchanged from v9.
// ═══════════════════════════════════════════════════════════════════════════
let P = null;          // decoded payload
let LANG = localStorage.getItem('pb_lang') || 'en';
let FIRST_RENDER = true;   // count-up runs only on the first render, not on language toggle

const I18N = {
  live:{en:'Live dues — calculated fresh every time you open this', ta:'நேரடி நிலுவை — ஒவ்வொரு முறையும் புதிதாக கணக்கிடப்படுகிறது'},
  gt:{en:'Enter your PIN', ta:'உங்கள் PIN-ஐ உள்ளிடவும்'},
  gp:{en:'This passbook is protected. Enter the PIN given to you by the shop.', ta:'இந்த பாஸ்புக் பாதுகாக்கப்பட்டது. கடையில் வழங்கிய PIN-ஐ உள்ளிடவும்.'},
  gb:{en:'🔓 Unlock Passbook', ta:'🔓 பாஸ்புக்கைத் திற'},
  wrong:{en:'Wrong PIN — please try again', ta:'தவறான PIN — மீண்டும் முயற்சிக்கவும்'},
  active:{en:'Active', ta:'செயலில்'}, duetoday:{en:'Due Today', ta:'இன்று செலுத்த'}, principal:{en:'Principal', ta:'அசல்'},
  asof:{en:'Data as of', ta:'தரவு தேதி'},
  stale:{en:'⚠️ This passbook snapshot is #D days old. Recent payments or renewals may not be shown — ask the shop for a fresh link or card.', ta:'⚠️ இந்த பாஸ்புக் தரவு #D நாட்கள் பழையது. சமீபத்திய கட்டணங்கள் காட்டப்படாமல் இருக்கலாம் — புதிய இணைப்பு/கார்டு கேட்கவும்.'},
  pledged:{en:'Pledged on', ta:'அடகு தேதி'}, duedate:{en:'Due date', ta:'கெடு தேதி'},
  lastpay:{en:'Last payment', ta:'கடைசி கட்டணம்'}, rate:{en:'Interest rate', ta:'வட்டி விகிதம்'},
  outp:{en:'Loan balance', ta:'கடன் நிலுவை'}, intnow:{en:'Interest due now', ta:'இப்போதைய வட்டி'},
  elapsed:{en:'Time elapsed', ta:'கடந்த காலம்'}, etot:{en:'days total', ta:'மொத்த நாட்கள்'}, emo:{en:'month', ta:'மாதம்'}, emos:{en:'months', ta:'மாதம்'}, edy:{en:'day', ta:'நாள்'}, edys:{en:'days', ta:'நாள்'},
  totnow:{en:'Total to close today', ta:'இன்று முடிக்க மொத்தம்'},
  grace:{en:'Within first 35 days — 1st month interest was collected upfront. Nothing due right now.', ta:'முதல் 35 நாட்களுக்குள் — முதல் மாத வட்டி முன்பே பெறப்பட்டது. இப்போது எதுவும் இல்லை.'},
  months:{en:'#M month(s) interest pending beyond the upfront first month', ta:'முன்பணம் போக #M மாத வட்டி நிலுவையில் உள்ளது'},
  overdue:{en:'#D days past due date', ta:'கெடு தேதி கடந்து #D நாட்கள்'},
  ontrack:{en:'On track', ta:'சரியாக உள்ளது'},
  paynow:{en:'Pay from your phone', ta:'உங்கள் போனிலிருந்தே செலுத்துங்கள்'},
  payhint:{en:'Prefilled with total to close today — you can edit the amount', ta:'இன்று முடிக்க மொத்தத் தொகை நிரப்பப்பட்டுள்ளது — தொகையை மாற்றலாம்'},
  payamt:{en:'Amount ₹', ta:'தொகை ₹'},
  paynote:{en:'After paying, inform the shop so your receipt is recorded.', ta:'செலுத்திய பின், ரசீது பதிவு செய்ய கடைக்கு தெரிவிக்கவும்.'},
  cfT:{en:'✅ Already paid? Confirm to the shop', ta:'✅ செலுத்திவிட்டீர்களா? கடைக்கு உறுதிப்படுத்தவும்'},
  cfU:{en:'UTR / Reference no. (from your payment app)', ta:'UTR / குறிப்பு எண் (உங்கள் பேமெண்ட் ஆப்பில் இருந்து)'},
  cfB:{en:'📤 Send confirmation on WhatsApp', ta:'📤 வாட்ஸ்அப்பில் உறுதிப்படுத்து'},
  cfErr:{en:'Please enter the amount you paid', ta:'செலுத்திய தொகையை உள்ளிடவும்'},
  hist:{en:'Recent payments', ta:'சமீபத்திய கட்டணங்கள்'},
  histk:{i:{en:'Interest', ta:'வட்டி'}, p:{en:'Principal', ta:'அசல்'}, m:{en:'Int+Prin', ta:'வட்டி+அசல்'}},
  closed:{en:'✅ Recently closed pledges', ta:'✅ சமீபத்தில் முடிந்த அடகுகள்'},
  redeemed:{en:'Redeemed', ta:'மீட்கப்பட்டது'}, foreclosed:{en:'Settled', ta:'முடிக்கப்பட்டது'},
  call:{en:'📞 Call Shop', ta:'📞 கடையை அழை'},
  privacy:{en:'Your details live only inside this link — nothing is stored on any server. Keep the link and PIN private.', ta:'உங்கள் விவரங்கள் இந்த இணைப்பில் மட்டுமே உள்ளன — எந்த சர்வரிலும் சேமிக்கப்படவில்லை. இணைப்பையும் PIN-ஐயும் பாதுகாப்பாக வைக்கவும்.'},
  badlink:{en:'⚠️ This passbook link is incomplete or damaged.<br>Please ask the shop to share it again.', ta:'⚠️ இந்த பாஸ்புக் இணைப்பு முழுமையற்றது.<br>கடையில் மீண்டும் கேட்கவும்.'}
};
const T = (k) => (I18N[k] && (I18N[k][LANG] || I18N[k].en)) || k;

function setLang(l) {
  LANG = l; localStorage.setItem('pb_lang', l);
  document.getElementById('lang-en').classList.toggle('on', l==='en');
  document.getElementById('lang-ta').classList.toggle('on', l==='ta');
  document.querySelectorAll('[data-i]').forEach(el => { el.innerHTML = T(el.getAttribute('data-i')); });
  if (document.getElementById('book').style.display === 'block') renderBook();
}

// ── Date & money helpers (mirrors the shop app's exact rules) ──────────────
const fmtR   = v => '₹' + Math.round(v||0).toLocaleString('en-IN');
const fmtD   = d => { if(!d) return '—'; const p = d.split('-'); return p[2]+'/'+p[1]+'/'+p[0]; };
const todayS = () => { const n = new Date(); return n.getFullYear()+'-'+String(n.getMonth()+1).padStart(2,'0')+'-'+String(n.getDate()).padStart(2,'0'); };
const daysBetween = (d1,d2) => Math.max(0, Math.floor((new Date(d2) - new Date(d1)) / 86400000));
const REDUCED = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;

// Animated count-up (rAF, ease-out cubic). Skips animation on reduced motion
// or re-renders — jumps straight to the final formatted value.
function countUp(el, target, fmt, dur) {
  if (!el) return;
  if (REDUCED || !FIRST_RENDER) { el.textContent = fmt(target); return; }
  const t0 = performance.now(); dur = dur || 900;
  function tick(now) {
    const p = Math.min(1, (now - t0) / dur);
    const e = 1 - Math.pow(1 - p, 3);
    el.textContent = fmt(target * e);
    if (p < 1) requestAnimationFrame(tick); else el.textContent = fmt(target);
  }
  requestAnimationFrame(tick);
}

// Scroll-reveal for pledge/closed cards via IntersectionObserver, staggered.
function reveal() {
  const els = document.querySelectorAll('.pcard,.ccard');
  if (REDUCED || !('IntersectionObserver' in window)) { els.forEach(e=>e.classList.add('vis')); return; }
  const io = new IntersectionObserver((entries) => {
    entries.forEach(en => {
      if (en.isIntersecting) {
        const d = parseFloat(en.target.dataset.rd || 0);
        setTimeout(() => en.target.classList.add('vis'), d * 1000);
        io.unobserve(en.target);
      }
    });
  }, { threshold: 0.08 });
  els.forEach(e => io.observe(e));
}

// Elapsed time since pledge, in calendar months + leftover days
function elapsedMD(from, to) {
  const a = new Date(from + 'T00:00:00'), b = new Date(to + 'T00:00:00');
  if (isNaN(a) || isNaN(b) || b < a) return { m: 0, d: 0 };
  let m = (b.getFullYear() - a.getFullYear()) * 12 + (b.getMonth() - a.getMonth());
  let anchor = new Date(a); anchor.setMonth(a.getMonth() + m);
  if (anchor > b) { m--; anchor = new Date(a); anchor.setMonth(a.getMonth() + m); }
  const d = Math.round((b - anchor) / 86400000);
  return { m: Math.max(0, m), d: Math.max(0, d) };
}
function fmtElapsed(from, to) {
  const e = elapsedMD(from, to);
  const mTxt = e.m + ' ' + T(e.m === 1 ? 'emo' : 'emos');
  const dTxt = e.d + ' ' + T(e.d === 1 ? 'edy' : 'edys');
  if (e.m === 0) return dTxt;
  if (e.d === 0) return mTxt;
  return mTxt + ' ' + dTxt;
}

// Interest rule parity: month 1 collected upfront at pledge; grace to day 35;
// each further 30-day block (any part) counts as a full month.
function calcDue(it, asOf) {
  const days = daysBetween(it.lp || it.d, asOf);
  let interest = 0, em = 0;
  if (days > 35) {
    em = Math.ceil((days - 35) / 30);
    const r = it.r || 0, pr = it.pr || 0;
    if (it.ty === 'compound') {
      interest = pr * (Math.pow(1 + r/100, em) - 1);
    } else if (it.ty === 'tiered') {
      // SHOP RULE: the tier threshold counts CHARGEABLE months — the months
      // after the upfront-paid first month (mirrors the shop app's engine).
      const t = it.tr || 6, r2 = it.r2 || r;
      const m1 = Math.min(em, t), m2 = Math.max(0, em - t);
      interest = pr * (r/100) * m1 + pr * (r2/100) * m2;
    } else {
      interest = pr * (r/100) * em;
    }
  }
  return { days, extraMonths: em, interest, total: (it.pr||0) + interest };
}

function upiLink(scheme, amt, bill) {
  const q = 'pa=' + encodeURIComponent(P.upi.pa)
          + '&pn=' + encodeURIComponent(P.upi.pn || P.sn || '')
          + (amt > 0 ? '&am=' + encodeURIComponent(amt.toFixed(2)) : '')
          + '&cu=INR&tn=' + encodeURIComponent(('Pledge '+bill+' payment').slice(0,50));
  if (scheme === 'gpay')    return 'tez://upi/pay?' + q;
  if (scheme === 'phonepe') return 'phonepe://pay?' + q;
  if (scheme === 'paytm')   return 'paytmmp://pay?' + q;
  return 'upi://pay?' + q;
}
function payAmtChanged(idx) {
  const v = parseFloat(document.getElementById('pay-amt-'+idx).value) || 0;
  const it = P.p[idx];
  ['gpay','phonepe','paytm','upi'].forEach(s => {
    const a = document.getElementById('pay-'+s+'-'+idx);
    if (a) a.href = upiLink(s, v, it.b);
  });
}

// ── Boot: decode fragment ───────────────────────────────────────────────────
(function boot(){
  try {
    const frag = location.hash.replace(/^#/, '');
    if (!frag) throw 0;
    P = JSON.parse(LZString.decompressFromEncodedURIComponent(frag));
    if (!P || !Array.isArray(P.p)) throw 0;
  } catch(e) {
    document.getElementById('gate').outerHTML = '<div class="badlink" data-i="badlink">'+T('badlink')+'</div>';
    document.querySelector('.langbar').style.display='none';
    return;
  }
  document.getElementById('h-shop').textContent = '📘 ' + (P.sn || 'Passbook');
  if (P.st) { const e = document.getElementById('h-shopta'); e.textContent = P.st; e.style.display='block'; }
  document.getElementById('g-cn').textContent = P.cn || '';
  setLang(LANG);
  setTimeout(()=>document.getElementById('pin').focus(), 300);
})();

function unlock() {
  const gate = document.getElementById('gate');
  const val = (document.getElementById('pin').value || '').trim();
  if (!P) return;
  if (val !== String(P.sec||'')) {
    gate.classList.remove('err'); void gate.offsetWidth; gate.classList.add('err');
    document.getElementById('g-err').textContent = T('wrong');
    return;
  }
  // Animated unlock: gate glides out, then the book cascades in.
  const show = () => {
    gate.style.display = 'none';
    document.getElementById('book').style.display = 'block';
    document.getElementById('foot').style.display = 'block';
    renderBook();
  };
  if (REDUCED) { show(); }
  else { gate.classList.add('leaving'); setTimeout(show, 360); }
}

function renderBook() {
  const asOf = todayS();
  // Silently omit pledges older than 450 days (from pledge date). Recomputed on
  // every open, so a pledge that crosses the limit after the QR was printed
  // disappears automatically. Idempotent — safe on language-toggle re-render.
  P.p = (P.p || []).filter(it => !it.d || daysBetween(it.d, asOf) <= 450);
  const book = document.getElementById('book');
  const dues = P.p.map(it => calcDue(it, asOf));
  const totPr  = P.p.reduce((s,it) => s + (it.pr||0), 0);
  const totDue = dues.reduce((s,d) => s + d.total, 0);
  const initials = (P.cn||'?').trim().split(/\s+/).slice(0,2).map(w=>w[0]).join('').toUpperCase() || '?';
  const genAge = daysBetween(P.gen || asOf, asOf);

  let h = `
    <div class="sumhero">
      <div class="av">${initials}</div>
      <div><div class="nm">${esc(P.cn)}</div><div class="asof">${T('asof')}: ${fmtD(P.gen)} · ${fmtD(asOf)}</div></div>
    </div>
    <div class="kpigrid">
      <div class="kpi"><div class="sheen"></div><div class="shimmer"></div>
        <div class="kico">📜</div><div class="kval" id="kpi-active">0</div><div class="klab">${T('active')}</div></div>
      <div class="kpi"><div class="sheen"></div><div class="shimmer"></div>
        <div class="kico">💰</div><div class="kval" id="kpi-due">₹0</div><div class="klab">${T('duetoday')}</div></div>
      <div class="kpi"><div class="sheen"></div><div class="shimmer"></div>
        <div class="kico">🏦</div><div class="kval" id="kpi-pr">₹0</div><div class="klab">${T('principal')}</div></div>
    </div>`;

  if (genAge > 7) h += `<div class="stale">${T('stale').replace('#D', genAge)}</div>`;

  P.p.forEach((it, i) => {
    const d = dues[i];
    const overdueDays = it.dd ? daysBetween(it.dd, asOf) : 0;
    const isOver = it.dd && asOf > it.dd;
    // Elapsed progress ring: pledge date → due date (capped at 100%).
    const totalSpan = (it.d && it.dd) ? Math.max(1, daysBetween(it.d, it.dd)) : 0;
    const spent = it.d ? daysBetween(it.d, asOf) : 0;
    const pct = totalSpan ? Math.min(1, spent / totalSpan) : 0;
    const C = 2 * Math.PI * 14;   // r=14
    const off = C * (1 - pct);
    h += `
    <div class="pcard" data-rd="${(i*0.07).toFixed(2)}">
      <div class="top">
        <div><div class="bill">BILL ${esc(it.b)}</div><div class="item">${esc(it.it)||'—'}</div></div>
        ${isOver ? `<span class="badge due">⏰ ${T('overdue').replace('#D', overdueDays)}</span>` : `<span class="badge ok">✓ ${T('ontrack')}</span>`}
      </div>
      <div class="kv">
        <div><div class="k">${T('pledged')}</div><div class="v">${fmtD(it.d)}</div></div>
        <div><div class="k">${T('duedate')}</div><div class="v">${fmtD(it.dd)}</div></div>
        <div><div class="k">${T('lastpay')}</div><div class="v">${fmtD(it.lp)}</div></div>
        <div><div class="k">${T('elapsed')}</div>
          <div class="v ering">
            ${totalSpan ? `<svg viewBox="0 0 34 34" style="--ring-c:${C.toFixed(1)};--ring-off:${off.toFixed(1)};">
              <circle class="bgc" cx="17" cy="17" r="14"></circle>
              <circle class="fgc${pct>=1?' hot':''}" cx="17" cy="17" r="14"></circle>
            </svg>` : ''}
            <span class="etxt" style="color:#1A4A8C;">⏱ ${fmtElapsed(it.d, asOf)}<br><span style="font-size:9.5px;color:#8A7350;font-weight:700;">= ${daysBetween(it.d, asOf)} ${T('etot')}</span></span>
          </div></div>
        <div><div class="k">${T('outp')}</div><div class="v">${fmtR(it.pr)}</div></div>
        <div><div class="k">${T('intnow')}</div><div class="v" style="color:${d.interest>0?'#C0392B':'#1A7A3C'};">${fmtR(d.interest)}</div></div>
      </div>
      ${d.interest > 0
        ? `<div class="duebar"><span class="l">${T('totnow')}</span><span class="v">${fmtR(d.total)}</span></div>
           <div class="mnote">${T('months').replace('#M', d.extraMonths)}</div>`
        : `<div class="duebar zero"><span class="l">${T('grace')}</span><span class="v">✓</span></div>`}
      ${P.upi && P.upi.pa ? payBlock(i, it, d) : ''}
      ${it.pm && it.pm.length ? histBlock(it) : ''}
    </div>`;
  });

  if (P.cl && P.cl.length) {
    h += `<div class="sect-title">${T('closed')}</div>`;
    P.cl.forEach((c, i) => {
      h += `<div class="ccard" data-rd="${(i*0.06).toFixed(2)}">
        <div class="ci"><div class="cb">BILL ${esc(c.b)} · ${fmtR(c.a)}</div>
        <div class="cn2">${esc(c.it)||'—'}</div>
        <div class="cd">${fmtD(c.d)} → ${fmtD(c.cd)}</div></div>
        <span class="cst${c.fc?' fc':''}">${c.fc ? T('foreclosed') : T('redeemed')}</span>
      </div>`;
    });
  }
  book.innerHTML = h;

  // Animated KPI count-up (first unlock only; language toggle re-renders static)
  countUp(document.getElementById('kpi-active'), P.p.length, v => String(Math.round(v)), 650);
  countUp(document.getElementById('kpi-due'), totDue, fmtR, 950);
  countUp(document.getElementById('kpi-pr'), totPr, fmtR, 950);
  reveal();
  FIRST_RENDER = false;

  // footer
  let f = '';
  if (P.sp) f += `<a class="callbtn" href="tel:${esc(P.sp).replace(/[^\d+]/g,'')}">${T('call')} · ${esc(P.sp)}</a>`;
  if (P.ad) f += `<div class="addr">📍 ${esc(P.ad)}</div>`;
  f += `<div class="note">🔒 ${T('privacy')}<br><span style="opacity:.55;">viewer v10</span></div>`;
  document.getElementById('foot').innerHTML = f;
}

function payBlock(i, it, d) {
  // Default = Total to close today (principal + interest). Field stays editable.
  const def = d.interest > 0 ? Math.round(d.total) : '';
  return `
  <div class="payrow">
    <div class="pl">📲 ${T('paynow')}</div>
    <div class="payamt"><span>${T('payamt')}</span><input id="pay-amt-${i}" type="number" inputmode="numeric" min="1" value="${def}" oninput="payAmtChanged(${i})"></div>
    ${def !== '' ? `<div class="mnote" style="margin:0 0 7px;">💡 ${T('payhint')}</div>` : ''}
    <div class="paybtns">
      <a id="pay-gpay-${i}"    class="gp" href="${upiLink('gpay',    def||0, it.b)}">GPay</a>
      <a id="pay-phonepe-${i}" class="pp" href="${upiLink('phonepe', def||0, it.b)}">PhonePe</a>
      <a id="pay-paytm-${i}"   class="pt" href="${upiLink('paytm',   def||0, it.b)}">Paytm</a>
      <a id="pay-upi-${i}"     class="up" href="${upiLink('upi',     def||0, it.b)}">UPI</a>
    </div>
    <div class="mnote" style="margin:7px 0 0;">${T('paynote')}</div>
    ${P.sp ? `
    <div style="border-top:1px dashed #E4D8B8;margin-top:10px;padding-top:9px;">
      <div class="pl">${T('cfT')}</div>
      <input id="utr-${i}" type="text" autocomplete="off" maxlength="40" placeholder="${T('cfU')}"
        style="width:100%;padding:8px 10px;border:1.5px solid #E4D8B8;border-radius:9px;font-size:12px;font-weight:700;color:#2C1F0A;background:#FFFDF4;outline:none;margin-bottom:7px;box-sizing:border-box;font-family:inherit;">
      <a href="#" onclick="sendPayConfirm(${i});return false;"
        style="display:block;text-align:center;text-decoration:none;font-size:11.5px;font-weight:800;padding:11px 4px;border-radius:10px;background:linear-gradient(135deg,#1A7A3C,#0F5C2A);color:#fff;box-shadow:0 5px 14px rgba(15,92,42,.3);">
        ${T('cfB')}</a>
    </div>` : ''}
  </div>`;
}

// ── "I have paid" → WhatsApp confirmation to the shop ───────────────────────
function sendPayConfirm(i) {
  const it  = P.p[i];
  const amt = parseFloat(document.getElementById('pay-amt-' + i).value) || 0;
  if (amt <= 0) { alert(T('cfErr')); return; }
  const utr = (document.getElementById('utr-' + i).value || '').trim();
  let digits = String(P.sp || '').replace(/\D/g, '');
  if (digits.length === 10) digits = '91' + digits;
  if (!digits) return;
  const msg = (LANG === 'ta'
    ? '✅ கட்டணம் செலுத்தப்பட்டது\nபில்: ' + it.b +
      '\nபெயர்: ' + (P.cn || '') +
      '\nதொகை: ₹' + Math.round(amt).toLocaleString('en-IN') +
      (utr ? '\nUTR/குறிப்பு: ' + utr : '') +
      '\nதேதி: ' + fmtD(todayS()) +
      '\nரசீது பதிவு செய்யவும்.'
    : '✅ Payment done\nBill: ' + it.b +
      '\nName: ' + (P.cn || '') +
      '\nAmount: ₹' + Math.round(amt).toLocaleString('en-IN') +
      (utr ? '\nUTR/Ref: ' + utr : '') +
      '\nDate: ' + fmtD(todayS()) +
      '\nPlease record my receipt.');
  window.open('https://wa.me/' + digits + '?text=' + encodeURIComponent(msg), '_blank');
}

function histBlock(it) {
  const rows = it.pm.map(p => `<tr><td>${fmtD(p[0])}</td><td><span class="hk">${(I18N.histk[p[2]]&&(I18N.histk[p[2]][LANG]||I18N.histk[p[2]].en))||''}</span></td><td>${fmtR(p[1])}</td></tr>`).join('');
  return `<details class="hist"><summary>🧾 ${T('hist')} (${it.pm.length})</summary><table>${rows}</table></details>`;
}

function esc(s){ return String(s==null?'':s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;'); }
</script>
</body>
</html>
