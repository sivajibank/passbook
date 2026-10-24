<html lang="ta">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
<meta name="robots" content="noindex, nofollow">
<meta http-equiv="Cache-Control" content="no-cache, must-revalidate">
<meta http-equiv="Pragma" content="no-cache">
<!-- PASSBOOK VIEWER v15 — encrypted links (E1): the customer's PIN decrypts the data on the phone;
     the PIN is no longer inside the link. Old links still open.
     PASSBOOK VIEWER v14 — Latest-gen UI/UX: aurora backdrop, glassmorphic animated
     KPI cards (orbs + sheen + shimmer + count-up, matching main app v183 dashboard),
     scroll-reveal pledge cards, animated unlock sequence, reduced-motion safe.
     ALL v9 logic preserved: LZString fragment payload, PIN gate, tiered/compound
     interest parity, 450-day filter, UPI deep links, WhatsApp UTR confirmation. -->
<title>Customer Passbook</title>
<meta name="theme-color" content="#0F4C5C">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Hind+Madurai:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  /* ═══════════════════════════════════════════════════════════════════════
     PASSBOOK VIEWER v16 — "Kanjeevaram" design, same family as the Owner
     Phone View: peacock header with a woven zari edge, ivory-mint page,
     one colour per figure. One spacing scale, one radius scale, one control
     height, so everything in a row lines up and every column shares an edge.
     ═══════════════════════════════════════════════════════════════════════ */
  :root{
    --peacock:#0F4C5C; --peacock-d:#0A3340; --peacock-l:#1B6B7E;
    --kumkum:#9E1B42; --turmeric:#E19A12; --leaf:#2E8B57; --zari:#E7BE5A; --zari-d:#B98A22;
    --indigo:#3B4C9B; --lotus:#B83C78;
    --bg:#EDF3F2; --card:#FFFFFF; --card-2:#F6FAF9;
    --ink:#13242A; --ink-2:#28414A; --ink-3:#4E666E; --ink-4:#7C9096;
    --line:#DDE8E6; --line-2:#CFDDDA;
    --t-peacock:#E3F0F1; --t-kumkum:#FBE8EE; --t-turmeric:#FDF2DC; --t-leaf:#E3F3EA; --t-indigo:#E8EBF7; --t-lotus:#F8E7F0;
    --green:#1F7A48; --red:#B3263E; --blue:#3B4C9B;
    --wa:#25D366; --wa-2:#128C7E;

    --s1:4px; --s2:8px; --s3:12px; --s4:16px; --s5:20px; --s6:24px; --s7:32px;
    --r1:10px; --r2:14px; --r3:18px; --r4:22px; --rp:999px;
    --ctl:44px; --ctl-sm:36px;

    --ease-out:cubic-bezier(.22,1,.36,1);
    --ease-spring:cubic-bezier(.22,.68,0,1.3);
    --shadow-1:0 1px 2px rgba(15,76,92,.06),0 2px 8px rgba(15,76,92,.06);
    --shadow-2:0 2px 6px rgba(15,76,92,.06),0 10px 26px rgba(15,76,92,.10);
    --shadow-3:0 4px 10px rgba(15,76,92,.08),0 18px 40px rgba(15,76,92,.16);
  }
  *{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
  html{scroll-behavior:smooth;-webkit-text-size-adjust:100%;}
  body{
    font-family:'Hind Madurai','Noto Sans Tamil','Segoe UI','Nirmala UI',Arial,sans-serif;
    background:var(--bg);min-height:100vh;color:var(--ink);
    padding:0 0 calc(var(--s6) + 56px);
    position:relative;overflow-x:hidden;line-height:1.5;font-size:14px;
  }
  .num,.kval,.v,.st-v,.pl-tot b,.sh-big{font-variant-numeric:tabular-nums;font-feature-settings:'tnum' 1;}
  :focus-visible{outline:3px solid var(--zari);outline-offset:2px;}
  .aurora{display:none;}
  .wrap{max-width:460px;margin:0 auto;position:relative;z-index:1;padding:0 var(--s4);}

  /* ── Motion: one orchestrated entrance, then quiet ─────────────────────── */
  @keyframes fadeUp{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:none}}
  @keyframes cardIn{from{opacity:0;transform:translateY(18px) scale(.98)}to{opacity:1;transform:none}}
  @keyframes rise{from{opacity:0;transform:translateY(22px) scale(.95)}to{opacity:1;transform:none}}
  @keyframes shine{from{transform:translateX(-120%) skewX(-18deg)}to{transform:translateX(260%) skewX(-18deg)}}
  @keyframes shake{0%,100%{transform:translateX(0)}20%,60%{transform:translateX(-8px)}40%,80%{transform:translateX(8px)}}
  @keyframes popIn{0%{opacity:0;transform:scale(.6)}70%{transform:scale(1.06)}100%{opacity:1;transform:scale(1)}}
  @keyframes pulse{0%{box-shadow:0 0 0 0 rgba(126,226,160,.6)}100%{box-shadow:0 0 0 8px rgba(126,226,160,0)}}
  @keyframes gateOut{to{opacity:0;transform:translateY(-14px) scale(.97)}}
  @keyframes ringDash{from{stroke-dashoffset:var(--ring-c)}to{stroke-dashoffset:var(--ring-off)}}
  @keyframes badgeGlow{0%,100%{box-shadow:0 0 0 0 rgba(179,38,62,.28)}50%{box-shadow:0 0 0 5px rgba(179,38,62,0)}}
  @keyframes shimmerRow{from{background-position:-160% 0}to{background-position:260% 0}}
  @keyframes slideDown{from{opacity:0;transform:translateY(-100%)}to{opacity:1;transform:none}}
  @keyframes fabIn{from{opacity:0;transform:translateY(16px) scale(.8)}to{opacity:1;transform:none}}
  @keyframes okPop{0%{opacity:0;transform:translate(-50%,10px) scale(.9)}15%,85%{opacity:1;transform:translate(-50%,0) scale(1)}100%{opacity:0;transform:translate(-50%,-6px) scale(.98)}}
  @keyframes grow{from{transform:scaleX(0)}to{transform:scaleX(1)}}

  /* ── Header band: peacock silk with a woven zari edge ──────────────────── */
  .hdr{position:relative;color:#fff;padding:calc(var(--s4) + env(safe-area-inset-top,0px)) 0 calc(var(--s7) + 22px);
    background:
      radial-gradient(120% 90% at 100% 0%,rgba(231,190,90,.20),transparent 55%),
      radial-gradient(90% 80% at 0% 100%,rgba(184,60,120,.22),transparent 60%),
      linear-gradient(160deg,var(--peacock-l) 0%,var(--peacock) 45%,var(--peacock-d) 100%);
    overflow:hidden;}
  .hdr::before{content:'';position:absolute;inset:0;pointer-events:none;opacity:.5;
    background-image:radial-gradient(rgba(255,255,255,.10) 1px,transparent 1.2px);background-size:14px 14px;}
  .hdr::after{content:'';position:absolute;left:0;right:0;bottom:0;height:11px;
    background:conic-gradient(from -45deg at 50% 100%,#E7BE5A 90deg,transparent 0) 0 2px/14px 9px repeat-x,#7E1638;}
  .hdr .hin{max-width:460px;margin:0 auto;padding:0 var(--s4);position:relative;z-index:1;
    animation:fadeUp .5s var(--ease-out) both;}
  .hrow{display:flex;align-items:center;gap:var(--s3);}
  .hdr .mark{width:42px;height:42px;flex:0 0 42px;border-radius:13px;display:grid;place-items:center;
    background:linear-gradient(145deg,#F6D985,#C99A2E);color:#5A3A06;
    box-shadow:0 6px 16px rgba(0,0,0,.25),inset 0 1px 0 rgba(255,255,255,.6);}
  .hdr .mark svg{width:24px;height:24px;}
  .hname{flex:1;min-width:0;}
  .hdr .shop{font-size:17px;font-weight:700;line-height:1.2;letter-spacing:.1px;
    white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
  .hdr .shopTa{font-size:12.5px;font-weight:600;color:rgba(255,255,255,.72);margin-top:1px;
    white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
  .langbar{display:flex;flex:0 0 auto;padding:3px;border-radius:var(--rp);
    background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.18);}
  .langbar button{height:30px;min-width:44px;padding:0 10px;border:none;border-radius:var(--rp);
    background:transparent;color:rgba(255,255,255,.82);font:inherit;font-size:12px;font-weight:700;cursor:pointer;
    transition:background .2s,color .2s;}
  .langbar button.on{background:#fff;color:var(--peacock);box-shadow:0 2px 8px rgba(0,0,0,.18);}
  .hdr .tag{display:inline-flex;align-items:center;gap:var(--s2);margin-top:var(--s4);
    font-size:12px;line-height:1.4;color:rgba(255,255,255,.86);font-weight:500;}
  .hdr .tag .dot{width:8px;height:8px;border-radius:50%;background:#7EE2A0;flex-shrink:0;
    animation:pulse 2s ease-out infinite;}

  /* everything below the header tucks up over its lower edge */
  .gate,.book,.badlink{margin-top:calc(-1 * (var(--s7) + 6px));position:relative;z-index:2;}

  /* ── PIN gate ──────────────────────────────────────────────────────────── */
  .gate{background:var(--card);border-radius:var(--r4);padding:var(--s6) var(--s5) var(--s5);text-align:center;
    box-shadow:var(--shadow-3);animation:cardIn .5s var(--ease-out) .08s both;overflow:hidden;}
  .gate.leaving{animation:gateOut .36s var(--ease-out) forwards;}
  .gate .lock{width:60px;height:60px;margin:0 auto;border-radius:20px;display:grid;place-items:center;
    background:linear-gradient(145deg,var(--peacock-l),var(--peacock-d));color:var(--zari);
    box-shadow:0 10px 22px rgba(15,76,92,.3);animation:popIn .55s var(--ease-out) .15s both;}
  .gate .lock svg{width:28px;height:28px;}
  .gate h2{font-size:19px;font-weight:700;color:var(--ink);margin:var(--s4) 0 var(--s1);}
  .gate .cn{font-size:14px;font-weight:700;color:var(--peacock);margin-bottom:var(--s1);}
  .gate p{font-size:13px;color:var(--ink-3);line-height:1.55;margin:0 auto var(--s5);max-width:290px;}
  .lg-stage{margin:0 auto var(--s4);max-width:320px;}
  .gate.err .lg-stage{animation:shake .4s ease;}
  .lg-pins{display:flex;gap:var(--s2);justify-content:center;}
  .lg-cell{flex:0 1 44px;height:54px;position:relative;cursor:text;border-radius:var(--r2);
    background:var(--card-2);border:1.5px solid var(--line-2);overflow:hidden;
    transition:transform .25s var(--ease-spring),border-color .2s,background .2s,box-shadow .2s;}
  .lg-dot{position:absolute;left:50%;top:50%;width:7px;height:7px;border-radius:50%;
    transform:translate(-50%,-50%);background:var(--line-2);transition:opacity .2s;}
  .lg-cell.filled .lg-dot,.lg-cell.active .lg-dot{opacity:0;}
  .lg-blob,.lg-sweep{display:none;}
  .lg-cell.active{border-color:var(--peacock);background:#fff;transform:translateY(-2px);
    box-shadow:0 0 0 4px rgba(15,76,92,.12);}
  .lg-cell.active::after{content:'';position:absolute;left:50%;top:28%;bottom:28%;width:2px;margin-left:-1px;
    background:var(--peacock);border-radius:2px;animation:blink 1s steps(1) infinite;}
  @keyframes blink{50%{opacity:0}}
  .lg-cell.filled{border-color:var(--peacock);background:var(--t-peacock);}
  .lg-digit{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;
    font-size:24px;font-weight:700;color:var(--peacock-d);opacity:0;}
  .lg-cell.filled .lg-digit{opacity:1;animation:lgPop .4s var(--ease-spring);}
  @keyframes lgPop{0%{opacity:0;transform:translateY(8px) scale(.5)}100%{opacity:1;transform:none}}
  .gate.err .lg-cell{border-color:var(--red);background:var(--t-kumkum);}
  .lg-pad{display:grid;grid-template-columns:repeat(3,1fr);gap:var(--s2);margin:0 auto var(--s2);max-width:276px;}
  .lg-key{height:50px;border-radius:var(--r2);border:1px solid var(--line);background:var(--card-2);
    font:inherit;font-size:21px;font-weight:600;color:var(--ink);cursor:pointer;
    transition:transform .1s,background .15s;display:flex;align-items:center;justify-content:center;}
  .lg-key:hover{background:var(--t-peacock);}
  .lg-key:active{transform:scale(.94);background:var(--t-peacock);}
  .lg-key.wide{font-size:18px;color:var(--peacock);}
  .gate .errmsg{font-size:12.5px;color:var(--red);font-weight:700;min-height:20px;margin-bottom:var(--s2);}
  .gate .ubtn{width:100%;max-width:276px;height:50px;border:none;border-radius:var(--r2);
    background:linear-gradient(135deg,var(--peacock-l),var(--peacock-d));color:#fff;font:inherit;
    font-size:15px;font-weight:700;cursor:pointer;box-shadow:0 10px 22px rgba(15,76,92,.28);
    display:inline-flex;align-items:center;justify-content:center;gap:var(--s2);
    transition:transform .18s var(--ease-spring),filter .15s;}
  .gate .ubtn:hover{filter:brightness(1.08);}
  .gate .ubtn:active{transform:scale(.97);}

  .book{display:none;}

  /* ── Sticky summary bar ────────────────────────────────────────────────── */
  #stickybar{position:fixed;top:0;left:0;right:0;z-index:40;display:none;
    padding:10px var(--s4);align-items:center;gap:var(--s3);color:#fff;
    background:rgba(10,51,64,.92);-webkit-backdrop-filter:blur(14px) saturate(1.4);
    backdrop-filter:blur(14px) saturate(1.4);box-shadow:0 4px 18px rgba(10,51,64,.25);}
  #stickybar::after{content:'';position:absolute;left:0;right:0;bottom:-4px;height:4px;
    background:linear-gradient(90deg,#7E1638,#E7BE5A,#7E1638);}
  #stickybar.on{display:flex;animation:slideDown .28s var(--ease-out) both;}
  #stickybar .sb-nm{font-size:14px;font-weight:700;flex:1;min-width:0;
    white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
  #stickybar .sb-v{font-size:16px;font-weight:700;color:var(--zari);white-space:nowrap;display:block;text-align:right;}
  #stickybar .sb-l{font-size:11px;font-weight:500;color:rgba(255,255,255,.7);display:block;text-align:right;}

  /* ── Live status chip ──────────────────────────────────────────────────── */
  #pblive{display:flex;width:100%;align-items:center;justify-content:center;gap:var(--s2);
    margin:0 0 var(--s3)!important;padding:9px var(--s3)!important;border-radius:var(--r2)!important;
    font-size:12px;font-weight:700;text-align:center;line-height:1.45;box-shadow:var(--shadow-1);
    animation:fadeUp .35s var(--ease-out) both;}

  /* ── Customer hero: the one number the customer opened this for ────────── */
  .sumhero{position:relative;overflow:hidden;border-radius:var(--r4);padding:var(--s5);
    margin-bottom:var(--s3);color:#fff;
    background:
      radial-gradient(110% 80% at 100% 0%,rgba(231,190,90,.28),transparent 55%),
      linear-gradient(150deg,#16303A 0%,var(--peacock-d) 55%,#062229 100%);
    box-shadow:0 14px 34px rgba(10,51,64,.32);animation:rise .6s var(--ease-out) both;}
  .sumhero::before{content:'';position:absolute;right:-30px;bottom:-40px;width:180px;height:180px;
    border-radius:50%;border:22px solid rgba(231,190,90,.08);pointer-events:none;}
  .sh-id{display:flex;align-items:center;gap:var(--s3);}
  .sumhero .av{width:44px;height:44px;border-radius:14px;flex-shrink:0;display:grid;place-items:center;
    background:linear-gradient(145deg,#F6D985,#C99A2E);font-weight:700;color:#4A2F05;font-size:16px;
    box-shadow:0 4px 12px rgba(0,0,0,.25);animation:popIn .5s var(--ease-out) .15s both;}
  .sumhero .nm{font-size:17px;font-weight:700;line-height:1.25;}
  .sumhero .asof{font-size:12px;color:rgba(255,255,255,.66);margin-top:1px;}
  .sh-lab{margin-top:var(--s5);font-size:13px;font-weight:500;color:rgba(255,255,255,.75);}
  .sh-big{font-size:40px;font-weight:700;letter-spacing:-.5px;line-height:1.1;margin-top:2px;
    color:#FFF6DC;text-shadow:0 2px 16px rgba(231,190,90,.25);}
  .split{display:flex;height:8px;border-radius:var(--rp);overflow:hidden;margin-top:var(--s4);
    background:rgba(255,255,255,.12);transform-origin:left;animation:grow .9s var(--ease-out) .35s both;}
  .split i{display:block;height:100%;transition:width 1s var(--ease-out);}
  .split .sp-p{background:linear-gradient(90deg,#5FC6D4,#8FDDE6);}
  .split .sp-i{background:linear-gradient(90deg,#F2C55C,#F59E6B);}
  .sh-leg{display:flex;justify-content:space-between;gap:var(--s3);margin-top:var(--s2);
    font-size:12px;color:rgba(255,255,255,.8);}
  .sh-leg span{display:inline-flex;align-items:center;gap:6px;white-space:nowrap;}
  .sh-leg b{width:8px;height:8px;border-radius:3px;display:inline-block;}
  .sh-leg .dp{background:#7FD3DE;} .sh-leg .di{background:#F2C55C;}
  .sh-leg strong{font-weight:700;color:#fff;}

  /* ── KPI tiles: one colour per figure ──────────────────────────────────── */
  .kpigrid,.kpigrid.has4{display:grid;grid-template-columns:repeat(2,1fr);gap:var(--s3);margin-bottom:var(--s3);}
  .kpi{position:relative;overflow:hidden;min-height:112px;border-radius:var(--r3);
    padding:var(--s4);color:#fff;display:flex;flex-direction:column;align-items:flex-start;
    user-select:none;animation:rise .6s var(--ease-out) both;
    transition:transform .22s var(--ease-spring),box-shadow .22s;}
  .kpi:nth-child(1){animation-delay:.12s} .kpi:nth-child(2){animation-delay:.2s}
  .kpi:nth-child(3){animation-delay:.28s} .kpi:nth-child(4){animation-delay:.36s}
  .kpi.c-tur{background:linear-gradient(145deg,#F3B33D,#D7820A);box-shadow:0 10px 22px rgba(215,130,10,.30);}
  .kpi.c-ind{background:linear-gradient(145deg,#5566B8,#2F3D85);box-shadow:0 10px 22px rgba(47,61,133,.30);}
  .kpi.c-lot{background:linear-gradient(145deg,#CF5591,#962C61);box-shadow:0 10px 22px rgba(150,44,97,.30);}
  .kpi.c-kum{background:linear-gradient(145deg,#C02E5A,#7E1638);box-shadow:0 10px 22px rgba(126,22,56,.32);}
  .kpi.c-leaf{background:linear-gradient(145deg,#3FA56B,#1E6E43);box-shadow:0 10px 22px rgba(30,110,67,.30);}
  .kpi.c-due{display:none;}
  .kpi::before{content:'';position:absolute;inset:0;pointer-events:none;
    background:radial-gradient(120% 90% at 100% 0%,rgba(255,255,255,.22),transparent 50%);}
  .kpi .shimmer{position:absolute;top:0;bottom:0;left:0;width:45%;pointer-events:none;
    background:linear-gradient(90deg,transparent,rgba(255,255,255,.28),transparent);
    transform:translateX(-120%) skewX(-18deg);animation:shine 1.1s var(--ease-out) .7s 1 both;}
  .kpi:nth-child(2) .shimmer{animation-delay:.8s} .kpi:nth-child(3) .shimmer{animation-delay:.9s}
  .kpi:nth-child(4) .shimmer{animation-delay:1s}
  .kpi .sheen{display:none;}
  .kpi>*:not(.shimmer){position:relative;z-index:1;}
  .kpi:active{transform:scale(.98);}
  .kpi .khead{display:flex;justify-content:space-between;align-items:flex-start;gap:var(--s2);width:100%;}
  .kpi .klab{font-size:13px;font-weight:600;line-height:1.3;opacity:.95;}
  .kpi .kico{width:34px;height:34px;flex:0 0 34px;border-radius:11px;display:grid;place-items:center;
    background:rgba(255,255,255,.2);border:1px solid rgba(255,255,255,.22);}
  .kpi .kico svg{width:18px;height:18px;}
  .kpi .kval{font-size:25px;font-weight:700;letter-spacing:-.3px;line-height:1.1;margin-top:auto;padding-top:var(--s3);}
  .kpi .ksub{font-size:11.5px;opacity:.82;margin-top:2px;}
  .kpi .kbar{height:4px;border-radius:var(--rp);background:rgba(255,255,255,.22);margin-top:var(--s2);width:100%;overflow:hidden;}
  .kpi .kbar i{display:block;height:100%;border-radius:inherit;background:rgba(255,255,255,.92);width:0;transition:width 1.1s var(--ease-out);}
  .kpi-over{cursor:pointer;}
  .kpi-over .ktap{font-size:11px;font-weight:700;opacity:.9;display:flex;align-items:center;gap:3px;margin-top:2px;}

  .stale{background:var(--t-turmeric);border:1px solid #F1D49A;border-radius:var(--r2);
    padding:var(--s3);font-size:12.5px;color:#7A5200;line-height:1.55;margin-bottom:var(--s3);
    animation:cardIn .45s var(--ease-out) .05s both;}

  /* ── Settle-everything band ────────────────────────────────────────────── */
  .settle{display:grid;grid-template-columns:1fr auto;align-items:center;gap:var(--s4);
    background:var(--card);border-radius:var(--r3);padding:var(--s4);margin-bottom:var(--s3);
    border-left:5px solid var(--leaf);box-shadow:var(--shadow-2);animation:cardIn .45s var(--ease-out) .4s both;}
  .settle .st-t{font-size:14px;font-weight:700;color:var(--ink);line-height:1.35;}
  .settle .st-s{font-size:12px;color:var(--ink-3);margin-top:2px;line-height:1.4;}
  .settle .st-om{font-size:11.5px;color:#9A5B00;margin-top:var(--s2);line-height:1.5;}
  .settle .st-r{text-align:right;}
  .settle .st-v{font-size:21px;font-weight:700;color:var(--green);line-height:1.1;}
  .settle .st-b{display:inline-flex;align-items:center;justify-content:center;height:var(--ctl-sm);
    margin-top:var(--s2);padding:0 var(--s4);text-decoration:none;font-size:12.5px;font-weight:700;
    border-radius:var(--rp);background:linear-gradient(135deg,#3FA56B,#1E6E43);color:#fff;
    box-shadow:0 5px 14px rgba(30,110,67,.28);transition:transform .15s var(--ease-spring);}
  .settle .st-b:active{transform:scale(.95);}

  /* ── Toolbar & sort chips ──────────────────────────────────────────────── */
  .tools,.sortbar{display:flex;align-items:center;gap:var(--s2);margin-bottom:var(--s3);
    overflow-x:auto;padding:2px 0;scrollbar-width:none;animation:fadeUp .45s var(--ease-out) .45s both;}
  .tools::-webkit-scrollbar,.sortbar::-webkit-scrollbar{display:none;}
  .tools .tl,.sortbar .chip{flex:0 0 auto;height:var(--ctl-sm);display:inline-flex;align-items:center;gap:6px;
    border:1px solid var(--line);background:var(--card);color:var(--ink-2);border-radius:var(--rp);
    padding:0 var(--s3);font:inherit;font-size:12.5px;font-weight:600;cursor:pointer;white-space:nowrap;
    box-shadow:var(--shadow-1);transition:transform .15s var(--ease-spring),background .18s,color .18s;}
  .tools .tl:active,.sortbar .chip:active{transform:scale(.95);}
  .tsz{flex:0 0 auto;display:inline-flex;align-items:center;gap:2px;height:var(--ctl-sm);margin-left:auto;
    background:var(--card);border:1px solid var(--line);border-radius:var(--rp);padding:0 3px;box-shadow:var(--shadow-1);}
  .tsz button{border:none;background:transparent;color:var(--ink-3);font-family:inherit;font-weight:700;
    height:28px;min-width:30px;border-radius:var(--rp);cursor:pointer;line-height:1;}
  .tsz button.on{background:var(--peacock);color:#fff;}
  .sortbar .sl{flex:0 0 auto;font-size:12.5px;font-weight:600;color:var(--ink-3);margin-right:2px;}
  .sortbar .chip.on{background:var(--peacock);border-color:var(--peacock);color:#fff;box-shadow:0 4px 12px rgba(15,76,92,.25);}

  /* ── Pledge card ───────────────────────────────────────────────────────── */
  .pcard{background:var(--card);border-radius:var(--r4);padding:var(--s4) var(--s4) var(--s4) calc(var(--s4) + 3px);
    scroll-margin-top:74px;margin-bottom:var(--s3);position:relative;overflow:hidden;box-shadow:var(--shadow-2);
    opacity:0;transform:translateY(20px) scale(.98);
    transition:opacity .55s var(--ease-out),transform .55s var(--ease-out),box-shadow .25s;}
  .pcard.vis{opacity:1;transform:none;}
  .pcard::before{content:'';position:absolute;left:0;top:0;bottom:0;width:5px;background:var(--leaf);}
  .pcard.is-over::before{background:linear-gradient(180deg,#C02E5A,#7E1638);}
  .pcard .top{display:flex;justify-content:space-between;align-items:flex-start;gap:var(--s3);margin-bottom:var(--s4);}
  .pcard .bill{display:inline-block;font-size:11.5px;color:var(--peacock);font-weight:700;letter-spacing:.3px;
    background:var(--t-peacock);border-radius:var(--rp);padding:2px 9px;}
  .pcard .item{font-size:16px;font-weight:700;color:var(--ink);margin-top:6px;line-height:1.3;}
  .badge{font-size:11.5px;font-weight:700;border-radius:var(--rp);padding:5px 10px;white-space:nowrap;flex-shrink:0;line-height:1.3;}
  .badge.ok{background:var(--t-leaf);color:var(--green);}
  .badge.due{background:var(--t-kumkum);color:var(--red);animation:popIn .4s ease both,badgeGlow 2.2s ease-in-out 1s 3;}

  .kv{display:grid;grid-template-columns:1fr 1fr;gap:var(--s4) var(--s3);font-size:13px;margin-bottom:var(--s4);}
  .kv>div{min-width:0;}
  .kv .k{color:var(--ink-4);font-size:12px;font-weight:500;line-height:1.3;}
  .kv .v{font-weight:700;color:var(--ink);margin-top:2px;line-height:1.35;min-height:19px;
    display:flex;align-items:center;flex-wrap:wrap;gap:2px;font-size:14px;}

  .ering{display:flex;align-items:center;gap:var(--s2);}
  .ering svg{width:34px;height:34px;flex-shrink:0;transform:rotate(-90deg);}
  .ering circle{fill:none;stroke-width:3.6;}
  .ering .bgc{stroke:var(--t-peacock);}
  .ering .fgc{stroke:var(--peacock-l);stroke-linecap:round;stroke-dasharray:var(--ring-c);
    stroke-dashoffset:var(--ring-off);animation:ringDash 1.1s var(--ease-out) .3s both;}
  .ering .fgc.hot{stroke:var(--kumkum);}
  .ering .etxt{line-height:1.35;font-size:12.5px;color:var(--ink)!important;}
  .ering .etxt span{color:var(--ink-4)!important;font-size:11.5px!important;font-weight:500!important;}

  .duebar{display:flex;justify-content:space-between;align-items:center;gap:var(--s3);
    background:var(--t-turmeric);border-radius:var(--r2);padding:var(--s3) var(--s4);margin-bottom:var(--s2);min-height:56px;}
  .duebar .l{font-size:13px;color:#8A5800;font-weight:600;line-height:1.35;}
  .duebar .v{font-size:21px;font-weight:700;color:#5E3B00;white-space:nowrap;}
  .duebar.zero{background:var(--t-leaf);}
  .duebar.zero .l,.duebar.zero .v{color:var(--green);}
  .duebar.zero .v{font-size:17px;}
  .mnote{font-size:12px;color:var(--ink-4);line-height:1.55;margin-bottom:var(--s3);}

  .jph{width:100%;max-height:200px;object-fit:cover;border-radius:var(--r2);margin:0 0 var(--s3);
    border:1px solid var(--line);background:var(--card-2);display:block;animation:fadeUp .4s var(--ease-out) both;}
  .rnw-tag{display:inline-block;margin-bottom:var(--s3);font-size:12px;font-weight:700;color:#8A5800;
    background:var(--t-turmeric);border-radius:var(--rp);padding:5px 11px;}
  .renew{margin-bottom:var(--s3);padding:var(--s3) var(--s4);border-radius:var(--r2);background:var(--t-indigo);}
  .renew .rn-t{font-size:13px;font-weight:700;color:var(--indigo);}
  .renew .rn-s{font-size:12.5px;color:#46518A;margin-top:3px;line-height:1.55;}

  /* ── Planner ───────────────────────────────────────────────────────────── */
  .planner{margin-bottom:var(--s3);padding:var(--s3) var(--s4) var(--s4);border-radius:var(--r2);
    background:var(--card-2);border:1px solid var(--line);}
  .planner .pl-h{font-size:13px;font-weight:700;color:var(--ink-2);margin-bottom:var(--s2);}
  .planner .pl-r{display:grid;grid-template-columns:1fr auto;gap:var(--s2);align-items:stretch;}
  .planner input[type=date]{height:var(--ctl);width:100%;min-width:0;font:inherit;font-size:14px;font-weight:600;
    color:var(--ink);padding:0 var(--s2) 0 var(--s3);border:1.5px solid var(--line-2);border-radius:var(--r1);
    background:#fff;-webkit-appearance:none;appearance:none;display:flex;align-items:center;}
  .planner input[type=date]::-webkit-calendar-picker-indicator{margin-left:auto;padding-left:4px;opacity:.6;}
  .planner input[type=date]:focus{outline:none;border-color:var(--peacock);box-shadow:0 0 0 3px rgba(15,76,92,.14);}
  .planner .pl-rem{height:var(--ctl);display:inline-flex;align-items:center;gap:5px;font:inherit;font-size:13px;
    font-weight:700;color:var(--peacock);padding:0 var(--s3);border:1.5px solid var(--line-2);border-radius:var(--r1);
    background:#fff;cursor:pointer;white-space:nowrap;transition:transform .15s var(--ease-spring),background .18s;}
  .planner .pl-rem:active{transform:scale(.96);background:var(--t-peacock);}
  .planner .pl-o:not(:empty){margin-top:var(--s3);padding-top:var(--s3);border-top:1px dashed var(--line-2);}
  .planner .pl-tot{display:flex;justify-content:space-between;align-items:baseline;gap:var(--s2);
    font-size:13px;color:var(--ink-3);animation:fadeUp .3s var(--ease-out) both;}
  .planner .pl-tot b{font-size:18px;color:var(--ink);}
  .planner .pl-d{margin-top:4px;font-size:12.5px;font-weight:600;}
  .planner .pl-d .up{color:#B4520F;} .planner .pl-d .ok{color:var(--green);}
  .planner .pw{font-size:12.5px;color:var(--red);font-weight:700;}

  /* ── Pay row ───────────────────────────────────────────────────────────── */
  .payrow{border-top:1px solid var(--line);padding-top:var(--s4);}
  .payrow .pl,.cfm .pl{font-size:13px;font-weight:700;color:var(--ink-2);margin-bottom:var(--s2);display:flex;align-items:center;gap:5px;}
  .payamt{display:grid;grid-template-columns:auto 1fr;align-items:center;gap:var(--s3);margin-bottom:var(--s2);}
  .payamt span{font-size:13px;font-weight:600;color:var(--ink-3);white-space:nowrap;}
  .payamt input{height:var(--ctl);width:100%;min-width:0;padding:0 var(--s3);border:1.5px solid var(--line-2);
    border-radius:var(--r1);font-family:inherit;font-size:17px;font-weight:700;color:var(--ink);background:#fff;outline:none;
    transition:border-color .2s,box-shadow .2s;}
  .payamt input:focus{border-color:var(--peacock);box-shadow:0 0 0 3px rgba(15,76,92,.14);}
  .paybtns{display:grid;grid-template-columns:repeat(4,1fr);gap:var(--s2);}
  .paybtns a{height:var(--ctl);display:flex;align-items:center;justify-content:center;text-decoration:none;
    font-size:12.5px;font-weight:700;border-radius:var(--r1);border:1px solid var(--line);background:#fff;
    text-align:center;line-height:1.2;transition:transform .15s var(--ease-spring),box-shadow .15s;}
  .paybtns a:active{transform:scale(.95);}
  .paybtns .wa{grid-column:1/-1;color:#fff;font-size:13.5px;border:none;
    background:linear-gradient(135deg,var(--wa),var(--wa-2));box-shadow:0 5px 14px rgba(18,140,126,.24);}
  .paybtns .gp{color:#1a73e8;} .paybtns .pp{color:#5f259f;} .paybtns .pt{color:#0091c7;}
  .paybtns .up{color:var(--peacock);background:var(--t-peacock);border-color:transparent;}

  .cfm{border-top:1px solid var(--line);margin-top:var(--s4);padding-top:var(--s4);}
  .cfm input{height:var(--ctl);width:100%;padding:0 var(--s3);border:1.5px solid var(--line-2);border-radius:var(--r1);
    font-size:14px;font-weight:600;color:var(--ink);background:#fff;outline:none;margin-bottom:var(--s2);font-family:inherit;
    transition:border-color .2s,box-shadow .2s;}
  .cfm input:focus{border-color:var(--leaf);box-shadow:0 0 0 3px rgba(46,139,87,.14);}
  .cfm .cfb{height:var(--ctl);display:flex;align-items:center;justify-content:center;text-decoration:none;
    font-size:14px;font-weight:700;border-radius:var(--r1);background:linear-gradient(135deg,#3FA56B,#1E6E43);color:#fff;
    box-shadow:0 5px 14px rgba(30,110,67,.24);transition:transform .15s var(--ease-spring);}
  .cfm .cfb:active{transform:scale(.97);}

  /* ── Payment history ───────────────────────────────────────────────────── */
  .hist{border-top:1px solid var(--line);margin-top:var(--s4);padding-top:var(--s3);}
  .hist summary{font-size:13px;font-weight:700;color:var(--peacock);cursor:pointer;list-style:none;
    display:flex;align-items:center;gap:6px;user-select:none;min-height:28px;}
  .hist summary::-webkit-details-marker{display:none;}
  .hist summary::before{content:'▸';transition:transform .2s;}
  .hist[open] summary::before{transform:rotate(90deg);}
  .hist table{width:100%;border-collapse:collapse;margin-top:var(--s2);font-size:13px;}
  .hist td{padding:8px 4px;border-bottom:1px solid var(--line);vertical-align:middle;}
  .hist td:last-child{text-align:right;font-weight:700;color:var(--green);white-space:nowrap;}
  .hist .hk{font-size:11.5px;background:var(--t-peacock);color:var(--peacock);border-radius:var(--rp);padding:2px 8px;font-weight:600;display:inline-block;}

  /* ── Closed pledges ────────────────────────────────────────────────────── */
  .sect-title{font-size:16px;font-weight:700;color:var(--ink);margin:var(--s6) 2px var(--s3);
    display:flex;align-items:center;gap:var(--s2);animation:fadeUp .4s var(--ease-out) both;}
  .sect-title::before{content:'';width:8px;height:8px;transform:rotate(45deg);background:var(--zari);border-radius:2px;}
  .ccard{display:flex;justify-content:space-between;align-items:center;gap:var(--s3);background:var(--card);
    border-radius:var(--r2);padding:var(--s3) var(--s4);margin-bottom:var(--s2);box-shadow:var(--shadow-1);
    opacity:0;transform:translateY(14px);transition:opacity .5s var(--ease-out),transform .5s var(--ease-out);}
  .ccard.vis{opacity:1;transform:none;}
  .ccard .ci{min-width:0;}
  .ccard .cb{font-size:12px;color:var(--peacock);font-weight:700;}
  .ccard .cn2{font-size:14px;font-weight:700;color:var(--ink);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;margin-top:1px;}
  .ccard .cd{font-size:12px;color:var(--ink-4);margin-top:1px;}
  .ccard .cst{font-size:11.5px;font-weight:700;border-radius:var(--rp);padding:5px 10px;flex-shrink:0;background:var(--t-leaf);color:var(--green);}
  .ccard .cst.fc{background:var(--t-kumkum);color:var(--red);}

  /* ── Footer / contact strip ────────────────────────────────────────────── */
  .foot{margin-top:var(--s6);animation:fadeUp .5s var(--ease-out) both;}
  .contact{display:grid;grid-template-columns:repeat(3,1fr);gap:var(--s2);margin-bottom:var(--s4);}
  .contact a{height:72px;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:2px;
    text-decoration:none;border-radius:var(--r2);background:var(--card);color:var(--ink);font-size:13px;font-weight:700;
    box-shadow:var(--shadow-1);transition:transform .15s var(--ease-spring);}
  .contact a .ci2{font-size:19px;line-height:1;}
  .contact a .cph{font-size:11px;font-weight:500;color:var(--ink-4);}
  .contact a:active{transform:scale(.96);}
  .contact a.wa2{background:linear-gradient(135deg,var(--wa),var(--wa-2));color:#fff;}
  .callbtn{display:inline-flex;align-items:center;justify-content:center;gap:7px;width:100%;height:var(--ctl);
    background:var(--card);color:var(--peacock);border-radius:var(--rp);font-size:14px;font-weight:700;text-decoration:none;box-shadow:var(--shadow-1);}
  .foot .addr{font-size:12.5px;color:var(--ink-3);margin-top:var(--s3);line-height:1.6;text-align:center;}
  .foot .note{font-size:11.5px;color:var(--ink-4);margin-top:var(--s4);line-height:1.7;text-align:center;}
  .badlink{background:var(--card);border-radius:var(--r3);padding:var(--s6) var(--s5);text-align:center;
    font-size:14px;color:var(--ink-3);line-height:1.7;box-shadow:var(--shadow-2);}

  /* ── Back-to-top & toast ───────────────────────────────────────────────── */
  #totop{position:fixed;right:var(--s4);bottom:var(--s4);z-index:41;display:none;width:48px;height:48px;border-radius:16px;
    border:none;background:var(--peacock);color:var(--zari);font-size:18px;cursor:pointer;align-items:center;justify-content:center;
    box-shadow:0 8px 22px rgba(10,51,64,.35);}
  #totop.on{display:flex;animation:fabIn .3s var(--ease-spring) both;}
  #totop:active{transform:scale(.92);}
  #pbtoast{position:fixed;left:50%;bottom:84px;transform:translate(-50%,0);z-index:60;background:var(--peacock-d);color:#fff;
    border-radius:var(--rp);padding:10px 18px;font-size:13px;font-weight:700;box-shadow:0 10px 30px rgba(10,51,64,.35);display:none;}
  #pbtoast.on{display:block;animation:okPop 2.4s var(--ease-out) both;}

  .psheet{display:none;}

  /* ── Print: A4 statement ───────────────────────────────────────────────── */
  @media print{
    @page{size:A4 portrait;margin:11mm 11mm 14mm;}
    html{font-size:13.5px!important;}
    body{background:#fff!important;color:#1A1209!important;padding:0!important;margin:0!important;}
    .no-print,.lockwrap,.langbar,.paybtns,.payrow,.planner,.pl-rem,.confirm,.cfm,.cta,
    .sortbar,.tools,.st-b,#pblive,.stale,.live-note,.foot,.note,.contact,
    .hdr,.tag,#stickybar,#totop,#pbtoast,.aurora,
    input,textarea,button,select{display:none!important;}
    .pcard,.ccard,.rv,.settle,.kpi{opacity:1!important;transform:none!important;}
    *{-webkit-print-color-adjust:exact!important;print-color-adjust:exact!important;
      animation:none!important;transition:none!important;}
    .psheet{display:block!important;margin:0 0 9px;}
    .psheet .ph-band{background:linear-gradient(135deg,#1A3A6A 0%,#2C6EB0 100%);color:#fff;
      border-radius:9px;padding:11px 15px;display:flex;justify-content:space-between;
      align-items:center;gap:14px;}
    .psheet .ph-shop{font-size:17px;font-weight:800;color:#FFD98A;letter-spacing:.2px;line-height:1.2;}
    .psheet .ph-addr{font-size:8.5px;opacity:.85;margin-top:3px;line-height:1.4;max-width:118mm;}
    .psheet .ph-tag{text-align:right;font-size:11px;font-weight:800;line-height:1.45;}
    .psheet .ph-tag span{display:block;font-size:9px;color:#FFD98A;font-weight:700;}
    .psheet .ph-cust{display:flex;justify-content:space-between;gap:12px;flex-wrap:wrap;
      border:1px solid #D8DEE7;border-left:3px solid #2C6EB0;border-radius:7px;
      padding:7px 12px;margin-top:7px;font-size:10px;}
    .psheet .ph-cust b{color:#1A3A6A;}
    .kpigrid,.kpigrid.has4{display:grid!important;grid-template-columns:none!important;grid-auto-flow:column!important;grid-auto-columns:1fr!important;
      gap:6px!important;margin:0 0 9px!important;break-inside:avoid;}
    .kpi{border-radius:9px!important;padding:9px 10px!important;color:#fff!important;
      box-shadow:none!important;border:none!important;min-height:0!important;break-inside:avoid;}
    .kpi .kico{width:19px!important;height:19px!important;font-size:10px!important;margin-bottom:5px!important;}
    .kpi .kval{font-size:14px!important;color:#fff!important;}
    .kpi .klab{font-size:6.5px!important;margin-bottom:5px!important;color:#fff!important;opacity:.92;}
    .kpi .ktap,.kpi .shimmer{display:none!important;}
    .kpi.c-due{display:flex!important;background:linear-gradient(145deg,#1B6B7E,#0A3340)!important;}
    .kpi .kval{padding-top:4px!important;font-size:11.5px!important;white-space:nowrap;} .kpi .kico,.kpi .ksub{display:none!important;}
    .kpi .klab{font-size:8px!important;text-transform:none!important;letter-spacing:0!important;}
    .kpi .kbar{height:2.5px!important;}
    .kpi::before,.kpi::after{display:none!important;}
    .settle{display:grid!important;background:linear-gradient(135deg,#12572F,#0C3D21)!important;
      border:none!important;border-radius:9px!important;padding:10px 15px!important;
      margin:0 0 10px!important;break-inside:avoid;}
    .settle .st-t{font-size:11.5px!important;color:#CFF3DE!important;}
    .settle .st-s,.settle .st-om{color:#A9DCC0!important;}
    .settle .st-v{font-size:18px!important;color:#fff!important;}
    .sumhero{display:none!important;}
    .pcard{background:#fff!important;border:1px solid #C9D2DE!important;
      border-left:3px solid #C9A84C!important;border-radius:8px!important;box-shadow:none!important;
      color:#1A1209!important;padding:10px 12px!important;margin:0 0 8px!important;
      break-inside:avoid;page-break-inside:avoid;}
    .pcard *{color:#1A1209!important;}
    .pcard .num,.pcard b{color:#0F2E5E!important;}
    .pcard .duebar{background:#FFF8E6!important;border:1px solid #E8CF8E!important;min-height:0!important;}
    .pcard .duebar *{color:#7A5C00!important;}
    /* a settled pledge must not print looking like money owed */
    .pcard .duebar.zero{background:#E8F6EE!important;border:1px solid #B7E0C8!important;}
    .pcard .duebar.zero *{color:#12572F!important;}
    .renew{background:#EEF4FF!important;border:1px solid #C3D6F5!important;break-inside:avoid;}
    .renew *{color:#1A4A8C!important;}
    .rnw-tag{background:#FFF3E0!important;border:1px solid #F0C97A!important;color:#8A5A00!important;}
    .jph{max-height:26mm!important;object-fit:cover;border:1px solid #D8DEE7!important;}
    .cst{background:#E8F6EE!important;color:#12572F!important;border:1px solid #B7E0C8!important;}
    .psheet .ph-foot{display:block!important;margin-top:10px;padding-top:7px;
      border-top:1px solid #D8DEE7;font-size:8px;color:#6B7280;line-height:1.55;text-align:center;}
  }

  /* ── Small phones ──────────────────────────────────────────────────────── */
  @media (max-width:360px){
    .kpigrid{grid-template-columns:repeat(2,1fr);}
    .kv{grid-template-columns:1fr;}
    .settle{grid-template-columns:1fr;gap:var(--s3);}
    .settle .st-r{text-align:left;}
    .paybtns{grid-template-columns:repeat(2,1fr);}
  }

  /* ── Reduced motion ────────────────────────────────────────────────────── */
  @media (prefers-reduced-motion: reduce){
    *,*::before,*::after{animation-duration:.001s!important;animation-iteration-count:1!important;
      transition-duration:.001s!important;}
    .pcard,.ccard{opacity:1;transform:none;}
    html{scroll-behavior:auto;}
  }

  /* v14 — duplicate receipt notice on a pledge card */
  .dup-tag{display:block;margin:0 0 var(--s3);padding:9px 12px;border-radius:var(--r1,10px);
    font-size:11.5px;font-weight:700;line-height:1.5;background:#FDF0E6;border:1px solid #E8C9A6;color:#8A4B12;}
  @media print{ .dup-tag{background:#fff!important;color:#000!important;border:1px solid #444!important;} }
</style>
</head>
<body>
<div class="aurora"></div>
<div id="stickybar" aria-hidden="true">
  <div class="sb-nm" id="sb-nm"></div>
  <div><span class="sb-l" id="sb-l"></span><span class="sb-v num" id="sb-v"></span></div>
</div>
<button id="totop" type="button" aria-label="Back to top" onclick="_pbTop()">&#8593;</button>
<div id="pbtoast" role="status" aria-live="polite"></div>
<header class="hdr"><div class="hin">
  <div class="hrow">
    <div class="mark" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linejoin="round"><path d="M6 3h12l4 6-10 12L2 9z"/><path d="M2 9h20M9 3 7.5 9 12 21l4.5-12L15 3"/></svg></div>
    <div class="hname"><div class="shop" id="h-shop">Passbook</div><div class="shopTa" id="h-shopta" style="display:none;"></div></div>
    <div class="langbar"><button id="lang-en" class="on" onclick="setLang('en')">EN</button><button id="lang-ta" onclick="setLang('ta')">தமிழ்</button></div>
  </div>
  <div class="tag"><span class="dot"></span><span data-i="live">Live dues — calculated fresh every time you open this</span></div>
</div></header>
<div class="wrap">

  <svg width="0" height="0" style="position:absolute" aria-hidden="true">
    <filter id="lgWarp">
      <feTurbulence type="fractalNoise" baseFrequency="0.014 0.016" numOctaves="2" seed="7" result="n"/>
      <feDisplacementMap in="SourceGraphic" in2="n" scale="14" xChannelSelector="R" yChannelSelector="G"/>
    </filter>
  </svg>

  <!-- PIN GATE -->
  <div class="gate" id="gate">
    <div class="lock" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><rect x="4.5" y="10.5" width="15" height="10.5" rx="3"/><path d="M8 10.5V7.5a4 4 0 0 1 8 0v3"/><circle cx="12" cy="15.6" r="1.4" fill="currentColor"/></svg></div>
    <h2 data-i="gt">Enter your PIN</h2>
    <div class="cn" id="g-cn"></div>
    <p data-i="gp">This passbook is protected. Enter the PIN given to you by the shop.</p>
    <div class="lg-stage"><div class="lg-pins" id="lg-pins"></div></div>
    <input id="pin" type="password" inputmode="numeric" autocomplete="off" aria-label="PIN" maxlength="12" onkeydown="if(event.key==='Enter')unlock()" oninput="pinSync()" style="position:absolute;opacity:0;width:1px;height:1px;pointer-events:none;">
    <div class="lg-pad" id="lg-pad"></div>
    <div class="errmsg" id="g-err"></div>
    <button class="ubtn" onclick="unlock()" data-i="gb">Unlock passbook</button>
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
// Customer Passbook Viewer v14 — Sivaji Bank Pawnshop Manager
// Data arrives compressed in the URL fragment (#...) — nothing is ever sent
// to any server. PIN gate is a privacy speed-bump, matching the app's model.
// Supports payload v1 (active pledges only) and v2 (+ payment history,
// closed pledges, UPI Pay-Now, shop address).
// v10: latest-gen UI — animated KPI cards (count-up + orbs + sheen + shimmer,
// dashboard parity with main app v183), elapsed progress ring, scroll-reveal
// cards, animated unlock. Calculation engine unchanged from v9.
// ═══════════════════════════════════════════════════════════════════════════
let P = null;          // decoded payload
let LIVE = null;       // {url,id,key} when this card is a live one

function b64uDec(str) {
  str = String(str).replace(/-/g, '+').replace(/_/g, '/');
  while (str.length % 4) str += '=';
  const bin = atob(str), out = new Uint8Array(bin.length);
  for (let i = 0; i < bin.length; i++) out[i] = bin.charCodeAt(i);
  return out;
}

// The key travels in the URL fragment, which browsers never transmit, so the
// server holding this blob cannot read it and neither can anyone who copies it
// out of storage.
function pbDecrypt(keyB64u, blobB64u) {
  const raw = b64uDec(blobB64u);
  return crypto.subtle.importKey('raw', b64uDec(keyB64u), 'AES-GCM', false, ['decrypt'])
    .then(k => crypto.subtle.decrypt({ name: 'AES-GCM', iv: raw.slice(0, 12) }, k, raw.slice(12)))
    .then(pt => JSON.parse(new TextDecoder().decode(pt)));
}
let LANG = localStorage.getItem('pb_lang') || 'en';
let FIRST_RENDER = true;   // count-up runs only on the first render, not on language toggle

const I18N = {
  live:{en:'Live dues — calculated fresh every time you open this', ta:'நேரடி நிலுவை — ஒவ்வொரு முறையும் புதிதாக கணக்கிடப்படுகிறது'},
  gt:{en:'Enter your PIN', ta:'உங்கள் PIN-ஐ உள்ளிடவும்'},
  gp:{en:'This passbook is protected. Enter the PIN given to you by the shop.', ta:'இந்த பாஸ்புக் பாதுகாக்கப்பட்டது. கடையில் வழங்கிய PIN-ஐ உள்ளிடவும்.'},
  gb:{en:'Unlock passbook', ta:'பாஸ்புக்கைத் திற'},
  wrong:{en:'Wrong PIN — please try again', ta:'தவறான PIN — மீண்டும் முயற்சிக்கவும்'},
  dupNote:{en:'🧾 Duplicate receipt #N — the original receipt is cancelled. Bring this duplicate when you come to redeem.', ta:'🧾 நகல் ரசீது #N — அசல் ரசீது ரத்து. மீட்கும்போது இந்த நகல் ரசீதை கொண்டு வாருங்கள்.'},
  active:{en:'Active', ta:'செயலில்'}, duetoday:{en:'Due Today', ta:'இன்று செலுத்த'}, principal:{en:'Principal', ta:'அசல்'},
  overdueN:{en:'Overdue', ta:'தாமதம்'},
  activeK:{en:'Open pledges', ta:'நடப்பு அடகுகள்'}, overdueK:{en:'Past due date', ta:'கெடு தாண்டியவை'},
  intK:{en:'Interest so far', ta:'இதுவரை வட்டி'}, intSub:{en:'added to the loan', ta:'கடனுடன் சேர்ந்தது'},
  prSub:{en:'amount you borrowed', ta:'நீங்கள் பெற்ற தொகை'}, openK:{en:'still with the shop', ta:'கடையில் உள்ளவை'},
  closedK:{en:'#N closed recently', ta:'சமீபத்தில் #N முடிந்தது'}, nextDue:{en:'Next due date', ta:'அடுத்த கெடு'},
  inDays:{en:'in #D days', ta:'#D நாளில்'}, noneDue:{en:'nothing due', ta:'கெடு இல்லை'}, billK:{en:'Bill', ta:'பில்'},
  tapOver:{en:'tap to view', ta:'பார்க்க தட்டவும்'},
  planTitle:{en:'Planning to pay later?', ta:'பின்னர் செலுத்த திட்டமா?'},
  planPick:{en:'Pick a date', ta:'தேதியைத் தேர்வு செய்க'},
  planTot:{en:'Total on that day', ta:'அன்றைய மொத்தம்'},
  planMore:{en:'more than today', ta:'இன்றை விட அதிகம்'},
  planSame:{en:'same as today', ta:'இன்று போலவே'},
  remind:{en:'Remind me', ta:'நினைவூட்டு'},
  days:{en:'days', ta:'நாட்கள்'},
  settleT:{en:'Settle everything today', ta:'இன்று அனைத்தையும் அடைக்க'},
  settleS:{en:'the #N pledges shown here', ta:'இங்கு காட்டப்படும் #N அடகுகள்'},
  omitN:{en:'#N older pledge(s) are not shown here — please ask the shop',
         ta:'#N பழைய அடகு(கள்) இங்கு இல்லை — கடையில் கேட்கவும்'},
  settlePay:{en:'Pay total now', ta:'மொத்தமும் செலுத்து'},
  remindAll:{en:'Remind me about all', ta:'அனைத்தையும் நினைவூட்டு'},
  txtSize:{en:'Text size', ta:'எழுத்து அளவு'},
  directions:{en:'Directions to shop', ta:'கடைக்கு வழி'},
  printBtn:{en:'Print / Save PDF', ta:'அச்சிடு / PDF'},
  renewT:{en:'Renew instead of closing', ta:'முடிக்காமல் புதுப்பிக்க'},
  renewS:{en:'Pay just the interest #A — then no further interest until #D',
          ta:'வட்டி #A மட்டும் செலுத்தினால் — #D வரை கூடுதல் வட்டி இல்லை'},
  renewedN:{en:'Renewed #N time(s)', ta:'#N முறை புதுப்பிக்கப்பட்டது'},
  renewedOn:{en:'last on #D', ta:'கடைசியாக #D'},
  photoAlt:{en:'Pledged item', ta:'அடகு பொருள்'},
  srtDue:{en:'Due date', ta:'கெடு தேதி'}, srtAmt:{en:'Amount', ta:'தொகை'},
  srtNew:{en:'Newest', ta:'புதியது'}, srtOver:{en:'Overdue first', ta:'தாமதம் முதலில்'},
  sortBy:{en:'Sort', ta:'வரிசை'},
  asof:{en:'Data as of', ta:'தரவு தேதி'},
  snap:{en:'card made', ta:'அட்டை தேதி'},
  stmtT:{en:'PLEDGE STATEMENT', ta:'அடகு அறிக்கை'},
  stmtS:{en:'Customer copy', ta:'வாடிக்கையாளர் பிரதி'},
  stmtCust:{en:'Customer', ta:'வாடிக்கையாளர்'},
  stmtFoot:{en:'Computer-generated statement · valid without signature. Dues are calculated to the date shown above and may change. Please verify at the shop before settlement.',
            ta:'கணினி மூலம் உருவாக்கப்பட்டது · கையொப்பம் தேவையில்லை. மேலே உள்ள தேதிக்கான கணக்கு. செலுத்தும் முன் கடையில் உறுதி செய்யவும்.'},
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
  closed:{en:'Recently closed pledges', ta:'சமீபத்தில் முடிந்த அடகுகள்'},
  redeemed:{en:'Redeemed', ta:'மீட்கப்பட்டது'}, foreclosed:{en:'Settled', ta:'முடிக்கப்பட்டது'},
  call:{en:'📞 Call Shop', ta:'📞 கடையை அழை'},
  callShort:{en:'Call', ta:'அழை'},
  dirShort:{en:'Directions', ta:'வழி'},
  sentOk:{en:'✅ Opening WhatsApp — press send', ta:'✅ வாட்ஸ்அப் திறக்கிறது — அனுப்பவும்'},
  privacy:{en:'Your details live only inside this link — nothing is stored on any server. Keep the link and PIN private.', ta:'உங்கள் விவரங்கள் இந்த இணைப்பில் மட்டுமே உள்ளன — எந்த சர்வரிலும் சேமிக்கப்படவில்லை. இணைப்பையும் PIN-ஐயும் பாதுகாப்பாக வைக்கவும்.'},
  badlink:{en:'⚠️ This passbook link is incomplete or damaged.<br>Please ask the shop to share it again.', ta:'⚠️ இந்த பாஸ்புக் இணைப்பு முழுமையற்றது.<br>கடையில் மீண்டும் கேட்கவும்.'}
};
const PBI = (function(){ const w = b => '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">' + b + '</svg>';
  return { ring: w('<circle cx="12" cy="14" r="6"/><path d="M9.5 4h5l1.5 3.2-4 2.3-4-2.3z"/>'), bank: w('<path d="M3 10l9-6 9 6"/><path d="M5 10v8M9.5 10v8M14.5 10v8M19 10v8M3 20h18"/>'),
    clock: w('<circle cx="12" cy="12" r="8.5"/><path d="M12 7.5V12l3 2"/>'), alert: w('<path d="M12 3.5 2.5 20h19z"/><path d="M12 10v4.5M12 17.2v.3"/>'),
    cal: w('<rect x="3.5" y="5" width="17" height="15.5" rx="2.5"/><path d="M3.5 10h17M8 3v4M16 3v4"/>'), cash: w('<rect x="2.5" y="6" width="19" height="12" rx="2.5"/><circle cx="12" cy="12" r="2.6"/>') }; })();
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

function addDaysISO(iso, n) {
  const d = new Date(iso + 'T00:00:00');
  d.setDate(d.getDate() + n);
  return d.getFullYear() + '-' + String(d.getMonth()+1).padStart(2,'0') + '-' + String(d.getDate()).padStart(2,'0');
}

// The rule in calcDue(): nothing for the first 35 days, then a fresh month of
// interest every 30 days. So the jumps land on day 36, 66, 96 … and the next
// one is always computable from today.
function nextStepUp(it, asOf) {
  const base = it.lp || it.d;
  if (!base) return null;
  const days = daysBetween(base, asOf);
  const b = days < 36 ? 36 : 36 + 30 * (Math.floor((days - 36) / 30) + 1);
  const when = addDaysISO(base, b);
  const now  = calcDue(it, asOf);
  const then = calcDue(it, when);
  const jump = Math.round(then.total - now.total);
  if (jump <= 0) return null;
  return { date: when, jump, inDays: daysBetween(asOf, when) };
}

// A .ics file works with every phone calendar and needs no app or account.
function remindICS(it, dateISO, label) {
  const stamp = dateISO.replace(/-/g, '');
  const uid = 'pb-' + (it.b || 'x') + '-' + stamp + '@sivajibank';
  const ics = [
    'BEGIN:VCALENDAR','VERSION:2.0','PRODID:-//Sivaji Bank//Passbook//EN',
    'BEGIN:VEVENT','UID:' + uid,
    'DTSTAMP:' + stamp + 'T090000Z',
    'DTSTART;VALUE=DATE:' + stamp,
    'SUMMARY:' + label,
    'DESCRIPTION:' + (P.sn || 'Pawnshop') + (P.sp ? ' \u00b7 ' + P.sp : ''),
    'BEGIN:VALARM','TRIGGER:-P1D','ACTION:DISPLAY','DESCRIPTION:' + label,'END:VALARM',
    'END:VEVENT','END:VCALENDAR'
  ].join('\r\n');
  const blob = new Blob([ics], { type: 'text/calendar;charset=utf-8' });
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'pledge-' + (it.b || 'reminder') + '.ics';
  document.body.appendChild(a); a.click();
  setTimeout(function(){ URL.revokeObjectURL(a.href); a.remove(); }, 400);
}
window._pbRemind = function(idx){
  const it = P.p[idx]; if (!it) return;
  const st = nextStepUp(it, todayS());
  const when = st ? st.date : (it.dd || todayS());
  remindICS(it, when, (P.sn || 'Pawnshop') + ' \u00b7 Pledge ' + (it.b || '') );
};

// Recalculates one pledge for a date the customer chooses. calcDue already
// accepts any date, so this is the same engine, not a second one that could
// drift out of step with the counter.
// One number for "how much to walk out clean today", plus a single UPI link.
// The most common question at the counter, and it was previously unanswerable
// without adding the cards up by hand.
// The overdue count is the figure a customer most wants to act on, so the card
// is a shortcut to the pledge itself rather than a dead statistic.
window._pbJumpOverdue = function(){
  const asOf = todayS();
  const idx = P.p.findIndex(it => it.dd && asOf > it.dd);
  if (idx < 0) return;
  const cards = document.querySelectorAll('#book .pcard');
  const el = cards[idx] || cards[0];
  if (!el) return;
  el.scrollIntoView({ behavior: REDUCED ? 'auto' : 'smooth', block: 'center' });
  if (!REDUCED && el.animate) {
    el.animate([{ boxShadow:'0 0 0 0 rgba(201,168,76,0)' },
                { boxShadow:'0 0 0 3px rgba(201,168,76,.8)' },
                { boxShadow:'0 0 0 0 rgba(201,168,76,0)' }],
               { duration:1500, easing:'ease-out' });
  }
};

window._pbSettleAll = function(){
  const t = todayS();
  let total = 0;
  P.p.forEach(function(it){ total += calcDue(it, t).total; });
  return Math.round(total);
};

window._pbRemindAll = function(){
  const t = todayS(), evts = [];
  P.p.forEach(function(it){
    const st = nextStepUp(it, t);
    if (st) evts.push({ it: it, date: st.date });
  });
  if (!evts.length) return;
  const lines = ['BEGIN:VCALENDAR','VERSION:2.0','PRODID:-//Sivaji Bank//Passbook//EN'];
  evts.forEach(function(e){
    const stamp = e.date.replace(/-/g,'');
    lines.push('BEGIN:VEVENT',
      'UID:pb-' + (e.it.b||'x') + '-' + stamp + '@sivajibank',
      'DTSTAMP:' + stamp + 'T090000Z',
      'DTSTART;VALUE=DATE:' + stamp,
      'SUMMARY:' + (P.sn||'Pawnshop') + ' \u00b7 Pledge ' + (e.it.b||''),
      'DESCRIPTION:Interest rises on this date' + (P.sp ? ' \u00b7 ' + P.sp : ''),
      'BEGIN:VALARM','TRIGGER:-P1D','ACTION:DISPLAY',
      'DESCRIPTION:Pledge ' + (e.it.b||'') + ' interest rises tomorrow','END:VALARM',
      'END:VEVENT');
  });
  lines.push('END:VCALENDAR');
  const blob = new Blob([lines.join('\r\n')], { type:'text/calendar;charset=utf-8' });
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'my-pledges.ics';
  document.body.appendChild(a); a.click();
  setTimeout(function(){ URL.revokeObjectURL(a.href); a.remove(); }, 400);
};

// Hands the shop address to whichever map app the phone uses.
window._pbDirections = function(){
  const q = encodeURIComponent([P.sn, P.ad].filter(Boolean).join(', '));
  window.open('https://www.google.com/maps/search/?api=1&query=' + q, '_blank');
};

// Mark everything visible before printing, so a card that was never scrolled
// past still appears on the sheet.
function _pbRevealAllForPrint(){
  document.querySelectorAll('.pcard').forEach(el => el.classList.add('vis'));
  document.querySelectorAll('.rv').forEach(el => el.classList.add('in'));
}
window.addEventListener('beforeprint', _pbRevealAllForPrint);
window._pbPrint = function(){ _pbRevealAllForPrint(); setTimeout(() => window.print(), 60); };

window._pbPlanDate = function(idx){
  const it = P.p[idx]; if (!it) return;
  const inp = document.getElementById('plan-d-' + idx);
  const out = document.getElementById('plan-o-' + idx);
  if (!inp || !out) return;
  const pick = inp.value;
  if (!pick) { out.innerHTML = ''; return; }
  const today = todayS();
  if (pick < today) { out.innerHTML = '<span class="pw">' + fmtD(pick) + ' is in the past.</span>'; return; }
  const now = calcDue(it, today), then = calcDue(it, pick);
  const diff = Math.round(then.total - now.total);
  out.innerHTML =
    '<div class="pl-tot"><span>' + T('planTot') + ' \u00b7 ' + fmtD(pick) + '</span>' +
    '<b class="num">' + fmtR(Math.round(then.total)) + '</b></div>' +
    '<div class="pl-d">' + (diff > 0
      ? '<span class="up">+' + fmtR(diff) + ' ' + T('planMore') + '</span>'
      : '<span class="ok">' + T('planSame') + '</span>') + '</div>';
};

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
let SECLEN = 4, _pinPrev = 0;   // declared before boot() so buildPinUI() can use them
// v15 · encrypted link: E1.<header>.<salt>.<nonce>.<ciphertext>.<tag>
// key = PBKDF2-SHA256(PIN, salt, 120000); keystream = HMAC-SHA256(Kenc, nonce||counter);
// tag = HMAC-SHA256(Kmac, header||nonce||ciphertext) — a wrong PIN decrypts nothing.
let ENC = null;
function _u8cat() { let n = 0; for (const a of arguments) n += a.length; const o = new Uint8Array(n); let p = 0; for (const a of arguments) { o.set(a, p); p += a.length; } return o; }
async function _hkey(raw) { return crypto.subtle.importKey('raw', raw, { name: 'HMAC', hash: 'SHA-256' }, false, ['sign']); }
async function _hmac(key, msg) { return new Uint8Array(await crypto.subtle.sign('HMAC', key, msg)); }
async function decEnc(pin) {
  try {
    const te = new TextEncoder();
    const base = await crypto.subtle.importKey('raw', te.encode(pin), 'PBKDF2', false, ['deriveBits']);
    const K = new Uint8Array(await crypto.subtle.deriveBits({ name: 'PBKDF2', salt: ENC.salt, iterations: 120000, hash: 'SHA-256' }, base, 256));
    const kK = await _hkey(K);
    const Ke = await _hmac(kK, te.encode('enc')), Km = await _hmac(kK, te.encode('mac'));
    const tag = (await _hmac(await _hkey(Km), _u8cat(ENC.hdrB, ENC.nonce, ENC.ct))).subarray(0, 16);
    let diff = tag.length ^ ENC.tag.length;
    for (let i = 0; i < Math.min(tag.length, ENC.tag.length); i++) diff |= tag[i] ^ ENC.tag[i];
    if (diff) return false;
    const ke = await _hkey(Ke), ct = ENC.ct, pt = new Uint8Array(ct.length), jobs = [];
    for (let off = 0, c = 0; off < ct.length; off += 32, c++) jobs.push(_hmac(ke, _u8cat(ENC.nonce, new Uint8Array([c >>> 24, c >>> 16, c >>> 8, c]))).then(ks => { for (let i = 0; i < 32 && off + i < ct.length; i++) pt[off + i] = ct[off + i] ^ ks[i]; }));
    await Promise.all(jobs);
    const obj = JSON.parse(LZString.decompressFromUint8Array(pt));
    if (!obj || !obj.p || !Array.isArray(obj.p.p)) return false;
    P = obj.p;
    if (obj.lv && obj.lv.u) LIVE = { url: obj.lv.u, id: obj.lv.id, key: obj.lv.k };
    return true;
  } catch (e) { return false; }
}
(function boot(){
  try {
    let frag = location.hash.replace(/^#/, '');
    if (frag.indexOf('E1.') === 0) {
      const parts = frag.split('.');
      if (parts.length !== 6) throw 0;
      const hdrB = b64uDec(parts[1]);
      ENC = { hdr: JSON.parse(new TextDecoder().decode(hdrB)), hdrB, salt: b64uDec(parts[2]), nonce: b64uDec(parts[3]), ct: b64uDec(parts[4]), tag: b64uDec(parts[5]) };
      if (!(window.crypto && crypto.subtle)) throw 0;
      document.getElementById('h-shop').textContent = (ENC.hdr.sn || 'Passbook');
      if (ENC.hdr.st) { const e = document.getElementById('h-shopta'); e.textContent = ENC.hdr.st; e.style.display = 'block'; }
      document.getElementById('g-cn').textContent = '';
      if (document.getElementById('lg-pins')) buildPinUI();
      else document.addEventListener('DOMContentLoaded', buildPinUI);
      setLang(LANG);
      setTimeout(() => document.getElementById('pin').focus(), 300);
      return;
    }
    // A live card looks like  L.<b64u worker url>.<record id>.<key>.<snapshot>
    // The snapshot still rides on the end, so the page opens instantly and
    // works with no signal; the fetch happens after the PIN, never before.
    if (frag.charAt(0) === 'L' && frag.charAt(1) === '.') {
      const parts = frag.split('.');
      if (parts.length >= 5) {
        try {
          LIVE = { url: new TextDecoder().decode(b64uDec(parts[1])), id: parts[2], key: parts[3] };
        } catch(e) { LIVE = null; }
        frag = parts.slice(4).join('.');
      }
    }
    if (!frag) throw 0;
    P = JSON.parse(LZString.decompressFromEncodedURIComponent(frag));
    if (!P || !Array.isArray(P.p)) throw 0;
  } catch(e) {
    document.getElementById('gate').outerHTML = '<div class="badlink" data-i="badlink">'+T('badlink')+'</div>';
    document.querySelector('.langbar').style.display='none';
    return;
  }
  document.getElementById('h-shop').textContent = (P.sn || 'Passbook');
  if (P.st) { const e = document.getElementById('h-shopta'); e.textContent = P.st; e.style.display='block'; }
  document.getElementById('g-cn').textContent = P.cn || '';
  if (document.getElementById('lg-pins')) buildPinUI();
  else document.addEventListener('DOMContentLoaded', buildPinUI);
  setLang(LANG);
  setTimeout(()=>document.getElementById('pin').focus(), 300);
})();

// ── Liquid-glass PIN input driver ────────────────────────────────────────────
// The visible cells are cosmetic; the real value lives in the hidden #pin input,
// so unlock() (which compares #pin to P.sec) is unchanged. Cell count matches the
// actual PIN length (4 by default) so any stored PIN still works.
function revealFallbackInput() {
  const inp = document.getElementById('pin');
  if (inp) inp.style.cssText = 'display:block;width:100%;max-width:220px;margin:2px auto 12px;text-align:center;font-family:monospace;font-size:22px;font-weight:800;letter-spacing:8px;padding:11px;border:2px solid #E4D8B8;border-radius:12px;background:#FFFDF4;color:#2C1F0A;outline:none;';
}
function buildPinUI() {
  try {
    SECLEN = Math.min(8, Math.max(4, (ENC ? +ENC.hdr.pl : String((P && P.sec) || '').length) || 4));
    const pins = document.getElementById('lg-pins');
    if (pins) {
      pins.setAttribute('role', 'group');
      pins.setAttribute('aria-label', 'PIN entry');
      pins.innerHTML = '';
      for (let i = 0; i < SECLEN; i++) {
        const c = document.createElement('div');
        c.className = 'lg-cell';
        c.innerHTML = '<span class="lg-dot"></span><span class="lg-blob"></span><span class="lg-sweep"></span><span class="lg-digit"></span>';
        c.onclick = () => document.getElementById('pin').focus({ preventScroll: true });
        pins.appendChild(c);
      }
    }
    const pad = document.getElementById('lg-pad');
    if (pad) {
      pad.innerHTML = '';
      [['1','1'],['2','2'],['3','3'],['4','4'],['5','5'],['6','6'],['7','7'],['8','8'],['9','9'],['⌫','Delete'],['0','0'],['✓','Unlock']].forEach(([k, label]) => {
        const b = document.createElement('button');
        b.type = 'button';
        b.className = 'lg-key' + (k.length > 1 ? ' wide' : '');
        b.textContent = k;
        b.setAttribute('aria-label', label);
        b.onclick = () => padKey(k);
        pad.appendChild(b);
      });
    }
    _pinPrev = 0;
    pinSync();
    if (!document.querySelector('#lg-pins .lg-cell')) {
      console.warn('[passbook] no PIN cells rendered — showing fallback input');
      revealFallbackInput();
    }
  } catch (e) {
    console.error('[passbook] buildPinUI failed:', e);
    revealFallbackInput();
  }
}
let _maskTimer = null;
function pinSync() {
  const inp = document.getElementById('pin');
  const v = (inp.value || '').replace(/\D/g, '').slice(0, SECLEN);
  inp.value = v;
  const cells = [...document.querySelectorAll('#lg-pins .lg-cell')];
  const grew = v.length > _pinPrev;
  cells.forEach((c, i) => {
    const has = i < v.length;
    c.classList.toggle('filled', has);
    c.classList.toggle('active', i === v.length);
    const dg = c.querySelector('.lg-digit');
    // Privacy: mask all digits as dots, except briefly reveal the one just typed.
    if (!has) dg.textContent = '';
    else if (i === v.length - 1 && grew) dg.textContent = v[i];
    else dg.textContent = '•';
  });
  if (grew && v.length > 0) {
    const c = cells[v.length - 1];
    if (c) { c.classList.remove('pop'); void c.offsetWidth; c.classList.add('pop'); }
    clearTimeout(_maskTimer);
    _maskTimer = setTimeout(() => {
      const last = document.querySelectorAll('#lg-pins .lg-cell')[v.length - 1];
      const dg = last && last.querySelector('.lg-digit');
      if (dg && dg.textContent && dg.textContent !== '•') dg.textContent = '•';
    }, 750);
  }
  _pinPrev = v.length;
  const err = document.getElementById('g-err'); if (err) err.textContent = '';
  if (v.length === SECLEN) setTimeout(unlock, 450);
}
function padKey(k) {
  const inp = document.getElementById('pin');
  if (k === '⌫') inp.value = inp.value.slice(0, -1);
  else if (k === '✓') { unlock(); return; }
  else { if ((inp.value.replace(/\D/g, '')).length >= SECLEN) return; inp.value += k; }
  pinSync();
}
function pinReset() { const inp = document.getElementById('pin'); if (inp) inp.value = ''; _pinPrev = 0; pinSync(); }

let _pinTries = 0, _pinLockUntil = 0;
function unlock() {
  const gate = document.getElementById('gate');
  const val = (document.getElementById('pin').value || '').trim();
  if (!P && !ENC) return;
  if (Date.now() < _pinLockUntil) {
    const secs = Math.ceil((_pinLockUntil - Date.now()) / 1000);
    document.getElementById('g-err').textContent = (LANG === 'ta'
      ? 'அதிக முயற்சிகள் — ' + secs + ' வினாடிகள் காத்திருக்கவும்'
      : 'Too many attempts — wait ' + secs + 's');
    return;
  }
  if (ENC && !P) {
    if (unlock._busy) return;
    unlock._busy = true;
    document.getElementById('g-err').textContent = LANG === 'ta' ? 'சரிபார்க்கிறது…' : 'Checking…';
    decEnc(val).then(ok => {
      unlock._busy = false;
      document.getElementById('g-err').textContent = '';
      if (ok) { unlock(); return; }
      _pinTries++;
      gate.classList.remove('err'); void gate.offsetWidth; gate.classList.add('err');
      document.getElementById('g-err').textContent = T('wrong');
      if (_pinTries >= 5) { _pinLockUntil = Date.now() + 15000; _pinTries = 0; }
      setTimeout(pinReset, 550);
    });
    return;
  }
  if (P && P.ex) {   // v15 · link expiry chosen by the shop
    const d = new Date(), today = d.getFullYear() + '-' + String(d.getMonth() + 1).padStart(2, '0') + '-' + String(d.getDate()).padStart(2, '0');
    if (P.ex < today) {
      document.getElementById('g-err').textContent = LANG === 'ta' ? 'இந்த இணைப்பு காலாவதியானது — கடையிடம் புதிய இணைப்பைக் கேளுங்கள்.' : 'This passbook link has expired — please ask the shop for a new one.';
      return;
    }
  }
  if (!ENC && val !== String(P.sec||'')) {
    _pinTries++;
    gate.classList.remove('err'); void gate.offsetWidth; gate.classList.add('err');
    document.getElementById('g-err').textContent = T('wrong');
    if (_pinTries >= 5) { _pinLockUntil = Date.now() + 15000; _pinTries = 0; }
    setTimeout(pinReset, 550);
    return;
  }
  _pinTries = 0;
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

// ── live refresh ──────────────────────────────────────────────────────────
// Runs only once the PIN is accepted, so an unopened link never touches the
// network. Every failure is silent and leaves the snapshot on screen: a
// customer with no signal is no worse off than before live sync existed.
// Older customers squint at this on a phone. Three steps, remembered, applied
// as a root font-size so every measurement scales with it.
let TSIZE = (function(){ try { return parseInt(localStorage.getItem('pb_tsize')) || 0; } catch(e) { return 0; } })();
function applyTsize(){
  document.documentElement.style.fontSize = [16, 17.6, 19.4][TSIZE] + 'px';
}
applyTsize();   // restore the saved size as soon as it is safe to do so

window._pbTsize = function(n){
  TSIZE = n; try { localStorage.setItem('pb_tsize', String(n)); } catch(e){}
  applyTsize();
  [].slice.call(document.querySelectorAll('.tsz button')).forEach(function(b,i){
    b.classList.toggle('on', i === n);
  });
};

let SORT = (function(){ try { return localStorage.getItem('pb_sort') || 'due'; } catch(e) { return 'due'; } })();
let _pbBannerState = null;
function pbLiveBanner(kind, text) {
  _pbBannerState = { kind, text };
  let el = document.getElementById('pblive');
  if (!el) {
    el = document.createElement('div');
    el.id = 'pblive';
    el.style.cssText = 'margin:0 0 11px;padding:8px 12px;border-radius:10px;font-size:11.5px;font-weight:700;text-align:center;';
    const bk = document.getElementById('book');
    if (!bk) return;
    // v16: the status sits under the customer card, never over the header edge
    const hero = bk.querySelector('.sumhero');
    if (hero && hero.parentNode === bk) bk.insertBefore(el, hero.nextSibling);
    else bk.insertBefore(el, bk.firstChild);
  }
  const c = { live:['#E6F6EC','#1A5C2C'], stale:['#FFF7E6','#8A5A00'], busy:['#EEF3F8','#3A5A7A'] }[kind] || ['#EEF3F8','#3A5A7A'];
  el.style.background = c[0]; el.style.color = c[1]; el.textContent = text;
}

function pbRefreshLive() {
  if (!LIVE || !LIVE.url || !LIVE.id || !LIVE.key) return;
  if (!(window.crypto && crypto.subtle)) return;      // needs https or localhost
  pbLiveBanner('busy', 'Checking for updates…');
  fetch(LIVE.url.replace(/\/+$/, '') + '/p/' + encodeURIComponent(LIVE.id) + '?t=' + Date.now(),
        { cache: 'no-store' })
    .then(r => { if (!r.ok) throw new Error('HTTP ' + r.status); return r.text(); })
    .then(blob => pbDecrypt(LIVE.key, blob.trim()))
    .then(fresh => {
      // The record carries both books; this viewer wants the pledge half.
      const pb = fresh && fresh.pb;
      if (!pb || !Array.isArray(pb.p)) throw new Error('no pledge data');
      const keepSec = P.sec;
      P = pb;
      if (!P.sec) P.sec = keepSec;      // PIN is not re-sent; keep the one that worked
      renderBook();
      const when = fresh.ts ? new Date(fresh.ts) : null;
      pbLiveBanner('live', '\u25CF Live \u00B7 updated ' +
        (when ? String(when.getDate()).padStart(2,'0') + '/' +
                String(when.getMonth()+1).padStart(2,'0') + '/' + when.getFullYear()
              : 'just now') +
        ' \u00B7 ' + P.p.length + ' active pledge' + (P.p.length === 1 ? '' : 's'));
    })
    .catch(() => {
      pbLiveBanner('stale', 'Offline \u2014 showing the details saved on this card' +
        (P.asOf ? ' (' + P.asOf + ')' : ''));
    });
}

// ── Chrome that reacts to scrolling ────────────────────────────────────────
// The hero scrolls away on a long card list, so the name and the total follow
// you down the page; the arrow only appears once there is something to go back
// up to.
function pbScrollUI() {
  const y = window.pageYOffset || document.documentElement.scrollTop || 0;
  const bookOpen = document.getElementById('book') &&
                   document.getElementById('book').style.display === 'block';
  const sb = document.getElementById('stickybar');
  const tt = document.getElementById('totop');
  if (sb) sb.classList.toggle('on', !!bookOpen && y > 240);
  if (tt) tt.classList.toggle('on', !!bookOpen && y > 520);
}
window.addEventListener('scroll', pbScrollUI, { passive: true });
window.addEventListener('resize', pbScrollUI, { passive: true });
window._pbTop = function(){ window.scrollTo({ top: 0, behavior: REDUCED ? 'auto' : 'smooth' }); };

function pbToast(msg) {
  const t = document.getElementById('pbtoast');
  if (!t) return;
  t.textContent = msg;
  t.classList.remove('on'); void t.offsetWidth; t.classList.add('on');
  setTimeout(function(){ t.classList.remove('on'); }, 2600);
}

function renderBook() {
  const asOf = todayS();
  // Silently omit pledges older than 450 days (from pledge date). Recomputed on
  // every open, so a pledge that crosses the limit after the QR was printed
  // disappears automatically. Idempotent — safe on language-toggle re-render.
  P.p = (P.p || []).filter(it => !it.d || daysBetween(it.d, asOf) <= 450);
  // Guard against recursion: renderBook() is what the live fetch calls back into.
  if (LIVE && !window._pbLiveStarted) { window._pbLiveStarted = 1; setTimeout(pbRefreshLive, 350); }
  if (_pbBannerState) setTimeout(() => pbLiveBanner(_pbBannerState.kind, _pbBannerState.text), 0);
  const book = document.getElementById('book');
  const dues = P.p.map(it => calcDue(it, asOf));
  const totPr  = P.p.reduce((s,it) => s + (it.pr||0), 0);
  const totDue = dues.reduce((s,d) => s + d.total, 0);
  const initials = (P.cn||'?').trim().split(/\s+/).slice(0,2).map(w=>w[0]).join('').toUpperCase() || '?';
  const genAge = daysBetween(P.gen || asOf, asOf);
  const overdueCt = P.p.filter(it => it.dd && asOf > it.dd).length;
  const closedCt = (P.cl && P.cl.length) || 0;
  const totInt = Math.max(0, totDue - totPr);
  const nextDd = P.p.map(it => it.dd).filter(x => x && x >= asOf).sort()[0] || '';

  let h = `
    <div class="psheet">
      <div class="ph-band">
        <div>
          <div class="ph-shop">${esc(P.sn || 'Passbook')}</div>
          ${P.ad ? `<div class="ph-addr">${esc(P.ad)}${P.sp ? ' · ' + esc(P.sp) : ''}</div>` : ''}
        </div>
        <div class="ph-tag">${T('stmtT')}<span>${T('stmtS')}</span></div>
      </div>
      <div class="ph-cust">
        <div><b>${T('stmtCust')}:</b> ${esc(P.cn)}</div>
        <div><b>${T('asof')}:</b> ${fmtD(asOf)}</div>
        <div><b>${T('active')}:</b> ${P.p.length}${overdueCt ? ' · ' + overdueCt + ' ' + T('overdueN') : ''}</div>
      </div>
    </div>
    <div class="sumhero">
      <div class="sh-id"><div class="av">${esc(initials)}</div>
        <div><div class="nm">${esc(P.cn)}</div><div class="asof">${T('asof')}: ${fmtD(asOf)}${P.gen && P.gen !== asOf ? ' · ' + T('snap') + ' ' + fmtD(P.gen) : ''}</div></div></div>
      <div class="sh-lab">${T('totnow')}</div>
      <div class="sh-big num" id="kpi-due">₹0</div>
      <div class="split" aria-hidden="true"><i class="sp-p" id="sp-p" style="width:0"></i><i class="sp-i" id="sp-i" style="width:0"></i></div>
      <div class="sh-leg"><span><b class="dp"></b>${T('principal')} <strong class="num">${fmtR(totPr)}</strong></span><span><b class="di"></b>${T('intK')} <strong class="num">${fmtR(totInt)}</strong></span></div>
    </div>
    <div class="kpigrid">
      <div class="kpi c-due"><div class="khead"><div class="klab">${T('totnow')}</div><div class="kico">${PBI.cash}</div></div>
        <div class="kval">${fmtR(totDue)}</div></div>
      <div class="kpi c-tur"><div class="shimmer"></div><div class="khead"><div class="klab">${T('activeK')}</div><div class="kico">${PBI.ring}</div></div>
        <div class="kval" id="kpi-active">0</div><div class="ksub">${closedCt ? T('closedK').replace('#N', closedCt) : T('openK')}</div>
        <div class="kbar"><i id="kbar-active"></i></div></div>
      <div class="kpi c-ind"><div class="shimmer"></div><div class="khead"><div class="klab">${T('principal')}</div><div class="kico">${PBI.bank}</div></div>
        <div class="kval" id="kpi-pr">₹0</div><div class="ksub">${T('prSub')}</div>
        <div class="kbar"><i id="kbar-pr"></i></div></div>
      <div class="kpi c-lot"><div class="shimmer"></div><div class="khead"><div class="klab">${T('intK')}</div><div class="kico">${PBI.clock}</div></div>
        <div class="kval" id="kpi-int">₹0</div><div class="ksub">${T('intSub')}</div>
        <div class="kbar"><i id="kbar-due"></i></div></div>
      ${overdueCt ? `<div class="kpi c-kum kpi-over" role="button" tabindex="0" onclick="_pbJumpOverdue()"><div class="shimmer"></div><div class="khead"><div class="klab">${T('overdueK')}</div><div class="kico">${PBI.alert}</div></div>
        <div class="kval" id="kpi-over">0</div>
        <div class="ktap">${T('tapOver')} ↓</div>
        <div class="kbar"><i id="kbar-over"></i></div></div>`
      : `<div class="kpi c-leaf"><div class="shimmer"></div><div class="khead"><div class="klab">${T('nextDue')}</div><div class="kico">${PBI.cal}</div></div>
        <div class="kval">${nextDd ? fmtD(nextDd).slice(0,5) : '—'}</div><div class="ksub">${nextDd ? T('inDays').replace('#D', daysBetween(asOf, nextDd)) : T('noneDue')}</div></div>`}
    </div>`;

  if (genAge > 7) h += `<div class="stale">${T('stale').replace('#D', genAge)}</div>`;

  // "Settle everything" only makes sense with more than one open pledge —
  // with a single pledge its own card already shows the same number.
  if (P.p.length > 1) {
    const st = _pbSettleAll();
    h += `<div class="settle no-print">
      <div class="st-l">
        <div class="st-t">${T('settleT')}</div>
        <div class="st-s">${T('settleS').replace('#N', P.p.length)}</div>
        ${P.om ? `<div class="st-om">${T('omitN').replace('#N', P.om)}</div>` : ''}
      </div>
      <div class="st-r">
        <div class="st-v num">${fmtR(st)}</div>
        ${P.upi && P.upi.pa ? `<a class="st-b" href="${upiLink('upi', st, 'ALL')}">${T('settlePay')}</a>` : ''}
      </div>
    </div>`;
  }

  // Utility row — reminders, directions, print, text size.
  h += `<div class="tools no-print">
    <button class="tl" onclick="_pbRemindAll()">🔔 ${T('remindAll')}</button>
    ${P.ad ? `<button class="tl" onclick="_pbDirections()">📍 ${T('directions')}</button>` : ''}
    <button class="tl" onclick="_pbPrint()">🖨 ${T('printBtn')}</button>
    <div class="tsz" title="${T('txtSize')}">
      <button class="${TSIZE===0?'on':''}" onclick="_pbTsize(0)" style="font-size:11px;">A</button>
      <button class="${TSIZE===1?'on':''}" onclick="_pbTsize(1)" style="font-size:13px;">A</button>
      <button class="${TSIZE===2?'on':''}" onclick="_pbTsize(2)" style="font-size:15px;">A</button>
    </div>
  </div>`;

  // With one or two pledges the chips are noise; past that, finding the one
  // the customer is asking about matters more than the original order.
  if (P.p.length > 2) {
    const chips = [['due', T('srtDue')], ['over', T('srtOver')], ['amt', T('srtAmt')], ['new', T('srtNew')]];
    h += `<div class="sortbar"><span class="sl">${T('sortBy')}</span>` +
      chips.map(([k, lbl]) =>
        `<button class="chip${SORT === k ? ' on' : ''}" data-sort="${k}">${esc(lbl)}</button>`
      ).join('') + `</div>`;
  }

  // Sort a view of the list, carrying each pledge's computed dues with it, so
  // the underlying payload order (and the live-sync snapshot) stays untouched.
  const view = P.p.map((it, i) => ({ it, d: dues[i], i }));
  const ovDays = x => (x.it.dd && asOf > x.it.dd) ? daysBetween(x.it.dd, asOf) : -1;
  if (SORT === 'due')  view.sort((a, b) => String(a.it.dd || '9999').localeCompare(String(b.it.dd || '9999')));
  if (SORT === 'over') view.sort((a, b) => ovDays(b) - ovDays(a));
  if (SORT === 'amt')  view.sort((a, b) => (b.d.total || 0) - (a.d.total || 0));
  if (SORT === 'new')  view.sort((a, b) => String(b.it.d || '').localeCompare(String(a.it.d || '')));

  view.forEach(({ it, d, i }) => {
    const overdueDays = it.dd ? daysBetween(it.dd, asOf) : 0;
    const isOver = it.dd && asOf > it.dd;
    // Elapsed progress ring: pledge date → due date (capped at 100%).
    const totalSpan = (it.d && it.dd) ? Math.max(1, daysBetween(it.d, it.dd)) : 0;
    const spent = it.d ? daysBetween(it.d, asOf) : 0;
    const pct = totalSpan ? Math.min(1, spent / totalSpan) : 0;
    const C = 2 * Math.PI * 14;   // r=14
    const off = C * (1 - pct);
    h += `
    <div class="pcard${isOver ? ' is-over' : ''}" data-rd="${(i*0.07).toFixed(2)}">
      <div class="top">
        <div><div class="bill">${T('billK')} ${esc(it.b)}</div><div class="item">${esc(it.it)||'—'}</div></div>
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
      ${it.ph ? `<img class="jph" src="${it.ph}" alt="${T('photoAlt')}" loading="lazy">` : ''}
      ${it.dp ? `<div class="dup-tag">${T('dupNote').replace('#N', esc(it.dp))}</div>` : ''}
      ${it.rn ? `<div class="rnw-tag">🔁 ${T('renewedN').replace('#N', it.rn)}${
        it.rd ? ' · ' + T('renewedOn').replace('#D', fmtD(it.rd)) : ''}</div>` : ''}
      ${(function(){
        // Renewing pays only the interest and pushes the clock forward. Shops
        // know this; customers often do not, and it is frequently the cheaper
        // option when they cannot clear the principal yet.
        const dd = calcDue(it, asOf);
        if (!dd.interest || dd.interest < 1) return '';
        // calcDue() charges nothing for the first 35 days after a payment, so
        // clearing the interest today buys exactly that much breathing room.
        const nd = addDaysISO(asOf, 35);
        return `<div class="renew">
          <div class="rn-t">🔁 ${T('renewT')}</div>
          <div class="rn-s">${T('renewS').replace('#A', fmtR(Math.round(dd.interest))).replace('#D', fmtD(nd))}</div>
        </div>`;
      })()}
      <div class="planner">
        <div class="pl-h">📅 ${T('planTitle')}</div>
        <div class="pl-r">
          <input type="date" id="plan-d-${i}" min="${asOf}" onchange="_pbPlanDate(${i})" aria-label="${T('planPick')}">
          <button class="pl-rem" onclick="_pbRemind(${i})">🔔 ${T('remind')}</button>
        </div>
        <div class="pl-o" id="plan-o-${i}"></div>
      </div>
      ${P.upi && P.upi.pa ? payBlock(i, it, d) : ''}
      ${it.pm && it.pm.length ? histBlock(it) : ''}
    </div>`;
  });

  if (P.cl && P.cl.length) {
    h += `<div class="sect-title">${T('closed')}</div>`;
    P.cl.forEach((c, i) => {
      h += `<div class="ccard" data-rd="${(i*0.06).toFixed(2)}">
        <div class="ci"><div class="cb">${T('billK')} ${esc(c.b)} · ${fmtR(c.a)}</div>
        <div class="cn2">${esc(c.it)||'—'}</div>
        <div class="cd">${fmtD(c.d)} → ${fmtD(c.cd)}</div></div>
        <span class="cst${c.fc?' fc':''}">${c.fc ? T('foreclosed') : T('redeemed')}</span>
      </div>`;
    });
  }
  h += `<div class="psheet"><div class="ph-foot">${T('stmtFoot')}</div></div>`;
  book.innerHTML = h;

  // Animated KPI count-up (first unlock only; language toggle re-renders static)
  countUp(document.getElementById('kpi-active'), P.p.length, v => String(Math.round(v)), 650);
  countUp(document.getElementById('kpi-due'), totDue, fmtR, 950);
  countUp(document.getElementById('kpi-pr'), totPr, fmtR, 950);
  countUp(document.getElementById('kpi-int'), totInt, fmtR, 950);
  if (overdueCt) countUp(document.getElementById('kpi-over'), overdueCt, v => String(Math.round(v)), 650);
  // Each bar shows that figure's share of the whole, so the numbers carry
  // proportion as well as magnitude. Widths are set a tick later so the CSS
  // transition has a zero-width frame to animate away from.
  setTimeout(() => {
    const setBar = (id, pct) => {
      const el = document.getElementById(id);
      if (el) el.style.width = Math.max(0, Math.min(100, pct)) + '%';
    };
    const interest = totInt;
    setBar('sp-p', totDue > 0 ? (totPr / totDue) * 100 : 100);
    setBar('sp-i', totDue > 0 ? (interest / totDue) * 100 : 0);
    // Each bar answers a different question, so none of them sits pinned at
    // full: how many of this customer's pledges are still open, how much of
    // what they owe is interest rather than principal, and how many pledges
    // have slipped past their due date.
    setBar('kbar-active', (P.p.length + closedCt) > 0 ? (P.p.length / (P.p.length + closedCt)) * 100 : 100);
    setBar('kbar-due',    totDue > 0 ? (interest / totDue) * 100 : 0);
    setBar('kbar-pr',     totDue > 0 ? (totPr    / totDue) * 100 : 100);
    if (overdueCt) setBar('kbar-over', P.p.length ? (overdueCt / P.p.length) * 100 : 0);
  }, 120);
  [].slice.call(book.querySelectorAll('.chip[data-sort]')).forEach(btn => {
    btn.addEventListener('click', () => {
      SORT = btn.getAttribute('data-sort');
      try { localStorage.setItem('pb_sort', SORT); } catch(e){}
      renderBook();
    });
  });
  reveal();
  FIRST_RENDER = false;

  // the sticky bar carries the one number a customer scrolls looking for
  const sbn = document.getElementById('sb-nm');
  const sbl = document.getElementById('sb-l');
  const sbv = document.getElementById('sb-v');
  if (sbn) sbn.textContent = P.cn || '';
  if (sbl) sbl.textContent = T('duetoday');
  if (sbv) sbv.textContent = fmtR(totDue);
  pbScrollUI();

  // footer
  let f = '';
  // Contact strip: the three things a customer reaches for, one row, equal size.
  const telNo = String(P.sp || '').replace(/[^\d+]/g, '');
  const waNo  = String(P.sp || '').replace(/\D/g, '').replace(/^(?!91)/, '91');
  if (P.sp || P.ad) {
    f += '<div class="contact no-print">' +
      (P.sp ? `<a href="tel:${esc(telNo)}"><span class="ci2">📞</span>${T('callShort')}<span class="cph">${esc(P.sp)}</span></a>` : '') +
      (P.sp ? `<a class="wa2" target="_blank" rel="noopener" href="https://wa.me/${waNo}?text=${
        encodeURIComponent((P.cn || '') + ' · ' + (P.sn || ''))
      }"><span class="ci2">💬</span>WhatsApp</a>` : '') +
      (P.ad ? `<a href="#" onclick="_pbDirections();return false;"><span class="ci2">📍</span>${T('dirShort')}</a>` : '') +
      '</div>';
  }
  if (P.ad) f += `<div class="addr">📍 ${esc(P.ad)}</div>`;
  f += `<div class="note">🔒 ${T('privacy')}<br><span style="opacity:.55;">viewer v16</span></div>`;
  document.getElementById('foot').innerHTML = f;
}

function payBlock(i, it, d) {
  // Default = Total to close today (principal + interest). Field stays editable.
  const def = d.interest > 0 ? Math.round(d.total) : '';
  return `
  <div class="payrow">
    <div class="pl">📲 ${T('paynow')}</div>
    <div class="payamt"><span>${T('payamt')}</span><input id="pay-amt-${i}" type="number" inputmode="numeric" min="1" value="${def}" oninput="payAmtChanged(${i})" placeholder="0" aria-label="${T('payamt')}"></div>
    ${def !== '' ? `<div class="mnote" style="margin:0 0 7px;">💡 ${T('payhint')}</div>` : ''}
    <div class="paybtns">
      <a id="pay-gpay-${i}"    class="gp" href="${upiLink('gpay',    def||0, it.b)}">GPay</a>
      <a id="pay-phonepe-${i}" class="pp" href="${upiLink('phonepe', def||0, it.b)}">PhonePe</a>
      <a id="pay-paytm-${i}"   class="pt" href="${upiLink('paytm',   def||0, it.b)}">Paytm</a>
      <a id="pay-upi-${i}"     class="up" href="${upiLink('upi',     def||0, it.b)}">UPI</a>
      ${P.sp ? `<a id="pay-wa-${i}" class="wa" target="_blank" rel="noopener"
        href="https://wa.me/${String(P.sp).replace(/\D/g,'').replace(/^(?!91)/, '91')}?text=${
          encodeURIComponent((P.cn || '') + ' \u00B7 Pledge ' + (it.b || '') + ' \u00B7 ' + T('paynow'))
        }">WhatsApp</a>` : ''}
    </div>
    <div class="mnote" style="margin:7px 0 0;">${T('paynote')}</div>
    ${P.sp ? `
    <div class="cfm">
      <div class="pl">${T('cfT')}</div>
      <input id="utr-${i}" type="text" autocomplete="off" maxlength="40" placeholder="${T('cfU')}">
      <a class="cfb" href="#" onclick="sendPayConfirm(${i});return false;">${T('cfB')}</a>
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
  pbToast(T('sentOk'));
}

function histBlock(it) {
  const rows = it.pm.map(p => `<tr><td>${fmtD(p[0])}</td><td><span class="hk">${(I18N.histk[p[2]]&&(I18N.histk[p[2]][LANG]||I18N.histk[p[2]].en))||''}</span></td><td>${fmtR(p[1])}</td></tr>`).join('');
  return `<details class="hist"><summary>🧾 ${T('hist')} (${it.pm.length})</summary><table>${rows}</table></details>`;
}

function esc(s){ return String(s==null?'':s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;'); }
</script>
</body>
</html>
