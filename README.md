<!DOCTYPE html>
<html lang="uk">
  <head>
   <meta charset="utf-8" />
   <meta name="viewport" content="width=device-width,initial-scale=1" />
<title>MED-BRASLET — Медичний профіль</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
/* Чітка червоно-біло-чорна палітра */
:root{
--bg-light: #ffffff;
--bg-dark: #0b0b0b;
--card-light: #fff;
--card-dark: #111;
--text-light: #0b0b0b;
--text-dark: #ffffff;
--accent-red: #b71c1c;
--accent-red-2: #800000;
--muted-light: #666;
--muted-dark: #cfcfcf;
--input-bg-light: rgba(0,0,0,0.03);
--input-bg-dark: rgba(255,255,255,0.03);
--preview-row-light: rgba(0,0,0,0.05);
--preview-row-dark: rgba(255,255,255,0.05);
--radius: 12px;
}
html,body{height:100%}
body{
margin:0;padding:18px;font-family:Inter,system-ui, Arial, sans-serif;
background:var(--bg-light);color:var(--text-light);
transition: background .3s, color .3s; /* Плавний перехід теми */
}
body.dark{
background:var(--bg-dark);color:var(--text-dark);
}

/* Коректна інверсія кольорів для ЛОГОТИПУ та АВАТАРА */
.logo, .avatar {
background: #000; color: #fff;
width:52px;height:52px;border-radius:10px;
display:flex;align-items:center;justify-content:center;
font-weight:700;
transition: background .3s, color .3s;
}
.avatar { width: 84px; height: 84px; font-size: 20px; }
body.dark .logo, body.dark .avatar { background: #fff; color: #000; }

.app{max-width:1100px;margin:0 auto;display:grid;grid-template-columns:1fr 380px;gap:18px;align-items:start}
@media (max-width:980px){.app{grid-template-columns:1fr;padding:12px}.rightCol{order:-1}}
header{display:flex;justify-content:space-between;align-items:center;gap:12px;margin-bottom:10px}
.brand{display:flex;align-items:center;gap:12px}

h1{margin:0;font-size:18px}
.subtitle{font-size:13px;color:var(--muted-light)}
body.dark .subtitle{color:var(--muted-dark)}
.card{
background:var(--card-light);
border-radius:var(--radius);
padding:16px;
border:1px solid rgba(0,0,0,0.04);
box-shadow:0 10px 30px rgba(0,0,0,0.06);
transition: background .3s, border-color .3s, box-shadow .3s; /* Анімація картки */
}
body.dark .card{background:var(--card-dark);border:1px solid rgba(255,255,255,0.03);box-shadow:none}

/* Анімація для форми */
#formCard {
opacity: 1;
height: auto; /* Повертаємо auto для коректного відображення */
transition: opacity 0.5s ease-in-out, margin 0.5s ease-in-out, padding 0.5s ease-in-out, border 0.5s ease-in-out, box-shadow 0.5s ease-in-out;
}
#formCard.hidden {
opacity: 0;
height: 0;
padding: 0 16px;
margin: 0;
border: none;
box-shadow: none;
overflow: hidden;
}

/* Форма */
label{display:block;font-size:14px;margin-bottom:6px;color:var(--muted-light)}
body.dark label{color:var(--muted-dark)}
#profileForm > div { margin-bottom: 12px; }

input[type="text"], input[type="number"], select, textarea{
width:100%;padding:10px 12px;border-radius:10px;border:1px solid rgba(0,0,0,0.06);background:var(--input-bg-light);color:var(--text-light);font-size:15px;outline:none;
box-sizing: border-box;
transition: background-color .2s, border-color .2s;
}
input[type="text"]:focus, input[type="number"]:focus, select:focus, textarea:focus {
border-color: var(--accent-red-2);
box-shadow: 0 0 0 1px var(--accent-red-2);
}
body.dark input[type="text"], body.dark input[type="number"], body.dark select, body.dark textarea {
background:var(--input-bg-dark); color:var(--text-dark); border:1px solid rgba(255,255,255,0.04);
}
body.dark input[type="text"]:focus, body.dark input[type="number"]:focus, body.dark select:focus, body.dark textarea:focus {
border-color: var(--accent-red);
box-shadow: 0 0 0 1px var(--accent-red);
}

/* КРИТИЧНЕ ВИПРАВЛЕННЯ: Стилі для select[multiple] (Алергії, Хвороби) */
select[multiple]{
min-height: 40px; /* Мінімальна висота, як у звичайного input */
height: 40px; /* Фіксована висота */
padding: 0; /* Прибираємо внутрішній паддінг, щоб вмістити більше */
line-height: 1.2;
overflow-y: auto; /* Додаємо прокрутку */
/* Забезпечує коректне відображення на Desktop */
-webkit-appearance: none;
-moz-appearance: none;
appearance: none;
cursor: pointer; /* Для імітації стандартного select */
}
select[multiple] option {
padding: 8px 12px;
}
select[multiple] option:checked {
background-color: var(--accent-red-2);
color: white;
}
select[multiple] option:hover {
background-color: rgba(0,0,0,0.05);
}
body.dark select[multiple] option:hover {
background-color: rgba(255,255,255,0.05);
}


.hint{font-size:13px;color:var(--muted-light);margin-bottom:6px}
body.dark .hint{color:var(--muted-dark)}

/* Кнопки з анімацією */
.btn{
background:linear-gradient(90deg,var(--accent-red),var(--accent-red-2));color:#fff;padding:10px 12px;border-radius:10px;border:none;cursor:pointer;font-weight:700;
transition: all 0.2s ease-in-out;
}
.btn:hover {
opacity: 0.9;
transform: translateY(-1px);
box-shadow: 0 2px 5px rgba(0,0,0,0.2);
}
.btn.ghost{background:transparent;border:1px solid rgba(0,0,0,0.06);color:inherit}
.btn.ghost:hover {
background: rgba(0,0,0,0.05);
transform: none;
box-shadow: none;
}
body.dark .btn.ghost{border:1px solid rgba(255,255,255,0.03)}
body.dark .btn.ghost:hover {
background: rgba(255,255,255,0.05);
}

.small{font-size:13px;padding:8px}
.actions{display:flex;gap:10px;align-items:center;margin-top:8px}

/* SOS секція - АДАПТИВНІСТЬ */
.sosList{display:flex;flex-direction:column;gap:12px;margin-top:8px}
.sosItem{
display:flex;
flex-wrap: wrap;
gap: 8px;
align-items: center;
border: 1px dashed rgba(0,0,0,0.1);
border-radius: 8px;
padding: 8px;
transition: border-color .3s;
}
body.dark .sosItem { border: 1px dashed rgba(255,255,255,0.1); }

