<img width="1792" height="1024" alt="image" src="https://github.com/user-attachments/assets/51a6b23c-80a8-4435-9503-f2ffee97d4b7" />
[StudyHub2.0.html](https://github.com/user-attachments/files/21923089/StudyHub2.0.html)
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>StudyHub — NEET Dashboard</title>

  <!-- Google Font -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

  <style>
    :root{
      --bg-dark: #071022;
      --glass: rgba(255,255,255,0.05);
      --card: rgba(255,255,255,0.06);
      --accent: #7c5cff; /* change this for theme color */
      --accent-2: #00d4ff;
      --text: #e8f0ff;
    }
    *{box-sizing:border-box}
    html,body{height:100%;}
    body{
      margin:0;
      font-family: 'Poppins', system-ui, Arial, sans-serif;
      background: var(--bg-dark);
      color:var(--text);
      -webkit-font-smoothing:antialiased;
      -moz-osx-font-smoothing:grayscale;
      overflow-x:hidden;
    }

    /* BLURRED BACKGROUND IMAGE */
    .bg-image{
      position:fixed; inset:0; z-index:-3;
      background-size:cover; background-position:center center; background-repeat:no-repeat;
      filter: blur(3px) brightness(0.75) saturate(1.05);
      transform: scale(1.02);
    }
    .bg-overlay{position:fixed; inset:0; z-index:-2; background: linear-gradient(120deg, rgba(7,10,24,0.45), rgba(5,8,20,0.55));}

    /* Header */
    .header{position:fixed; top:18px; left:22px; right:22px; display:flex; justify-content:space-between; align-items:center; z-index:6}
    .brand{font-weight:700; font-size:20px; letter-spacing:0.3px}
    .quick-links{display:flex; gap:10px; align-items:center}
    .qlink{width:44px; height:44px; display:inline-grid; place-items:center; border-radius:10px; background:linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.01)); border:1px solid rgba(255,255,255,0.04); cursor:pointer}
    .qlink img{width:22px; opacity:0.95}

    /* MAIN LAYOUT */
    .main{min-height:100vh; display:flex; align-items:center; justify-content:center; gap:28px; padding:86px 20px 40px}

    /* CENTER CARD (pomodoro) */
    .card-center{
      width:620px; max-width:94%; background:var(--card); border-radius:18px; padding:28px; box-shadow:0 10px 30px rgba(2,6,23,0.6); border:1px solid rgba(255,255,255,0.04);
      display:flex; flex-direction:column; gap:18px; align-items:center; backdrop-filter: blur(6px);
    }

    /* circular timer */
    .timer-wrap{display:flex; flex-direction:column; align-items:center}
    .ring{width:360px; height:360px; display:grid; place-items:center}
    svg{width:100%; height:100%}
    .time-label{position:absolute; top:35%; left:50%; transform:translate(-50%, -50%); text-align;:center}
    #time-display{font-size:64px; font-weight:700; line-height:1; letter-spacing:1px}
    #session-label{font-size:18px; opacity:0.85; margin-top:8px}

    .controls{display:flex; gap:12px; margin-top:8px}
    .btn{padding:10px 18px; border-radius:10px; cursor:pointer; border:0; font-weight:600}
    .btn-start{background:linear-gradient(90deg,var(--accent),var(--accent-2)); color:rgb(255, 255, 255)}
    .btn-pause{background:transparent; color:var(--text); border:1px solid rgba(255,255,255,0.06)}
    .btn-reset{background:transparent; color:var(--text); border:1px solid rgba(255,255,255,0.06)}

    .settings{display:flex; gap:12px; margin-top:12px; align-items:center}
    .settings input{width:80px; padding:8px 10px; border-radius:8px; border:1px solid rgba(255,255,255,0.04); background:transparent; color:var(--text)}
    .small{font-size:13px; opacity:0.9}

    /* Sidebar for notes & chapters */
    .sidebar{width:360px; max-width:92%; display:flex; flex-direction:column; gap:18px}
    .panel{background:var(--glass); padding:16px; border-radius:12px; border:1px solid rgba(255,255,255,0.03)}
    .panel h4{margin:0 0 8px 0; font-size:16px}

    /* Notes */
    .notes-form input, .notes-form textarea{width:100%; padding:10px; border-radius:8px; border:1px solid rgba(255,255,255,0.04); background:transparent; color:var(--text)}
    .notes-list{display:flex; flex-direction:column; gap:8px; max-height:220px; overflow:auto}
    .note{padding:10px; border-radius:8px; background:rgba(255,255,255,0.02); border:1px solid rgba(255,255,255,0.03)}
    .note h5{margin:0 0 6px 0}
    .note .note-actions{display:flex; gap:8px; margin-top:8px}
    .tiny{font-size:12px; opacity:0.8}

    /* Chapters */
    .chapters-list{display:flex; flex-direction:column; gap:8px; max-height:300px; overflow:auto}
    .chapter{display:flex; justify-content:space-between; align-items:center; padding:8px 10px; border-radius:8px; background:rgba(255,255,255,0.02); border:1px solid rgba(255,255,255,0.03)}
    .chapter input[type=checkbox]{width:18px;height:18px}

    /* Footer small tips */
    .footer-note{font-size:13px; opacity:0.8; text-align:center; margin-top:10px}

    /* responsive */
    @media (max-width:1000px){
      .main{flex-direction:column; padding-top:110px}
      .sidebar{width:92%}
      .card-center{width:92%}
      .ring{width:320px;height:320px}
    }
    @media (max-width:420px){
      #time-display{font-size:44px}
      .ring{width:260px;height: 260px;}
    }

  </style>
