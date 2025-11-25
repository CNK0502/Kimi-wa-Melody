<html....>
<html lang="th">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Music Note Reading Game — เกมอ่านโน้ต</title>
  <style>
    /* --------------------------
       Base & Layout
       -------------------------- */
    :root{
      --radius:14px;
      --card-pad:18px;
      --font: "Noto Sans", "Inter", sans-serif;
      --soft-shadow: 0 6px 18px rgba(17,17,17,0.06);
    }
    html,body{margin:0;height:100%;font-family:var(--font);background:#fff8fb;color:#222}
    .app {max-width:1100px;margin:24px auto;padding:20px;}
    header{display:flex;align-items:center;justify-content:space-between;gap:12px}
    h1{margin:0;font-size:20px}
    nav{display:flex;gap:8px;flex-wrap:wrap}
    button, .btn {cursor:pointer;border:0;border-radius:10px;padding:10px 14px;font-weight:600}
    .btn {background:#fff;color:#333;box-shadow:var(--soft-shadow);}

    /* --------------------------
       Pages (sections) different pastel themes
       -------------------------- */
    .page {display:none;padding:20px;border-radius:16px;box-shadow:var(--soft-shadow);margin-top:18px}
    .page.active{display:block}

    /* Home (pink pastel) */
    #home{background: linear-gradient(180deg,#fff0f7,#ffeef6);border:1px solid rgba(255,123,176,0.08)}
    /* Practice (blue pastel) */
    #practice{background: linear-gradient(180deg,#f0fbff,#e6f9ff);border:1px solid rgba(58,166,208,0.06)}
    /* Time (mint pastel) */
    #time{background: linear-gradient(180deg,#f0fff7,#e8fff4);border:1px solid rgba(0,159,128,0.06)}
    /* Level (lavender) */
    #level{background: linear-gradient(180deg,#f6f2ff,#efe9ff);border:1px solid rgba(106,90,205,0.06)}
    /* Matching (yellow/peach) */
    #matching{background: linear-gradient(180deg,#fff9ec,#fff3e6);border:1px solid rgba(210,139,0,0.06)}
    /* Ranking (gradient) */
    #ranking{background: linear-gradient(135deg,#fff4ff,#f3fff9);border:1px solid rgba(150,110,180,0.05)}

    /* --------------------------
       Staff & Note area
       -------------------------- */
    .game-area{display:flex;gap:20px;align-items:flex-start;flex-wrap:wrap}
    .left-col{flex:1;min-width:280px}
    .right-col{width:320px}
    .card{background:#fff;padding:var(--card-pad);border-radius:12px;box-shadow:var(--soft-shadow)}
    .score{font-size:18px;font-weight:700;margin-bottom:8px}
    .controls{display:flex;gap:8px;flex-wrap:wrap;margin-top:8px}
    .note-buttons{display:flex;flex-wrap:wrap;gap:8px;margin-top:12px}
    .note-buttons button{flex:1 1 30%;padding:10px;border-radius:12px;background:rgba(255,255,255,0.9);box-shadow:0 4px 10px rgba(0,0,0,0.05);}

    /* --------------------------
       Matching cards
       -------------------------- */
    .match-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:12px}
    .match-card{background:#fff;padding:12px;border-radius:10px;text-align:center;user-select:none;cursor:pointer;box-shadow:var(--soft-shadow)}
    .match-card.matched{opacity:0.45;transform:scale(0.98)}

    /* --------------------------
       Small UI
       -------------------------- */
    .meta{font-size:13px;color:#555}
    .timer-bar{height:12px;background:rgba(0,0,0,0.06);border-radius:999px;overflow:hidden;margin-top:8px}
    .timer-fill{height:100%;width:0%;background:linear-gradient(90deg,#ffd58a,#ffd2b0)}

    /* responsive */
    @media (max-width:900px){
      .right-col{width:100%}
      .game-area{flex-direction:column}
    }

    /* prettier buttons for navigation */
    nav button{padding:10px 12px;background:#fff;border-radius:10px;box-shadow:var(--soft-shadow)}
    .primary{background:#ff7bb0;color:#fff}
  </style>
</head>
<body>
  <div class="app">
    <header>
      <h1>🎵 เกมอ่านโน้ต — Music Note Reading Game (โด-เร-มี)</h1>
      <nav>
        <button onclick="showPage('home')">Home</button>
        <button onclick="showPage('practice')">Practice</button>
        <button onclick="showPage('time')">Time Challenge</button>
        <button onclick="showPage('level')">Level Mode</button>
        <button onclick="showPage('matching')">Matching Mode</button>
        <button onclick="showPage('ranking')">Ranking</button>
      </nav>
    </header>

    <!-- ===========================
         HOME
         =========================== -->
    <section id="home" class="page active">
      <div style="display:flex;gap:18px;align-items:center;flex-wrap:wrap">
        <div style="flex:1" class="card">
          <h2 style="margin-top:0;color:#ff4f91">ยินดีต้อนรับ</h2>
          <p class="meta">เกมนี้สอนการอ่านโน้ตในคีย์ Treble Clef (ช่วง E4–F5) พร้อมคำอ่านภาษาไทย: C=โด, D=เร, E=มี, F=ฟา, G=ซอล, A=ลา, B=ที</p>
          <ul>
            <li>Practice: ฝึกอ่านทีละโน้ต</li>
            <li>Time Challenge: ท้าทายเวลา 60 วินาที</li>
            <li>Level Mode: ผ่านแต่ละด่าน</li>
            <li>Matching Mode: จับคู่โน้ตกับชื่

าย</li>
          </ul>
          <div style="margin-top:12px">
            <input id="playerName" placeholder="ใส่ชื่อสำหรับ Leaderboard (เช่น: นุ่น)" style="padding:8px;border-radius:8px;border:1px solid #eee;width:60%" />
            <button class="btn" onclick="setPlayerName()">บันทึกชื่อ</button>
          </div>
        </div>

        <div style="width:300px;" class="card">
          <h3 style="margin:0;color:#ff7bb0">เคล็ดลับ</h3>
          <p class="meta">แตะหรือคลิกบนโน้ตเพื่อฟังเสียง — ใช้สายตาจำตำแหน่งบน staff แล้วตอบเป็นตัวอักษร (C..B) หรือคำไทย (โด..ที)</p>
          <div style="margin-top:10px">
            <button class="btn primary" onclick="showPage('practice')">เริ่มฝึกเดี๋ยวนี้</button>
          </div>
        </div>
      </div>
    </section>

    <!-- ===========================
         PRACTICE PAGE (blue pastel)
         =========================== -->
    <section id="practice" class="page">
      <div class="game-area">
        <div class="left-col card">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div>
              <div class="score">Practice Mode</div>
              <div class="meta">โหมดฝึก — ไม่จำกัดเวลาตอบ</div>
            </div>
            <div id="practice-score" class="meta">คะแนน: 0</div>
          </div>

          <!-- Staff -->
          <div id="practice-staff" style="margin-top:14px"></div>

          <div class="note-buttons" id="practice-buttons" style="margin-top:12px"></div>

          <div style="margin-top:10px" class="controls">
            <button class="btn" onclick="practiceNext()">ถัดไป</button>
            <button class="btn" onclick="practiceClear()">รีเซ็ตคะแนน</button>
          </div>
        </div>

        <div class="right-col">
          <div class="card">
            <h4 style="margin:0">คำตอบ</h4>
            <div id="practice-feedback" style="margin-top:8px" class="meta">รอคำถาม...</div>
            <div style="margin-top:10px">
              <button class="btn" onclick="playCurrentNote()">ฟังอีกครั้ง</button>
            </div>
          </div>

          <div class="card" style="margin-top:12px">
            <h4 style="margin:0">คำอธิบายสั้น</h4>
            <p class="meta">โน้ตจะขึ้นบน staff เป็น SVG — แตะชื่อโน้ตเพื่อเลือกคำตอบ</p>
          </div>
        </div>
      </div>
    </section>

    <!-- ===========================
         TIME CHALLENGE (mint pastel)
         =========================== -->
    <section id="time" class="page">
      <div class="game-area">
        <div class="left-col card">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div>
              <div class="score">Time Challenge</div>
              <div class="meta">ท้าทายเวลา 60 วินาที</div>
            </div>
            <div id="time-score" class="meta">คะแนน: 0</div>
          </div>

          <div id="time-staff" style="margin-top:14px"></div>

          <div class="note-buttons" id="time-buttons" style="margin-top:12px"></div>

          <div style="margin-top:10px">
            <button class="btn primary" onclick="timeStart()">เริ่ม 60 วินาที</button>
            <button class="btn" onclick="timeReset()">รีเซ็ต</button>
          </div>

          <div style="margin-top:12px">
            <div class="timer-bar"><div id="time-fill" class="timer-fill"></div></div>
          </div>
        </div>

        <div class="right-col">
          <div class="card">
            <h4 style="margin:0">คำตอบ</h4>
            <div id="time-feedback" style="margin-top:8px" class="meta">เตรียมพร้อม…</div>
          </div>

          <div class="card" style="margin-top:12px">
            <h4 style="margin:0">Leaderboard: Time</h4>
            <div id="leader-time" style="margin-top:8px" class="meta">-</div>
          </div>
        </div>
      </div>
    </section>

    <!-- ===========================
         LEVEL MODE (lavender)
         =========================== -->
    <section id="level" class="page">
      <div class="game-area">
        <div class="left-col card">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div>
              <div class="score">Level Mode</div>
              <div class="meta">ผ่านด่านเพื่อเพิ่มความยาก</div>
            </div>
            <div id="level-score" class="meta">คะแนน: 0</div>
          </div>

          <div id="level-staff" style="margin-top:14px"></div>

          <div class="note-buttons" id="level-buttons" style="margin-top:12px"></div>

          <div style="margin-top:10px">
            <button class="btn" onclick="levelNext()">เริ่ม/ถัดไป</button>
            <button class="btn" onclick="levelReset()">รีเซ็ต</button>
          </div>

          <div style="margin-top:8px" class="meta">ด่านปัจจุบัน: <span id="level-num">1</span></div>
        </div>

        <div class="right-col">
          <div class="card">
            <h4 style="margin:0">คำตอบ</h4>
            <div id="level-feedback" style="margin-top:8px" class="meta">เริ่มด่าน 1</div>
          </div>

          <div class="card" style="margin-top:12px">
            <h4 style="margin:0">Leaderboard: Level</h4>
            <div id="leader-level" style="margin-top:8px" class="meta">-</div>
          </div>
        </div>
      </div>
    </section>

    <!-- ===========================
         MATCHING MODE (yellow/peach)
         =========================== -->
    <section id="matching" class="page">
      <div class="game-area">
        <div class="left-col card">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div>
              <div class="score">Matching Mode</div>
              <div class="meta">จับคู่โน้ตบน staff กับชื่อโน้ตภาษาไทย</div>
            </div>
            <div id="match-score" class="meta">คะแนน: 0</div>
          </div>

          <div style="margin-top:12px" class="meta">แตะการ์ดสองใบเพื่อจับคู่ (หรือใช้ drag/drop ใน desktop)</div>
          <div id="match-grid" class="match-grid" style="margin-top:12px"></div>

          <div style="margin-top:12px">
            <button class="btn" onclick="startMatching()">เริ่มใหม่</button>
            <button class="btn" onclick="shuffleMatching()">สับการ์ด</button>
          </div>
        </div>

        <div class="right-col">
          <div class="card">
            <h4 style="margin:0">คำแนะนำ</h4>
            <p class="meta">การ์ดประเภทหนึ่งจะแสดงโน้ตบน staff อีกประเภทจะแสดงคำไทย (โด/เร/มี) — จับคู่ให้ถูก</p>
            <div style="margin-top:8px">
              <button class="btn" onclick="playAllHints()">เล่นเสียงทั้งหมด</button>
            </div>
          </div>

          <div class="card" style="margin-top:12px">
            <h4 style="margin:0">Leaderboard: Matching</h4>
            <div id="leader-match" style="margin-top:8px" class="meta">-</div>
          </div>
        </div>
      </div>
    </section>

    <!-- ===========================
         RANKING
         =========================== -->
    <section id="ranking" class="page">
      <div class="card">
        <h2 style="margin:0">Leaderboard (Local)</h2>
        <p class="meta">บันทึกคะแนนดีที่สุดในเครื่องนี้ (localStorage)</p>
        <div style="margin-top:12px">
          <table id="leaderboard-table" style="width:100%;border-collapse:collapse">
            <thead><tr style="text-align:left"><th>ลำดับ</th><th>ชื่อ</th><th>โหมด</th><th>คะแนน</th><th>วันที่</th></tr></thead>
            <tbody></tbody>
          </table>
        </div>
        <div style="margin-top:12px">
          <button class="btn" onclick="clearLeaderboard()">ลบ Leaderboard</button>
        </div>
      </div>
    </section>
  </div>

<script>
/* ============================
   Constants & Note Data
   ============================ */
const NOTE_MAP = {
  "C": "โด",
  "D": "เร",
  "E": "มี",
  "F": "ฟา",
  "G": "ซอล",
  "A": "ลา",
  "B": "ที"
};
// A simple list of playable notes (Treble range E4-F5)
const PLAYABLE_NOTES = [
  {name:"E", octave:4}, {name:"F", octave:4}, {name:"G", octave:4},
  {name:"A", octave:4}, {name:"B", octave:4}, {name:"C", octave:5},
  {name:"D", octave:5}, {name:"E", octave:5}, {name:"F", octave:5}
];
// Frequency calc (A4 = 440Hz)
function noteFrequency(name,octave){
  const SEMITONE = {"C": -9,"D": -7,"E": -5,"F": -4,"G": -2,"A": 0,"B": 2};
  const n = SEMITONE[name] + (octave - 4)*12;
  return 440 * Math.pow(2, n/12);
}

/* ============================
   Audio (WebAudio API)
   ============================ */
const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
function playNoteSound(name,octave,duration=0.8){
  const freq = noteFrequency(name,octave);
  const o = audioCtx.createOscillator();
  const g = audioCtx.createGain();
  o.type = 'sine';
  o.frequency.value = freq;
  g.gain.value = 0;
  o.connect(g);
  g.connect(audioCtx.destination);
  const t = audioCtx.currentTime;
  g.gain.linearRampToValueAtTime(0.001, t);
  g.gain.exponentialRampToValueAtTime(0.3, t + 0.02);
  g.gain.exponentialRampToValueAtTime(0.0001, t + duration);
  o.start(t);
  o.stop(t + duration + 0.02);
}

/* ============================
   Utility: shuffle
   ============================ */
function shuffleArray(a){
  for(let i=a.length-1;i>0;i--){
    const j=Math.floor(Math.random()*(i+1));
    [a[i],a[j]]=[a[j],a[i]];
  }
  return a;
}

/* ============================
   Staff rendering (SVG)
   Simple staff with note positions
   ============================ */
function createStaffSVG(noteObj, options={}){
  // noteObj: {name:"C", octave:5} or null for blank
  const w = options.width || 520;
  const h = options.height || 140;
  const viewBox = `0 0 ${w} ${h}`;
  // staff lines positions
  const lineYs = [30,46,62,78,94]; // 5 lines
  // map note to y: simple map for treble (E4 bottom line -> E5 two ledger above)
  const positionMap = { // approximate y values for positions
    "E4": 94, "F4": 86, "G4":78, "A4":70, "B4":62, "C5":54, "D5":46, "E5":38, "F5":30
  };
  const svgNS = 'http://www.w3.org/2000/svg';
  const svg = document.createElementNS(svgNS,'svg');
  svg.setAttribute('width','100%');
  svg.setAttribute('height',h);
  svg.setAttribute('viewBox',viewBox);
  svg.setAttribute('role','img');
  // draw lines
  lineYs.forEach(y=>{
    const line = document.createElementNS(svgNS,'line');
    line.setAttribute('x1',20); line.setAttribute('x2',w-20);
    line.setAttribute('y1',y); line.setAttribute('y2',y);
    line.setAttribute('stroke','#222'); line.setAttribute('stroke-opacity',0.12);
    line.setAttribute('stroke-width',2);
    svg.appendChild(line);
  });
  // draw clef (simple G-clef curve using path)
  const clef = document.createElementNS(svgNS,'text');
  clef.setAttribute('x',22); clef.setAttribute('y',82);
  clef.setAttribute('font-size',48); clef.setAttribute('fill','#222'); clef.setAttribute('font-family','serif');
  clef.textContent = '𝄞';
  svg.appendChild(clef);

  // if there is a note, place an oval
  if(noteObj){
    const key = `${noteObj.name}${noteObj.octave}`;
    const y = positionMap[key] || 70;
    const cx = w/2;
    const cy = y;
    const n = document.createElementNS(svgNS,'ellipse');
    n.setAttribute('cx',cx); n.setAttribute('cy',cy);
    n.setAttribute('rx',14); n.setAttribute('ry',10);
    n.setAttribute('transform',`rotate(-18 ${cx} ${cy})`);
    n.setAttribute('fill','#222'); n.setAttribute('fill-opacity',0.95); n.setAttribute('stroke','#000'); n.setAttribute('stroke-width',0.6);
    n.setAttribute('class','svg-note');
    svg.appendChild(n);
    // ledger lines for out-of-staff if needed (not heavy here)
    if(key === 'C5' || key==='D5' || key==='E5' || key==='F5'){
      // possibly draw small ledger lines near the note
      const ledger = document.createElementNS(svgNS,'line');
      ledger.setAttribute('x1',cx-22); ledger.setAttribute('x2',cx+22);
      ledger.setAttribute('y1',cy+20); ledger.setAttribute('y2',cy+20);
      ledger.setAttribute('stroke','#222'); ledger.setAttribute('stroke-width',2);
      ledger.setAttribute('stroke-opacity',0.12);
      svg.appendChild(ledger);
    }
    // attach data for click to listen
    svg.dataset.note = noteObj.name;
    svg.dataset.octave = noteObj.octave;
    svg.style.cursor = 'pointer';
  }
  return svg;
}

/* ============================
   Page management (show/hide)
   ============================ */
function showPage(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  const el = document.getElementById(id);
  if(el) el.classList.add('active');
  // reset certain UI when switching pages
  if(id==='practice') { practiceInit() }
  if(id==='time') { timeReset() }
  if(id==='level') { levelInit() }
  if(id==='matching') { startMatching() }
  if(id==='ranking') { renderLeaderboardTable() }
}

/* ============================
   Player name + Leaderboard storage
   ============================ */
function getPlayerName(){ return localStorage.getItem('playerName') || 'ผู้เล่น' }
function setPlayerName(){
  const inp = document.getElementById('playerName');
  if(inp && inp.value.trim()){ localStorage.setItem('playerName', inp.value.trim()); alert('บันทึกชื่อแล้ว: '+inp.value.trim()); }
}
function saveScore(mode,score){
  const arr = JSON.parse(localStorage.getItem('mnr_leaderboard')||'[]');
  arr.push({name:getPlayerName(),mode,score,date:new Date().toLocaleString()});
  // keep up to 50 records
  localStorage.setItem('mnr_leaderboard', JSON.stringify(arr.slice(-500)));
}
function getLeaderboard(){
  return JSON.parse(localStorage.getItem('mnr_leaderboard')||'[]');
}
function clearLeaderboard(){
  if(confirm('ลบ Leaderboard ทั้งหมด?')){ localStorage.removeItem('mnr_leaderboard'); renderLeaderboardTable(); alert('ลบแล้ว'); }
}
function renderLeaderboardTable(){
  const tbl = document.querySelector('#leaderboard-table tbody');
  if(!tbl) return;
  const arr = getLeaderboard().sort((a,b)=>b.score - a.score);
  tbl.innerHTML = '';
  arr.forEach((r,i)=>{
    const tr = document.createElement('tr');
    tr.innerHTML = `<td>${i+1}</td><td>${escapeHtml(r.name)}</td><td>${escapeHtml(r.mode)}</td><td>${r.score}</td><td>${escapeHtml(r.date)}</td>`;
    tbl.appendChild(tr);
  });
}

/* simple escape */
function escapeHtml(s){ return (''+s).replace(/[&<>"']/g, c=>({ '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;' }[c])) }

/* ============================
   Practice Mode Implementation
   ============================ */
let practiceState = {score:0,current:null};
function practiceInit(){
  practiceState.score = 0;
  practiceState.current = null;
  document.getElementById('practice-score').textContent = 'คะแนน: 0';
  practiceNext();
}
function practiceNext(){
  // pick random note
  const note = PLAYABLE_NOTES[Math.floor(Math.random()*PLAYABLE_NOTES.length)];
  practiceState.current = note;
  // render
  const container = document.getElementById('practice-staff');
  container.innerHTML = '';
  const svg = createStaffSVG(note,{width:520,height:140});
  svg.onclick = ()=>{ playNoteSound(note.name,note.octave) };
  container.appendChild(svg);
  // create buttons
  const btns = document.getElementById('practice-buttons');
  btns.innerHTML = '';
  const choices = shuffleArray(Object.keys(NOTE_MAP).slice());
  choices.forEach(k=>{
    const b = document.createElement('button');
    b.innerHTML = `${k} (${NOTE_MAP[k]})`;
    b.onclick = ()=> practiceAnswer(k);
    btns.appendChild(b);
  });
  document.getElementById('practice-feedback').textContent = 'เลือกคำตอบ...';
}
function practiceAnswer(chosen){
  const cur = practiceState.current;
  if(!cur) return;
  if(chosen === cur.name){
    practiceState.score+=10;
    document.getElementById('practice-feedback').textContent = `ถูกต้อง! ${chosen} (${NOTE_MAP[chosen]})`;
    playNoteSound(cur.name,cur.octave,0.9);
  } else {
    practiceState.score = Math.max(0,practiceState.score-3);
    document.getElementById('practice-feedback').textContent = `ผิด! คำตอบ: ${cur.name} (${NOTE_MAP[cur.name]})`;
    // play correct note as hint
    playNoteSound(cur.name,cur.octave,0.9);
  }
  document.getElementById('practice-score').textContent = 'คะแนน: '+practiceState.score;
  // auto next after small delay
  setTimeout(practiceNext, 700);
}
function practiceClear(){ practiceState.score=0; document.getElementById('practice-score').textContent='คะแนน: 0'; }

/* ============================
   Time Challenge Implementation
   ============================ */
let timeState = {score:0,remaining:60,interval:null,current:null,started:false};
function timeReset(){
  timeState = {score:0,remaining:60,interval:null,current:null,started:false};
  document.getElementById('time-score').textContent = 'คะแนน: 0';
  document.getElementById('time-fill').style.width = '0%';
  document.getElementById('time-feedback').textContent = 'เตรียมพร้อม...';
  const container = document.getElementById('time-staff'); container.innerHTML='';
  document.getElementById('time-buttons').innerHTML='';
}
function timeStart(){
  if(timeState.started) return;
  timeState.started = true;
  timeState.score = 0; timeState.remaining = 60;
  document.getElementById('time-score').textContent = 'คะแนน: 0';
  nextTimeNote();
  timeState.interval = setInterval(()=>{
    timeState.remaining--;
    const pct = (60 - timeState.remaining)/60*100;
    document.getElementById('time-fill').style.width = `${pct}%`;
    if(timeState.remaining<=0){
      clearInterval(timeState.interval);
      timeState.started=false;
      document.getElementById('time-feedback').textContent = `จบ! คะแนน: ${timeState.score}`;
      saveScore('Time', timeState.score);
      renderTopByMode('Time','leader-time');
    }
  },1000);
}
function nextTimeNote(){
  const note = PLAYABLE_NOTES[Math.floor(Math.random()*PLAYABLE_NOTES.length)];
  timeState.current = note;
  const container = document.getElementById('time-staff');
  container.innerHTML='';
  const svg = createStaffSVG(note,{width:520,height:140});
  svg.onclick = ()=> playNoteSound(note.name,note.octave);
  container.appendChild(svg);
  // build buttons
  const btns = document.getElementById('time-buttons'); btns.innerHTML='';
  const choices = shuffleArray(Object.keys(NOTE_MAP).slice());
  choices.forEach(k=>{
    const b = document.createElement('button');
    b.innerHTML = `${k} (${NOTE_MAP[k]})`;
    b.onclick = ()=> {
      if(!timeState.started) return;
      if(k===note.name){ timeState.score+=10; document.getElementById('time-feedback').textContent='ถูก!'; playNoteSound(note.name,note.octave) }
      else { timeState.score = Math.max(0,timeState.score-2); document.getElementById('time-feedback').textContent=`ผิด! คำตอบ: ${note.name}`; playNoteSound(note.name,note.octave) }
      document.getElementById('time-score').textContent='คะแนน: '+timeState.score;
      nextTimeNote();
    };
    btns.appendChild(b);
  });
}
function playCurrentNote(){ // practice
  if(practiceState.current) playNoteSound(practiceState.current.name, practiceState.current.octave);
}

/* ============================
   Level Mode Implementation
   ============================ */
let levelState = {score:0,level:1,current:null};
function levelInit(){ levelState={score:0,level:1,current:null}; document.getElementById('level-score').textContent='คะแนน: 0'; document.getElementById('level-num').textContent='1'; levelNext(); }
function levelNext(){
  // difficulty increases with level: reduce choices or add ledger notes - here simulate by auto-pick from longer list
  const pool = PLAYABLE_NOTES.slice();
  // for higher levels we can add duplicate random to increase confusion
  const note = pool[Math.floor(Math.random()*pool.length)];
  levelState.current = note;
  const container = document.getElementById('level-staff'); container.innerHTML='';
  const svg = createStaffSVG(note,{width:520,height:140});
  svg.onclick = ()=> playNoteSound(note.name,note.octave);
  container.appendChild(svg);
  // create buttons: number of choices decreases as level up (harder)
  const choicesCount = Math.max(3, 7 - Math.min(5, levelState.level-1));
  const choices = shuffleArray(Object.keys(NOTE_MAP).slice()).slice(0,choicesCount);
  const btns = document.getElementById('level-buttons'); btns.innerHTML='';
  choices.forEach(k=>{
    const b = document.createElement('button');
    b.innerHTML = `${k} (${NOTE_MAP[k]})`;
    b.onclick = ()=> {
      if(k===note.name){ levelState.score+=15; document.getElementById('level-feedback').textContent='ถูก!'; playNoteSound(note.name,note.octave); levelState.level++; }
      else { levelState.score = Math.max(0, levelState.score-5); document.getElementById('level-feedback').textContent=`ผิด! คำตอบ: ${note.name}`; playNoteSound(note.name,note.octave); }
      document.getElementById('level-score').textContent='คะแนน: '+levelState.score;
      document.getElementById('level-num').textContent=levelState.level;
      // if reach threshold, save score to leaderboard for that level
      if(levelState.level>5){ // example: after 5 levels save
        saveScore('Level', levelState.score);
        renderTopByMode('Level','leader-level');
        alert('ผ่านด่านชุดนี้! บันทึกคะแนนแล้ว');
        levelReset();
      } else {
        levelNext();
      }
    };
    btns.appendChild(b);
  });
}
function levelReset(){ levelInit(); }

/* ============================
   Matching Mode Implementation
   ============================ */
let matchState = {pairs:[],selected:null,score:0};
function startMatching(){
  // create pairs: half notes (svg) + half labels (thai)
  matchState.score = 0; matchState.selected = null;
  document.getElementById('match-score').textContent='คะแนน: 0';
  const count = 4; // number of pairs
  const pool = shuffleArray(PLAYABLE_NOTES.slice()).slice(0,count);
  const noteCards = pool.map(n=>({type:'note',id:randomId(),note:n}));
  const labelCards = pool.map(n=>({type:'label',id:randomId(),note:n}));
  let cards = noteCards.concat(labelCards);
  cards = shuffleArray(cards);
  matchState.pairs = cards;
  renderMatchingGrid();
}
function renderMatchingGrid(){
  const grid = document.getElementById('match-grid'); grid.innerHTML='';
  matchState.pairs.forEach(card=>{
    const div = document.createElement('div');
    div.className='match-card';
    div.dataset.id=card.id;
    if(card.type==='note'){
      // embed small staff svg
      const svg = createStaffSVG(card.note,{width:200,height:80});
      svg.style.height='80px'; svg.style.width='100%';
      div.appendChild(svg);
      div.insertAdjacentHTML('beforeend',`<div class="meta" style="margin-top:6px">แตะเพื่อเล่นเสียง</div>`);
      div.onclick = ()=> {
        // reveal or select
        if(div.classList.contains('matched')) return;
        playNoteSound(card.note.name,card.note.octave);
        selectMatch(card.id);
      };
    } else {
      div.innerHTML = `<div style="font-size:24px;font-weight:700">${card.note.name} (${NOTE_MAP[card.note.name]})</div>`;
      div.onclick = ()=> selectMatch(card.id);
    }
    grid.appendChild(div);
  });
}
function selectMatch(id){
  if(!id) return;
  const card = matchState.pairs.find(c=>c.id===id);
  if(!card) return;
  // if already matched, ignore
  const cardElem = document.querySelector(`.match-card[data-id="${id}"]`);
  if(cardElem && cardElem.classList.contains('matched')) return;
  if(!matchState.selected){
    matchState.selected = card;
    // highlight
    highlightCard(id,true);
  } else {
    const prev = matchState.selected;
    if(prev.id === id){ // deselect
      highlightCard(id,false); matchState.selected = null; return;
    }
    // check match: one must be 'note' and the other 'label' and same note name
    const ok = (prev.note.name === card.note.name) && (prev.type !== card.type);
    if(ok){
      // mark matched
      markMatched(prev.id); markMatched(card.id);
      matchState.score += 20;
      document.getElementById('match-score').textContent = 'คะแนน: '+matchState.score;
      playNoteSound(card.note.name, card.note.octave);
      // check complete
      const remaining = matchState.pairs.filter(c=>!document.querySelector(`.match-card[data-id="${c.id}"]`).classList.contains('matched'));
      if(remaining.length===0){
        alert('จบ! คุณทำคะแนน '+matchState.score);
        saveScore('Matching',matchState.score);
        renderTopByMode('Matching','leader-match');
      }
    } else {
      // wrong
      matchState.score = Math.max(0, matchState.score-5);
      document.getElementById('match-score').textContent = 'คะแนน: '+matchState.score;
      // brief shake
      const e1 = document.querySelector(`.match-card[data-id="${prev.id}"]`);
      const e2 = document.querySelector(`.match-card[data-id="${card.id}"]`);
      [e1,e2].forEach(el=>{
        if(!el) return;
        el.animate([{transform:'translateX(0)'},{transform:'translateX(-8px)'},{transform:'translateX(8px)'},{transform:'translateX(0)'}],{duration:260});
      });
    }
    // clear selection highlight
    if(document.querySelector(`.match-card[data-id="${prev.id}"]`)) highlightCard(prev.id,false);
    matchState.selected = null;
  }
}
function highlightCard(id,on){
  const el = document.querySelector(`.match-card[data-id="${id}"]`);
  if(!el) return;
  if(on) el.style.outline='3px solid rgba(255,123,176,0.22)';
  else el.style.outline='none';
}
function markMatched(id){
  const el = document.querySelector(`.match-card[data-id="${id}"]`);
  if(!el) return;
  el.classList.add('matched');
  el.style.opacity='0.5';
}

/* helper */
function randomId(){ return Math.random().toString(36).slice(2,9); }
function shuffleMatching(){ matchState.pairs = shuffleArray(matchState.pairs); renderMatchingGrid(); }
function playAllHints(){ matchState.pairs.forEach((c,i)=> setTimeout(()=> playNoteSound(c.note.name,c.note.octave), i*300)); }

/* ============================
   Leaderboard mini-render helpers
   ============================ */
function renderTopByMode(mode,elementId){
  const arr = getLeaderboard().filter(r=>r.mode===mode).sort((a,b)=>b.score-a.score).slice(0,5);
  const el = document.getElementById(elementId);
  if(!el) return;
  if(arr.length===0) el.textContent='ยังไม่มีคะแนน';
  else el.innerHTML = arr.map(r=>`${escapeHtml(r.name)}: ${r.score}`).join('<br/>');
}

/* ============================
   Init / Wire up initial UI
   ============================ */
(function init(){
  // prefill player name input
  const inpn = document.getElementById('playerName');
  if(inpn) inpn.value = getPlayerName();
  // show initial small leader parts
  renderTopByMode('Time','leader-time'); renderTopByMode('Level','leader-level'); renderTopByMode('Matching','leader-match');
  // ensure practice initialized
  practiceInit();
  // Attach global playCurrentNote to window used by UI
  window.playCurrentNote = playCurrentNote;
})();

</script>
</body>
</html>
