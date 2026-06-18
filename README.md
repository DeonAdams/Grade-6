<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>🌾 Fair Trade Adventure Quiz</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@700;900&family=Exo+2:wght@400;600;700&display=swap" rel="stylesheet"/>
<style>
/* ══ THEME VARIABLES ══ */
:root{
  /* Section 1 — Fair Trade — warm harvest gold/green (agriculture) */
  --fair:#10b981;--fair2:#059669;--fair3:#6ee7b7;
  /* Section 2 — Unfair Trade — blood red/dark (slavery) */
  --unfair:#ef4444;--unfair2:#b91c1c;--unfair3:#fca5a5;
  /* Section 3 — Case Study/Word Salad — amber (justice) */
  --case:#f59e0b;--case2:#d97706;--case3:#fde68a;
  --green:#10b981;--red:#ef4444;--amber:#f59e0b;
  --dark:#080c14;--mid:#0d1a2e;
  --text:#f0fdf4;--subtext:rgba(200,240,210,.85);
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;}
body{font-family:'Exo 2',sans-serif;background:var(--dark);color:var(--text);min-height:100vh;overflow-x:hidden;padding-bottom:70px;}

/* ══ BACKGROUND — wheat field rows ══ */
.bg-layer{position:fixed;top:0;left:0;right:0;bottom:0;z-index:0;pointer-events:none;
  background-image:
    linear-gradient(rgba(16,185,129,.025) 1px,transparent 1px),
    linear-gradient(90deg,rgba(16,185,129,.025) 1px,transparent 1px);
  background-size:44px 44px;}
.glow{position:fixed;border-radius:50%;pointer-events:none;z-index:0;animation:gp 8s ease-in-out infinite;}
.glow:nth-child(2){width:700px;height:700px;top:-250px;left:-200px;background:radial-gradient(circle,rgba(16,185,129,.07) 0%,transparent 65%);}
.glow:nth-child(3){width:500px;height:500px;bottom:-150px;right:-120px;background:radial-gradient(circle,rgba(239,68,68,.06) 0%,transparent 65%);animation-delay:4s;}
@keyframes gp{0%,100%{opacity:.4;}50%{opacity:1;}}

/* ══ HEADER ══ */
.sticky-header{position:sticky;top:0;z-index:100;background:rgba(8,12,20,.97);
  backdrop-filter:blur(16px);padding:11px 16px;
  border-bottom:2px solid rgba(16,185,129,.4);
  box-shadow:0 2px 28px rgba(16,185,129,.15);}
.header-title{font-family:'Orbitron',monospace;font-size:clamp(.6rem,2.2vw,.88rem);font-weight:900;
  color:var(--fair);text-align:center;letter-spacing:.14em;text-transform:uppercase;margin-bottom:6px;
  text-shadow:0 0 16px rgba(16,185,129,.7);}
.score-board{display:flex;justify-content:space-around;}
.score-item{flex:1;text-align:center;}
.score-label{font-size:.6rem;color:rgba(16,185,129,.6);font-weight:700;letter-spacing:.08em;text-transform:uppercase;margin-bottom:2px;}
.score-value{font-family:'Orbitron',monospace;font-size:.92rem;font-weight:700;}

/* ══ PROGRESS BAR ══ */
.prog-wrap{background:rgba(8,12,20,.92);padding:6px 16px;position:sticky;top:66px;z-index:99;
  border-bottom:1px solid rgba(16,185,129,.1);}
.prog-bg{background:rgba(255,255,255,.07);border-radius:20px;height:6px;overflow:hidden;margin-bottom:3px;}
.prog-fill{height:100%;border-radius:20px;transition:width .4s ease;}
.prog-fill.fair{background:linear-gradient(90deg,var(--fair),var(--fair2));box-shadow:0 0 10px rgba(16,185,129,.6);}
.prog-fill.unfair{background:linear-gradient(90deg,var(--unfair),var(--unfair2));box-shadow:0 0 10px rgba(239,68,68,.6);}
.prog-fill.case{background:linear-gradient(90deg,var(--case),var(--case2));box-shadow:0 0 10px rgba(245,158,11,.6);}
.prog-fill.none{background:linear-gradient(90deg,var(--fair),var(--case));}
.prog-label{text-align:right;font-size:.6rem;color:rgba(16,185,129,.5);font-weight:600;}

/* ══ LAYOUT ══ */
.wrapper{max-width:900px;margin:0 auto;padding:24px 14px;position:relative;z-index:1;}

/* ══ HOME ══ */
.section-home{text-align:center;margin-top:16px;}
.sh-title{font-family:'Orbitron',monospace;font-size:clamp(.95rem,3.8vw,1.65rem);margin-bottom:8px;}
.sh-title.fair{color:var(--fair);text-shadow:0 0 22px rgba(16,185,129,.5);}
.sh-title.unfair{color:var(--unfair);text-shadow:0 0 22px rgba(239,68,68,.5);}
.sh-title.case{color:var(--case);text-shadow:0 0 22px rgba(245,158,11,.5);}
.sh-sub{font-size:.87rem;letter-spacing:.09em;margin-bottom:26px;}
.sh-sub.fair{color:rgba(16,185,129,.55);}
.sh-sub.unfair{color:rgba(239,68,68,.5);}
.sh-sub.case{color:rgba(245,158,11,.5);}

/* ══ SECTION CARDS ══ */
.section-cards{display:grid;grid-template-columns:repeat(3,1fr);gap:16px;max-width:800px;margin:0 auto;}
@media(max-width:600px){.section-cards{grid-template-columns:1fr;}}
.section-card{border-radius:18px;padding:26px 14px;cursor:pointer;text-align:center;
  transition:all .3s;box-shadow:0 4px 24px rgba(0,0,0,.5);border:2px solid transparent;}
.section-card.fair-card{background:linear-gradient(145deg,rgba(0,25,15,.9),rgba(0,20,10,.95));border-color:rgba(16,185,129,.3);}
.section-card.fair-card:hover{border-color:var(--fair);box-shadow:0 6px 36px rgba(16,185,129,.3);transform:translateY(-5px);}
.section-card.unfair-card{background:linear-gradient(145deg,rgba(30,5,5,.9),rgba(40,0,0,.95));border-color:rgba(239,68,68,.3);}
.section-card.unfair-card:hover{border-color:var(--unfair);box-shadow:0 6px 36px rgba(239,68,68,.3);transform:translateY(-5px);}
.section-card.case-card{background:linear-gradient(145deg,rgba(25,15,0,.9),rgba(35,20,0,.95));border-color:rgba(245,158,11,.3);}
.section-card.case-card:hover{border-color:var(--case);box-shadow:0 6px 36px rgba(245,158,11,.3);transform:translateY(-5px);}
.section-card .ci{font-size:44px;margin-bottom:12px;display:block;}
.section-card .cn{font-family:'Orbitron',monospace;font-size:.76rem;font-weight:900;letter-spacing:.08em;margin-bottom:5px;}
.fair-card .cn{color:var(--fair);}
.unfair-card .cn{color:var(--unfair);}
.case-card .cn{color:var(--case);}
.section-card .cd{font-size:.72rem;color:rgba(200,230,200,.4);line-height:1.45;}

/* ══ CONTENT CARD ══ */
.card{background:rgba(8,14,24,.95);border-radius:18px;padding:24px 20px;margin-bottom:18px;
  box-shadow:0 4px 24px rgba(0,0,0,.6);position:relative;overflow:hidden;animation:fsIn .35s ease;}
.card::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;}
.card.fair-card::before{background:linear-gradient(90deg,var(--fair),var(--fair2),var(--fair3));}
.card.unfair-card::before{background:linear-gradient(90deg,var(--unfair),var(--unfair2),var(--unfair3));}
.card.case-card::before{background:linear-gradient(90deg,var(--case),var(--case2),var(--case3));}
.card.fair-card{border:2px solid rgba(16,185,129,.2);}
.card.unfair-card{border:2px solid rgba(239,68,68,.2);}
.card.case-card{border:2px solid rgba(245,158,11,.2);}
@keyframes fsIn{from{opacity:0;transform:translateY(14px);}to{opacity:1;transform:translateY(0);}}

