/* MORTIS — 3D Horror Restyle (video background) */
:root{
  --blood:#8B0000;
  --accent:#FF0000;
  --overlay:rgba(10,0,0,0.75);
  --parchment:#e8d5b7;
  --ink:#040202;
}

/* Video background layers */
.bg-video-wrap{
  position:fixed; inset:0;
  z-index:-10;
  overflow:hidden;
  transform:translateZ(0);
}
.bg-video{
  position:absolute; inset:0;
  width:100%; height:100%;
  object-fit:cover;
  filter:saturate(0.85) contrast(1.08) brightness(0.55);
}
.bg-blood-mist{
  position:absolute; inset:0;
  background:
    radial-gradient(ellipse 80% 55% at 50% 25%, rgba(255,0,0,0.18), transparent 60%),
    radial-gradient(ellipse 90% 70% at 30% 60%, rgba(139,0,0,0.26), transparent 62%),
    linear-gradient(180deg, rgba(10,0,0,0.75), rgba(5,0,0,0.82));
  mix-blend-mode:multiply;
  pointer-events:none;
}
.bg-vignette{
  position:absolute; inset:-2px;
  background:radial-gradient(ellipse 80% 65% at 50% 35%, transparent 55%, rgba(0,0,0,0.85) 100%);
  pointer-events:none;
}
.bg-fog{
  position:absolute; inset:-30%;
  background:
    radial-gradient(circle at 20% 30%, rgba(240,240,255,0.06), transparent 55%),
    radial-gradient(circle at 70% 55%, rgba(240,240,255,0.05), transparent 60%),
    radial-gradient(circle at 45% 70%, rgba(240,240,255,0.045), transparent 62%);
  filter:blur(6px);
  opacity:0.9;
  animation:fogDrift3d 18s linear infinite;
  pointer-events:none;
}
@keyframes fogDrift3d{
  0%{ transform:translate3d(-3%, -2%, 0); }
  50%{ transform:translate3d(3%, 2%, 0); }
  100%{ transform:translate3d(-3%, -2%, 0); }
}
.bg-dust{
  position:absolute; inset:0;
  background:
    radial-gradient(1px 1px at 10% 20%, rgba(255,255,255,0.25), transparent),
    radial-gradient(1px 1px at 40% 60%, rgba(255,255,255,0.18), transparent),
    radial-gradient(1px 1px at 70% 30%, rgba(255,255,255,0.22), transparent),
    radial-gradient(1px 1px at 80% 80%, rgba(255,255,255,0.15), transparent);
  background-size: 180px 180px;
  opacity:0.35;
  animation:dustFloat 10s linear infinite;
  pointer-events:none;
}
@keyframes dustFloat{
  from{ transform:translate3d(0,0,0); }
  to{ transform:translate3d(-90px, 90px, 0); }
}
.bg-drip{
  position:absolute; left:0; right:0; top:0;
  height:120px;
  background:
    linear-gradient(180deg, rgba(139,0,0,0.95), rgba(139,0,0,0.15) 70%, transparent),
    radial-gradient(circle at 8% 25%, rgba(255,0,0,0.35), transparent 45%),
    radial-gradient(circle at 22% 70%, rgba(139,0,0,0.5), transparent 55%),
    radial-gradient(circle at 45% 60%, rgba(255,0,0,0.3), transparent 55%),
    radial-gradient(circle at 72% 65%, rgba(139,0,0,0.55), transparent 55%),
    radial-gradient(circle at 88% 35%, rgba(255,0,0,0.28), transparent 45%);
  clip-path: polygon(0 0,100% 0,100% 60%,92% 55%,86% 70%,78% 52%,70% 72%,62% 54%,55% 78%,48% 56%,40% 74%,34% 56%,26% 78%,18% 55%,12% 68%,6% 52%,0 60%);
  filter:drop-shadow(0 10px 18px rgba(139,0,0,0.35));
  animation:dripPulseTop 3.2s ease-in-out infinite;
  pointer-events:none;
}
@keyframes dripPulseTop{ 0%,100%{ opacity:.9 } 50%{ opacity:.75 } }

/* Global restyle */
body{
  background:transparent !important;
  color:var(--parchment) !important;
  text-shadow:0 0 12px rgba(139,0,0,0.25);
  cursor: crosshair;
}

