# Momentum-training
My gym workout tracker
<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black">
<meta name="apple-mobile-web-app-title" content="Momentum">
<meta name="theme-color" content="#0d0d0d">
<title>Momentum Training</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@400;600;700&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,400&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0d0d0d;
  --bg2: #171717;
  --bg3: #1f1f1f;
  --bg4: #2a2a2a;
  --text: #f2f2f2;
  --text2: #a0a0a0;
  --text3: #606060;
  --border: rgba(255,255,255,0.08);
  --border2: rgba(255,255,255,0.14);
  --green: #22c55e;
  --green-bg: rgba(34,197,94,0.12);
  --amber: #f59e0b;
  --amber-bg: rgba(245,158,11,0.12);
  --red: #ef4444;
  --red-bg: rgba(239,68,68,0.12);
  --blue: #3b82f6;
  --blue-bg: rgba(59,130,246,0.12);
  --purple: #a855f7;
  --purple-bg: rgba(168,85,247,0.12);
  --teal: #14b8a6;
  --teal-bg: rgba(20,184,166,0.12);
  --accent: #22c55e;
  --radius: 12px;
  --radius-sm: 8px;
  --tab-h: 72px;
  --header-h: 56px;
}
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { font-size: 16px; background: var(--bg); }
body {
  font-family: 'DM Sans', sans-serif;
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  min-height: -webkit-fill-available;
  overscroll-behavior: none;
  -webkit-tap-highlight-color: transparent;
}
input, button, select { font-family: 'DM Sans', sans-serif; }
.condensed { font-family: 'Barlow Condensed', sans-serif; }

/* LAYOUT */
#app {
display: flex;
flex-direction: column;
height: 100vh;
height: -webkit-fill-available;
}
.header {
height: var(–header-h);
padding: 0 18px;
padding-top: env(safe-area-inset-top, 0);
background: var(–bg);
border-bottom: 1px solid var(–border);
display: flex;
align-items: flex-end;
justify-content: space-between;
padding-bottom: 12px;
flex-shrink: 0;
}
.header-title {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 22px;
font-weight: 700;
letter-spacing: 0.08em;
color: var(–text);
}
.readiness-badge {
display: flex;
align-items: center;
gap: 7px;
background: var(–bg3);
border: 1px solid var(–border);
border-radius: 20px;
padding: 5px 10px;
cursor: pointer;
}
.r-dot {
width: 8px; height: 8px;
border-radius: 50%;
background: var(–green);
flex-shrink: 0;
}
.r-dot.amber { background: var(–amber); }
.r-dot.red { background: var(–red); }
.r-dot.grey { background: var(–text3); }
.readiness-badge span {
font-size: 12px;
font-weight: 500;
color: var(–text2);
}

.content {
flex: 1;
overflow-y: auto;
overflow-x: hidden;
-webkit-overflow-scrolling: touch;
}
.view { display: none; padding-bottom: calc(var(–tab-h) + env(safe-area-inset-bottom, 0px) + 16px); }
.view.active { display: block; }

/* TAB BAR */
.tab-bar {
height: var(–tab-h);
padding-bottom: env(safe-area-inset-bottom, 0px);
background: var(–bg);
border-top: 1px solid var(–border);
display: grid;
grid-template-columns: 1fr 1fr 1fr;
flex-shrink: 0;
}
.tab-btn {
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
gap: 4px;
background: none;
border: none;
color: var(–text3);
font-size: 10px;
font-weight: 500;
letter-spacing: 0.04em;
cursor: pointer;
transition: color .15s;
padding: 0;
}
.tab-btn.active { color: var(–accent); }
.tab-icon { width: 22px; height: 22px; }

/* SECTION LABEL */
.section-label {
font-size: 10px;
font-weight: 500;
letter-spacing: 0.08em;
color: var(–text3);
text-transform: uppercase;
padding: 18px 18px 8px;
}

/* CARDS */
.card {
background: var(–bg2);
border: 1px solid var(–border);
border-radius: var(–radius);
margin: 0 14px 10px;
overflow: hidden;
}
.card-header {
padding: 14px 16px;
}
.card-title {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 20px;
font-weight: 700;
letter-spacing: 0.02em;
margin-bottom: 2px;
}
.card-sub {
font-size: 12px;
color: var(–text2);
line-height: 1.4;
}
.card-meta {
display: flex;
gap: 8px;
flex-wrap: wrap;
margin-top: 10px;
}

/* BADGES */
.badge {
display: inline-flex;
align-items: center;
font-size: 10px;
font-weight: 500;
padding: 3px 8px;
border-radius: 20px;
}
.badge-blue { background: var(–blue-bg); color: var(–blue); }
.badge-green { background: var(–green-bg); color: var(–green); }
.badge-amber { background: var(–amber-bg); color: var(–amber); }
.badge-red { background: var(–red-bg); color: var(–red); }
.badge-purple { background: var(–purple-bg); color: var(–purple); }
.badge-teal { background: var(–teal-bg); color: var(–teal); }
.badge-grey { background: var(–bg4); color: var(–text2); }

/* SECTION HEADERS */
.sec-head {
display: flex;
align-items: center;
gap: 8px;
padding: 8px 16px;
background: var(–bg3);
border-top: 1px solid var(–border);
border-bottom: 1px solid var(–border);
}
.sec-head-label {
font-size: 10px;
font-weight: 500;
letter-spacing: 0.06em;
text-transform: uppercase;
color: var(–text3);
}

/* EXERCISE ROWS */
.ex-row {
border-bottom: 1px solid var(–border);
padding: 0;
cursor: pointer;
}
.ex-row:last-child { border-bottom: none; }
.ex-main {
display: flex;
align-items: center;
padding: 11px 16px;
gap: 10px;
}
.ex-done-btn {
width: 22px; height: 22px;
border-radius: 50%;
border: 1.5px solid var(–border2);
background: none;
flex-shrink: 0;
display: flex;
align-items: center;
justify-content: center;
cursor: pointer;
transition: all .15s;
}
.ex-done-btn.done {
background: var(–green);
border-color: var(–green);
}
.ex-done-btn.done svg { display: block; }
.ex-done-btn svg { display: none; }
.ex-info { flex: 1; min-width: 0; }
.ex-name {
font-size: 13px;
font-weight: 500;
color: var(–text);
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
}
.ex-name.done-text { color: var(–text3); text-decoration: line-through; }
.ex-stats {
display: flex;
gap: 6px;
margin-top: 3px;
flex-wrap: wrap;
}
.stat-pill {
font-size: 11px;
color: var(–text2);
background: var(–bg3);
border-radius: 4px;
padding: 1px 6px;
}
.stat-pill.load { color: var(–blue); background: var(–blue-bg); }
.stat-pill.rpe-low { color: var(–green); background: var(–green-bg); }
.stat-pill.rpe-med { color: var(–amber); background: var(–amber-bg); }
.stat-pill.rpe-high { color: var(–red); background: var(–red-bg); }
.stat-pill.reduced { color: var(–amber); background: var(–amber-bg); }

.ex-chevron {
color: var(–text3);
transition: transform .2s;
flex-shrink: 0;
}
.ex-chevron.open { transform: rotate(90deg); }

.ex-note-wrap {
display: none;
padding: 0 16px 12px 48px;
font-size: 12px;
color: var(–text2);
line-height: 1.6;
}
.ex-note-wrap.open { display: block; }
.mo-tags { display: flex; gap: 4px; flex-wrap: wrap; margin-top: 6px; }
.mo-tag {
font-size: 10px;
padding: 1px 6px;
border-radius: 4px;
}
.mo-acc { background: var(–amber-bg); color: var(–amber); }
.mo-dec { background: var(–purple-bg); color: var(–purple); }
.mo-cod { background: var(–teal-bg); color: var(–teal); }
.mo-mass { background: var(–blue-bg); color: var(–blue); }
.mo-power { background: var(–red-bg); color: var(–red); }

