<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="robots" content="noindex,nofollow">
<meta name="color-scheme" content="dark">
<meta name="theme-color" content="#140A06">
<meta http-equiv="Cache-Control" content="no-cache, must-revalidate">
<!-- PASSBOOK VIEWER v10 — redesigned UI, animated KPIs, a11y fixes.
     Interest engine, UPI links and WhatsApp confirmation unchanged from v9. -->
<title>📘 Customer Passbook</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Tamil:wght@400;500;600;700;800&family=DM+Serif+Display&family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">
<style>
@property --sheen{syntax:'<length>';inherits:false;initial-value:-140px;}
:root{
 --bg-0:#140A06;--bg-2:#1A0D08;--gold:#D9A93C;--gold-2:#F2D592;--gold-dim:rgba(217,169,60,.28);
 --maroon:#7A1226;--maroon-2:#A6203A;--paper:#FCF6E9;--ink:#2A1810;--muted:#8A6E52;
 --green:#2E9B57;--green-2:#7BD9A1;--red:#D9534F;--red-2:#F0918D;
 --glass:rgba(255,255,255,.055);--glass-line:rgba(232,200,116,.16);--r-lg:20px;--r-md:15px;
 --spring:cubic-bezier(.22,1,.36,1);
 --spring:linear(0,.006,.025 2.8%,.101 6.1%,.539 18.9%,.721 25.3%,.849 31.5%,.937 38.1%,.968 41.8%,.991 45.7%,1.006 50.1%,1.015 55%,1.017 63.9%,1.001);
 --ease:cubic-bezier(.4,0,.2,1);}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
