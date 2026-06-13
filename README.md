<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Leave Data Pro</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&family=IBM+Plex+Mono:wght@400;600&display=swap');

  :root {
    --purple-dark: #3B0A6E;
    --purple: #6C3CE1;
    --purple-mid: #8B5CF6;
    --purple-light: #C4B5FD;
    --purple-pale: #EDE9FE;
    --purple-glass: rgba(108,60,225,0.12);
    --white: #FFFFFF;
    --off-white: #F8F7FF;
    --card-white: #FFFFFF;
    --text-dark: #1A0A3C;
    --text-mid: #5B4B8A;
    --text-muted: #9B89C4;
    --success: #10B981;
    --warning: #F59E0B;
    --danger: #EF4444;
    --info: #6366F1;
    --accent-green: #34D399;
    --accent-pink: #F472B6;
    --shadow-purple: 0 8px 32px rgba(108,60,225,0.22);
    --shadow-card: 0 4px 20px rgba(59,10,110,0.10);
    --radius: 20px;
    --radius-sm: 14px;
    --radius-pill: 50px;
    --font: 'Prompt', sans-serif;
    --mono: 'IBM Plex Mono', monospace;
  }

  * { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }

  body {
    font-family: var(--font);
    background: var(--off-white);
    color: var(--text-dark);
    min-height: 100vh;
    max-width: 430px;
    margin: 0 auto;
    overflow-x: hidden;
    position: relative;
  }

  .screen { display:none; min-height:100vh; flex-direction:column; }
  .screen.active { display:flex; }

  /* =================== BLOBS =================== */
  .blob-bg {
    position: absolute; pointer-events: none; z-index: 0;
    border-radius: 50%; filter: blur(60px); opacity: 0.55;
  }

  /* =================== SPLASH =================== */
  #screen-splash {
    background: linear-gradient(155deg, #3B0A6E 0%, #6C3CE1 55%, #A78BFA 100%);
    align-items: center; justify-content: space-between;
    overflow: hidden; position: relative;
  }

  .splash-blob1 {
    width: 280px; height: 280px;
    background: rgba(255,255,255,0.08);
    top: -60px; right: -80px;
  }
  .splash-blob2 {
    width: 220px; height: 220px;
    background: rgba(167,139,250,0.25);
    bottom: 120px; left: -60px;
  }

  .splash-hero {
    flex: 1; display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    padding: 70px 32px 32px; position: relative; z-index: 2;
  }

  .splash-icon-wrap {
    width: 110px; height: 110px; border-radius: 32px;
    background: rgba(255,255,255,0.18);
    backdrop-filter: blur(12px);
    border: 1.5px solid rgba(255,255,255,0.3);
    display: flex; align-items: center; justify-content: center;
    font-size: 52px; margin-bottom: 28px;
    box-shadow: 0 8px 40px rgba(59,10,110,0.35), inset 0 1px 0 rgba(255,255,255,0.3);
    animation: floatIcon 3s ease-in-out infinite;
  }

  @keyframes floatIcon {
    0%,100% { transform: translateY(0); }
    50% { transform: translateY(-8px); }
  }

  .splash-brand h1 {
    font-size: 30px; font-weight: 700; color: #fff;
    text-align: center; letter-spacing: -0.5px; line-height: 1.1;
  }

  .splash-brand .sub {
    font-size: 12px; color: rgba(255,255,255,0.65);
    font-family: var(--mono); letter-spacing: 2.5px;
    text-transform: uppercase; text-align: center;
    margin-top: 6px;
  }

  .splash-tagline {
    font-size: 14px; color: rgba(255,255,255,0.7);
    text-align: center; max-width: 260px; line-height: 1.7;
    margin: 16px 0 36px;
  }

  .splash-pills {
    display: flex; gap: 10px; flex-wrap: wrap; justify-content: center;
    margin-bottom: 40px;
  }

  .splash-pill {
    background: rgba(255,255,255,0.15);
    backdrop-filter: blur(8px);
    border: 1px solid rgba(255,255,255,0.25);
    border-radius: var(--radius-pill);
    padding: 8px 16px;
    font-size: 12px; color: #fff; font-weight: 500;
    display: flex; align-items: center; gap: 6px;
  }

  .splash-bottom {
    padding: 20px 24px 48px; width: 100%; position: relative; z-index: 2;
  }

  .btn-white {
    width: 100%; padding: 17px;
    background: #fff; border: none;
    border-radius: var(--radius-pill);
    color: var(--purple); font-family: var(--font);
    font-size: 16px; font-weight: 700;
    cursor: pointer; letter-spacing: 0.2px;
    box-shadow: 0 8px 30px rgba(0,0,0,0.2);
    transition: all 0.2s;
    display: flex; align-items: center; justify-content: center; gap: 8px;
  }

  .btn-white:active { transform: scale(0.97); }

  .splash-version {
    text-align: center; margin-top: 14px;
    font-size: 11px; color: rgba(255,255,255,0.4);
    font-family: var(--mono);
  }

  /* =================== LOGIN =================== */
  #screen-login {
    background: var(--off-white);
    overflow-y: auto;
    flex-direction: column;
  }

  .login-body {
    padding: 22px 24px 32px;
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .login-header-wrap {
    background: linear-gradient(150deg, #3B0A6E 0%, #6C3CE1 100%);
    padding: 32px 24px 28px;
    position: relative; overflow: hidden;
    display: flex; align-items: center; gap: 14px;
  }

  .login-header-wrap::before {
    content: '';
    position: absolute; inset: 0;
    background-image: radial-gradient(rgba(255,255,255,0.10) 1px, transparent 1px);
    background-size: 16px 16px;
    opacity: 0.5;
  }

  .login-header-blob {
    position: absolute; width: 160px; height: 160px;
    background: rgba(167,139,250,0.22);
    border-radius: 50%; top: -70px; right: -50px;
    filter: blur(4px);
  }

  .login-logo-sm {
    width: 50px; height: 50px; border-radius: 16px;
    background: rgba(255,255,255,0.16);
    border: 1.5px solid rgba(255,255,255,0.28);
    display: flex; align-items: center; justify-content: center;
    backdrop-filter: blur(10px);
    flex-shrink: 0; position: relative; z-index: 1;
  }

  .login-header-text { position: relative; z-index: 1; min-width: 0; }
  .login-header-wrap h2 { font-size: 19px; font-weight: 700; color: #fff; line-height: 1.2; }
  .login-header-wrap p { font-size: 12px; color: rgba(255,255,255,0.6); margin-top: 3px; }

  .login-section-label {
    font-size: 11px; font-weight: 700; color: var(--text-muted);
    text-transform: uppercase; letter-spacing: 1px;
    margin-bottom: 10px; margin-top: 22px;
  }
  .login-section-label:first-child { margin-top: 0; }

  .role-toggle {
    display: flex; gap: 8px;
    background: var(--purple-pale);
    border-radius: var(--radius);
    padding: 5px;
  }

  .role-toggle .role-option {
    flex: 1; display: flex; align-items: center; justify-content: center; gap: 8px;
    padding: 12px 10px;
    border-radius: var(--radius-sm);
    cursor: pointer; transition: all 0.2s;
    font-size: 13px; font-weight: 600; color: var(--text-mid);
  }

  .role-toggle .role-option.selected {
    background: #fff; color: var(--purple);
    box-shadow: 0 3px 12px rgba(108,60,225,0.18);
  }

  .role-toggle .role-option svg { width: 17px; height: 17px; stroke-width: 2; flex-shrink: 0; }

  .form-group { margin-bottom: 14px; }

  .form-label {
    display: block; font-size: 12px; font-weight: 600;
    color: var(--text-mid); margin-bottom: 8px;
    text-transform: uppercase; letter-spacing: 0.8px;
  }

  .form-control {
    width: 100%; padding: 13px 16px;
    background: #fff;
    border: 1.5px solid #E5E0F5;
    border-radius: var(--radius-sm);
    color: var(--text-dark);
    font-family: var(--font); font-size: 15px;
    outline: none; transition: all 0.2s;
    box-shadow: 0 2px 8px rgba(108,60,225,0.06);
  }

  .form-control:focus {
    border-color: var(--purple);
    box-shadow: 0 0 0 4px rgba(108,60,225,0.1);
  }

  .form-control::placeholder { color: var(--text-muted); }

  .input-with-icon { position: relative; }
  .input-with-icon .form-control { padding-left: 46px; }
  .input-icon {
    position: absolute; left: 14px; top: 50%;
    transform: translateY(-50%); font-size: 18px;
  }

  .login-meta-row {
    display: flex; justify-content: flex-end;
    margin: 4px 0 18px;
  }

  .login-hint {
    background: var(--purple-pale);
    border: 1px solid var(--purple-light);
    border-radius: var(--radius-sm);
    padding: 10px 12px; margin: 18px 0 0;
    font-size: 11.5px; color: var(--text-mid); line-height: 1.5;
    display: flex; align-items: flex-start; gap: 8px;
  }

  .login-hint svg { flex-shrink: 0; margin-top: 1px; color: var(--purple); }
  .login-hint strong { color: var(--purple); }

  .btn-purple {
    width: 100%; padding: 17px;
    background: linear-gradient(135deg, var(--purple) 0%, var(--purple-dark) 100%);
    border: none; border-radius: var(--radius-pill);
    color: #fff; font-family: var(--font);
    font-size: 16px; font-weight: 700;
    cursor: pointer; box-shadow: var(--shadow-purple);
    transition: all 0.2s;
  }

  .btn-purple:active { transform: scale(0.98); }

  /* =================== APP SHELL =================== */
  #screen-app { background: var(--off-white); flex-direction: column; }

  .app-topbar {
    background: linear-gradient(135deg, #3B0A6E, #6C3CE1);
    padding: 16px 20px;
    display: flex; align-items: center; justify-content: space-between;
    position: sticky; top: 0; z-index: 100;
    min-height: 66px;
    box-shadow: 0 4px 20px rgba(59,10,110,0.25);
  }

  .topbar-left { display: flex; align-items: center; gap: 12px; }

  .topbar-avatar {
    width: 40px; height: 40px; border-radius: 14px;
    background: rgba(255,255,255,0.25);
    border: 2px solid rgba(255,255,255,0.4);
    display: flex; align-items: center; justify-content: center;
    font-size: 16px; font-weight: 700; color: white;
    flex-shrink: 0;
  }

  .topbar-info h3 { font-size: 14px; font-weight: 600; color: #fff; }
  .topbar-info span { font-size: 11px; color: rgba(255,255,255,0.65); }

  .notif-btn {
    width: 40px; height: 40px; border-radius: 12px;
    background: rgba(255,255,255,0.2);
    border: 1px solid rgba(255,255,255,0.3);
    display: flex; align-items: center; justify-content: center;
    cursor: pointer; font-size: 18px; position: relative;
    backdrop-filter: blur(8px);
  }

  .notif-badge {
    position: absolute; top: -5px; right: -5px;
    width: 20px; height: 20px; border-radius: 50%;
    background: var(--accent-pink); color: white;
    font-size: 10px; font-weight: 700;
    display: flex; align-items: center; justify-content: center;
    border: 2px solid var(--off-white);
  }

  /* TABS */
  .tab-content { flex: 1; overflow-y: auto; padding-bottom: 88px; }
  .tab-page { display: none; }
  .tab-page.active { display: block; }

  /* =================== DASHBOARD =================== */
  .dash-hero {
    background: linear-gradient(145deg, #3B0A6E 0%, #6C3CE1 100%);
    padding: 24px 20px 44px;
    position: relative; overflow: hidden;
  }

  .dash-hero-blob {
    position: absolute; width: 200px; height: 200px;
    background: rgba(255,255,255,0.07);
    border-radius: 50%; right: -60px; top: -60px;
  }
  .dash-hero-blob2 {
    position: absolute; width: 120px; height: 120px;
    background: rgba(167,139,250,0.18);
    border-radius: 50%; left: 20px; bottom: -30px;
  }

  .dash-greeting { font-size: 13px; color: rgba(255,255,255,0.65); margin-bottom: 2px; }
  .dash-name { font-size: 22px; font-weight: 700; color: #fff; margin-bottom: 6px; }

  .dept-pill {
    display: inline-flex; align-items: center; gap: 6px;
    background: rgba(255,255,255,0.18);
    border: 1px solid rgba(255,255,255,0.28);
    border-radius: var(--radius-pill);
    padding: 4px 12px; font-size: 11px; color: #fff;
    margin-bottom: 24px; font-weight: 500;
    backdrop-filter: blur(8px);
  }

  /* QUOTA CARDS — float up over hero */
  .quota-row-wrap {
    padding: 0 16px;
    margin-top: -28px;
    position: relative; z-index: 10;
  }

  .quota-row {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .quota-card {
    background: #fff;
    border-radius: var(--radius);
    padding: 14px 14px 12px;
    box-shadow: var(--shadow-card);
    display: flex; align-items: center; gap: 12px;
    border: 1.5px solid #F0EDFB;
  }

  .quota-icon-ring {
    width: 44px; height: 44px; border-radius: 14px;
    display: flex; align-items: center; justify-content: center;
    font-size: 20px; flex-shrink: 0;
  }

  .quota-info .q-label { font-size: 10px; color: var(--text-muted); font-weight: 500; display: block; margin-bottom: 2px; }
  .quota-info .q-val { font-family: var(--mono); font-size: 20px; font-weight: 600; display: block; line-height: 1; }
  .quota-info .q-sub { font-size: 9px; color: var(--text-muted); display: block; margin-top: 2px; }

  .quota-card.sick .quota-icon-ring { background: rgba(239,68,68,0.1); }
  .quota-card.sick .q-val { color: var(--danger); }
  .quota-card.personal .quota-icon-ring { background: rgba(99,102,241,0.1); }
  .quota-card.personal .q-val { color: var(--info); }
  .quota-card.vacation .quota-icon-ring { background: rgba(16,185,129,0.1); }
  .quota-card.vacation .q-val { color: var(--success); }
  .quota-card.special .quota-icon-ring { background: rgba(245,158,11,0.1); }
  .quota-card.special .q-val { color: var(--warning); }

  /* SECTION */
  .section { padding: 20px 16px 0; }

  .section-header {
    display: flex; align-items: center; justify-content: space-between;
    margin-bottom: 14px;
  }

  .section-title {
    font-size: 15px; font-weight: 700; color: var(--text-dark);
    display: flex; align-items: center; gap: 8px;
  }

  .section-link {
    font-size: 12px; color: var(--purple); cursor: pointer; font-weight: 600;
  }

  /* SUMMARY RING */
  .summary-card {
    background: #fff; border-radius: var(--radius);
    box-shadow: var(--shadow-card);
    padding: 18px; border: 1.5px solid #F0EDFB;
    display: flex; align-items: center; gap: 18px;
  }

  .ring-legend { flex: 1; }
  .ring-legend-item {
    display: flex; align-items: center; gap: 8px;
    font-size: 12px; margin-bottom: 8px; color: var(--text-mid);
  }
  .ring-dot { width: 10px; height: 10px; border-radius: 4px; flex-shrink: 0; }
  .ring-legend-item .rl-val { margin-left: auto; font-weight: 700; font-family: var(--mono); font-size: 13px; }

  /* RECENT STATUS */
  .leave-status-list { display: flex; flex-direction: column; gap: 10px; }

  .leave-status-card {
    background: #fff;
    border: 1.5px solid #F0EDFB;
    border-radius: var(--radius);
    padding: 14px 16px;
    display: flex; align-items: center; gap: 14px;
    cursor: pointer;
    box-shadow: var(--shadow-card);
    transition: all 0.2s;
  }

  .leave-status-card:active { transform: scale(0.98); box-shadow: 0 2px 10px rgba(108,60,225,0.12); }

  .lsc-icon {
    width: 46px; height: 46px; border-radius: 14px;
    display: flex; align-items: center; justify-content: center;
    font-size: 20px; flex-shrink: 0;
  }

  .lsc-icon.sick { background: rgba(239,68,68,0.1); }
  .lsc-icon.personal { background: rgba(99,102,241,0.1); }
  .lsc-icon.vacation { background: rgba(16,185,129,0.1); }
  .lsc-icon.special { background: rgba(245,158,11,0.1); }

  .lsc-info { flex: 1; }
  .lsc-info h4 { font-size: 13px; font-weight: 700; color: var(--text-dark); margin-bottom: 3px; }
  .lsc-info p { font-size: 11px; color: var(--text-muted); }

  .lsc-meta { text-align: right; }
  .status-badge {
    font-size: 10px; font-weight: 700;
    padding: 4px 10px; border-radius: var(--radius-pill);
    display: inline-block; margin-bottom: 4px;
  }
  .status-badge.pending { background: rgba(245,158,11,0.12); color: var(--warning); }
  .status-badge.approved { background: rgba(16,185,129,0.12); color: var(--success); }
  .status-badge.rejected { background: rgba(239,68,68,0.12); color: var(--danger); }
  .lsc-meta .date { font-size: 10px; color: var(--text-muted); }

  /* QUICK ACTIONS */
  .quick-actions {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .qa-btn {
    background: #fff;
    border: 1.5px solid #F0EDFB;
    border-radius: var(--radius);
    padding: 16px 14px;
    cursor: pointer; transition: all 0.2s;
    display: flex; flex-direction: column; gap: 10px;
    box-shadow: var(--shadow-card);
  }

  .qa-btn:active { transform: scale(0.97); border-color: var(--purple-light); }

  .qa-icon {
    width: 40px; height: 40px; border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    font-size: 19px;
  }

  .qa-label { font-size: 13px; font-weight: 700; color: var(--text-dark); }
  .qa-sub { font-size: 10px; color: var(--text-muted); margin-top: -7px; }

  /* MINI CHART */
  .chart-card {
    background: #fff; border-radius: var(--radius);
    border: 1.5px solid #F0EDFB; padding: 16px;
    box-shadow: var(--shadow-card);
  }

  .chart-bars {
    display: flex; align-items: flex-end;
    gap: 5px; height: 56px; margin-top: 12px;
  }

  .chart-bar-wrap { flex: 1; display: flex; flex-direction: column; align-items: center; gap: 5px; }
  .chart-bar {
    width: 100%; border-radius: 5px;
    background: var(--purple-pale);
    min-height: 4px; transition: height 0.5s;
  }
  .chart-bar.active { background: linear-gradient(180deg, var(--purple-mid), var(--purple)); }
  .chart-bar-label { font-size: 8px; color: var(--text-muted); }

  /* =================== LEAVE FORM =================== */
  .form-page { padding: 20px 16px; }

  .form-page-title { font-size: 22px; font-weight: 700; color: var(--text-dark); margin-bottom: 4px; }
  .form-page-sub { font-size: 13px; color: var(--text-muted); margin-bottom: 24px; }

  .form-section-title {
    font-size: 11px; font-weight: 700;
    text-transform: uppercase; letter-spacing: 1px;
    color: var(--text-muted); margin: 20px 0 10px;
  }

  .leave-type-selector { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 20px; }

  .leave-type-btn {
    padding: 14px 10px;
    background: #fff;
    border: 2px solid #F0EDFB;
    border-radius: var(--radius);
    cursor: pointer; text-align: center;
    transition: all 0.2s;
    box-shadow: var(--shadow-card);
  }

  .leave-type-btn .lt-icon { font-size: 26px; display: block; margin-bottom: 6px; }
  .leave-type-btn .lt-name { font-size: 12px; font-weight: 700; display: block; color: var(--text-dark); }
  .leave-type-btn .lt-days { font-size: 10px; color: var(--text-muted); margin-top: 2px; display: block; }

  .leave-type-btn.selected { border-color: var(--purple); background: var(--purple-pale); }
  .leave-type-btn.selected.sick { border-color: var(--danger); background: rgba(239,68,68,0.06); }
  .leave-type-btn.selected.personal { border-color: var(--info); background: rgba(99,102,241,0.06); }
  .leave-type-btn.selected.vacation { border-color: var(--success); background: rgba(16,185,129,0.06); }
  .leave-type-btn.selected.special { border-color: var(--warning); background: rgba(245,158,11,0.06); }

  .duration-selector { display: flex; gap: 8px; margin-bottom: 16px; }

  .dur-btn {
    flex: 1; padding: 10px 8px;
    background: #fff;
    border: 1.5px solid #E5E0F5;
    border-radius: var(--radius-pill);
    color: var(--text-mid); font-family: var(--font);
    font-size: 12px; font-weight: 600;
    cursor: pointer; text-align: center; transition: all 0.2s;
  }

  .dur-btn.selected {
    background: var(--purple);
    border-color: var(--purple);
    color: #fff;
    box-shadow: 0 4px 14px rgba(108,60,225,0.3);
  }

  .form-row { display: flex; gap: 10px; }
  .form-row .form-group { flex: 1; }

  .date-display {
    background: #fff;
    border: 1.5px solid #E5E0F5;
    border-radius: var(--radius-sm);
    padding: 12px 14px;
    display: flex; align-items: center; gap: 10px;
    cursor: pointer; box-shadow: 0 2px 8px rgba(108,60,225,0.06);
  }

  .date-display .cal-icon { font-size: 20px; }
  .date-display .cal-label { font-size: 10px; color: var(--text-muted); }
  .date-display .cal-value { font-size: 13px; font-weight: 700; color: var(--text-dark); }

  textarea.form-control { resize: none; min-height: 90px; line-height: 1.6; }

  .upload-area {
    border: 2px dashed #D1C9F0;
    border-radius: var(--radius);
    padding: 24px 16px;
    text-align: center; cursor: pointer; transition: all 0.2s;
    margin-bottom: 16px; background: #faf8ff;
  }

  .upload-area:hover { border-color: var(--purple); background: var(--purple-pale); }
  .upload-icon { font-size: 32px; margin-bottom: 8px; display: block; }
  .upload-text { font-size: 13px; color: var(--text-mid); font-weight: 500; }
  .upload-sub { font-size: 11px; color: var(--text-muted); margin-top: 4px; }

  .upload-preview {
    display: none; align-items: center; gap: 10px;
    background: var(--purple-pale);
    border: 1.5px solid var(--purple-light);
    border-radius: var(--radius-sm);
    padding: 12px 14px; margin-bottom: 16px;
  }

  .upload-preview.show { display: flex; }
  .preview-icon { font-size: 24px; }
  .preview-info { flex: 1; }
  .preview-name { font-size: 13px; font-weight: 700; color: var(--text-dark); }
  .preview-size { font-size: 11px; color: var(--text-muted); }
  .preview-del { font-size: 18px; cursor: pointer; color: var(--danger); }

  /* =================== APPROVALS =================== */
  .approval-banner {
    background: linear-gradient(135deg, rgba(245,158,11,0.1), rgba(239,68,68,0.06));
    border: 1.5px solid rgba(245,158,11,0.25);
    border-radius: var(--radius);
    padding: 16px 18px;
    margin: 16px 16px 0;
    display: flex; align-items: center; gap: 12px;
  }

  .approval-banner-icon { font-size: 28px; }
  .approval-banner-info h4 { font-size: 14px; font-weight: 700; color: var(--warning); }
  .approval-banner-info p { font-size: 12px; color: var(--text-muted); margin-top: 2px; }

  .approval-card {
    background: #fff;
    border: 1.5px solid #F0EDFB;
    border-radius: var(--radius);
    padding: 16px; margin-bottom: 12px;
    box-shadow: var(--shadow-card);
    position: relative; overflow: hidden;
  }

  .approval-card::before {
    content: ''; position: absolute; left: 0; top: 0; bottom: 0;
    width: 4px; border-radius: 4px 0 0 4px;
  }

  .approval-card.sick::before { background: var(--danger); }
  .approval-card.personal::before { background: var(--info); }
  .approval-card.vacation::before { background: var(--success); }
  .approval-card.special::before { background: var(--warning); }

  .appr-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 12px; }
  .appr-requester { display: flex; align-items: center; gap: 10px; }

  .appr-avatar {
    width: 38px; height: 38px; border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    font-size: 14px; font-weight: 700; color: white;
    background: linear-gradient(135deg, var(--purple), var(--purple-dark));
  }

  .appr-name { font-size: 13px; font-weight: 700; color: var(--text-dark); }
  .appr-dept { font-size: 11px; color: var(--text-muted); }

  .appr-type-badge {
    font-size: 11px; font-weight: 700;
    padding: 4px 10px; border-radius: var(--radius-pill);
  }

  .appr-type-badge.sick { background: rgba(239,68,68,0.1); color: var(--danger); }
  .appr-type-badge.personal { background: rgba(99,102,241,0.1); color: var(--info); }
  .appr-type-badge.vacation { background: rgba(16,185,129,0.1); color: var(--success); }
  .appr-type-badge.special { background: rgba(245,158,11,0.1); color: var(--warning); }

  .appr-details { margin-bottom: 12px; }
  .appr-detail-row {
    display: flex; justify-content: space-between;
    font-size: 12px; padding: 5px 0;
    border-bottom: 1px solid #F5F3FF;
  }
  .appr-detail-row .d-key { color: var(--text-muted); }
  .appr-detail-row .d-val { font-weight: 600; color: var(--text-dark); }

  .appr-reason {
    background: #FAF8FF; border-radius: var(--radius-sm);
    padding: 10px 12px; font-size: 12px;
    color: var(--text-mid); margin-bottom: 14px; line-height: 1.5;
    border: 1px solid #EDE9FE;
  }

  .appr-actions { display: flex; gap: 10px; }

  .btn-reject {
    flex: 1; padding: 12px;
    background: rgba(239,68,68,0.08);
    border: 1.5px solid rgba(239,68,68,0.25);
    border-radius: var(--radius-pill);
    color: var(--danger); font-family: var(--font);
    font-size: 13px; font-weight: 700; cursor: pointer;
    transition: all 0.2s;
  }

  .btn-reject:active { background: rgba(239,68,68,0.15); }

  .btn-approve {
    flex: 2; padding: 12px;
    background: linear-gradient(135deg, var(--success), #059669);
    border: none; border-radius: var(--radius-pill);
    color: white; font-family: var(--font);
    font-size: 13px; font-weight: 700; cursor: pointer;
    box-shadow: 0 4px 14px rgba(16,185,129,0.3);
    transition: all 0.2s;
  }

  .btn-approve:active { transform: scale(0.98); }

  /* =================== HISTORY =================== */
  .history-filter {
    display: flex; gap: 8px; padding: 16px 16px 0;
    overflow-x: auto; scrollbar-width: none;
  }

  .history-filter::-webkit-scrollbar { display: none; }

  .filter-chip {
    padding: 7px 14px;
    background: #fff;
    border: 1.5px solid #E5E0F5;
    border-radius: var(--radius-pill); white-space: nowrap;
    font-size: 12px; font-weight: 600;
    cursor: pointer; transition: all 0.2s; color: var(--text-mid);
    box-shadow: 0 2px 8px rgba(108,60,225,0.06);
  }

  .filter-chip.active {
    background: var(--purple); border-color: var(--purple);
    color: #fff; box-shadow: 0 4px 14px rgba(108,60,225,0.3);
  }

  /* =================== PROFILE =================== */
  .profile-hero {
    background: linear-gradient(145deg, #3B0A6E, #6C3CE1);
    padding: 32px 20px 28px;
    text-align: center; position: relative; overflow: hidden;
  }

  .profile-hero-blob {
    position: absolute; width: 180px; height: 180px;
    background: rgba(255,255,255,0.07);
    border-radius: 50%; right: -50px; top: -50px;
  }

  .profile-avatar {
    width: 80px; height: 80px; border-radius: 24px;
    background: rgba(255,255,255,0.22);
    border: 2.5px solid rgba(255,255,255,0.4);
    display: flex; align-items: center; justify-content: center;
    font-size: 32px; font-weight: 700; color: white;
    margin: 0 auto 14px;
    box-shadow: 0 8px 30px rgba(59,10,110,0.3);
    backdrop-filter: blur(8px);
  }

  .profile-name { font-size: 20px; font-weight: 700; color: #fff; }
  .profile-id { font-family: var(--mono); font-size: 11px; color: rgba(255,255,255,0.55); margin-top: 4px; }

  .profile-role {
    display: inline-block; margin-top: 10px;
    background: rgba(255,255,255,0.18);
    border: 1px solid rgba(255,255,255,0.3);
    border-radius: var(--radius-pill); padding: 5px 14px;
    font-size: 12px; color: #fff; font-weight: 600;
    backdrop-filter: blur(8px);
  }

  .profile-stats {
    display: grid; grid-template-columns: repeat(3, 1fr);
    gap: 1px; background: #F0EDFB;
    margin: 16px 16px 0; border-radius: var(--radius);
    overflow: hidden; box-shadow: var(--shadow-card);
  }

  .pstat {
    background: #fff; padding: 16px 10px; text-align: center;
  }

  .pstat .ps-val {
    font-family: var(--mono); font-size: 22px; font-weight: 700;
    color: var(--purple); display: block;
  }

  .pstat .ps-lbl { font-size: 10px; color: var(--text-muted); margin-top: 4px; display: block; }

  /* PROGRESS BARS */
  .leave-quota-card {
    background: #fff; border: 1.5px solid #F0EDFB;
    border-radius: var(--radius); padding: 16px;
    box-shadow: var(--shadow-card);
  }

  .lq-row { margin-bottom: 14px; }
  .lq-row:last-child { margin-bottom: 0; }
  .lq-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px; }
  .lq-label { font-size: 13px; color: var(--text-dark); display: flex; align-items: center; gap: 6px; }
  .lq-val { font-family: var(--mono); font-size: 12px; font-weight: 700; }
  .lq-bar-bg { height: 7px; background: #F0EDFB; border-radius: 10px; }
  .lq-bar { height: 100%; border-radius: 10px; transition: width 0.5s; }

  .profile-menu { padding: 0 16px 20px; }

  .menu-item {
    display: flex; align-items: center; gap: 14px;
    padding: 15px 16px;
    background: #fff; border: 1.5px solid #F0EDFB;
    border-radius: var(--radius-sm); margin-bottom: 8px;
    cursor: pointer; transition: all 0.2s;
    box-shadow: var(--shadow-card);
  }

  .menu-item:active { border-color: var(--purple-light); }

  .mi-icon {
    width: 38px; height: 38px; border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    font-size: 16px;
  }

  .mi-text { flex: 1; }
  .mi-text h4 { font-size: 14px; font-weight: 600; color: var(--text-dark); }
  .mi-text span { font-size: 11px; color: var(--text-muted); }
  .mi-arrow { color: var(--purple-light); font-size: 16px; font-weight: 700; }

  .btn-logout {
    width: 100%; padding: 15px;
    background: rgba(239,68,68,0.07);
    border: 1.5px solid rgba(239,68,68,0.2);
    border-radius: var(--radius-pill);
    color: var(--danger); font-family: var(--font);
    font-size: 14px; font-weight: 700; cursor: pointer;
    transition: all 0.2s; margin-top: 8px;
  }

  /* =================== BOTTOM NAV =================== */
  .bottom-nav {
    position: fixed; bottom: 0; left: 50%; transform: translateX(-50%);
    width: 100%; max-width: 430px;
    background: #fff;
    border-top: 1.5px solid #EDE9FE;
    display: flex; padding: 10px 0 22px;
    z-index: 200;
    box-shadow: 0 -4px 20px rgba(108,60,225,0.1);
  }

  .nav-item {
    flex: 1; display: flex; flex-direction: column;
    align-items: center; gap: 4px;
    cursor: pointer; padding: 4px 0;
    transition: all 0.2s; position: relative;
  }

  .nav-icon { font-size: 22px; transition: transform 0.2s; }
  .nav-label { font-size: 10px; color: var(--text-muted); font-weight: 600; }

  .nav-item.active .nav-label { color: var(--purple); }
  .nav-item.active .nav-icon { transform: translateY(-2px); }

  .nav-indicator {
    position: absolute; top: -1px; left: 50%; transform: translateX(-50%);
    width: 24px; height: 3px; border-radius: 0 0 4px 4px;
    background: var(--purple); opacity: 0; transition: opacity 0.2s;
  }

  .nav-item.active .nav-indicator { opacity: 1; }

  .nav-center-wrap { flex: 1; display: flex; justify-content: center; align-items: flex-start; }

  .nav-center-btn {
    width: 54px; height: 54px; border-radius: 18px;
    background: linear-gradient(135deg, var(--purple-mid), var(--purple-dark));
    display: flex; align-items: center; justify-content: center;
    font-size: 24px; margin-top: -18px;
    box-shadow: 0 6px 20px rgba(108,60,225,0.45);
    cursor: pointer; transition: transform 0.2s;
  }

  .nav-center-btn:active { transform: scale(0.93); }

  /* =================== MODALS =================== */
  .modal-overlay {
    display: none; position: fixed; inset: 0;
    background: rgba(30,10,60,0.5);
    backdrop-filter: blur(6px);
    z-index: 500; align-items: flex-end;
  }

  .modal-overlay.open { display: flex; }

  .modal-sheet {
    width: 100%; max-width: 430px; margin: 0 auto;
    background: var(--off-white);
    border-radius: 28px 28px 0 0;
    max-height: 90vh; overflow-y: auto;
    animation: slideUp 0.3s ease;
  }

  @keyframes slideUp {
    from { transform: translateY(100%); }
    to { transform: translateY(0); }
  }

  .modal-handle {
    width: 40px; height: 4px; border-radius: 2px;
    background: #D1C9F0; margin: 12px auto 8px;
  }

  .modal-header {
    padding: 0 20px 16px;
    border-bottom: 1px solid #F0EDFB;
    display: flex; align-items: center; justify-content: space-between;
  }

  .modal-title { font-size: 17px; font-weight: 700; color: var(--text-dark); }

  .modal-close {
    width: 32px; height: 32px; border-radius: 50%;
    background: #F0EDFB;
    display: flex; align-items: center; justify-content: center;
    cursor: pointer; font-size: 16px; color: var(--text-mid);
  }

  .modal-body { padding: 20px; }

  /* NOTIFICATION */
  .notif-item {
    display: flex; gap: 12px; padding: 14px 0;
    border-bottom: 1px solid #F0EDFB;
  }

  .notif-dot {
    width: 9px; height: 9px; border-radius: 50%;
    background: var(--purple); margin-top: 5px; flex-shrink: 0;
  }

  .notif-dot.read { background: #D1C9F0; }

  .notif-content .nc-title { font-size: 13px; font-weight: 700; color: var(--text-dark); margin-bottom: 3px; }
  .notif-content .nc-body { font-size: 12px; color: var(--text-mid); line-height: 1.4; }
  .notif-content .nc-time { font-size: 10px; color: var(--text-muted); margin-top: 4px; font-family: var(--mono); }

  /* CALENDAR */
  .cal-widget {
    background: #fff; border: 1.5px solid #F0EDFB;
    border-radius: var(--radius); padding: 16px;
    margin: 0 16px 16px; box-shadow: var(--shadow-card);
  }

  .cal-month-header {
    display: flex; align-items: center; justify-content: space-between;
    margin-bottom: 12px;
  }

  .cal-month-nav {
    width: 32px; height: 32px; border-radius: 10px;
    background: var(--purple-pale); border: none;
    color: var(--purple); font-size: 16px; cursor: pointer;
    display: flex; align-items: center; justify-content: center;
    font-weight: 700;
  }

  .cal-month-title { font-size: 14px; font-weight: 700; color: var(--text-dark); }
  .cal-grid { display: grid; grid-template-columns: repeat(7, 1fr); gap: 2px; }
  .cal-day-header { text-align: center; font-size: 10px; font-weight: 700; color: var(--text-muted); padding: 4px 0; }

  .cal-day {
    aspect-ratio: 1; display: flex; align-items: center;
    justify-content: center; font-size: 12px; border-radius: 10px;
    cursor: pointer;
  }

  .cal-day:hover { background: var(--purple-pale); }
  .cal-day.today { background: var(--purple); color: #fff; font-weight: 700; }
  .cal-day.has-leave { background: rgba(245,158,11,0.15); color: var(--warning); font-weight: 700; }
  .cal-day.has-holiday { background: rgba(239,68,68,0.12); color: var(--danger); font-weight: 700; }
  .cal-day.has-holiday.today { background: var(--purple); color: #fff; box-shadow: inset 0 0 0 2px var(--danger); }
  .cal-day.other-month { opacity: 0.3; }

  .cal-legend {
    display: flex; gap: 14px; flex-wrap: wrap;
    margin-top: 14px; padding-top: 12px;
    border-top: 1px solid #F0EDFB;
  }
  .cal-legend-item {
    display: flex; align-items: center; gap: 6px;
    font-size: 11px; color: var(--text-mid);
  }
  .cal-legend-dot {
    width: 10px; height: 10px; border-radius: 4px; flex-shrink: 0;
  }
  .cal-legend-dot.leave { background: rgba(245,158,11,0.4); }
  .cal-legend-dot.holiday { background: rgba(239,68,68,0.35); }
  .cal-legend-dot.today { background: var(--purple); }

  /* TOAST */
  .toast {
    position: fixed; top: 76px; left: 50%; transform: translateX(-50%);
    background: var(--text-dark); border-radius: var(--radius-pill);
    padding: 12px 20px;
    display: flex; align-items: center; gap: 10px;
    font-size: 13px; font-weight: 600; color: #fff;
    z-index: 1000; opacity: 0; transition: opacity 0.3s;
    min-width: 220px; max-width: 340px;
    box-shadow: 0 8px 30px rgba(0,0,0,0.2);
  }

  .toast.show { opacity: 1; }
  .toast.success { background: var(--success); }
  .toast.error { background: var(--danger); }
  .toast.warning { background: var(--warning); }

  /* LOADING */
  .loading-overlay {
    display: none; position: fixed; inset: 0;
    background: rgba(30,10,60,0.4);
    backdrop-filter: blur(8px);
    z-index: 900; align-items: center; justify-content: center;
  }
  .loading-overlay.show { display: flex; }

  .spinner-wrap {
    background: #fff; border-radius: 24px;
    width: 80px; height: 80px;
    display: flex; align-items: center; justify-content: center;
    box-shadow: var(--shadow-purple);
  }

  .spinner {
    width: 36px; height: 36px;
    border: 3px solid var(--purple-pale);
    border-top-color: var(--purple);
    border-radius: 50%; animation: spin 0.8s linear infinite;
  }

  @keyframes spin { to { transform: rotate(360deg); } }


  /* =================== SVG ICON SYSTEM =================== */
  svg.icon, [class*="-icon"] svg, .nav-icon svg,
  .splash-icon-wrap svg, .qa-icon svg, .lsc-icon svg,
  .quota-icon-ring svg, .mi-icon svg, .upload-icon svg,
  .notif-btn svg, .modal-close svg, .appr-avatar svg,
  .topbar-avatar svg, .profile-avatar svg, .login-logo-sm svg {
    display: inline-block;
    vertical-align: -0.15em;
  }

  /* Splash hero icon — big centered */
  .splash-icon-wrap svg { width: 52px; height: 52px; stroke-width: 1.5; }
  .login-logo-sm svg { width: 28px; height: 28px; stroke-width: 1.8; }
  .topbar-avatar svg, .profile-avatar svg { width: 20px; height: 20px; stroke-width: 2; }

  /* Quota & leave type icons */
  .quota-icon-ring svg { width: 22px; height: 22px; stroke-width: 2; }
  .lsc-icon svg { width: 22px; height: 22px; stroke-width: 2; }
  .leave-type-btn .lt-icon svg { width: 28px; height: 28px; stroke-width: 1.8; }
  .lt-icon svg { width: 28px; height: 28px; stroke-width: 1.8; }

  /* Quick action buttons */
  .qa-icon svg { width: 22px; height: 22px; stroke-width: 2; }

  /* Bottom nav */
  .nav-icon svg { width: 24px; height: 24px; stroke-width: 2; }
  .nav-center-btn svg { width: 26px; height: 26px; stroke-width: 2.2; color: white; }

  /* Notification bell */
  .notif-btn svg { width: 20px; height: 20px; stroke-width: 2; color: white; }

  /* Profile menu */
  .mi-icon svg { width: 18px; height: 18px; stroke-width: 2; }

  /* Section titles */
  .section-title svg { width: 16px; height: 16px; stroke-width: 2; vertical-align: -0.15em; }

  /* Upload area */
  .upload-icon svg { width: 36px; height: 36px; stroke-width: 1.5; color: var(--purple-mid); }

  /* Approval cards */
  .appr-type-badge svg { width: 13px; height: 13px; stroke-width: 2.2; }

  /* Buttons with icons */
  .btn-white svg, .btn-purple svg, .btn-reject svg, .btn-approve svg, .btn-logout svg {
    width: 16px; height: 16px; stroke-width: 2.2; vertical-align: -0.2em;
  }

  /* Status badges */
  .status-badge svg { width: 12px; height: 12px; stroke-width: 2.5; vertical-align: -0.1em; }

  /* Toast */
  .toast svg { width: 16px; height: 16px; stroke-width: 2.2; vertical-align: -0.2em; }

  /* Notification items */
  .nc-title svg { width: 14px; height: 14px; stroke-width: 2; }

  /* Modal */
  .modal-close svg { width: 16px; height: 16px; stroke-width: 2.5; }

  /* Splash pills */
  .splash-pill svg { width: 13px; height: 13px; stroke-width: 2.2; }

  /* Approval requester avatar */
  .appr-avatar svg { width: 16px; height: 16px; stroke-width: 2; }

  /* Dept pill */
  .dept-pill svg { width: 13px; height: 13px; stroke-width: 2; }

  /* Profile id block */
  .profile-role svg { width: 13px; height: 13px; stroke-width: 2; }

  /* Generic inline context */
  p svg, span svg, div svg { vertical-align: -0.15em; }

  /* Greeting text icons */
  .dash-greeting svg { width: 16px; height: 16px; stroke-width: 2; }

  /* Hint block */
  .login-hint svg { width: 14px; height: 14px; stroke-width: 2; }

  select.form-control {
    appearance: none;
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%239B89C4' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E");
    background-repeat: no-repeat;
    background-position: right 14px center;
    padding-right: 38px;
  }

  .appr-detail-row .d-val.good { color: var(--success); }
  .appr-detail-row .d-val.none { color: var(--text-muted); }

  /* Icon container overrides for SVG-replaced emoji */
  .r-icon svg { width: 28px; height: 28px; stroke-width: 1.8; display: block; margin: 0 auto 8px; }
  .r-icon { font-size: 1px; /* collapse old font-size */ display: flex; justify-content: center; }
  .lt-icon svg { width: 30px; height: 30px; stroke-width: 1.8; display: block; margin: 0 auto 6px; }
  .lt-icon { font-size: 1px; display: flex; justify-content: center; }
  .upload-icon svg { width: 38px; height: 38px; stroke-width: 1.5; display: block; margin: 0 auto 8px; color: var(--purple-mid); }
  .upload-icon { font-size: 1px; display: flex; justify-content: center; }
  .preview-icon svg { width: 26px; height: 26px; stroke-width: 1.8; }
  .approval-banner-icon svg { width: 30px; height: 30px; stroke-width: 1.8; color: var(--warning); }
  .approval-banner-icon { font-size: 1px; }
  .appr-avatar svg { width: 17px; height: 17px; stroke-width: 2; color: white; }
  .appr-type-badge svg { width: 13px; height: 13px; stroke-width: 2; }

  /* Fix dash-greeting and similar inline text icons */
  .dash-greeting svg { width: 15px; height: 15px; stroke-width: 2; color: rgba(255,255,255,0.8); }
  .dash-name svg { width: 18px; height: 18px; }

  /* Section title icons */
  .section-title svg { width: 17px; height: 17px; stroke-width: 2; color: var(--purple); }

  /* Nav items */
  .nav-item .nav-icon { font-size: 1px; line-height: 0; }
  .nav-item .nav-icon svg { width: 24px; height: 24px; stroke-width: 2; display: block; color: var(--text-muted); }
  .nav-item.active .nav-icon svg { color: var(--purple); }
  .nav-center-btn svg { width: 28px; height: 28px; stroke-width: 2.2; color: white; }

  /* Topbar & profile avatars — just initial letters, no emoji replacement needed, but nav bell: */
  .notif-btn { font-size: 1px; }
  .notif-btn svg { width: 22px; height: 22px; stroke-width: 2; color: white; display: block; }

  /* Modal close */
  .modal-close { font-size: 1px; }
  .modal-close svg { width: 16px; height: 16px; stroke-width: 2.5; color: var(--text-mid); }

  /* Dept pill */
  .dept-pill svg { width: 14px; height: 14px; stroke-width: 2; }

  /* Splash pill */
  .splash-pill svg { width: 14px; height: 14px; stroke-width: 2.2; }

  /* Login logo */
  .login-logo-sm { font-size: 1px; display: flex; align-items: center; justify-content: center; }
  .login-logo-sm svg { width: 30px; height: 30px; stroke-width: 1.8; color: white; }

  /* Splash icon wrap */
  .splash-icon-wrap { font-size: 1px; }
  .splash-icon-wrap svg { width: 56px; height: 56px; stroke-width: 1.5; color: white; }

  /* Profile menu icons */
  .mi-icon { font-size: 1px; display: flex; align-items: center; justify-content: center; }
  .mi-icon svg { width: 18px; height: 18px; stroke-width: 2; }

  /* Quick action icon */
  .qa-icon { font-size: 1px; display: flex; align-items: center; justify-content: center; }
  .qa-icon svg { width: 22px; height: 22px; stroke-width: 2; }

  /* Leave status card icon */
  .lsc-icon { font-size: 1px; display: flex; align-items: center; justify-content: center; }
  .lsc-icon svg { width: 22px; height: 22px; stroke-width: 2; }
  .lsc-icon.sick svg { color: var(--danger); }
  .lsc-icon.personal svg { color: var(--info); }
  .lsc-icon.vacation svg { color: var(--success); }
  .lsc-icon.special svg { color: var(--warning); }

  /* Quota ring icons */
  .quota-icon-ring { font-size: 1px; display: flex; align-items: center; justify-content: center; }
  .quota-icon-ring svg { width: 22px; height: 22px; stroke-width: 2; }
  .quota-card.sick .quota-icon-ring svg { color: var(--danger); }
  .quota-card.personal .quota-icon-ring svg { color: var(--info); }
  .quota-card.vacation .quota-icon-ring svg { color: var(--success); }
  .quota-card.special .quota-icon-ring svg { color: var(--warning); }

  /* Button SVG icons */
  .btn-reject svg, .btn-approve svg { width: 14px; height: 14px; stroke-width: 2.5; vertical-align: -0.15em; }
  .btn-logout svg { width: 16px; height: 16px; stroke-width: 2; vertical-align: -0.2em; }
  .btn-white svg { width: 16px; height: 16px; stroke-width: 2; vertical-align: -0.2em; color: var(--purple); }
  .btn-purple svg { width: 16px; height: 16px; stroke-width: 2; vertical-align: -0.2em; }

  /* Notif badge needs repositioning when icon is svg */
  .notif-btn { display: flex; align-items: center; justify-content: center; }

  /* Input icons */
  .input-icon { font-size: 1px; }
  .input-icon svg { width: 18px; height: 18px; stroke-width: 2; color: var(--text-muted); display: block; }

  /* lq-label icons */
  .lq-label svg { width: 14px; height: 14px; stroke-width: 2; vertical-align: -0.15em; }

  /* toast icon */
  #toast-icon svg { width: 16px; height: 16px; stroke-width: 2.2; vertical-align: -0.2em; }

  /* Notif modal */
  .nc-title svg { width: 14px; height: 14px; stroke-width: 2; vertical-align: -0.15em; }

  /* Upload hint */
  .upload-text svg, .upload-sub svg { width: 14px; height: 14px; stroke-width: 2; }

  /* appr detail rows */
  .d-key svg { width: 13px; height: 13px; stroke-width: 2; vertical-align: -0.15em; }
  .d-val svg { width: 13px; height: 13px; stroke-width: 2; vertical-align: -0.15em; }

  /* ring legend */
  .ring-legend-item svg { width: 13px; height: 13px; stroke-width: 2; vertical-align: -0.15em; }

  /* Status badges */
  .status-badge svg { width: 11px; height: 11px; stroke-width: 2.5; vertical-align: -0.1em; }

  /* =================== HOLIDAYS MODAL =================== */
  .holiday-month-group { margin-bottom: 20px; }
  .holiday-month-label {
    font-size: 11px; font-weight: 700; text-transform: uppercase;
    letter-spacing: 1px; color: var(--text-muted);
    margin-bottom: 8px; padding: 0 4px;
  }
  .holiday-item {
    display: flex; align-items: center; gap: 12px;
    padding: 11px 14px;
    background: #fff; border: 1.5px solid #F0EDFB;
    border-radius: var(--radius-sm); margin-bottom: 8px;
    box-shadow: 0 2px 8px rgba(108,60,225,0.05);
  }
  .holiday-date-box {
    width: 44px; height: 44px; border-radius: 12px;
    background: var(--purple-pale);
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    flex-shrink: 0;
  }
  .holiday-date-box .hd-day {
    font-family: var(--mono); font-size: 16px; font-weight: 700;
    color: var(--purple); line-height: 1;
  }
  .holiday-date-box .hd-mon {
    font-size: 9px; color: var(--text-muted); font-weight: 600;
    margin-top: 1px;
  }
  .holiday-info { flex: 1; }
  .holiday-info .hi-desc {
    font-size: 12px; font-weight: 600; color: var(--text-dark);
    line-height: 1.4;
  }
  .holiday-info .hi-dow {
    font-size: 10px; color: var(--text-muted); margin-top: 2px;
  }
  .holiday-dot {
    width: 8px; height: 8px; border-radius: 50%;
    background: var(--purple-light); flex-shrink: 0;
  }
  .holiday-count-badge {
    background: var(--purple); color: #fff;
    font-size: 11px; font-weight: 700;
    padding: 3px 10px; border-radius: var(--radius-pill);
    font-family: var(--mono);
  }

  /* =================== CUSTOM DATE PICKER =================== */
  .datepicker-overlay {
    display: none; position: fixed; inset: 0;
    background: rgba(30,10,60,0.55);
    backdrop-filter: blur(10px);
    z-index: 600; align-items: flex-end; justify-content: center;
  }
  .datepicker-overlay.open { display: flex; }

  .datepicker-sheet {
    width: 100%; max-width: 430px;
    background: var(--off-white);
    border-radius: 32px 32px 0 0;
    overflow: hidden;
    animation: slideUp 0.35s cubic-bezier(.32,1.2,.5,1);
    box-shadow: 0 -8px 40px rgba(59,10,110,0.22);
  }

  .dp-header {
    background: linear-gradient(135deg, #3B0A6E 0%, #6C3CE1 100%);
    padding: 20px 20px 24px;
    position: relative; overflow: hidden;
  }

  .dp-header::before {
    content: '';
    position: absolute; inset: 0;
    background-image: radial-gradient(rgba(255,255,255,0.08) 1.5px, transparent 1.5px);
    background-size: 18px 18px;
  }

  .dp-header-blob {
    position: absolute; width: 160px; height: 160px;
    background: rgba(167,139,250,0.2);
    border-radius: 50%; right: -50px; top: -60px;
    filter: blur(4px); pointer-events: none;
  }

  .dp-handle {
    width: 36px; height: 4px; border-radius: 2px;
    background: rgba(255,255,255,0.3);
    margin: 0 auto 16px; position: relative; z-index: 1;
  }

  .dp-header-top {
    display: flex; align-items: center; justify-content: space-between;
    position: relative; z-index: 1; margin-bottom: 4px;
  }

  .dp-header-label {
    font-size: 11px; font-weight: 700; letter-spacing: 1.5px;
    text-transform: uppercase; color: rgba(255,255,255,0.6);
    font-family: var(--mono);
  }

  .dp-close-btn {
    width: 30px; height: 30px; border-radius: 50%;
    background: rgba(255,255,255,0.18);
    border: 1px solid rgba(255,255,255,0.25);
    display: flex; align-items: center; justify-content: center;
    cursor: pointer; color: white; backdrop-filter: blur(4px);
  }

  .dp-close-btn svg { width: 14px; height: 14px; stroke-width: 2.5; }

  .dp-selected-display {
    position: relative; z-index: 1;
  }

  .dp-selected-day {
    font-size: 42px; font-weight: 700; color: white;
    line-height: 1; font-family: var(--mono);
    display: flex; align-items: baseline; gap: 8px;
  }

  .dp-selected-day .dp-day-num { font-size: 52px; }

  .dp-selected-month-row {
    display: flex; align-items: center; gap: 8px; margin-top: 4px;
  }

  .dp-selected-month-th {
    font-size: 18px; font-weight: 600; color: rgba(255,255,255,0.95);
  }

  .dp-selected-month-en {
    font-size: 12px; font-weight: 500; color: rgba(255,255,255,0.55);
    font-family: var(--mono); letter-spacing: 0.5px;
    background: rgba(255,255,255,0.12);
    padding: 2px 8px; border-radius: 20px;
    border: 1px solid rgba(255,255,255,0.18);
  }

  .dp-selected-year {
    font-size: 13px; color: rgba(255,255,255,0.6);
    font-family: var(--mono); margin-top: 2px;
  }

  .dp-body {
    padding: 16px 16px 4px;
  }

  .dp-month-nav {
    display: flex; align-items: center; justify-content: space-between;
    margin-bottom: 14px; padding: 0 2px;
  }

  .dp-nav-btn {
    width: 38px; height: 38px; border-radius: 12px;
    background: white; border: 1.5px solid #EDE9FE;
    color: var(--purple); font-size: 18px;
    display: flex; align-items: center; justify-content: center;
    cursor: pointer; transition: all 0.15s; font-weight: 700;
    box-shadow: 0 2px 8px rgba(108,60,225,0.1);
  }

  .dp-nav-btn svg { width: 18px; height: 18px; stroke-width: 2.5; }
  .dp-nav-btn:active { background: var(--purple-pale); transform: scale(0.94); }

  .dp-month-title {
    text-align: center;
  }

  .dp-month-th {
    font-size: 16px; font-weight: 700; color: var(--text-dark); display: block; line-height: 1.2;
  }

  .dp-month-en {
    font-size: 11px; color: var(--text-muted);
    font-family: var(--mono); letter-spacing: 0.5px;
  }

  .dp-weekdays {
    display: grid; grid-template-columns: repeat(7, 1fr);
    margin-bottom: 6px;
  }

  .dp-weekday {
    text-align: center; padding: 6px 0;
    font-size: 10px; font-weight: 700;
    color: var(--text-muted);
  }

  .dp-weekday.weekend { color: var(--danger); opacity: 0.7; }

  .dp-grid {
    display: grid; grid-template-columns: repeat(7, 1fr);
    gap: 3px;
  }

  .dp-cell {
    aspect-ratio: 1; display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    border-radius: 12px; cursor: pointer;
    transition: all 0.15s; position: relative;
    border: 1.5px solid transparent;
  }

  .dp-cell:hover:not(.dp-other):not(.dp-disabled) {
    background: var(--purple-pale);
    border-color: var(--purple-light);
  }

  .dp-cell:active:not(.dp-other):not(.dp-disabled) { transform: scale(0.88); }

  .dp-cell .dp-num {
    font-size: 13px; font-weight: 600; color: var(--text-dark);
    line-height: 1;
  }

  .dp-cell .dp-dot-row {
    display: flex; gap: 2px; margin-top: 3px; min-height: 5px;
  }

  .dp-dot {
    width: 4px; height: 4px; border-radius: 50%;
  }

  .dp-cell.dp-today {
    background: var(--purple-pale);
    border-color: var(--purple-light);
  }

  .dp-cell.dp-today .dp-num { color: var(--purple); font-weight: 700; }

  .dp-cell.dp-selected {
    background: linear-gradient(135deg, var(--purple-mid), var(--purple-dark)) !important;
    border-color: transparent !important;
    box-shadow: 0 4px 16px rgba(108,60,225,0.45);
  }

  .dp-cell.dp-selected .dp-num { color: white; font-weight: 700; }

  .dp-cell.dp-holiday {
    background: rgba(239,68,68,0.07);
    border-color: rgba(239,68,68,0.18);
  }

  .dp-cell.dp-holiday .dp-num { color: var(--danger); }

  .dp-cell.dp-other { opacity: 0; pointer-events: none; }

  .dp-cell.dp-disabled { opacity: 0.3; pointer-events: none; }

  .dp-cell.dp-weekend .dp-num { color: var(--danger); }

  .dp-cell.dp-range-start {
    background: linear-gradient(135deg, var(--purple-mid), var(--purple-dark)) !important;
    border-radius: 12px 0 0 12px;
  }

  .dp-cell.dp-range-end {
    background: linear-gradient(135deg, var(--purple-mid), var(--purple-dark)) !important;
    border-radius: 0 12px 12px 0;
  }

  .dp-cell.dp-range-between {
    background: rgba(108,60,225,0.1);
    border-radius: 0;
    border-color: transparent;
  }

  .dp-cell.dp-range-between .dp-num { color: var(--purple); }
  .dp-cell.dp-range-start .dp-num, .dp-cell.dp-range-end .dp-num { color: white; font-weight: 700; }

  .dp-legend {
    display: flex; gap: 12px; flex-wrap: wrap;
    padding: 10px 2px 14px;
    border-top: 1px solid #F0EDFB; margin-top: 10px;
  }

  .dp-legend-item {
    display: flex; align-items: center; gap: 5px;
    font-size: 10px; color: var(--text-muted);
  }

  .dp-legend-dot {
    width: 8px; height: 8px; border-radius: 3px;
  }

  .dp-actions {
    padding: 0 16px 32px;
    display: flex; gap: 10px;
  }

  .dp-btn-cancel {
    flex: 1; padding: 14px;
    background: white; border: 1.5px solid #E5E0F5;
    border-radius: var(--radius-pill);
    color: var(--text-mid); font-family: var(--font);
    font-size: 14px; font-weight: 600; cursor: pointer;
  }

  .dp-btn-confirm {
    flex: 2; padding: 14px;
    background: linear-gradient(135deg, var(--purple) 0%, var(--purple-dark) 100%);
    border: none; border-radius: var(--radius-pill);
    color: white; font-family: var(--font);
    font-size: 14px; font-weight: 700; cursor: pointer;
    box-shadow: 0 4px 18px rgba(108,60,225,0.38);
    transition: all 0.2s;
  }

  .dp-btn-confirm:active { transform: scale(0.97); }

  .dp-holiday-tip {
    background: rgba(239,68,68,0.07);
    border: 1px solid rgba(239,68,68,0.15);
    border-radius: var(--radius-sm);
    padding: 8px 12px; margin: 0 16px 12px;
    font-size: 11px; color: var(--danger);
    display: none; align-items: center; gap: 7px;
    line-height: 1.4;
  }

  .dp-holiday-tip.show { display: flex; }
  .dp-holiday-tip svg { width: 14px; height: 14px; stroke-width: 2; flex-shrink: 0; }
</style>
</head>
<body>

<!-- ==================== SPLASH ==================== -->
<div id="screen-splash" class="screen active">
  <div class="blob-bg splash-blob1"></div>
  <div class="blob-bg splash-blob2"></div>

  <div class="splash-hero">
    <div class="splash-icon-wrap"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="3" width="18" height="18" rx="2"/><line x1="9" y1="3" x2="9" y2="21"/><line x1="3" y1="9" x2="21" y2="9"/><line x1="3" y1="15" x2="21" y2="15"/><line x1="15" y1="3" x2="15" y2="21"/></svg></div>

    <div class="splash-brand">
      <h1>Leave Data Pro</h1>
      <div class="sub">ระบบลาดาต้าโปร</div>
    </div>

    <p class="splash-tagline">ระบบบริหารการลาอัจฉริยะ สำหรับองค์กรสมัยใหม่</p>

    <div class="splash-pills">
      <div class="splash-pill"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg> 4 ประเภทการลา</div>
      <div class="splash-pill"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"/></svg> Real-time</div>
      <div class="splash-pill"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="11" width="18" height="11" rx="2" ry="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg> ปลอดภัย 100%</div>
    </div>
  </div>

  <div class="splash-bottom">
    <button class="btn-white" onclick="showScreen('login')">
      <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="11" width="18" height="11" rx="2" ry="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg> เข้าสู่ระบบ
    </button>
    <div class="splash-version">v2.5.1 • HR Edition • © 2024</div>
  </div>
</div>

<!-- ==================== LOGIN ==================== -->
<div id="screen-login" class="screen">
  <div class="login-header-wrap">
    <div class="login-header-blob"></div>
    <div class="login-logo-sm"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;color:white;"><rect x="3" y="3" width="18" height="18" rx="2"/><line x1="9" y1="3" x2="9" y2="21"/><line x1="3" y1="9" x2="21" y2="9"/><line x1="3" y1="15" x2="21" y2="15"/><line x1="15" y1="3" x2="15" y2="21"/></svg></div>
    <div class="login-header-text">
      <h2>เข้าสู่ระบบ</h2>
      <p>Leave Data Pro — ระบบลาดาต้าโปร</p>
    </div>
  </div>

  <div class="login-body">
    <p class="login-section-label">เลือกบทบาท</p>
    <div class="role-toggle">
      <div class="role-option selected" id="role-emp" onclick="selectRole('employee')">
        <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
        พนักงาน
      </div>
      <div class="role-option" id="role-mgr" onclick="selectRole('manager')">
        <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/><path d="M12 11 10 21l2-2 2 2-2-10"/></svg>
        หัวหน้า
      </div>
    </div>

    <p class="login-section-label">ข้อมูลเข้าสู่ระบบ</p>
    <div class="form-group">
      <label class="form-label">ชื่อผู้ใช้ / รหัสพนักงาน</label>
      <div class="input-with-icon">
        <span class="input-icon"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg></span>
        <input type="text" class="form-control" id="login-user" placeholder="กรอกชื่อผู้ใช้" value="EMP001">
      </div>
    </div>

    <div class="form-group">
      <label class="form-label">รหัสผ่าน</label>
      <div class="input-with-icon">
        <span class="input-icon"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="11" width="18" height="11" rx="2" ry="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg></span>
        <input type="password" class="form-control" id="login-pass" placeholder="กรอกรหัสผ่าน" value="••••••">
      </div>
    </div>

    <div class="login-meta-row">
      <span style="font-size:12px;color:var(--purple);cursor:pointer;font-weight:600;">ลืมรหัสผ่าน?</span>
    </div>

    <button class="btn-purple" onclick="doLogin()">เข้าสู่ระบบ →</button>

    <div class="login-hint">
      <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><path d="M9.09 9a3 3 0 0 1 5.83 1c0 2-3 3-3 3"/><line x1="12" y1="17" x2="12.01" y2="17"/></svg>
      <span><strong>สาธิตระบบ:</strong> เลือกบทบาทด้านบน แล้วกดเข้าสู่ระบบ — หากมีปัญหาการเข้าถึง ติดต่อ HR ที่ต่อ 1234</span>
    </div>
  </div>
</div>

<!-- ==================== MAIN APP ==================== -->
<div id="screen-app" class="screen">

  <!-- TOP BAR -->
  <div class="app-topbar">
    <div class="topbar-left">
      <div class="topbar-avatar" id="topbar-avatar">น</div>
      <div class="topbar-info">
        <h3 id="topbar-name">นายสมชาย ใจดี</h3>
        <span id="topbar-dept">ฝ่ายการตลาด • EMP001</span>
      </div>
    </div>
    <div class="topbar-right">
      <div class="notif-btn" onclick="openNotifications()">
        <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.73 21a2 2 0 0 1-3.46 0"/></svg>
        <div class="notif-badge" id="notif-count">3</div>
      </div>
    </div>
  </div>

  <div class="tab-content">

    <!-- ===== DASHBOARD ===== -->
    <div class="tab-page active" id="tab-home">

      <div class="dash-hero">
        <div class="dash-hero-blob"></div>
        <div class="dash-hero-blob2"></div>
        <div class="dash-greeting" id="dash-greeting">สวัสดีตอนเช้า <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M12 2v4"/><path d="M4.93 4.93l2.83 2.83"/><path d="M2 12h4"/><path d="M17.07 7.76l2.83-2.83"/><path d="M22 12h-4"/><path d="M4.93 19.07l2.83-2.83"/><path d="M19.07 19.07l-2.83-2.83"/><path d="M5 17a7 7 0 0 1 14 0"/></svg></div>
        <div class="dash-name" id="dash-name">นายสมชาย ใจดี</div>
        <div class="dept-pill" id="dash-dept-badge"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="3" width="18" height="18" rx="2"/><line x1="9" y1="3" x2="9" y2="21"/><line x1="3" y1="9" x2="21" y2="9"/><line x1="3" y1="15" x2="21" y2="15"/><line x1="15" y1="3" x2="15" y2="21"/></svg> ฝ่ายการตลาด</div>
      </div>

      <!-- Quota cards floating -->
      <div class="quota-row-wrap">
        <div class="quota-row">
          <div class="quota-card sick">
            <div class="quota-icon-ring"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="3" width="18" height="18" rx="2"/><path d="M12 8v8"/><path d="M8 12h8"/></svg></div>
            <div class="quota-info">
              <span class="q-label">ลาป่วยคงเหลือ</span>
              <span class="q-val" id="q-sick">8</span>
              <span class="q-sub">จาก 30 วัน</span>
            </div>
          </div>
          <div class="quota-card personal">
            <div class="quota-icon-ring"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"/><rect x="8" y="2" width="8" height="4" rx="1" ry="1"/><line x1="8" y1="12" x2="16" y2="12"/><line x1="8" y1="16" x2="12" y2="16"/></svg></div>
            <div class="quota-info">
              <span class="q-label">ลากิจคงเหลือ</span>
              <span class="q-val" id="q-personal">4</span>
              <span class="q-sub">จาก 6 วัน</span>
            </div>
          </div>
          <div class="quota-card vacation">
            <div class="quota-icon-ring"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M17.5 7A6.5 6.5 0 0 0 5 10.5c0 1.5.5 2.9 1.3 4L3 18l3.5.5L8 22l3.5-3.5c1 .6 2.2 1 3.5 1a6.5 6.5 0 0 0 0-13z"/><path d="M12 13a2 2 0 1 0 0-4 2 2 0 0 0 0 4z" fill="currentColor" stroke="none"/></svg>️</div>
            <div class="quota-info">
              <span class="q-label">พักร้อนคงเหลือ</span>
              <span class="q-val" id="q-vacation">10</span>
              <span class="q-sub">จาก 10 วัน</span>
            </div>
          </div>
          <div class="quota-card special">
            <div class="quota-icon-ring"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg></div>
            <div class="quota-info">
              <span class="q-label">กิจพิเศษ</span>
              <span class="q-val" id="q-special">3</span>
              <span class="q-sub">จาก 3 วัน</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Summary Ring -->
      <div class="section" style="margin-top:20px;">
        <div class="section-header">
          <div class="section-title"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/><line x1="2" y1="20" x2="22" y2="20"/></svg> ภาพรวมการลาปีนี้</div>
          <span class="section-link">ดูรายละเอียด</span>
        </div>
        <div class="summary-card">
          <svg width="90" height="90" viewBox="0 0 90 90">
            <circle cx="45" cy="45" r="36" fill="none" stroke="#F0EDFB" stroke-width="10"/>
            <circle cx="45" cy="45" r="36" fill="none" stroke="#EF4444" stroke-width="10"
              stroke-dasharray="226" stroke-dashoffset="181" transform="rotate(-90 45 45)"/>
            <circle cx="45" cy="45" r="36" fill="none" stroke="#6366F1" stroke-width="10"
              stroke-dasharray="226" stroke-dashoffset="198" transform="rotate(-72 45 45)"/>
            <circle cx="45" cy="45" r="36" fill="none" stroke="#10B981" stroke-width="10"
              stroke-dasharray="226" stroke-dashoffset="226" transform="rotate(-49 45 45)"/>
            <text x="45" y="49" text-anchor="middle" fill="#1A0A3C" font-size="15" font-family="IBM Plex Mono" font-weight="700">12</text>
            <text x="45" y="60" text-anchor="middle" fill="#9B89C4" font-size="8">วัน</text>
          </svg>
          <div class="ring-legend">
            <div class="ring-legend-item">
              <div class="ring-dot" style="background:#EF4444"></div>
              <span>ลาป่วย</span>
              <span class="rl-val" style="color:#EF4444">7</span>
            </div>
            <div class="ring-legend-item">
              <div class="ring-dot" style="background:#6366F1"></div>
              <span>ลากิจ</span>
              <span class="rl-val" style="color:#6366F1">3</span>
            </div>
            <div class="ring-legend-item">
              <div class="ring-dot" style="background:#10B981"></div>
              <span>พักร้อน</span>
              <span class="rl-val" style="color:#10B981">2</span>
            </div>
            <div class="ring-legend-item">
              <div class="ring-dot" style="background:#F59E0B"></div>
              <span>กิจพิเศษ</span>
              <span class="rl-val" style="color:#F59E0B">0</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Quick Actions -->
      <div class="section">
        <div class="section-header">
          <div class="section-title"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>️ ยื่นคำขอลา</div>
        </div>
        <div class="quick-actions">
          <div class="qa-btn" onclick="openLeaveForm('sick')">
            <div class="qa-icon" style="background:rgba(239,68,68,0.1)"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="3" width="18" height="18" rx="2"/><path d="M12 8v8"/><path d="M8 12h8"/></svg></div>
            <div class="qa-label">ลาป่วย</div>
            <div class="qa-sub">เจ็บป่วย / รักษาพยาบาล</div>
          </div>
          <div class="qa-btn" onclick="openLeaveForm('personal')">
            <div class="qa-icon" style="background:rgba(99,102,241,0.1)"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"/><rect x="8" y="2" width="8" height="4" rx="1" ry="1"/><line x1="8" y1="12" x2="16" y2="12"/><line x1="8" y1="16" x2="12" y2="16"/></svg></div>
            <div class="qa-label">ลากิจ</div>
            <div class="qa-sub">ธุระส่วนตัว</div>
          </div>
          <div class="qa-btn" onclick="openLeaveForm('vacation')">
            <div class="qa-icon" style="background:rgba(16,185,129,0.1)"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M17.5 7A6.5 6.5 0 0 0 5 10.5c0 1.5.5 2.9 1.3 4L3 18l3.5.5L8 22l3.5-3.5c1 .6 2.2 1 3.5 1a6.5 6.5 0 0 0 0-13z"/><path d="M12 13a2 2 0 1 0 0-4 2 2 0 0 0 0 4z" fill="currentColor" stroke="none"/></svg>️</div>
            <div class="qa-label">ลาพักร้อน</div>
            <div class="qa-sub">วันหยุดพักผ่อน</div>
          </div>
          <div class="qa-btn" onclick="openLeaveForm('special')">
            <div class="qa-icon" style="background:rgba(245,158,11,0.1)"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg></div>
            <div class="qa-label">กิจพิเศษ</div>
            <div class="qa-sub">แต่งงาน / บวช ฯลฯ</div>
          </div>
        </div>
      </div>

      <!-- Recent -->
      <div class="section">
        <div class="section-header">
          <div class="section-title"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><circle cx="12" cy="12" r="9"/><polyline points="12 7 12 12 14 14"/></svg> คำขอล่าสุด</div>
          <span class="section-link" onclick="switchTab('history')">ดูทั้งหมด</span>
        </div>
        <div class="leave-status-list">
          <div class="leave-status-card" onclick="showLeaveDetail('sick','2024-12-10','2024-12-11','2','รอ')">
            <div class="lsc-icon sick"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="3" width="18" height="18" rx="2"/><path d="M12 8v8"/><path d="M8 12h8"/></svg></div>
            <div class="lsc-info">
              <h4>ลาป่วย</h4>
              <p>10–11 ธ.ค. 2567 • 2 วัน</p>
            </div>
            <div class="lsc-meta">
              <div class="status-badge pending">รออนุมัติ</div>
              <div class="date">2 วันที่แล้ว</div>
            </div>
          </div>
          <div class="leave-status-card">
            <div class="lsc-icon vacation"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M17.5 7A6.5 6.5 0 0 0 5 10.5c0 1.5.5 2.9 1.3 4L3 18l3.5.5L8 22l3.5-3.5c1 .6 2.2 1 3.5 1a6.5 6.5 0 0 0 0-13z"/><path d="M12 13a2 2 0 1 0 0-4 2 2 0 0 0 0 4z" fill="currentColor" stroke="none"/></svg>️</div>
            <div class="lsc-info">
              <h4>ลาพักร้อน</h4>
              <p>20–22 พ.ย. 2567 • 3 วัน</p>
            </div>
            <div class="lsc-meta">
              <div class="status-badge approved">อนุมัติแล้ว</div>
              <div class="date">15 วันที่แล้ว</div>
            </div>
          </div>
          <div class="leave-status-card">
            <div class="lsc-icon personal"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"/><rect x="8" y="2" width="8" height="4" rx="1" ry="1"/><line x1="8" y1="12" x2="16" y2="12"/><line x1="8" y1="16" x2="12" y2="16"/></svg></div>
            <div class="lsc-info">
              <h4>ลากิจ</h4>
              <p>5 พ.ย. 2567 • ครึ่งวัน</p>
            </div>
            <div class="lsc-meta">
              <div class="status-badge approved">อนุมัติแล้ว</div>
              <div class="date">25 วันที่แล้ว</div>
            </div>
          </div>
        </div>
      </div>

      <!-- Calendar -->
      <div class="section">
        <div class="section-header">
          <div class="section-title"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg> ปฏิทินการลา</div>
          <span class="section-link" onclick="openHolidaysModal()">วันหยุดบริษัท ประจำปี</span>
        </div>
      </div>
      <div id="mini-calendar"></div>
      <div style="height:8px;"></div>
    </div>

    <!-- ===== LEAVE FORM ===== -->
    <div class="tab-page" id="tab-apply">
      <div class="form-page">
        <div class="form-page-title">ยื่นคำขอลา</div>
        <div class="form-page-sub">กรอกข้อมูลเพื่อส่งคำขอลา</div>

        <p class="form-section-title">ประเภทการลา</p>
        <div class="leave-type-selector">
          <div class="leave-type-btn sick selected" id="lt-sick" onclick="selectLeaveType('sick')">
            <span class="lt-icon"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="3" width="18" height="18" rx="2"/><path d="M12 8v8"/><path d="M8 12h8"/></svg></span>
            <span class="lt-name">ลาป่วย</span>
            <span class="lt-days">คงเหลือ 8 วัน</span>
          </div>
          <div class="leave-type-btn personal" id="lt-personal" onclick="selectLeaveType('personal')">
            <span class="lt-icon"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"/><rect x="8" y="2" width="8" height="4" rx="1" ry="1"/><line x1="8" y1="12" x2="16" y2="12"/><line x1="8" y1="16" x2="12" y2="16"/></svg></span>
            <span class="lt-name">ลากิจ</span>
            <span class="lt-days">คงเหลือ 4 วัน</span>
          </div>
          <div class="leave-type-btn vacation" id="lt-vacation" onclick="selectLeaveType('vacation')">
            <span class="lt-icon"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M17.5 7A6.5 6.5 0 0 0 5 10.5c0 1.5.5 2.9 1.3 4L3 18l3.5.5L8 22l3.5-3.5c1 .6 2.2 1 3.5 1a6.5 6.5 0 0 0 0-13z"/><path d="M12 13a2 2 0 1 0 0-4 2 2 0 0 0 0 4z" fill="currentColor" stroke="none"/></svg>️</span>
            <span class="lt-name">ลาพักร้อน</span>
            <span class="lt-days">คงเหลือ 10 วัน</span>
          </div>
          <div class="leave-type-btn special" id="lt-special" onclick="selectLeaveType('special')">
            <span class="lt-icon"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg></span>
            <span class="lt-name">กิจพิเศษ</span>
            <span class="lt-days">คงเหลือ 3 วัน</span>
          </div>
        </div>

        <p class="form-section-title">ช่วงเวลา</p>
        <div class="duration-selector">
          <button class="dur-btn selected" id="dur-half" onclick="selectDuration('half')">ครึ่งวัน</button>
          <button class="dur-btn" id="dur-full" onclick="selectDuration('full')">เต็มวัน</button>
          <button class="dur-btn" id="dur-multi" onclick="selectDuration('multi')">หลายวัน</button>
        </div>

        <div id="half-day-options" style="margin-bottom:14px;">
          <div class="duration-selector" style="margin-bottom:0;">
            <button class="dur-btn selected" onclick="this.parentNode.querySelectorAll('.dur-btn').forEach(b=>b.classList.remove('selected'));this.classList.add('selected')">ช่วงเช้า</button>
            <button class="dur-btn" onclick="this.parentNode.querySelectorAll('.dur-btn').forEach(b=>b.classList.remove('selected'));this.classList.add('selected')">ช่วงบ่าย</button>
          </div>
        </div>

        <div class="form-row">
          <div class="form-group">
            <label class="form-label">วันที่เริ่มลา</label>
            <div class="date-display" onclick="pickDate('start')">
              <span class="cal-icon"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg></span>
              <div>
                <div class="cal-label">วันที่เริ่ม</div>
                <div class="cal-value" id="date-start-display">เลือกวันที่</div>
              </div>
            </div>
            <input type="date" id="date-start" style="display:none;" onchange="updateDateDisplay()">
          </div>
          <div class="form-group" id="end-date-group" style="display:none;">
            <label class="form-label">วันที่สิ้นสุด</label>
            <div class="date-display" onclick="pickDate('end')">
              <span class="cal-icon"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg></span>
              <div>
                <div class="cal-label">วันที่สิ้นสุด</div>
                <div class="cal-value" id="date-end-display">เลือกวันที่</div>
              </div>
            </div>
            <input type="date" id="date-end" style="display:none;" onchange="updateDateDisplay()">
          </div>
        </div>

        <div class="form-group">
          <label class="form-label">ผู้รับทราบ / ผู้แทน</label>
          <select class="form-control">
            <option>นายวิชัย สุขใส (หัวหน้าฝ่าย)</option>
            <option>นางสาวพิมพ์ใจ มานะ (ผู้จัดการ)</option>
          </select>
        </div>

        <p class="form-section-title">เหตุผลการลา</p>
        <div class="form-group">
          <textarea class="form-control" id="leave-reason" placeholder="กรอกเหตุผลการลา เช่น ป่วยเป็นไข้หวัด มีไข้สูง..."></textarea>
        </div>

        <p class="form-section-title">เอกสารประกอบ (ถ้ามี)</p>

        <div class="upload-area" id="upload-area" onclick="triggerUpload()">
          <span class="upload-icon"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="m21.44 11.05-9.19 9.19a6 6 0 0 1-8.49-8.49l9.19-9.19a4 4 0 0 1 5.66 5.66l-9.2 9.19a2 2 0 0 1-2.83-2.83l8.49-8.48"/></svg></span>
          <div class="upload-text">แนบใบรับรองแพทย์ หรือเอกสาร</div>
          <div class="upload-sub">รูปภาพ / PDF ขนาดไม่เกิน 10MB</div>
        </div>
        <input type="file" id="file-input" style="display:none;" accept="image/*,application/pdf" onchange="handleFileUpload(event)">

        <div class="upload-preview" id="upload-preview">
          <span class="preview-icon" id="preview-icon"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/></svg></span>
          <div class="preview-info">
            <div class="preview-name" id="preview-name">ใบรับรองแพทย์.jpg</div>
            <div class="preview-size" id="preview-size">1.2 MB</div>
          </div>
          <span class="preview-del" onclick="removeUpload()"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg></span>
        </div>

        <div style="margin-bottom:8px;padding:12px 14px;background:rgba(99,102,241,0.06);border:1.5px solid rgba(99,102,241,0.15);border-radius:var(--radius-sm);">
          <div style="font-size:11px;color:var(--text-mid);">
            <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z"/><circle cx="12" cy="13" r="4"/></svg> <strong style="color:var(--info);">ถ่ายรูป</strong> ใบรับรองแพทย์ได้โดยตรงจากกล้องมือถือ
          </div>
        </div>

        <div style="display:flex;gap:10px;margin-top:20px;">
          <button style="flex:1;padding:15px;background:#fff;border:1.5px solid #E5E0F5;border-radius:var(--radius-pill);color:var(--text-mid);font-family:var(--font);font-size:14px;font-weight:600;cursor:pointer;" onclick="switchTab('home')">ยกเลิก</button>
          <button class="btn-purple" style="flex:2;padding:15px;" onclick="submitLeave()">ส่งคำขอลา <svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><polyline points="20 6 9 17 4 12"/></svg></button>
        </div>
      </div>
    </div>

    <!-- ===== APPROVAL TAB ===== -->
    <div class="tab-page" id="tab-approve">

      <!-- MANAGER VIEW -->
      <div id="view-manager-approve">
      <div class="approval-banner">
        <div class="approval-banner-icon"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="m10.29 3.86-8.6 14.9A1 1 0 0 0 2.57 20h17.86a1 1 0 0 0 .87-1.5L12.7 3.86a1 1 0 0 0-1.73 0h.02z"/><line x1="12" y1="9" x2="12" y2="13"/><line x1="12" y1="17" x2="12.01" y2="17"/></svg>️</div>
        <div class="approval-banner-info">
          <h4>รออนุมัติ 3 รายการ</h4>
          <p>กรุณาตรวจสอบและดำเนินการ</p>
        </div>
      </div>

      <div class="section">
        <div class="section-header" style="margin-top:16px;">
          <div class="section-title"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"/><rect x="8" y="2" width="8" height="4" rx="1" ry="1"/><line x1="8" y1="12" x2="16" y2="12"/><line x1="8" y1="16" x2="12" y2="16"/></svg> คำขอที่รออนุมัติ</div>
          <span class="section-link">ทั้งหมด (3)</span>
        </div>

        <div class="approval-card sick">
          <div class="appr-header">
            <div class="appr-requester">
              <div class="appr-avatar">ว</div>
              <div>
                <div class="appr-name">นายวรพล สมบัติ</div>
                <div class="appr-dept">ฝ่ายการตลาด</div>
              </div>
            </div>
            <span class="appr-type-badge sick"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="3" width="18" height="18" rx="2"/><path d="M12 8v8"/><path d="M8 12h8"/></svg> ลาป่วย</span>
          </div>
          <div class="appr-details">
            <div class="appr-detail-row"><span class="d-key"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg> วันที่ลา</span><span class="d-val">10–11 ธ.ค. 2567</span></div>
            <div class="appr-detail-row"><span class="d-key"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><circle cx="12" cy="12" r="9"/><polyline points="12 7 12 12 14 14"/></svg> ระยะเวลา</span><span class="d-val">2 วันทำการ</span></div>
            <div class="appr-detail-row"><span class="d-key"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/></svg> เอกสาร</span><span class="d-val good"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><polyline points="20 6 9 17 4 12"/></svg> แนบใบแพทย์</span></div>
            <div class="appr-detail-row"><span class="d-key"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/></svg> วันลาคงเหลือ</span><span class="d-val">28/30 วัน</span></div>
          </div>
          <div class="appr-reason"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg> "มีไข้สูง 38.5 องศา แพทย์แนะนำให้พักฟื้น 2 วัน มีใบรับรองแพทย์แนบ"</div>
          <div class="appr-actions">
            <button class="btn-reject" onclick="handleApproval('reject','นายวรพล สมบัติ')"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg> ปฏิเสธ</button>
            <button class="btn-approve" onclick="handleApproval('approve','นายวรพล สมบัติ')"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><polyline points="20 6 9 17 4 12"/></svg> อนุมัติ</button>
          </div>
        </div>

        <div class="approval-card vacation">
          <div class="appr-header">
            <div class="appr-requester">
              <div class="appr-avatar" style="background:linear-gradient(135deg,#F472B6,#F59E0B);">ป</div>
              <div>
                <div class="appr-name">นางสาวประภา ดีงาม</div>
                <div class="appr-dept">ฝ่ายบัญชี</div>
              </div>
            </div>
            <span class="appr-type-badge vacation"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M17.5 7A6.5 6.5 0 0 0 5 10.5c0 1.5.5 2.9 1.3 4L3 18l3.5.5L8 22l3.5-3.5c1 .6 2.2 1 3.5 1a6.5 6.5 0 0 0 0-13z"/><path d="M12 13a2 2 0 1 0 0-4 2 2 0 0 0 0 4z" fill="currentColor" stroke="none"/></svg>️ พักร้อน</span>
          </div>
          <div class="appr-details">
            <div class="appr-detail-row"><span class="d-key"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg> วันที่ลา</span><span class="d-val">20–24 ธ.ค. 2567</span></div>
            <div class="appr-detail-row"><span class="d-key"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><circle cx="12" cy="12" r="9"/><polyline points="12 7 12 12 14 14"/></svg> ระยะเวลา</span><span class="d-val">5 วันทำการ</span></div>
            <div class="appr-detail-row"><span class="d-key"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/></svg> เอกสาร</span><span class="d-val none">— ไม่มีเอกสาร</span></div>
            <div class="appr-detail-row"><span class="d-key"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/></svg> วันลาคงเหลือ</span><span class="d-val">10/10 วัน</span></div>
          </div>
          <div class="appr-reason"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg> "ต้องการพักผ่อนช่วงปีใหม่ ท่องเที่ยวกับครอบครัว"</div>
          <div class="appr-actions">
            <button class="btn-reject" onclick="handleApproval('reject','นางสาวประภา ดีงาม')"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg> ปฏิเสธ</button>
            <button class="btn-approve" onclick="handleApproval('approve','นางสาวประภา ดีงาม')"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><polyline points="20 6 9 17 4 12"/></svg> อนุมัติ</button>
          </div>
        </div>

        <div class="approval-card personal">
          <div class="appr-header">
            <div class="appr-requester">
              <div class="appr-avatar" style="background:linear-gradient(135deg,#6366F1,#8B5CF6);">ก</div>
              <div>
                <div class="appr-name">นายกิตติ รักษา</div>
                <div class="appr-dept">ฝ่าย IT</div>
              </div>
            </div>
            <span class="appr-type-badge personal"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"/><rect x="8" y="2" width="8" height="4" rx="1" ry="1"/><line x1="8" y1="12" x2="16" y2="12"/><line x1="8" y1="16" x2="12" y2="16"/></svg> ลากิจ</span>
          </div>
          <div class="appr-details">
            <div class="appr-detail-row"><span class="d-key"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg> วันที่ลา</span><span class="d-val">12 ธ.ค. 2567</span></div>
            <div class="appr-detail-row"><span class="d-key"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><circle cx="12" cy="12" r="9"/><polyline points="12 7 12 12 14 14"/></svg> ระยะเวลา</span><span class="d-val">ครึ่งวัน (บ่าย)</span></div>
            <div class="appr-detail-row"><span class="d-key"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/></svg> เอกสาร</span><span class="d-val none">— ไม่มีเอกสาร</span></div>
            <div class="appr-detail-row"><span class="d-key"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/></svg> วันลาคงเหลือ</span><span class="d-val">5.5/6 วัน</span></div>
          </div>
          <div class="appr-reason"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg> "นัดแพทย์ฟันยามบ่าย ประมาณ 14.00 น."</div>
          <div class="appr-actions">
            <button class="btn-reject" onclick="handleApproval('reject','นายกิตติ รักษา')"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg> ปฏิเสธ</button>
            <button class="btn-approve" onclick="handleApproval('approve','นายกิตติ รักษา')"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertical-align:-0.15em;"><polyline points="20 6 9 17 4 12"/></svg> อนุมัติ</button>
          </div>
        </div>
      </div>

      <div class="section">
        <div class="section-header" style="margin-top:8px;">
          <div class="section-title"><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="display:inline-block;vertica