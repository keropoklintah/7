<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Calorie & Exercise Tracker — Malaysian/Asian Food</title>
<style>
  :root{
    --bg: #FAF8F3;
    --card: #FFFFFF;
    --border: rgba(40,35,25,0.12);
    --border-strong: rgba(40,35,25,0.22);
    --text: #2B2620;
    --text-secondary: #6B6356;
    --text-tertiary: #9A9384;
    --accent: #B5562B;
    --accent-bg: #FBEAE0;
    --accent-text: #7A3013;
    --green: #4C7A3D;
    --green-bg: #E9F1E3;
    --blue: #3B6E8C;
    --blue-bg: #E6EFF3;
    --radius-md: 8px;
    --radius-lg: 14px;
    font-size: 16px;
  }
  *{ box-sizing: border-box; }
  body{
    margin: 0;
    background: var(--bg);
    color: var(--text);
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    line-height: 1.6;
  }
  .wrap{
    max-width: 640px;
    margin: 0 auto;
    padding: 2.5rem 1.25rem 4rem;
  }
  header{ margin-bottom: 2rem; }
  .eyebrow{
    font-size: 12px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--accent-text);
    font-weight: 600;
    margin: 0 0 6px;
  }
  h1{
    font-family: Georgia, 'Times New Roman', serif;
    font-size: 30px;
    font-weight: 400;
    margin: 0 0 8px;
    line-height: 1.2;
  }
  .sub{
    font-size: 14px;
    color: var(--text-secondary);
    margin: 0;
    max-width: 480px;
  }
  .disclaimer{
    font-size: 12.5px;
    color: var(--text-tertiary);
    margin: 14px 0 0;
    padding: 10px 14px;
    border-left: 2px solid var(--border-strong);
  }

  /* ---------- Setup screen ---------- */
  #setup-screen{
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: var(--radius-lg);
    padding: 1.75rem;
  }
  .field-group{ margin-bottom: 1.5rem; }
  .field-label{
    display: block;
    font-size: 13px;
    font-weight: 600;
    color: var(--text-secondary);
    margin-bottom: 8px;
  }
  .field-row{
    display: grid;
    grid-template-columns: repeat(2, minmax(0,1fr));
    gap: 12px;
  }
  .field-group input[type="number"]{
    width: 100%;
    padding: 10px 12px;
    font-size: 15px;
    border: 1px solid var(--border-strong);
    border-radius: var(--radius-md);
    background: var(--bg);
    color: var(--text);
    font-family: inherit;
  }
  .field-group input:focus{
    outline: none;
    border-color: var(--accent);
    box-shadow: 0 0 0 3px var(--accent-bg);
  }
  .pill-options{
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }
  .pill-option{
    padding: 9px 14px;
    font-size: 13.5px;
    border: 1px solid var(--border-strong);
    border-radius: 999px;
    background: var(--bg);
    color: var(--text-secondary);
    cursor: pointer;
    font-weight: 500;
  }
  .pill-option:hover{ border-color: var(--accent); }
  .pill-option.selected{
    background: var(--accent);
    border-color: var(--accent);
    color: #fff;
  }
  .pill-option .pill-desc{
    display: block;
    font-size: 11px;
    font-weight: 400;
    opacity: 0.85;
    margin-top: 2px;
  }
  .goal-grid{
    display: grid;
    grid-template-columns: repeat(2, minmax(0,1fr));
    gap: 8px;
  }
  .goal-card{
    padding: 12px 14px;
    border: 1px solid var(--border-strong);
    border-radius: var(--radius-md);
    background: var(--bg);
    cursor: pointer;
  }
  .goal-card:hover{ border-color: var(--accent); }
  .goal-card.selected{
    background: var(--accent-bg);
    border-color: var(--accent);
  }
  .goal-card .goal-name{ font-size: 13.5px; font-weight: 600; margin: 0 0 2px; }
  .goal-card .goal-desc{ font-size: 11.5px; color: var(--text-tertiary); margin: 0; }
  .goal-card.selected .goal-name{ color: var(--accent-text); }

  #setup-error{
    font-size: 13px;
    color: var(--accent-text);
    background: var(--accent-bg);
    padding: 10px 12px;
    border-radius: var(--radius-md);
    margin-bottom: 1rem;
    display: none;
  }
  #start-btn{
    width: 100%;
    padding: 13px;
    font-size: 15px;
    font-weight: 600;
    background: var(--text);
    color: var(--bg);
    border: none;
    border-radius: var(--radius-md);
    cursor: pointer;
  }
  #start-btn:hover{ opacity: 0.88; }

  /* ---------- Main app ---------- */
  #app-screen{ display: none; }

  .profile-bar{
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: var(--radius-lg);
    padding: 12px 16px;
    margin-bottom: 1.5rem;
    font-size: 13px;
    color: var(--text-secondary);
  }
  .profile-bar button{
    background: transparent;
    border: 1px solid var(--border-strong);
    border-radius: var(--radius-md);
    padding: 6px 12px;
    font-size: 12.5px;
    color: var(--text-secondary);
    cursor: pointer;
  }
  .profile-bar button:hover{ border-color: var(--accent); color: var(--accent-text); }

  .targets-box{
    background: var(--blue-bg);
    border-radius: var(--radius-lg);
    padding: 14px 16px;
    margin-bottom: 1.75rem;
    font-size: 13.5px;
    color: var(--blue);
  }
  .targets-box strong{ font-weight: 700; }

  input[type="text"]{
    flex: 1;
    padding: 11px 14px;
    font-size: 15px;
    border: 1px solid var(--border-strong);
    border-radius: var(--radius-md);
    background: var(--card);
    color: var(--text);
    outline: none;
    font-family: inherit;
  }
  input[type="text"]:focus{
    border-color: var(--accent);
    box-shadow: 0 0 0 3px var(--accent-bg);
  }
  button{ font-family: inherit; cursor: pointer; }

  .input-row{ display: flex; gap: 8px; margin-bottom: 8px; }
  #add-btn{
    padding: 11px 18px;
    font-size: 14px;
    font-weight: 600;
    background: var(--text);
    color: var(--bg);
    border: none;
    border-radius: var(--radius-md);
    white-space: nowrap;
  }
  #add-btn:hover{ opacity: 0.88; }

  #suggestions{ display: flex; flex-wrap: wrap; gap: 6px; min-height: 30px; margin-bottom: 2px; }
  .chip{
    font-size: 13px;
    padding: 6px 12px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 999px;
    color: var(--text);
  }
  .chip:hover{ border-color: var(--accent); background: var(--accent-bg); color: var(--accent-text); }
  #match-note{ font-size: 12.5px; color: var(--text-tertiary); margin: 6px 0 1.75rem; min-height: 16px; }

  .totals{ display: grid; grid-template-columns: repeat(4, minmax(0,1fr)); gap: 10px; margin-bottom: 1.75rem; }
  .stat{ background: var(--card); border: 1px solid var(--border); border-radius: var(--radius-lg); padding: 14px 12px; }
  .stat-label{ font-size: 11.5px; color: var(--text-secondary); margin: 0 0 4px; text-transform: uppercase; letter-spacing: 0.04em; }
  .stat-value{ font-size: 22px; font-weight: 600; margin: 0; }
  .stat.kcal .stat-value{ color: var(--accent-text); }

  #log-list{ display: flex; flex-direction: column; gap: 8px; margin-bottom: 1rem; }
  .log-item{
    display: flex; align-items: center; justify-content: space-between;
    padding: 10px 14px; background: var(--card); border: 1px solid var(--border); border-radius: var(--radius-md);
  }
  .log-item .name{ margin: 0; font-size: 14px; font-weight: 600; }
  .log-item .note{ margin: 2px 0 0; font-size: 12px; color: var(--text-tertiary); }
  .log-item .right{ display: flex; align-items: center; gap: 10px; flex-shrink: 0; margin-left: 12px; }
  .log-item .kcal{ font-size: 14px; font-weight: 600; white-space: nowrap; }
  .del-btn{
    background: transparent; border: 1px solid var(--border); border-radius: 6px;
    width: 26px; height: 26px; display: flex; align-items: center; justify-content: center;
    color: var(--text-tertiary); font-size: 14px; line-height: 1;
  }
  .del-btn:hover{ border-color: var(--accent); color: var(--accent-text); }

  #empty-state{
    text-align: center; padding: 2rem 1rem; color: var(--text-tertiary); font-size: 14px;
    border: 1px dashed var(--border); border-radius: var(--radius-lg);
  }
  .footer-row{ display: flex; justify-content: flex-end; margin-top: 10px; }
  #clear-btn, #clear-exercise-btn{ font-size: 13px; color: var(--text-secondary); background: transparent; border: none; padding: 4px 8px; }
  #clear-btn:hover, #clear-exercise-btn:hover{ color: var(--accent-text); }

  footer{ margin-top: 2.5rem; padding-top: 1.25rem; border-top: 1px solid var(--border); font-size: 12px; color: var(--text-tertiary); }

  @media (max-width: 420px){
    .totals{ grid-template-columns: repeat(2, minmax(0,1fr)); }
    h1{ font-size: 26px; }
    .goal-grid{ grid-template-columns: 1fr; }
  }

  .net-summary{ display: grid; grid-template-columns: repeat(3, minmax(0,1fr)); gap: 10px; margin: 0 0 1.5rem; }
  .net-stat{ background: var(--card); border: 1px solid var(--border); border-radius: var(--radius-lg); padding: 14px 12px; text-align: center; }
  .net-stat.burn .stat-value{ color: var(--green); }
  .net-stat.net .stat-value{ color: var(--accent-text); }

  .section-tabs{ display: flex; gap: 6px; margin-bottom: 1.5rem; border-bottom: 1px solid var(--border); }
  .tab-btn{
    background: transparent; border: none; padding: 10px 4px; margin-right: 18px;
    font-size: 15px; font-weight: 600; color: var(--text-tertiary); border-bottom: 2px solid transparent;
  }
  .tab-btn.active{ color: var(--text); border-bottom-color: var(--accent); }
  .tab-panel{ display: none; }
  .tab-panel.active{ display: block; }

  .goal-box{ background: var(--accent-bg); border-radius: var(--radius-lg); padding: 14px 16px; margin-bottom: 1.75rem; font-size: 13.5px; color: var(--accent-text); }
  .goal-box strong{ font-weight: 700; }

  .section-label{ font-size: 14px; text-transform: uppercase; letter-spacing: 0.04em; color: var(--text-secondary); margin: 0 0 4px; font-weight: 600; }
  .plan-sub{ font-size: 13px; color: var(--text-tertiary); margin: 0 0 14px; }

  .plan-item{
    display: flex; align-items: center; gap: 12px; background: var(--card); border: 1px solid var(--border);
    border-radius: var(--radius-md); padding: 12px 14px; margin-bottom: 8px; cursor: pointer;
    transition: background 0.15s, border-color 0.15s;
  }
  .plan-item:hover{ border-color: var(--border-strong); }
  .plan-item.done{ background: var(--green-bg); border-color: var(--green); }
  .plan-item.done .plan-name{ text-decoration: line-through; color: var(--text-secondary); }
  .plan-checkbox{
    width: 22px; height: 22px; border-radius: 6px; border: 1.5px solid var(--border-strong);
    background: var(--card); flex-shrink: 0; display: flex; align-items: center; justify-content: center;
    font-size: 14px; color: var(--card);
  }
  .plan-item.done .plan-checkbox{ background: var(--green); border-color: var(--green); color: #fff; }
  .plan-left{ flex: 1; min-width: 0; }
  .plan-name{ margin: 0 0 2px; font-size: 14px; font-weight: 600; }
  .plan-desc{ margin: 0; font-size: 12px; color: var(--text-tertiary); }
  .plan-kcal{ font-size: 13px; font-weight: 600; color: var(--green); white-space: nowrap; flex-shrink: 0; }

  .plan-progress{ margin: 1.25rem 0 1rem; }
  .plan-progress-bar{ height: 8px; background: var(--border); border-radius: 999px; overflow: hidden; }
  .plan-progress-fill{ height: 100%; width: 0%; background: var(--green); border-radius: 999px; transition: width 0.2s; }
  #plan-progress-text{ font-size: 13px; color: var(--text-secondary); margin: 8px 0 0; }

  .oneoff-grid{ display: grid; grid-template-columns: repeat(3, minmax(0,1fr)); gap: 10px; }
  .oneoff-card{ background: var(--card); border: 1px solid var(--border); border-radius: var(--radius-lg); padding: 14px 12px; text-align: center; }
  .oneoff-icon{ font-size: 22px; font-style: normal; display: block; margin-bottom: 6px; }
  .oneoff-name{ font-size: 13px; font-weight: 600; margin: 0 0 10px; }
  .oneoff-row{ display: flex; gap: 6px; }
  .oneoff-row input{
    width: 100%; min-width: 0; padding: 8px 6px; font-size: 13px; text-align: center;
    border: 1px solid var(--border-strong); border-radius: var(--radius-md); background: var(--bg); color: var(--text);
  }
  .oneoff-log-btn{
    background: var(--green-bg); color: var(--green); border: none; border-radius: var(--radius-md);
    padding: 8px 10px; font-size: 13px; font-weight: 600; white-space: nowrap; flex-shrink: 0;
  }
  .oneoff-log-btn:hover{ opacity: 0.85; }

  @media (max-width: 420px){ .oneoff-grid{ grid-template-columns: 1fr; } }

  #new-day-btn{
    background: var(--accent); color: #fff; border: none; border-radius: var(--radius-md);
    padding: 6px 12px; font-size: 12.5px; font-weight: 600; cursor: pointer;
  }
  #new-day-btn:hover{ opacity: 0.88; }

  .history-card{
    background: var(--card); border: 1px solid var(--border); border-radius: var(--radius-lg);
    margin-bottom: 10px; overflow: hidden;
  }
  .history-card-header{
    display: flex; align-items: center; justify-content: space-between;
    padding: 14px 16px; cursor: pointer;
  }
  .history-card-header:hover{ background: var(--bg); }
  .history-date{ font-size: 14px; font-weight: 600; margin: 0; }
  .history-summary{ font-size: 12px; color: var(--text-tertiary); margin: 2px 0 0; }
  .history-totals{ display: flex; gap: 14px; align-items: center; flex-shrink: 0; }
  .history-totals .h-stat{ text-align: center; }
  .history-totals .h-stat .h-val{ font-size: 14px; font-weight: 600; }
  .history-totals .h-stat .h-lbl{ font-size: 10.5px; color: var(--text-tertiary); text-transform: uppercase; }
  .history-chevron{ font-size: 12px; color: var(--text-tertiary); margin-left: 8px; transition: transform 0.15s; }
  .history-card.expanded .history-chevron{ transform: rotate(90deg); }
  .history-detail{ display: none; padding: 0 16px 16px; border-top: 1px solid var(--border); }
  .history-card.expanded .history-detail{ display: block; }
  .history-detail h4{ font-size: 12px; text-transform: uppercase; letter-spacing: 0.04em; color: var(--text-secondary); margin: 14px 0 8px; }
  .history-item-row{ display: flex; justify-content: space-between; font-size: 13px; padding: 5px 0; border-bottom: 1px solid var(--border); }
  .history-item-row:last-child{ border-bottom: none; }
  .history-delete-btn{
    background: transparent; border: 1px solid var(--border-strong); border-radius: var(--radius-md);
    padding: 6px 10px; font-size: 12px; color: var(--text-secondary); margin-top: 10px;
  }
  .history-delete-btn:hover{ border-color: var(--accent); color: var(--accent-text); }