.sosItem input, .sosItem select{
padding:8px;border-radius:8px;
flex: 1 1 30%;
box-sizing: border-box;
min-width: 0;
}
.sosItem .sosName { flex-basis: 35%; }
.sosItem .sosPhone { flex-basis: 35%; }
.sosItem .sosRelation { flex-basis: 20%; }
.sosItem .removeBtn { flex: 0 0 auto; }

/* Поле "Інше" для SOS - займає всю ширину */
.sosOtherField {
flex: 1 1 100%;
margin-top: 4px;
}

@media (max-width: 600px) {
.sosItem input, .sosItem select { flex: 1 1 100%; }
.sosItem .sosName, .sosItem .sosPhone, .sosItem .sosRelation { flex-basis: 100%; }
}

.removeBtn{background:transparent;border:none;color:var(--accent-red);font-weight:700;cursor:pointer}
.removeBtn:hover { text-decoration: underline; }

.profileCard .header{display:flex;gap:12px;align-items:center}

.pill{
background:linear-gradient(90deg,var(--accent-red),var(--accent-red-2));color:#fff;padding:6px 10px;border-radius:999px;font-weight:700;
transition: background 0.3s;
}
.infoList{display:flex;flex-direction:column;gap:8px;margin-top:12px}

/* Grid-вирівнювання для профілю */
.infoItem{
display:grid;
grid-template-columns: 120px 1fr;
padding:10px 12px;
border-radius:var(--radius);
background:var(--preview-row-light);
align-items: start;
transition: background 0.3s;
}
body.dark .infoItem{background:var(--preview-row-dark)}

/* ЧІТКЕ ВІДОБРАЖЕННЯ SOS-КОНТАКТІВ */
.sosPreview{
display: flex;
flex-direction: column;
gap: 8px;
margin-top: 12px;
}
.sosPreview a{
display: flex;
justify-content: space-between;
align-items: center;
color:inherit;
text-decoration:none;
font-weight:700;
padding: 4px 0;
transition: color 0.2s;
}
.sosPreview a:hover {
color: var(--accent-red);
}
.sosPreview a span.number {
font-weight: 600;
color: var(--accent-red);
transition: color 0.2s;
}
body.dark .sosPreview a span.number {
color: var(--muted-dark);
}
body.dark .sosPreview a:hover span.number {
color: var(--accent-red);
}

/* ОНОВЛЕНИЙ ФУТЕР */
footer{
margin-top:18px;
color:var(--muted-light);
font-size:13px;
text-align: center;
}
.modal{
position:fixed;left:0;top:0;width:100%;height:100%;display:none;align-items:center;justify-content:center;background:rgba(0,0,0,0.65);padding:20px;z-index:9999;
/* Анімація модального вікна */
transition: opacity 0.3s ease-in-out;
opacity: 0;
}
.modal.show {
opacity: 1;
}
.modalCard{width:100%;max-width:700px;max-height: 90vh; overflow-y: auto;}
.linkBtn{background:transparent;border:1px solid rgba(0,0,0,0.06);padding:8px;border-radius:8px;color:var(--accent-red);font-weight:700}
body.dark .linkBtn{border:1px solid rgba(255,255,255,0.03)}
.muted{color:var(--muted-light);font-size:13px}
body.dark .muted{color:var(--muted-dark)}

/* Стилі для модального вікна "Перша допомога" */
.video-responsive {
overflow: hidden;
padding-bottom: 56.25%;
position: relative;
height: 0;
margin-bottom: 12px;
}
.video-responsive iframe {
left: 0;
top: 0;
height: 100%;
width: 100%;
position: absolute;
}
#firstAidInfo h4 {
margin-top: 1.2em;
margin-bottom: 0.5em;
color: var(--accent-red-2);
}

</style>
</head>
<body>
<div class="app">
<main>
<header>
<div class="brand">
<div class="logo">MB</div>
<div>
<h1 id="brandTitle">MED-BRASLET</h1>
<div class="subtitle" id="brandSubtitle">Медичний профіль — інформація, що рятує життя.</div>
</div>
</div>

<div style="display:flex;gap:8px;align-items:center">
<select id="langSwitch" aria-label="Language switch">
<option value="uk">Українська 🇺🇦</option>
<option value="en">English 🇬🇧</option>
</select>
<button id="themeToggle" class="linkBtn" title="Theme">🌙</button>
</div>
</header>

<section class="card" id="formCard" aria-labelledby="formTitle">
<h2 id="formTitle">Створити медичний профіль</h2>
<p class="hint" id="formHint">Потрібні дані, які допомагають швидко надати допомогу. Рекомендуємо встановити код редагування.</p>

<form id="profileForm" onsubmit="return false;">
<div><label id="lblName">Ім'я</label><input id="name" type="text" placeholder="Ім'я"></div>
<div><label id="lblSurname">Прізвище</label><input id="surname" type="text" placeholder="Прізвище"></div>
<div><label id="lblAge">Вік</label><input id="age" type="number" min="0" max="120" placeholder="Наприклад: 34"></div>
<div><label id="lblAddress">Адреса (місто)</label><input id="address" type="text" placeholder="Місто, вулиця"></div>
<div>
<label id="lblBlood">Група крові</label>
<select id="blood"></select>
</div>
<div>
<label id="lblRh">Rh</label>
<select id="rh"></select>
</div>

<div>
<label id="lblAllergy">Алергії</label>
<div class="hint" id="allergyHint">Виберіть одну або кілька опцій (Ctrl/Cmd + клік). Якщо виберете «Інше», з'явиться поле для вводу.</div>
<select id="allergy" multiple aria-label="Allergies"></select>
<input id="allergyOther" type="text" placeholder="Інше — впишіть тут" style="display:none;margin-top:6px">
</div>

<div>
<label id="lblDisease">Хронічні хвороби</label>
<div class="hint" id="diseaseHint">Виберіть одну або кілька опцій (Ctrl/Cmd + клік). Якщо виберете «Інше», з'явиться поле для вводу.</div>
<select id="disease" multiple aria-label="Diseases"></select>
<input id="diseaseOther" type="text" placeholder="Інше — впишіть тут" style="display:none;margin-top:6px">
</div>

<div><label id="lblMeds">Медикаменти</label><input id="meds" type="text" placeholder="Перелік медикаментів"></div>

<div>
<label id="lblSos">Контакти SOS</label>
<div class="hint" id="sosHint">Додайте 1–6 контактів. Для кожного вкажіть, ким є людина.</div>
<div id="sosList" class="sosList"></div>
<div style="margin-top:8px">
<button id="addContactBtn" type="button" class="btn small">➕ Додати контакт</button>
</div>
</div>

<div>
<label id="lblPin">Код для редагування (опційно)</label>
<div class="hint" id="pinHint">4–8 цифр — рекомендуємо, але не обов'язково</div>
<input id="pin" type="text" maxlength="8" placeholder="4–8 цифр або залиште порожнім">
<div id="pinErr" class="muted" style="color:var(--accent-red);display:none;margin-top:6px"></div>
</div>

