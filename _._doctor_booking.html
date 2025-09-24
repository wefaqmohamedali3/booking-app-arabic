<!--
Simple single-file Patient Booking app for a doctor
Features:
- User booking page (open with ?role=booker) where patients enter full name (3 parts) and phone, choose date and a 10-minute slot
- Admin dashboard (open with ?role=admin or default) to view bookings, add/cancel, export CSV, set working hours and max bookings (default 100)
- Booking code: unpredictable, non-sequential alphanumeric code
- Persists data in localStorage; can export CSV for Excel
- Instructions: save as booking.html, open in browser. To open booking form share file URL with ?role=booker
-->

<!doctype html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>نظام حجوزات الدكتور - مصغر</title>
  <style>
    body{font-family:Tahoma, Arial, sans-serif;background:#f5f7fb;color:#222;padding:18px}
    .container{max-width:1100px;margin:0 auto;background:#fff;padding:18px;border-radius:8px;box-shadow:0 6px 18px rgba(0,0,0,0.06)}
    h1,h2{margin:6px 0}
    label{display:block;margin:8px 0 4px}
    input,select,button{padding:8px;border-radius:6px;border:1px solid #cbd5e1;font-size:14px}
    .flex{display:flex;gap:10px}
    .col{flex:1}
    table{width:100%;border-collapse:collapse;margin-top:12px}
    th,td{padding:8px;border:1px solid #e2e8f0;text-align:center}
    .small{font-size:13px;color:#555}
    .btn{cursor:pointer}
    .success{background:#10b981;color:white;border:none}
    .danger{background:#ef4444;color:white;border:none}
    .muted{color:#64748b}
    .badge{display:inline-block;padding:6px 10px;border-radius:999px;background:#eef2ff;color:#3730a3}
    .top{display:flex;justify-content:space-between;align-items:center}
    .note{background:#fffbea;padding:8px;border-left:4px solid #f59e0b;margin:8px 0;border-radius:6px}
    .right{text-align:right}
  </style>
</head>
<body>
  <div class="container">
    <div class="top">
      <h1>نظام حجوزات المرضى (مصغر)</h1>
      <div class="small muted">احفظ الملف كـ <code>booking.html</code> وشاركه أو استضيفه</div>
    </div>

    <div id="app"></div>

    <div style="margin-top:14px" class="small muted">البيانات مخزنة محلياً في متصفحك (localStorage). لتجربة نظيفة افتح نافذة جديدة (أخرى) أو اضغط زر إعادة ضبط.</div>
  </div>

<script>
// ======= CONFIG ========
const STORAGE_KEY = 'doctor_booking_v1';
const DEFAULT_CONFIG = {
  workStart: '09:00',
  workEnd: '18:00',
  slotMinutes: 10,
  maxBookingsPerDay: 100
};
// =======================

// Utilities
function loadState(){
  const raw = localStorage.getItem(STORAGE_KEY);
  if(!raw) return {config: DEFAULT_CONFIG, bookings: []};
  try{ return JSON.parse(raw);}catch(e){return {config: DEFAULT_CONFIG, bookings: []};}
}
function saveState(state){ localStorage.setItem(STORAGE_KEY, JSON.stringify(state)); }

function uid(len=8){
  // unpredictable code (crypto-based) - not sequential
  const arr = new Uint8Array(len);
  crypto.getRandomValues(arr);
  return Array.from(arr).map(b=>b.toString(36).padStart(2,'0')).join('').slice(0,len);
}
function genBookingCode(){
  // e.g. BK-4k9a2f-27
  const part = uid(8);
  const d = new Date();
  const day = String(d.getDate()).padStart(2,'0');
  const code = `BK-${part}-${day}`;
  return code.toUpperCase();
}

function parseTime(t){ const [hh,mm]=t.split(':').map(Number); return hh*60+mm; }
function formatTimeFromMin(mins){ const hh=Math.floor(mins/60); const mm=mins%60; return `${String(hh).padStart(2,'0')}:${String(mm).padStart(2,'0')}`; }

function getSlotsForDate(cfg, date){
  const start = parseTime(cfg.workStart);
  const end = parseTime(cfg.workEnd);
  const slots = [];
  for(let m=start; m+cfg.slotMinutes<=end; m+=cfg.slotMinutes){
    slots.push(formatTimeFromMin(m));
    if(slots.length>=cfg.maxBookingsPerDay) break;
  }
  return slots;
}

// State
let state = loadState();

// Basic UI helpers
const app = document.getElementById('app');
function clearApp(){app.innerHTML='';}

// Booking operations
function addBooking({nameParts, phone, date, time}){
  const code = genBookingCode();
  const booking = {
    id: Date.now().toString(36) + '-' + uid(4),
    code, nameParts, phone, date, time,
    status: 'booked', createdAt: new Date().toISOString()
  };
  state.bookings.push(booking); saveState(state);
  return booking;
}
function cancelBooking(id){
  const b = state.bookings.find(x=>x.id===id);
  if(b){ b.status='cancelled'; saveState(state); }
}
function completeBooking(id){ const b=state.bookings.find(x=>x.id===id); if(b){ b.status='done'; saveState(state);} }

function bookingsForDate(date){ return state.bookings.filter(b=>b.date===date && b.status!=='cancelled'); }
function isSlotAvailable(date,time){ const used = state.bookings.some(b=>b.date===date && b.time===time && b.status!=='cancelled'); return !used; }

// Export CSV
function exportCSV(rows, filename='bookings.csv'){
  const header = Object.keys(rows[0] || {}).join(',');
  const lines = rows.map(r=>Object.values(r).map(v=>`"${String(v||'').replace(/"/g,'""')}"`).join(','));
  const csv = [header, ...lines].join('\r\n');
  const blob = new Blob([csv], {type:'text/csv;charset=utf-8;'});
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a'); a.href=url; a.download=filename; a.click(); URL.revokeObjectURL(url);
}

// Renderers
function renderAdmin(){
  clearApp();
  const cfg = state.config || DEFAULT_CONFIG;
  app.innerHTML = `
    <h2>لوحة التحكم (Admin)</h2>
    <div class="note">لرابط الحجز للمستخدم: افتح نفس الملف مع <code>?role=booker</code> (أو ارفعه إلى سيرفر وشارك الرابط مع المستخدمين)</div>
    <div class="flex">
      <div class="col">
        <h3>إعدادات</h3>
        <label>ساعة بداية العمل <input id="cfgStart" value="${cfg.workStart}"></label>
        <label>ساعة نهاية العمل <input id="cfgEnd" value="${cfg.workEnd}"></label>
        <label>مدة الشريحة (دقائق) <input id="cfgSlot" value="${cfg.slotMinutes}" type="number"></label>
        <label>أقصى عدد حجوزات في اليوم <input id="cfgMax" value="${cfg.maxBookingsPerDay}" type="number"></label>
        <div style="margin-top:8px"><button id="saveCfg" class="btn">حفظ الإعدادات</button>
        <button id="resetAll" class="btn danger">إعادة ضبط وحذف كل البيانات</button></div>
      </div>
      <div class="col">
        <h3>إضافة حجز يدوي</h3>
        <label>الاسم (الاسم الثلاثي مطلوب) <input id="manName" placeholder="الاسم الأول الأوسط الأخير"></label>
        <label>الجوال <input id="manPhone" placeholder="05xxxxxxxx"></label>
        <label>التاريخ <input id="manDate" type="date"></label>
        <label>الوقت <input id="manTime" placeholder="مثال 09:10"></label>
        <div style="margin-top:8px"><button id="addManual" class="btn success">أضف حجز</button></div>
      </div>
    </div>

    <h3>لوحة الإحصاء</h3>
    <div class="flex">
      <div class="col">الحجوزات اليوم: <span id="todayCount" class="badge">0</span></div>
      <div class="col">الحجوزات المنفذة اليوم: <span id="todayDone" class="badge">0</span></div>
      <div class="col">مجموع الحجوزات: <span id="totalCount" class="badge">0</span></div>
      <div class="col">متبقي / متاح اليوم: <span id="availableToday" class="badge">0</span></div>
    </div>

    <h3>إدارة الحجوزات</h3>
    <label>عرض تاريخ <input id="viewDate" type="date"></label>
    <div id="bookingsTable"></div>
    <div style="margin-top:12px">
      <button id="exportAll" class="btn">تصدير كل الحجوزات (CSV)</button>
      <button id="exportDay" class="btn">تصدير تاريخ العرض (CSV)</button>
    </div>
  `;

  // events
  document.getElementById('saveCfg').onclick = ()=>{
    state.config = state.config || {};
    state.config.workStart = document.getElementById('cfgStart').value || DEFAULT_CONFIG.workStart;
    state.config.workEnd = document.getElementById('cfgEnd').value || DEFAULT_CONFIG.workEnd;
    state.config.slotMinutes = Number(document.getElementById('cfgSlot').value) || DEFAULT_CONFIG.slotMinutes;
    state.config.maxBookingsPerDay = Number(document.getElementById('cfgMax').value) || DEFAULT_CONFIG.maxBookingsPerDay;
    saveState(state); renderAdmin();
  };
  document.getElementById('resetAll').onclick = ()=>{
    if(confirm('هل أنت متأكد من حذف جميع البيانات؟')){ localStorage.removeItem(STORAGE_KEY); state = loadState(); renderAdmin(); }
  };
  document.getElementById('addManual').onclick = ()=>{
    const name = document.getElementById('manName').value.trim();
    const phone = document.getElementById('manPhone').value.trim();
    const date = document.getElementById('manDate').value;
    const time = document.getElementById('manTime').value.trim();
    if(!name || name.split(/\s+/).length<3){ alert('الاسم الثلاثي مطلوب'); return; }
    if(!phone || !date || !time){ alert('أكمل البيانات'); return; }
    const nameParts = name.split(/\s+/).slice(0,3);
    addBooking({nameParts, phone, date, time});
    alert('تم إضافة الحجز'); renderAdmin();
  };
  document.getElementById('viewDate').value = new Date().toISOString().slice(0,10);
  document.getElementById('viewDate').onchange = renderBookingsForView;
  document.getElementById('exportAll').onclick = ()=>{
    if(state.bookings.length===0){ alert('لا توجد حجوزات للتصدير'); return; }
    exportCSV(state.bookings.map(b=>({code:b.code,date:b.date,time:b.time,name:b.nameParts.join(' '),phone:b.phone,status:b.status,createdAt:b.createdAt})), 'all_bookings.csv');
  };
  document.getElementById('exportDay').onclick = ()=>{
    const vd = document.getElementById('viewDate').value;
    const rows = state.bookings.filter(b=>b.date===vd).map(b=>({code:b.code,date:b.date,time:b.time,name:b.nameParts.join(' '),phone:b.phone,status:b.status,createdAt:b.createdAt}));
    if(rows.length===0){ alert('لا توجد حجوزات لليوم المختار'); return; }
    exportCSV(rows, `bookings_${vd}.csv`);
  };

  updateStats();
  renderBookingsForView();
}

function renderBookingsForView(){
  const vd = document.getElementById('viewDate').value;
  const cfg = state.config || DEFAULT_CONFIG;
  const slots = getSlotsForDate(cfg, vd);
  const rows = slots.map(slot=>{
    const b = state.bookings.find(x=>x.date===vd && x.time===slot && x.status!=='cancelled');
    return {slot, booked: !!b, booking: b||null};
  });
  const container = document.getElementById('bookingsTable');
  container.innerHTML = '<table><thead><tr><th>الوقت</th><th>الحالة</th><th>تفاصيل</th><th>إجراءات</th></tr></thead><tbody>' +
    rows.map(r=>{
      const statusText = r.booked? (r.booking.status==='done'? 'منفذ':'محجوز') : 'متاح';
      const details = r.booked? `${r.booking.nameParts.join(' ')} | ${r.booking.phone} | ${r.booking.code}` : '-';
      const action = r.booked? `<button data-id="${r.booking.id}" class="cancelBtn btn danger">إلغاء</button> <button data-id="${r.booking.id}" class="doneBtn btn">تم</button>` : '-';
      return `<tr><td>${r.slot}</td><td>${statusText}</td><td>${details}</td><td>${action}</td></tr>`;
    }).join('') + '</tbody></table>';

  container.querySelectorAll('.cancelBtn').forEach(btn=>btn.onclick = ()=>{ if(confirm('إلغاء هذا الحجز؟')){ cancelBooking(btn.dataset.id); renderAdmin(); }});
  container.querySelectorAll('.doneBtn').forEach(btn=>btn.onclick = ()=>{ completeBooking(btn.dataset.id); renderAdmin(); });
}

function updateStats(){
  const today = new Date().toISOString().slice(0,10);
  const todayBookings = state.bookings.filter(b=>b.date===today && b.status!=='cancelled');
  const todayDone = state.bookings.filter(b=>b.date===today && b.status==='done');
  document.getElementById('todayCount').innerText = todayBookings.length;
  document.getElementById('todayDone').innerText = todayDone.length;
  document.getElementById('totalCount').innerText = state.bookings.length;
  const cfg = state.config || DEFAULT_CONFIG;
  const totalSlotsToday = getSlotsForDate(cfg, today).length;
  document.getElementById('availableToday').innerText = Math.max(0, totalSlotsToday - todayBookings.length);
}

// User booking page
function renderBooker(){
  clearApp();
  const cfg = state.config || DEFAULT_CONFIG;
  app.innerHTML = `
    <h2>حجز موعد لمراجعة الطبيب</h2>
    <div class="note">الرجاء إدخال الاسم الثلاثي (الاسم الأول والاسم الأوسط واللقب) ورقم الجوال. اختر التاريخ ثم اختر وقت متاح.</div>
    <label>الاسم الثلاثي <input id="uName" placeholder="مثال: محمد أحمد علي"></label>
    <label>رقم الجوال <input id="uPhone" placeholder="05xxxxxxxx"></label>
    <label>التاريخ <input id="uDate" type="date" value="${new Date().toISOString().slice(0,10)}"></label>
    <label>الأوقات المتاحة</label>
    <div id="slotsArea"></div>
    <div style="margin-top:8px"><button id="doBook" class="btn success">تأكيد الحجز</button> <button id="clearForm" class="btn">مسح</button></div>
    <div id="bookResult" style="margin-top:12px"></div>
  `;

  function refreshSlots(){
    const date = document.getElementById('uDate').value;
    const slots = getSlotsForDate(cfg,date);
    const html = slots.map(s=>{
      const used = state.bookings.some(b=>b.date===date && b.time===s && b.status!=='cancelled');
      return `<button class="slotBtn btn" data-time="${s}" ${used? 'disabled': ''}>${s} ${used? '(محجوز)':''}</button>`;
    }).join(' ');
    document.getElementById('slotsArea').innerHTML = html;
    document.querySelectorAll('.slotBtn').forEach(b=>b.onclick = ()=>{
      document.querySelectorAll('.slotBtn').forEach(x=>x.style.outline=''); b.style.outline='3px solid #60a5fa'; b.dataset.selected='1'; document.getElementById('bookResult').innerText='';
      // mark selection
      document.getElementById('slotsArea').dataset.selected = b.dataset.time;
    });
  }
  document.getElementById('uDate').onchange = refreshSlots;
  document.getElementById('clearForm').onclick = ()=>{ document.getElementById('uName').value=''; document.getElementById('uPhone').value=''; document.getElementById('bookResult').innerText=''; }
  document.getElementById('doBook').onclick = ()=>{
    const name = document.getElementById('uName').value.trim();
    const phone = document.getElementById('uPhone').value.trim();
    const date = document.getElementById('uDate').value;
    const time = document.getElementById('slotsArea').dataset.selected;
    if(!name || name.split(/\s+/).length<3){ alert('الاسم الثلاثي مطلوب'); return; }
    if(!phone || !date || !time){ alert('اختر تاريخاً ووقتاً'); return; }
    if(!isSlotAvailable(date,time)){ alert('هذه الشريحة لم تعد متاحة'); refreshSlots(); return; }
    const nameParts = name.split(/\s+/).slice(0,3);
    const booking = addBooking({nameParts, phone, date, time});
    document.getElementById('bookResult').innerHTML = `<div class="note">تم الحجز! رقم الحجز: <strong>${booking.code}</strong><br/>التاريخ: ${booking.date} - ${booking.time}</div>`;
    refreshSlots();
  };

  refreshSlots();
}

// Router: use ?role=booker to show booking form, ?role=admin or default show admin
function router(){
  const qs = new URLSearchParams(location.search);
  const role = qs.get('role') || 'admin';
  state = loadState();
  if(role==='booker') renderBooker(); else renderAdmin();
}

// Init
router();

// For SPA: handle back/forward
window.addEventListener('popstate', router);

</script>

</body>
</html>