</style>
</head>
<body>
<div class="wrap">

  <header>
    <p class="eyebrow">Daily intake & output</p>
    <h1>Calorie &amp; home exercise tracker</h1>
    <p class="sub">Built for Malaysian/Asian meals — works for anyone. Set up your profile once, then log food and exercise.</p>
  </header>

  <!-- ============ SETUP SCREEN ============ -->
  <div id="setup-screen">

    <div class="field-group">
      <span class="field-label">Gender</span>
      <div class="pill-options" id="gender-options">
        <div class="pill-option" data-value="male">Male</div>
        <div class="pill-option" data-value="female">Female</div>
      </div>
    </div>

    <div class="field-group">
      <div class="field-row">
        <div>
          <span class="field-label">Height (cm)</span>
          <input type="number" id="input-height" placeholder="e.g. 174" min="100" max="230" />
        </div>
        <div>
          <span class="field-label">Weight (kg)</span>
          <input type="number" id="input-weight" placeholder="e.g. 71" min="30" max="250" />
        </div>
      </div>
    </div>

    <div class="field-group">
      <span class="field-label">Age</span>
      <input type="number" id="input-age" placeholder="e.g. 29" min="13" max="100" style="max-width: 160px;" />
    </div>

    <div class="field-group">
      <span class="field-label">Daily activity level (outside dedicated exercise)</span>
      <div class="pill-options" id="activity-options">
        <div class="pill-option" data-value="deskbound">Desk-bound<span class="pill-desc">Sit most of the day</span></div>
        <div class="pill-option" data-value="some">Some movement<span class="pill-desc">On feet part of the day</span></div>
        <div class="pill-option" data-value="active">Active job<span class="pill-desc">On feet most of the day</span></div>
      </div>
    </div>

    <div class="field-group">
      <span class="field-label">Goal</span>
      <div class="goal-grid" id="goal-options">
        <div class="goal-card" data-value="lose">
          <p class="goal-name">Lose weight</p>
          <p class="goal-desc">Fat loss focus, larger deficit</p>
        </div>
        <div class="goal-card" data-value="recomp">
          <p class="goal-name">Lean recomposition</p>
          <p class="goal-desc">Lose some fat, build some muscle</p>
        </div>
        <div class="goal-card" data-value="muscle">
          <p class="goal-name">Build muscle</p>
          <p class="goal-desc">Mild surplus, strength focus</p>
        </div>
        <div class="goal-card" data-value="maintain">
          <p class="goal-name">Maintain weight</p>
          <p class="goal-desc">Stay around current weight</p>
        </div>
      </div>
    </div>

    <div class="field-group">
      <span class="field-label">Where do you train?</span>
      <div class="pill-options" id="location-options">
        <div class="pill-option" data-value="home">Home<span class="pill-desc">Bodyweight-focused plan</span></div>
        <div class="pill-option" data-value="gym">Gym<span class="pill-desc">Full equipment, more options</span></div>
      </div>
    </div>

    <div class="field-group" id="home-equipment-group" style="display:none;">
      <span class="field-label">Any equipment at home?</span>
      <div class="pill-options" id="home-equipment-options">
        <div class="pill-option" data-value="none">Bodyweight only</div>
        <div class="pill-option" data-value="pullup">Pull-up bar</div>
        <div class="pill-option" data-value="dumbbell">Dumbbells</div>
        <div class="pill-option" data-value="both">Pull-up bar + dumbbells</div>
      </div>
    </div>

    <div class="field-group" id="gym-equipment-group" style="display:none;">
      <span class="field-label">What's available at your gym? (select all that apply)</span>
      <div class="pill-options" id="gym-equipment-options">
        <div class="pill-option" data-value="barbell">Barbell + rack</div>
        <div class="pill-option" data-value="dumbbell">Dumbbells</div>
        <div class="pill-option" data-value="machines">Resistance machines</div>
        <div class="pill-option" data-value="cables">Cable / pulley station</div>
        <div class="pill-option" data-value="pullup">Pull-up bar / assisted pull-up</div>
        <div class="pill-option" data-value="cardio">Cardio machines (treadmill, bike, rower)</div>
      </div>
      <p class="plan-sub" style="margin-top:8px;">Pick everything you have access to — the gym plan will use the best option per move.</p>
    </div>

    <p id="setup-error">Please fill in all fields above before continuing.</p>
    <button id="start-btn">Calculate my targets</button>

    <p class="disclaimer">This uses the Mifflin-St Jeor formula, a standard estimate with roughly 10% margin of error — not a lab-measured metabolic rate. Treat the numbers as a planning guide.</p>
  </div>

  <!-- ============ MAIN APP ============ -->
  <div id="app-screen">

    <div class="profile-bar">
      <span id="profile-summary"></span>
      <div style="display:flex; gap:8px; align-items:center;">
        <span id="current-date-label" style="font-size:12.5px; color:var(--text-tertiary);"></span>
        <button id="new-day-btn" title="Archive today's log and start fresh">New Day</button>
        <button id="edit-profile-btn">Edit profile</button>
      </div>
    </div>

    <div class="targets-box" id="targets-box"></div>

    <div class="net-summary">
      <div class="net-stat"><p class="stat-label">Eaten</p><p class="stat-value" id="net-eaten">0</p></div>
      <div class="net-stat burn"><p class="stat-label">Burned</p><p class="stat-value" id="net-burned">0</p></div>
      <div class="net-stat net"><p class="stat-label">Net</p><p class="stat-value" id="net-total">0</p></div>
    </div>

    <div class="section-tabs">
      <button class="tab-btn active" id="tab-food" data-tab="food">Food log</button>
      <button class="tab-btn" id="tab-exercise" data-tab="exercise">Exercise</button>
      <button class="tab-btn" id="tab-history" data-tab="history">History</button>
    </div>

    <div class="tab-panel active" id="panel-food">
      <p class="disclaimer" style="margin: 0 0 1.25rem;">Cooked mixed dishes like nasi lemak or mee goreng vary a lot by stall and home recipe — "one serving" can range from 350 to 800+ kcal in published data. These are sourced midpoints for normal Asian portions, useful for tracking trends, not exact lab values.</p>

      <div class="input-row">
        <input id="food-input" type="text" placeholder="e.g. nasi lemak ayam, mee goreng, teh o ais" autocomplete="off" />
        <button id="add-btn">+ Add</button>
      </div>
      <div id="suggestions"></div>
      <p id="match-note"></p>

      <div class="totals" style="grid-template-columns: repeat(2, minmax(0,1fr));">
        <div class="stat kcal"><p class="stat-label">Calories</p><p class="stat-value" id="total-kcal">0</p></div>
        <div class="stat"><p class="stat-label">Protein</p><p class="stat-value" id="total-protein">0g</p></div>
      </div>

      <div id="log-list"></div>
      <div id="empty-state">No food logged yet. Type a dish above to start today's total.</div>

      <div class="footer-row"><button id="clear-btn">Clear log</button></div>
    </div>

    <div class="tab-panel" id="panel-exercise">
      <div class="goal-box" id="exercise-goal-box"></div>

      <h3 class="section-label">Today's circuit — tick off as you go</h3>
      <p class="plan-sub" id="circuit-sub">Same plan every day, about 10 minutes.</p>

      <div id="plan-checklist"></div>

      <div class="plan-progress">
        <div class="plan-progress-bar"><div class="plan-progress-fill" id="plan-progress-fill"></div></div>
        <p id="plan-progress-text">0 of 0 done · 0 kcal so far</p>
      </div>

      <div class="footer-row"><button id="reset-plan-btn">Reset today's circuit</button></div>

      <h3 class="section-label" style="margin-top:2.25rem;">One-off activities</h3>
      <p class="plan-sub">For gym, running, or swimming sessions — log these whenever they actually happen.</p>

      <div class="oneoff-grid">
        <div class="oneoff-card">
          <i class="oneoff-icon">🏋️</i>
          <p class="oneoff-name">Gym session</p>
          <div class="oneoff-row">
            <input type="number" id="gym-minutes" placeholder="min" min="0" value="45" />
            <button class="oneoff-log-btn" data-activity="gym">Log</button>
          </div>
        </div>
        <div class="oneoff-card">
          <i class="oneoff-icon">🏃</i>
          <p class="oneoff-name">Running</p>
          <div class="oneoff-row">
            <input type="number" id="run-minutes" placeholder="min" min="0" value="20" />
            <button class="oneoff-log-btn" data-activity="run">Log</button>
          </div>
        </div>
        <div class="oneoff-card">
          <i class="oneoff-icon">🏊</i>
          <p class="oneoff-name">Swimming</p>
          <div class="oneoff-row">
            <input type="number" id="swim-minutes" placeholder="min" min="0" value="30" />
            <button class="oneoff-log-btn" data-activity="swim">Log</button>
          </div>
        </div>
      </div>

      <h3 class="section-label" style="margin-top:2rem;">Today's exercise log</h3>
      <div id="exercise-log-list"></div>
      <div id="exercise-empty-state" style="text-align:center; padding:1.5rem 1rem; color:var(--text-tertiary); font-size:14px; border:1px dashed var(--border); border-radius:var(--radius-lg);">Nothing logged yet — tick off the circuit above or log a one-off activity.</div>

      <div class="footer-row"><button id="clear-exercise-btn">Clear exercise log</button></div>
    </div>

    <div class="tab-panel" id="panel-history">
      <p class="plan-sub" style="margin-bottom: 1.25rem;">Each day you click "New Day," today's log is saved here and a fresh log starts. This is stored in your browser, so it stays even if you close this page — until you clear it yourself.</p>

      <div id="history-list"></div>
      <div id="history-empty-state" style="text-align:center; padding:2rem 1rem; color:var(--text-tertiary); font-size:14px; border:1px dashed var(--border); border-radius:var(--radius-lg);">No history yet. Click "New Day" above once you've logged today's food and exercise, to save it here and start fresh.</div>

      <div class="footer-row"><button id="clear-history-btn">Clear all history</button></div>
    </div>

    <footer>
      Today's log and your saved history are stored in this browser (localStorage) and stay until you clear them — they are not synced anywhere else, so they won't appear if you open this file on a different device or browser. Food values are reference estimates for normal Asian-sized portions. Exercise calorie burn uses standard MET formulas calibrated to your entered body weight — actual burn varies with effort, form, and individual fitness. Not a substitute for lab-tested nutrition data or medical advice. If you have any underlying health conditions, check with a doctor before starting a new exercise routine or calorie target.
    </footer>

  </div>

</div>

<script>
/* =========================================================
   FOOD DATABASE — Calories + Protein
   Sources (Malaysian government health references):
   - KKM Bahagian Pemakanan, "Senarai Kalori Bagi Makanan dan Minuman"
   - JKN Selangor, "Bank Kalori Makanan"
   Protein values are estimated from typical macro ratios for each
   food category where the source lists kcal only (e.g. meat/fish
   dishes ~18-22% kcal from protein, rice/noodle dishes ~8-12%,
   vegetables/fruit ~3-8%). Carbs/fat are intentionally omitted —
   dropping them let us source far more dishes without guessing
   numbers we can't back up.
   ========================================================= */

