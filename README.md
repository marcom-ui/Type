<!doctype html>

<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Kraken‑Style Market Dashboard (Demo)</title>
  <style>
    /* ---- Minimal professional styling ---- */
    :root{--bg:#0f1724;--card:#0b1220;--muted:#9aa4b2;--accent:#1fb6ff;--glass:rgba(255,255,255,0.03)}
    html,body{height:100%;margin:0;font-family:Inter,ui-sans-serif,system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial;background:linear-gradient(180deg,#071028 0%, #07162a 100%);color:#e6eef6}
    .container{max-width:1100px;margin:28px auto;padding:22px}
    header{display:flex;align-items:center;gap:18px}
    .logo{width:64px;height:64px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#0066ff);display:flex;align-items:center;justify-content:center;font-weight:700;font-size:22px;box-shadow:0 6px 18px rgba(16,30,60,0.6)}
    h1{margin:0;font-size:20px}
    .sub{color:var(--muted);font-size:13px;margin-top:6px}
    .card{background:var(--card);border-radius:12px;padding:14px;box-shadow:0 6px 20px rgba(2,8,23,0.6);margin-top:18px}
    .grid{display:grid;grid-template-columns:1fr 360px;gap:16px}
    .search-row{display:flex;gap:8px;align-items:center}
    input[type=text]{flex:1;padding:10px 12px;border-radius:8px;border:1px solid rgba(255,255,255,0.04);background:var(--glass);color:inherit}
    button{padding:10px 12px;border-radius:8px;border:0;background:linear-gradient(90deg,var(--accent),#0077ff);color:#022033;font-weight:600;cursor:pointer}
    table{width:100%;border-collapse:collapse;margin-top:12px}
    thead th{color:var(--muted);text-align:left;padding:10px 8px;font-size:12px}
    tbody td{padding:10px 8px;border-top:1px solid rgba(255,255,255,0.03)}
    .positive{color:#66f07a}
    .negative{color:#ff7b7b}
    .muted{color:var(--muted);font-size:13px}
    .small{font-size:12px}
    .right{text-align:right}
    .feedback{margin-left:auto}
    .top-info{display:flex;gap:12px;flex-wrap:wrap;margin-top:8px}
    .pill{background:rgba(255,255,255,0.02);padding:8px 10px;border-radius:8px;color:var(--muted);font-size:13px}
    .history{max-height:360px;overflow:auto;margin-top:12px}
    .footer{margin-top:18px;color:var(--muted);font-size:13px}
    @media(max-width:900px){.grid{grid-template-columns:1fr;}.feedback{margin-left:0}}
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="logo">KR</div>
      <div>
        <h1>Kraken — Market Dashboard (demo)</h1>
        <div class="sub">A concise company snapshot and real-time crypto market viewer. Built for demonstration and local use in Spck.</div>
        <div class="top-info">
          <div class="pill">Founded: Oct 1, 2011</div>
          <div class="pill">CEO: David Ripley</div>
          <div class="pill">Partners: Fidelity · Tribe Capital</div>
          <div class="pill">Market Cap (company): $10.8B</div>
        </div>
      </div>
      <div class="feedback">
        <a id="feedbackLink" href="mailto:krakenfeedbackhelp@gmail.com?subject=Kraken%20Dashboard%20Feedback" style="text-decoration:none"><button>Send Feedback</button></a>
      </div>
    </header><div class="card grid">
  <div>
    <div style="display:flex;align-items:center;gap:12px">
      <div style="font-weight:700">Market Watch</div>
      <div class="muted small">Live crypto prices via CoinGecko · Auto-refresh every 60s</div>
    </div>

    <div style="margin-top:12px" class="search-row">
      <input id="searchInput" type="text" placeholder="Search coin by name or symbol (e.g. bitcoin, eth, sol)">
      <button id="searchBtn">Search</button>
      <button id="refreshBtn" title="Refresh now">Refresh</button>
    </div>

    <div class="card" style="margin-top:8px;padding:8px">
      <table id="resultsTable">
        <thead>
          <tr>
            <th>Name</th>
            <th>Symbol</th>
            <th class="right">Price (USD)</th>
            <th class="right">24h</th>
            <th class="right">Market Cap</th>
          </tr>
        </thead>
        <tbody id="resultsBody">
          <tr><td colspan="5" class="muted">Search for a coin and press Search — examples: bitcoin, ethereum, solana, dogecoin</td></tr>
        </tbody>
      </table>
    </div>

    <div class="card" style="margin-top:12px">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <div style="font-weight:700">Recent Trades (demo — 58 entries)</div>
        <div class="muted small">Generated locally using recent market prices</div>
      </div>
      <div class="history">
        <table>
          <thead>
            <tr>
              <th>Time</th>
              <th>Pair</th>
              <th>Side</th>
              <th class="right">Amount</th>
              <th class="right">Price (USD)</th>
              <th class="right">Total (USD)</th>
            </tr>
          </thead>
          <tbody id="tradesBody">
            <!-- 58 rows injected by JS -->
          </tbody>
        </table>
      </div>
    </div>

  </div>

  <aside>
    <div class="card">
      <div style="font-weight:700">Portfolio Snapshot</div>
      <div class="muted small" style="margin-top:6px">Demo holdings based on live prices</div>
      <div style="margin-top:12px">
        <div style="display:flex;justify-content:space-between"><div>BTC</div><div id="p_btc">—</div></div>
        <div style="display:flex;justify-content:space-between"><div>ETH</div><div id="p_eth">—</div></div>
        <div style="display:flex;justify-content:space-between"><div>SOL</div><div id="p_sol">—</div></div>
        <div style="display:flex;justify-content:space-between;margin-top:8px;font-weight:700"><div>Total Value</div><div id="p_total">—</div></div>
      </div>
    </div>

    <div class="card" style="margin-top:12px">
      <div style="font-weight:700">Company Links</div>
      <div class="muted small" style="margin-top:8px">Legal & Contact</div>
      <ul style="padding-left:16px;margin-top:8px;color:var(--muted)">
        <li><a href="#" style="color:inherit">Terms & Privacy</a></li>
        <li><a href="#" style="color:inherit">Audit Reports</a></li>
        <li><a href="#" style="color:inherit">Contact</a></li>
      </ul>
    </div>

  </aside>
</div>

<div class="footer">Note: This is a demo dashboard that uses CoinGecko's public API for crypto prices. Do not enter private keys or sensitive info here. For production you'll need proper API keys, backend rate limiting, and security audits.</div>

  </div>  <script>
    // ---- Configuration ----
    const COINGECKO_BASE = 'https://api.coingecko.com/api/v3';
    const AUTO_REFRESH_MS = 60000; // 60s

    // A curated list of widely-known coins used for trade generation & quick lookup
    const demoCoinIds = ['bitcoin','ethereum','solana','dogecoin','ripple','cardano','polkadot','litecoin','chainlink','uniswap','matic-network','avalanche-2','tron','stellar','vechain','filecoin','algorand','hedera-hashgraph','monero','theta-token'];

    // State
    let latestPrices = {}; // coinId -> price USD

    // Utility: friendly number format
    function fmt(n){
      if (n === null || n === undefined) return '—';
      if (Math.abs(n) >= 1e9) return '$' + (n/1e9).toFixed(2) + 'B';
      if (Math.abs(n) >= 1e6) return '$' + (n/1e6).toFixed(2) + 'M';
      return '$' + Number(n).toLocaleString(undefined, {maximumFractionDigits:2});
    }

    function fmtPrice(n){
      if (n === null || n === undefined) return '—';
      return '$' + Number(n).toLocaleString(undefined, {maximumFractionDigits:2});
    }

    // Fetch simple price data for demoCoinIds in USD
    async function fetchDemoPrices(){
      try{
        const ids = demoCoinIds.join(',');
        const res = await fetch(`${COINGECKO_BASE}/simple/price?ids=${ids}&vs_currencies=usd&include_24hr_change=true&include_market_cap=true`);
        const data = await res.json();
        latestPrices = {};
        Object.keys(data).forEach(id => {
          latestPrices[id] = {
            price: data[id].usd,
            change24h: data[id].usd_24h_change,
            marketCap: data[id].usd_market_cap
          }
        });
        // update portfolio demo values
        updatePortfolio();
      }catch(err){
        console.error('Price fetch failed', err);
      }
    }

    // Search CoinGecko for a coin by name or symbol
    async function searchCoin(query){
      query = (query || '').trim();
      if (!query) return [];
      const res = await fetch(`${COINGECKO_BASE}/search?query=${encodeURIComponent(query)}`);
      const data = await res.json();
      // return top 10 matches
      return (data.coins || []).slice(0,10);
    }

    // Get market data for a specific coin id
    async function getCoinMarketData(id){
      const res = await fetch(`${COINGECKO_BASE}/coins/markets?vs_currency=usd&ids=${encodeURIComponent(id)}&order=market_cap_desc&per_page=1&page=1&sparkline=false`);
      const data = await res.json();
      return data && data[0];
    }

    // Handlers
    document.getElementById('searchBtn').addEventListener('click', async ()=>{
      const q = document.getElementById('searchInput').value.trim();
      if (!q) return alert('Type a coin name or symbol (e.g. bitcoin, eth)');
      const matches = await searchCoin(q);
      const tbody = document.getElementById('resultsBody');
      tbody.innerHTML = '';
      if (!matches.length){
        tbody.innerHTML = '<tr><td colspan="5" class="muted">No results found.</td></tr>';
        return;
      }
      // For each match, fetch market data
      for (const m of matches){
        const market = await getCoinMarketData(m.id);
        const row = document.createElement('tr');
        const change = market ? market.price_change_percentage_24h : null;
        row.innerHTML = `
          <td>${m.name}</td>
          <td>${m.symbol.toUpperCase()}</td>
          <td class="right">${market ? fmtPrice(market.current_price) : '—'}</td>
          <td class="right ${change>=0?'positive':'negative'}">${change!==null && change!==undefined?change.toFixed(2)+'%':'—'}</td>
          <td class="right small">${market ? fmt(market.market_cap) : '—'}</td>
        `;
        tbody.appendChild(row);
      }
    });

    document.getElementById('refreshBtn').addEventListener('click', async ()=>{
      await initData();
    });

    // Portfolio demo (fake holdings but priced by live data)
    const demoHoldings = { bitcoin:0.23, ethereum:3.1, solana:25 };
    function updatePortfolio(){
      const btc = latestPrices['bitcoin']?.price || 0;
      const eth = latestPrices['ethereum']?.price || 0;
      const sol = latestPrices['solana']?.price || 0;
      const v_btc = demoHoldings.bitcoin * btc;
      const v_eth = demoHoldings.ethereum * eth;
      const v_sol = demoHoldings.solana * sol;
      const total = v_btc + v_eth + v_sol;
      document.getElementById('p_btc').textContent = fmtPrice(v_btc) + ' ('+demoHoldings.bitcoin+' BTC)';
      document.getElementById('p_eth').textContent = fmtPrice(v_eth) + ' ('+demoHoldings.ethereum+' ETH)';
      document.getElementById('p_sol').textContent = fmtPrice(v_sol) + ' ('+demoHoldings.solana+' SOL)';
      document.getElementById('p_total').textContent = fmtPrice(total);
    }

    // Generate N demo trades based on latestPrices
    function generateDemoTrades(n = 58){
      const coins = Object.keys(latestPrices).length?Object.keys(latestPrices):demoCoinIds;
      const rows = [];
      for (let i=0;i<n;i++){
        const coinId = coins[Math.floor(Math.random()*coins.length)];
        const priceNow = latestPrices[coinId]?.price || (Math.random()*200);
        // random time within last 7 days
        const t = new Date(Date.now() - Math.floor(Math.random()*7*24*60*60*1000) - Math.floor(Math.random()*60000));
        const side = Math.random()>0.5?'BUY':'SELL';
        // amount chosen so total between $10 and $50k
        const totalUSD = Math.random()*(50000-10)+10;
        const amount = totalUSD / (priceNow || 1);
        const price = priceNow * (1 + (Math.random()-0.5)*0.02); // small slippage
        rows.push({time:t.toISOString(), pair:coinId.toUpperCase()+'/USD', side, amount, price, total: amount*price});
      }
      return rows.sort((a,b)=>new Date(b.time)-new Date(a.time));
    }

    function renderTrades(trades){
      const tbody = document.getElementById('tradesBody');
      tbody.innerHTML = '';
      trades.forEach(tr => {
        const trEl = document.createElement('tr');
        trEl.innerHTML = `
          <td class="small">${new Date(tr.time).toLocaleString()}</td>
          <td>${tr.pair}</td>
          <td>${tr.side}</td>
          <td class="right small">${Number(tr.amount).toFixed(6)}</td>
          <td class="right small">${fmtPrice(tr.price)}</td>
          <td class="right small">${fmtPrice(tr.total)}</td>
        `;
        tbody.appendChild(trEl);
      });
    }

    // Initialize app: fetch demo prices, generate trades, render
    async function initData(){
      await fetchDemoPrices();
      const trades = generateDemoTrades(58);
      renderTrades(trades);
    }

    // Auto-refresh loop
    initData();
    setInterval(async ()=>{ await fetchDemoPrices(); }, AUTO_REFRESH_MS);

  </script></body>
</html>