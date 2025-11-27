<html....>
<html lang="th">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Kimi-wa-Melody — Final (Full)</title>
<link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600&display=swap" rel="stylesheet">
<style>
:root{--bg:#efe7d7;--card:#fff7ee;--accent:#7C5A3A;--muted:#765b44;--good:#2E8B57;--bad:#C03B3B}
*{box-sizing:border-box} body{margin:0;font-family:'Kanit',sans-serif;background:linear-gradient(135deg,#d4c5a9,#b8a58a)}
.app{max-width:1100px;margin:20px auto;padding:16px}
.card{background:var(--card);border-radius:14px;padding:14px;margin-bottom:12px;box-shadow:0 10px 30px rgba(0,0,0,.12)}
.header{display:flex;align-items:center;gap:12px}
.mascot{font-size:34px}
.controls{display:flex;gap:8px;flex-wrap:wrap}
.btn{padding:10px 12px;border-radius:8px;border:none;cursor:pointer;font-weight:700}
.btn-primary{background:var(--accent);color:#fff}
.btn-info{background:#7a96aa;color:#fff}
.btn-success{background:#5d7a52;color:#fff}
.small{color:var(--muted);font-size:13px}
.staff-card{background:#fff;padding:12px;border-radius:10px;box-shadow:inset 0 2px 8px rgba(0,0,0,.04)}
#staffSVG{width:100%;height:auto;display:block}
.choices{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:8px;margin-top:10px}
.choice{padding:12px;border-radius:8px;background:#fff;border:1px solid #eee;cursor:pointer;font-weight:700;text-align:center}
.choice.correct{background:var(--good);color:#fff} .choice.wrong{background:var(--bad);color:#fff}
.feedback{margin-top:10px;padding:10px;border-radius:8px;display:none}
.feedback.show{display:block}
.modal-backdrop{position:fixed;inset:0;background:rgba(0,0,0,.45);display:none;align-items:center;justify-content:center;z-index:80}
.modal{background:var(--card);padding:14px;border-radius:12px;min-width:300px}
.qr-img{width:220px;height:220px;border-radius:8px;display:block;margin:12px auto}
.fullscreen-btn{position:fixed;right:18px;bottom:18px;background:var(--accent);color:#fff;border-radius:50%;width:56px;height:56px;border:none;box-shadow:0 12px 30px rgba(0,0,0,.2);cursor:pointer}
.hidden{display:none}
</style>
</head>
<body>
<div class="app">
  <div class="card header">
    <div class="mascot">🐱</div>
    <div>
      <h2 style="margin:0">Kimi-wa-Melody</h2>
      <div class="small">ฝึกอ่านโน้ต — MelodyCat</div>
    </div>
    <div style="margin-left:auto" class="small">PIN ครู: <strong>Teacherversion5791</strong></div>
  </div>

  <!-- Landing -->
  <div id="landing" class="card">
    <div style="display:flex;gap:10px;align-items:center;justify-content:space-between">
      <div>
        <h3 style="margin:0">เริ่มต้น</h3>
        <div class="small">กรอกข้อมูลนักเรียนก่อนเริ่ม</div>
      </div>
    </div>

    <div style="margin-top:10px;display:flex;gap:10px;flex-wrap:wrap">
      <input id="name" placeholder="ชื่อ-สกุล / ชื่อกลุ่ม" style="flex:1;padding:10px;border-radius:8px;border:1px solid #ddd">
      <input id="no" placeholder="เลขที่" style="width:110px;padding:10px;border-radius:8px;border:1px solid #ddd">
      <input id="cls" placeholder="ห้อง" style="width:140px;padding:10px;border-radius:8px;border:1px solid #ddd">
      <select id="mode" style="width:220px;padding:10px;border-radius:8px;border:1px solid #ddd">
        <option value="practice">Practice</option>
        <option value="time">Time Challenge (60s)</option>
      </select>
    </div>

    <div style="margin-top:10px" class="controls">
      <button class="btn btn-primary" id="start">เริ่มเกม</button>
      <button class="btn btn-info" id="showLB">ดูกระดานคะแนน</button>
      <button class="btn btn-success" id="showExport">ส่งออก (ครู)</button>
      <button class="btn" id="zipBtn">สร้าง ZIP (คำสั่ง)</button>
      <button class="btn" id="qrRoomBtn">แชร์ห้อง (QR)</button>
    </div>
  </div>

  <!-- Level panel -->
  <div id="levels" class="card hidden">
    <h3>เลือกด่าน</h3>
    <div class="small">1–7: 1 โน้ต · 8–14: 2 โน้ต · 15–20: 3 โน้ต</div>
    <div id="levelGrid" style="margin-top:8px;display:grid;grid-template-columns:repeat(auto-fit,minmax(80px,1fr));gap:8px"></div>
    <div style="margin-top:10px"><button class="btn" id="backToLanding">กลับ</button></div>
  </div>

  <!-- Game panel -->
  <div id="game" class="card hidden">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <div><strong>ด่าน</strong> <span id="levelLabel">1</span> · <strong>ข้อ</strong> <span id="qLabel">1</span>/10</div>
      <div><strong>คะแนน</strong> <span id="scoreLabel">0</span></div>
      <div id="timerWrap" class="small hidden">เวลา: <span id="timerLabel">60</span>s</div>
    </div>

    <div style="margin-top:10px" class="staff-card">
      <svg id="staffSVG" viewBox="0 0 900 300" xmlns="http://www.w3.org/2000/svg" aria-label="Staff"></svg>
    </div>

    <div style="margin-top:8px" class="controls">
      <button class="btn btn-info" id="playBtn">🔊 ฟัง</button>
      <button class="btn btn-primary" id="showAnsBtn">ดูคำตอบ</button>
      <button class="btn btn-success hidden" id="nextBtn">ถัดไป</button>
      <button class="btn" id="fullscreenToggle">Full</button>
    </div>

    <div id="choices" class="choices"></div>
    <div id="feedback" class="feedback"></div>

    <div style="margin-top:8px" class="controls">
      <button class="btn btn-success" id="saveBtn">บันทึกคะแนน</button>
      <button class="btn" id="toLevels">กลับ</button>
    </div>
  </div>

  <!-- Leaderboard -->
  <div id="leaderboard" class="card hidden">
    <h3>กระดานคะแนน (Time Challenge)</h3>
    <div id="lbList" style="max-height:320px;overflow:auto"></div>
    <div style="margin-top:8px"><button class="btn" id="lbBack">กลับ</button></div>
  </div>

  <!-- PIN modal -->
  <div id="pinModal" class="modal-backdrop">
    <div class="modal">
      <h4>กรอกรหัส PIN ครู</h4>
      <input id="pin" type="password" class="input" placeholder="PIN ครู" style="width:100%;padding:8px;border-radius:8px;border:1px solid #ddd">
      <div style="margin-top:8px" class="controls">
        <button class="btn btn-primary" id="pinOk">ยืนยัน</button>
        <button class="btn" id="pinCancel">ยกเลิก</button>
      </div>
      <div id="pinErr" style="color:var(--bad);display:none;margin-top:8px">รหัสไม่ถูกต้อง</div>
    </div>
  </div>

  <!-- QR modal -->
  <div id="qrModal" class="modal-backdrop">
    <div class="modal" style="text-align:center">
      <h4>แชร์ห้อง</h4>
      <div id="roomLink" style="word-break:break-all"></div>
      <img id="qrImg" class="qr-img" alt="QR code"/>
      <div style="margin-top:8px" class="controls">
        <button class="btn btn-primary" id="closeQr">ปิด</button>
      </div>
    </div>
  </div>

</div>

<button id="fsBtn" class="fullscreen-btn" title="Fullscreen">⤢</button>

<script>
/* ================== CONFIG ================== */
/* If you want to use your image as clef: set USE_CLEF_IMAGE = true and put a URL in CLEF_IMAGE_URL.
   CLEF_IMAGE_URL can be a hosted URL (e.g., GitHub raw URL, S3) or a data URI (base64).
   If USE_CLEF_IMAGE=false, the embedded SVG path CLEF_PATH will be used. */
const USE_CLEF_IMAGE = true;
const CLEF_IMAGE_URL = ""; // <-- ใส่ URL ของภาพที่คุณอัปโหลดไว้ เช่น "https://your.site/treble.png" หรือ data:image/png;base64,...
const SHEETS_WEBHOOK_URL = ""; // <-- ใส่ URL ที่ได้จากการ deploy Google Apps Script (ส่วน B) ถ้าต้องการเชื่อม

const TEACHER_PIN = "Teacherversion5791";
const TOTAL_LEVELS = 20;
const QUESTIONS_PER_LEVEL = 10;

/* Notes & staff config */
const NOTES = ['C','D','E','F','G','A','B'];
const NOTE_TH = {C:'โด',D:'เร',E:'มี',F:'ฟา',G:'ซอล',A:'ลา',B:'ที'};
const NOTE_FREQ = {C:261.63,D:293.66,E:329.63,F:349.23,G:392.00,A:440.00,B:493.88};

const STAFF = { left:110, right:760, bottomY:170, gap:20, strokeWidth:4 };
const NOTE_CFG = { startX:360, stepX:48, rx:16, ry:12, stemW:3.8, stemH:60 };

/* Clef fallback path (validated high-fidelity path). Kept for vector fallback. */
const CLEF_PATH = `M115.9,19.6c-3.1,1.6-6.8,4.8-9.9,8.6c-6.0,7.6-8.5,16.8-6.3,24.0c2.1,6.9,8.5,11.8,16.3,13.4c5.8,1.1,11.6,0.7,16.3-1.3
c8.6-3.6,13.8-11.3,14.9-20.3c1.2-9.9-2.9-20.6-12.2-30.9c-2.9-3.0-6.0-5.6-9.3-7.7c-4.1-2.6-8.0-4.6-11.8-6.1z
M111.4,46.8c2.6-0.9,5.9-0.6,9.4,0.8c6.1,2.4,9.6,6.7,10.0,11.0c0.6,6.7-3.7,13.3-11.8,17.4c-4.5,2.4-9.6,3.4-14.8,2.9
c-6.2-0.6-11.3-3.7-14.6-8.4c-3.0-4.2-3.8-9.5-2.2-14.1c1.1-3.1,3.5-6.0,6.6-8.4C98.1,50.9,104.6,48.3,111.4,46.8z
M121.0,95.3c-0.3,1.3-0.7,2.5-1.3,3.7c-2.8,6.4-8.9,11.6-17.6,15.0c-3.9,1.5-8.0,2.5-12.0,3.2c-6.6,1.0-12.2,2.6-16.1,4.6
c-6.2,3.2-9.6,7.6-9.7,12.9c-0.2,6.2,4.0,11.8,12.4,16.5c7.8,4.3,17.9,6.5,28.7,6.5c9.6,0,19.1-1.9,26.5-6.4
c6.2-3.8,9.7-8.5,10.6-13.2c0.9-4.8-0.6-9.5-4.1-13.4c-3.8-4.2-9.9-6.8-18.0-7.9c-1.9-0.2-4.0-0.2-6.1,0.0c-4.3,0.4-7.9,1.3-10.6,2.7
c-2.6,1.3-4.5,3.0-5.6,5.1c-1.2,2.3-1.5,5.0-0.6,7.9c1.3,4.1,5.0,7.6,10.8,10.8c5.6,3.0,12.0,4.5,18.6,4.5c5.6,0,11.2-0.9,15.7-2.6
c3.5-1.3,6.6-3.0,9.2-5.1c2.5-2.0,4.6-4.4,6.1-7.1c1.5-2.8,2.3-5.7,2.4-8.6c0.1-3.3-0.9-6.6-2.9-9.9c-3.3-5.3-9.5-9.3-18.4-11.6
c-3.9-1.0-8.3-1.8-13.1-2.2c-0.6-0.0-1.1-0.0-1.7-0.0C123.3,94.9,122.1,95.1,121.0,95.3z`;

/* Fine-tune clef position when using image (pixel perfect): adjust THESE values */
let CLEF_IMAGE_TRANSFORM = { x: 48, y: -60, scale: 0.95 }; // change to fit your image

/* =============== State =============== */
let appState = {
  student: null,
  mode: 'practice',
  level: 1,
  qIndex: 0,
  score: 0,
  current: null,
  answered: false,
  timer: null,
  timeLeft: 60
};

/* =============== Audio helpers =============== */
let audioCtx = null;
function ensureAudio(){ if(!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)(); }
function playTone(freq, dur=0.45){
  ensureAudio();
  const o = audioCtx.createOscillator();
  const g = audioCtx.createGain();
  o.type='sine'; o.frequency.value=freq;
  o.connect(g); g.connect(audioCtx.destination);
  g.gain.setValueAtTime(0.001,audioCtx.currentTime); g.gain.exponentialRampToValueAtTime(0.18,audioCtx.currentTime+0.01);
  o.start(); g.gain.exponentialRampToValueAtTime(0.001,audioCtx.currentTime+dur);
  setTimeout(()=>o.stop(), (dur+0.05)*1000);
}
function playSeq(notes, interval=380){ notes.forEach((n,i)=> setTimeout(()=>playTone(NOTE_FREQ[n]), i*interval)); }
function playCorrect(){ playSeq(['C','E','G'],180); }
function playWrong(){ playSeq(['G','F','E'],160); }

/* =============== SVG draw =============== */
const svgNS = 'http://www.w3.org/2000/svg';
function drawStaff(){
  const svg = document.getElementById('staffSVG');
  svg.innerHTML = '';
  // draw 5 lines
  for(let i=0;i<5;i++){
    const y = STAFF.bottomY - i*STAFF.gap;
    const L = document.createElementNS(svgNS,'line');
    L.setAttribute('x1', STAFF.left); L.setAttribute('y1', y);
    L.setAttribute('x2', STAFF.right); L.setAttribute('y2', y);
    L.setAttribute('stroke','#000'); L.setAttribute('stroke-width', STAFF.strokeWidth);
    L.setAttribute('stroke-linecap','round');
    svg.appendChild(L);
  }

  // clef: either image or path
  if(USE_CLEF_IMAGE && CLEF_IMAGE_URL){
    const g = document.createElementNS(svgNS,'g');
    const img = document.createElementNS(svgNS,'image');
    img.setAttributeNS('http://www.w3.org/1999/xlink','href', CLEF_IMAGE_URL);
    // size and position: you may adjust these multipliers for pixel-perfect fit
    const width = 220; const height = 320;
    img.setAttribute('width', width); img.setAttribute('height', height);
    // position - tuned with CLEF_IMAGE_TRANSFORM
    const tx = CLEF_IMAGE_TRANSFORM.x; const ty = CLEF_IMAGE_TRANSFORM.y; const s = CLEF_IMAGE_TRANSFORM.scale;
    // place image's top-left so that it visually overlays staff near left
    g.setAttribute('transform', `translate(${tx}, ${ty}) scale(${s})`);
    g.appendChild(img);
    svg.appendChild(g);
  } else {
    const g = document.createElementNS(svgNS,'g');
    // default transform chosen to circle line 2 (G line)
    g.setAttribute('transform', `translate(52, -68) scale(0.21)`);
    const p = document.createElementNS(svgNS,'path');
    p.setAttribute('d', CLEF_PATH); p.setAttribute('fill','#000');
    g.appendChild(p); svg.appendChild(g);
  }

  // store bottomY and gap for notes
  svg.dataset.bottomY = STAFF.bottomY;
  svg.dataset.gap = STAFF.gap;
}

function noteY(n){
  const svg = document.getElementById('staffSVG');
  const bottomY = parseFloat(svg.dataset.bottomY || STAFF.bottomY);
  const gap = parseFloat(svg.dataset.gap || STAFF.gap);
  const map = { C: bottomY + gap, D: bottomY + gap/2, E: bottomY, F: bottomY - gap/2, G: bottomY - gap, A: bottomY - gap*1.5, B: bottomY - gap*2 };
  return map[n];
}

function renderSeq(seq){
  const svg = document.getElementById('staffSVG');
  // preserve staff lines and clef (assume first children are lines & clef)
  const preserved = Array.from(svg.childNodes).filter(n => n.tagName === 'line' || (n.tagName==='g' && n.querySelector('path') || n.tagName==='g' && n.querySelector('image')));
  svg.innerHTML = '';
  preserved.forEach(n => svg.appendChild(n.cloneNode(true)));
  // draw notes
  seq.forEach((nt,idx)=>{
    const x = NOTE_CFG.startX + idx*NOTE_CFG.stepX;
    const y = noteY(nt);
    if(nt === 'C'){
      const led = document.createElementNS(svgNS,'line');
      led.setAttribute('x1', x - 22); led.setAttribute('y1', y); led.setAttribute('x2', x + 22); led.setAttribute('y2', y);
      led.setAttribute('stroke','#000'); led.setAttribute('stroke-width','3'); led.setAttribute('stroke-linecap','round');
      svg.appendChild(led);
    }
    const head = document.createElementNS(svgNS,'ellipse');
    head.setAttribute('cx', x); head.setAttribute('cy', y); head.setAttribute('rx', NOTE_CFG.rx); head.setAttribute('ry', NOTE_CFG.ry);
    head.setAttribute('fill','#000'); head.setAttribute('transform', `rotate(-12 ${x} ${y})`);
    svg.appendChild(head);

    const stem = document.createElementNS(svgNS,'rect');
    stem.setAttribute('x', x + NOTE_CFG.rx - 2); stem.setAttribute('y', y - NOTE_CFG.stemH);
    stem.setAttribute('width', NOTE_CFG.stemW); stem.setAttribute('height', NOTE_CFG.stemH); stem.setAttribute('fill','#000');
    svg.appendChild(stem);
  });
}

/* =============== Questions & choices =============== */
function notesPerQ(l){ if(l<=7) return 1; if(l<=14) return 2; return 3; }
function randSeq(k){ return Array.from({length:k},()=> NOTES[Math.floor(Math.random()*NOTES.length)]); }
function seqLabel(s){ return s.map(n=> n + '(' + (NOTE_TH[n]||'') + ')' ).join(' '); }

function makeChoices(correct){
  const k = correct.length;
  if(k===1){
    return shuffle(NOTES.map(n=>[n])); // each choice is array of length 1
  } else {
    const set = new Set([JSON.stringify(correct)]);
    const choices = [correct];
    while(choices.length<4){
      const c = randSeq(k);
      const s = JSON.stringify(c);
      if(!set.has(s)){ set.add(s); choices.push(c); }
    }
    return shuffle(choices);
  }
}
function shuffle(a){ const arr=a.slice(); for(let i=arr.length-1;i>0;i--){ const j=Math.floor(Math.random()*(i+1)); [arr[i],arr[j]]=[arr[j],arr[i]] } return arr; }

function generateQuestion(){
  appState.answered = false;
  const k = notesPerQ(appState.level);
  const seq = randSeq(k);
  const choices = makeChoices(seq);
  appState.current = { seq, choices, answer: JSON.stringify(seq) };
  renderSeq(seq);
  renderChoices(choices);
  document.getElementById('qLabel').textContent = appState.qIndex + 1;
  document.getElementById('feedback').className = 'feedback';
  document.getElementById('nextBtn').style.display = 'none';
}

function renderChoices(choices){
  const ctn = document.getElementById('choices'); ctn.innerHTML = '';
  choices.forEach(ch=>{
    const b = document.createElement('button'); b.className='choice'; b.textContent = seqLabel(ch);
    b.onclick = ()=> checkAnswer(ch,b); ctn.appendChild(b);
  });
}

function checkAnswer(choice, btn){
  if(appState.answered) return;
  appState.answered = true;
  const ok = JSON.stringify(choice) === appState.current.answer;
  if(ok){ btn.classList.add('correct'); document.getElementById('feedback').textContent='ถูกต้อง!'; document.getElementById('feedback').className='feedback show feedback correct'; playCorrect(); appState.score++; }
  else { btn.classList.add('wrong'); document.getElementById('feedback').textContent = 'ผิด! คำตอบ: ' + seqLabel(JSON.parse(appState.current.answer)); document.getElementById('feedback').className='feedback show feedback incorrect'; playWrong();
    Array.from(document.querySelectorAll('.choice')).forEach(b=>{ if(b.textContent === seqLabel(JSON.parse(appState.current.answer))) b.classList.add('correct'); });
  }
  Array.from(document.querySelectorAll('.choice')).forEach(b=>b.disabled=true);
  document.getElementById('scoreLabel').textContent = appState.score;
  document.getElementById('nextBtn').style.display = 'inline-block';
}

/* =============== Flow =============== */
function startPractice(level){
  appState.mode='practice'; appState.level=level; appState.qIndex=0; appState.score=0; appState.answered=false;
  document.getElementById('landing').style.display='none'; document.getElementById('levels').style.display='none'; document.getElementById('game').style.display='block';
  document.getElementById('levelLabel').textContent = level; document.getElementById('timerWrap').classList.add('hidden');
  drawStaff(); generateQuestion();
}
function startTime(){
  appState.mode='time'; appState.level=1; appState.qIndex=0; appState.score=0; appState.answered=false; appState.timeLeft=60;
  document.getElementById('landing').style.display='none'; document.getElementById('game').style.display='block';
  document.getElementById('levelLabel').textContent='Time Challenge'; document.getElementById('timerWrap').classList.remove('hidden');
  drawStaff(); generateQuestion(); startTimer(); playSeq(appState.current.seq);
}
function nextQ(){
  appState.answered=false; appState.qIndex++;
  if(appState.mode==='practice'){
    if(appState.qIndex >= QUESTIONS_PER_LEVEL){ endLevel(); return; }
    generateQuestion();
  } else {
    generateQuestion(); playSeq(appState.current.seq);
  }
}
function endLevel(){
  document.getElementById('feedback').textContent = `จบด่าน ${appState.level} คะแนน ${appState.score}`; document.getElementById('feedback').className='feedback show feedback correct';
  document.getElementById('nextBtn').style.display='none';
  // mark done
  const done = JSON.parse(localStorage.getItem('kimi_done')||'[]'); if(!done.includes(appState.level)){ done.push(appState.level); localStorage.setItem('kimi_done', JSON.stringify(done)); }
}

/* =============== Timer =============== */
function startTimer(){
  stopTimer(); appState.timer = setInterval(()=>{ appState.timeLeft--; document.getElementById('timerLabel').textContent = appState.timeLeft; if(appState.timeLeft<=0){ stopTimer(); finishTime(); } },1000);
}
function stopTimer(){ if(appState.timer){ clearInterval(appState.timer); appState.timer=null; } }
function finishTime(){
  document.getElementById('feedback').textContent = `หมดเวลา! คะแนน ${appState.score}`; document.getElementById('feedback').className='feedback show feedback correct';
  saveTimeLeader();
  Array.from(document.querySelectorAll('.choice')).forEach(b=>b.disabled=true);
  document.getElementById('nextBtn').style.display='none';
}

/* =============== Storage & leaderboard =============== */
function saveTimeLeader(){
  const key='kimi_time_lb'; const lb = JSON.parse(localStorage.getItem(key)||'[]');
  lb.push({name: appState.student.name, class: appState.student.class, no: appState.student.no, score: appState.score, total: appState.qIndex+1, date: new Date().toLocaleString()});
  lb.sort((a,b)=> b.score - a.score);
  localStorage.setItem(key, JSON.stringify(lb.slice(0,50)));
}
function renderLB(){
  const lb = JSON.parse(localStorage.getItem('kimi_time_lb')||'[]'); const el=document.getElementById('lbList');
  if(lb.length===0){ el.innerHTML='<div class="small">ยังไม่มีคะแนน</div>'; return; }
  el.innerHTML = lb.slice(0,20).map((r,i)=> `<div style="padding:6px;border-bottom:1px solid #eee">${i+1}. ${r.name} (${r.class} ${r.no}) — ${r.score}/${r.total} — ${r.date}</div>`).join('');
}

/* =============== Save / Export =============== */
function saveRecordLocal(){
  const key='kimi_records_all'; const arr = JSON.parse(localStorage.getItem(key)||'[]');
  arr.push({student_name: appState.student.name, class_room: appState.student.class, student_no: appState.student.no, mode: appState.mode, level: appState.level, score: appState.score, total: appState.qIndex+1, timestamp: new Date().toISOString()});
  localStorage.setItem(key, JSON.stringify(arr)); alert('บันทึกคะแนนเรียบร้อย');
}

/* Export CSV local and optionally POST to Sheets webhook */
async function exportCSV(){
  const recs = JSON.parse(localStorage.getItem('kimi_records_all')||'[]');
  if(recs.length===0){ alert('ไม่มีข้อมูลให้ส่งออก'); return; }
  let csv = 'name,class,no,mode,level,score,total,date\n';
  recs.forEach(r => { csv += `"${r.student_name}","${r.class_room}","${r.student_no}","${r.mode}",${r.level},${r.score},${r.total},"${new Date(r.timestamp).toLocaleString('th-TH')}"\n`; });
  const blob = new Blob([csv], {type:'text/csv;charset=utf-8;'}); const a = document.createElement('a'); a.href = URL.createObjectURL(blob);
  a.download = `kimi_records_${new Date().toISOString().split('T')[0]}.csv`; a.click(); alert('ดาวน์โหลด CSV เรียบร้อย');
  // optional: send to Google Sheets webhook
  if(SHEETS_WEBHOOK_URL){
    try{
      const resp = await fetch(SHEETS_WEBHOOK_URL, {method:'POST', headers:{ 'Content-Type':'application/json' }, body: JSON.stringify({records: recs})});
      if(resp.ok) alert('ส่งข้อมูลไป Google Sheets เรียบร้อย');
      else alert('ส่งไป Google Sheets ไม่สำเร็จ: ' + resp.status);
    }catch(e){ console.error(e); alert('ส่งไป Google Sheets ขัดข้อง'); }
  }
}

/* =============== Fullscreen & QR =============== */
const fsBtn = document.getElementById('fsBtn'); fsBtn.addEventListener('click', ()=> {
  if(!document.fullscreenElement) document.documentElement.requestFullscreen(); else document.exitFullscreen();
});

function openQR(roomId){
  const link = `${location.origin}${location.pathname}?room=${encodeURIComponent(roomId)}`;
  document.getElementById('roomLink').textContent = link;
  // use Google Chart API for QR image (simple & reliable). If you need offline QR, we'll add a JS QR lib.
  const qrSrc = `https://chart.googleapis.com/chart?cht=qr&chs=300x300&chl=${encodeURIComponent(link)}`;
  document.getElementById('qrImg').src = qrSrc;
  document.getElementById('qrModal').style.display = 'flex';
}

/* =============== UI wiring =============== */
document.getElementById('start').addEventListener('click', ()=> {
  const name = document.getElementById('name').value.trim(); const no=document.getElementById('no').value.trim(); const cls=document.getElementById('cls').value.trim(); const mode=document.getElementById('mode').value;
  if(!name||!no||!cls){ alert('กรุณากรอกข้อมูลให้ครบ'); return; }
  appState.student = {name, no, class:cls};
  appState.mode = mode;
  localStorage.setItem('kimi_student', JSON.stringify(appState.student));
  if(mode==='time'){ startTime(); } else { // show levels
    document.getElementById('landing').style.display='none'; document.getElementById('levels').style.display='block'; renderLevels();
  }
});
function renderLevels(){ const ctn=document.getElementById('levelGrid'); ctn.innerHTML=''; const done = JSON.parse(localStorage.getItem('kimi_done')||'[]'); for(let i=1;i<=TOTAL_LEVELS;i++){ const b=document.createElement('button'); b.className='btn level-btn'; b.textContent='ด่าน '+i; if(done.includes(i)){ b.style.background='var(--good)'; b.style.color='#fff'; } (function(li){ b.addEventListener('click', ()=> startPractice(li)); })(i); ctn.appendChild(b);} }
document.getElementById('backToLanding').addEventListener('click', ()=>{ document.getElementById('levels').style.display='none'; document.getElementById('landing').style.display='block'; });
document.getElementById('toLevels').addEventListener('click', ()=>{ stopTimer(); document.getElementById('game').style.display='none'; document.getElementById('levels').style.display='block'; renderLevels(); });
document.getElementById('showLB').addEventListener('click', ()=>{ renderLB(); document.getElementById('landing').style.display='none'; document.getElementById('leaderboard').style.display='block'; });
document.getElementById('lbBack').addEventListener('click', ()=>{ document.getElementById('leaderboard').style.display='none'; document.getElementById('landing').style.display='block'; });
document.getElementById('playBtn').addEventListener('click', ()=>{ if(appState.current) playSeq(appState.current.seq); });
document.getElementById('showAnsBtn').addEventListener('click', ()=>{ if(!appState.current) return; document.getElementById('feedback').textContent='คำตอบ: '+ seqLabel(JSON.parse(appState.current.answer)); document.getElementById('feedback').className='feedback show'; Array.from(document.querySelectorAll('.choice')).forEach(b=>{ if(b.textContent===seqLabel(JSON.parse(appState.current.answer))) b.classList.add('correct'); b.disabled=true;}); document.getElementById('nextBtn').style.display='inline-block'; });
document.getElementById('nextBtn').addEventListener('click', ()=> nextQ());
document.getElementById('saveBtn').addEventListener('click', ()=> saveRecordLocal());
document.getElementById('showExport').addEventListener('click', ()=> { document.getElementById('pinModal').style.display='flex'; });
document.getElementById('pinCancel').addEventListener('click', ()=> { document.getElementById('pinModal').style.display='none'; document.getElementById('pinErr').style.display='none'; });
document.getElementById('pinOk').addEventListener('click', async ()=> { const val=document.getElementById('pin').value; if(val===TEACHER_PIN){ document.getElementById('pinModal').style.display='none'; await exportCSV(); } else { document.getElementById('pinErr').style.display='block'; } });
document.getElementById('qrRoomBtn').addEventListener('click', ()=> { const roomId = `${appState.student?appState.student.name:'guest'}_${Date.now()}`; openQR(roomId); });
document.getElementById('closeQr').addEventListener('click', ()=> { document.getElementById('qrModal').style.display='none'; });
document.getElementById('zipBtn').addEventListener('click', ()=> { alert('คำสั่งสร้าง ZIP: เปิด terminal ในโฟลเดอร์โปรเจกต์ แล้วรัน:\nzip -r kimi-wa-melody.zip index.html assets/ (ถ้ามี)\nหรือใช้ GUI zip ในเครื่องของคุณ'); });

/* =============== Helper: restore student & init =============== */
(function init(){
  const s = JSON.parse(localStorage.getItem('kimi_student')||'null'); if(s){ document.getElementById('name').value = s.name; document.getElementById('no').value = s.no; document.getElementById('cls').value = s.class; appState.student=s; }
  drawStaff();
})();

/* =============== Google Sheets webhook helper (optional) =============== */
/* If you set SHEETS_WEBHOOK_URL to an Apps Script WebApp URL, exportCSV() will POST JSON there.
   See section B for the exact Apps Script code and deploy steps. */

</script>
</body>
</html>
