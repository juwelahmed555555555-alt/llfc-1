<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>LLFC eFootball Division System</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Rajdhani:wght@400;500;600;700&family=Montserrat:wght@400;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
<style>
/* ===== UCL THEME ===== */
:root{
  --ucl-navy:#0A1628;
  --ucl-blue:#1B3A6B;
  --ucl-mid:#2A5298;
  --ucl-light:#4472C4;
  --ucl-bright:#5B8FE8;
  --ucl-star:#F5C518;
  --ucl-silver:#C8D8F0;
  --ucl-white:#EEF4FF;
  --ucl-dark:#060E1C;
  --ucl-card:#0D1F3C;
  --ucl-border:rgba(68,114,196,0.35);
  --gold:#FFD700;--silver:#C0C0C0;--bronze:#CD7F32;
  --green:#00E676;--yellow:#FFEA00;--red:#FF3D3D;--purple:#CE93D8;
  --card-bg:var(--ucl-card);--card-border:var(--ucl-border);
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{font-family:'Montserrat',sans-serif;background:var(--ucl-dark);color:var(--ucl-white);min-height:100vh;overflow-x:hidden;}

/* Stars bg */
body::before{
  content:'';position:fixed;inset:0;
  background:
    radial-gradient(ellipse at 20% 20%, rgba(27,58,107,0.5) 0%, transparent 50%),
    radial-gradient(ellipse at 80% 80%, rgba(42,82,152,0.3) 0%, transparent 50%),
    radial-gradient(ellipse at 50% 50%, rgba(6,14,28,0.8) 0%, transparent 100%);
  pointer-events:none;z-index:0;
}
body::after{
  content:'';position:fixed;inset:0;
  background-image:
    radial-gradient(1px 1px at 10% 15%, rgba(245,197,24,0.6) 0%, transparent 100%),
    radial-gradient(1px 1px at 30% 40%, rgba(245,197,24,0.4) 0%, transparent 100%),
    radial-gradient(1px 1px at 50% 25%, rgba(255,255,255,0.3) 0%, transparent 100%),
    radial-gradient(1px 1px at 70% 60%, rgba(245,197,24,0.5) 0%, transparent 100%),
    radial-gradient(1px 1px at 85% 20%, rgba(255,255,255,0.25) 0%, transparent 100%),
    radial-gradient(1px 1px at 15% 70%, rgba(245,197,24,0.4) 0%, transparent 100%),
    radial-gradient(1px 1px at 60% 80%, rgba(255,255,255,0.2) 0%, transparent 100%),
    radial-gradient(1px 1px at 90% 45%, rgba(245,197,24,0.35) 0%, transparent 100%),
    radial-gradient(1px 1px at 40% 90%, rgba(255,255,255,0.15) 0%, transparent 100%),
    radial-gradient(1px 1px at 75% 35%, rgba(245,197,24,0.5) 0%, transparent 100%);
  pointer-events:none;z-index:0;
}

/* ===== HEADER ===== */
header{
  position:sticky;top:0;z-index:1000;
  background:rgba(6,14,28,0.97);
  backdrop-filter:blur(16px);
  border-bottom:1px solid var(--ucl-border);
  box-shadow:0 4px 30px rgba(27,58,107,0.5);
}
.header-inner{max-width:1400px;margin:0 auto;padding:0 20px;display:flex;align-items:center;justify-content:space-between;height:62px;gap:8px;}
.logo-area{display:flex;align-items:center;gap:12px;cursor:pointer;flex-shrink:0;}
.logo-badge{
  width:44px;height:44px;
  background:linear-gradient(135deg,var(--ucl-mid),var(--ucl-blue));
  border:2px solid var(--ucl-light);
  border-radius:50%;display:flex;align-items:center;justify-content:center;
  font-family:'Bebas Neue',sans-serif;font-size:13px;color:white;
  box-shadow:0 0 16px rgba(68,114,196,0.5);flex-shrink:0;letter-spacing:0.5px;
}
.logo-text{display:flex;flex-direction:column;line-height:1.1;}
.logo-main{font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:3px;color:var(--ucl-white);}
.logo-sub{font-size:9px;color:var(--ucl-star);letter-spacing:4px;text-transform:uppercase;font-weight:700;}
.header-nav{display:flex;gap:2px;align-items:center;}
.nav-btn{
  background:none;border:1px solid transparent;color:var(--ucl-silver);
  padding:7px 14px;font-family:'Montserrat',sans-serif;font-weight:600;font-size:12px;
  letter-spacing:1px;cursor:pointer;border-radius:4px;transition:all .2s;text-transform:uppercase;
}
.nav-btn:hover,.nav-btn.active{color:var(--ucl-white);border-color:var(--ucl-light);background:rgba(68,114,196,0.18);}
.header-auth{display:flex;gap:6px;align-items:center;flex-shrink:0;}
.btn-login{
  background:transparent;border:1px solid var(--ucl-light);color:var(--ucl-bright);
  padding:6px 14px;font-family:'Montserrat',sans-serif;font-weight:700;font-size:12px;
  cursor:pointer;border-radius:4px;transition:all .2s;text-transform:uppercase;
}
.btn-login:hover{background:var(--ucl-mid);color:white;}
.btn-register{
  background:linear-gradient(135deg,var(--ucl-mid),var(--ucl-light));
  border:none;color:white;padding:6px 14px;
  font-family:'Montserrat',sans-serif;font-weight:700;font-size:12px;
  cursor:pointer;border-radius:4px;transition:all .2s;text-transform:uppercase;
}
.btn-register:hover{background:linear-gradient(135deg,var(--ucl-light),var(--ucl-bright));box-shadow:0 0 12px rgba(68,114,196,0.5);}
.user-pill{
  display:flex;align-items:center;gap:8px;
  background:rgba(68,114,196,0.15);border:1px solid var(--ucl-light);
  border-radius:20px;padding:4px 14px 4px 4px;cursor:pointer;
}
.user-avatar{
  width:30px;height:30px;
  background:linear-gradient(135deg,var(--ucl-mid),var(--ucl-light));
  border-radius:50%;display:flex;align-items:center;justify-content:center;
  font-size:12px;font-weight:700;flex-shrink:0;font-family:'Bebas Neue',sans-serif;
}
.user-name{font-size:13px;font-weight:600;color:var(--ucl-white);}
.mod-badge-hdr{font-size:9px;background:rgba(206,147,216,0.25);border:1px solid var(--purple);color:var(--purple);padding:1px 5px;border-radius:3px;letter-spacing:1px;}

/* ===== MAIN ===== */
main{position:relative;z-index:1;max-width:1400px;margin:0 auto;padding:24px 20px;min-height:calc(100vh - 62px);}
.page{display:none;}.page.active{display:block;animation:fadeIn 0.3s ease;}
@keyframes fadeIn{from{opacity:0;transform:translateY(8px);}to{opacity:1;transform:translateY(0);}}

/* ===== CARDS ===== */
.card{background:var(--ucl-card);border:1px solid var(--ucl-border);border-radius:10px;padding:20px;}
.card-blue{background:linear-gradient(135deg,rgba(27,58,107,0.5),rgba(10,22,40,0.95));border:1px solid var(--ucl-light);}

/* ===== BUTTONS ===== */
.btn-primary{
  background:linear-gradient(135deg,var(--ucl-mid),var(--ucl-light));
  color:white;border:none;padding:10px 24px;
  font-family:'Montserrat',sans-serif;font-weight:700;font-size:13px;
  letter-spacing:1px;cursor:pointer;border-radius:6px;text-transform:uppercase;
  transition:all .2s;box-shadow:0 4px 14px rgba(68,114,196,0.35);
}
.btn-primary:hover{background:linear-gradient(135deg,var(--ucl-light),var(--ucl-bright));transform:translateY(-1px);box-shadow:0 6px 18px rgba(68,114,196,0.5);}
.btn-secondary{
  background:transparent;color:var(--ucl-silver);
  border:1px solid rgba(68,114,196,0.5);
  padding:10px 24px;font-family:'Montserrat',sans-serif;font-weight:600;font-size:13px;
  cursor:pointer;border-radius:6px;text-transform:uppercase;transition:all .2s;
}
.btn-secondary:hover{border-color:var(--ucl-light);background:rgba(68,114,196,0.1);color:white;}
.btn-sm{padding:5px 12px;font-family:'Montserrat',sans-serif;font-weight:700;font-size:11px;letter-spacing:0.5px;cursor:pointer;border-radius:4px;transition:all .2s;text-transform:uppercase;}
.btn-approve{background:rgba(0,230,118,.15);color:#00E676;border:1px solid rgba(0,230,118,.4);}
.btn-approve:hover{background:rgba(0,230,118,.3);}
.btn-reject{background:rgba(255,61,61,.15);color:#FF3D3D;border:1px solid rgba(255,61,61,.4);}
.btn-reject:hover{background:rgba(255,61,61,.3);}
.btn-edit{background:rgba(255,234,0,.12);color:#FFEA00;border:1px solid rgba(255,234,0,.35);}
.btn-edit:hover{background:rgba(255,234,0,.22);}
.btn-ban{background:rgba(206,147,216,.15);color:#CE93D8;border:1px solid rgba(206,147,216,.35);}
.btn-ban:hover{background:rgba(206,147,216,.25);}
.btn-mod{background:rgba(68,153,255,.14);color:#82B1FF;border:1px solid rgba(68,153,255,.35);}
.btn-mod:hover{background:rgba(68,153,255,.25);}
.w-full{width:100%;}

/* ===== SECTION TITLE ===== */
.section-title{
  font-family:'Bebas Neue',sans-serif;font-size:26px;letter-spacing:4px;
  color:var(--ucl-white);display:flex;align-items:center;gap:14px;margin-bottom:18px;
}
.section-title::after{content:'';flex:1;height:1px;background:linear-gradient(90deg,var(--ucl-light),transparent);}

/* ===== HERO ===== */
.hero{
  background:linear-gradient(135deg,rgba(27,58,107,0.5) 0%,rgba(10,22,40,0.95) 60%);
  border:1px solid var(--ucl-light);border-radius:14px;padding:40px 32px;margin-bottom:24px;
  position:relative;overflow:hidden;
}
.hero::before{
  content:'UCL';position:absolute;right:-20px;bottom:-30px;
  font-family:'Bebas Neue',sans-serif;font-size:220px;
  color:rgba(68,114,196,0.05);pointer-events:none;line-height:1;letter-spacing:10px;
}
.hero::after{
  content:'';position:absolute;top:0;left:0;right:0;height:2px;
  background:linear-gradient(90deg,transparent,var(--ucl-star),var(--ucl-light),transparent);
}
.hero-tag{
  display:inline-block;background:linear-gradient(135deg,var(--ucl-star),#E6A800);
  color:#0A1628;font-size:11px;font-weight:800;letter-spacing:3px;
  padding:3px 12px;border-radius:2px;margin-bottom:12px;text-transform:uppercase;
}
.hero h1{font-family:'Bebas Neue',sans-serif;font-size:clamp(32px,5vw,68px);letter-spacing:5px;line-height:1;margin-bottom:12px;color:var(--ucl-white);}
.hero h1 span{color:var(--ucl-star);}
.hero p{color:var(--ucl-silver);font-size:15px;max-width:520px;margin-bottom:24px;line-height:1.6;}
.hero-actions{display:flex;gap:12px;flex-wrap:wrap;}

/* ===== STATS ===== */
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(130px,1fr));gap:12px;margin-bottom:24px;}
.stat-card{
  background:var(--ucl-card);border:1px solid var(--ucl-border);border-radius:10px;padding:16px;
  text-align:center;transition:border-color .2s;
  background:linear-gradient(135deg,rgba(27,58,107,0.3),rgba(10,22,40,0.8));
}
.stat-card:hover{border-color:var(--ucl-light);}
.stat-num{font-family:'Bebas Neue',sans-serif;font-size:36px;color:var(--ucl-star);line-height:1;}
.stat-label{font-size:10px;color:var(--ucl-silver);letter-spacing:2px;text-transform:uppercase;margin-top:4px;}

/* ===== GRIDS ===== */
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:22px;}
.three-col{display:grid;grid-template-columns:repeat(3,1fr);gap:16px;}
@media(max-width:900px){.two-col{grid-template-columns:1fr;}.three-col{grid-template-columns:1fr 1fr;}.header-nav{display:none;}}
@media(max-width:500px){.three-col{grid-template-columns:1fr;}}

/* ===== DIVISION BADGES ===== */
.div-badge{
  display:inline-flex;align-items:center;justify-content:center;
  width:34px;height:34px;border-radius:50%;font-weight:800;font-size:13px;
  flex-shrink:0;font-family:'Montserrat',sans-serif;
}
.div-1{background:linear-gradient(135deg,#FFD700,#FF8C00);color:#000;box-shadow:0 0 10px rgba(255,215,0,0.5);}
.div-2{background:linear-gradient(135deg,#E8E8E8,#909090);color:#000;box-shadow:0 0 8px rgba(192,192,192,0.4);}
.div-3{background:linear-gradient(135deg,#E8A060,#8B4513);color:#fff;box-shadow:0 0 8px rgba(205,127,50,0.4);}
.div-4{background:linear-gradient(135deg,#3A8FD4,#1B5A9E);color:#fff;box-shadow:0 0 6px rgba(58,143,212,0.4);}
.div-5{background:linear-gradient(135deg,#2E75B6,#1A4A7A);color:#eee;}
.div-6{background:linear-gradient(135deg,#1B5499,#0E3060);color:#ccc;}
.div-7{background:linear-gradient(135deg,#123C7A,#082050);color:#bbb;}
.div-8{background:linear-gradient(135deg,#0A2850,#061530);color:#999;border:1px solid #1B3A6B;}
.div-9{background:linear-gradient(135deg,#071428,#030A14);color:#667;border:1px solid #1B3A6B;}

/* ===== DIVISION GUIDE CARDS (bigger, green) ===== */
.div-guide-card{
  background:linear-gradient(135deg,rgba(0,100,50,0.22),rgba(10,22,40,0.9));
  border:1px solid rgba(0,200,80,0.35);border-radius:12px;padding:18px;
  transition:all .2s;
}
.div-guide-card:hover{border-color:rgba(0,230,118,0.6);transform:translateY(-2px);box-shadow:0 6px 20px rgba(0,200,80,0.15);}
.div-guide-name{font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:2px;color:#00E676;margin:8px 0 4px;}
.div-guide-desc{font-size:12px;color:var(--ucl-silver);line-height:1.5;}
.div-guide-pts{font-size:11px;color:#FFEA00;font-weight:700;margin-top:5px;letter-spacing:1px;}
.div-guide-badge{font-size:10px;color:#00E676;margin-top:4px;font-weight:700;letter-spacing:1.5px;}

/* ===== TABLE - FORCED DARK (GitHub-safe) ===== */
.lb-table-wrap{overflow-x:auto;border-radius:10px;border:1px solid var(--ucl-border);background:#060E1C !important;}
table{width:100%;border-collapse:collapse;background:#060E1C !important;color:#D0E4FF !important;}
thead,thead tr{background:#0D1E3A !important;}
thead th{
  padding:12px 14px;text-align:left;font-size:10px;letter-spacing:2px;
  text-transform:uppercase;color:#82B1FF !important;font-weight:700;
  white-space:nowrap;background:#0D1E3A !important;
}
tbody,tbody tr{background:#060E1C !important;}
tbody tr{border-bottom:1px solid rgba(27,58,107,0.5);}
tbody tr:hover{background:#0D1E3A !important;}
tbody tr:last-child{border-bottom:none;}
tbody td{padding:11px 14px;font-size:14px;font-weight:500;vertical-align:middle;color:#D0E4FF !important;background:transparent;}
tbody tr.top-1{background:linear-gradient(90deg,rgba(255,215,0,0.1),#060E1C) !important;}
tbody tr.top-2{background:linear-gradient(90deg,rgba(192,192,192,0.07),#060E1C) !important;}
tbody tr.top-3{background:linear-gradient(90deg,rgba(205,127,50,0.07),#060E1C) !important;}
.rank-num{font-family:'Bebas Neue',sans-serif;font-size:24px;color:#4472C4;}
.rank-1{color:var(--gold)!important;}.rank-2{color:var(--silver)!important;}.rank-3{color:var(--bronze)!important;}

/* WDL PILLS */
.wdl-row{display:flex;align-items:center;gap:5px;}
.wdl-pill{display:inline-flex;align-items:center;gap:3px;padding:4px 9px;border-radius:5px;font-size:12px;font-weight:700;white-space:nowrap;}
.wdl-w{background:rgba(0,230,118,.18);color:#00E676;border:1px solid rgba(0,230,118,.35);}
.wdl-d{background:rgba(255,234,0,.15);color:#FFEA00;border:1px solid rgba(255,234,0,.3);}
.wdl-l{background:rgba(255,61,61,.15);color:#FF5555;border:1px solid rgba(255,61,61,.3);}
.wdl-num{font-family:'Bebas Neue',sans-serif;font-size:17px;line-height:1;}

/* WINRATE */
.winrate-wrap{display:flex;align-items:center;gap:5px;}
.winrate-bar{background:rgba(255,255,255,.08);border-radius:8px;height:5px;width:52px;overflow:hidden;flex-shrink:0;position:relative;}
.winrate-fill{position:absolute;left:0;top:0;bottom:0;background:linear-gradient(90deg,var(--ucl-mid),var(--ucl-bright));border-radius:8px;}
.winrate-pct{font-size:12px;font-weight:700;color:#82B1FF;white-space:nowrap;}

/* FORM DOTS */
.form-dots{display:flex;gap:3px;align-items:center;}
.form-dot{width:9px;height:9px;border-radius:50%;}
.form-w{background:#00E676;}.form-d{background:#FFEA00;}.form-l{background:#FF3D3D;}

/* PLAYER LINK */
.player-link{cursor:pointer;color:#D0E4FF;font-weight:600;transition:color .2s;display:inline-flex;align-items:center;gap:7px;}
.player-link:hover{color:var(--ucl-star);}

/* STATUS BADGES */
.status-badge{display:inline-block;padding:2px 8px;border-radius:8px;font-size:10px;font-weight:700;letter-spacing:1px;text-transform:uppercase;}
.status-confirmed{background:rgba(0,230,118,.18);color:#00E676;border:1px solid rgba(0,230,118,.3);}
.status-pending{background:rgba(255,234,0,.15);color:#FFEA00;border:1px solid rgba(255,234,0,.3);}
.status-disputed{background:rgba(255,61,61,.18);color:#FF5555;border:1px solid rgba(255,61,61,.3);}

/* LB TABS */
.lb-tabs{display:flex;gap:5px;margin-bottom:18px;background:rgba(27,58,107,.2);border:1px solid var(--ucl-border);border-radius:10px;padding:5px;flex-wrap:wrap;}
.lb-tab{flex:1;min-width:70px;background:none;border:none;color:var(--ucl-silver);padding:8px 12px;font-family:'Montserrat',sans-serif;font-weight:600;font-size:12px;cursor:pointer;border-radius:7px;transition:all .2s;text-transform:uppercase;letter-spacing:1px;}
.lb-tab.active{background:linear-gradient(135deg,var(--ucl-mid),var(--ucl-light));color:white;box-shadow:0 2px 8px rgba(68,114,196,0.4);}

/* SEARCH */
.search-bar{display:flex;gap:8px;margin-bottom:16px;}
.search-input{flex:1;background:rgba(27,58,107,.25);border:1px solid var(--ucl-border);border-radius:6px;color:#D0E4FF;padding:10px 14px;font-family:'Montserrat',sans-serif;font-size:14px;}
.search-input:focus{outline:none;border-color:var(--ucl-light);}
.search-input::placeholder{color:#4472C4;}
.form-select-sm{background:rgba(27,58,107,.25);border:1px solid var(--ucl-border);border-radius:6px;color:#D0E4FF;padding:10px 10px;font-family:'Montserrat',sans-serif;font-size:12px;cursor:pointer;}
.form-select-sm:focus{outline:none;border-color:var(--ucl-light);}
.form-select-sm option{background:#0D1E3A;color:#D0E4FF;}

/* FORM INPUTS */
.match-form{display:grid;gap:14px;}
.form-group{display:flex;flex-direction:column;gap:6px;}
.form-label{font-size:10px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:#82B1FF;}
.form-input,.form-select{
  background:rgba(27,58,107,.2);border:1px solid var(--ucl-border);border-radius:6px;
  color:#D0E4FF;padding:10px 14px;font-family:'Montserrat',sans-serif;font-size:14px;
  font-weight:500;transition:border-color .2s;width:100%;
}
.form-input:focus,.form-select:focus{outline:none;border-color:var(--ucl-light);}
.form-select option{background:#0D1E3A;color:#D0E4FF;}
.score-row{display:grid;grid-template-columns:1fr auto 1fr;gap:12px;align-items:center;}
.score-vs{font-family:'Bebas Neue',sans-serif;font-size:24px;color:var(--ucl-star);text-align:center;}
.score-input{text-align:center;font-size:28px;font-family:'Bebas Neue',sans-serif;padding:10px;}

/* MODAL */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.88);z-index:2000;display:none;align-items:center;justify-content:center;padding:16px;backdrop-filter:blur(6px);}
.modal-overlay.open{display:flex;}
.modal{
  background:#0A1628;border:1px solid var(--ucl-light);border-radius:12px;
  padding:26px;width:100%;max-width:480px;max-height:90vh;overflow-y:auto;position:relative;
  box-shadow:0 20px 60px rgba(0,0,0,.7);
}
.modal-title{font-family:'Bebas Neue',sans-serif;font-size:26px;letter-spacing:3px;color:var(--ucl-white);margin-bottom:18px;}
.modal-close{
  position:absolute;top:14px;right:14px;
  background:rgba(68,114,196,.2);border:1px solid var(--ucl-light);
  color:var(--ucl-bright);width:28px;height:28px;border-radius:50%;
  font-size:13px;cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .2s;
}
.modal-close:hover{background:var(--ucl-mid);color:white;}

/* TOAST */
.toast{
  position:fixed;bottom:80px;right:16px;z-index:9999;
  background:#0D1E3A;border-left:4px solid var(--ucl-light);border-radius:8px;
  padding:13px 18px;min-width:240px;max-width:340px;
  box-shadow:0 8px 30px rgba(0,0,0,.6);transform:translateX(120%);
  transition:transform .3s;font-weight:600;font-size:14px;color:#D0E4FF;
}
.toast.show{transform:translateX(0);}
.toast.success{border-color:var(--green);}
.toast.error{border-color:#FF3D3D;}
.toast.info{border-color:var(--ucl-star);}

/* NEWS TICKER */
.news-ticker{
  background:linear-gradient(135deg,rgba(27,58,107,0.4),rgba(10,22,40,0.9));
  border:1px solid var(--ucl-border);border-radius:8px;margin-bottom:18px;overflow:hidden;display:flex;align-items:center;
}
.news-label{
  background:linear-gradient(135deg,var(--ucl-star),#E6A800);color:#0A1628;
  padding:9px 16px;font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:2px;flex-shrink:0;white-space:nowrap;
}
.news-scroll-wrap{overflow:hidden;flex:1;padding:9px 14px;}
.news-scroll-text{font-size:13px;font-weight:600;color:var(--ucl-star);white-space:nowrap;display:inline-block;animation:scrollNews 22s linear infinite;}
@keyframes scrollNews{0%{transform:translateX(100vw);}100%{transform:translateX(-100%);}}

/* MATCH CARD */
.match-card{
  background:linear-gradient(135deg,rgba(27,58,107,.2),rgba(10,22,40,.8));
  border:1px solid var(--ucl-border);border-radius:8px;padding:13px 16px;margin-bottom:9px;
  display:flex;align-items:center;gap:12px;transition:all .2s;
}
.match-card:hover{border-color:var(--ucl-light);transform:translateX(2px);}
.match-card.high-score{border-color:rgba(245,197,24,.45);}
.match-result-badge{width:36px;height:36px;border-radius:6px;display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:17px;font-weight:700;flex-shrink:0;}
.result-W{background:rgba(0,230,118,.2);color:#00E676;border:1px solid rgba(0,230,118,.4);}
.result-D{background:rgba(255,234,0,.18);color:#FFEA00;border:1px solid rgba(255,234,0,.4);}
.result-L{background:rgba(255,61,61,.18);color:#FF5555;border:1px solid rgba(255,61,61,.4);}
.match-info{flex:1;min-width:0;}
.match-vs{font-size:14px;font-weight:600;color:#D0E4FF;}
.match-meta{font-size:11px;color:#4472C4;margin-top:2px;}
.match-score{font-family:'Bebas Neue',sans-serif;font-size:26px;color:var(--ucl-white);text-align:right;flex-shrink:0;}
.high-score-badge{background:rgba(245,197,24,.2);color:var(--ucl-star);border:1px solid rgba(245,197,24,.4);border-radius:4px;font-size:10px;font-weight:700;padding:1px 7px;letter-spacing:1px;}
.x2-badge{background:rgba(0,230,118,.2);color:#00E676;border:1px solid rgba(0,230,118,.4);border-radius:4px;font-size:10px;font-weight:700;padding:1px 7px;letter-spacing:1px;}

/* PENDING */
.pending-item{
  background:linear-gradient(135deg,rgba(27,58,107,.2),rgba(10,22,40,.8));
  border:1px solid var(--ucl-border);border-radius:8px;padding:13px 16px;margin-bottom:8px;
  display:flex;align-items:center;gap:10px;flex-wrap:wrap;
}
.pending-info{flex:1;min-width:120px;}
.pending-name{font-size:15px;font-weight:700;color:#D0E4FF;}
.pending-meta{font-size:11px;color:#4472C4;margin-top:2px;}

/* CONFIRM CARD */
.confirm-card{
  background:linear-gradient(135deg,rgba(68,114,196,.15),rgba(10,22,40,.9));
  border:1px solid var(--ucl-light);border-radius:10px;padding:16px;margin-bottom:12px;
}
.confirm-vs{display:flex;align-items:center;justify-content:space-between;gap:8px;margin-bottom:10px;flex-wrap:wrap;}
.confirm-player{text-align:center;flex:1;}
.confirm-player-name{font-size:15px;font-weight:700;color:#D0E4FF;}
.confirm-score-display{font-family:'Bebas Neue',sans-serif;font-size:36px;color:var(--ucl-star);padding:0 12px;flex-shrink:0;}

/* PROFILE */
.profile-header{display:flex;gap:22px;align-items:flex-start;flex-wrap:wrap;margin-bottom:22px;}
.profile-avatar{
  width:80px;height:80px;
  background:linear-gradient(135deg,var(--ucl-blue),var(--ucl-light));
  border:3px solid var(--ucl-light);border-radius:50%;display:flex;align-items:center;justify-content:center;
  font-family:'Bebas Neue',sans-serif;font-size:32px;color:white;flex-shrink:0;
  box-shadow:0 0 24px rgba(68,114,196,.5);
}
.profile-info{flex:1;}
.profile-name{font-family:'Bebas Neue',sans-serif;font-size:36px;letter-spacing:3px;line-height:1;color:var(--ucl-white);}
.profile-cat{
  display:inline-block;background:rgba(68,114,196,.25);border:1px solid var(--ucl-light);
  color:var(--ucl-bright);font-size:11px;font-weight:700;letter-spacing:2px;
  padding:2px 10px;border-radius:3px;margin-top:5px;text-transform:uppercase;
}
.profile-stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(92px,1fr));gap:10px;margin-bottom:18px;}
.p-stat{
  background:linear-gradient(135deg,rgba(27,58,107,.3),rgba(10,22,40,.8));
  border:1px solid var(--ucl-border);border-radius:8px;padding:12px;text-align:center;
}
.p-stat-val{font-family:'Bebas Neue',sans-serif;font-size:28px;line-height:1;}
.p-stat-lbl{font-size:9px;color:#4472C4;letter-spacing:2px;text-transform:uppercase;margin-top:3px;}

/* PROMO */
.promo-tracker{
  background:linear-gradient(135deg,rgba(0,100,50,.2),rgba(10,22,40,.9));
  border:1px solid rgba(0,200,80,.3);border-radius:10px;padding:16px;margin-top:16px;
}
.promo-title{font-size:11px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:#00E676;margin-bottom:8px;}
.promo-bar-wrap{background:rgba(255,255,255,.07);border-radius:8px;height:10px;margin-bottom:6px;overflow:hidden;}
.promo-bar-fill{height:100%;background:linear-gradient(90deg,#00A550,#00E676);border-radius:8px;transition:width .5s;}
.promo-label{font-size:12px;color:#82B1FF;display:flex;justify-content:space-between;}
.promo-cycle-info{font-size:11px;color:#FFEA00;margin-top:6px;font-weight:700;}

/* ACHIEVEMENT BADGES - tiered visual style */
.badges-row{display:flex;flex-wrap:wrap;gap:6px;margin-top:10px;}
.player-badge{display:inline-flex;align-items:center;gap:5px;padding:5px 11px;border-radius:5px;font-size:10px;font-weight:700;letter-spacing:1px;text-transform:uppercase;border:1px solid;position:relative;}
.badge-gold{background:rgba(255,215,0,.18);color:#FFD700;border-color:rgba(255,215,0,.45);box-shadow:0 0 8px rgba(255,215,0,.15);}
.badge-silver{background:rgba(192,192,192,.14);color:#C0C0C0;border-color:rgba(192,192,192,.4);}
.badge-green{background:rgba(0,230,118,.14);color:#00E676;border-color:rgba(0,230,118,.38);}
.badge-blue{background:rgba(68,114,196,.16);color:#82B1FF;border-color:rgba(68,114,196,.42);}
.badge-purple{background:rgba(206,147,216,.14);color:#CE93D8;border-color:rgba(206,147,216,.38);}
.badge-red{background:rgba(255,61,61,.14);color:#FF5555;border-color:rgba(255,61,61,.38);}
.badge-star{background:rgba(245,197,24,.16);color:var(--ucl-star);border-color:rgba(245,197,24,.42);box-shadow:0 0 10px rgba(245,197,24,.18);}
.badge-diamond{background:linear-gradient(135deg,rgba(68,114,196,.2),rgba(206,147,216,.2));color:#A8D8FF;border-color:rgba(150,180,255,.5);box-shadow:0 0 12px rgba(100,150,255,.2);}
.badge-icon{font-size:13px;}
.cat-main{color:#FF6B6B;font-weight:700;}
.cat-youth{color:#82B1FF;font-weight:700;}
.cat-academy{color:#A5D6A7;font-weight:700;}

/* ADMIN */
.admin-tabs{display:flex;gap:4px;flex-wrap:wrap;margin-bottom:18px;border-bottom:1px solid var(--ucl-border);padding-bottom:10px;}
.admin-tab{background:none;border:1px solid transparent;color:var(--ucl-silver);padding:7px 13px;font-family:'Montserrat',sans-serif;font-weight:600;font-size:11px;cursor:pointer;border-radius:5px;transition:all .2s;text-transform:uppercase;letter-spacing:1px;}
.admin-tab.active{background:linear-gradient(135deg,var(--ucl-mid),var(--ucl-light));color:white;border-color:var(--ucl-light);}
.admin-tab:hover:not(.active){border-color:var(--ucl-light);color:white;}

/* MOD INFO */
.mod-info-box{background:rgba(68,114,196,.1);border:1px solid rgba(68,114,196,.3);border-radius:8px;padding:14px;margin-bottom:16px;}
.mod-info-title{font-family:'Bebas Neue',sans-serif;font-size:20px;letter-spacing:2px;color:#82B1FF;margin-bottom:5px;}

/* RANKING CARD */
.rc-card{width:820px;background:#060E1C;border:2px solid #1B3A6B;border-radius:14px;overflow:hidden;font-family:'Montserrat',sans-serif;}
.rc-header{background:linear-gradient(135deg,#0A1E3C 0%,#1B3A6B 40%,#0A1E3C 100%);padding:22px 28px 18px;position:relative;overflow:hidden;}
.rc-header::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;background:linear-gradient(90deg,transparent,#F5C518,#4472C4,#F5C518,transparent);}
.rc-header::after{content:'UCL';position:absolute;right:-15px;bottom:-25px;font-family:'Bebas Neue',sans-serif;font-size:100px;color:rgba(68,114,196,0.07);pointer-events:none;}
.rc-header-top{display:flex;align-items:center;justify-content:space-between;}
.rc-title{font-family:'Bebas Neue',sans-serif;font-size:30px;letter-spacing:5px;color:white;}
.rc-subtitle{font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:3px;color:rgba(255,255,255,0.6);margin-top:3px;}
.rc-period{background:rgba(245,197,24,.15);border:1px solid rgba(245,197,24,.4);border-radius:5px;padding:5px 14px;font-size:12px;font-weight:700;letter-spacing:2px;color:#F5C518;text-transform:uppercase;}
.rc-body{padding:0;background:#060E1C;}
.rc-row{display:grid;grid-template-columns:48px 1fr 90px 110px 80px 70px;align-items:center;padding:12px 28px;border-bottom:1px solid rgba(27,58,107,0.5);gap:8px;}
.rc-row:last-child{border-bottom:none;}
.rc-header-row{background:#0D1E3A !important;padding:9px 28px;border-bottom:2px solid rgba(68,114,196,0.4);}
.rc-header-row span{font-size:9px;letter-spacing:2px;text-transform:uppercase;color:#4472C4;font-weight:700;}
.rc-row.rank-1-row{background:linear-gradient(90deg,rgba(255,215,0,.08),transparent);}
.rc-row.rank-2-row{background:linear-gradient(90deg,rgba(192,192,192,.06),transparent);}
.rc-row.rank-3-row{background:linear-gradient(90deg,rgba(205,127,50,.06),transparent);}
.rc-rank{font-family:'Bebas Neue',sans-serif;font-size:28px;color:#1B3A6B;}
.rc-rank.r1{color:#FFD700;}.rc-rank.r2{color:#C0C0C0;}.rc-rank.r3{color:#CD7F32;}
.rc-player-info{display:flex;align-items:center;gap:10px;}
.rc-avatar{width:30px;height:30px;border-radius:50%;background:linear-gradient(135deg,#1B3A6B,#4472C4);display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:13px;color:white;flex-shrink:0;}
.rc-name{font-family:'Bebas Neue',sans-serif;font-size:17px;letter-spacing:1px;color:#D0E4FF;}
.rc-div-small{font-size:9px;color:#4472C4;letter-spacing:1px;font-weight:600;}
.rc-rating{font-family:'Bebas Neue',sans-serif;font-size:22px;color:#F5C518;text-align:right;}
.rc-wdl-nums{font-family:'Bebas Neue',sans-serif;font-size:14px;display:flex;gap:6px;}
.rc-w{color:#00E676;}.rc-d{color:#FFEA00;}.rc-l{color:#FF5555;}
.rc-winpct{font-family:'Bebas Neue',sans-serif;font-size:18px;color:#4472C4;text-align:right;}
.rc-footer{background:#040A14;padding:10px 28px;display:flex;justify-content:space-between;align-items:center;border-top:1px solid rgba(27,58,107,.4);}
.rc-footer-brand{font-family:'Bebas Neue',sans-serif;font-size:14px;letter-spacing:4px;color:#1B3A6B;}
.rc-footer-date{font-size:10px;color:#1B3A6B;letter-spacing:2px;}

/* RANKING PREVIEW */
.ranking-card-preview{display:none;position:fixed;inset:0;background:rgba(0,0,0,.93);z-index:3000;align-items:center;justify-content:center;flex-direction:column;gap:18px;padding:20px;overflow:auto;}
.ranking-card-preview.open{display:flex;}
.ranking-card-close{position:absolute;top:16px;right:16px;background:rgba(27,58,107,.4);border:1px solid var(--ucl-light);color:white;width:34px;height:34px;border-radius:50%;font-size:16px;cursor:pointer;display:flex;align-items:center;justify-content:center;}

/* MOBILE NAV */
.mobile-nav{display:none;position:fixed;bottom:0;left:0;right:0;background:rgba(6,14,28,.98);border-top:1px solid var(--ucl-border);z-index:999;padding:6px 0;}
.mobile-nav-inner{display:flex;justify-content:space-around;}
.mob-nav-btn{display:flex;flex-direction:column;align-items:center;gap:2px;background:none;border:none;color:#4472C4;font-family:'Montserrat',sans-serif;font-size:10px;font-weight:600;padding:4px 10px;cursor:pointer;transition:color .2s;text-transform:uppercase;}
.mob-nav-btn.active,.mob-nav-btn:hover{color:var(--ucl-star);}
.mob-nav-icon{font-size:19px;}
@media(max-width:768px){.mobile-nav{display:block;}main{padding-bottom:72px;}}

/* MISC */
.loading-spinner{display:flex;align-items:center;justify-content:center;padding:48px;gap:12px;color:#4472C4;}
.spinner{width:26px;height:26px;border:2px solid rgba(68,114,196,0.2);border-top-color:var(--ucl-light);border-radius:50%;animation:spin .7s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}
.empty-state{text-align:center;padding:48px 20px;color:#4472C4;}
.empty-icon{font-size:44px;margin-bottom:12px;}
.empty-text{font-size:17px;font-weight:700;color:#82B1FF;}
.empty-sub{font-size:13px;margin-top:5px;opacity:.6;}
.text-gold{color:var(--gold);}.text-green{color:#00E676;}.text-red{color:#FF5555;}.text-yellow{color:#FFEA00;}.text-blue{color:#82B1FF;}.text-gray{color:#4472C4;}.text-sm{font-size:13px;}.font-bold{font-weight:700;}
.mt-8{margin-top:8px;}.mt-12{margin-top:12px;}.mt-16{margin-top:16px;}.mb-8{margin-bottom:8px;}.mb-16{margin-bottom:16px;}
</style>
</head>
<body>

<header>
  <div class="header-inner">
    <div class="logo-area" onclick="navTo('home')">
      <div class="logo-badge">LLFC</div>
      <div class="logo-text">
        <span class="logo-main">LLFC</span>
        <span class="logo-sub">eFootball Division</span>
      </div>
    </div>
    <nav class="header-nav">
      <button class="nav-btn active" id="navHome" onclick="navTo('home');setNavActive(this)">Home</button>
      <button class="nav-btn" id="navLeaderboard" onclick="navTo('leaderboard');setNavActive(this)">Rankings</button>
      <button class="nav-btn" id="navMatches" onclick="navTo('matches');setNavActive(this)">Matches</button>
      <button class="nav-btn" id="navSubmit" onclick="navTo('submit');setNavActive(this)">Submit</button>
    </nav>
    <div class="header-auth" id="headerAuth">
      <button class="btn-login" onclick="openModal('loginModal')">Login</button>
      <button class="btn-register" onclick="openModal('registerModal')">Register</button>
      <button class="btn-login" style="border-color:var(--ucl-star);color:var(--ucl-star);font-size:11px" onclick="navTo('admin')">Admin</button>
    </div>
  </div>
</header>

<main>

<!-- HOME -->
<div class="page active" id="page-home">
  <div class="news-ticker" id="newsTicker" style="display:none">
    <div class="news-label">BREAKING</div>
    <div class="news-scroll-wrap"><span class="news-scroll-text" id="newsText"></span></div>
  </div>
  <div class="hero">
    <div class="hero-tag">Season Active</div>
    <h1>LLFC <span>eFootball</span> Division</h1>
    <p>Play freely. Submit results. Climb the ranks. From Division 9 to Division 1 — prove yourself on the pitch.</p>
    <div class="hero-actions">
      <button class="btn-primary" onclick="navTo('leaderboard')">View Rankings</button>
      <button class="btn-secondary" onclick="navTo('submit')">Submit Result</button>
    </div>
  </div>
  <div class="stats-grid">
    <div class="stat-card"><div class="stat-num" id="statPlayers">-</div><div class="stat-label">Active Players</div></div>
    <div class="stat-card"><div class="stat-num" id="statMatches">-</div><div class="stat-label">Total Matches</div></div>
    <div class="stat-card"><div class="stat-num" id="statToday">-</div><div class="stat-label">Today</div></div>
    <div class="stat-card"><div class="stat-num" id="statPending">-</div><div class="stat-label">Pending</div></div>
  </div>
  <div class="two-col">
    <div>
      <div class="section-title">Top Players</div>
      <div id="homeTopPlayers"><div class="loading-spinner"><div class="spinner"></div></div></div>
    </div>
    <div>
      <div class="section-title">Recent Matches</div>
      <div id="homeRecentMatches"><div class="loading-spinner"><div class="spinner"></div></div></div>
    </div>
  </div>
  <div class="mt-16">
    <div class="section-title">Division Structure</div>
    <div class="three-col" id="divisionGuide"></div>
  </div>
</div>

<!-- LEADERBOARD -->
<div class="page" id="page-leaderboard">
  <div style="display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:12px;margin-bottom:18px">
    <div class="section-title" style="margin-bottom:0;flex:1">Rankings</div>
    <button class="btn-primary" style="padding:9px 18px;font-size:11px;flex-shrink:0" onclick="openRankingCardPreview()">Download Ranking Card (JPG)</button>
  </div>
  <div class="lb-tabs">
    <button class="lb-tab active" onclick="switchLbTab('overall',this)">Overall</button>
    <button class="lb-tab" onclick="switchLbTab('season',this)">Season</button>
    <button class="lb-tab" onclick="switchLbTab('monthly',this)">Monthly</button>
    <button class="lb-tab" onclick="switchLbTab('weekly',this)">Weekly</button>
    <button class="lb-tab" onclick="switchLbTab('daily',this)">Daily</button>
  </div>
  <div class="search-bar">
    <input class="search-input" placeholder="Search player..." id="lbSearch" oninput="filterLeaderboard()">
    <select class="form-select-sm" id="lbSeasonFilter" onchange="filterLeaderboard()" style="display:none">
      <option value="">All Seasons</option>
    </select>
    <select class="form-select-sm" id="lbDivFilter" onchange="filterLeaderboard()">
      <option value="">All Divs</option>
      <option value="1">Div 1</option><option value="2">Div 2</option><option value="3">Div 3</option>
      <option value="4">Div 4</option><option value="5">Div 5</option><option value="6">Div 6</option>
      <option value="7">Div 7</option><option value="8">Div 8</option><option value="9">Div 9</option>
    </select>
  </div>
  <div class="lb-table-wrap">
    <table>
      <thead>
        <tr>
          <th>#</th><th>Player</th><th>Div</th><th>Rating</th>
          <th>W / D / L</th><th>MP</th><th>Win%</th><th>GD</th><th>CS</th><th>Form</th><th>Cycle</th>
        </tr>
      </thead>
      <tbody id="lbTableBody">
        <tr><td colspan="11" style="text-align:center;padding:30px"><div class="spinner" style="margin:0 auto"></div></td></tr>
      </tbody>
    </table>
  </div>
</div>

<!-- MATCHES -->
<div class="page" id="page-matches">
  <div class="section-title">Match History</div>
  <div class="search-bar">
    <input class="search-input" placeholder="Search player..." id="matchSearch" oninput="filterMatches()">
    <select class="form-select-sm" id="matchStatusFilter" onchange="filterMatches()">
      <option value="">All</option><option value="confirmed">Confirmed</option>
      <option value="pending">Pending</option><option value="disputed">Disputed</option>
    </select>
  </div>
  <div id="matchesList"><div class="loading-spinner"><div class="spinner"></div></div></div>
  <div id="pendingConfirmSection" style="display:none">
    <div class="section-title mt-16">Awaiting Your Confirmation</div>
    <div id="pendingConfirmList"></div>
  </div>
</div>

<!-- SUBMIT -->
<div class="page" id="page-submit">
  <div class="section-title">Submit Match Result</div>
  <div id="submitRequireLogin" style="display:none">
    <div class="empty-state">
      <div class="empty-icon">&#128274;</div>
      <div class="empty-text">Login Required</div>
      <div class="empty-sub">Please login to submit match results</div>
      <button class="btn-primary mt-12" onclick="openModal('loginModal')">Login Now</button>
    </div>
  </div>
  <div id="submitForm" style="display:none">
    <div class="card card-blue" style="max-width:540px;margin:0 auto">
      <div class="match-form">
        <div class="form-group"><label class="form-label">Your Name</label><input class="form-input" id="submitMyName" readonly></div>
        <div class="form-group"><label class="form-label">Opponent</label>
          <select class="form-select" id="submitOpponent"><option value="">-- Select Opponent --</option></select>
        </div>
        <div class="form-group">
          <label class="form-label">Score</label>
          <div class="score-row">
            <input class="form-input score-input" type="number" min="0" max="99" id="scoreA" placeholder="0">
            <div class="score-vs">VS</div>
            <input class="form-input score-input" type="number" min="0" max="99" id="scoreB" placeholder="0">
          </div>
        </div>
        <div class="form-group"><label class="form-label">Match Date</label><input class="form-input" type="date" id="matchDate"></div>
        <button class="btn-primary w-full" onclick="submitMatchResult()">Submit Result</button>
        <p class="text-gray text-sm" style="text-align:center;margin-top:8px">Opponent must confirm. Multiple pending matches allowed.</p>
      </div>
    </div>
  </div>
</div>

<!-- PROFILE -->
<div class="page" id="page-profile">
  <button class="btn-secondary mb-16" onclick="navBack()">&#8592; Back</button>
  <div id="profileContent"><div class="loading-spinner"><div class="spinner"></div></div></div>
</div>

<!-- MY PROFILE -->
<div class="page" id="page-myprofile">
  <div class="section-title">My Profile</div>
  <div id="myProfileContent"><div class="loading-spinner"><div class="spinner"></div></div></div>
</div>

<!-- ADMIN -->
<div class="page" id="page-admin">
  <div class="section-title">Admin Panel</div>
  <div id="adminLoginWrap">
    <div class="card" style="max-width:340px;margin:0 auto">
      <div class="modal-title">Admin Access</div>
      <div class="match-form">
        <div class="form-group"><label class="form-label">Password</label>
          <input class="form-input" type="password" id="adminPwInput" placeholder="Enter admin password" onkeydown="if(event.key==='Enter')adminLogin()">
        </div>
        <button class="btn-primary w-full" onclick="adminLogin()">Enter Panel</button>
      </div>
    </div>
  </div>
  <div id="adminPanelWrap" style="display:none">
    <div class="admin-tabs">
      <button class="admin-tab active" onclick="switchAdminTab('pending',this)">Pending</button>
      <button class="admin-tab" onclick="switchAdminTab('players',this)">Players</button>
      <button class="admin-tab" onclick="switchAdminTab('adminMatches',this)">Matches</button>
      <button class="admin-tab" onclick="switchAdminTab('moderators',this)">Moderators</button>
      <button class="admin-tab" onclick="switchAdminTab('season',this)">Season</button>
      <button class="admin-tab" onclick="switchAdminTab('adminSettings',this)">Settings</button>
    </div>
    <div id="adminTab-pending">
      <div class="section-title">Pending Registrations</div>
      <div id="adminPendingList"><div class="loading-spinner"><div class="spinner"></div></div></div>
    </div>
    <div id="adminTab-players" style="display:none">
      <div class="section-title">All Players</div>
      <div class="search-bar"><input class="search-input" placeholder="Search..." id="adminPlayerSearch" oninput="filterAdminPlayers()"></div>
      <div id="adminPlayersList"></div>
    </div>
    <div id="adminTab-adminMatches" style="display:none">
      <div class="section-title">All Matches</div>
      <div id="adminMatchesList"></div>
    </div>
    <div id="adminTab-moderators" style="display:none">
      <div class="section-title">Moderator Management</div>
      <div class="mod-info-box">
        <div class="mod-info-title">About Moderators</div>
        <p class="text-gray text-sm">Moderators can approve or dispute any pending match result. They cannot edit players or change admin settings.</p>
      </div>
      <div class="search-bar"><input class="search-input" placeholder="Search player..." id="modPlayerSearch" oninput="filterModPlayers()"></div>
      <div id="modPlayersList"></div>
    </div>
    <div id="adminTab-season" style="display:none">
      <div class="section-title">Season Management</div>

      <!-- Active Season Config -->
      <div class="card card-blue" style="max-width:540px;margin-bottom:20px">
        <div style="font-family:'Bebas Neue',sans-serif;font-size:18px;letter-spacing:2px;color:var(--ucl-star);margin-bottom:14px">Active Season Settings</div>
        <div class="match-form">
          <div class="form-group"><label class="form-label">Season Name (e.g. Season 1)</label><input class="form-input" id="seasonName" placeholder="Season 1"></div>
          <div class="form-group"><label class="form-label">Season Start Date</label><input class="form-input" type="date" id="seasonStart"></div>
          <div class="form-group"><label class="form-label">Season End Date</label><input class="form-input" type="date" id="seasonEnd"></div>
          <button class="btn-primary" onclick="saveSeasonSettings()">Save Season Settings</button>
        </div>
        <div id="currentSeasonInfo" style="margin-top:14px;padding-top:14px;border-top:1px solid var(--ucl-border);font-size:13px;color:#82B1FF"></div>
      </div>

      <!-- Award daily/weekly/monthly winners -->
      <div class="card" style="max-width:540px;margin-bottom:20px">
        <div style="font-family:'Bebas Neue',sans-serif;font-size:18px;letter-spacing:2px;color:#00E676;margin-bottom:14px">Award Badges</div>
        <p class="text-gray text-sm mb-8">Auto-award POTD/POTW/POTM/Most Active to the current leaderboard top performers.</p>
        <div style="display:flex;gap:8px;flex-wrap:wrap">
          <button class="btn-sm btn-approve" onclick="autoAwardPOTD()">Auto POTD</button>
          <button class="btn-sm btn-edit" onclick="autoAwardPOTW()">Auto POTW</button>
          <button class="btn-sm btn-mod" onclick="autoAwardPOTM()">Auto POTM</button>
          <button class="btn-sm btn-ban" onclick="autoAwardPOTS()">Auto POTS</button>
          <button class="btn-sm btn-approve" onclick="autoAwardMostActive()">Auto Most Active</button>
        </div>
        <div id="awardResult" style="margin-top:12px;font-size:12px;color:#82B1FF"></div>
      </div>

      <!-- Past Seasons -->
      <div class="card" style="max-width:540px;margin-bottom:20px">
        <div style="font-family:'Bebas Neue',sans-serif;font-size:18px;letter-spacing:2px;color:#82B1FF;margin-bottom:14px">Past Seasons</div>
        <div id="pastSeasonsList"><div class="loading-spinner" style="padding:16px"><div class="spinner"></div></div></div>
      </div>

      <!-- End Season -->
      <div class="card" style="max-width:540px">
        <div style="font-family:'Bebas Neue',sans-serif;font-size:18px;letter-spacing:2px;color:#FF5555;margin-bottom:10px">End Season</div>
        <p class="text-sm mb-16" style="color:#FF8888">Ends current season, archives all stats, resets player cycle data. Players keep their division.</p>
        <div style="display:flex;gap:10px;flex-wrap:wrap">
          <button class="btn-reject btn-sm" style="padding:10px 24px;font-size:13px" onclick="endCurrentSeason()">End &amp; Archive Season</button>
          <button class="btn-reject btn-sm" style="padding:10px 24px;font-size:13px;background:rgba(100,0,0,.3)" onclick="confirmSeasonReset()">Full Reset (Danger)</button>
        </div>
      </div>
    </div>
    <div id="adminTab-adminSettings" style="display:none">
      <div class="section-title">Settings</div>
      <div class="card" style="max-width:400px">
        <div class="match-form">
          <div class="form-group"><label class="form-label">New Admin Password</label><input class="form-input" type="password" id="newAdminPw"></div>
          <div class="form-group"><label class="form-label">Confirm Password</label><input class="form-input" type="password" id="confirmAdminPw"></div>
          <button class="btn-primary" onclick="changeAdminPassword()">Update Password</button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- MOD PANEL -->
<div class="page" id="page-modpanel">
  <div class="section-title">Moderator Panel</div>
  <div class="mod-info-box">
    <div class="mod-info-title">Moderator Access</div>
    <p class="text-gray text-sm">Approve or dispute any pending match result below.</p>
  </div>
  <div id="modPendingMatches"><div class="loading-spinner"><div class="spinner"></div></div></div>
</div>

</main>

<nav class="mobile-nav">
  <div class="mobile-nav-inner">
    <button class="mob-nav-btn active" onclick="navTo('home');setMobActive(this)"><span class="mob-nav-icon">&#127968;</span>Home</button>
    <button class="mob-nav-btn" onclick="navTo('leaderboard');setMobActive(this)"><span class="mob-nav-icon">&#127942;</span>Ranks</button>
    <button class="mob-nav-btn" onclick="navTo('matches');setMobActive(this)"><span class="mob-nav-icon">&#9917;</span>Matches</button>
    <button class="mob-nav-btn" onclick="navTo('submit');setMobActive(this)"><span class="mob-nav-icon">&#128203;</span>Submit</button>
    <button class="mob-nav-btn" onclick="navTo('myprofile');setMobActive(this)"><span class="mob-nav-icon">&#128100;</span>Me</button>
  </div>
</nav>

<!-- RANKING CARD PREVIEW -->
<div class="ranking-card-preview" id="rankingCardPreview">
  <button class="ranking-card-close" onclick="closeRankingPreview()">X</button>
  <div id="rcCardContainer" style="overflow:auto;max-width:100%"></div>
  <div style="display:flex;gap:10px;flex-wrap:wrap;justify-content:center">
    <button class="btn-primary" onclick="downloadRankingCard()">Download JPG</button>
    <button class="btn-secondary" onclick="closeRankingPreview()">Close</button>
  </div>
</div>

<!-- MODALS -->
<div class="modal-overlay" id="loginModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('loginModal')">X</button>
    <div class="modal-title">Player Login</div>
    <div class="match-form">
      <div class="form-group"><label class="form-label">Name</label><input class="form-input" id="loginName" placeholder="Your registered name"></div>
      <div class="form-group"><label class="form-label">Password</label><input class="form-input" type="password" id="loginPw" onkeydown="if(event.key==='Enter')doLogin()"></div>
      <button class="btn-primary w-full" onclick="doLogin()">Login</button>
      <p class="text-gray text-sm" style="text-align:center;margin-top:8px">No account? <span style="color:var(--ucl-star);cursor:pointer" onclick="closeModal('loginModal');openModal('registerModal')">Register</span></p>
    </div>
  </div>
</div>

<div class="modal-overlay" id="registerModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('registerModal')">X</button>
    <div class="modal-title">Register</div>
    <div class="match-form">
      <div class="form-group"><label class="form-label">Full Name</label><input class="form-input" id="regName" placeholder="Your name"></div>
      <div class="form-group"><label class="form-label">Category</label>
        <select class="form-select" id="regCategory">
          <option value="Main">Main Team</option>
          <option value="Youth">Youth</option>
          <option value="Academy">Academy</option>
        </select>
      </div>
      <div class="form-group"><label class="form-label">Password</label><input class="form-input" type="password" id="regPw"></div>
      <div class="form-group"><label class="form-label">Confirm Password</label><input class="form-input" type="password" id="regPwConfirm"></div>
      <button class="btn-primary w-full" onclick="doRegister()">Register</button>
      <p class="text-gray text-sm" style="text-align:center;margin-top:8px">Requires admin approval before playing.</p>
    </div>
  </div>
</div>

<div class="modal-overlay" id="changePwModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('changePwModal')">X</button>
    <div class="modal-title">Change Password</div>
    <div class="match-form">
      <div class="form-group"><label class="form-label">Current Password</label><input class="form-input" type="password" id="cpOld"></div>
      <div class="form-group"><label class="form-label">New Password</label><input class="form-input" type="password" id="cpNew"></div>
      <div class="form-group"><label class="form-label">Confirm New</label><input class="form-input" type="password" id="cpConfirm"></div>
      <button class="btn-primary w-full" onclick="changeMyPassword()">Update Password</button>
    </div>
  </div>
</div>

<div class="modal-overlay" id="editPlayerModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('editPlayerModal')">X</button>
    <div class="modal-title">Edit Player</div>
    <div class="match-form">
      <input type="hidden" id="editPlayerId">
      <div class="form-group"><label class="form-label">Player Name</label><input class="form-input" id="editPlayerName" placeholder="Player name"></div>
      <div class="form-group"><label class="form-label">Division (1-9)</label><input class="form-input" type="number" min="1" max="9" id="editDivision"></div>
      <div class="form-group"><label class="form-label">Category</label>
        <select class="form-select" id="editCategory">
          <option value="Main">Main Team</option>
          <option value="Youth">Youth</option>
          <option value="Academy">Academy</option>
        </select>
      </div>
      <div class="form-group"><label class="form-label">Wins</label><input class="form-input" type="number" id="editWins"></div>
      <div class="form-group"><label class="form-label">Draws</label><input class="form-input" type="number" id="editDraws"></div>
      <div class="form-group"><label class="form-label">Losses</label><input class="form-input" type="number" id="editLosses"></div>
      <div class="form-group"><label class="form-label">Goals For</label><input class="form-input" type="number" id="editGF"></div>
      <div class="form-group"><label class="form-label">Goals Against</label><input class="form-input" type="number" id="editGA"></div>
      <div class="form-group"><label class="form-label">Clean Sheets</label><input class="form-input" type="number" id="editCS"></div>
      <div class="form-group"><label class="form-label">Cycle MP</label><input class="form-input" type="number" id="editCycleMP"></div>
      <div class="form-group"><label class="form-label">Cycle Points</label><input class="form-input" type="number" id="editCyclePts"></div>
      <div class="form-group"><label class="form-label">Status</label>
        <select class="form-select" id="editStatus">
          <option value="active">Active</option><option value="banned">Banned</option><option value="pending">Pending</option>
        </select>
      </div>
      <div class="form-group"><label class="form-label">Reset Password (leave blank to keep current)</label><input class="form-input" type="text" id="editPlayerPw" placeholder="New password (optional)"></div>
      <button class="btn-primary w-full" onclick="savePlayerEdit()">Save Changes</button>
    </div>
  </div>
</div>

<div class="modal-overlay" id="editMatchModal">
  <div class="modal">
    <button class="modal-close" onclick="closeModal('editMatchModal')">X</button>
    <div class="modal-title">Edit Match</div>
    <div class="match-form">
      <input type="hidden" id="editMatchId">
      <div id="editMatchInfo" class="text-gray text-sm mb-8"></div>
      <div class="form-group"><label class="form-label">Score - Player A</label><input class="form-input" type="number" min="0" id="editScoreA"></div>
      <div class="form-group"><label class="form-label">Score - Player B</label><input class="form-input" type="number" min="0" id="editScoreB"></div>
      <div class="form-group"><label class="form-label">Status</label>
        <select class="form-select" id="editMatchStatus">
          <option value="confirmed">Confirmed</option><option value="pending">Pending</option><option value="disputed">Disputed</option>
        </select>
      </div>
      <button class="btn-primary w-full" onclick="saveMatchEdit()">Save</button>
      <button class="btn-reject btn-sm w-full mt-8" onclick="adminDeleteMatch()">Delete Match</button>
    </div>
  </div>
</div>

<div class="toast" id="toast"></div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import {
  getFirestore,collection,doc,getDoc,getDocs,addDoc,setDoc,
  updateDoc,deleteDoc,query,where,orderBy,limit,serverTimestamp
} from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

const app = initializeApp({
  apiKey:"AIzaSyCsZrHcpJgGoTHeW0Ex4Hv20KLtDopPq4",
  authDomain:"llfc-4d2df.firebaseapp.com",projectId:"llfc-4d2df",
  storageBucket:"llfc-4d2df.firebasestorage.app",
  messagingSenderId:"697058785471",appId:"1:697058785471:web:7481cae8fe6b682d762e0a"
});
const db = getFirestore(app);

// ===== DIVISION RULES =====
// Div 9-4: cycle-based point system (10 matches per cycle)
// Div 3-1: ELO-style rating system (starts at 1200, promoted at 1500->Div2, 1800->Div1)
const DIV_RULES = {
  9:{cycle:10,promo:9, relo:0, next:8,name:'Rookie',      useRating:false},
  8:{cycle:10,promo:11,relo:2, next:7,name:'Amateur',     useRating:false},
  7:{cycle:10,promo:13,relo:3, next:6,name:'Regional',    useRating:false},
  6:{cycle:10,promo:15,relo:4, next:5,name:'National',    useRating:false},
  5:{cycle:10,promo:16,relo:5, next:4,name:'League Two',  useRating:false},
  4:{cycle:10,promo:18,relo:6, next:3,name:'League One',  useRating:false},
  3:{useRating:true, name:'Championship', ratingFloor:1200},
  2:{useRating:true, name:'Premier',      ratingFloor:1200},
  1:{useRating:true, name:'Elite',        ratingFloor:1200},
};
// Rating thresholds for Div 3+ system
const RATING_PROMO = {3:1500, 2:1800}; // rating needed to promote
const RATING_RELO  = {2:1200, 1:1200}; // rating below which relegated (back to Div 3 floor)
const DEFAULT_DIV3_RATING = 1200;

// ===== STATE =====
let S={
  user:null,lbTab:'overall',players:[],matches:[],
  lbPlayers:[],allMatchesData:[],adminPlayers:[],
  pageHistory:['home'],adminPw:'fardous'
};

// ===== UTILS =====
const $=id=>document.getElementById(id);
function T(msg,type='info'){
  const t=$('toast');t.textContent=msg;t.className=`toast show ${type}`;
  clearTimeout(window._tt);window._tt=setTimeout(()=>t.classList.remove('show'),3500);
}
function openModal(id){$(id).classList.add('open');}
function closeModal(id){$(id).classList.remove('open');}

function showPage(pg){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  const el=$('page-'+pg);if(el)el.classList.add('active');
}
function navTo(pg){
  S.pageHistory.push(pg);showPage(pg);
  const m={home:'navHome',leaderboard:'navLeaderboard',matches:'navMatches',submit:'navSubmit'};
  document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
  if(m[pg])$(m[pg])?.classList.add('active');
  if(pg==='home')loadHome();
  else if(pg==='leaderboard')loadLeaderboard(S.lbTab);
  else if(pg==='matches')loadMatches();
  else if(pg==='submit')loadSubmitPage();
  else if(pg==='myprofile')loadMyProfile();
  else if(pg==='modpanel')loadModPanel();
}
function navBack(){S.pageHistory.pop();const p=S.pageHistory[S.pageHistory.length-1]||'home';showPage(p);}
function setNavActive(b){document.querySelectorAll('.nav-btn').forEach(x=>x.classList.remove('active'));b.classList.add('active');}
function setMobActive(b){document.querySelectorAll('.mob-nav-btn').forEach(x=>x.classList.remove('active'));b.classList.add('active');}

function divBadge(d){return`<div class="div-badge div-${d||9}">${d||9}</div>`;}
function formBadge(r){const c=r==='W'?'form-w':r==='D'?'form-d':'form-l';return`<div class="form-dot ${c}"></div>`;}
function statusBadge(s){return`<span class="status-badge status-${s}">${s}</span>`;}
function fmtDate(ts){
  if(!ts)return'';
  try{const d=ts.toDate?ts.toDate():new Date(ts);return d.toLocaleDateString('en-GB',{day:'2-digit',month:'short',year:'numeric'});}catch{return'';}
}
function timeAgo(ts){
  if(!ts)return'';
  try{
    const d=ts.toDate?ts.toDate():new Date(ts),diff=Date.now()-d.getTime(),m=Math.floor(diff/60000);
    if(m<1)return'just now';if(m<60)return m+'m ago';
    const h=Math.floor(m/60);if(h<24)return h+'h ago';return Math.floor(h/24)+'d ago';
  }catch{return'';}
}
function getRC(sA,sB,side){const my=side==='A'?sA:sB,op=side==='A'?sB:sA;return my>op?'W':my<op?'L':'D';}
function isHigh(sA,sB){return(sA+sB)>7;}
function catClass(c){return c==='Main'?'cat-main':c==='Youth'?'cat-youth':'cat-academy';}

// 2x RATING LOGIC
// If a non-Main (Youth/Academy) beats a Main player -> 2x rating gain
// If a Main player loses to a non-Main -> 2x rating loss
function getRatingMultiplier(myCategory, oppCategory, result) {
  const imNonMain = myCategory==='Youth'||myCategory==='Academy';
  const oppIsMain = oppCategory==='Main';
  const imMain = myCategory==='Main';
  const oppIsNonMain = oppCategory==='Youth'||oppCategory==='Academy';
  if(imNonMain && oppIsMain && result==='W') return 2;
  if(imMain && oppIsNonMain && result==='L') return 2;
  return 1;
}

// RATING = computed from match history (always fresh)
// W*10 + D*5 + L*(-5) + GD*1 + CS*2
// multiplier applied at match time is stored per match, but we recompute from stored aggregate stats
function calcRating(w,d,l,gf,ga,cs){
  return Math.max(0, w*10 + d*5 + l*(-5) + (gf-ga) + cs*2);
}

// ===== NEWS =====
function buildNews(matches){
  const hi=matches.filter(m=>m.status==='confirmed'&&isHigh(m.scoreA,m.scoreB));
  if(!hi.length){$('newsTicker').style.display='none';return;}
  $('newsText').textContent=hi.slice(0,8).map(m=>`GOAL FEST: ${m.playerAName} ${m.scoreA}-${m.scoreB} ${m.playerBName} (${m.scoreA+m.scoreB} goals!)`).join('     |     ');
  $('newsTicker').style.display='flex';
}

// ===== AUTH =====
async function doLogin(){
  const name=$('loginName').value.trim(),pw=$('loginPw').value;
  if(!name||!pw)return T('Fill in all fields','error');
  try{
    const snap=await getDocs(query(collection(db,'players'),where('name','==',name)));
    if(snap.empty)return T('Player not found','error');
    const d=snap.docs[0],p=d.data();
    if(p.password!==pw)return T('Wrong password','error');
    if(p.status==='pending')return T('Account pending admin approval','info');
    if(p.status==='banned')return T('Account banned. Contact admin.','error');
    S.user={id:d.id,...p};
    closeModal('loginModal');updateHeaderAuth();
    T('Welcome back, '+name+'!','success');
    loadSubmitPage();loadMatches();
  }catch(e){T('Login failed: '+e.message,'error');}
}

async function doRegister(){
  const name=$('regName').value.trim(),cat=$('regCategory').value;
  const pw=$('regPw').value,pw2=$('regPwConfirm').value;
  if(!name||!pw)return T('Fill in all fields','error');
  if(pw!==pw2)return T('Passwords do not match','error');
  if(pw.length<4)return T('Password too short','error');
  try{
    const ex=await getDocs(query(collection(db,'players'),where('name','==',name)));
    if(!ex.empty)return T('Name already taken','error');
    await addDoc(collection(db,'players'),{
      name,category:cat,password:pw,status:'pending',division:9,
      wins:0,draws:0,losses:0,goalsFor:0,goalsAgainst:0,cleanSheets:0,
      form:[],rivals:[],isModerator:false,highestDivision:9,
      cycleMP:0,cyclePts:0,eloRating:0,eloChange:0,
      isPOTD:false,isPOTW:false,isPOTM:false,isPOTS:false,
      createdAt:serverTimestamp()
    });
    closeModal('registerModal');
    T('Registration submitted! Awaiting admin approval','success');
    ['regName','regPw','regPwConfirm'].forEach(id=>$(id).value='');
  }catch(e){T('Registration failed: '+e.message,'error');}
}

function doLogout(){S.user=null;updateHeaderAuth();T('Logged out','info');navTo('home');}

function updateHeaderAuth(){
  const el=$('headerAuth');
  if(S.user){
    const isMod=S.user.isModerator;
    el.innerHTML=`
      <div class="user-pill" onclick="navTo('myprofile')">
        <div class="user-avatar">${S.user.name[0].toUpperCase()}</div>
        <span class="user-name">${S.user.name}</span>
        ${isMod?'<span class="mod-badge-hdr">MOD</span>':''}
      </div>
      ${isMod?`<button class="btn-login" style="border-color:#82B1FF;color:#82B1FF;font-size:11px" onclick="navTo('modpanel')">Mod Panel</button>`:''}
      <button class="btn-login" onclick="doLogout()">Logout</button>
      <button class="btn-login" style="border-color:var(--ucl-star);color:var(--ucl-star);font-size:11px" onclick="navTo('admin')">Admin</button>
    `;
  }else{
    el.innerHTML=`
      <button class="btn-login" onclick="openModal('loginModal')">Login</button>
      <button class="btn-register" onclick="openModal('registerModal')">Register</button>
      <button class="btn-login" style="border-color:var(--ucl-star);color:var(--ucl-star);font-size:11px" onclick="navTo('admin')">Admin</button>
    `;
  }
}

// ===== PASSWORD CHANGE =====
async function changeMyPassword(){
  if(!S.user)return;
  const oldPw=$('cpOld').value,newPw=$('cpNew').value,conf=$('cpConfirm').value;
  if(!oldPw||!newPw||!conf)return T('Fill in all fields','error');
  if(oldPw!==S.user.password)return T('Current password is wrong','error');
  if(newPw!==conf)return T('Passwords do not match','error');
  if(newPw.length<4)return T('Password too short','error');
  try{
    await updateDoc(doc(db,'players',S.user.id),{password:newPw});
    S.user.password=newPw;
    closeModal('changePwModal');
    T('Password updated successfully','success');
    ['cpOld','cpNew','cpConfirm'].forEach(id=>$(id).value='');
  }catch(e){T('Error: '+e.message,'error');}
}

// ===== HOME =====
async function loadHome(){
  try{
    const [pSnap,mSnap]=await Promise.all([
      getDocs(collection(db,'players')),
      getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(100)))
    ]);
    S.players=pSnap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
    S.matches=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    buildNews(S.matches);
    await loadSystemNews();
    const now=Date.now();
    $('statPlayers').textContent=S.players.length;
    $('statMatches').textContent=S.matches.filter(m=>m.status==='confirmed').length;
    $('statToday').textContent=S.matches.filter(m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<86400000).length;
    $('statPending').textContent=S.matches.filter(m=>m.status==='pending').length;

    const sorted=[...S.players].map(p=>{
      const div=p.division||9;
      const rules=DIV_RULES[div]||DIV_RULES[9];
      const rating=rules.useRating
        ? (p.eloRating||DEFAULT_DIV3_RATING)
        : calcRating(p.wins||0,p.draws||0,p.losses||0,p.goalsFor||0,p.goalsAgainst||0,p.cleanSheets||0);
      return {...p,rating};
    }).sort((a,b)=>b.rating-a.rating).slice(0,5);

    $('homeTopPlayers').innerHTML=sorted.length?sorted.map((p,i)=>`
      <div class="pending-item" style="cursor:pointer" onclick="viewProfile('${p.id}')">
        <span class="rank-num rank-${i+1}" style="font-size:22px;width:28px">${i+1}</span>
        ${divBadge(p.division)}
        <div class="pending-info">
          <div class="pending-name">${p.name} <span class="${catClass(p.category||'Main')}" style="font-size:11px">${p.category||'Main'}</span></div>
          <div class="pending-meta">${p.wins||0}W ${p.draws||0}D ${p.losses||0}L</div>
        </div>
        <span style="font-family:'Bebas Neue',sans-serif;font-size:22px;color:var(--ucl-star)">${p.rating}</span>
      </div>`).join(''):'<div class="empty-state"><div class="empty-text">No players yet</div></div>';

    const recent=S.matches.filter(m=>m.status==='confirmed').slice(0,6);
    $('homeRecentMatches').innerHTML=recent.length?recent.map(m=>{
      const hi=isHigh(m.scoreA,m.scoreB),x2=m.is2x;
      return `<div class="match-card${hi?' high-score':''}">
        <div class="match-info">
          <div class="match-vs">
            <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerAId}')">${m.playerAName}</span>
            <span class="text-gray"> vs </span>
            <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerBId}')">${m.playerBName}</span>
            ${hi?' <span class="high-score-badge">GOAL FEST</span>':''}
            ${x2?' <span class="x2-badge">2X RATING</span>':''}
          </div>
          <div class="match-meta">${fmtDate(m.createdAt)}</div>
        </div>
        <div class="match-score">${m.scoreA}-${m.scoreB}</div>
      </div>`;
    }).join(''):'<div class="empty-state"><div class="empty-text">No matches yet</div></div>';

    // Division Guide with corrected thresholds
    // Load season info for display
    let seasonName='Season', seasonRankHtml='';
    try{
      const ss=await getDoc(doc(db,'settings','season'));
      if(ss.exists()&&ss.data().name) seasonName=ss.data().name;

      // Compute seasonal rank (current season) for logged-in user
      if(S.user&&ss.exists()&&ss.data().startDate){
        const seasonStartMs=new Date(ss.data().startDate).getTime();
        const seasonEndMs=ss.data().endDate?new Date(ss.data().endDate).getTime():Date.now();
        const playerCatMap={};S.players.forEach(p=>playerCatMap[p.id]=p.category||'Main');
        const seasonMatches=S.matches.filter(m=>m.status==='confirmed'&&(()=>{const t=m.createdAt?.toDate?.()?.getTime()||0;return t>=seasonStartMs&&t<=seasonEndMs;})());

        const seasonRanked=S.players.map(p=>{
          const pm=seasonMatches.filter(m=>m.playerAId===p.id||m.playerBId===p.id);
          let w=0,d=0,l=0,gf=0,ga=0,cs=0;
          pm.forEach(m=>{
            const side=m.playerAId===p.id?'A':'B';
            const res=getRC(m.scoreA,m.scoreB,side);
            const myG=side==='A'?m.scoreA:m.scoreB,opG=side==='A'?m.scoreB:m.scoreA;
            const oppCat=playerCatMap[side==='A'?m.playerBId:m.playerAId]||'Main';
            const mult=getRatingMultiplier(p.category||'Main',oppCat,res);
            if(res==='W')w+=mult;else if(res==='D')d++;else l+=mult;
            gf+=myG;ga+=opG;if(opG===0)cs++;
          });
          const rating=Math.max(0,Math.round(w*10+d*5+l*(-5)+(gf-ga)+cs*2));
          return{id:p.id,rating};
        }).sort((a,b)=>b.rating-a.rating);

        const mySeasonRank=seasonRanked.findIndex(p=>p.id===S.user.id)+1;
        if(mySeasonRank>0){
          const badgeColor=mySeasonRank===1?'badge-star':mySeasonRank===2?'badge-silver':mySeasonRank===3?'badge-gold':mySeasonRank<=10?'badge-blue':'badge-green';
          const icon=mySeasonRank===1?'★':mySeasonRank===2?'◆':mySeasonRank===3?'◈':'#';
          seasonRankHtml=`
            <div style="margin-bottom:16px;background:linear-gradient(135deg,rgba(27,58,107,0.4),rgba(10,22,40,0.9));border:1px solid var(--ucl-border);border-radius:10px;padding:14px 18px;display:flex;align-items:center;gap:14px;flex-wrap:wrap">
              <div style="font-family:'Bebas Neue',sans-serif;font-size:40px;color:var(--ucl-star);line-height:1">#${mySeasonRank}</div>
              <div>
                <div style="font-family:'Bebas Neue',sans-serif;font-size:16px;letter-spacing:2px;color:#82B1FF">${seasonName} RANKING</div>
                <div style="font-size:12px;color:#4472C4">Your current season standing</div>
              </div>
              <span class="player-badge ${badgeColor}" style="margin-left:auto"><span class="badge-icon">${icon}</span>${seasonName} Rank #${mySeasonRank}</span>
            </div>`;
        }
      }
    }catch(e){console.error(e);}

    // Inject seasonal rank above division guide
    const divGuideEl=$('divisionGuide');
    if(divGuideEl&&seasonRankHtml){
      const wrapper=divGuideEl.parentElement;
      const existing=$('seasonRankBanner');
      if(existing)existing.remove();
      const banner=document.createElement('div');
      banner.id='seasonRankBanner';
      banner.innerHTML=seasonRankHtml;
      wrapper.insertBefore(banner,divGuideEl);
    }

    const divInfo=[
      {d:9,name:'Rookie',     promo:'9 pts in 10 matches',   relo:'No relegation — entry level',      tier:'low'},
      {d:8,name:'Amateur',    promo:'11 pts in 10 matches',  relo:'Relegated if ≤2 pts in cycle',    tier:'low'},
      {d:7,name:'Regional',   promo:'13 pts in 10 matches',  relo:'Relegated if ≤3 pts in cycle',    tier:'low'},
      {d:6,name:'National',   promo:'15 pts in 10 matches',  relo:'Relegated if ≤4 pts in cycle',    tier:'low'},
      {d:5,name:'League Two', promo:'16 pts in 10 matches',  relo:'Relegated if ≤5 pts in cycle',    tier:'low'},
      {d:4,name:'League One', promo:'18 pts in 10 matches',  relo:'Relegated if ≤6 pts in cycle',    tier:'low'},
      {d:3,name:'Championship',promo:'ELO 1500 → Div 2',    relo:'No relegation — ELO floor 1200',  tier:'top'},
      {d:2,name:'Premier',    promo:'ELO 1800 → Div 1',     relo:'ELO below 1200 → back to Div 3',  tier:'top'},
      {d:1,name:'Elite',      promo:'Top Division',          relo:'ELO below 1200 → Div 2',          tier:'top'},
    ];
    $('divisionGuide').innerHTML=divInfo.map(di=>`
      <div class="div-guide-card" style="${di.tier==='top'?'border-color:rgba(245,197,24,0.4);background:linear-gradient(135deg,rgba(245,197,24,0.08),rgba(10,22,40,0.9))':''}">
        <div style="display:flex;align-items:center;gap:10px">
          ${divBadge(di.d)}
          <div class="div-guide-name">${di.name}</div>
        </div>
        <div style="font-size:10px;font-weight:700;letter-spacing:1px;color:var(--ucl-star);margin:4px 0 2px;text-transform:uppercase">${seasonName}</div>
        <div class="div-guide-pts">&#8679; ${di.promo}</div>
        <div class="div-guide-desc">${di.relo}</div>
        ${di.tier==='top'?'<div class="div-guide-badge" style="color:#F5C518">ELO RATING SYSTEM</div>':''}
      </div>`).join('');
  }catch(e){console.error(e);T('Error loading home','error');}
}

// ===== LEADERBOARD - COMPUTED FROM MATCH HISTORY ONLY =====
async function loadLeaderboard(tab='overall'){
  S.lbTab=tab;
  $('lbTableBody').innerHTML='<tr><td colspan="11" style="text-align:center;padding:30px"><div class="spinner" style="margin:0 auto"></div></td></tr>';

  // Season selector visibility
  const seasonSel=$('lbSeasonFilter');
  if(seasonSel){
    if(tab==='season'){
      seasonSel.style.display='block';
      if(seasonSel.options.length<=1){
        try{
          const snap=await getDocs(collection(db,'pastSeasons'));
          const seasons=snap.docs.map(d=>({id:d.id,...d.data()})).sort((a,b)=>(b.endedAt?.seconds||0)-(a.endedAt?.seconds||0));
          const curSnap=await getDoc(doc(db,'settings','season'));
          const curName=curSnap.exists()?(curSnap.data().name||'Current Season'):'Current Season';
          seasonSel.innerHTML=`<option value="current">${curName} (Current)</option>`+seasons.map(s=>`<option value="${s.id}">${s.name||'Season'} (${s.startDate||''})</option>`).join('');
        }catch(e){console.error(e);}
      }
    } else {
      seasonSel.style.display='none';
    }
  }

  try{
    const [pSnap,mSnap]=await Promise.all([
      getDocs(collection(db,'players')),
      getDocs(collection(db,'matches'))
    ]);
    S.players=pSnap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
    S.matches=mSnap.docs.map(d=>({id:d.id,...d.data()}))
      .sort((a,b)=>(b.createdAt?.seconds||0)-(a.createdAt?.seconds||0));

    const now=Date.now();
    let seasonStartMs=0,seasonEndMs=now;

    // Determine time filter
    let matchFilter;
    if(tab==='daily'){matchFilter=m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<86400000;}
    else if(tab==='weekly'){matchFilter=m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<604800000;}
    else if(tab==='monthly'){matchFilter=m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<2592000000;}
    else if(tab==='season'){
      const selVal=$('lbSeasonFilter')?.value||'current';
      if(selVal==='current'){
        try{
          const ss=await getDoc(doc(db,'settings','season'));
          if(ss.exists()&&ss.data().startDate)seasonStartMs=new Date(ss.data().startDate).getTime();
          if(ss.exists()&&ss.data().endDate)seasonEndMs=new Date(ss.data().endDate).getTime();
        }catch(e){console.error(e);}
      }else{
        try{
          const ps=await getDoc(doc(db,'pastSeasons',selVal));
          if(ps.exists()){
            if(ps.data().startDate)seasonStartMs=new Date(ps.data().startDate).getTime();
            if(ps.data().endDate)seasonEndMs=new Date(ps.data().endDate).getTime();
          }
        }catch(e){console.error(e);}
      }
      matchFilter=m=>{const t=m.createdAt?.toDate?.()?.getTime()||0;return t>=seasonStartMs&&t<=seasonEndMs;};
    }
    else{matchFilter=null;} // overall = no filter

    const playerCatMap={};
    S.players.forEach(p=>playerCatMap[p.id]=p.category||'Main');

    let players=S.players.map(p=>{
      let pm=S.matches.filter(m=>(m.playerAId===p.id||m.playerBId===p.id)&&m.status==='confirmed');
      if(matchFilter)pm=pm.filter(matchFilter);

      let w=0,d=0,l=0,gf=0,ga=0,cs=0;
      pm.forEach(m=>{
        const side=m.playerAId===p.id?'A':'B';
        const result=getRC(m.scoreA,m.scoreB,side);
        const myG=side==='A'?m.scoreA:m.scoreB,opG=side==='A'?m.scoreB:m.scoreA;
        const oppCat=playerCatMap[side==='A'?m.playerBId:m.playerAId]||'Main';
        const mult=getRatingMultiplier(p.category||'Main',oppCat,result);
        if(result==='W')w+=mult;else if(result==='D')d++;else l+=mult;
        gf+=myG;ga+=opG;if(opG===0)cs++;
      });

      const total=pm.length,wr=total>0?Math.round((w/(w+d+l||1))*100):0,gd=gf-ga;
      const div=p.division||9,rules=DIV_RULES[div]||DIV_RULES[9];
      const rating=rules.useRating?(p.eloRating||DEFAULT_DIV3_RATING):Math.max(0,Math.round(w*10+d*5+l*(-5)+gd+cs*2));

      return {...p,tw:Math.round(w),td:d,tl:Math.round(l),tgf:gf,tga:ga,tcs:cs,tgd:gd,twr:wr,total,rating,cyclePts:p.cyclePts||0,cycleMP:p.cycleMP||0};
    });

    if(tab!=='overall')players=players.filter(p=>p.total>0);
    players.sort((a,b)=>b.rating-a.rating||b.tgd-a.tgd||b.twr-a.twr);
    S.lbPlayers=players;
    renderLbTable(players);
  }catch(e){
    $('lbTableBody').innerHTML='<tr><td colspan="11" style="text-align:center;color:#FF5555">Error loading</td></tr>';
    console.error(e);
  }
}

function renderLbTable(players){
  const search=($('lbSearch')?.value||'').toLowerCase();
  const divF=$('lbDivFilter')?.value||'';
  const filtered=players.filter(p=>p.name.toLowerCase().includes(search)&&(!divF||String(p.division||9)===divF));
  const tbody=$('lbTableBody');
  if(!filtered.length){
    tbody.innerHTML='<tr><td colspan="11"><div class="empty-state"><div class="empty-text">No players found</div></div></td></tr>';return;
  }
  tbody.innerHTML=filtered.map((p,i)=>{
    const r=i+1,rc=r===1?'top-1':r===2?'top-2':r===3?'top-3':'';
    const form=(p.form||[]).slice(-5);
    const rules=DIV_RULES[p.division||9]||DIV_RULES[9];
    const isElo=rules.useRating;
    let cycleCell='';
    if(isElo){
      const elo=p.eloRating||DEFAULT_DIV3_RATING;
      const next=RATING_PROMO[p.division];
      if(next){
        const pct=Math.min(100,Math.round(Math.max(0,elo-DEFAULT_DIV3_RATING)/(next-DEFAULT_DIV3_RATING)*100));
        cycleCell=`<div style="font-size:10px;color:#F5C518">${elo} ELO</div>
          <div style="background:rgba(255,255,255,.06);border-radius:3px;height:4px;width:48px;margin-top:3px;overflow:hidden">
            <div style="height:100%;width:${pct}%;background:linear-gradient(90deg,#F5C518,#FFD700);border-radius:3px"></div>
          </div>`;
      } else {
        cycleCell=`<div style="font-size:10px;color:#F5C518">${elo} ELO</div><div style="font-size:9px;color:#4472C4">Elite</div>`;
      }
    } else {
      const pct=Math.min(100,Math.round((p.cyclePts||0)/(rules.promo||1)*100));
      cycleCell=`<div style="font-size:10px;color:#4472C4">${p.cycleMP||0}/10</div>
        <div style="background:rgba(255,255,255,.06);border-radius:3px;height:4px;width:48px;margin-top:3px;overflow:hidden">
          <div style="height:100%;width:${pct}%;background:linear-gradient(90deg,#00A550,#00E676);border-radius:3px"></div>
        </div>`;
    }
    return `<tr class="${rc}">
      <td><span class="rank-num rank-${r}">${r}</span></td>
      <td>
        <span class="player-link" onclick="viewProfile('${p.id}')">
          <div class="user-avatar" style="width:28px;height:28px;font-size:11px">${p.name[0].toUpperCase()}</div>
          ${p.name}&nbsp;<span class="${catClass(p.category||'Main')}" style="font-size:10px;font-weight:700">${p.category||'Main'}</span>
          ${p.isModerator?'&nbsp;<span class="mod-badge-hdr">MOD</span>':''}
        </span>
      </td>
      <td>${divBadge(p.division)}</td>
      <td><span style="font-family:'Bebas Neue',sans-serif;font-size:20px;color:var(--ucl-star)">${p.rating}</span></td>
      <td>
        <div class="wdl-row">
          <span class="wdl-pill wdl-w"><span class="wdl-num">${p.tw}</span>&nbsp;W</span>
          <span class="wdl-pill wdl-d"><span class="wdl-num">${p.td}</span>&nbsp;D</span>
          <span class="wdl-pill wdl-l"><span class="wdl-num">${p.tl}</span>&nbsp;L</span>
        </div>
      </td>
      <td style="color:#82B1FF">${p.total}</td>
      <td>
        <div class="winrate-wrap">
          <div class="winrate-bar"><div class="winrate-fill" style="width:${p.twr}%"></div></div>
          <span class="winrate-pct">${p.twr}%</span>
        </div>
      </td>
      <td><span style="font-family:'Bebas Neue',sans-serif;font-size:16px;color:${p.tgd>=0?'#00E676':'#FF5555'}">${p.tgd>=0?'+':''}${p.tgd}</span></td>
      <td><span style="font-family:'Bebas Neue',sans-serif;font-size:16px;color:#82B1FF">${p.tcs}</span></td>
      <td><div class="form-dots">${form.map(r=>formBadge(r)).join('')}</div></td>
      <td>${cycleCell}</td>
    </tr>`;
  }).join('');
}

function filterLeaderboard(){if(S.lbPlayers.length)renderLbTable(S.lbPlayers);}
function switchLbTab(tab,btn){
  document.querySelectorAll('.lb-tab').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');loadLeaderboard(tab);
}

// ===== RANKING CARD =====
function openRankingCardPreview(){buildRankingCard();$('rankingCardPreview').classList.add('open');}
function closeRankingPreview(){$('rankingCardPreview').classList.remove('open');}

function buildRankingCard(){
  const top10=S.lbPlayers.slice(0,10);
  const labels={overall:'Overall',season:'Season Ranking',daily:'Daily Top',weekly:'Weekly Top',monthly:'Monthly Top'};
  const now=new Date().toLocaleDateString('en-GB',{day:'2-digit',month:'short',year:'numeric'});
  if(!top10.length){$('rcCardContainer').innerHTML='<div style="color:#666;padding:20px">Load leaderboard first</div>';return;}
  const divNames=['','Elite','Premier','Championship','League One','League Two','National','Regional','Amateur','Rookie'];
  const rows=top10.map((p,i)=>{
    const r=i+1,rc=r===1?'rank-1-row':r===2?'rank-2-row':r===3?'rank-3-row':'';
    const rankCls=r===1?'r1':r===2?'r2':r===3?'r3':'';
    return `<div class="rc-row ${rc}">
      <div class="rc-rank ${rankCls}">${r}</div>
      <div class="rc-player-info">
        <div class="rc-avatar">${p.name[0].toUpperCase()}</div>
        <div>
          <div class="rc-name">${p.name}</div>
          <div class="rc-div-small">DIV ${p.division||9} - ${divNames[p.division||9]||''} | ${p.category||'Main'}</div>
        </div>
      </div>
      <div class="rc-rating">${p.rating}</div>
      <div class="rc-wdl-nums"><span class="rc-w">${p.tw}W</span><span class="rc-d">&nbsp;${p.td}D</span><span class="rc-l">&nbsp;${p.tl}L</span></div>
      <div style="display:flex;gap:5px;align-items:center">
        <div style="background:rgba(255,255,255,.06);border-radius:4px;height:5px;width:58px;overflow:hidden">
          <div style="height:100%;width:${p.twr}%;background:linear-gradient(90deg,#1B3A6B,#4472C4);border-radius:4px"></div>
        </div>
        <span style="font-family:'Bebas Neue',sans-serif;font-size:13px;color:#4472C4">${p.twr}%</span>
      </div>
      <div class="rc-winpct" style="color:${p.tgd>=0?'#00E676':'#FF5555'}">${p.tgd>=0?'+':''}${p.tgd}</div>
    </div>`;
  }).join('');
  $('rcCardContainer').innerHTML=`
    <div class="rc-card" id="theRankingCard">
      <div class="rc-header">
        <div class="rc-header-top">
          <div><div class="rc-title">LLFC EFOOTBALL DIVISION</div><div class="rc-subtitle">PLAYER RANKING - TOP 10</div></div>
          <div class="rc-period">${labels[S.lbTab]||'Overall'}</div>
        </div>
      </div>
      <div class="rc-body">
        <div class="rc-row rc-header-row">
          <span>Rank</span><span>Player</span><span>Rating</span><span>W/D/L</span><span>Win%</span><span>GD</span>
        </div>
        ${rows}
      </div>
      <div class="rc-footer">
        <div class="rc-footer-brand">LLFC EFOOTBALL DIVISION SYSTEM</div>
        <div class="rc-footer-date">GENERATED: ${now}</div>
      </div>
    </div>`;
}

async function downloadRankingCard(){
  const card=$('theRankingCard');
  if(!card)return T('No card to download','error');
  try{
    T('Generating...','info');
    const canvas=await html2canvas(card,{backgroundColor:'#060E1C',scale:2,useCORS:true,logging:false});
    const link=document.createElement('a');
    link.download=`LLFC-Ranking-${S.lbTab}-${new Date().toISOString().split('T')[0]}.jpg`;
    link.href=canvas.toDataURL('image/jpeg',0.95);link.click();
    T('Downloaded!','success');
  }catch(e){T('Download failed: '+e.message,'error');}
}

// ===== MATCHES =====
async function loadMatches(){
  try{
    // Fetch all matches client-side sort to avoid composite index requirement
    const mSnap=await getDocs(query(collection(db,'matches'),limit(200)));
    S.matches=mSnap.docs.map(d=>({id:d.id,...d.data()}))
      .sort((a,b)=>(b.createdAt?.seconds||0)-(a.createdAt?.seconds||0));
    S.allMatchesData=S.matches;
    renderMatchesList(S.matches);
    renderPendingConfirms();
  }catch(e){$('matchesList').innerHTML='<div class="empty-state"><div class="empty-text">Error loading</div></div>';console.error(e);}
}

function renderMatchesList(matches){
  const search=($('matchSearch')?.value||'').toLowerCase();
  const sf=$('matchStatusFilter')?.value||'';
  let f=matches;
  if(search)f=f.filter(m=>m.playerAName?.toLowerCase().includes(search)||m.playerBName?.toLowerCase().includes(search));
  if(sf)f=f.filter(m=>m.status===sf);
  const el=$('matchesList');
  if(!f.length){el.innerHTML='<div class="empty-state"><div class="empty-icon">&#9917;</div><div class="empty-text">No matches found</div></div>';return;}
  el.innerHTML=f.map(m=>{
    const hi=isHigh(m.scoreA,m.scoreB),x2=m.is2x;
    return `<div class="match-card${hi?' high-score':''}">
      <div class="match-info">
        <div class="match-vs">
          <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerAId}')">${m.playerAName}</span>
          <span class="text-gray"> vs </span>
          <span class="player-link" style="display:inline" onclick="viewProfile('${m.playerBId}')">${m.playerBName}</span>
          ${hi?' <span class="high-score-badge">GOAL FEST</span>':''}
          ${x2?' <span class="x2-badge">2X RATING</span>':''}
        </div>
        <div class="match-meta">${fmtDate(m.createdAt||m.matchDate)} - ${statusBadge(m.status)}</div>
      </div>
      <div class="match-score">${m.scoreA}-${m.scoreB}</div>
    </div>`;
  }).join('');
}

function renderPendingConfirms(){
  const section=$('pendingConfirmSection'),list=$('pendingConfirmList');
  if(!S.user){section.style.display='none';return;}
  const isMod=S.user.isModerator;
  const pending=S.allMatchesData.filter(m=>m.status==='pending'&&(isMod||m.playerBId===S.user.id));
  if(!pending.length){section.style.display='none';return;}
  section.style.display='block';
  list.innerHTML=pending.map(m=>`
    <div class="confirm-card">
      ${isMod&&m.playerBId!==S.user.id?'<div style="font-size:11px;color:#CE93D8;font-weight:700;margin-bottom:8px;letter-spacing:1px">MODERATOR REVIEW</div>':''}
      <div class="confirm-vs">
        <div class="confirm-player"><div class="confirm-player-name">${m.playerAName}</div><div class="text-gray text-sm">${m.playerACat||''}</div></div>
        <div class="confirm-score-display">${m.scoreA}-${m.scoreB}</div>
        <div class="confirm-player"><div class="confirm-player-name">${m.playerBName}</div><div class="text-gray text-sm">${m.playerBCat||''}</div></div>
      </div>
      <div class="text-gray text-sm mb-8">${fmtDate(m.createdAt)} - ${timeAgo(m.createdAt)}</div>
      <div style="display:flex;gap:8px;flex-wrap:wrap">
        <button class="btn-approve btn-sm" onclick="confirmMatch('${m.id}',true)">Confirm</button>
        <button class="btn-reject btn-sm" onclick="confirmMatch('${m.id}',false)">Dispute</button>
      </div>
    </div>`).join('');
}

function filterMatches(){if(S.allMatchesData.length)renderMatchesList(S.allMatchesData);}

async function confirmMatch(matchId,confirmed){
  try{
    const mRef=doc(db,'matches',matchId);
    const mSnap=await getDoc(mRef);
    if(!mSnap.exists())return T('Match not found','error');
    const m=mSnap.data();
    if(confirmed){
      await updateDoc(mRef,{status:'confirmed',confirmedAt:serverTimestamp()});
      await applyMatchStats({...m, id:matchId});
      T('Match confirmed! Stats updated','success');
    }else{
      await updateDoc(mRef,{status:'disputed'});
      T('Match disputed. Admin will review.','info');
    }
    S.matches=[];S.allMatchesData=[];
    // Reload whichever view is active
    if(document.getElementById('page-modpanel')?.classList.contains('active')){loadModPanel();}
    else{loadMatches();}
  }catch(e){T('Error: '+e.message,'error');}
}

async function applyMatchStats(m){
  const [aSnap,bSnap]=await Promise.all([
    getDoc(doc(db,'players',m.playerAId)),
    getDoc(doc(db,'players',m.playerBId))
  ]);
  if(!aSnap.exists()||!bSnap.exists())return;
  const aData=aSnap.data(), bData=bSnap.data();
  const aCat=aData.category||'Main', bCat=bData.category||'Main';

  // Store category on match for display
  await updateDoc(doc(db,'matches',m.id||'_'),{
    playerACat:aCat,playerBCat:bCat,
    is2x:getRatingMultiplier(aCat,bCat,getRC(m.scoreA,m.scoreB,'A'))>1||
         getRatingMultiplier(bCat,aCat,getRC(m.scoreA,m.scoreB,'B'))>1
  }).catch(()=>{});

  async function upd(pid,pData,side,oppData){
    const ref=doc(db,'players',pid);
    const oppCat=oppData.category||'Main';
    const result=getRC(m.scoreA,m.scoreB,side);
    const myG=side==='A'?m.scoreA:m.scoreB, opG=side==='A'?m.scoreB:m.scoreA;
    const isCS=opG===0;
    const form=[...(pData.form||[]).slice(-19),result];
    const div=pData.division||9;
    const rules=DIV_RULES[div]||DIV_RULES[9];
    const mult=getRatingMultiplier(pData.category||'Main',oppCat,result);

    let updates={
      wins:(pData.wins||0)+(result==='W'?mult:0),
      draws:(pData.draws||0)+(result==='D'?1:0),
      losses:(pData.losses||0)+(result==='L'?mult:0),
      goalsFor:(pData.goalsFor||0)+myG,
      goalsAgainst:(pData.goalsAgainst||0)+opG,
      cleanSheets:(pData.cleanSheets||0)+(isCS?1:0),
      form,
    };

    if(rules.useRating){
      // === DIV 3-1: ELO-style rating system ===
      const myRating=pData.eloRating||DEFAULT_DIV3_RATING;
      const oppRating=oppData.eloRating||DEFAULT_DIV3_RATING;
      const oppRank=S.lbPlayers.findIndex(x=>x.id===pid);
      const myRank=S.lbPlayers.findIndex(x=>x.id===(side==='A'?m.playerBId:m.playerAId));
      const oppIsBetterRanked=(myRank>oppRank)&&oppRank>=0; // lower index = better rank

      let ratingChange=0;
      if(result==='W'){
        ratingChange=oppIsBetterRanked?40:25;
        ratingChange=Math.round(ratingChange*mult);
      }else if(result==='L'){
        ratingChange=oppIsBetterRanked?-25:-40;
        ratingChange=Math.round(ratingChange*mult);
      }else{
        ratingChange=0;
      }

      const newRating=Math.max(DEFAULT_DIV3_RATING, myRating+ratingChange);
      updates.eloRating=newRating;
      updates.eloChange=ratingChange;

      // Div 3+ promotion/relegation based on eloRating
      let newDiv=div, action=null;
      if(div===3&&newRating>=RATING_PROMO[3]){newDiv=2;action='promote';}
      else if(div===2&&newRating>=RATING_PROMO[2]){newDiv=1;action='promote';}
      else if(div===2&&newRating<RATING_RELO[2]){
        // Relegate back to div 3, reset rating to floor
        newDiv=3;action='relegate';updates.eloRating=DEFAULT_DIV3_RATING;
      }else if(div===1&&newRating<RATING_RELO[1]){
        newDiv=2;action='relegate';
      }
      if(action){
        updates.division=newDiv;
        updates.highestDivision=Math.min(newDiv,pData.highestDivision||9);
        if(action==='promote')setTimeout(()=>T(pData.name+' promoted to Division '+newDiv+'!','success'),100);
        else if(action==='relegate')setTimeout(()=>T(pData.name+' relegated to Division '+newDiv+'.','info'),100);
      }
    } else {
      // === DIV 4-9: Cycle-based point system ===
      const cyclePtsGain=result==='W'?3:result==='D'?1:0;
      const newCycleMP=(pData.cycleMP||0)+1;
      const newCyclePts=(pData.cyclePts||0)+cyclePtsGain;
      updates.cycleMP=newCycleMP;
      updates.cyclePts=newCyclePts;

      // Check div promotion/relegation
      let newDiv=div, action=null;
      if(newCyclePts>=rules.promo&&div>4){
        // Promote to Div 3 -> enter rating system
        newDiv=div-1;action='promote';
        if(newDiv<=3){updates.eloRating=DEFAULT_DIV3_RATING;}
        updates.cycleMP=0;updates.cyclePts=0;
      }else if(newCyclePts>=rules.promo&&div>1){
        newDiv=div-1;action='promote';
        updates.cycleMP=0;updates.cyclePts=0;
      }else if(newCycleMP>=rules.cycle){
        if(newCyclePts<=rules.relo&&div<9){newDiv=div+1;action='relegate';}
        updates.cycleMP=0;updates.cyclePts=0;
      }
      if(action){
        updates.division=newDiv;
        updates.highestDivision=Math.min(newDiv,pData.highestDivision||9);
        if(action==='promote')setTimeout(()=>T(pData.name+' promoted to Division '+newDiv+'!','success'),100);
        else if(action==='relegate')setTimeout(()=>T(pData.name+' relegated to Division '+newDiv+'.','info'),100);
      }
    }

    await updateDoc(ref,updates);
  }

  await Promise.all([
    upd(m.playerAId,aData,'A',bData),
    upd(m.playerBId,bData,'B',aData)
  ]);
}

// ===== SUBMIT =====
async function loadSubmitPage(){
  if(!S.user){$('submitRequireLogin').style.display='block';$('submitForm').style.display='none';return;}
  $('submitRequireLogin').style.display='none';$('submitForm').style.display='block';
  $('submitMyName').value=S.user.name;
  $('matchDate').value=new Date().toISOString().split('T')[0];
  const snap=await getDocs(collection(db,'players'));
  S.players=snap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
  const sel=$('submitOpponent');
  sel.innerHTML='<option value="">-- Select Opponent --</option>'+
    S.players.filter(p=>p.id!==S.user.id).map(p=>`<option value="${p.id}">${p.name} (Div ${p.division||9} - ${p.category||'Main'})</option>`).join('');
}

async function submitMatchResult(){
  if(!S.user)return T('Login required','error');
  const oppId=$('submitOpponent').value;
  const sA=parseInt($('scoreA').value);
  const sB=parseInt($('scoreB').value);
  const matchDate=$('matchDate').value;
  if(!oppId)return T('Select an opponent','error');
  if(isNaN(sA)||isNaN(sB)||$('scoreA').value===''||$('scoreB').value==='')return T('Enter both scores','error');
  const opp=S.players.find(p=>p.id===oppId);
  if(!opp)return T('Opponent not found','error');
  const btn=document.querySelector('#submitForm .btn-primary');
  if(btn)btn.disabled=true;
  try{
    await addDoc(collection(db,'matches'),{
      playerAId:S.user.id,playerAName:S.user.name,playerACat:S.user.category||'Main',
      playerBId:oppId,playerBName:opp.name,playerBCat:opp.category||'Main',
      scoreA:sA,scoreB:sB,status:'pending',matchDate,
      createdAt:serverTimestamp(),submittedBy:S.user.id
    });
    const msg=isHigh(sA,sB)?`GOAL FEST! ${sA+sB} goals submitted. Waiting for ${opp.name}.`:`Result submitted. Waiting for ${opp.name} to confirm.`;
    T(msg,'success');
    // Reset all fields — force user to re-select opponent
    $('scoreA').value='';
    $('scoreB').value='';
    $('submitOpponent').value='';  // reset to placeholder
    S.matches=[];
  }catch(e){T('Submit failed: '+e.message,'error');}
  finally{if(btn)btn.disabled=false;}
}

// ===== MOD PANEL =====
async function loadModPanel(){
  if(!S.user||!S.user.isModerator){
    $('modPendingMatches').innerHTML='<div class="empty-state"><div class="empty-text">Moderator access required. Login with a moderator account.</div></div>';return;
  }
  const el=$('modPendingMatches');
  el.innerHTML='<div class="loading-spinner"><div class="spinner"></div></div>';
  try{
    // Simple query without composite index - filter status only, sort client-side
    const mSnap=await getDocs(query(collection(db,'matches'),where('status','==','pending'),limit(100)));
    const pending=mSnap.docs.map(d=>({id:d.id,...d.data()}))
      .sort((a,b)=>(b.createdAt?.seconds||0)-(a.createdAt?.seconds||0));
    if(!pending.length){
      el.innerHTML='<div class="empty-state"><div class="empty-icon">&#10003;</div><div class="empty-text">No pending matches</div><div class="empty-sub">All caught up!</div></div>';return;
    }
    el.innerHTML=pending.map(m=>`
      <div class="confirm-card">
        <div style="font-size:10px;color:#CE93D8;font-weight:700;letter-spacing:2px;margin-bottom:8px">MODERATOR REVIEW</div>
        <div class="confirm-vs">
          <div class="confirm-player">
            <div class="confirm-player-name">${m.playerAName}</div>
            <div class="text-gray text-sm">${m.playerACat||'Main'}</div>
          </div>
          <div class="confirm-score-display">${m.scoreA}-${m.scoreB}</div>
          <div class="confirm-player">
            <div class="confirm-player-name">${m.playerBName}</div>
            <div class="text-gray text-sm">${m.playerBCat||'Main'}</div>
          </div>
        </div>
        <div class="text-gray text-sm mb-8">${fmtDate(m.createdAt)} - ${timeAgo(m.createdAt)}</div>
        <div style="display:flex;gap:8px;flex-wrap:wrap">
          <button class="btn-approve btn-sm" onclick="confirmMatch('${m.id}',true)">Approve</button>
          <button class="btn-reject btn-sm" onclick="confirmMatch('${m.id}',false)">Dispute</button>
        </div>
      </div>`).join('');
  }catch(e){
    el.innerHTML=`<div class="empty-state"><div class="empty-text">Error: ${e.message}</div><div class="empty-sub">Try refreshing the page</div></div>`;
    console.error('Mod panel error:',e);
  }
}

// ===== PROFILE =====
async function viewProfile(playerId){
  S.pageHistory.push('profile');showPage('profile');
  $('profileContent').innerHTML='<div class="loading-spinner"><div class="spinner"></div></div>';
  try{
    const [snap,mSnap]=await Promise.all([
      getDoc(doc(db,'players',playerId)),
      getDocs(query(collection(db,'matches'),orderBy('createdAt','desc'),limit(500)))
    ]);
    if(!snap.exists()){$('profileContent').innerHTML='<div class="empty-state"><div class="empty-text">Player not found</div></div>';return;}
    const p={id:snap.id,...snap.data()};
    const allM=mSnap.docs.map(d=>({id:d.id,...d.data()}));
    
    // Compute stats strictly from match history
    const myConfirmed=allM.filter(m=>(m.playerAId===playerId||m.playerBId===playerId)&&m.status==='confirmed');
    const recent=myConfirmed.slice(0,10);
    
    // Build player category map for 2x calc
    const playerCatMap={};
    S.players.forEach(pp=>playerCatMap[pp.id]=pp.category||'Main');
    
    let w=0,d=0,l=0,gf=0,ga=0,cs=0,x2Count=0;
    myConfirmed.forEach(m=>{
      const side=m.playerAId===playerId?'A':'B';
      const result=getRC(m.scoreA,m.scoreB,side);
      const myG=side==='A'?m.scoreA:m.scoreB, opG=side==='A'?m.scoreB:m.scoreA;
      const oppId=side==='A'?m.playerBId:m.playerAId;
      const oppCat=playerCatMap[oppId]||(side==='A'?m.playerBCat:m.playerACat)||'Main';
      const mult=getRatingMultiplier(p.category||'Main',oppCat,result);
      if(mult>1)x2Count++;
      if(result==='W')w+=mult;
      else if(result==='D')d+=1;
      else l+=mult;
      gf+=myG;ga+=opG;if(opG===0)cs++;
    });
    const total=myConfirmed.length,wr=total>0?Math.round((w/(w+d+l||1))*100):0;
    const gd=gf-ga;
    // Display rating: ELO for div 3+, computed for div 4-9
    const displayRating=(p.division||9)<=3
      ? (p.eloRating||DEFAULT_DIV3_RATING)
      : Math.max(0,Math.round(w*10+d*5+l*(-5)+gd+cs*2));
    
    const div=p.division||9,rules=DIV_RULES[div]||DIV_RULES[9];
    const isEloDiv=rules.useRating;
    const cmp=p.cycleMP||0,cpts=p.cyclePts||0;
    const eloRating=p.eloRating||DEFAULT_DIV3_RATING;
    
    // Build promo tracker HTML
    let promoHTML='';
    if(isEloDiv){
      const nextPromo=RATING_PROMO[div];
      const floor=DEFAULT_DIV3_RATING;
      if(nextPromo){
        const pct=Math.min(100,Math.round(Math.max(0,eloRating-floor)/(nextPromo-floor)*100));
        promoHTML=`<div class="promo-tracker">
          <div class="promo-title">ELO Rating - Division ${div} (${rules.name})</div>
          <div class="promo-bar-wrap"><div class="promo-bar-fill" style="width:${pct}%;background:linear-gradient(90deg,#F5C518,#FFD700)"></div></div>
          <div class="promo-label"><span>${eloRating} ELO</span><span>Promote at ${nextPromo}</span></div>
          <div class="promo-cycle-info" style="color:#F5C518">Win vs higher ranks: +40 | Normal win: +25 | Loss: -25 to -40</div>
        </div>`;
      } else {
        promoHTML=`<div class="promo-tracker">
          <div class="promo-title">ELO Rating - Division 1 Elite</div>
          <div class="promo-bar-wrap"><div class="promo-bar-fill" style="width:100%;background:linear-gradient(90deg,#FFD700,#FF8C00)"></div></div>
          <div class="promo-label"><span>${eloRating} ELO</span><span>Top Division</span></div>
          <div class="promo-cycle-info" style="color:#FFD700">Maintain rating above 1200 to stay in Division 1</div>
        </div>`;
      }
    } else {
      const pct=Math.min(100,Math.round(cpts/(rules.promo||1)*100));
      promoHTML=`<div class="promo-tracker">
        <div class="promo-title">Division ${div} Cycle Progress</div>
        <div class="promo-bar-wrap"><div class="promo-bar-fill" style="width:${pct}%"></div></div>
        <div class="promo-label"><span>${cpts} pts / ${rules.promo} needed</span><span>${cmp}/10 matches</span></div>
        ${cmp>=rules.cycle?'<div class="promo-cycle-info" style="color:#00E676">Cycle complete - awaiting review</div>':
        `<div class="promo-cycle-info">${Math.max(0,rules.cycle-cmp)} matches left this cycle</div>`}
      </div>`;
    }
    const form=(p.form||[]).slice(-5);
    const isMe=S.user&&S.user.id===playerId,isRival=S.user&&(S.user.rivals||[]).includes(playerId);

    // ===== ACHIEVEMENT BADGES =====
    const badges=[];
    // Division achievement
    if(div===1)badges.push({t:'Elite Division',c:'badge-star',icon:'★'});
    else if(div===2)badges.push({t:'Premier Division',c:'badge-silver',icon:'◆'});
    else if(div===3)badges.push({t:'Championship',c:'badge-gold',icon:'◈'});
    const highest=p.highestDivision||div;
    if(highest<div)badges.push({t:'Peak: Div '+highest,c:'badge-blue',icon:'▲'});
    // Win ratio
    if(wr>=80&&total>=5)badges.push({t:'Win Machine 80%+',c:'badge-gold',icon:'⚡'});
    else if(wr>=70&&total>=5)badges.push({t:'Sharp 70%+',c:'badge-green',icon:'✦'});
    // Streak
    let streak=0;const fm=p.form||[];for(let i=fm.length-1;i>=0;i--){if(fm[i]==='W')streak++;else break;}
    if(streak>=5)badges.push({t:'On Fire '+streak+'W',c:'badge-red',icon:'🔥'});
    else if(streak>=3)badges.push({t:streak+' Win Streak',c:'badge-green',icon:'↑'});
    // 2x upsets
    if(x2Count>0)badges.push({t:'Upset King x'+x2Count,c:'badge-purple',icon:'⚔'});
    // POTD tiered
    const potdC=p.potdCount||0;
    if(p.isPOTD||potdC>0){
      if(potdC>=5)badges.push({t:'POTD Legend x'+potdC,c:'badge-diamond',icon:'♦'});
      else if(potdC>=3)badges.push({t:'POTD Elite x'+potdC,c:'badge-star',icon:'★'});
      else if(potdC>=2)badges.push({t:'2x Player of Day',c:'badge-gold',icon:'☀'});
      else badges.push({t:'Player of the Day',c:'badge-gold',icon:'☀'});
    }
    // POTW tiered
    const potwC=p.potwCount||0;
    if(p.isPOTW||potwC>0){
      if(potwC>=3)badges.push({t:'POTW Legend x'+potwC,c:'badge-diamond',icon:'♦'});
      else if(potwC>=2)badges.push({t:'2x Player of Week',c:'badge-purple',icon:'◉'});
      else badges.push({t:'Player of the Week',c:'badge-purple',icon:'◉'});
    }
    // POTM tiered
    const potmC=p.potmCount||0;
    if(p.isPOTM||potmC>0){
      if(potmC>=3)badges.push({t:'POTM Legend x'+potmC,c:'badge-diamond',icon:'♦'});
      else if(potmC>=2)badges.push({t:'2x Player of Month',c:'badge-blue',icon:'◑'});
      else badges.push({t:'Player of the Month',c:'badge-blue',icon:'◑'});
    }
    // POTS tiered
    const potsC=p.potsCount||0;
    if(p.isPOTS||potsC>0){
      if(potsC>=2)badges.push({t:'Season Champion x'+potsC,c:'badge-diamond',icon:'♛'});
      else badges.push({t:'Player of the Season',c:'badge-star',icon:'♛'});
    }
    // Most active
    if(p.isMostActiveD){const dC=p.mostActiveDCount||1;badges.push({t:'Most Active Today'+(dC>1?' x'+dC:''),c:'badge-green',icon:'▶'});}
    if(p.isMostActiveW){const wC=p.mostActiveWCount||1;badges.push({t:'Most Active Week'+(wC>1?' x'+wC:''),c:'badge-green',icon:'▶▶'});}
    if(p.isMostActiveM){const mC=p.mostActiveMCount||1;badges.push({t:'Most Active Month'+(mC>1?' x'+mC:''),c:'badge-blue',icon:'▶▶▶'});}
    // Moderator
    if(p.isModerator)badges.push({t:'Moderator',c:'badge-blue',icon:'⚑'});

    $('profileContent').innerHTML=`
      <div class="profile-header">
        <div class="profile-avatar">${p.name[0].toUpperCase()}</div>
        <div class="profile-info">
          <div class="profile-name">${p.name}</div>
          <span class="profile-cat ${catClass(p.category||'Main')}">${p.category||'Main'}</span>
          <div style="display:flex;align-items:center;gap:10px;margin-top:8px;flex-wrap:wrap">
            ${divBadge(div)} <span class="text-gray text-sm">Division ${div} - ${rules.name}</span>
            ${highest<div?`<span class="text-blue text-sm">Best Div: ${highest}</span>`:''}
          </div>
          <div class="form-dots mt-8">${form.map(r=>formBadge(r)).join('')}</div>
          <div class="badges-row">${badges.map(b=>`<span class="player-badge ${b.c}"><span class="badge-icon">${b.icon||''}</span>${b.t}</span>`).join('')}</div>
          <div style="display:flex;gap:8px;margin-top:10px;flex-wrap:wrap">
            ${!isMe&&S.user?`<button class="btn-sm ${isRival?'btn-reject':'btn-edit'}" onclick="toggleRival('${playerId}','${p.name}')">
              ${isRival?'Remove Rival':'Add Rival'}</button>`:''}
            ${isMe?`<button class="btn-sm btn-edit" onclick="openModal('changePwModal')">Change Password</button>`:''}
          </div>
        </div>
      </div>
      <div class="profile-stats">
        <div class="p-stat"><div class="p-stat-val" style="color:var(--ucl-star)">${displayRating}</div><div class="p-stat-lbl">${(p.division||9)<=3?'ELO Rating':'Rating'}</div></div>
        <div class="p-stat"><div class="p-stat-val text-green">${Math.round(w)}</div><div class="p-stat-lbl">Wins</div></div>
        <div class="p-stat"><div class="p-stat-val text-yellow">${d}</div><div class="p-stat-lbl">Draws</div></div>
        <div class="p-stat"><div class="p-stat-val text-red">${Math.round(l)}</div><div class="p-stat-lbl">Losses</div></div>
        <div class="p-stat"><div class="p-stat-val" style="color:#82B1FF">${total}</div><div class="p-stat-lbl">Matches</div></div>
        <div class="p-stat"><div class="p-stat-val">${wr}%</div><div class="p-stat-lbl">Win Rate</div></div>
        <div class="p-stat"><div class="p-stat-val" style="color:${gd>=0?'#00E676':'#FF5555'}">${gd>=0?'+':''}${gd}</div><div class="p-stat-lbl">Goal Diff</div></div>
        <div class="p-stat"><div class="p-stat-val" style="color:#82B1FF">${cs}</div><div class="p-stat-lbl">Clean Sheets</div></div>
      </div>
      ${promoHTML}
      <div class="section-title mt-16">Recent Matches</div>
      ${recent.length?recent.map(m=>{
        const side=m.playerAId===playerId?'A':'B';
        const res=getRC(m.scoreA,m.scoreB,side);
        const oppName=side==='A'?m.playerBName:m.playerAName;
        const oppId2=side==='A'?m.playerBId:m.playerAId;
        const myG=side==='A'?m.scoreA:m.scoreB,opG=side==='A'?m.scoreB:m.scoreA;
        const hi=isHigh(m.scoreA,m.scoreB),x2=m.is2x;
        return `<div class="match-card${hi?' high-score':''}">
          <div class="match-result-badge result-${res}">${res}</div>
          <div class="match-info">
            <div class="match-vs">vs <span class="player-link" style="display:inline" onclick="viewProfile('${oppId2}')">${oppName}</span>
              ${hi?' <span class="high-score-badge">GOAL FEST</span>':''}
              ${x2?' <span class="x2-badge">2X</span>':''}
            </div>
            <div class="match-meta">${fmtDate(m.createdAt||m.matchDate)} - ${statusBadge(m.status)}</div>
          </div>
          <div class="match-score">${myG}-${opG}</div>
        </div>`;
      }).join(''):'<div class="empty-state"><div class="empty-text">No matches yet</div></div>'}
    `;
  }catch(e){$('profileContent').innerHTML='<div class="empty-state"><div class="empty-text">Error loading profile</div></div>';console.error(e);}
}

async function loadMyProfile(){
  if(!S.user){
    $('myProfileContent').innerHTML='<div class="empty-state"><div class="empty-icon">&#128274;</div><div class="empty-text">Not logged in</div><button class="btn-primary mt-12" onclick="openModal(\'loginModal\')">Login</button></div>';return;
  }
  // Refresh user data
  try{
    const snap=await getDoc(doc(db,'players',S.user.id));
    if(snap.exists())S.user={...S.user,...snap.data()};
  }catch{}
  await viewProfile(S.user.id);
  $('myProfileContent').innerHTML=$('profileContent').innerHTML;
}

async function toggleRival(playerId,playerName){
  if(!S.user)return;
  const rivals=S.user.rivals||[];
  const nr=rivals.includes(playerId)?rivals.filter(r=>r!==playerId):[...rivals,playerId];
  await updateDoc(doc(db,'players',S.user.id),{rivals:nr});
  S.user.rivals=nr;
  T(rivals.includes(playerId)?playerName+' removed from rivals':playerName+' added as rival','success');
  viewProfile(playerId);
}

// ===== ADMIN =====
async function adminLogin(){
  const pw=$('adminPwInput').value;
  let stored=S.adminPw;
  try{const s=await getDoc(doc(db,'settings','admin'));if(s.exists()&&s.data().password)stored=s.data().password;}catch{}
  if(pw===stored){
    $('adminLoginWrap').style.display='none';$('adminPanelWrap').style.display='block';
    loadAdminPanel('pending');T('Admin access granted','success');
  }else T('Wrong password','error');
}

async function loadAdminPanel(tab){
  if(tab==='pending'){
    const snap=await getDocs(query(collection(db,'players'),where('status','==','pending')));
    const pending=snap.docs.map(d=>({id:d.id,...d.data()}));
    const el=$('adminPendingList');
    if(!pending.length){el.innerHTML='<div class="empty-state"><div class="empty-icon">&#10003;</div><div class="empty-text">No pending</div></div>';return;}
    el.innerHTML=pending.map(p=>`
      <div class="pending-item">
        <div class="pending-info"><div class="pending-name">${p.name}</div><div class="pending-meta">${p.category} - ${fmtDate(p.createdAt)}</div></div>
        <div style="display:flex;gap:6px;flex-wrap:wrap">
          <button class="btn-sm btn-approve" onclick="adminApprove('${p.id}')">Approve</button>
          <button class="btn-sm btn-reject" onclick="adminReject('${p.id}')">Reject</button>
        </div>
      </div>`).join('');
  }
  if(tab==='players'){
    const snap=await getDocs(collection(db,'players'));
    S.adminPlayers=snap.docs.map(d=>({id:d.id,...d.data()}));
    renderAdminPlayers(S.adminPlayers);
  }
  if(tab==='adminMatches'){
    const snap=await getDocs(query(collection(db,'matches'),limit(150)));
    const matches=snap.docs.map(d=>({id:d.id,...d.data()}))
      .sort((a,b)=>(b.createdAt?.seconds||0)-(a.createdAt?.seconds||0));
    const el=$('adminMatchesList');
    if(!matches.length){el.innerHTML='<div class="empty-state"><div class="empty-text">No matches</div></div>';return;}
    el.innerHTML=matches.map(m=>{
      const hi=isHigh(m.scoreA,m.scoreB),x2=m.is2x;
      return `<div class="pending-item${hi?' high-score':''}">
        <div class="pending-info">
          <div class="pending-name">${m.playerAName} ${m.scoreA}-${m.scoreB} ${m.playerBName}${hi?' [GOAL FEST]':''}${x2?' [2X]':''}</div>
          <div class="pending-meta">${fmtDate(m.createdAt)} - ${statusBadge(m.status)}</div>
        </div>
        <div style="display:flex;gap:5px;flex-wrap:wrap">
          ${m.status==='pending'?`<button class="btn-sm btn-approve" onclick="adminConfirmMatch('${m.id}')">Confirm</button>`:''}
          <button class="btn-sm btn-edit" onclick="adminEditMatch('${m.id}','${m.playerAName}','${m.playerBName}',${m.scoreA},${m.scoreB},'${m.status}')">Edit</button>
          <button class="btn-sm btn-reject" onclick="adminDeleteMatchDirect('${m.id}')">Delete</button>
        </div>
      </div>`;
    }).join('');
  }
  if(tab==='moderators'){
    const snap=await getDocs(collection(db,'players'));
    S.adminPlayers=snap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
    renderModPlayers(S.adminPlayers);
  }
  if(tab==='season'){
    loadSeasonInfo();
  }
}

function renderAdminPlayers(players){
  const search=($('adminPlayerSearch')?.value||'').toLowerCase();
  const filtered=players.filter(p=>p.name?.toLowerCase().includes(search));
  const getDisplayRating=p=>{
    const rules=DIV_RULES[p.division||9]||DIV_RULES[9];
    if(rules.useRating) return (p.eloRating||DEFAULT_DIV3_RATING)+' ELO';
    return Math.max(0,Math.round((p.wins||0)*10+(p.draws||0)*5+(p.losses||0)*(-5)+((p.goalsFor||0)-(p.goalsAgainst||0))+(p.cleanSheets||0)*2))+'';
  };
  $('adminPlayersList').innerHTML=filtered.length?filtered.map(p=>`
    <div class="pending-item">
      ${divBadge(p.division)}
      <div class="pending-info">
        <div class="pending-name">${p.name} <span class="${catClass(p.category||'Main')}" style="font-size:11px">${p.category||'Main'}</span>${p.status==='banned'?' [BANNED]':''}${p.isModerator?' [MOD]':''}</div>
        <div class="pending-meta">Div${p.division||9} - Rating:${getDisplayRating(p)} - ${p.wins||0}W ${p.draws||0}D ${p.losses||0}L - Cycle:${p.cycleMP||0}/10 (${p.cyclePts||0}pts) - ${statusBadge(p.status||'active')}</div>
      </div>
      <div style="display:flex;gap:4px;flex-wrap:wrap">
        <button class="btn-sm btn-edit" onclick="adminEditPlayer('${p.id}',${p.division||9},'${p.category||'Main'}',${p.wins||0},${p.draws||0},${p.losses||0},${p.goalsFor||0},${p.goalsAgainst||0},${p.cleanSheets||0},${p.cycleMP||0},${p.cyclePts||0},'${p.status||'active'}','${(p.name||'').replace(/'/g,"\\'")}')">Edit</button>
        <button class="btn-sm btn-ban" onclick="adminToggleBan('${p.id}','${p.name}','${p.status||'active'}')">
          ${p.status==='banned'?'Unban':'Ban'}</button>
        <button class="btn-sm ${p.isPOTD?'btn-reject':'btn-approve'}" onclick="adminTogglePOTD('${p.id}','${p.name}',${!!p.isPOTD})">${p.isPOTD?'Rem POTD':'POTD'}</button>
        <button class="btn-sm ${p.isPOTW?'btn-reject':'btn-edit'}" onclick="adminTogglePOTW('${p.id}','${p.name}',${!!p.isPOTW})">${p.isPOTW?'Rem POTW':'POTW'}</button>
        <button class="btn-sm ${p.isPOTM?'btn-reject':'btn-mod'}" onclick="adminTogglePOTM('${p.id}','${p.name}',${!!p.isPOTM})">${p.isPOTM?'Rem POTM':'POTM'}</button>
        <button class="btn-sm ${p.isPOTS?'btn-reject':'btn-ban'}" onclick="adminTogglePOTS('${p.id}','${p.name}',${!!p.isPOTS})">${p.isPOTS?'Rem POTS':'POTS'}</button>
      </div>
    </div>`).join(''):'<div class="empty-state"><div class="empty-text">No players</div></div>';
}

function filterAdminPlayers(){if(S.adminPlayers.length)renderAdminPlayers(S.adminPlayers);}

function renderModPlayers(players){
  const search=($('modPlayerSearch')?.value||'').toLowerCase();
  const filtered=players.filter(p=>p.name?.toLowerCase().includes(search));
  $('modPlayersList').innerHTML=filtered.length?filtered.map(p=>`
    <div class="pending-item">
      ${divBadge(p.division)}
      <div class="pending-info">
        <div class="pending-name">${p.name} <span class="${catClass(p.category||'Main')}" style="font-size:11px">${p.category||'Main'}</span>${p.isModerator?' [MODERATOR]':''}</div>
        <div class="pending-meta">${p.wins||0}W ${p.draws||0}D ${p.losses||0}L</div>
      </div>
      <button class="btn-sm ${p.isModerator?'btn-reject':'btn-mod'}" onclick="adminToggleMod('${p.id}','${p.name}',${!!p.isModerator})">
        ${p.isModerator?'Remove Mod':'Give Mod'}</button>
    </div>`).join(''):'<div class="empty-state"><div class="empty-text">No active players</div></div>';
}

function filterModPlayers(){if(S.adminPlayers.length)renderModPlayers(S.adminPlayers);}

async function adminToggleMod(id,name,isMod){
  const nv=!isMod;
  await updateDoc(doc(db,'players',id),{isModerator:nv});
  T(name+(nv?' is now a Moderator':' mod removed'),nv?'success':'info');
  if(S.user&&S.user.id===id){S.user.isModerator=nv;updateHeaderAuth();}
  loadAdminPanel('moderators');
}

async function adminApprove(id){await updateDoc(doc(db,'players',id),{status:'active'});T('Player approved','success');loadAdminPanel('pending');}
async function adminReject(id){if(!confirm('Reject and delete this registration?'))return;await deleteDoc(doc(db,'players',id));T('Rejected','info');loadAdminPanel('pending');}

function adminEditPlayer(id,div,cat,wins,draws,losses,gf,ga,cs,cmp,cpts,status,name){
  $('editPlayerId').value=id;$('editPlayerName').value=name||'';
  $('editDivision').value=div;$('editCategory').value=cat;
  $('editWins').value=wins;$('editDraws').value=draws;$('editLosses').value=losses;
  $('editGF').value=gf;$('editGA').value=ga;$('editCS').value=cs;
  $('editCycleMP').value=cmp;$('editCyclePts').value=cpts;$('editStatus').value=status;
  $('editPlayerPw').value='';
  openModal('editPlayerModal');
}

async function savePlayerEdit(){
  const id=$('editPlayerId').value,div=parseInt($('editDivision').value);
  const newName=($('editPlayerName').value||'').trim();
  const cat=$('editCategory').value;
  const wins=parseInt($('editWins').value),draws=parseInt($('editDraws').value),losses=parseInt($('editLosses').value);
  const gf=parseInt($('editGF').value),ga=parseInt($('editGA').value),cs=parseInt($('editCS').value);
  const cmp=parseInt($('editCycleMP').value),cpts=parseInt($('editCyclePts').value);
  const status=$('editStatus').value;
  const newPw=($('editPlayerPw').value||'').trim();
  if(div<1||div>9)return T('Division 1-9 only','error');
  if(!newName)return T('Player name cannot be empty','error');
  if(newPw&&newPw.length<4)return T('Password must be at least 4 characters','error');
  try{
    // Check if name already taken by another player
    if(newName){
      const existing=await getDocs(query(collection(db,'players'),where('name','==',newName)));
      const conflict=existing.docs.find(d=>d.id!==id);
      if(conflict)return T('Name "'+newName+'" is already taken','error');
    }
    const updates={name:newName,division:div,category:cat,wins,draws,losses,goalsFor:gf,goalsAgainst:ga,cleanSheets:cs,cycleMP:cmp,cyclePts:cpts,status};
    if(newPw)updates.password=newPw;
    await updateDoc(doc(db,'players',id),updates);
    T('Player updated'+(newPw?' + password changed':''),'success');
    closeModal('editPlayerModal');loadAdminPanel('players');
  }catch(e){T('Error: '+e.message,'error');}
}

async function adminToggleBan(id,name,cs){const ns=cs==='banned'?'active':'banned';await updateDoc(doc(db,'players',id),{status:ns});T(name+' '+ns,'info');loadAdminPanel('players');}
async function adminTogglePOTD(id,n,c){await updateDoc(doc(db,'players',id),{isPOTD:!c});T(n+(!c?' POTD set':'POTD removed'),'success');loadAdminPanel('players');}
async function adminTogglePOTW(id,n,c){await updateDoc(doc(db,'players',id),{isPOTW:!c});T(n+(!c?' POTW set':'POTW removed'),'success');loadAdminPanel('players');}
async function adminTogglePOTM(id,n,c){await updateDoc(doc(db,'players',id),{isPOTM:!c});T(n+(!c?' POTM set':'POTM removed'),'success');loadAdminPanel('players');}
async function adminTogglePOTS(id,n,c){await updateDoc(doc(db,'players',id),{isPOTS:!c});T(n+(!c?' POTS set':'POTS removed'),'success');loadAdminPanel('players');}

function adminEditMatch(id,nA,nB,sA,sB,status){
  $('editMatchId').value=id;$('editMatchInfo').textContent=`${nA} vs ${nB}`;
  $('editScoreA').value=sA;$('editScoreB').value=sB;$('editMatchStatus').value=status;
  openModal('editMatchModal');
}

async function adminConfirmMatch(matchId){
  const mRef=doc(db,'matches',matchId),mSnap=await getDoc(mRef);
  if(!mSnap.exists())return;
  await updateDoc(mRef,{status:'confirmed',confirmedAt:serverTimestamp()});
  await applyMatchStats({...mSnap.data(),id:matchId});
  T('Match confirmed by admin','success');S.matches=[];loadAdminPanel('adminMatches');
}

async function saveMatchEdit(){
  const id=$('editMatchId').value,sA=parseInt($('editScoreA').value),sB=parseInt($('editScoreB').value);
  const status=$('editMatchStatus').value;
  try{
    // If changing to confirmed from pending, also apply stats
    const mRef=doc(db,'matches',id);
    const old=await getDoc(mRef);
    await updateDoc(mRef,{scoreA:sA,scoreB:sB,status});
    if(status==='confirmed'&&old.data().status!=='confirmed'){
      const m={...old.data(),scoreA:sA,scoreB:sB,id};
      await applyMatchStats(m);
    }
    T('Match updated','success');closeModal('editMatchModal');S.matches=[];loadAdminPanel('adminMatches');
  }catch(e){T('Error: '+e.message,'error');}
}

async function adminDeleteMatch(){
  const id=$('editMatchId').value;
  if(!confirm('Delete this match permanently?'))return;
  await deleteDoc(doc(db,'matches',id));
  T('Match deleted','info');closeModal('editMatchModal');S.matches=[];loadAdminPanel('adminMatches');
}

async function adminDeleteMatchDirect(id){
  if(!confirm('Delete this match?'))return;
  await deleteDoc(doc(db,'matches',id));
  // NOTE: Since stats are computed live from history, no need to reverse stats
  T('Match deleted. Ranking will update automatically.','info');
  S.matches=[];loadAdminPanel('adminMatches');
}

async function saveSeasonSettings(){
  const name=$('seasonName')?.value||'Season 1';
  const startDate=$('seasonStart').value;
  const endDate=$('seasonEnd').value;
  if(!startDate||!endDate)return T('Set start and end dates','error');
  try{
    const snap=await getDoc(doc(db,'settings','season'));
    const existing=snap.exists()?snap.data():{};
    await setDoc(doc(db,'settings','season'),{
      ...existing, name, startDate, endDate,
      updatedAt:serverTimestamp()
    },{merge:true});
    T('Season settings saved','success');
    loadSeasonInfo();
  }catch(e){T('Error: '+e.message,'error');}
}

async function loadSeasonInfo(){
  try{
    const snap=await getDoc(doc(db,'settings','season'));
    const el=$('currentSeasonInfo');
    if(!el)return;
    if(snap.exists()){
      const d=snap.data();
      const now=new Date();
      const start=d.startDate?new Date(d.startDate):null;
      const end=d.endDate?new Date(d.endDate):null;
      const daysLeft=end?Math.max(0,Math.ceil((end-now)/86400000)):null;
      el.innerHTML=`
        <div style="font-weight:700;color:var(--ucl-star)">${d.name||'No season set'}</div>
        <div>Start: ${d.startDate||'-'} &nbsp;|&nbsp; End: ${d.endDate||'-'}</div>
        ${daysLeft!==null?`<div style="color:#00E676;margin-top:4px">${daysLeft} days remaining</div>`:''}
      `;
    } else {
      el.innerHTML='<div style="color:#4472C4">No active season configured</div>';
    }
    // Load past seasons
    await loadPastSeasons();
  }catch(e){console.error(e);}
}

async function loadPastSeasons(){
  const el=$('pastSeasonsList');
  if(!el)return;
  try{
    const snap=await getDocs(collection(db,'pastSeasons'));
    const seasons=snap.docs.map(d=>({id:d.id,...d.data()}))
      .sort((a,b)=>(b.endedAt?.seconds||0)-(a.endedAt?.seconds||0));
    if(!seasons.length){el.innerHTML='<div class="text-gray text-sm">No past seasons yet</div>';return;}
    el.innerHTML=seasons.map(s=>`
      <div style="padding:10px;border:1px solid var(--ucl-border);border-radius:6px;margin-bottom:8px">
        <div style="font-family:'Bebas Neue',sans-serif;font-size:16px;letter-spacing:2px;color:var(--ucl-star)">${s.name||'Season'}</div>
        <div class="text-gray text-sm">${s.startDate||''} to ${s.endDate||''}</div>
        ${s.topPlayer?`<div style="font-size:12px;color:#00E676;margin-top:4px">Top: ${s.topPlayer}</div>`:''}
        ${s.potd?`<div style="font-size:11px;color:#CE93D8">POTD: ${s.potd} | POTW: ${s.potw||'-'} | POTM: ${s.potm||'-'}</div>`:''}
      </div>`).join('');
  }catch(e){el.innerHTML='<div class="text-gray text-sm">Error loading past seasons</div>';}
}

async function endCurrentSeason(){
  if(!confirm('End current season and archive all stats?\n\nThis will:\n- Save season record to archive\n- Reset all cycle data\n- Keep player divisions\n\nOK to confirm.'))return;
  try{
    // Get current season info
    const seasonSnap=await getDoc(doc(db,'settings','season'));
    const seasonData=seasonSnap.exists()?seasonSnap.data():{name:'Season',startDate:'',endDate:''};

    // Get current top players for archive
    const pSnap=await getDocs(collection(db,'players'));
    const players=pSnap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
    const mSnap=await getDocs(collection(db,'matches'));
    const matches=mSnap.docs.map(d=>({id:d.id,...d.data()})).filter(m=>m.status==='confirmed');

    // Find top performers
    const sorted=players.map(p=>{
      const pm=matches.filter(m=>m.playerAId===p.id||m.playerBId===p.id);
      const w=p.wins||0,d2=p.draws||0,l=p.losses||0;
      const rating=(DIV_RULES[p.division||9]||{}).useRating?(p.eloRating||1200):Math.max(0,w*10+d2*5+l*(-5)+((p.goalsFor||0)-(p.goalsAgainst||0))+(p.cleanSheets||0)*2);
      return{...p,rating,mp:pm.length};
    }).sort((a,b)=>b.rating-a.rating);

    const topPlayer=sorted[0]?.name||'-';
    const topActive=[...players].sort((a,b)=>{
      const ma=matches.filter(m=>m.playerAId===a.id||m.playerBId===a.id).length;
      const mb=matches.filter(m=>m.playerAId===b.id||m.playerBId===b.id).length;
      return mb-ma;
    })[0]?.name||'-';

    // Find players with POTD/POTW/POTM
    const potd=players.find(p=>p.isPOTD)?.name||'-';
    const potw=players.find(p=>p.isPOTW)?.name||'-';
    const potm=players.find(p=>p.isPOTM)?.name||'-';

    // Archive season
    await addDoc(collection(db,'pastSeasons'),{
      name:seasonData.name||'Season',
      startDate:seasonData.startDate||'',
      endDate:seasonData.endDate||'',
      topPlayer, topActive, potd, potw, potm,
      playerCount:players.length,
      matchCount:matches.length,
      endedAt:serverTimestamp()
    });

    // Reset cycles but keep divisions
    await Promise.all(players.map(p=>updateDoc(doc(db,'players',p.id),{
      cycleMP:0,cyclePts:0,
      wins:0,draws:0,losses:0,goalsFor:0,goalsAgainst:0,cleanSheets:0,
      form:[],isPOTD:false,isPOTW:false,isPOTM:false,isPOTS:false,
      mostActiveD:0,mostActiveW:0,mostActiveM:0
    })));

    // Archive matches
    await Promise.all(mSnap.docs.map(d=>deleteDoc(doc(db,'matches',d.id))));

    // Clear season award data but keep settings
    await updateDoc(doc(db,'settings','season'),{lastEndedAt:serverTimestamp()}).catch(()=>{});

    S.players=[];S.matches=[];
    T('Season ended and archived!','success');
    loadSeasonInfo();
    // Post a news item
    await postSystemNews(`Season "${seasonData.name}" has ended! Winner: ${topPlayer}. See you next season!`);
  }catch(e){T('Error: '+e.message,'error');console.error(e);}
}

// ===== AUTO AWARD FUNCTIONS =====
async function autoAwardPOTD(){
  // Top player in last 24h
  const winner=await getTopPlayerInWindow(86400000);
  if(!winner)return T('No matches in last 24h','info');
  await grantAward(winner.id,winner.name,'POTD','isPOTD','potdCount');
  await postSystemNews(`PLAYER OF THE DAY: ${winner.name} claimed the daily top spot!`);
  $('awardResult').textContent='POTD awarded to: '+winner.name;
  T('POTD awarded to '+winner.name,'success');
}

async function autoAwardPOTW(){
  const winner=await getTopPlayerInWindow(604800000);
  if(!winner)return T('No matches this week','info');
  await grantAward(winner.id,winner.name,'POTW','isPOTW','potwCount');
  await postSystemNews(`PLAYER OF THE WEEK: ${winner.name} dominated the weekly rankings!`);
  $('awardResult').textContent='POTW awarded to: '+winner.name;
  T('POTW awarded to '+winner.name,'success');
}

async function autoAwardPOTM(){
  const winner=await getTopPlayerInWindow(2592000000);
  if(!winner)return T('No matches this month','info');
  await grantAward(winner.id,winner.name,'POTM','isPOTM','potmCount');
  await postSystemNews(`PLAYER OF THE MONTH: ${winner.name} is the standout performer this month!`);
  $('awardResult').textContent='POTM awarded to: '+winner.name;
  T('POTM awarded to '+winner.name,'success');
}

async function autoAwardPOTS(){
  // Top player overall
  const winner=await getTopPlayerInWindow(Infinity);
  if(!winner)return T('No matches found','info');
  await grantAward(winner.id,winner.name,'POTS','isPOTS','potsCount');
  await postSystemNews(`PLAYER OF THE SEASON: ${winner.name} is crowned the season champion!`);
  $('awardResult').textContent='POTS awarded to: '+winner.name;
  T('POTS awarded to '+winner.name,'success');
}

async function autoAwardMostActive(){
  const mSnap=await getDocs(collection(db,'matches'));
  const matches=mSnap.docs.map(d=>({id:d.id,...d.data()})).filter(m=>m.status==='confirmed');
  const pSnap=await getDocs(collection(db,'players'));
  const players=pSnap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
  const now=Date.now();

  // Day
  const dayM=matches.filter(m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<86400000);
  const weekM=matches.filter(m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<604800000);
  const monthM=matches.filter(m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<2592000000);

  const countFor=(ms,pid)=>ms.filter(m=>m.playerAId===pid||m.playerBId===pid).length;
  const topFor=(ms)=>players.reduce((best,p)=>{
    const c=countFor(ms,p.id);return c>best.count?{...p,count:c}:best;
  },{count:0});

  const dayTop=topFor(dayM),weekTop=topFor(weekM),monthTop=topFor(monthM);

  const updates=[];
  if(dayTop.count>0){
    await grantAward(dayTop.id,dayTop.name,'Most Active Day','isMostActiveD','mostActiveDCount');
    updates.push('Day: '+dayTop.name+' ('+dayTop.count+'m)');
  }
  if(weekTop.count>0){
    await grantAward(weekTop.id,weekTop.name,'Most Active Week','isMostActiveW','mostActiveWCount');
    updates.push('Week: '+weekTop.name+' ('+weekTop.count+'m)');
  }
  if(monthTop.count>0){
    await grantAward(monthTop.id,monthTop.name,'Most Active Month','isMostActiveM','mostActiveMCount');
    updates.push('Month: '+monthTop.name+' ('+monthTop.count+'m)');
  }
  $('awardResult').textContent='Most Active: '+updates.join(' | ');
  if(dayTop.count>0)await postSystemNews(`MOST ACTIVE: ${dayTop.name} leads with ${dayTop.count} matches today!`);
  T('Most Active badges awarded','success');
}

async function getTopPlayerInWindow(windowMs){
  const [pSnap,mSnap]=await Promise.all([
    getDocs(collection(db,'players')),
    getDocs(collection(db,'matches'))
  ]);
  const players=pSnap.docs.map(d=>({id:d.id,...d.data()})).filter(p=>p.status==='active');
  const matches=mSnap.docs.map(d=>({id:d.id,...d.data()})).filter(m=>m.status==='confirmed');
  const now=Date.now();
  const filtered=windowMs===Infinity?matches:matches.filter(m=>now-(m.createdAt?.toDate?.()?.getTime()||0)<windowMs);
  const playerCatMap={};players.forEach(p=>playerCatMap[p.id]=p.category||'Main');

  let best=null,bestRating=-Infinity;
  for(const p of players){
    const pm=filtered.filter(m=>m.playerAId===p.id||m.playerBId===p.id);
    if(!pm.length)continue;
    let w=0,d=0,l=0,gf=0,ga=0,cs=0;
    pm.forEach(m=>{
      const side=m.playerAId===p.id?'A':'B';
      const res=getRC(m.scoreA,m.scoreB,side);
      const myG=side==='A'?m.scoreA:m.scoreB,opG=side==='A'?m.scoreB:m.scoreA;
      const oppCat=playerCatMap[side==='A'?m.playerBId:m.playerAId]||'Main';
      const mult=getRatingMultiplier(p.category||'Main',oppCat,res);
      if(res==='W')w+=mult;else if(res==='D')d++;else l+=mult;
      gf+=myG;ga+=opG;if(opG===0)cs++;
    });
    const r=Math.max(0,w*10+d*5+l*(-5)+(gf-ga)+cs*2);
    if(r>bestRating){bestRating=r;best={...p,windowRating:r};}
  }
  return best;
}

async function grantAward(pid,name,awardLabel,field,countField){
  const ref=doc(db,'players',pid);
  const snap=await getDoc(ref);
  if(!snap.exists())return;
  const current=snap.data()[countField]||0;
  const updates={[field]:true,[countField]:current+1};
  // Also clear award from previous holder
  const allSnap=await getDocs(collection(db,'players'));
  const clearOthers=allSnap.docs
    .filter(d=>d.id!==pid&&d.data()[field])
    .map(d=>updateDoc(doc(db,'players',d.id),{[field]:false}));
  await Promise.all([updateDoc(ref,updates),...clearOthers]);
}

async function postSystemNews(text){
  try{
    await addDoc(collection(db,'systemNews'),{
      text, createdAt:serverTimestamp(), type:'award'
    });
  }catch(e){console.error('News post failed:',e);}
}

async function loadSystemNews(){
  try{
    const snap=await getDocs(collection(db,'systemNews'));
    const items=snap.docs.map(d=>({id:d.id,...d.data()}))
      .sort((a,b)=>(b.createdAt?.seconds||0)-(a.createdAt?.seconds||0))
      .slice(0,10);
    if(!items.length)return;
    // Merge with existing news
    const existing=$('newsText').textContent;
    const newsItems=items.map(n=>n.text).join('     |     ');
    $('newsText').textContent=newsItems+(existing?' |  '+existing:'');
    $('newsTicker').style.display='flex';
  }catch(e){console.error(e);}
}

async function confirmSeasonReset(){
  if(!confirm('RESET ENTIRE SEASON?\n\nAll matches deleted, all stats reset. Player accounts remain.\n\nOK to confirm.'))return;
  try{
    const [pSnap,mSnap]=await Promise.all([getDocs(collection(db,'players')),getDocs(collection(db,'matches'))]);
    await Promise.all([
      ...pSnap.docs.map(d=>updateDoc(doc(db,'players',d.id),{wins:0,draws:0,losses:0,goalsFor:0,goalsAgainst:0,cleanSheets:0,form:[],division:9,cycleMP:0,cyclePts:0,highestDivision:9})),
      ...mSnap.docs.map(d=>deleteDoc(doc(db,'matches',d.id)))
    ]);
    S.players=[];S.matches=[];T('Season reset complete!','success');
  }catch(e){T('Error: '+e.message,'error');}
}

async function changeAdminPassword(){
  const pw=$('newAdminPw').value,pw2=$('confirmAdminPw').value;
  if(!pw||pw.length<4)return T('Password too short','error');
  if(pw!==pw2)return T('Passwords do not match','error');
  try{await setDoc(doc(db,'settings','admin'),{password:pw},{merge:true});S.adminPw=pw;T('Admin password updated','success');$('newAdminPw').value='';$('confirmAdminPw').value='';}catch(e){T('Error','error');}
}

function switchAdminTab(tab,btn){
  document.querySelectorAll('.admin-tab').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  document.querySelectorAll('[id^="adminTab-"]').forEach(el=>el.style.display='none');
  $('adminTab-'+tab).style.display='block';
  loadAdminPanel(tab);
}

// ===== EXPOSE =====
Object.assign(window,{
  navTo,navBack,setNavActive,setMobActive,openModal,closeModal,
  doLogin,doRegister,doLogout,changeMyPassword,
  switchLbTab,filterLeaderboard,filterMatches,confirmMatch,
  submitMatchResult,loadSubmitPage,viewProfile,toggleRival,loadMyProfile,
  openRankingCardPreview,closeRankingPreview,downloadRankingCard,
  adminLogin,loadAdminPanel,switchAdminTab,adminApprove,adminReject,
  adminEditPlayer,savePlayerEdit,adminToggleBan,adminToggleMod,
  adminTogglePOTD,adminTogglePOTW,adminTogglePOTM,adminTogglePOTS,
  adminEditMatch,saveMatchEdit,adminDeleteMatch,adminDeleteMatchDirect,
  adminConfirmMatch,filterAdminPlayers,filterModPlayers,
  confirmSeasonReset,endCurrentSeason,changeAdminPassword,loadModPanel,
  saveSeasonSettings,autoAwardPOTD,autoAwardPOTW,autoAwardPOTM,autoAwardPOTS,autoAwardMostActive
});

// INIT
updateHeaderAuth();loadHome();
document.querySelectorAll('.modal-overlay').forEach(m=>{
  m.addEventListener('click',e=>{if(e.target===m)m.classList.remove('open');});
});
</script>
</body>
</html>
