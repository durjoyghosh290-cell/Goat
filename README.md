<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Durjay Ghosh — Craft Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=VT323&family=Teko:wght@500;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --font-pixel:'Press Start 2P', monospace;
  --font-mono:'VT323', monospace;
  --font-head:'Teko', sans-serif;
  --glass-bg: rgba(10,6,14,0.35);
  --glass-border: rgba(255,110,170,0.22);
  --emerald:#20e56f;
  --emerald-dark:#0b8f3f;
  --gold:#ffd94a;
  --hp-red:#ff5a5a;
  --xp-green:#8dff3a;
  --text-cream:#f3efdd;
  --accent: #b57bff;
  --val-red:#ff4655;
  /* ===== Vice City palette ===== */
  --vc-magenta:#7a1257;
  --vc-pink:#ff2e92;
  --vc-hotpink:#ff5fa8;
  --vc-orange:#ff6a3d;
  --vc-slate:#0c0810;
  --vc-slate2:#150c1c;
}
*{box-sizing:border-box;}
html,body{margin:0;padding:0;height:100%;overflow:hidden;font-family:var(--font-mono);}
body{
  background:
    radial-gradient(ellipse at 15% 100%, rgba(255,106,61,.25), transparent 55%),
    linear-gradient(165deg, #1a0a20 0%, #3a0f3a 28%, #7a1257 52%, #b6236f 72%, #ff6a3d 100%);
  color:var(--text-cream);
}
button{font-family:inherit;cursor:pointer;}
::selection{background:var(--vc-pink);color:#000;}

/* ============ GLOBAL AMBIENT BACKGROUND ============ */
#bg-skyline{position:fixed; inset:0; z-index:-4; width:100%; height:100%;}
#bg-skyline svg{width:100%; height:100%; display:block;}
#bg-canvas{position:fixed; inset:0; z-index:-3; width:100%; height:100%;}
#bg-video{position:fixed; inset:0; z-index:-2; width:100%; height:100%; object-fit:cover; display:none; filter:brightness(.55) saturate(1.15);}
#bg-tint{position:fixed; inset:0; z-index:-1; transition:background 1.1s ease; background:radial-gradient(ellipse at 50% 15%, rgba(255,95,168,.20), rgba(10,6,16,.7) 75%);}

/* ============ GLASS PANEL SYSTEM ============ */
.glass{
  background:var(--glass-bg);
  border:1px solid var(--glass-border);
  backdrop-filter: blur(22px) saturate(150%);
  -webkit-backdrop-filter: blur(22px) saturate(150%);
  box-shadow: 0 10px 40px rgba(0,0,0,.5), inset 0 0 0 1px rgba(255,255,255,.04);
  border-radius:6px;
}
/* ===== ultra-soft "breathing" panel — a slow ambient pulse, never dips toward invisible ===== */
@keyframes panelBreathe{
  0%,100%{box-shadow: 0 10px 40px rgba(0,0,0,.5), inset 0 0 0 1px rgba(255,255,255,.04), 0 0 0 rgba(181,123,255,0);}
  50%{box-shadow: 0 10px 44px rgba(0,0,0,.45), inset 0 0 0 1px rgba(255,255,255,.07), 0 0 30px rgba(181,123,255,.12);}
}
.glow-emerald{box-shadow: 0 0 24px rgba(32,229,111,.35), 0 10px 40px rgba(0,0,0,.55);}
.glow-purple{box-shadow: 0 0 24px rgba(255,46,146,.35), 0 10px 40px rgba(0,0,0,.55);}
.glow-gold{box-shadow: 0 0 24px rgba(255,217,74,.35), 0 10px 40px rgba(0,0,0,.55);}

/* ===== animated border pulse — kept only on the few large panels, not on every repeated card (many blurred+animated cards at once caused jank/lag on About Me) ===== */
@keyframes borderPulse{
  0%,100%{border-color: rgba(255,110,170,.2);}
  50%{border-color: rgba(255,106,61,.65);}
}
.glass{
  animation: borderPulse 9s ease-in-out infinite, panelBreathe 7s ease-in-out infinite;
}

/* ===== staggered entrance — subtle slide only, never fades to invisible ===== */
.rise-in{ animation-name: riseIn; animation-duration:.9s; animation-timing-function: cubic-bezier(.22,.85,.32,1); animation-fill-mode:both; }
@keyframes riseIn{0%{transform:translateY(14px);} 100%{transform:translateY(0);}}

/* ===== gentle continuous glow breathing on text & key elements — text NEVER dims below full opacity, only the glow intensity breathes, like a slow ASMR pulse ===== */
@keyframes textGlowBreathe{
  0%,100%{text-shadow:0 0 6px rgba(255,255,255,.18), 0 0 2px rgba(255,255,255,.25);}
  50%{text-shadow:0 0 22px rgba(255,95,168,.85), 0 0 8px rgba(255,255,255,.5), 0 0 42px rgba(255,106,61,.4);}
}
.ench-name, .adv-title, .about-item b, .trade-give, .exp-card b{
  animation: textGlowBreathe 6s ease-in-out infinite;
}
.screen h2{ animation: textGlowBreathe 6s ease-in-out infinite; }
.screen h1{ animation: heroGlowBreathe 6s ease-in-out infinite; }
@keyframes heroGlowBreathe{
  0%,100%{text-shadow:0 2px 12px rgba(0,0,0,.8), 0 0 10px rgba(255,255,255,.15);}
  50%{text-shadow:0 2px 12px rgba(0,0,0,.8), 0 0 34px rgba(255,106,61,.85), 0 0 64px rgba(255,46,146,.4);}
}

/* ===== animated underline under every h2 ===== */
.screen h2{position:relative; display:inline-block; padding-bottom:10px;}
.screen h2::after{
  content:""; position:absolute; left:50%; bottom:0; width:0; height:3px; border-radius:3px;
  background:linear-gradient(90deg,var(--vc-pink),var(--vc-orange),var(--gold));
  transform:translateX(-50%);
  animation: underlineDraw .8s .25s ease forwards;
}
@keyframes underlineDraw{to{width:65%;}}

/* ===== shine sweep on buttons ===== */
.pixel-btn{position:relative; overflow:hidden;}
.pixel-btn::before{
  content:""; position:absolute; top:0; left:-60%; width:35%; height:100%;
  background:linear-gradient(120deg, transparent, rgba(255,255,255,.4), transparent);
  transform:skewX(-20deg);
}
.pixel-btn:hover::before{ animation: shineSweep .7s ease; }
@keyframes shineSweep{from{left:-60%;} to{left:130%;}}

/* small "open project" badge on chest slots that link out */
.link-badge{
  position:absolute; top:3px; right:4px; font-size:9px; color:var(--emerald);
  text-shadow:0 0 6px var(--emerald); animation: linkPulse 2.6s ease-in-out infinite;
}
@keyframes linkPulse{0%,100%{opacity:.5;} 50%{opacity:1;}}

.pixel-btn{
  background:rgba(255,255,255,.06);
  border:1px solid var(--glass-border);
  backdrop-filter: blur(8px);
  color:#fff;
  font-family:var(--font-pixel);
  padding:12px 20px;
  font-size:11px;
  letter-spacing:1px;
  border-radius:4px;
  transition: transform .15s, background .15s, box-shadow .15s;
}
.pixel-btn:hover{background:rgba(255,255,255,.18); transform:translateY(-2px); box-shadow:0 6px 18px rgba(0,0,0,.4);}
.pixel-btn:active{transform:translateY(1px) scale(.97);}
.pixel-btn.emerald-btn{background:rgba(32,229,111,.22); border-color:rgba(32,229,111,.6); color:#c9ffdf;}
.pixel-btn.emerald-btn:hover{background:rgba(32,229,111,.36);}

/* ============ APP SHELL ============ */
#app{position:relative;width:100vw;height:100vh;overflow:hidden;}

.screen{
  position:absolute; inset:0;
  display:none;
  flex-direction:column;
  align-items:center;
  justify-content:center;
  padding:90px 40px 130px;
  overflow-y:auto;
}
.screen.active{display:flex;}
.screen h1,.screen h2{font-family:var(--font-head); text-shadow:0 2px 12px rgba(0,0,0,.8); text-align:center; letter-spacing:1px;}
.screen h1{
  font-size:clamp(34px,5.5vw,60px); font-weight:600; text-transform:uppercase; line-height:1;
  background:linear-gradient(180deg,#fff 0%,#ffe3d6 35%,var(--vc-orange) 70%,var(--vc-pink) 100%);
  -webkit-background-clip:text; background-clip:text; -webkit-text-fill-color:transparent; color:#fff;
  filter:drop-shadow(0 3px 14px rgba(0,0,0,.7));
}
.screen h2{font-size:clamp(22px,2.6vw,32px); font-weight:600; text-transform:uppercase; color:var(--gold); margin-bottom:26px; letter-spacing:2px;}
.screen p, .screen li{font-family:var(--font-mono); font-size:clamp(17px,1.3vw,21px); line-height:1.55;}
.screen .content{position:relative; z-index:1; max-width:min(1600px,96vw); width:100%;}

/* per-screen tint colors, applied to #bg-tint via JS */
/* hero:#2a5c3a  about:#123a5c  skills:#3a1a52  projects:#4a3016  experience:#2b2620
   achievements:#4a3a00  services:#1f3d1a  contact:#2a1a3d  outro:#0a0620 */

/* ============ TRANSITION FX ============ */
#transition-fx{
  position:fixed; inset:0; z-index:150; pointer-events:none;
  background: radial-gradient(circle at 50% 50%, var(--accent) 0%, transparent 70%);
  clip-path: circle(0% at 50% 50%);
  opacity:0;
}
#transition-fx.firing{
  animation: portalWipe .6s ease forwards;
}
@keyframes portalWipe{
  0%{clip-path:circle(0% at 50% 50%); opacity:.95;}
  45%{clip-path:circle(75% at 50% 50%); opacity:.85;}
  100%{clip-path:circle(150% at 50% 50%); opacity:0;}
}
.screen.leaving{
  animation: screenLeave .35s ease forwards;
}
.screen.entering{
  animation: screenEnter .5s cubic-bezier(.2,.9,.25,1.15) forwards;
}
@keyframes screenLeave{
  0%{opacity:1; transform:scale(1);}
  100%{opacity:0; transform:scale(1.08);}
}
@keyframes screenEnter{
  0%{opacity:0; transform:scale(.94) translateY(24px);}
  60%{opacity:1; transform:scale(1.01) translateY(-3px);}
  100%{opacity:1; transform:scale(1) translateY(0);}
}

/* ============ HUD — LEVEL / XP SYSTEM ============ */
#hud-top{
  position:fixed; top:16px; left:0; right:0;
  display:flex; flex-direction:column; align-items:center; gap:6px;
  z-index:50; pointer-events:none;
}
#xp-cluster{display:flex; align-items:center; gap:12px;}
#level-badge{
  position:relative; width:46px; height:46px; border-radius:50%;
  background:radial-gradient(circle at 35% 30%, rgba(141,255,58,.35), rgba(10,20,10,.85) 70%);
  border:2px solid var(--xp-green);
  display:flex; align-items:center; justify-content:center;
  font-family:var(--font-pixel); font-size:9px; color:#fff; line-height:1.3; text-align:center;
  box-shadow:0 0 16px rgba(141,255,58,.5);
  animation: levelBadgeBreathe 5s ease-in-out infinite;
}
#level-badge span{display:block; font-size:15px; color:var(--xp-green); text-shadow:0 0 8px rgba(141,255,58,.8);}
@keyframes levelBadgeBreathe{0%,100%{box-shadow:0 0 14px rgba(141,255,58,.4);} 50%{box-shadow:0 0 26px rgba(141,255,58,.85);}}
#level-badge.level-up-flash{ animation: levelUpPop .7s ease; }
@keyframes levelUpPop{
  0%{transform:scale(1); box-shadow:0 0 14px rgba(141,255,58,.4);}
  35%{transform:scale(1.35); box-shadow:0 0 46px rgba(255,217,74,1), 0 0 20px rgba(141,255,58,1);}
  100%{transform:scale(1); box-shadow:0 0 14px rgba(141,255,58,.4);}
}
#xp-bar-wrap{
  width:min(360px,48vw); height:16px; background:rgba(0,0,0,.55);
  border:1px solid var(--glass-border); border-radius:9px; position:relative; overflow:hidden;
}
#xp-bar-fill{height:100%; width:0%; background:linear-gradient(90deg,#8dff3a,#20e56f); transition:width .5s ease; box-shadow:0 0 12px rgba(141,255,58,.6);}
#xp-bar-text{
  position:absolute; inset:0; display:flex; align-items:center; justify-content:center;
  font-family:var(--font-pixel); font-size:9px; color:#fff; text-shadow:0 1px 4px rgba(0,0,0,.9); letter-spacing:.5px;
}
#xp-bar-wrap.level-up-flash::after{
  content:""; position:absolute; inset:0; border-radius:9px;
  animation: xpBarFlash .7s ease;
}
@keyframes xpBarFlash{
  0%{box-shadow:inset 0 0 0 2px rgba(255,217,74,0);}
  40%{box-shadow:inset 0 0 0 2px rgba(255,217,74,1), 0 0 26px rgba(255,217,74,.9);}
  100%{box-shadow:inset 0 0 0 2px rgba(255,217,74,0);}
}

