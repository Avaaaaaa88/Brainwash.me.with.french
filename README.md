<!DOCTYPE html>
<html>
<head>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400;1,700&family=Courier+Prime:wght@400;700&family=IM+Fell+English:ital@0;1&display=swap');
  *{box-sizing:border-box;margin:0;padding:0}
  :root{--orange:#FF5C00;--cream:#E8DFD0;--dark:#0A0A0F;--shadow:#0D1B2A;--muted:#8A7F72;}
  body{background:var(--dark);color:var(--cream);font-family:'Courier Prime',monospace;overflow-x:hidden;}
  .ts{font-family:'Courier Prime',monospace;color:var(--orange);font-size:11px;letter-spacing:0.08em;font-weight:700;}

  /* NAV */
  nav{position:fixed;top:0;left:0;right:0;z-index:200;display:flex;justify-content:space-between;align-items:center;padding:12px 24px;background:rgba(10,10,15,0.97);border-bottom:1px solid rgba(255,92,0,0.15);}
  .logo{font-family:'Playfair Display',serif;font-size:16px;letter-spacing:0.12em;color:var(--cream);}
  .nav-links{display:flex;gap:4px;}
  .nav-links button{background:none;border:none;cursor:pointer;font-family:'Courier Prime',monospace;font-size:10px;letter-spacing:0.1em;color:var(--muted);text-transform:uppercase;padding:6px 12px;transition:all 0.2s;border-bottom:1px solid transparent;}
  .nav-links button:hover,.nav-links button.active{color:var(--orange);border-bottom-color:var(--orange);}

  /* PAGES */
  .page{display:none;padding-top:48px;}
  .page.active{display:block;}

  /* LANDING */
  .hero{position:relative;height:280px;overflow:hidden;display:flex;align-items:flex-end;}
  .hero-media{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;opacity:0.45;}
  .hero-media-fallback{position:absolute;inset:0;background:linear-gradient(135deg,#0A0A0F 0%,#0D1B2A 40%,#1A2A1E 75%,#0A0A0F 100%);}
  .hero-overlay{position:absolute;inset:0;background:linear-gradient(to top,rgba(10,10,15,1) 0%,rgba(10,10,15,0.3) 60%,transparent 100%);}
  .hero-content{position:relative;z-index:2;padding:24px 24px 20px;width:100%;}
  .hero h1{font-family:'Playfair Display',serif;font-size:36px;font-weight:900;line-height:1;color:var(--cream);margin-bottom:6px;}
  .hero h1 em{font-style:italic;color:transparent;-webkit-text-stroke:1px var(--cream);}
  .hero-sub{font-family:'Courier Prime',monospace;font-size:11px;color:var(--muted);line-height:1.5;margin-bottom:14px;max-width:420px;}
  .hero-btns{display:flex;gap:10px;flex-wrap:wrap;}

  .btn-p{background:var(--orange);color:var(--dark);border:none;cursor:pointer;font-family:'Courier Prime',monospace;font-size:10px;font-weight:700;letter-spacing:0.12em;text-transform:uppercase;padding:10px 22px;transition:all 0.2s;}
  .btn-p:hover{background:#FF7722;}
  .btn-g{background:none;color:var(--cream);border:1px solid rgba(232,223,208,0.3);cursor:pointer;font-family:'Courier Prime',monospace;font-size:10px;letter-spacing:0.12em;text-transform:uppercase;padding:9px 18px;transition:all 0.2s;}
  .btn-g:hover{border-color:var(--cream);}
  .btn-sm{background:none;border:1px solid rgba(255,92,0,0.35);cursor:pointer;font-family:'Courier Prime',monospace;font-size:8px;letter-spacing:0.1em;color:var(--orange);padding:4px 10px;text-transform:uppercase;transition:all 0.2s;white-space:nowrap;}
  .btn-sm:hover,.btn-sm.on{background:rgba(255,92,0,0.12);border-color:var(--orange);}

  /* SECTION LABEL */
  .slabel{font-family:'Courier Prime',monospace;font-size:9px;letter-spacing:0.22em;color:var(--orange);text-transform:uppercase;margin-bottom:12px;display:flex;align-items:center;gap:10px;}
  .slabel::after{content:'';flex:1;height:1px;background:linear-gradient(to right,rgba(255,92,0,0.35),transparent);}

  /* THEMES GRID */
  .themes-wrap{padding:20px 24px 24px;}
  .themes-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:2px;}
  .tcard{position:relative;overflow:hidden;cursor:pointer;transition:all 0.25s;}
  .tcard:hover{transform:scale(1.01);z-index:2;}
  .tcard-bg{position:absolute;inset:0;}
  .tcard-img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;opacity:0.4;}
  .tcard-overlay{position:absolute;inset:0;background:linear-gradient(to top,rgba(10,10,15,0.95) 0%,rgba(10,10,15,0.3) 60%,transparent 100%);}
  .tcard-content{position:relative;z-index:2;padding:16px;padding-top:80px;}
  .tcard-tag{font-family:'Courier Prime',monospace;font-size:8px;letter-spacing:0.18em;color:var(--orange);text-transform:uppercase;margin-bottom:4px;}
  .tcard h3{font-family:'Playfair Display',serif;font-size:20px;font-weight:700;color:var(--cream);line-height:1.1;margin-bottom:4px;}
  .tcard p{font-size:10px;color:var(--muted);line-height:1.4;}
  .tcard-stamp{position:absolute;top:10px;right:10px;z-index:3;}
  .tcard-badge{position:absolute;top:10px;left:10px;background:var(--orange);color:var(--dark);font-family:'Courier Prime',monospace;font-size:8px;letter-spacing:0.12em;font-weight:700;padding:3px 8px;text-transform:uppercase;z-index:3;}
  .tcard-bm{position:absolute;bottom:12px;right:12px;z-index:3;}

  /* LESSON */
  .lesson-wrap{padding:16px 24px 32px;}
  .lesson-hdr{margin-bottom:16px;padding-bottom:16px;border-bottom:1px solid rgba(232,223,208,0.1);}
  .lesson-hdr-top{display:flex;align-items:flex-start;justify-content:space-between;gap:12px;flex-wrap:wrap;}
  .lesson-title{font-family:'Playfair Display',serif;font-size:32px;font-weight:900;color:var(--cream);line-height:1;}
  .lesson-meta{display:flex;gap:16px;align-items:center;flex-wrap:wrap;margin-top:8px;}
  .video-wrap{width:100%;aspect-ratio:16/9;background:var(--shadow);margin-bottom:20px;border:1px solid rgba(255,92,0,0.2);overflow:hidden;}
  .video-wrap iframe{width:100%;height:100%;border:none;display:block;}

  /* VOCAB */
  .vocab-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(160px,1fr));gap:8px;margin-bottom:20px;}
  .vcard{background:rgba(13,27,42,0.7);border:1px solid rgba(232,223,208,0.1);padding:12px 14px;transition:all 0.2s;}
  .vcard:hover{border-color:rgba(255,92,0,0.5);}
  .vword{font-family:'Playfair Display',serif;font-size:18px;font-weight:700;color:var(--cream);margin-bottom:2px;}
  .vtype{font-family:'Courier Prime',monospace;font-size:8px;letter-spacing:0.12em;color:var(--orange);text-transform:uppercase;}
  .vtrans{font-family:'Courier Prime',monospace;font-size:10px;color:var(--muted);margin-top:4px;line-height:1.3;}
  .vbtns{display:flex;gap:6px;margin-top:8px;}

  /* PHRASES */
  .phrase-list{margin-bottom:20px;}
  .phrase-row{display:flex;gap:16px;padding:12px 0;border-bottom:1px solid rgba(232,223,208,0.07);align-items:flex-start;}
  .pnum{font-family:'Courier Prime',monospace;font-size:9px;color:var(--orange);min-width:24px;padding-top:5px;}
  .ptext{font-family:'IM Fell English',serif;font-size:20px;font-style:italic;color:var(--cream);line-height:1.3;flex:1;}

  /* POLAROID */
  .polaroid{background:#F0EAE0;padding:14px 14px 36px;max-width:300px;transform:rotate(-1.5deg);box-shadow:6px 10px 30px rgba(0,0,0,0.6);position:relative;margin-bottom:24px;}
  .pol-inner{background:var(--shadow);aspect-ratio:4/3;display:flex;align-items:center;justify-content:center;margin-bottom:12px;}
  .pol-text{font-family:'Courier Prime',monospace;font-size:10px;color:#333;text-align:center;line-height:1.5;padding:0 4px;}
  .pol-cap{position:absolute;bottom:8px;left:14px;right:14px;text-align:center;font-family:'Courier Prime',monospace;font-size:9px;color:#666;}

  /* BRAINWASH */
  .brain-wrap{padding:16px 24px 32px;}
  .wb-grid{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:16px;}
  .wb-pill{padding:5px 12px;border:1px solid rgba(232,223,208,0.12);font-family:'Playfair Display',serif;font-size:14px;color:var(--muted);cursor:pointer;transition:all 0.2s;}
  .wb-pill.learning{border-color:rgba(255,92,0,0.4);color:var(--cream);background:rgba(255,92,0,0.05);}
  .wb-pill.done{border-color:rgba(76,175,80,0.4);color:#A8E6AB;background:rgba(76,175,80,0.05);}

  /* QUIZ */
  .qprog{background:rgba(255,255,255,0.07);height:2px;margin-bottom:20px;overflow:hidden;}
  .qprog-fill{height:100%;background:var(--orange);transition:width 0.4s;}
  .qword{font-family:'Playfair Display',serif;font-size:44px;font-weight:900;text-align:center;color:var(--cream);margin-bottom:6px;}
  .qlabel{font-family:'Courier Prime',monospace;font-size:9px;letter-spacing:0.18em;color:var(--muted);text-align:center;text-transform:uppercase;margin-bottom:20px;}
  .qopts{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:16px;}
  .qopt{background:rgba(13,27,42,0.6);border:1px solid rgba(232,223,208,0.12);padding:14px 12px;cursor:pointer;font-family:'Courier Prime',monospace;font-size:11px;color:var(--cream);text-align:left;display:flex;align-items:center;gap:8px;transition:all 0.15s;}
  .qopt::before{content:attr(data-k);font-size:8px;color:var(--orange);font-weight:700;min-width:12px;}
  .qopt:hover:not(:disabled){border-color:var(--orange);background:rgba(255,92,0,0.07);}
  .qopt.ok{border-color:#4CAF50;background:rgba(76,175,80,0.1);color:#A8E6AB;}
  .qopt.no{border-color:#E24B4A;background:rgba(226,75,74,0.1);color:#F09595;animation:sh 0.3s;}
  @keyframes sh{0%,100%{transform:translateX(0)}25%{transform:translateX(-5px)}75%{transform:translateX(5px)}}
  .qopt:disabled{cursor:not-allowed;}
  .qfb{text-align:center;font-family:'Courier Prime',monospace;font-size:11px;letter-spacing:0.08em;min-height:28px;padding:6px;}
  .qfb.ok{color:#A8E6AB;} .qfb.no{color:#F09595;}
  .mdots{display:flex;gap:3px;margin-top:16px;align-items:center;}
  .mlabel{font-family:'Courier Prime',monospace;font-size:8px;letter-spacing:0.12em;color:var(--muted);text-transform:uppercase;min-width:56px;}
  .mdot{width:8px;height:8px;border:1px solid rgba(255,92,0,0.35);border-radius:50%;background:transparent;transition:background 0.3s;}
  .mdot.on{background:var(--orange);border-color:var(--orange);}

  /* POPUP */
  .pop-ov{position:fixed;inset:0;z-index:9000;background:rgba(0,0,0,0.9);display:none;}
  .pop-ov.on{display:block;}
  .pop-win{position:absolute;background:var(--dark);border:1px solid var(--orange);min-width:240px;max-width:280px;box-shadow:0 0 30px rgba(255,92,0,0.25);animation:pi 0.15s ease-out;}
  @keyframes pi{from{transform:scale(0.85) translateY(8px);opacity:0;}to{transform:scale(1) translateY(0);opacity:1;}}
  .pop-bar{background:var(--orange);padding:5px 8px;display:flex;align-items:center;justify-content:space-between;font-family:'Courier Prime',monospace;font-size:9px;color:var(--dark);font-weight:700;letter-spacing:0.1em;text-transform:uppercase;}
  .pop-x{background:var(--dark);border:none;cursor:pointer;width:14px;height:14px;font-size:9px;color:var(--orange);display:flex;align-items:center;justify-content:center;font-weight:700;}
  .pop-body{padding:18px 20px 14px;text-align:center;}
  .pop-word{font-family:'Playfair Display',serif;font-size:36px;font-weight:900;color:var(--cream);margin-bottom:4px;animation:wp 0.6s ease-in-out infinite alternate;}
  @keyframes wp{from{color:var(--cream);}to{color:var(--orange);}}
  .pop-trans{font-family:'Courier Prime',monospace;font-size:10px;letter-spacing:0.1em;color:var(--muted);text-transform:uppercase;}
  .pop-cnt{font-family:'Courier Prime',monospace;font-size:9px;color:var(--orange);margin-top:8px;letter-spacing:0.1em;}
  .pop-dots{display:flex;gap:4px;justify-content:center;margin-top:8px;}
  .pop-dot{width:7px;height:7px;border-radius:50%;background:rgba(255,92,0,0.15);border:1px solid rgba(255,92,0,0.35);}
  .pop-dot.on{background:var(--orange);border-color:var(--orange);}
  .pop-spk{font-family:'Courier Prime',monospace;font-size:8px;color:var(--orange);margin-top:6px;letter-spacing:0.12em;opacity:0.7;}

  /* SAVED */
  .saved-wrap{padding:16px 24px 32px;}
  .bm-card{background:rgba(13,27,42,0.6);border:1px solid rgba(255,92,0,0.18);padding:14px 18px;margin-bottom:8px;display:flex;align-items:center;justify-content:space-between;cursor:pointer;transition:all 0.2s;}
  .bm-card:hover{border-color:var(--orange);transform:translateX(3px);}
  .bm-title{font-family:'Playfair Display',serif;font-size:18px;color:var(--cream);}
  .bm-meta{font-family:'Courier Prime',monospace;font-size:8px;color:var(--muted);letter-spacing:0.08em;text-transform:uppercase;margin-top:3px;}
  .sv-row{display:flex;align-items:center;justify-content:space-between;padding:10px 0;border-bottom:1px solid rgba(232,223,208,0.07);}
  .sv-word{font-family:'Playfair Display',serif;font-size:17px;color:var(--cream);}
  .sv-trans{font-family:'Courier Prime',monospace;font-size:9px;color:var(--muted);margin-top:2px;}
  .sv-acts{display:flex;gap:8px;align-items:center;}
  .empty{font-family:'Courier Prime',monospace;font-size:11px;color:var(--muted);text-align:center;padding:24px;border:1px dashed rgba(255,92,0,0.18);letter-spacing:0.06em;}

  /* TOAST */
  .toast{position:fixed;bottom:20px;right:20px;background:var(--orange);color:var(--dark);font-family:'Courier Prime',monospace;font-size:10px;font-weight:700;letter-spacing:0.1em;padding:8px 16px;z-index:9999;transform:translateY(50px);opacity:0;transition:all 0.28s;text-transform:uppercase;}
  .toast.on{transform:translateY(0);opacity:1;}

  .vignette{position:fixed;inset:0;pointer-events:none;z-index:50;background:radial-gradient(ellipse 90% 80% at 50% 50%,transparent 50%,rgba(10,10,15,0.35) 100%);}
  .divider{height:1px;background:rgba(232,223,208,0.08);margin:16px 0;}
</style>
</head>
<body>
<div class="vignette"></div>
<div class="toast" id="toast"></div>

<nav>
  <div class="logo">Le&nbsp;<em style="font-style:italic;color:var(--orange)">Brainwash</em></div>
  <div class="nav-links">
    <button onclick="go('home')" id="nb-home" class="active">Accueil</button>
    <button onclick="go('lesson')" id="nb-lesson">Leçon</button>
    <button onclick="go('brain')" id="nb-brain">Mémoriser</button>
    <button onclick="go('saved')" id="nb-saved">Sauvegardé<span id="sbadge" style="color:var(--orange);margin-left:3px;"></span></button>
  </div>
</nav>

<!-- HOME -->
<div class="page active" id="page-home">
  <div class="hero">
    <div class="hero-media-fallback"></div>
    <!-- swap below src to any MP4/image URL for background media -->
    <!-- <video class="hero-media" autoplay muted loop playsinline src="YOUR_VIDEO_URL"></video> -->
    <div class="hero-overlay"></div>
    <div class="hero-content">
      <div style="font-family:'Courier Prime',monospace;font-size:9px;letter-spacing:0.22em;color:var(--orange);text-transform:uppercase;margin-bottom:8px;display:flex;align-items:center;gap:8px;"><span style="display:block;width:20px;height:1px;background:var(--orange)"></span>Langue Vivante — Module I</div>
      <h1>Le <em>Français</em> Profond</h1>
      <p class="hero-sub">Une méthode d'immersion hypnotique. Chaque mot s'imprime.</p>
      <div class="hero-btns">
        <button class="btn-p" onclick="go('lesson')">Commencer →</button>
        <button class="btn-g" onclick="go('brain')">Mode mémoire</button>
      </div>
    </div>
  </div>

  <div class="themes-wrap">
    <div class="slabel">Thèmes</div>
    <div class="themes-grid" id="themes-grid"></div>
  </div>
</div>

<!-- LESSON -->
<div class="page" id="page-lesson">
  <div class="lesson-wrap">
    <div class="lesson-hdr">
      <div class="lesson-hdr-top">
        <div>
          <div style="font-family:'Courier Prime',monospace;font-size:9px;letter-spacing:0.18em;color:var(--orange);text-transform:uppercase;margin-bottom:6px;">Module I — Société &amp; Histoire</div>
          <h1 class="lesson-title">Le 1<sup style="font-size:0.5em">er</sup>&nbsp;Mai</h1>
        </div>
        <button id="bm-btn" class="btn-sm" onclick="toggleBM('mai')">☆ Bookmark</button>
      </div>
      <div class="lesson-meta">
        <span class="ts">OCT 26 '99</span>
        <span style="font-size:10px;color:var(--muted);">7 mots · 3 phrases · B2</span>
      </div>
    </div>

    <div class="video-wrap">
      <iframe src="https://www.youtube.com/embed/aeA6btkJMIM?rel=0&modestbranding=1" allowfullscreen allow="accelerometer;autoplay;clipboard-write;encrypted-media;gyroscope;picture-in-picture"></iframe>
    </div>

    <div class="slabel">Vocabulaire clé</div>
    <div class="vocab-grid" id="vocab-grid"></div>

    <div class="divider"></div>
    <div class="slabel">Phrases essentielles</div>
    <div class="phrase-list" id="phrase-list"></div>

    <div class="divider"></div>
    <div class="slabel">À retenir</div>
    <div class="polaroid">
      <div class="pol-inner">
        <div style="text-align:center;padding:12px;">
          <div style="font-family:'Playfair Display',serif;font-size:26px;font-weight:900;color:var(--orange);margin-bottom:4px;">1er Mai</div>
          <div style="font-family:'Courier Prime',monospace;font-size:8px;color:var(--muted);letter-spacing:0.12em;text-transform:uppercase;">JOURNÉE INTERNATIONALE</div>
        </div>
      </div>
      <div class="pol-text">Le 1er mai est un <em>jour férié chômé et payé</em> depuis 1947. Il célèbre les <strong>ouvriers</strong> et la <em>lutte des classes</em>.</div>
      <div class="pol-cap">OCT 26 '99 — SÉRIE 001</div>
    </div>

    <div style="display:flex;gap:10px;margin-top:16px;flex-wrap:wrap;">
      <button class="btn-p" onclick="go('brain')">Mode mémoire →</button>
      <button class="btn-g" onclick="go('home')">← Thèmes</button>
    </div>
  </div>
</div>

<!-- BRAIN -->
<div class="page" id="page-brain">
  <div class="brain-wrap">
    <div style="margin-bottom:16px;">
      <div style="font-family:'Courier Prime',monospace;font-size:9px;letter-spacing:0.18em;color:var(--orange);text-transform:uppercase;margin-bottom:4px;">Mode Mémoire</div>
      <h2 style="font-family:'Playfair Display',serif;font-size:28px;font-weight:900;color:var(--cream);">Brainwash <em style="font-style:italic;color:var(--orange)">Protocol</em></h2>
    </div>

    <div class="slabel">Banque de mots</div>
    <div class="wb-grid" id="wb-grid"></div>

    <div style="display:flex;gap:10px;align-items:center;flex-wrap:wrap;margin:14px 0 20px;">
      <button class="btn-p" onclick="startBW()">⚡ Activer brainwash</button>
      <span style="font-size:9px;color:var(--muted);letter-spacing:0.06em;">× 5 répétitions + audio</span>
    </div>

    <div class="divider"></div>
    <div class="slabel" style="margin-top:16px;">Quiz</div>
    <div class="qprog"><div class="qprog-fill" id="qpf" style="width:0%"></div></div>
    <div class="qword" id="qword">—</div>
    <div class="qlabel">Choisissez la traduction</div>
    <div class="qopts" id="qopts"></div>
    <div class="qfb" id="qfb"></div>
    <div class="mdots">
      <span class="mlabel">Maîtrisé</span>
      <div style="display:flex;gap:3px;" id="mdots"></div>
    </div>

    <div style="display:flex;gap:10px;margin-top:24px;flex-wrap:wrap;">
      <button class="btn-g" onclick="go('lesson')">← Leçon</button>
      <button class="btn-p" onclick="resetQ()">Recommencer</button>
    </div>
  </div>
</div>

<!-- SAVED -->
<div class="page" id="page-saved">
  <div class="saved-wrap">
    <div style="margin-bottom:16px;">
      <div style="font-family:'Courier Prime',monospace;font-size:9px;letter-spacing:0.18em;color:var(--orange);text-transform:uppercase;margin-bottom:4px;">Ma collection</div>
      <h2 style="font-family:'Playfair Display',serif;font-size:28px;font-weight:900;color:var(--cream);">Sauvegardé</h2>
    </div>

    <div class="slabel">Articles bookmarkés</div>
    <div id="bm-list"></div>

    <div class="divider"></div>
    <div class="slabel" style="margin-top:16px;">Mon vocabulaire</div>
    <div id="sv-list"></div>

    <div style="margin-top:20px;">
      <button class="btn-g" onclick="go('home')">← Retour</button>
    </div>
  </div>
</div>

<!-- POPUP -->
<div class="pop-ov" id="pop-ov"></div>

<script>
// ---- DATA ----
const VOCAB=[
  {word:"Ouvrier",type:"n.m.",trans:"Worker / laborer",mastered:false},
  {word:"Légaliser",type:"v.",trans:"To legalize",mastered:false},
  {word:"S'approprier",type:"v. pron.",trans:"To appropriate",mastered:false},
  {word:"Chômé",type:"adj.",trans:"Non-working day",mastered:false},
  {word:"Concorde",type:"n.f.",trans:"Harmony / concord",mastered:false},
  {word:"Lutte des classes",type:"n.f.",trans:"Class struggle",mastered:false},
  {word:"Muguet",type:"n.m.",trans:"Lily of the valley",mastered:false},
];
const PHRASES=["La journée de huit heures","Sous l'occupation","Un jour férié chômé et payé"];
const ARTS=[
  {id:'mai',title:'Le 1er Mai',tag:'Société · Histoire',stamp:"OCT 26 '99",bg:'linear-gradient(160deg,#1a2a1e,#0d1b2a)',featured:true},
  {id:'table',title:'La Table',tag:'Culture · Gastronomie',stamp:"NOV 02 '99",bg:'linear-gradient(160deg,#2a1a1a,#1a0d1a)',featured:false},
  {id:'rep',title:'La République',tag:'Politique · Liberté',stamp:"DEC 14 '99",bg:'linear-gradient(160deg,#1a1a2a,#0a0a1e)',featured:false},
];

// ---- STORAGE ----
function gBM(){try{return JSON.parse(localStorage.getItem('lb_bm')||'[]');}catch(e){return[];}}
function gSV(){try{return JSON.parse(localStorage.getItem('lb_sv')||'[]');}catch(e){return[];}}
function sBM(d){try{localStorage.setItem('lb_bm',JSON.stringify(d));}catch(e){}}
function sSV(d){try{localStorage.setItem('lb_sv',JSON.stringify(d));}catch(e){}}

function toggleBM(id){
  let bm=gBM(),i=bm.indexOf(id);
  if(i===-1){bm.push(id);toast('Article sauvegardé ★');}else{bm.splice(i,1);toast('Retiré');}
  sBM(bm);updateBMBtn(id);updateBadge();
  renderThemes();
}
function toggleSV(word,trans){
  let sv=gSV(),i=sv.findIndex(v=>v.word===word);
  if(i===-1){sv.push({word,trans});toast('Mot sauvegardé !');}else{sv.splice(i,1);toast('Mot retiré');}
  sSV(sv);updateBadge();renderVocab();
}

function updateBMBtn(id){
  const bm=gBM(),btn=document.getElementById('bm-btn');
  if(!btn) return;
  if(bm.includes(id)){btn.textContent='★ Bookmarké';btn.classList.add('on');}
  else{btn.textContent='☆ Bookmark';btn.classList.remove('on');}
}
function updateBadge(){
  const t=gBM().length+gSV().length;
  document.getElementById('sbadge').textContent=t>0?`(${t})`:'';
}

// ---- TOAST ----
function toast(msg){
  const el=document.getElementById('toast');
  el.textContent=msg;el.classList.add('on');
  clearTimeout(el._t);el._t=setTimeout(()=>el.classList.remove('on'),2000);
}

// ---- AUDIO ----
let voices=[];
function loadVoices(){voices=window.speechSynthesis?window.speechSynthesis.getVoices():[];}
if(window.speechSynthesis){
  loadVoices();
  window.speechSynthesis.onvoiceschanged=loadVoices;
}

function speak(word,cb){
  if(!window.speechSynthesis){if(cb)cb();return;}
  window.speechSynthesis.cancel();
  setTimeout(()=>{
    const u=new SpeechSynthesisUtterance(word);
    u.lang='fr-FR';u.rate=0.82;u.pitch=0.92;u.volume=1;
    if(!voices.length) voices=window.speechSynthesis.getVoices();
    const fr=voices.find(v=>v.lang&&v.lang.startsWith('fr'));
    if(fr) u.voice=fr;
    u.onend=()=>{if(cb)cb();};
    u.onerror=()=>{if(cb)cb();};
    window.speechSynthesis.speak(u);
  },80);
}

// ---- NAV ----
function go(p){
  document.querySelectorAll('.page').forEach(el=>el.classList.remove('active'));
  document.querySelectorAll('.nav-links button').forEach(b=>b.classList.remove('active'));
  document.getElementById('page-'+p).classList.add('active');
  const nb=document.getElementById('nb-'+p);
  if(nb) nb.classList.add('active');
  if(p==='home'){renderThemes();}
  if(p==='lesson'){renderVocab();updateBMBtn('mai');}
  if(p==='brain'){renderWB();renderQuiz();renderMD();}
  if(p==='saved'){renderSaved();}
  updateBadge();
  window.scrollTo(0,0);
}

// ---- THEMES ----
function renderThemes(){
  const grid=document.getElementById('themes-grid'),bm=gBM();
  grid.innerHTML='';
  ARTS.forEach(a=>{
    const d=document.createElement('div');
    d.className='tcard';
    d.style.cssText='position:relative;overflow:hidden;cursor:pointer;transition:all 0.25s;';
    d.innerHTML=`
      <div class="tcard-bg" style="background:${a.bg};position:absolute;inset:0;"></div>
      <div class="tcard-overlay"></div>
      ${a.featured?'<div class="tcard-badge">En cours</div>':''}
      <div class="tcard-stamp"><span class="ts" style="font-size:9px;">${a.stamp}</span></div>
      <div class="tcard-content">
        <div class="tcard-tag">${a.tag}</div>
        <h3>${a.title}</h3>
        <p>Cliquer pour la leçon</p>
      </div>
      <div class="tcard-bm">
        <button class="btn-sm ${bm.includes(a.id)?'on':''}" onclick="event.stopPropagation();toggleBM('${a.id}')">
          ${bm.includes(a.id)?'★':'☆'}
        </button>
      </div>
    `;
    if(a.featured) d.onclick=()=>go('lesson');
    grid.appendChild(d);
  });
}

// ---- VOCAB ----
function renderVocab(){
  const sv=gSV(),grid=document.getElementById('vocab-grid');
  grid.innerHTML='';
  VOCAB.forEach(v=>{
    const saved=sv.some(s=>s.word===v.word);
    const c=document.createElement('div');
    c.className='vcard';
    c.innerHTML=`
      <div class="vword">${v.word}</div>
      <div class="vtype">${v.type}</div>
      <div class="vtrans">${v.trans}</div>
      <div class="vbtns">
        <button class="btn-sm" onclick="trigSpeakBtn(this,'${v.word.replace(/'/g,"\\'")}')">▶</button>
        <button class="btn-sm ${saved?'on':''}" onclick="toggleSV('${v.word.replace(/'/g,"\\'")}','${v.trans.replace(/'/g,"\\'")}')">
          ${saved?'★':'☆'}
        </button>
      </div>
    `;
    grid.appendChild(c);
  });

  const pl=document.getElementById('phrase-list');
  pl.innerHTML='';
  PHRASES.forEach((ph,i)=>{
    pl.innerHTML+=`<div class="phrase-row">
      <div class="pnum">0${i+1}</div>
      <div class="ptext">「${ph}」</div>
    </div>`;
  });
}

function trigSpeakBtn(btn,word){
  btn.textContent='♪';
  speak(word,()=>{btn.textContent='▶';});
}

// ---- WORDBANK ----
function renderWB(){
  const wb=document.getElementById('wb-grid');
  wb.innerHTML='';
  VOCAB.forEach(v=>{
    const p=document.createElement('div');
    p.className='wb-pill '+(v.mastered?'done':'learning');
    p.textContent=v.word;
    p.onclick=()=>trigBW(v);
    wb.appendChild(p);
  });
}

// ---- BRAINWASH ----
let bwQ=[],bwI=0,bwR=0;
const REP=5;

function startBW(){
  bwQ=VOCAB.filter(v=>!v.mastered);
  if(!bwQ.length) bwQ=[...VOCAB];
  bwI=0;bwR=0;showBW();
}
function trigBW(v){bwQ=[v];bwI=0;bwR=0;showBW();}

function showBW(){
  if(bwI>=bwQ.length){closeBW();return;}
  const v=bwQ[bwI];
  const ov=document.getElementById('pop-ov');
  ov.innerHTML='';ov.classList.add('on');

  const positions=[
    {top:'10%',left:'4%'},{top:'16%',left:'50%'},
    {top:'50%',left:'12%'},{top:'56%',left:'52%'},
    {top:'30%',left:'26%'},
  ];
  const count=Math.min(bwR+1,positions.length);

  for(let i=0;i<count;i++){
    const pos=positions[i];
    const w=document.createElement('div');
    w.className='pop-win';
    w.style.top=pos.top;w.style.left=pos.left;
    const dots=Array.from({length:REP},(_,di)=>`<div class="pop-dot ${di<=bwR?'on':''}"></div>`).join('');
    w.innerHTML=`
      <div class="pop-bar">
        <span>MÉMOIRE.EXE</span>
        <button class="pop-x" onclick="nextBW()">✕</button>
      </div>
      <div class="pop-body">
        <div class="pop-word">${v.word}</div>
        <div class="pop-trans">${v.trans}</div>
        <div class="pop-cnt">Répétition ${bwR+1} / ${REP}</div>
        <div class="pop-dots">${dots}</div>
        <div class="pop-spk" id="spk-ind-${i}">♪ lecture...</div>
      </div>
    `;
    ov.appendChild(w);
  }
  // Speak after a tiny delay so DOM is ready
  speak(v.word, null);
}

function nextBW(){
  if(window.speechSynthesis) window.speechSynthesis.cancel();
  bwR++;
  if(bwR>=REP){bwR=0;bwI++;if(bwI>=bwQ.length){closeBW();return;}}
  showBW();
}
function closeBW(){
  if(window.speechSynthesis) window.speechSynthesis.cancel();
  const ov=document.getElementById('pop-ov');
  ov.classList.remove('on');ov.innerHTML='';
}
document.getElementById('pop-ov').addEventListener('click',function(e){if(e.target===this)nextBW();});

// ---- QUIZ ----
let qI=0,qM=0,qAns=false,qQ=[...VOCAB];

function renderQuiz(){
  if(!qQ.length){qQ=[...VOCAB];qM=0;}
  qAns=false;
  const v=qQ[qI%qQ.length];
  document.getElementById('qword').textContent=v.word;
  const others=VOCAB.filter(x=>x.word!==v.word).sort(()=>Math.random()-0.5).slice(0,3);
  const ch=[...others,v].sort(()=>Math.random()-0.5);
  const keys=['A','B','C','D'];
  const opts=document.getElementById('qopts');
  opts.innerHTML='';
  ch.forEach((c,i)=>{
    const b=document.createElement('button');
    b.className='qopt';b.setAttribute('data-k',keys[i]);b.textContent=c.trans;
    b.onclick=()=>checkQ(c.trans,v,b);
    opts.appendChild(b);
  });
  document.getElementById('qfb').textContent='';
  document.getElementById('qfb').className='qfb';
  document.getElementById('qpf').style.width=Math.round((qM/VOCAB.length)*100)+'%';
}

function checkQ(chosen,vocab,btn){
  if(qAns) return;
  qAns=true;
  document.querySelectorAll('.qopt').forEach(b=>b.disabled=true);
  if(chosen===vocab.trans){
    btn.classList.add('ok');
    document.getElementById('qfb').textContent='✓ Correct !';
    document.getElementById('qfb').className='qfb ok';
    if(!vocab.mastered){vocab.mastered=true;qM=Math.min(qM+1,VOCAB.length);}
    renderMD();speak(vocab.word,null);
    setTimeout(()=>{qI++;renderQuiz();},1300);
  } else {
    btn.classList.add('no');
    document.querySelectorAll('.qopt').forEach(b=>{if(b.textContent===vocab.trans)b.classList.add('ok');});
    document.getElementById('qfb').textContent='✗ Brainwash activé !';
    document.getElementById('qfb').className='qfb no';
    setTimeout(()=>{
      trigBW(vocab);
      setTimeout(()=>{qAns=false;renderQuiz();},3000);
    },900);
  }
}

function renderMD(){
  const md=document.getElementById('mdots');
  md.innerHTML='';
  VOCAB.forEach(v=>{
    const d=document.createElement('div');
    d.className='mdot'+(v.mastered?' on':'');
    d.title=v.word;
    md.appendChild(d);
  });
}
function resetQ(){VOCAB.forEach(v=>v.mastered=false);qI=0;qM=0;qQ=[...VOCAB];renderWB();renderQuiz();renderMD();}

// ---- SAVED ----
function renderSaved(){
  const bm=gBM(),sv=gSV();
  const bl=document.getElementById('bm-list');
  bl.innerHTML='';
  if(!bm.length){bl.innerHTML='<div class="empty">Aucun article sauvegardé</div>';}
  else bm.forEach(id=>{
    const a=ARTS.find(x=>x.id===id);if(!a) return;
    const c=document.createElement('div');
    c.className='bm-card';
    c.onclick=()=>go('lesson');
    c.innerHTML=`
      <div><div class="bm-title">${a.title}</div><div class="bm-meta">${a.tag} · ${a.stamp}</div></div>
      <button onclick="event.stopPropagation();toggleBM('${id}');renderSaved();" class="btn-sm">Retirer</button>
    `;
    bl.appendChild(c);
  });

  const sl=document.getElementById('sv-list');
  sl.innerHTML='';
  if(!sv.length){sl.innerHTML='<div class="empty">Aucun mot sauvegardé</div>';}
  else sv.forEach(v=>{
    const r=document.createElement('div');
    r.className='sv-row';
    r.innerHTML=`
      <div><div class="sv-word">${v.word}</div><div class="sv-trans">${v.trans}</div></div>
      <div class="sv-acts">
        <button class="btn-sm" onclick="trigSpeakBtn(this,'${v.word.replace(/'/g,"\\'")}')">▶</button>
        <button class="btn-sm" onclick="toggleSV('${v.word.replace(/'/g,"\\'")}','${v.trans.replace(/'/g,"\\'")}');renderSaved();">Retirer</button>
      </div>
    `;
    sl.appendChild(r);
  });
}

// INIT
loadVoices();
renderThemes();
updateBadge();
</script>
</body>
</html>