const DB = [
// ===== DRINKS / MINUMAN =====
  {names:["air limau nipis","limau ais","air limau","lime water"], kcal:31, p:0, note:"1 glass, 1/2 lime + 1 tsp sugar (KKM)"},
  {names:["limau ais kosong","air limau kosong","lime water no sugar"], kcal:5, p:0, note:"1 glass, no sugar"},
  {names:["teh o ais limau","teh o limau"], kcal:120, p:0, note:"1 glass, iced lime tea, standard sugar"},
  {names:["air kosong","plain water","sky juice"], kcal:0, p:0, note:"0 calories (KKM)"},
  {names:["air barli","barley drink"], kcal:193, p:0, note:"1 glass, 250ml (KKM)"},
  {names:["air batu campur","abc"], kcal:417, p:2, note:"1 bowl, 250g, mixed shaved ice (KKM)"},
  {names:["air cincau","grass jelly drink","cincau"], kcal:108, p:0, note:"1 glass, 250ml (KKM)"},
  {names:["air jagung","corn juice","jus jagung"], kcal:256, p:2, note:"1 glass, 250ml (KKM)"},
  {names:["air kelapa","coconut water","coconut drink"], kcal:55, p:1, note:"1 cup, 250ml (KKM)"},
  {names:["air soya","soymilk","susu soya tanpa gula"], kcal:150, p:8, note:"1 glass, 250ml, unsweetened (KKM)"},
  {names:["air soya cincau","soymilk cincau"], kcal:138, p:5, note:"1 glass, 250ml (KKM)"},
  {names:["air tebu","sugarcane juice","jus tebu"], kcal:184, p:0, note:"1 glass, 250ml (KKM)"},
  {names:["air teh bunga","chrysanthemum tea"], kcal:48, p:0, note:"1 cup, 250ml (KKM)"},
  {names:["ais kopi","iced coffee"], kcal:63, p:1, note:"100ml (KKM, scales with size)"},
  {names:["asam boi","limau asam boi","calamansi sour plum"], kcal:57, p:0, note:"1 cup (general reference)"},
  {names:["teh tarik"], kcal:120, p:2, note:"1 glass, normal sugar"},
  {names:["teh o","teh o ais","teh o ice"], kcal:60, p:0, note:"1 glass, black tea with sugar"},
  {names:["teh o kosong"], kcal:5, p:0, note:"1 glass, no sugar"},
  {names:["teh ais","teh c ais"], kcal:130, p:2, note:"1 glass, milk tea iced"},
  {names:["kopi o","kopi o ais"], kcal:60, p:0, note:"1 glass, black coffee with sugar"},
  {names:["kopi","kopi ais","kopi c"], kcal:130, p:2, note:"1 glass, white coffee"},
  {names:["nescafe o","nescafe tarik"], kcal:80, p:1, note:"1 glass, with sugar only (KKM-derived)"},
  {names:["milo","milo ais","milo ice"], kcal:180, p:5, note:"1 glass"},
  {names:["milo panas","hot milo"], kcal:136, p:4, note:"8oz, 180ml (KKM)"},
  {names:["horlicks"], kcal:80, p:2, note:"200ml, sugar only (KKM)"},
  {names:["teh halia","ginger tea"], kcal:25, p:0, note:"1 glass, 200ml (KKM)"},
  {names:["sirap bandung","bandung"], kcal:125, p:1, note:"1 cup, 250ml (KKM)"},
  {names:["lassi","indian yogurt drink"], kcal:114, p:4, note:"1 glass, 250g (general reference)"},
  {names:["bir","beer"], kcal:135, p:1, note:"1 can, 330ml (KKM)"},
  {names:["coke","coca cola"], kcal:153, p:0, note:"1 medium glass, 364ml (KKM)"},
  {names:["coke light","diet coke"], kcal:1, p:0, note:"1 small glass (KKM)"},
  {names:["cappuccino"], kcal:75, p:3, note:"1 serving, 197ml (KKM)"},

  // ===== ICED DESSERTS / SHAVED ICE =====
  {names:["ais kacang","ice kacang"], kcal:250, p:3, note:"1 rice bowl, 400g (KKM)"},
  {names:["ais kacang durian","durian ice kacang"], kcal:275, p:3, note:"1 serving, 341g (KKM)"},
  {names:["cendol"], kcal:278, p:2, note:"1 glass, 200ml (KKM)"},
  {names:["cendol durian"], kcal:410, p:3, note:"1 bowl, 398g (KKM)"},
  {names:["cendol mangga","mango cendol"], kcal:335, p:2, note:"1 bowl, 383g (KKM)"},
  {names:["ais jagung","ice sweetcorn"], kcal:165, p:2, note:"1 serving, 292g (KKM)"},
  {names:["ais durian belanda","ice soursop"], kcal:200, p:1, note:"1 serving, 299g (KKM)"},
  {names:["bubur cha cha"], kcal:536, p:5, note:"1 packet, 355g (KKM)"},
  {names:["cheng tng"], kcal:200, p:2, note:"1 bowl, 400g (KKM)"},
  {names:["tau fu fah","tofu fah","soybean pudding"], kcal:183, p:7, note:"1 serving, 537g (general reference)"},

  // ===== MAIN RICE DISHES / NASI =====
  {names:["nasi lemak","nasi lemak biasa","nasi lemak kosong"], kcal:540, p:11, note:"rice, sambal, egg, anchovies, peanuts"},
  {names:["nasi lemak ayam","nasi lemak with chicken","nasi lemak fried chicken"], kcal:760, p:28, note:"nasi lemak + fried chicken"},
  {names:["nasi lemak rendang","nasi lemak rendang ayam"], kcal:780, p:26, note:"nasi lemak + rendang"},
  {names:["nasi lemak bersambal"], kcal:400, p:7, note:"1 plate, sambal-focused (KKM-aligned)"},
  {names:["nasi goreng","fried rice"], kcal:500, p:14, note:"plate of fried rice"},
  {names:["nasi goreng ayam","nasi goreng kampung ayam"], kcal:620, p:24, note:"fried rice + chicken"},
  {names:["nasi goreng bertelur","nasi goreng telur"], kcal:635, p:16, note:"1 plate, fried rice with egg (KKM-aligned)"},
  {names:["nasi campur","mixed rice","economy rice"], kcal:620, p:22, note:"rice + 3 dish helpings (veg, egg, chicken)"},
  {names:["nasi kandar","nasi kandar campur"], kcal:900, p:28, note:"rice with mixed curry gravies, banjir style"},
  {names:["nasi dagang"], kcal:600, p:18, note:"coconut rice with fish curry"},
  {names:["nasi ayam","chicken rice","hainanese chicken rice","hainan chicken rice"], kcal:600, p:28, note:"rice + steamed/roast chicken"},
  {names:["nasi ayam kosong"], kcal:300, p:10, note:"1 plate, plain chicken rice no chicken (KKM-aligned)"},
  {names:["nasi briyani","nasi beriani","chicken briyani","nasi briyani berayam"], kcal:880, p:30, note:"1 plate, spiced rice with chicken (KKM-aligned)"},
  {names:["nasi minyak kosong"], kcal:445, p:8, note:"1 plate, ghee rice, plain (KKM-aligned)"},
  {names:["nasi putih","white rice","plain rice"], kcal:200, p:4, note:"1 normal bowl, cooked"},
  {names:["nasi putih 1.5 cawan"], kcal:260, p:5, note:"1.5 cups, larger serving (KKM-aligned)"},
  {names:["beras basmati","basmati rice"], kcal:320, p:7, note:"1 serving, 100g raw-equivalent (KKM)"},
  {names:["nasi minyak","ghee rice"], kcal:380, p:7, note:"1 plate, ghee/oil rice"},

  // ===== NOODLES / MEE, BIHUN, KUETIAU =====
  {names:["mee goreng","mee goreng mamak","mi goreng mamak"], kcal:660, p:17, note:"1 plate, fried yellow noodles mamak style (KKM-aligned)"},
  {names:["maggi goreng"], kcal:750, p:16, note:"fried instant noodles"},
  {names:["bihun goreng","fried bihun","fried vermicelli","mi hoon goreng"], kcal:295, p:8, note:"1 plate, 170g (KKM)"},
  {names:["bihun goreng dengan ayam","fried beehoon with chicken"], kcal:540, p:20, note:"1 set, with fried chicken, 260g (KKM)"},
  {names:["bihun goreng dengan telur","fried beehoon with egg"], kcal:397, p:14, note:"1 set, with egg, 224g (KKM)"},
  {names:["bihun sup","mee hoon soup"], kcal:290, p:12, note:"1 bowl, 450g (KKM)"},
  {names:["bihun bandung","meehoon bandung"], kcal:490, p:18, note:"1 bowl, 450g (KKM)"},
  {names:["kway teow goreng","char kway teow","char kuetiau"], kcal:743, p:18, note:"1 plate, fried flat rice noodles (KKM-aligned)"},
  {names:["fried kuetiau cina","chinese fried kuetiau"], kcal:296, p:9, note:"1 plate, 180g (KKM)"},
  {names:["hokkien mee"], kcal:743, p:22, note:"1 plate, prawn/pork stock fried noodles (general reference)"},
  {names:["mee rebus"], kcal:556, p:18, note:"1 plate, noodles in thick sweet potato gravy (KKM-aligned)"},
  {names:["mee soup","mee sup","noodle soup"], kcal:381, p:16, note:"1 bowl, noodles in clear soup (KKM-aligned)"},
  {names:["wantan mee","wonton mee"], kcal:409, p:20, note:"1 plate, dry, with wonton and char siu (KKM-aligned)"},
  {names:["wantan mee soup","wonton mee soup"], kcal:217, p:14, note:"1 bowl, soup version (KKM-aligned)"},
  {names:["laksa","curry laksa","laksa johor"], kcal:600, p:20, note:"noodles in spicy coconut curry broth"},
  {names:["asam laksa"], kcal:450, p:14, note:"sour fish-based noodle soup"},
  {names:["penang laksa"], kcal:436, p:15, note:"1 bowl (KKM-aligned)"},
  {names:["lor mee"], kcal:383, p:14, note:"1 bowl, thick gravy noodles (KKM-aligned)"},
  {names:["mee hailam","hailam mee"], kcal:277, p:10, note:"1 plate (KKM-aligned)"},
  {names:["prawn mee soup","mee udang"], kcal:293, p:16, note:"1 bowl (KKM-aligned)"},

  // ===== BREAD / ROTI / CAPATI =====
  {names:["roti canai","roti kosong"], kcal:300, p:6, note:"1 piece, plain (KKM-aligned)"},
  {names:["roti canai telur","roti telur"], kcal:414, p:10, note:"1 piece with egg (KKM-aligned)"},
  {names:["roti canai dhal","roti canai with dhal","roti telur dhal"], kcal:359, p:9, note:"1 piece with lentil dhal (KKM-aligned)"},
  {names:["roti tisu"], kcal:380, p:5, note:"crispy sweet roti, 1 serving"},
  {names:["roti bom"], kcal:450, p:7, note:"sweet condensed milk roti"},
  {names:["murtabak","murtabak ayam"], kcal:700, p:25, note:"1 piece, stuffed flatbread"},
  {names:["capati","chapati"], kcal:300, p:8, note:"1 piece, 100g (KKM)"},
  {names:["capati dan kuah dhal","chapati with dhal gravy"], kcal:391, p:11, note:"1 set, 160g (KKM)"},
  {names:["chapati green gravy"], kcal:166, p:5, note:"1 serving (general reference)"},
  {names:["roti putih","white bread"], kcal:70, p:2, note:"1 slice (general reference)"},
  {names:["thosai","dosai","tosai"], kcal:120, p:3, note:"1 piece, plain"},
  {names:["rawa dosai","rava thosai"], kcal:200, p:5, note:"1 piece, semolina dosai"},
  {names:["idli"], kcal:40, p:2, note:"1 piece, steamed rice cake"},
  {names:["putu mayam","string hoppers"], kcal:90, p:2, note:"1 serving"},
  {names:["bhatura"], kcal:420, p:9, note:"1 piece, fried bread, 113g (KKM)"},

  // ===== CURRIES, MEAT, FISH MAINS =====
  {names:["chicken curry","kari ayam","curry chicken","ayam masak kari"], kcal:195, p:18, note:"1 piece with gravy, 125g (KKM-aligned)"},
  {names:["beef rendang","rendang daging","daging rendang"], kcal:232, p:18, note:"1 piece, no rice (KKM-aligned)"},
  {names:["ayam rendang","rendang chicken"], kcal:250, p:18, note:"1 plate, 116g (KKM)"},
  {names:["sambal udang","prawn sambal"], kcal:280, p:18, note:"normal portion, no rice"},
  {names:["sambal sotong"], kcal:55, p:6, note:"half cup (general reference)"},
  {names:["ayam goreng","fried chicken","fried chicken piece"], kcal:290, p:24, note:"1 piece"},
  {names:["ayam goreng berempah","spiced fried chicken"], kcal:226, p:20, note:"1 piece (KKM)"},
  {names:["ayam masak merah"], kcal:255, p:18, note:"1 serving, 118g (KKM)"},
  {names:["ayam masak kicap","soy sauce chicken"], kcal:215, p:18, note:"1 serving, 95g (KKM)"},
  {names:["ayam percik"], kcal:440, p:30, note:"1 piece, 244g (KKM)"},
  {names:["ayam masak kurma"], kcal:180, p:16, note:"1 piece, 125g (KKM)"},
  {names:["ayam tandoori","tandoori chicken"], kcal:135, p:20, note:"1 piece, 100g, without skin (KKM)"},
  {names:["ayam bakar","grilled chicken"], kcal:150, p:22, note:"1 piece, 100g (KKM)"},
  {names:["ayam kukus","steamed chicken"], kcal:208, p:24, note:"1 plate with blanched bean sprouts, 100g (KKM)"},
  {names:["satay ayam","chicken satay","satay"], kcal:365, p:25, note:"10 sticks with peanut sauce (KKM-aligned)"},
  {names:["satay sauce","satay sauce only","kuah satay"], kcal:129, p:4, note:"1/2 cup (KKM)"},
  {names:["mutton curry","kari kambing"], kcal:287, p:20, note:"2 small pieces (KKM-aligned)"},
  {names:["fish curry","kari ikan"], kcal:200, p:18, note:"1 portion, general reference"},
  {names:["fish head curry","kari kepala ikan"], kcal:288, p:24, note:"1 small plate (KKM-aligned)"},
  {names:["char siew","char siu"], kcal:191, p:16, note:"1 small plate (KKM-aligned)"},
  {names:["ikan kembong goreng","fried mackerel"], kcal:140, p:18, note:"1 whole fish (KKM-aligned)"},
  {names:["ikan kembong kari","mackerel curry"], kcal:85, p:14, note:"1 whole fish, gravy-based (KKM-aligned)"},
  {names:["ikan tenggiri goreng","fried spanish mackerel"], kcal:142, p:16, note:"1 piece, with chili (KKM-aligned)"},
  {names:["ikan senangin masam manis","sweet sour fish"], kcal:210, p:18, note:"1 piece with gravy (KKM-aligned)"},
  {names:["telur goreng","fried egg","telur mata"], kcal:92, p:6, note:"1 egg, fried (KKM-aligned)"},
  {names:["telur rebus","boiled egg"], kcal:78, p:6, note:"1 egg"},
  {names:["taukua goreng","fried tofu"], kcal:110, p:8, note:"1 piece (KKM-aligned)"},
  {names:["kacang panggang","baked beans"], kcal:40, p:2, note:"2 tablespoons, canned (KKM-aligned)"},

  // ===== SNACKS / KUIH / FRIED ITEMS =====
  {names:["popiah"], kcal:188, p:5, note:"1 roll, fresh (KKM-aligned)"},
  {names:["fried popiah","popiah goreng"], kcal:220, p:5, note:"1 roll, fried"},
  {names:["pasembur","rojak"], kcal:450, p:12, note:"normal plate with peanut sauce"},
  {names:["rojak chinese style"], kcal:559, p:10, note:"1 serving (KKM-aligned)"},
  {names:["lontong"], kcal:500, p:12, note:"rice cake in coconut vegetable gravy"},
  {names:["curry puff","kuih kapit","epok-epok","karipap"], kcal:246, p:5, note:"2 pieces, chicken filling (KKM-aligned)"},
  {names:["yau char kuih","cakoi","you tiao"], kcal:292, p:5, note:"1 piece (KKM-aligned)"},
  {names:["pisang goreng","goreng pisang"], kcal:129, p:1, note:"1 piece, fried banana (KKM-aligned)"},
  {names:["cucur udang"], kcal:144, p:3, note:"1 piece, prawn fritter (KKM-aligned)"},
  {names:["cucur bawang"], kcal:68, p:2, note:"3 pieces, onion fritter (KKM)"},
  {names:["cucur badak"], kcal:75, p:1, note:"1 piece (KKM)"},
  {names:["cekodok pisang","cokodok pisang"], kcal:180, p:2, note:"1 piece, banana fritter (KKM-aligned)"},
  {names:["apam balik"], kcal:280, p:5, note:"1 folded piece with peanuts (KKM-aligned)"},
  {names:["kuih","kuih muih"], kcal:150, p:2, note:"1 piece, average traditional kuih"},
  {names:["kuih seri muka","seri muka"], kcal:250, p:3, note:"1 potong (general reference)"},
  {names:["kuih ketayap","ketayap","kuih kosui"], kcal:120, p:2, note:"1 piece (general reference)"},
  {names:["kuih talam"], kcal:183, p:2, note:"1 piece (KKM)"},
  {names:["kuih koci"], kcal:183, p:2, note:"1 piece (KKM)"},
  {names:["bingka ubi kayu","bingka tapioca"], kcal:220, p:2, note:"1 piece, 100g (KKM)"},
  {names:["lepat pisang"], kcal:160, p:2, note:"1 piece, banana in coconut wrap (general reference)"},
  {names:["vadai","vada"], kcal:150, p:5, note:"1 piece, lentil fritter (general reference)"},
  {names:["papadam","papadum"], kcal:40, p:2, note:"1 piece (general reference)"},
  {names:["donut","doughnut"], kcal:268, p:3, note:"1 piece (KKM-aligned)"},
  {names:["keropok","fish crackers"], kcal:150, p:2, note:"1 small bowl (general reference)"},
  {names:["chee cheong fun"], kcal:133, p:3, note:"1 roll, plain with sauce (KKM-aligned)"},
  {names:["chee cheong fun char siew"], kcal:65, p:4, note:"1 piece, char siew filling (KKM)"},
  {names:["chee cheong fun udang","chee cheong fun prawn"], kcal:160, p:6, note:"1 piece, prawn filling (KKM)"},
  {names:["siew mai","dim sum siew mai"], kcal:105, p:6, note:"3 pieces (KKM-aligned)"},
  {names:["dim sum","dim sum mixed"], kcal:400, p:18, note:"4-5 normal pieces mixed"},
  {names:["chwee kway"], kcal:40, p:1, note:"1 piece (KKM-aligned)"},
  {names:["curry puff chicken","karipap ayam"], kcal:339, p:8, note:"1 piece, larger version (KKM-aligned)"},

  // ===== INDIAN BANANA LEAF / RICE SET =====
  {names:["banana leaf rice","nasi daun pisang"], kcal:200, p:4, note:"2 scoops plain rice base (KKM-aligned)"},
  {names:["sambal telur goreng"], kcal:130, p:6, note:"1 piece, fried egg with sambal (KKM-aligned)"},
  {names:["sotong goreng","fried squid"], kcal:47, p:6, note:"1 piece (KKM-aligned)"},
  {names:["kari kambing berempah","spiced mutton curry"], kcal:265, p:20, note:"1 bowl (KKM-aligned)"},
  {names:["aloo gobi"], kcal:50, p:2, note:"1 scoop (KKM)"},
  {names:["aloo mattar"], kcal:85, p:3, note:"1 serving, 140g (KKM)"},
  {names:["chana masala"], kcal:110, p:5, note:"1 scoop (general reference)"},
  {names:["dhal","dal curry"], kcal:120, p:6, note:"1 bowl, lentil curry (general reference)"},
  {names:["bak kut teh"], kcal:325, p:25, note:"1 soup bowl with pork ribs, no rice (KKM)"},
  {names:["satay celup"], kcal:350, p:18, note:"normal serving with peanut sauce"},
  {names:["pad thai"], kcal:600, p:20, note:"1 normal plate"},
  {names:["tom yum","tom yam soup"], kcal:200, p:14, note:"1 bowl, no rice"},

  // ===== PORRIDGE / BUBUR =====
  {names:["bubur ayam","chicken porridge"], kcal:177, p:8, note:"1 bowl, 500g (KKM)"},
  {names:["bubur nasi kosong","plain porridge"], kcal:190, p:4, note:"1 cup, 500g (KKM)"},
  {names:["bubur kacang hijau","green bean porridge"], kcal:245, p:8, note:"1 bowl, dessert, 230g (KKM)"},
  {names:["bubur kacang merah","red bean porridge"], kcal:100, p:5, note:"1 bowl, 230g (KKM)"},
  {names:["bubur pulut hitam","black glutinous rice porridge"], kcal:415, p:6, note:"1 bowl, 367g (KKM)"},
  {names:["bubur lambuk"], kcal:202, p:7, note:"1 bowl, 332g (KKM)"},
  {names:["bubur gandum","oatmeal porridge"], kcal:353, p:10, note:"1 bowl, 200g (KKM)"},

  // ===== FAST FOOD =====
  {names:["burger ayam mcd","mcd chicken burger"], kcal:285, p:14, note:"1 piece, 117g (KKM)"},
  {names:["burger keju","cheese burger"], kcal:340, p:16, note:"1 piece, 124g (KKM)"},
  {names:["burger daging lembu","beef burger"], kcal:430, p:22, note:"1 piece, 180g (KKM)"},
  {names:["zinger burger","kfc zinger"], kcal:550, p:24, note:"1 piece, 180g (KKM)"},
  {names:["ayam goreng kfc dada","kfc chicken breast"], kcal:276, p:24, note:"1 piece, 95g (KKM)"},
  {names:["ayam goreng kfc paha","kfc chicken thigh"], kcal:176, p:18, note:"1 piece, 104g (KKM)"},
  {names:["ayam goreng popcorn","popcorn chicken"], kcal:262, p:16, note:"4 pieces, 100g (KKM)"},
  {names:["mcchicken"], kcal:395, p:14, note:"1 piece, 156g (KKM)"},

  // ===== FRUITS =====
  {names:["rambutan"], kcal:75, p:1, note:"100g, about 5-6 fruits (general reference)"},
  {names:["mangosteen","manggis"], kcal:73, p:1, note:"100g flesh (general reference)"},
  {names:["durian"], kcal:147, p:2, note:"100g, about 3 seeds (general reference)"},
  {names:["jackfruit","cempedak","nangka"], kcal:90, p:1, note:"5 pieces, 117g (KKM)"},
  {names:["watermelon","tembikai"], kcal:46, p:1, note:"1 slice (general reference)"},
  {names:["papaya","betik"], kcal:55, p:1, note:"1 slice, 159g, no skin/seeds (KKM)"},
  {names:["mango","mangga"], kcal:150, p:1, note:"1 medium whole (general reference)"},
  {names:["banana","pisang"], kcal:105, p:1, note:"1 medium whole (general reference)"},
  {names:["apple","epal"], kcal:95, p:0, note:"1 medium whole (general reference)"},
  {names:["orange","oren"], kcal:62, p:1, note:"1 medium whole (general reference)"},
  {names:["grapes","anggur"], kcal:60, p:1, note:"8 fruits, 93g (KKM)"},
  {names:["lychee","laici"], kcal:60, p:1, note:"5 pieces, 118g (KKM)"},
  {names:["longan","mata kucing"], kcal:60, p:1, note:"similar serving to lychee (general reference)"},
  {names:["starfruit","belimbing"], kcal:55, p:1, note:"1 whole, 261g (KKM)"},
  {names:["dragon fruit","buah naga"], kcal:78, p:2, note:"1/2 fruit, 160g (KKM)"},
  {names:["avocado","apokat"], kcal:290, p:4, note:"1 whole fruit, 229g (KKM)"},
  {names:["dates","kurma"], kcal:155, p:1, note:"5 pieces, 60g (KKM)"},
  {names:["guava","jambu"], kcal:60, p:2, note:"1 medium whole (general reference)"},
  {names:["pomelo","limau bali"], kcal:90, p:2, note:"1 wedge (general reference)"},
  {names:["soursop","durian belanda"], kcal:100, p:1, note:"1 cup flesh (general reference)"},

// ===== NASI, MEE, BIHUN, KUETIAU (rice & noodle mains) =====
  {names:["bihun bandung sayur telur","bihun bandung dengan sayur dan telur"], kcal:350, p:14, note:"1 mangkuk, 250g, with veg + egg (JKN Selangor)"},
  {names:["bihun goreng 2 senduk"], kcal:290, p:9, note:"2 senduk, 170g (JKN Selangor)"},
  {names:["bihun goreng sayur fish cake"], kcal:240, p:11, note:"2 senduk, 140g, with fish cake (JKN Selangor)"},
  {names:["bihun goreng cina","bihun goreng ala cina"], kcal:220, p:7, note:"2 senduk, 140g (JKN Selangor)"},
  {names:["bihun goreng putih"], kcal:200, p:6, note:"2 senduk, 120g, plain (JKN Selangor)"},
  {names:["bihun goreng singapura"], kcal:150, p:5, note:"2 senduk, 120g (JKN Selangor)"},
  {names:["bihun hailam sayur ayam"], kcal:350, p:16, note:"1 mangkuk, 250g, with chicken (JKN Selangor)"},
  {names:["bihun kantonis sayur ayam"], kcal:430, p:18, note:"1 pinggan, 280g (JKN Selangor)"},
  {names:["bihun kari","mee hoon curry"], kcal:325, p:12, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["bihun kari sayur ayam"], kcal:330, p:15, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["bihun latna sayur ayam"], kcal:380, p:16, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["bihun rebus sayur telur"], kcal:310, p:13, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["bihun sup sayur ayam"], kcal:200, p:11, note:"1 mangkuk, 200g, with chicken (JKN Selangor)"},
  {names:["bihun tom yam sayur ayam"], kcal:230, p:11, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["bubur daging","beef porridge"], kcal:120, p:7, note:"1 mangkuk, 200g (JKN Selangor)"},
  {names:["bubur ikan","fish porridge"], kcal:80, p:5, note:"1 mangkuk, 200g (JKN Selangor)"},
  {names:["bubur nasi sayur ayam"], kcal:140, p:6, note:"1 mangkuk, 150g, mixed (JKN Selangor)"},
  {names:["chap chye"], kcal:50, p:2, note:"1 senduk, 60g, mixed veg stew (JKN Selangor)"},
  {names:["char kuetiau 2 senduk"], kcal:230, p:7, note:"2 senduk, 120g (JKN Selangor)"},
  {names:["ketupat nasi"], kcal:215, p:4, note:"5 potong, 200g (JKN Selangor)"},
  {names:["kuetiau bandung"], kcal:540, p:18, note:"1 mangkuk kecil, 450g (JKN Selangor)"},
  {names:["kuetiau bandung sayur telur"], kcal:300, p:13, note:"1 mangkuk kecil, 200g (JKN Selangor)"},
  {names:["kuetiau goreng sayur fish cake"], kcal:250, p:10, note:"2 senduk, 120g (JKN Selangor)"},
  {names:["kuetiau goreng 2 senduk"], kcal:320, p:9, note:"2 senduk, 170g (JKN Selangor)"},
  {names:["kuetiau hailam sayur ayam"], kcal:380, p:17, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["kuetiau kantonis sayur ayam"], kcal:410, p:18, note:"1 pinggan, 280g (JKN Selangor)"},
  {names:["kuetiau kari","kuey teow curry"], kcal:315, p:11, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["kuetiau kari sayur ayam"], kcal:320, p:14, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["kuetiau latna sayur ayam"], kcal:320, p:14, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["kuetiau sup","kuey teow soup"], kcal:140, p:8, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["kuetiau sup sayur ayam"], kcal:140, p:9, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["kuetiau tom yam sayur ayam"], kcal:210, p:11, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["laksa sayur telur"], kcal:240, p:11, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["laksa sarawak"], kcal:320, p:13, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["lemang"], kcal:100, p:2, note:"1 potong, 30g, glutinous rice in bamboo (JKN Selangor)"},
  {names:["lontong nasi impit"], kcal:340, p:9, note:"1 mangkuk, 300g (JKN Selangor)"},
  {names:["makaroni ayam"], kcal:150, p:7, note:"1 senduk, 100g (JKN Selangor)"},
  {names:["makaroni bakar","baked macaroni"], kcal:150, p:6, note:"2 senduk, 90g (JKN Selangor)"},
  {names:["makaroni goreng","fried macaroni"], kcal:300, p:8, note:"2 senduk, 90g (JKN Selangor)"},
  {names:["mi bandung","mee bandung"], kcal:550, p:18, note:"1 mangkuk, 450g (JKN Selangor)"},
  {names:["mi bandung sayur ayam"], kcal:310, p:14, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["mi goreng 3 senduk"], kcal:280, p:9, note:"3 senduk, 170g (JKN Selangor)"},
  {names:["mi goreng sayur fish cake"], kcal:250, p:10, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["mi goreng mamak 3 senduk"], kcal:270, p:9, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["mi hailam sayur ayam"], kcal:340, p:16, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["mi hailam berkuah"], kcal:340, p:13, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["mi kantonis sayur ayam"], kcal:410, p:18, note:"1 mangkuk, 280g (JKN Selangor)"},
  {names:["mi kari","mee curry"], kcal:530, p:17, note:"1 mangkuk, 410g (JKN Selangor)"},
  {names:["mi kari sayur ayam"], kcal:320, p:14, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["mi kungfu","kungfu mee"], kcal:220, p:9, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["mi latna sayur ayam"], kcal:400, p:17, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["mi rebus sayur telur"], kcal:170, p:8, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["mi siam"], kcal:120, p:5, note:"2 senduk, 100g (JKN Selangor)"},
  {names:["mi sup besar"], kcal:380, p:14, note:"1 mangkuk besar, 560g (JKN Selangor)"},
  {names:["mi sup sayur ayam"], kcal:170, p:9, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["mi tom yam sayur ayam"], kcal:130, p:8, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["mi udang sup","prawn mee soup big bowl"], kcal:250, p:14, note:"1 mangkuk, 480g (JKN Selangor)"},
  {names:["mi wantan sup","wonton mee soup small"], kcal:125, p:8, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["nasi ambang"], kcal:325, p:12, note:"1 hidangan, 250g, mixed rice set (JKN Selangor)"},
  {names:["nasi ayam nasi sahaja","chicken rice rice only"], kcal:160, p:3, note:"2 senduk, 100g, rice only (JKN Selangor)"},
  {names:["nasi ayam set"], kcal:280, p:13, note:"1 pinggan, 250g (JKN Selangor)"},
  {names:["nasi ayam lengkap","nasi ayam ayam sayur sos cili"], kcal:450, p:22, note:"1 pinggan, 250g, full set (JKN Selangor)"},
  {names:["nasi beriani nasi sahaja"], kcal:200, p:4, note:"1 cawan, 110g, rice only (JKN Selangor)"},
  {names:["nasi briyani set"], kcal:460, p:18, note:"1 pinggan, 250g (JKN Selangor)"},
  {names:["nasi briyani ayam goreng sayur dal"], kcal:450, p:20, note:"1 pinggan, 250g, full set (JKN Selangor)"},
  {names:["nasi goreng 3 senduk"], kcal:290, p:8, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng biasa sayur fish cake"], kcal:290, p:9, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng ayam cendawan set"], kcal:450, p:20, note:"1 set, 240g (JKN Selangor)"},
  {names:["nasi goreng cendawan","mushroom fried rice"], kcal:290, p:7, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng cina"], kcal:320, p:9, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng cina sayur telur"], kcal:320, p:11, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng gajus","cashew fried rice"], kcal:330, p:8, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng ikan masin","salted fish fried rice"], kcal:280, p:8, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng kampung 3 senduk"], kcal:270, p:8, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng kerabu"], kcal:340, p:9, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng lada hitam sayur ayam"], kcal:290, p:13, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng paprik"], kcal:240, p:7, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng paprik sayur ayam"], kcal:240, p:12, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng pattaya sayur ayam telur dadar"], kcal:370, p:15, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng pattaya"], kcal:285, p:10, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng udang sayur"], kcal:380, p:14, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng usa"], kcal:285, p:9, note:"3 senduk, 150g (JKN Selangor)"},
  {names:["nasi goreng usa udang fried egg"], kcal:490, p:18, note:"3 senduk, 150g, full set (JKN Selangor)"},
  {names:["nasi impit"], kcal:80, p:2, note:"8 kiub, 50g (JKN Selangor)"},
  {names:["nasi kerabu set"], kcal:260, p:10, note:"1 set, 250g (JKN Selangor)"},
  {names:["nasi khabsa"], kcal:280, p:9, note:"1 cawan, 110g (JKN Selangor)"},
  {names:["nasi lemak biasa set"], kcal:320, p:7, note:"1 set, 180g (JKN Selangor)"},
  {names:["nasi lemak ayam goreng berempah timun sambal"], kcal:490, p:20, note:"1 set, 220g (JKN Selangor)"},
  {names:["nasi lemak rendang ayam daging timun sambal"], kcal:420, p:18, note:"1 set (JKN Selangor)"},
  {names:["nasi lemak sambal sotong timun sambal"], kcal:410, p:16, note:"1 set, 210g (JKN Selangor)"},
  {names:["nasi lemak telur mata kerbau timun sambal"], kcal:350, p:10, note:"1 set, 180g (JKN Selangor)"},
  {names:["nasi nenas","pineapple fried rice"], kcal:160, p:3, note:"3 senduk, 170g (JKN Selangor)"},
  {names:["nasi tomato"], kcal:185, p:4, note:"2 senduk, 100g (JKN Selangor)"},
  {names:["pasta plain"], kcal:165, p:6, note:"2 senduk, 110g (JKN Selangor)"},
  {names:["soto"], kcal:260, p:10, note:"1 mangkuk, 250g (JKN Selangor)"},
  {names:["soto ayam besar","chicken soto large"], kcal:510, p:22, note:"1 mangkuk, 490g (JKN Selangor)"},
  {names:["spaghetti keju sos daging","spaghetti with cheese and meat sauce"], kcal:440, p:18, note:"1 mangkuk, 440g (JKN Selangor)"},

  // ===== AYAM DAN DAGING (chicken & meat dishes) =====
  {names:["ayam gajus","cashew chicken"], kcal:165, p:13, note:"1 senduk, 50g (JKN Selangor)"},
  {names:["ayam goreng 1 ketul besar"], kcal:270, p:22, note:"1 ketul, 120g (JKN Selangor)"},
  {names:["ayam goreng berempah 1 ketul"], kcal:200, p:18, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["ayam goreng madu","honey fried chicken"], kcal:240, p:18, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["ayam masak cili","chili chicken"], kcal:140, p:14, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["ayam masak halia","ginger chicken small"], kcal:60, p:6, note:"1 senduk, 50g (JKN Selangor)"},
  {names:["ayam masak kicap 1 ketul"], kcal:200, p:16, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["ayam masak kunyit","turmeric chicken small"], kcal:80, p:7, note:"1 senduk, 50g (JKN Selangor)"},
  {names:["ayam masak kurma 1 ketul"], kcal:190, p:15, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["ayam masak kuzi"], kcal:180, p:14, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["ayam masak lemak cili api"], kcal:150, p:13, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["ayam masak lemon","lemon chicken"], kcal:160, p:14, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["ayam masak lengkuas","galangal chicken small"], kcal:80, p:7, note:"1 senduk, 50g (JKN Selangor)"},
  {names:["ayam masak merah 1 ketul small"], kcal:140, p:13, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["ayam masak nyonya"], kcal:140, p:13, note:"1 ketul, 80g (JKN Selangor)"},
  {names:["ayam masak paprik small"], kcal:70, p:7, note:"1 senduk, 70g (JKN Selangor)"},
  {names:["ayam masak sambal 1 ketul"], kcal:180, p:16, note:"1 ketul, 100g (JKN Selangor)"},
  {names:["ayam masak tomato"], kcal:150, p:15, note:"1 ketul, 100g (JKN Selangor)"},
  {names:["ayam panggang 1 ketul"], kcal:130, p:16, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["ayam panggang tanpa kulit","grilled chicken skinless"], kcal:150, p:18, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["ayam percik 1 ketul kecil"], kcal:140, p:14, note:"1 ketul, 80g (JKN Selangor)"},
  {names:["ayam percik kelantan"], kcal:140, p:14, note:"1 ketul, 80g (JKN Selangor)"},
  {names:["ayam seroja"], kcal:110, p:11, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["ayam tandoori 1 ketul besar"], kcal:200, p:20, note:"1 ketul, 100g (JKN Selangor)"},
  {names:["ayam tandoori tanpa kulit"], kcal:175, p:21, note:"1 ketul, 100g, skinless (JKN Selangor)"},
  {names:["bebola ikan goreng","fried fish balls"], kcal:105, p:6, note:"1 senduk, 40g (JKN Selangor)"},
  {names:["bebola ikan masak sambal","fish balls in sambal"], kcal:110, p:7, note:"1 senduk, 70g (JKN Selangor)"},
  {names:["burger daging ayam set"], kcal:240, p:14, note:"1 set, 100g (JKN Selangor)"},
  {names:["burger daging ayam special"], kcal:290, p:16, note:"1 set, 130g (JKN Selangor)"},
  {names:["buttered prawn","prawn in butter sauce"], kcal:180, p:14, note:"5 ekor, 100g (JKN Selangor)"},
  {names:["chicken boxing"], kcal:120, p:10, note:"3 ketul, 50g (JKN Selangor)"},
  {names:["chilli prawn chinese style"], kcal:120, p:11, note:"3 ekor, 60g (JKN Selangor)"},
  {names:["daging asam pedas small"], kcal:70, p:6, note:"2 ketul, 80g (JKN Selangor)"},
  {names:["daging belada","beef with chili"], kcal:90, p:7, note:"2 ketul, 80g (JKN Selangor)"},
  {names:["daging dendeng","dried spiced beef"], kcal:125, p:9, note:"1 ketul, 35g (JKN Selangor)"},
  {names:["daging goreng 1 ketul"], kcal:140, p:9, note:"1 ketul, 40g (JKN Selangor)"},
  {names:["daging goreng kunyit","turmeric fried beef"], kcal:80, p:7, note:"1 senduk, 80g (JKN Selangor)"},
  {names:["daging kambing goreng","fried mutton"], kcal:220, p:14, note:"2 ketul, 80g (JKN Selangor)"},
  {names:["daging kambing masak kurma","mutton kurma"], kcal:120, p:9, note:"1 senduk, 80g (JKN Selangor)"},
  {names:["daging kicap berempah"], kcal:80, p:6, note:"1 ketul, 60g (JKN Selangor)"},
  {names:["daging lembu goreng 1 ketul"], kcal:140, p:9, note:"1 ketul, 40g (JKN Selangor)"},
  {names:["daging lembu masak merah"], kcal:140, p:10, note:"1 ketul + kuah, 90g (JKN Selangor)"},
  {names:["daging masak asam pedas small"], kcal:45, p:4, note:"1 ketul, 40g (JKN Selangor)"},
  {names:["daging masak dendeng","dendeng beef cooked"], kcal:215, p:13, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["daging masak halia","ginger beef"], kcal:90, p:7, note:"2 ketul, 60g (JKN Selangor)"},
  {names:["daging masak hitam","black sauce beef"], kcal:145, p:10, note:"1 senduk, 90g (JKN Selangor)"},
  {names:["daging masak kicap 1 ketul"], kcal:80, p:6, note:"1 ketul, 60g (JKN Selangor)"},
  {names:["daging masak kurma 2 ketul"], kcal:80, p:6, note:"2 ketul, 80g (JKN Selangor)"},
  {names:["daging masak lada hitam","black pepper beef"], kcal:180, p:13, note:"3 ketul, 90g (JKN Selangor)"},
  {names:["daging masak lemak cili api small"], kcal:65, p:5, note:"1 ketul, 42g (JKN Selangor)"},
  {names:["daging masak singgang"], kcal:100, p:9, note:"3 ketul, 90g (JKN Selangor)"},
  {names:["daging masak taucu","beef with fermented bean"], kcal:180, p:11, note:"1 senduk, 80g (JKN Selangor)"},
  {names:["daging merah ala thai"], kcal:100, p:8, note:"2 keping, 60g (JKN Selangor)"},
  {names:["daging palembang"], kcal:110, p:7, note:"1 ketul, 30g (JKN Selangor)"},
  {names:["daging salai masak lemak","smoked beef in coconut gravy"], kcal:190, p:12, note:"3 ketul, 110g (JKN Selangor)"},
  {names:["daging tetel masak asam pedas"], kcal:160, p:11, note:"3 ketul, 90g (JKN Selangor)"},
  {names:["kari kambing small","mutton curry small"], kcal:140, p:11, note:"2 ketul, 80g (JKN Selangor)"},
  {names:["kari lembu","beef curry"], kcal:130, p:10, note:"2 ketul, 90g (JKN Selangor)"},
  {names:["kari telur half","egg curry half"], kcal:130, p:6, note:"1/2 biji, 20g (JKN Selangor)"},
  {names:["kerabu perut","tripe salad"], kcal:80, p:8, note:"1 senduk, 70g (JKN Selangor)"},
  {names:["kuzee ayam"], kcal:145, p:10, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["paru lembu goreng","fried beef lung"], kcal:290, p:18, note:"1 keping, 60g (JKN Selangor)"},
  {names:["puyuh masak sambal","quail in sambal"], kcal:145, p:13, note:"1 ekor, 100g (JKN Selangor)"},
  {names:["rendang ayam small","chicken rendang small"], kcal:100, p:8, note:"1 senduk, 50g (JKN Selangor)"},
  {names:["rendang daging lembu small"], kcal:130, p:9, note:"2 keping, 50g (JKN Selangor)"},
  {names:["sate ayam 5 cucuk"], kcal:200, p:18, note:"5 cucuk, 80g (JKN Selangor)"},
  {names:["sate daging lembu 5 cucuk"], kcal:190, p:16, note:"5 cucuk, 80g (JKN Selangor)"},
  {names:["sosej","sausage"], kcal:100, p:5, note:"1 ketul, 30g (JKN Selangor)"},
  {names:["sosej roti bakar scramble egg","sausage toast scrambled egg"], kcal:310, p:14, note:"1 set, 160g (JKN Selangor)"},
  {names:["sup ayam","chicken soup small"], kcal:80, p:7, note:"1 mangkuk kecil, 150g (JKN Selangor)"},
  {names:["sup daging","beef soup small"], kcal:90, p:8, note:"1 mangkuk kecil, 150g (JKN Selangor)"},
  {names:["sup ekor","oxtail soup"], kcal:120, p:10, note:"1 mangkuk kecil, 150g (JKN Selangor)"},
  {names:["sup tulang","bone soup"], kcal:75, p:6, note:"1 mangkuk, 150g (JKN Selangor)"},
  {names:["telur half masak","egg half boiled"], kcal:80, p:6, note:"1 biji, 50g (JKN Selangor)"},
  {names:["telur dadar","omelette plain"], kcal:100, p:6, note:"1 potong, 45g (JKN Selangor)"},
  {names:["telur mata kerbau","sunny side up egg"], kcal:110, p:6, note:"1 biji, 54g (JKN Selangor)"},

  // ===== IKAN DAN HASIL LAUT (fish & seafood) =====
  {names:["ikan acar","pickled fish"], kcal:155, p:14, note:"1 ekor, 90g (JKN Selangor)"},
  {names:["ikan bawal hitam goreng","fried black pomfret"], kcal:150, p:16, note:"1 ekor, 100g (JKN Selangor)"},
  {names:["ikan bawal hitam masak 3 rasa"], kcal:210, p:17, note:"1 ekor, 100g (JKN Selangor)"},
  {names:["ikan bawal putih goreng","fried white pomfret"], kcal:190, p:15, note:"1 ekor, 80g (JKN Selangor)"},
  {names:["ikan cencaru goreng belada"], kcal:200, p:16, note:"2 potong, 150g (JKN Selangor)"},
  {names:["ikan cencaru kukus","steamed mackerel"], kcal:80, p:14, note:"1 ekor, 100g (JKN Selangor)"},
  {names:["ikan haruan kering goreng","fried dried snakehead fish"], kcal:160, p:14, note:"1 ekor kecil, 40g (JKN Selangor)"},
  {names:["ikan keli goreng berlada","fried catfish with chili"], kcal:90, p:11, note:"1 ekor, 90g (JKN Selangor)"},
  {names:["ikan kembong bakar","grilled mackerel"], kcal:80, p:13, note:"1 ekor, 70g (JKN Selangor)"},
  {names:["ikan kembong goreng (1 ekor kecil)"], kcal:160, p:14, note:"1 ekor, 70g (JKN Selangor)"},
  {names:["ikan kembong goreng belada"], kcal:300, p:18, note:"1 ekor, 110g (JKN Selangor)"},
  {names:["ikan kembong masak asam rebus"], kcal:100, p:13, note:"1 ekor, 80g (JKN Selangor)"},
  {names:["ikan kembong masak kicap"], kcal:160, p:13, note:"1 ekor, 80g (JKN Selangor)"},
  {names:["ikan kembong masak taucu"], kcal:130, p:12, note:"1 ekor, 80g (JKN Selangor)"},
  {names:["ikan kerisi goreng"], kcal:205, p:15, note:"1 ekor, 75g (JKN Selangor)"},
  {names:["ikan kerisi masak kicap"], kcal:150, p:13, note:"1 ekor, 75g (JKN Selangor)"},
  {names:["ikan masam manis","sweet sour fish whole"], kcal:220, p:15, note:"1 ekor, 80g (JKN Selangor)"},
  {names:["ikan masin goreng bawang","fried salted fish with onion"], kcal:100, p:9, note:"3 ketul, 50g (JKN Selangor)"},
  {names:["ikan masin masak lemak","salted fish in coconut gravy"], kcal:145, p:9, note:"1 senduk, 50g (JKN Selangor)"},
  {names:["ikan merah goreng berlada small"], kcal:130, p:11, note:"1 potong kecil, 50g (JKN Selangor)"},
  {names:["ikan merah masak asam"], kcal:180, p:13, note:"1 potong sederhana, 80g (JKN Selangor)"},
  {names:["ikan merah masak lemak"], kcal:200, p:13, note:"1 potong sederhana, 80g (JKN Selangor)"},
  {names:["ikan merah singgang"], kcal:115, p:13, note:"1 ekor, 80g (JKN Selangor)"},
  {names:["ikan pari masak asam pedas"], kcal:120, p:11, note:"1 potong, 60g (JKN Selangor)"},
  {names:["ikan selar goreng"], kcal:105, p:9, note:"1 ekor, 60g (JKN Selangor)"},
  {names:["ikan selar kuning goreng"], kcal:100, p:9, note:"1 ekor, 60g (JKN Selangor)"},
  {names:["ikan sembilang goreng"], kcal:280, p:18, note:"1 ekor, 100g (JKN Selangor)"},
  {names:["ikan senangin goreng"], kcal:220, p:15, note:"1 ekor, 80g (JKN Selangor)"},
  {names:["ikan senangin masak cili"], kcal:145, p:11, note:"1 potong, 60g (JKN Selangor)"},
  {names:["ikan tenggiri asam pedas"], kcal:120, p:10, note:"1 keping, 55g (JKN Selangor)"},
  {names:["ikan tenggiri goreng (1 keping)"], kcal:190, p:14, note:"1 keping, 60g (JKN Selangor)"},
  {names:["ikan tiga rasa","fish 3 flavour"], kcal:80, p:9, note:"1 ekor, 80g (JKN Selangor)"},
  {names:["ikan tilapia goreng berlada"], kcal:145, p:11, note:"1 ekor, 60g (JKN Selangor)"},
  {names:["ikan tilapia masak lemak"], kcal:70, p:8, note:"1 ekor, 60g (JKN Selangor)"},
  {names:["isi ikan fillet","fish fillet plain"], kcal:105, p:11, note:"3 ketul, 45g (JKN Selangor)"},
  {names:["kari ikan kembong"], kcal:70, p:9, note:"1 ekor, 80g (JKN Selangor)"},
  {names:["kari ikan masin","salted fish curry"], kcal:95, p:7, note:"3 ketul, 60g (JKN Selangor)"},
  {names:["kerabu sotong","squid salad"], kcal:55, p:6, note:"1 senduk, 50g (JKN Selangor)"},
  {names:["kerang masak sambal","cockles in sambal"], kcal:60, p:5, note:"1 senduk, 55g (JKN Selangor)"},
  {names:["keropok ikan"], kcal:150, p:3, note:"5 keping, 30g (JKN Selangor)"},
  {names:["keropok udang"], kcal:85, p:1, note:"1/2 cawan, 20g (JKN Selangor)"},
  {names:["ketam masak cili","crab in chili"], kcal:140, p:14, note:"2 ekor, 100g (JKN Selangor)"},
  {names:["nugget ayam","chicken nugget"], kcal:60, p:3, note:"1 keping, 20g (JKN Selangor)"},
  {names:["otak otak"], kcal:70, p:5, note:"1 keping, 30g (JKN Selangor)"},
  {names:["sambal goreng ikan bilis kacang tanah"], kcal:150, p:7, note:"1 senduk, 50g (JKN Selangor)"},
  {names:["sambal ikan bilis","anchovy sambal"], kcal:100, p:5, note:"2 sudu makan, 30g (JKN Selangor)"},
  {names:["sambal sotong (4 ekor kecil)"], kcal:100, p:7, note:"4 ekor kecil, 80g (JKN Selangor)"},
  {names:["sambal telur rebus","boiled egg sambal"], kcal:160, p:7, note:"1 biji, 60g (JKN Selangor)"},
  {names:["sambal tumis udang","prawn sambal tumis"], kcal:145, p:10, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["sotong goreng kunyit","turmeric fried squid"], kcal:90, p:8, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["sotong goreng tepung","battered fried squid"], kcal:150, p:8, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["sotong masak kicap","squid soy sauce"], kcal:90, p:7, note:"2 ekor, 60g (JKN Selangor)"},
  {names:["udang goreng kunyit","turmeric fried prawn"], kcal:90, p:9, note:"3 ekor sederhana, 80g (JKN Selangor)"},

  // ===== BUAH-BUAHAN (fruits, more entries) =====
  {names:["acar timun","pickled cucumber"], kcal:50, p:0, note:"1 senduk, 50g (JKN Selangor)"},
  {names:["belimbing (starfruit, JKN portion)","starfruit (whole)"], kcal:70, p:1, note:"1 biji, 300g (JKN Selangor)"},
  {names:["betik (papaya, potong sederhana)","papaya (medium slice)"], kcal:70, p:1, note:"1 potong sederhana, 200g (JKN Selangor)"},
  {names:["buah lai","durian-like fruit"], kcal:70, p:1, note:"1 biji sederhana, 200g (JKN Selangor)"},
  {names:["epal hijau","green apple"], kcal:60, p:0, note:"1 biji, 110g (JKN Selangor)"},
  {names:["epal merah","red apple"], kcal:60, p:0, note:"1 biji, 110g (JKN Selangor)"},
  {names:["jagung rebus","boiled corn"], kcal:110, p:3, note:"1 cawan kecil, 120g (JKN Selangor)"},
  {names:["jambu air","water apple"], kcal:10, p:0, note:"1 biji, 50g (JKN Selangor)"},
  {names:["jambu batu (potong sederhana)","guava (medium slice)"], kcal:70, p:1, note:"1/2 biji tanpa biji, 150g (JKN Selangor)"},
  {names:["mangga (biji sederhana)","mango (medium fruit)"], kcal:70, p:1, note:"1 biji sederhana, 100g (JKN Selangor)"},
  {names:["nenas (potong sederhana)","pineapple (medium slice)"], kcal:60, p:0, note:"1 potong sederhana, 130g (JKN Selangor)"},
  {names:["pisang berangan"], kcal:60, p:1, note:"1 biji sederhana, 90g (JKN Selangor)"},
  {names:["pisang mas"], kcal:80, p:1, note:"2 biji sederhana, 100g (JKN Selangor)"},
  {names:["tembikai JKN","watermelon JKN"], kcal:40, p:1, note:"1 potong sederhana, 130g (JKN Selangor)"},

  // ===== SAYUR-SAYURAN (vegetables) =====
  {names:["bayam goreng","fried spinach"], kcal:80, p:2, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["brocolli cauliflower goreng"], kcal:20, p:1, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["cekur manis masak lemak"], kcal:120, p:3, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["dalca kacang kuda"], kcal:130, p:5, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["dalca sayur","vegetable dhal"], kcal:130, p:5, note:"1 senduk, 80g (JKN Selangor)"},
  {names:["fucuk tumis air","stir fried beancurd skin"], kcal:80, p:4, note:"1 senduk, 90g (JKN Selangor)"},
  {names:["kacang botol goreng","four-angled bean fried"], kcal:50, p:2, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["kacang buncis goreng","fried green beans"], kcal:40, p:2, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["kacang kuda rebus","boiled peanuts"], kcal:160, p:7, note:"1 senduk, 50g (JKN Selangor)"},
  {names:["kacang panjang goreng","fried long beans"], kcal:55, p:2, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["kailan goreng"], kcal:40, p:2, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["kailan ikan masin"], kcal:80, p:4, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["kailan masak sos tiram","kailan oyster sauce"], kcal:40, p:2, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["kangkung goreng"], kcal:50, p:2, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["kari sayur","vegetable curry"], kcal:60, p:2, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["keladi masak asam rebus"], kcal:60, p:1, note:"1 mangkuk kecil, 100g (JKN Selangor)"},
  {names:["keledek goreng","fried sweet potato"], kcal:170, p:1, note:"2 keping, 40g (JKN Selangor)"},
  {names:["keledek keladi goreng"], kcal:175, p:1, note:"3 keping, 90g (JKN Selangor)"},
  {names:["kobis goreng","fried cabbage"], kcal:50, p:1, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["kobis masak lemak putih","cabbage white coconut gravy"], kcal:135, p:3, note:"1 senduk, 70g (JKN Selangor)"},
  {names:["labu kuning masak lemak","pumpkin in coconut milk"], kcal:50, p:1, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["lontong sayur lodeh","lontong with vegetable stew"], kcal:280, p:8, note:"1 mangkuk, 270g (JKN Selangor)"},
  {names:["peria goreng telur","bitter gourd egg fried"], kcal:70, p:3, note:"1 senduk, 40g (JKN Selangor)"},
  {names:["pucuk manis labu kuning masak lemak"], kcal:150, p:4, note:"1 senduk, 105g (JKN Selangor)"},
  {names:["pucuk paku masak lemak","fiddlehead fern coconut milk"], kcal:140, p:3, note:"1 senduk, 40g (JKN Selangor)"},
  {names:["rebung masak lemak","bamboo shoot coconut milk"], kcal:50, p:1, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["sawi chap choy goreng"], kcal:50, p:2, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["sawi hijau goreng sos tiram"], kcal:55, p:2, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["sawi putih goreng"], kcal:50, p:2, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["sayur campur goreng"], kcal:50, p:2, note:"1 senduk, 60g (JKN Selangor)"},
  {names:["sayur goreng jawa"], kcal:70, p:2, note:"1 senduk, 50g (JKN Selangor)"},
  {names:["sayur lodeh","vegetable stew coconut"], kcal:125, p:4, note:"2 senduk, 90g (JKN Selangor)"},
  {names:["sup cendawan","mushroom soup"], kcal:75, p:2, note:"1 mangkuk kecil, 150g (JKN Selangor)"},
  {names:["sup sayur campur"], kcal:45, p:2, note:"1 mangkuk kecil, 150g (JKN Selangor)"},
  {names:["sup yong tau foo"], kcal:50, p:4, note:"1 senduk, 50g (JKN Selangor)"},
  {names:["taugeh","bean sprouts plain"], kcal:10, p:1, note:"1 senduk, 30g (JKN Selangor)"},
  {names:["taugeh sos tiram"], kcal:40, p:2, note:"1 senduk, 40g (JKN Selangor)"},
  {names:["terung goreng berlada","fried eggplant with chili"], kcal:70, p:1, note:"1 senduk, 70g (JKN Selangor)"},
  {names:["ubi kayu goreng","fried tapioca"], kcal:145, p:1, note:"3 keping, 90g (JKN Selangor)"},
  {names:["ulam JKN","raw ulam vegetables"], kcal:10, p:1, note:"1 cawan, 30g (JKN Selangor)"},

  // ===== KEKACANG (tofu, tempeh, legumes) =====
  {names:["sup tauhu jepun","japanese tofu soup"], kcal:60, p:5, note:"1 senduk, 90g (JKN Selangor)"},
  {names:["tauhu goreng (1 keping kecil)"], kcal:70, p:5, note:"1 keping, 40g (JKN Selangor)"},
  {names:["tauhu kukus","steamed tofu"], kcal:35, p:4, note:"1 keping, 50g (JKN Selangor)"},
  {names:["tauhu masak sos tiram","tofu oyster sauce"], kcal:100, p:7, note:"1 ketul, 90g (JKN Selangor)"},
  {names:["tauhu sambal (1 keping)"], kcal:105, p:6, note:"1 keping, 70g (JKN Selangor)"},
  {names:["tauhu sumbat (2 keping)","stuffed tofu (2 pieces)"], kcal:140, p:9, note:"2 keping, 100g (JKN Selangor)"},
  {names:["tempe goreng JKN","tempe goreng (1 keping besar)"], kcal:255, p:13, note:"1 keping, 70g (JKN Selangor)"},
  {names:["tempe goreng cili"], kcal:80, p:4, note:"1 senduk, 40g (JKN Selangor)"},
  {names:["tempe goreng jawa"], kcal:100, p:5, note:"1 senduk, 40g (JKN Selangor)"},

  // ===== KUIH MUIH, SNEK DAN PENCUCI MULUT (kuih, snacks, desserts) =====
  {names:["agar agar buah","fruit agar agar"], kcal:20, p:0, note:"1 potong kecil, 30g (JKN Selangor)"},
  {names:["aiskrim coklat","chocolate ice cream"], kcal:305, p:4, note:"2 senduk, 70g (JKN Selangor)"},
  {names:["aneka kuih talam","assorted kuih talam"], kcal:60, p:1, note:"1 ketul, 40g (JKN Selangor)"},
  {names:["apam kukus"], kcal:60, p:1, note:"1 biji, 30g (JKN Selangor)"},
  {names:["apam balik JKN besar","apam balik large piece"], kcal:290, p:5, note:"1 keping besar, 120g (JKN Selangor)"},
  {names:["apam beras","rice apam"], kcal:50, p:1, note:"1 biji, 30g (JKN Selangor)"},
  {names:["apam butter"], kcal:110, p:2, note:"1 keping, 40g (JKN Selangor)"},
  {names:["apam gula hangus","caramel apam"], kcal:160, p:2, note:"1 biji, 50g (JKN Selangor)"},
  {names:["apam pisang","banana apam"], kcal:110, p:2, note:"1 keping, 40g (JKN Selangor)"},
  {names:["apam putih kukus kelapa"], kcal:95, p:2, note:"1 biji, 50g (JKN Selangor)"},
  {names:["apam salut kelapa","coconut coated apam"], kcal:110, p:2, note:"1 biji, 40g (JKN Selangor)"},
  {names:["baulu","traditional sponge cake"], kcal:40, p:1, note:"1 ketul, 10g (JKN Selangor)"},
  {names:["bergedil kentang","potato patty"], kcal:110, p:3, note:"1 ketul, 50g (JKN Selangor)"},
  {names:["bijirin sarapan","breakfast cereal"], kcal:130, p:3, note:"1 cawan, 40g (JKN Selangor)"},
  {names:["bingka jagung","corn bingka"], kcal:150, p:2, note:"1 potong, 30g (JKN Selangor)"},
  {names:["bingka pandan"], kcal:80, p:1, note:"1 potong, 40g (JKN Selangor)"},
  {names:["bingka roti","bread bingka"], kcal:80, p:2, note:"1 potong, 70g (JKN Selangor)"},
  {names:["bingka tepung beras","rice flour bingka"], kcal:75, p:1, note:"1 potong, 40g (JKN Selangor)"},
  {names:["biskut almond london"], kcal:30, p:0, note:"1 keping, 5g (JKN Selangor)"},
  {names:["biskut cornflakes"], kcal:80, p:1, note:"2 keping, 15g (JKN Selangor)"},
  {names:["biskut kraker","cream cracker"], kcal:40, p:1, note:"1 keping, 10g (JKN Selangor)"},
  {names:["biskut marie"], kcal:100, p:2, note:"3 keping, 20g (JKN Selangor)"},
  {names:["biskut oat","oat biscuit"], kcal:200, p:4, note:"3 keping, 40g (JKN Selangor)"},
  {names:["buah melaka","gula melaka sweet balls"], kcal:60, p:1, note:"2 biji kecil, 30g (JKN Selangor)"},
  {names:["bubur cha cha (mangkuk kecil)"], kcal:180, p:2, note:"1 mangkuk kecil, 120g (JKN Selangor)"},
  {names:["bubur jagung","corn porridge dessert"], kcal:210, p:3, note:"2 senduk, 100g (JKN Selangor)"},
  {names:["bubur kacang hijau (mangkuk kecil)"], kcal:240, p:8, note:"1 mangkuk kecil, 230g (JKN Selangor)"},
  {names:["bubur kacang merah (mangkuk kecil)"], kcal:101, p:4, note:"1 mangkuk kecil, 230g (JKN Selangor)"},
  {names:["bubur pulut hitam (mangkuk kecil)"], kcal:115, p:2, note:"1 mangkuk kecil, 150g (JKN Selangor)"},
  {names:["bun ikan bilis","anchovy bun"], kcal:180, p:5, note:"1 biji, 60g (JKN Selangor)"},
  {names:["bun kacang","red bean bun"], kcal:190, p:5, note:"1 biji, 60g (JKN Selangor)"},
  {names:["bun kismis","raisin bun"], kcal:115, p:3, note:"1 biji, 40g (JKN Selangor)"},
  {names:["bun pandan kelapa","pandan coconut bun"], kcal:165, p:3, note:"1 biji, 50g (JKN Selangor)"},
  {names:["burger daging set","beef burger set"], kcal:320, p:15, note:"1 set, 130g (JKN Selangor)"},
  {names:["butter cookies"], kcal:130, p:1, note:"3 keping, 30g (JKN Selangor)"},
];