/* ============ RETRO SOUND TOGGLE ============ */
#sound-toggle{
  position:fixed; top:16px; right:16px; z-index:55;
  display:flex; align-items:center; gap:8px;
  background:linear-gradient(160deg,rgba(255,46,146,.14),rgba(10,6,14,.9));
  border:1px solid rgba(255,110,170,.35); border-radius:8px;
  padding:8px 12px; cursor:pointer; color:#fff;
  font-family:var(--font-pixel); font-size:8px; letter-spacing:1px;
  transition: border-color .2s, box-shadow .2s;
}
#sound-toggle:hover{border-color:var(--vc-pink); box-shadow:0 0 16px rgba(255,46,146,.4);}
.st-bars{display:flex; align-items:flex-end; gap:2px; height:14px;}
.st-bars i{display:block; width:3px; background:linear-gradient(0deg,var(--vc-orange),var(--vc-pink)); border-radius:1px; animation: eqBounce 1s ease-in-out infinite;}
.st-bars i:nth-child(1){height:40%; animation-delay:0s;}
.st-bars i:nth-child(2){height:100%; animation-delay:.15s;}
.st-bars i:nth-child(3){height:65%; animation-delay:.3s;}
.st-bars i:nth-child(4){height:85%; animation-delay:.45s;}
@keyframes eqBounce{0%,100%{transform:scaleY(.4);} 50%{transform:scaleY(1);}}
#sound-toggle.muted .st-bars i{animation-play-state:paused; opacity:.3; transform:scaleY(.2);}