.card-title{font-family:'Orbitron',monospace;font-size:clamp(.82rem,2.8vw,1.1rem);
  text-align:center;margin-bottom:16px;letter-spacing:.1em;}
.card-title.fair{color:var(--fair);text-shadow:0 0 10px rgba(16,185,129,.4);}
.card-title.unfair{color:var(--unfair);text-shadow:0 0 10px rgba(239,68,68,.4);}
.card-title.case{color:var(--case);text-shadow:0 0 10px rgba(245,158,11,.4);}

.intro-text{font-size:.89rem;line-height:1.65;color:var(--subtext);margin-bottom:14px;}
.info-box{border-radius:8px;padding:14px;margin:14px 0;font-size:.86rem;line-height:1.65;color:var(--subtext);}
.info-box.fair{background:rgba(16,185,129,.07);border-left:4px solid var(--fair);}
.info-box.unfair{background:rgba(239,68,68,.07);border-left:4px solid var(--unfair);}
.info-box.case{background:rgba(245,158,11,.07);border-left:4px solid var(--case);}

/* ══ MEME PANEL ══ */
.meme-panel{font-size:clamp(2.8rem,10vw,5rem);text-align:center;margin:10px 0 4px;
  animation:memePop .4s cubic-bezier(.34,1.56,.64,1);}
@keyframes memePop{from{transform:scale(0) rotate(-12deg);}to{transform:scale(1) rotate(0);}}
.meme-caption{text-align:center;font-size:.76rem;letter-spacing:.09em;
  font-family:'Orbitron',monospace;margin-bottom:14px;}
.meme-caption.fair{color:rgba(16,185,129,.55);}
.meme-caption.unfair{color:rgba(239,68,68,.55);}
.meme-caption.case{color:rgba(245,158,11,.55);}

