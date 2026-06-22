!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Besichtigungstermine</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&family=Playfair+Display:wght@500&display=swap');
 
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
 
  :root {
    --bg: #F7F6F2;
    --white: #FFFFFF;
    --ink: #1C1C1A;
    --ink-light: #6B6B62;
    --accent: #8B6F47;
    --accent-light: #F0E9DE;
    --green: #3A7D5A;
    --green-light: #E6F2EC;
    --red: #C0392B;
    --red-light: #FDECEA;
    --border: #E0DDD6;
    --radius: 10px;
    --shadow: 0 2px 12px rgba(0,0,0,0.07);
  }
 
  body {
    font-family: 'Inter', sans-serif;
    background: var(--bg);
    color: var(--ink);
    min-height: 100vh;
  }
 
  /* ── Navigation ── */
  .nav {
    background: var(--white);
    border-bottom: 1px solid var(--border);
    padding: 0 24px;
    display: flex;
    align-items: center;
    position: sticky;
    top: 0;
    z-index: 100;
  }
 
  .nav-brand {
    font-family: 'Playfair Display', serif;
    font-size: 17px;
    color: var(--accent);
    padding: 16px 0;
    flex: 1;
    letter-spacing: 0.01em;
  }
 
  /* Admin-Tab ist standardmäßig versteckt */
  #tabAdmin { display: none; }
 
  .nav-tabs { display: flex; }
 
  .tab-btn {
    padding: 18px 20px;
    border: none;
    background: none;
    font-family: 'Inter', sans-serif;
    font-size: 13px;
    font-weight: 500;
    color: var(--ink-light);
    cursor: pointer;
    border-bottom: 2px solid transparent;
    transition: all 0.15s;
    letter-spacing: 0.02em;
    text-transform: uppercase;
  }
 
  .tab-btn:hover { color: var(--accent); }
  .tab-btn.active { color: var(--accent); border-bottom-color: var(--accent); }
 
  /* ── Pages ── */
  .page { display: none; }
  .page.active { display: block; }
 
  /* ── Layout ── */
  .container {
    max-width: 720px;
    margin: 0 auto;
    padding: 36px 24px 60px;
  }
 
  .page-title {
    font-family: 'Playfair Display', serif;
    font-size: 26px;
    font-weight: 500;
    color: var(--ink);
    margin-bottom: 6px;
  }
 
  .page-sub {
    font-size: 13px;
    color: var(--ink-light);
    margin-bottom: 32px;
    line-height: 1.5;
  }
 
  /* ── Cards ── */
  .card {
    background: var(--white);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 24px;
    box-shadow: var(--shadow);
    margin-bottom: 16px;
  }
 
  .card-title {
    font-size: 13px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--ink-light);
    margin-bottom: 18px;
  }
 
  /* ── Form ── */
  .form-group {
    display: flex;
    flex-direction: column;
    gap: 6px;
  }
 
  label {
    font-size: 12px;
    font-weight: 500;
    color: var(--ink-light);
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }
 
  input[type="text"],
  input[type="email"] {
    padding: 10px 13px;
    border: 1px solid var(--border);
    border-radius: 7px;
    font-family: 'Inter', sans-serif;
    font-size: 14px;
    color: var(--ink);
    background: var(--bg);
    outline: none;
    transition: border-color 0.15s;
  }
 
  input:focus { border-color: var(--accent); background: var(--white); }
  input.error { border-color: var(--red); }
 
  .field-error {
    font-size: 11px;
    color: var(--red);
    margin-top: 2px;
    min-height: 14px;
  }
 
  .btn {
    padding: 11px 22px;
    border: none;
    border-radius: 7px;
    font-family: 'Inter', sans-serif;
    font-size: 13px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.15s;
    letter-spacing: 0.02em;
  }
 
  .btn-primary { background: var(--accent); color: var(--white); }
  .btn-primary:hover { background: #7a5e38; }
 
  .btn-full { width: 100%; margin-top: 8px; }
 
  /* ── Slot items (Admin) ── */
  .slot-list { display: flex; flex-direction: column; gap: 10px; }
 
  .slot-item {
    display: flex;
    align-items: center;
    gap: 14px;
    padding: 14px 16px;
    border-radius: 8px;
    border: 1px solid var(--border);
    background: var(--white);
  }
 
  .slot-dot {
    width: 9px; height: 9px;
    border-radius: 50%;
    flex-shrink: 0;
    background: var(--green);
  }
 
  .slot-info { flex: 1; min-width: 0; }
 
  .slot-datetime { font-size: 14px; font-weight: 500; color: var(--ink); }
 
  .slot-badge {
    font-size: 11px;
    font-weight: 600;
    padding: 4px 10px;
    border-radius: 20px;
    letter-spacing: 0.03em;
    white-space: nowrap;
  }
 
  .badge-free { background: var(--green-light); color: var(--green); }
 
  .empty-state {
    text-align: center;
    padding: 40px 20px;
    color: var(--ink-light);
    font-size: 14px;
  }
  .empty-state .icon { font-size: 32px; margin-bottom: 10px; }
 
  /* ── Visitor slots ── */
  .visitor-slots { display: flex; flex-direction: column; gap: 10px; }
 
  .visitor-slot {
    display: flex;
    align-items: center;
    gap: 14px;
    padding: 16px 18px;
    border-radius: 8px;
    border: 1.5px solid var(--border);
    background: var(--white);
    transition: all 0.15s;
  }
 
  .visitor-slot:hover {
    border-color: var(--accent);
    transform: translateY(-1px);
    box-shadow: 0 4px 14px rgba(139,111,71,0.12);
  }
 
  .visitor-slot .slot-datetime { font-size: 15px; }
 
  .btn-book {
    margin-left: auto;
    padding: 8px 18px;
    border-radius: 6px;
    font-size: 12px;
    font-weight: 600;
    background: var(--accent);
    color: var(--white);
    border: none;
    cursor: pointer;
    transition: background 0.15s;
    white-space: nowrap;
  }
  .btn-book:hover { background: #7a5e38; }
 
  /* ── Modal ── */
  .modal-overlay {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.4);
    z-index: 200;
    align-items: center;
    justify-content: center;
    padding: 24px;
  }
  .modal-overlay.open { display: flex; }
 
  .modal {
    background: var(--white);
    border-radius: 14px;
    padding: 32px;
    max-width: 460px;
    width: 100%;
    box-shadow: 0 20px 50px rgba(0,0,0,0.15);
  }
 
  .modal-title {
    font-family: 'Playfair Display', serif;
    font-size: 20px;
    margin-bottom: 6px;
  }
 
  .modal-sub {
    font-size: 13px;
    color: var(--ink-light);
    margin-bottom: 22px;
  }
 
  .modal-slot-info {
    background: var(--accent-light);
    border-radius: 8px;
    padding: 12px 16px;
    font-size: 14px;
    font-weight: 500;
    color: var(--accent);
    margin-bottom: 20px;
  }
 
  .modal-form { display: flex; flex-direction: column; gap: 14px; }
 
  .modal-actions {
    display: flex;
    gap: 10px;
    margin-top: 8px;
  }
 
  .btn-cancel {
    flex: 1;
    padding: 11px;
    background: none;
    border: 1px solid var(--border);
    border-radius: 7px;
    font-family: 'Inter', sans-serif;
    font-size: 13px;
    font-weight: 500;
    cursor: pointer;
    color: var(--ink-light);
    transition: all 0.15s;
  }
  .btn-cancel:hover { background: var(--bg); }
 
  .btn-confirm {
    flex: 2;
    padding: 11px;
    background: var(--accent);
    color: var(--white);
    border: none;
    border-radius: 7px;
    font-family: 'Inter', sans-serif;
    font-size: 13px;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.15s;
  }
  .btn-confirm:hover { background: #7a5e38; }
 
  /* ── Object badge ── */
  .object-badge {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    font-size: 12px;
    color: var(--ink-light);
    background: var(--white);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 5px 12px;
    margin-bottom: 24px;
  }
  .object-dot { width: 6px; height: 6px; background: var(--accent); border-radius: 50%; }
 
  /* ── Hinweis-Box ── */
  .info-note {
    background: var(--accent-light);
    border-radius: 8px;
    padding: 14px 16px;
    font-size: 12.5px;
    color: var(--ink-light);
    line-height: 1.55;
    margin-bottom: 24px;
  }
 
  /* ── PIN overlay ── */
  .pin-overlay {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.55);
    z-index: 300;
    align-items: center;
    justify-content: center;
    padding: 24px;
    backdrop-filter: blur(3px);
  }
  .pin-overlay.open { display: flex; }
 
  .pin-box {
    background: var(--white);
    border-radius: 14px;
    padding: 40px 36px;
    max-width: 340px;
    width: 100%;
    border: 1px solid var(--border);
    box-shadow: 0 20px 50px rgba(0,0,0,0.18);
    text-align: center;
  }
 
  .pin-title {
    font-family: 'Playfair Display', serif;
    font-size: 22px;
    margin-bottom: 8px;
  }
 
  .pin-sub {
    font-size: 13px;
    color: var(--ink-light);
    margin-bottom: 24px;
    line-height: 1.5;
  }
 
  .pin-input {
    width: 100%;
    text-align: center;
    font-size: 28px;
    letter-spacing: 10px;
    padding: 14px;
    border: 1.5px solid var(--border);
    border-radius: 8px;
    font-family: 'Inter', sans-serif;
    margin-bottom: 8px;
    outline: none;
    background: var(--bg);
  }
  .pin-input:focus { border-color: var(--accent); background: var(--white); }
 
  .pin-error {
    color: var(--red);
    font-size: 12px;
    margin-bottom: 12px;
    min-height: 16px;
  }
 
  /* admin mode indicator */
  .admin-indicator {
    display: none;
    align-items: center;
    gap: 6px;
    font-size: 11px;
    color: var(--accent);
    background: var(--accent-light);
    border-radius: 20px;
    padding: 4px 12px;
    margin-right: 12px;
  }
  .admin-indicator.show { display: flex; }
  .admin-indicator-dot {
    width: 5px; height: 5px;
    background: var(--accent);
    border-radius: 50%;
  }
 
  @media (max-width: 520px) {
    .stat-num { font-size: 20px; }
    .modal { padding: 24px; }
  }
</style>
</head>
<body>
 
<!-- ════════════════════════════════════════════════════════════════
     HIER DEINE TERMINE EINTRAGEN
     ────────────────────────────────────────────────────────────────
     Trage unten deine Besichtigungstermine ein. Jeder Termin steht in
     einer Zeile zwischen { } :
        { date: "JAHR-MONAT-TAG", time: "STUNDE:MINUTE" }
     Beispiel:
        { date: "2026-06-28", time: "18:00" },
     Termine, die vorbei sind, werden automatisch ausgeblendet.
     Zum Ändern: Datei bei GitHub bearbeiten und neu speichern.
     ════════════════════════════════════════════════════════════════ -->
<script>
  const TERMINE = [
    { date: "2026-06-28", time: "18:00" },
    { date: "2026-06-29", time: "17:30" },
    { date: "2026-07-02", time: "18:30" },
  ];
 
  // Empfänger der Buchungsanfragen (deine E-Mail):
  const KONTAKT_EMAIL = "werner.lars94@googlemail.com";
 
  // Admin-Zugang:
  const ADMIN_PIN  = '1234';     // ← hier deinen PIN setzen
  const ADMIN_PARAM = 'admin';   // Admin-URL:  ...?admin
</script>
 
<!-- PIN Overlay — nur sichtbar wenn ?admin in URL -->
<div class="pin-overlay" id="pinOverlay">
  <div class="pin-box">
    <div class="pin-title">Admin-Zugang</div>
    <div class="pin-sub">Bitte PIN eingeben, um<br>die Terminübersicht zu sehen</div>
    <input class="pin-input" type="password" id="pinInput" maxlength="4" placeholder="····" inputmode="numeric" autocomplete="off">
    <div class="pin-error" id="pinError"></div>
    <button class="btn btn-primary btn-full" onclick="checkPin()">Weiter</button>
    <div style="margin-top: 14px;">
      <button class="btn" style="background:none;color:var(--ink-light);font-size:12px;" onclick="closePinOverlay()">Abbrechen</button>
    </div>
  </div>
</div>
 
<!-- Booking Modal -->
<div class="modal-overlay" id="bookingModal">
  <div class="modal">
    <div class="modal-title">Termin anfragen</div>
    <div class="modal-sub">Bitte alle Felder ausfüllen. Beim Absenden öffnet sich dein E-Mail-Programm mit einer vorausgefüllten Nachricht — du musst sie nur noch abschicken.</div>
    <div class="modal-slot-info" id="modalSlotInfo"></div>
    <div class="modal-form">
      <div class="form-group">
        <label>Vor- und Nachname *</label>
        <input type="text" id="bookName" placeholder="z.B. Anna Müller" autocomplete="name">
        <div class="field-error" id="errName"></div>
      </div>
      <div class="form-group">
        <label>Telefon *</label>
        <input type="text" id="bookPhone" placeholder="z.B. 0711 123456" autocomplete="tel">
        <div class="field-error" id="errPhone"></div>
      </div>
      <div class="form-group">
        <label>E-Mail-Adresse *</label>
        <input type="email" id="bookEmail" placeholder="z.B. anna@beispiel.de" autocomplete="email">
        <div class="field-error" id="errEmail"></div>
      </div>
    </div>
    <div class="modal-actions" style="margin-top: 20px;">
      <button class="btn-cancel" onclick="closeModal()">Abbrechen</button>
      <button class="btn-confirm" onclick="confirmBooking()">Anfrage per E-Mail senden</button>
    </div>
  </div>
</div>
 
<!-- Nav -->
<nav class="nav">
  <div class="nav-brand">Wohnungsbesichtigung</div>
  <div class="admin-indicator" id="adminIndicator">
    <div class="admin-indicator-dot"></div>
    Admin
  </div>
  <div class="nav-tabs">
    <button class="tab-btn" id="tabAdmin" onclick="showPage('admin')">Verwaltung</button>
    <button class="tab-btn active" id="tabVisitor" onclick="showPage('visitor')">Termine</button>
  </div>
</nav>
 
<!-- ADMIN PAGE -->
<div class="page" id="pageAdmin">
  <div class="container">
    <h1 class="page-title">Terminübersicht</h1>
    <p class="page-sub">Das sind die aktuell eingetragenen Termine. Buchungsanfragen erhältst du per E-Mail. Termine änderst du, indem du die Datei bei GitHub bearbeitest.</p>
 
    <div class="object-badge">
      <div class="object-dot"></div>
      Dornhaldenstr. 14/1 · Stuttgart-Süd · 59 m²
    </div>
 
    <div class="info-note">
      <strong>So fügst du Termine hinzu oder entfernst sie:</strong><br>
      Öffne die Datei <code>index.html</code> in deinem GitHub-Repo, klicke auf den Stift (Bearbeiten) und passe die Liste <code>TERMINE</code> oben in der Datei an. Speichern („Commit changes") — die Seite aktualisiert sich nach kurzer Zeit von selbst.<br><br>
      Buchungsanfragen kommen an: <strong id="adminEmail"></strong>
    </div>
 
    <div class="card">
      <div class="card-title">Eingetragene Termine</div>
      <div class="slot-list" id="adminSlotList">
        <div class="empty-state">
          <div class="icon">🗓</div>
          Keine (kommenden) Termine eingetragen.
        </div>
      </div>
    </div>
  </div>
</div>
 
<!-- VISITOR PAGE -->
<div class="page active" id="pageVisitor">
  <div class="container">
    <h1 class="page-title">Besichtigungstermine</h1>
    <p class="page-sub">Wähle einen Termin und sende uns kurz deine Daten. Wir bestätigen dir den Termin und melden uns kurz vorher.</p>
 
    <div class="object-badge">
      <div class="object-dot"></div>
      Dornhaldenstr. 14/1 · Stuttgart-Süd · 59 m² · 2-Zimmer-Altbau
    </div>
 
    <div class="visitor-slots" id="visitorSlotList">
      <div class="empty-state">
        <div class="icon">🕐</div>
        Aktuell sind keine Termine verfügbar.<br>Bitte später nochmal schauen.
      </div>
    </div>
  </div>
</div>
 
<script>
  // ── State ──
  let selectedSlotIndex = null;
  let isAdmin = false;
 
  // Nur kommende Termine, chronologisch sortiert
  function activeSlots() {
    const now = new Date();
    return TERMINE
      .map((t, i) => ({ ...t, _i: i }))
      .filter(t => new Date(t.date + 'T' + (t.time || '00:00')) >= now)
      .sort((a, b) => (a.date + a.time).localeCompare(b.date + b.time));
  }
 
  // ── URL prüfen beim Start ──
  function init() {
    document.getElementById('adminEmail').textContent = KONTAKT_EMAIL;
    const params = new URLSearchParams(window.location.search);
    if (params.has(ADMIN_PARAM)) {
      document.getElementById('pinOverlay').classList.add('open');
      setTimeout(() => document.getElementById('pinInput').focus(), 200);
    }
    showPage('visitor');
    renderVisitor();
  }
 
  // ── PIN ──
  function checkPin() {
    const val = document.getElementById('pinInput').value;
    if (val === ADMIN_PIN) {
      document.getElementById('pinOverlay').classList.remove('open');
      document.getElementById('pinInput').value = '';
      document.getElementById('pinError').textContent = '';
      unlockAdmin();
    } else {
      document.getElementById('pinError').textContent = 'Falscher PIN — bitte erneut versuchen.';
      document.getElementById('pinInput').value = '';
      document.getElementById('pinInput').focus();
    }
  }
 
  function closePinOverlay() {
    document.getElementById('pinOverlay').classList.remove('open');
    document.getElementById('pinInput').value = '';
    document.getElementById('pinError').textContent = '';
  }
 
  document.getElementById('pinInput').addEventListener('keydown', e => {
    if (e.key === 'Enter') checkPin();
  });
 
  function unlockAdmin() {
    isAdmin = true;
    document.getElementById('tabAdmin').style.display = '';
    document.getElementById('adminIndicator').classList.add('show');
    showPage('admin');
    renderAdmin();
  }
 
  // ── Navigation ──
  function showPage(which) {
    document.getElementById('pageAdmin').classList.toggle('active', which === 'admin');
    document.getElementById('pageVisitor').classList.toggle('active', which === 'visitor');
    document.getElementById('tabAdmin').classList.toggle('active', which === 'admin');
    document.getElementById('tabVisitor').classList.toggle('active', which === 'visitor');
  }
 
  // ── Helpers ──
  function formatDate(dateStr) {
    const d = new Date(dateStr + 'T00:00:00');
    return d.toLocaleDateString('de-DE', { weekday: 'short', day: '2-digit', month: '2-digit', year: 'numeric' });
  }
 
  function formatSlot(s) {
    return `${formatDate(s.date)}, ${s.time} Uhr`;
  }
 
  function isValidEmail(email) {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
  }
 
  // ── Admin (Übersicht der definierten Termine) ──
  function renderAdmin() {
    const list = document.getElementById('adminSlotList');
    const slots = activeSlots();
    if (!slots.length) {
      list.innerHTML = `<div class="empty-state"><div class="icon">🗓</div>Keine (kommenden) Termine eingetragen.</div>`;
      return;
    }
    list.innerHTML = slots.map(s => `
      <div class="slot-item">
        <div class="slot-dot"></div>
        <div class="slot-info">
          <div class="slot-datetime">${formatSlot(s)}</div>
        </div>
        <span class="slot-badge badge-free">Verfügbar</span>
      </div>
    `).join('');
  }
 
  // ── Visitor ──
  function renderVisitor() {
    const list = document.getElementById('visitorSlotList');
    const slots = activeSlots();
    if (!slots.length) {
      list.innerHTML = `<div class="empty-state"><div class="icon">🕐</div>Aktuell sind keine Termine verfügbar.<br>Bitte später nochmal schauen.</div>`;
      return;
    }
    list.innerHTML = slots.map(s => `
      <div class="visitor-slot">
        <div class="slot-dot"></div>
        <div class="slot-info">
          <div class="slot-datetime">${formatSlot(s)}</div>
        </div>
        <button class="btn-book" onclick="openModal(${s._i})">Anfragen</button>
      </div>
    `).join('');
  }
 
  // ── Modal ──
  function openModal(index) {
    selectedSlotIndex = index;
    const s = TERMINE[index];
    document.getElementById('modalSlotInfo').textContent = formatSlot(s);
    ['bookName','bookPhone','bookEmail'].forEach(f => {
      document.getElementById(f).value = '';
      document.getElementById(f).classList.remove('error');
    });
    ['errName','errPhone','errEmail'].forEach(f => document.getElementById(f).textContent = '');
    document.getElementById('bookingModal').classList.add('open');
    setTimeout(() => document.getElementById('bookName').focus(), 100);
  }
 
  function closeModal() {
    document.getElementById('bookingModal').classList.remove('open');
    selectedSlotIndex = null;
  }
 
  function confirmBooking() {
    const name  = document.getElementById('bookName').value.trim();
    const phone = document.getElementById('bookPhone').value.trim();
    const email = document.getElementById('bookEmail').value.trim();
 
    let valid = true;
 
    if (!name) {
      document.getElementById('errName').textContent = 'Bitte Namen eingeben.';
      document.getElementById('bookName').classList.add('error');
      valid = false;
    } else {
      document.getElementById('errName').textContent = '';
      document.getElementById('bookName').classList.remove('error');
    }
 
    if (!phone) {
      document.getElementById('errPhone').textContent = 'Bitte Telefonnummer eingeben.';
      document.getElementById('bookPhone').classList.add('error');
      valid = false;
    } else {
      document.getElementById('errPhone').textContent = '';
      document.getElementById('bookPhone').classList.remove('error');
    }
 
    if (!email || !isValidEmail(email)) {
      document.getElementById('errEmail').textContent = !email
        ? 'Bitte E-Mail-Adresse eingeben.'
        : 'Bitte eine gültige E-Mail-Adresse eingeben.';
      document.getElementById('bookEmail').classList.add('error');
      valid = false;
    } else {
      document.getElementById('errEmail').textContent = '';
      document.getElementById('bookEmail').classList.remove('error');
    }
 
    if (!valid) return;
 
    const s = TERMINE[selectedSlotIndex];
    const terminText = formatSlot(s);
 
    const subject = `Besichtigungsanfrage – ${terminText}`;
    const body =
`Hallo,
 
ich möchte die Wohnung in der Dornhaldenstr. 14/1, 70199 Stuttgart-Süd besichtigen.
 
Gewünschter Termin: ${terminText}
 
Meine Daten:
Name: ${name}
Telefon: ${phone}
E-Mail: ${email}
 
Viele Grüße
${name}`;
 
    const mailto = `mailto:${KONTAKT_EMAIL}`
      + `?subject=${encodeURIComponent(subject)}`
      + `&body=${encodeURIComponent(body)}`;
 
    window.location.href = mailto;
    closeModal();
  }
 
  // Modal schließen bei Klick auf Overlay
  document.getElementById('bookingModal').addEventListener('click', function(e) {
    if (e.target === this) closeModal();
  });
 
  // Start
  init();
</script>
</body>
</html>
 
