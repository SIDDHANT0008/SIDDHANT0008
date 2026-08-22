<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Siddhant — Full Stack Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#0a0a09;
    --surface:#121210;
    --surface-2:#17160f;
    --line:#28261c;
    --text:#f2f0e8;
    --text-dim:#8d897c;
    --text-faint:#54524a;
    --accent:#ffb703;
    --accent-soft:#4a3a12;
    --mono:'Space Mono', monospace;
    --sans:'Inter', sans-serif;
  }
  *{margin:0;padding:0;box-sizing:border-box;}
  html{background:var(--bg);}
  ::selection{background:var(--accent);color:#0a0a09;}
  body{
    background:var(--bg);
    color:var(--text);
    font-family:var(--sans);
    overflow-x:hidden;
    cursor:none;
  }
  @media (max-width:820px){ body{cursor:auto;} }
  a{color:inherit;text-decoration:none;}
  ::-webkit-scrollbar{width:0;background:transparent;}
 
  /* ---------- custom cursor ---------- */
  .cursor-dot, .cursor-ring{
    position:fixed;top:0;left:0;pointer-events:none;z-index:9999;
    border-radius:50%;transform:translate(-50%,-50%);
    mix-blend-mode:difference;
  }
  .cursor-dot{width:6px;height:6px;background:var(--accent);}
  .cursor-ring{width:34px;height:34px;border:1px solid var(--text-dim);transition:width .25s,height .25s,border-color .25s,opacity .25s;}
  .cursor-ring.hover{width:64px;height:64px;border-color:var(--accent);}
  @media (max-width:820px){ .cursor-dot,.cursor-ring{display:none;} }
 
  /* ---------- layout shell ---------- */
  .noise{
    position:fixed;inset:0;z-index:1;pointer-events:none;opacity:.035;
    background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='120' height='120'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  }
 
  section, header, footer{position:relative;z-index:2;}
 
  .container{
    max-width:920px;
    margin:0 auto;
    padding:0 40px;
  }
  @media (max-width:640px){ .container{padding:0 24px;} }
 
  .eyebrow{
    font-family:var(--mono);
    font-size:12px;
    letter-spacing:.18em;
    text-transform:uppercase;
    color:var(--accent);
    display:flex;
    align-items:center;
    gap:10px;
  }
  .eyebrow::before{
    content:'';
    width:14px;height:1px;background:var(--accent);
  }
 
  /* ---------- git rail ---------- */
  .rail{
    position:fixed;
    left:44px;
    top:0;
    height:100vh;
    width:1px;
    z-index:5;
    display:flex;
    align-items:center;
  }
  .rail-track{
    position:relative;
    height:52vh;
    width:1px;
    background:var(--line);
  }
  .rail-fill{
    position:absolute;top:0;left:0;width:100%;height:0%;
    background:var(--accent);
    transform-origin:top;
  }
  .rail-node{
    position:absolute;left:50%;
    transform:translate(-50%,-50%);
    width:9px;height:9px;border-radius:50%;
    background:var(--bg);
    border:1px solid var(--text-faint);
    transition:border-color .3s, background .3s, box-shadow .3s;
  }
  .rail-node.active{
    border-color:var(--accent);
    background:var(--accent);
    box-shadow:0 0 0 4px var(--accent-soft);
  }
  .rail-label{
    position:absolute;left:22px;top:50%;transform:translateY(-50%);
    font-family:var(--mono);font-size:11px;color:var(--text-faint);
    white-space:nowrap;opacity:0;transition:opacity .3s, color .3s;
  }
  .rail-node.active .rail-label{opacity:1;color:var(--text-dim);}
  @media (max-width:980px){ .rail{display:none;} }
 
  /* ---------- top progress ---------- */
  .topbar{
    position:fixed;top:0;left:0;width:100%;height:2px;z-index:20;
    background:var(--line);
  }
  .topbar-fill{width:0%;height:100%;background:var(--accent);}
 
  /* ---------- hero ---------- */
  .hero{
    min-height:100svh;
    display:flex;flex-direction:column;justify-content:center;
    padding-top:100px;
  }
  .hero .eyebrow{margin-bottom:28px;}
  .hero h1{
    font-family:var(--mono);
    font-weight:700;
    font-size:clamp(44px, 9vw, 104px);
    line-height:0.98;
    letter-spacing:-.02em;
  }
  .hero h1 .cursor-blink{
    display:inline-block;width:.5em;background:var(--accent);
    animation:blink 1s steps(1) infinite;
    transform:translateY(2px);
  }
  @keyframes blink{ 50%{opacity:0;} }
  .hero p.tag{
    margin-top:28px;
    font-size:clamp(16px,2.4vw,20px);
    color:var(--text-dim);
    max-width:560px;
    line-height:1.6;
  }
  .hero p.tag span{color:var(--text);}
  .hero .scroll-cue{
    margin-top:80px;
    display:flex;align-items:center;gap:12px;
    font-family:var(--mono);font-size:11px;color:var(--text-faint);
    letter-spacing:.1em;text-transform:uppercase;
  }
  .scroll-cue .line{width:32px;height:1px;background:var(--text-faint);animation:pulseline 2.4s ease-in-out infinite;}
  @keyframes pulseline{ 0%,100%{opacity:.3;} 50%{opacity:1;} }
 
  /* ---------- shared section spacing ---------- */
  section.block{padding:150px 0;}
  @media (max-width:640px){ section.block{padding:100px 0;} }
 
  h2.section-title{
    font-family:var(--mono);
    font-weight:700;
    font-size:clamp(28px,4vw,42px);
    letter-spacing:-.01em;
    margin:18px 0 44px;
  }
 
  /* ---------- about ---------- */
  .about-body{
    font-size:clamp(16px,2vw,19px);
    line-height:1.85;
    color:var(--text-dim);
    max-width:640px;
  }
  .about-body strong{color:var(--text);font-weight:600;}
  .about-body p + p{margin-top:22px;}
 
  .stat-row{
    display:flex;gap:48px;margin-top:56px;flex-wrap:wrap;
  }
  .stat{font-family:var(--mono);}
  .stat b{display:block;font-size:30px;color:var(--accent);font-weight:700;}
  .stat span{font-size:12px;color:var(--text-faint);letter-spacing:.08em;text-transform:uppercase;}
 
  /* ---------- projects ---------- */
  .proj-list{border-top:1px solid var(--line);}
  .proj{
    border-bottom:1px solid var(--line);
    padding:34px 0;
    display:grid;
    grid-template-columns:120px 1fr auto;
    gap:24px;
    align-items:start;
    transition:padding-left .35s ease;
  }
  .proj:hover{padding-left:14px;}
  @media (max-width:640px){ .proj{grid-template-columns:1fr;gap:10px;} }
  .proj-idx{font-family:var(--mono);color:var(--text-faint);font-size:13px;padding-top:4px;}
  .proj-name{
    font-family:var(--mono);font-size:19px;font-weight:700;color:var(--text);
    display:flex;align-items:center;gap:10px;
  }
  .proj-name::before{content:'>';color:var(--accent);}
  .proj-desc{font-size:15px;color:var(--text-dim);margin-top:8px;line-height:1.65;max-width:480px;}
  .proj-tags{display:flex;gap:8px;flex-wrap:wrap;justify-content:flex-end;align-self:start;}
  @media (max-width:640px){ .proj-tags{justify-content:flex-start;} }
  .proj-tags span{
    font-family:var(--mono);font-size:11px;color:var(--text-faint);
    border:1px solid var(--line);padding:4px 9px;border-radius:20px;
  }
 
  /* ---------- connect ---------- */
  .connect-title{font-size:clamp(28px,5vw,54px);font-weight:800;line-height:1.15;max-width:680px;}
  .connect-title span{color:var(--accent);}
  .connect-links{margin-top:70px;border-top:1px solid var(--line);}
  .clink{
    display:flex;justify-content:space-between;align-items:center;
    padding:26px 4px;border-bottom:1px solid var(--line);
    font-family:var(--mono);font-size:clamp(18px,3vw,26px);
    position:relative;overflow:hidden;
  }
  .clink .arrow{color:var(--accent);opacity:0;transform:translateX(-8px);transition:opacity .3s, transform .3s;}
  .clink:hover .arrow{opacity:1;transform:translateX(0);}
  .clink small{font-size:12px;color:var(--text-faint);font-family:var(--sans);letter-spacing:.05em;}
 
  footer{
    padding:60px 0 50px;
    display:flex;justify-content:space-between;align-items:center;
    color:var(--text-faint);font-family:var(--mono);font-size:12px;
    border-top:1px solid var(--line);
  }
  @media (max-width:560px){ footer{flex-direction:column;gap:10px;text-align:center;} }
 
  .reveal{opacity:0;transform:translateY(28px);}
</style>
</head>
<body>
 
<div class="noise"></div>
<div class="cursor-dot" id="cdot"></div>
<div class="cursor-ring" id="cring"></div>
<div class="topbar"><div class="topbar-fill" id="topbarFill"></div></div>
 
<div class="rail">
  <div class="rail-track" id="railTrack">
    <div class="rail-fill" id="railFill"></div>
    <div class="rail-node" data-section="hero" style="top:0%"><span class="rail-label">init</span></div>
    <div class="rail-node" data-section="about" style="top:32%"><span class="rail-label">about.md</span></div>
    <div class="rail-node" data-section="projects" style="top:66%"><span class="rail-label">projects/</span></div>
    <div class="rail-node" data-section="connect" style="top:100%"><span class="rail-label">connect</span></div>
  </div>
</div>
 
<header class="hero container" id="hero">
  <div class="eyebrow">whoami</div>
  <h1>Siddhant<span class="cursor-blink">&nbsp;</span></h1>
  <p class="tag">Full stack developer running mostly on <span>chai</span> and a refusal to ship un-refactored code. Deploys things at 2am, then spends the morning explaining to himself why it broke.</p>
  <div class="scroll-cue"><div class="line"></div> scroll to continue</div>
</header>
 
<section class="block container" id="about">
  <div class="eyebrow">01 — about.md</div>
  <h2 class="section-title reveal">Bugs are just<br>undocumented features.</h2>
  <div class="about-body reveal">
    <p>I build full stack products end to end — <strong>React and Node</strong> on the surface, careful architecture underneath. I care more about the codebase surviving contact with a second developer than about looking clever in a pull request.</p>
    <p>Most nights land the same way: something ships, something breaks, and I spend the next morning arguing with a version of myself from twelve hours ago. So far, I keep winning — the commits keep landing slightly less terrible than the ones before.</p>
  </div>
  <div class="stat-row reveal">
    <div class="stat"><b id="statStars">0</b><span>github stars</span></div>
    <div class="stat"><b id="statFollowers">0</b><span>followers</span></div>
    <div class="stat"><b>2am</b><span>usual deploy time</span></div>
  </div>
</section>
 
<section class="block container" id="projects">
  <div class="eyebrow">02 — projects/</div>
  <h2 class="section-title reveal">Built to avoid manual labor.</h2>
  <div class="proj-list reveal">
    <div class="proj">
      <div class="proj-idx">01</div>
      <div>
        <div class="proj-name">project-one</div>
        <div class="proj-desc">Does the thing nobody asked for — and does it properly, with the kind of polish that only comes from over-engineering a side project.</div>
      </div>
      <div class="proj-tags"><span>full stack</span></div>
    </div>
    <div class="proj">
      <div class="proj-idx">02</div>
      <div>
        <div class="proj-name">project-two</div>
        <div class="proj-desc">A Node.js service that keeps side projects on track better than its author keeps a sleep schedule.</div>
      </div>
      <div class="proj-tags"><span>node.js</span><span>service</span></div>
    </div>
    <div class="proj">
      <div class="proj-idx">03</div>
      <div>
        <div class="proj-name">project-three</div>
        <div class="proj-desc">A full stack app that exists mainly because reading the documentation felt like more effort than writing it from scratch.</div>
      </div>
      <div class="proj-tags"><span>react</span><span>full stack</span></div>
    </div>
  </div>
</section>
 
<section class="block container" id="connect">
  <div class="eyebrow">03 — connect</div>
  <h2 class="connect-title reveal">Every commit is a small,<br>desperate apology to <span>future me.</span></h2>
  <div class="connect-links reveal">
    <a class="clink magnetic" href="https://github.com/SIDDHANT0008" target="_blank" rel="noopener">
      <span>GitHub <small>/ code lives here</small></span>
      <span class="arrow">→</span>
    </a>
    <a class="clink magnetic" href="https://linkedin.com/in/siddhant-nathani-801678369" target="_blank" rel="noopener">
      <span>LinkedIn <small>/ the professional version</small></span>
      <span class="arrow">→</span>
    </a>
    <a class="clink magnetic" href="mailto:yourname@gmail.com">
      <span>Email <small>/ fastest way to reach me</small></span>
      <span class="arrow">→</span>
    </a>
    <a class="clink magnetic" href="#">
      <span>Resume <small>/ the formal record</small></span>
      <span class="arrow">→</span>
    </a>
  </div>
</section>
 
<footer class="container">
  <span>&copy; 2026 Siddhant — branch out, merge greatness.</span>
  <span id="clock"></span>
</footer>
 
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script>
gsap.registerPlugin(ScrollTrigger);
 
/* smooth-ish native scroll easing */
document.documentElement.style.scrollBehavior = 'smooth';
 
/* ---------- custom cursor ---------- */
const cdot = document.getElementById('cdot');
const cring = document.getElementById('cring');
let mx=0,my=0, rx=0, ry=0;
window.addEventListener('mousemove', e=>{
  mx=e.clientX; my=e.clientY;
  cdot.style.left=mx+'px'; cdot.style.top=my+'px';
});
gsap.ticker.add(()=>{
  rx += (mx-rx)*0.18; ry += (my-ry)*0.18;
  cring.style.left=rx+'px'; cring.style.top=ry+'px';
});
document.querySelectorAll('a, .proj').forEach(el=>{
  el.addEventListener('mouseenter', ()=>cring.classList.add('hover'));
  el.addEventListener('mouseleave', ()=>cring.classList.remove('hover'));
});
 
/* ---------- magnetic links ---------- */
document.querySelectorAll('.magnetic').forEach(el=>{
  const strength = 18;
  el.addEventListener('mousemove', e=>{
    const r = el.getBoundingClientRect();
    const relX = e.clientX - r.left - r.width/2;
    gsap.to(el, {x: relX/r.width*strength, duration:.4, ease:'power2.out'});
  });
  el.addEventListener('mouseleave', ()=>{
    gsap.to(el, {x:0, duration:.5, ease:'elastic.out(1,0.4)'});
  });
});
 
/* ---------- reveals ---------- */
gsap.utils.toArray('.reveal').forEach(el=>{
  gsap.to(el, {
    opacity:1, y:0, duration:1, ease:'power3.out',
    scrollTrigger:{ trigger: el, start:'top 85%' }
  });
});
 
/* ---------- top progress bar ---------- */
gsap.to('#topbarFill', {
  width:'100%', ease:'none',
  scrollTrigger:{ trigger: document.body, start:'top top', end:'bottom bottom', scrub:0.3 }
});
 
/* ---------- rail fill + active node ---------- */
gsap.to('#railFill', {
  height:'100%', ease:'none',
  scrollTrigger:{ trigger: document.body, start:'top top', end:'bottom bottom', scrub:0.3 }
});
const nodes = document.querySelectorAll('.rail-node');
nodes.forEach(node=>{
  const id = node.dataset.section;
  const target = document.getElementById(id);
  ScrollTrigger.create({
    trigger: target,
    start:'top 60%',
    end:'bottom 40%',
    onEnter:()=>setActive(node),
    onEnterBack:()=>setActive(node)
  });
});
function setActive(active){
  nodes.forEach(n=>n.classList.toggle('active', n===active));
}
setActive(nodes[0]);
 
/* ---------- animated stat counters (illustrative placeholders) ---------- */
function countUp(elId, end, dur=1.4){
  const el = document.getElementById(elId);
  const obj={v:0};
  gsap.to(obj,{
    v:end, duration:dur, ease:'power2.out',
    onUpdate:()=>{ el.textContent = Math.floor(obj.v); },
    scrollTrigger:{ trigger: el, start:'top 90%' }
  });
}
countUp('statStars', 0);
countUp('statFollowers', 0);
 
/* ---------- footer clock ---------- */
function tick(){
  const d = new Date();
  document.getElementById('clock').textContent = d.toLocaleTimeString('en-US', {hour:'2-digit',minute:'2-digit'});
}
tick(); setInterval(tick, 1000*30);
 
/* reduced motion respect */
if (window.matchMedia('(prefers-reduced-motion: reduce)').matches){
  gsap.globalTimeline.timeScale(50);
  document.documentElement.style.scrollBehavior='auto';
}
</script>
 
</body>
</html>
 
