<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Spelling Quiz! ⭐</title>
<link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet">
<script src="https://js.puter.com/v2/"></script>
<style>
  :root {
    --coral: #ff7b7b;
    --mint: #7be8a8;
    --purple: #c084fc;
    --gold: #ffe066;
    --navy: #1a1a4e;
    --card: #ffffff;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    font-family: 'Nunito', sans-serif;
    background: linear-gradient(160deg, #c9f0ff 0%, #ffe8f5 50%, #fff3c4 100%);
    min-height: 100vh;
    display: flex; flex-direction: column; align-items: center;
    padding: 24px 16px 48px;
    overflow-x: hidden;
  }
  .star { position: fixed; font-size: 1.4rem; animation: floatStar 8s ease-in-out infinite; pointer-events: none; opacity: 0.4; z-index: 0; }
  @keyframes floatStar { 0%,100%{transform:translateY(0) rotate(0deg)} 50%{transform:translateY(-18px) rotate(15deg)} }

  h1 { font-family:'Fredoka One',cursive; font-size:clamp(2rem,6vw,3.2rem); color:var(--navy); text-align:center; letter-spacing:1px; margin-bottom:4px; position:relative; z-index:1; text-shadow:3px 3px 0 rgba(255,255,255,0.6); }
  .subtitle { font-size:1rem; color:#5a5a8a; font-weight:700; text-align:center; margin-bottom:28px; z-index:1; position:relative; }

  /* MODE SCREEN */
  .mode-card { background:var(--card); border-radius:28px; padding:36px 32px; max-width:480px; width:100%; box-shadow:0 8px 36px rgba(100,100,180,0.13); z-index:1; position:relative; animation:popIn 0.4s cubic-bezier(.34,1.56,.64,1); text-align:center; }
  .mode-title { font-family:'Fredoka One',cursive; font-size:1.6rem; color:var(--navy); margin-bottom:8px; }
  .mode-sub { font-size:.95rem; color:#7070a8; font-weight:700; margin-bottom:28px; }
  .mode-options { display:flex; flex-direction:column; gap:14px; }
  .mode-btn { display:flex; align-items:center; gap:18px; border-radius:18px; padding:18px 22px; cursor:pointer; transition:all 0.18s; text-align:left; width:100%; border:3px solid; }
  .mode-btn.hint-btn  { background:#f6f4ff; border-color:#e0d8ff; }
  .mode-btn.listen-btn{ background:#f0faff; border-color:#a8edff; }
  .mode-btn.both-btn  { background:#fffbe8; border-color:#ffe066; }
  .mode-btn:hover { transform:translateY(-2px); box-shadow:0 6px 18px rgba(0,0,0,0.1); }
  .mode-icon { font-size:2.4rem; flex-shrink:0; }
  .mode-name { font-family:'Fredoka One',cursive; font-size:1.2rem; color:var(--navy); margin-bottom:3px; }
  .mode-desc { font-size:.85rem; color:#7070a8; font-weight:700; line-height:1.4; }

  /* SCORE BAR */
  .score-bar { display:flex; gap:10px; margin-bottom:20px; z-index:1; position:relative; flex-wrap:wrap; justify-content:center; }
  .score-pill { background:#fff; border-radius:50px; padding:7px 16px; font-weight:800; font-size:.9rem; color:var(--navy); box-shadow:0 4px 12px rgba(0,0,0,0.1); display:flex; align-items:center; gap:5px; }

  /* PROGRESS */
  .progress-wrap { background:#eeeeff; border-radius:50px; height:10px; margin-bottom:24px; overflow:hidden; position:relative; z-index:1; max-width:480px; width:100%; }
  .progress-fill { height:100%; background:linear-gradient(90deg,#a78bfa,#7be8a8); border-radius:50px; transition:width 0.5s cubic-bezier(.34,1.56,.64,1); }

  /* QUIZ CARD */
  .card { background:var(--card); border-radius:28px; padding:32px 28px 28px; max-width:480px; width:100%; box-shadow:0 8px 36px rgba(100,100,180,0.13); position:relative; z-index:1; animation:popIn 0.4s cubic-bezier(.34,1.56,.64,1); }
  @keyframes popIn { from{transform:scale(.88);opacity:0} to{transform:scale(1);opacity:1} }

  .card-top-row { display:flex; justify-content:space-between; align-items:center; margin-bottom:14px; }
  .question-count { font-size:.85rem; font-weight:800; color:#9090bb; text-transform:uppercase; letter-spacing:1.5px; }
  .mode-badge { font-size:.75rem; font-weight:800; padding:4px 12px; border-radius:50px; }
  .mode-badge.hint   { background:#ede8ff; color:#7c3aed; }
  .mode-badge.listen { background:#e0f5ff; color:#0284c7; }
  .mode-badge.both   { background:#fff8d0; color:#b45309; }

  /* HINT BOX */
  .hint-box { background:linear-gradient(135deg,#f0f4ff,#fdf0ff); border-radius:16px; padding:14px 18px; margin-bottom:16px; border-left:5px solid var(--purple); }
  .hint-label { font-size:.72rem; font-weight:800; color:#9b6bcc; text-transform:uppercase; letter-spacing:1px; margin-bottom:5px; }
  .hint-text { font-size:1rem; font-weight:700; color:var(--navy); line-height:1.5; }

  /* LISTEN BOX */
  .listen-box { background:linear-gradient(135deg,#e8f6ff,#e0f0ff); border-radius:18px; padding:18px; margin-bottom:16px; border-left:5px solid #38bdf8; text-align:center; }
  .listen-label { font-size:.72rem; font-weight:800; color:#0284c7; text-transform:uppercase; letter-spacing:1px; margin-bottom:12px; }
  .btn-speak { background:linear-gradient(135deg,#38bdf8,#0284c7); color:#fff; border:none; border-radius:50px; padding:13px 28px; font-family:'Fredoka One',cursive; font-size:1.1rem; cursor:pointer; display:inline-flex; align-items:center; gap:8px; box-shadow:0 4px 16px rgba(2,132,199,0.3); transition:all 0.18s; }
  .btn-speak:hover { transform:translateY(-2px); }
  .btn-speak.speaking { background:linear-gradient(135deg,#a78bfa,#7c3aed); animation:pulse 0.8s ease-in-out infinite alternate; }
  @keyframes pulse { from{box-shadow:0 4px 16px rgba(124,58,237,0.3)} to{box-shadow:0 4px 28px rgba(124,58,237,0.6);transform:scale(1.04)} }
  .sentence-display { margin-top:12px; background:rgba(255,255,255,0.75); border-radius:12px; padding:10px 14px; font-size:.95rem; font-weight:700; color:var(--navy); line-height:1.5; text-align:left; border-left:3px solid #38bdf8; }
  .listen-hint { margin-top:8px; font-size:.78rem; color:#5a8aaa; font-weight:700; }

  /* TRIES */
  .tries-row { display:flex; gap:8px; justify-content:center; margin-bottom:14px; }
  .try-dot { width:14px; height:14px; border-radius:50%; border:2.5px solid #ccc; background:#fff; transition:all 0.3s; }
  .try-dot.used-correct { background:var(--mint); border-color:#3ecf7a; }
  .try-dot.used-wrong   { background:var(--coral); border-color:#e05555; }
  .try-dot.active       { border-color:#a78bfa; background:#f0e8ff; }

  /* INPUT */
  .input-row { display:flex; gap:10px; margin-bottom:10px; }
  input[type="text"] { flex:1; padding:13px 16px; font-family:'Nunito',sans-serif; font-size:1.15rem; font-weight:700; border:3px solid #e0e0f0; border-radius:14px; outline:none; color:var(--navy); transition:border-color 0.2s; background:#fafaff; }
  input[type="text"]:focus { border-color:var(--purple); background:#fff; }
  input.correct { border-color:var(--mint); background:#f0fff6; }
  input.wrong   { border-color:var(--coral); background:#fff5f5; animation:shake 0.4s; }
  @keyframes shake { 0%,100%{transform:translateX(0)} 20%{transform:translateX(-6px)} 40%{transform:translateX(6px)} 60%{transform:translateX(-4px)} 80%{transform:translateX(4px)} }

  /* FEEDBACK */
  .feedback { text-align:center; font-size:1rem; font-weight:800; min-height:24px; margin-bottom:4px; }
  .feedback.correct { color:#22a85a; }
  .feedback.wrong   { color:var(--coral); }
  .answer-reveal { text-align:center; font-size:.92rem; color:#7070a8; font-weight:700; min-height:20px; margin-bottom:10px; }
  .answer-reveal strong { color:var(--navy); }

  /* BUTTONS */
  .btn { padding:13px 24px; font-family:'Fredoka One',cursive; font-size:1.1rem; border:none; border-radius:14px; cursor:pointer; transition:transform 0.15s,box-shadow 0.15s; letter-spacing:.5px; width:100%; margin-bottom:8px; }
  .btn:active { transform:scale(.95); }
  .btn-check { background:linear-gradient(135deg,#7be8a8,#3ecf7a); color:#fff; box-shadow:0 4px 14px rgba(62,207,122,.35); }
  .btn-check:hover { box-shadow:0 6px 20px rgba(62,207,122,.45); transform:translateY(-1px); }
  .btn-next  { background:linear-gradient(135deg,#a78bfa,#7c3aed); color:#fff; box-shadow:0 4px 14px rgba(124,58,237,.3); }
  .btn-skip  { background:#f3f3fa; color:#8888bb; font-family:'Nunito',sans-serif; font-weight:800; font-size:.88rem; }

  /* RESULTS */
  .results { background:var(--card); border-radius:28px; padding:40px 28px; max-width:480px; width:100%; text-align:center; box-shadow:0 8px 36px rgba(100,100,180,.13); position:relative; z-index:1; animation:popIn 0.5s cubic-bezier(.34,1.56,.64,1); }
  .results-emoji { font-size:4rem; margin-bottom:8px; }
  .results-title { font-family:'Fredoka One',cursive; font-size:2rem; color:var(--navy); margin-bottom:10px; }
  .results-score { font-size:3rem; font-weight:800; color:#7c3aed; margin-bottom:6px; }
  .results-msg { font-size:1rem; color:#5a5a8a; font-weight:700; margin-bottom:20px; line-height:1.5; }

  /* SCORE BREAKDOWN */
  .breakdown { background:#f8f6ff; border-radius:16px; padding:14px 18px; margin-bottom:18px; text-align:left; }
  .breakdown-title { font-size:.78rem; font-weight:800; color:#7c3aed; text-transform:uppercase; letter-spacing:1px; margin-bottom:10px; }
  .breakdown-row { display:flex; align-items:center; gap:10px; margin-bottom:6px; font-size:.9rem; font-weight:700; color:var(--navy); }
  .breakdown-badge { border-radius:50px; padding:3px 10px; font-size:.78rem; font-weight:800; white-space:nowrap; }
  .b-1st { background:#d1fae5; color:#065f46; }
  .b-2nd { background:#fef3c7; color:#92400e; }
  .b-3rd { background:#fee2e2; color:#991b1b; }
  .b-miss{ background:#f3f4f6; color:#6b7280; }

  .missed-list { background:#fff5f5; border-radius:16px; padding:14px 18px; margin-bottom:18px; text-align:left; }
  .missed-title { font-size:.78rem; font-weight:800; color:#cc5555; text-transform:uppercase; letter-spacing:1px; margin-bottom:8px; }
  .missed-word { display:inline-block; background:#ffe0e0; color:var(--navy); font-weight:800; font-size:.92rem; border-radius:8px; padding:3px 10px; margin:3px 4px 3px 0; }

  .results-btns { display:flex; flex-direction:column; gap:10px; }
  .btn-restart { background:linear-gradient(135deg,#ffe066,#ffa94d); color:var(--navy); box-shadow:0 4px 14px rgba(255,169,77,.3); font-size:1.05rem; margin-bottom:0; }
  .btn-change-mode { background:#f0f4ff; color:#7c3aed; font-family:'Nunito',sans-serif; font-weight:800; font-size:.92rem; margin-bottom:0; }

  .hidden { display:none !important; }
</style>
</head>
<body>

<div class="star" style="top:6%;left:5%;animation-delay:0s">⭐</div>
<div class="star" style="top:12%;right:8%;animation-delay:1.5s">🌟</div>
<div class="star" style="top:40%;left:2%;animation-delay:3s">✨</div>
<div class="star" style="top:60%;right:4%;animation-delay:2s">⭐</div>
<div class="star" style="bottom:10%;left:10%;animation-delay:1s">🌟</div>
<div class="star" style="bottom:20%;right:6%;animation-delay:4s">✨</div>

<h1>✏️ Spelling Quiz!</h1>
<p class="subtitle">Friday test — you've got this! 🌈</p>

<!-- MODE PICKER -->
<div class="mode-card" id="mode-screen">
  <div class="mode-title">How do you want to practice?</div>
  <div class="mode-sub">Pick your quiz style!</div>
  <div class="mode-options">
    <button class="mode-btn hint-btn" onclick="startQuiz('hint')">
      <div class="mode-icon">💡</div>
      <div><div class="mode-name">Hint Mode</div><div class="mode-desc">Read a clue and spell the word</div></div>
    </button>
    <button class="mode-btn listen-btn" onclick="startQuiz('listen')">
      <div class="mode-icon">🔊</div>
      <div><div class="mode-name">Listen &amp; Spell</div><div class="mode-desc">Hear the word spoken — just like the real test!</div></div>
    </button>
    <button class="mode-btn both-btn" onclick="startQuiz('both')">
      <div class="mode-icon">🌟</div>
      <div><div class="mode-name">Both Together</div><div class="mode-desc">Hear the word AND get a hint</div></div>
    </button>
  </div>
</div>

<!-- SCORE BAR -->
<div class="score-bar hidden" id="score-bar">
  <div class="score-pill">🥇 <span id="cnt-1">0</span> first try</div>
  <div class="score-pill">🥈 <span id="cnt-2">0</span> second</div>
  <div class="score-pill">🥉 <span id="cnt-3">0</span> third</div>
  <div class="score-pill">❌ <span id="cnt-miss">0</span> missed</div>
</div>
<div class="progress-wrap hidden" id="progress-wrap">
  <div class="progress-fill" id="progress-fill" style="width:0%"></div>
</div>

<!-- QUIZ CARD -->
<div class="card hidden" id="quiz-card">
  <div class="card-top-row">
    <div class="question-count" id="question-count">Word 1 of 20</div>
    <div class="mode-badge hint" id="mode-badge">💡 Hint</div>
  </div>

  <div class="hint-box hidden" id="hint-box">
    <div class="hint-label">💡 Hint</div>
    <div class="hint-text" id="hint-text"></div>
  </div>

  <div class="listen-box hidden" id="listen-box">
    <div class="listen-label">🔊 Listen carefully</div>
    <button class="btn-speak" id="speak-btn" onclick="speakWord()">
      <span>🔊</span><span id="speak-label">Hear the Word</span>
    </button>
    <div class="sentence-display hidden" id="sentence-display"></div>
    <div class="listen-hint">Tap to hear it again anytime!</div>
  </div>

  <!-- Try dots -->
  <div class="tries-row" id="tries-row">
    <div class="try-dot active" id="dot-0"></div>
    <div class="try-dot" id="dot-1"></div>
    <div class="try-dot" id="dot-2"></div>
  </div>

  <div class="input-row">
    <input type="text" id="answer-input" placeholder="Type your answer…" autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"/>
  </div>
  <div class="feedback" id="feedback"></div>
  <div class="answer-reveal" id="answer-reveal"></div>

  <button class="btn btn-check" id="check-btn" onclick="checkAnswer()">Check ✓</button>
  <button class="btn btn-next hidden" id="next-btn" onclick="nextWord()">Next Word →</button>
  <button class="btn btn-skip" id="skip-btn" onclick="skipWord()">Skip this one</button>
</div>

<!-- RESULTS -->
<div class="results hidden" id="results-screen">
  <div class="results-emoji" id="results-emoji">🏆</div>
  <div class="results-title">Quiz Done!</div>
  <div class="results-score" id="results-score">20/20</div>
  <div class="results-msg" id="results-msg"></div>

  <div class="breakdown" id="breakdown">
    <div class="breakdown-title">📊 How you did</div>
    <div class="breakdown-row"><span class="breakdown-badge b-1st">1st try</span><span id="bd-1">0 words</span></div>
    <div class="breakdown-row"><span class="breakdown-badge b-2nd">2nd try</span><span id="bd-2">0 words</span></div>
    <div class="breakdown-row"><span class="breakdown-badge b-3rd">3rd try</span><span id="bd-3">0 words</span></div>
    <div class="breakdown-row"><span class="breakdown-badge b-miss">Missed</span><span id="bd-miss">0 words</span></div>
  </div>

  <div class="missed-list hidden" id="missed-list">
    <div class="missed-title">Practice these again 👇</div>
    <div id="missed-words"></div>
  </div>

  <div class="results-btns">
    <button class="btn btn-restart" onclick="restartSameMode()">🔄 Try Again!</button>
    <button class="btn btn-change-mode" onclick="goToModeScreen()">← Change Mode</button>
  </div>
</div>

<script>
const words = [
  { word:"pounce",   hint:"A cat does this when it jumps to catch something",      sentence:"The cat was ready to _____ on the toy mouse." },
  { word:"placed",   hint:"You ___ the book on the table",                         sentence:"She _____ her backpack by the door before school." },
  { word:"dice",     hint:"You roll these in a board game — they have dots",        sentence:"He rolled the _____ and moved six spaces on the board." },
  { word:"cents",    hint:"Pennies are worth one of these each",                    sentence:"The candy bar cost seventy-five _____ at the store." },
  { word:"price",    hint:"How much something costs at the store",                  sentence:"The _____ of the new book was five dollars." },
  { word:"space",    hint:"Astronauts travel here — it has stars and planets",      sentence:"The astronaut floated through _____ looking at the stars." },
  { word:"mice",     hint:"More than one mouse",                                    sentence:"The three _____ ran quickly across the kitchen floor." },
  { word:"office",   hint:"A place where people go to work at desks",               sentence:"My dad works in a tall building with a big _____." },
  { word:"wage",     hint:"The money you earn for doing a job",                     sentence:"She earned a good _____ for helping in the garden." },
  { word:"age",      hint:"How old you are",                                        sentence:"At the _____ of nine, she learned how to ride a bike." },
  { word:"gyms",     hint:"Places where people exercise — more than one",           sentence:"The two _____ in our town both have swimming pools." },
  { word:"giant",    hint:"Another word for very, very big",                        sentence:"A _____ wave splashed over the rocks at the beach." },
  { word:"changes",  hint:"When something is different than before",                sentence:"The weather _____ a lot during the month of March." },
  { word:"message",  hint:"A note or text you send to someone",                     sentence:"She left a _____ for her friend on the kitchen table." },
  { word:"pages",    hint:"A book has lots of these",                               sentence:"I have read fifty _____ of my new library book." },
  { word:"you",      hint:"The word we use when talking to someone directly",       sentence:"I saved a seat at lunch just for _____." },
  { word:"road",     hint:"Cars drive on this",                                     sentence:"We drove down the long, winding _____ to the farm." },
  { word:"peace",    hint:"When there is quiet and no fighting",                    sentence:"After the argument, the two friends made _____ with each other." },
  { word:"giraffe",  hint:"The tallest animal in the world, with a very long neck", sentence:"The _____ stretched its long neck to eat leaves from the tree." },
  { word:"peaceful", hint:"Calm and quiet — like a ___ forest",                    sentence:"The park was so _____ early in the morning." }
];

// Scoring: counts[attempt] where attempt = 0 (1st), 1 (2nd), 2 (3rd), 3 (missed)
let shuffled=[], current=0, triesLeft=3, currentTry=0;
let counts=[0,0,0,0]; // 1st, 2nd, 3rd, missed
let missedWords=[], answered=false, quizMode='hint';
let currentAudio=null;

const MAX_TRIES = 3;

function shuffle(arr){ return [...arr].sort(()=>Math.random()-.5); }

function startQuiz(mode){
  quizMode=mode;
  shuffled=shuffle(words);
  current=0; counts=[0,0,0,0]; missedWords=[]; answered=false;

  document.getElementById('mode-screen').classList.add('hidden');
  document.getElementById('score-bar').classList.remove('hidden');
  document.getElementById('progress-wrap').classList.remove('hidden');
  document.getElementById('quiz-card').classList.remove('hidden');

  const badge=document.getElementById('mode-badge');
  if(mode==='hint')  { badge.textContent='💡 Hint Mode';   badge.className='mode-badge hint'; }
  if(mode==='listen'){ badge.textContent='🔊 Listen Mode'; badge.className='mode-badge listen'; }
  if(mode==='both')  { badge.textContent='🌟 Both Modes';  badge.className='mode-badge both'; }

  updateScores();
  showWord();
}

function showWord(){
  answered=false; triesLeft=MAX_TRIES; currentTry=0;
  const w=shuffled[current];

  document.getElementById('question-count').textContent=`Word ${current+1} of ${shuffled.length}`;
  document.getElementById('answer-input').value='';
  document.getElementById('answer-input').className='';
  document.getElementById('answer-input').disabled=false;
  document.getElementById('feedback').textContent='';
  document.getElementById('feedback').className='feedback';
  document.getElementById('answer-reveal').textContent='';
  document.getElementById('check-btn').classList.remove('hidden');
  document.getElementById('next-btn').classList.add('hidden');
  document.getElementById('skip-btn').classList.remove('hidden');
  document.getElementById('progress-fill').style.width=(current/shuffled.length*100)+'%';

  // Try dots
  for(let i=0;i<3;i++){
    const d=document.getElementById('dot-'+i);
    d.className='try-dot'+(i===0?' active':'');
  }

  // Hint / listen boxes
  const hb=document.getElementById('hint-box'), lb=document.getElementById('listen-box');
  if(quizMode==='hint')  { hb.classList.remove('hidden'); lb.classList.add('hidden'); }
  if(quizMode==='listen'){ hb.classList.add('hidden');    lb.classList.remove('hidden'); }
  if(quizMode==='both')  { hb.classList.remove('hidden'); lb.classList.remove('hidden'); }

  document.getElementById('hint-text').textContent=w.hint;

  // Reset speak
  const sb=document.getElementById('speak-btn');
  sb.classList.remove('speaking');
  document.getElementById('speak-label').textContent='Hear the Word';
  const sd=document.getElementById('sentence-display');
  sd.classList.add('hidden'); sd.textContent='';

  // Animate card
  const card=document.getElementById('quiz-card');
  card.style.animation='none'; card.offsetHeight;
  card.style.animation='popIn 0.35s cubic-bezier(.34,1.56,.64,1)';

  if(quizMode==='listen'||quizMode==='both') setTimeout(()=>speakWord(),450);
  setTimeout(()=>document.getElementById('answer-input').focus(),100);
}

/* ── TTS ── */
function setSpeakBtn(state){
  const btn=document.getElementById('speak-btn'), lbl=document.getElementById('speak-label');
  if(state==='loading'){ btn.classList.add('speaking');  lbl.textContent='Loading...'; }
  else if(state==='playing'){ btn.classList.add('speaking'); lbl.textContent='Listening...'; }
  else { btn.classList.remove('speaking'); lbl.textContent='Hear Again 🔁'; }
}

async function ttsPlay(text, onDone){
  try {
    // Puter generative engine = most human-like (Amazon Polly generative)
    const audio = await puter.ai.txt2speech(text, {
      voice: 'Joanna',
      engine: 'generative',
      language: 'en-US'
    });
    currentAudio = audio;
    audio.onended = ()=>{ currentAudio=null; onDone&&onDone(); };
    audio.onerror = ()=>{ currentAudio=null; fallbackSpeak(text, onDone); };
    audio.play();
  } catch(e){
    fallbackSpeak(text, onDone);
  }
}

function fallbackSpeak(text, onDone){
  if(!window.speechSynthesis){ onDone&&onDone(); return; }
  window.speechSynthesis.cancel();
  const u=new SpeechSynthesisUtterance(text);
  u.rate=0.85; u.pitch=1.0; u.lang='en-US';
  const voices=window.speechSynthesis.getVoices();
  const v=voices.find(v=>v.lang==='en-US')||voices.find(v=>v.lang.startsWith('en'));
  if(v) u.voice=v;
  u.onend=()=>{ onDone&&onDone(); };
  window.speechSynthesis.speak(u);
}

async function speakWord(){
  if(currentAudio){ currentAudio.pause(); currentAudio=null; }
  if(window.speechSynthesis) window.speechSynthesis.cancel();

  const w=shuffled[current];
  const sd=document.getElementById('sentence-display');
  sd.classList.add('hidden'); sd.textContent='';
  setSpeakBtn('loading');

  const usePuter = typeof puter!=='undefined' && puter.ai && puter.ai.txt2speech;
  const speak = usePuter ? ttsPlay : fallbackSpeak;

  setSpeakBtn('playing');

  // Word → pause → sentence (with blank shown) → done
  speak(w.word, ()=>{
    setTimeout(()=>{
      sd.textContent = w.sentence; // sentence already has _____ blanks
      sd.classList.remove('hidden');
      speak(w.sentence.replace(/_+/g, w.word), ()=>{
        setSpeakBtn('done');
        document.getElementById('answer-input').focus();
      });
    }, 650);
  });
}

function stopAudio(){
  if(currentAudio){ currentAudio.pause(); currentAudio=null; }
  if(window.speechSynthesis) window.speechSynthesis.cancel();
}

/* ── ANSWER CHECKING ── */
function checkAnswer(){
  if(answered) return;
  const input=document.getElementById('answer-input');
  const userAnswer=input.value.trim().toLowerCase();
  const correctWord=shuffled[current].word.toLowerCase();
  if(!userAnswer){ input.focus(); return; }

  if(userAnswer===correctWord){
    // Correct!
    stopAudio();
    input.classList.add('correct');
    input.disabled=true;
    answered=true;

    // Mark dot
    document.getElementById('dot-'+currentTry).className='try-dot used-correct';

    counts[currentTry]++;
    const msgs=['Perfect! 🌟','Got it on try 2! ⭐','Got it on try 3! 💪'];
    document.getElementById('feedback').textContent=msgs[currentTry];
    document.getElementById('feedback').className='feedback correct';

    document.getElementById('check-btn').classList.add('hidden');
    document.getElementById('next-btn').classList.remove('hidden');
    document.getElementById('skip-btn').classList.add('hidden');
    updateScores();

  } else {
    // Wrong attempt
    input.classList.add('wrong');
    document.getElementById('dot-'+currentTry).className='try-dot used-wrong';
    currentTry++;
    triesLeft--;

    setTimeout(()=>{ input.value=''; input.className=''; }, 600);

    if(triesLeft>0){
      const tryMsgs=['Not quite — try again! 🤔','One more try! You can do it! 💪'];
      document.getElementById('feedback').textContent=tryMsgs[currentTry-1]||'Try again!';
      document.getElementById('feedback').className='feedback wrong';
      // Activate next dot
      document.getElementById('dot-'+currentTry).className='try-dot active';
      setTimeout(()=>input.focus(), 650);
    } else {
      // All tries used
      stopAudio();
      answered=true;
      input.disabled=true;
      counts[3]++;
      missedWords.push(shuffled[current].word);
      document.getElementById('feedback').textContent='The answer was:';
      document.getElementById('feedback').className='feedback wrong';
      document.getElementById('answer-reveal').innerHTML=`<strong>${shuffled[current].word}</strong>`;
      document.getElementById('check-btn').classList.add('hidden');
      document.getElementById('next-btn').classList.remove('hidden');
      document.getElementById('skip-btn').classList.add('hidden');
      updateScores();
    }
  }
}

function skipWord(){
  if(answered) return;
  stopAudio();
  answered=true;
  // Mark remaining dots as wrong
  for(let i=currentTry;i<3;i++) document.getElementById('dot-'+i).className='try-dot used-wrong';
  counts[3]++;
  missedWords.push(shuffled[current].word);
  document.getElementById('answer-input').disabled=true;
  document.getElementById('feedback').textContent='Skipped — the answer was:';
  document.getElementById('feedback').className='feedback wrong';
  document.getElementById('answer-reveal').innerHTML=`<strong>${shuffled[current].word}</strong>`;
  document.getElementById('check-btn').classList.add('hidden');
  document.getElementById('next-btn').classList.remove('hidden');
  document.getElementById('skip-btn').classList.add('hidden');
  updateScores();
}

function nextWord(){
  current++;
  if(current>=shuffled.length) showResults();
  else showWord();
}

function updateScores(){
  document.getElementById('cnt-1').textContent=counts[0];
  document.getElementById('cnt-2').textContent=counts[1];
  document.getElementById('cnt-3').textContent=counts[2];
  document.getElementById('cnt-miss').textContent=counts[3];
}

function showResults(){
  stopAudio();
  document.getElementById('quiz-card').classList.add('hidden');
  document.getElementById('results-screen').classList.remove('hidden');
  document.getElementById('progress-fill').style.width='100%';

  const total=shuffled.length;
  const totalCorrect=counts[0]+counts[1]+counts[2];
  const pts=counts[0]*3+counts[1]*2+counts[2]*1; // weighted score
  const maxPts=total*3;
  const pct=Math.round(pts/maxPts*100);

  document.getElementById('results-score').textContent=`${totalCorrect} / ${total}`;

  let emoji,msg;
  if(counts[3]===0 && counts[0]===total){ emoji='🏆'; msg='PERFECT! Every word on the first try! ⭐'; }
  else if(pct>=85){ emoji='🌟'; msg="Amazing work! Friday's test is going to go great!"; }
  else if(pct>=65){ emoji='😊'; msg="Really good job! Practice the ones you missed and you'll ace it!"; }
  else if(pct>=45){ emoji='💪'; msg="Good effort! Keep practicing — you're getting there!"; }
  else { emoji='📚'; msg='Keep going! Every practice makes you better!'; }

  document.getElementById('results-emoji').textContent=emoji;
  document.getElementById('results-msg').textContent=msg;

  document.getElementById('bd-1').textContent=counts[0]+' word'+(counts[0]!==1?'s':'');
  document.getElementById('bd-2').textContent=counts[1]+' word'+(counts[1]!==1?'s':'');
  document.getElementById('bd-3').textContent=counts[2]+' word'+(counts[2]!==1?'s':'');
  document.getElementById('bd-miss').textContent=counts[3]+' word'+(counts[3]!==1?'s':'');

  if(missedWords.length>0){
    document.getElementById('missed-list').classList.remove('hidden');
    document.getElementById('missed-words').innerHTML=missedWords.map(w=>`<span class="missed-word">${w}</span>`).join('');
  } else {
    document.getElementById('missed-list').classList.add('hidden');
  }
}

function restartSameMode(){
  document.getElementById('results-screen').classList.add('hidden');
  document.getElementById('quiz-card').classList.remove('hidden');
  startQuiz(quizMode);
}

function goToModeScreen(){
  stopAudio();
  document.getElementById('results-screen').classList.add('hidden');
  document.getElementById('score-bar').classList.add('hidden');
  document.getElementById('progress-wrap').classList.add('hidden');
  document.getElementById('mode-screen').classList.remove('hidden');
}

if(window.speechSynthesis){
  window.speechSynthesis.getVoices();
  window.speechSynthesis.onvoiceschanged=()=>window.speechSynthesis.getVoices();
}

document.getElementById('answer-input').addEventListener('keydown', e=>{
  if(e.key==='Enter'){
    if(!answered) checkAnswer();
    else if(!document.getElementById('next-btn').classList.contains('hidden')) nextWord();
  }
});
</script>
</body>
</html>