<div class="actions">
<button id="saveBtn" type="button" class="btn">💾 Зберегти профіль</button>
<button id="clearBtn" type="button" class="btn ghost">🗑 Очистити</button>
</div>
</form>
</section>

</main>

<aside class="rightCol">
<section class="card profileCard" id="profileCard">
<div class="header">
<div class="avatar" id="avatar">MB</div>
<div>
<div id="previewName" style="font-weight:700">Профіль не створено</div>
<div id="previewSub" class="muted">Після збереження тут буде публічний профіль</div>
<div id="bloodBadge" style="margin-top:8px;display:none" class="pill"></div>
</div>
</div>

<div class="infoList" id="infoList"></div>

<div id="shareSection" style="margin-top:12px;display:none;text-align:center;">
<button id="copyProfileLinkBtn" class="btn small ghost" style="width:100%;" title="Скопіювати посилання для поширення">🔗 Поділитись профілем</button>
</div>

<div style="margin-top:12px">
<div style="display:flex;gap:8px">
<button id="sosBtn" class="btn small" style="flex:1">📞 SOS</button>
<button id="editBtn" class="btn small ghost" style="flex:1">✏️ Редагувати</button>
</div>
<div id="sosPreview" class="sosPreview"></div>
</div>
</section>

<section class="card" id="firstAidCard" style="margin-top:12px; display:none; text-align: center;">
<button id="openFirstAidModal" class="btn">Перша медична допомога</button>
<div style="margin-top:8px" class="muted" id="firstAidHint">Відео-інструкція та інформація</div>
</section>

<section class="card" style="margin-top:12px">
<h3 id="adviceTitle">Поради</h3>
<ul style="margin:8px 0 0 18px;color:var(--muted-light)" id="adviceList">
<li>Рекомендуємо встановити код для захисту редагування.</li>
<li>Додавайте контакт лікаря або найближчого родича.</li>
<li>Діліться профілем лише тим, кому довіряєте.</li>
</ul>
</section>
</aside>
</div>

<footer id="appFooter">
</footer>

<div id="sosModal" class="modal" role="dialog" aria-hidden="true">
<div class="modalCard card">
<button id="closeSos" style="float:right;border:none;background:transparent;font-size:18px">✖</button>
<h3 id="sosModalTitle">Контакти SOS</h3>
<ul id="sosModalList" style="list-style:none;padding-left:0;margin-top:8px"></ul>
</div>
</div>

<div id="firstAidModal" class="modal" role="dialog" aria-hidden="true">
<div class="modalCard card">
<button id="closeFirstAid" style="float:right;border:none;background:transparent;font-size:18px">✖</button>
<h3 id="firstAidModalTitle">Перша медична допомога (Basic Life Support)</h3>

<div class="video-responsive">
<iframe id="firstAidVideo" width="560" height="315" src="" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<div id="firstAidInfo">
</div>
</div>
</div>

