# flyer-

<!DOCTYPE html>
<html lang="nl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ouderenavond – De Kettekeet</title>
<style>
* { margin:0; padding:0; box-sizing:border-box; }

/* ── LANGUAGE PICKER OVERLAY ── */
#lang-picker {
  display: none;
  position: fixed;
  inset: 0;
  background: #1A1A1A;
  z-index: 1000;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0;
}
#lang-picker.active { display: flex; }

.picker-mosaic {
  width: 100%;
  height: 12px;
  display: flex;
  position: absolute;
  top: 0;
}
.picker-mosaic.bottom { top: auto; bottom: 0; }
.tm1{background:#CC1126;flex:3} .tm2{background:#F5A623;flex:2} .tm3{background:#2B7BBF;flex:2}
.tm4{background:#7B9E2C;flex:2} .tm5{background:#5B3A8E;flex:1} .tm6{background:#E8421A;flex:2}
.tm7{background:#1A6B4A;flex:2} .tm8{background:#CC1126;flex:2} .tm9{background:#F5A623;flex:1}

.picker-logo {
  display: flex; align-items: center; gap: 12px;
  margin-bottom: 40px;
}
.picker-logo svg { width: 44px; height: 44px; }
.picker-logo-text { color: white; font-family: Arial, sans-serif; }
.picker-logo-name { font-size: 22px; font-weight: 900; letter-spacing: -0.5px; }
.picker-logo-sub { font-size: 11px; color: rgba(255,255,255,0.5); letter-spacing: 1px; text-transform: uppercase; }

.picker-prompt {
  font-family: Arial, sans-serif;
  font-size: 14px;
  color: rgba(255,255,255,0.5);
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 28px;
}

.lang-options {
  display: flex;
  flex-direction: column;
  gap: 12px;
  width: 280px;
}

.lang-btn {
  display: flex;
  align-items: center;
  gap: 16px;
  background: rgba(255,255,255,0.06);
  border: 1.5px solid rgba(255,255,255,0.12);
  border-radius: 10px;
  padding: 16px 20px;
  cursor: pointer;
  transition: background 0.15s, border-color 0.15s;
  width: 100%;
  text-align: left;
}
.lang-btn:hover {
  background: rgba(255,255,255,0.12);
  border-color: rgba(255,255,255,0.3);
}
.lang-flag {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  flex-shrink: 0;
}
.flag-nl { background: #003DA5; }
.flag-fr { background: #EF4135; }
.flag-ar { background: #007A3D; }

.lang-btn-text { font-family: Arial, sans-serif; }
.lang-btn-name { font-size: 16px; font-weight: 700; color: white; display: block; }
.lang-btn-native { font-size: 12px; color: rgba(255,255,255,0.5); display: block; margin-top: 1px; }

/* ── FLYER PAGE ── */
body {
  background: #f0ede8;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  min-height: 100vh;
  padding: 2rem;
  font-family: Arial, sans-serif;
}

.page {
  width: 210mm;
  min-height: 297mm;
  background: white;
  position: relative;
  overflow: hidden;
}

.header { background: #CC1126; position: relative; overflow: hidden; }

.mosaic-row { display: flex; }
.tile { flex:1; height:10px; }
.t1{background:#CC1126} .t2{background:#E8421A} .t3{background:#F5A623}
.t4{background:#7B9E2C} .t5{background:#2B7BBF} .t6{background:#5B3A8E}
.t7{background:#1A6B4A} .t8{background:#CC1126} .t9{background:#E8421A}

.header-content { padding: 28px 32px 24px; position: relative; }
.header-content::before {
  content:''; position:absolute; right:-20px; top:-20px;
  width:200px; height:200px; border-radius:50%;
  border:40px solid rgba(255,255,255,0.07);
}

.supertitle {
  font-size:11px; font-weight:700; letter-spacing:2px;
  text-transform:uppercase; color:rgba(255,255,255,0.7); margin-bottom:8px;
}
.main-title {
  font-size:44px; font-weight:900; color:white;
  line-height:1.0; margin-bottom:4px; letter-spacing:-1px;
}
.sub-title { font-size:16px; color:rgba(255,255,255,0.85); margin-top:6px; }

/* RTL for Arabic */
.rtl { direction: rtl; text-align: right; }
.rtl .header-content { padding: 28px 32px 24px; }
.rtl .intro { border-left: none; border-right: 4px solid #CC1126; padding-left: 0; padding-right: 14px; }
.rtl .section-label { text-align: right; }
.rtl .partner-chip { flex-direction: row-reverse; }
.rtl .qr-section { flex-direction: row-reverse; }
.rtl .qr-text { text-align: right; }
.rtl .lang-badges { justify-content: flex-end; }
.rtl .footer-address { text-align: left; }
.rtl .item-card { flex-direction: row-reverse; text-align: right; }

.date-banner { background:#1A1A1A; display:flex; align-items:stretch; }
.date-block {
  background:#F5A623; padding:14px 28px;
  display:flex; flex-direction:column; align-items:center;
  justify-content:center; min-width:130px;
}
.date-day { font-size:38px; font-weight:900; color:#1A1A1A; line-height:1; }
.date-month { font-size:13px; font-weight:700; color:#1A1A1A; text-transform:uppercase; letter-spacing:1px; }
.date-info { padding:14px 24px; display:flex; flex-direction:column; justify-content:center; gap:4px; }
.date-time { font-size:22px; font-weight:700; color:white; letter-spacing:-0.5px; }
.date-location { font-size:13px; color:rgba(255,255,255,0.7); }

.body { padding:28px 32px; }
.intro {
  font-size:15px; color:#333; line-height:1.6; margin-bottom:24px;
  border-left:4px solid #CC1126; padding-left:14px;
}
.section-label {
  font-size:10px; font-weight:700; letter-spacing:2px;
  text-transform:uppercase; color:#CC1126; margin-bottom:12px;
}
.items-grid { display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-bottom:24px; }
.item-card {
  border:1.5px solid #e8e8e8; border-radius:6px; padding:12px 14px;
  display:flex; align-items:flex-start; gap:10px;
}
.item-icon {
  width:32px; height:32px; border-radius:50%;
  display:flex; align-items:center; justify-content:center;
  flex-shrink:0; font-size:15px;
}
.icon-red{background:#fde8eb} .icon-blue{background:#e3eef9}
.icon-green{background:#e4f0d8} .icon-orange{background:#fdf0d8}
.item-text strong { display:block; font-size:13px; font-weight:700; color:#1A1A1A; margin-bottom:2px; }
.item-text span { font-size:11.5px; color:#666; line-height:1.4; }

.partners-section { margin-bottom:24px; }
.partners-row { display:flex; gap:8px; flex-wrap:wrap; }
.partner-chip {
  background:#f5f5f5; border:1px solid #ddd; border-radius:4px;
  padding:7px 14px; font-size:12px; font-weight:600; color:#333;
  display:flex; align-items:center; gap:6px;
}
.partner-dot { width:8px; height:8px; border-radius:50%; background:#CC1126; }

.qr-section {
  background:#f9f6f2; border-radius:8px; padding:18px 20px;
  display:flex; align-items:center; gap:20px; margin-bottom:24px;
  border:1px solid #ece8e2;
}
.qr-img { width:80px; height:80px; flex-shrink:0; image-rendering:pixelated; border-radius:4px; }
.qr-label { font-size:13px; font-weight:700; color:#1A1A1A; margin-bottom:4px; }
.qr-desc { font-size:11.5px; color:#666; line-height:1.5; }
.lang-badges { display:flex; gap:6px; margin-top:8px; flex-wrap:wrap; }
.lang-badge { font-size:10px; font-weight:700; letter-spacing:0.5px; padding:3px 8px; border-radius:3px; text-transform:uppercase; }
.lang-nl{background:#003DA5;color:white} .lang-fr{background:#EF4135;color:white} .lang-ar{background:#007A3D;color:white}

.footer { position:absolute; bottom:0; left:0; right:0; }
.mosaic-footer { display:flex; height:8px; }
.footer-bar {
  background:#1A1A1A; padding:12px 32px;
  display:flex; align-items:center; justify-content:space-between;
}
.leuven-logo { display:flex; align-items:center; gap:10px; }
.footer-name { font-size:16px; font-weight:900; color:white; letter-spacing:-0.5px; }
.footer-tagline { font-size:10px; color:rgba(255,255,255,0.5); letter-spacing:1px; text-transform:uppercase; }
.footer-address { font-size:11px; color:rgba(255,255,255,0.6); text-align:right; line-height:1.5; }

@media print {
  body { background:white; padding:0; }
  #lang-picker { display:none !important; }
}
</style>
</head>
<body>

<!-- ══ LANGUAGE PICKER ══ -->
<div id="lang-picker">
  <div class="picker-mosaic">
    <div class="tm1"></div><div class="tm2"></div><div class="tm3"></div>
    <div class="tm4"></div><div class="tm5"></div><div class="tm6"></div>
    <div class="tm7"></div><div class="tm8"></div><div class="tm9"></div>
  </div>

  <div class="picker-logo">
    <svg viewBox="0 0 44 44" xmlns="http://www.w3.org/2000/svg">
      <circle cx="22" cy="22" r="21" fill="#CC1126"/>
      <path d="M22 1 A21 21 0 0 1 43 22" fill="#F5A623"/>
      <path d="M43 22 A21 21 0 0 1 31 40" fill="#2B7BBF"/>
      <path d="M31 40 A21 21 0 0 1 11 39" fill="#7B9E2C"/>
      <path d="M11 39 A21 21 0 0 1 1 22" fill="#5B3A8E"/>
      <path d="M1 22 A21 21 0 0 1 11 5" fill="#E8421A"/>
      <path d="M11 5 A21 21 0 0 1 22 1" fill="#1A6B4A"/>
      <circle cx="22" cy="22" r="10" fill="white"/>
      <text x="22" y="27" font-family="Arial" font-weight="900" font-size="11" fill="#CC1126" text-anchor="middle">L</text>
    </svg>
    <div class="picker-logo-text">
      <div class="picker-logo-name">leuven</div>
      <div class="picker-logo-sub">De Kettekeet</div>
    </div>
  </div>

  <div class="picker-prompt">Kies uw taal / Choisissez votre langue / اختر لغتك</div>

  <div class="lang-options">
    <button class="lang-btn" onclick="setLang('nl')">
      <div class="lang-flag flag-nl" style="color:white;font-size:14px;font-weight:700">NL</div>
      <div class="lang-btn-text">
        <span class="lang-btn-name">Nederlands</span>
        <span class="lang-btn-native">Vlaams / Belgisch</span>
      </div>
    </button>
    <button class="lang-btn" onclick="setLang('fr')">
      <div class="lang-flag flag-fr" style="color:white;font-size:14px;font-weight:700">FR</div>
      <div class="lang-btn-text">
        <span class="lang-btn-name">Français</span>
        <span class="lang-btn-native">Soirée des parents</span>
      </div>
    </button>
    <button class="lang-btn" onclick="setLang('ar')">
      <div class="lang-flag flag-ar" style="color:white;font-size:14px;font-weight:700">AR</div>
      <div class="lang-btn-text">
        <span class="lang-btn-name">العربية</span>
        <span class="lang-btn-native">أمسية الآباء والأمهات</span>
      </div>
    </button>
  </div>

  <div class="picker-mosaic bottom">
    <div class="tm3"></div><div class="tm7"></div><div class="tm2"></div>
    <div class="tm5"></div><div class="tm1"></div><div class="tm4"></div>
    <div class="tm6"></div><div class="tm8"></div><div class="tm9"></div>
  </div>
</div>

<!-- ══ FLYER ══ -->
<div class="page" id="flyer">

  <div class="header">
    <div class="mosaic-row">
      <div class="tile t1"></div><div class="tile t3"></div><div class="tile t5"></div>
      <div class="tile t4"></div><div class="tile t2"></div><div class="tile t6"></div>
      <div class="tile t7"></div><div class="tile t3"></div><div class="tile t5"></div>
      <div class="tile t1"></div><div class="tile t4"></div><div class="tile t2"></div>
      <div class="tile t6"></div><div class="tile t3"></div><div class="tile t7"></div>
      <div class="tile t5"></div><div class="tile t1"></div><div class="tile t2"></div>
      <div class="tile t4"></div><div class="tile t3"></div>
    </div>
    <div class="header-content">
      <div class="supertitle" id="t-supertitle">De Kettekeet · Buurtcentrum Leuven</div>
      <div class="main-title" id="t-title">Ouderen&shy;avond</div>
      <div class="sub-title" id="t-subtitle">Activiteiten voor uw kinderen deze zomer — kom alles ontdekken!</div>
    </div>
    <div class="mosaic-row" style="height:6px">
      <div class="tile t2"></div><div class="tile t7"></div><div class="tile t3"></div>
      <div class="tile t5"></div><div class="tile t1"></div><div class="tile t6"></div>
      <div class="tile t4"></div><div class="tile t2"></div><div class="tile t3"></div>
      <div class="tile t7"></div><div class="tile t5"></div><div class="tile t1"></div>
      <div class="tile t6"></div><div class="tile t4"></div><div class="tile t2"></div>
      <div class="tile t3"></div><div class="tile t7"></div><div class="tile t5"></div>
      <div class="tile t1"></div><div class="tile t6"></div>
    </div>
  </div>

  <div class="date-banner">
    <div class="date-block">
      <div class="date-day">3</div>
      <div class="date-month" id="t-month">Juni 2025</div>
    </div>
    <div class="date-info">
      <div class="date-time">16:00 – 18:00</div>
      <div class="date-location" id="t-location">De Kettekeet · Buurtcentrum · Leuven</div>
    </div>
  </div>

  <div class="body">
    <p class="intro" id="t-intro">
      Bent u op zoek naar leuke activiteiten voor uw kind deze zomer? Kom langs op onze ouderenavond en ontdek kampen, speelstraten, hobbyclubs en veel meer — alles op één plek!
    </p>

    <div class="section-label" id="t-what-label">Wat kan u verwachten?</div>
    <div class="items-grid">
      <div class="item-card">
        <div class="item-icon icon-red">🏕️</div>
        <div class="item-text">
          <strong id="t-i1-title">Infokraampjes</strong>
          <span id="t-i1-desc">Kampen, speelstraten en zomerse activiteiten in de buurt</span>
        </div>
      </div>
      <div class="item-card">
        <div class="item-icon icon-blue">⚽</div>
        <div class="item-text">
          <strong id="t-i2-title">Inschrijven hobby's</strong>
          <span id="t-i2-desc">Turnen, dansen, sport en meer — direct inschrijven ter plaatse</span>
        </div>
      </div>
      <div class="item-card">
        <div class="item-icon icon-green">🍽️</div>
        <div class="item-text">
          <strong id="t-i3-title">Multicultureel eten</strong>
          <span id="t-i3-desc">Ouders uit de buurt brengen gerechten uit hun cultuur mee</span>
        </div>
      </div>
      <div class="item-card">
        <div class="item-icon icon-orange">🎨</div>
        <div class="item-text">
          <strong id="t-i4-title">Knutselactiviteiten</strong>
          <span id="t-i4-desc">Leuke doe-activiteiten voor kinderen en ouders samen</span>
        </div>
      </div>
    </div>

    <div class="partners-section">
      <div class="section-label" id="t-partners-label">Aanwezig op de avond</div>
      <div class="partners-row">
        <div class="partner-chip"><div class="partner-dot"></div>Jeugddienst Leuven</div>
        <div class="partner-chip"><div class="partner-dot"></div>Uitpas</div>
        <div class="partner-chip"><div class="partner-dot"></div>Rap op Stap</div>
        <div class="partner-chip"><div class="partner-dot"></div>TOF Sportvakantie</div>
      </div>
    </div>

    <div class="qr-section">
      <img class="qr-img" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAN4AAADeCAIAAADdBSngAAAE9UlEQVR4nO3dS4oYNwBAwTjkIoEscv/TZBHIHbwweJcDKAQh9HkzU7X2dPfYD4Gsbunbzx/ff4GeX18/APw3aRIlTaKkSZQ0iZImUdIkSppESZMoaRIlTaJ+m/lDv//x5+nn+B///P3Xwk+NzzxeZ+33mnmembvPmHnCc1c+Z+aZjZpESZMoaRIlTaKkSdTUDH20NiucMTNzXJu37po1zzzP2t3PPeGMt/+mI6MmUdIkSppESZMoaRK1OEMfnVuPXrvOuVXstevM/NTaKn9tZr3reYyaREmTKGkSJU2ipEnUthn617E2b9012117x+DmWvwuRk2ipEmUNImSJlHSJOpDztBr33TPWPt6/dy9+oyaREmTKGkSJU2ipEnUthn621nhrtn3zfe6z329Pjr3Zv45Rk2ipEmUNImSJlHSJGpxhv52J/Bd89abO7y9/TMz3v6bjoyaREmTKGkSJU2ipEnU1Ay9/9b0udnlrvnv6NyX6Wu70tUYNYmSJlHSJEqaREmTqMXz0G/uH35uF/SZu8/ca+Y6b09/m1H7CsCoSZQ0iZImUdIkSppEffv54/uWC/XP+669xT2qnaL+duc6oyZR0iRKmkRJkyhpErXtO/SbK93n3vS++bb86CPuHXfub8yoSZQ0iZImUdIkSppELa6hv53Jrrl5Ivk5N/eN38UaOp+KNImSJlHSJEqaRC1+hz7aNXOsrWLvus7bXdlvrrOvPc/IqEmUNImSJlHSJEqaRG07D31txlebNfd3wKvxljtfjjSJkiZR0iRKmkRNveW+Nrtcm1m/3U1udPNL+V2/+9uv+3f9FkZNoqRJlDSJkiZR0iRq23nou+Zlb98hP7fKv8vaM9/c733X3Y2aREmTKGkSJU2ipEnU1TX0m++0v32e/rlyN79MN0PnU5EmUdIkSppESZOobeehz3h7cndt9/K38+j+/1cYNYmSJlHSJEqaREmTqG3noY9uvjH+9lv1c3P/c3u519b9R0ZNoqRJlDSJkiZR0iTq4Fvuu65zbtV45jr9df/aCfIjO8XxqUiTKGkSJU2ipEnU49PW1q4z81M3T1KbcW4+fnOX+NG5N+qNmkRJkyhpEiVNoqRJ1LYZem1Vfe3u55zb2X7Xdd5+lT8yahIlTaKkSZQ0iZImUVfX0Ec3d0I7d501N8+D23X3meuMzND5VKRJlDSJkiZR0iTq8Rr6ruvc3Be9dirZuefZdXdvufOpSJMoaRIlTaKkSdTiTnEz+ieO7XJzJ72bb+bPOPfNu1GTKGkSJU2ipEmUNIm6eh76LrvWmmvz33Or/LX/MbCGzgcmTaKkSZQ0iZImUVNvudfmrW/PVT+3d/ralc/tfr+LNXQ+FWkSJU2ipEmUNIla/A69fwb3rnudO/38I+6vfnNN36hJlDSJkiZR0iRKmkTl9nLfdfebK8I37z46t86+6+5rjJpESZMoaRIlTaKkSdS2GfrnsLZGvOsN9nPr2qNzM+tdVzZqEiVNoqRJlDSJkiZRn2SGfvPL9No+bDfX9G++mW/UJEqaREmTKGkSJU2icuehr1mbk669H35ztrvrHPNzv8W5Kxs1iZImUdIkSppESZOoxRn6293dZ+6+a+a4Ntu9ub/6293knIfOlyNNoqRJlDSJkiZRH/I8dL4CoyZR0iRKmkRJkyhpEiVNoqRJlDSJkiZR0iRKmkT9C/aD4ZAX1FESAAAAAElFTkSuQmCC" alt="QR code">
      <div class="qr-text">
        <div class="qr-label" id="t-qr-label">Meer info in uw taal</div>
        <div class="qr-desc" id="t-qr-desc">Scan de QR-code met uw telefoon voor alle informatie in het Frans of Arabisch.</div>
        <div class="lang-badges">
          <span class="lang-badge lang-nl">NL</span>
          <span class="lang-badge lang-fr">FR</span>
          <span class="lang-badge lang-ar">AR</span>
        </div>
      </div>
    </div>
  </div>

  <div class="footer">
    <div class="mosaic-footer">
      <div class="tile t5" style="flex:3"></div><div class="tile t3" style="flex:2"></div>
      <div class="tile t7" style="flex:2"></div><div class="tile t6" style="flex:1"></div>
      <div class="tile t2" style="flex:2"></div><div class="tile t4" style="flex:3"></div>
      <div class="tile t1" style="flex:2"></div><div class="tile t3" style="flex:2"></div>
      <div class="tile t5" style="flex:1"></div><div class="tile t7" style="flex:2"></div>
    </div>
    <div class="footer-bar">
      <div class="leuven-logo">
        <svg width="32" height="32" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg">
          <circle cx="16" cy="16" r="15" fill="#CC1126"/>
          <path d="M16 1 A15 15 0 0 1 31 16" fill="#F5A623"/>
          <path d="M31 16 A15 15 0 0 1 22 29" fill="#2B7BBF"/>
          <path d="M22 29 A15 15 0 0 1 8 28" fill="#7B9E2C"/>
          <path d="M8 28 A15 15 0 0 1 1 16" fill="#5B3A8E"/>
          <path d="M1 16 A15 15 0 0 1 8 4" fill="#E8421A"/>
          <path d="M8 4 A15 15 0 0 1 16 1" fill="#1A6B4A"/>
          <circle cx="16" cy="16" r="7" fill="white"/>
          <text x="16" y="20" font-family="Arial" font-weight="900" font-size="8" fill="#CC1126" text-anchor="middle">L</text>
        </svg>
        <div>
          <div class="footer-name">leuven</div>
          <div class="footer-tagline">Buurtcentrum De Kettekeet</div>
        </div>
      </div>
      <div class="footer-address" id="t-address">
        De Kettekeet · [adres invullen]<br>
        [contactpersoon] · [tel/mail]
      </div>
    </div>
  </div>
</div>

<script>
const translations = {
  nl: {
    lang: 'nl',
    rtl: false,
    supertitle: 'De Kettekeet · Buurtcentrum Leuven',
    title: 'Ouderenavond',
    subtitle: 'Activiteiten voor uw kinderen deze zomer — kom alles ontdekken!',
    month: 'Juni 2025',
    location: 'De Kettekeet · Buurtcentrum · Leuven',
    intro: 'Bent u op zoek naar leuke activiteiten voor uw kind deze zomer? Kom langs op onze ouderenavond en ontdek kampen, speelstraten, hobbyclubs en veel meer — alles op één plek!',
    whatLabel: 'Wat kan u verwachten?',
    i1Title: 'Infokraampjes',
    i1Desc: 'Kampen, speelstraten en zomerse activiteiten in de buurt',
    i2Title: "Inschrijven hobby's",
    i2Desc: 'Turnen, dansen, sport en meer — direct inschrijven ter plaatse',
    i3Title: 'Multicultureel eten',
    i3Desc: 'Ouders uit de buurt brengen gerechten uit hun cultuur mee',
    i4Title: 'Knutselactiviteiten',
    i4Desc: 'Leuke doe-activiteiten voor kinderen en ouders samen',
    partnersLabel: 'Aanwezig op de avond',
    qrLabel: 'Meer info in uw taal',
    qrDesc: 'Scan de QR-code met uw telefoon voor alle informatie in het Frans of Arabisch.',
    address: 'De Kettekeet · [adres invullen]<br>[contactpersoon] · [tel/mail]',
  },
  fr: {
    lang: 'fr',
    rtl: false,
    supertitle: 'De Kettekeet · Centre de quartier Leuven',
    title: 'Soirée parents',
    subtitle: 'Activités pour vos enfants cet été — venez tout découvrir !',
    month: 'Juin 2025',
    location: 'De Kettekeet · Centre de quartier · Leuven',
    intro: "Vous cherchez des activités amusantes pour votre enfant cet été ? Venez à notre soirée parents et découvrez des camps, des rues de jeux, des clubs de loisirs et bien plus encore — tout en un seul endroit !",
    whatLabel: 'Que pouvez-vous attendre ?',
    i1Title: 'Stands d\'information',
    i1Desc: 'Camps, rues de jeux et activités estivales dans le quartier',
    i2Title: "Inscription aux loisirs",
    i2Desc: 'Gym, danse, sport et plus — inscription sur place directement',
    i3Title: 'Repas multiculturels',
    i3Desc: 'Des parents du quartier apportent des plats de leur culture',
    i4Title: 'Activités créatives',
    i4Desc: 'Activités manuelles amusantes pour enfants et parents ensemble',
    partnersLabel: 'Présents lors de la soirée',
    qrLabel: 'Plus d\'info dans votre langue',
    qrDesc: 'Scannez le code QR avec votre téléphone pour toutes les informations en néerlandais ou en arabe.',
    address: 'De Kettekeet · [adresse à compléter]<br>[contact] · [tél/mail]',
  },
  ar: {
    lang: 'ar',
    rtl: true,
    supertitle: 'دي كيتيكيت · مركز الحي لوفن',
    title: 'أمسية الآباء والأمهات',
    subtitle: 'أنشطة لأطفالكم هذا الصيف — تعالوا واكتشفوا كل شيء!',
    month: 'يونيو 2025',
    location: 'دي كيتيكيت · مركز الحي · لوفن',
    intro: 'هل تبحثون عن أنشطة ممتعة لطفلكم هذا الصيف؟ تعالوا إلى أمسية الآباء واكتشفوا المخيمات وشوارع اللعب والأندية الترفيهية وأكثر من ذلك بكثير — كل شيء في مكان واحد!',
    whatLabel: 'ماذا يمكنكم أن تتوقعوا؟',
    i1Title: 'أكشاك المعلومات',
    i1Desc: 'مخيمات وشوارع للعب وأنشطة صيفية في الحي',
    i2Title: 'التسجيل في الهوايات',
    i2Desc: 'جمناستيك، رقص، رياضة والمزيد — التسجيل مباشرة في المكان',
    i3Title: 'أكل متعدد الثقافات',
    i3Desc: 'أولياء الأمور من الحي يجلبون أطباقاً من ثقافاتهم',
    i4Title: 'أنشطة إبداعية',
    i4Desc: 'أنشطة يدوية ممتعة للأطفال وأولياء الأمور معاً',
    partnersLabel: 'الحاضرون في الأمسية',
    qrLabel: 'مزيد من المعلومات بلغتكم',
    qrDesc: 'امسح رمز QR بهاتفكم للحصول على جميع المعلومات بالفرنسية أو الهولندية.',
    address: 'دي كيتيكيت · [العنوان]<br>[المسؤول] · [هاتف/بريد]',
  }
};

function setLang(code) {
  const t = translations[code];
  const flyer = document.getElementById('flyer');

  document.getElementById('t-supertitle').textContent = t.supertitle;
  document.getElementById('t-title').innerHTML = t.title;
  document.getElementById('t-subtitle').textContent = t.subtitle;
  document.getElementById('t-month').textContent = t.month;
  document.getElementById('t-location').textContent = t.location;
  document.getElementById('t-intro').textContent = t.intro;
  document.getElementById('t-what-label').textContent = t.whatLabel;
  document.getElementById('t-i1-title').textContent = t.i1Title;
  document.getElementById('t-i1-desc').textContent = t.i1Desc;
  document.getElementById('t-i2-title').textContent = t.i2Title;
  document.getElementById('t-i2-desc').textContent = t.i2Desc;
  document.getElementById('t-i3-title').textContent = t.i3Title;
  document.getElementById('t-i3-desc').textContent = t.i3Desc;
  document.getElementById('t-i4-title').textContent = t.i4Title;
  document.getElementById('t-i4-desc').textContent = t.i4Desc;
  document.getElementById('t-partners-label').textContent = t.partnersLabel;
  document.getElementById('t-qr-label').textContent = t.qrLabel;
  document.getElementById('t-qr-desc').textContent = t.qrDesc;
  document.getElementById('t-address').innerHTML = t.address;

  if (t.rtl) {
    flyer.classList.add('rtl');
    flyer.setAttribute('lang', 'ar');
    flyer.setAttribute('dir', 'rtl');
  } else {
    flyer.classList.remove('rtl');
    flyer.setAttribute('lang', t.lang);
    flyer.removeAttribute('dir');
  }

  document.getElementById('lang-picker').classList.remove('active');
  window.location.hash = code;
}

function init() {
  const hash = window.location.hash.replace('#','');
  if (hash === 'fr' || hash === 'ar' || hash === 'nl') {
    setLang(hash);
  } else if (hash === 'select') {
    document.getElementById('lang-picker').classList.add('active');
  }
  // default: NL flyer shown as-is (no picker, no redirect)
}

window.addEventListener('load', init);
window.addEventListener('hashchange', init);
</script>
</body>
</html>