/* WARMUP SECTION */
.warmup-wrap {
padding: 12px 16px;
border-top: 1px solid var(–border);
}
.warmup-title {
font-size: 10px;
font-weight: 500;
letter-spacing: 0.06em;
text-transform: uppercase;
color: var(–text3);
margin-bottom: 8px;
}
.warmup-tags { display: flex; flex-wrap: wrap; gap: 5px; }
.warmup-tag {
font-size: 11px;
padding: 3px 9px;
border-radius: 20px;
border: 1px solid var(–border2);
color: var(–text2);
}

/* SLED CARDS */
.sled-grid {
display: grid;
grid-template-columns: 1fr 1fr;
gap: 8px;
padding: 12px 16px;
border-top: 1px solid var(–border);
}
.sled-card {
background: var(–bg3);
border: 1px solid var(–border);
border-radius: var(–radius-sm);
padding: 10px 12px;
}
.sled-type { font-size: 10px; font-weight: 500; color: var(–text3); text-transform: uppercase; letter-spacing: .04em; margin-bottom: 4px; }
.sled-load {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 24px;
font-weight: 700;
color: var(–amber);
margin-bottom: 2px;
}
.sled-desc { font-size: 10px; color: var(–text3); line-height: 1.5; }

/* SESSION NOTE */
.session-note {
padding: 12px 16px;
border-top: 1px solid var(–border);
font-size: 12px;
color: var(–text3);
line-height: 1.6;
font-style: italic;
}

/* PROG NOTE */
.prog-note {
margin: 0 14px 10px;
background: var(–bg3);
border: 1px solid var(–border);
border-radius: var(–radius);
padding: 12px 14px;
font-size: 12px;
color: var(–text2);
line-height: 1.7;
}
.prog-note-label {
font-size: 10px;
font-weight: 500;
letter-spacing: .05em;
text-transform: uppercase;
margin-bottom: 4px;
}

/* DAY STRIP (WEEK VIEW) */
.day-strip {
display: grid;
grid-template-columns: repeat(7, 1fr);
gap: 5px;
padding: 0 14px;
margin-bottom: 14px;
}
.day-chip {
display: flex;
flex-direction: column;
align-items: center;
gap: 2px;
padding: 8px 2px;
border-radius: var(–radius-sm);
border: 1px solid var(–border);
background: var(–bg2);
cursor: pointer;
transition: all .15s;
}
.day-chip:active { transform: scale(.96); }
.day-chip.selected {
background: var(–text);
border-color: var(–text);
}
.day-chip.selected .day-chip-name,
.day-chip.selected .day-chip-type { color: var(–bg); }
.day-chip.is-rest { background: var(–bg3); opacity: .6; cursor: default; }
.day-chip.is-game { background: var(–red-bg); border-color: var(–red); opacity: .85; cursor: default; }
.day-chip.is-prac { background: var(–amber-bg); border-color: var(–amber); opacity: .85; cursor: default; }
.day-chip.is-deload { border-color: var(–green); }
.day-chip-name { font-size: 10px; font-weight: 600; letter-spacing: .04em; color: var(–text2); }
.day-chip-type { font-size: 9px; color: var(–text3); text-align: center; line-height: 1.3; }

/* PHASE PILLS */
.phase-row {
display: flex;
gap: 6px;
padding: 0 14px;
overflow-x: auto;
scrollbar-width: none;
margin-bottom: 12px;
}
.phase-row::-webkit-scrollbar { display: none; }
.phase-pill {
flex-shrink: 0;
padding: 5px 12px;
border-radius: 20px;
border: 1px solid var(–border);
background: var(–bg3);
color: var(–text2);
font-size: 11px;
font-weight: 500;
cursor: pointer;
white-space: nowrap;
transition: all .15s;
}
.phase-pill.active {
background: var(–text);
color: var(–bg);
border-color: var(–text);
}
.phase-pill.deload { border-color: var(–green); color: var(–green); }
.phase-pill.deload.active { background: var(–green); color: var(–bg); }
.phase-pill.test-wk { border-color: var(–amber); color: var(–amber); }
.phase-pill.test-wk.active { background: var(–amber); color: var(–bg); }

/* TOGGLE */
.toggle-row {
display: flex;
gap: 6px;
padding: 0 14px;
margin-bottom: 12px;
}
.toggle-btn {
flex: 1;
padding: 8px;
border-radius: var(–radius-sm);
border: 1px solid var(–border);
background: var(–bg3);
color: var(–text2);
font-size: 12px;
font-weight: 500;
cursor: pointer;
transition: all .15s;
text-align: center;
}
.toggle-btn.active {
background: var(–bg2);
border-color: var(–border2);
color: var(–text);
}

/* SETTINGS */
.settings-block {
margin: 0 14px 14px;
background: var(–bg2);
border: 1px solid var(–border);
border-radius: var(–radius);
padding: 16px;
}
.settings-label {
font-size: 11px;
font-weight: 500;
letter-spacing: .04em;
color: var(–text3);
text-transform: uppercase;
margin-bottom: 10px;
}
.readiness-score-big {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 56px;
font-weight: 700;
line-height: 1;
margin-bottom: 4px;
}
.readiness-status {
font-size: 13px;
font-weight: 500;
margin-bottom: 12px;
}
input[type=range] {
width: 100%;
height: 4px;
appearance: none;
-webkit-appearance: none;
background: var(–bg4);
border-radius: 2px;
outline: none;
cursor: pointer;
margin-bottom: 14px;
}
input[type=range]::-webkit-slider-thumb {
-webkit-appearance: none;
width: 22px; height: 22px;
border-radius: 50%;
background: var(–text);
border: none;
box-shadow: 0 1px 3px rgba(0,0,0,.4);
}
.readiness-mods {
font-size: 12px;
color: var(–text2);
line-height: 1.7;
padding-top: 12px;
border-top: 1px solid var(–border);
}
.pr-grid {
display: grid;
grid-template-columns: 1fr 1fr;
gap: 8px;
}
.pr-cell {
background: var(–bg3);
border-radius: var(–radius-sm);
padding: 10px 12px;
}
.pr-label { font-size: 10px; color: var(–text3); margin-bottom: 3px; }
.pr-val {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 22px;
font-weight: 700;
}
.pr-target { font-size: 10px; color: var(–green); margin-top: 1px; }

/* TODAY SESSION HEADER */
.today-header {
padding: 20px 18px 16px;
}
.today-date {
font-size: 12px;
color: var(–text3);
margin-bottom: 4px;
text-transform: uppercase;
letter-spacing: .04em;
}
.today-session-name {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 36px;
font-weight: 700;
letter-spacing: .02em;
line-height: 1;
margin-bottom: 8px;
}
.today-badges { display: flex; gap: 6px; flex-wrap: wrap; }

/* FATIGUE NOTE */
.mod-alert {
margin: 0 14px 10px;
padding: 10px 14px;
border-radius: var(–radius-sm);
font-size: 12px;
line-height: 1.6;
border: 1px solid;
}
.mod-alert.green { background: var(–green-bg); border-color: var(–green); color: var(–green); }
.mod-alert.amber { background: var(–amber-bg); border-color: var(–amber); color: var(–amber); }
.mod-alert.red { background: var(–red-bg); border-color: var(–red); color: var(–red); }

/* NON-TRAINING */
.non-training {
margin: 0 14px;
background: var(–bg2);
border: 1px solid var(–border);
border-radius: var(–radius);
padding: 28px 20px;
text-align: center;
}
.non-training-title {
font-family: ‘Barlow Condensed’, sans-serif;
font-size: 28px;
font-weight: 700;
margin-bottom: 10px;
}
.non-training-body {
font-size: 13px;
color: var(–text2);
line-height: 1.8;
max-width: 300px;
margin: 0 auto;
}

