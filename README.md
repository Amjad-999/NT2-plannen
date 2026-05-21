<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NT2 Planner — منصة تعلم اللغة الهولندية</title>
<meta name="description" content="أداة شاملة ومجانية للاستعداد لامتحان NT2 مع بنك مفردات وقارئ كتب">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Readex+Pro:wght@300;400;500;600;700&family=Cormorant+Garamond:ital,wght@0,600;0,700;1,600&display=swap" rel="stylesheet">
<!-- PDF.js من CDN -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/2.16.105/pdf.min.js"></script>
<style>
:root {
  --bg:#F3F0E8;--surface:#FFFFFF;--surface2:#FAF8F3;--surface3:#F0ECE2;
  --border:#E4DECE;--border2:#CFC8B4;
  --text:#1C1812;--text2:#4A4438;--muted:#8C8272;--muted2:#B5A990;
  --orange:#C84B0E;--orange-d:#A03B0B;--orange-l:#FDF0E8;--orange-m:#F5D4BF;
  --blue:#1A5CB4;--blue-l:#EAF1FB;
  --green:#1E7A3C;--green-l:#E8F6EE;
  --amber:#A05C0A;--amber-l:#FBF2E2;
  --purple:#6B2FA0;--purple-l:#F4EEF9;
  --red:#B91C1C;--red-l:#FEF0F0;
  --c1:#1A5CB4;--c2:#A05C0A;--c3:#C84B0E;--c4:#1E7A3C;--c5:#6B2FA0;
  --shadow-sm:0 1px 4px rgba(0,0,0,.06), 0 0 0 1px rgba(0,0,0,.04);
  --shadow:0 4px 16px rgba(0,0,0,.08), 0 1px 4px rgba(0,0,0,.04);
  --shadow-lg:0 16px 48px rgba(0,0,0,.14), 0 4px 16px rgba(0,0,0,.06);
  --r:14px;--r-sm:8px;
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{font-size:15px;scroll-behavior:smooth}
body{background:var(--bg);color:var(--text);font-family:'Readex Pro',sans-serif;font-weight:400;line-height:1.6;min-height:100vh}

/* شريط علوي */
.topbar{position:sticky;top:0;z-index:200;background:rgba(243,240,232,.95);backdrop-filter:blur(18px) saturate(1.3);-webkit-backdrop-filter:blur(18px) saturate(1.3);border-bottom:1px solid var(--border);display:flex;align-items:center;gap:12px;padding:0 28px;height:62px}
.topbar-logo{display:flex;align-items:center;gap:10px;text-decoration:none;flex-shrink:0}
.logo-mark{width:34px;height:34px;border-radius:8px;background:var(--orange);display:flex;align-items:center;justify-content:center;font-size:1rem;color:#fff;flex-shrink:0;box-shadow:0 2px 8px rgba(200,75,14,.3)}
.logo-text{font-family:'Cormorant Garamond',serif;font-size:1.25rem;font-weight:700;color:var(--text);letter-spacing:-.3px;line-height:1}
.logo-text span{color:var(--orange)}
.topbar-gap{flex:1}
.top-pill{display:flex;align-items:center;gap:6px;border:1px solid var(--border2);border-radius:99px;padding:5px 14px;font-size:.8rem;color:var(--muted);background:var(--surface);white-space:nowrap}
.top-pill strong{color:var(--orange);font-weight:600}
.top-user{display:flex;align-items:center;gap:8px;font-size:.82rem;color:var(--text2);font-weight:500}
.user-avatar{width:32px;height:32px;border-radius:99px;background:var(--orange);color:#fff;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:.85rem;flex-shrink:0}
.icon-btn{width:36px;height:36px;border-radius:8px;border:1px solid var(--border2);background:var(--surface);color:var(--muted);cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:1rem;transition:.18s;flex-shrink:0}
.icon-btn:hover{border-color:var(--orange);color:var(--orange);background:var(--orange-l)}

/* شريط التبويبات */
.nav-bar{background:var(--surface);border-bottom:1px solid var(--border);display:flex;align-items:center;padding:0 28px;position:sticky;top:62px;z-index:190;overflow-x:auto;-webkit-overflow-scrolling:touch;scrollbar-width:none}
.nav-bar::-webkit-scrollbar{display:none}
.nav-tab{background:none;border:none;border-bottom:2px solid transparent;font-family:'Readex Pro',sans-serif;font-size:.88rem;font-weight:500;color:var(--muted);padding:14px 20px;cursor:pointer;white-space:nowrap;display:flex;align-items:center;gap:7px;transition:.18s}
.nav-tab:hover{color:var(--text2)}
.nav-tab.active{color:var(--orange);border-bottom-color:var(--orange);font-weight:600}
.nav-tab .tab-icon{font-size:1rem}
.nav-tab-featured{color:var(--orange-d);font-weight:600;position:relative}
.nav-tab-featured::after{content:'';position:absolute;top:10px;left:6px;width:6px;height:6px;border-radius:50%;background:var(--orange);animation:pulse 1.8s infinite}

/* الأقسام */
.section{display:none;padding:28px;max-width:980px;margin:0 auto}
.section.active{display:block;animation:fadeIn .22s ease}
@keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}

/* البطاقات والإحصائيات */
.stats-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-bottom:24px}
.stat-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:18px 20px;box-shadow:var(--shadow-sm);transition:.18s;position:relative}
.stat-card:hover{transform:translateY(-2px);box-shadow:var(--shadow)}
.stat-card.editable{cursor:pointer}
.stat-card.editable::after{content:'✏️';position:absolute;top:10px;left:12px;font-size:.78rem;opacity:.35;transition:opacity .18s}
.stat-card.editable:hover::after{opacity:.85}
.stat-icon-wrap{width:38px;height:38px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:1.1rem;margin-bottom:12px}
.stat-val{font-family:'Cormorant Garamond',serif;font-size:2rem;font-weight:700;line-height:1;color:var(--text)}
.stat-lbl{font-size:.78rem;color:var(--muted);margin-top:4px}
.stat-sub{font-size:.72rem;color:var(--muted2);margin-top:2px}