let log = [];

function normalize(s){ return s.toLowerCase().trim().replace(/\s+/g,' '); }

// word-boundary substring check: true only if `needle` appears in `haystack`
// as a whole word or sequence of whole words, not as a raw character substring
// (prevents false matches like "oren" inside "goreng")
function containsWholeWords(haystack, needle){
  return (' ' + haystack + ' ').includes(' ' + needle + ' ');
}

function scoreMatch(query, entry){
  const q = normalize(query);
  let best = 0;
  for(const name of entry.names){
    const n = normalize(name);
    if(q === n) return 100;
    if(containsWholeWords(q, n) || containsWholeWords(n, q)){
      best = Math.max(best, 80);
      continue; // exact phrase containment always wins for this name; skip fuzzy scoring
    }
    // fuzzy overlap: capped well below the substring-match tier (80), and
    // scaled by how much of the *longer* side actually matched, so a few
    // shared words between two long, different dish names can't masquerade
    // as a strong match.
    const qWords = q.split(' ');
    const nWords = n.split(' ');
    const overlap = qWords.filter(w => nWords.includes(w)).length;
    const longerLen = Math.max(qWords.length, nWords.length);
    const coverage = overlap / longerLen;
    if(overlap > 0) best = Math.max(best, Math.round(coverage * 70));
  }
  return best;
}