/* Horror cursor (simple) */
@supports (cursor: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24'%3E%3Ccircle cx='12' cy='12' r='3' fill='%23FF0000'/%3E%3Cpath d='M12 0 V6 M12 18 V24 M0 12 H6 M18 12 H24' stroke='%23FF0000' stroke-width='1.5'/%3E%3C/svg%3E") 12 12, crosshair){
  body{
    cursor: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24'%3E%3Ccircle cx='12' cy='12' r='3' fill='%23FF0000'/%3E%3Cpath d='M12 0 V6 M12 18 V24 M0 12 H6 M18 12 H24' stroke='%23FF0000' stroke-width='1.5'/%3E%3C/svg%3E") 12 12, crosshair;
  }
  button, a{ cursor: inherit; }
}

/* 3D stage */
main{ perspective: 1100px; transform-style: preserve-3d; }
.section-inner, .hero-inner{
  transform-style: preserve-3d;
}

/* Typography: horror titles */
.hero-title, .footer-logo, .thank-logo, .logo-link{
  font-family: "Nosifer","Creepster","UnifrakturMaguntia",cursive !important;
  letter-spacing: .08em;
}
.section-title, .font-section{
  font-family: "Creepster","Cinzel Decorative",serif !important;
}
.nav-links a, .btn, .font-ui{
  font-family: "Creepster","Cinzel",serif !important;
}

/* Eerie glow + flicker */
.glow-heading, .hero-title{
  color: var(--parchment) !important;
  text-shadow:
    0 0 10px rgba(139,0,0,0.55),
    0 0 22px rgba(255,0,0,0.25),
    0 0 42px rgba(139,0,0,0.35);
}
.hero-title{
  animation: heartbeat 1.8s ease-in-out infinite, flicker 6.5s infinite;
  transform: translateZ(34px);
}
@keyframes heartbeat{
  0%,100%{ transform: translateZ(34px) scale(1); filter:brightness(1); }
  12%{ transform: translateZ(34px) scale(1.03); filter:brightness(1.08); }
  24%{ transform: translateZ(34px) scale(0.99); filter:brightness(0.96); }
  36%{ transform: translateZ(34px) scale(1.05); filter:brightness(1.12); }
  48%{ transform: translateZ(34px) scale(1); filter:brightness(1); }
}
@keyframes flicker{
  0%, 100%{ opacity:1; }
  7%{ opacity:.85; }
  8%{ opacity:.3; }
  9%{ opacity:.95; }
  22%{ opacity:.6; }
  23%{ opacity:1; }
  54%{ opacity:.75; }
  55%{ opacity:.2; }
  56%{ opacity:1; }
}

/* Subtle screen shake on load */
body.shake main{ animation: shakeIn .7s ease-out 1; }
@keyframes shakeIn{
  0%{ transform: translate3d(0,0,0); }
  15%{ transform: translate3d(-2px, 1px, 0); }
  30%{ transform: translate3d(2px, -1px, 0); }
  45%{ transform: translate3d(-1px, -2px, 0); }
  60%{ transform: translate3d(1px, 2px, 0); }
  100%{ transform: translate3d(0,0,0); }
}

/* Nav / buttons */
.nav-bar{
  background: rgba(0,0,0,0.55) !important;
  backdrop-filter: blur(8px);
  border-bottom: 1px solid rgba(255,0,0,0.25) !important;
}
.nav-links a{
  color: var(--parchment) !important;
  text-shadow: 0 0 10px rgba(139,0,0,0.25);
}
.btn-primary{
  background: linear-gradient(180deg, var(--accent), var(--blood)) !important;
  border: 1px solid rgba(255,0,0,0.35) !important;
}
.btn-outline{
  border-color: rgba(255,0,0,0.45) !important;
  color: var(--parchment) !important;
}
.btn:hover, .nav-links a:hover{
  animation: glitchHover .55s steps(2,end);
}
@keyframes glitchHover{
  0%{ transform: translateZ(0) translateX(0); filter: none; }
  20%{ transform: translateZ(0) translateX(-2px); filter: hue-rotate(-10deg); }
  40%{ transform: translateZ(0) translateX(2px); filter: contrast(1.2); }
  60%{ transform: translateZ(0) translateX(-1px); filter: saturate(1.3); }
  100%{ transform: translateZ(0) translateX(0); filter: none; }
}

/* 3D tilt for content sections */
.section-inner{
  background: rgba(0,0,0,0.45);
  border: 1px solid rgba(139,0,0,0.35);
  box-shadow: 0 0 24px rgba(139,0,0,0.18);
  transform: translateZ(10px);
}
.section-inner:hover{
  transform: translateZ(16px) rotateX(.6deg) rotateY(-.6deg);
  transition: transform .25s ease, box-shadow .25s ease;
}

/* Reduce existing bright backgrounds */
.victorian-corners{ background: rgba(0,0,0,0.55) !important; }

/* Ensure hero isn’t a solid block */
.hero{ background: transparent !important; }