/* PROGRESS BARS */
.progress-row {
display: flex;
align-items: center;
gap: 10px;
padding: 8px 0;
border-bottom: 1px solid var(–border);
}
.progress-row:last-child { border-bottom: none; }
.progress-label { font-size: 12px; color: var(–text2); width: 80px; flex-shrink: 0; }
.progress-bar-wrap { flex: 1; height: 5px; background: var(–bg4); border-radius: 3px; overflow: hidden; }
.progress-bar { height: 100%; border-radius: 3px; background: var(–accent); }
.progress-pct { font-size: 11px; color: var(–text3); width: 32px; text-align: right; }

/* INLINE ICONS */
svg { display: block; }

/* DELOAD/TEST BANNERS */
.phase-info-banner {
margin: 0 14px 12px;
padding: 12px 14px;
border-radius: var(–radius);
font-size: 12px;
line-height: 1.6;
border: 1px solid;
}
.phase-info-banner.deload { background: var(–green-bg); border-color: var(–green); color: var(–green); }
.phase-info-banner.test { background: var(–amber-bg); border-color: var(–amber); color: var(–amber); }
.phase-info-banner.normal { background: var(–blue-bg); border-color: var(–blue); color: var(–blue); }

/* WEEK COMPLETE BAR */
.week-summary {
margin: 0 14px 14px;
background: var(–bg2);
border: 1px solid var(–border);
border-radius: var(–radius);
padding: 14px 16px;
}
.ws-title { font-size: 11px; font-weight: 500; color: var(–text3); text-transform: uppercase; letter-spacing: .04em; margin-bottom: 10px; }
</style>

</head>
<body>
<div id="app">
  <div class="header">
    <div class="header-title condensed">MOMENTUM</div>
    <div class="readiness-badge" onclick="switchTab('settings')">
      <div class="r-dot" id="r-dot"></div>
      <span id="r-badge-text">78 — Ready</span>
    </div>
  </div>

  <div class="content">

```
<!-- TODAY VIEW -->
<div class="view active" id="view-today">
  <div class="today-header">
    <div class="today-date" id="today-date"></div>
    <div class="today-session-name condensed" id="today-name"></div>
    <div class="today-badges" id="today-badges"></div>
  </div>
  <div id="today-content"></div>
</div>

<!-- WEEK VIEW -->
<div class="view" id="view-week">
  <div class="section-label">Week type</div>
  <div class="toggle-row">
    <button class="toggle-btn active" id="wt-p" onclick="setWT('practice')">Practice week</button>
    <button class="toggle-btn" id="wt-g" onclick="setWT('game')">Game week</button>
  </div>
  <div class="section-label">Phase</div>
  <div class="phase-row" id="phase-row"></div>
  <div class="section-label">Days</div>
  <div class="day-strip" id="day-strip"></div>
  <div id="week-session-content"></div>
</div>

<!-- SETTINGS VIEW -->
<div class="view" id="view-settings">
  <div class="section-label">Fitbit readiness score</div>
  <div class="settings-block">
    <div class="readiness-score-big condensed" id="settings-score">78</div>
    <div class="readiness-status" id="settings-status">High readiness — full session</div>
    <input type="range" min="1" max="100" value="78" id="r-slider" oninput="setReadiness(this.value)">
    <div class="readiness-mods" id="settings-mods">All sets and loads as programmed.</div>
  </div>
  <div class="section-label">Baselines &amp; targets</div>
  <div class="settings-block">
    <div class="pr-grid">
      <div class="pr-cell"><div class="pr-label">40-yard dash</div><div class="pr-val condensed">4.63s</div><div class="pr-target">Target: sub 4.50</div></div>
      <div class="pr-cell"><div class="pr-label">Throw distance</div><div class="pr-val condensed">45 yd</div><div class="pr-target">Target: 52+ yards</div></div>
      <div class="pr-cell"><div class="pr-label">Squat est. 1RM</div><div class="pr-val condensed">152kg</div><div class="pr-target">Start: 110kg</div></div>
      <div class="pr-cell"><div class="pr-label">Bench 1RM</div><div class="pr-val condensed">100kg</div><div class="pr-target">Start: 75kg</div></div>
      <div class="pr-cell"><div class="pr-label">Trap bar 1RM</div><div class="pr-val condensed">188kg</div><div class="pr-target">Start: 152kg</div></div>
      <div class="pr-cell"><div class="pr-label">Bodyweight</div><div class="pr-val condensed">80kg</div><div class="pr-target">17% BF → lean mass</div></div>
    </div>
  </div>
  <div class="section-label">Momentum score pillars</div>
  <div class="settings-block">
    <div class="ws-title">Training targets this programme</div>
    <div class="progress-row"><div class="progress-label">Acceleration</div><div class="progress-bar-wrap"><div class="progress-bar" style="width:90%"></div></div><div class="progress-pct">High</div></div>
    <div class="progress-row"><div class="progress-label">Deceleration</div><div class="progress-bar-wrap"><div class="progress-bar" style="width:80%"></div></div><div class="progress-pct">High</div></div>
    <div class="progress-row"><div class="progress-label">Agility / COD</div><div class="progress-bar-wrap"><div class="progress-bar" style="width:75%"></div></div><div class="progress-pct">High</div></div>
    <div class="progress-row"><div class="progress-label">Lean mass</div><div class="progress-bar-wrap"><div class="progress-bar" style="width:70%"></div></div><div class="progress-pct">Med</div></div>
    <div class="progress-row"><div class="progress-label">Power</div><div class="progress-bar-wrap"><div class="progress-bar" style="width:85%"></div></div><div class="progress-pct">High</div></div>
  </div>
</div>
```

  </div>

  <div class="tab-bar">
    <button class="tab-btn active" id="tab-today" onclick="switchTab('today')">
      <svg class="tab-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>
      Today
    </button>
    <button class="tab-btn" id="tab-week" onclick="switchTab('week')">
      <svg class="tab-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg>
      Programme
    </button>
    <button class="tab-btn" id="tab-settings" onclick="switchTab('settings')">
      <svg class="tab-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg>
      Settings
    </button>
  </div>
</div>

<script>
// ─── STATE ───────────────────────────────────────────────
var state = {
  phase: parseInt(localStorage.getItem('mo_ph')) || 0,
  wt: localStorage.getItem('mo_wt') || 'practice',
  readiness: parseInt(localStorage.getItem('mo_r')) || 78,
  selDay: parseInt(localStorage.getItem('mo_sd')) || 0,
  tab: 'today'
};

function saveState() {
  localStorage.setItem('mo_ph', state.phase);
  localStorage.setItem('mo_wt', state.wt);
  localStorage.setItem('mo_r', state.readiness);
  localStorage.setItem('mo_sd', state.selDay);
}

// ─── PHASES ──────────────────────────────────────────────
var PHASES = [
  {type:'train', label:'Ph 1 · wks 1–3', short:'Phase 1', desc:'Acceleration & mass foundation. Heavy sled. Quality plyos. RPE builds week on week.'},
  {type:'deload', label:'Deload · wk 4', short:'Deload', desc:'60% volume. Maintain load. Supercompensation happens here — do not skip.'},
  {type:'train', label:'Ph 2 · wks 5–7', short:'Phase 2', desc:'COD, deceleration & power. Dual sled model. Sprint volume increases.'},
  {type:'deload', label:'Deload · wk 8', short:'Deload', desc:'60% volume. Maintain intensity. Sleep and nutrition priority.'},
  {type:'train', label:'Ph 3 · wks 9–11', short:'Phase 3', desc:'Momentum expression & peak. Lighter sled for velocity. Intensity peaks.'},
  {type:'test', label:'Test · wk 12', short:'Test Wk', desc:'Retest all baselines: 40-yard, throw, 5-10-5, strength estimates.'}
];