function findMatches(query){
  if(!query.trim()) return [];
  return DB.map(e => ({entry: e, score: scoreMatch(query, e)}))
    .filter(r => r.score > 30)
    .sort((a,b) => b.score - a.score)
    .slice(0, 5);
}

function escapeHtml(str){
  return str.replace(/[&<>"']/g, c => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
}

const PORTION_MULTIPLIERS = { small: 0.6, normal: 1.0, large: 1.4, xl: 1.8 };
const PORTION_LABELS = { small: "Small", normal: "Normal", large: "Large", xl: "Extra Large" };

let pendingEntry = null;

function renderSuggestions(){
  const query = document.getElementById('food-input').value;
  const box = document.getElementById('suggestions');
  const note = document.getElementById('match-note');
  box.innerHTML = '';
  pendingEntry = null;
  if(!query.trim()){ note.textContent = ''; return; }
  const matches = findMatches(query);
  if(matches.length === 0){
    note.textContent = 'No close match found in the database yet — try a simpler term, e.g. "mee goreng".';
    return;
  }
  note.textContent = matches[0].score >= 80 ? 'Pick a portion size to log the top match.' : 'Closest matches:';
  matches.forEach(m => {
    const chip = document.createElement('button');
    chip.className = 'chip';
    chip.textContent = m.entry.names[0] + ' · ' + m.entry.kcal + ' kcal';
    chip.onclick = () => showPortionPicker(m.entry);
    box.appendChild(chip);
  });
}

function showPortionPicker(entry){
  pendingEntry = entry;
  const box = document.getElementById('suggestions');
  const note = document.getElementById('match-note');
  box.innerHTML = '';
  note.textContent = 'How much ' + entry.names[0] + ' did you have?';
  Object.keys(PORTION_MULTIPLIERS).forEach(key => {
    const mult = PORTION_MULTIPLIERS[key];
    const adjKcal = Math.round(entry.kcal * mult);
    const chip = document.createElement('button');
    chip.className = 'chip';
    chip.textContent = PORTION_LABELS[key] + ' · ' + adjKcal + ' kcal';
    if(key === 'normal') chip.style.borderColor = 'var(--accent)';
    chip.onclick = () => addEntry(entry, key);
    box.appendChild(chip);
  });
  const cancelChip = document.createElement('button');
  cancelChip.className = 'chip';
  cancelChip.textContent = '✕ Cancel';
  cancelChip.onclick = () => { renderSuggestions(); };
  box.appendChild(cancelChip);
}

function addEntry(entry, portionKey){
  portionKey = portionKey || 'normal';
  const mult = PORTION_MULTIPLIERS[portionKey];
  log.push({
    ...entry,
    kcal: Math.round(entry.kcal * mult),
    p: Math.round(entry.p * mult),
    portion: portionKey,
    id: Date.now() + Math.random()
  });
  document.getElementById('food-input').value = '';
  pendingEntry = null;
  renderSuggestions();
  renderLog();
  document.getElementById('food-input').focus();
}

function removeEntry(id){
  log = log.filter(e => e.id !== id);
  renderLog();
}

function renderLog(){
  const list = document.getElementById('log-list');
  const empty = document.getElementById('empty-state');
  list.innerHTML = '';
  empty.style.display = log.length === 0 ? 'block' : 'none';

  log.forEach(item => {
    const row = document.createElement('div');
    row.className = 'log-item';
    const portionTag = item.portion && item.portion !== 'normal' ? ' · ' + PORTION_LABELS[item.portion] : '';
    const left = document.createElement('div');
    left.innerHTML = '<p class="name">' + escapeHtml(item.names[0]) + portionTag + '</p>' +
      '<p class="note">' + escapeHtml(item.note) + '</p>';
    const right = document.createElement('div');
    right.className = 'right';
    right.innerHTML = '<span class="kcal">' + item.kcal + ' kcal</span>';
    const delBtn = document.createElement('button');
    delBtn.className = 'del-btn';
    delBtn.setAttribute('aria-label', 'Remove ' + item.names[0]);
    delBtn.textContent = '✕';
    delBtn.onclick = () => removeEntry(item.id);
    right.appendChild(delBtn);
    row.appendChild(left);
    row.appendChild(right);
    list.appendChild(row);
  });

  const totals = log.reduce((acc, e) => ({
    kcal: acc.kcal + e.kcal, p: acc.p + e.p
  }), {kcal:0, p:0});

  document.getElementById('total-kcal').textContent = Math.round(totals.kcal);
  document.getElementById('total-protein').textContent = Math.round(totals.p) + 'g';

  updateNetSummary();
  saveTodayToStorage();
}

document.getElementById('food-input').addEventListener('input', renderSuggestions);
document.getElementById('food-input').addEventListener('keydown', (e) => {
  if(e.key === 'Enter'){
    e.preventDefault();
    if(pendingEntry){
      addEntry(pendingEntry, 'normal');
      return;
    }
    const matches = findMatches(document.getElementById('food-input').value);
    if(matches.length > 0) showPortionPicker(matches[0].entry);
  }
});
document.getElementById('add-btn').addEventListener('click', () => {
  if(pendingEntry){
    addEntry(pendingEntry, 'normal');
    return;
  }
  const matches = findMatches(document.getElementById('food-input').value);
  if(matches.length > 0) showPortionPicker(matches[0].entry);
});
document.getElementById('clear-btn').addEventListener('click', () => {
  log = [];
  renderLog();
});

/* =========================================================
   SETUP SCREEN
   ========================================================= */
let profile = {
  gender: null, height: null, weight: null, age: null,
  activity: null, goal: null, trainLocation: null,
  homeEquipment: null, gymEquipment: []
};

function setupPillGroup(containerId, key){
  const container = document.getElementById(containerId);
  container.querySelectorAll('.pill-option').forEach(el => {
    el.addEventListener('click', () => {
      container.querySelectorAll('.pill-option').forEach(o => o.classList.remove('selected'));
      el.classList.add('selected');
      profile[key] = el.getAttribute('data-value');
    });
  });
}

function setupMultiSelectGroup(containerId, key){
  const container = document.getElementById(containerId);
  container.querySelectorAll('.pill-option').forEach(el => {
    el.addEventListener('click', () => {
      const val = el.getAttribute('data-value');
      const idx = profile[key].indexOf(val);
      if(idx === -1){
        profile[key].push(val);
        el.classList.add('selected');
      } else {
        profile[key].splice(idx, 1);
        el.classList.remove('selected');
      }
    });
  });
}

setupPillGroup('gender-options', 'gender');
setupPillGroup('activity-options', 'activity');
setupPillGroup('location-options', 'trainLocation');
setupPillGroup('home-equipment-options', 'homeEquipment');
setupMultiSelectGroup('gym-equipment-options', 'gymEquipment');

document.getElementById('location-options').querySelectorAll('.pill-option').forEach(el => {
  el.addEventListener('click', () => {
    const val = el.getAttribute('data-value');
    document.getElementById('home-equipment-group').style.display = (val === 'home') ? 'block' : 'none';
    document.getElementById('gym-equipment-group').style.display = (val === 'gym') ? 'block' : 'none';
  });
});

document.getElementById('goal-options').querySelectorAll('.goal-card').forEach(el => {
  el.addEventListener('click', () => {
    document.querySelectorAll('.goal-card').forEach(o => o.classList.remove('selected'));
    el.classList.add('selected');
    profile.goal = el.getAttribute('data-value');
  });
});

const ACTIVITY_MULTIPLIER = { deskbound: 1.2, some: 1.375, active: 1.55 };
const ACTIVITY_LABEL = { deskbound: "Desk-bound", some: "Some movement", active: "Active job" };
const GOAL_LABEL = { lose: "Lose weight", recomp: "Lean recomposition", muscle: "Build muscle", maintain: "Maintain weight" };
const HOME_EQUIPMENT_LABEL = { none: "Bodyweight only", pullup: "Pull-up bar", dumbbell: "Dumbbells", both: "Pull-up bar + dumbbells" };
const GYM_EQUIPMENT_LABEL = { barbell: "Barbell", dumbbell: "Dumbbells", machines: "Machines", cables: "Cables", pullup: "Pull-up bar", cardio: "Cardio machines" };

function calcBMR(weight, height, age, gender){
  const base = 10*weight + 6.25*height - 5*age;
  return gender === 'male' ? base + 5 : base - 161;
}

function calcGoalAdjustment(goal){
  // returns kcal/day adjustment relative to TDEE
  switch(goal){
    case 'lose': return -450;
    case 'recomp': return -250;
    case 'muscle': return 250;
    case 'maintain': return 0;
    default: return 0;
  }
}

document.getElementById('start-btn').addEventListener('click', () => {
  const height = parseFloat(document.getElementById('input-height').value);
  const weight = parseFloat(document.getElementById('input-weight').value);
  const age = parseFloat(document.getElementById('input-age').value);
  profile.height = height;
  profile.weight = weight;
  profile.age = age;

  const errorEl = document.getElementById('setup-error');
  const locationOk = profile.trainLocation === 'home' ? !!profile.homeEquipment
    : profile.trainLocation === 'gym' ? profile.gymEquipment.length > 0
    : false;
  if(!profile.gender || !height || !weight || !age || !profile.activity || !profile.goal || !locationOk){
    errorEl.style.display = 'block';
    return;
  }
  errorEl.style.display = 'none';

  document.getElementById('setup-screen').style.display = 'none';
  document.getElementById('app-screen').style.display = 'block';
  initApp();
});

document.getElementById('edit-profile-btn').addEventListener('click', () => {
  document.getElementById('app-screen').style.display = 'none';
  document.getElementById('setup-screen').style.display = 'block';
  prefillSetupForm();
});

function selectPill(containerId, value){
  const container = document.getElementById(containerId);
  container.querySelectorAll('.pill-option').forEach(el => {
    el.classList.toggle('selected', el.getAttribute('data-value') === value);
  });
}

function selectMultiPill(containerId, values){
  const container = document.getElementById(containerId);
  container.querySelectorAll('.pill-option').forEach(el => {
    el.classList.toggle('selected', (values || []).includes(el.getAttribute('data-value')));
  });
}

function prefillSetupForm(){
  if(profile.gender) selectPill('gender-options', profile.gender);
  if(profile.activity) selectPill('activity-options', profile.activity);
  if(profile.trainLocation){
    selectPill('location-options', profile.trainLocation);
    document.getElementById('home-equipment-group').style.display = (profile.trainLocation === 'home') ? 'block' : 'none';
    document.getElementById('gym-equipment-group').style.display = (profile.trainLocation === 'gym') ? 'block' : 'none';
  }
  if(profile.homeEquipment) selectPill('home-equipment-options', profile.homeEquipment);
  if(profile.gymEquipment) selectMultiPill('gym-equipment-options', profile.gymEquipment);
  if(profile.goal){
    document.querySelectorAll('.goal-card').forEach(el => {
      el.classList.toggle('selected', el.getAttribute('data-value') === profile.goal);
    });
  }
  if(profile.height) document.getElementById('input-height').value = profile.height;
  if(profile.weight) document.getElementById('input-weight').value = profile.weight;
  if(profile.age) document.getElementById('input-age').value = profile.age;
}

function initApp(){
  const bmr = calcBMR(profile.weight, profile.height, profile.age, profile.gender);
  const tdee = bmr * ACTIVITY_MULTIPLIER[profile.activity];
  const adjustment = calcGoalAdjustment(profile.goal);
  const target = tdee + adjustment;

  document.getElementById('profile-summary').textContent =
    (profile.gender === 'male' ? 'Male' : 'Female') + ' · ' + profile.height + 'cm · ' + profile.weight + 'kg · ' + profile.age + 'y · ' +
    ACTIVITY_LABEL[profile.activity] + ' · ' + GOAL_LABEL[profile.goal];
  document.getElementById('current-date-label').textContent = currentDateLabel;

  let targetHtml = '<strong>Estimated BMR:</strong> ' + Math.round(bmr) + ' kcal &nbsp;·&nbsp; <strong>Maintenance (TDEE):</strong> ~' + Math.round(tdee) + ' kcal/day. ';
  if(profile.goal === 'lose'){
    targetHtml += 'For your goal (lose weight), aim for roughly <strong>' + Math.round(target) + ' kcal/day</strong>, a deficit of about 450 kcal. Expect ~0.4-0.5kg/week loss.';
  } else if(profile.goal === 'recomp'){
    targetHtml += 'For lean recomposition, aim for roughly <strong>' + Math.round(target) + ' kcal/day</strong>, a mild deficit. Pair this with resistance training and higher protein (~' + Math.round(profile.weight * 1.8) + 'g/day) to preserve and build muscle while leaning out.';
  } else if(profile.goal === 'muscle'){
    targetHtml += 'For building muscle, aim for roughly <strong>' + Math.round(target) + ' kcal/day</strong>, a mild surplus. Prioritize protein (~' + Math.round(profile.weight * 1.8) + 'g/day) and progressive resistance training.';
  } else {
    targetHtml += 'To maintain your current weight, aim for roughly <strong>' + Math.round(target) + ' kcal/day</strong>.';
  }
  targetHtml += ' This is a planning estimate (Mifflin-St Jeor formula, ~10% margin of error), not a lab measurement.';
  document.getElementById('targets-box').innerHTML = targetHtml;

  let exGoalHtml = '<strong>Your numbers:</strong> ' + profile.height + 'cm, ' + profile.weight + 'kg, ' + profile.age + ', ' + (profile.gender === 'male' ? 'male' : 'female') + '. ';
  if(profile.goal === 'muscle'){
    exGoalHtml += 'Since the goal is building muscle, this circuit emphasizes resistance moves — focus on slow, controlled reps rather than rushing through.';
  } else if(profile.goal === 'recomp'){
    exGoalHtml += 'For lean recomposition, diet does most of the work. This circuit is for muscle stimulus, not a big calorie burn — that is normal and expected.';
  } else if(profile.goal === 'lose'){
    exGoalHtml += 'This circuit adds a bit of extra burn and keeps muscle active while you are in a deficit — the bigger lever is still your food intake.';
  } else {
    exGoalHtml += 'This circuit helps maintain strength and mobility day to day.';
  }
  document.getElementById('exercise-goal-box').innerHTML = exGoalHtml;

  buildDailyPlan();

  // restore today's in-progress log if one was saved (e.g. page was reopened)
  try{
    const savedToday = localStorage.getItem(STORAGE_KEY_TODAY);
    if(savedToday){
      const parsed = JSON.parse(savedToday);
      log = parsed.log || [];
      exerciseLog = (parsed.exerciseLog || []).filter(e => e.source !== 'plan');
      planDone = parsed.planDone || {};
      currentDateLabel = parsed.dateLabel || currentDateLabel;
      document.getElementById('current-date-label').textContent = currentDateLabel;
    }
  } catch(e){ console.warn('Could not restore today\'s log:', e); }

  renderPlanChecklist();
  renderExerciseLog();
  renderLog();
  saveProfileToStorage();
}

/* =========================================================
   EXERCISE — location & equipment aware circuit
   ========================================================= */
function kcalForMinutes(met, minutes){
  return Math.round(met * profile.weight * (minutes/60));
}

// HOME move pool — bodyweight, optionally pull-up bar / dumbbells
const HOME_MOVE_POOL = {
  warmup: {name:"Marching in place", desc:"60 sec warm-up", met:3.0, minutes:1, equip:"none"},
  squats: {name:"Bodyweight squats", desc:"3 sets of 15-20", met:5.0, minutes:2, equip:"none"},
  gobletSquats: {name:"Dumbbell goblet squats", desc:"3 sets of 12-15", met:5.5, minutes:2, equip:"dumbbell"},
  pushups: {name:"Push-ups", desc:"3 sets of 12-15", met:7.0, minutes:1.5, equip:"none"},
  dbPress: {name:"Dumbbell floor press", desc:"3 sets of 10-12", met:5.0, minutes:1.5, equip:"dumbbell"},
  pullups: {name:"Pull-ups (or negatives)", desc:"3 sets of 5-8", met:6.5, minutes:1.5, equip:"pullup"},
  invertedRow: {name:"Inverted rows (low bar)", desc:"3 sets of 8-10", met:6.0, minutes:1.5, equip:"pullup"},
  dbRow: {name:"Dumbbell bent-over rows", desc:"3 sets of 12", met:5.0, minutes:1.5, equip:"dumbbell"},
  supermanRow: {name:"Superman holds", desc:"3 sets of 20-30 sec", met:3.5, minutes:1.5, equip:"none"},
  plank: {name:"Plank hold", desc:"2 rounds of 30-40 sec", met:3.5, minutes:1, equip:"none"},
  lunges: {name:"Alternating lunges", desc:"2 sets of 10 per leg", met:5.5, minutes:1.3, equip:"none"},
  dbLunges: {name:"Dumbbell lunges", desc:"2 sets of 10 per leg", met:6.0, minutes:1.3, equip:"dumbbell"},
  jacks: {name:"Jumping jacks (finisher)", desc:"2 rounds of 45 sec", met:7.0, minutes:1.5, equip:"none"},
};

// GYM move pool — picks best available equipment per functional slot
const GYM_MOVE_POOL = {
  warmup: {name:"Treadmill or bike warm-up", desc:"3-5 min easy pace", met:4.5, minutes:4, equip:"cardio"},
  warmupBodyweight: {name:"Bodyweight warm-up (jog + dynamic stretch)", desc:"3-5 min", met:4.0, minutes:4, equip:"none"},
  squatBarbell: {name:"Barbell back squat", desc:"3 sets of 8-10", met:6.0, minutes:5, equip:"barbell"},
  legPressMachine: {name:"Leg press machine", desc:"3 sets of 10-12", met:5.0, minutes:5, equip:"machines"},
  gobletSquatGym: {name:"Dumbbell goblet squat", desc:"3 sets of 12-15", met:5.5, minutes:4, equip:"dumbbell"},
  benchPress: {name:"Barbell bench press", desc:"3 sets of 8-10", met:5.5, minutes:5, equip:"barbell"},
  chestPressMachine: {name:"Chest press machine", desc:"3 sets of 10-12", met:5.0, minutes:5, equip:"machines"},
  dbBenchPress: {name:"Dumbbell bench press", desc:"3 sets of 10-12", met:5.5, minutes:5, equip:"dumbbell"},
  latPulldown: {name:"Lat pulldown (cable)", desc:"3 sets of 10-12", met:5.0, minutes:4, equip:"cables"},
  pullupsGym: {name:"Pull-ups / assisted pull-up machine", desc:"3 sets of 6-10", met:6.5, minutes:4, equip:"pullup"},
  seatedRowCable: {name:"Seated cable row", desc:"3 sets of 10-12", met:5.0, minutes:4, equip:"cables"},
  dbRowGym: {name:"Dumbbell bent-over row", desc:"3 sets of 10-12", met:5.0, minutes:4, equip:"dumbbell"},
  legCurlMachine: {name:"Leg curl machine", desc:"3 sets of 12", met:4.5, minutes:4, equip:"machines"},
  romanianDeadlift: {name:"Barbell Romanian deadlift", desc:"3 sets of 8-10", met:6.0, minutes:5, equip:"barbell"},
  dbLungesGym: {name:"Dumbbell walking lunges", desc:"2 sets of 10 per leg", met:6.0, minutes:3, equip:"dumbbell"},
  cableCoreRotation: {name:"Cable core rotation / woodchopper", desc:"2 sets of 12 per side", met:4.5, minutes:3, equip:"cables"},
  plankGym: {name:"Plank hold", desc:"2 rounds of 30-40 sec", met:3.5, minutes:1.5, equip:"none"},
  cardioFinisher: {name:"Cardio finisher (bike/rower, moderate)", desc:"5 min steady pace", met:7.0, minutes:5, equip:"cardio"},
  bodyweightFinisher: {name:"Bodyweight finisher (jumping jacks)", desc:"2 rounds of 45 sec", met:7.0, minutes:1.5, equip:"none"},
};

function hasHomeEquip(required){
  if(required === 'none') return true;
  if(profile.homeEquipment === 'both') return true;
  return profile.homeEquipment === required;
}

function hasGymEquip(required){
  if(required === 'none') return true;
  return profile.gymEquipment.includes(required);
}

let DAILY_PLAN = [];

function buildHomePlan(intensityScale){
  const lowerBodyMove = (profile.homeEquipment === 'dumbbell' || profile.homeEquipment === 'both') ? HOME_MOVE_POOL.gobletSquats : HOME_MOVE_POOL.squats;
  const pushMove = (profile.homeEquipment === 'dumbbell') ? HOME_MOVE_POOL.dbPress : HOME_MOVE_POOL.pushups;
  const pullMove = hasHomeEquip('pullup') ? HOME_MOVE_POOL.pullups
    : (profile.homeEquipment === 'dumbbell' ? HOME_MOVE_POOL.dbRow : HOME_MOVE_POOL.supermanRow);
  const secondPullMove = hasHomeEquip('pullup') ? HOME_MOVE_POOL.invertedRow : null;
  const lungeMove = (profile.homeEquipment === 'dumbbell' || profile.homeEquipment === 'both') ? HOME_MOVE_POOL.dbLunges : HOME_MOVE_POOL.lunges;

  const plan = [
    {...HOME_MOVE_POOL.warmup, id:'warmup'},
    {...lowerBodyMove, id:'lowerbody'},
    {...pushMove, id:'push'},
    {...pullMove, id:'pull'},
  ];
  if(secondPullMove) plan.push({...secondPullMove, id:'pull2'});
  plan.push({...HOME_MOVE_POOL.plank, id:'core'});
  plan.push({...lungeMove, id:'lunge'});
  plan.push({...HOME_MOVE_POOL.jacks, id:'finisher'});

  return plan.map(p => ({...p, minutes: Math.round(p.minutes * intensityScale * 10) / 10}));
}

function buildGymPlan(intensityScale){
  // pick the best available equipment for each functional slot, preferring
  // barbell > machines > dumbbell > cables > bodyweight where multiple fit
  const warmupMove = hasGymEquip('cardio') ? GYM_MOVE_POOL.warmup : GYM_MOVE_POOL.warmupBodyweight;
  const squatMove = hasGymEquip('barbell') ? GYM_MOVE_POOL.squatBarbell
    : hasGymEquip('machines') ? GYM_MOVE_POOL.legPressMachine
    : hasGymEquip('dumbbell') ? GYM_MOVE_POOL.gobletSquatGym
    : HOME_MOVE_POOL.squats;
  const pressMove = hasGymEquip('barbell') ? GYM_MOVE_POOL.benchPress
    : hasGymEquip('machines') ? GYM_MOVE_POOL.chestPressMachine
    : hasGymEquip('dumbbell') ? GYM_MOVE_POOL.dbBenchPress
    : HOME_MOVE_POOL.pushups;
  const pullMove = hasGymEquip('pullup') ? GYM_MOVE_POOL.pullupsGym
    : hasGymEquip('cables') ? GYM_MOVE_POOL.latPulldown
    : hasGymEquip('dumbbell') ? GYM_MOVE_POOL.dbRowGym
    : HOME_MOVE_POOL.supermanRow;
  const secondPullMove = hasGymEquip('cables') ? GYM_MOVE_POOL.seatedRowCable
    : (hasGymEquip('pullup') && hasGymEquip('dumbbell')) ? GYM_MOVE_POOL.dbRowGym
    : null;
  const posteriorMove = hasGymEquip('barbell') ? GYM_MOVE_POOL.romanianDeadlift
    : hasGymEquip('machines') ? GYM_MOVE_POOL.legCurlMachine
    : null;
  const lungeMove = hasGymEquip('dumbbell') ? GYM_MOVE_POOL.dbLungesGym : null;
  const coreMove = hasGymEquip('cables') ? GYM_MOVE_POOL.cableCoreRotation : GYM_MOVE_POOL.plankGym;
  const finisherMove = hasGymEquip('cardio') ? GYM_MOVE_POOL.cardioFinisher : GYM_MOVE_POOL.bodyweightFinisher;

  const plan = [
    {...warmupMove, id:'warmup'},
    {...squatMove, id:'lowerbody'},
    {...pressMove, id:'push'},
    {...pullMove, id:'pull'},
  ];
  if(secondPullMove) plan.push({...secondPullMove, id:'pull2'});
  if(posteriorMove) plan.push({...posteriorMove, id:'posterior'});
  if(lungeMove) plan.push({...lungeMove, id:'lunge'});
  plan.push({...coreMove, id:'core'});
  plan.push({...finisherMove, id:'finisher'});

  return plan.map(p => ({...p, minutes: Math.round(p.minutes * intensityScale * 10) / 10}));
}

function buildDailyPlan(){
  const intensityScale = profile.activity === 'active' ? 1.15 : (profile.activity === 'deskbound' ? 0.9 : 1.0);

  DAILY_PLAN = (profile.trainLocation === 'gym') ? buildGymPlan(intensityScale) : buildHomePlan(intensityScale);

  const circuitMinutes = DAILY_PLAN.reduce((s,p) => s + p.minutes, 0);
  const equipDesc = profile.trainLocation === 'gym'
    ? profile.gymEquipment.map(e => GYM_EQUIPMENT_LABEL[e]).join(', ')
    : HOME_EQUIPMENT_LABEL[profile.homeEquipment];
  document.getElementById('circuit-sub').textContent =
    'Same plan every day, about ' + Math.round(circuitMinutes) + ' minutes. Built for: ' + equipDesc + '.';
}

const ONEOFF_MET = { gym: 6.0, run: 9.8, swim: 7.0 };
const ONEOFF_LABEL = { gym: "Gym session", run: "Running", swim: "Swimming" };

let planDone = {};

function renderPlanChecklist(){
  const preserved = planDone || {};
  planDone = {};
  DAILY_PLAN.forEach(p => planDone[p.id] = preserved[p.id] || false);

  const container = document.getElementById('plan-checklist');
  container.innerHTML = '';
  DAILY_PLAN.forEach(p => {
    const kcal = kcalForMinutes(p.met, p.minutes);
    const item = document.createElement('div');
    item.className = 'plan-item' + (planDone[p.id] ? ' done' : '');
    item.innerHTML =
      '<div class="plan-checkbox">' + (planDone[p.id] ? '✓' : '') + '</div>' +
      '<div class="plan-left">' +
        '<p class="plan-name">' + escapeHtml(p.name) + '</p>' +
        '<p class="plan-desc">' + escapeHtml(p.desc) + '</p>' +
      '</div>' +
      '<span class="plan-kcal">~' + kcal + ' kcal</span>';
    item.onclick = () => togglePlanItem(p.id, item);
    container.appendChild(item);
  });
  updatePlanProgress();
}

function togglePlanItem(id, el){
  planDone[id] = !planDone[id];
  el.classList.toggle('done');
  const checkbox = el.querySelector('.plan-checkbox');
  checkbox.textContent = planDone[id] ? '✓' : '';
  updatePlanProgress();
}

function updatePlanProgress(){
  const doneCount = DAILY_PLAN.filter(p => planDone[p.id]).length;
  const totalCount = DAILY_PLAN.length;
  const burnedSoFar = DAILY_PLAN.filter(p => planDone[p.id])
    .reduce((sum, p) => sum + kcalForMinutes(p.met, p.minutes), 0);
  const pct = totalCount > 0 ? Math.round((doneCount/totalCount) * 100) : 0;
  document.getElementById('plan-progress-fill').style.width = pct + '%';
  document.getElementById('plan-progress-text').textContent =
    doneCount + ' of ' + totalCount + ' done · ' + Math.round(burnedSoFar) + ' kcal so far';
  syncPlanToExerciseLog();
}

function syncPlanToExerciseLog(){
  exerciseLog = exerciseLog.filter(e => e.source !== 'plan');
  DAILY_PLAN.forEach(p => {
    if(planDone[p.id]){
      exerciseLog.push({
        name: p.name, kcal: kcalForMinutes(p.met, p.minutes), desc: "daily circuit",
        id: "plan-" + p.id, source: 'plan'
      });
    }
  });
  renderExerciseLog();
}

document.getElementById('reset-plan-btn').addEventListener('click', () => {
  renderPlanChecklist();
});

document.querySelectorAll('.oneoff-log-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    const activity = btn.getAttribute('data-activity');
    const minutesInput = document.getElementById(activity + '-minutes');
    const minutes = parseFloat(minutesInput.value) || 0;
    if(minutes <= 0) return;
    const kcal = kcalForMinutes(ONEOFF_MET[activity], minutes);
    exerciseLog.push({
      name: ONEOFF_LABEL[activity], kcal: kcal, desc: minutes + " min session",
      id: Date.now() + Math.random(), source: 'oneoff'
    });
    renderExerciseLog();
  });
});

