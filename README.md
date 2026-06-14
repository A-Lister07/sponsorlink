<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SponsorLink — Sponsorship Marketplace</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@3.19.0/dist/tabler-icons.min.css">
<style>
  :root {
    --bg: #ffffff;
    --bg2: #f7f7f5;
    --bg3: #f0efeb;
    --text: #1a1a18;
    --text2: #6b6b67;
    --text3: #9e9e99;
    --border: rgba(0,0,0,0.1);
    --border2: rgba(0,0,0,0.18);
    --radius: 8px;
    --radius-lg: 12px;
    --blue: #185FA5;
    --blue-bg: #E6F1FB;
    --blue-text: #0C447C;
    --teal: #1D9E75;
    --teal-bg: #E1F5EE;
    --teal-text: #085041;
    --amber-bg: #FAEEDA;
    --amber-text: #854F0B;
    --purple-bg: #EEEDFE;
    --purple-text: #534AB7;
    --green-bg: #EAF3DE;
    --green-text: #3B6D11;
    --coral-bg: #FAECE7;
    --coral-text: #993C1D;
  }
  @media (prefers-color-scheme: dark) {
    :root {
      --bg: #1c1c1a;
      --bg2: #242422;
      --bg3: #2c2c2a;
      --text: #f0efe9;
      --text2: #9e9e97;
      --text3: #6b6b67;
      --border: rgba(255,255,255,0.1);
      --border2: rgba(255,255,255,0.18);
      --blue-bg: #0c2d52;
      --blue-text: #85B7EB;
      --teal-bg: #053425;
      --teal-text: #5DCAA5;
      --amber-bg: #3d2700;
      --amber-text: #EF9F27;
      --purple-bg: #1e1a4a;
      --purple-text: #AFA9EC;
      --green-bg: #0f2200;
      --green-text: #97C459;
      --coral-bg: #3d1008;
      --coral-text: #F0997B;
    }
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; background: var(--bg3); color: var(--text); min-height: 100vh; font-size: 14px; }

  /* NAV */
  .topnav { background: var(--bg); border-bottom: 0.5px solid var(--border); display: flex; align-items: center; padding: 0 24px; position: sticky; top: 0; z-index: 50; }
  .nav-logo { font-size: 16px; font-weight: 600; padding: 14px 20px 14px 0; border-right: 0.5px solid var(--border); display: flex; align-items: center; gap: 8px; color: var(--text); }
  .nav-logo i { font-size: 20px; color: var(--blue); }
  .nav-tabs { display: flex; flex: 1; padding: 0 20px; }
  .nav-tab { padding: 14px 16px; font-size: 13px; color: var(--text2); cursor: pointer; border-bottom: 2px solid transparent; margin-bottom: -1px; transition: color .15s; text-decoration: none; }
  .nav-tab:hover, .nav-tab.active { color: var(--text); }
  .nav-tab.active { font-weight: 500; border-bottom-color: var(--text); }
  .nav-right { display: flex; gap: 8px; padding-left: 16px; }
  .btn { padding: 7px 14px; font-size: 13px; border: 0.5px solid var(--border2); border-radius: var(--radius); cursor: pointer; background: var(--bg); color: var(--text); transition: background .15s; display: inline-flex; align-items: center; gap: 5px; }
  .btn:hover { background: var(--bg2); }
  .btn-primary { background: var(--blue); color: #fff; border-color: var(--blue); }
  .btn-primary:hover { background: var(--blue-text); }
  .btn-sm { padding: 5px 11px; font-size: 12px; }
  .btn-success { background: var(--teal); color: #fff; border-color: var(--teal); }
  .btn-success:hover { opacity: .88; }

  /* LAYOUT */
  .page { display: none; max-width: 1100px; margin: 0 auto; padding: 24px 20px; }
  .page.active { display: block; }

  /* STATS */
  .stat-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; margin-bottom: 24px; }
  .stat { background: var(--bg); border-radius: var(--radius); padding: 14px 16px; border: 0.5px solid var(--border); }
  .stat-val { font-size: 24px; font-weight: 600; color: var(--text); }
  .stat-lbl { font-size: 12px; color: var(--text2); margin-top: 2px; }

  /* CARDS */
  .section-hdr { display: flex; justify-content: space-between; align-items: center; margin-bottom: 14px; }
  .section-title { font-size: 14px; font-weight: 500; }
  .filters { display: flex; gap: 8px; margin-bottom: 16px; flex-wrap: wrap; }
  .pill { padding: 5px 13px; font-size: 12px; border: 0.5px solid var(--border2); border-radius: 20px; cursor: pointer; background: var(--bg); color: var(--text2); transition: all .15s; }
  .pill.active { background: var(--text); color: var(--bg); border-color: var(--text); }
  .grid-2 { display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; }
  .card { background: var(--bg); border: 0.5px solid var(--border); border-radius: var(--radius-lg); padding: 16px; transition: border-color .15s; }
  .card:hover { border-color: var(--border2); }
  .card-hdr { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 10px; }
  .card-title { font-size: 14px; font-weight: 500; }
  .card-sub { font-size: 12px; color: var(--text2); margin-top: 2px; }
  .avatar { width: 36px; height: 36px; border-radius: 8px; display: flex; align-items: center; justify-content: center; font-size: 12px; font-weight: 600; flex-shrink: 0; }
  .av-blue { background: var(--blue-bg); color: var(--blue-text); }
  .av-teal { background: var(--teal-bg); color: var(--teal-text); }
  .av-amber { background: var(--amber-bg); color: var(--amber-text); }
  .av-purple { background: var(--purple-bg); color: var(--purple-text); }
  .av-coral { background: var(--coral-bg); color: var(--coral-text); }
  .av-green { background: var(--green-bg); color: var(--green-text); }
  .detail-row { display: flex; align-items: flex-start; gap: 6px; font-size: 12px; color: var(--text2); margin-top: 6px; line-height: 1.4; }
  .detail-row i { font-size: 14px; flex-shrink: 0; margin-top: 1px; }
  .divider { border: none; border-top: 0.5px solid var(--border); margin: 12px 0; }
  .badge { display: inline-flex; align-items: center; padding: 3px 8px; border-radius: 20px; font-size: 11px; font-weight: 500; }
  .badge-cash { background: var(--green-bg); color: var(--green-text); }
  .badge-inkind { background: var(--blue-bg); color: var(--blue-text); }
  .badge-promo { background: var(--amber-bg); color: var(--amber-text); }
  .badge-media { background: var(--purple-bg); color: var(--purple-text); }
  .badge-open { background: var(--green-bg); color: var(--green-text); }
  .badge-hot { background: var(--amber-bg); color: var(--amber-text); font-size: 10px; }

  /* MATCHES */
  .match-card { background: var(--bg); border: 1.5px solid #9FE1CB; border-radius: var(--radius-lg); padding: 16px; position: relative; margin-bottom: 14px; }
  .match-score { position: absolute; top: -11px; right: 16px; background: var(--teal); color: #fff; font-size: 11px; font-weight: 600; padding: 3px 10px; border-radius: 20px; }
  .match-bar { height: 5px; border-radius: 3px; background: var(--bg3); margin-top: 8px; overflow: hidden; }
  .match-fill { height: 100%; border-radius: 3px; background: var(--teal); }
  .tag { display: inline-flex; align-items: center; gap: 4px; padding: 3px 8px; background: var(--bg2); border: 0.5px solid var(--border); border-radius: var(--radius); font-size: 11px; color: var(--text2); }

  /* DEALS / PIPELINE */
  .deal-card { background: var(--bg); border: 0.5px solid var(--border); border-radius: var(--radius-lg); padding: 16px; margin-bottom: 12px; }
  .pipeline { display: flex; align-items: center; margin: 12px 0 8px; }
  .p-step { display: flex; flex-direction: column; align-items: center; flex: 1; position: relative; }
  .p-step:not(:last-child)::after { content: ''; position: absolute; top: 9px; left: 50%; width: 100%; height: 1px; background: var(--border); z-index: 0; }
  .p-dot { width: 18px; height: 18px; border-radius: 50%; border: 1.5px solid var(--border2); background: var(--bg); display: flex; align-items: center; justify-content: center; z-index: 1; font-size: 9px; color: var(--text2); }
  .p-dot.done { background: var(--teal); border-color: var(--teal); color: #fff; }
  .p-dot.current { background: var(--blue); border-color: var(--blue); color: #fff; }
  .p-lbl { font-size: 10px; color: var(--text2); margin-top: 4px; text-align: center; }
  .p-lbl.current { color: var(--blue); font-weight: 500; }

  /* DEAL ROOM */
  .dealroom-wrap { display: grid; grid-template-columns: 260px 1fr; border: 0.5px solid var(--border); border-radius: var(--radius-lg); overflow: hidden; background: var(--bg); min-height: 640px; }
  .sidebar { border-right: 0.5px solid var(--border); display: flex; flex-direction: column; background: var(--bg2); }
  .sb-hdr { padding: 14px; border-bottom: 0.5px solid var(--border); }
  .sb-title { font-size: 13px; font-weight: 500; display: flex; justify-content: space-between; align-items: center; }
  .sb-search { margin-top: 8px; position: relative; }
  .sb-search input { width: 100%; font-size: 12px; padding: 6px 10px 6px 28px; border: 0.5px solid var(--border2); border-radius: var(--radius); background: var(--bg); color: var(--text); outline: none; }
  .sb-search i { position: absolute; left: 8px; top: 50%; transform: translateY(-50%); font-size: 14px; color: var(--text3); pointer-events: none; }
  .room-list { flex: 1; overflow-y: auto; }
  .room-item { padding: 11px 14px; cursor: pointer; border-bottom: 0.5px solid var(--border); transition: background .12s; }
  .room-item:hover { background: var(--bg); }
  .room-item.active { background: var(--bg); border-left: 2px solid var(--blue); }
  .room-top { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 3px; }
  .room-name { font-size: 12px; font-weight: 500; line-height: 1.3; }
  .room-time { font-size: 10px; color: var(--text3); white-space: nowrap; margin-left: 6px; }
  .room-preview { font-size: 11px; color: var(--text2); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
  .unread-dot { display: inline-block; width: 7px; height: 7px; border-radius: 50%; background: var(--blue); margin-left: 4px; vertical-align: middle; }
  .stage-pill { display: inline-block; padding: 2px 6px; border-radius: 10px; font-size: 10px; font-weight: 500; margin-top: 3px; }
  .s-matched { background: var(--blue-bg); color: var(--blue-text); }
  .s-proposal { background: var(--amber-bg); color: var(--amber-text); }
  .s-negotiation { background: var(--purple-bg); color: var(--purple-text); }
  .s-contract { background: var(--green-bg); color: var(--green-text); }
  .s-done { background: var(--teal-bg); color: var(--teal-text); }

  /* CHAT */
  .main-col { display: flex; flex-direction: column; min-height: 640px; overflow: hidden; }
  .room-hdr { padding: 12px 18px; border-bottom: 0.5px solid var(--border); display: flex; align-items: center; justify-content: space-between; }
  .room-hdr-left { display: flex; align-items: center; gap: 10px; }
  .room-hdr-title { font-size: 14px; font-weight: 500; }
  .room-hdr-sub { font-size: 11px; color: var(--text2); margin-top: 2px; display: flex; align-items: center; gap: 6px; flex-wrap: wrap; }
  .hdr-actions { display: flex; gap: 6px; }
  .icon-btn { background: none; border: 0.5px solid var(--border2); border-radius: var(--radius); padding: 5px 9px; cursor: pointer; color: var(--text2); font-size: 13px; display: inline-flex; align-items: center; gap: 5px; transition: background .12s; }
  .icon-btn:hover { background: var(--bg2); }
  .pipe-bar { padding: 10px 18px; border-bottom: 0.5px solid var(--border); display: flex; align-items: center; }
  .chat-area { flex: 1; padding: 16px 18px; display: flex; flex-direction: column; gap: 10px; overflow-y: auto; max-height: 380px; }
  .msg-row { display: flex; gap: 8px; align-items: flex-end; }
  .msg-row.mine { flex-direction: row-reverse; }
  .msg-av { width: 26px; height: 26px; border-radius: 6px; display: flex; align-items: center; justify-content: center; font-size: 10px; font-weight: 600; flex-shrink: 0; }
  .bubble { max-width: 72%; padding: 9px 12px; border-radius: 12px; font-size: 13px; line-height: 1.5; background: var(--bg2); border: 0.5px solid var(--border); color: var(--text); }
  .mine .bubble { background: var(--blue); color: #fff; border-color: var(--blue); }
  .msg-meta { font-size: 10px; color: var(--text3); margin-top: 3px; }
  .mine .msg-meta { text-align: left; }
  .system-msg { text-align: center; font-size: 11px; color: var(--text2); padding: 4px 0; }
  .system-msg span { background: var(--bg2); padding: 3px 10px; border-radius: 10px; border: 0.5px solid var(--border); }
  .doc-bubble { background: var(--bg); border: 0.5px solid var(--border2); border-radius: 10px; padding: 10px 12px; max-width: 72%; cursor: pointer; }
  .doc-bubble:hover { border-color: var(--blue); }
  .doc-title { font-size: 13px; font-weight: 500; display: flex; align-items: center; gap: 6px; }
  .doc-sub { font-size: 11px; color: var(--text2); margin-top: 2px; }
  .offer-bubble { background: var(--bg); border: 1.5px solid #9FE1CB; border-radius: 10px; padding: 12px 14px; max-width: 82%; }
  .offer-label { font-size: 10px; font-weight: 600; color: var(--teal-text); letter-spacing: .5px; margin-bottom: 8px; display: flex; align-items: center; gap: 4px; }
  .offer-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-bottom: 10px; }
  .offer-cell { background: var(--teal-bg); border-radius: 6px; padding: 7px 9px; }
  .offer-cell-lbl { font-size: 10px; color: var(--teal-text); margin-bottom: 2px; }
  .offer-cell-val { font-size: 12px; font-weight: 500; color: var(--teal-text); }
  .offer-actions { display: flex; gap: 6px; }
  .accept-btn { flex: 1; padding: 6px; font-size: 12px; font-weight: 500; background: var(--teal); color: #fff; border: none; border-radius: var(--radius); cursor: pointer; }
  .counter-btn { flex: 1; padding: 6px; font-size: 12px; background: var(--bg2); color: var(--text); border: 0.5px solid var(--border2); border-radius: var(--radius); cursor: pointer; }
  .input-area { padding: 12px 18px; border-top: 0.5px solid var(--border); }
  .toolbar { display: flex; gap: 6px; margin-bottom: 8px; align-items: center; }
  .tool-btn { background: none; border: none; cursor: pointer; color: var(--text2); font-size: 17px; padding: 3px 5px; border-radius: 4px; display: inline-flex; align-items: center; }
  .tool-btn:hover { color: var(--text); background: var(--bg2); }
  .input-row { display: flex; gap: 8px; align-items: flex-end; }
  .input-row textarea { flex: 1; font-size: 13px; padding: 8px 12px; border: 0.5px solid var(--border2); border-radius: var(--radius); resize: none; background: var(--bg); color: var(--text); outline: none; min-height: 38px; max-height: 100px; line-height: 1.5; font-family: inherit; }
  .send-btn { padding: 8px 16px; background: var(--blue); color: #fff; border: none; border-radius: var(--radius); cursor: pointer; font-size: 13px; font-weight: 500; display: inline-flex; align-items: center; gap: 5px; white-space: nowrap; }
  .send-btn:hover { background: var(--blue-text); }

  /* SIDE PANEL */
  .side-panel { display: none; width: 220px; border-left: 0.5px solid var(--border); flex-direction: column; background: var(--bg2); }
  .side-panel.open { display: flex; }
  .sp-hdr { padding: 12px 14px; border-bottom: 0.5px solid var(--border); font-size: 13px; font-weight: 500; display: flex; justify-content: space-between; align-items: center; }
  .sp-section { padding: 12px 14px; border-bottom: 0.5px solid var(--border); }
  .sp-label { font-size: 10px; font-weight: 600; color: var(--text2); letter-spacing: .5px; margin-bottom: 6px; }
  .sp-val { font-size: 12px; color: var(--text); line-height: 1.6; }
  .sp-file { display: flex; align-items: center; gap: 6px; padding: 6px 8px; background: var(--bg); border: 0.5px solid var(--border); border-radius: var(--radius); cursor: pointer; margin-bottom: 5px; }
  .sp-file:hover { border-color: var(--border2); }
  .sp-file-name { font-size: 11px; flex: 1; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
  .sp-file-size { font-size: 10px; color: var(--text3); }

  /* COUNTER MODAL */
  .counter-modal { display: none; padding: 14px 18px; border-bottom: 0.5px solid var(--border); background: var(--bg2); }
  .counter-modal.open { display: block; }
  .counter-title { font-size: 13px; font-weight: 500; margin-bottom: 10px; display: flex; justify-content: space-between; align-items: center; }
  .counter-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-bottom: 10px; }
  .cg label { font-size: 11px; color: var(--text2); display: block; margin-bottom: 3px; }
  .cg input { font-size: 12px; padding: 5px 8px; border: 0.5px solid var(--border2); border-radius: var(--radius); width: 100%; background: var(--bg); color: var(--text); outline: none; }

  /* MODAL */
  .modal-overlay { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.4); z-index: 200; align-items: flex-start; justify-content: center; padding-top: 60px; overflow-y: auto; }
  .modal-overlay.open { display: flex; }
  .modal { background: var(--bg); border: 0.5px solid var(--border2); border-radius: var(--radius-lg); padding: 24px; width: 100%; max-width: 500px; margin: 0 16px 40px; }
  .modal-hdr { display: flex; justify-content: space-between; align-items: center; margin-bottom: 18px; }
  .modal-title { font-size: 16px; font-weight: 600; }
  .close-x { background: none; border: none; cursor: pointer; color: var(--text2); font-size: 20px; line-height: 1; padding: 2px; }
  .form-row { display: flex; gap: 12px; margin-bottom: 12px; }
  .fg { display: flex; flex-direction: column; gap: 4px; flex: 1; }
  .fg label { font-size: 12px; color: var(--text2); }
  .fg input, .fg select, .fg textarea { font-size: 13px; padding: 8px 10px; border: 0.5px solid var(--border2); border-radius: var(--radius); background: var(--bg); color: var(--text); outline: none; width: 100%; font-family: inherit; }
  .fg textarea { min-height: 72px; resize: vertical; line-height: 1.5; }
  .form-actions { display: flex; justify-content: flex-end; gap: 8px; margin-top: 6px; }

  /* TOAST */
  .toast { position: fixed; bottom: 24px; right: 24px; background: var(--text); color: var(--bg); padding: 10px 18px; border-radius: var(--radius); font-size: 13px; z-index: 999; opacity: 0; transform: translateY(8px); transition: all .25s; pointer-events: none; }
  .toast.show { opacity: 1; transform: translateY(0); }

  /* EMPTY */
  .empty { text-align: center; padding: 48px 20px; color: var(--text2); grid-column: 1/-1; }
  .empty i { font-size: 36px; display: block; margin-bottom: 12px; opacity: .35; }

  /* RESPONSIVE */
  @media (max-width: 700px) {
    .stat-grid { grid-template-columns: 1fr 1fr; }
    .dealroom-wrap { grid-template-columns: 1fr; }
    .sidebar { display: none; }
    .form-row { flex-direction: column; }
    .topnav { padding: 0 12px; }
    .nav-tab { padding: 14px 10px; font-size: 12px; }
  }
</style>
</head>
<body>

<!-- TOP NAV -->
<nav class="topnav">
  <div class="nav-logo"><i class="ti ti-exchange"></i>SponsorLink</div>
  <div class="nav-tabs">
    <a class="nav-tab active" onclick="showPage('marketplace',this)" href="#">Marketplace</a>
    <a class="nav-tab" onclick="showPage('organizations',this)" href="#">Organizations</a>
    <a class="nav-tab" onclick="showPage('matches',this)" href="#">Matches</a>
    <a class="nav-tab" onclick="showPage('deals',this)" href="#">Active Deals</a>
    <a class="nav-tab" onclick="showPage('dealroom',this)" href="#">Deal Rooms</a>
  </div>
  <div class="nav-right">
    <button class="btn btn-sm" onclick="openModal('company')"><i class="ti ti-plus"></i> Post offer</button>
    <button class="btn btn-sm btn-primary" onclick="openModal('org')"><i class="ti ti-plus"></i> List event</button>
  </div>
</nav>

<!-- PAGE: MARKETPLACE -->
<div id="page-marketplace" class="page active">
  <div class="stat-grid">
    <div class="stat"><div class="stat-val" id="s-offers">24</div><div class="stat-lbl">Open offers</div></div>
    <div class="stat"><div class="stat-val" id="s-orgs">18</div><div class="stat-lbl">Organizations</div></div>
    <div class="stat"><div class="stat-val" id="s-deals">7</div><div class="stat-lbl">Active deals</div></div>
    <div class="stat"><div class="stat-val">৳12.4L</div><div class="stat-lbl">Total value listed</div></div>
  </div>
  <div class="section-hdr">
    <span class="section-title">Sponsor offers</span>
    <span id="offer-count" style="font-size:12px;color:var(--text2)"></span>
  </div>
  <div class="filters" id="offer-filters">
    <div class="pill active" onclick="filterOffers('all',this)">All types</div>
    <div class="pill" onclick="filterOffers('cash',this)">Cash</div>
    <div class="pill" onclick="filterOffers('inkind',this)">In-kind</div>
    <div class="pill" onclick="filterOffers('promo',this)">Promotional</div>
    <div class="pill" onclick="filterOffers('media',this)">Media</div>
  </div>
  <div id="offers-grid" class="grid-2"></div>
</div>

<!-- PAGE: ORGANIZATIONS -->
<div id="page-organizations" class="page">
  <div class="section-hdr">
    <span class="section-title">Events &amp; organizations seeking sponsors</span>
    <span id="org-count" style="font-size:12px;color:var(--text2)"></span>
  </div>
  <div class="filters" id="org-filters">
    <div class="pill active" onclick="filterOrgs('all',this)">All events</div>
    <div class="pill" onclick="filterOrgs('competition',this)">Competition</div>
    <div class="pill" onclick="filterOrgs('conference',this)">Conference</div>
    <div class="pill" onclick="filterOrgs('festival',this)">Festival</div>
    <div class="pill" onclick="filterOrgs('hackathon',this)">Hackathon</div>
  </div>
  <div id="orgs-grid" class="grid-2"></div>
</div>

<!-- PAGE: MATCHES -->
<div id="page-matches" class="page">
  <div class="section-hdr">
    <span class="section-title">Top compatibility matches</span>
    <span style="font-size:12px;color:var(--text2)">Ranked by alignment score</span>
  </div>
  <div id="matches-list"></div>
</div>

<!-- PAGE: ACTIVE DEALS -->
<div id="page-deals" class="page">
  <div class="section-hdr">
    <span class="section-title">Active deals in progress</span>
    <span style="font-size:12px;color:var(--text2)" id="deal-count"></span>
  </div>
  <div id="deals-list"></div>
</div>

<!-- PAGE: DEAL ROOMS -->
<div id="page-dealroom" class="page" style="max-width:1100px">
  <div class="dealroom-wrap" id="dealroom-wrap">
    <div class="sidebar">
      <div class="sb-hdr">
        <div class="sb-title">Deal rooms <span id="room-badge" style="background:var(--blue);color:#fff;font-size:11px;padding:2px 7px;border-radius:10px"></span></div>
        <div class="sb-search" style="margin-top:8px">
          <i class="ti ti-search"></i>
          <input placeholder="Search rooms…" oninput="filterRooms(this.value)" id="room-search">
        </div>
      </div>
      <div class="room-list" id="room-list"></div>
    </div>
    <div class="main-col" id="main-col">
      <div class="room-hdr" id="room-hdr"></div>
      <div class="pipe-bar" id="pipe-bar"></div>
      <div class="counter-modal" id="counter-modal">
        <div class="counter-title">Send counter-offer <button onclick="closeCounter()" style="background:none;border:none;cursor:pointer;color:var(--text2);font-size:18px;line-height:1"><i class="ti ti-x"></i></button></div>
        <div class="counter-grid">
          <div class="cg"><label>Cash amount (BDT)</label><input id="cnt-cash" placeholder="e.g. ৳80,000"></div>
          <div class="cg"><label>Non-monetary offer</label><input id="cnt-nonmon" placeholder="e.g. 3 social posts"></div>
          <div class="cg"><label>Branding placement</label><input id="cnt-brand" placeholder="e.g. Stage + t-shirts"></div>
          <div class="cg"><label>Additional ask</label><input id="cnt-ask" placeholder="e.g. Speaking slot"></div>
        </div>
        <button onclick="sendCounter()" style="width:100%;padding:7px;background:var(--purple-text);color:#fff;border:none;border-radius:var(--radius);cursor:pointer;font-size:13px;font-weight:500">Send counter-offer</button>
      </div>
      <div class="chat-area" id="chat-area"></div>
      <div class="input-area">
        <div class="toolbar">
          <button class="tool-btn" title="Attach file" onclick="attachFile()"><i class="ti ti-paperclip"></i></button>
          <button class="tool-btn" title="Send proposal" onclick="sendProposalMsg()"><i class="ti ti-file-description"></i></button>
          <button class="tool-btn" title="Make offer" onclick="toggleCounter()"><i class="ti ti-receipt"></i></button>
          <button class="tool-btn" title="Advance stage" onclick="advanceStage()"><i class="ti ti-circle-check"></i></button>
          <span style="font-size:11px;color:var(--text3);margin-left:4px">Attach · Proposal · Offer · Advance stage</span>
        </div>
        <div class="input-row">
          <textarea id="msg-input" placeholder="Type a message…" rows="1" onkeydown="handleKey(event)" oninput="autoResize(this)"></textarea>
          <button class="send-btn" onclick="sendMessage()"><i class="ti ti-send"></i> Send</button>
        </div>
      </div>
    </div>
    <div class="side-panel" id="side-panel">
      <div class="sp-hdr">Deal info <button onclick="togglePanel()" style="background:none;border:none;cursor:pointer;color:var(--text2);font-size:18px;line-height:1"><i class="ti ti-x"></i></button></div>
      <div id="sp-content" style="overflow-y:auto"></div>
    </div>
  </div>
</div>

<!-- MODAL: Post Offer -->
<div class="modal-overlay" id="modal-company" onclick="if(event.target===this)closeModal('company')">
  <div class="modal">
    <div class="modal-hdr"><div class="modal-title">Post a sponsorship offer</div><button class="close-x" onclick="closeModal('company')"><i class="ti ti-x"></i></button></div>
    <div class="form-row">
      <div class="fg"><label>Company name *</label><input id="c-name" placeholder="e.g. Grameenphone"></div>
      <div class="fg"><label>Industry</label><select id="c-industry"><option>Telecom</option><option>Banking</option><option>Tech</option><option>FMCG</option><option>Retail</option><option>Media</option><option>Fintech</option><option>Other</option></select></div>
    </div>
    <div class="form-row">
      <div class="fg"><label>Offer type</label><select id="c-type"><option value="cash">Cash sponsorship</option><option value="inkind">In-kind support</option><option value="promo">Promotional partnership</option><option value="media">Media coverage</option></select></div>
      <div class="fg"><label>Value / description</label><input id="c-value" placeholder="e.g. ৳50,000 or 'Print ads'"></div>
    </div>
    <div class="form-row"><div class="fg"><label>What you offer</label><textarea id="c-offer" placeholder="Describe what your company provides…"></textarea></div></div>
    <div class="form-row"><div class="fg"><label>What you want in return</label><textarea id="c-want" placeholder="Branding, social posts, speaking slot…"></textarea></div></div>
    <div class="form-row">
      <div class="fg"><label>Target audience</label><input id="c-audience" placeholder="Students, young professionals…"></div>
      <div class="fg"><label>Min. audience size</label><input id="c-minaud" type="number" placeholder="e.g. 500"></div>
    </div>
    <div class="form-actions"><button class="btn" onclick="closeModal('company')">Cancel</button><button class="btn btn-primary" onclick="submitOffer()">Post offer</button></div>
  </div>
</div>

<!-- MODAL: List Event -->
<div class="modal-overlay" id="modal-org" onclick="if(event.target===this)closeModal('org')">
  <div class="modal">
    <div class="modal-hdr"><div class="modal-title">List your event or organization</div><button class="close-x" onclick="closeModal('org')"><i class="ti ti-x"></i></button></div>
    <div class="form-row">
      <div class="fg"><label>Event / Organization name *</label><input id="o-name" placeholder="e.g. BUET Case Competition 2025"></div>
      <div class="fg"><label>Type</label><select id="o-type"><option value="competition">Business competition</option><option value="conference">Conference</option><option value="festival">Cultural festival</option><option value="hackathon">Hackathon</option><option value="other">Other</option></select></div>
    </div>
    <div class="form-row">
      <div class="fg"><label>University / Institution</label><input id="o-uni" placeholder="e.g. BUET"></div>
      <div class="fg"><label>Expected attendance</label><input id="o-att" type="number" placeholder="e.g. 800"></div>
    </div>
    <div class="form-row"><div class="fg"><label>What you offer sponsors</label><textarea id="o-offering" placeholder="Logo on materials, social media, booth space, MC mention…"></textarea></div></div>
    <div class="form-row"><div class="fg"><label>What you need from sponsors</label><textarea id="o-need" placeholder="Cash for venue, printing, food, prizes, or in-kind…"></textarea></div></div>
    <div class="form-row">
      <div class="fg"><label>Event date</label><input type="date" id="o-date"></div>
      <div class="fg"><label>Budget gap (BDT)</label><input id="o-gap" placeholder="e.g. ৳1,50,000"></div>
    </div>
    <div class="form-actions"><button class="btn" onclick="closeModal('org')">Cancel</button><button class="btn btn-primary" onclick="submitOrg()">List event</button></div>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<script>
const AV_CLS = ['av-blue','av-teal','av-amber','av-purple','av-coral','av-green'];
const STAGES = ['Matched','Proposal','Negotiation','Contract','Done'];
const STAGE_CLS = ['s-matched','s-proposal','s-negotiation','s-contract','s-done'];
const TYPE_ICON = {competition:'🏆',conference:'🎤',festival:'🎉',hackathon:'💻',other:'📋'};

function av(init, idx, size) {
  size = size || 36;
  return `<div class="avatar ${AV_CLS[idx % AV_CLS.length]}" style="width:${size}px;height:${size}px;font-size:${size===26?10:12}px">${init.slice(0,2).toUpperCase()}</div>`;
}
function badgeType(t) {
  const map = {cash:'badge-cash 💵 Cash',inkind:'badge-inkind 📦 In-kind',promo:'badge-promo 📣 Promo',media:'badge-media 🎬 Media'};
  const p = (map[t]||'badge-cash '+t).split(' ');
  return `<span class="badge ${p[0]}">${p.slice(1).join(' ')}</span>`;
}
function stagePill(s) {
  return `<span class="stage-pill ${STAGE_CLS[s]}">${STAGES[s]}</span>`;
}
function toast(msg) {
  const el = document.getElementById('toast');
  el.textContent = msg; el.classList.add('show');
  clearTimeout(el._t); el._t = setTimeout(() => el.classList.remove('show'), 2800);
}

// ── DATA ──────────────────────────────────────────────────────────────────────

let offers = [
  {id:1,company:'Grameenphone',industry:'Telecom',type:'cash',value:'৳1,00,000',offer:'Main title sponsor cash grant',want:'Logo on all banners, social posts, 2 speaking slots',audience:'Students',minAud:500,hot:true},
  {id:2,company:'Dutch Bangla Bank',industry:'Banking',type:'cash',value:'৳75,000',offer:'Cash for venue & logistics',want:'Logo placement, ATM booth at venue',audience:'University students',minAud:300,hot:false},
  {id:3,company:'Shajgoj',industry:'FMCG',type:'inkind',value:'Product hampers',offer:'Gift hampers for 100 winners',want:'Instagram mention, product placement',audience:'Young women',minAud:200,hot:false},
  {id:4,company:'Prothom Alo',industry:'Media',type:'media',value:'Print + digital coverage',offer:'Full-page ad + online article',want:'Event co-branding, media partner tag',audience:'General',minAud:1000,hot:true},
  {id:5,company:'Daraz',industry:'Retail',type:'promo',value:'Vouchers worth ৳50,000',offer:'Daraz shopping vouchers as prizes',want:'Booth at venue, social media tags',audience:'All students',minAud:400,hot:false},
  {id:6,company:'Khaas Food',industry:'FMCG',type:'inkind',value:'Food & beverages',offer:'Free catering for up to 300 people',want:'Logo on stage backdrop, story mention',audience:'Youth',minAud:200,hot:false},
  {id:7,company:'SSL Wireless',industry:'Tech',type:'cash',value:'৳40,000',offer:'Tech innovation track cash prize',want:'Tech partner branding, demo booth',audience:'Tech students',minAud:150,hot:false},
  {id:8,company:'Robi Axiata',industry:'Telecom',type:'promo',value:'Social reach 2M+',offer:'Social media campaign co-promotion',want:'Co-branding, hashtag campaign',audience:'18–25',minAud:500,hot:false},
  {id:9,company:'BRAC Bank',industry:'Banking',type:'cash',value:'৳60,000',offer:'Entrepreneurship award fund',want:'Branding, panel seat',audience:'Entrepreneurs',minAud:300,hot:false},
  {id:10,company:'Nagad',industry:'Fintech',type:'promo',value:'QR & digital exposure',offer:'Payment partner + digital promo',want:'Payment integration, branding',audience:'Students',minAud:200,hot:false},
  {id:11,company:'BTV',industry:'Media',type:'media',value:'TV broadcast slot',offer:'15-min feature on national TV',want:'Media partner, exclusive rights',audience:'National',minAud:2000,hot:true},
  {id:12,company:'Meena Bazar',industry:'Retail',type:'inkind',value:'Grocery hampers',offer:'Hampers for top 50 participants',want:'Social posts, banner',audience:'Families',minAud:200,hot:false},
];

let orgs = [
  {id:1,name:'IBA BizCase Nationals 2025',uni:'University of Dhaka – IBA',type:'competition',att:1200,offering:'Stage branding, social 10K reach, certificate, 5 MC mentions',need:'Cash for prizes & venue, media',date:'2025-09-20',gap:'৳2,00,000'},
  {id:2,name:'BUET Techfest',uni:'BUET',type:'hackathon',att:600,offering:'Booth, logo on shirts, tech session slot',need:'Cash for equipment & food, tech prizes',date:'2025-10-05',gap:'৳1,20,000'},
  {id:3,name:'NSU Business Carnival',uni:'North South University',type:'festival',att:2000,offering:'Full stage branding, VIP table, social media partner',need:'Cash + food catering + media',date:'2025-11-10',gap:'৳3,50,000'},
  {id:4,name:'BRACU Marketing Summit',uni:'BRAC University',type:'conference',att:400,offering:'Speaking slot, brochure ad, LinkedIn post',need:'Cash for venue, printing',date:'2025-08-15',gap:'৳80,000'},
  {id:5,name:'DU Case Competition',uni:'University of Dhaka',type:'competition',att:800,offering:'Logo on all creatives, social mention, 3 judging seats',need:'Cash for prizes, food & beverage',date:'2025-09-01',gap:'৳1,50,000'},
  {id:6,name:'AIUB CultureFest',uni:'AIUB',type:'festival',att:3000,offering:'Mega banner, stage logo, sponsored stalls, social reach 20K',need:'Food & beverages in-kind, cash',date:'2025-12-01',gap:'৳4,00,000'},
  {id:7,name:'SUST Startup Expo',uni:'SUST',type:'conference',att:500,offering:'Startup partner logo, panel seat, Instagram post',need:'Media coverage, cash for logistics',date:'2025-10-20',gap:'৳90,000'},
  {id:8,name:'UIU Hackathon',uni:'UIU',type:'hackathon',att:350,offering:'Tech partner branding, session host slot',need:'Tech prizes, venue funding',date:'2025-09-28',gap:'৳70,000'},
];

const matches = [
  {oi:0,ori:0,score:94,reasons:['Both target 500+ student audience','Cash offer matches cash need','IBA has national media reach for GP branding']},
  {oi:3,ori:2,score:91,reasons:['PA media coverage fits NSU Carnival scale','2000+ audience exceeds PA minimum','Co-branding aligns with both goals']},
  {oi:1,ori:4,score:87,reasons:['DBBL cash offer vs DU cash need','Banking audience matches student demographics','ATM booth works at DU campus event']},
  {oi:6,ori:1,score:85,reasons:['SSL Wireless tech prize aligns with BUET Techfest','Both target tech students','Demo booth fits hackathon format']},
  {oi:4,ori:5,score:82,reasons:['Daraz voucher prizes suit festival format','3000 attendees well above 400 minimum','Booth + social tags easily deliverable']},
  {oi:5,ori:2,score:80,reasons:['Khaas Food catering suits 2000-person event','Food need explicitly listed by NSU','Stage backdrop branding is available']},
];

let deals = [
  {company:'Grameenphone',org:'IBA BizCase Nationals',type:'cash',value:'৳1,00,000',stage:2},
  {company:'Prothom Alo',org:'NSU Business Carnival',type:'media',value:'Print + digital',stage:3},
  {company:'Dutch Bangla Bank',org:'DU Case Competition',type:'cash',value:'৳60,000',stage:1},
  {company:'SSL Wireless',org:'BUET Techfest',type:'cash',value:'৳40,000',stage:4},
  {company:'Khaas Food',org:'NSU Business Carnival',type:'inkind',value:'Catering 300',stage:2},
  {company:'BRAC Bank',org:'BRACU Marketing Summit',type:'cash',value:'৳60,000',stage:3},
  {company:'Daraz',org:'AIUB CultureFest',type:'promo',value:'৳50,000 vouchers',stage:1},
];

let rooms = [
  {id:0,company:'Grameenphone',cInit:'GP',org:'IBA BizCase Nationals',oInit:'IB',stage:2,value:'৳1,00,000',type:'Cash',unread:2,
   details:{audience:'1200 students',date:'Sep 20, 2025',gap:'৳2,00,000',offering:'Stage logo, social 10K, 5 MC mentions',cc:'Rafiq Hassan, Partnerships Lead',co:'Nadia Islam, Event Director'},
   files:[{name:'GP_Sponsorship_Brief.pdf',size:'245 KB'},{name:'IBA_Event_Deck.pdf',size:'1.2 MB'}],
   msgs:[
     {type:'system',text:'Deal room opened — 94% compatibility match'},
     {side:'org',text:'Hello! We\'re excited about the possibility of having Grameenphone as our title sponsor. Our event last year had 900 attendees and this year we\'re expecting 1,200+.',time:'10:24 AM',init:'IB',idx:1},
     {side:'co',text:'Thank you for reaching out. We reviewed your event profile — the audience demographics align well with our student engagement campaign. Could you share your event deck?',time:'10:31 AM',init:'GP',idx:0},
     {side:'org',text:'Of course! I\'ve attached our event deck. We\'re offering title branding on all creatives, 5 MC mentions, and prominent stage backdrop placement.',time:'10:45 AM',init:'IB',idx:1},
     {type:'file',side:'org',name:'IBA_Event_Deck.pdf',size:'1.2 MB',time:'10:45 AM',init:'IB',idx:1},
     {side:'co',text:'Great deck. Our standard title sponsorship is ৳1,00,000 in exchange for logo exclusivity across all printed materials and 3 social posts tagging our student campaign.',time:'11:02 AM',init:'GP',idx:0},
     {type:'offer',side:'co',cash:'৳1,00,000',nonmon:'—',brand:'All printed materials + stage backdrop',ask:'Logo exclusivity + 3 social posts',time:'11:03 AM',init:'GP',idx:0},
     {side:'org',text:'We appreciate the offer! Could we negotiate on the exclusivity clause? We have two other confirmed sponsors in the printing category already.',time:'11:20 AM',init:'IB',idx:1},
   ]},
  {id:1,company:'Prothom Alo',cInit:'PA',org:'NSU Business Carnival',oInit:'NS',stage:3,value:'Print + digital',type:'Media',unread:0,
   details:{audience:'2000 students',date:'Nov 10, 2025',gap:'৳3,50,000',offering:'Full stage branding, VIP table, media partner badge',cc:'Sumaiya Khan, Marketing Manager',co:'Farhan Chowdhury, President'},
   files:[{name:'PA_MediaKit_2025.pdf',size:'3.1 MB'},{name:'NSU_Carnival_Proposal.pdf',size:'890 KB'}],
   msgs:[
     {type:'system',text:'Deal room opened — 91% compatibility match'},
     {side:'co',text:'We\'re keen on co-branding NSU Carnival as our media partner event this year. Our print + digital package would give the event national exposure.',time:'9:10 AM',init:'PA',idx:2},
     {side:'org',text:'That would be incredible for us. Prothom Alo\'s brand recognition would add huge credibility. What does the media package include exactly?',time:'9:18 AM',init:'NS',idx:3},
     {side:'co',text:'A full-page feature in our weekend print edition (500K circulation), an article on prothomalo.com, and 2 Facebook posts to our 8M followers.',time:'9:25 AM',init:'PA',idx:2},
     {type:'file',side:'co',name:'PA_MediaKit_2025.pdf',size:'3.1 MB',time:'9:26 AM',init:'PA',idx:2},
     {side:'org',text:'Perfect. We\'re offering: "Media Partner — Prothom Alo" badge on all event materials, a VIP table for 6, and a 10-minute slot at the opening ceremony.',time:'9:40 AM',init:'NS',idx:3},
     {type:'offer',side:'org',cash:'—',nonmon:'Full-page print + online article',brand:'"Media Partner" on all creatives + VIP table',ask:'Prothom Alo branded content rights',time:'9:41 AM',init:'NS',idx:3},
     {side:'co',text:'We accept the terms. Please send the MOU draft and our legal team will review within 3 working days.',time:'10:05 AM',init:'PA',idx:2},
   ]},
  {id:2,company:'Dutch Bangla Bank',cInit:'DB',org:'DU Case Competition',oInit:'DU',stage:1,value:'৳75,000',type:'Cash',unread:1,
   details:{audience:'800 students',date:'Sep 1, 2025',gap:'৳1,50,000',offering:'Logo on all creatives, 3 judging seats, social mention',cc:'Imran Ali, CSR Head',co:'Tanvir Ahmed, Organizing Secretary'},
   files:[{name:'DU_CaseComp_Brief.pdf',size:'420 KB'}],
   msgs:[
     {type:'system',text:'Deal room opened — 87% compatibility match'},
     {side:'org',text:'Hi DBBL team! We\'d love to have Dutch Bangla Bank sponsor our annual case competition at Dhaka University. 800 students from 20+ universities will attend.',time:'2:10 PM',init:'DU',idx:4},
     {side:'co',text:'This sounds aligned with our university outreach program. Could you tell us more about the judging panel and visibility during the competition?',time:'2:35 PM',init:'DB',idx:5},
   ]},
  {id:3,company:'SSL Wireless',cInit:'SL',org:'BUET Techfest',oInit:'BT',stage:4,value:'৳40,000',type:'Cash',unread:0,
   details:{audience:'600 students',date:'Oct 5, 2025',gap:'৳1,20,000',offering:'Booth, logo on shirts, tech session host slot',cc:'Arif Hossain, BD Manager',co:'Protik Das, General Secretary'},
   files:[{name:'SSL_TechPartner_Agreement.pdf',size:'780 KB'},{name:'BUET_Techfest_Final.pdf',size:'1.5 MB'}],
   msgs:[
     {type:'system',text:'Deal room opened — 85% compatibility match'},
     {side:'co',text:'We\'re excited to be the tech partner for BUET Techfest! SSL Wireless has a strong history with BUET graduates.',time:'11:00 AM',init:'SL',idx:0},
     {side:'org',text:'Wonderful! Your demo booth will be in the main hall and we\'ll allocate a 45-minute session slot for your team.',time:'11:15 AM',init:'BT',idx:3},
     {side:'co',text:'Perfect. We\'re sending ৳40,000 as the tech prize fund. Can we get co-branding on the competition certificates as well?',time:'11:30 AM',init:'SL',idx:0},
     {side:'org',text:'"Powered by SSL Wireless" on all certificates — we\'ll include that in the MOU. Contract draft is being prepared.',time:'11:45 AM',init:'BT',idx:3},
     {type:'file',side:'org',name:'SSL_TechPartner_Agreement.pdf',size:'780 KB',time:'11:47 AM',init:'BT',idx:3},
     {side:'co',text:'Reviewed and approved on our end. Sending to legal for final sign-off.',time:'12:10 PM',init:'SL',idx:0},
   ]},
  {id:4,company:'Khaas Food',cInit:'KF',org:'NSU Business Carnival',oInit:'NS',stage:2,value:'Catering 300',type:'In-kind',unread:3,
   details:{audience:'2000 students',date:'Nov 10, 2025',gap:'৳3,50,000',offering:'Stage logo, story mention, pamphlet ad',cc:'Mehnaz Begum, Marketing',co:'Farhan Chowdhury, President'},
   files:[],
   msgs:[
     {type:'system',text:'Deal room opened — 80% compatibility match'},
     {side:'org',text:'Hi Khaas Food! We\'re organizing NSU Business Carnival for 2,000 attendees. Your in-kind catering offer is a perfect fit.',time:'4:00 PM',init:'NS',idx:3},
     {side:'co',text:'We love supporting university events. We can provide full catering for up to 300 people — snacks, drinks, and a meal package. What\'s the event schedule?',time:'4:15 PM',init:'KF',idx:5},
     {side:'org',text:'The event runs 9 AM – 6 PM on Nov 10. We were thinking breakfast snacks + lunch for the core team (300 people) and packaged snacks for all 2000 attendees.',time:'4:28 PM',init:'NS',idx:3},
   ]},
  {id:5,company:'BRAC Bank',cInit:'BB',org:'BRACU Marketing Summit',oInit:'BM',stage:3,value:'৳60,000',type:'Cash',unread:0,
   details:{audience:'400 students',date:'Aug 15, 2025',gap:'৳80,000',offering:'Speaking slot, brochure ad, LinkedIn post',cc:'Zahid Hasan, Sponsorships',co:'Raisa Kabir, Summit Director'},
   files:[{name:'BRACU_Summit_MOU_Draft.pdf',size:'560 KB'}],
   msgs:[
     {type:'system',text:'Deal room opened — match via direct outreach'},
     {side:'org',text:'Hi BRAC Bank, we\'d love to feature you as our banking partner for the Marketing Summit — 30-minute keynote slot to 400 marketing students.',time:'8:30 AM',init:'BM',idx:4},
     {side:'co',text:'This is exactly the engagement we look for. ৳60,000 works for us. We\'d like the keynote to focus on fintech and career opportunities at BRAC Bank.',time:'9:00 AM',init:'BB',idx:2},
     {side:'org',text:'Absolutely. Full-page ad in our Summit brochure (500 copies) and a LinkedIn post to our 3K followers. MOU draft attached.',time:'9:20 AM',init:'BM',idx:4},
     {type:'file',side:'org',name:'BRACU_Summit_MOU_Draft.pdf',size:'560 KB',time:'9:21 AM',init:'BM',idx:4},
     {side:'co',text:'MOU looks good overall. One change: we need a clause allowing us to collect student CVs via a form at our booth. Is that acceptable?',time:'10:05 AM',init:'BB',idx:2},
   ]},
  {id:6,company:'Daraz',cInit:'DZ',org:'AIUB CultureFest',oInit:'AC',stage:1,value:'৳50,000 vouchers',type:'Promo',unread:1,
   details:{audience:'3000 students',date:'Dec 1, 2025',gap:'৳4,00,000',offering:'Mega banner, stage logo, sponsored stalls',cc:'Lubna Morshed, Campaigns',co:'Shafiq Rahman, Cultural Secretary'},
   files:[],
   msgs:[
     {type:'system',text:'Deal room opened — 82% compatibility match'},
     {side:'co',text:'Hi AIUB! Daraz would like to participate in CultureFest as a promotional partner — ৳50,000 in shopping vouchers as prizes and a branded stall.',time:'3:00 PM',init:'DZ',idx:0},
     {side:'org',text:'Welcome! With 3,000 attendees, it\'s great exposure. Can the vouchers be distributed as lucky draw prizes throughout the day?',time:'3:30 PM',init:'AC',idx:5},
   ]},
];

// ── FILTERS ───────────────────────────────────────────────────────────────────

let offerFilter = 'all', orgFilter = 'all';

function filterOffers(type, el) {
  document.querySelectorAll('#offer-filters .pill').forEach(p => p.classList.remove('active'));
  el.classList.add('active'); offerFilter = type;
  renderOffers(type === 'all' ? offers : offers.filter(o => o.type === type));
}
function filterOrgs(type, el) {
  document.querySelectorAll('#org-filters .pill').forEach(p => p.classList.remove('active'));
  el.classList.add('active'); orgFilter = type;
  renderOrgs(type === 'all' ? orgs : orgs.filter(o => o.type === type));
}

// ── RENDERERS ─────────────────────────────────────────────────────────────────

function renderOffers(list) {
  document.getElementById('offer-count').textContent = list.length + ' listings';
  document.getElementById('offers-grid').innerHTML = list.length ? list.map((o, i) => `
    <div class="card">
      <div class="card-hdr">
        <div style="display:flex;gap:10px;align-items:center">${av(o.company, i)}<div>
          <div class="card-title">${o.company}</div>
          <div class="card-sub">${o.industry}${o.hot ? ' · <span style="color:var(--amber-text)">Hot offer</span>' : ''}</div>
        </div></div>${badgeType(o.type)}
      </div>
      <div style="font-size:14px;font-weight:500;margin-bottom:4px">${o.value}</div>
      <div style="font-size:12px;color:var(--text2);margin-bottom:8px">${o.offer}</div>
      <div class="detail-row"><i class="ti ti-target"></i>${o.want}</div>
      <div class="detail-row"><i class="ti ti-users"></i>Min ${o.minAud.toLocaleString()} attendees · ${o.audience}</div>
      <hr class="divider">
      <div style="display:flex;gap:6px">
        <button class="btn btn-sm" style="flex:1" onclick="toast('Interest sent to ${o.company}!')">Express interest</button>
        <button class="btn btn-sm" onclick="toast('${o.company} saved!')"><i class="ti ti-bookmark"></i></button>
      </div>
    </div>`) .join('') : '<div class="empty"><i class="ti ti-search"></i>No offers match this filter</div>';
}

function renderOrgs(list) {
  document.getElementById('org-count').textContent = list.length + ' events';
  document.getElementById('orgs-grid').innerHTML = list.length ? list.map((o, i) => `
    <div class="card">
      <div class="card-hdr">
        <div style="display:flex;gap:10px;align-items:center">${av(o.name, i+3)}<div>
          <div class="card-title">${o.name}</div>
          <div class="card-sub">${o.uni}</div>
        </div></div>
        <span class="badge" style="background:var(--bg2);color:var(--text2)">${TYPE_ICON[o.type]||'📋'} ${o.type}</span>
      </div>
      <div class="detail-row" style="margin-top:0"><strong style="color:var(--text);font-size:12px">Offering:</strong></div>
      <div style="font-size:12px;color:var(--text2);margin-bottom:6px">${o.offering}</div>
      <div class="detail-row" style="margin-top:0"><strong style="color:var(--text);font-size:12px">Need:</strong></div>
      <div style="font-size:12px;color:var(--text2);margin-bottom:8px">${o.need}</div>
      <div style="display:flex;gap:12px;flex-wrap:wrap">
        <div class="detail-row"><i class="ti ti-users"></i>${o.att.toLocaleString()} expected</div>
        <div class="detail-row"><i class="ti ti-calendar"></i>${o.date}</div>
        <div class="detail-row"><i class="ti ti-cash"></i>Gap: ${o.gap}</div>
      </div>
      <hr class="divider">
      <button class="btn btn-sm" style="width:100%" onclick="toast('Proposal sent to ${o.name}!')">Contact organizers</button>
    </div>`).join('') : '<div class="empty"><i class="ti ti-search"></i>No events match this filter</div>';
}

function renderMatches() {
  document.getElementById('matches-list').innerHTML = matches.map(m => {
    const o = offers[m.oi], org = orgs[m.ori];
    return `<div class="match-card">
      <div class="match-score">✦ ${m.score}% match</div>
      <div style="display:grid;grid-template-columns:1fr 28px 1fr;gap:10px;align-items:center">
        <div>
          <div style="font-size:10px;color:var(--text2);margin-bottom:4px;font-weight:600;letter-spacing:.4px">SPONSOR</div>
          <div style="font-size:14px;font-weight:500">${o.company}</div>
          <div style="font-size:12px;color:var(--text2);margin-top:2px">${badgeType(o.type)} ${o.value}</div>
        </div>
        <div style="text-align:center;font-size:20px;color:var(--teal)">⇄</div>
        <div>
          <div style="font-size:10px;color:var(--text2);margin-bottom:4px;font-weight:600;letter-spacing:.4px">ORGANIZATION</div>
          <div style="font-size:14px;font-weight:500">${org.name}</div>
          <div style="font-size:12px;color:var(--text2);margin-top:2px">${org.uni} · ${org.att.toLocaleString()} att.</div>
        </div>
      </div>
      <div class="match-bar"><div class="match-fill" style="width:${m.score}%"></div></div>
      <div style="margin-top:8px;display:flex;gap:6px;flex-wrap:wrap">${m.reasons.map(r => `<span class="tag"><i class="ti ti-check" style="font-size:12px;color:var(--teal)"></i>${r}</span>`).join('')}</div>
      <hr class="divider">
      <div style="display:flex;gap:6px">
        <button class="btn btn-sm" style="flex:1" onclick="toast('Introduction sent between ${o.company} and ${org.name}!')">Connect them</button>
        <button class="btn btn-sm" onclick="toast('Match saved!')"><i class="ti ti-bookmark"></i></button>
      </div>
    </div>`;
  }).join('');
}

function renderDeals() {
  document.getElementById('deal-count').textContent = deals.length + ' deals';
  document.getElementById('deals-list').innerHTML = deals.map((d, i) => `
    <div class="deal-card">
      <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px">
        <div>
          <div style="font-size:14px;font-weight:500">${d.company} × ${d.org}</div>
          <div style="font-size:12px;color:var(--text2);margin-top:2px">${badgeType(d.type)} · ${d.value}</div>
        </div>
        ${stagePill(d.stage)}
      </div>
      <div class="pipeline">${STAGES.map((s, si) => `<div class="p-step">
        <div class="p-dot${si < d.stage ? ' done' : si === d.stage ? ' current' : ''}">${si < d.stage ? '<i class="ti ti-check" style="font-size:9px"></i>' : si+1}</div>
        <div class="p-lbl${si === d.stage ? ' current' : ''}">${s}</div>
      </div>`).join('')}</div>
      <button class="btn btn-sm" onclick="advanceDeal(${i})">Advance stage</button>
    </div>`).join('');
}

function advanceDeal(i) {
  if (deals[i].stage >= 4) { toast('Deal complete!'); return; }
  deals[i].stage++;
  toast(`Advanced to "${STAGES[deals[i].stage]}"`);
  renderDeals();
}

// ── DEAL ROOM ─────────────────────────────────────────────────────────────────

let activeRoom = 0, panelOpen = false;

function renderRoomList(list) {
  document.getElementById('room-badge').textContent = rooms.reduce((a, r) => a + (r.unread || 0), 0) || rooms.length;
  document.getElementById('room-list').innerHTML = list.map(r => `
    <div class="room-item${r.id === activeRoom ? ' active' : ''}" onclick="openRoom(${r.id})">
      <div class="room-top">
        <div class="room-name">${r.company} × ${r.org.split(' ').slice(0,3).join(' ')}${r.unread ? '<span class="unread-dot"></span>' : ''}</div>
        <div class="room-time">${r.unread && r.msgs.length ? (r.msgs[r.msgs.length-1].time||'') : ''}</div>
      </div>
      <div class="room-preview">${r.msgs[r.msgs.length-1].text || r.msgs[r.msgs.length-1].name || 'File shared'}</div>
      ${stagePill(r.stage)}
    </div>`).join('');
}

function filterRooms(q) {
  const f = q ? rooms.filter(r => (r.company + r.org).toLowerCase().includes(q.toLowerCase())) : rooms;
  renderRoomList(f);
}

function openRoom(id) {
  activeRoom = id;
  rooms.find(r => r.id === id).unread = 0;
  renderRoomList(rooms);
  renderRoomHeader();
  renderPipeBar();
  renderChat();
  document.getElementById('counter-modal').classList.remove('open');
  if (panelOpen) renderPanel();
}

function renderRoomHeader() {
  const r = rooms.find(x => x.id === activeRoom);
  document.getElementById('room-hdr').innerHTML = `
    <div class="room-hdr-left">
      <div style="display:flex;gap:4px">
        ${av(r.cInit, r.id, 30)}${av(r.oInit, (r.id+2)%6, 30)}
      </div>
      <div>
        <div class="room-hdr-title">${r.company} × ${r.org}</div>
        <div class="room-hdr-sub">${r.type} · ${r.value} · ${stagePill(r.stage)}</div>
      </div>
    </div>
    <div class="hdr-actions">
      <button class="icon-btn" onclick="advanceStage()"><i class="ti ti-circle-check"></i> Advance</button>
      <button class="icon-btn" onclick="togglePanel()"><i class="ti ti-info-circle"></i> Info</button>
    </div>`;
}

function renderPipeBar() {
  const r = rooms.find(x => x.id === activeRoom);
  document.getElementById('pipe-bar').innerHTML = STAGES.map((s, i) => `
    <div class="p-step">
      <div class="p-dot${i < r.stage ? ' done' : i === r.stage ? ' current' : ''}">${i < r.stage ? '<i class="ti ti-check" style="font-size:9px"></i>' : i+1}</div>
      <div class="p-lbl${i === r.stage ? ' current' : ''}">${s}</div>
    </div>`).join('');
}

function renderChat() {
  const r = rooms.find(x => x.id === activeRoom);
  const ca = document.getElementById('chat-area');
  ca.innerHTML = r.msgs.map((m, mi) => {
    if (m.type === 'system') return `<div class="system-msg"><span>${m.text}</span></div>`;
    const mine = m.side === 'org';
    const avEl = `<div class="msg-av ${AV_CLS[m.idx % AV_CLS.length]}">${m.init}</div>`;
    if (m.type === 'file') return `<div class="msg-row${mine ? ' mine' : ''}">
      ${!mine ? avEl : ''}
      <div>${mine ? '' : ''}<div class="doc-bubble" onclick="toast('Opening ${m.name}')">
        <div class="doc-title"><i class="ti ti-file-text" style="font-size:16px;color:var(--blue)"></i>${m.name}</div>
        <div class="doc-sub">${m.size} · Click to open</div>
      </div><div class="msg-meta">${m.time||''}</div></div>
      ${mine ? avEl : ''}
    </div>`;
    if (m.type === 'offer') return `<div class="msg-row${mine ? ' mine' : ''}">
      ${!mine ? avEl : ''}
      <div><div class="offer-bubble">
        <div class="offer-label"><i class="ti ti-receipt" style="font-size:12px"></i> FORMAL OFFER</div>
        <div class="offer-grid">
          <div class="offer-cell"><div class="offer-cell-lbl">Cash</div><div class="offer-cell-val">${m.cash}</div></div>
          <div class="offer-cell"><div class="offer-cell-lbl">Non-monetary</div><div class="offer-cell-val">${m.nonmon}</div></div>
          <div class="offer-cell"><div class="offer-cell-lbl">Branding given</div><div class="offer-cell-val">${m.brand}</div></div>
          <div class="offer-cell"><div class="offer-cell-lbl">In return</div><div class="offer-cell-val">${m.ask}</div></div>
        </div>
        ${!mine ? `<div class="offer-actions"><button class="accept-btn" onclick="acceptOffer(${mi})">Accept offer</button><button class="counter-btn" onclick="toggleCounter()">Counter</button></div>` : '<div style="font-size:11px;color:var(--teal-text)">Sent · awaiting response</div>'}
      </div><div class="msg-meta">${m.time||''}</div></div>
      ${mine ? avEl : ''}
    </div>`;
    return `<div class="msg-row${mine ? ' mine' : ''}">
      ${!mine ? avEl : ''}
      <div><div class="bubble">${m.text}</div><div class="msg-meta">${m.time||''}</div></div>
      ${mine ? avEl : ''}
    </div>`;
  }).join('');
  ca.scrollTop = ca.scrollHeight;
}

function renderPanel() {
  const r = rooms.find(x => x.id === activeRoom), d = r.details;
  document.getElementById('sp-content').innerHTML = `
    <div class="sp-section"><div class="sp-label">Deal value</div><div class="sp-val" style="font-size:16px;font-weight:600">${r.value}</div></div>
    <div class="sp-section"><div class="sp-label">Type</div><div class="sp-val">${r.type}</div></div>
    <div class="sp-section"><div class="sp-label">Event</div><div class="sp-val">${d.audience}<br>${d.date}</div></div>
    <div class="sp-section"><div class="sp-label">Org offering</div><div class="sp-val">${d.offering}</div></div>
    <div class="sp-section"><div class="sp-label">Contacts</div><div class="sp-val">${d.cc}<br><span style="color:var(--text2)">${r.company}</span><br><br>${d.co}<br><span style="color:var(--text2)">${r.org}</span></div></div>
    <div class="sp-section"><div class="sp-label">Shared files</div>
      ${r.files.length ? r.files.map(f => `<div class="sp-file" onclick="toast('Opening ${f.name}')"><i class="ti ti-file-text" style="font-size:16px;color:var(--blue)"></i><div class="sp-file-name">${f.name}</div><div class="sp-file-size">${f.size}</div></div>`).join('') : '<div style="font-size:12px;color:var(--text2)">No files yet</div>'}
    </div>`;
}

function togglePanel() {
  panelOpen = !panelOpen;
  const sp = document.getElementById('side-panel');
  if (panelOpen) { sp.classList.add('open'); renderPanel(); }
  else sp.classList.remove('open');
}

function advanceStage() {
  const r = rooms.find(x => x.id === activeRoom);
  if (r.stage >= 4) { toast('Deal is already complete!'); return; }
  r.stage++;
  r.msgs.push({ type: 'system', text: `Stage advanced to: ${STAGES[r.stage]}` });
  renderRoomList(rooms); renderRoomHeader(); renderPipeBar(); renderChat();
  if (panelOpen) renderPanel();
  toast(`Advanced to "${STAGES[r.stage]}" stage`);
}

function acceptOffer(msgIdx) {
  const r = rooms.find(x => x.id === activeRoom);
  r.msgs.push({ type: 'system', text: 'Offer accepted — moving to Contract stage' });
  if (r.stage < 3) r.stage = 3;
  renderRoomList(rooms); renderRoomHeader(); renderPipeBar(); renderChat();
  toast('Offer accepted! Stage advanced to Contract.');
}

function sendMessage() {
  const inp = document.getElementById('msg-input'), txt = inp.value.trim();
  if (!txt) return;
  const r = rooms.find(x => x.id === activeRoom);
  const now = new Date();
  const time = now.getHours() + ':' + String(now.getMinutes()).padStart(2, '0') + ' ' + (now.getHours() < 12 ? 'AM' : 'PM');
  r.msgs.push({ side: 'org', text: txt, time, init: r.oInit, idx: (r.id + 2) % 6 });
  inp.value = ''; inp.style.height = '38px';
  renderChat(); renderRoomList(rooms);
}

function handleKey(e) { if (e.key === 'Enter' && !e.shiftKey) { e.preventDefault(); sendMessage(); } }
function autoResize(el) { el.style.height = '38px'; el.style.height = Math.min(el.scrollHeight, 100) + 'px'; }

function attachFile() {
  const r = rooms.find(x => x.id === activeRoom);
  const files = ['Proposal_Draft.pdf','Budget_Breakdown.xlsx','Event_Schedule.pdf','Sponsorship_Tiers.pdf'];
  const sizes = ['340 KB','128 KB','560 KB','220 KB'];
  const idx = Math.floor(Math.random() * files.length);
  const now = new Date();
  const time = now.getHours() + ':' + String(now.getMinutes()).padStart(2, '0') + ' PM';
  r.msgs.push({ type: 'file', side: 'org', name: files[idx], size: sizes[idx], time, init: r.oInit, idx: (r.id + 2) % 6 });
  r.files.push({ name: files[idx], size: sizes[idx] });
  renderChat(); if (panelOpen) renderPanel();
  toast('File attached: ' + files[idx]);
}

function sendProposalMsg() {
  const r = rooms.find(x => x.id === activeRoom);
  const now = new Date();
  const time = now.getHours() + ':' + String(now.getMinutes()).padStart(2, '0') + ' PM';
  r.msgs.push({ side: 'org', text: 'Please find our formal sponsorship proposal attached. We believe this outlines a mutually beneficial partnership and look forward to your feedback.', time, init: r.oInit, idx: (r.id + 2) % 6 });
  r.msgs.push({ type: 'file', side: 'org', name: 'Sponsorship_Proposal_Final.pdf', size: '1.8 MB', time, init: r.oInit, idx: (r.id + 2) % 6 });
  renderChat(); toast('Proposal sent!');
}

function toggleCounter() { document.getElementById('counter-modal').classList.toggle('open'); }
function closeCounter() { document.getElementById('counter-modal').classList.remove('open'); }

function sendCounter() {
  const r = rooms.find(x => x.id === activeRoom);
  const now = new Date();
  const time = now.getHours() + ':' + String(now.getMinutes()).padStart(2, '0') + ' PM';
  r.msgs.push({
    type: 'offer', side: 'org',
    cash: document.getElementById('cnt-cash').value || '—',
    nonmon: document.getElementById('cnt-nonmon').value || '—',
    brand: document.getElementById('cnt-brand').value || '—',
    ask: document.getElementById('cnt-ask').value || '—',
    time, init: r.oInit, idx: (r.id + 2) % 6
  });
  closeCounter(); renderChat(); toast('Counter-offer sent!');
}

// ── MODALS ────────────────────────────────────────────────────────────────────

function openModal(t) { document.getElementById('modal-' + t).classList.add('open'); }
function closeModal(t) { document.getElementById('modal-' + t).classList.remove('open'); }

function submitOffer() {
  const name = document.getElementById('c-name').value.trim();
  if (!name) { toast('Please enter a company name'); return; }
  offers.unshift({
    id: offers.length + 1, company: name,
    industry: document.getElementById('c-industry').value,
    type: document.getElementById('c-type').value,
    value: document.getElementById('c-value').value || 'TBD',
    offer: document.getElementById('c-offer').value || 'Details TBD',
    want: document.getElementById('c-want').value || 'TBD',
    audience: document.getElementById('c-audience').value || 'General',
    minAud: parseInt(document.getElementById('c-minaud').value) || 100,
    hot: false
  });
  document.getElementById('s-offers').textContent = offers.length;
  closeModal('company');
  renderOffers(offerFilter === 'all' ? offers : offers.filter(o => o.type === offerFilter));
  toast('Offer posted by ' + name + '!');
}

function submitOrg() {
  const name = document.getElementById('o-name').value.trim();
  if (!name) { toast('Please enter an event name'); return; }
  orgs.unshift({
    id: orgs.length + 1, name,
    type: document.getElementById('o-type').value,
    uni: document.getElementById('o-uni').value || 'Unknown university',
    att: parseInt(document.getElementById('o-att').value) || 200,
    offering: document.getElementById('o-offering').value || 'Details TBD',
    need: document.getElementById('o-need').value || 'TBD',
    date: document.getElementById('o-date').value || 'TBD',
    gap: document.getElementById('o-gap').value || 'TBD'
  });
  document.getElementById('s-orgs').textContent = orgs.length;
  closeModal('org');
  renderOrgs(orgFilter === 'all' ? orgs : orgs.filter(o => o.type === orgFilter));
  toast('Event listed: ' + name + '!');
}

// ── PAGE SWITCHING ─────────────────────────────────────────────────────────────

function showPage(id, el) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  el.classList.add('active');
}

// ── INIT ──────────────────────────────────────────────────────────────────────

renderOffers(offers);
renderOrgs(orgs);
renderMatches();
renderDeals();
renderRoomList(rooms);
openRoom(0);
</script>
</body>
</html>
