<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
  <meta name="theme-color" content="#0F766E" />
  <meta name="description" content="Crypto-M-Pesa Control Interface — Multi-chain crypto to M-Pesa bridge" />
  <title>Crypto-M-Pesa | Control Interface</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            brand: {
              50: '#F0FDFA',
              100: '#CCFBF1',
              200: '#99F6E4',
              300: '#5EEAD4',
              400: '#2DD4BF',
              500: '#14B8A6',
              600: '#0D9488',
              700: '#0F766E',
              800: '#115E59',
              900: '#134E4A',
              950: '#042F2E',
            },
            mpesa: '#00A651',
          },
          fontFamily: {
            sans: ['Inter', 'system-ui', 'sans-serif'],
          },
        },
      },
    };
  </script>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet" />
  <style>
    * { box-sizing: border-box; }
    body { font-family: 'Inter', system-ui, sans-serif; }
    .glass { background: rgba(15, 118, 110, 0.08); backdrop-filter: blur(12px); border: 1px solid rgba(20, 184, 166, 0.15); }
    .card { background: linear-gradient(145deg, rgba(19, 78, 74, 0.4) 0%, rgba(15, 23, 42, 0.6) 100%); border: 1px solid rgba(20, 184, 166, 0.12); }
    .glow { box-shadow: 0 0 40px rgba(20, 184, 166, 0.08); }
    .tab-active { background: linear-gradient(135deg, #0F766E, #14B8A6); color: white; }
    input[type="number"]::-webkit-inner-spin-button, input[type="number"]::-webkit-outer-spin-button { -webkit-appearance: none; margin: 0; }
    input[type="number"] { -moz-appearance: textfield; }
    .chart-bar { transition: height 0.6s cubic-bezier(0.34, 1.56, 0.64, 1); }
    .pulse-dot { animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite; }
    @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.4; } }
    .slide-up { animation: slideUp 0.35s ease-out; }
    @keyframes slideUp { from { opacity: 0; transform: translateY(12px); } to { opacity: 1; transform: translateY(0); } }
    .toast { animation: toastIn 0.3s ease-out; }
    @keyframes toastIn { from { opacity: 0; transform: translateY(20px) scale(0.95); } to { opacity: 1; transform: translateY(0) scale(1); } }
    ::-webkit-scrollbar { width: 6px; height: 6px; }
    ::-webkit-scrollbar-track { background: transparent; }
    ::-webkit-scrollbar-thumb { background: #0F766E; border-radius: 3px; }
  </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen antialiased">
  <header class="sticky top-0 z-50 border-b border-brand-800/40 bg-slate-950/90 backdrop-blur-xl">
    <div class="max-w-6xl mx-auto px-4 h-14 flex items-center justify-between">
      <div class="flex items-center gap-3">
        <div class="w-9 h-9 rounded-xl bg-gradient-to-br from-brand-500 to-brand-700 flex items-center justify-center shadow-lg shadow-brand-500/20">
          <svg class="w-5 h-5 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 8c-1.657 0-3 .895-3 2s1.343 2 3 2 3 .895 3 2-1.343 2-3 2m0-8c1.11 0 2.08.402 2.599 1M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.601-1.009A3.214 3.214 0 0 0 9.4 17.5M12 8V7m0 1v8m0 0v1m0-1c-1.11 0-2.08-.402-2.601-1.009A3.214 3.214 0 0 1 9.4 15.5" />
          </svg>
        </div>
        <div>
          <h1 class="text-sm font-bold tracking-tight">Crypto-M-Pesa</h1>
          <p class="text-[10px] text-brand-400 font-medium">Control Interface</p>
        </div>
      </div>
      <div class="flex items-center gap-3">
        <div class="hidden sm:flex items-center gap-1.5 px-2.5 py-1 rounded-full bg-brand-900/50 border border-brand-700/40">
          <span class="w-1.5 h-1.5 rounded-full bg-emerald-400 pulse-dot"></span>
          <span class="text-[11px] text-brand-300 font-medium">Mainnet</span>
        </div>
        <button id="btn-security" class="flex items-center gap-1.5 px-3 py-1.5 rounded-lg bg-slate-800/80 hover:bg-slate-700/80 border border-slate-700/50 text-xs font-medium transition">
          <svg class="w-3.5 h-3.5 text-brand-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 15v2m-6 4h12a2 2 0 002-2v-6a2 2 0 00-2-2H6a2 2 0 00-2 2v6a2 2 0 002 2zm10-10V7a4 4 0 00-8 0v4h8z" />
          </svg>
          Secured
        </button>
        <div class="w-8 h-8 rounded-full bg-gradient-to-br from-brand-400 to-brand-600 flex items-center justify-center text-xs font-bold text-white">JK</div>
      </div>
    </div>
  </header>

  <main class="max-w-6xl mx-auto px-4 py-5 pb-24">
    <section class="card rounded-2xl p-5 mb-5 glow slide-up">
      <div class="flex flex-col sm:flex-row sm:items-end sm:justify-between gap-4">
        <div>
          <p class="text-xs text-slate-400 font-medium mb-1">Total Portfolio Value</p>
          <div class="flex items-baseline gap-2">
            <h2 id="net-worth" class="text-3xl sm:text-4xl font-extrabold tracking-tight text-white">KSh 847,320</h2>
            <span id="net-change" class="text-sm font-semibold text-emerald-400">+2.4%</span>
          </div>
          <p class="text-xs text-slate-500 mt-1">≈ $6,540.12 USD · Live rates</p>
        </div>
        <div class="flex gap-2">
          <button onclick="showTab('convert')" class="flex-1 sm:flex-none px-4 py-2.5 rounded-xl bg-gradient-to-r from-brand-600 to-brand-500 hover:from-brand-500 hover:to-brand-400 text-white text-sm font-semibold transition">Convert</button>
          <button onclick="showTab('mpesa')" class="flex-1 sm:flex-none px-4 py-2.5 rounded-xl bg-mpesa hover:bg-emerald-500 text-white text-sm font-semibold shadow-lg shadow-emerald-600/20 transition">Cash Out</button>
        </div>
      </div>
      <div class="mt-5 flex items-end gap-1 h-16" id="mini-chart"></div>
    </section>

    <section class="grid grid-cols-2 sm:grid-cols-4 gap-3 mb-5">
      <div class="card rounded-xl p-3.5">
        <div class="flex items-center gap-2 mb-2">
          <div class="w-7 h-7 rounded-full bg-orange-500/20 flex items-center justify-center text-orange-400 text-xs font-bold">₿</div>
          <span class="text-xs text-slate-400">Bitcoin</span>
        </div>
        <p class="text-lg font-bold" id="bal-btc">0.0842</p>
        <p class="text-[11px] text-slate-500">KSh 412,500</p>
      </div>
      <div class="card rounded-xl p-3.5">
        <div class="flex items-center gap-2 mb-2">
          <div class="w-7 h-7 rounded-full bg-indigo-500/20 flex items-center justify-center text-indigo-400 text-xs font-bold">Ξ</div>
          <span class="text-xs text-slate-400">Ethereum</span>
        </div>
        <p class="text-lg font-bold" id="bal-eth">1.245</p>
        <p class="text-[11px] text-slate-500">KSh 298,800</p>
      </div>
      <div class="card rounded-xl p-3.5">
        <div class="flex items-center gap-2 mb-2">
          <div class="w-7 h-7 rounded-full bg-emerald-500/20 flex items-center justify-center text-emerald-400 text-xs font-bold">₮</div>
          <span class="text-xs text-slate-400">USDT</span>
        </div>
        <p class="text-lg font-bold" id="bal-usdt">1,050.00</p>
        <p class="text-[11px] text-slate-500">KSh 136,020</p>
      </div>
      <div class="card rounded-xl p-3.5">
        <div class="flex items-center gap-2 mb-2">
          <div class="w-7 h-7 rounded-full bg-mpesa/20 flex items-center justify-center text-mpesa text-xs font-bold">M</div>
          <span class="text-xs text-slate-400">M-Pesa</span>
        </div>
        <p class="text-lg font-bold" id="bal-mpesa">KSh 12,450</p>
        <p class="text-[11px] text-slate-500">+254 727 ***599</p>
      </div>
    </section>

    <nav class="flex gap-1 p-1 rounded-xl bg-slate-900/80 border border-slate-800 mb-5 overflow-x-auto">
      <button data-tab="dashboard" class="tab-btn tab-active flex-1 min-w-[80px] py-2.5 px-3 rounded-lg text-xs font-semibold transition">Dashboard</button>
      <button data-tab="convert" class="tab-btn flex-1 min-w-[80px] py-2.5 px-3 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition">Convert</button>
      <button data-tab="mpesa" class="tab-btn flex-1 min-w-[80px] py-2.5 px-3 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition">M-Pesa</button>
      <button data-tab="security" class="tab-btn flex-1 min-w-[80px] py-2.5 px-3 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition">Security</button>
    </nav>

    <div id="tab-dashboard" class="tab-panel slide-up">
      <div class="grid sm:grid-cols-2 gap-4 mb-4">
        <div class="card rounded-xl p-4">
          <h3 class="text-sm font-semibold mb-3 text-slate-300">24h Performance</h3>
          <div class="space-y-3">
            <div class="flex justify-between items-center"><span class="text-xs text-slate-400">BTC/KES</span><span class="text-xs font-semibold text-emerald-400">+1.8%</span></div>
            <div class="w-full h-1.5 bg-slate-800 rounded-full overflow-hidden"><div class="h-full bg-emerald-500 rounded-full" style="width:62%"></div></div>
            <div class="flex justify-between items-center"><span class="text-xs text-slate-400">ETH/KES</span><span class="text-xs font-semibold text-emerald-400">+3.1%</span></div>
            <div class="w-full h-1.5 bg-slate-800 rounded-full overflow-hidden"><div class="h-full bg-emerald-500 rounded-full" style="width:78%"></div></div>
            <div class="flex justify-between items-center"><span class="text-xs text-slate-400">USDT/KES</span><span class="text-xs font-semibold text-slate-400">+0.02%</span></div>
            <div class="w-full h-1.5 bg-slate-800 rounded-full overflow-hidden"><div class="h-full bg-slate-500 rounded-full" style="width:50%"></div></div>
          </div>
        </div>
        <div class="card rounded-xl p-4">
          <h3 class="text-sm font-semibold mb-3 text-slate-300">Recent Activity</h3>
          <div class="space-y-2.5" id="activity-feed">
            <div class="flex items-center gap-3 text-xs">
              <div class="w-8 h-8 rounded-lg bg-emerald-500/15 flex items-center justify-center text-emerald-400 shrink-0">↓</div>
              <div class="flex-1 min-w-0"><p class="font-medium truncate">M-Pesa Deposit</p><p class="text-slate-500">STK Push · 2 min ago</p></div>
              <span class="text-emerald-400 font-semibold shrink-0">+5,000</span>
            </div>
            <div class="flex items-center gap-3 text-xs">
              <div class="w-8 h-8 rounded-lg bg-brand-500/15 flex items-center justify-center text-brand-400 shrink-0">⇄</div>
              <div class="flex-1 min-w-0"><p class="font-medium truncate">ETH → USDT</p><p class="text-slate-500">Fusion · 18 min ago</p></div>
              <span class="text-slate-300 font-semibold shrink-0">0.12 ETH</span>
            </div>
            <div class="flex items-center gap-3 text-xs">
              <div class="w-8 h-8 rounded-lg bg-orange-500/15 flex items-center justify-center text-orange-400 shrink-0">↑</div>
              <div class="flex-1 min-w-0"><p class="font-medium truncate">Withdraw to M-Pesa</p><p class="text-slate-500">B2C · 1 hr ago</p></div>
              <span class="text-orange-400 font-semibold shrink-0">-8,500</span>
            </div>
          </div>
        </div>
      </div>
      <div class="card rounded-xl p-4">
        <div class="flex items-center justify-between mb-3"><h3 class="text-sm font-semibold text-slate-300">Live Rates (KES)</h3><span class="text-[10px] text-brand-400 flex items-center gap-1"><span class="w-1.5 h-1.5 rounded-full bg-brand-400 pulse-dot"></span> Live</span></div>
        <div class="grid grid-cols-3 gap-3 text-center">
          <div class="bg-slate-900/50 rounded-lg p-3"><p class="text-[10px] text-slate-500 mb-0.5">BTC</p><p class="text-sm font-bold" id="rate-btc">4,899,050</p></div>
          <div class="bg-slate-900/50 rounded-lg p-3"><p class="text-[10px] text-slate-500 mb-0.5">ETH</p><p class="text-sm font-bold" id="rate-eth">239,920</p></div>
          <div class="bg-slate-900/50 rounded-lg p-3"><p class="text-[10px] text-slate-500 mb-0.5">USDT</p><p class="text-sm font-bold" id="rate-usdt">129.54</p></div>
        </div>
      </div>
    </div>

    <div id="tab-convert" class="tab-panel hidden slide-up">
      <div class="card rounded-2xl p-5 max-w-md mx-auto glow">
        <h3 class="text-sm font-semibold mb-4 text-center">Instant Convert</h3>
        <div class="bg-slate-900/70 rounded-xl p-4 mb-1 border border-slate-800">
          <div class="flex justify-between mb-2"><span class="text-[11px] text-slate-500">From</span><span class="text-[11px] text-slate-500">Balance: <span id="from-bal" class="text-slate-300">1.245 ETH</span></span></div>
          <div class="flex items-center gap-3">
            <input type="number" id="from-amount" value="0.25" min="0" step="any" class="flex-1 bg-transparent text-2xl font-bold outline-none placeholder-slate-600 w-full" placeholder="0.00" oninput="calcConvert()" />
            <select id="from-token" onchange="calcConvert()" class="bg-slate-800 border border-slate-700 rounded-lg px-3 py-2 text-sm font-semibold outline-none cursor-pointer">
              <option value="ETH">ETH</option>
              <option value="BTC">BTC</option>
              <option value="USDT">USDT</option>
            </select>
          </div>
        </div>

        <div class="flex justify-center -my-2 relative z-10">
          <button onclick="swapDirection()" class="w-9 h-9 rounded-full bg-brand-700 border-4 border-slate-950 flex items-center justify-center hover:bg-brand-600 transition">
            <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M7 16V4m0 0L3 8m4-4l4 4m6 0v12m0 0l4-4m-4 4l-4-4" /></svg>
          </button>
        </div>

        <div class="bg-slate-900/70 rounded-xl p-4 mb-4 border border-slate-800">
          <div class="flex justify-between mb-2"><span class="text-[11px] text-slate-500">To</span><span class="text-[11px] text-slate-500">You receive</span></div>
          <div class="flex items-center gap-3">
            <input type="number" id="to-amount" readonly class="flex-1 bg-transparent text-2xl font-bold outline-none text-brand-300 w-full" value="59,980" />
            <select id="to-token" onchange="calcConvert()" class="bg-slate-800 border border-slate-700 rounded-lg px-3 py-2 text-sm font-semibold outline-none cursor-pointer">
              <option value="KES">KES</option>
              <option value="USDT">USDT</option>
              <option value="ETH">ETH</option>
            </select>
          </div>
        </div>

        <div class="bg-brand-950/40 border border-brand-800/30 rounded-xl p-3 mb-4 text-xs space-y-1.5">
          <div class="flex justify-between"><span class="text-slate-400">Route</span><span class="text-brand-300 font-medium">1inch Fusion · MEV Protected</span></div>
          <div class="flex justify-between"><span class="text-slate-400">Rate</span><span id="convert-rate" class="font-medium">1 ETH = 239,920 KES</span></div>
          <div class="flex justify-between"><span class="text-slate-400">Est. fee</span><span class="font-medium">~0.3% · Gasless</span></div>
          <div class="flex justify-between"><span class="text-slate-400">Min received</span><span id="min-received" class="font-medium text-emerald-400">59,680 KES</span></div>
        </div>

        <button onclick="executeConvert()" id="btn-convert" class="w-full py-3.5 rounded-xl bg-gradient-to-r from-brand-600 to-brand-500 hover:from-brand-500 hover:to-brand-400 text-white font-semibold text-sm shadow-lg shadow-brand-600/30 transition active:scale-[0.98]">Convert with Fusion</button>
        <p class="text-[10px] text-center text-slate-500 mt-3">Signed via biometric · Intent never enters public mempool</p>
      </div>
    </div>

    <div id="tab-mpesa" class="tab-panel hidden slide-up">
      <div class="max-w-md mx-auto space-y-4">
        <div class="card rounded-xl p-4 flex items-center gap-3">
          <div class="w-11 h-11 rounded-xl bg-mpesa/20 flex items-center justify-center"><svg class="w-6 h-6 text-mpesa" fill="currentColor" viewBox="0 0 24 24"><path d="M17 1.01L7 1c-1.1 0-2 .9-2 2v18c0 1.1.9 2 2 2h10c1.1 0 2-.9 2-2V3c0-1.1-.9-1.99-2-1.99zM17 19H7V5h10v14z"/></svg></div>
          <div class="flex-1"><p class="text-xs text-slate-400">Linked M-Pesa Number</p><p class="font-semibold tracking-wide">+254 727 357 599</p></div>
          <span class="text-[10px] px-2 py-0.5 rounded-full bg-emerald-500/15 text-emerald-400 font-medium">Verified</span>
        </div>

        <div class="flex gap-1 p-1 rounded-xl bg-slate-900 border border-slate-800">
          <button id="mode-deposit" onclick="setMpesaMode('deposit')" class="flex-1 py-2.5 rounded-lg text-xs font-semibold tab-active transition">Deposit via STK</button>
          <button id="mode-withdraw" onclick="setMpesaMode('withdraw')" class="flex-1 py-2.5 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition">Withdraw to M-Pesa</button>
        </div>

        <div class="card rounded-2xl p-5">
          <p class="text-xs text-slate-400 mb-2" id="mpesa-label">Amount to deposit (KES)</p>
          <div class="flex items-baseline gap-2 mb-4"><span class="text-xl text-slate-500 font-medium">KSh</span><input type="number" id="mpesa-amount" value="5000" min="10" step="1" class="flex-1 bg-transparent text-3xl font-extrabold outline-none w-full" oninput="updateMpesaCalc()" /></div>
          <div class="flex gap-2 mb-4">
            <button onclick="setMpesaAmt(1000)" class="flex-1 py-1.5 rounded-lg bg-slate-800 hover:bg-slate-700 text-xs font-medium transition">1,000</button>
            <button onclick="setMpesaAmt(5000)" class="flex-1 py-1.5 rounded-lg bg-slate-800 hover:bg-slate-700 text-xs font-medium transition">5,000</button>
            <button onclick="setMpesaAmt(10000)" class="flex-1 py-1.5 rounded-lg bg-slate-800 hover:bg-slate-700 text-xs font-medium transition">10,000</button>
            <button onclick="setMpesaAmt(25000)" class="flex-1 py-1.5 rounded-lg bg-slate-800 hover:bg-slate-700 text-xs font-medium transition">25,000</button>
          </div>

          <div id="withdraw-calc" class="hidden bg-slate-900/60 border border-slate-800 rounded-xl p-3 mb-4 text-xs space-y-1.5">
            <div class="flex justify-between"><span class="text-slate-400">Crypto source</span><span class="font-medium">USDT balance</span></div>
            <div class="flex justify-between"><span class="text-slate-400">USDT required</span><span id="usdt-needed" class="font-medium text-brand-300">38.60 USDT</span></div>
            <div class="flex justify-between"><span class="text-slate-400">Route</span><span class="font-medium">Fusion → Daraja B2C</span></div>
            <div class="flex justify-between"><span class="text-slate-400">Est. arrival</span><span class="font-medium text-emerald-400">&lt; 30 seconds</span></div>
          </div>

          <button onclick="executeMpesa()" id="btn-mpesa" class="w-full py-3.5 rounded-xl bg-mpesa hover:bg-emerald-500 text-white font-semibold text-sm shadow-lg shadow-emerald-600/25 transition active:scale-[0.98]">Deposit via STK Push</button>
          <p class="text-[10px] text-center text-slate-500 mt-3" id="mpesa-hint">Safaricom will send an STK prompt to +254 727 357 599</p>
        </div>
      </div>
    </div>

    <div id="tab-security" class="tab-panel hidden slide-up">
      <div class="max-w-md mx-auto space-y-4">
        <div class="card rounded-xl p-4">
          <h3 class="text-sm font-semibold mb-3">Authorization Status</h3>
          <div class="space-y-3">
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-2.5">
                <div class="w-8 h-8 rounded-lg bg-emerald-500/15 flex items-center justify-center"><svg class="w-4 h-4 text-emerald-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/></svg></div>
                <div><p class="text-xs font-medium">Biometric</p><p class="text-[10px] text-slate-500">Face ID / Fingerprint</p></div>
              </div>
              <span class="text-[10px] px-2 py-0.5 rounded-full bg-emerald-500/15 text-emerald-400 font-medium">Active</span>
            </div>
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-2.5">
                <div class="w-8 h-8 rounded-lg bg-emerald-500/15 flex items-center justify-center"><svg class="w-4 h-4 text-emerald-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7"/></svg></div>
                <div><p class="text-xs font-medium">Transaction PIN</p><p class="text-[10px] text-slate-500">6-digit · Last used today</p></div>
              </div>
              <span class="text-[10px] px-2 py-0.5 rounded-full bg-emerald-500/15 text-emerald-400 font-medium">Set</span>
            </div>
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-2.5">
                <div class="w-8 h-8 rounded-lg bg-brand-500/15 flex items-center justify-center"><svg class="w-4 h-4 text-brand-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M15 7a2 2 0 012 2m4 0a2 2 0 01.9 1.4l.1.6v5.4a2 2 0 01-2 2H4a2 2 0 01-2-2v-5.4a2 2 0 012-2h1.1M8 9V6a4 4 0 118 0v3"/></svg></div>
                <div><p class="text-xs font-medium">Private Key Vault</p><p class="text-[10px] text-slate-500">Device-bound · Non-custodial</p></div>
              </div>
              <span class="text-[10px] px-2 py-0.5 rounded-full bg-brand-500/15 text-brand-400 font-medium">Locked</span>
            </div>
          </div>
        </div>

        <div class="card rounded-xl p-4">
          <h3 class="text-sm font-semibold mb-3">Session &amp; Device</h3>
          <div class="space-y-2 text-xs">
            <div class="flex justify-between py-1.5 border-b border-slate-800/50"><span class="text-slate-400">Device</span><span class="font-medium">iPhone 16 · Safari</span></div>
            <div class="flex justify-between py-1.5 border-b border-slate-800/50"><span class="text-slate-400">Session</span><span class="font-medium text-emerald-400">Trusted · 2h remaining</span></div>
            <div class="flex justify-between py-1.5 border-b border-slate-800/50"><span class="text-slate-400">RPC Path</span><span class="font-medium">Flashbots Protect</span></div>
            <div class="flex justify-between py-1.5"><span class="text-slate-400">Last signed tx</span><span class="font-medium">18 min ago</span></div>
          </div>
        </div>

        <div class="card rounded-xl p-4">
          <h3 class="text-sm font-semibold mb-3">Signing Preferences</h3>
          <label class="flex items-center justify-between py-2 cursor-pointer"><span class="text-xs">Require biometric for all swaps</span><input type="checkbox" checked class="w-4 h-4 rounded accent-brand-500" /></label>
          <label class="flex items-center justify-between py-2 cursor-pointer"><span class="text-xs">Prefer intent-based (Fusion / CoW)</span><input type="checkbox" checked class="w-4 h-4 rounded accent-brand-500" /></label>
          <label class="flex items-center justify-between py-2 cursor-pointer"><span class="text-xs">Auto-confirm under KSh 2,000</span><input type="checkbox" class="w-4 h-4 rounded accent-brand-500" /></label>
        </div>

        <button onclick="showToast('Session locked. Re-authenticate to continue.', 'info')" class="w-full py-3 rounded-xl border border-slate-700 hover:bg-slate-800/50 text-sm font-medium transition">Lock Session</button>
      </div>
    </div>
  </main>

  <div class="h-6"></div>
  <div id="toast-container" class="fixed bottom-6 left-1/2 -translate-x-1/2 z-[100] flex flex-col gap-2 pointer-events-none w-full max-w-sm px-4"></div>
  <div id="modal" class="fixed inset-0 z-[90] hidden items-center justify-center bg-black/60 backdrop-blur-sm p-4">
    <div class="card rounded-2xl p-6 max-w-sm w-full glow slide-up">
      <h3 id="modal-title" class="text-base font-bold mb-2">Confirm Transaction</h3>
      <p id="modal-body" class="text-sm text-slate-400 mb-5"></p>
      <div class="flex gap-3">
        <button onclick="closeModal()" class="flex-1 py-2.5 rounded-xl border border-slate-700 text-sm font-medium hover:bg-slate-800 transition">Cancel</button>
        <button id="modal-confirm" class="flex-1 py-2.5 rounded-xl bg-brand-600 hover:bg-brand-500 text-white text-sm font-semibold transition">Confirm</button>
      </div>
    </div>
  </div>

  <script>
    const RATES = { BTC: 4899050, ETH: 239920, USDT: 129.54, KES: 1 };
    let mpesaMode = 'deposit';

    (function buildChart() {
      const el = document.getElementById('mini-chart');
      const heights = [28,35,30,42,38,50,45,55,48,62,58,70,65,72,68,80,75,85,78,90,82,88,85,92];
      heights.forEach((h, i) => {
        const bar = document.createElement('div');
        bar.className = 'chart-bar flex-1 rounded-t bg-gradient-to-t from-brand-700 to-brand-400 opacity-80';
        bar.style.height = '4px';
        el.appendChild(bar);
        setTimeout(() => { bar.style.height = h + '%'; }, 50 + i * 20);
      });
    })();

    function showTab(name) {
      document.querySelectorAll('.tab-panel').forEach(p => p.classList.add('hidden'));
      document.getElementById('tab-' + name).classList.remove('hidden');
      document.querySelectorAll('.tab-btn').forEach(b => {
        b.classList.remove('tab-active');
        b.classList.add('text-slate-400');
        if (b.dataset.tab === name) { b.classList.add('tab-active'); b.classList.remove('text-slate-400'); }
      });
    }
    document.querySelectorAll('.tab-btn').forEach(b => b.addEventListener('click', () => showTab(b.dataset.tab)));
    document.getElementById('btn-security').addEventListener('click', () => showTab('security'));

    function calcConvert() {
      const fromTok = document.getElementById('from-token').value;
      const toTok = document.getElementById('to-token').value;
      const amt = parseFloat(document.getElementById('from-amount').value) || 0;
      const fromRate = RATES[fromTok] || 1;
      const toRate = RATES[toTok] || 1;
      const result = (amt * fromRate) / toRate;
      const formatted = toTok === 'KES' ? Math.round(result).toLocaleString() : result.toFixed(toTok === 'BTC' ? 6 : 4);
      document.getElementById('to-amount').value = formatted;
      document.getElementById('convert-rate').textContent = `1 ${fromTok} = ${(fromRate / toRate).toLocaleString(undefined, { maximumFractionDigits: 2 })} ${toTok}`;
      const minR = result * 0.995;
      document.getElementById('min-received').textContent = (toTok === 'KES' ? Math.round(minR).toLocaleString() : minR.toFixed(4)) + ' ' + toTok;
      const bals = { ETH: '1.245 ETH', BTC: '0.0842 BTC', USDT: '1,050.00 USDT' };
      document.getElementById('from-bal').textContent = bals[fromTok] || '—';
    }

    function swapDirection() {
      const ft = document.getElementById('from-token');
      const tt = document.getElementById('to-token');
      const fa = document.getElementById('from-amount');
      const tmp = ft.value;
      ft.value = tt.value === 'KES' ? 'USDT' : tt.value;
      tt.value = tmp === 'ETH' || tmp === 'BTC' ? 'KES' : tmp;
      fa.value = '';
      calcConvert();
    }

    function executeConvert() {
      const from = document.getElementById('from-amount').value;
      const fromTok = document.getElementById('from-token').value;
      const to = document.getElementById('to-amount').value;
      const toTok = document.getElementById('to-token').value;
      openModal('Confirm Conversion', `Convert ${from} ${fromTok} → ${to} ${toTok} via 1inch Fusion (MEV-protected, gasless). Biometric approval required.`, () => {
        closeModal();
        showToast('Intent signed. Resolver filling…', 'info');
        setTimeout(() => {
          showToast(`Converted ${from} ${fromTok} → ${to} ${toTok}`, 'success');
          addActivity('⇄', `${fromTok} → ${toTok}`, 'Fusion · just now', from + ' ' + fromTok);
        }, 2200);
      });
    }

    function setMpesaMode(mode) {
      mpesaMode = mode;
      const dep = document.getElementById('mode-deposit');
      const wit = document.getElementById('mode-withdraw');
      const calc = document.getElementById('withdraw-calc');
      const btn = document.getElementById('btn-mpesa');
      const label = document.getElementById('mpesa-label');
      const hint = document.getElementById('mpesa-hint');
      if (mode === 'deposit') {
        dep.classList.add('tab-active'); dep.classList.remove('text-slate-400');
        wit.classList.remove('tab-active'); wit.classList.add('text-slate-400');
        calc.classList.add('hidden');
        btn.textContent = 'Deposit via STK Push';
        btn.className = 'w-full py-3.5 rounded-xl bg-mpesa hover:bg-emerald-500 text-white font-semibold text-sm shadow-lg shadow-emerald-600/25 transition active:scale-[0.98]';
        label.textContent = 'Amount to deposit (KES)';
        hint.textContent = 'Safaricom will send an STK prompt to +254 727 357 599';
      } else {
        wit.classList.add('tab-active'); wit.classList.remove('text-slate-400');
        dep.classList.remove('tab-active'); dep.classList.add('text-slate-400');
        calc.classList.remove('hidden');
        btn.textContent = 'Withdraw to M-Pesa';
        btn.className = 'w-full py-3.5 rounded-xl bg-gradient-to-r from-brand-600 to-brand-500 hover:from-brand-500 hover:to-brand-400 text-white font-semibold text-sm shadow-lg shadow-brand-600/30 transition active:scale-[0.98]';
        label.textContent = 'Amount to withdraw (KES)';
        hint.textContent = 'USDT → Fusion swap → Daraja B2C to +254 727 357 599';
        updateMpesaCalc();
      }
    }

    function setMpesaAmt(n) {
      document.getElementById('mpesa-amount').value = n;
      updateMpesaCalc();
    }

    function updateMpesaCalc() {
      const kes = parseFloat(document.getElementById('mpesa-amount').value) || 0;
      const usdt = (kes / RATES.USDT).toFixed(2);
      document.getElementById('usdt-needed').textContent = usdt + ' USDT';
    }

    function executeMpesa() {
      const amt = parseFloat(document.getElementById('mpesa-amount').value) || 0;
      if (amt < 10) { showToast('Minimum amount is KSh 10', 'error'); return; }
      if (mpesaMode === 'deposit') {
        openModal('STK Push Deposit', `Deposit KSh ${amt.toLocaleString()} from M-Pesa (+254 727 357 599). You will receive an STK prompt on your phone.`, () => {
          closeModal();
          showToast('STK Push sent. Check your phone…', 'info');
          setTimeout(() => {
            showToast(`KSh ${amt.toLocaleString()} deposited successfully`, 'success');
            addActivity('↓', 'M-Pesa Deposit', 'STK Push · just now', '+' + amt.toLocaleString());
            const bal = document.getElementById('bal-mpesa');
            const current = parseInt(bal.textContent.replace(/[^\d]/g, '')) || 0;
            bal.textContent = 'KSh ' + (current + amt).toLocaleString();
          }, 3000);
        });
      } else {
        const usdt = (amt / RATES.USDT).toFixed(2);
        openModal('Withdraw to M-Pesa', `Convert ${usdt} USDT → KSh ${amt.toLocaleString()} and send via Daraja B2C to +254 727 357 599. Biometric + PIN required.`, () => {
          closeModal();
          showToast('Signing intent… Fusion filling…', 'info');
          setTimeout(() => {
            showToast('Swap confirmed. Sending to M-Pesa…', 'info');
            setTimeout(() => {
              showToast(`KSh ${amt.toLocaleString()} sent to M-Pesa`, 'success');
              addActivity('↑', 'Withdraw to M-Pesa', 'B2C · just now', '-' + amt.toLocaleString());
              const bal = document.getElementById('bal-mpesa');
              const current = parseInt(bal.textContent.replace(/[^\d]/g, '')) || 0;
              bal.textContent = 'KSh ' + (current + amt).toLocaleString();
            }, 2000);
          }, 2000);
        });
      }
    }

    function addActivity(icon, title, sub, amount) {
      const feed = document.getElementById('activity-feed');
      const colors = { '↓': 'emerald', '↑': 'orange', '⇄': 'brand' };
      const c = colors[icon] || 'brand';
      const row = document.createElement('div');
      row.className = 'flex items-center gap-3 text-xs slide-up';
      row.innerHTML = `<div class="w-8 h-8 rounded-lg bg-${c}-500/15 flex items-center justify-center text-${c}-400 shrink-0">${icon}</div><div class="flex-1 min-w-0"><p class="font-medium truncate">${title}</p><p class="text-slate-500">${sub}</p></div><span class="text-${c}-400 font-semibold shrink-0">${amount}</span>`;
      feed.insertBefore(row, feed.firstChild);
    }

    let modalCb = null;
    function openModal(title, body, onConfirm) {
      document.getElementById('modal-title').textContent = title;
      document.getElementById('modal-body').textContent = body;
      modalCb = onConfirm;
      const m = document.getElementById('modal');
      m.classList.remove('hidden');
      m.classList.add('flex');
    }
    function closeModal() {
      const m = document.getElementById('modal');
      m.classList.add('hidden');
      m.classList.remove('flex');
      modalCb = null;
    }
    document.getElementById('modal-confirm').addEventListener('click', () => { if (modalCb) modalCb(); });
    document.getElementById('modal').addEventListener('click', (e) => { if (e.target === e.currentTarget) closeModal(); });

    function showToast(msg, type = 'info') {
      const colors = { success: 'bg-emerald-600 border-emerald-500', error: 'bg-red-600 border-red-500', info: 'bg-brand-700 border-brand-500' };
      const el = document.createElement('div');
      el.className = `toast pointer-events-auto ${colors[type] || colors.info} text-white text-sm font-medium px-4 py-3 rounded-xl shadow-xl border text-center`;
      el.textContent = msg;
      document.getElementById('toast-container').appendChild(el);
      setTimeout(() => {
        el.style.opacity = '0';
        el.style.transition = 'opacity 0.3s';
        setTimeout(() => el.remove(), 300);
      }, 3200);
    }

    setInterval(() => {
      const jitter = () => 1 + (Math.random() - 0.5) * 0.002;
      RATES.BTC = Math.round(4899050 * jitter());
      RATES.ETH = Math.round(239920 * jitter());
      RATES.USDT = +(129.54 * jitter()).toFixed(2);
      document.getElementById('rate-btc').textContent = RATES.BTC.toLocaleString();
      document.getElementById('rate-eth').textContent = RATES.ETH.toLocaleString();
      document.getElementById('rate-usdt').textContent = RATES.USDT.toFixed(2);
      if (!document.getElementById('tab-convert').classList.contains('hidden')) calcConvert();
      if (mpesaMode === 'withdraw') updateMpesaCalc();
    }, 4000);

    calcConvert();
  </script>
</body>
</html>
name: Deploy static site to GitHub Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Pages
        uses: actions/configure-pages@v5

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: .

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4