// ─── DAYS ─────────────────────────────────────────────────
var DAYS = {
  practice: [
    {n:'Mon', t:'Full Body', type:'fullbody'},
    {n:'Tue', t:'Sprint + Sled', type:'sprint'},
    {n:'Wed', t:'Rest', type:'rest'},
    {n:'Thu', t:'Lower Power', type:'lower'},
    {n:'Fri', t:'Full Upper', type:'upper'},
    {n:'Sat', t:'Skill + Agility', type:'skill'},
    {n:'Sun', t:'Practice', type:'practice'}
  ],
  game: [
    {n:'Mon', t:'Full Body', type:'fullbody'},
    {n:'Tue', t:'Sprint + Sled', type:'sprint'},
    {n:'Wed', t:'Rest', type:'rest'},
    {n:'Thu', t:'Lower Power', type:'lower'},
    {n:'Fri', t:'Skill Only', type:'skilllite'},
    {n:'Sat', t:'Full Rest', type:'rest'},
    {n:'Sun', t:'Game Day', type:'game'}
  ]
};

function getDays() { return DAYS[state.wt]; }

// ─── WEIGHTS ─────────────────────────────────────────────
// [ph0, ph1-deload, ph2, ph3-deload, ph4, ph5-test]
var WTS = {
  squat: [[110,115,120],[66,69,72],[127,132,137],[76,79,82],[140,145,150],[152]],
  trap:  [[152,157,162],[91,94,97],[165,170,175],[99,102,105],[175,180,185],[185]],
  bench: [[75,77.5,80],[45,47,48],[82.5,85,87.5],[50,52,53],[90,92.5,95],[100]],
  rdl:   [[80,85,90],[48,51,54],[95,100,105],[57,60,63],[107,112,117],[117]]
};
function sw(key) {
  var a = WTS[key]; if(!a) return '—';
  var v = a[state.phase];
  return Array.isArray(v) ? v[0]+'kg' : v+'kg';
}
function pw(key) {
  var a = WTS[key]; if(!a) return '—';
  var v = a[state.phase];
  if(!Array.isArray(v)) return v+'kg';
  var step = (v[2]-v[0])/2;
  return v[0]+'→'+v[2]+'kg (+'+step+'kg/wk)';
}
function isDeload() { return PHASES[state.phase].type === 'deload'; }
function isTest() { return PHASES[state.phase].type === 'test'; }

// ─── SLED LOADS ──────────────────────────────────────────
var SLED_FORCE = [['BW+20%','BW+18%','BW+10%'],['BW+12%','BW+10%','BW+6%'],['BW+18%','BW+15%','BW+8%'],['BW+11%','BW+9%','BW+6%'],['BW+12%','BW+10%','BW+6%'],['BW+8%']];
var SLED_VELO  = [['BW+11%','BW+10%','BW+8%'],['BW+7%','BW+6%','BW+5%'],['BW+13%','BW+11%','BW+9%'],['BW+8%','BW+7%','BW+6%'],['BW+8%','BW+7%','BW+6%'],['BW+6%']];
function slF() { var a = SLED_FORCE[state.phase]; return Array.isArray(a) ? a[0] : a; }
function slV() { var a = SLED_VELO[state.phase]; return Array.isArray(a) ? a[0] : a; }

// ─── READINESS ───────────────────────────────────────────
function rMod() {
  if (state.readiness >= 73) return 0;
  if (state.readiness >= 46) return 1;
  if (state.readiness >= 30) return 2;
  return 3;
}
function rpeBase(base) {
  var phShift = state.phase >= 4 ? 2 : state.phase >= 2 ? 1 : 0;
  return Math.min(10, base + phShift);
}
function rpeAdj(base) {
  var r = rpeBase(base);
  var m = rMod();
  return Math.max(4, r - m);
}
function setsAdj(s) {
  var n = parseInt(s);
  if (isNaN(n)) return s;
  if (isDeload()) return Math.max(2, Math.round(n * 0.6)) + '';
  var m = rMod();
  if (m === 0) return s;
  if (m === 1) return Math.max(2, n-1) + '';
  if (m >= 2) return Math.max(2, Math.round(n * 0.6)) + '';
  return s;
}
function rpeCls(r) {
  if (r <= 6) return 'rpe-low';
  if (r <= 8) return 'rpe-med';
  return 'rpe-high';
}