<script>
/* ========== MED-BRASLET — FINAL STABLE (v5 - Fixed Public/Edit Mode - Subtitle dot fix) =========== */
const I18N = {
uk: {
brandTitle: 'MED-BRASLET',
brandSubtitle: 'Медичний профіль — інформація, що рятує життя.', // КРАПКА ДОДАНА
formTitle: 'Створити медичний профіль',
formHint: 'Потрібні дані, які допомагають швидко надати допомогу. Рекомендуємо встановити код редагування.',
addContact: 'Додати контакт',
save: 'Зберегти профіль',
saved: 'Збережено ✅',
clear: 'Очистити',
edit: 'Редагувати',
shareLinkText: '🔗 Поділитись профілем',
linkCopied: 'Скопійовано! ✅',
firstAidLinkText: 'Перша медична допомога',
firstAidHint: 'Відео-інструкція та інформація',
firstAidVideoId: 'EfnpLUcALps',
firstAidModalTitle: 'Перша медична допомога (Базова підтримка життя)',
firstAidInfo: `
<h4>Базовий алгоритм дій:</h4>
<ol>
<li><strong>Оцініть безпеку.</strong> Переконайтеся, що вам та постраждалому нічого не загрожує.</li>
<li><strong>Перевірте свідомість.</strong> Потрусіть за плечі та голосно запитайте: "З Вами все гаразд?"</li>
<li><strong>Викличте допомогу.</strong> Якщо людина не реагує, негайно телефонуйте **103** або **112**. Чітко повідомте місце та ситуацію.</li>
<li><strong>Відкрийте дихальні шляхи.</strong> Закиньте голову назад і підніміть підборіддя, щоб забезпечити прохідність.</li>
<li><strong>Перевірте дихання.</strong> Нахиліться і протягом 10 секунд послухайте, подивіться та відчуйте дихання (бажано).</li>
<li><strong>Почніть СЛР (Серцево-легенева реанімація).</strong> Якщо дихання відсутнє або ненормальне (агональне), виконайте 30 натискань на грудну клітку (посередині грудей, глибина 5-6 см) та, якщо навчені, 2 вдихи (30:2).</li>
<li><strong>Продовжуйте СЛР</strong> до прибуття допомоги або відновлення ознак життя.</li>
</ol>
<p>Джерело: Рекомендації МОЗ України та Європейської Ради з реанімації (ERC).</p>
`,
bloodOptions: ['— Оберіть —','0 (I)','A (II)','B (III)','AB (IV)'],
rhOptions: ['— —','+','-'],
relations: ['Батько','Мати','Брат','Сестра','Дідусь','Бабуся','Дружина','Чоловік','Лікар','Інше'],
allergyOptions: ['Пилок','Пил','Риба','Молоко','Медикаменти (антибіотики)','Укус комах','Горіхи','Інше'],
diseaseOptions: ['Діабет','Астма','Гіпертонія','Хвороба серця','Епілепсія','Онкологічні','Інше'],
noSos: 'Немає контактів SOS',
enterPin: 'Введіть код редагування',
pinWrong: 'Невірний код',
confirmClear: 'Ви впевнені, що хочете видалити локальний профіль?',
labelName: "Ім'я", placeholderName: "Ім'я",
labelSurname: 'Прізвище', placeholderSurname: 'Прізвище',
labelAge: 'Вік', placeholderAge: 'Наприклад: 34', ageUnits: 'років',
labelAddress: 'Адреса', placeholderAddress: 'Місто, вулиця',
labelBlood: 'Група крові',
labelRh: 'Rh',
labelAllergy: 'Алергії', allergyHint: 'Виберіть одну або кілька опцій (Ctrl/Cmd + клік). Якщо виберете «Інше», з\'явиться поле для вводу.', placeholderAllergyOther: 'Інше — впишіть тут',
labelDisease: 'Хронічні хвороби', diseaseHint: 'Виберіть одну або кілька опцій (Ctrl/Cmd + клік). Якщо виберете «Інше», з\'явиться поле для вводу.', placeholderDiseaseOther: 'Інше — впишіть тут',
labelMeds: 'Медикаменти', placeholderMeds: 'Перелік медикаментів',
labelSos: 'Контакти SOS', sosHint: 'Додайте 1–6 контактів. Для кожного вкажіть, ким є людина.',
labelPin: 'Код для редагування', pinHint: '4–8 цифр — рекомендуємо, але не обов\'язково',
previewNotCreated: 'Профіль не створено', previewSubHint: 'Після збереження тут буде публічний профіль',
adviceTitle: 'Поради',
advice1: 'Рекомендуємо встановити код для захисту редагування.',
advice2: 'Додавайте контакт лікаря або найближчого родича.',
advice3: 'Діліться профілем лише тим, кому довіряєте.',
sosModalTitle: 'Контакти SOS', sosItemPlaceholderName: "Ім'я", sosItemPlaceholderPhone: "Телефон", sosItemRelation: "Стосунок", sosItemRemove: "Видалити", sosItemPlaceholderOther: "Інше — впишіть тут",
alertName: "Вкажіть ім'я або прізвище", alertSos: 'У профілі нема SOS контактів. Продовжити?', alertMaxSos: 'Максимум 6 контактів', alertPin: 'Код має бути 4–8 цифр',
alertNoProfile: 'Спочатку створіть та збережіть профіль.',
alertEditShare: 'Будь ласка, видаліть частину URL після знаку "#", щоб повернутися в режим редагування.',
creationFooter: 'Створено за допомогою компанії VITRODUY',
},
en: {
brandTitle: 'MED-BRASLET',
brandSubtitle: 'Medical profile — information that saves lives.', // КРАПКА ДОДАНА
formTitle: 'Create medical profile',
formHint: 'Fill only what you are comfortable sharing. We recommend an edit PIN for protection.',
addContact: 'Add contact',
save: 'Save profile',
saved: 'Saved ✅',
clear: 'Clear',
edit: 'Edit',
shareLinkText: '🔗 Share Profile',
linkCopied: 'Copied! ✅',
firstAidLinkText: 'First Medical Aid',
firstAidHint: 'Video instruction and information',
firstAidVideoId: 'I-p_YnvOs-0',
firstAidModalTitle: 'First Medical Aid (Basic Life Support)',
firstAidInfo: `
<h4>Basic Life Support Algorithm:</h4>
<ol>
<li><strong>Check for danger.</strong> Ensure the area is safe for you and the casualty.</li>
<li><strong>Check for response.</strong> Shake the shoulders gently and ask loudly, "Are you alright?"</li>
<li><strong>Call for help.</strong> If there is no response, call **911** or your local emergency number immediately. Provide clear location and situation details.</li>
<li><strong>Open the airway.</strong> Tilt the head back and lift the chin to open the airway.</li>
<li><strong>Check for breathing.</strong> Look, listen, and feel for normal breathing for no more than 10 seconds.</li>
<li><strong>Start CPR (Cardiopulmonary Resuscitation).</strong> If breathing is absent or abnormal (agonal), start with 30 chest compressions (center of the chest, depth 5-6 cm) and, if trained, follow with 2 rescue breaths (30:2).</li>
<li><strong>Continue CPR</strong> until professional help arrives or the casualty shows signs of recovery.</li>
</ol>
<p>Source: European Resuscitation Council (ERC) Guidelines.</p>
`,
bloodOptions: ['— Select —','0 (I)','A (II)','B (III)','AB (IV)'],
rhOptions: ['— —','+','-'],
relations: ['Father','Mother','Brother','Sister','Grandpa','Grandma','Wife','Husband','Doctor','Other'],
allergyOptions: ['Pollen','Dust','Fish','Milk','Medications (antibiotics)','Insect sting','Nuts','Other'],
diseaseOptions: ['Diabetes','Astma','Hypertension','Heart disease','Epilepsy','Oncological','Other'],
noSos: 'No SOS contacts',
enterPin: 'Enter edit PIN',
pinWrong: 'Wrong PIN',
confirmClear: 'Are you sure you want to delete the local profile?',
labelName: 'Name', placeholderName: 'Name',
labelSurname: 'Surname', placeholderSurname: 'Surname',
labelAge: 'Age', placeholderAge: 'E.g.: 34', ageUnits: 'y.o.',
labelAddress: 'Address', placeholderAddress: 'City, street',
labelBlood: 'Blood group',
labelRh: 'Rh',
labelAllergy: 'Allergies', allergyHint: 'Select one or more options (Ctrl/Cmd + click). If you select "Other", an input field will appear.', placeholderAllergyOther: 'Other — enter here',
labelDisease: 'Chronic diseases', diseaseHint: 'Select one or more options (Ctrl/Cmd + click). If you select "Other", an input field will appear.', placeholderDiseaseOther: 'Other — enter here',
labelMeds: 'Medications', placeholderMeds: 'List of medications',
labelSos: 'SOS contacts', sosHint: 'Add 1–6 contacts. For each, specify the relation.',
labelPin: 'Edit PIN (optional)', pinHint: '4–8 digits — optional but recommended',
previewNotCreated: 'Profile not created', previewSubHint: 'Your public profile will appear here after saving',
adviceTitle: 'Advice',
advice1: 'We recommend setting a PIN to protect editing.',
advice2: 'Add the contact of a doctor or closest relative.',
advice3: 'Share the profile only with those you trust.',
sosModalTitle: 'SOS Contacts', sosItemPlaceholderName: "Name", sosItemPlaceholderPhone: "Phone", sosItemRelation: "Relation", sosItemRemove: "Remove", sosItemPlaceholderOther: "Other — enter here",
alertName: "Please enter name or surname", alertSos: 'No SOS contacts. Continue?', alertMaxSos: 'Max 6 contacts', alertPin: 'PIN must be 4–8 digits',
alertNoProfile: 'Create and save a profile first.',
alertEditShare: 'Please remove the part of the URL after the "#" sign to return to editing mode.',
creationFooter: 'Created with the help of VITRODUY company',
}
};

/* ---------- Keys & state ---------- */
const PROFILE_KEY = 'med_braslet_profile_v2';
const PIN_KEY = 'med_braslet_pin_v2';
let lang = localStorage.getItem('mb_lang') || (navigator.language && navigator.language.startsWith('en') ? 'en' : 'uk');
let theme = localStorage.getItem('mb_theme') || 'dark';