let exerciseLog = [];

function removeExerciseEntry(id){
  const entry = exerciseLog.find(e => e.id === id);
  if(entry && entry.source === 'plan'){
    const planId = entry.id.replace('plan-', '');
    planDone[planId] = false;
    const items = document.querySelectorAll('#plan-checklist .plan-item');
    DAILY_PLAN.forEach((p, idx) => {
      if(p.id === planId){
        items[idx].classList.remove('done');
        items[idx].querySelector('.plan-checkbox').textContent = '';
      }
    });
    updatePlanProgress();
    return;
  }
  exerciseLog = exerciseLog.filter(e => e.id !== id);
  renderExerciseLog();
}

function renderExerciseLog(){
  const list = document.getElementById('exercise-log-list');
  const empty = document.getElementById('exercise-empty-state');
  list.innerHTML = '';
  empty.style.display = exerciseLog.length === 0 ? 'block' : 'none';

  exerciseLog.forEach(item => {
    const row = document.createElement('div');
    row.className = 'log-item exercise';
    const left = document.createElement('div');
    left.innerHTML = '<p class="name">' + escapeHtml(item.name) + '</p>' +
      '<p class="note">' + escapeHtml(item.desc) + '</p>';
    const right = document.createElement('div');
    right.className = 'right';
    right.innerHTML = '<span class="kcal" style="color:var(--green);">-' + item.kcal + ' kcal</span>';
    const delBtn = document.createElement('button');
    delBtn.className = 'del-btn';
    delBtn.setAttribute('aria-label', 'Remove ' + item.name);
    delBtn.textContent = '✕';
    delBtn.onclick = () => removeExerciseEntry(item.id);
    right.appendChild(delBtn);
    row.appendChild(left);
    row.appendChild(right);
    list.appendChild(row);
  });

  updateNetSummary();
  saveTodayToStorage();
}