html{-webkit-text-size-adjust:100%;}
body{font-family:'Inter','Noto Sans Tamil','Nirmala UI',Latha,system-ui,-apple-system,sans-serif;
 background:radial-gradient(120% 80% at 50% -10%,#4A1424 0%,transparent 60%),
  radial-gradient(90% 60% at 100% 100%,#2A1208 0%,transparent 55%),
  linear-gradient(170deg,var(--bg-0) 0%,var(--bg-2) 55%,#0E0705 100%);
 background-attachment:fixed;color:var(--paper);min-height:100dvh;
 padding:calc(14px + env(safe-area-inset-top)) calc(13px + env(safe-area-inset-right))
   calc(34px + env(safe-area-inset-bottom)) calc(13px + env(safe-area-inset-left));
 -webkit-font-smoothing:antialiased;}
.wrap{width:100%;max-width:460px;margin:0 auto;}
.ta{font-family:'Noto Sans Tamil','Nirmala UI',Latha,sans-serif;}
.num{font-variant-numeric:tabular-nums;}
:focus-visible{outline:2.5px solid var(--gold-2);outline-offset:3px;border-radius:6px;}
.rv{opacity:0;transform:translateY(18px) scale(.985);transition:opacity .6s var(--ease),transform .7s var(--spring);}
.rv.in{opacity:1;transform:none;}
@media (prefers-reduced-motion:reduce){*,*::before,*::after{animation-duration:.001ms!important;
 animation-iteration-count:1!important;transition-duration:.001ms!important;}.rv{opacity:1;transform:none;}}
.langbar{display:flex;justify-content:center;margin-bottom:12px;}
.langbar .seg{display:flex;gap:4px;background:rgba(0,0,0,.3);border:1px solid var(--glass-line);border-radius:22px;padding:4px;}
.langbar button{border:none;background:transparent;color:rgba(252,246,233,.62);cursor:pointer;font-family:inherit;
 font-size:11.5px;font-weight:700;padding:7px 18px;border-radius:18px;transition:color .25s var(--ease),background .3s var(--ease);}
.langbar button.on{background:linear-gradient(150deg,var(--gold),#B8860B);color:#2A1810;box-shadow:0 4px 12px -4px rgba(217,169,60,.7);}
.hdr{text-align:center;padding:4px 8px 16px;animation:riseIn .55s var(--spring) both;}
@keyframes riseIn{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:none}}
.hdr .shop{font-family:'DM Serif Display',serif;font-size:24px;color:var(--gold-2);line-height:1.15;}
.hdr .shopTa{font-size:13px;font-weight:600;color:rgba(242,213,146,.7);margin-top:3px;}
.hdr .tag{display:inline-flex;align-items:center;gap:7px;margin-top:11px;font-size:10.5px;color:rgba(252,246,233,.66);
 background:var(--glass);border:1px solid var(--glass-line);border-radius:20px;padding:5px 13px;line-height:1.4;text-align:left;}
.hdr .tag .dot{width:7px;height:7px;border-radius:50%;background:#66BB6A;flex-shrink:0;animation:ping 2.4s var(--ease) infinite;}
@keyframes ping{0%{box-shadow:0 0 0 0 rgba(102,187,106,.55)}70%{box-shadow:0 0 0 10px rgba(102,187,106,0)}100%{box-shadow:0 0 0 0 rgba(102,187,106,0)}}
.paper{background:var(--paper);border-radius:var(--r-lg);padding:5px;color:var(--ink);
 box-shadow:0 30px 70px -18px rgba(0,0,0,.8),0 0 0 1px var(--gold-dim);animation:riseIn .5s var(--spring) both;}
.paper>.in{border:1px solid rgba(184,134,11,.32);border-radius:14px;padding:24px 20px;text-align:center;position:relative;overflow:hidden;}
.kolam{height:7px;border-radius:4px;opacity:.45;background:repeating-linear-gradient(90deg,var(--gold) 0 5px,transparent 5px 11px);}
.seal{width:70px;height:70px;margin:16px auto 14px;border-radius:50%;position:relative;
 background:linear-gradient(145deg,var(--maroon-2),var(--maroon));display:grid;place-items:center;font-size:30px;
 box-shadow:0 10px 26px -6px rgba(122,18,38,.6),inset 0 1px 0 rgba(255,255,255,.18);}
.seal::after{content:'';position:absolute;inset:-7px;border-radius:50%;border:1.5px solid var(--gold-dim);animation:halo 3.4s ease-in-out infinite;}
@keyframes halo{0%,100%{transform:scale(1);opacity:.65}50%{transform:scale(1.09);opacity:.15}}
.gate h2{font-size:17px;font-weight:800;color:var(--ink);margin:6px 0 4px;}
.gate .cn{font-size:13.5px;font-weight:800;color:var(--maroon);margin-bottom:6px;}
.gate p{font-size:12px;color:var(--muted);line-height:1.6;margin-bottom:20px;}
.pins{display:flex;gap:11px;justify-content:center;}
.pins input{width:54px;height:64px;text-align:center;font-size:27px;font-weight:800;border:2px solid rgba(184,134,11,.4);
 border-radius:14px;background:#fff;color:var(--maroon);outline:none;font-family:'Inter',sans-serif;
 transition:border-color .2s var(--ease),box-shadow .2s var(--ease),transform .35s var(--spring);}
.pins input:focus{border-color:var(--maroon);box-shadow:0 0 0 4px rgba(122,18,38,.13);transform:translateY(-3px);}
.pins input.ok{border-color:var(--green);background:#F5FDF8;transform:scale(1.04);}
.pinlong{width:100%;max-width:230px;margin:0 auto;display:block;text-align:center;font-family:'Inter',monospace;
 font-size:22px;font-weight:800;letter-spacing:7px;padding:13px 10px;border:2px solid rgba(184,134,11,.4);
 border-radius:14px;background:#fff;color:var(--maroon);outline:none;}
.pinlong:focus{border-color:var(--maroon);box-shadow:0 0 0 4px rgba(122,18,38,.13);}
.shake{animation:shake .45s var(--ease);}
@keyframes shake{0%,100%{transform:translateX(0)}18%{transform:translateX(-10px)}36%{transform:translateX(10px)}56%{transform:translateX(-6px)}76%{transform:translateX(4px)}}
.errmsg{font-size:12px;color:var(--red);font-weight:700;min-height:18px;margin-top:11px;}
.gbtn{width:100%;max-width:230px;margin:10px auto 0;display:block;padding:14px;border:none;border-radius:13px;
 background:linear-gradient(140deg,var(--maroon-2),var(--maroon));color:#fff;font-family:inherit;font-size:14.5px;
 font-weight:800;cursor:pointer;box-shadow:0 14px 30px -14px rgba(122,18,38,.95);transition:transform .3s var(--spring);}
.gbtn:active{transform:scale(.975);}
.hint{font-size:10.5px;color:#A88A60;margin-top:17px;line-height:1.65;}
#fx{position:fixed;inset:0;z-index:200;display:none;place-items:center;background:rgba(14,7,5,.94);
 backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px);}
#fx.on{display:grid;}
#fx .rng{width:88px;height:88px;border-radius:50%;background:conic-gradient(from 0deg,transparent,var(--gold-2));
 -webkit-mask:radial-gradient(farthest-side,transparent calc(100% - 4px),#000 0);
 mask:radial-gradient(farthest-side,transparent calc(100% - 4px),#000 0);animation:spin .85s linear infinite;}
@keyframes spin{to{transform:rotate(1turn)}}
#fx .tick{position:absolute;font-size:42px;opacity:0;transform:scale(.3);}
#fx .tick.go{animation:pop .5s var(--spring) forwards;}
@keyframes pop{to{opacity:1;transform:scale(1)}}
#bar{position:fixed;left:0;right:0;top:0;z-index:120;padding:calc(9px + env(safe-area-inset-top)) 16px 9px;
 background:rgba(20,10,6,.82);backdrop-filter:blur(16px) saturate(1.5);-webkit-backdrop-filter:blur(16px) saturate(1.5);
 border-bottom:1px solid var(--glass-line);display:flex;justify-content:space-between;align-items:center;gap:12px;
 transform:translateY(-102%);transition:transform .42s var(--spring);}
#bar.on{transform:none;}
#bar .l{font-size:12.5px;font-weight:800;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
#bar .l small{display:block;font-size:9.5px;font-weight:600;color:rgba(252,246,233,.55);}
#bar .r{font-size:15px;font-weight:800;color:var(--gold-2);white-space:nowrap;}
.book{display:none;}
.hero{position:relative;border-radius:var(--r-lg);padding:18px 17px 16px;margin-bottom:12px;overflow:hidden;
 background:linear-gradient(150deg,var(--maroon-2) 0%,var(--maroon) 48%,#55091A 100%);
 box-shadow:0 24px 54px -20px rgba(122,18,38,.85),inset 0 1px 0 rgba(255,255,255,.14);}
.hero::before{content:'';position:absolute;inset:0;pointer-events:none;
 background:radial-gradient(70% 50% at 85% 0%,rgba(255,255,255,.14),transparent 70%);}
.hero .who{display:flex;align-items:center;gap:12px;position:relative;}
.hero .av{width:46px;height:46px;flex-shrink:0;border-radius:50%;display:grid;place-items:center;font-size:16px;
 font-weight:900;color:#2A1810;background:linear-gradient(140deg,var(--gold-2),var(--gold));
 box-shadow:0 6px 16px -6px rgba(0,0,0,.5),inset 0 1px 0 rgba(255,255,255,.5);}
.hero .nm{font-size:18px;font-weight:800;line-height:1.2;}
.hero .asof{font-size:10px;color:rgba(252,246,233,.62);margin-top:2px;}
.hero .odtag{margin-left:auto;flex-shrink:0;font-size:9px;font-weight:800;letter-spacing:.06em;padding:5px 10px;
 border-radius:20px;background:rgba(217,83,79,.28);border:1px solid rgba(240,145,141,.5);color:#FFD8D6;}
.hero .odtag.ok{background:rgba(255,255,255,.13);border-color:rgba(242,213,146,.3);color:var(--gold-2);}
.hero .grand{margin-top:16px;position:relative;}
.hero .grand .l{font-size:9px;font-weight:800;letter-spacing:.13em;color:var(--gold-2);opacity:.85;}
.hero .grand .v{font-family:'DM Serif Display',serif;font-size:clamp(30px,9.2vw,38px);line-height:1.05;margin-top:5px;
 text-shadow:0 2px 14px rgba(0,0,0,.28);}
.kpis{display:grid;grid-template-columns:1fr 1fr 1fr;gap:9px;margin-bottom:12px;}
.kpi{position:relative;overflow:hidden;border-radius:var(--r-md);padding:12px 9px;text-align:center;
 background:var(--glass);border:1px solid var(--glass-line);backdrop-filter:blur(9px);-webkit-backdrop-filter:blur(9px);
 transition:transform .34s var(--spring);}
.kpi::after{content:'';position:absolute;top:0;bottom:0;width:70px;pointer-events:none;left:var(--sheen);
 background:linear-gradient(100deg,transparent,rgba(255,255,255,.11),transparent);}
.kpi.lit::after{animation:sheen 1.15s var(--ease) forwards;}
@keyframes sheen{from{--sheen:-140px}to{--sheen:130%}}
.kpi:active{transform:scale(.97);}
.kpi .v{font-size:clamp(14px,4.3vw,17px);font-weight:800;color:var(--gold-2);line-height:1.15;}
.kpi.red .v{color:var(--red-2);}.kpi.green .v{color:var(--green-2);}
.kpi .l{font-size:8px;font-weight:800;letter-spacing:.06em;text-transform:uppercase;color:rgba(252,246,233,.62);margin-top:4px;line-height:1.35;}
.notice{border-radius:var(--r-md);padding:11px 13px;font-size:11px;line-height:1.6;font-weight:600;margin-bottom:12px;
 background:rgba(224,167,59,.13);border:1px solid rgba(224,167,59,.3);color:#F0CE8C;}
.pcard{background:var(--glass);border:1px solid var(--glass-line);border-radius:var(--r-lg);padding:15px;
 margin-bottom:12px;position:relative;overflow:hidden;backdrop-filter:blur(9px);-webkit-backdrop-filter:blur(9px);}
.pcard::before{content:'';position:absolute;top:0;left:0;right:0;height:2.5px;
 background:linear-gradient(90deg,var(--gold),#F5E3A8,var(--gold));opacity:.85;}
.pcard.over::before{background:linear-gradient(90deg,var(--red),#F0918D,var(--red));}
.pcard .top{display:flex;justify-content:space-between;align-items:flex-start;gap:10px;margin-bottom:11px;}
.pcard .bill{font-size:9.5px;font-weight:800;letter-spacing:.07em;color:var(--gold-2);opacity:.85;}
.pcard .item{font-size:15px;font-weight:800;margin-top:2px;line-height:1.3;}
.badge{font-size:9px;font-weight:800;border-radius:14px;padding:5px 10px;white-space:nowrap;flex-shrink:0;}
.badge.ok{background:rgba(46,155,87,.2);color:var(--green-2);border:1px solid rgba(123,217,161,.3);}
.badge.due{background:rgba(217,83,79,.2);color:var(--red-2);border:1px solid rgba(217,83,79,.4);}
.kv{display:grid;grid-template-columns:1fr 1fr;gap:11px 12px;margin-bottom:12px;}
.kv .k{font-size:9px;font-weight:800;letter-spacing:.05em;text-transform:uppercase;color:rgba(252,246,233,.62);}
.kv .val{font-size:13px;font-weight:700;margin-top:2px;}
.kv .val small{display:block;font-size:9.5px;font-weight:600;color:rgba(252,246,233,.62);margin-top:1px;}
.kv .val.hot{color:var(--red-2);}.kv .val.cool{color:var(--green-2);}
.duebar{border-radius:13px;padding:12px 14px;display:flex;justify-content:space-between;align-items:center;gap:10px;
 margin-bottom:9px;background:linear-gradient(135deg,rgba(217,169,60,.2),rgba(217,169,60,.08));border:1px solid rgba(217,169,60,.35);}
.duebar .l{font-size:10.5px;font-weight:800;color:var(--gold-2);}
.duebar .v{font-size:20px;font-weight:800;}
.duebar.zero{background:linear-gradient(135deg,rgba(46,155,87,.2),rgba(46,155,87,.07));border-color:rgba(123,217,161,.35);}
.duebar.zero .l{color:var(--green-2);font-size:10px;line-height:1.45;font-weight:700;}
.duebar.zero .v{color:var(--green-2);font-size:17px;}
.mnote{font-size:9.5px;color:rgba(252,246,233,.62);line-height:1.55;margin-bottom:9px;}
.payrow{border-top:1px dashed rgba(232,200,116,.22);padding-top:12px;margin-top:4px;}
.pl{font-size:9.5px;font-weight:800;letter-spacing:.07em;text-transform:uppercase;color:var(--gold-2);margin-bottom:8px;}
.payamt{display:flex;align-items:center;gap:9px;margin-bottom:8px;}
.payamt span{font-size:11.5px;font-weight:800;color:rgba(252,246,233,.75);white-space:nowrap;}
.fld{flex:1;min-width:0;width:100%;padding:11px 12px;border:1.5px solid var(--glass-line);border-radius:11px;
 font-family:inherit;font-size:16px;font-weight:800;color:var(--paper);background:rgba(0,0,0,.26);outline:none;
 transition:border-color .2s var(--ease);}
.fld::placeholder{color:rgba(252,246,233,.4);font-weight:600;font-size:12px;}
.fld:focus{border-color:var(--gold);}
.paybtns{display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:6px;}
.paybtns a{display:block;text-align:center;text-decoration:none;font-size:9.5px;font-weight:800;padding:10px 2px;
 border-radius:10px;border:1px solid var(--glass-line);background:rgba(255,255,255,.07);color:var(--paper);
 transition:transform .25s var(--spring),background .25s var(--ease);}
.paybtns a:active{transform:scale(.94);background:rgba(255,255,255,.14);}
.paybtns .up{background:linear-gradient(140deg,rgba(217,169,60,.28),rgba(217,169,60,.12));
 border-color:rgba(217,169,60,.45);color:var(--gold-2);}
.wabtn{display:block;text-align:center;font-family:inherit;font-size:13px;font-weight:800;padding:13px 8px;
 border-radius:12px;border:none;cursor:pointer;width:100%;background:linear-gradient(135deg,#35B36B,#1C7C46);
 color:#fff;position:relative;overflow:hidden;box-shadow:0 14px 30px -14px rgba(46,155,87,.95);transition:transform .3s var(--spring);}
.wabtn:active{transform:scale(.98);}
.hist{border-top:1px dashed rgba(232,200,116,.22);margin-top:12px;padding-top:10px;}
.hist summary{font-size:11px;font-weight:800;color:var(--gold-2);cursor:pointer;list-style:none;display:flex;align-items:center;gap:7px;user-select:none;}
.hist summary::-webkit-details-marker{display:none;}
.hist summary::before{content:'▸';transition:transform .25s var(--ease);}
.hist[open] summary::before{transform:rotate(90deg);}
.hist table{width:100%;border-collapse:collapse;margin-top:9px;font-size:11.5px;}
.hist td{padding:7px 4px;border-bottom:1px solid rgba(232,200,116,.1);}
.hist tr:last-child td{border-bottom:none;}
.hist td:last-child{text-align:right;font-weight:800;color:var(--green-2);}
.hk{font-size:8.5px;font-weight:700;background:rgba(255,255,255,.09);color:rgba(252,246,233,.75);border-radius:8px;padding:2px 7px;}
.sect-title{font-size:11px;font-weight:800;letter-spacing:.09em;text-transform:uppercase;color:var(--gold-2);margin:20px 3px 10px;}
.ccard{background:var(--glass);border:1px solid var(--glass-line);border-radius:14px;padding:12px 14px;margin-bottom:9px;
 display:flex;justify-content:space-between;align-items:center;gap:10px;backdrop-filter:blur(9px);-webkit-backdrop-filter:blur(9px);}
.ccard .cb{font-size:9.5px;font-weight:800;color:var(--gold-2);opacity:.85;}
.ccard .cn2{font-size:13px;font-weight:800;margin-top:2px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.ccard .cd{font-size:9.5px;color:rgba(252,246,233,.62);margin-top:2px;}
.ccard .cst{font-size:9px;font-weight:800;border-radius:12px;padding:5px 10px;flex-shrink:0;
 background:rgba(46,155,87,.2);color:var(--green-2);border:1px solid rgba(123,217,161,.3);}
.ccard .cst.fc{background:rgba(217,83,79,.2);color:var(--red-2);border-color:rgba(217,83,79,.4);}
.foot{text-align:center;margin-top:20px;display:none;}
.callbtn{display:inline-flex;align-items:center;gap:8px;background:var(--glass);border:1px solid var(--glass-line);
 color:var(--gold-2);border-radius:24px;padding:12px 22px;font-size:13px;font-weight:800;text-decoration:none;
 transition:transform .3s var(--spring);}
.callbtn:active{transform:scale(.96);}
.foot .addr{font-size:10.5px;color:rgba(252,246,233,.62);margin-top:12px;line-height:1.6;}
.foot .note{font-size:9.5px;color:rgba(252,246,233,.48);margin-top:14px;line-height:1.7;}
.bad{text-align:center;padding:26px 8px;}
.bad h1{font-family:'DM Serif Display',serif;font-size:21px;color:var(--maroon);margin-bottom:10px;}
.bad p{font-size:12.5px;color:var(--muted);line-height:1.7;}
.diag{margin-top:16px;padding:9px 11px;background:rgba(184,134,11,.11);border-radius:9px;font-size:10px;color:#8A6D00;line-height:1.55;}
</style>
</head>
<body>
<div id="fx"><div class="rng"></div><div class="tick">🔓</div></div>
<div id="bar" aria-hidden="true"><div class="l" id="barL"></div><div class="r num" id="barR"></div></div>
<div class="wrap">
  <div class="langbar" id="langbar"><div class="seg">
    <button id="lang-en" class="on" onclick="setLang('en')">English</button>
    <button id="lang-ta" class="ta" onclick="setLang('ta')">தமிழ்</button>
  </div></div>
  <div class="hdr">
    <div class="shop" id="h-shop">📘</div>
    <div class="shopTa ta" id="h-shopta" style="display:none;"></div>
    <div class="tag"><span class="dot"></span><span data-i="live"></span></div>
  </div>
  <main class="paper" id="gate"><div class="in gate">
    <div class="kolam"></div>
    <div class="seal">🔐</div>
    <h2 data-i="gt"></h2>
    <div class="cn" id="g-cn"></div>
    <p data-i="gp"></p>
    <div id="pinwrap"></div>
    <div class="errmsg" id="g-err" role="alert" aria-live="assertive"></div>
    <button class="gbtn" id="g-btn" onclick="unlock()" data-i="gb"></button>
    <div class="hint" data-i="offline"></div>
    <div class="kolam" style="margin-top:18px;"></div>
  </div></main>
  <div class="book" id="book"></div>
  <div class="foot" id="foot"></div>
</div>

<script>/* ⬇ PASTE LZSTRING HERE ⬇ — copy the single long `var LZString=function(){...}` line from your current passbook.html */</script>

<script>
'use strict';
// ═══════════════════════════════════════════════════════════════════════════
// Customer Passbook Viewer v10 — Sivaji Bank Pawnshop Manager
// Data arrives compressed in the URL fragment (#...) — nothing is ever sent to
// any server. PIN gate is a privacy speed-bump, matching the app's model.
// v10 is a UI/UX + accessibility rework. calcDue, elapsedMD, daysBetween, the
// 450-day filter, upiLink and sendPayConfirm are carried over from v9 verbatim.
// ═══════════════════════════════════════════════════════════════════════════
let P = null;
let LANG = 'en';
try { LANG = localStorage.getItem('pb_lang') || 'en'; } catch(e) {}
let FIRST_RENDER = true;
const REDUCED = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
const buzz = ms => { try { if (navigator.vibrate && !REDUCED) navigator.vibrate(ms); } catch(e){} };

const I18N = {
  live:{en:'Live dues — calculated fresh every time you open this', ta:'நேரடி நிலுவை — ஒவ்வொரு முறையும் புதிதாக கணக்கிடப்படுகிறது'},
  gt:{en:'Enter your PIN', ta:'உங்கள் PIN-ஐ உள்ளிடவும்'},
  gp:{en:'This passbook is protected. Enter the PIN given to you by the shop.', ta:'இந்த பாஸ்புக் பாதுகாக்கப்பட்டது. கடையில் வழங்கிய PIN-ஐ உள்ளிடவும்.'},
  gb:{en:'🔓 Unlock Passbook', ta:'🔓 பாஸ்புக்கைத் திற'},
  offline:{en:'Works without internet — your details travel inside the link itself.', ta:'இணையம் இல்லாமலும் வேலை செய்யும் — உங்கள் விவரங்கள் இந்த இணைப்பிலேயே உள்ளன.'},
  wrong:{en:'Wrong PIN — please try again', ta:'தவறான PIN — மீண்டும் முயற்சிக்கவும்'},
  wrong3:{en:'Still wrong — please call the shop.', ta:'மீண்டும் தவறு — கடையை அழைக்கவும்.'},
  active:{en:'Active', ta:'செயலில்'},
  toclose:{en:'To close all', ta:'அனைத்தும் முடிக்க'},
  principal:{en:'Principal', ta:'அசல்'},
  grandl:{en:'TOTAL TO CLOSE TODAY', ta:'இன்று முடிக்க மொத்தம்'},
  asof:{en:'Data as of', ta:'தரவு தேதி'},
  odn:{en:'#N OVERDUE', ta:'#N தாமதம்'}, ontrackall:{en:'ON TRACK', ta:'சரியாக உள்ளது'},
  stale:{en:'⚠️ This passbook snapshot is #D days old. Recent payments or renewals may not be shown — ask the shop for a fresh link or card.', ta:'⚠️ இந்த பாஸ்புக் தரவு #D நாட்கள் பழையது. சமீபத்திய கட்டணங்கள் காட்டப்படாமல் இருக்கலாம் — புதிய இணைப்பு/கார்டு கேட்கவும்.'},
  pledged:{en:'Pledged on', ta:'அடகு தேதி'}, duedate:{en:'Due date', ta:'கெடு தேதி'},
  lastpay:{en:'Last payment', ta:'கடைசி கட்டணம்'},
  outp:{en:'Loan balance', ta:'கடன் நிலுவை'}, intnow:{en:'Interest due now', ta:'இப்போதைய வட்டி'},
  elapsed:{en:'Time elapsed', ta:'கடந்த காலம்'}, etot:{en:'days total', ta:'மொத்த நாட்கள்'},
  emo:{en:'month', ta:'மாதம்'}, emos:{en:'months', ta:'மாதம்'}, edy:{en:'day', ta:'நாள்'}, edys:{en:'days', ta:'நாள்'},
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
  badT:{en:'Link not readable', ta:'இணைப்பு படிக்க முடியவில்லை'},
  badP:{en:'This passbook link looks incomplete — it was probably cut short when it was copied or forwarded. Please scan the QR on your card again, or ask the shop to resend it.', ta:'இந்த இணைப்பு முழுமையாக இல்லை. கார்டில் உள்ள QR-ஐ மீண்டும் ஸ்கேன் செய்யவும், அல்லது கடையில் கேட்கவும்.'},
  noneT:{en:'Nothing to open yet', ta:'திறக்க எதுவும் இல்லை'},
  noneP:{en:'This page only works when opened from the QR code on your passbook card, or from the link the shop sent you — your details travel inside that link.', ta:'கார்டில் உள்ள QR-ஐ ஸ்கேன் செய்து திறக்கவும். உங்கள் விவரங்கள் அந்த இணைப்பிலேயே உள்ளன.'},
  diag:{en:'Received #C characters — a full link is usually 400–1200. Show this line to the shop if it keeps happening.', ta:'#C எழுத்துகள் மட்டுமே கிடைத்தன. இது தொடர்ந்தால் கடையில் காட்டவும்.'}
};
const T = k => (I18N[k] && (I18N[k][LANG] || I18N[k].en)) || k;

function setLang(l) {
  LANG = l;
  try { localStorage.setItem('pb_lang', l); } catch(e) {}
  document.documentElement.lang = l;
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

// ── Boot ────────────────────────────────────────────────────────────────────
// Share paths mangle fragments: some in-app browsers percent-encode them, some
// turn '+' into a space, long links occasionally get clipped. Try the plausible
// repairs before giving up, and never leave the reader on a blank page.
function readFragment(){
  const raw = (location.hash || '').replace(/^#/, '');
  if (!raw) return { frag:'', data:null };
  const tries = [raw];
  if (raw.indexOf('%') > -1) { try { tries.push(decodeURIComponent(raw)); } catch(e){} }
  if (raw.indexOf(' ') > -1) tries.push(raw.replace(/ /g, '+'));
  for (const t of tries) {
    try {
      const s = LZString.decompressFromEncodedURIComponent(t);
      if (s) { const o = JSON.parse(s); if (o && Array.isArray(o.p)) return { frag:raw, data:o }; }
    } catch(e){}
  }
  return { frag:raw, data:null };
}

(function boot(){
  const r = readFragment();
  P = r.data;
  if (!P) {
    const title = r.frag ? 'badT' : 'noneT';
    const para  = r.frag ? 'badP' : 'noneP';
    const diag  = r.frag ? '<div class="diag" data-i="diag"></div>' : '';
    document.getElementById('gate').outerHTML =
      '<div class="paper"><div class="in"><div class="bad"><h1 data-i="'+title+'"></h1><p data-i="'+para+'"></p>'+diag+'</div></div></div>';
    document.querySelector('.hdr').style.display = 'none';
    setLang(LANG);
    if (r.frag) { const d = document.querySelector('.diag'); if (d) d.innerHTML = T('diag').replace('#C', r.frag.length); }
    return;
  }
  document.getElementById('h-shop').textContent = P.sn || 'Passbook';
  if (P.st) { const e = document.getElementById('h-shopta'); e.textContent = P.st; e.style.display='block'; }
  document.getElementById('g-cn').textContent = P.cn || '';
  buildPinUI();
  setLang(LANG);
})();

// A 4-character secret (a 4-digit PIN, or the last 4 digits of an ID) gets the
// OTP-style boxes. Anything longer keeps a single field so custom PINs of any
// length still work.
let PINBOXES = null;
function buildPinUI(){
  const wrap = document.getElementById('pinwrap');
  const sec = String(P.sec || '');
  if (sec.length === 4) {
    wrap.innerHTML = '<div class="pins" id="pins" role="group" aria-label="PIN">' +
      [1,2,3,4].map(i => '<input type="tel" inputmode="numeric" maxlength="1" aria-label="PIN digit '+i+'" autocomplete="'+(i===1?'one-time-code':'off')+'">').join('') + '</div>';
    document.getElementById('g-btn').style.display = 'none';
    PINBOXES = [].slice.call(wrap.querySelectorAll('input'));
    PINBOXES.forEach((b,i) => {
      b.addEventListener('input', () => {
        b.value = b.value.replace(/\D/g,'');
        if (b.value) { b.classList.add('ok'); buzz(9); if (i<3) PINBOXES[i+1].focus(); else unlock(); }
        else b.classList.remove('ok');
      });
      b.addEventListener('keydown', e => {
        if (e.key==='Backspace' && !b.value && i>0){ PINBOXES[i-1].focus(); PINBOXES[i-1].value=''; PINBOXES[i-1].classList.remove('ok'); }
        if (e.key==='Enter') unlock();
      });
      b.addEventListener('paste', e => {
        const t=(e.clipboardData||window.clipboardData).getData('text').replace(/\D/g,'').slice(0,4);
        if(!t.length) return;
        e.preventDefault();
        PINBOXES.forEach((x,j)=>{x.value=t[j]||'';x.classList.toggle('ok',!!t[j]);});
        if(t.length===4) unlock(); else PINBOXES[t.length].focus();
      });
    });
  } else {
    wrap.innerHTML = '<input id="pin" class="pinlong" type="password" inputmode="numeric" autocomplete="off" maxlength="12" placeholder="••••" aria-label="PIN">';
    document.getElementById('pin').addEventListener('keydown', e => { if (e.key==='Enter') unlock(); });
  }
  setTimeout(() => { if (window.innerWidth > 640) (PINBOXES ? PINBOXES[0] : document.getElementById('pin')).focus(); }, 350);
}

let tries = 0;
function readPin(){
  return PINBOXES ? PINBOXES.map(b=>b.value).join('') : (document.getElementById('pin').value || '').trim();
}
function unlock() {
  if (!P) return;
  const val = readPin();
  if (PINBOXES && val.length < 4) return;
  if (val !== String(P.sec||'')) {
    tries++; buzz([40,60,40]);
    const target = document.getElementById('pins') || document.getElementById('pin');
    target.classList.remove('shake'); void target.offsetWidth; target.classList.add('shake');
    document.getElementById('g-err').textContent = T(tries>=3 ? 'wrong3' : 'wrong');
    if (PINBOXES) setTimeout(()=>{ PINBOXES.forEach(b=>{b.value='';b.classList.remove('ok');}); PINBOXES[0].focus(); }, 500);
    return;
  }
  buzz([14,50,26]);
  if (REDUCED) { reveal(); return; }
  const fx = document.getElementById('fx');
  fx.classList.add('on');
  setTimeout(()=>{ fx.querySelector('.rng').style.display='none'; fx.querySelector('.tick').classList.add('go'); }, 640);
  setTimeout(()=>{
    fx.classList.remove('on');
    if (document.startViewTransition) document.startViewTransition(reveal); else reveal();
  }, 1120);
}
function reveal(){
  document.getElementById('gate').style.display = 'none';
  document.querySelector('.hdr').style.display = 'none';
  document.getElementById('book').style.display = 'block';
  document.getElementById('foot').style.display = 'block';
  renderBook();
  window.scrollTo(0,0);
}

function renderBook() {
  const asOf = todayS();
  // Silently omit pledges older than 450 days (from pledge date). Recomputed on
  // every open, so a pledge that crosses the limit after the QR was printed
  // disappears automatically. Idempotent — safe on language-toggle re-render.
  P.p = (P.p || []).filter(it => !it.d || daysBetween(it.d, asOf) <= 450);
  const book = document.getElementById('book');

  // Preserve anything already typed or opened, so switching language does not
  // wipe an amount mid-payment. (v9 lost both.)
  const keep = { amt:{}, utr:{}, open:{} };
  P.p.forEach((it,i) => {
    const a = document.getElementById('pay-amt-'+i); if (a) keep.amt[i] = a.value;
    const u = document.getElementById('utr-'+i);     if (u) keep.utr[i] = u.value;
    const d = document.getElementById('hist-'+i);    if (d) keep.open[i] = d.open;
  });

  const dues   = P.p.map(it => calcDue(it, asOf));
  const totPr  = P.p.reduce((s,it) => s + (it.pr||0), 0);
  const totDue = dues.reduce((s,d) => s + d.total, 0);
  const initials = (P.cn||'?').trim().split(/\s+/).slice(0,2).map(w=>w[0]).join('').toUpperCase() || '?';
  const genAge = daysBetween(P.gen || asOf, asOf);
  const overdueCt = P.p.filter(it => it.dd && asOf > it.dd).length;

  // v9 printed "Data as of: <snapshot> · <today>", two unexplained dates.
  // Show the snapshot date, and only mention today when they differ.
  const asofTxt = (P.gen && P.gen !== asOf)
    ? T('asof') + ': ' + fmtD(P.gen) + ' → ' + fmtD(asOf)
    : T('asof') + ': ' + fmtD(asOf);

  let h = `
    <section class="hero rv">
      <div class="who">
        <div class="av">${esc(initials)}</div>
        <div style="min-width:0;"><div class="nm">${esc(P.cn)}</div><div class="asof num">${esc(asofTxt)}</div></div>
        <span class="odtag${overdueCt?'':' ok'}">${overdueCt ? T('odn').replace('#N',overdueCt) : T('ontrackall')}</span>
      </div>
      <div class="grand">
        <div class="l">${T('grandl')}</div>
        <div class="v num" id="grandV">₹0</div>
      </div>
    </section>
    <div class="kpis">
      <div class="kpi rv"><div class="v num" data-count="${P.p.length}" data-plain="1">0</div><div class="l">${T('active')}</div></div>
      <div class="kpi rv ${overdueCt?'red':''}"><div class="v num" data-count="${Math.round(totDue)}">₹0</div><div class="l">${T('toclose')}</div></div>
      <div class="kpi rv green"><div class="v num" data-count="${Math.round(totPr)}">₹0</div><div class="l">${T('principal')}</div></div>
    </div>`;

  if (genAge > 7) h += `<div class="notice rv">${T('stale').replace('#D', genAge)}</div>`;

  P.p.forEach((it, i) => {
    const d = dues[i];
    const overdueDays = it.dd ? daysBetween(it.dd, asOf) : 0;
    const isOver = it.dd && asOf > it.dd;
    h += `
    <article class="pcard rv${isOver?' over':''}">
      <div class="top">
        <div style="min-width:0;"><div class="bill num">BILL ${esc(it.b)}</div><div class="item">${esc(it.it)||'—'}</div></div>
        ${isOver ? `<span class="badge due">⏰ ${T('overdue').replace('#D', overdueDays)}</span>` : `<span class="badge ok">✓ ${T('ontrack')}</span>`}
      </div>
      <div class="kv">
        <div><div class="k">${T('pledged')}</div><div class="val num">${fmtD(it.d)}</div></div>
        <div><div class="k">${T('duedate')}</div><div class="val num">${fmtD(it.dd)}</div></div>
        <div><div class="k">${T('lastpay')}</div><div class="val num">${fmtD(it.lp)}</div></div>
        <div><div class="k">${T('elapsed')}</div><div class="val num">⏱ ${fmtElapsed(it.d, asOf)}<small>= ${daysBetween(it.d, asOf)} ${T('etot')}</small></div></div>
        <div><div class="k">${T('outp')}</div><div class="val num">${fmtR(it.pr)}</div></div>
        <div><div class="k">${T('intnow')}</div><div class="val num ${d.interest>0?'hot':'cool'}">${fmtR(d.interest)}</div></div>
      </div>
      ${d.interest > 0
        ? `<div class="duebar"><span class="l">${T('totnow')}</span><span class="v num">${fmtR(d.total)}</span></div>
           <div class="mnote">${T('months').replace('#M', d.extraMonths)}</div>`
        : `<div class="duebar zero"><span class="l">${T('grace')}</span><span class="v">✓</span></div>`}
      ${P.upi && P.upi.pa ? payBlock(i, it, d) : ''}
      ${it.pm && it.pm.length ? histBlock(it, i) : ''}
    </article>`;
  });

  if (P.cl && P.cl.length) {
    h += `<div class="sect-title rv">${T('closed')}</div>`;
    P.cl.forEach(c => {
      h += `<div class="ccard rv">
        <div style="min-width:0;"><div class="cb num">BILL ${esc(c.b)} · ${fmtR(c.a)}</div>
        <div class="cn2">${esc(c.it)||'—'}</div>
        <div class="cd num">${fmtD(c.d)} → ${fmtD(c.cd)}</div></div>
        <span class="cst${c.fc?' fc':''}">${c.fc ? T('foreclosed') : T('redeemed')}</span>
      </div>`;
    });
  }
  book.innerHTML = h;

  P.p.forEach((it,i) => {
    if (keep.amt[i] !== undefined) { const a=document.getElementById('pay-amt-'+i); if(a){a.value=keep.amt[i]; payAmtChanged(i);} }
    if (keep.utr[i] !== undefined) { const u=document.getElementById('utr-'+i);     if(u) u.value=keep.utr[i]; }
    if (keep.open[i])              { const dt=document.getElementById('hist-'+i);   if(dt) dt.open=true; }
  });

  let f = '';
  if (P.sp) f += `<a class="callbtn" href="tel:${esc(P.sp).replace(/[^\d+]/g,'')}">${T('call')} · ${esc(P.sp)}</a>`;
  if (P.ad) f += `<div class="addr">📍 ${esc(P.ad)}</div>`;
  f += `<div class="note">🔒 ${T('privacy')}<br><span style="opacity:.6;">viewer v10</span></div>`;
  document.getElementById('foot').innerHTML = f;

  document.getElementById('barL').innerHTML = esc(P.cn||'') + '<small>' + P.p.length + ' ' + T('active') + '</small>';
  document.getElementById('barR').textContent = fmtR(totDue);

  animate({ grand: totDue, first: FIRST_RENDER });
  FIRST_RENDER = false;
}

function payBlock(i, it, d) {
  // Default = Total to close today (principal + interest). Field stays editable.
  const def = d.interest > 0 ? Math.round(d.total) : '';
  return `
  <div class="payrow">
    <div class="pl">📲 ${T('paynow')}</div>
    <div class="payamt"><span>${T('payamt')}</span><input id="pay-amt-${i}" class="fld" type="number" inputmode="numeric" min="1" value="${def}" oninput="payAmtChanged(${i})" aria-label="${T('payamt')}"></div>
    ${def !== '' ? `<div class="mnote">💡 ${T('payhint')}</div>` : ''}
    <div class="paybtns">
      <a id="pay-gpay-${i}"    href="${upiLink('gpay',    def||0, it.b)}">GPay</a>
      <a id="pay-phonepe-${i}" href="${upiLink('phonepe', def||0, it.b)}">PhonePe</a>
      <a id="pay-paytm-${i}"   href="${upiLink('paytm',   def||0, it.b)}">Paytm</a>
      <a id="pay-upi-${i}"     class="up" href="${upiLink('upi', def||0, it.b)}">UPI</a>
    </div>
    <div class="mnote" style="margin:9px 0 0;">${T('paynote')}</div>
    ${P.sp ? `
    <div style="border-top:1px dashed rgba(232,200,116,.22);margin-top:12px;padding-top:11px;">
      <div class="pl">${T('cfT')}</div>
      <input id="utr-${i}" class="fld" type="text" autocomplete="off" maxlength="40" placeholder="${T('cfU')}" aria-label="${T('cfU')}" style="margin-bottom:9px;">
      <button class="wabtn" onclick="sendPayConfirm(${i})">${T('cfB')}</button>
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

function histBlock(it, i) {
  const rows = it.pm.map(p => `<tr><td class="num">${fmtD(p[0])}</td><td><span class="hk">${(I18N.histk[p[2]]&&(I18N.histk[p[2]][LANG]||I18N.histk[p[2]].en))||''}</span></td><td class="num">${fmtR(p[1])}</td></tr>`).join('');
  return `<details class="hist" id="hist-${i}"><summary>🧾 ${T('hist')} (${it.pm.length})</summary><table>${rows}</table></details>`;
}

// ── entrance choreography ───────────────────────────────────────────────────
// requestAnimationFrame pauses while a tab is backgrounded — a customer who
// scans, switches to WhatsApp and comes back would otherwise find a figure
// frozen part-way. Every animation is guaranteed to land on its true value.
function countUp(el, to, fmt) {
  if (REDUCED || to <= 0) { el.textContent = fmt(to); return; }
  let t0 = null, done = false; const dur = 900;
  const land = () => { if (done) return; done = true; el.textContent = fmt(to); };
  const step = t => {
    if (done) return;
    if (!t0) t0 = t;
    const p = Math.min(1, (t - t0) / dur);
    el.textContent = fmt(Math.round(to * (1 - Math.pow(1 - p, 4))));
    if (p < 1) requestAnimationFrame(step); else land();
  };
  requestAnimationFrame(step);
  setTimeout(land, dur + 260);
  document.addEventListener('visibilitychange', function h(){
    if (document.visibilityState === 'visible') { land(); document.removeEventListener('visibilitychange', h); }
  });
}

function animate(opt) {
  const items = [].slice.call(document.querySelectorAll('#book .rv'));
  // On a language toggle the content is already familiar — show it at once
  // rather than replaying the whole entrance.
  if (!opt.first || REDUCED || !('IntersectionObserver' in window)) {
    items.forEach(el => el.classList.add('in'));
  } else {
    const io = new IntersectionObserver(es => {
      es.forEach(e => {
        if (!e.isIntersecting) return;
        const el = e.target, i = items.indexOf(el);
        el.style.transitionDelay = Math.min(i*70, 420) + 'ms';
        el.classList.add('in');
        if (el.classList.contains('kpi')) setTimeout(()=>el.classList.add('lit'), 260);
        io.unobserve(el);
      });
    }, { threshold:.12, rootMargin:'0px 0px -8% 0px' });
    items.forEach(el => io.observe(el));
  }

  const g = document.getElementById('grandV');
  if (g) { if (opt.first) countUp(g, opt.grand, fmtR); else g.textContent = fmtR(opt.grand); }
  [].slice.call(document.querySelectorAll('#book [data-count]')).forEach(el => {
    const to = parseFloat(el.getAttribute('data-count')) || 0;
    const fmt = el.getAttribute('data-plain') ? (v => String(v)) : fmtR;
    if (opt.first) countUp(el, to, fmt); else el.textContent = fmt(to);
  });

  const hero = document.querySelector('#book .hero'), bar = document.getElementById('bar');
  if (hero && bar && 'IntersectionObserver' in window && !bar._wired) {
    bar._wired = true;
    new IntersectionObserver(es => {
      bar.classList.toggle('on', !es[0].isIntersecting);
      bar.setAttribute('aria-hidden', es[0].isIntersecting ? 'true' : 'false');
    }, { threshold:0, rootMargin:'-56px 0px 0px 0px' }).observe(hero);
  }
}

function esc(s){ return String(s==null?'':s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;'); }
</script>
</body>
</html>
