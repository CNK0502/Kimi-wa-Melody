<html....>
<html lang="th">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Kimi-wa-Melody — Staff + Clef Updated</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#F5EFE6; --card:#FFFFFF; --accent:#7C5A3A; --muted:#7B6C5E; --good:#2E8B57; --bad:#C03B3B;
  --timegreen-start:#E6F7ED; --timegreen-accent:#4B8A5A;
}
*{box-sizing:border-box}
body{margin:0;font-family:Inter,system-ui,Segoe UI,Roboto,'Noto Sans',Arial;color:#222;background:linear-gradient(180deg,#F7F3EE 0%, #EEF5F1 100%)}
.container{max-width:1200px;margin:20px auto;padding:18px;display:grid;grid-template-columns:1fr 360px;gap:18px}
.header{grid-column:1/-1;display:flex;align-items:center;gap:12px}
.logo{display:flex;gap:12px;align-items:center}
.logo .mascot{font-size:40px}
.title h1{margin:0;font-size:20px}
.title p{margin:0;color:var(--muted);font-size:13px}

/* cards, buttons */
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

/* Time Challenge styling override */
.time-theme .staff{background:linear-gradient(180deg,var(--timegreen-start), #F1FAF2); border:1px solid rgba(75,138,90,0.06)}
.time-theme .big-btn{background:var(--timegreen-accent)}
.time-theme .choice{box-shadow:0 6px 14px rgba(55,120,80,0.04)}
.time-theme .choice.correct{background:linear-gradient(180deg,#E8F7EB,#F7FFF6)}

/* sidebar and inputs */
.sidebar{display:flex;flex-direction:column;gap:12px}
.teacher-card{padding:12px;border-radius:12px;background:linear-gradient(180deg,#FFFFFF, #FFF8F2);box-shadow:0 8px 20px rgba(0,0,0,0.05)}
.input{width:100%;padding:10px;border-radius:8px;border:1px solid rgba(0,0,0,0.06);font-size:14px}

.modal-backdrop{position:fixed;inset:0;background:rgba(0,0,0,0.45);display:none;align-items:center;justify-content:center;z-index:60}
.modal{width:360px;background:white;padding:18px;border-radius:12px;box-shadow:0 20px 60px rgba(0,0,0,0.3)}
.leaderboard{max-height:180px;overflow:auto;padding:8px;border-radius:8px;background:#fff;box-shadow:inset 0 1px 0 rgba(0,0,0,0.02)}
.center{display:flex;align-items:center;justify-content:center}

/* landing overlay */
.landing{position:fixed;inset:0;background:linear-gradient(180deg, rgba(0,0,0,0.25), rgba(0,0,0,0.25));display:flex;align-items:center;justify-content:center;z-index:80}
.landing .card{width:680px;padding:20px}
.landing .row{display:flex;gap:8px;align-items:center;margin-top:8px}

/* responsive */
@media(max-width:980px){.container{grid-template-columns:1fr;}.sidebar{order:2}.landing .card{width:92%;}}
/* small cosmetic for SVG */
svg { width:100%; height:auto; display:block; }
</style>
</head>
<body>

<!-- Landing screen -->
<div class="landing" id="landingScreen" role="dialog" aria-modal="true">
  <div class="card">
    <div style="display:flex;align-items:center;gap:12px">
      <div style="font-size:44px">🐱🎵</div>
      <div>
        <h2 style="margin:0">Kimi-wa-Melody</h2>
        <div style="color:var(--muted)">กรุณากรอกข้อมูลก่อนเริ่ม — ข้อมูลจะถูกเก็บไว้ในเครื่อง</div>
      </div>
    </div>

    <div style="margin-top:12px">
      <label class="small">ชื่อ-สกุล (หรือ ชื่อกลุ่ม)</label>
      <input id="landingName" class="input" placeholder="ตัวอย่าง: นุ่น / กลุ่ม 1">
    </div>
    <div class="row" style="margin-top:8px">
      <div style="flex:1">
        <label class="small">เลขที่</label>
        <input id="landingNo" class="input" placeholder="เลขที่">
      </div>
      <div style="flex:1">
        <label class="small">ห้อง</label>
        <input id="landingClass" class="input" placeholder="เช่น ป.4/1">
      </div>
    </div>

    <div style="margin-top:12px">
      <label class="small">เลือกโหมด</label>
      <select id="landingMode" class="input">
        <option value="practice">Practice — แบบฝึกหัด (20 ด่าน × 10 ข้อ)</option>
        <option value="time">Time Challenge — แข่ง 60 วินาที (เก็บคะแนนสูงสุด)</option>
      </select>
    </div>

    <div style="display:flex;gap:8px;justify-content:flex-end;margin-top:14px">
      <button id="landingStart" class="big-btn">เริ่มเลย</button>
    </div>
  </div>
</div>

<div class="container" id="appRoot" aria-hidden="true">
  <div class="header">
    <div class="logo">
      <div class="mascot">🐱🎵</div>
      <div class="title">
        <h1>Kimi-wa-Melody</h1>
        <p class="small">Practice & Time Challenge — ฝึกอ่านโน้ต</p>
      </div>
    </div>
    <div style="margin-left:auto" class="small">Pin ครูสำหรับ Export: change TEACHER_PIN in code</div>
  </div>

  <div class="main" id="mainCol">
    <div class="card controls">
      <div style="display:flex;gap:8px;align-items:center;flex-wrap:wrap">
        <label class="small">Level</label>
        <select id="levelSelect"></select>
        <button id="startBtn" class="big-btn">เริ่มด่าน</button>
        <div id="progress" class="small">ด่าน - | ข้อ - / 10</div>
      </div>
      <div style="margin-left:auto;display:flex;gap:8px;align-items:center;margin-top:8px">
        <label class="small">Mode</label>
        <select id="modeSelect"><option value="practice">Practice</option><option value="time">Time Challenge</option></select>
      </div>
    </div>

    <div class="staff-area" id="staffArea">
      <div class="staff card" id="staffCard">
        <!-- SVG staff area -->
        <svg id="staffSVG" viewBox="0 0 900 300" xmlns="http://www.w3.org/2000/svg" aria-label="staff" role="img">
          <g id="staffLines" stroke="#000" stroke-width="4" stroke-linecap="round"></g>
          <g id="clefGroup" aria-hidden="true"></g>
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
        <div id="feedback" class="small" style="margin-top:10px">กดเริ่มเพื่อเริ่ม</div>
      </div>
    </div>
  </div>

  <div class="sidebar">
    <div class="teacher-card card">
      <strong>ข้อมูลนักเรียน (ครู)</strong>
      <div style="display:flex;flex-direction:column;gap:8px;margin-top:8px">
        <input id="stuName" class="input" placeholder="ชื่อ-สกุล นักเรียน (หรือ ชื่อกลุ่ม)" />
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
        <div class="small" style="margin-top:8px">Export จะขอ PIN ครู แล้วจะดาวน์โหลด CSV หรือส่งไป Google Sheets (ถ้าตั้งค่า)</div>

        <hr style="border:none;border-top:1px solid rgba(0,0,0,0.06)">
        <div><strong>Time Challenge leaderboard</strong></div>
        <div id="leaderboard" class="leaderboard small">ยังไม่มีผลการแข่งขัน</div>
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
/* -------------- Configuration -------------- */
const TEACHER_PIN = "Teacherversion5791";
let SHEETS_WEBHOOK_URL = ""; // set Apps Script URL if needed

/* notes */
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

/* -------------- State & DOM -------------- */
let state = { level:1, qIndex:0, current:null, score:0, running:false, mode:'practice', student:{name:'',no:'',class:''}, timeModeTimer:null, timeRemaining:0 };

const landingScreen = document.getElementById('landingScreen');
const landingStart = document.getElementById('landingStart');
const landingName = document.getElementById('landingName');
const landingNo = document.getElementById('landingNo');
const landingClass = document.getElementById('landingClass');
const landingMode = document.getElementById('landingMode');

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

const leaderboardEl = document.getElementById('leaderboard');
const staffCard = document.getElementById('staffCard');

/* -------------- Draw staff & clef (replaced with your updated code) -------------- */
function drawStaffAndClef(){
    // 1. ล้างข้อมูลเก่า
    staffLines.innerHTML = '';
    clefGroup.innerHTML = '';
    noteGroup.innerHTML = '';
    ledgerGroup.innerHTML = '';

    const left = 110, right = 760, bottomY = 170, gap = 20;
    const svgNS = 'http://www.w3.org/2000/svg';

    // 2. วาดบรรทัดห้าเส้น
    for(let i=0;i<5;i++){
        const y = bottomY - i*gap;
        const line = document.createElementNS(svgNS, 'line');
        line.setAttribute('x1', left);
        line.setAttribute('y1', y);
        line.setAttribute('x2', right);
        line.setAttribute('y2', y);
        line.setAttribute('stroke', '#000');
        line.setAttribute('stroke-width', 4);
        line.setAttribute('stroke-linecap', 'round');
        staffLines.appendChild(line);
    }

    // 3. ข้อมูล Path สำหรับกุญแจซอล (จากรูปที่คุณให้)
    const clefPathD =
        "M115.9,19.6c-3.1,1.6-6.8,4.8-9.9,8.6c-6.0,7.6-8.5,16.8-6.3,24.0c2.1,6.9,8.5,11.8,16.3,13.4c5.8,1.1,11.6,0.7,16.3-1.3c8.6-3.6,13.8-11.3,14.9-20.3c1.2-9.9-2.9-20.6-12.2-30.9c-2.9-3.0-6.0-5.6-9.3-7.7c-4.1-2.6-8.0-4.6-11.8-6.1z " +
        "M111.4,46.8c2.6-0.9,5.9-0.6,9.4,0.8c6.1,2.4,9.6,6.7,10.0,11.0c0.6,6.7-3.7,13.3-11.8,17.4c-4.5,2.4-9.6,3.4-14.8,2.9c-6.2-0.6-11.3-3.7-14.6-8.4c-3.0-4.2-3.8-9.5-2.2-14.1c1.1-3.1,3.5-6.0,6.6-8.4C98.1,50.9,104.6,48.3,111.4,46.8z " +
        "M121.0,95.3c-0.3,1.3-0.7,2.5-1.3,3.7c-2.8,6.4-8.9,11.6-17.6,15.0c-3.9,1.5-8.0,2.5-12.0,3.2c-6.6,1.0-12.2,2.6-16.1,4.6c-6.2,3.2-9.6,7.6-9.7,12.9c-0.2,6.2,4.0,11.8,12.4,16.5c7.8,4.3,17.9,6.5,28.7,6.5c9.6,0,19.1-1.9,26.5-6.4c6.2-3.8,9.7-8.5,10.6-13.2c0.9-4.8-0.6-9.5-4.1-13.4c-3.8-4.2-9.9-6.8-18.0-7.9c-1.9-0.2-4.0-0.2-6.1,0.0c-4.3,0.4-7.9,1.3-10.6,2.7c-2.6,1.3-4.5,3.0-5.6,5.1c-1.2,2.3-1.5,5.0-0.6,7.9c1.3,4.1,5.0,7.6,10.8,10.8c5.6,3.0,12.0,4.5,18.6,4.5c5.6,0,11.2-0.9,15.7-2.6c3.5-1.3,6.6-3.0,9.2-5.1c2.5-2.0,4.6-4.4,6.1-7.1c1.5-2.8,2.3-5.7,2.4-8.6c0.1-3.3-0.9-6.6-2.9-9.9c-3.3-5.3-9.5-9.3-18.4-11.6c-3.9-1.0-8.3-1.8-13.1-2.2c-0.6-0.0-1.1-0.0-1.7-0.0C123.3,94.9,122.1,95.1,121.0,95.3z";

    // 4. วาดกุญแจซอล
    const g = document.createElementNS(svgNS, 'g');

    const clefPath = document.createElementNS(svgNS, 'path');
    clefPath.setAttribute('d', clefPathD);
    clefPath.setAttribute('fill', '#000');

    // ปรับตำแหน่งกุญแจซอลให้เหมาะสมกับ Staff Lines ที่วาดไว้
    // default transform — ปรับค่า translate(x,y) และ scale(...) ถ้าต้องการ
    g.setAttribute('transform', 'translate(52, -68) scale(0.21)');

    g.appendChild(clefPath);
    clefGroup.appendChild(g);

    // ให้ตำแหน่งสำหรับการวาดโน้ตใช้งานต่อ
    staffSVG.dataset.bottomY = bottomY;
    staffSVG.dataset.gap = gap;
}
drawStaffAndClef();

/* -------------- Staff mapping & rendering notes -------------- */
function getStaffY(noteName){
  const bottomY = parseFloat(staffSVG.dataset.bottomY);
  const gap = parseFloat(staffSVG.dataset.gap);
  const map = {"C": bottomY + gap, "D": bottomY + gap/2, "E": bottomY, "F": bottomY - gap/2, "G": bottomY - gap, "A": bottomY - gap*1.5, "B": bottomY - gap*2};
  return map[noteName];
}

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
    if(n === 'C'){
      const ledger = document.createElementNS(svgNS,'line');
      ledger.setAttribute('x1',x-28); ledger.setAttribute('x2',x+28); ledger.setAttribute('y1',y); ledger.setAttribute('y2',y);
      ledger.setAttribute('stroke','#000'); ledger.setAttribute('stroke-width',3);
      ledgerGroup.appendChild(ledger);
    }
  });
}

/* -------------- Choices & questions -------------- */
function seqToLabel(seq){ return seq.join(' '); }
function seqToDisplay(seq){
  return seq.map(n=>{
    const o = NOTES.find(x=>x.name===n);
    return o ? `${o.name}(${o.thai})` : n;
  }).join(' ');
}

function createChoices(correctSeq){
  const k = correctSeq.length;
  if(k === 1){
    const arr = NOTES.map(n=> n.name);
    for(let i=arr.length-1;i>0;i--){ const j = Math.floor(Math.random()*(i+1)); [arr[i],arr[j]]=[arr[j],arr[i]]; }
    return arr.map(s=> ({ label: s, display: seqToDisplay([s]) }) );
  } else {
    const set = new Set();
    set.add(seqToLabel(correctSeq));
    while(set.size < 4){
      const arr = [];
      for(let i=0;i<k;i++){ arr.push(NOTES[Math.floor(Math.random()*NOTES.length)].name); }
      set.add(seqToLabel(arr));
    }
    const arr = Array.from(set);
    for(let i=arr.length-1;i>0;i--){ const j = Math.floor(Math.random()*(i+1)); [arr[i],arr[j]]=[arr[j],arr[i]]; }
    return arr.map(s=> ({ label: s, display: seqToDisplay(s.split(' ')) }) );
  }
}

function generateQuestion(level){
  const k = notesPerQuestion(level);
  const seq = [];
  for(let i=0;i<k;i++){ seq.push(NOTES[Math.floor(Math.random()*NOTES.length)].name); }
  const choices = createChoices(seq);
  return { seq, choices, answer: seqToLabel(seq) };
}

/* populate levels */
for(let i=1;i<=TOTAL_LEVELS;i++){
  const o = document.createElement('option'); o.value = i; o.textContent = 'Level ' + i + ' (' + notesPerQuestion(i) + ' โน้ต/ข้อ)';
  levelSelect.appendChild(o);
}
levelSelect.value = 1;

/* audio */
const AudioCtx = window.AudioContext || window.webkitAudioContext;
const ctx = new AudioCtx();
function playTone(freq,dur=0.42){
  const o = ctx.createOscillator(); const g = ctx.createGain();
  o.type='sine'; o.frequency.setValueAtTime(freq, ctx.currentTime);
  o.connect(g); g.connect(ctx.destination);
  g.gain.setValueAtTime(0, ctx.currentTime); g.gain.linearRampToValueAtTime(0.18, ctx.currentTime+0.01);
  o.start(); g.gain.exponentialRampToValueAtTime(0.001, ctx.currentTime + dur);
  setTimeout(()=> o.stop(), dur*1000 + 60);
}
function playSequence(freqs,interval=300){ freqs.forEach((f,i)=> setTimeout(()=> playTone(f,0.42), i*interval)); }
function playCorrect(seq){ playSequence(seq.map(n=>NOTES.find(x=>x.name===n).freq),200); setTimeout(()=>{ playTone(880,0.08); setTimeout(()=>playTone(1174,0.08),100); }, seq.length*220 + 40); }
function playWrong(){ playTone(220,0.18); }

/* runtime functions */
function renderCurrent(){
  renderSequence(state.current.seq);
  choicesArea.innerHTML = '';
  state.current.choices.forEach(ch=>{
    const d = document.createElement('div'); d.className='choice'; d.dataset.value = ch.label;
    d.innerHTML = `<div style="font-weight:600">${ch.display}</div>`;
    d.addEventListener('click', ()=> onChoice(ch.label, d));
    choicesArea.appendChild(d);
  });
  feedback.textContent = 'ข้อที่ ' + (state.qIndex+1) + ' — เลือกคำตอบ';
  scoreEl.textContent = state.score;
}

function onChoice(choiceLabel, el){
  if(!state.running) return;
  const correct = choiceLabel === state.current.answer;
  if(correct){
    el.classList.add('correct'); feedback.textContent = 'ถูกต้อง!'; playCorrect(state.current.seq); state.score++;
  } else {
    el.classList.add('wrong'); feedback.textContent = 'ผิด! คำตอบ: ' + seqToDisplay(state.current.answer.split(' ')); playWrong();
  }
  Array.from(choicesArea.children).forEach(c=> c.style.pointerEvents = 'none');

  if(state.mode === 'practice'){
    setTimeout(()=> {
      state.qIndex++;
      updateProgress();
      if(state.qIndex < QUESTIONS_PER_LEVEL){
        state.current = generateQuestion(state.level); renderCurrent();
      } else finishLevel();
    }, 800);
  } else if(state.mode === 'time'){
    setTimeout(()=> {
      state.current = generateQuestion(state.level); renderCurrent();
    }, 250);
  }
}

startBtn.addEventListener('click', ()=> startExercise());

function startExercise(){
  state.level = parseInt(levelSelect.value);
  state.mode = modeSelect.value;
  state.qIndex = 0; state.score = 0; state.running = true;
  if(state.mode === 'time'){ document.getElementById('mainCol').classList.add('time-theme'); staffCard.classList.add('time-theme'); }
  else { document.getElementById('mainCol').classList.remove('time-theme'); staffCard.classList.remove('time-theme'); }

  if(state.mode === 'practice'){
    state.current = generateQuestion(state.level); renderCurrent(); updateProgress(); timerEl.textContent='--';
  } else if(state.mode === 'time'){
    state.timeRemaining = 60; timerEl.textContent = formatTime(state.timeRemaining);
    state.current = generateQuestion(state.level); renderCurrent(); updateProgress();
    state.timeModeTimer && clearInterval(state.timeModeTimer);
    state.timeModeTimer = setInterval(()=> {
      state.timeRemaining--; timerEl.textContent = formatTime(state.timeRemaining); updateProgress();
      if(state.timeRemaining <= 0){ clearInterval(state.timeModeTimer); finishTimeChallenge(); }
    },1000);
  }
}

function formatTime(s){ const mm = Math.floor(s/60); const ss = s%60; return `${mm}:${ss.toString().padStart(2,'0')}`; }
function updateProgress(){ if(state.mode==='practice') progress.textContent = 'ด่าน: '+state.level+' | ข้อ: '+Math.min(state.qIndex+1,QUESTIONS_PER_LEVEL)+' / '+QUESTIONS_PER_LEVEL; else progress.textContent = 'Time Challenge — เวลา: '+formatTime(state.timeRemaining)+' | คะแนน: '+state.score; }
function finishLevel(){ state.running=false; feedback.textContent = `จบด่าน! คะแนน: ${state.score} / ${QUESTIONS_PER_LEVEL}`; timerEl.textContent='--'; }

function finishTimeChallenge(){
  state.running=false; feedback.textContent = `Time up! คะแนนที่ได้: ${state.score}`; timerEl.textContent='0:00';
  const rec = { student: state.student, score: state.score, level: state.level, date: new Date().toISOString() };
  const key = 'kimi_time_leaderboard';
  const arr = JSON.parse(localStorage.getItem(key) || '[]'); arr.push(rec); localStorage.setItem(key, JSON.stringify(arr)); renderLeaderboard();
}

/* play / answer / next */
playBtn.addEventListener('click', ()=> { if(!state.current) return; if(ctx.state==='suspended') ctx.resume(); const freqs = state.current.seq.map(n=>NOTES.find(x=>x.name===n).freq); playSequence(freqs,300); });
answerBtn.addEventListener('click', ()=> { if(!state.current) return; feedback.textContent = 'คำตอบ: ' + seqToDisplay(state.current.answer.split(' ')); });
nextBtn.addEventListener('click', ()=> { if(!state.running) return; if(state.mode==='practice'){ state.qIndex++; if(state.qIndex < QUESTIONS_PER_LEVEL){ state.current = generateQuestion(state.level); renderCurrent(); updateProgress(); } else finishLevel(); } });

/* landing / student info */
landingStart.addEventListener('click', ()=> {
  const n = landingName.value.trim(); const no = landingNo.value.trim(); const cls = landingClass.value.trim();
  if(!n){ alert('กรุณากรอกชื่อ / ชื่อกลุ่ม'); return; }
  state.student = { name: n, no: no, class: cls };
  stuName.value = state.student.name; stuNo.value = state.student.no; stuClass.value = state.student.class;
  modeSelect.value = landingMode.value;
  landingScreen.style.display='none'; document.getElementById('appRoot').setAttribute('aria-hidden','false');
  levelSelect.value = 1;
});

/* student storage & save */
saveStu.addEventListener('click', ()=> { state.student.name = stuName.value.trim(); state.student.no = stuNo.value.trim(); state.student.class = stuClass.value.trim(); localStorage.setItem('kimi_student', JSON.stringify(state.student)); alert('บันทึกข้อมูลนักเรียนแล้ว ✅'); });
clearStu.addEventListener('click', ()=> { stuName.value=''; stuNo.value=''; stuClass.value=''; state.student = {name:'',no:'',class:''}; localStorage.removeItem('kimi_student'); alert('ลบข้อมูลแล้ว'); });

saveScore.addEventListener('click', ()=> {
  const rec = { student: state.student, level: state.level, score: state.score, total: (state.mode==='practice'? QUESTIONS_PER_LEVEL : ''), mode: state.mode, date: new Date().toISOString() };
  const key = 'kimi_records_all';
  const arr = JSON.parse(localStorage.getItem(key) || '[]'); arr.push(rec); localStorage.setItem(key, JSON.stringify(arr)); alert('บันทึกคะแนนเรียบร้อย ✅');
});

/* export CSV with PIN */
exportCSV.addEventListener('click', ()=> { modalBackdrop.style.display='flex'; pinInput.value=''; pinInput.focus(); });
pinCancel.addEventListener('click', ()=> modalBackdrop.style.display='none');
pinOk.addEventListener('click', async ()=> {
  const pin = pinInput.value.trim(); if(pin !== TEACHER_PIN){ alert('รหัสไม่ถูกต้อง'); return; }
  modalBackdrop.style.display='none';
  const records = JSON.parse(localStorage.getItem('kimi_records_all') || '[]');
  const tboard = JSON.parse(localStorage.getItem('kimi_time_leaderboard') || '[]');
  const all = records.concat(tboard.map(r=> ({student:r.student, level:r.level||'', score:r.score, total:r.total||'', mode:r.mode||'time', date:r.date})));
  if(all.length === 0){ alert('ไม่มีข้อมูลให้ส่งออก'); return; }
  if(SHEETS_WEBHOOK_URL){
    try{
      const resp = await fetch(SHEETS_WEBHOOK_URL, { method:'POST', headers:{ 'Content-Type':'application/json' }, body: JSON.stringify({ records: all })});
      if(resp.ok) alert('ส่งข้อมูลไปยัง Google Sheets สำเร็จ'); else alert('ส่งไปยัง Google Sheets ไม่สำเร็จ (status ' + resp.status + ')');
    }catch(e){ console.error(e); alert('เกิดข้อผิดพลาดในการส่งข้อมูลไปยัง Google Sheets'); }
  }
  let csv = 'name,class,no,mode,level,score,total,date\n';
  all.forEach(r=>{ const n = r.student && r.student.name ? r.student.name.replace(/"/g,'""') : ''; const c = r.student && r.student.class ? r.student.class.replace(/"/g,'""') : ''; const no = r.student && r.student.no ? r.student.no.replace(/"/g,'""') : ''; csv += `"${n}","${c}","${no}","${r.mode||'practice'}","${r.level||''}",${r.score || 0},${r.total || ''},"${r.date}"\n`; });
  const blob = new Blob([csv], {type:'text/csv;charset=utf-8;'}); const url = URL.createObjectURL(blob); const a = document.createElement('a'); a.href = url; a.download = 'kimi_records_export.csv'; document.body.appendChild(a); a.click(); a.remove(); URL.revokeObjectURL(url);
  alert('ดาวน์โหลด CSV เรียบร้อย');
});

/* leaderboard */
function renderLeaderboard(){
  const arr = JSON.parse(localStorage.getItem('kimi_time_leaderboard') || '[]');
  if(arr.length === 0){ leaderboardEl.innerHTML = 'ยังไม่มีผลการแข่งขัน'; return; }
  const sorted = arr.slice().sort((a,b)=> b.score - a.score);
  const top = sorted.slice(0,10);
  leaderboardEl.innerHTML = top.map((r,i)=> `<div style="padding:6px;border-bottom:1px solid rgba(0,0,0,0.04)">${i+1}. ${r.student.name||'-'} (${r.student.class||'-'} ${r.student.no||''}) — ${r.score} pts — ${new Date(r.date).toLocaleString()}</div>`).join('');
}
renderLeaderboard();

/* init saved student */
document.addEventListener('DOMContentLoaded', ()=> {
  const saved = JSON.parse(localStorage.getItem('kimi_student') || 'null');
  if(saved){ landingName.value = saved.name || ''; landingNo.value = saved.no || ''; landingClass.value = saved.class || ''; stuName.value = saved.name || ''; stuNo.value = saved.no || ''; stuClass.value = saved.class || ''; state.student = saved; }
});
</script>

</body>
</html>