// ─── SESSION DATA ─────────────────────────────────────────
function SESSIONS(type) {
  var dl = isDeload();
  var data = {
    fullbody: {
      title: 'Full Body',
      sub: 'Monday — activate without pre-loading legs for sprints',
      dur: '60–65 min',
      shoulder: true,
      wu: ['Shoulder CARs ×10','Band pull-apart 2×20','Hip 90/90 ×45s each','Goblet squat 2×8 light','Leg swing ×10','Cat-cow ×8'],
      secs: [
        { h: 'Plyo primer', bt: 'plyo', exs: [
          { n:'Broad jump — stick landing', s:'3', r:'3', rpe:6, kg:'Bodyweight', note:'60% effort. Focus on landing mechanics — wide base, soft knees. Activates without fatiguing legs for Tuesday.', m:['Power','Dec'] },
          { n:'MB scoop throw', s:'3', r:'5', rpe:6, kg:'4–5kg', note:'Drive hips forward to launch ball upward. Posterior chain activation. Low shoulder stress.', m:['Power'] }
        ]},
        { h: 'Lower — moderate only', bt: 'str', exs: [
          { n:'Goblet squat', s:'3', r:'10', rpe:rpeAdj(6), kg:'32–40kg', note:'Activation not loading. Legs must feel fresh tomorrow. Drop weight further if Sunday felt heavy.', m:['Mass'] },
          { n:'Romanian deadlift', s:'3', r:'10', rpe:rpeAdj(6), kg:sw('rdl'), note:'Hip hinge pattern. Light enough that hamstrings feel ready for sprints tomorrow.', m:['Mass','Acc'] }
        ]},
        { h: 'Upper pull', bt: 'str', exs: [
          { n:'Chest-supported DB row', s:'4', r:'8–10', rpe:rpeAdj(7), kg:'32–36kg DBs', note:'Primary pull stimulus. Chest on bench removes lower back load. Drive elbow back, 1s hold at top.', m:['Mass'] },
          { n:'Single-arm cable row', s:'3', r:'12 each', rpe:rpeAdj(6), kg:'Moderate', note:'Slight rotation at top activates serratus. Throwing shoulder stability.', m:['Mass','Power'] }
        ]},
        { h: 'Upper push — submaximal', bt: 'str', skipMED: true, exs: [
          { n:'Landmine press — half-kneeling', s:'3', r:'10 each', rpe:rpeAdj(6), kg:'25–35kg', note:'Shoulder-safe pressing angle. Moderate only — Friday is the heavy push day.', m:['Mass'] },
          { n:'Cable lateral raise', s:'3', r:'15', rpe:rpeAdj(5), kg:'Light', note:'Shoulder health and size. Controlled.', m:['Mass'] }
        ]},
        { h: 'Core + prehab', bt: 'rehab', exs: [
          { n:'Pallof press — anti-rotation', s:'3', r:'12 each', rpe:5, kg:'Light', note:'Core stability for throwing and contact resistance.', m:['Power'] },
          { n:'Face pull', s:'3', r:'20', rpe:5, kg:'Band/cable', note:'Posterior capsule. Every session, no exceptions.' },
          { n:'Band external rotation', s:'3', r:'15 each', rpe:4, kg:'Band', note:'Non-negotiable. Rotator cuff protection post-dislocation.' },
          { n:'Wrist stretch — flexor + extensor', s:'2', r:'45s each', rpe:3, kg:'—', note:'Clears forearm tension.' }
        ]}
      ],
      note: "Monday's job: full-body activation and mass stimulus without pre-loading the legs. If legs are heavy from Sunday, drop lower work to bodyweight only."
    },
    sprint: {
      title: 'Sprint & Sled',
      sub: 'Tuesday — legs completely fresh, maximum quality',
      dur: '55–65 min',
      sled: true,
      wu: ['A-skip 2×20m','B-skip 2×20m','High knee march 2×20m','Leg swing front+side ×10','Pogo jumps 2×10','Hip 90/90 ×60s each'],
      secs: [
        { h: 'Plyo activation', bt: 'plyo', exs: [
          { n:'Broad jump — max distance', s:'4', r:'3', rpe:rpeAdj(8), kg:'Bodyweight', note:'Max intent today — legs are fresh. Horizontal power in the same direction as sled drive. Full 60s reset.', m:['Power','Acc'] },
          { n:'Pogo jump — bilateral', s:'3', r:'10', rpe:rpeAdj(7), kg:'Bodyweight', note:'Stiff ankle, minimal knee bend. Fast ground contact. Phase 2+: progress to single-leg.', m:['Power','Acc'] }
        ]},
        { h: 'Sled — force sets (heavy)', bt: 'sled', exs: [
          { n:'Heavy sled push — 10m drive phase', s:'5', r:'1', rpe:rpeAdj(9), kg:slF(), note:'Body angle 45°, short powerful strides, stay low. 3 min full rest. Loaded triple extension — best first-step exercise.', m:['Acc'] },
          { n:'Sled resisted backpedal — 10m', s:'4', r:'1', rpe:rpeAdj(8), kg:slF(), note:'Drive heels back, stay low, wide base. Trains posterior chain in braking pattern. Direct deceleration score work.', m:['Dec'] }
        ]},
        { h: 'Sled — velocity sets (light)', bt: 'sled', exs: [
          { n:'Light sled push — 20–25m build', s:'4', r:'1', rpe:rpeAdj(8), kg:slV(), note:'Lighter load preserves mechanics. Rise to upright by 12m. Targets speed-strength transition on the force-velocity curve.', m:['Acc','Power'] },
          { n:'Lateral sled drag — both directions', s:'4', r:'10m each way', rpe:rpeAdj(8), kg:slV(), note:'Hips low, push from lateral hip, no crossover. Best COD strength exercise without a partner.', m:['COD','Dec'] }
        ]},
        { h: 'Free sprints', bt: 'speed', exs: [
          { n:'Flying 20m — 10m build, 20m max', s:'4', r:'1', rpe:rpeAdj(9), kg:'Unloaded', note:'Post-sled CNS is primed. 4 min full rest. Phase 1: 3 reps only. Time these weekly — track toward sub-4.50.', m:['Power'] },
          { n:'Pro-agility 5-10-5 — timed both ways', s:'4', r:'1 each way', rpe:rpeAdj(8), kg:'Unloaded', note:'Full accel + decel + reaccel. Time it every session. Most sport-specific COD drill for a QB.', m:['COD','Dec','Acc'] }
        ]},
        { h: 'QB footwork', bt: 'skill', skipMED: true, exs: [
          { n:'3-step + 5-step drop-back', s:'3', r:'6 each', rpe:5, kg:'—', note:'Footwork only — no ball. Weight transfer and platform mechanics. Groove pattern while legs warm.' },
          { n:'Sprint-out left + right — 10m', s:'3', r:'4 each', rpe:rpeAdj(6), kg:'—', note:'Accelerate off 5-step drop. Hips open to throw side. QB speed-on-the-move.', m:['Acc'] }
        ]}
      ],
      note: 'Dual sled model: force sets (heavy, short) build max force for first step. Velocity sets (light, long) build speed-strength transition. Both needed for complete momentum score.'
    },
    lower: {
      title: 'Lower Power & Mass',
      sub: 'Thursday — 2 days post-sprint, heaviest lower session',
      dur: '70–80 min',
      wu: ['Hip 90/90 ×60s each','Glute bridge 2×15','Banded clamshell 2×15 each','Goblet squat 3×8 light','Leg swing ×10 each direction'],
      secs: [
        { h: 'Plyo primer — max power first', bt: 'plyo', exs: [
          { n:'Box jump — max height, step down', s:'4', r:'4', rpe:rpeAdj(8), kg:'Bodyweight', note:'Step down every rep — never jump down in-season. Full reset. Vertical power for trucking and contact.', m:['Power','Acc'] },
          { n:'Lateral bound — stick landing 2s', s:'3', r:'5 each', rpe:rpeAdj(8), kg:'Bodyweight', note:'Push laterally, land single-leg, hold 2s. The hold trains deceleration absorption.', m:['COD','Dec','Power'] },
          { n:'Depth drop → 5m sprint', s:'3', r:'4', rpe:rpeAdj(8), kg:'Bodyweight', note:'Step off 30cm box, absorb, sprint immediately. Decel-to-reaccel — exact scramble pattern.', m:['Dec','Acc'] }
        ]},
        { h: 'Main strength', bt: 'str', exs: [
          { n:'Barbell back squat', s:'4', r:'4–6', rpe:rpeAdj(8), kg:pw('squat'), note:'Est. 1RM 152kg. Starting '+sw('squat')+'. Add 5kg/wk Ph1, 2.5kg Ph2+. Hard brace, drive the floor away.', m:['Mass','Acc'] },
          { n:'Trap bar deadlift', s:'4', r:'5–6', rpe:rpeAdj(8), kg:pw('trap'), note:'1RM 188kg. Starting '+sw('trap')+'. Add 5kg/wk Ph1, 2.5kg Ph2+. Neutral spine. Reduced lumbar stress vs barbell.', m:['Mass','Acc','Dec'] }
        ]},
        { h: 'Unilateral + hamstring', bt: 'str', skipMED: true, exs: [
          { n:'Bulgarian split squat', s:'3', r:'8 each', rpe:rpeAdj(7), kg:'60–70kg total (DBs)', note:'Single-leg stability under load. Transfers directly to cutting mechanics.', m:['Mass','COD'] },
          { n:'Nordic hamstring curl', s:'3', r:'5–6', rpe:rpeAdj(8), kg:'Bodyweight', note:'51% injury reduction in footballers (Petersen 2011). Eccentric only if full rep too hard. Priority.', m:['Dec','Acc'] },
          { n:'Leg press — feet high and wide', s:'3', r:'12–15', rpe:rpeAdj(7), kg:'Heavy', note:'Glute/hamstring dominant. Good volume accumulator. Add 10kg/wk.', m:['Mass'] }
        ]},
        { h: 'Hip power + ankle', bt: 'plyo', skipMED: true, exs: [
          { n:'Barbell hip thrust', s:'3', r:'10–12', rpe:rpeAdj(7), kg:'100–120kg', note:'Full glute contraction at top. Sprint drive and pelvic stability. Add 5kg/wk.', m:['Mass','Acc'] },
          { n:'Single-leg calf raise — 3s up, 3s down', s:'3', r:'15 each', rpe:rpeAdj(7), kg:'Bodyweight+', note:'Builds ankle stiffness for sled and sprint demands. Reduces Achilles risk in-season.', m:['Acc','Power'] }
        ]}
      ],
      note: 'Plyo primer goes first while CNS is sharp — never move these to the end. Stop main lifts 1–2 reps short of failure. Track every weight every session.'
    },
    upper: {
      title: 'Full Upper — Push + Pull',
      sub: 'Friday — comprehensive upper, furthest from Sunday',
      dur: '70–80 min',
      shoulder: true,
      wu: ['Shoulder CARs ×10','Band pull-apart 2×20','Push-up to down-dog ×8','MB chest pass ×5 explosive','Dead hang 20s','Scap wall slide 2×12'],
      secs: [
        { h: 'Plyo + rotational power', bt: 'plyo', exs: [
          { n:'MB chest pass — wall, explosive', s:'4', r:'5', rpe:rpeAdj(7), kg:'4–5kg', note:'Max intent. Horizontal rate of force development. Throwing push phase and blocking power.', m:['Power'] },
          { n:'MB rotational slam — both sides', s:'3', r:'5 each', rpe:rpeAdj(7), kg:'4–6kg', note:'Hips first, arms follow. Exact throwing mechanics under load. Rotational power for velocity and trucking.', m:['Power'] }
        ]},
        { h: 'Main push', bt: 'str', exs: [
          { n:'Barbell bench press', s:'4', r:'6–8', rpe:rpeAdj(7), kg:pw('bench'), note:'1RM 100kg. Start '+sw('bench')+'. Add 2.5kg/wk. 2s eccentric. Grip just outside shoulder — capsule protection.', m:['Mass'] },
          { n:'Incline DB press', s:'3', r:'10–12', rpe:rpeAdj(6), kg:'28–32kg DBs', note:'Stop 10° short of full stretch at bottom. Upper chest mass. Add 2kg DBs when range feels easy.', m:['Mass'] }
        ]},
        { h: 'Main pull', bt: 'str', exs: [
          { n:'Weighted pull-up (or neutral-grip pulldown)', s:'4', r:'5–8', rpe:rpeAdj(7), kg:'+5–10kg added', note:'Full hang at bottom. Neutral grip if elbow sensitive. Add 2.5kg when top of range feels clean.', m:['Mass'] },
          { n:'Bent-over row', s:'4', r:'8–10', rpe:rpeAdj(7), kg:'70–80kg', note:'Hip hinge, flat back. Drive elbow back, 1s hold. Phase 2+: add chest-support if lower back fatigues.', m:['Mass'] }
        ]},
        { h: 'Accessory supersets', bt: 'str', skipMED: true, exs: [
          { n:'Landmine press (A) + face pull (B)', s:'3', r:'8 each / 20', rpe:rpeAdj(6), kg:'30–40kg / band', note:'Superset. Shoulder-safe pressing + posterior capsule. 60s rest between pairs.', m:['Mass'] },
          { n:'Cable lateral raise (A) + hammer curl (B)', s:'3', r:'15 / 12–15', rpe:rpeAdj(6), kg:'Light / 16–20kg', note:'Superset. Delt size + elbow-friendly bicep work.', m:['Mass'] }
        ]},
        { h: 'Shoulder + elbow prehab', bt: 'rehab', exs: [
          { n:'Band ER — elbow pinned at 90°', s:'3', r:'15 each', rpe:4, kg:'Band', note:'Every upper session. No exceptions.' },
          { n:'Side-lying ER — 2kg max', s:'2', r:'15 each', rpe:4, kg:'2kg', note:'Infraspinatus strength. Protective only — keep it light.' },
          { n:'Prone Y-T-W — 2kg', s:'2', r:'10 each', rpe:4, kg:'2kg', note:'Lower trap and posterior rotator cuff. Non-negotiable post-dislocation.' },
          { n:'Wrist flexor + extensor stretch', s:'2', r:'45s each', rpe:3, kg:'—', note:'Non-negotiable after pressing and pulling.' }
        ]}
      ],
      note: 'Friday is the best upper day — push main compounds hard. Game week: this session becomes skill-lite only. Switch to landmine immediately at first sign of shoulder impingement.'
    },
    skill: {
      title: 'Skill + Agility',
      sub: 'Saturday — high quality, low fatigue before Sunday',
      dur: '50–55 min',
      shoulder: true,
      wu: ['Shoulder CARs ×10','Band pull-apart 2×15','Arm circles ×10','Light jog 5 min','MB wrist snap throws ×10'],
      secs: [
        { h: 'Reactive agility + deceleration', bt: 'skill', exs: [
          { n:'L-drill 3-cone — both directions, timed', s:'5', r:'1 each way', rpe:rpeAdj(6), kg:'—', note:'Plant foot outside edge at change point. Hips low. Time every session — direct momentum score measurement.', m:['COD','Acc'] },
          { n:'20m sprint to full stop — braking drill', s:'5', r:'1', rpe:rpeAdj(7), kg:'—', note:'Sprint 90%, brake in 3–4 steps. Wide base, heels back, low hips. Practising deceleration mechanics improves your score.', m:['Dec'] },
          { n:'Reactive shuffle to sprint — visual cue', s:'4', r:'5', rpe:rpeAdj(7), kg:'—', note:'Shuffle laterally, react to cue, accelerate 5m. First-step from lateral base — pocket scramble pattern.', m:['COD','Acc'] }
        ]},
        { h: 'QB throwing', bt: 'skill', exs: [
          { n:'Wrist snap throws — 5m', s:'3', r:'10', rpe:5, kg:'—', note:'Fingertip control, no arm. Minimal shoulder stress.' },
          { n:'Hip-driven throws — 15–20m', s:'4', r:'8', rpe:6, kg:'Ball', note:'Hips first, arm follows. Platform, weight transfer, follow-through. Stop immediately at shoulder tightness.', m:['Power'] },
          { n:'Drop-back + throw — 3 and 5 step', s:'3', r:'6 each', rpe:6, kg:'Ball', note:'Full footwork + throw integration. Sprint-out both directions.', m:['Power','Acc'] }
        ]},
        { h: 'MB power + plyo', bt: 'plyo', skipMED: true, exs: [
          { n:'MB rotational throw — both sides', s:'3', r:'8 each', rpe:rpeAdj(6), kg:'4–6kg', note:'Rotational power for throw velocity and trucking.', m:['Power'] },
          { n:'Broad jump → deceleration stick', s:'3', r:'5', rpe:rpeAdj(6), kg:'—', note:'Jump forward, absorb landing with wide base. Jump-to-brake pattern of scrambles.', m:['Power','Dec'] }
        ]},
        { h: 'Soft tissue close-out', bt: 'rehab', exs: [
          { n:'Foam roll — thoracic, quads, IT band', s:'1', r:'60s each', rpe:3, kg:'—', note:'' },
          { n:'Hip flexor kneeling stretch', s:'2', r:'60s each', rpe:3, kg:'—', note:'' },
          { n:'Wrist flexor + extensor stretch', s:'2', r:'45s each', rpe:3, kg:'—', note:'Non-negotiable after throwing.' }
        ]}
      ],
      note: 'Leave this session feeling sharp, not fatigued. If tired, drop throwing and keep agility only. You perform tomorrow.'
    },
    skilllite: {
      title: 'Skill + Prehab Only',
      sub: 'Game week Friday — protect the body for Sunday',
      dur: '35–40 min',
      shoulder: true,
      wu: ['Shoulder CARs ×10','Band pull-apart 2×15','Light jog 5 min'],
      secs: [
        { h: 'Light activation', bt: 'plyo', exs: [
          { n:'Box jump — 70% effort, step down', s:'3', r:'3', rpe:5, kg:'—', note:'CNS wake-up only. Not for adaptation today. Easy, fast, sharp.' },
          { n:'Lateral bound — pattern only', s:'2', r:'4 each', rpe:5, kg:'—', note:'Feel the landing mechanics. Not for power output.' }
        ]},
        { h: 'QB throwing — low volume', bt: 'skill', exs: [
          { n:'Wrist snap + hip throws + drop-back', s:'2', r:'6–8 each', rpe:4, kg:'Ball', note:'Low volume. Feel the mechanics. Stop at any shoulder tightness.' }
        ]},
        { h: 'Full prehab protocol', bt: 'rehab', exs: [
          { n:'Band ER + face pull + side-lying ER', s:'3', r:'15/20/15', rpe:4, kg:'Band/2kg', note:'Full shoulder sequence. This is the priority today.' },
          { n:'Wrist + hip flexor + thoracic', s:'2', r:'60s each', rpe:3, kg:'—', note:'' }
        ]}
      ],
      note: 'Non-negotiable light session. Any fatigue today directly costs Sunday output.'
    }
  };
  return data[type] || null;
}

