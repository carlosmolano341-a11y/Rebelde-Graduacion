# Rebelde-Graduacion

<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Rebelde Live - Management Dashboard</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700;800&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #FE2C55;
      --secondary: #25F4EE;
      --green: #00E676;
      --gold: #FFD700;
      --bg-base: #050505;
      --bg-surface: #121212;
      --bg-surface-hover: #1a1a1a;
      --border-color: rgba(255, 255, 255, 0.1);
      --text-main: #F3F4F6;
      --text-muted: #9CA3AF;
    }

    body {
      background-color: var(--bg-base); 
      color: var(--text-main); 
      font-family: 'Inter', sans-serif;
      margin: 0; 
      padding: 20px 15px 50px 15px; 
      max-width: 600px;
      margin-left: auto;
      margin-right: auto;
      -webkit-font-smoothing: antialiased;
    }

    /* HEADER */
    .header-container {
      text-align: center;
      margin-bottom: 25px;
    }
    h1 {
      color: var(--text-main);
      font-weight: 800;
      font-size: 1.8em; 
      margin: 0 0 5px 0;
      letter-spacing: -0.5px;
    }
    h1 span { color: var(--primary); }
    .subtitle { 
      font-size: 0.9em; 
      color: var(--secondary); 
      font-weight: 500;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    /* TARJETAS GLOBALES */
    .card {
      background: var(--bg-surface);
      border: 1px solid var(--border-color);
      border-radius: 12px;
      padding: 20px;
      margin-bottom: 20px;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
    }

    /* RECORDATORIO IMPORTANTE (ALERTA PREMIUM) */
    .important-reminder {
      background: linear-gradient(145deg, rgba(255, 215, 0, 0.05), rgba(255, 215, 0, 0.02));
      border: 1px solid rgba(255, 215, 0, 0.2);
      border-left: 4px solid var(--gold);
    }
    .reminder-title {
      color: var(--gold);
      font-weight: 700;
      font-size: 0.85em;
      text-transform: uppercase;
      margin-bottom: 8px;
      display: flex;
      align-items: center;
      gap: 5px;
    }
    .reminder-text {
      font-size: 0.85em;
      line-height: 1.6;
      color: #E5E7EB;
    }

    /* TICKET MOTIVACIONAL */
    .motivational-card {
      background: linear-gradient(145deg, rgba(0, 230, 118, 0.08), rgba(0,0,0,0));
      border: 1px solid rgba(0, 230, 118, 0.2);
    }
    .m-greeting { font-size: 1.2em; font-weight: 800; color: var(--text-main); margin-bottom: 5px; }
    .m-greeting span { color: var(--green); }
    .m-subtitle { color: var(--text-muted); font-size: 0.85em; margin-bottom: 15px; }
    .m-section-title { font-weight: 700; color: var(--secondary); margin: 15px 0 10px 0; font-size: 0.85em; text-transform: uppercase; letter-spacing: 0.5px;}
    
    .m-list { margin: 0; padding: 0; list-style: none; display: flex; flex-direction: column; gap: 8px;}
    .m-list li { font-size: 0.9em; display: flex; align-items: center; background: rgba(255,255,255,0.03); padding: 8px 12px; border-radius: 6px;}
    .m-list li::before { content: '✔️'; margin-right: 10px; font-size: 0.9em; }
    
    .m-bonus { 
      background: rgba(0, 230, 118, 0.1); 
      border: 1px solid rgba(0, 230, 118, 0.3); 
      padding: 15px; 
      border-radius: 8px; 
      margin-top: 15px; 
      font-weight: 700; 
      color: var(--green);
      font-size: 1.1em;
      text-align: center;
    }
    
    .m-alert-gold { 
      background: rgba(255, 215, 0, 0.1); 
      padding: 12px; 
      border-radius: 8px; 
      margin-top: 15px; 
      font-size: 0.9em; 
      border: 1px solid rgba(255, 215, 0, 0.5); 
      font-weight: 700; 
      color: var(--gold); 
      text-align: center; 
      box-shadow: 0 0 15px rgba(255, 215, 0, 0.1);
    }
    
    .m-info-block { background: rgba(255, 255, 255, 0.03); padding: 12px; border-radius: 8px; margin-top: 15px; font-size: 0.85em; border: 1px solid var(--border-color); line-height: 1.5; color: var(--text-muted);}
    .m-info-block strong { color: var(--text-main); }
    .m-signoff { margin-top: 20px; font-weight: 700; color: var(--text-muted); font-size: 0.85em; text-align: right;}
    .m-signoff span { color: var(--primary); }

    /* CALENDARIO CONTROLES */
    .controls {
      display: flex; justify-content: space-between; align-items: center;
      margin-bottom: 15px;
    }
    .btn-icon {
      background-color: var(--bg-surface); color: var(--text-main); border: 1px solid var(--border-color); 
      padding: 8px 15px; border-radius: 8px; cursor: pointer; font-size: 1em; transition: 0.2s;
    }
    .btn-icon:hover { background-color: var(--bg-surface-hover); border-color: var(--secondary); color: var(--secondary);}
    #monthDisplay { margin: 0; font-size: 1em; font-weight: 700; letter-spacing: 0.5px; }

    /* GRILLA CALENDARIO */
    .grid { display: grid; grid-template-columns: repeat(7, 1fr); gap: 6px; margin-bottom: 10px;}
    .day-name { font-weight: 600; color: var(--text-muted); font-size: 0.75em; text-align: center; text-transform: uppercase;}
    .day {
      background-color: var(--bg-surface); border: 1px solid var(--border-color); min-height: 65px; border-radius: 8px;
      padding: 6px; display: flex; flex-direction: column; cursor: pointer; transition: all 0.2s;
    }
    .day:hover:not(.empty) { border-color: var(--secondary); transform: translateY(-2px); }
    .day.empty { background-color: transparent; border: none; cursor: default; }
    
    .date-num { font-size: 0.8em; font-weight: 700; color: var(--text-muted); margin-bottom: auto;}
    .task { font-size: 0.7em; font-weight: 700; text-align: center; line-height: 1.3;}
    .task-h { color: var(--text-main); }
    .task-d { color: var(--primary); }

    .cumplido { border-color: rgba(37, 244, 238, 0.4); background: linear-gradient(180deg, var(--bg-surface), rgba(37, 244, 238, 0.05)); }
    .cumplido .date-num { color: var(--secondary); }
    .invalid-day { border-color: rgba(254, 44, 85, 0.4); opacity: 0.7; }

    /* INGRESO MANUAL */
    .manual-section { border: 1px dashed var(--border-color); }
    .manual-inputs { display: flex; gap: 10px; margin: 15px 0; }
    .m-input-group { flex: 1; display: flex; flex-direction: column; }
    .m-input-group label { font-size: 0.75em; color: var(--text-muted); margin-bottom: 5px; font-weight: 600; text-transform: uppercase;}
    .input-modern {
      padding: 12px; border-radius: 8px; border: 1px solid var(--border-color); background: var(--bg-base);
      color: var(--text-main); width: 100%; box-sizing: border-box; text-align: center; font-size: 1em; font-weight: 600; font-family: 'Inter', sans-serif;
      transition: all 0.3s;
    }
    .input-modern:focus { outline: none; border-color: var(--secondary); box-shadow: 0 0 0 2px rgba(37,244,238,0.1); }
    
    .btn-primary {
      width: 100%; background-color: var(--secondary); color: #000; border: none; padding: 14px;
      border-radius: 8px; font-weight: 700; font-size: 0.95em; cursor: pointer; transition: 0.2s; font-family: 'Inter', sans-serif;
    }
    .btn-primary:hover { background-color: #1fd1cb; transform: translateY(-1px); }
    
    .btn-outline {
      width: 100%; background-color: transparent; color: var(--text-main); border: 1px solid var(--border-color);
      padding: 14px; border-radius: 8px; font-weight: 600; font-size: 0.9em; cursor: pointer; transition: 0.2s; font-family: 'Inter', sans-serif;
    }
    .btn-outline:hover { border-color: var(--secondary); color: var(--secondary); }

    /* BARRAS DE PROGRESO (DASHBOARD) */
    .dash-title { color: var(--text-main); font-size: 1.1em; margin-bottom: 20px; font-weight: 800; display: flex; align-items: center; gap: 8px;}
    .dash-title::before { content: ''; display: block; width: 4px; height: 18px; background: var(--primary); border-radius: 2px;}
    
    .stat-row { margin-bottom: 18px; }
    .stat-header { display: flex; justify-content: space-between; font-size: 0.85em; font-weight: 600; color: var(--text-muted); margin-bottom: 8px;}
    .stat-value { color: var(--text-main); font-weight: 700;}
    .stat-value span { color: var(--secondary); }
    
    .progress-bar-bg { width: 100%; background-color: var(--bg-base); border-radius: 20px; height: 10px; overflow: hidden; border: 1px solid #222; }
    .progress-fill { 
      height: 100%; width: 0%; transition: width 1s cubic-bezier(0.4, 0, 0.2, 1); border-radius: 20px;
    }
    .fill-days { background: linear-gradient(90deg, #25F4EE, #00B4D8); box-shadow: 0 0 10px rgba(37,244,238,0.4); }
    .fill-hours { background: linear-gradient(90deg, #A855F7, #D946EF); box-shadow: 0 0 10px rgba(217,70,239,0.4); }
    .fill-diamonds { background: linear-gradient(90deg, #FE2C55, #FF4B6E); box-shadow: 0 0 10px rgba(254,44,85,0.4); }

    /* FORMULARIO CALIDAD */
    .report-section { border-top: 1px solid var(--border-color); padding-top: 25px; margin-top: 10px;}
    .question-box { background: var(--bg-base); padding: 15px; border-radius: 8px; margin-bottom: 12px; border: 1px solid var(--border-color); }
    .question-text { font-size: 0.85em; margin-bottom: 12px; font-weight: 600; color: var(--text-main); text-align: center;}
    .radio-group { display: flex; gap: 30px; justify-content: center;}
    .radio-group label { font-size: 0.9em; display: flex; align-items: center; gap: 8px; cursor: pointer; color: var(--text-muted); font-weight: 500;}
    .radio-group input[type="radio"] { accent-color: var(--secondary); width: 18px; height: 18px; cursor: pointer;}

    .btn-whatsapp { 
      width: 100%; background: linear-gradient(135deg, #25D366, #128C7E); color: white; border: none;
      padding: 16px; font-size: 1em; border-radius: 8px; margin-top: 10px; font-weight: 700; cursor: pointer;
      box-shadow: 0 4px 15px rgba(37, 211, 102, 0.2); transition: 0.3s; font-family: 'Inter', sans-serif;
    }
    .btn-whatsapp:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(37, 211, 102, 0.3); }

    /* MODAL */
    #modalOverlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.85); backdrop-filter: blur(5px); display: none; justify-content: center; align-items: center; z-index: 1000; }
    .modal-content { background: var(--bg-surface); padding: 25px; border-radius: 12px; border: 1px solid var(--border-color); width: 90%; max-width: 340px; box-shadow: 0 10px 40px rgba(0,0,0,0.5); }
    .modal-content h3 { margin: 0 0 10px 0; color: var(--text-main); font-size: 1.2em;}
    .modal-warning { font-size: 0.75em; color: var(--primary); background: rgba(254,44,85,0.1); padding: 10px; border-radius: 6px; margin-bottom: 20px; line-height: 1.4;}
    .modal-content label { display: block; margin-bottom: 8px; font-size: 0.8em; color: var(--text-muted); font-weight: 600;}
    .modal-content input { margin-bottom: 15px; }
    .modal-buttons { display: flex; gap: 10px; margin-top: 10px; }
  </style>
</head>
<body>

  <div class="header-container">
    <h1>Rebelde <span>Live</span></h1>
    <div class="subtitle">Management & Growth Tracker</div>
  </div>

  <div class="card important-reminder">
    <div class="reminder-title">⚠️ Regla de Corte Oficial</div>
    <div class="reminder-text">
      Tu mes inicia desde el día que ingresas a la agencia. Tu acumulado de dinero se calcula sumando datos hasta el <strong>último día de cada mes a las 7:00 PM</strong>. A partir de esa hora exacta, comienza a contar tu nuevo mes de recompensas.
    </div>
  </div>

  <div id="motivationalCard" class="card motivational-card"></div>

  <!-- CALENDARIO -->
  <div class="controls">
    <button id="prevBtn" class="btn-icon">&lt;</button>
    <div id="monthDisplay"></div>
    <button id="nextBtn" class="btn-icon">&gt;</button>
  </div>

  <div class="grid" id="calendarDays"></div>

  <!-- INGRESO MANUAL -->
  <div class="card manual-section">
    <div class="dash-title" style="font-size: 0.95em; margin-bottom: 5px;">⚡ Carga de Datos Rápida (Fin de Mes)</div>
    <p style="font-size: 0.75em; color: var(--text-muted); margin: 0 0 15px 0; line-height: 1.4;">Si olvidaste registrar días o extrajiste la data directo del panel de 15 días de TikTok, ingresa tus métricas totales aquí:</p>
    
    <div class="manual-inputs">
      <div class="m-input-group">
        <label>Días:</label>
        <input type="number" id="manualDays" class="input-modern" placeholder="Ej. 18" min="0">
      </div>
      <div class="m-input-group">
        <label>Horas:</label>
        <input type="number" id="manualHours" class="input-modern" placeholder="Ej. 50" min="0" step="0.1">
      </div>
      <div class="m-input-group">
        <label>Diamantes:</label>
        <input type="number" id="manualDiamonds" class="input-modern" placeholder="Ej. 45000" min="0">
      </div>
    </div>
    <button class="btn-outline" onclick="applyManualStats()">Calcular mis Totales</button>
  </div>

  <!-- DASHBOARD -->
  <div class="card dashboard">
    <div class="dash-title">Métricas de Rendimiento</div>
    
    <div class="stat-row">
      <div class="stat-header">
        <span>Días Válidos (Meta: 22)</span>
        <span class="stat-value" id="statDays">0</span>
      </div>
      <div class="progress-bar-bg"><div class="progress-fill fill-days" id="barDays"></div></div>
    </div>
    
    <div class="stat-row">
      <div class="stat-header">
        <span>Horas Live (Meta: 90)</span>
        <span class="stat-value" id="statHours">0</span>
      </div>
      <div class="progress-bar-bg"><div class="progress-fill fill-hours" id="barHours"></div></div>
    </div>

    <div class="stat-row" style="margin-bottom: 0;">
      <div class="stat-header">
        <span>Diamantes (Meta: 80k)</span>
        <span class="stat-value" id="statDiamonds">0</span>
      </div>
      <div class="progress-bar-bg"><div class="progress-fill fill-diamonds" id="barDiamonds"></div></div>
    </div>
    
    <div class="report-section">
      <div class="dash-title" style="justify-content: center; font-size: 0.9em; margin-bottom: 15px;">Control de Calidad</div>
      
      <div class="question-box">
        <div class="question-text">¿Has recibido infracciones este mes?</div>
        <div class="radio-group">
          <label><input type="radio" name="normas" value="Sí"> Sí</label>
          <label><input type="radio" name="normas" value="No" checked> No</label>
        </div>
      </div>

      <div class="question-box">
        <div class="question-text">¿Realizaste lives estáticos o de ventanita?</div>
        <div class="radio-group">
          <label><input type="radio" name="calidad" value="Sí"> Sí</label>
          <label><input type="radio" name="calidad" value="No" checked> No</label>
        </div>
      </div>

      <input type="text" id="creatorName" class="input-modern" style="margin: 15px 0;" placeholder="Firma: Tu Nombre/Usuario" onkeyup="updateName()">
      <button class="btn-whatsapp" onclick="sendWhatsApp()">Enviar Reporte Oficial a Manager</button>
    </div>
  </div>

  <!-- MODAL -->
  <div id="modalOverlay">
    <div class="modal-content">
      <h3 id="modalDateTitle">Día X</h3>
      <div class="modal-warning">Mínimo 1 hora completa (60 min) de corrido para validar el día. No aplican horas fragmentadas.</div>
      
      <label>Horas acumuladas hoy:</label>
      <input type="number" id="inputHours" class="input-modern" placeholder="Ej. 2.5" min="0" step="0.1">
      
      <label>Diamantes generados hoy:</label>
      <input type="number" id="inputDiamonds" class="input-modern" placeholder="Ej. 3500" min="0">
      
      <input type="hidden" id="editingDateKey">
      <div class="modal-buttons">
        <button class="btn-outline" style="border-color: #444; color: #aaa;" onclick="closeModal()">Cancelar</button>
        <button class="btn-primary" onclick="saveDay()">Guardar</button>
      </div>
    </div>
  </div>

  <script>
    const monthNames = ["Enero", "Febrero", "Marzo", "Abril", "Mayo", "Junio", "Julio", "Agosto", "Septiembre", "Octubre", "Noviembre", "Diciembre"];
    let currentDate = new Date(); 
    let globalStats = { validDays: 0, hours: 0, diamonds: 0, pocketMoney: 0.00, over80k: false, today: new Date().getDate() };
    let userName = localStorage.getItem('rebelde_creator_name') || 'Creador(a)';

    window.onload = () => {
      if (userName !== 'Creador(a)') document.getElementById('creatorName').value = userName;
      renderCalendar();
    };

    function updateName() {
      userName = document.getElementById('creatorName').value || 'Creador(a)';
      localStorage.setItem('rebelde_creator_name', userName);
      updateMotivationalCard();
    }

    // LÓGICA DE MONETIZACIÓN ACTUALIZADA
    function computeMonetization(tDays, tHours, tDiamonds) {
      let baseMoney = 0;
      let isOver80k = false;

      // Se activan las bonificaciones si alcanza los mínimos requeridos (10 días, 60 horas, 40k diamantes)
      if (tDays >= 10 && tHours >= 60 && tDiamonds >= 40000) {
        let dCapped = Math.min(tDiamonds, 80000);
        let diamondValue = 3.00 + ((dCapped - 40000) / (80000 - 40000)) * (34.00 - 3.00);

        let dayValue = 2.00 + ((tDays - 10) / (22 - 10)) * (8.00 - 2.00);
        let hourValue = 2.00 + ((tHours - 60) / (90 - 60)) * (8.00 - 2.00);

        baseMoney = diamondValue + dayValue + hourValue;

        // ESTRICTO: Se activa el premio si supera las metas máximas
        if (tDiamonds > 80000 && tDays >= 22 && tHours >= 90) {
          isOver80k = true;
        }
      }

      return { pocketMoney: baseMoney, over80k: isOver80k };
    }

    function renderCalendar() {
      const year = currentDate.getFullYear();
      const month = currentDate.getMonth();
      document.getElementById('monthDisplay').innerText = `${monthNames[month]} ${year}`;

      const firstDayIndex = new Date(year, month, 1).getDay();
      const startDay = firstDayIndex === 0 ? 6 : firstDayIndex - 1; 
      const daysInMonth = new Date(year, month + 1, 0).getDate();

      const calendarDays = document.getElementById('calendarDays');
      calendarDays.innerHTML = `
        <div class="day-name">Lun</div><div class="day-name">Mar</div><div class="day-name">Mié</div>
        <div class="day-name">Jue</div><div class="day-name">Vie</div><div class="day-name">Sáb</div><div class="day-name">Dom</div>
      `;

      let savedData = JSON.parse(localStorage.getItem('rebelde_data')) || {};

      for (let i = 0; i < startDay; i++) {
        calendarDays.innerHTML += '<div class="day empty"></div>';
      }

      for (let i = 1; i <= daysInMonth; i++) {
        const dateKey = `${year}-${month + 1}-${i}`;
        const dayData = savedData[dateKey] || { hours: 0, diamonds: 0 };
        
        let displayHtml = '';
        let classes = 'day';
        
        if (dayData.hours > 0 || dayData.diamonds > 0) {
          displayHtml = `<span class="task-h">${dayData.hours}h</span><br><span class="task-d">${dayData.diamonds >= 1000 ? (dayData.diamonds/1000).toFixed(1)+'k' : dayData.diamonds}</span>`;
          if (dayData.hours >= 1) classes += ' cumplido';
          else classes += ' invalid-day'; 
        }

        calendarDays.innerHTML += `
          <div class="${classes}" onclick="openModal('${dateKey}', ${i}, ${dayData.hours}, ${dayData.diamonds})">
            <span class="date-num">${i}</span>
            <span class="task">${displayHtml}</span>
          </div>
        `;
      }
      
      calculateStats(year, month + 1, daysInMonth);
    }

    function calculateStats(year, month, daysInMonth) {
      let savedData = JSON.parse(localStorage.getItem('rebelde_data')) || {};
      let tHours = 0, tDiamonds = 0, tDays = 0;

      for (let i = 1; i <= daysInMonth; i++) {
        const key = `${year}-${month}-${i}`;
        if (savedData[key]) {
          tHours += savedData[key].hours;
          tDiamonds += savedData[key].diamonds;
          if (savedData[key].hours >= 1) tDays++;
        }
      }

      let mon = computeMonetization(tDays, tHours, tDiamonds);
      let todayNum = (year === new Date().getFullYear() && month === new Date().getMonth() + 1) ? new Date().getDate() : daysInMonth;

      globalStats = { 
        validDays: tDays, 
        hours: tHours, 
        diamonds: tDiamonds, 
        pocketMoney: mon.pocketMoney, 
        over80k: mon.over80k,
        today: todayNum
      };

      updateUI();
    }

    function applyManualStats() {
      const tDays = parseInt(document.getElementById('manualDays').value) || 0;
      const tHours = parseFloat(document.getElementById('manualHours').value) || 0;
      const tDiamonds = parseInt(document.getElementById('manualDiamonds').value) || 0;

      if (tDays === 0 && tHours === 0 && tDiamonds === 0) {
        alert("Agrega al menos una métrica para calcular.");
        return;
      }

      let mon = computeMonetization(tDays, tHours, tDiamonds);
      
      globalStats = { 
        validDays: tDays, 
        hours: tHours, 
        diamonds: tDiamonds, 
        pocketMoney: mon.pocketMoney, 
        over80k: mon.over80k,
        today: new Date().getDate()
      };

      updateUI();
      document.querySelector('.dashboard').scrollIntoView({ behavior: 'smooth' });
    }

    function updateUI() {
      let dDisplay = globalStats.diamonds >= 1000 ? (globalStats.diamonds/1000).toFixed(1) + 'k' : globalStats.diamonds;

      document.getElementById('statDays').innerHTML = `<span>${globalStats.validDays}</span> / 22`;
      document.getElementById('statHours').innerHTML = `<span>${globalStats.hours.toFixed(1)}</span> / 90`;
      document.getElementById('statDiamonds').innerHTML = `<span>${dDisplay}</span> / 80k`;

      setTimeout(() => {
        document.getElementById('barDays').style.width = `${Math.min((globalStats.validDays / 22) * 100, 100)}%`;
        document.getElementById('barHours').style.width = `${Math.min((globalStats.hours / 90) * 100, 100)}%`;
        document.getElementById('barDiamonds').style.width = `${Math.min((globalStats.diamonds / 80000) * 100, 100)}%`;
      }, 50);

      updateMotivationalCard();
    }

    function updateMotivationalCard() {
      const card = document.getElementById('motivationalCard');
      
      let faltanDias = Math.max(22 - globalStats.validDays, 0);
      let faltanHoras = Math.max(90 - globalStats.hours, 0).toFixed(1);
      let faltanDiamantes = Math.max(80000 - globalStats.diamonds, 0);
      
      let currentDDisp = globalStats.diamonds >= 1000 ? (globalStats.diamonds/1000).toFixed(1) + 'k' : globalStats.diamonds;

      let over80kHtml = globalStats.over80k 
        ? `<div class="m-alert-gold">🌟 PREMIO EXCLUSIVO + BONO DESBLOQUEADO<br><span style="font-size:0.85em; font-weight:500; color:#eee;">Consulta con tu manager al enviar estas métricas.</span></div>` 
        : '';

      card.innerHTML = `
        <div class="m-greeting">Hola, <span>${userName}</span></div>
        <div class="m-subtitle">Reporte de progreso (Día ${globalStats.today} del ciclo)</div>
        
        <div class="m-section-title">Resumen Actual</div>
        <ul class="m-list">
          <li>Días: ${globalStats.validDays}/22 ${faltanDias > 0 ? `<span style="color:#aaa; font-size:0.85em; margin-left:auto;">Faltan ${faltanDias}</span>` : '<span style="color:var(--secondary); font-size:0.85em; margin-left:auto; font-weight:bold;">Completado</span>'}</li>
          <li>Horas: ${globalStats.hours}/90 ${faltanHoras > 0 ? `<span style="color:#aaa; font-size:0.85em; margin-left:auto;">Faltan ${faltanHoras}</span>` : '<span style="color:var(--secondary); font-size:0.85em; margin-left:auto; font-weight:bold;">Completado</span>'}</li>
          <li>Diamantes: ${currentDDisp}/80k ${faltanDiamantes > 0 ? `<span style="color:#aaa; font-size:0.85em; margin-left:auto;">En proceso</span>` : '<span style="color:var(--secondary); font-size:0.85em; margin-left:auto; font-weight:bold;">Completado</span>'}</li>
        </ul>

        <div class="m-bonus">
          SALDO A FAVOR: $${globalStats.pocketMoney.toFixed(2)} USD
        </div>
        
        ${over80kHtml}

        <div class="m-info-block" style="border: 1px dashed rgba(255, 215, 0, 0.4); background: rgba(255, 215, 0, 0.05);">
          <strong style="color: var(--gold);">🌟 META EXTRA (+80K DIAMANTES):</strong><br>
          Si superas los 80,000 diamantes (junto a tus 22 días y 90 horas) obtendrás un <strong>PREMIO EXCLUSIVO + BONO DESBLOQUEADO</strong>. Consulta con tu manager al enviar tus métricas.
        </div>

        <div class="m-info-block">
          <strong>Beneficios Activos:</strong> Acceso a campañas para colaborar con marcas y programa de capacitaciones exclusivas.
        </div>

        <div class="m-info-block">
          <strong>Pagos:</strong> Los cortes se abonan entre los días 7 y 10 de cada mes, liquidados al valor oficial del dólar en la cuenta registrada.
        </div>

        <div class="m-signoff">
          Rebelde Live Management<br><span>Dir. Karen</span>
        </div>
      `;
    }

    function openModal(dateKey, dayNum, currentHours, currentDiamonds) {
      document.getElementById('modalDateTitle').innerText = `Día ${dayNum}`;
      document.getElementById('inputHours').value = currentHours || '';
      document.getElementById('inputDiamonds').value = currentDiamonds || '';
      document.getElementById('editingDateKey').value = dateKey;
      document.getElementById('modalOverlay').style.display = 'flex';
    }

    function closeModal() { document.getElementById('modalOverlay').style.display = 'none'; }

    function saveDay() {
      const dateKey = document.getElementById('editingDateKey').value;
      const hours = parseFloat(document.getElementById('inputHours').value) || 0;
      const diamonds = parseInt(document.getElementById('inputDiamonds').value) || 0;

      let savedData = JSON.parse(localStorage.getItem('rebelde_data')) || {};
      savedData[dateKey] = { hours: hours, diamonds: diamonds };
      
      localStorage.setItem('rebelde_data', JSON.stringify(savedData));
      closeModal();
      
      document.getElementById('manualDays').value = '';
      document.getElementById('manualHours').value = '';
      document.getElementById('manualDiamonds').value = '';
      
      renderCalendar();
    }

    function sendWhatsApp() {
      if (userName === 'Creador(a)' || !userName.trim()) {
        alert("Por favor, ingresa tu Nombre o Usuario en el campo de firma antes de enviar.");
        return;
      }

      const normas = document.querySelector('input[name="normas"]:checked').value;
      const calidad = document.querySelector('input[name="calidad"]:checked').value;
      const monthText = document.getElementById('monthDisplay').innerText;
      
      const miNumero = "573114835387"; 
      
      let extraNote = globalStats.over80k ? "%0A%0A🌟 *PREMIO EXCLUSIVO + BONO DESBLOQUEADO*%0A_Consulta con tu manager al enviar estas métricas._" : "";

      const text = `🚀 Hola Karen! Soy *${userName}*.%0A%0A`
        + `Adjunto reporte de métricas correspondiente a *${monthText}* (Agencia Rebelde Live):%0A%0A`
        + `📊 *RESUMEN DE RENDIMIENTO:*%0A`
        + `├ 📅 Días Válidos: ${globalStats.validDays} / 22%0A`
        + `├ ⏱️ Horas Total: ${globalStats.hours.toFixed(1)} / 90%0A`
        + `└ 💎 Diamantes: ${globalStats.diamonds}%0A%0A`
        + `💰 *SALDO A FAVOR PROYECTADO:* *$${globalStats.pocketMoney.toFixed(2)} USD*%0A`
        + extraNote
        + `%0A%0A🛑 *AUDITORÍA DE CALIDAD:*%0A`
        + `├ Infracciones de normas: ${normas}%0A`
        + `└ Lives estáticos/ventanita: ${calidad}%0A%0A`
        + `Envío reporte para revisión y gestión. 🔥`;
      
      const url = `https://wa.me/${miNumero}?text=${text}`;
      window.open(url, '_blank');
    }

    document.getElementById('prevBtn').addEventListener('click', () => { 
      currentDate.setMonth(currentDate.getMonth() - 1); 
      renderCalendar(); 
    });
    document.getElementById('nextBtn').addEventListener('click', () => { 
      currentDate.setMonth(currentDate.getMonth() + 1); 
      renderCalendar(); 
    });
  </script>
</body>
</html>  
