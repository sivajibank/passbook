<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
<title>Customer Passbook</title>
<style>
  :root{
    --gold:#C9A84C; --gold-dk:#9A7A30; --ink:#2C1F0A; --ink2:#1A1209;
    --cream:#FFFEFA; --paper:#FAF5EC; --line:#EDE3C5; --muted:#8A7350;
    --ok:#1A7A3C; --warn:#B36B00; --bad:#C0392B;
  }
  *{box-sizing:border-box;margin:0;padding:0;}
  body{
    font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Arial,sans-serif;
    background:linear-gradient(135deg,#0F1A10 0%,#16331F 45%,#2C1F0A 100%);
    min-height:100vh; display:flex; align-items:center; justify-content:center;
    padding:18px; color:var(--ink2);
  }
  .card{
    background:var(--cream); border-radius:18px; max-width:430px; width:100%;
    box-shadow:0 20px 60px rgba(0,0,0,.5); overflow:hidden;
  }
  .hdr{
    background:linear-gradient(135deg,#0F1A10 0%,#16331F 45%,#2C1F0A 100%);
    padding:18px 52px 18px 20px; color:#E8C97A; position:relative;
  }
  .hdr .brand{font-size:15px;font-weight:800;letter-spacing:.2px;}
  .hdr .sub{font-size:11px;color:rgba(232,201,122,.75);margin-top:2px;}
  .hdr .lang-toggle{
    position:absolute; top:14px; right:14px; background:rgba(255,255,255,.12);
    border:1px solid rgba(232,201,122,.35); color:#E8C97A; border-radius:8px;
    font-size:11px; font-weight:700; padding:6px 9px; cursor:pointer;
  }
  .body{padding:20px;}
  .gate{text-align:center;}
  .gate .icon{font-size:38px;margin-bottom:6px;}
  .gate h2{font-size:15px;font-weight:800;color:var(--ink);margin-bottom:6px;}
  .gate p{font-size:12.5px;color:var(--muted);line-height:1.5;margin-bottom:18px;}
  .pin-input{
    width:100%; max-width:220px; text-align:center; letter-spacing:6px;
    font-size:22px; font-weight:800; padding:12px 10px; border:2px solid var(--line);
    border-radius:10px; outline:none; font-family:monospace; color:var(--ink);
  }
  .pin-input:focus{border-color:var(--gold);}
  .unlock-btn{
    margin-top:16px; width:100%; max-width:220px; padding:12px; border:none;
    border-radius:10px; background:linear-gradient(135deg,var(--gold),var(--gold-dk));
    color:#fff; font-size:14px; font-weight:800; cursor:pointer;
  }
  .unlock-btn:disabled{opacity:.5;cursor:not-allowed;}
  .err-msg{color:var(--bad); font-size:12px; font-weight:700; margin-top:12px; min-height:16px;}
  .footer-note{font-size:10.5px;color:#aaa;text-align:center;margin-top:18px;line-height:1.5;}

  .pb-header-row{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:14px;}
  .pb-cust{font-size:16px;font-weight:800;color:var(--ink);}
  .pb-asof{font-size:10.5px;color:var(--muted);margin-top:2px;}
  .summary{
    background:var(--ink2); color:#E8C97A; border-radius:12px; padding:14px 16px;
    margin-bottom:16px; display:flex; justify-content:space-between; align-items:center;
  }
  .summary .lbl{font-size:10px;text-transform:uppercase;letter-spacing:.5px;color:rgba(232,201,122,.7);}
  .summary .val{font-size:20px;font-weight:800;margin-top:2px;}
  .pledge-card{
    border:1.5px solid var(--line); border-radius:12px; padding:13px 14px; margin-bottom:12px;
    background:var(--paper);
  }
  .pledge-top{display:flex;justify-content:space-between;align-items:flex-start;gap:8px;margin-bottom:8px;}
  .pledge-no{font-size:13px;font-weight:800;color:var(--ink);}
  .pledge-item{font-size:11px;color:var(--muted);margin-top:1px;}
  .badge{font-size:9.5px;font-weight:800;padding:3px 8px;border-radius:20px;white-space:nowrap;}
  .badge.ok{background:#E3F5E8;color:var(--ok);}
  .badge.due{background:#FFF3DC;color:var(--warn);}
  .badge.overdue{background:#FDE6E4;color:var(--bad);}
  .row{display:flex;justify-content:space-between;font-size:12px;padding:3px 0;color:#5A4A2E;}
  .row b{color:var(--ink);font-weight:700;}
  .row.total{border-top:1px dashed var(--line);margin-top:6px;padding-top:7px;font-size:13px;}
  .row.total b{color:var(--gold-dk);font-size:15px;}
  .shop-foot{
    text-align:center; padding:14px 20px 20px; font-size:11px; color:var(--muted);
    border-top:1px solid var(--line); margin-top:6px;
  }
  .shop-foot b{color:var(--ink);}
  .lockout{background:#FDE6E4;color:var(--bad);border-radius:10px;padding:10px;font-size:12px;font-weight:700;margin-top:14px;}
  .empty-state{text-align:center;padding:30px 10px;color:var(--muted);font-size:13px;}
  .no-data{padding:34px 20px;text-align:center;color:#888;}
  .warn-strip{background:#FFF8E1;border:1px solid #FCE38A;border-radius:8px;padding:9px 11px;font-size:10.5px;color:#8A6D00;margin-bottom:14px;line-height:1.5;}
</style>
</head>
<body>
<div class="card" id="app">
  <div class="no-data">
    <div style="font-size:38px;margin-bottom:10px;">🔗</div>
    <div>Loading…</div>
  </div>
</div>

<script>
// ── LZString (same library used by the main app — needed to decompress the fragment) ──
var LZString=function(){var r=String.fromCharCode,o="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=",n="ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+-$",e={};function t(r,o){if(!e[r]){e[r]={};for(var n=0;n<r.length;n++)e[r][r.charAt(n)]=n}return e[r][o]}var i={compressToBase64:function(r){if(null==r)return"";var n=i._compress(r,6,function(r){return o.charAt(r)});switch(n.length%4){default:case 0:return n;case 1:return n+"===";case 2:return n+"==";case 3:return n+"="}},decompressFromBase64:function(r){return null==r?"":""==r?null:i._decompress(r.length,32,function(n){return t(o,r.charAt(n))})},compressToUTF16:function(o){return null==o?"":i._compress(o,15,function(o){return r(o+32)})+" "},decompressFromUTF16:function(r){return null==r?"":""==r?null:i._decompress(r.length,16384,function(o){return r.charCodeAt(o)-32})},compressToUint8Array:function(r){for(var o=i.compress(r),n=new Uint8Array(2*o.length),e=0,t=o.length;e<t;e++){var s=o.charCodeAt(e);n[2*e]=s>>>8,n[2*e+1]=s%256}return n},decompressFromUint8Array:function(o){if(null==o)return i.decompress(o);for(var n=new Array(o.length/2),e=0,t=n.length;e<t;e++)n[e]=256*o[2*e]+o[2*e+1];var s=[];return n.forEach(function(o){s.push(r(o))}),i.decompress(s.join(""))},compressToEncodedURIComponent:function(r){return null==r?"":i._compress(r,6,function(r){return n.charAt(r)})},decompressFromEncodedURIComponent:function(r){return null==r?"":""==r?null:(r=r.replace(/ /g,"+"),i._decompress(r.length,32,function(o){return t(n,r.charAt(o))}))},compress:function(o){return i._compress(o,16,function(o){return r(o)})},_compress:function(r,o,n){if(null==r)return"";var e,t,i,s={},u={},a="",p="",c="",l=2,f=3,h=2,d=[],m=0,v=0;for(i=0;i<r.length;i+=1)if(a=r.charAt(i),Object.prototype.hasOwnProperty.call(s,a)||(s[a]=f++,u[a]=!0),p=c+a,Object.prototype.hasOwnProperty.call(s,p))c=p;else{if(Object.prototype.hasOwnProperty.call(u,c)){if(c.charCodeAt(0)<256){for(e=0;e<h;e++)m<<=1,v==o-1?(v=0,d.push(n(m)),m=0):v++;for(t=c.charCodeAt(0),e=0;e<8;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1}else{for(t=1,e=0;e<h;e++)m=m<<1|t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t=0;for(t=c.charCodeAt(0),e=0;e<16;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1}0==--l&&(l=Math.pow(2,h),h++),delete u[c]}else for(t=s[c],e=0;e<h;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1;0==--l&&(l=Math.pow(2,h),h++),s[p]=f++,c=String(a)}if(""!==c){if(Object.prototype.hasOwnProperty.call(u,c)){if(c.charCodeAt(0)<256){for(e=0;e<h;e++)m<<=1,v==o-1?(v=0,d.push(n(m)),m=0):v++;for(t=c.charCodeAt(0),e=0;e<8;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1}else{for(t=1,e=0;e<h;e++)m=m<<1|t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t=0;for(t=c.charCodeAt(0),e=0;e<16;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1}0==--l&&(l=Math.pow(2,h),h++),delete u[c]}else for(t=s[c],e=0;e<h;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1;0==--l&&(l=Math.pow(2,h),h++)}for(t=2,e=0;e<h;e++)m=m<<1|1&t,v==o-1?(v=0,d.push(n(m)),m=0):v++,t>>=1;for(;;){if(m<<=1,v==o-1){d.push(n(m));break}v++}return d.join("")},decompress:function(r){return null==r?"":""==r?null:i._decompress(r.length,32768,function(o){return r.charCodeAt(o)})},_decompress:function(o,n,e){var t,i,s,u,a,p,c,l=[],f=4,h=4,d=3,m="",v=[],g={val:e(0),position:n,index:1};for(t=0;t<3;t+=1)l[t]=t;for(s=0,a=Math.pow(2,2),p=1;p!=a;)u=g.val&g.position,g.position>>=1,0==g.position&&(g.position=n,g.val=e(g.index++)),s|=(u>0?1:0)*p,p<<=1;switch(s){case 0:for(s=0,a=Math.pow(2,8),p=1;p!=a;)u=g.val&g.position,g.position>>=1,0==g.position&&(g.position=n,g.val=e(g.index++)),s|=(u>0?1:0)*p,p<<=1;c=r(s);break;case 1:for(s=0,a=Math.pow(2,16),p=1;p!=a;)u=g.val&g.position,g.position>>=1,0==g.position&&(g.position=n,g.val=e(g.index++)),s|=(u>0?1:0)*p,p<<=1;c=r(s);break;case 2:return""}for(l[3]=c,i=c,v.push(c);;){if(g.index>o)return"";for(s=0,a=Math.pow(2,d),p=1;p!=a;)u=g.val&g.position,g.position>>=1,0==g.position&&(g.position=n,g.val=e(g.index++)),s|=(u>0?1:0)*p,p<<=1;switch(c=s){case 0:for(s=0,a=Math.pow(2,8),p=1;p!=a;)u=g.val&g.position,g.position>>=1,0==g.position&&(g.position=n,g.val=e(g.index++)),s|=(u>0?1:0)*p,p<<=1;l[h++]=r(s),c=h-1,f--;break;case 1:for(s=0,a=Math.pow(2,16),p=1;p!=a;)u=g.val&g.position,g.position>>=1,0==g.position&&(g.position=n,g.val=e(g.index++)),s|=(u>0?1:0)*p,p<<=1;l[h++]=r(s),c=h-1,f--;break;case 2:return v.join("")}if(0==f&&(f=Math.pow(2,d),d++),l[c])m=l[c];else{if(c!==h)return null;m=i+i.charAt(0)}v.push(m),l[h++]=i+m.charAt(0),i=m,0==--f&&(f=Math.pow(2,d),d++)}}};return i}();"function"==typeof define&&define.amd?define(function(){return LZString}):"undefined"!=typeof module&&null!=module?module.exports=LZString:"undefined"!=typeof angular&&null!=angular&&angular.module("LZString",[]).factory("LZString",function(){return LZString});

// ── State ──────────────────────────────────────────────────────────────────
var PAYLOAD = null;
var IS_TAMIL = false;
var ATTEMPTS = 0;
var LOCKED_UNTIL = 0;
var MAX_ATTEMPTS = 5;
var LOCK_SECONDS = 30;

function ut(en, ta) { return IS_TAMIL ? (ta || en) : en; }

function fmtRs(v) {
  v = Math.round(parseFloat(v||0));
  return '₹' + v.toLocaleString('en-IN');
}
function fmtD(d) {
  if (!d) return '—';
  var q = d.split('-');
  if (q.length !== 3) return d;
  return q[2] + '/' + q[1] + '/' + q[0];
}

// ── Interest math — mirrors calcInterest()/calcPledgeDue() in the main app ──
// Month 1 interest is collected upfront at pledge time. Renewal interest is
// charged only beyond the first 35 days; any partial extra month counts as a
// full month (ceiling rule). e.g. days 1-35 = 0 due, 36-65 = 1 month, etc.
function daysBetween(d1, d2) {
  var a = new Date(d1 + 'T00:00:00'), b = new Date(d2 + 'T00:00:00');
  return Math.floor((b - a) / 86400000);
}
function calcInterest(principal, ratePerMonth, days, type, r2, tier1Months) {
  type = type || 'simple';
  if (days <= 35) return 0;
  var extraDays = days - 35;
  var extraMonths = Math.ceil(extraDays / 30);
  var monthly = principal * (ratePerMonth / 100);
  if (type === 'compound') return principal * (Math.pow(1 + ratePerMonth/100, extraMonths) - 1);
  if (type === 'tiered') {
    var rate1 = ratePerMonth, rate2 = r2 || rate1, t1 = tier1Months || 6;
    var m1 = Math.min(extraMonths, t1), m2 = Math.max(0, extraMonths - t1);
    return principal*(rate1/100)*m1 + principal*(rate2/100)*m2;
  }
  return monthly * extraMonths;
}
function today() {
  var d = new Date();
  return d.getFullYear()+'-'+String(d.getMonth()+1).padStart(2,'0')+'-'+String(d.getDate()).padStart(2,'0');
}
function pledgeDue(pl) {
  var asOf = today();
  var days = daysBetween(pl.lp || pl.d, asOf);
  var interest = calcInterest(pl.pr, pl.r, days, pl.ty, pl.r2, pl.tr);
  return { days: days, interest: interest, total: pl.pr + interest };
}

// ── Boot ───────────────────────────────────────────────────────────────────
function boot() {
  var frag = location.hash.replace(/^#/, '');
  if (!frag) { renderNoData(); return; }
  try {
    var json = LZString.decompressFromEncodedURIComponent(frag);
    PAYLOAD = JSON.parse(json);
    if (!PAYLOAD || !PAYLOAD.v) throw new Error('bad payload');
  } catch (e) {
    renderNoData();
    return;
  }
  renderGate();
}

function renderNoData() {
  document.getElementById('app').innerHTML =
    '<div class="no-data">' +
      '<div style="font-size:38px;margin-bottom:10px;">⚠️</div>' +
      '<div style="font-weight:700;color:#444;margin-bottom:4px;">Link not recognised</div>' +
      '<div style="font-size:12px;">This link looks incomplete or damaged. Please ask the shop to resend your passbook QR.</div>' +
    '</div>';
}

function langToggleHtml() {
  return '<button class="lang-toggle" onclick="toggleLang()">' + (IS_TAMIL ? 'EN' : 'தமிழ்') + '</button>';
}
function toggleLang() {
  IS_TAMIL = !IS_TAMIL;
  if (document.getElementById('pin-gate-box')) renderGate();
  else renderPassbook();
}

function renderGate() {
  var locked = Date.now() < LOCKED_UNTIL;
  var secsLeft = Math.ceil((LOCKED_UNTIL - Date.now())/1000);
  document.getElementById('app').innerHTML =
    '<div class="hdr">' + langToggleHtml() +
      '<div class="brand">' + esc(IS_TAMIL && PAYLOAD.st ? PAYLOAD.st : (PAYLOAD.sn || 'Pawnshop')) + '</div>' +
      '<div class="sub">' + ut('Customer Passbook', 'வாடிக்கையாளர் பாஸ்புக்') + '</div>' +
    '</div>' +
    '<div class="body">' +
      '<div class="gate" id="pin-gate-box">' +
        '<div class="icon">🔒</div>' +
        '<h2>' + ut('Enter your PIN to view your passbook', 'உங்கள் பாஸ்புக்கைப் பார்க்க PIN உள்ளிடவும்') + '</h2>' +
        '<p>' + ut('This is the PIN or last 4 digits of your ID proof given to you by the shop.', 'இது கடை வழங்கிய PIN அல்லது உங்கள் அடையாள எண்ணின் கடைசி 4 இலக்கங்கள்.') + '</p>' +
        '<input type="text" inputmode="numeric" maxlength="6" class="pin-input" id="pin-field" placeholder="••••" ' + (locked?'disabled':'') + '>' +
        '<br>' +
        '<button class="unlock-btn" id="unlock-btn" onclick="tryUnlock()" ' + (locked?'disabled':'') + '>' + ut('Unlock', 'திற') + '</button>' +
        '<div class="err-msg" id="err-msg"></div>' +
      '</div>' +
      (locked ? '<div class="lockout" id="lock-msg">' + ut('Too many attempts. Try again in ', 'பல முயற்சிகள். மீண்டும் முயற்சிக்கவும்: ') + secsLeft + 's</div>' : '') +
      '<div class="footer-note">' + ut('Your details stay on this page only — nothing is sent anywhere.', 'உங்கள் தகவல்கள் இந்த பக்கத்தில் மட்டுமே உள்ளன — எங்கும் அனுப்பப்படாது.') + '</div>' +
    '</div>';
  var f = document.getElementById('pin-field');
  if (f) { f.focus(); f.onkeydown = function(e){ if (e.key === 'Enter') tryUnlock(); }; }
  if (locked) tickLockout();
}

function tickLockout() {
  var msEl = document.getElementById('lock-msg');
  if (!msEl) return;
  var iv = setInterval(function() {
    var left = Math.ceil((LOCKED_UNTIL - Date.now())/1000);
    if (left <= 0) { clearInterval(iv); renderGate(); return; }
    var el = document.getElementById('lock-msg');
    if (!el) { clearInterval(iv); return; }
    el.textContent = ut('Too many attempts. Try again in ', 'பல முயற்சிகள். மீண்டும் முயற்சிக்கவும்: ') + left + 's';
  }, 1000);
}

function tryUnlock() {
  if (Date.now() < LOCKED_UNTIL) return;
  var val = (document.getElementById('pin-field').value || '').trim();
  var expected = String(PAYLOAD.sec || '').trim();
  if (!val) return;
  if (expected && val === expected) {
    ATTEMPTS = 0;
    renderPassbook();
    return;
  }
  ATTEMPTS++;
  var errEl = document.getElementById('err-msg');
  if (ATTEMPTS >= MAX_ATTEMPTS) {
    LOCKED_UNTIL = Date.now() + LOCK_SECONDS*1000;
    renderGate();
    return;
  }
  if (errEl) errEl.textContent = ut('Incorrect PIN. ', 'தவறான PIN. ') + (MAX_ATTEMPTS-ATTEMPTS) + ' ' + ut('attempts left.', 'முயற்சிகள் மீதம்.');
  document.getElementById('pin-field').value = '';
  document.getElementById('pin-field').focus();
}

function esc(s) { return String(s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

function renderPassbook() {
  var pledges = PAYLOAD.p || [];
  var totalOutstanding = 0;
  var cardsHtml = pledges.map(function(pl) {
    var due = pledgeDue(pl);
    totalOutstanding += due.total;
    var overdueDays = daysBetween(pl.dd, today()); // positive once due date is in the past
    var badge, badgeClass;
    if (overdueDays > 0) { badgeClass='overdue'; badge = ut('Overdue '+overdueDays+'d','தாமதம் '+overdueDays+'நா'); }
    else if (overdueDays === 0) { badgeClass='due'; badge = ut('Due today','இன்று செலுத்த வேண்டும்'); }
    else { badgeClass='ok'; badge = ut('Active','செயலில்'); }
    return '<div class="pledge-card">' +
      '<div class="pledge-top">' +
        '<div><div class="pledge-no">' + esc(pl.b) + '</div>' +
        '<div class="pledge-item">' + esc(pl.it || '—') + '</div></div>' +
        '<span class="badge ' + badgeClass + '">' + badge + '</span>' +
      '</div>' +
      '<div class="row"><span>' + ut('Pledged on','அடகு வைத்த தேதி') + '</span><b>' + fmtD(pl.d) + '</b></div>' +
      '<div class="row"><span>' + ut('Due date','செலுத்த வேண்டிய தேதி') + '</span><b>' + fmtD(pl.dd) + '</b></div>' +
      '<div class="row"><span>' + ut('Outstanding principal','நிலுவையில் உள்ள அசல்') + '</span><b>' + fmtRs(pl.pr) + '</b></div>' +
      '<div class="row"><span>' + ut('Accrued interest (today)','இன்று வரை வட்டி') + '</span><b>' + fmtRs(due.interest) + '</b></div>' +
      '<div class="row total"><span>' + ut('Total payable now','இப்போது செலுத்த வேண்டியது') + '</span><b>' + fmtRs(due.total) + '</b></div>' +
    '</div>';
  }).join('') || '<div class="empty-state">' + ut('No active pledges on record.','செயலில் உள்ள அடகுகள் இல்லை.') + '</div>';

  document.getElementById('app').innerHTML =
    '<div class="hdr">' + langToggleHtml() +
      '<div class="brand">' + esc(IS_TAMIL && PAYLOAD.st ? PAYLOAD.st : (PAYLOAD.sn || 'Pawnshop')) + '</div>' +
      '<div class="sub">' + ut('Customer Passbook', 'வாடிக்கையாளர் பாஸ்புக்') + '</div>' +
    '</div>' +
    '<div class="body">' +
      '<div class="pb-header-row">' +
        '<div><div class="pb-cust">' + esc(PAYLOAD.cn) + '</div>' +
        '<div class="pb-asof">' + ut('Snapshot generated on','தரவு உருவாக்கப்பட்ட தேதி') + ' ' + fmtD(PAYLOAD.gen) + '</div></div>' +
      '</div>' +
      '<div class="summary">' +
        '<div><div class="lbl">' + ut('Total Payable Today','இன்று செலுத்த வேண்டிய மொத்தம்') + '</div><div class="val">' + fmtRs(totalOutstanding) + '</div></div>' +
        '<div style="font-size:26px;">📘</div>' +
      '</div>' +
      '<div class="warn-strip">⚠️ ' + ut('Principal figures are as of the snapshot date above. If you made a payment after that date, the figures here may not reflect it yet — please confirm with the shop.','மேலே உள்ள தேதி வரை உள்ள தரவு இது. அதற்குப் பின் பணம் செலுத்தியிருந்தால், இங்குள்ள தொகை புதுப்பிக்கப்படாமல் இருக்கலாம் — கடையில் உறுதி செய்யவும்.') + '</div>' +
      cardsHtml +
    '</div>' +
    '<div class="shop-foot">' +
      (PAYLOAD.sp ? ('📞 ' + ut('Contact','தொடர்பு') + ': <b>' + esc(PAYLOAD.sp) + '</b>') : '') +
    '</div>';
}

boot();
</script>
</body>
</html>