/* ============ HOTBAR ============ */
#hotbar-wrap{
  position:fixed; bottom:22px; left:50%; transform:translateX(-50%);
  z-index:60; display:flex; gap:6px; padding:8px;
  border-radius:12px;
}
.hotbar-slot{
  position:relative;
  width:60px; height:60px;
  background:rgba(255,255,255,.06);
  border:1px solid var(--glass-border);
  border-radius:8px;
  display:flex; align-items:center; justify-content:center;
  font-size:26px;
  transition:transform .18s cubic-bezier(.3,1.5,.5,1), background .18s, box-shadow .18s;
}
.hotbar-slot .num{
  position:absolute; top:2px; left:6px; font-family:'Segoe UI', Arial, sans-serif; font-weight:600; font-size:12px; color:#fff; opacity:.8;
}
.hotbar-slot.selected{
  background:rgba(181,123,255,.28);
  border-color: var(--accent);
  box-shadow:0 0 22px rgba(181,123,255,.55);
  transform:translateY(-8px) scale(1.06);
}
.hotbar-slot:hover{transform:translateY(-5px); background:rgba(255,255,255,.14);}
.tooltip{
  position:absolute; bottom:74px; left:50%; transform:translateX(-50%);
  background:rgba(10,5,20,.85); border:1px solid var(--accent); color:#fff;
  font-family:var(--font-pixel); font-size:10px; padding:7px 12px; border-radius:5px;
  white-space:nowrap; opacity:0; pointer-events:none; transition:opacity .15s, transform .15s;
  transform-origin:bottom center;
}
.hotbar-slot:hover .tooltip{opacity:1; transform:translateX(-50%) translateY(-4px);}

