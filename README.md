# divorce-model
Divorce Financial Model
[index.html](https://github.com/user-attachments/files/26313211/index.html.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Divorce Financial Model — Toby Salgado</title>
<style>
  :root {
    --bg: #0d1117; --surface: #161b22; --surface2: #1c2128; --border: #30363d;
    --text: #e6edf3; --muted: #8b949e; --accent: #58a6ff; --green: #3fb950;
    --red: #f85149; --yellow: #d29922; --orange: #e3b341; --purple: #bc8cff;
    --radius: 8px; --font: 'SF Mono','Fira Code','Consolas',monospace;
    --sans: -apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { background: var(--bg); color: var(--text); font-family: var(--sans); font-size: 14px; min-height: 100vh; }
  .header { background: var(--surface); border-bottom: 1px solid var(--border); padding: 12px 16px; position: sticky; top: 0; z-index: 100; }
  .header-top { display: flex; align-items: center; justify-content: space-between; gap: 8px; }
  .header h1 { font-size: 15px; font-weight: 600; white-space: nowrap; }
  .header .subtitle { font-size: 11px; color: var(--muted); margin-top: 2px; }
  .badge { background: var(--red); color: #fff; font-size: 10px; font-weight: 700; padding: 2px 6px; border-radius: 4px; white-space: nowrap; }
  .badge.green { background: var(--green); }
  .tab-nav { display: flex; overflow-x: auto; background: var(--surface); border-bottom: 1px solid var(--border); scrollbar-width: none; -webkit-overflow-scrolling: touch; }
  .tab-nav::-webkit-scrollbar { display: none; }
  .tab-btn { flex: 0 0 auto; padding: 10px 14px; font-size: 12px; font-weight: 500; color: var(--muted); background: none; border: none; border-bottom: 2px solid transparent; cursor: pointer; white-space: nowrap; transition: color .15s,border-color .15s; font-family: var(--sans); }
  .tab-btn:hover { color: var(--text); }
  .tab-btn.active { color: var(--accent); border-bottom-color: var(--accent); }
  .content { padding: 16px; max-width: 900px; margin: 0 auto; }
  .panel { display: none; }
  .panel.active { display: block; }
  .card { background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); margin-bottom: 12px; overflow: hidden; }
  .card-header { padding: 10px 14px; background: var(--surface2); border-bottom: 1px solid var(--border); font-size: 12px; font-weight: 600; color: var(--muted); text-transform: uppercase; letter-spacing: .5px; display: flex; align-items: center; justify-content: space-between; }
  .card-body { padding: 14px; }
  .data-table { width: 100%; border-collapse: collapse; }
  .data-table tr { border-bottom: 1px solid var(--border); }
  .data-table tr:last-child { border-bottom: none; }
  .data-table td { padding: 8px 0; font-size: 13px; vertical-align: top; line-height: 1.4; }
  .data-table td:last-child { text-align: right; font-family: var(--font); font-size: 12px; white-space: nowrap; padding-left: 8px; }
  .data-table .label { color: var(--muted); }
  .data-table .subtotal td { color: var(--text); font-weight: 600; border-top: 1px solid var(--border); padding-top: 10px; }
  .data-table .total td { color: var(--accent); font-weight: 700; font-size: 14px; border-top: 2px solid var(--accent); padding-top: 10px; }
  .data-table .pos { color: var(--green); }
  .data-table .neg { color: var(--red); }
  .data-table .warn { color: var(--yellow); }
  .stat-row { display: grid; grid-template-columns: repeat(2,1fr); gap: 10px; margin-bottom: 12px; }
  @media(min-width:480px){.stat-row{grid-template-columns:repeat(3,1fr);}}
  @media(min-width:700px){.stat-row{grid-template-columns:repeat(4,1fr);}}
  .stat { background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); padding: 12px; }
  .stat .s-label { font-size: 10px; color: var(--muted); text-transform: uppercase; letter-spacing: .5px; margin-bottom: 4px; }
  .stat .s-value { font-size: 18px; font-weight: 700; font-family: var(--font); }
  .stat .s-value.green { color: var(--green); }
  .stat .s-value.red { color: var(--red); }
  .stat .s-value.yellow { color: var(--yellow); }
  .stat .s-sub { font-size: 10px; color: var(--muted); margin-top: 2px; }
  .slider-group { background: var(--surface); border: 1px solid var(--border); border-radius: var(--radius); padding: 14px; margin-bottom: 10px; }
  .slider-label { display: flex; justify-content: space-between; align-items: baseline; margin-bottom: 8px; }
  .slider-label span:first-child { font-size: 12px; font-weight: 500; }
  .slider-val { font-family: var(--font); font-size: 13px; font-weight: 700; color: var(--accent); background: var(--surface2); padding: 2px 8px; border-radius: 4px; min-width: 80px; text-align: right; }
  input[type=range] { width: 100%; -webkit-appearance: none; height: 4px; border-radius: 2px; background: var(--border); outline: none; cursor: pointer; }
  input[type=range]::-webkit-slider-thumb { -webkit-appearance: none; width: 18px; height: 18px; border-radius: 50%; background: var(--accent); cursor: pointer; border: 2px solid var(--bg); box-shadow: 0 0 0 1px var(--accent); }
  input[type=range]::-moz-range-thumb { width: 18px; height: 18px; border-radius: 50%; background: var(--accent); cursor: pointer; border: 2px solid var(--bg); }
  .toggle-row { display: flex; border: 1px solid var(--border); border-radius: var(--radius); overflow: hidden; margin-bottom: 12px; }
  .toggle-btn { flex: 1; padding: 10px; font-size: 12px; font-weight: 600; background: var(--surface); color: var(--muted); border: none; cursor: pointer; transition: all .15s; font-family: var(--sans); }
  .toggle-btn.active { background: var(--accent); color: #fff; }
  .two-col { display: grid; grid-template-columns: 1fr; gap: 12px; }
  @media(min-width:600px){.two-col{grid-template-columns:1fr 1fr;}}
  .result-box { background: var(--surface2); border: 1px solid var(--border); border-radius: var(--radius); padding: 16px; margin-top: 12px; text-align: center; }
  .result-box .r-label { font-size: 11px; color: var(--muted); text-transform: uppercase; letter-spacing: .5px; margin-bottom: 6px; }
  .result-box .r-value { font-size: 26px; font-weight: 800; font-family: var(--font); }
  .result-box .r-sub { font-size: 11px; color: var(--muted); margin-top: 4px; }
  .checklist-item { display: flex; align-items: flex-start; gap: 10px; padding: 10px 0; border-bottom: 1px solid var(--border); font-size: 13px; }
  .checklist-item:last-child { border-bottom: none; }
  .check-dot { flex: 0 0 8px; height: 8px; width: 8px; border-radius: 50%; margin-top: 4px; }
  .check-dot.urgent { background: var(--red); }
  .check-dot.critical { background: var(--orange); }
  .check-dot.done { background: var(--green); }
  .check-dot.defer { background: var(--muted); }
  .check-text { flex: 1; }
  .check-text strong { color: var(--text); display: block; }
  .check-text small { color: var(--muted); }
  .settings-section { margin-bottom: 20px; }
  .settings-section h3 { font-size: 11px; text-transform: uppercase; letter-spacing: .5px; color: var(--muted); margin-bottom: 10px; padding-bottom: 6px; border-bottom: 1px solid var(--border); }
  .settings-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
  @media(min-width:600px){.settings-grid{grid-template-columns:1fr 1fr 1fr;}}
  .s-field { display: flex; flex-direction: column; gap: 4px; }
  .s-field label { font-size: 11px; color: var(--muted); }
  .s-field input { background: var(--surface2); border: 1px solid var(--border); border-radius: 6px; color: var(--text); font-family: var(--font); font-size: 13px; padding: 8px 10px; width: 100%; -webkit-appearance: none; }
  .s-field input:focus { outline: none; border-color: var(--accent); box-shadow: 0 0 0 2px rgba(88,166,255,.2); }
  .apply-btn { width: 100%; padding: 12px; background: var(--accent); color: #fff; font-size: 14px; font-weight: 700; border: none; border-radius: var(--radius); cursor: pointer; margin-top: 16px; font-family: var(--sans); transition: opacity .15s; }
  .apply-btn:hover { opacity: .85; }
  .bar-chart { margin-top: 4px; }
  .bar-row { display: flex; align-items: center; gap: 8px; margin-bottom: 6px; }
  .bar-name { font-size: 11px; color: var(--muted); min-width: 80px; flex: 0 0 80px; }
  .bar-track { flex: 1; background: var(--surface2); border-radius: 2px; height: 14px; overflow: hidden; }
  .bar-fill { height: 100%; border-radius: 2px; transition: width .3s; }
  .bar-val { font-size: 11px; font-family: var(--font); color: var(--muted); min-width: 55px; text-align: right; }
  .notice { background: rgba(210,153,34,.1); border: 1px solid rgba(210,153,34,.3); border-radius: var(--radius); padding: 10px 12px; font-size: 12px; color: var(--yellow); margin-bottom: 12px; line-height: 1.5; }
  .notice strong { display: block; margin-bottom: 2px; }
  .divider { border: none; border-top: 1px solid var(--border); margin: 14px 0; }
  .mt { margin-top: 12px; }
  .mono { font-family: var(--font); }
  .section-label { font-size: 11px; font-weight: 700; text-transform: uppercase; letter-spacing: .8px; color: var(--muted); margin-bottom: 8px; margin-top: 16px; }
  .section-label:first-child { margin-top: 0; }
  .disclaimer { font-size: 11px; color: var(--muted); text-align: center; padding: 16px; border-top: 1px solid var(--border); line-height: 1.6; }
</style>
</head>
<body>

<div class="header">
  <div class="header-top">
    <div>
      <h1>💼 Divorce Financial Model</h1>
      <div class="subtitle">Toby Salgado · v9 · Actively Negotiating · Updated: Mar 27, 2026</div>
    </div>
    <div style="display:flex;gap:8px;align-items:center">
      <span class="badge">⚠ Negotiating</span>
      <button onclick="shareModel()" style="background:var(--surface2);border:1px solid var(--border);color:var(--text);padding:5px 10px;border-radius:6px;font-size:12px;cursor:pointer;font-family:var(--sans);white-space:nowrap">⬆ Share</button>
    </div>
  </div>
</div>

<div class="tab-nav">
  <button class="tab-btn active" onclick="show('estate',this)">Estate</button>
  <button class="tab-btn" onclick="show('walkaway',this)">Walkaway</button>
  <button class="tab-btn" onclick="show('scenarios',this)">Scenarios</button>
  <button class="tab-btn" onclick="show('cashflow',this)">Cash Flow</button>
  <button class="tab-btn" onclick="show('business',this)">Business</button>
  <button class="tab-btn" onclick="show('taximpact',this)">Tax Impact</button>
  <button class="tab-btn" onclick="show('supportmod',this)">Support Mod</button>
  <button class="tab-btn" onclick="show('pending',this)">Pending</button>
  <button class="tab-btn" onclick="show('settings',this)">⚙ Settings</button>
</div>

<div class="content">

  <!-- ESTATE -->
  <div class="panel active" id="panel-estate">
    <div class="stat-row">
      <div class="stat"><div class="s-label">Toby Controls</div><div class="s-value green" id="es-toby-controls"></div><div class="s-sub">Assets in hand</div></div>
      <div class="stat"><div class="s-label">Brandy Controls</div><div class="s-value red" id="es-brandy-controls"></div><div class="s-sub">Paseo equity + furnishings</div></div>
      <div class="stat"><div class="s-label">Total Estate</div><div class="s-value" id="es-total"></div><div class="s-sub">Combined marital</div></div>
      <div class="stat"><div class="s-label">50/50 Target Each</div><div class="s-value" id="es-target"></div><div class="s-sub">Equal split</div></div>
    </div>

    <div class="card" style="border-color:var(--red);background:rgba(248,81,73,.07)">
      <div class="card-header" style="background:rgba(248,81,73,.15);color:var(--red)">
        <span>⚖ Position Imbalance</span>
        <span class="mono" id="es-imbalance-badge"></span>
      </div>
      <div class="card-body">
        <table class="data-table">
          <tr><td class="label">Brandy controls</td><td id="es-b-controls-detail"></td></tr>
          <tr><td class="label">Toby controls</td><td id="es-t-controls-detail"></td></tr>
          <tr class="total"><td>Brandy has more by</td><td class="neg" id="es-imbalance"></td></tr>
          <tr><td class="label">Equalization owed to Toby</td><td class="pos" id="es-eq"></td></tr>
          <tr><td class="label" style="font-size:11px;color:var(--muted)">Brandy pays Toby half the gap to reach 50/50</td><td></td></tr>
        </table>
      </div>
    </div>
    <div class="two-col">
      <div class="card">
        <div class="card-header"><span>Toby's Assets</span><span class="mono green" id="es-toby-total"></span></div>
        <div class="card-body">
          <table class="data-table">
            <tr><td class="label">RKD House Equity</td><td id="es-rkd"></td></tr>
            <tr><td class="label">TSLA — 196 sh</td><td id="es-tsla"></td></tr>
            <tr><td class="label">META — 30 sh</td><td id="es-meta"></td></tr>
            <tr><td class="label">Life Insurance CSV</td><td id="es-life"></td></tr>
            <tr><td class="label">Porsche 911 C4S (2003)</td><td id="es-p911"></td></tr>
            <tr><td class="label">Porsche 944 Turbo (1986)</td><td id="es-p944"></td></tr>
            <tr><td class="label">Porsche 944S (1987, NR)</td><td id="es-p944s"></td></tr>
            <tr><td class="label">Ford F-250 (2003)</td><td id="es-ford"></td></tr>
            <tr><td class="label">Ford Flatbed (1998)</td><td id="es-flatbed" class="warn"></td></tr>
            <tr><td class="label">Honda Odyssey (2006, NR)</td><td id="es-odyssey"></td></tr>
            <tr><td class="label">Yamaha PW50 (2006)</td><td id="es-pw50"></td></tr>
            <tr><td class="label">Suzuki DRZ400SM (2009)</td><td id="es-drz"></td></tr>
            <tr><td class="label">Trailer Homemade</td><td id="es-trailer"></td></tr>
            <tr><td class="label">Sports & Climbing Equipment</td><td id="es-sports"></td></tr>
            <tr class="total"><td>TOTAL</td><td id="es-toby-sum" class="pos"></td></tr>
          </table>
        </div>
      </div>
      <div class="card">
        <div class="card-header"><span>Brandy's Assets</span><span class="mono" style="color:var(--red)" id="es-brandy-total"></span></div>
        <div class="card-body">
          <table class="data-table">
            <tr><td class="label">Paseo Gross Value</td><td id="es-paseo-gross"></td></tr>
            <tr><td class="label">Paseo Mortgage</td><td id="es-paseo-mort" class="neg"></td></tr>
            <tr class="subtotal"><td>Paseo Net Equity</td><td id="es-paseo-net"></td></tr>
            <tr><td class="label">Home Furnishings</td><td id="es-furn"></td></tr>
            <tr><td class="label">Porsche Cayenne (2006)</td><td id="es-cayenne"></td></tr>
            <tr class="total"><td>TOTAL</td><td id="es-brandy-sum" class="neg"></td></tr>
          </table>
        </div>
      </div>
    </div>
    <div class="card mt" style="border-color:var(--red);background:rgba(248,81,73,.05)">
      <div class="card-header" style="background:rgba(248,81,73,.12);color:var(--red)">
        <span>🔥 Marital Estate Depletion</span>
        <span style="font-size:10px;color:var(--muted);font-weight:400">Updates live</span>
      </div>
      <div class="card-body">

        <!-- Bleeding clock stat row -->
        <div class="stat-row" style="margin-bottom:14px">
          <div class="stat" style="border-color:var(--red);background:rgba(248,81,73,.08)">
            <div class="s-label">Estate Burns / Month</div>
            <div class="s-value red" id="es-dep-monthly"></div>
            <div class="s-sub">Both parties losing</div>
          </div>
          <div class="stat" style="border-color:var(--red);background:rgba(248,81,73,.08)">
            <div class="s-label">Estate Burns / Year</div>
            <div class="s-value red" id="es-dep-annual"></div>
            <div class="s-sub">Annualized destruction</div>
          </div>
          <div class="stat" style="border-color:var(--yellow);background:rgba(210,153,34,.08)">
            <div class="s-label">Equalization Consumed</div>
            <div class="s-value yellow" id="es-dep-breakeven"></div>
            <div class="s-sub">Months until eq. is gone</div>
          </div>
          <div class="stat" style="border-color:var(--yellow);background:rgba(210,153,34,.08)">
            <div class="s-label">Remaining Eq. Today</div>
            <div class="s-value yellow" id="es-dep-remaining"></div>
            <div class="s-sub">After <span id="es-dep-paid-mo">2</span> mo paid</div>
          </div>
        </div>

        <!-- Burn breakdown -->
        <table class="data-table" style="margin-bottom:16px">
          <tr><td class="label">Toby cash deficit / month</td><td class="neg" id="es-dep-toby"></td></tr>
          <tr><td class="label">Paseo interest / month</td><td class="neg" id="es-dep-interest"></td></tr>
          <tr><td class="label" style="font-size:11px;color:var(--muted);padding-left:12px">Non-recoverable — no equity built</td><td></td></tr>
          <tr><td class="label">Paseo taxes &amp; insurance / month</td><td class="neg" id="es-dep-escrow"></td></tr>
          <tr><td class="label" style="font-size:11px;color:var(--muted);padding-left:12px">Pure carrying cost — Brandy occupies rent-free</td><td></td></tr>
          <tr class="subtotal"><td>Paseo carrying costs / month</td><td class="neg" id="es-dep-carry"></td></tr>
          <tr class="total"><td>Total estate burn / month</td><td class="neg" id="es-dep-total"></td></tr>
        </table>

        <!-- Dual-line depletion chart -->
        <div style="font-size:11px;color:var(--muted);margin-bottom:6px;text-transform:uppercase;letter-spacing:.5px">Equalization Remaining vs. Cumulative Estate Burn</div>
        <canvas id="es-dep-chart" style="width:100%;height:220px;display:block"></canvas>
        <div style="display:flex;flex-wrap:wrap;gap:14px;margin-top:8px;font-size:10px;color:var(--muted)">
          <span style="display:flex;align-items:center;gap:4px"><span style="display:inline-block;width:14px;height:2px;background:#58a6ff"></span>Equalization remaining</span>
          <span style="display:flex;align-items:center;gap:4px"><span style="display:inline-block;width:14px;height:2px;background:#f85149"></span>Cumulative estate burn</span>
          <span style="display:flex;align-items:center;gap:4px"><span style="display:inline-block;width:8px;height:8px;border-radius:50%;background:#d29922"></span>Today (~mo <span id="es-dep-today-mo" style="margin-left:2px">2</span>)</span>
        </div>
        <div style="font-size:11px;color:var(--muted);margin-top:10px;line-height:1.6;padding:10px;background:var(--surface2);border-radius:6px;border-left:3px solid var(--red)">
          <strong style="color:var(--text)">Judicial argument:</strong> The marital estate loses <strong id="es-dep-monthly-inline"></strong>/month in real wealth — $<span id="es-dep-interest-inline"></span>/mo in non-recoverable mortgage interest, $<span id="es-dep-escrow-inline"></span>/mo in property taxes &amp; insurance, plus <strong id="es-dep-toby-inline"></strong>/mo cash deficit while Brandy occupies the asset rent-free. Prompt resolution is in both parties' interest.
        </div>
      </div>
    </div>
  </div>

  <!-- CASH FLOW -->
  <div class="panel" id="panel-cashflow">
    <div class="card">
      <div class="card-header"><span>Monthly Cash Flow — Current</span><span class="badge">Active</span></div>
      <div class="card-body">
        <div class="section-label">Fixed Expenses</div>
        <table class="data-table">
          <tr><td class="label">RKD Mortgage</td><td id="cf-rkdmort" class="neg"></td></tr>
          <tr><td class="label">Spousal Support</td><td id="cf-support" class="neg"></td></tr>
          <tr><td class="label">Auto Insurance (3 vehicles)</td><td id="cf-autoins" class="neg"></td></tr>
          <tr><td class="label">Blake Support (avg)</td><td id="cf-blake" class="neg"></td></tr>
          <tr class="subtotal"><td>Fixed Subtotal</td><td class="neg" id="cf-fixed-sub"></td></tr>
        </table>
        <div class="section-label" style="margin-top:14px">Variable Expenses (83-day avg)</div>
        <table class="data-table">
          <tr><td class="label">Groceries</td><td id="cf-groc" class="neg"></td></tr>
          <tr><td class="label">Shopping</td><td id="cf-shop" class="neg"></td></tr>
          <tr><td class="label">Travel / REI</td><td id="cf-travel" class="neg"></td></tr>
          <tr><td class="label">Home Improvement</td><td id="cf-home" class="neg"></td></tr>
          <tr><td class="label">Vehicle Gas (incl Food 4 Less)</td><td id="cf-gas" class="neg"></td></tr>
          <tr><td class="label">Utilities</td><td id="cf-util" class="neg"></td></tr>
          <tr><td class="label">Phone (Verizon)</td><td id="cf-phone" class="neg"></td></tr>
          <tr><td class="label">Clothing</td><td id="cf-cloth" class="neg"></td></tr>
          <tr><td class="label">Dining Out</td><td id="cf-dining" class="neg"></td></tr>
          <tr><td class="label">Entertainment</td><td id="cf-ent" class="neg"></td></tr>
          <tr><td class="label">Auto Maintenance</td><td id="cf-autom" class="neg"></td></tr>
          <tr><td class="label">Medical</td><td id="cf-med" class="neg"></td></tr>
          <tr><td class="label">Misc / Personal</td><td id="cf-misc" class="neg"></td></tr>
          <tr class="subtotal"><td>Variable Subtotal</td><td class="neg" id="cf-var-sub"></td></tr>
        </table>
        <hr class="divider">
        <table class="data-table">
          <tr><td class="label">W2 Net Income</td><td id="cf-w2" class="pos"></td></tr>
          <tr class="total"><td>MONTHLY DEFICIT</td><td class="neg" id="cf-p1-deficit"></td></tr>
        </table>
      </div>
    </div>
  </div>
  <!-- WALKAWAY -->
  <div class="panel" id="panel-walkaway">
    <div class="toggle-row">
      <button class="toggle-btn active" id="wa-mode-buyout" onclick="setWaMode('buyout')">Brandy Buys Out</button>
      <button class="toggle-btn" id="wa-mode-sale" onclick="setWaMode('sale')">Paseo Sold</button>
    </div>
    <div class="slider-group">
      <div class="slider-label"><span>Paseo Value</span><span class="slider-val" id="wa-paseo-val"></span></div>
      <input type="range" id="wa-paseo" min="1400000" max="2000000" step="5000" oninput="onSlider('paseo',+this.value)">
      <div style="display:flex;justify-content:space-between;font-size:10px;color:var(--muted);margin-top:4px"><span>$1.4M (Redfin)</span><span>$1.91M (Zillow)</span></div>
    </div>
    <div class="slider-group" id="wa-costs-group">
      <div class="slider-label"><span>Selling Costs</span><span class="slider-val" id="wa-costs-val"></span></div>
      <input type="range" id="wa-costs" min="1" max="8" step="0.5" oninput="onSlider('sellingCosts',+this.value)">
    </div>
    <div class="slider-group">
      <div class="slider-label"><span>Mortgage Payoff</span><span class="slider-val" id="wa-mort-val"></span></div>
      <input type="range" id="wa-mort" min="300000" max="370000" step="1000" oninput="onSlider('paseoMort',+this.value)">
    </div>
    <div class="card">
      <div class="card-header">Walkaway Analysis — <span id="wa-mode-label">Buyout Mode</span></div>
      <div class="card-body">
        <table class="data-table">
          <tr><td class="label">Paseo Gross Value</td><td id="wa-gross"></td></tr>
          <tr id="wa-selling-row"><td class="label">Less: Selling Costs</td><td id="wa-selling" class="neg"></td></tr>
          <tr><td class="label">Less: Mortgage Payoff</td><td id="wa-payoff" class="neg"></td></tr>
          <tr class="subtotal"><td>Paseo Net Equity</td><td id="wa-net"></td></tr>
          <tr><td class="label">Total Estate</td><td id="wa-total-estate"></td></tr>
          <tr><td class="label">50/50 Target Each</td><td id="wa-target"></td></tr>
          <tr><td class="label">Toby Controls</td><td id="wa-toby-other"></td></tr>
          <tr class="total"><td>Equalization to Toby</td><td id="wa-equalization"></td></tr>
        </table>
      </div>
    </div>
  </div>

  <!-- SCENARIOS -->
  <div class="panel" id="panel-scenarios">
    <div class="slider-group">
      <div class="slider-label"><span>Paseo Value</span><span class="slider-val" id="sc-paseo-val"></span></div>
      <input type="range" id="sc-paseo" min="1400000" max="2000000" step="5000" oninput="onSlider('paseo',+this.value)">
    </div>
    <div class="slider-group">
      <div class="slider-label"><span>Spousal Support ($/mo)</span><span class="slider-val" id="sc-support-val"></span></div>
      <input type="range" id="sc-support" min="0" max="4000" step="50" oninput="onSlider('ssupport',+this.value)">
    </div>
    <div class="slider-group">
      <div class="slider-label"><span>Months to Settlement</span><span class="slider-val" id="sc-months-val"></span></div>
      <input type="range" id="sc-months" min="1" max="24" step="1" oninput="onSlider('settlementMonths',+this.value)">
    </div>
    <div class="stat-row">
      <div class="stat"><div class="s-label">Equalization</div><div class="s-value green" id="sc-eq"></div><div class="s-sub">Brandy → Toby</div></div>
      <div class="stat"><div class="s-label">Total Support Paid</div><div class="s-value red" id="sc-support-total"></div><div class="s-sub">Cumulative outflow</div></div>
      <div class="stat"><div class="s-label">Net After Support</div><div class="s-value yellow" id="sc-net-after"></div><div class="s-sub">Effective walkaway</div></div>
      <div class="stat"><div class="s-label">Monthly Deficit</div><div class="s-value red" id="sc-deficit"></div><div class="s-sub">Cash burn / month</div></div>
    </div>
    <div class="card">
      <div class="card-header">Scenario Summary</div>
      <div class="card-body">
        <table class="data-table">
          <tr><td class="label">Paseo Value</td><td id="sc-s-paseo"></td></tr>
          <tr><td class="label">Paseo Net Equity (basis)</td><td id="sc-s-net"></td></tr>
          <tr class="subtotal"><td>Equalization to Toby</td><td class="pos" id="sc-s-eq"></td></tr>
          <tr><td class="label">Months of Support</td><td id="sc-s-months"></td></tr>
          <tr><td class="label">Total Support Paid</td><td class="neg" id="sc-s-paid"></td></tr>
          <tr class="total"><td>NET WALKAWAY</td><td class="green" id="sc-s-walkaway"></td></tr>
        </table>
      </div>
    </div>
    <div class="card" style="margin-top:12px">
      <div class="card-header">
        <span>Cost of Delay — Estate Depletion Over Time</span>
        <span style="font-size:10px;color:var(--muted);font-weight:400">Updates with sliders above</span>
      </div>
      <div class="card-body">
        <div class="notice" style="margin-bottom:14px"><strong>Every month of delay costs you support paid + cash deficit burned.</strong> The curve below shows your net walkaway shrinking over time.</div>
        <table class="data-table" style="margin-bottom:16px">
          <tr><td class="label">Equalization (Brandy → Toby)</td><td class="pos" id="dep-eq"></td></tr>
          <tr><td class="label">Monthly cash deficit</td><td class="neg" id="dep-deficit"></td></tr>
          <tr><td class="label">Monthly spousal support</td><td class="neg" id="dep-support"></td></tr>
          <tr><td class="label" style="font-weight:600">Total burn per month</td><td class="neg" id="dep-burn"></td></tr>
          <tr class="subtotal"><td>Net walkaway at month <span id="dep-mo-label">6</span></td><td id="dep-net-walkaway" class="yellow"></td></tr>
          <tr><td class="label">Cost of each additional month</td><td class="neg" id="dep-monthly-cost"></td></tr>
        </table>
        <div style="font-size:11px;color:var(--muted);margin-bottom:8px;text-transform:uppercase;letter-spacing:.5px">Net Walkaway by Month of Settlement</div>
        <canvas id="dep-chart" style="width:100%;height:200px;display:block"></canvas>
        <div style="display:flex;gap:16px;margin-top:8px;font-size:10px;color:var(--muted)">
          <span style="display:flex;align-items:center;gap:4px"><span style="display:inline-block;width:12px;height:2px;background:#58a6ff"></span>Net Walkaway</span>
          <span style="display:flex;align-items:center;gap:4px"><span style="display:inline-block;width:12px;height:2px;background:#f85149;border-top:2px dashed #f85149"></span>Break Even</span>
          <span id="dep-current-marker-legend" style="display:flex;align-items:center;gap:4px"><span style="display:inline-block;width:8px;height:8px;border-radius:50%;background:#d29922"></span>Current month</span>
        </div>
      </div>
    </div>
  </div>

  <!-- SUPPORT MOD -->
  <div class="panel" id="panel-supportmod">
    <div class="notice"><strong>⚡ File Support Modification Immediately</strong>Brandy now earns ~$18/hr full-time (~$3,000/mo gross). Father paying $4,750/mo Paseo mortgage directly — income attribution argument. CA Family Code §3651 applies.</div>
    <div class="slider-group">
      <div class="slider-label"><span>New Support Amount ($/mo)</span><span class="slider-val" id="sm-new-val"></span></div>
      <input type="range" id="sm-new" min="0" max="2124" step="25" oninput="onSlider('ssupport',+this.value)">
      <div style="display:flex;justify-content:space-between;font-size:10px;color:var(--muted);margin-top:4px"><span>$0 (eliminated)</span><span>$2,124 (current)</span></div>
    </div>
    <div class="stat-row">
      <div class="stat"><div class="s-label">Current / Original</div><div class="s-value red">$2,124</div><div class="s-sub">Court-ordered</div></div>
      <div class="stat"><div class="s-label">New Support</div><div class="s-value yellow" id="sm-new-display"></div><div class="s-sub">Modified</div></div>
      <div class="stat"><div class="s-label">Monthly Savings</div><div class="s-value green" id="sm-savings"></div><div class="s-sub">Cash freed up</div></div>
      <div class="stat"><div class="s-label">Annual Savings</div><div class="s-value green" id="sm-annual"></div><div class="s-sub">Per year</div></div>
    </div>
    <div class="card">
      <div class="card-header">Cash Flow Impact</div>
      <div class="card-body">
        <table class="data-table">
          <tr><td class="label">Current Monthly Deficit</td><td class="neg" id="sm-current-deficit"></td></tr>
          <tr><td class="label">Support Reduction</td><td class="pos" id="sm-reduction"></td></tr>
          <tr class="total"><td>New Monthly Deficit</td><td class="neg" id="sm-new-deficit"></td></tr>
        </table>
      </div>
    </div>
    <div class="card">
      <div class="card-header">Brandy's Income Evidence</div>
      <div class="card-body">
        <table class="data-table">
          <tr><td class="label">Wages ($18/hr FT)</td><td>~$3,000/mo gross</td></tr>
          <tr><td class="label">Father — Paseo mortgage</td><td>$4,750/mo (documented)</td></tr>
          <tr><td class="label">Father — historical payments</td><td>$3,150/mo (pattern)</td></tr>
          <tr class="subtotal"><td>Brandy Effective Income</td><td class="warn">~$7,850/mo</td></tr>
          <tr><td class="label">Toby W2 Net</td><td id="sm-toby-w2"></td></tr>
          <tr class="total"><td>Income Disparity</td><td class="pos">Brandy earns MORE</td></tr>
        </table>
      </div>
    </div>
  </div>

  <!-- TAX IMPACT -->
  <div class="panel" id="panel-taximpact">
    <div class="notice"><strong>⚠ Cost Basis Required from Brokerage</strong>TSLA and META basis deferred. Plug in once confirmed. Affects settlement structure decisions.</div>
    <div class="slider-group">
      <div class="slider-label"><span>TSLA Cost Basis (per share)</span><span class="slider-val" id="tx-tsla-val"></span></div>
      <input type="range" id="tx-tsla" min="50" max="400" step="5" oninput="onSlider('tslaBasis',+this.value)">
    </div>
    <div class="slider-group">
      <div class="slider-label"><span>META Cost Basis (per share)</span><span class="slider-val" id="tx-meta-val"></span></div>
      <input type="range" id="tx-meta" min="100" max="600" step="10" oninput="onSlider('metaBasis',+this.value)">
    </div>
    <div class="slider-group">
      <div class="slider-label"><span>Cap Gains Rate</span><span class="slider-val" id="tx-rate-val"></span></div>
      <input type="range" id="tx-rate" min="0" max="23.8" step="0.1" oninput="onSlider('capGainsRate',+this.value)">
    </div>
    <div class="card">
      <div class="card-header">Tax Exposure</div>
      <div class="card-body">
        <table class="data-table">
          <tr><td class="label">TSLA — 196 sh FMV</td><td id="tx-tsla-fmv"></td></tr>
          <tr><td class="label">TSLA Cost Basis (196 sh)</td><td id="tx-tsla-basis" class="neg"></td></tr>
          <tr class="subtotal"><td>TSLA Gain</td><td id="tx-tsla-gain"></td></tr>
          <tr><td class="label">META — 30 sh FMV</td><td id="tx-meta-fmv"></td></tr>
          <tr><td class="label">META Cost Basis (30 sh)</td><td id="tx-meta-basis" class="neg"></td></tr>
          <tr class="subtotal"><td>META Gain</td><td id="tx-meta-gain"></td></tr>
          <tr class="total"><td>TOTAL TAX LIABILITY</td><td class="neg" id="tx-total-tax"></td></tr>
        </table>
      </div>
    </div>
    <div class="card">
      <div class="card-header">Settlement Strategy</div>
      <div class="card-body">
        <table class="data-table">
          <tr><td class="label">Transfer stocks (no liquidation)</td><td class="pos">$0 tax now</td></tr>
          <tr><td class="label">Sell stocks, pay gains</td><td class="neg" id="tx-sell-cost"></td></tr>
        </table>
        <div class="result-box" style="margin-top:12px">
          <div class="r-label">Stock Transfer Benefit</div>
          <div class="r-value green" id="tx-benefit"></div>
          <div class="r-sub">Tax deferred by transferring vs. liquidating</div>
        </div>
      </div>
    </div>
  </div>

  <!-- BUSINESS -->
  <div class="panel" id="panel-business">
    <div class="notice"><strong>⚠ Revenue ≠ Income</strong>$322K gross → $0 net after expenses. Only documentable personal income: $86,667 W2. Verified from QuickBooks Jan–Dec 2025.</div>
    <div class="stat-row">
      <div class="stat"><div class="s-label">Gross Revenue</div><div class="s-value">$322,230</div></div>
      <div class="stat"><div class="s-label">Total Expenses</div><div class="s-value red">$325,049</div></div>
      <div class="stat"><div class="s-label">Net Income</div><div class="s-value red">-$2,819</div></div>
      <div class="stat"><div class="s-label">Owner Draws</div><div class="s-value yellow">$26,682</div><div class="s-sub">$2,224/mo avg</div></div>
    </div>
    <div class="card">
      <div class="card-header">2025 P&L — BNT Erosion Control dba Super Agents Live</div>
      <div class="card-body">
        <table class="data-table">
          <tr><td class="label">Gross Sales</td><td class="pos">$349,366</td></tr>
          <tr><td class="label">Less: Refunds</td><td class="neg">-$27,136</td></tr>
          <tr class="subtotal"><td>NET REVENUE</td><td>$322,230</td></tr>
        </table>
        <div class="section-label" style="margin-top:14px">Expenses</div>
        <table class="data-table">
          <tr><td class="label">Advertising & Promo</td><td class="neg">-$272,411 <small style="color:var(--muted)">(84.5%)</small></td></tr>
          <tr><td class="label">Utilities</td><td class="neg">-$14,044</td></tr>
          <tr><td class="label">Insurance</td><td class="neg">-$10,187</td></tr>
          <tr><td class="label">Repairs & Maintenance</td><td class="neg">-$9,303</td></tr>
          <tr><td class="label">Travel</td><td class="neg">-$4,508</td></tr>
          <tr><td class="label">Automobile</td><td class="neg">-$4,065</td></tr>
          <tr><td class="label">Computer & Internet</td><td class="neg">-$2,798</td></tr>
          <tr><td class="label">Telephone</td><td class="neg">-$2,389</td></tr>
          <tr><td class="label">Office Supplies</td><td class="neg">-$2,202</td></tr>
          <tr><td class="label">Professional Fees</td><td class="neg">-$1,886</td></tr>
          <tr><td class="label">Medical</td><td class="neg">-$1,564</td></tr>
          <tr><td class="label">Meals & Entertainment</td><td class="neg">-$1,415</td></tr>
          <tr><td class="label">Other</td><td class="neg">-$2,277</td></tr>
          <tr class="total"><td>NET INCOME (LOSS)</td><td class="neg">-$2,819</td></tr>
        </table>
      </div>
    </div>
    <div class="card">
      <div class="card-header">Cash Flow Summary</div>
      <div class="card-body">
        <table class="data-table">
          <tr><td class="label">Cash on Hand Dec 31</td><td>$7,474</td></tr>
          <tr><td class="label">Net AMEX Liability</td><td class="neg">-$4,597</td></tr>
          <tr class="total"><td>Net Cash Position</td><td class="warn">$2,877</td></tr>
        </table>
        <div class="notice" style="margin-top:12px"><strong>⚠ Commingling Exposure</strong>Some business costs charged to personal AmEx. Attorney should be prepared to address.</div>
      </div>
    </div>
    <div class="card"><div class="card-header">Expense Breakdown</div><div class="card-body"><div class="bar-chart" id="biz-chart"></div></div></div>
  </div>

  <!-- PENDING -->
  <div class="panel" id="panel-pending">
    <div class="card" style="border-color:var(--yellow)">
      <div class="card-header" style="color:var(--yellow)">Paseo Valuation Risk</div>
      <div class="card-body">
        <div class="notice"><strong>⚠ Formal appraisal NOT yet ordered — URGENT</strong>Every $100K change in Paseo value = $50K shift in equalization.</div>
        <table class="data-table">
          <tr><td class="label">Zillow AVM</td><td>$1,914,700</td></tr>
          <tr><td class="label">Redfin AVM</td><td>$1,575,107</td></tr>
          <tr class="subtotal"><td>Spread</td><td class="warn">$339,593</td></tr>
          <tr><td class="label">Mortgage Payoff (3/23)</td><td>$336,438</td></tr>
          <tr><td class="label">Model Value</td><td id="es-paseo-model"></td></tr>
        </table>
      </div>
    </div>
    <div class="card">
      <div class="card-header">Evidence Needed</div>
      <div class="card-body">
        <div class="checklist-item"><div class="check-dot urgent"></div><div class="check-text"><strong>Paseo Formal Appraisal</strong><small>Request through attorney immediately. Every $100K = $50K shift in Toby's position.</small></div></div>
        <div class="checklist-item"><div class="check-dot urgent"></div><div class="check-text"><strong>Brandy Paystubs ($18/hr)</strong><small>URGENT — via discovery/subpoena. Key for support modification.</small></div></div>
        <div class="checklist-item"><div class="check-dot critical"></div><div class="check-text"><strong>Father's Bank Records ($4,750/mo)</strong><small>CRITICAL — income attribution argument. Documents direct mortgage payments.</small></div></div>
        <div class="checklist-item"><div class="check-dot defer"></div><div class="check-text"><strong>TSLA / META Cost Basis</strong><small>Deferred — needed for cap gains modeling. Get from brokerage statement.</small></div></div>
        <div class="checklist-item"><div class="check-dot defer"></div><div class="check-text"><strong>401(k) Separation Balance</strong><small>Document ~$10K at separation vs ~$21K now. Full separate property argument.</small></div></div>
        <div class="checklist-item"><div class="check-dot defer"></div><div class="check-text"><strong>Other Debts / Liabilities</strong><small>Confirm none outstanding beyond AMEX.</small></div></div>
      </div>
    </div>
    <div class="card">
      <div class="card-header">Confirmed This Session</div>
      <div class="card-body">
        <div class="checklist-item"><div class="check-dot done"></div><div class="check-text"><strong>Food 4 Less = ALL Gas</strong><small>Groceries $1,536 / Gas $413 — confirmed separate categories.</small></div></div>
        <div class="checklist-item"><div class="check-dot done"></div><div class="check-text"><strong>Simplepeptide = All One-Time</strong><small>4–5 charges, all one-time. Excluded from recurring medical.</small></div></div>
        <div class="checklist-item"><div class="check-dot done"></div><div class="check-text"><strong>DRZ400 Added to Estate</strong><small>$3,200 estimated — added to Toby's assets.</small></div></div>
        <div class="checklist-item"><div class="check-dot done"></div><div class="check-text"><strong>Porsche Cayenne Added</strong><small>$3,000 KBB marital value — added to Brandy's assets.</small></div></div>
        <div class="checklist-item"><div class="check-dot done"></div><div class="check-text"><strong>Stock Cost Basis Deferred</strong><small>Not needed for current settlement modeling.</small></div></div>
      </div>
    </div>
    <div class="card">
      <div class="card-header">Strategic Notes</div>
      <div class="card-body">
        <div class="section-label">Support Modification</div>
        <table class="data-table">
          <tr><td class="label">Brandy's Employment</td><td>$18/hr FT (~$3K/mo gross)</td></tr>
          <tr><td class="label">Father Paseo Payment</td><td class="warn">$4,750/mo (documented)</td></tr>
          <tr><td class="label">Brandy Effective Income</td><td class="warn">~$7,850/mo</td></tr>
          <tr><td class="label">Toby W2 Net</td><td id="pen-w2"></td></tr>
          <tr class="total"><td>Code Basis</td><td class="pos">CA FC §3651</td></tr>
        </table>
        <div class="section-label" style="margin-top:14px">401(k) Position</div>
        <table class="data-table">
          <tr><td class="label">Balance at Separation</td><td>~$10,000</td></tr>
          <tr><td class="label">Balance Today</td><td>~$21,000</td></tr>
          <tr><td class="label">Growth</td><td class="pos">~$11,000 (post-sep)</td></tr>
          <tr class="total"><td>Argument</td><td class="pos">Full separate property</td></tr>
        </table>
      </div>
    </div>
  </div>

  <!-- SETTINGS -->
  <div class="panel" id="panel-settings">
    <div class="notice"><strong>⚙ Data Editor — v9 Fully Linked</strong>Every field updates all tabs instantly on Apply.</div>
    <div class="settings-section">
      <h3>Toby's Assets</h3>
      <div class="settings-grid">
        <div class="s-field"><label>RKD Equity</label><input type="number" id="si-rkd"></div>
        <div class="s-field"><label>TSLA (196 sh) FMV</label><input type="number" id="si-tsla"></div>
        <div class="s-field"><label>META (30 sh) FMV</label><input type="number" id="si-meta"></div>
        <div class="s-field"><label>Life Insurance CSV</label><input type="number" id="si-life"></div>
        <div class="s-field"><label>Porsche 911 C4S (2003)</label><input type="number" id="si-p911"></div>
        <div class="s-field"><label>Porsche 944 Turbo (1986)</label><input type="number" id="si-p944"></div>
        <div class="s-field"><label>Porsche 944S (1987, NR)</label><input type="number" id="si-p944s"></div>
        <div class="s-field"><label>Ford F-250 (2003)</label><input type="number" id="si-ford"></div>
        <div class="s-field"><label>Honda Odyssey (2006, NR)</label><input type="number" id="si-odyssey"></div>
        <div class="s-field"><label>Yamaha PW50 (2006)</label><input type="number" id="si-pw50"></div>
        <div class="s-field"><label>Suzuki DRZ400SM (2009)</label><input type="number" id="si-drz"></div>
        <div class="s-field"><label>Trailer Homemade</label><input type="number" id="si-trailer"></div>
        <div class="s-field"><label>Sports &amp; Climbing Equip</label><input type="number" id="si-sports"></div>
      </div>
    </div>
    <div class="settings-section">
      <h3>Brandy's Assets</h3>
      <div class="settings-grid">
        <div class="s-field"><label>Paseo Gross Value</label><input type="number" id="si-paseo"></div>
        <div class="s-field"><label>Paseo Mortgage</label><input type="number" id="si-paseo-mort"></div>
        <div class="s-field"><label>Paseo Interest / mo</label><input type="number" id="si-paseo-interest"></div>
        <div class="s-field"><label>Paseo Escrow / mo</label><input type="number" id="si-paseo-escrow"></div>
        <div class="s-field"><label>Home Furnishings</label><input type="number" id="si-furn"></div>
        <div class="s-field"><label>Porsche Cayenne</label><input type="number" id="si-cayenne"></div>
        <div class="s-field"><label>Months Support Paid</label><input type="number" id="si-months-paid"></div>
      </div>
    </div>
    <div class="settings-section">
      <h3>Fixed Expenses</h3>
      <div class="settings-grid">
        <div class="s-field"><label>RKD Mortgage</label><input type="number" id="si-rkdmort"></div>
        <div class="s-field"><label>Spousal Support</label><input type="number" id="si-ssupport"></div>
        <div class="s-field"><label>Auto Insurance</label><input type="number" id="si-autoins"></div>
        <div class="s-field"><label>Blake Support</label><input type="number" id="si-blake"></div>
      </div>
    </div>
    <div class="settings-section">
      <h3>Variable Expenses</h3>
      <div class="settings-grid">
        <div class="s-field"><label>Groceries</label><input type="number" id="si-groc"></div>
        <div class="s-field"><label>Shopping</label><input type="number" id="si-shop"></div>
        <div class="s-field"><label>Travel / REI</label><input type="number" id="si-travel"></div>
        <div class="s-field"><label>Home Improvement</label><input type="number" id="si-home"></div>
        <div class="s-field"><label>Vehicle Gas</label><input type="number" id="si-gas"></div>
        <div class="s-field"><label>Utilities</label><input type="number" id="si-util"></div>
        <div class="s-field"><label>Phone</label><input type="number" id="si-phone"></div>
        <div class="s-field"><label>Clothing</label><input type="number" id="si-cloth"></div>
        <div class="s-field"><label>Dining Out</label><input type="number" id="si-dining"></div>
        <div class="s-field"><label>Entertainment</label><input type="number" id="si-ent"></div>
        <div class="s-field"><label>Auto Maintenance</label><input type="number" id="si-autom"></div>
        <div class="s-field"><label>Medical</label><input type="number" id="si-med"></div>
        <div class="s-field"><label>Misc / Personal</label><input type="number" id="si-misc"></div>
      </div>
    </div>
    <div class="settings-section">
      <h3>Income</h3>
      <div class="settings-grid">
        <div class="s-field"><label>W2 Net Income</label><input type="number" id="si-w2"></div>
      </div>
    </div>
    <button class="apply-btn" onclick="applySettings()">✓ Apply Changes — Recalculate All Tabs</button>
  </div>

</div>

<div class="disclaimer">Personal financial planning tool only.<br>Not legal or tax advice. Verify all figures with attorney and CPA before court use.</div>

<script>
// ═══════════════════ SINGLE SOURCE OF TRUTH ═══════════════════
const D = {
  // Toby assets
  rkd:709763, tsla:72951, meta:18201, life:239000,
  p911:36500, ford:4705, p944:17000, drz:3200,
  p944s:1500, odyssey:400, pw50:600, trailer:100, sports:2000,
  // Brandy assets
  paseo:1744904, paseoMort:336438, furn:50000, cayenne:3653,
  // Phase 1 fixed
  rkdMort:1642, ssupport:2124, autoIns:800, blake:238,
  // Phase 1 variable
  groc:1536, shop:1259, travel:564, home:338, gas:413,
  util:300, phone:136, cloth:113, dining:95, ent:58,
  autom:37, med:87, misc:50,
  // Phase 2
  w2:5506, draw:2160, gx:1400, p2Ins:800, p2Groc:900,
  p2Shop:500, p2Trav:300, p2Other:689,
  // Tax
  tslaBasis:150, metaBasis:250, capGainsRate:15,
  // Scenario
  settlementMonths:6,
  // Walkaway
  sellingCosts:6,
  // Depletion — exact figures from mortgage statement
  paseoInterestAmt:1462, paseoEscrowAmt:1315, monthsPaid:2,
};

let waMode = 'buyout';

// ═══════════════════ UTILS ═══════════════════
const $ = id => document.getElementById(id);
function fmt(n) {
  const abs = Math.abs(Math.round(n));
  return (n < 0 ? '-$' : '$') + abs.toLocaleString('en-US');
}
function set(id, val) { const el=$(id); if(el) el.textContent = val; }
function syncSlider(id, val) { const el=$(id); if(el) el.value = val; }
function syncInput(id, val) { const el=$(id); if(el) el.value = val; }

// ═══════════════════ SINGLE ENTRY POINT FOR ALL CHANGES ═══════════════════
function onSlider(key, val) {
  D[key] = val;
  syncAllControls();
  renderAll();
}

function syncAllControls() {
  // Sliders
  syncSlider('wa-paseo', D.paseo);
  syncSlider('wa-mort', D.paseoMort);
  syncSlider('wa-costs', D.sellingCosts);
  syncSlider('sc-paseo', D.paseo);
  syncSlider('sc-support', D.ssupport);
  syncSlider('sc-months', D.settlementMonths);
  syncSlider('sm-new', D.ssupport);
  syncSlider('tx-tsla', D.tslaBasis);
  syncSlider('tx-meta', D.metaBasis);
  syncSlider('tx-rate', D.capGainsRate);
  // Settings inputs
  syncInput('si-rkd', D.rkd);
  syncInput('si-tsla', D.tsla);
  syncInput('si-meta', D.meta);
  syncInput('si-life', D.life);
  syncInput('si-p911', D.p911);
  syncInput('si-ford', D.ford);
  syncInput('si-p944', D.p944);
  syncInput('si-drz', D.drz);
  syncInput('si-p944s', D.p944s);
  syncInput('si-odyssey', D.odyssey);
  syncInput('si-pw50', D.pw50);
  syncInput('si-trailer', D.trailer);
  syncInput('si-sports', D.sports);
  syncInput('si-paseo', D.paseo);
  syncInput('si-paseo-mort', D.paseoMort);
  syncInput('si-furn', D.furn);
  syncInput('si-cayenne', D.cayenne);
  syncInput('si-rkdmort', D.rkdMort);
  syncInput('si-ssupport', D.ssupport);
  syncInput('si-autoins', D.autoIns);
  syncInput('si-blake', D.blake);
  syncInput('si-groc', D.groc);
  syncInput('si-shop', D.shop);
  syncInput('si-travel', D.travel);
  syncInput('si-home', D.home);
  syncInput('si-gas', D.gas);
  syncInput('si-util', D.util);
  syncInput('si-phone', D.phone);
  syncInput('si-cloth', D.cloth);
  syncInput('si-dining', D.dining);
  syncInput('si-ent', D.ent);
  syncInput('si-autom', D.autom);
  syncInput('si-med', D.med);
  syncInput('si-misc', D.misc);
  syncInput('si-w2', D.w2);
  syncInput('si-paseo-interest', D.paseoInterestAmt);
  syncInput('si-paseo-escrow', D.paseoEscrowAmt);
  syncInput('si-months-paid', D.monthsPaid);
}

// ═══════════════════ APPLY SETTINGS (reads inputs → D → render) ═══════════════════
function applySettings() {
  const r = id => +$(id).value || 0;
  D.rkd=r('si-rkd'); D.tsla=r('si-tsla'); D.meta=r('si-meta'); D.life=r('si-life');
  D.p911=r('si-p911'); D.ford=r('si-ford'); D.p944=r('si-p944'); D.drz=r('si-drz');
  D.p944s=r('si-p944s'); D.odyssey=r('si-odyssey'); D.pw50=r('si-pw50');
  D.trailer=r('si-trailer'); D.sports=r('si-sports');
  D.paseo=r('si-paseo'); D.paseoMort=r('si-paseo-mort'); D.furn=r('si-furn'); D.cayenne=r('si-cayenne');
  D.rkdMort=r('si-rkdmort'); D.ssupport=r('si-ssupport'); D.autoIns=r('si-autoins'); D.blake=r('si-blake');
  D.groc=r('si-groc'); D.shop=r('si-shop'); D.travel=r('si-travel'); D.home=r('si-home');
  D.gas=r('si-gas'); D.util=r('si-util'); D.phone=r('si-phone'); D.cloth=r('si-cloth');
  D.dining=r('si-dining'); D.ent=r('si-ent'); D.autom=r('si-autom'); D.med=r('si-med'); D.misc=r('si-misc');
  D.w2=r('si-w2');
  D.paseoInterestAmt=r('si-paseo-interest') || 1462;
  D.paseoEscrowAmt=r('si-paseo-escrow') || 1315;
  D.monthsPaid=r('si-months-paid');
  syncAllControls();
  renderAll();
  const btn = document.querySelector('.apply-btn');
  btn.textContent = '✓ Applied!'; btn.style.background = '#3fb950';
  setTimeout(() => { btn.textContent = '✓ Apply Changes — Recalculate All Tabs'; btn.style.background = ''; }, 1800);
}

// ═══════════════════ DERIVED CALCULATIONS — SINGLE SOURCE OF TRUTH ═══════════════════
function calc() {
  // ── ESTATE ──
  const tobyAssets = D.rkd+D.tsla+D.meta+D.life+D.p911+D.ford+D.p944+D.drz+D.p944s+D.odyssey+D.pw50+D.trailer+D.sports;
  const paseoNet   = D.paseo - D.paseoMort;
  const brandyAssets = paseoNet + D.furn + D.cayenne;
  const totalEstate  = tobyAssets + brandyAssets;
  const target       = totalEstate / 2;
  // equalization: positive = Brandy owes Toby, negative = Toby owes Brandy
  const equalization = target - tobyAssets;
  const imbalance    = brandyAssets - tobyAssets; // raw gap before split

  // ── CASH FLOW ──
  const fixedTotal = D.rkdMort+D.ssupport+D.autoIns+D.blake;
  const varTotal   = D.groc+D.shop+D.travel+D.home+D.gas+D.util+D.phone+D.cloth+D.dining+D.ent+D.autom+D.med+D.misc;
  const p1Deficit  = D.w2 - fixedTotal - varTotal; // negative = deficit

  const p2Inc     = D.w2 + D.draw;
  const p2Out     = D.rkdMort+D.gx+D.p2Ins+D.p2Groc+D.p2Shop+D.p2Trav+D.p2Other;
  const p2Surplus = p2Inc - p2Out;

  // ── WALKAWAY (Paseo sale or buyout) ──
  // Buyout: no sale costs, equalization = same as estate (Brandy pays Toby the gap in cash)
  // Sale:   selling costs reduce net Paseo proceeds, so Toby's share of Paseo shrinks by sellingCostAmt/2
  const sellingCostAmt = waMode==='sale' ? D.paseo*D.sellingCosts/100 : 0;
  const waNetEquity = D.paseo - sellingCostAmt - D.paseoMort;
  const waHalf      = waNetEquity / 2;  // each party's share of Paseo net
  // Equalization: start from estate baseline, then adjust for selling cost impact on Toby's Paseo share
  const waEq        = equalization - sellingCostAmt / 2;  // sale costs reduce what Toby nets
  // These are kept for the display table
  const waTarget    = target;

  // ── SCENARIOS (uses same estate math — equalization is always c.equalization) ──
  // scEq === equalization (same formula, kept as alias for display clarity)
  const scEq           = equalization;
  const scSupportTotal = D.ssupport * D.settlementMonths;
  const scWalkaway     = scEq - scSupportTotal;

  // ── SUPPORT MOD ──
  const smSavings = 2124 - D.ssupport;

  // ── TAX ──
  const tslaFMV  = D.tsla;
  const metaFMV  = D.meta;
  const tslaCost = D.tslaBasis * 196;
  const metaCost = D.metaBasis * 30;
  const tslaGain = Math.max(0, tslaFMV - tslaCost);
  const metaGain = Math.max(0, metaFMV - metaCost);
  const totalTax = (tslaGain + metaGain) * D.capGainsRate / 100;

  return {
    tobyAssets, paseoNet, brandyAssets, totalEstate, target, equalization, imbalance,
    fixedTotal, varTotal, p1Deficit,
    p2Inc, p2Out, p2Surplus,
    sellingCostAmt, waNetEquity, waHalf, waTarget, waEq,
    scEq, scSupportTotal, scWalkaway,
    smSavings,
    tslaFMV, metaFMV, tslaCost, metaCost, tslaGain, metaGain, totalTax,
  };
}

// ═══════════════════ RENDER ALL ═══════════════════
function renderAll() {
  const c = calc();

  // ── ESTATE ──
  set('es-toby-controls', fmt(c.tobyAssets));
  set('es-brandy-controls', fmt(c.brandyAssets));
  set('es-total', fmt(c.totalEstate));
  set('es-target', fmt(c.target));
  set('es-eq', fmt(c.equalization));
  set('es-imbalance', fmt(c.imbalance));
  set('es-imbalance-badge', fmt(c.imbalance) + ' advantage to Brandy');
  set('es-b-controls-detail', fmt(c.brandyAssets));
  set('es-t-controls-detail', fmt(c.tobyAssets));
  set('es-toby-total', fmt(c.tobyAssets));
  set('es-brandy-total', fmt(c.brandyAssets));
  set('es-toby-sum', fmt(c.tobyAssets));
  set('es-brandy-sum', fmt(c.brandyAssets));
  set('es-rkd', fmt(D.rkd)); set('es-tsla', fmt(D.tsla)); set('es-meta', fmt(D.meta));
  set('es-life', fmt(D.life)); set('es-p911', fmt(D.p911)); set('es-ford', fmt(D.ford));
  set('es-p944', fmt(D.p944)); set('es-drz', fmt(D.drz));
  set('es-p944s', fmt(D.p944s)); set('es-odyssey', fmt(D.odyssey));
  set('es-pw50', fmt(D.pw50)); set('es-trailer', fmt(D.trailer));
  set('es-flatbed', 'Gifted to Hudson');
  set('es-sports', fmt(D.sports));
  set('es-paseo-gross', fmt(D.paseo)); set('es-paseo-mort', fmt(-D.paseoMort));
  set('es-paseo-net', fmt(c.paseoNet)); set('es-furn', fmt(D.furn)); set('es-cayenne', fmt(D.cayenne));
  set('es-paseo-model', fmt(D.paseo));

  // ── ESTATE DEPLETION ──
  const paseoInterest = D.paseoInterestAmt;
  const paseoEscrow   = D.paseoEscrowAmt;
  const paseoCarry    = paseoInterest + paseoEscrow;
  const estateBurn    = Math.abs(c.p1Deficit) + paseoCarry;
  const monthsPaid    = D.monthsPaid;
  const eqRemaining   = c.equalization - estateBurn * monthsPaid;
  const breakevenMo   = c.equalization / estateBurn;
  set('es-dep-monthly',        fmt(-estateBurn));
  set('es-dep-annual',         fmt(-estateBurn * 12));
  set('es-dep-breakeven',      breakevenMo.toFixed(1) + ' mo');
  set('es-dep-remaining',      fmt(eqRemaining));
  set('es-dep-toby',           fmt(c.p1Deficit));
  set('es-dep-interest',       fmt(-paseoInterest));
  set('es-dep-escrow',         fmt(-paseoEscrow));
  set('es-dep-carry',          fmt(-paseoCarry));
  set('es-dep-total',          fmt(-estateBurn));
  set('es-dep-paid-mo',        monthsPaid);
  set('es-dep-today-mo',       monthsPaid);
  set('es-dep-monthly-inline', fmt(-estateBurn));
  set('es-dep-interest-inline', Math.round(paseoInterest).toLocaleString('en-US'));
  set('es-dep-escrow-inline',  Math.round(paseoEscrow).toLocaleString('en-US'));
  set('es-dep-toby-inline',    fmt(c.p1Deficit));
  renderEstateBurnChart(c.equalization, estateBurn, monthsPaid);

  // ── CASH FLOW ──
  set('cf-rkdmort', fmt(-D.rkdMort)); set('cf-support', fmt(-D.ssupport));
  set('cf-autoins', fmt(-D.autoIns)); set('cf-blake', fmt(-D.blake));
  set('cf-fixed-sub', fmt(-c.fixedTotal));
  set('cf-groc', fmt(-D.groc)); set('cf-shop', fmt(-D.shop)); set('cf-travel', fmt(-D.travel));
  set('cf-home', fmt(-D.home)); set('cf-gas', fmt(-D.gas)); set('cf-util', fmt(-D.util));
  set('cf-phone', fmt(-D.phone)); set('cf-cloth', fmt(-D.cloth)); set('cf-dining', fmt(-D.dining));
  set('cf-ent', fmt(-D.ent)); set('cf-autom', fmt(-D.autom)); set('cf-med', fmt(-D.med));
  set('cf-misc', fmt(-D.misc)); set('cf-var-sub', fmt(-c.varTotal));
  set('cf-w2', fmt(D.w2)); set('cf-p1-deficit', fmt(c.p1Deficit));
  // Phase 2 removed for external sharing

  // ── WALKAWAY ──
  set('wa-paseo-val', fmt(D.paseo));
  set('wa-costs-val', D.sellingCosts.toFixed(1) + '%');
  set('wa-mort-val', fmt(D.paseoMort));
  set('wa-gross', fmt(D.paseo));
  set('wa-selling', waMode==='sale' ? fmt(-c.sellingCostAmt) : '$0 (buyout)');
  set('wa-payoff', fmt(-D.paseoMort));
  set('wa-net', fmt(c.waNetEquity));
  set('wa-total-estate', fmt(c.totalEstate));
  set('wa-target', fmt(c.target));
  set('wa-toby-other', fmt(c.tobyAssets));
  set('wa-equalization', fmt(c.waEq));
  const eqEl = $('wa-equalization');
  if (eqEl) eqEl.className = c.waEq >= 0 ? 'pos' : 'neg';

  // ── SCENARIOS ──
  set('sc-paseo-val', fmt(D.paseo));
  set('sc-support-val', fmt(D.ssupport));
  set('sc-months-val', D.settlementMonths + ' mo');
  set('sc-eq', fmt(c.scEq));
  set('sc-support-total', fmt(c.scSupportTotal));
  set('sc-net-after', fmt(c.scWalkaway));
  set('sc-deficit', fmt(c.p1Deficit));
  set('sc-s-paseo', fmt(D.paseo)); set('sc-s-net', fmt(c.paseoNet));
  set('sc-s-target', fmt(c.target)); set('sc-s-eq', fmt(c.scEq));
  set('sc-s-months', D.settlementMonths + ' months');
  set('sc-s-paid', fmt(-c.scSupportTotal)); set('sc-s-walkaway', fmt(c.scWalkaway));

  // ── DEPLETION ──
  // p1Deficit is negative (a deficit), already includes support — no double counting
  const depBurn = Math.abs(c.p1Deficit);
  set('dep-eq', fmt(c.scEq));
  set('dep-deficit', fmt(c.p1Deficit));
  set('dep-support', fmt(-D.ssupport));
  set('dep-burn', fmt(-depBurn));
  set('dep-mo-label', D.settlementMonths);
  set('dep-net-walkaway', fmt(c.scEq - depBurn * D.settlementMonths));
  set('dep-monthly-cost', fmt(-depBurn));
  renderDepletionChart(c.scEq, depBurn);

  // ── SUPPORT MOD ──
  set('sm-new-val', fmt(D.ssupport));
  set('sm-new-display', fmt(D.ssupport));
  set('sm-savings', fmt(c.smSavings));
  set('sm-annual', fmt(c.smSavings * 12));
  set('sm-current-deficit', fmt(c.p1Deficit));
  set('sm-reduction', fmt(c.smSavings));
  set('sm-new-deficit', fmt(c.p1Deficit + c.smSavings));
  set('sm-toby-w2', fmt(D.w2) + '/mo');

  // ── TAX ──
  set('tx-tsla-val', '$' + D.tslaBasis.toFixed(2));
  set('tx-meta-val', '$' + D.metaBasis.toFixed(2));
  set('tx-rate-val', D.capGainsRate.toFixed(1) + '%');
  set('tx-tsla-fmv', fmt(c.tslaFMV)); set('tx-tsla-basis', fmt(-c.tslaCost));
  set('tx-tsla-gain', fmt(c.tslaGain)); set('tx-meta-fmv', fmt(c.metaFMV));
  set('tx-meta-basis', fmt(-c.metaCost)); set('tx-meta-gain', fmt(c.metaGain));
  set('tx-total-tax', fmt(-c.totalTax));
  set('tx-sell-cost', fmt(-c.totalTax) + ' tax owed');
  set('tx-benefit', fmt(c.totalTax));

  // ── PENDING ──
  set('pen-w2', fmt(D.w2) + '/mo');
}

// ═══════════════════ WALKAWAY MODE ═══════════════════
function setWaMode(mode) {
  waMode = mode;
  $('wa-mode-buyout').classList.toggle('active', mode==='buyout');
  $('wa-mode-sale').classList.toggle('active', mode==='sale');
  $('wa-mode-label').textContent = mode==='buyout' ? 'Buyout Mode' : 'Sale Mode';
  // Show selling costs slider and row only in sale mode
  const cg = $('wa-costs-group');
  if (cg) cg.style.display = mode==='sale' ? '' : 'none';
  const sr = $('wa-selling-row');
  if (sr) sr.style.display = mode==='sale' ? '' : 'none';
  renderAll();
}

// ═══════════════════ TAB NAV ═══════════════════
function show(tab, btn) {
  document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  $('panel-' + tab).classList.add('active');
  btn.classList.add('active');
  btn.scrollIntoView({ behavior:'smooth', block:'nearest', inline:'center' });
}

// ═══════════════════ BUSINESS CHART ═══════════════════
function buildBizChart() {
  const items = [
    {name:'Advertising',val:272411,color:'#f85149'},{name:'Utilities',val:14044,color:'#e3b341'},
    {name:'Insurance',val:10187,color:'#d29922'},{name:'Repairs',val:9303,color:'#58a6ff'},
    {name:'Travel',val:4508,color:'#3fb950'},{name:'Automobile',val:4065,color:'#bc8cff'},
    {name:'Other',val:10531,color:'#8b949e'},
  ];
  const max = items[0].val;
  $('biz-chart').innerHTML = items.map(i =>
    `<div class="bar-row"><div class="bar-name">${i.name}</div>
    <div class="bar-track"><div class="bar-fill" style="width:${(i.val/max*100).toFixed(1)}%;background:${i.color}"></div></div>
    <div class="bar-val">${fmt(i.val)}</div></div>`
  ).join('');
}

// ═══════════════════ SHARE ═══════════════════
async function shareModel() {
  const blob = new Blob([document.documentElement.outerHTML], {type:'text/html'});
  const file = new File([blob], 'divorce_model_Mar272026.html', {type:'text/html'});
  const btn = document.querySelector('[onclick="shareModel()"]');
  if (navigator.canShare && navigator.canShare({files:[file]})) {
    try { await navigator.share({files:[file],title:'Divorce Financial Model'}); return; }
    catch(e) { if(e.name==='AbortError') return; }
  }
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a'); a.href=url; a.download='divorce_model_Mar272026.html'; a.click();
  URL.revokeObjectURL(url);
  btn.textContent='✓ Saved — attach & send';
  setTimeout(()=>btn.textContent='⬆ Share',3000);
}


// ═══════════════════ DEPLETION CHART ═══════════════════
function renderDepletionChart(equalization, burnPerMonth) {
  const canvas = document.getElementById('dep-chart');
  if (!canvas) return;
  const dpr = window.devicePixelRatio || 1;
  const W = canvas.offsetWidth || 600;
  const H = 200;
  canvas.width  = W * dpr;
  canvas.height = H * dpr;
  canvas.style.width  = W + 'px';
  canvas.style.height = H + 'px';
  const ctx = canvas.getContext('2d');
  ctx.scale(dpr, dpr);

  const months = 24;
  const pad = { top: 16, right: 16, bottom: 32, left: 68 };
  const cW = W - pad.left - pad.right;
  const cH = H - pad.top - pad.bottom;

  // Build data
  const values = [];
  for (let m = 0; m <= months; m++) values.push(equalization - burnPerMonth * m);

  const maxV = Math.max(...values, 0);
  const minV = Math.min(...values, 0);
  const range = maxV - minV || 1;

  function xPos(m)  { return pad.left + (m / months) * cW; }
  function yPos(v)  { return pad.top + cH - ((v - minV) / range) * cH; }

  // Background
  ctx.clearRect(0, 0, W, H);

  // Zero line
  const y0 = yPos(0);
  ctx.beginPath(); ctx.moveTo(pad.left, y0); ctx.lineTo(pad.left + cW, y0);
  ctx.strokeStyle = '#f8514955'; ctx.lineWidth = 1; ctx.setLineDash([4,4]);
  ctx.stroke(); ctx.setLineDash([]);

  // Shade below zero red
  if (minV < 0) {
    const yZero = yPos(0);
    ctx.save();
    ctx.beginPath(); ctx.rect(pad.left, yZero, cW, pad.top + cH - yZero);
    ctx.clip();
    ctx.fillStyle = 'rgba(248,81,73,0.07)'; ctx.fillRect(pad.left, yZero, cW, pad.top + cH - yZero);
    ctx.restore();
  }

  // Gradient fill under curve
  const grad = ctx.createLinearGradient(0, pad.top, 0, pad.top + cH);
  grad.addColorStop(0, 'rgba(88,166,255,0.25)');
  grad.addColorStop(1, 'rgba(88,166,255,0.02)');
  ctx.beginPath();
  ctx.moveTo(xPos(0), yPos(0));
  values.forEach((v, m) => ctx.lineTo(xPos(m), yPos(v)));
  ctx.lineTo(xPos(months), yPos(minV < 0 ? minV : 0));
  ctx.lineTo(xPos(0), yPos(minV < 0 ? minV : 0));
  ctx.closePath();
  ctx.fillStyle = grad; ctx.fill();

  // Curve line
  ctx.beginPath();
  values.forEach((v, m) => m === 0 ? ctx.moveTo(xPos(m), yPos(v)) : ctx.lineTo(xPos(m), yPos(v)));
  ctx.strokeStyle = '#58a6ff'; ctx.lineWidth = 2; ctx.setLineDash([]);
  ctx.stroke();

  // Current settlement month dot
  const cm = D.settlementMonths;
  const cv = equalization - burnPerMonth * cm;
  ctx.beginPath();
  ctx.arc(xPos(cm), yPos(cv), 5, 0, Math.PI*2);
  ctx.fillStyle = '#d29922'; ctx.fill();

  // X axis labels
  ctx.fillStyle = '#8b949e'; ctx.font = '10px -apple-system,sans-serif'; ctx.textAlign = 'center';
  [0,3,6,9,12,15,18,21,24].forEach(m => {
    ctx.fillText('mo ' + m, xPos(m), H - pad.bottom + 14);
  });

  // Y axis labels
  ctx.textAlign = 'right';
  const ticks = 4;
  for (let i = 0; i <= ticks; i++) {
    const v = minV + (range / ticks) * i;
    const y = yPos(v);
    ctx.fillText(fmtK(v), pad.left - 6, y + 3);
    ctx.beginPath(); ctx.moveTo(pad.left - 3, y); ctx.lineTo(pad.left, y);
    ctx.strokeStyle = '#30363d'; ctx.lineWidth = 1; ctx.stroke();
  }
}

function fmtK(n) {
  const abs = Math.abs(n);
  const sign = n < 0 ? '-$' : '$';
  if (abs >= 1000000) return sign + (abs/1000000).toFixed(1) + 'M';
  if (abs >= 1000)    return sign + Math.round(abs/1000) + 'K';
  return sign + Math.round(abs);
}

// ═══════════════════ ESTATE BURN CHART ═══════════════════
function renderEstateBurnChart(equalization, burnPerMonth, monthsPaid) {
  const canvas = document.getElementById('es-dep-chart');
  if (!canvas) return;
  const dpr = window.devicePixelRatio || 1;
  const W = canvas.offsetWidth || 600;
  const H = 220;
  canvas.width  = W * dpr;
  canvas.height = H * dpr;
  canvas.style.width  = W + 'px';
  canvas.style.height = H + 'px';
  const ctx = canvas.getContext('2d');
  ctx.scale(dpr, dpr);

  const months = 24;
  const pad = { top: 20, right: 16, bottom: 34, left: 72 };
  const cW = W - pad.left - pad.right;
  const cH = H - pad.top - pad.bottom;

  // Data: equalization remaining (decreasing) and cumulative burn (increasing)
  const eqLine    = [];
  const burnLine  = [];
  for (let m = 0; m <= months; m++) {
    eqLine.push(equalization - burnPerMonth * m);
    burnLine.push(burnPerMonth * m);
  }

  const maxV = Math.max(equalization, burnPerMonth * months);
  const minV = Math.min(...eqLine, 0);
  const range = maxV - minV || 1;

  function xPos(m) { return pad.left + (m / months) * cW; }
  function yPos(v) { return pad.top + cH - ((v - minV) / range) * cH; }

  ctx.clearRect(0, 0, W, H);

  // Zero line
  ctx.beginPath(); ctx.moveTo(pad.left, yPos(0)); ctx.lineTo(pad.left + cW, yPos(0));
  ctx.strokeStyle = '#30363d'; ctx.lineWidth = 1; ctx.setLineDash([3,3]);
  ctx.stroke(); ctx.setLineDash([]);

  // Red zone (eq goes negative)
  const crossMonth = equalization / burnPerMonth;
  if (crossMonth <= months) {
    const xCross = xPos(crossMonth);
    ctx.save();
    ctx.beginPath(); ctx.rect(xCross, pad.top, pad.left + cW - xCross, cH);
    ctx.clip();
    ctx.fillStyle = 'rgba(248,81,73,0.07)';
    ctx.fillRect(xCross, pad.top, pad.left + cW - xCross, cH);
    ctx.restore();
  }

  // Draw cumulative burn line (red, fills below)
  const burnGrad = ctx.createLinearGradient(0, pad.top, 0, pad.top + cH);
  burnGrad.addColorStop(0, 'rgba(248,81,73,0.18)');
  burnGrad.addColorStop(1, 'rgba(248,81,73,0.02)');
  ctx.beginPath();
  ctx.moveTo(xPos(0), yPos(0));
  burnLine.forEach((v, m) => ctx.lineTo(xPos(m), yPos(v)));
  ctx.lineTo(xPos(months), yPos(0));
  ctx.closePath();
  ctx.fillStyle = burnGrad; ctx.fill();
  ctx.beginPath();
  burnLine.forEach((v, m) => m === 0 ? ctx.moveTo(xPos(m), yPos(v)) : ctx.lineTo(xPos(m), yPos(v)));
  ctx.strokeStyle = '#f85149'; ctx.lineWidth = 2; ctx.setLineDash([]);
  ctx.stroke();

  // Draw equalization remaining line (blue)
  const eqGrad = ctx.createLinearGradient(0, pad.top, 0, pad.top + cH);
  eqGrad.addColorStop(0, 'rgba(88,166,255,0.18)');
  eqGrad.addColorStop(1, 'rgba(88,166,255,0.02)');
  ctx.beginPath();
  ctx.moveTo(xPos(0), yPos(eqLine[0]));
  eqLine.forEach((v, m) => ctx.lineTo(xPos(m), yPos(v)));
  ctx.lineTo(xPos(months), yPos(Math.max(minV, 0)));
  ctx.lineTo(xPos(0), yPos(Math.max(minV, 0)));
  ctx.closePath();
  ctx.fillStyle = eqGrad; ctx.fill();
  ctx.beginPath();
  eqLine.forEach((v, m) => m === 0 ? ctx.moveTo(xPos(m), yPos(v)) : ctx.lineTo(xPos(m), yPos(v)));
  ctx.strokeStyle = '#58a6ff'; ctx.lineWidth = 2.5;
  ctx.stroke();

  // Crossover dot (where lines meet)
  if (crossMonth > 0 && crossMonth <= months) {
    const crossV = 0;
    ctx.beginPath();
    ctx.arc(xPos(crossMonth), yPos(crossV), 5, 0, Math.PI * 2);
    ctx.fillStyle = '#f85149'; ctx.fill();
    ctx.fillStyle = '#8b949e'; ctx.font = '10px -apple-system,sans-serif'; ctx.textAlign = 'left';
    ctx.fillText('eq. exhausted', xPos(crossMonth) + 7, yPos(crossV) + 4);
  }

  // Today dot
  if (monthsPaid >= 0 && monthsPaid <= months) {
    const todayEq = eqLine[Math.round(monthsPaid)];
    ctx.beginPath();
    ctx.arc(xPos(monthsPaid), yPos(todayEq), 5, 0, Math.PI * 2);
    ctx.fillStyle = '#d29922'; ctx.fill();
  }

  // X axis labels
  ctx.fillStyle = '#8b949e'; ctx.font = '10px -apple-system,sans-serif'; ctx.textAlign = 'center';
  [0,3,6,9,12,15,18,21,24].forEach(m => {
    ctx.fillText('mo ' + m, xPos(m), H - pad.bottom + 14);
  });

  // Y axis labels
  ctx.textAlign = 'right';
  const ticks = 4;
  for (let i = 0; i <= ticks; i++) {
    const v = minV + (range / ticks) * i;
    const y = yPos(v);
    ctx.fillText(fmtK(v), pad.left - 6, y + 3);
    ctx.beginPath(); ctx.moveTo(pad.left - 3, y); ctx.lineTo(pad.left, y);
    ctx.strokeStyle = '#30363d'; ctx.lineWidth = 1; ctx.stroke();
  }
}

// ═══════════════════ PASSWORD GATE ═══════════════════
function checkPw() {
  const val = document.getElementById('pw-input').value;
  // Hash check — password is stored as a simple hash, not plaintext
  if (simpleHash(val) === 691007715) {
    document.getElementById('pw-gate').style.display = 'none';
    document.getElementById('main-content').style.display = 'block';
    sessionStorage.setItem('auth', '1');
  } else {
    const err = document.getElementById('pw-error');
    err.textContent = 'Incorrect password — try again';
    document.getElementById('pw-input').value = '';
    document.getElementById('pw-input').focus();
    setTimeout(() => err.textContent = '', 3000);
  }
}

function simpleHash(str) {
  let hash = 0;
  for (let i = 0; i < str.length; i++) {
    hash = ((hash << 5) - hash) + str.charCodeAt(i);
    hash |= 0;
  }
  return hash;
}

// ═══════════════════ INIT ═══════════════════
document.addEventListener('DOMContentLoaded', () => {
  // Check session auth (so refresh doesn't re-prompt within same tab)
  if (sessionStorage.getItem('auth') === '1') {
    document.getElementById('pw-gate').style.display = 'none';
    document.getElementById('main-content').style.display = 'block';
  } else {
    setTimeout(() => document.getElementById('pw-input').focus(), 100);
  }
  syncAllControls();
  renderAll();
  buildBizChart();
  // Hide selling costs slider on load (default is buyout mode)
  const cg = $('wa-costs-group');
  if (cg) cg.style.display = 'none';
  const sr = $('wa-selling-row');
  if (sr) sr.style.display = 'none';
});
</script>
</div><!-- /main-content -->
</body>
</html>