// ─── BUILD SESSION HTML ───────────────────────────────────
function buildSessionHTML(type) {
  if (!type || type === 'rest' || type === 'game' || type === 'practice') {
    return buildNonTraining(type);
  }
  if (isTest()) {
    return buildTestWeek(type);
  }
  var sess = SESSIONS(type);
  if (!sess) return buildNonTraining('rest');

  var m = rMod();
  var html = '';

  // Readiness alert
  if (m === 1) {
    html += '<div class="mod-alert amber">Readiness score '+state.readiness+' — moderate. RPE down 1 point. Remove one accessory set per exercise.</div>';
  } else if (m === 2) {
    html += '<div class="mod-alert red">Readiness score '+state.readiness+' — low. Minimum effective dose. Main lifts only. Volume cut 40%.</div>';
  } else if (m >= 3) {
    html += '<div class="non-training" style="margin:0 14px"><div class="non-training-title condensed">Prehab Only Today</div><div class="non-training-body">Fitbit score below 30. Band ERs 3×15, face pulls 3×20, wrist stretches, thoracic rotation, hip 90/90. Sleep 8+ hrs tonight.</div></div>';
    return html;
  }

  // Phase banner
  var pi = PHASES[state.phase];
  if (isDeload()) {
    html += '<div class="phase-info-banner deload">Deload week — sets reduced to 60%. Load unchanged. Supercompensation happens here (Kiely, 2012).</div>';
  }

  // Sled dual load
  if (sess.sled) {
    html += '<div class="card"><div class="sled-grid">';
    html += '<div class="sled-card"><div class="sled-type">Force sets</div><div class="sled-load condensed">'+slF()+'</div><div class="sled-desc">10m drives · 5 reps · 3 min rest<br>Low angle · first-step acceleration</div></div>';
    html += '<div class="sled-card"><div class="sled-type">Velocity sets</div><div class="sled-load condensed">'+slV()+'</div><div class="sled-desc">20–25m builds · 4 reps · 4 min rest<br>Speed-strength expression</div></div>';
    html += '</div></div>';
  }

  // Warmup
  html += '<div class="card">';
  html += '<div class="warmup-wrap"><div class="warmup-title">Warm-up</div><div class="warmup-tags">';
  (sess.wu || []).forEach(function(w) { html += '<span class="warmup-tag">'+w+'</span>'; });
  html += '</div></div>';

  // Sections
  (sess.secs || []).forEach(function(sec) {
    var skip = m >= 2 && sec.skipMED;
    if (skip) {
      html += '<div class="sec-head"><span class="sec-head-label">'+sec.h+'</span><span class="badge badge-amber" style="margin-left:4px">skipped — low readiness</span></div>';
      return;
    }
    var btLabels = {plyo:'Plyometric', sled:'Sled', str:'Strength', speed:'Speed', skill:'Skill', rehab:'Prehab'};
    var btCls = {plyo:'badge-purple', sled:'badge-amber', str:'badge-blue', speed:'badge-red', skill:'badge-teal', rehab:'badge-red'};
    html += '<div class="sec-head"><span class="sec-head-label">'+sec.h+'</span><span class="badge '+(btCls[sec.bt]||'badge-grey')+'">'+btLabels[sec.bt]+'</span></div>';

    (sec.exs || []).forEach(function(ex, ei) {
      var adjS = setsAdj(ex.s);
      var r = rpeAdj(ex.rpe);
      var rc = rpeCls(r);
      var doneKey = 'done_'+getTodayKey()+'_'+type+'_'+sec.h+'_'+ei;
      var isDone = localStorage.getItem(doneKey) === '1';
      var exId = 'ex_'+type+'_'+sec.h.replace(/\s/g,'')+'_'+ei;

      html += '<div class="ex-row" id="row_'+exId+'">';
      html += '<div class="ex-main">';
      html += '<button class="ex-done-btn'+(isDone?' done':'')+'" onclick="toggleDone(\''+doneKey+'\',\'row_'+exId+'\')" ontouchend="this.click()">';
      html += '<svg width="12" height="12" viewBox="0 0 12 12" fill="none"><polyline points="2 6 5 9 10 3" stroke="white" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/></svg>';
      html += '</button>';
      html += '<div class="ex-info">';
      html += '<div class="ex-name'+(isDone?' done-text':'')+'">'+ex.n+'</div>';
      html += '<div class="ex-stats">';
      html += '<span class="stat-pill">'+adjS+'×'+ex.r+'</span>';
      if (ex.kg && ex.kg !== '—') html += '<span class="stat-pill load">'+ex.kg+'</span>';
      html += '<span class="stat-pill '+rc+'">RPE '+r+'</span>';
      if (m === 1 && ex.rpe > 5) html += '<span class="stat-pill reduced">-1 RPE</span>';
      html += '</div></div>';
      html += '<svg class="ex-chevron" id="chev_'+exId+'" width="16" height="16" viewBox="0 0 16 16" fill="none"><polyline points="6 4 10 8 6 12" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg>';
      html += '</div>';

      if (ex.note || (ex.m && ex.m.length)) {
        html += '<div class="ex-note-wrap" id="note_'+exId+'">';
        if (ex.note) html += ex.note;
        if (ex.m && ex.m.length) {
          html += '<div class="mo-tags">';
          ex.m.forEach(function(tag) {
            var tc = {Acc:'mo-acc',Dec:'mo-dec',COD:'mo-cod',Mass:'mo-mass',Power:'mo-power'}[tag] || 'mo-acc';
            html += '<span class="mo-tag '+tc+'">'+tag+'</span>';
          });
          html += '</div>';
        }
        html += '</div>';
        html = html.replace('id="row_'+exId+'"', 'id="row_'+exId+'" onclick="toggleNote(\''+exId+'\')"');
      }

      html += '</div>';
    });
  });

  html += '<div class="session-note">'+sess.note+'</div>';
  html += '</div>';

  return html;
}