/* ---------- Element refs & Helpers (DRY) ---------- */
const el = id => document.getElementById(id);
const qsa = sel => Array.from(document.querySelectorAll(sel));
function b64EncodeUnicode(str){ return btoa(encodeURIComponent(str).replace(/%([0-9A-F]{2})/g,(m,p)=>String.fromCharCode('0x'+p))); }
function b64DecodeUnicode(str){ return decodeURIComponent(Array.prototype.map.call(atob(str), c => '%' + ('00' + c.charCodeAt(0).toString(16)).slice(-2)).join('')); }
function escapeHtml(s){ return s ? String(s).replaceAll('<','&lt;').replaceAll('>','&gt;') : ''; }
function populateSelect(selectEl, optionsArray, initialValue){
selectEl.innerHTML = '';
optionsArray.forEach((opt, idx) => {
const o=document.createElement('option');
o.value = idx === 0 ? '' : opt;
o.textContent = opt;
selectEl.appendChild(o);
});
if(initialValue) selectEl.value = initialValue;
}
function repopulateSelectMultiple(selectEl, optionsArray, currentValues){
selectEl.innerHTML = optionsArray.map(opt => `<option value="${opt}">${opt}</option>`).join('');
qsa(`#${selectEl.id} option`).forEach(o => {
// Порівнюємо значення (value) або текст (textContent)
if (currentValues.includes(o.value) || currentValues.includes(o.textContent)) {
o.selected = true;
}
});
// Запускаємо перевірку "Інше" після репопуляції
selectEl.dispatchEvent(new Event('change'));
}
function getSelectedValues(selectEl){
return Array.from(selectEl.selectedOptions).map(o=>o.value).filter(v => v !== '');
}


/* Form elements */
const nameEl = el('name'), surnameEl = el('surname'), ageEl = el('age'), addressEl = el('address');
const bloodEl = el('blood'), rhEl = el('rh'), allergyEl = el('allergy'), allergyOtherEl = el('allergyOther');
const diseaseEl = el('disease'), diseaseOtherEl = el('diseaseOther'), medsEl = el('meds');
const sosListEl = el('sosList'), addContactBtn = el('addContactBtn');
const pinEl = el('pin'), pinErrEl = el('pinErr');
const saveBtn = el('saveBtn'), clearBtn = el('clearBtn');
const editBtn = el('editBtn');
const appFooter = el('appFooter');
const formCard = el('formCard');
const themeToggle = el('themeToggle');
const langSwitch = el('langSwitch');
const sosModal = el('sosModal'), closeSos = el('closeSos'), sosModalList = el('sosModalList');
const firstAidModal = el('firstAidModal'), closeFirstAid = el('closeFirstAid'), firstAidVideo = el('firstAidVideo');
const shareSection = el('shareSection');
const copyProfileLinkBtn = el('copyProfileLinkBtn');


/* NEW: Footer update logic */
function updateFooter(isProfileSaved){
const L = I18N[lang];
if(appFooter) appFooter.textContent = isProfileSaved ? L.creationFooter : '';
}

/* ---------- SOS item (Updated with dynamic relations) ---------- */
function createSosItem(data = {name:'', phone:'', relation:'', relationOther:''}){
const L = I18N[lang];
const div = document.createElement('div'); div.className='sosItem';
// Оновлюємо options, щоб вони були коректні для поточної мови
const options = L.relations.map(r=>`<option value="${r}">${r}</option>`).join('');

div.innerHTML = `
<input class="sosName" type="text" placeholder="${L.sosItemPlaceholderName}" value="${escapeHtml(data.name)}">
<input class="sosPhone" type="text" placeholder="${L.sosItemPlaceholderPhone}" value="${escapeHtml(data.phone)}">
<select class="sosRelation">${'<option value="">'+L.sosItemRelation+'</option>' + options}</select>
<button class="removeBtn" title="${L.sosItemRemove}">✖</button>
<input type="text" class="sosRelationOther sosOtherField" placeholder="${L.sosItemPlaceholderOther}" value="${escapeHtml(data.relationOther)}" style="display:none;">
`;

const selectEl = div.querySelector('.sosRelation');
if(data.relation) {
selectEl.value = data.relation;
if(selectEl.value !== data.relation && data.relation !== '') {
const option = Array.from(selectEl.options).find(o => o.textContent === data.relation);
if(option) selectEl.value = option.value;
}
}


// NEW: Logic for "Other" in SOS relations
const otherEl = div.querySelector('.sosRelationOther');
const lastOption = L.relations.slice(-1)[0];

// Ініціалізація видимості при створенні елемента
if (selectEl.value === lastOption && selectEl.value !== '') {
otherEl.style.display = 'block';
}

// Прив'язка обробника подій
selectEl.addEventListener('change', () => {
otherEl.style.display = (selectEl.value === lastOption && selectEl.value !== '') ? 'block' : 'none';
if(otherEl.style.display === 'none') otherEl.value = ''; // Очищаємо, якщо переключили на інше
});

div.querySelector('.removeBtn').addEventListener('click', ()=> div.remove());
return div;
}

/* ---------- Collect profile ---------- */
function collectProfileFromForm(){
const L = I18N[lang];
const lastAllergy = L.allergyOptions.slice(-1)[0];
const lastDisease = L.diseaseOptions.slice(-1)[0];
// const lastRelation = L.relations.slice(-1)[0]; // Не використовується тут

const selectedAllergies = getSelectedValues(allergyEl);
const selectedDiseases = getSelectedValues(diseaseEl);

const profile = {
name: nameEl.value.trim(),
surname: surnameEl.value.trim(),
age: ageEl.value ? Number(ageEl.value) : null,
address: addressEl.value.trim(),
blood: bloodEl.value,
rh: rhEl.value,

allergy: selectedAllergies,
allergyOther: (selectedAllergies.includes(lastAllergy) && allergyOtherEl.value.trim()) ? allergyOtherEl.value.trim() : '',

disease: selectedDiseases,
diseaseOther: (selectedDiseases.includes(lastDisease) && diseaseOtherEl.value.trim()) ? diseaseOtherEl.value.trim() : '',

meds: medsEl.value.trim(),
sos: []
};

qsa('.sosItem').forEach(si=>{
const L = I18N[lang]; // Повторне визначення для доступу до relations
const lastRelation = L.relations.slice(-1)[0];
const name = si.querySelector('.sosName').value.trim();
const phone = si.querySelector('.sosPhone').value.trim();
const relation = si.querySelector('.sosRelation').value;
let relationOther = '';

if (relation === lastRelation) {
const otherInput = si.querySelector('.sosRelationOther');
if (otherInput) relationOther = otherInput.value.trim();
}

if(name && phone) profile.sos.push({name, phone, relation, relationOther});
});
return profile;
}