/* ══ MCQ OPTIONS ══ */
.opt-btn{display:flex;align-items:center;gap:12px;width:100%;min-height:52px;padding:13px 16px;
  background:rgba(255,255,255,.04);border-radius:12px;cursor:pointer;font-size:.9rem;
  color:#d4fce8;text-align:left;font-family:'Exo 2',sans-serif;font-weight:500;transition:all .2s;}
.opt-btn.fair-opt{border:1.5px solid rgba(16,185,129,.2);}
.opt-btn.fair-opt:hover:not(.disabled){background:rgba(16,185,129,.1);border-color:var(--fair);color:#fff;transform:translateX(4px);}
.opt-btn.unfair-opt{border:1.5px solid rgba(239,68,68,.2);}
.opt-btn.unfair-opt:hover:not(.disabled){background:rgba(239,68,68,.1);border-color:var(--unfair);color:#fff;transform:translateX(4px);}
.opt-btn.case-opt{border:1.5px solid rgba(245,158,11,.2);}
.opt-btn.case-opt:hover:not(.disabled){background:rgba(245,158,11,.1);border-color:var(--case);color:#fff;transform:translateX(4px);}
.opt-btn.correct{background:rgba(16,185,129,.18)!important;border-color:var(--green)!important;color:#d1fae5!important;}
.opt-btn.incorrect{background:rgba(239,68,68,.14)!important;border-color:var(--red)!important;color:#fee2e2!important;}
.opt-btn.disabled{cursor:not-allowed;}
.oi{font-size:20px;flex-shrink:0;}

/* ══ BUTTONS ══ */
.action-btn{display:block;width:100%;max-width:360px;margin:14px auto 0;padding:14px 24px;
  border:none;border-radius:50px;font-family:'Orbitron',monospace;font-size:.78rem;font-weight:900;
  letter-spacing:.08em;cursor:pointer;color:#040810;min-height:48px;transition:transform .2s;}
.action-btn:hover{transform:scale(1.03);}
.action-btn:active{transform:scale(.97);}
.action-btn.fair{background:linear-gradient(135deg,var(--fair),var(--fair2));box-shadow:0 4px 20px rgba(16,185,129,.4);}
.action-btn.unfair{background:linear-gradient(135deg,var(--unfair),var(--unfair2));box-shadow:0 4px 20px rgba(239,68,68,.4);}
.action-btn.case{background:linear-gradient(135deg,var(--case),var(--case2));box-shadow:0 4px 20px rgba(245,158,11,.4);}

.back-btn{display:block;width:100%;max-width:360px;margin:10px auto 0;padding:13px 24px;
  background:rgba(255,255,255,.05);border-radius:50px;font-family:'Exo 2',sans-serif;
  font-size:.8rem;font-weight:600;cursor:pointer;min-height:48px;transition:background .2s;}
.back-btn:hover{background:rgba(255,255,255,.1);}
.back-btn.fair{border:1.5px solid rgba(16,185,129,.28);color:var(--fair);}
.back-btn.unfair{border:1.5px solid rgba(239,68,68,.28);color:var(--unfair);}
.back-btn.case{border:1.5px solid rgba(245,158,11,.28);color:var(--case);}

.section-back{display:block;width:100%;max-width:360px;margin:12px auto 0;padding:12px 24px;
  background:rgba(255,255,255,.04);border:1.5px solid rgba(255,255,255,.1);color:rgba(255,255,255,.45);
  border-radius:50px;font-family:'Exo 2',sans-serif;font-size:.78rem;cursor:pointer;transition:all .2s;}
.section-back:hover{background:rgba(255,255,255,.09);color:rgba(255,255,255,.8);}

/* ══ Q-NUMBER BADGE ══ */
.q-badge{display:flex;align-items:center;justify-content:center;width:38px;height:38px;
  border-radius:50%;margin:0 auto 16px;font-family:'Orbitron',monospace;font-weight:900;
  font-size:.85rem;color:#04080e;}
.q-badge.fair{background:linear-gradient(135deg,var(--fair),var(--fair2));box-shadow:0 0 14px rgba(16,185,129,.5);}
.q-badge.unfair{background:linear-gradient(135deg,var(--unfair),var(--unfair2));box-shadow:0 0 14px rgba(239,68,68,.5);}
.q-badge.case{background:linear-gradient(135deg,var(--case),var(--case2));box-shadow:0 0 14px rgba(245,158,11,.5);}

/* ══ RESULTS ══ */
.results-box{text-align:center;padding:28px 16px;}
.res-title{font-family:'Orbitron',monospace;font-size:1.1rem;margin-bottom:10px;letter-spacing:.1em;}
.res-title.fair{color:var(--fair);}
.res-title.unfair{color:var(--unfair);}
.res-title.case{color:var(--case);}
.res-score{font-size:1.05rem;margin:10px 0;font-weight:600;}
.stars-row{font-size:1.7rem;margin:10px 0;letter-spacing:2px;}

/* ══ WORD SALAD ══ */
.word-salad-wrap{margin:18px 0;display:flex;flex-wrap:wrap;gap:10px;justify-content:center;}
.ws-word{padding:9px 16px;border-radius:50px;font-size:.85rem;font-weight:700;cursor:pointer;
  background:rgba(245,158,11,.1);border:2px solid rgba(245,158,11,.3);color:var(--case3);
  transition:all .22s;font-family:'Exo 2',sans-serif;user-select:none;}
.ws-word:hover{background:rgba(245,158,11,.2);border-color:var(--case);transform:scale(1.06);}
.ws-word.selected{background:rgba(245,158,11,.28);border-color:var(--case);color:#fff;transform:scale(1.08);}
.ws-word.correct-word{background:rgba(16,185,129,.25);border-color:var(--green);color:#d1fae5;cursor:default;}
.ws-word.wrong-word{background:rgba(239,68,68,.2);border-color:var(--red);color:#fee2e2;cursor:default;}
.ws-selected-area{min-height:44px;background:rgba(245,158,11,.05);border:1.5px dashed rgba(245,158,11,.25);
  border-radius:12px;padding:10px 14px;margin-top:10px;font-size:.88rem;color:var(--case3);
  display:flex;flex-wrap:wrap;gap:8px;align-items:center;}
.check-btn{padding:11px 26px;border-radius:50px;border:none;font-family:'Orbitron',monospace;
  font-size:.75rem;font-weight:900;cursor:pointer;letter-spacing:.07em;margin-right:8px;transition:transform .2s;}
.check-btn:hover{transform:scale(1.03);}
.check-btn.case{background:linear-gradient(135deg,var(--case),var(--case2));color:#040810;box-shadow:0 3px 14px rgba(245,158,11,.35);}
.check-btn.fair{background:linear-gradient(135deg,var(--fair),var(--fair2));color:#040810;}
.check-btn.unfair{background:linear-gradient(135deg,var(--unfair),var(--unfair2));color:#040810;}
.reset-btn{padding:11px 22px;border-radius:50px;background:transparent;font-size:.75rem;
  font-family:'Exo 2',sans-serif;cursor:pointer;border:1.5px solid rgba(245,158,11,.28);color:var(--case);}
.score-bar{font-size:.86rem;font-weight:700;margin-top:10px;}
.score-bar.case{color:var(--case);}
.score-bar.fair{color:var(--fair);}
.score-bar.unfair{color:var(--unfair);}
.hint-text{font-size:.74rem;color:rgba(245,158,11,.8);margin-top:6px;display:none;}
.hint-text.show{display:block;}
.fi{font-size:1.1rem;margin-left:4px;}
.feedback-box{border-radius:8px;padding:13px;margin-top:12px;font-size:.85rem;line-height:1.6;animation:fsIn .3s ease;}
.feedback-box.fb-correct{background:rgba(16,185,129,.12);border-left:4px solid var(--green);color:#d1fae5;}
.feedback-box.fb-wrong{background:rgba(245,158,11,.08);border-left:4px solid var(--case);color:var(--case3);}
.next-btn{display:none;margin:16px auto 0;}
@media(min-width:640px){.section-cards{grid-template-columns:repeat(3,1fr);}}
</style>
</head>
<body>
<div class="bg-layer"></div><div class="glow"></div><div class="glow"></div>

<div class="sticky-header">
  <div class="header-title" id="hTitle">🌾 FAIR TRADE ADVENTURE QUIZ ⚖️</div>
  <div class="score-board">
    <div class="score-item"><div class="score-label">Section</div><div class="score-value" id="hPart">-</div></div>
    <div class="score-item"><div class="score-label">Score</div><div class="score-value" id="hScore">0</div></div>
    <div class="score-item"><div class="score-label">Stars</div><div class="score-value" id="hStars">☆</div></div>
  </div>
</div>
<div class="prog-wrap">
  <div class="prog-bg"><div class="prog-fill none" id="pFill" style="width:0%"></div></div>
  <div class="prog-label" id="pLabel">&nbsp;</div>
</div>
<div class="wrapper" id="main"></div>

<script>
// ═══════════════════════════════════════════════════════
// MEME HELPER
// ═══════════════════════════════════════════════════════
const MEMES = {
  fair:{
    correct:['🌾✅','🤝💚','☀️🌱','🏅🌿','🎉🌾'],
    wrong:['🌧️❓','🤔🌱','📖🌿','💭❌','🌾⚠️'],
    great:'🏆🌾',good:'🌱📋',low:'📖🌿'
  },
  unfair:{
    correct:['🔍✅','⛓️💡','🕵️✔️','🚨✅','👁️💚'],
    wrong:['⛓️❓','🚨📖','🌑❌','💢📚','🔗⚠️'],
    great:'🔓🏆',good:'🔍📋',low:'📖⛓️'
  },
  case:{
    correct:['⚖️✅','📜💚','🔑✔️','💡✅','🕊️💚'],
    wrong:['⚖️❓','📜❌','🔑📖','💡⚠️','🕊️⚠️'],
    great:'⚖️🏆',good:'📜📋',low:'📖⚖️'
  }
};
function rand(a){return a[Math.floor(Math.random()*a.length)];}
function meme(theme,key){
  const em=typeof key==='number'
    ?rand(MEMES[theme][key===1?'correct':'wrong'])
    :MEMES[theme][key];
  const caps={fair:{correct:'FAIR TRADE HERO!',wrong:'CHECK YOUR NOTES!',great:'AGRICULTURE CHAMPION!',good:'SOLID WORK!',low:'REVISE & RETRY!'},
    unfair:{correct:'EXPLOITATION SPOTTER!',wrong:'LOOK AGAIN!',great:'JUSTICE HERO!',good:'GOOD ANALYSIS!',low:'REVIEW THE NOTES!'},
    case:{correct:'TRADE DETECTIVE!',wrong:'THINK IT THROUGH!',great:'EQUITY MASTER!',good:'NICE WORK!',low:'STUDY AND RETRY!'}};
  const capArr=caps[theme];
  const cap=typeof key==='number'?capArr[key===1?'correct':'wrong']:capArr[key];
  return `<div class="meme-panel">${em}</div><div class="meme-caption ${theme}">${cap}</div>`;
}

// ═══════════════════════════════════════════════════════
// SECTION 1 — FAIR TRADE (10 MCQ, agriculture theme)
// ═══════════════════════════════════════════════════════
const FAIR_QS = [
  {
    q:"🌾 Amara is a coffee farmer in Ethiopia. She sells her beans through a fair trade cooperative. The buyers agree to pay R18 per kg — above the market rate of R12. What is the MAIN fair trade principle this shows?",
    opts:["Buyers should always pay the lowest possible price to save money","Fair trade ensures sellers receive a DECENT and agreed-upon price for their crops","Buyers choose the price and sellers must accept it","Prices are set only by large supermarkets"],
    c:1,
    exp:"In FAIR TRADE, buyers and sellers AGREE on a fair price that covers the real cost of production and allows farmers to earn enough to live. Amara's cooperative is an example of this principle in action — she earns R18/kg instead of being forced to accept R12/kg."
  },
  {
    q:"👶 The Kuapa Kokoo cocoa cooperative in Ghana ensures that children in member families are NOT required to work on farms during school hours. Which fair trade benefit does this represent?",
    opts:["Lower product prices for consumers","Workers forming companies to control prices","Fair trade helps stop child labour by paying parents enough so children can go to school","Fair trade only benefits buyers in developed countries"],
    c:2,
    exp:"One of the key benefits of fair trade is that when parents earn FAIR WAGES, they can afford to send their children to school. The Kuapa Kokoo cooperative in Ghana is a real example — fair trade income helped build schools and remove the need for child labour."
  },
  {
    q:"🏥 The Body Shop buys shea nut butter from women farmers in Ghana at a fair trade price. The women use the extra income to pay for community health care and build a small clinic. Which fair trade outcome does this show?",
    opts:["Fair trade increases the price of products so only rich people can buy them","Fair trade income allows communities to fund health care and education services","Fair trade means buyers can choose any price they like","The Body Shop forces farmers to use only natural products"],
    c:1,
    exp:"FAIR TRADE income goes back into the community. Anita Roddick (founder of The Body Shop) said the business helped women farmers in Ghana buy books and school uniforms and improve community services. This is a direct benefit of fair trade to sellers and their families."
  },
  {
    q:"🤝 A Belgian chocolate company visits a cocoa farming village in Ghana. Instead of setting the price themselves, they SIT DOWN WITH FARMERS and agree together on a price that covers costs AND leaves a profit for the farmers. What type of trade is this?",
    opts:["Unfair trade — the company is wasting time","Free trade — prices are set by the market","Fair trade — buyers and sellers agree on a fair price together","Forced trade — the company is exploiting the farmers"],
    c:2,
    exp:"This is FAIR TRADE. Fair trade happens when countries and companies agree to buy goods at DECENT PRICES from companies that pay workers fairly and treat them well. The key element here is MUTUAL AGREEMENT on price — not one side forcing the other."
  },
  {
    q:"🌿 Which of the following is a benefit of fair trade for WORKERS (sellers)?",
    opts:[
      "Workers earn less so prices can be kept low for buyers",
      "Workers are paid fair wages, work in safe conditions, and have money to send children to school",
      "Fair trade means workers work longer hours for the same pay",
      "Workers must give most of their earnings to the government"
    ],
    c:1,
    exp:"According to the textbook, fair trade benefits workers by: paying FAIR WAGES, providing SAFE and healthy working conditions, funding health care and education, and giving workers the power to form companies for more control over prices."
  },
  {
    q:"☕ A South African retailer decides to only stock coffee that carries the FAIRTRADE FOUNDATION mark. What does this label guarantee consumers?",
    opts:[
      "The product is the cheapest available",
      "The product was made in a developed country",
      "The product was produced according to fair trading standards — workers were paid fairly and treated well",
      "The product has no artificial ingredients"
    ],
    c:2,
    exp:"The INTERNATIONAL FAIRTRADE mark (the blue and green symbol) shows that products have been produced according to FAIR TRADING STANDARDS. This means farmers and workers received fair prices, safe working conditions, and the trade met ethical requirements."
  },
  {
    q:"🏘️ A cocoa farmer in Ghana earns a fair trade premium — extra money above the crop price. The farmers collectively decide to use this premium to build a water dam and improve their village. What does this show about fair trade?",
    opts:[
      "Fair trade only helps individual farmers, not communities",
      "Fair trade forces farmers to spend money on infrastructure",
      "Fair trade premiums help communities invest in their own development — like clean water and schools",
      "The dam was built by the Belgian chocolate company, not the farmers"
    ],
    c:2,
    exp:"The FAIRTRADE PREMIUM is extra money paid above the crop price specifically for community development. In the textbook case study, fair trade income helped a Ghanaian cocoa village build a school AND a small dam, and gave children access to CLEAN and SAFE WATER. This is the community development power of fair trade."
  },
  {
    q:"👗 Hasina makes sports shoes in Bangladesh. Under fair trade conditions, her employer would be required to do which THREE things?",
    opts:[
      "Pay her R20/day, give her 12-hour shifts, and allow no sick leave",
      "Pay a fair wage, ensure safe working conditions, and limit working hours to a reasonable number",
      "Make her work on Sundays and give her less pay to keep prices competitive",
      "Transfer her to a factory in a developed country so wages are automatically higher"
    ],
    c:1,
    exp:"Under FAIR TRADE principles, Hasina's employer would need to: pay a FAIR WAGE (not R20/day), ensure SAFE and HEALTHY working conditions (not dangerous tools), and set REASONABLE WORKING HOURS. Her current situation — R20/day, 12 hours/day, 6 days/week — is exploitation, NOT fair trade."
  },
  {
    q:"🌍 Zanele visits a supermarket and sees two bars of soap. One costs R20 (regular supplier) and one costs R25 (fair trade supplier). The fair trade soap has no artificial chemicals. Is the R25 fair trade soap BETTER VALUE?",
    opts:[
      "No — more expensive always means worse value",
      "Yes — the higher price ensures the seller is paid fairly, the product is natural, and communities benefit",
      "No — both soaps do the same thing so the cheap one is always better",
      "Yes — but only because it has no artificial chemicals, not because of fair trade"
    ],
    c:1,
    exp:"The textbook (Activity 12) asks exactly this question. The R25 FAIR TRADE soap offers better VALUE because: (1) the seller is paid a fair price, (2) workers have safe conditions, (3) it has NO ARTIFICIAL CHEMICALS, and (4) the premium supports community development. 'Better value' means more than just price — it includes social and ethical benefits."
  },
  {
    q:"🔄 Workers on a fair trade certified coffee farm in Colombia decide to form a CO-OPERATIVE. What is the advantage of workers forming companies or cooperatives under fair trade?",
    opts:[
      "It means workers no longer need to farm — they become managers",
      "Workers have more control over prices and wages when they organise together",
      "Cooperatives reduce the quality of products because too many people are involved",
      "Forming a cooperative means buyers pay less for the product"
    ],
    c:1,
    exp:"One of the key fair trade principles (from page 43 of the textbook) is: 'Workers form companies so that they have MORE CONTROL over prices and wages.' A COOPERATIVE gives farmers collective bargaining power — they negotiate together rather than alone, which helps them get fairer prices from buyers."
  }
];

// ═══════════════════════════════════════════════════════
// SECTION 2 — UNFAIR TRADE (10 MCQ, slavery theme)
// ═══════════════════════════════════════════════════════
const UNFAIR_QS = [
  {
    q:"⛓️ A cocoa buyer from Europe arrives at a farm in Ivory Coast. He offers to pay R5 per kg for cocoa — well below what it costs the farmer to produce it (R8/kg). The farmer has no other buyers and is forced to accept. Which UNFAIR TRADE practice does this show?",
    opts:[
      "Fair negotiation — the buyer has the right to offer any price",
      "The PRICE of raw materials is decided by BUYERS, not sellers — leaving producers earning less than production costs",
      "The farmer should have grown a different crop",
      "This is normal market behaviour — prices always drop"
    ],
    c:1,
    exp:"This is UNFAIR TRADE. The textbook explains: 'the PRICE of raw materials is decided by buyers, not by the sellers.' When prices are set too low, farmers cannot even cover their costs. This keeps many countries POOR and is a central feature of unfair trade."
  },
  {
    q:"💀 Hamed lives in Ivory Coast. A man promised to help him get an education, but instead forced him to work on a cocoa farm — using dangerous tools and poisonous chemicals — for very little pay. Which form of exploitation does this represent?",
    opts:[
      "Skills training — Hamed is learning useful agricultural skills",
      "Child labour and exploitation — Hamed was deceived and forced into dangerous, low-paid work",
      "Fair trade — the man is providing Hamed with work experience",
      "Government employment — cocoa farming is required by law in Ivory Coast"
    ],
    c:1,
    exp:"This is EXPLOITATION — treating people in a selfish and unfair way. Hamed's story (textbook p.44) shows: DECEPTION (promised education but got forced labour), CHILD LABOUR, DANGEROUS CONDITIONS (poisonous chemicals), and LOW PAY. These are all forms of exploitation linked to unfair trade systems."
  },
  {
    q:"🏭 A large clothing brand pays factory workers in Bangladesh R20 per day to work 12-hour shifts, 6 days a week, with no sick leave and unsafe machinery. What makes this UNFAIR TRADE?",
    opts:[
      "The workers are not skilled enough to earn more",
      "Low pay, long hours, dangerous conditions, and no benefits — workers are exploited for profit",
      "The factory is in Bangladesh, not a developed country, so lower wages are normal",
      "The brand is providing jobs which is always positive for developing countries"
    ],
    c:1,
    exp:"Hasina's story (textbook p.44) shows unfair trade through: LOW WAGES (R20/day), LONG HOURS (12 hours/day), UNSAFE MACHINERY, and NO SICK LEAVE. The textbook identifies these as examples of EXPLOITATION in the workplace. Low pay and long hours are 'the most common forms of exploitation'."
  },
  {
    q:"🌑 A developing country earns most of its income by selling raw materials (like copper ore) to developed countries. Even though copper prices drop, the developing country has no way to change the price. Which unfair trade consequence does this cause?",
    opts:[
      "The developing country becomes richer because it sells more ore",
      "Low prices for raw materials keep the country poor — the government cannot collect enough taxes to provide services",
      "The country can use the copper internally and does not need to sell it",
      "Low prices are good because it helps developed countries grow"
    ],
    c:1,
    exp:"The textbook (p.41) explains: when developing countries get LOW PRICES for raw materials, governments CANNOT COLLECT ENOUGH TAXES. Without tax income, they cannot fund education, healthcare, infrastructure, or SKILLS TRAINING. This creates a cycle of poverty."
  },
  {
    q:"👧 In a banana plantation in Central America, young children work in the fields instead of attending school. Their parents earn so little from unfair banana prices that the family needs the children's income to survive. What is the ROOT CAUSE of child labour here?",
    opts:[
      "Parents do not value education",
      "Children prefer to work rather than go to school",
      "Unfair trade keeps wages so low that families cannot survive without child labour",
      "The government has banned schooling in rural areas"
    ],
    c:2,
    exp:"UNFAIR TRADE creates a chain of poverty: LOW CROP PRICES → LOW FARMER WAGES → PARENTS CANNOT AFFORD SCHOOL FEES → CHILDREN FORCED TO WORK. The textbook lists 'sometimes children are forced to work' as a direct consequence of developing countries receiving low prices for their raw materials."
  },
  {
    q:"🔗 A developing country grows cotton and sells it cheaply to a developed country. The developed country uses the cotton to make T-shirts, which it then sells back to the developing country at a HIGH PRICE. The developing country cannot afford to manufacture T-shirts itself. What unfair trade cycle does this create?",
    opts:[
      "A fair exchange — both countries get what they need",
      "The developing country sells cheap raw materials but buys expensive manufactured goods — it cannot break out of poverty",
      "This is normal trade — prices always rise with manufacturing",
      "The developing country should simply stop selling cotton"
    ],
    c:1,
    exp:"This describes the UNFAIR TRADE CYCLE: raw materials from poor countries are CHEAP; manufactured goods sold back are EXPENSIVE. The textbook (p.41) states: 'poor countries do not have money to buy expensive manufacturing products, like MACHINES, which could help them process their own raw materials.' Without machines, they stay trapped as raw material exporters."
  },
  {
    q:"🏥 Because of unfair trade prices, a farming community in Mozambique cannot afford to pay for a nurse at their local clinic. Children in the village suffer from preventable diseases. Which unfair trade consequence does this illustrate?",
    opts:[
      "Unfair trade has no impact on health — these are unrelated issues",
      "Low income from unfair trade means communities cannot fund basic services like health care",
      "The government of Mozambique is responsible, not trade prices",
      "Developed countries provide free health care to all developing nations"
    ],
    c:1,
    exp:"The textbook (p.41) lists this as a direct unfair trade effect: 'Low-income communities do not have enough money to pay for BASIC SERVICES, such as EDUCATION and HEALTH CARE.' Unfair trade prices reduce the income available for communities and governments to fund essential services."
  },
  {
    q:"📉 A country exports raw coffee beans at R12/kg. A developed country buys these beans, processes them into branded coffee, and sells the final product for R200/kg. The developing country earns only R12. What does this show about MANUFACTURED GOODS vs RAW MATERIALS in unfair trade?",
    opts:[
      "The developing country should stop drinking coffee",
      "Manufactured goods sell at MUCH HIGHER PRICES than raw materials — this gap creates and sustains inequality",
      "The R12 is a fair price because farming is simple work",
      "Processing coffee is not valuable because it is just a drink"
    ],
    c:1,
    exp:"The textbook opens with: 'manufactured goods sell at HIGHER PRICES than raw materials.' When a developing country only sells raw coffee at R12/kg but the same coffee — once processed — sells for R200/kg, the developing country misses out on R188 of potential value. This value gap is a CORE problem of unfair trade."
  },
  {
    q:"🚫 A gold mining company in a developing country pays miners R30/day to work in tunnels with no safety equipment. When a miner is injured, he receives no compensation and loses his job. Which aspects of UNFAIR exploitation are present here?",
    opts:[
      "Low wages only",
      "Only dangerous working conditions",
      "Low wages, dangerous conditions, no sick leave, and job insecurity — multiple forms of exploitation combined",
      "This is normal — mining is always dangerous no matter who owns the mine"
    ],
    c:2,
    exp:"The textbook (p.44) lists examples of exploitation: LOW WAGES, LONG WORKING HOURS, UNHEALTHY AND DANGEROUS PLACES OF WORK, CHILD WORKERS, and NO SICK LEAVE. This mining scenario shows multiple exploitation factors combined — which makes it a clear case of unfair trade and exploitation."
  },
  {
    q:"🌍 A developing country wants to improve its economy by processing its own raw materials. However, it cannot afford the expensive machines needed. Why does unfair trade PREVENT this from happening?",
    opts:[
      "Developing countries are not allowed to buy machines by international law",
      "Unfair trade keeps raw material prices so low that developing countries cannot earn enough money to buy manufacturing equipment",
      "Machines are not useful for processing raw materials",
      "Developed countries share their machines freely with developing countries"
    ],
    c:1,
    exp:"The textbook (p.41) explains: 'poor countries do not have money to buy expensive manufacturing products, LIKE MACHINES, which could help them process their own raw materials.' This creates a trap: UNFAIR PRICES → NO MACHINES → STUCK SELLING RAW MATERIALS → MORE UNFAIR PRICES. This cycle is sustained by unfair trade."
  }
];

// ═══════════════════════════════════════════════════════
// SECTION 3 — CASE STUDY + WORD SALAD (5 questions)
// ═══════════════════════════════════════════════════════
const CASE_STUDY = `
🌿 <strong>Case Study: The Msaada Tea Farm, Kenya</strong><br><br>
Joseph Otieno is a tea farmer in Kenya. He grows high-quality green tea on a small 2-hectare farm. 
A British tea company buys his tea through a MIDDLEMAN agent. 
The agent pays Joseph <strong>R8 per kg</strong>. The British company sells the branded tea in UK supermarkets for <strong>R120 per kg</strong>. 
Joseph has no say in the price set by the middleman. He earns so little that:<br>
• His children, aged 8 and 11, must help pick tea leaves every morning before school — sometimes missing lessons<br>
• The family cannot afford medical care when Joseph's wife becomes ill<br>
• Joseph has no protective gloves and uses pesticide sprays with his bare hands<br>
• When a drought reduces his harvest, the middleman <em>lowers</em> the price to R6/kg<br>
• The village has no clean water because the local government has no tax income to provide services<br>
• Joseph cannot save money to buy a better irrigation system, so his yields stay low<br><br>
The British tea company has a profit margin of over 900%.
`;

const CASE_QS = [
  {
    type:'mcq',
    q:"⚖️ CASE STUDY — Joseph Otieno (Kenya Tea): What is the MAIN reason this trade is UNFAIR?",
    opts:[
      "Joseph grows too little tea to earn a decent price",
      "The PRICE is decided by the middleman and the buyer — Joseph has NO say and earns far below the selling price",
      "Tea farming is not valuable and prices are always low",
      "The British company is paying a fair market price"
    ],
    c:1,
    exp:"The trade is UNFAIR because Joseph has NO POWER over the price. The textbook states: 'prices of raw materials are decided by BUYERS, not by sellers.' Joseph earns R8/kg while the final product sells for R120/kg — he receives less than 7% of the value his product ultimately creates. This is a defining feature of UNFAIR TRADE."
  },
  {
    type:'mcq',
    q:"🔍 CASE STUDY — Joseph's tea: Identify THREE forms of EXPLOITATION visible in Joseph's situation.",
    opts:[
      "No exploitation — Joseph chose to be a farmer",
      "Child labour, dangerous working conditions (no gloves with pesticides), and no sick leave / healthcare",
      "Only low pay — there is no other exploitation present",
      "Joseph is exploited only because he lives in Kenya"
    ],
    c:1,
    exp:"The textbook (p.44) defines exploitation as treating people in a selfish and unfair way. In Joseph's case: (1) CHILD LABOUR — children miss school to pick tea, (2) DANGEROUS CONDITIONS — no gloves with pesticide sprays, (3) NO HEALTHCARE — cannot afford medical care when his wife is ill. These match the textbook's list of exploitation examples exactly."
  },
  {
    type:'mcq',
    q:"💡 CASE STUDY — If Joseph's tea became FAIR TRADE certified, which change would MOST DIRECTLY help his children attend school regularly?",
    opts:[
      "The fair trade label would automatically build a new school",
      "A fair trade price would increase Joseph's income so he could afford school fees and children would NOT need to work",
      "Fair trade would send the children to school in Britain",
      "Fair trade certification would reduce the amount of tea Joseph needs to grow"
    ],
    c:1,
    exp:"The textbook explains: 'workers can use [fair trade] money to send their children to school so that they do NOT HAVE TO WORK.' A FAIR TRADE price for Joseph's tea would give him enough income to pay school fees, removing the economic pressure that forces his children into the fields. This is a direct and documented benefit of fair trade."
  },
  {
    type:'wordsalad',
    q:"🌿 WORD SALAD — Joseph's Story: Select ALL the words/phrases that describe NEGATIVE CONSEQUENCES of UNFAIR TRADE for Joseph and his family. (Tap each correct word, then click Check.)",
    words:[
      "Child labour","Fair wages","Healthy food","No healthcare",
      "Dangerous pesticide exposure","Clean water","School for children",
      "Cannot buy irrigation equipment","Low wages","Village has no services",
      "Safe working conditions","Price set by buyer","Drought makes things worse"
    ],
    correct:["Child labour","No healthcare","Dangerous pesticide exposure","Cannot buy irrigation equipment","Low wages","Village has no services","Price set by buyer","Drought makes things worse"],
    exp:"The NEGATIVE CONSEQUENCES of unfair trade for Joseph include: CHILD LABOUR (children miss school), NO HEALTHCARE (cannot afford treatment), DANGEROUS PESTICIDE EXPOSURE (no gloves), CANNOT BUY IRRIGATION EQUIPMENT (stuck in low yields), LOW WAGES (R8/kg), VILLAGE HAS NO SERVICES (no tax income), PRICE SET BY BUYER (no bargaining power), and DROUGHT MAKES THINGS WORSE (price drops further). The words 'Fair wages', 'Clean water', 'Healthy food', 'School for children', and 'Safe working conditions' describe fair trade BENEFITS — not Joseph's reality."
  },
  {
    type:'mcq',
    q:"⚖️ CASE STUDY — Final: The British tea company earns over 900% profit on Joseph's tea. What is the MOST EFFECTIVE fair trade solution to close this gap?",
    opts:[
      "The British government should close the tea company",
      "Joseph should stop growing tea and grow a different crop",
      "A fair trade agreement where buyers and sellers agree on a price that covers costs AND provides a fair profit for farmers — removing the exploitative middleman",
      "Developed countries should simply donate money to farmers like Joseph"
    ],
    c:2,
    exp:"The textbook (p.42) defines fair trade as: countries agreeing to buy goods at DECENT PRICES from companies that PAY WORKERS FAIRLY. The solution is a DIRECT FAIR TRADE AGREEMENT — Joseph's cooperative negotiates with buyers to receive a fair portion of the final value. This removes the exploitative middleman, gives Joseph BARGAINING POWER, and ensures the fair trade premium goes back into his community."
  }
];

// ═══════════════════════════════════════════════════════
// STATE
// ═══════════════════════════════════════════════════════
let score=0, stars=0;
let fairQ=0, unfairQ=0, caseQ=0;
let answered=false;
let wsSelected=[], wsChecked=false;

function setHdr(part){
  document.getElementById('hPart').textContent=part;
  document.getElementById('hScore').textContent=score;
  document.getElementById('hStars').textContent=stars>0?'⭐'.repeat(Math.min(stars,20)):'☆';
}
function setProgress(n,t,lbl,theme){
  document.getElementById('pFill').className='prog-fill '+(theme||'none');
  document.getElementById('pFill').style.width=(t>0?Math.round(n/t*100):0)+'%';
  document.getElementById('pLabel').textContent=lbl;
}

// ═══════════════════════════════════════════════════════
// HOME
// ═══════════════════════════════════════════════════════
function renderHome(){
  fairQ=0; unfairQ=0; caseQ=0; setHdr('-');
  setProgress(0,0,'Choose a section','none');
  document.getElementById('hTitle').textContent='🌾 FAIR TRADE ADVENTURE QUIZ ⚖️';
  document.getElementById('main').innerHTML=`
    <div class="section-home">
      <div class="sh-title fair" style="font-size:clamp(1.1rem,4vw,1.8rem);">🌾 Fair Trade Adventure Quiz ⚖️</div>
      <div class="sh-sub fair">Three sections — agriculture, slavery &amp; justice themes</div>
      <div class="section-cards">
        <div class="section-card fair-card" onclick="renderFairIntro()">
          <span class="ci">🌱</span>
          <div class="cn">Section 1</div>
          <div style="font-size:.88rem;font-weight:700;color:var(--fair);margin-bottom:4px;">Fair Trade</div>
          <div class="cd">10 questions · Identify fair trade practices &amp; benefits for sellers · Agriculture theme 🌾</div>
        </div>
        <div class="section-card unfair-card" onclick="renderUnfairIntro()">
          <span class="ci">⛓️</span>
          <div class="cn">Section 2</div>
          <div style="font-size:.88rem;font-weight:700;color:var(--unfair);margin-bottom:4px;">Unfair Trade</div>
          <div class="cd">10 questions · Identify exploitation &amp; consequences · Slavery theme 🔗</div>
        </div>
        <div class="section-card case-card" onclick="renderCaseIntro()">
          <span class="ci">⚖️</span>
          <div class="cn">Section 3</div>
          <div style="font-size:.88rem;font-weight:700;color:var(--case);margin-bottom:4px;">Case Study + Word Salad</div>
          <div class="cd">5 questions · New scenario · Identify unfair trade + word salad consequences · Justice theme 📜</div>
        </div>
      </div>
    </div>`;
}

// ═══════════════════════════════════════════════════════
// SECTION 1 — FAIR TRADE
// ═══════════════════════════════════════════════════════
function renderFairIntro(){
  fairQ=0; setHdr('Section 1');
  setProgress(0,FAIR_QS.length,'Read the intro — then start!','fair');
  document.getElementById('main').innerHTML=`
    <div class="card fair-card">
      <div class="card-title fair">🌾 Section 1 — Fair Trade</div>
      <div class="intro-text">In this section you will be given NEW examples of fair trade situations. For each scenario you must IDENTIFY the fair trade practice at work and the BENEFITS it brings to sellers, workers and their communities.</div>
      <div class="info-box fair">
        🤝 <strong>Fair trade happens when:</strong><br>
        • Countries agree to buy goods at <strong>decent prices</strong><br>
        • Buyers and sellers <strong>agree together</strong> on the price<br>
        • Workers are paid <strong>fair wages</strong><br>
        • Working conditions are <strong>safe and healthy</strong><br>
        • Traders make sure money goes to <strong>health care and education</strong><br>
        • Workers form <strong>cooperatives</strong> for more price control<br>
        • The <strong>Fairtrade Foundation mark</strong> guarantees standards
      </div>
      <button class="action-btn fair" onclick="renderFairQ()">Start Section 1 🌱</button>
      <button class="back-btn fair" onclick="renderHome()">← Back to Menu</button>
    </div>`;
}

function renderFairQ(){
  if(fairQ>=FAIR_QS.length){renderFairResults();return;}
  answered=false;
  setHdr('Fair '+(fairQ+1)+'/'+FAIR_QS.length);
  setProgress(fairQ,FAIR_QS.length,'Question '+(fairQ+1)+' of '+FAIR_QS.length,'fair');
  const q=FAIR_QS[fairQ];
  const sh=shuffle(q.opts,q.c);
  const optsHTML=sh.opts.map((o,i)=>`<button class="opt-btn fair-opt" onclick="pickMCQ(${i},${sh.ci},'fair',${fairQ})">${o}</button>`).join('');
  document.getElementById('main').innerHTML=`
    <div class="card fair-card">
      <div class="q-badge fair">${fairQ+1}</div>
      <div style="font-size:1rem;font-weight:600;color:var(--text);text-align:center;margin-bottom:20px;line-height:1.55;">${q.q}</div>
      <div id="optWrap" style="display:flex;flex-direction:column;gap:10px;">${optsHTML}</div>
      <button class="action-btn fair next-btn" id="nextBtn" onclick="advanceQ('fair')">Next Question 🌾</button>
    </div>`;
}

function renderFairResults(){
  logScore('Section 1 - Fair Trade', score);
  const pct=Math.round((score/(score+((FAIR_QS.length-(stars-(unfairQ>0?UNFAIR_QS.length:0)-(caseQ>0?CASE_QS.length:0)))*0)))*100)||Math.round((stars/FAIR_QS.length)*100);
  let key,msg;
  if(pct>=80){key='great';msg='🏆 Agriculture Champion! You know fair trade inside out!';}
  else if(pct>=50){key='good';msg='🌱 Good effort! Review the benefits of fair trade.';}
  else{key='low';msg='📖 Review the fair trade notes and try again!';}
  setHdr('Section 1 Done!');
  setProgress(FAIR_QS.length,FAIR_QS.length,'Section 1 complete!','fair');
  document.getElementById('main').innerHTML=`
    <div class="card fair-card results-box">
      ${meme('fair',key)}
      <div class="res-title fair">Fair Trade Complete! 🎉</div>
      <div style="font-size:.95rem;color:var(--subtext);margin-bottom:10px;">${msg}</div>
      <div class="res-score">Score: ${score} points</div>
      <div class="stars-row">${'⭐'.repeat(Math.min(stars,20))||'☆'}</div>
      <button class="action-btn fair" onclick="fairQ=0;renderFairQ()">Retry Section 1 🌾</button>
      <button class="back-btn fair" onclick="renderHome()">← Section Menu</button>
    </div>`;
}

// ═══════════════════════════════════════════════════════
// SECTION 2 — UNFAIR TRADE
// ═══════════════════════════════════════════════════════
function renderUnfairIntro(){
  unfairQ=0; setHdr('Section 2');
  setProgress(0,UNFAIR_QS.length,'Read the intro — then start!','unfair');
  document.getElementById('main').innerHTML=`
    <div class="card unfair-card">
      <div class="card-title unfair">⛓️ Section 2 — Unfair Trade</div>
      <div class="intro-text">You will be given NEW scenarios showing unfair trade in action. For each one you must IDENTIFY what makes the trade unfair and explain the NEGATIVE CONSEQUENCES for sellers, workers and their communities.</div>
      <div class="info-box unfair">
        ⚠️ <strong>Unfair trade happens when:</strong><br>
        • Prices are <strong>decided by buyers</strong>, not sellers<br>
        • Farmers and workers receive <strong>low wages</strong><br>
        • Workers face <strong>dangerous conditions</strong> and long hours<br>
        • <strong>Children are forced to work</strong> instead of going to school<br>
        • Communities cannot fund <strong>health care or education</strong><br>
        • Developing countries <strong>stay poor</strong> because raw material prices are too low<br>
        • Workers are <strong>exploited</strong> — treated in a selfish and unfair way
      </div>
      <button class="action-btn unfair" onclick="renderUnfairQ()">Start Section 2 ⛓️</button>
      <button class="back-btn unfair" onclick="renderHome()">← Back to Menu</button>
    </div>`;
}

function renderUnfairQ(){
  if(unfairQ>=UNFAIR_QS.length){renderUnfairResults();return;}
  answered=false;
  setHdr('Unfair '+(unfairQ+1)+'/'+UNFAIR_QS.length);
  setProgress(unfairQ,UNFAIR_QS.length,'Question '+(unfairQ+1)+' of '+UNFAIR_QS.length,'unfair');
  const q=UNFAIR_QS[unfairQ];
  const sh=shuffle(q.opts,q.c);
  const optsHTML=sh.opts.map((o,i)=>`<button class="opt-btn unfair-opt" onclick="pickMCQ(${i},${sh.ci},'unfair',${unfairQ})">${o}</button>`).join('');
  document.getElementById('main').innerHTML=`
    <div class="card unfair-card">
      <div class="q-badge unfair">${unfairQ+1}</div>
      <div style="font-size:1rem;font-weight:600;color:var(--text);text-align:center;margin-bottom:20px;line-height:1.55;">${q.q}</div>
      <div id="optWrap" style="display:flex;flex-direction:column;gap:10px;">${optsHTML}</div>
      <button class="action-btn unfair next-btn" id="nextBtn" onclick="advanceQ('unfair')">Next Question ⛓️</button>
    </div>`;
}

function renderUnfairResults(){
  logScore('Section 2 - Unfair Trade', score);
  setHdr('Section 2 Done!');
  setProgress(UNFAIR_QS.length,UNFAIR_QS.length,'Section 2 complete!','unfair');
  const pct=Math.round((stars/UNFAIR_QS.length)*100);
  let key,msg;
  if(pct>=80){key='great';msg='🔓 Justice Hero! You can spot exploitation like a detective!';}
  else if(pct>=50){key='good';msg='🔍 Good work! Review the exploitation examples.';}
  else{key='low';msg='📖 Review Hamed and Hasina\'s stories and retry!';}
  document.getElementById('main').innerHTML=`
    <div class="card unfair-card results-box">
      ${meme('unfair',key)}
      <div class="res-title unfair">Unfair Trade Complete! 🎉</div>
      <div style="font-size:.95rem;color:var(--subtext);margin-bottom:10px;">${msg}</div>
      <div class="res-score">Score: ${score} points</div>
      <div class="stars-row">${'⭐'.repeat(Math.min(stars,20))||'☆'}</div>
      <button class="action-btn unfair" onclick="unfairQ=0;renderUnfairQ()">Retry Section 2 ⛓️</button>
      <button class="back-btn unfair" onclick="renderHome()">← Section Menu</button>
    </div>`;
}

// ═══════════════════════════════════════════════════════
// SECTION 3 — CASE STUDY + WORD SALAD
// ═══════════════════════════════════════════════════════
function renderCaseIntro(){
  caseQ=0; setHdr('Section 3');
  setProgress(0,CASE_QS.length,'Read the case study — then start!','case');
  document.getElementById('main').innerHTML=`
    <div class="card case-card">
      <div class="card-title case">⚖️ Section 3 — Case Study + Word Salad</div>
      <div class="info-box case">${CASE_STUDY}</div>
      <div class="intro-text">Read the case study above carefully. The questions that follow will ask you to: <strong>(1)</strong> identify what makes the trade UNFAIR and <strong>(2)</strong> use a WORD SALAD to select the negative consequences of unfair trade for Joseph and his family.</div>
      <button class="action-btn case" onclick="renderCaseQ()">Start Section 3 ⚖️</button>
      <button class="back-btn case" onclick="renderHome()">← Back to Menu</button>
    </div>`;
}

function renderCaseQ(){
  if(caseQ>=CASE_QS.length){renderCaseResults();return;}
  const q=CASE_QS[caseQ];
  if(q.type==='wordsalad'){renderWordSalad(q);return;}
  answered=false;
  setHdr('Case '+(caseQ+1)+'/'+CASE_QS.length);
  setProgress(caseQ,CASE_QS.length,'Question '+(caseQ+1)+' of '+CASE_QS.length,'case');
  const sh=shuffle(q.opts,q.c);
  const optsHTML=sh.opts.map((o,i)=>`<button class="opt-btn case-opt" onclick="pickMCQ(${i},${sh.ci},'case',${caseQ})">${o}</button>`).join('');
  document.getElementById('main').innerHTML=`
    <div class="card case-card">
      <div class="info-box case" style="font-size:.78rem;margin-bottom:14px;">📋 <strong>Refer to: The Msaada Tea Farm, Kenya</strong> — Joseph earns R8/kg; sells for R120/kg; children miss school; no healthcare; no gloves with pesticides; no clean water in village.</div>
      <div class="q-badge case">${caseQ+1}</div>
      <div style="font-size:1rem;font-weight:600;color:var(--text);text-align:center;margin-bottom:20px;line-height:1.55;">${q.q}</div>
      <div id="optWrap" style="display:flex;flex-direction:column;gap:10px;">${optsHTML}</div>
      <button class="action-btn case next-btn" id="nextBtn" onclick="advanceQ('case')">Next ⚖️</button>
    </div>`;
}

function renderWordSalad(q){
  wsSelected=[]; wsChecked=false;
  setHdr('Case '+(caseQ+1)+'/'+CASE_QS.length);
  setProgress(caseQ,CASE_QS.length,'Question '+(caseQ+1)+' of '+CASE_QS.length,'case');
  const wordsHTML=q.words.map((w,i)=>`<span class="ws-word" id="wsw${i}" onclick="toggleWord(${i},'${w.replace(/'/g,"\\'")}',${JSON.stringify(q.correct).replace(/"/g,"'")})">${w}</span>`).join('');
  document.getElementById('main').innerHTML=`
    <div class="card case-card">
      <div class="info-box case" style="font-size:.78rem;margin-bottom:14px;">📋 <strong>Case Study: Joseph Otieno</strong> — R8/kg tea; children miss school; no healthcare; pesticide sprays without gloves; village has no services.</div>
      <div class="q-badge case">${caseQ+1}</div>
      <div style="font-size:1rem;font-weight:600;color:var(--text);text-align:center;margin-bottom:16px;line-height:1.55;">${q.q}</div>
      <div class="word-salad-wrap" id="wordSalad">${wordsHTML}</div>
      <div class="ws-selected-area" id="wsArea"><span style="opacity:.4;font-size:.8rem;">Tap words above to select them…</span></div>
      <div id="wsFeedback"></div>
      <div style="display:flex;align-items:center;gap:10px;flex-wrap:wrap;margin-top:14px;">
        <button class="check-btn case" onclick="checkWordSalad()">✅ Check Selections</button>
        <button class="reset-btn" onclick="resetWordSalad()">Reset</button>
        <span class="score-bar case" id="wsBar"></span>
      </div>
      <button class="action-btn case next-btn" id="nextBtn" onclick="advanceQ('case')" style="display:none;">Next ⚖️</button>
    </div>`;
}

function toggleWord(idx,word,correct){
  if(wsChecked)return;
  const el=document.getElementById('wsw'+idx);
  const i=wsSelected.indexOf(word);
  if(i>=0){wsSelected.splice(i,1);el.classList.remove('selected');}
  else{wsSelected.push(word);el.classList.add('selected');}
  const area=document.getElementById('wsArea');
  area.innerHTML=wsSelected.length?wsSelected.map(w=>`<span style="background:rgba(245,158,11,.2);border:1px solid var(--case);border-radius:20px;padding:5px 12px;font-size:.82rem;">${w}</span>`).join(''):'<span style="opacity:.4;font-size:.8rem;">Tap words above to select them…</span>';
}

function checkWordSalad(){
  if(wsChecked)return; wsChecked=true;
  const q=CASE_QS[caseQ];
  const correct=q.correct;
  let right=0,wrong=0;
  q.words.forEach((w,i)=>{
    const el=document.getElementById('wsw'+i);
    const isCorrect=correct.includes(w);
    const wasSelected=wsSelected.includes(w);
    if(wasSelected&&isCorrect){el.classList.add('correct-word');right++;}
    else if(wasSelected&&!isCorrect){el.classList.add('wrong-word');wrong++;}
    else if(!wasSelected&&isCorrect){el.classList.add('wrong-word');/* missed */}
    el.classList.remove('selected');
  });
  const missed=correct.filter(w=>!wsSelected.includes(w)).length;
  const points=Math.max(0,right-wrong)*2;
  score+=points; if(right>=correct.length*0.75)stars++;
  setHdr('Case '+(caseQ+1)+'/'+CASE_QS.length);
  const fb=document.getElementById('wsFeedback');
  fb.className='feedback-box '+(right>=correct.length*0.75?'fb-correct':'fb-wrong');
  fb.innerHTML=`<strong>${right>=correct.length*0.75?'✅ Well done!':'📖 Review needed'}</strong> You selected ${right}/${correct.length} correct consequences (${wrong} incorrect, ${missed} missed).<br><br>${q.exp}`;
  document.getElementById('wsBar').textContent=right+'/'+correct.length+' correct consequences identified';
  document.getElementById('nextBtn').style.display='block';
}

function resetWordSalad(){
  wsSelected=[];wsChecked=false;
  renderWordSalad(CASE_QS[caseQ]);
}

function renderCaseResults(){
  logScore('Section 3 - Case Study', score);
  setHdr('All Done!');
  setProgress(CASE_QS.length,CASE_QS.length,'Case study complete!','case');
  const pct=Math.round((stars/CASE_QS.length)*100);
  let key,msg;
  if(pct>=80){key='great';msg='⚖️ Equity Master! You can analyse unfair trade like a pro!';}
  else if(pct>=50){key='good';msg='📜 Good analysis! Review the case study and explanations.';}
  else{key='low';msg='📖 Read Joseph\'s story again carefully and retry!';}
  document.getElementById('main').innerHTML=`
    <div class="card case-card results-box">
      ${meme('case',key)}
      <div class="res-title case">Case Study Complete! 🎉</div>
      <div style="font-size:.95rem;color:var(--subtext);margin-bottom:10px;">${msg}</div>
      <div class="res-score">Score: ${score} points total</div>
      <div class="stars-row">${'⭐'.repeat(Math.min(stars,20))||'☆'}</div>
      <button class="action-btn case" onclick="caseQ=0;renderCaseQ()">Retry Section 3 ⚖️</button>
      <button class="back-btn case" onclick="renderHome()">← Section Menu</button>
    </div>`;
}

// ═══════════════════════════════════════════════════════
// SHARED MCQ HANDLER
// ═══════════════════════════════════════════════════════
function pickMCQ(sel,ci,theme,qi){
  if(answered)return; answered=true;
  const isOK=sel===ci;
  if(isOK){score+=10;stars++;}
  setHdr(theme==='fair'?'Fair '+(fairQ+1)+'/'+FAIR_QS.length:theme==='unfair'?'Unfair '+(unfairQ+1)+'/'+UNFAIR_QS.length:'Case '+(caseQ+1)+'/'+CASE_QS.length);
  const dataset=theme==='fair'?FAIR_QS:theme==='unfair'?UNFAIR_QS:CASE_QS;
  const q=dataset[qi];
  document.querySelectorAll('.opt-btn').forEach((b,i)=>{
    b.classList.add('disabled');
    if(i===ci)b.classList.add('correct');
    else if(i===sel&&!isOK)b.classList.add('incorrect');
  });
  const fb=document.createElement('div');
  fb.className='feedback-box '+(isOK?'fb-correct':'fb-wrong');
  fb.innerHTML=(isOK?`${meme(theme,1)}<strong>✅ Correct!</strong> `:`${meme(theme,0)}<strong>❌ Correct answer:</strong> ${q.opts[q.c]}<br><br>`)+q.exp;
  document.getElementById('optWrap').after(fb);
  document.getElementById('nextBtn').style.display='block';
}

function advanceQ(theme){
  if(theme==='fair'){fairQ++;renderFairQ();}
  else if(theme==='unfair'){unfairQ++;renderUnfairQ();}
  else{caseQ++;renderCaseQ();}
}

// ═══════════════════════════════════════════════════════
// SHUFFLE
// ═══════════════════════════════════════════════════════
function shuffle(opts,ci){
  const p=opts.map((t,i)=>({t,isC:i===ci}));
  for(let i=p.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[p[i],p[j]]=[p[j],p[i]];}
  return{opts:p.map(x=>x.t),ci:p.findIndex(x=>x.isC)};
}

window.addEventListener('DOMContentLoaded',renderHome);

// ═══════════════════════════════════════════════════════
// SCORE LOGGING — sends result to local Python server
// ═══════════════════════════════════════════════════════
function logScore(section, points){
  fetch('http://localhost:5050/log_score', {
    method: 'POST',
    headers: {'Content-Type': 'application/json'},
    body: JSON.stringify({section: section, score: points})
  }).catch(()=>{}); // silently ignore if server not running
}
</script>
</body>
</html>