/* تنسيقات خطة الدراسة والكتب والمصادر - مختصرة للوضوح */
.hero-card{background:var(--text);border-radius:20px;padding:32px 36px;display:flex;align-items:center;gap:28px;margin-bottom:24px;position:relative;overflow:hidden;box-shadow:0 8px 32px rgba(28,24,18,.25);}
.hero-content{position:relative;z-index:2;color:#fff}
.hero-name{font-family:'Cormorant Garamond',serif;font-size:2.2rem;font-weight:700}
.hero-cd-num{font-family:'Cormorant Garamond',serif;font-size:4.5rem;font-weight:700;color:var(--orange);text-shadow:0 2px 12px rgba(200,75,14,.45)}
.today-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:20px 24px;display:flex;align-items:center;gap:20px}
.phase-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);overflow:hidden;margin-bottom:14px}
.task-tbl{width:100%;border-collapse:collapse}
.btn-complete{background:none;border:1px solid var(--border2);color:var(--muted);border-radius:6px;padding:5px 11px;cursor:pointer;font-size:.75rem}
.btn-primary{background:var(--orange);color:#fff;border:none;border-radius:9px;padding:11px 20px;cursor:pointer;font-weight:600}
.overlay{display:none;position:fixed;inset:0;z-index:400;background:rgba(28,24,18,.6);backdrop-filter:blur(6px);justify-content:center;align-items:center;padding:20px}
.overlay.open{display:flex}
.modal{background:var(--surface);border:1px solid var(--border);border-radius:20px;width:100%;max-width:480px;box-shadow:var(--shadow-lg);animation:modalIn .22s ease;max-height:90vh;overflow-y:auto}
@keyframes modalIn{from{transform:scale(.96);opacity:0}to{transform:scale(1);opacity:1}}
.save-flash{position:fixed;bottom:24px;right:24px;z-index:350;background:var(--green);color:#fff;padding:10px 16px;border-radius:99px;opacity:0;transition:.22s;pointer-events:none}
.save-flash.show{opacity:1}
.timer-float{position:fixed;bottom:24px;left:24px;z-index:300;background:var(--text);border-radius:18px;padding:18px 22px;min-width:230px;display:none}
.timer-float.visible{display:block}
/* استجابة */
@media(max-width:760px){ .stats-grid{grid-template-columns:repeat(2,1fr)} }
</style>
</head>
<body>

<!-- الشريط العلوي -->
<header class="topbar">
  <a class="topbar-logo" href="#" onclick="switchTab('dashboard'); return false;">
    <div class="logo-mark">🇳🇱</div>
    <span class="logo-text">NT2 <span>Planner</span></span>
  </a>
  <div class="topbar-gap"></div>
  <div class="top-pill">⏱ وقت الدراسة: <strong id="topStudyTime">0 د</strong></div>
  <div class="top-pill">⏳ <strong id="topCdDays">—</strong> يوم</div>
  <div class="top-user"><div class="user-avatar" id="topAvatar">؟</div><span id="topUserName">—</span></div>
  <button class="icon-btn" onclick="openSettings()">⚙️</button>
</header>

<!-- التبويبات -->
<nav class="nav-bar">
  <button class="nav-tab active" onclick="switchTab('dashboard')"><span class="tab-icon">📊</span> لوحة التحكم</button>
  <button class="nav-tab" onclick="switchTab('plan')"><span class="tab-icon">🗓️</span> خطة الدراسة</button>
  <button class="nav-tab" onclick="switchTab('books')"><span class="tab-icon">📖</span> الكتب والوحدات</button>
  <button class="nav-tab" onclick="switchTab('resources')"><span class="tab-icon">🔗</span> مصادر</button>
  <button class="nav-tab nav-tab-featured" onclick="switchTab('platform')"><span class="tab-icon">⭐</span> منصتي</button>
  <button class="nav-tab" onclick="switchTab('vocab')"><span class="tab-icon">📚</span> مفرداتي</button>
  <button class="nav-tab" onclick="switchTab('reader')"><span class="tab-icon">📖</span> قارئ الكتب</button>
</nav>

<!-- المحتوى الرئيسي -->
<main id="tab-dashboard" class="section active">
  <div class="hero-card">
    <div class="hero-content"><div class="hero-name" id="heroName">NT2 Planner</div><div id="heroSub">أداتك الشاملة</div></div>
    <div class="hero-cd-num" id="heroCdNum">—</div>
  </div>
  <div class="stats-grid">
    <div class="stat-card"><div class="stat-val" id="statDone">0</div><div class="stat-lbl">مهام منجزة</div></div>
    <div class="stat-card"><div class="stat-val" id="statDays">—</div><div class="stat-lbl">أيام متبقية</div></div>
    <div class="stat-card editable" onclick="openStudyTimeModal()"><div class="stat-val" id="statHours">0</div><div class="stat-lbl">ساعات الدراسة</div></div>
    <div class="stat-card"><div class="stat-val" id="statPct">0%</div><div class="stat-lbl">نسبة الإنجاز</div></div>
  </div>
  <div class="today-card"><div class="today-day-num" id="todayDayNum">—</div><div><div id="todayTitle">—</div><div id="todayMeta">—</div></div><button onclick="toggleTodayDone()">○ إتمام</button></div>
</main>

<main id="tab-plan" class="section"><div id="phases-container"></div></main>
<main id="tab-books" class="section"><div id="books-container"></div></main>
<main id="tab-resources" class="section"><p>مصادر ومواقع...</p></main>
<main id="tab-platform" class="section"><p>منصتي الأساسية...</p></main>

<!-- تبويب المفردات -->
<main id="tab-vocab" class="section">
  <h2>📚 مفرداتي</h2>
  <div style="margin:10px 0;">
    <select id="vocabBookSelect" onchange="renderVocabList()">
      <option value="A2">A2</option>
      <option value="B1_deel1">B1 Deel 1</option>
      <option value="B1_deel2">B1 Deel 2</option>
    </select>
    <button class="btn-primary" onclick="openVocabImport()" style="margin-right:10px;">+ استيراد CSV</button>
  </div>
  <div class="stats-grid" style="grid-template-columns: repeat(3,1fr);">
    <div class="stat-card"><div class="stat-val" id="vTotal">0</div><div class="stat-lbl">إجمالي الكلمات</div></div>
    <div class="stat-card"><div class="stat-val" id="vLearned">0</div><div class="stat-lbl">متقنة</div></div>
    <div class="stat-card"><div class="stat-val" id="vDue">0</div><div class="stat-lbl">للمراجعة اليوم</div></div>
  </div>
  <div id="vocab-list"></div>
</main>

<!-- قارئ PDF -->
<main id="tab-reader" class="section">
  <h2>📖 قارئ الكتب</h2>
  <select id="pdfBookSelect" onchange="loadPDF()">
    <option value="">اختر كتاباً...</option>
    <option value="books/a2.pdf">A2 - Taalcompleet</option>
    <option value="books/b1_deel1.pdf">B1 Deel 1</option>
    <option value="books/b1_deel2.pdf">B1 Deel 2</option>
  </select>
  <div><canvas id="pdf-canvas" style="border:1px solid #ccc; width:100%; max-width:800px; margin-top:10px;"></canvas></div>
  <div style="margin-top:10px;"><button onclick="prevPage()">السابق</button> <span id="pageNum">1</span>/<span id="pageCount">--</span> <button onclick="nextPage()">التالي</button></div>
</main>

<!-- نوافذ منبثقة -->
<div id="overlayOnboard" class="overlay open">
  <div class="modal"><div class="modal-body"><p>أدخل اسمك وتاريخ الامتحان</p><input id="obName" placeholder="اسمك"><input type="date" id="obDate"><button onclick="saveOnboarding()">ابدأ</button></div></div>
</div>
<div id="overlaySettings" class="overlay"><div class="modal">...الإعدادات...</div></div>
<div id="overlayVocabImport" class="overlay">
  <div class="modal">
    <h3>استيراد كلمات CSV</h3>
    <textarea id="csvInput" placeholder="الصق المحتوى هنا..." style="width:100%; height:150px;"></textarea>
    <button class="btn-primary" onclick="importFromTextarea()">استيراد</button>
    <button onclick="closeVocabImport()">إلغاء</button>
  </div>
</div>

<div id="saveFlash" class="save-flash">✓ تم الحفظ</div>
<div id="timerFloat" class="timer-float">...</div>

<script>
'use strict';
// ---------------------- بيانات المخطط ----------------------
const PHASES = [
  { id:'p1', title:'المرحلة الأولى', sub:'A2', days:'1–14', color:'var(--c1)', tasks:[
    {day:'1',text:'وحدة 1 مراجعة',type:'review',dur:60},
    {day:'2',text:'وحدة 1 متقدم',type:'review',dur:60}
  ]},
  { id:'p2', title:'المرحلة الثانية', sub:'B1 deel1', days:'15–21', color:'var(--c2)', tasks:[
    {day:'15',text:'وحدة 1 مراجعة',type:'review',dur:60}
  ]}
];
const BOOKS = [
  {id:'b1',title:'Taalcompleet A2', units:['وحدة 1','وحدة 2']},
  {id:'b2',title:'B1 Deel 1', units:['وحدة 1','وحدة 2']}
];

// ---------------------- التخزين ----------------------
const SK = 'nt2_v5';
let S = { name:'', examDate:'', planDay:1, done:{}, studySec:0, bookUnits:{}, customDur:{}, vocab:{A2:[],B1_deel1:[],B1_deel2:[]} };
function loadState(){
  try{
    const raw = localStorage.getItem(SK);
    if(raw) S = JSON.parse(raw);
  }catch(e){}
}
function saveState(){ localStorage.setItem(SK, JSON.stringify(S)); document.getElementById('saveFlash').classList.add('show'); setTimeout(()=>document.getElementById('saveFlash').classList.remove('show'),1400); }
loadState();
if(!S.name) document.getElementById('overlayOnboard').classList.add('open');

// ---------------------- دوال عامة ----------------------
function switchTab(id){
  document.querySelectorAll('.section').forEach(s=>s.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(b=>b.classList.remove('active'));
  document.getElementById('tab-'+id).classList.add('active');
  const btn = document.getElementById('ntab-'+id) || document.querySelector(`[onclick="switchTab('${id}')"]`);
  if(btn) btn.classList.add('active');
  window.scrollTo({top:0,behavior:'smooth'});
}
function refreshAll(){
  updateCountdown(); updateProgress(); updateStudy(); updateTodayTask(); updateUserInfo();
}

// ---------------------- إعدادات سريعة ----------------------
function saveOnboarding(){
  S.name = document.getElementById('obName').value.trim() || 'مستخدم';
  S.examDate = document.getElementById('obDate').value;
  saveState(); document.getElementById('overlayOnboard').classList.remove('open'); refreshAll();
}

// ---------------------- مفردات ----------------------
function renderVocabList(){
  const book = document.getElementById('vocabBookSelect').value;
  const words = S.vocab[book] || [];
  const container = document.getElementById('vocab-list');
  let html = '';
  words.forEach((w,i)=>{
    html += `<div style="display:flex;justify-content:space-between;padding:8px;border-bottom:1px solid #eee;">
      <span><strong>${w.dutch}</strong> - ${w.arabic}</span>
      <button onclick="speakDutch('${w.dutch}')">🔊</button>
    </div>`;
  });
  container.innerHTML = html || '<p>لا توجد كلمات. استورد CSV.</p>';
  document.getElementById('vTotal').textContent = words.length;
}
function openVocabImport(){ document.getElementById('overlayVocabImport').classList.add('open'); }
function closeVocabImport(){ document.getElementById('overlayVocabImport').classList.remove('open'); }
function importFromTextarea(){
  const book = document.getElementById('vocabBookSelect').value;
  const csv = document.getElementById('csvInput').value.trim();
  if(!csv) return;
  const lines = csv.split('\n');
  const words = [];
  lines.forEach(line=>{
    const parts = line.split(',');
    if(parts.length>=2) words.push({dutch:parts[0].trim(), arabic:parts[1].trim()});
  });
  S.vocab[book] = words;
  saveState(); closeVocabImport(); renderVocabList();
}
function speakDutch(text){
  const u = new SpeechSynthesisUtterance(text);
  u.lang = 'nl-NL';
  speechSynthesis.speak(u);
}

// ---------------------- قارئ PDF ----------------------
let pdfDoc=null, pageNum=1;
function loadPDF(){
  const url = document.getElementById('pdfBookSelect').value;
  if(!url) return;
  pdfjsLib.getDocument(url).promise.then(pdf=>{
    pdfDoc=pdf;
    document.getElementById('pageCount').textContent=pdf.numPages;
    renderPage(1);
  });
}
function renderPage(num){
  pdfDoc.getPage(num).then(page=>{
    const canvas=document.getElementById('pdf-canvas');
    const ctx=canvas.getContext('2d');
    const vp=page.getViewport({scale:1.5});
    canvas.height=vp.height; canvas.width=vp.width;
    page.render({canvasContext:ctx,viewport:vp});
  });
  document.getElementById('pageNum').textContent=num;
}
function prevPage(){ if(pageNum<=1)return; pageNum--; renderPage(pageNum); }
function nextPage(){ if(!pdfDoc||pageNum>=pdfDoc.numPages)return; pageNum++; renderPage(pageNum); }

// ---------------------- دوال مؤقتة للإكمال ----------------------
function updateCountdown(){ document.getElementById('topCdDays').textContent='30'; }
function updateProgress(){ document.getElementById('statDone').textContent='0'; }
function updateStudy(){ document.getElementById('statHours').textContent='0'; }
function updateTodayTask(){ document.getElementById('todayTitle').textContent='مهمة اليوم'; }
function updateUserInfo(){ document.getElementById('topUserName').textContent=S.name||'مستخدم'; }
function openStudyTimeModal(){}
function toggleTodayDone(){}

// تشغيل أولي
refreshAll();
</script>
</body>
</html>