/* ---------- i18n apply (FULL) ---------- */
function applyLanguage(){
localStorage.setItem('mb_lang', lang);
const L = I18N[lang];

// 1. Зберігаємо поточний стан форми перед реініціалізацією
const currentProfile = collectProfileFromForm();
const isFormVisible = formCard.style.display !== 'none' && !formCard.classList.contains('hidden');

// 2. Оновлення всіх статичних текстів та плейсхолдерів
qsa('[id]').forEach(element => {
const id = element.id;
if (L[id]) element.textContent = L[id];
if (L['lbl' + id.charAt(0).toUpperCase() + id.slice(1)]) {
element.textContent = L['lbl' + id.charAt(0).toUpperCase() + id.slice(1)];
}
if (L['placeholder' + id.charAt(0).toUpperCase() + id.slice(1)] && element.placeholder !== undefined) {
element.placeholder = L['placeholder' + id.charAt(0).toUpperCase() + id.slice(1)];
}
});
// Спеціальні елементи
el('brandSubtitle').textContent = L.brandSubtitle; // ОНОВЛЕНО
el('allergyHint').textContent = L.allergyHint;
el('diseaseHint').textContent = L.diseaseHint;
el('sosHint').textContent = L.sosHint;
el('pinHint').textContent = L.pinHint;
el('firstAidHint').textContent = L.firstAidHint;
el('firstAidModalTitle').textContent = L.firstAidModalTitle;
el('firstAidInfo').innerHTML = L.firstAidInfo;

addContactBtn.textContent = '➕ ' + L.addContact;
saveBtn.textContent = '💾 ' + L.save;
clearBtn.textContent = '🗑 ' + L.clear;
editBtn.textContent = '✏️ ' + L.edit;
el('copyProfileLinkBtn').textContent = L.shareLinkText;
el('openFirstAidModal').textContent = L.firstAidLinkText;
el('sosModalTitle').textContent = L.sosModalTitle;

// 3. Populate select options (blood, rh)
populateSelect(bloodEl, L.bloodOptions, currentProfile.blood);
populateSelect(rhEl, L.rhOptions, currentProfile.rh);

// 4. Repopulate multi-select and restore selection
repopulateSelectMultiple(allergyEl, L.allergyOptions, currentProfile.allergy);
repopulateSelectMultiple(diseaseEl, L.diseaseOptions, currentProfile.disease);
setupOtherToggles();

// 5. Відновлення інших полів форми (текстові)
nameEl.value = currentProfile.name; surnameEl.value = currentProfile.surname;
ageEl.value = currentProfile.age; addressEl.value = currentProfile.address;
medsEl.value = currentProfile.meds; pinEl.value = localStorage.getItem(PIN_KEY) || '';
allergyOtherEl.value = currentProfile.allergyOther; diseaseOtherEl.value = currentProfile.diseaseOther;

// 6. Повне оновлення SOS-контактів з динамічними елементами
sosListEl.innerHTML = '';
(currentProfile.sos || []).forEach(c => sosListEl.appendChild(createSosItem(c)));
if((currentProfile.sos || []).length === 0 && document.querySelectorAll('.sosItem').length === 0) {
sosListEl.appendChild(createSosItem());
}

// 7. Advice list
el('adviceList').innerHTML = `
<li>${L.advice1}</li>
<li>${L.advice2}</li>
<li>${L.advice3}</li>
`;

// 8. Оновлюємо відображення (preview)
updateProfileDisplay();

// 9. Відновлення видимості форми
if(isFormVisible) {
formCard.style.display = 'block';
formCard.classList.remove('hidden');
} else {
formCard.classList.add('hidden');
formCard.style.display = 'none';
}
}

/* ---------- Theme apply (Fixed) ---------- */
function applyTheme(){
localStorage.setItem('mb_theme', theme);
if(theme === 'dark') document.body.classList.add('dark'); else document.body.classList.remove('dark');
el('themeToggle').textContent = theme === 'dark' ? '☀️' : '🌙';
}

/* ---------- Show public profile ---------- */
function showPublicProfile(profile, readonly=false){
// ... (логіка відображення профілю коректна)
const L = I18N[lang];

if(!profile || !profile.name && !profile.surname && !profile.age){
el('previewName').textContent = L.previewNotCreated;
el('previewSub').textContent = L.previewSubHint;
el('avatar').textContent = 'MB';
el('bloodBadge').style.display = 'none';
el('infoList').innerHTML = '';
el('sosPreview').innerHTML = `<div class="muted">${L.noSos}</div>`;
el('editBtn').style.display = 'none';
el('firstAidCard').style.display = 'block';
updateFooter(false);
return;
}

const fullName = `${profile.name || ''} ${profile.surname || ''}`.trim();
el('previewName').textContent = fullName;
el('previewSub').textContent = profile.age ? `${profile.age} ${L.ageUnits}` : L.previewSubHint;
el('avatar').textContent = ((profile.name||'').charAt(0)||'M') + ((profile.surname||'').charAt(0)||'B');

if(profile.blood){ el('bloodBadge').style.display='inline-block'; el('bloodBadge').textContent = `${profile.blood}${profile.rh ? ' • ' + profile.rh : ''}`; } else el('bloodBadge').style.display='none';

el('infoList').innerHTML = '';

const lastAllergy = L.allergyOptions.slice(-1)[0];
const lastDisease = L.diseaseOptions.slice(-1)[0];

const allergiesDisplay = (profile.allergy || [])
.filter(v => !(v === lastAllergy && profile.allergyOther))
.concat(profile.allergyOther ? profile.allergyOther : [])
.filter(Boolean)
.join(', ');

const diseasesDisplay = (profile.disease || [])
.filter(v => !(v === lastDisease && profile.diseaseOther))
.concat(profile.diseaseOther ? profile.diseaseOther : [])
.filter(Boolean)
.join(', ');

const infoRows = [
{k: L.labelAddress, v: profile.address},
{k: L.labelAllergy, v: allergiesDisplay},
{k: L.labelDisease, v: diseasesDisplay},
{k: L.labelMeds, v: profile.meds}
];

infoRows.forEach(r=>{
if(r.v){
const d = document.createElement('div'); d.className='infoItem';
const keyText = r.k.replace(' (місто)', '').replace(' (city)', '');
d.innerHTML = `<div>${escapeHtml(keyText)}</div><div>${escapeHtml(String(r.v))}</div>`;
el('infoList').appendChild(d);
}
});

el('sosPreview').innerHTML = '';
if(profile.sos && profile.sos.length){
const lastRelation = L.relations.slice(-1)[0];
profile.sos.forEach(c=>{
const a = document.createElement('a');
a.href = 'tel:' + encodeURIComponent(c.phone);

let relationDisplay = c.relation;
if (c.relation === lastRelation && c.relationOther) {
relationDisplay = c.relationOther;
} else if (c.relation) {
relationDisplay = c.relation;
} else {
relationDisplay = '';
}
const nameText = `${c.name}${relationDisplay ? ' (' + relationDisplay + ')' : ''}`;
a.innerHTML = `<span>${escapeHtml(nameText)}</span><span class="number">${escapeHtml(c.phone)}</span>`;
el('sosPreview').appendChild(a);
});
} else {
const p = document.createElement('div'); p.className='muted'; p.textContent = L.noSos; el('sosPreview').appendChild(p);
}

// КРИТИЧНЕ ВИПРАВЛЕННЯ: Кнопка редагування буде керуватися в updateProfileDisplay
el('editBtn').style.display = 'none';
el('firstAidCard').style.display = 'block';
updateFooter(true);
}


