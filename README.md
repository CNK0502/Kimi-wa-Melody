<html....>
<html lang="th">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Kimi-wa-Melody — GitHub-ready (Full HTML)</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#F5EFE6; --card:#FFFFFF; --accent:#7C5A3A; --muted:#7B6C5E; --good:#2E8B57; --bad:#C03B3B;
}
*{box-sizing:border-box}
body{margin:0;font-family:Inter,system-ui,Segoe UI,Roboto,'Noto Sans',Arial;color:#222;background:linear-gradient(180deg,#F7F3EE 0%, #EEF5F1 100%)}
.container{max-width:1200px;margin:20px auto;padding:18px;display:grid;grid-template-columns:1fr 360px;gap:18px}
.header{grid-column:1/-1;display:flex;align-items:center;gap:12px}
.logo{display:flex;gap:12px;align-items:center}
.logo .mascot{font-size:40px}
.title h1{margin:0;font-size:20px}
.title p{margin:0;color:var(--muted);font-size:13px}

.card{background:var(--card);border-radius:14px;padding:14px;box-shadow:0 8px 30px rgba(18,18,18,0.06)}
.controls{display:flex;gap:8px;align-items:center;flex-wrap:wrap;margin-top:8px}
select,input,button{padding:8px 12px;border-radius:10px;border:1px solid rgba(0,0,0,0.06);font-size:14px;background:#fff}
.big-btn{background:var(--accent);color:white;border:none;padding:10px 14px;border-radius:10px;cursor:pointer;box-shadow:0 6px 18px rgba(124,90,58,0.18)}
.small{font-size:13px;color:var(--muted)}

.main{display:flex;flex-direction:column;gap:12px}
.staff-area{display:flex;gap:12px;align-items:flex-start;flex-wrap:wrap}
.staff{flex:1;min-width:520px;padding:12px;border-radius:12px;background:linear-gradient(180deg,#fff 0%, #fffefc 100%);box-shadow:0 10px 30px rgba(17,17,17,0.06)}
.toolbar{display:flex;justify-content:space-between;align-items:center;gap:8px;margin-top:8px}
.choices{display:flex;gap:8px;flex-wrap:wrap;margin-top:10px}
.choice{flex:1;min-width:120px;background:linear-gradient(180deg,#fff 0%, #fbfbfb 100%);padding:12px;border-radius:10px;text-align:center;cursor:pointer;border:1px solid rgba(0,0,0,0.04);box-shadow:0 6px 14px rgba(50,50,50,0.04)}
.choice.correct{border-color:var(--good);background:linear-gradient(180deg,#E9FCF0,#F7FFF6)}
.choice.wrong{border-color:var(--bad);background:linear-gradient(180deg,#FFF2F2,#FFF9F9)}

.sidebar{display:flex;flex-direction:column;gap:12px}
.teacher-card{padding:12px;border-radius:12px;background:linear-gradient(180deg,#FFFFFF, #FFF8F2);box-shadow:0 8px 20px rgba(0,0,0,0.05)}
.input{width:100%;padding:10px;border-radius:8px;border:1px solid rgba(0,0,0,0.06);font-size:14px}

.modal-backdrop{position:fixed;inset:0;background:rgba(0,0,0,0.45);display:none;align-items:center;justify-content:center;z-index:60}
.modal{width:360px;background:white;padding:18px;border-radius:12px;box-shadow:0 20px 60px rgba(0,0,0,0.3)}
.gpt-box{background:linear-gradient(180deg,#fffefc,#ffffff);padding:10px;border-radius:12px;box-shadow:inset 0 1px 0 rgba(255,255,255,0.6),0 8px 20px rgba(20,20,20,0.04);height:220px;overflow:auto}
.gpt-msg{padding:8px;border-radius:8px;margin-bottom:8px;background:#f3f6ff;border:1px solid rgba(55,85,255,0.06)}

@media(max-width:980px){.container{grid-template-columns:1fr;}.sidebar{order:2}}
</style>
</head>
<body>
<div class="container">
  <div class="header">
    <div class="logo">
      <div class="mascot">🐱🎵</div>
      <div class="title">
        <h1>Kimi-wa-Melody</h1>
        <p class="small">Prototype — GitHub-ready single-file</p>
      </div>
    </div>
    <div style="margin-left:auto" class="small">Use in classroom — teacher PIN protected export</div>
  </div>

  <!-- Main area -->
  <div class="main">
    <div class="card controls">
      <div style="display:flex;gap:8px;align-items:center;flex-wrap:wrap">
        <label class="small">Level</label>
        <select id="levelSelect"></select>
        <button id="startBtn" class="big-btn">เริ่มด่าน</button>
        <div id="progress" class="small">ด่าน - | ข้อ - / 10</div>
      </div>
      <div style="margin-left:auto;display:flex;gap:8px;align-items:center;margin-top:8px">
        <label class="small">Mode</label>
        <select id="modeSelect"><option value="practice">Practice</option><option value="time">Time Challenge</option><option value="matching">Matching</option></select>
      </div>
    </div>

    <div class="staff-area">
      <div class="staff card">
        <svg id="staffSVG" viewBox="0 0 900 300" xmlns="http://www.w3.org/2000/svg" aria-label="staff">
          <g id="staffLines" stroke="#000" stroke-width="4" stroke-linecap="round"></g>
          <g id="clefGroup"></g>
          <g id="noteGroup"></g>
          <g id="ledgerGroup" stroke="#000" stroke-width="3"></g>
        </svg>

        <div class="toolbar">
          <div style="display:flex;gap:8px;align-items:center">
            <button id="playBtn" class="big-btn">🔊 ฟัง</button>
            <button id="answerBtn" class="big-btn" style="background:#6b8b9b">ดูคำตอบ</button>
            <button id="nextBtn" class="big-btn" style="background:#5a6">ถัดไป</button>
          </div>
          <div style="display:flex;gap:12px;align-items:center">
            <div class="small">เวลา: <span id="timer">--</span></div>
            <div class="small">คะแนน: <span id="score">0</span> ⭐</div>
          </div>
        </div>

        <div class="choices" id="choicesArea" aria-live="polite"></div>
        <div id="feedback" class="small" style="margin-top:10px">กดเริ่มด่านเพื่อเริ่ม</div>
      </div>
    </div>
  </div>

  <!-- Sidebar -->
  <div class="sidebar">
    <div class="teacher-card card">
      <strong>ใครกันนะ? ใส่ชื่อกันด้วยนะจ๊ะ</strong>
      <div style="display:flex;flex-direction:column;gap:8px;margin-top:8px">
        <input id="stuName" class="input" placeholder="ชื่อ-สกุล นักเรียน" />
        <input id="stuNo" class="input" placeholder="เลขที่" />
        <input id="stuClass" class="input" placeholder="ห้อง" />
        <div style="display:flex;gap:8px;margin-top:6px">
          <button id="saveStu" class="big-btn">บันทึกข้อมูล</button>
          <button id="clearStu" class="big-btn" style="background:#999">ลบ</button>
        </div>
        <hr style="border:none;border-top:1px solid rgba(0,0,0,0.06)">

        <div style="display:flex;gap:8px;flex-wrap:wrap">
          <button id="saveScore" class="big-btn">บันทึกคะแนน</button>
          <button id="exportCSV" class="big-btn" style="background:#666">Export CSV (PIN)</button>
        </div>
        <div class="small" style="margin-top:8px">Export จะขอ PIN ครู แล้วจะดาวน์โหลด CSV หรือส่งไป Google Sheets (ถ้าตั้งไว้)</div>
      </div>
    </div>

    <div class="card">
      <strong>GPT — ช่วยครู (local)</strong>
      <div class="gpt-box" id="gptBox">
        <div class="gpt-msg">สวัสดีครู! พิมพ์คำสั่งสั้นๆ เช่น "สรุปคะแนนล่าสุด" หรือ "วิธีใช้"</div>
      </div>
      <div style="display:flex;gap:8px;margin-top:8px">
        <input id="gptInput" class="input" placeholder="พิมพ์คำถามหรือคำสั่ง">
        <button id="gptSend" class="big-btn">ส่ง</button>
      </div>
    </div>
  </div>
</div>

<!-- PIN modal -->
<div class="modal-backdrop" id="modalBackdrop">
  <div class="modal">
    <h3>ยืนยันสิทธิ์ครู</h3>
    <p class="small">กรอก PIN ครูเพื่ออนุญาตการส่งออก/ส่งไป Google Sheets</p>
    <div style="display:flex;gap:8px;align-items:center;margin-top:10px">
      <input id="pinInput" style="flex:1;padding:10px;border-radius:8px;border:1px solid #ddd" placeholder="รหัสครู...">
      <button id="pinOk" class="big-btn">ยืนยัน</button>
    </div>
    <div style="display:flex;justify-content:flex-end;margin-top:10px">
      <button id="pinCancel" style="padding:8px 12px;border-radius:8px;border:none;background:#eee;cursor:pointer">ยกเลิก</button>
    </div>
  </div>
</div>

<script>
/* ----------------- Configuration ----------------- */
/* Teacher PIN (change if you want) */
const TEACHER_PIN = "Teacherversion5791";
/* Optional: if you deploy Apps Script Web App, paste URL here to send results to a Google Sheet */
let SHEETS_WEBHOOK_URL = ""; // e.g. "https://script.google.com/macros/s/XXXX/exec"

/* ----------------- Note Definitions ----------------- */
/* The seven notes with Thai names as requested:
   C (โด), D (เร), E (มี), F (ฟา), G (ซอล), A (ลา), B (ที)
*/
const NOTES = [
  {name:"C",thai:"โด",freq:261.63},
  {name:"D",thai:"เร",freq:293.66},
  {name:"E",thai:"มี",freq:329.63},
  {name:"F",thai:"ฟา",freq:349.23},
  {name:"G",thai:"ซอล",freq:392.00},
  {name:"A",thai:"ลา",freq:440.00},
  {name:"B",thai:"ที",freq:493.88}
];
const TOTAL_LEVELS = 20;
const QUESTIONS_PER_LEVEL = 10;
function notesPerQuestion(level){ if(level<=7) return 1; if(level<=14) return 2; return 3; }

/* ----------------- State & DOM refs ----------------- */
let state = { level:1, qIndex:0, current:null, score:0, running:false, mode:'practice', student:{name:'',no:'',class:''} };

const levelSelect = document.getElementById('levelSelect');
const startBtn = document.getElementById('startBtn');
const progress = document.getElementById('progress');
const playBtn = document.getElementById('playBtn');
const answerBtn = document.getElementById('answerBtn');
const nextBtn = document.getElementById('nextBtn');
const choicesArea = document.getElementById('choicesArea');
const scoreEl = document.getElementById('score');
const feedback = document.getElementById('feedback');
const modeSelect = document.getElementById('modeSelect');
const timerEl = document.getElementById('timer');

const stuName = document.getElementById('stuName');
const stuNo = document.getElementById('stuNo');
const stuClass = document.getElementById('stuClass');
const saveStu = document.getElementById('saveStu');
const clearStu = document.getElementById('clearStu');
const saveScore = document.getElementById('saveScore');
const exportCSV = document.getElementById('exportCSV');

const staffSVG = document.getElementById('staffSVG');
const staffLines = document.getElementById('staffLines');
const clefGroup = document.getElementById('clefGroup');
const noteGroup = document.getElementById('noteGroup');
const ledgerGroup = document.getElementById('ledgerGroup');

const modalBackdrop = document.getElementById('modalBackdrop');
const pinInput = document.getElementById('pinInput');
const pinOk = document.getElementById('pinOk');
const pinCancel = document.getElementById('pinCancel');

const gptBox = document.getElementById('gptBox');
const gptInput = document.getElementById('gptInput');
const gptSend = document.getElementById('gptSend');

/* ----------------- Drawing staff & clef ----------------- */
function drawStaffAndClef(){
  staffLines.innerHTML=''; clefGroup.innerHTML=''; noteGroup.innerHTML=''; ledgerGroup.innerHTML='';
  const left=110, right=760, bottomY=170, gap=20;
  for(let i=0;i<5;i++){
    const y = bottomY - i*gap;
    const line = document.createElementNS('http://www.w3.org/2000/svg','line');
    line.setAttribute('x1',left); line.setAttribute('y1',y); line.setAttribute('x2',right); line.setAttribute('y2',y);
    line.setAttribute('stroke','#000'); line.setAttribute('stroke-width',4); line.setAttribute('stroke-linecap','round');
    staffLines.appendChild(line);
  }
  // SMuFL-like treble clef path (vector) tuned to circle the 2nd line
  const clefPathD = "M38.5,6.3c-1.8,0.9-4.3,4.1-5.3,6.4c-0.9,2-1.4,4.8-0.9,7.2c0.5,2.7,2.2,5.1,5.2,6.7c2.7,1.4,5.1,1.8,7.1,2.0c5.6,0.7,9.1,3.6,9.4,8.1c0.3,4.6-3.1,9.1-8.7,13.4c-2.3,1.6-5.0,3.2-8.2,4.7c-3.3,1.6-6.0,3.1-8.1,4.6c-3.1,2.4-4.8,5.1-4.8,8.1c0,2.8,1.2,5.0,3.6,6.5c2.4,1.6,5.9,2.3,10.2,2.3c3.0,0,5.8-0.4,8.3-1.2c0.5-0.2,0.9-0.3,1.3-0.5c4.2-1.6,6.9-3.6,7.4-6.1c0.4-2.7-1.0-5.7-4.0-8.3c-3.1-2.6-7.3-3.7-12.3-3.7c-3.0,0-5.4,0.4-7.2,1.2c-1.1,0.4-2.0,0.8-2.7,1.2c-0.8,0.8-1.2,1.9-1.2,3.3c0,2,1.1,3.9,3.4,5.4c2.2,1.6,5.1,2.4,8.8,2.4c7.4,0,12.8-2.6,16.1-7.8c2.0-3.1,2.4-6.2,1.4-8.9c-0.9-2.7-3.2-5.1-6.9-6.9c-2.1-1.0-4.7-1.9-7.7-2.9c-3-0.9-5.4-2.0-7.2-3.6c-3.9-3.3-6.2-7.8-6.2-13.3c0-6.3,2.8-11.9,8.3-16.8c5.5-4.9,13.1-8.0,22.8-8.9c4.8-0.4,8.8-1.5,12.0-3.3c5.2-2.7,7.9-6.7,7.9-11.4c0-5.0-2.3-9.3-6.8-12.7c-4.6-3.4-10.8-5.1-18.6-5.1c-5.7,0-12.2,1.1-19.5,3.5z";
  const svgNS = 'http://www.w3.org/2000/svg';
  const g = document.createElementNS(svgNS,'g');
  const p = document.createElementNS(svgNS,'path');
  p.setAttribute('d', clefPathD);
  p.setAttribute('fill', '#000');
  const baseX = 30, baseY = 8, scale = 1.12;
  g.appendChild(p);
  g.setAttribute('transform', `translate(${baseX}, ${baseY}) scale(${scale})`);
  clefGroup.appendChild(g);

  staffSVG.dataset.bottomY = bottomY;
  staffSVG.dataset.gap = gap;
}
drawStaffAndClef();

/* ---------- staff mapping ---------- */
function getStaffY(noteName){
  const bottomY = parseFloat(staffSVG.dataset.bottomY);
  const gap = parseFloat(staffSVG.dataset.gap);
  // mapping as requested: C below staff with ledger, then D (below 1st line), E (1st line), F (1st space), etc.
  const map = {"C": bottomY + gap, "D": bottomY + gap/2, "E": bottomY, "F": bottomY - gap/2, "G": bottomY - gap, "A": bottomY - gap*1.5, "B": bottomY - gap*2};
  return map[noteName];
}

/* ---------- render sequence (quarter notes) ---------- */
function renderSequence(seq){
  noteGroup.innerHTML=''; ledgerGroup.innerHTML='';
  const startX = 360; const stepX = 48;
  seq.forEach((n,i)=>{
    const x = startX + i*stepX;
    const y = getStaffY(n);
    const svgNS = 'http://www.w3.org/2000/svg';
    const head = document.createElementNS(svgNS,'ellipse');
    head.setAttribute('cx',x); head.setAttribute('cy',y); head.setAttribute('rx',16); head.setAttribute('ry',12);
    head.setAttribute('fill','#000'); head.setAttribute('transform',`rotate(-12 ${x} ${y})`);
    noteGroup.appendChild(head);
    const stem = document.createElementNS(svgNS,'rect');
    stem.setAttribute('x',x+14); stem.setAttribute('y',y-60); stem.setAttribute('width',3.8); stem.setAttribute('height',60); stem.setAttribute('fill','#000');
    noteGroup.appendChild(stem);
    // ledger for middle C
    if(n === 'C'){
      const ledger = document.createElementNS(svgNS,'line');
      ledger.setAttribute('x1',x-28); ledger.setAttribute('x2',x+28); ledger.setAttribute('y1',y); ledger.setAttribute('y2',y);
      ledger.setAttribute('stroke','#000'); ledger.setAttribute('stroke-width',3);
      ledgerGroup.appendChild(ledger);
    }
  });
}

/* ---------- choices creation ----------
   Requirement:
   - If question is single-note (k==1): choices must be ALL 7 notes (shuffled), showing "C (โด)" etc.
   - If question has k>1: produce 4 options (1 correct + 3 distractors).
*/
function seqToLabel(seq){ return seq.join(' '); }
function seqToDisplay(seq){
  // display with Thai names: "C(โด) D(เร)"
  return seq.map(n => {
    const obj = NOTES.find(x => x.name === n);
    return obj ? `${obj.name}(${obj.thai})` : n;
  }).join(' ');
}

function createChoices(correctSeq){
  const k = correctSeq.length;
  if(k === 1){
    // return all 7 notes as choices, shuffled
    const arr = NOTES.map(n => n.name);
    // shuffle
    for(let i=arr.length-1;i>0;i--){ const j = Math.floor(Math.random()*(i+1)); [arr[i],arr[j]]=[arr[j],arr[i]]; }
    // Map to display form
    return arr.map(s => ({label: s, display: seqToDisplay([s])}));
  } else {
    // create 4 options: one is correct (seqToLabel) and three distractors made of random notes (avoid duplicates)
    const set = new Set();
    const correctLabel = seqToLabel(correctSeq);
    set.add(correctLabel);
    while(set.size < 4){
      const arr = [];
      for(let i=0;i<k;i++){ arr.push(NOTES[Math.floor(Math.random()*NOTES.length)].name); }
      set.add(seqToLabel(arr));
    }
    const arr = Array.from(set);
    // shuffle
    for(let i=arr.length-1;i>0;i--){ const j = Math.floor(Math.random()*(i+1)); [arr[i],arr[j]]=[arr[j],arr[i]]; }
    return arr.map(s => ({label: s, display: seqToDisplay(s.split(' '))}));
  }
}

/* ---------- question generator ---------- */
function generateQuestion(level){
  const k = notesPerQuestion(level);
  const seq = [];
  for(let i=0;i<k;i++){ seq.push(NOTES[Math.floor(Math.random()*NOTES.length)].name); }
  const choices = createChoices(seq);
  return {seq, choices, answer: seqToLabel(seq)};
}

/* ---------- populate level select ---------- */
for(let i=1;i<=TOTAL_LEVELS;i++){
  const o = document.createElement('option');
  o.value = i;
  o.textContent = 'Level ' + i + ' (' + notesPerQuestion(i) + ' โน้ต/ข้อ)';
  levelSelect.appendChild(o);
}
levelSelect.value = 1;

/* ---------- audio helpers ---------- */
const AudioCtx = window.AudioContext || window.webkitAudioContext;
const ctx = new AudioCtx();
function playTone(freq,dur=0.45){
  const o = ctx.createOscillator();
  const g = ctx.createGain();
  o.type = 'sine';
  o.frequency.setValueAtTime(freq, ctx.currentTime);
  o.connect(g); g.connect(ctx.destination);
  g.gain.setValueAtTime(0, ctx.currentTime);
  g.gain.linearRampToValueAtTime(0.18, ctx.currentTime + 0.01);
  o.start();
  g.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + dur);
  setTimeout(()=>o.stop(), dur*1000 + 60);
}
function playSequence(freqs, interval = 320){
  freqs.forEach((f,i) => setTimeout(()=> playTone(f, 0.44), i*interval));
}
function playCorrect(seq){
  const freqs = seq.map(n => NOTES.find(x=>x.name===n).freq);
  playSequence(freqs, 250);
  setTimeout(()=>{ playTone(880,0.08); setTimeout(()=>playTone(1174,0.08),100); }, seq.length*250 + 80);
}
function playWrong(){ playTone(220,0.18); }

/* ---------- runtime ---------- */
function renderCurrent(){
  renderSequence(state.current.seq);
  choicesArea.innerHTML = '';
  // if single-note and choices array contains all 7 (object with label/display), render accordingly
  state.current.choices.forEach(ch => {
    const d = document.createElement('div');
    d.className = 'choice';
    d.dataset.value = ch.label;
    d.innerHTML = `<div style="font-weight:600">${ch.display}</div>`;
    d.addEventListener('click', ()=> onChoice(ch.label, d));
    choicesArea.appendChild(d);
  });
  feedback.textContent = 'ข้อที่ ' + (state.qIndex+1) + ' — เลือกคำตอบที่ถูกต้อง';
  scoreEl.textContent = state.score;
}

function onChoice(choiceLabel, el){
  if(!state.running) return;
  const correct = choiceLabel === state.current.answer;
  if(correct){
    el.classList.add('correct');
    feedback.textContent = 'ถูกต้อง!';
    playCorrect(state.current.seq);
    state.score++;
  } else {
    el.classList.add('wrong');
    feedback.textContent = 'ผิด! คำตอบคือ ' + seqToDisplay(state.current.answer.split(' '));
    playWrong();
  }
  // disable further clicks
  Array.from(choicesArea.children).forEach(c=> c.style.pointerEvents='none');
  setTimeout(()=> {
    state.qIndex++;
    updateProgress();
    if(state.qIndex < QUESTIONS_PER_LEVEL){
      state.current = generateQuestion(state.level);
      renderCurrent();
    } else {
      finishLevel();
    }
  }, 900);
}

startBtn.addEventListener('click', ()=>{
  state.level = parseInt(levelSelect.value);
  state.qIndex = 0;
  state.score = 0;
  state.running = true;
  state.mode = modeSelect.value;
  state.current = generateQuestion(state.level);
  renderCurrent();
  updateProgress();
});

function updateProgress(){
  progress.textContent = 'ด่าน: ' + state.level + ' | ข้อ: ' + Math.min(state.qIndex+1, QUESTIONS_PER_LEVEL) + ' / ' + QUESTIONS_PER_LEVEL;
}

function finishLevel(){
  state.running = false;
  feedback.textContent = `จบด่าน! คะแนน: ${state.score} / ${QUESTIONS_PER_LEVEL}`;
  // show summary in sidebar
  const summaryEl = document.getElementById('summary');
  if(summaryEl) summaryEl.textContent = `นักเรียน: ${state.student.name||'-'} | ห้อง: ${state.student.class||'-'} | เลขที่: ${state.student.no||'-'} | ด่าน: ${state.level} | คะแนน: ${state.score}/${QUESTIONS_PER_LEVEL}`;
}

/* play / answer / next */
playBtn.addEventListener('click', ()=> {
  if(!state.current) return;
  if(ctx.state === 'suspended') ctx.resume();
  const freqs = state.current.seq.map(n => NOTES.find(x=>x.name===n).freq);
  playSequence(freqs, 360);
});
answerBtn.addEventListener('click', ()=> {
  if(!state.current) return;
  feedback.textContent = 'คำตอบ: ' + seqToDisplay(state.current.answer.split(' '));
});
nextBtn.addEventListener('click', ()=> {
  if(!state.running) return;
  state.qIndex++;
  if(state.qIndex < QUESTIONS_PER_LEVEL){
    state.current = generateQuestion(state.level);
    renderCurrent();
    updateProgress();
  } else finishLevel();
});

/* ---------- student info and local records ---------- */
saveStu.addEventListener('click', ()=>{
  state.student.name = stuName.value.trim();
  state.student.no = stuNo.value.trim();
  state.student.class = stuClass.value.trim();
  localStorage.setItem('kimi_student', JSON.stringify(state.student));
  alert('บันทึกข้อมูลนักเรียนแล้ว ✅');
  const summaryEl = document.getElementById('summary');
  if(summaryEl) summaryEl.textContent = `นักเรียน: ${state.student.name||'-'} | ชั้น: ${state.student.class||'-'} | เลขที่: ${state.student.no||'-'}`;
});
clearStu.addEventListener('click', ()=> {
  stuName.value=''; stuNo.value=''; stuClass.value='';
  state.student = {name:'',no:'',class:''};
  localStorage.removeItem('kimi_student');
  const summaryEl = document.getElementById('summary');
  if(summaryEl) summaryEl.textContent = 'ยังไม่มีการฝึก';
});

/* save score */
saveScore.addEventListener('click', ()=> {
  const rec = { student: state.student, level: state.level, score: state.score, total: QUESTIONS_PER_LEVEL, date: new Date().toISOString() };
  const key = 'kimi_records_v_final';
  const arr = JSON.parse(localStorage.getItem(key) || '[]');
  arr.push(rec);
  localStorage.setItem(key, JSON.stringify(arr));
  alert('บันทึกคะแนนเรียบร้อย ✅');
});

/* ---------- Export CSV with modal PIN ---------- */
exportCSV.addEventListener('click', ()=> {
  modalBackdrop.style.display = 'flex';
  pinInput.value = '';
  pinInput.focus();
});
pinCancel.addEventListener('click', ()=> modalBackdrop.style.display = 'none');
pinOk.addEventListener('click', async ()=> {
  const pin = pinInput.value.trim();
  if(pin !== TEACHER_PIN){ alert('รหัสไม่ถูกต้อง'); return; }
  modalBackdrop.style.display = 'none';
  const key = 'kimi_records_v_final';
  const arr = JSON.parse(localStorage.getItem(key) || '[]');
  if(arr.length === 0){ alert('ยังไม่มีข้อมูลให้ส่งออก'); return; }

  // Optionally send to Google Sheets webhook (Apps Script)
  if(SHEETS_WEBHOOK_URL){
    try{
      const resp = await fetch(SHEETS_WEBHOOK_URL, {
        method: 'POST',
        headers: {'Content-Type':'application/json'},
        body: JSON.stringify({records: arr})
      });
      if(resp.ok) alert('ส่งข้อมูลไปยัง Google Sheets สำเร็จ');
      else alert('ส่งไปยัง Google Sheets ไม่สำเร็จ (status ' + resp.status + ')');
    }catch(e){
      console.error(e); alert('เกิดข้อผิดพลาดในการส่งข้อมูลไปยัง Google Sheets');
    }
  }

  // build CSV
  let csv = 'name,class,no,level,score,total,date\n';
  arr.forEach(r => {
    const n = r.student && r.student.name ? r.student.name.replace(/"/g,'""') : '';
    const c = r.student && r.student.class ? r.student.class.replace(/"/g,'""') : '';
    const no = r.student && r.student.no ? r.student.no.replace(/"/g,'""') : '';
    csv += `"${n}","${c}","${no}",${r.level},${r.score},${r.total},"${r.date}"\n`;
  });
  const blob = new Blob([csv], {type:'text/csv;charset=utf-8;'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a'); a.href = url; a.download = 'kimi_records.csv'; document.body.appendChild(a); a.click(); a.remove(); URL.revokeObjectURL(url);
  alert('ดาวน์โหลด CSV เรียบร้อย');
});

/* ---------- GPT-like sidebar (local/simple) ---------- */
gptSend.addEventListener('click', ()=> {
  const q = gptInput.value.trim();
  if(!q) return;
  const askBox = document.createElement('div'); askBox.className='gpt-msg'; askBox.textContent = 'คุณ: ' + q; gptBox.appendChild(askBox);

  const resp = document.createElement('div'); resp.className='gpt-msg';
  if(/สรุปคะแนน/.test(q)){
    const arr = JSON.parse(localStorage.getItem('kimi_records_v_final') || '[]');
    if(arr.length === 0) resp.textContent = 'ยังไม่มีคะแนนบันทึกไว้';
    else {
      const last = arr[arr.length-1];
      resp.textContent = `ล่าสุด: ${last.student.name||'-'} | ด่าน ${last.level} | คะแนน ${last.score}/${last.total}`;
    }
  } else if(/วิธีใช้|help/i.test(q)){
    resp.textContent = 'กด Start เพื่อเริ่มด่าน บันทึกคะแนนด้วย "บันทึกคะแนน" และใช้ "Export CSV" เพื่อดาวน์โหลดผล (ต้องการ PIN ครู)';
  } else {
    resp.textContent = 'ฉันช่วยได้: "สรุปคะแนน", "วิธีใช้" หรือ "ส่งไป Google Sheets" — ลองพิมพ์คำสั่งสั้น ๆ';
  }
  gptBox.appendChild(resp);
  gptInput.value = '';
  gptBox.scrollTop = gptBox.scrollHeight;
});

/* ---------- init on load ---------- */
document.addEventListener('DOMContentLoaded', ()=>{
  const saved = JSON.parse(localStorage.getItem('kimi_student') || 'null');
  if(saved){
    state.student = saved;
    stuName.value = saved.name || '';
    stuNo.value = saved.no || '';
    stuClass.value = saved.class || '';
    const summaryEl = document.getElementById('summary');
    if(summaryEl) summaryEl.textContent = `นักเรียน: ${state.student.name||'-'} | ชั้น: ${state.student.class||'-'} | เลขที่: ${state.student.no||'-'}`;
  }
  drawStaffAndClef();
});
</script>
</body>
</html>