</head>
<body>

  <!-- Background (place your PNG as bg.png in same folder) -->
  <div class="bg-image" style="background-image:url('image.png')"></div>
  <div class="bg-overlay"></div>

  <!-- Header with quick links -->
  <div class="header">
    <div class="brand">StudyHub • NEET Mode</div>
    <div class="quick-links">
      <a class="qlink" href="https://pw.live" target="_blank" title="PW">
        <img src="https://img.icons8.com/ios-filled/50/ffffff/school.png" alt="PW">
      </a>
      <a class="qlink" href="https://www.youtube.com" target="_blank" title="YouTube">
        <img src="https://img.icons8.com/ios-filled/50/ffffff/youtube-play.png" alt="YT">
      </a>
    </div>
  </div>

  <!-- Main area -->
  <div class="main">

    <!-- center pomodoro card -->
    <div class="card-center" role="main">
      <div class="timer-wrap">
        <div class="ring" aria-hidden="true">
          <!-- SVG circular progress ring -->
          <svg viewBox="0 0 120 120">
            <defs>
              <linearGradient id="g1" x1="0%" x2="100%" y1="0%" y2="0%">
                <stop offset="0%" stop-color="var(--accent)"/>
                <stop offset="100%" stop-color="var(--accent-2)"/>
              </linearGradient>
            </defs>
            <circle cx="60" cy="60" r="52" fill="none" stroke="rgba(255,255,255,0.06)" stroke-width="8" />
            <circle class="progress-ring__circle" cx="60" cy="60" r="52" fill="none" stroke="url(#g1)" stroke-width="8" stroke-linecap="round" transform="rotate(-90 60 60)" stroke-dasharray="0 999" />
          </svg>
        </div>

        <div class="time-label">
          <div id="time-display">25:00</div>
          <div id="session-label">Work • Focus mode</div>
        </div>

      </div>

      <div class="controls">
        <button id="startBtn" class="btn btn-start">Start</button>
        <button id="pauseBtn" class="btn btn-pause">Pause</button>
        <button id="resetBtn" class="btn btn-reset">Reset</button>
      </div>

      <div class="settings small">
        <label>Work (min): <input id="work-min" type="number" min="5" max="180" value="50"></label>
        <label>Break (min): <input id="break-min" type="number" min="1" max="60" value="10"></label>
        <label><input id="auto-switch" type="checkbox" checked> Auto-switch</label>
      </div>

      <div class="footer-note tiny">Tip: Click Start once to allow sound. Replace <code>bg.png</code> and <code>start.mp3/end.mp3</code> in the folder for custom background & sounds.</div>
    </div>

    <!-- sidebar: notes + chapters -->
    <aside class="sidebar">
      <div class="panel notes-panel">
        <h4>Quick Notes</h4>
        <form id="noteForm" class="notes-form">
          <input id="note-title" placeholder="Title (e.g., Cell cycle)" />
          <textarea id="note-body" rows="3" placeholder="Short note or formula..."></textarea>
          <div style="display:flex; gap:8px; margin-top:8px">
            <button id="saveNote" type="button" class="btn btn-start" style="flex:1">Save Note</button>
            <button id="clearNote" type="button" class="btn btn-pause" style="flex:0 0 90px">Clear</button>
          </div>
        </form>
        <div class="notes-list" id="notesList" aria-live="polite"></div>
      </div>

      <div class="panel chapters-panel">
        <h4>Syllabus Tracker</h4>
        <div style="display:flex; gap:8px; margin-bottom:8px">
          <input id="chapter-input" placeholder="Add chapter / topic" style="flex:1" />
          <button id="addChapter" class="btn btn-start">Add</button>
        </div>
        <div class="chapters-list" id="chaptersList"></div>
      </div>

    </aside>

  </div>

  <!-- Audio files should be present in same folder: start.mp3, end.mp3 -->
  <script>
    // ====== Simple StudyHub Pomodoro + Notes + Chapters (single-file) ======
    // Audio
    const startSound = new Audio('game-start-317318.mp3');
    const endSound = new Audio('timer-terminer-342934.mp3');
    startSound.volume = 0.9; endSound.volume = 0.8;

    // Timer variables
    let timer = null;
    let totalSeconds = 25 * 60;
    let remaining = totalSeconds;
    let running = false;
    let sessionType = 'work'; // work / break

    // DOM
    const timeDisplay = document.getElementById('time-display');
    const sessionLabel = document.getElementById('session-label');
    const startBtn = document.getElementById('startBtn');
    const pauseBtn = document.getElementById('pauseBtn');
    const resetBtn = document.getElementById('resetBtn');
    const workMinInput = document.getElementById('work-min');
    const breakMinInput = document.getElementById('break-min');
    const autoSwitch = document.getElementById('auto-switch');
    const progressCircle = document.querySelector('.progress-ring__circle');

    // circle progress setup
    const radius = progressCircle.r.baseVal.value;
    const circumference = 2 * Math.PI * radius;
    progressCircle.style.strokeDasharray = `${circumference} ${circumference}`;
    progressCircle.style.strokeDashoffset = circumference;
    function setProgress(percent){
      const offset = circumference - percent/100 * circumference;
      progressCircle.style.strokeDashoffset = offset;
    }

    // helpers
    function formatTime(s){
      const m = Math.floor(s/60); const sec = s%60;
      return `${m}:${sec.toString().padStart(2,'0')}`;
    }

    function updateDisplay(){
      timeDisplay.textContent = formatTime(remaining);
      const total = totalSeconds;
      const percent = Math.max(0, Math.min(100, (remaining/total)*100));
      setProgress(percent);
    }

    function saveSettings(){
      const work = parseInt(workMinInput.value) || 25;
      const br = parseInt(breakMinInput.value) || 5;
      localStorage.setItem('studyhub_settings', JSON.stringify({work,br,auto:autoSwitch.checked}));
    }

    function loadSettings(){
      const s = JSON.parse(localStorage.getItem('studyhub_settings')||'null');
      if(s){ workMinInput.value = s.work; breakMinInput.value = s.br; autoSwitch.checked = !!s.auto; }
      totalSeconds = parseInt(workMinInput.value)*60;
      remaining = totalSeconds;
      updateDisplay();
    }

    // start/pause/reset
    startBtn.addEventListener('click', ()=>{
      if(!running){
        // start
        running = true;
        startBtn.textContent = 'Running';
        pauseBtn.textContent = 'Pause';
        try{ startSound.currentTime = 0; startSound.play(); }catch(e){console.log('audio play error',e)}
        if(!timer) timer = setInterval(tick, 1000);
      }
    });
    pauseBtn.addEventListener('click', ()=>{
      if(running){ running = false; startBtn.textContent = 'Start'; pauseBtn.textContent = 'Paused'; clearInterval(timer); timer = null; }
    });
    resetBtn.addEventListener('click', ()=>{
      running = false; clearInterval(timer); timer=null; totalSeconds = (parseInt(workMinInput.value)||25)*60; remaining = totalSeconds; sessionType='work'; sessionLabel.textContent='Work • Focus mode'; startBtn.textContent='Start'; pauseBtn.textContent='Pause'; updateDisplay(); try{startSound.pause(); endSound.pause(); startSound.currentTime=0; endSound.currentTime=0;}catch(e){}
    });

    function tick(){
      if(remaining>0){ remaining--; updateDisplay(); }
      else {
        // session ended
        clearInterval(timer); timer=null; running=false;
        try{ endSound.currentTime = 0; endSound.play(); }catch(e){console.log('audio blocked',e)}

        // visual feedback
        flashMessage(sessionType === 'work' ? 'Work session complete!' : 'Break finished!');

        // auto switch
        if(autoSwitch.checked){
          if(sessionType === 'work'){
            sessionType = 'break';
            totalSeconds = (parseInt(breakMinInput.value)||5)*60;
            remaining = totalSeconds;
            sessionLabel.textContent = 'Break • Relax';
            // small delay before starting break
            setTimeout(()=>{
              try{ startSound.currentTime = 0; startSound.play(); }catch(e){}
              running = true; if(!timer) timer = setInterval(tick,1000); startBtn.textContent='Running';
            },650);
          } else {
            sessionType = 'work';
            totalSeconds = (parseInt(workMinInput.value)||25)*60;
            remaining = totalSeconds;
            sessionLabel.textContent = 'Work • Focus mode';
            setTimeout(()=>{
              try{ startSound.currentTime = 0; startSound.play(); }catch(e){}
              running = true; if(!timer) timer = setInterval(tick,1000); startBtn.textContent='Running';
            },650);
          }
        } else {
          // no auto switch: reset to work default
          sessionType = 'work'; totalSeconds = (parseInt(workMinInput.value)||25)*60; remaining = totalSeconds; sessionLabel.textContent='Work • Focus mode'; startBtn.textContent='Start';
        }
      }
    }

    // simple toast
    function flashMessage(txt){
      const el = document.createElement('div');
      el.textContent = txt; el.style.position='fixed'; el.style.left='50%'; el.style.top='20px'; el.style.transform='translateX(-50%)'; el.style.padding='10px 18px'; el.style.background='linear-gradient(90deg,var(--accent),var(--accent-2))'; el.style.color='white'; el.style.borderRadius='8px'; el.style.zIndex=9999; el.style.boxShadow='0 6px 20px rgba(0,0,0,0.6)';
      document.body.appendChild(el);
      setTimeout(()=>{ el.style.transition='opacity 400ms'; el.style.opacity='0'; setTimeout(()=>el.remove(),500); },1800);
    }

    // NOTES logic
    const notesKey = 'studyhub_notes';
    const noteForm = document.getElementById('noteForm');
    const notesList = document.getElementById('notesList');
    const noteTitle = document.getElementById('note-title');
    const noteBody = document.getElementById('note-body');

    function getNotes(){ return JSON.parse(localStorage.getItem(notesKey)||'[]'); }
    function saveNotes(arr){ localStorage.setItem(notesKey, JSON.stringify(arr)); renderNotes(); }
    function renderNotes(){
      const arr = getNotes(); notesList.innerHTML='';
      if(arr.length===0){ notesList.innerHTML='<div class="tiny" style="opacity:0.8">No notes yet — add quick formulas or short points.</div>'; return; }
      arr.slice().reverse().forEach((n, idx)=>{
        const div = document.createElement('div'); div.className='note';
        div.innerHTML = `<h5>${escapeHtml(n.title)}</h5><div class='tiny'>${escapeHtml(n.body)}</div>
          <div class='note-actions'><button data-i='${arr.length-1-idx}' class='btn btn-pause tiny'>Delete</button></div>`;
        notesList.appendChild(div);
      });
      // attach delete
      notesList.querySelectorAll('button[data-i]').forEach(b=>b.addEventListener('click', ()=>{ const i= +b.dataset.i; const a=getNotes(); a.splice(i,1); saveNotes(a); }));
    }

    document.getElementById('saveNote').addEventListener('click', ()=>{
      const t = noteTitle.value.trim(); const b = noteBody.value.trim(); if(!t && !b) return flashMessage('Note empty');
      const arr = getNotes(); arr.push({title:t||'(no title)', body:b}); saveNotes(arr); noteTitle.value=''; noteBody.value=''; flashMessage('Note saved');
    });
    document.getElementById('clearNote').addEventListener('click', ()=>{ noteTitle.value=''; noteBody.value=''; });

    // CHAPTERS
    const chKey = 'studyhub_chapters';
    const chapterInput = document.getElementById('chapter-input');
    const chaptersList = document.getElementById('chaptersList');
    function getCh(){ return JSON.parse(localStorage.getItem(chKey)||'[]'); }
    function saveCh(a){ localStorage.setItem(chKey, JSON.stringify(a)); renderCh(); }
    function renderCh(){ const a = getCh(); chaptersList.innerHTML=''; if(a.length===0){ chaptersList.innerHTML='<div class="tiny">No chapters yet.</div>'; return; } a.forEach((c,i)=>{ const el = document.createElement('div'); el.className='chapter'; el.innerHTML=`<label style="display:flex;gap:10px;align-items:center"><input type='checkbox' data-i='${i}' ${c.done? 'checked':''}><span>${escapeHtml(c.name)}</span></label><div><button data-del='${i}' class='btn btn-pause tiny'>Delete</button></div>`; chaptersList.appendChild(el); }); chaptersList.querySelectorAll('input[type=checkbox]').forEach(cb=>cb.addEventListener('change', ()=>{ const i=+cb.dataset.i; const a=getCh(); a[i].done = cb.checked; saveCh(a); })); chaptersList.querySelectorAll('button[data-del]').forEach(b=>b.addEventListener('click', ()=>{ const i=+b.dataset.del; const a=getCh(); a.splice(i,1); saveCh(a); })); }
    document.getElementById('addChapter').addEventListener('click', ()=>{ const val = chapterInput.value.trim(); if(!val) return; const a = getCh(); a.push({name:val, done:false}); saveCh(a); chapterInput.value=''; flashMessage('Chapter added'); });

    // small helper
    function escapeHtml(s){ return String(s).replace(/[&<>'"]/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','\'':'&#39;','"':'&quot;'}[c]||c)); }

    // init
    loadSettings(); renderNotes(); renderCh();

    // save settings on change
    [workMinInput, breakMinInput, autoSwitch].forEach(el=>el.addEventListener('change', ()=>{ saveSettings(); totalSeconds = (parseInt(workMinInput.value)||25)*60; if(!running){ remaining = totalSeconds; updateDisplay(); } }));

  </script>
</body>
</html>[timer-terminer-342934.mp3](https://github.com/user-attachments/files/21923106/timer-terminer-342934.mp3)[game-start-317318.mp3](https://github.com/user-attachments/files/21923113/game-start-317318.mp3)