/* ---------- Hide Form when in public (read-only) mode - UPDATED LOGIC ---------- */
function handlePublicMode(isPublic) {
const raw = localStorage.getItem(PROFILE_KEY);

if (isPublic) {
formCard.classList.add('hidden');
formCard.style.display = 'none';
shareSection.style.display = 'none';

// Кнопка "Редагувати" видима, тільки якщо є локальний профіль (тобто це власник)
el('editBtn').style.display = raw ? 'inline-block' : 'none';
} else {
// Локальний режим
formCard.classList.remove('hidden');
formCard.style.display = 'block';
shareSection.style.display = raw ? 'block' : 'none';
el('editBtn').style.display = raw ? 'inline-block' : 'none';
}
}


/* ---------- Update profile display (Вся логіка визначення режиму тут) ---------- */
function updateProfileDisplay(){
const raw = localStorage.getItem(PROFILE_KEY);
const profile = raw ? JSON.parse(raw) : null;
let isPublicMode = false;

if(location.hash && location.hash.startsWith('#profile=')){
try{
const decoded = b64DecodeUnicode(location.hash.replace('#profile=',''));
const hashProfile = JSON.parse(decoded);
showPublicProfile(hashProfile, true); // Відображаємо тільки для читання (readonly=true)
isPublicMode = true;
} catch(e) { /* ignore */ }
}

if (isPublicMode) {
handlePublicMode(true);
return;
}

// Локальний режим (з можливістю редагування)
if (profile) {
showPublicProfile(profile, false);
} else {
showPublicProfile(null, false);
}
handlePublicMode(false);
}


/* ---------- Save profile (показуємо кнопку Share після збереження) ---------- */
function saveProfile(){
const L = I18N[lang];
const profile = collectProfileFromForm();

if(!profile.name && !profile.surname){ alert(L.alertName); return; }
if(!profile.sos || profile.sos.length === 0){ if(!confirm(L.alertSos)) return; }
const pinVal = pinEl.value.trim();
if(pinVal && !/^\d{4,8}$/i.test(pinVal)){ pinErrEl.style.display='block'; pinErrEl.textContent = L.alertPin; return; }
pinErrEl.style.display='none';

if(pinVal) localStorage.setItem(PIN_KEY, pinVal);

localStorage.setItem(PROFILE_KEY, JSON.stringify(profile));
updateProfileDisplay();

// Анімація зникнення форми
formCard.classList.add('hidden');
setTimeout(() => formCard.style.display = 'none', 500);

saveBtn.textContent = L.saved;
setTimeout(()=> saveBtn.textContent = '💾 ' + L.save, 1400);

// Додатково: переконатися, що кнопки "Поділитись" та "Редагувати" тепер видимі
shareSection.style.display = 'block';
el('editBtn').style.display = 'inline-block';
}

/* ---------- Clear ---------- */
function clearProfile(){
const L = I18N[lang];
if(!confirm(L.confirmClear)) return;
localStorage.removeItem(PROFILE_KEY);
localStorage.removeItem(PIN_KEY);
resetForm();
updateProfileDisplay();

// Приховуємо кнопки після очищення
shareSection.style.display = 'none';
el('editBtn').style.display = 'none';

// Анімація появи форми
formCard.style.display = 'block';
setTimeout(() => formCard.classList.remove('hidden'), 10);
}

/* ---------- Reset form (заповнює форму порожніми значеннями) ---------- */
function resetForm(){
[nameEl,surnameEl,ageEl,addressEl,medsEl,pinEl].forEach(i=>i.value='');
if(bloodEl.options.length > 0) bloodEl.selectedIndex = 0;
if(rhEl.options.length > 0) rhEl.selectedIndex = 0;
qsa('#allergy option').forEach(o=>o.selected=false); allergyOtherEl.value = ''; allergyOtherEl.style.display = 'none';
qsa('#disease option').forEach(o=>o.selected=false); diseaseOtherEl.value = ''; diseaseOtherEl.style.display = 'none';
sosListEl.innerHTML = '';
sosListEl.appendChild(createSosItem());
setupOtherToggles();
}

/* ---------- Load on start / Edit mode logic (ОНОВЛЕНО) ---------- */
function requestEdit(profileFromLoad = null, checkPin = true){
const L = I18N[lang];
const storedPin = localStorage.getItem(PIN_KEY);
const raw = localStorage.getItem(PROFILE_KEY);

// 1. ПЕРЕВІРКА НАЯВНОСТІ ЛОКАЛЬНОГО ПРОФІЛЮ
if(!raw) {
// Якщо відкрили публічне посилання, але локального профілю нема - це стороння особа.
if(location.hash && location.hash.startsWith('#profile=')) return;

resetForm();
formCard.style.display = 'block';
formCard.classList.remove('hidden');
return;
}

// 2. ПЕРЕВІРКА PIN-КОДУ (якщо встановлено)
if(checkPin && storedPin){
const entered = prompt(L.enterPin);
if(entered === null) return;
if(entered !== storedPin){ alert(L.pinWrong); return; }
}

// 3. ЗАВАНТАЖЕННЯ ДАНИХ (Завжди з локального сховища)
const profile = JSON.parse(raw);

// Repopulate form
nameEl.value = profile.name || ''; surnameEl.value = profile.surname || '';
ageEl.value = profile.age || ''; addressEl.value = profile.address || '';
medsEl.value = profile.meds || ''; pinEl.value = localStorage.getItem(PIN_KEY) || '';

bloodEl.value = profile.blood || ''; rhEl.value = profile.rh || '';

allergyOtherEl.value = profile.allergyOther || '';
diseaseOtherEl.value = profile.diseaseOther || '';

// Sos
sosListEl.innerHTML = '';
(profile.sos || []).forEach(c => sosListEl.appendChild(createSosItem(c)));
if((profile.sos || []).length === 0) sosListEl.appendChild(createSosItem());

// Repopulate select-multiple
repopulateSelectMultiple(allergyEl, L.allergyOptions, profile.allergy || []);
repopulateSelectMultiple(diseaseEl, L.diseaseOptions, profile.disease || []);
setupOtherToggles();

// Анімація появи форми
formCard.style.display = 'block';
setTimeout(() => formCard.classList.remove('hidden'), 10);

// Очищуємо хеш, щоб повернутися в локальний режим, якщо він був
if(location.hash) window.history.replaceState(null, null, window.location.pathname + window.location.search);

// Оновлюємо відображення
updateProfileDisplay();
}