document.getElementById('clear-exercise-btn').addEventListener('click', () => {
  exerciseLog = [];
  renderPlanChecklist();
});

function updateNetSummary(){
  const eaten = log.reduce((sum, e) => sum + e.kcal, 0);
  const burned = exerciseLog.reduce((sum, e) => sum + e.kcal, 0);
  document.getElementById('net-eaten').textContent = Math.round(eaten);
  document.getElementById('net-burned').textContent = Math.round(burned);
  document.getElementById('net-total').textContent = Math.round(eaten - burned);
}

/* ---------- Tabs ---------- */
document.getElementById('tab-food').addEventListener('click', () => switchTab('food'));
document.getElementById('tab-exercise').addEventListener('click', () => switchTab('exercise'));
document.getElementById('tab-history').addEventListener('click', () => { switchTab('history'); renderHistory(); });
function switchTab(name){
  document.getElementById('tab-food').classList.toggle('active', name === 'food');
  document.getElementById('tab-exercise').classList.toggle('active', name === 'exercise');
  document.getElementById('tab-history').classList.toggle('active', name === 'history');
  document.getElementById('panel-food').classList.toggle('active', name === 'food');
  document.getElementById('panel-exercise').classList.toggle('active', name === 'exercise');
  document.getElementById('panel-history').classList.toggle('active', name === 'history');
}