function buildNonTraining(type) {
  var info = {
    rest: { title: 'Rest Day', body: 'Light prehab only — band ERs, face pulls, wrist stretches, thoracic mobility, hip 90/90. Optional 20 min walk.' },
    game: { title: 'Game Day', body: 'No training. Dynamic activation only (10 min): leg swings, A-skips, arm circles, shoulder CARs.\n\nPost-game: protein within 30 min, ice contact areas, 8+ hrs sleep.' },
    practice: { title: 'Team Practice', body: 'No gym today. Pre-practice: A-skips, leg swings, shoulder CARs, band pull-aparts (10 min).\n\nPost-practice: wrist stretches, foam roll quads + thoracic. Hydrate.' }
  };
  var i = info[type] || { title: 'Rest', body: 'Light prehab and mobility.' };
  return '<div class="non-training"><div class="non-training-title condensed">'+i.title+'</div><div class="non-training-body">'+i.body+'</div></div>';
}

function buildTestWeek(type) {
  return '<div class="non-training"><div class="non-training-title condensed">Test Week</div><div class="non-training-body" style="text-align:left">Retest all baselines this week:<br><br><strong>Tue:</strong> 40-yard dash (3 attempts, best). Flying 20m. Pro-agility 5-10-5.<br><strong>Thu:</strong> Squat 3RM estimate. Trap bar 3RM estimate.<br><strong>Fri:</strong> Bench 3RM estimate.<br><strong>Sat:</strong> Throw distance (5 attempts).<br><br>Compare vs Week 1 baselines.</div></div>';
}

// ─── TOGGLE EXERCISE NOTE ─────────────────────────────────
function toggleNote(id) {
  var note = document.getElementById('note_'+id);
  var chev = document.getElementById('chev_'+id);
  if (!note) return;
  var open = note.classList.contains('open');
  note.classList.toggle('open', !open);
  if (chev) chev.classList.toggle('open', !open);
}

// ─── TOGGLE DONE ─────────────────────────────────────────
function toggleDone(key, rowId) {
  var isDone = localStorage.getItem(key) === '1';
  localStorage.setItem(key, isDone ? '0' : '1');
  var row = document.getElementById(rowId);
  if (!row) return;
  var btn = row.querySelector('.ex-done-btn');
  var name = row.querySelector('.ex-name');
  if (!isDone) {
    btn && btn.classList.add('done');
    name && name.classList.add('done-text');
  } else {
    btn && btn.classList.remove('done');
    name && name.classList.remove('done-text');
  }
}

function getTodayKey() {
  var d = new Date();
  return d.getFullYear()+''+(d.getMonth()+1)+''+d.getDate();
}

// ─── TODAY VIEW ───────────────────────────────────────────
function getTodayDayIndex() {
  var jsDay = new Date().getDay(); // 0=Sun, 1=Mon...
  var map = [6, 0, 1, 2, 3, 4, 5]; // Map JS day to our Mon-Sun array
  return map[jsDay];
}