/* ---------- 'Other' toggles (Оптимізована логіка) ---------- */
function setupOtherToggles(){
const checkOther = (selectEl, otherEl, optionsList) => {
const lastOption = optionsList.slice(-1)[0];
const isOtherSelected = Array.from(selectEl.selectedOptions).some(o => o.value === lastOption || o.textContent === lastOption);

otherEl.style.display = isOtherSelected ? 'block' : 'none';
if (otherEl.style.display === 'none') otherEl.value = '';
};

// Прив'язка для алергій
function allergyChangeListener(){
checkOther(allergyEl, allergyOtherEl, I18N[lang].allergyOptions);
}
allergyEl.removeEventListener('change', allergyChangeListener);
allergyEl.addEventListener('change', allergyChangeListener);

// Прив'язка для хвороб
function diseaseChangeListener(){
checkOther(diseaseEl, diseaseOtherEl, I18N[lang].diseaseOptions);
}
diseaseEl.removeEventListener('change', diseaseChangeListener);
diseaseEl.addEventListener('change', diseaseChangeListener);

allergyEl.dispatchEvent(new Event('change'));
diseaseEl.dispatchEvent(new Event('change'));
}

/* ---------- Modal functions ---------- */
function openModal(modalEl) {
modalEl.style.display = 'flex';
setTimeout(() => modalEl.classList.add('show'), 10);
modalEl.setAttribute('aria-hidden', 'false');
}

function closeModal(modalEl) {
modalEl.classList.remove('show');
setTimeout(() => modalEl.style.display = 'none', 300);
modalEl.setAttribute('aria-hidden', 'true');
}

function openSosModal(){
const L = I18N[lang];
let profile = null;
if(location.hash && location.hash.startsWith('#profile=')){
try{ profile = JSON.parse(b64DecodeUnicode(location.hash.replace('#profile=',''))); } catch(e) { /* ignore */ }
} else {
profile = localStorage.getItem(PROFILE_KEY) ? JSON.parse(localStorage.getItem(PROFILE_KEY)) : null;
}

sosModalList.innerHTML = '';
const lastRelation = L.relations.slice(-1)[0];

if(!profile || !profile.sos || profile.sos.length === 0){
const li = document.createElement('li'); li.textContent = L.noSos; sosModalList.appendChild(li);
} else {
profile.sos.forEach(c=>{
const li = document.createElement('li');
const a = document.createElement('a');
a.href = 'tel:' + encodeURIComponent(c.phone);

let relationDisplay = c.relation;
if (c.relation === lastRelation && c.relationOther) {
relationDisplay = c.relationOther;
} else if (c.relation) {
relationDisplay = c.relation;
} else {
relationDisplay = '';
}

const relationText = relationDisplay ? ` (${relationDisplay})` : '';
a.textContent = `${c.name}${relationText} — ${c.phone}`;
a.style.display='block'; a.style.padding='8px 0'; a.style.color='inherit'; a.style.textDecoration='none';
a.style.fontWeight = 'bold';
li.appendChild(a); sosModalList.appendChild(li);
});
}
openModal(sosModal);
}

function closeSosModal(){ closeModal(sosModal); }

function openFirstAid(){
const videoId = I18N[lang].firstAidVideoId;
firstAidVideo.src = `https://www.youtube.com/embed/${videoId}?autoplay=1&rel=0`;
openModal(firstAidModal);
}

function closeFirstAidModal(){
firstAidVideo.src = '';
closeModal(firstAidModal);
}

/* ---------- Generate and Share Link (NEW) ---------- */
function generateProfileLink(){
const raw = localStorage.getItem(PROFILE_KEY);
if(!raw) return null;

try {
const encoded = b64EncodeUnicode(raw);
const baseUrl = window.location.href.split('#')[0];
return `${baseUrl}#profile=${encoded}`;
} catch(e) {
console.error('Failed to generate profile link:', e);
return null;
}
}

async function shareProfileLink(){
const L = I18N[lang];
const link = generateProfileLink();
const profile = localStorage.getItem(PROFILE_KEY) ? JSON.parse(localStorage.getItem(PROFILE_KEY)) : null;

if(!link){
alert(L.alertNoProfile);
return;
}

// 1. Спроба використовувати нативний Web Share API
if (navigator.share) {
const fullName = `${profile.name || ''} ${profile.surname || ''}`.trim() || 'Медичний Профіль';
try {
await navigator.share({
title: `${fullName} | MED-BRASLET`,
text: `Мій медичний профіль. Ця інформація може допомогти в екстреній ситуації.`,
url: link,
});
return;
} catch (error) {
console.log('Web Share API failed or cancelled. Proceeding to copy:', error);
}
}

// 2. Копіювання в буфер
try {
await navigator.clipboard.writeText(link);
const btn = el('copyProfileLinkBtn');
const originalText = btn.textContent;
btn.textContent = L.linkCopied;
setTimeout(() => { btn.textContent = originalText; }, 1500);
} catch(err) {
console.error('Failed to copy link:', err);
prompt('Скопіюйте посилання вручну (Ctrl+C):', link);
}
}


/* ---------- Event Listeners (Fixed) ---------- */
langSwitch.value = lang;
langSwitch.addEventListener('change', (e)=> {
lang = e.target.value;
applyLanguage();
});

themeToggle.addEventListener('click', ()=> {
theme = (theme==='dark' ? 'light' : 'dark');
applyTheme();
});

addContactBtn.addEventListener('click', ()=> {
if(document.querySelectorAll('.sosItem').length >= 6){ alert(I18N[lang].alertMaxSos); return; }
sosListEl.appendChild(createSosItem());
});

saveBtn.addEventListener('click', saveProfile);
clearBtn.addEventListener('click', clearProfile);
el('editBtn').addEventListener('click', () => requestEdit(null, true));
el('sosBtn').addEventListener('click', openSosModal);
copyProfileLinkBtn.addEventListener('click', shareProfileLink);
closeSos.addEventListener('click', closeSosModal);
el('openFirstAidModal').addEventListener('click', openFirstAid);
closeFirstAid.addEventListener('click', closeFirstAidModal);

window.addEventListener('click', (e)=> {
if(e.target === sosModal){ closeSosModal(); }
if(e.target === firstAidModal){ closeFirstAidModal(); }
});


/* ---------- Init ---------- */
(function init(){
applyTheme();
applyLanguage();

// КОРЕКТНО ВИЗНАЧАЄМО ПОЧАТКОВИЙ РЕЖИМ ПІСЛЯ ЗАВАНТАЖЕННЯ ДАНИХ
if (location.hash && location.hash.startsWith('#profile=')) {
// Якщо відкрили публічне посилання
handlePublicMode(true);
} else if (localStorage.getItem(PROFILE_KEY)) {
// Якщо є локальний профіль, але це не публічне посилання - приховуємо форму
formCard.classList.add('hidden');
formCard.style.display = 'none';
}
})();
</script>
</body>
</html>