/* ============ TOASTS ============ */
#toast-wrap{position:fixed; top:70px; right:20px; z-index:80; display:flex; flex-direction:column; gap:10px;}
.toast{
  display:flex; align-items:center; gap:12px; padding:10px 18px;
  min-width:250px; font-family:var(--font-mono); font-size:17px;
  transform:translateX(140%) scale(.9); transition:transform .4s cubic-bezier(.2,.9,.3,1.3);
  border-left:3px solid var(--gold);
}
.toast.show{transform:translateX(0) scale(1);}
.toast .t-icon{font-size:28px;}
.toast .t-title{font-family:var(--font-pixel); font-size:9px; color:var(--gold); display:block; margin-bottom:4px;}

/* ============ HERO ============ */
.hero-block{
  width:120px;height:120px;margin:0 auto 22px;
  background:linear-gradient(135deg,#6cbf3a,#4c9a2a 60%,#3d7a20);
  border-radius:14px;
  box-shadow:0 0 40px rgba(108,191,58,.5), inset 0 0 30px rgba(0,0,0,.25);
}
.avatar-wrap{
  width:160px; height:160px; margin:0 auto 22px; position:relative; border-radius:50%;
}
.avatar-wrap::before{
  content:""; position:absolute; inset:-5px; border-radius:50%;
  background:conic-gradient(from 0deg, var(--accent), var(--emerald), var(--gold), var(--accent));
  animation: rotateRing 4s linear infinite; z-index:0;
}
.avatar-wrap img{
  position:relative; z-index:1; width:100%; height:100%; object-fit:cover; border-radius:50%;
  display:block; border:4px solid #0a0810; box-shadow:0 0 30px rgba(0,0,0,.6);
}
@keyframes rotateRing{to{transform:rotate(360deg);}}
.hero-sub{text-align:center; font-family:var(--font-pixel); font-size:clamp(11px,1.3vw,15px); color:#fffbe0; margin-top:8px;}
.hero-cta{margin-top:30px; text-align:center;}

/* ============ ABOUT ============ */
.book-panel{padding:32px 40px;}
.about-grid{display:grid; grid-template-columns:repeat(2,1fr); gap:16px; margin-top:16px;}
@media(min-width:900px){.about-grid{grid-template-columns:repeat(3,1fr);}}
@media(min-width:1400px){.about-grid{grid-template-columns:repeat(4,1fr);}}
@media(max-width:640px){.about-grid{grid-template-columns:1fr;}}

/* ===== About Me backdrop texture (decorative only — not an identity photo) ===== */
#screen-about{position:relative;}
.about-bg-texture{
  position:absolute; inset:0; z-index:0; overflow:hidden; pointer-events:none;
}
.about-bg-texture img{
  position:absolute; right:-4%; bottom:-6%; width:340px; max-width:38vw;
  opacity:.10; filter:grayscale(.7) contrast(1.1);
}
#screen-about .content{position:relative; z-index:1;}

/* ===== Favorite Player card ===== */
.fav-player-card{
  grid-column:1 / -1;
  display:flex; align-items:center; gap:16px;
  background:rgba(255,255,255,.055); border:1px solid var(--glass-border); border-radius:6px;
  padding:12px 16px;
}
.fav-player-card img{
  width:56px; height:56px; border-radius:8px; object-fit:cover; object-position:50% 15%;
  border:1px solid rgba(255,255,255,.2); flex-shrink:0;
}
.fav-player-card .fp-text b{display:block; color:#fff;}
.fav-player-card .fp-text small{color:rgba(255,255,255,.45); font-size:12px;}
.about-item{background:linear-gradient(160deg,rgba(20,10,26,.85),rgba(10,6,14,.85)); border:1px solid var(--glass-border); border-radius:6px; padding:12px 16px;}
.about-item b{color:var(--gold); font-family:var(--font-pixel); font-size:11px; display:block; margin-bottom:7px;}

/* ============ SKILLS ============ */
.ench-wrap{display:flex; flex-direction:column; gap:14px;}
@media(min-width:900px){.ench-wrap{display:grid; grid-template-columns:repeat(2,1fr); gap:14px 24px;}}
@media(min-width:1400px){.ench-wrap{grid-template-columns:repeat(3,1fr);}}
.ench-row{
  display:flex; align-items:center; gap:14px;
  padding:12px 18px; border-radius:6px;
  background:linear-gradient(160deg,rgba(255,46,146,.12),rgba(12,8,16,.85)); border:1px solid rgba(255,95,168,.4);
  transition:transform .2s, background .2s;
}
.ench-row:hover{transform:translateX(6px); background:linear-gradient(160deg,rgba(255,46,146,.2),rgba(12,8,16,.85));}
.ench-name{font-family:var(--font-pixel); font-size:11px; color:#e9d4ff; min-width:170px;}
.ench-bar-wrap{flex:1; height:14px; background:rgba(0,0,0,.4); border-radius:8px; overflow:hidden;}
.ench-bar-fill{height:100%; background:linear-gradient(90deg,#b57bff,#7a3fc9); border-radius:8px; transition:width 1s ease; animation: enchGlow 5s ease-in-out infinite;}
@keyframes enchGlow{0%,100%{box-shadow:0 0 8px rgba(181,123,255,.65);} 50%{box-shadow:0 0 26px rgba(181,123,255,1), 0 0 10px rgba(255,255,255,.7);}}
.ench-lv{font-family:var(--font-pixel); font-size:12px; color:var(--gold); min-width:48px; text-align:right; animation: pctGlow 5s ease-in-out infinite;}
@keyframes pctGlow{0%,100%{text-shadow:0 0 5px rgba(255,217,74,.55);} 50%{text-shadow:0 0 18px rgba(255,217,74,1), 0 0 6px #fff, 0 0 32px rgba(255,217,74,.6);}}

/* ============ PROJECTS ============ */
.chest-lid{width:100%; max-width:680px; margin:0 auto 14px; text-align:center; opacity:.75;}
.chest-grid{
  display:grid; grid-template-columns:repeat(auto-fit,minmax(140px,170px));
  justify-content:center;
  gap:16px; padding:20px; border-radius:10px;
  background:rgba(10,6,14,.4); border:1px solid rgba(255,106,61,.3);
}
.chest-slot{
  aspect-ratio:3/4; border-radius:8px; padding:14px 10px;
  background:linear-gradient(165deg,rgba(255,106,61,.10),rgba(10,6,14,.92));
  border:1px solid rgba(255,110,170,.3);
  display:flex; flex-direction:column; align-items:center; justify-content:center; gap:8px;
  font-size:34px; position:relative; cursor:pointer;
  transition:transform .2s, border-color .2s, box-shadow .2s;
}
.chest-slot:hover{transform:translateY(-5px) scale(1.04); border-color:var(--vc-pink); box-shadow:0 10px 28px rgba(255,46,146,.35);}
.mission-icon{font-size:30px; filter:drop-shadow(0 2px 6px rgba(0,0,0,.6));}
.mission-title{font-family:var(--font-head); font-weight:600; font-size:15px; letter-spacing:.5px; text-transform:uppercase; color:#fff; text-align:center; line-height:1.15;}
.mission-go{font-family:var(--font-pixel); font-size:8px; letter-spacing:1px; color:var(--vc-orange); text-shadow:0 0 8px rgba(255,106,61,.6);}
.chest-slot .tooltip{bottom:auto; top:-4px; transform:translate(-50%,-100%); white-space:normal; width:200px; font-size:9px; line-height:1.6;}
.chest-slot:hover .tooltip{transform:translate(-50%,-110%);}

/* ============ EXPERIENCE ============ */
.exp-card{background:linear-gradient(160deg,rgba(20,10,26,.85),rgba(10,6,14,.85)); border:1px solid var(--glass-border); border-radius:6px; padding:16px 18px; margin-bottom:14px;}
@media(min-width:900px){
  #exp-wrap{display:grid; grid-template-columns:repeat(2,1fr); gap:14px 20px;}
  #exp-wrap .exp-card{margin-bottom:0;}
}
@media(min-width:1400px){#exp-wrap{grid-template-columns:repeat(3,1fr);}}
.exp-card b{font-family:var(--font-pixel); font-size:12px; color:var(--gold);}
.stat-bar-wrap{height:16px; background:rgba(0,0,0,.4); border-radius:8px; margin-top:8px; overflow:hidden;}
.stat-bar-fill{height:100%; background:linear-gradient(90deg,#ffd94a,#c98a00); border-radius:8px; transition:width 1s ease; animation: statGlow 3.2s ease-in-out infinite;}
@keyframes statGlow{0%,100%{box-shadow:0 0 6px rgba(255,217,74,.6);} 50%{box-shadow:0 0 20px rgba(255,217,74,1);}}

/* ============ ACHIEVEMENTS ============ */
.adv-grid{display:grid; grid-template-columns:repeat(auto-fit,minmax(260px,1fr)); gap:14px;}
.adv-card{
  display:flex; gap:12px; align-items:center;
  background:linear-gradient(160deg,rgba(255,217,74,.10),rgba(12,8,16,.88)); border:1px solid rgba(255,217,74,.4); border-radius:8px;
  padding:12px 16px; transition:transform .2s;
}
.adv-card:hover{transform:translateY(-4px);}
.adv-icon{font-size:32px;}
.adv-title{font-family:var(--font-pixel); font-size:10px; color:var(--gold); margin-bottom:5px;}
.adv-desc{font-size:15px; color:#f5eecb;}

/* ============ SERVICES ============ */
.villager-head{
  width:76px;height:96px;margin:0 auto 16px;
  background:#5ba85b; border-radius:50% 50% 40% 40%/60% 60% 40% 40%;
  border:3px solid #2f5c2f; position:relative;
}
.villager-head::after{content:"";position:absolute; left:16px; top:36px; width:44px; height:28px; background:#3a7a2f; border-radius:50%;}
.trade-list{display:flex; flex-direction:column; gap:12px;}
@media(min-width:900px){.trade-list{display:grid; grid-template-columns:repeat(2,1fr); gap:12px 20px;}}
@media(min-width:1400px){.trade-list{grid-template-columns:repeat(3,1fr);}}
.trade-row{
  display:flex; align-items:center; justify-content:space-between; gap:12px;
  background:linear-gradient(160deg,rgba(32,229,111,.10),rgba(12,8,16,.88)); border:1px solid rgba(32,229,111,.4); border-radius:8px;
  padding:12px 18px; transition:transform .2s, background .2s;
}
.trade-row:hover{transform:translateX(6px) scale(1.01); background:linear-gradient(160deg,rgba(32,229,111,.18),rgba(12,8,16,.88));}
.trade-give{font-size:16px;}
.trade-cost{display:flex; align-items:center; gap:7px; font-family:var(--font-pixel); font-size:12px; color:var(--emerald);}
.emerald-gem{width:16px; height:16px; background:var(--emerald); clip-path:polygon(50% 0,100% 25%,100% 75%,50% 100%,0 75%,0 25%); box-shadow:0 0 6px var(--emerald);}

/* ============ CONTACT ============ */
.contact-form{display:flex; flex-direction:column; gap:12px; max-width:480px; margin:0 auto;}
.contact-form input, .contact-form textarea{
  font-family:var(--font-mono); font-size:17px; padding:11px 14px;
  background:rgba(255,255,255,.06); border:1px solid var(--glass-border); border-radius:6px; color:#fff;
}
.contact-form input:focus, .contact-form textarea:focus{outline:none; border-color:var(--accent); box-shadow:0 0 12px rgba(181,123,255,.4);}
.contact-form textarea{resize:vertical; min-height:100px;}
.contact-note{font-size:13px; opacity:.65; text-align:center; margin-top:10px;}

/* ============ OUTRO ============ */
#credits{max-height:64vh; overflow-y:auto; text-align:center;}
#credits .line{margin:10px 0; font-size:19px;}
#credits .big{font-family:var(--font-pixel); font-size:16px; color:var(--gold); margin:26px 0 12px;}

/* ============ F3 DEBUG ============ */
#f3{
  position:fixed; top:10px; left:10px; z-index:90;
  background:rgba(0,0,0,.6); color:#fff; font-family:var(--font-mono);
  font-size:14px; padding:10px 12px; line-height:1.5; display:none; pointer-events:none;
  border-left:2px solid #fff; border-radius:4px;
}
#f3.show{display:block;}

/* ============ MINING MINIGAME ============ */
#mine-overlay{
  position:fixed; inset:0; background:rgba(0,0,0,.65); backdrop-filter:blur(6px); z-index:120;
  display:none; align-items:center; justify-content:center; flex-direction:column;
}
#mine-overlay.show{display:flex;}
#mine-grid{display:grid; grid-template-columns:repeat(6,56px); grid-template-rows:repeat(4,56px); gap:6px; margin-top:16px;}
.ore-block{
  border-radius:6px; background:rgba(255,255,255,.1); border:1px solid var(--glass-border);
  display:flex; align-items:center; justify-content:center; font-size:24px;
  transition:transform .18s, opacity .18s;
}
.ore-block:hover{transform:scale(1.08); background:rgba(255,255,255,.2);}
.ore-block.mined{opacity:0; transform:scale(.2) rotate(30deg); pointer-events:none;}
#mine-score{font-family:var(--font-pixel); color:var(--gold); font-size:14px; margin-top:10px;}
#mine-close{margin-top:18px;}

/* ============ AMBIENT CURSOR SPARKLE (ASMR touch) ============ */
.cursor-spark{
  position:fixed; z-index:65; pointer-events:none; border-radius:50%;
  width:10px; height:10px; margin:-5px 0 0 -5px;
  background:radial-gradient(circle, rgba(181,123,255,.9), rgba(181,123,255,.25) 55%, transparent 75%);
  animation: sparkFade 1.1s ease-out forwards;
}
@keyframes sparkFade{
  0%{opacity:.75; transform:scale(1);}
  100%{opacity:0; transform:scale(2.6) translateY(-14px);}
}

::-webkit-scrollbar{width:10px;}
::-webkit-scrollbar-track{background:transparent;}
::-webkit-scrollbar-thumb{background:rgba(255,255,255,.2); border-radius:6px;}

/* ============ BOOT LOADER — GTA V style split-screen intro ============ */
#boot-loader{
  position:fixed; inset:0; z-index:300;
  background:#020103;
  overflow:hidden;
  transition: opacity .9s ease, filter .9s ease;
}
#boot-loader.hide{ opacity:0; filter:blur(20px); pointer-events:none; }

.boot-portrait{
  position:absolute; top:0; left:0; bottom:0; width:54%;
  overflow:hidden;
}
.boot-portrait img{
  width:100%; height:100%; object-fit:cover; object-position:50% 18%;
  filter:grayscale(.6) contrast(1.2) brightness(.85) saturate(1.1);
  transform:scale(1.04);
}
.boot-portrait::after{
  content:""; position:absolute; inset:0;
  background:
    linear-gradient(90deg, transparent 45%, #020103 97%),
    linear-gradient(0deg, #020103 0%, transparent 22%, transparent 78%, rgba(2,1,3,.7) 100%),
    linear-gradient(135deg, rgba(255,46,146,.22), rgba(255,106,61,.1) 60%, transparent 80%);
}
.boot-portrait::before{
  content:""; position:absolute; inset:0; z-index:2;
  background:repeating-linear-gradient(0deg, rgba(255,255,255,.025) 0 1px, transparent 1px 3px);
  mix-blend-mode:overlay;
}

.boot-info{
  position:absolute; top:0; right:0; bottom:0; width:58%;
  display:flex; flex-direction:column; justify-content:center;
  padding:0 6vw 0 8vw; box-sizing:border-box;
}
.boot-kicker{
  font-family:var(--font-pixel); font-size:10px; letter-spacing:4px; color:var(--vc-orange);
  text-shadow:0 0 12px rgba(255,106,61,.7); margin-bottom:18px; opacity:.9;
}
.boot-title{
  font-family:var(--font-head); font-weight:600; color:#fff; line-height:1.1; text-transform:uppercase;
  font-size:clamp(26px,5vw,52px); letter-spacing:1px;
  animation: heroGlowBreathe 3.2s ease-in-out infinite;
}
.boot-sub{
  font-family:var(--font-mono); font-size:clamp(15px,1.6vw,19px); color:var(--vc-hotpink);
  letter-spacing:3px; opacity:.85; margin-top:10px;
}
.boot-tip{
  margin-top:42px; min-height:44px; font-family:var(--font-mono);
  font-size:clamp(14px,1.3vw,17px); color:#cfc2f2; opacity:.85; max-width:34ch; line-height:1.5;
}
.boot-tip b{color:var(--gold);}

.boot-bottom-bar{
  position:absolute; left:0; right:0; bottom:0;
  display:flex; align-items:center; gap:16px;
  padding:0 26px 20px;
}
.boot-bar-wrap{flex:1; height:6px; border-radius:3px; background:rgba(255,255,255,.08); overflow:hidden; position:relative;}
.boot-bar-fill{height:100%; width:0%; background:linear-gradient(90deg,#ff6a3d,#ff2e92,#ffb84d); background-size:220% 100%; animation: bootBarShimmer 2.4s linear infinite, bootBarGlow 2.4s ease-in-out infinite; transition:width .25s linear;}
@keyframes bootBarShimmer{0%{background-position:0% 0;} 100%{background-position:220% 0;}}
@keyframes bootBarGlow{0%,100%{box-shadow:0 0 8px rgba(255,106,61,.55);} 50%{box-shadow:0 0 22px rgba(255,46,146,.85);}}
#boot-pct{font-family:var(--font-pixel); font-size:13px; color:var(--gold); min-width:48px; text-align:right; animation: pctGlow 1.6s ease-in-out infinite;}
.boot-skip{
  position:absolute; top:20px; right:26px; font-family:var(--font-pixel); font-size:9px;
  color:rgba(255,255,255,.4); letter-spacing:1px;
}

@media(max-width:900px){
  .boot-portrait{width:100%; height:46%; top:0; bottom:auto;}
  .boot-portrait::after{background:
    linear-gradient(0deg, #020103 2%, transparent 45%, transparent 70%, rgba(2,1,3,.85) 100%),
    linear-gradient(135deg, rgba(181,123,255,.22), rgba(32,229,111,.08) 60%, transparent 80%);}
  .boot-info{width:100%; height:54%; top:46%; bottom:auto; padding:0 8vw; align-items:flex-start;}
  .boot-tip{max-width:100%;}
}

/* ============ ENTER OVERLAY — Valorant-style title/play screen ============ */
#enter-overlay{
  position:fixed; inset:0; z-index:200;
  background:#0a0b0d; overflow:hidden;
  display:flex; align-items:center;
  transition:opacity .5s ease;
  font-family:'Teko',sans-serif;
}
.val-portrait{
  position:absolute; right:0; top:0; bottom:0; width:58%;
  clip-path: polygon(16% 0, 100% 0, 100% 100%, 0% 100%);
  overflow:hidden; background:#000;
}
.val-portrait video, .val-portrait img{
  position:absolute; inset:0; width:100%; height:100%; object-fit:cover; object-position:50% 22%;
  filter:grayscale(.25) contrast(1.15) brightness(.75) saturate(1.15);
}
.val-portrait::after{
  content:""; position:absolute; inset:0;
  background:
    linear-gradient(90deg, rgba(10,11,13,.97) 0%, rgba(10,11,13,.55) 30%, transparent 55%),
    linear-gradient(0deg, rgba(10,11,13,.85) 0%, transparent 28%, transparent 72%, rgba(10,11,13,.6) 100%);
}
.val-slash{position:absolute; top:-25%; height:150%; width:5px; background:var(--val-red); box-shadow:0 0 22px var(--val-red); transform:rotate(15deg); z-index:1;}
.slash1{left:42%;}
.slash2{left:45.5%; width:2px; opacity:.4;}
.val-content{
  position:relative; z-index:2; padding:0 6vw; max-width:600px;
  display:flex; flex-direction:column; gap:6px;
}
.val-kicker{
  font-family:var(--font-mono); font-size:13px; letter-spacing:5px; color:var(--val-red);
  text-transform:uppercase; margin-bottom:4px;
}
#enter-overlay h1{
  font-family:'Teko',sans-serif; font-weight:600; text-transform:uppercase;
  font-size:clamp(48px,8vw,104px); line-height:.88; color:#fff; letter-spacing:1px;
}
#enter-overlay h1 span{display:block; -webkit-text-stroke:2px var(--val-red); color:transparent;}
#enter-overlay p{font-family:var(--font-mono); font-size:16px; color:#aeb4ba; opacity:.9; max-width:40ch; margin-top:10px;}
.enter-cta{margin-top:26px;}
#enter-btn{
  font-family:'Teko',sans-serif; font-weight:600; font-size:26px; letter-spacing:4px; text-transform:uppercase;
  background:var(--val-red); color:#fff; border:none; padding:13px 40px;
  clip-path: polygon(14px 0, 100% 0, calc(100% - 14px) 100%, 0 100%);
  cursor:pointer; transition: transform .15s ease, background .15s ease;
  animation: startPulse 1.8s ease-in-out infinite;
}
#enter-btn:hover{ background:#ff2e45; transform:translateX(5px); }
@keyframes startPulse{
  0%,100%{box-shadow:0 0 0 rgba(255,70,85,0);}
  50%{box-shadow:0 0 32px rgba(255,70,85,.75);}
}
.enter-hint{
  font-family:var(--font-mono); font-size:11px; letter-spacing:3px; color:#6b7075; margin-top:14px;
  text-transform:uppercase;
}

@media(max-width:900px){
  .val-portrait{width:100%; clip-path:none; opacity:.35;}
  .val-slash{display:none;}
  .val-content{padding:0 7vw; max-width:none;}
}

/* ============ TABLET / PC BREAKPOINTS ============ */
@media(min-width:1400px){
  .hotbar-slot{width:66px;height:66px;font-size:28px;}
  #xp-bar-wrap{width:460px;}
}
@media(max-width:1024px){ /* tablet / iPad */
  .screen{padding:80px 26px 130px;}
  .hotbar-slot{width:54px;height:54px;font-size:23px;}
}
</style>
</head>
<body>

<canvas id="bg-canvas"></canvas>
<video id="bg-video" muted loop playsinline></video>
<div id="bg-skyline" aria-hidden="true">
  <svg viewBox="0 0 1000 600" preserveAspectRatio="xMidYMax slice" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <radialGradient id="sunGrad" cx="50%" cy="50%" r="50%">
        <stop offset="0%" stop-color="#ffb84d"/>
        <stop offset="45%" stop-color="#ff6a3d" stop-opacity="0.85"/>
        <stop offset="100%" stop-color="#ff2e92" stop-opacity="0"/>
      </radialGradient>
      <linearGradient id="waterGrad" x1="0" y1="0" x2="0" y2="1">
        <stop offset="0%" stop-color="#2a0f2e"/>
        <stop offset="100%" stop-color="#0c0810"/>
      </linearGradient>
    </defs>
    <circle cx="500" cy="435" r="150" fill="url(#sunGrad)"/>
    <g fill="#0c0810">
      <rect x="0" y="370" width="26" height="120"/>
      <rect x="30" y="340" width="20" height="150"/>
      <rect x="55" y="390" width="34" height="100"/>
      <rect x="94" y="310" width="22" height="180"/>
      <rect x="122" y="360" width="30" height="130"/>
      <rect x="158" y="285" width="18" height="205"/>
      <rect x="182" y="345" width="26" height="145"/>
      <rect x="214" y="320" width="20" height="170"/>
      <rect x="240" y="400" width="40" height="90"/>
      <rect x="286" y="355" width="24" height="135"/>
      <rect x="316" y="300" width="18" height="190"/>
      <rect x="340" y="375" width="30" height="115"/>
      <rect x="376" y="330" width="22" height="160"/>
      <rect x="404" y="420" width="46" height="70"/>
      <rect x="456" y="270" width="16" height="220"/>
      <rect x="478" y="360" width="28" height="130"/>
      <rect x="512" y="300" width="18" height="190"/>
      <rect x="536" y="420" width="46" height="70"/>
      <rect x="588" y="375" width="24" height="115"/>
      <rect x="618" y="330" width="20" height="160"/>
      <rect x="644" y="390" width="34" height="100"/>
      <rect x="684" y="285" width="18" height="205"/>
      <rect x="708" y="350" width="26" height="140"/>
      <rect x="740" y="315" width="20" height="175"/>
      <rect x="766" y="400" width="40" height="90"/>
      <rect x="812" y="355" width="24" height="135"/>
      <rect x="842" y="300" width="18" height="190"/>
      <rect x="866" y="375" width="30" height="115"/>
      <rect x="902" y="330" width="22" height="160"/>
      <rect x="930" y="400" width="30" height="90"/>
      <rect x="964" y="360" width="20" height="130"/>
      <rect x="0" y="480" width="1000" height="14"/>
    </g>
    <rect x="0" y="490" width="1000" height="110" fill="url(#waterGrad)"/>
    <g opacity="0.35" stroke="#ff5fa8" stroke-width="1.4">
      <line x1="120" y1="500" x2="120" y2="595"/>
      <line x1="340" y1="505" x2="340" y2="595"/>
      <line x1="560" y1="500" x2="560" y2="595"/>
      <line x1="780" y1="505" x2="780" y2="595"/>
    </g>
    <g transform="translate(520,110)" opacity="0.45" fill="#0c0810">
      <ellipse cx="0" cy="0" rx="9" ry="3.4"/>
      <rect x="-13" y="-1" width="26" height="1.6"/>
    </g>
    <g transform="translate(75,60)" fill="none" stroke="#0c0810" stroke-width="7" stroke-linecap="round" opacity="0.9">
      <line x1="0" y1="0" x2="0" y2="95"/>
      <path d="M0 15 C -45 -5, -70 15, -85 45" stroke-width="5"/>
      <path d="M0 15 C 45 -5, 70 15, 85 45" stroke-width="5"/>
      <path d="M0 5 C -30 -25, -55 -20, -70 5" stroke-width="5"/>
      <path d="M0 5 C 30 -25, 55 -20, 70 5" stroke-width="5"/>
      <path d="M0 0 C -8 -35, 5 -55, 10 -70" stroke-width="5"/>
    </g>
    <g transform="translate(925,80) scale(-1,1)" fill="none" stroke="#0c0810" stroke-width="7" stroke-linecap="round" opacity="0.9">
      <line x1="0" y1="0" x2="0" y2="95"/>
      <path d="M0 15 C -45 -5, -70 15, -85 45" stroke-width="5"/>
      <path d="M0 15 C 45 -5, 70 15, 85 45" stroke-width="5"/>
      <path d="M0 5 C -30 -25, -55 -20, -70 5" stroke-width="5"/>
      <path d="M0 5 C 30 -25, 55 -20, 70 5" stroke-width="5"/>
      <path d="M0 0 C -8 -35, 5 -55, 10 -70" stroke-width="5"/>
    </g>
  </svg>
</div>
<div id="bg-tint"></div>

<!-- ================= BOOT LOADER (GTA V style split intro) ================= -->
<div id="boot-loader">
  <div class="boot-portrait"><img src="data:image/jpeg;base64,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" alt="Durjay Ghosh"></div>
  <div class="boot-info">
    <div class="boot-kicker">◆ CRAFT PORTFOLIO ◆</div>
    <div class="boot-title">DURJAY<br>GHOSH</div>
    <div class="boot-sub">LOADING WORLD…</div>
    <div class="boot-tip" id="boot-tip"></div>
  </div>
  <div class="boot-skip">CLICK ANYWHERE TO SKIP</div>
  <div class="boot-bottom-bar">
    <div class="boot-bar-wrap"><div class="boot-bar-fill" id="boot-bar-fill"></div></div>
    <div id="boot-pct">0%</div>
  </div>
</div>

<!-- ================= ENTER SCREEN (Valorant-style play card) ================= -->
<div id="enter-overlay">
  <div class="val-portrait">
    <video autoplay muted loop playsinline poster="data:image/jpeg;base64,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