function renderToday() {
  var idx = getTodayDayIndex();
  var d = getDays()[idx];
  var dateStr = new Date().toLocaleDateString('en-GB', {weekday:'long', day:'numeric', month:'long'});
  document.getElementById('today-date').textContent = dateStr;

  var sess = (d.type !== 'rest' && d.type !== 'game' && d.type !== 'practice') ? SESSIONS(d.type) : null;
  document.getElementById('today-name').textContent = sess ? sess.title : d.t;

  var badges = document.getElementById('today-badges');
  var ph = PHASES[state.phase];
  badges.innerHTML = '<span class="badge badge-blue">'+ph.short+'</span>';
  if (sess && sess.shoulder) badges.innerHTML += '<span class="badge badge-amber">Shoulder active</span>';
  if (state.wt === 'game') badges.innerHTML += '<span class="badge badge-red">Game week</span>';

  document.getElementById('today-content').innerHTML = buildSessionHTML(d.type);
}

// ─── WEEK VIEW ────────────────────────────────────────────
function renderWeek() {
  renderPhaseRow();
  renderDayStrip();
  renderWeekSession();
}

function renderPhaseRow() {
  var row = document.getElementById('phase-row');
  row.innerHTML = '';
  PHASES.forEach(function(p, i) {
    var cls = 'phase-pill';
    if (p.type === 'deload') cls += ' deload';
    if (p.type === 'test') cls += ' test-wk';
    if (i === state.phase) cls += ' active';
    var btn = document.createElement('button');
    btn.className = cls;
    btn.textContent = p.label;
    btn.onclick = function() { state.phase = i; saveState(); renderAll(); };
    row.appendChild(btn);
  });
}

function renderDayStrip() {
  var strip = document.getElementById('day-strip');
  strip.innerHTML = '';
  getDays().forEach(function(d, i) {
    var el = document.createElement('div');
    var cls = 'day-chip';
    if (d.type === 'rest') cls += ' is-rest';
    else if (d.type === 'game') cls += ' is-game';
    else if (d.type === 'practice') cls += ' is-prac';
    else if (isDeload() || isTest()) cls += ' is-deload';
    if (i === state.selDay) cls += ' selected';
    el.className = cls;
    el.innerHTML = '<div class="day-chip-name">'+d.n+'</div><div class="day-chip-type">'+d.t.replace(' + ','\n').replace(' & ','\n')+'</div>';
    if (d.type !== 'rest' && d.type !== 'game' && d.type !== 'practice') {
      (function(idx) { el.onclick = function() { state.selDay = idx; saveState(); renderDayStrip(); renderWeekSession(); }; })(i);
    }
    strip.appendChild(el);
  });
}

function renderWeekSession() {
  var d = getDays()[state.selDay];
  var cont = document.getElementById('week-session-content');
  if (!d) { cont.innerHTML = ''; return; }

  var sess = (d.type !== 'rest' && d.type !== 'game' && d.type !== 'practice') ? SESSIONS(d.type) : null;
  var html = '';

  // Session header card
  html += '<div class="card"><div class="card-header">';
  html += '<div class="card-title condensed">'+(sess ? sess.title : d.t)+'</div>';
  html += '<div class="card-sub">'+(sess ? sess.sub : '')+'</div>';
  html += '<div class="card-meta">';
  html += '<span class="badge badge-blue">'+PHASES[state.phase].short+'</span>';
  if (sess && sess.dur) html += '<span class="badge badge-grey">'+sess.dur+'</span>';
  if (sess && sess.shoulder) html += '<span class="badge badge-amber">Shoulder active</span>';
  html += '</div></div></div>';

  html += buildSessionHTML(d.type);
  cont.innerHTML = html;
}

// ─── SETTINGS VIEW ────────────────────────────────────────
function renderSettings() {
  document.getElementById('r-slider').value = state.readiness;
  updateReadinessUI();
}

function setReadiness(v) {
  state.readiness = parseInt(v);
  saveState();
  updateReadinessUI();
}

function updateReadinessUI() {
  var v = state.readiness;
  var score = document.getElementById('settings-score');
  var status = document.getElementById('settings-status');
  var mods = document.getElementById('settings-mods');
  var dot = document.getElementById('r-dot');
  var badge = document.getElementById('r-badge-text');

  score.textContent = v;

  var label, statusTxt, modsTxt, color;
  if (v >= 73) {
    label = 'High — full session'; color = 'var(--green)'; statusTxt = 'Full session as programmed';
    modsTxt = 'All sets, loads and RPE targets as programmed. Push the main lifts.';
    dot.className = 'r-dot'; badge.textContent = v + ' — Ready';
  } else if (v >= 46) {
    label = 'Moderate'; color = 'var(--amber)'; statusTxt = 'Slight modification in effect';
    modsTxt = 'Main lift RPE reduced by 1. Remove one accessory set per exercise. Loads unchanged — stop a rep earlier.';
    dot.className = 'r-dot amber'; badge.textContent = v + ' — Caution';
  } else if (v >= 30) {
    label = 'Low — minimum dose'; color = 'var(--red)'; statusTxt = 'Minimum effective dose';
    modsTxt = 'Volume cut 40%. RPE down 2. Main compounds only. Skip accessory work. Keep all prehab.';
    dot.className = 'r-dot red'; badge.textContent = v + ' — Low';
  } else {
    label = 'Very low — rest'; color = 'var(--text3)'; statusTxt = 'Prehab and mobility only';
    modsTxt = 'No training today. 20 min prehab protocol only. Prioritise sleep tonight.';
    dot.className = 'r-dot grey'; badge.textContent = v + ' — Rest';
  }

  score.style.color = color;
  status.textContent = statusTxt;
  status.style.color = color;
  mods.textContent = modsTxt;
}

// ─── WEEK TYPE ────────────────────────────────────────────
function setWT(t) {
  state.wt = t;
  saveState();
  document.getElementById('wt-p').classList.toggle('active', t === 'practice');
  document.getElementById('wt-g').classList.toggle('active', t === 'game');
  renderWeek();
  renderToday();
}

// ─── TAB SWITCHING ────────────────────────────────────────
function switchTab(name) {
  state.tab = name;
  ['today','week','settings'].forEach(function(t) {
    document.getElementById('view-'+t).classList.toggle('active', t === name);
    document.getElementById('tab-'+t).classList.toggle('active', t === name);
  });
  if (name === 'today') renderToday();
  if (name === 'week') renderWeek();
  if (name === 'settings') renderSettings();
}

// ─── RENDER ALL ───────────────────────────────────────────
function renderAll() {
  renderToday();
  renderWeek();
  renderSettings();
}

// ─── GENERATE HOME SCREEN ICON ───────────────────────────
function createIcon() {
  try {
    var c = document.createElement('canvas');
    c.width = 180; c.height = 180;
    var ctx = c.getContext('2d');
    ctx.fillStyle = '#0d0d0d';
    ctx.beginPath();
    ctx.roundRect(0, 0, 180, 180, 36);
    ctx.fill();
    ctx.fillStyle = '#22c55e';
    ctx.font = 'bold 28px "Barlow Condensed", sans-serif';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.fillText('MOMENTUM', 90, 46);
    ctx.fillStyle = '#f2f2f2';
    ctx.font = 'bold 82px "Barlow Condensed", sans-serif';
    ctx.fillText('M', 90, 112);
    ctx.fillStyle = '#1f1f1f';
    ctx.fillRect(20, 148, 140, 4);
    ctx.fillStyle = '#22c55e';
    ctx.fillRect(20, 148, 90, 4);
    var link = document.createElement('link');
    link.rel = 'apple-touch-icon';
    link.href = c.toDataURL('image/png');
    document.head.appendChild(link);
  } catch(e) {}
}

// ─── INIT ─────────────────────────────────────────────────
createIcon();
document.getElementById('r-slider').value = state.readiness;
document.getElementById('wt-p').classList.toggle('active', state.wt === 'practice');
document.getElementById('wt-g').classList.toggle('active', state.wt === 'game');
updateReadinessUI();
renderAll();
</script>

</body>
</html>