/* =========================================================
   PERSISTENCE — localStorage, survives closing the page
   ========================================================= */
const STORAGE_KEY_PROFILE = 'calorieTracker_profile';
const STORAGE_KEY_TODAY = 'calorieTracker_today';
const STORAGE_KEY_HISTORY = 'calorieTracker_history';

function saveTodayToStorage(){
  try{
    localStorage.setItem(STORAGE_KEY_TODAY, JSON.stringify({
      log: log, exerciseLog: exerciseLog, planDone: planDone,
      dateLabel: currentDateLabel
    }));
  } catch(e){ console.warn('Could not save today\'s log:', e); }
}

function saveProfileToStorage(){
  try{ localStorage.setItem(STORAGE_KEY_PROFILE, JSON.stringify(profile)); }
  catch(e){ console.warn('Could not save profile:', e); }
}

function loadHistoryFromStorage(){
  try{
    const raw = localStorage.getItem(STORAGE_KEY_HISTORY);
    return raw ? JSON.parse(raw) : [];
  } catch(e){ console.warn('Could not load history:', e); return []; }
}

function saveHistoryToStorage(historyArr){
  try{ localStorage.setItem(STORAGE_KEY_HISTORY, JSON.stringify(historyArr)); }
  catch(e){ console.warn('Could not save history:', e); }
}

let currentDateLabel = formatDateLabel(new Date());

function formatDateLabel(d){
  return d.toLocaleDateString(undefined, { weekday:'short', day:'numeric', month:'short' });
}

document.getElementById('new-day-btn').addEventListener('click', () => {
  const hasAnything = log.length > 0 || exerciseLog.length > 0;
  if(!hasAnything){
    alert('Nothing logged yet today — log some food or exercise before starting a new day.');
    return;
  }
  const eatenTotal = log.reduce((s,e) => s + e.kcal, 0);
  const burnedTotal = exerciseLog.reduce((s,e) => s + e.kcal, 0);
  const proteinTotal = log.reduce((s,e) => s + e.p, 0);

  const history = loadHistoryFromStorage();
  history.unshift({
    id: Date.now() + Math.random(),
    dateLabel: currentDateLabel,
    savedAt: new Date().toISOString(),
    foodLog: log,
    exerciseLog: exerciseLog,
    totalEaten: eatenTotal,
    totalBurned: burnedTotal,
    totalProtein: proteinTotal
  });
  saveHistoryToStorage(history);

  // reset today
  log = [];
  exerciseLog = [];
  currentDateLabel = formatDateLabel(new Date());
  document.getElementById('current-date-label').textContent = currentDateLabel;
  renderPlanChecklist();
  renderExerciseLog();
  renderLog();
  saveTodayToStorage();
  renderHistory();
});

function renderHistory(){
  const history = loadHistoryFromStorage();
  const list = document.getElementById('history-list');
  const empty = document.getElementById('history-empty-state');
  list.innerHTML = '';
  empty.style.display = history.length === 0 ? 'block' : 'none';

  history.forEach(day => {
    const card = document.createElement('div');
    card.className = 'history-card';

    const header = document.createElement('div');
    header.className = 'history-card-header';
    header.innerHTML =
      '<div>' +
        '<p class="history-date">' + escapeHtml(day.dateLabel) + '</p>' +
        '<p class="history-summary">' + day.foodLog.length + ' food item(s) · ' + day.exerciseLog.length + ' exercise item(s)</p>' +
      '</div>' +
      '<div class="history-totals">' +
        '<div class="h-stat"><p class="h-val">' + Math.round(day.totalEaten) + '</p><p class="h-lbl">Eaten</p></div>' +
        '<div class="h-stat"><p class="h-val">' + Math.round(day.totalBurned) + '</p><p class="h-lbl">Burned</p></div>' +
        '<div class="h-stat"><p class="h-val">' + Math.round(day.totalEaten - day.totalBurned) + '</p><p class="h-lbl">Net</p></div>' +
        '<span class="history-chevron">▶</span>' +
      '</div>';
    header.onclick = () => card.classList.toggle('expanded');

    const detail = document.createElement('div');
    detail.className = 'history-detail';
    let detailHtml = '';
    if(day.foodLog.length > 0){
      detailHtml += '<h4>Food</h4>';
      day.foodLog.forEach(item => {
        detailHtml += '<div class="history-item-row"><span>' + escapeHtml(item.names[0]) + '</span><span>' + item.kcal + ' kcal</span></div>';
      });
    }
    if(day.exerciseLog.length > 0){
      detailHtml += '<h4>Exercise</h4>';
      day.exerciseLog.forEach(item => {
        detailHtml += '<div class="history-item-row"><span>' + escapeHtml(item.name) + '</span><span>-' + item.kcal + ' kcal</span></div>';
      });
    }
    detail.innerHTML = detailHtml;

    const deleteBtn = document.createElement('button');
    deleteBtn.className = 'history-delete-btn';
    deleteBtn.textContent = 'Delete this day';
    deleteBtn.onclick = (e) => {
      e.stopPropagation();
      const updated = loadHistoryFromStorage().filter(d => d.id !== day.id);
      saveHistoryToStorage(updated);
      renderHistory();
    };
    detail.appendChild(deleteBtn);

    card.appendChild(header);
    card.appendChild(detail);
    list.appendChild(card);
  });
}

document.getElementById('clear-history-btn').addEventListener('click', () => {
  if(loadHistoryFromStorage().length === 0) return;
  if(confirm('Delete all saved history? This cannot be undone.')){
    saveHistoryToStorage([]);
    renderHistory();
  }
});

/* ---------- Auto-load on page open ---------- */
// If a profile was saved on a previous visit, restore it and skip straight
// to the app screen instead of showing the setup form again.
(function tryAutoLoadProfile(){
  try{
    const savedProfile = localStorage.getItem(STORAGE_KEY_PROFILE);
    if(savedProfile){
      const parsed = JSON.parse(savedProfile);
      Object.assign(profile, parsed);
      document.getElementById('setup-screen').style.display = 'none';
      document.getElementById('app-screen').style.display = 'block';
      initApp();
    }
  } catch(e){ console.warn('Could not auto-load profile:', e); }
})();
</script>
</body>
</html>
