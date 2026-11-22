[index.hyml.html](https://github.com/user-attachments/files/35234786/index.hyml.html)
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>環航智造科技：科技化訓練危機決策戰情室</title>
  <script src="https://cdn.tailwindcss.com/3.4.17"></script>
  <script src="https://cdn.jsdelivr.net/npm/lucide@0.460.0/dist/umd/lucide.min.js"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=Noto+Sans+TC:wght@400;500;700;900&display=swap');
    html {
      font-size: 18px;
    }
    body {
      font-family: 'Inter', 'Noto Sans TC', -apple-system, BlinkMacSystemFont, sans-serif;
      background-color: #0b1120;
      color: #f1f5f9;
      font-size: 1.05rem;
      line-height: 1.65;
    }
    .glass-panel {
      background: rgba(30, 41, 59, 0.78);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(148, 163, 184, 0.18);
    }
    .card-selectable {
      transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .card-selectable:hover {
      transform: translateY(-2px);
      border-color: rgba(56, 189, 248, 0.5);
    }
    .card-selected {
      background: rgba(14, 116, 144, 0.35) !important;
      border-color: #38bdf8 !important;
      box-shadow: 0 0 0 1px #38bdf8, 0 8px 20px -4px rgba(56, 189, 248, 0.25);
    }
    .custom-scrollbar::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    .custom-scrollbar::-webkit-scrollbar-track {
      background: rgba(15, 23, 42, 0.6);
    }
    .custom-scrollbar::-webkit-scrollbar-thumb {
      background: rgba(100, 116, 139, 0.5);
      border-radius: 3px;
    }
  </style>
</head>
<body class="min-h-screen flex flex-col selection:bg-sky-500 selection:text-white">

  <!-- Top Navigation & Classroom Timer Bar -->
  <header class="sticky top-0 z-40 bg-slate-900/95 border-b border-slate-800 px-4 py-3 backdrop-blur">
    <div class="max-w-7xl mx-auto flex flex-wrap items-center justify-between gap-3">
      <div class="flex items-center gap-3">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-sky-500 to-indigo-600 flex items-center justify-center shadow-lg shadow-sky-500/20">
          <i data-lucide="cpu" class="w-5 h-5 text-white"></i>
        </div>
        <div>
          <div class="flex items-center gap-2">
            <span class="text-xs font-bold uppercase tracking-wider px-2 py-0.5 rounded bg-amber-500/20 text-amber-300 border border-amber-500/30">第7章 嚴肅遊戲實作</span>
            <span class="text-xs text-slate-400">研究所 4–5 人小組決策模擬</span>
          </div>
          <h1 class="text-base sm:text-lg font-bold text-white tracking-tight">《環航智造科技》跨國人才培訓危機決策戰情室</h1>
        </div>
      </div>

      <!-- Mode Switcher Tabs -->
      <nav class="flex items-center bg-slate-800/90 p-1 rounded-xl border border-slate-700/70">
        <button id="tab-game" onclick="switchMainView('game')" class="px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition flex items-center gap-1.5 bg-sky-500 text-white shadow">
          <i data-lucide="gamepad-2" class="w-4 h-4"></i>
          <span>1. 互動決策闖關</span>
        </button>
        <button id="tab-pitch" onclick="switchMainView('pitch')" class="px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition flex items-center gap-1.5 text-slate-300 hover:text-white">
          <i data-lucide="presentation" class="w-4 h-4"></i>
          <span>2. 小組發表簡報看板</span>
        </button>
        <button id="tab-matrix" onclick="switchMainView('matrix')" class="px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition flex items-center gap-1.5 text-slate-300 hover:text-white">
          <i data-lucide="table-2" class="w-4 h-4"></i>
          <span>3. 表7.12 理論秘笈</span>
        </button>
        <button id="tab-lesson" onclick="switchMainView('lesson')" class="px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition flex items-center gap-1.5 text-slate-300 hover:text-white">
          <i data-lucide="clock" class="w-4 h-4"></i>
          <span>4. 50分鐘教師詳案</span>
        </button>
        <button id="tab-quiz" onclick="switchMainView('quiz')" class="px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition flex items-center gap-1.5 text-slate-300 hover:text-white">
          <i data-lucide="list-checks" class="w-4 h-4"></i>
          <span>5. 學習目標檢核</span>
        </button>
      </nav>

      <!-- Classroom Timer & Sound Toggle -->
      <div class="flex items-center gap-2">
        <div class="flex items-center gap-1.5 bg-slate-800 border border-slate-700 rounded-xl px-3 py-1.5">
          <i data-lucide="timer" class="w-4 h-4 text-sky-400"></i>
          <span id="timer-phase-label" class="text-xs text-slate-400 hidden md:inline">戰情闖關</span>
          <span id="timer-display" class="font-mono text-sm font-bold text-amber-400">18:00</span>
          <button onclick="toggleTimer()" id="timer-btn" class="ml-1 text-xs px-2 py-0.5 rounded bg-sky-500/20 text-sky-300 hover:bg-sky-500/30 border border-sky-500/30 font-medium">開始</button>
          <button onclick="resetTimer()" class="text-xs px-1.5 py-0.5 rounded bg-slate-700 text-slate-300 hover:bg-slate-600" title="重設計時">↺</button>
        </div>
        <button onclick="openQrModal()" id="qr-btn" class="px-3 py-1.5 rounded-xl bg-emerald-500/20 border border-emerald-500/40 text-emerald-300 hover:bg-emerald-500/30 text-xs sm:text-sm font-bold flex items-center gap-1.5 shadow" title="開啟課堂投影 QR Code 讓學生掃描">
          <i data-lucide="qr-code" class="w-4 h-4"></i>
          <span>課堂 QR Code</span>
        </button>
        <button onclick="toggleMute()" id="mute-btn" class="p-2 rounded-xl bg-slate-800 border border-slate-700 text-slate-300 hover:text-white" title="切換音效">
          <i data-lucide="volume-2" class="w-4 h-4"></i>
        </button>
      </div>
    </div>
  </header>

  <!-- Main Content Container -->
  <main class="flex-1 max-w-7xl w-full mx-auto px-4 py-6">

    <!-- ==================== VIEW 1: INTERACTIVE DECISION GAME ==================== -->
    <section id="view-game" class="space-y-6">

      <!-- Top Mission Banner & Group Profile Bar -->
      <div class="glass-panel rounded-2xl p-4 sm:p-5 border border-sky-500/30 shadow-xl">
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-4 items-center">
          <div class="lg:col-span-7 space-y-1.5">
            <div class="flex items-center gap-2 text-sky-400 text-xs font-bold uppercase tracking-wider">
              <i data-lucide="siren" class="w-4 h-4 text-rose-400 animate-pulse"></i>
              <span>企業緊急委託任務：3 個月內完成全球 18 國人才培訓轉型</span>
            </div>
            <p class="text-xs sm:text-sm text-slate-300 leading-relaxed">
              環航智造科技（AeroTech Global）過去把「2 小時上課簡報錄影直接放上網（課本 p.277 <strong>再利用 Repurposing</strong>）」，導致全球完課率跌至 18% 且現場失誤頻傳！請你們這組（4–5 人顧問團）認領一個危機職群，透過<strong>四關科技化訓練決策＋隨機突發事件卡</strong>，打造高成效解決方案並上台提案！
            </p>
          </div>
          <div class="lg:col-span-5 flex flex-wrap sm:flex-nowrap items-center gap-3 justify-end">
            <div class="w-full sm:w-44">
              <label class="block text-xs text-slate-400 mb-1">顧問小組名稱（4–5人一組）</label>
              <input id="group-name-input" type="text" value="第一組：比奇堡顧問團" oninput="updateGroupName(this.value)" class="w-full bg-slate-900/90 border border-slate-700 rounded-lg px-3 py-1.5 text-sm text-white focus:outline-none focus:border-sky-400">
            </div>
            <div class="w-full sm:w-56">
              <label class="block text-xs text-slate-400 mb-1">切換負責的個案危機職群</label>
              <select id="mission-select" onchange="selectMission(this.value)" class="w-full bg-slate-900/90 border border-sky-500/50 rounded-lg px-3 py-1.5 text-sm text-sky-300 font-semibold focus:outline-none focus:border-sky-400">
                <option value="eng">危機一：全球設備維修工程師 (600人)</option>
                <option value="pm">危機二：跨國區域專案經理 (80人)</option>
                <option value="sales">危機三：第一線業務與客服代表 (1,200人)</option>
              </select>
            </div>
          </div>
        </div>
      </div>

      <!-- Main Game Grid: Left Mission & Stages (8 cols) | Right Live HUD & Radar (4 cols) -->
      <div class="grid grid-cols-1 lg:grid-cols-12 gap-6 items-start">

        <!-- Left Column: Active Mission Brief & 4-Stage Interactive Builder -->
        <div class="lg:col-span-8 space-y-5">

          <!-- Mission Briefing Card -->
          <div id="mission-brief-card" class="glass-panel rounded-2xl p-5 border-l-4 border-l-amber-500">
            <!-- Populated dynamically by JS -->
          </div>

          <!-- Stage Stepper Progress Bar -->
          <div class="grid grid-cols-4 gap-2">
            <button onclick="goToStage(1)" id="step-btn-1" class="p-2.5 rounded-xl border text-left transition flex items-center gap-2 bg-sky-500/20 border-sky-400 text-white">
              <span class="w-6 h-6 rounded-full bg-sky-500 text-slate-950 font-bold text-xs flex items-center justify-center shrink-0">1</span>
              <div class="truncate">
                <div class="text-xs text-sky-300 font-semibold">STAGE 1</div>
                <div class="text-xs font-bold truncate">需求與成果診斷</div>
              </div>
            </button>
            <button onclick="goToStage(2)" id="step-btn-2" class="p-2.5 rounded-xl border text-left transition flex items-center gap-2 bg-slate-800/70 border-slate-700 text-slate-300 hover:border-slate-500">
              <span class="w-6 h-6 rounded-full bg-slate-700 text-slate-200 font-bold text-xs flex items-center justify-center shrink-0">2</span>
              <div class="truncate">
                <div class="text-xs text-slate-400 font-semibold">STAGE 2</div>
                <div class="text-xs font-bold truncate">科技與支援組合</div>
              </div>
            </button>
            <button onclick="goToStage(3)" id="step-btn-3" class="p-2.5 rounded-xl border text-left transition flex items-center gap-2 bg-slate-800/70 border-slate-700 text-slate-300 hover:border-slate-500">
              <span class="w-6 h-6 rounded-full bg-slate-700 text-slate-200 font-bold text-xs flex items-center justify-center shrink-0">3</span>
              <div class="truncate">
                <div class="text-xs text-slate-400 font-semibold">STAGE 3</div>
                <div class="text-xs font-bold truncate">學習環境與掌控權</div>
              </div>
            </button>
            <button onclick="goToStage(4)" id="step-btn-4" class="p-2.5 rounded-xl border text-left transition flex items-center gap-2 bg-slate-800/70 border-slate-700 text-slate-300 hover:border-slate-500">
              <span class="w-6 h-6 rounded-full bg-slate-700 text-slate-200 font-bold text-xs flex items-center justify-center shrink-0">4</span>
              <div class="truncate">
                <div class="text-xs text-slate-400 font-semibold">STAGE 4</div>
                <div class="text-xs font-bold truncate">突發危機與LMS</div>
              </div>
            </button>
          </div>

          <!-- Active Stage Interactive Workspace -->
          <div id="stage-workspace" class="glass-panel rounded-2xl p-5 sm:p-6 space-y-5">
            <!-- Dynamically rendered by renderCurrentStage() -->
          </div>

          <!-- Stage Navigation Footer -->
          <div class="flex items-center justify-between">
            <button id="prev-stage-btn" onclick="prevStage()" class="px-4 py-2 rounded-xl bg-slate-800 border border-slate-700 text-slate-300 hover:text-white text-sm font-semibold flex items-center gap-1.5">
              <i data-lucide="arrow-left" class="w-4 h-4"></i>
              <span>上一關</span>
            </button>
            <div class="flex items-center gap-3">
              <button id="demo-btn" onclick="loadOptimalDemo()" class="px-3.5 py-2 rounded-xl bg-amber-500/15 border border-amber-500/40 text-amber-300 hover:bg-amber-500/25 text-xs sm:text-sm font-semibold flex items-center gap-1.5" title="教師講評示範用：一鍵載入課本理論最佳解">
                <i data-lucide="sparkles" class="w-4 h-4"></i>
                <span>載入課本最佳實務示範</span>
              </button>
              <button id="next-stage-btn" onclick="nextStage()" class="px-5 py-2.5 rounded-xl bg-gradient-to-r from-sky-500 to-indigo-600 hover:from-sky-400 hover:to-indigo-500 text-white text-sm font-bold shadow-lg shadow-sky-500/25 flex items-center gap-1.5">
                <span>下一關</span>
                <i data-lucide="arrow-right" class="w-4 h-4"></i>
              </button>
            </div>
          </div>

        </div>

        <!-- Right Column: Real-Time KPI Dashboard & Advisor Feedback (4 cols) -->
        <div class="lg:col-span-4 space-y-5 lg:sticky lg:top-20">

          <!-- Total Score & Budget Card -->
          <div class="glass-panel rounded-2xl p-5 space-y-4">
            <div class="flex items-center justify-between border-b border-slate-700/80 pb-3">
              <div>
                <span class="text-xs font-bold uppercase tracking-wider text-sky-400">REAL-TIME SIMULATION</span>
                <h3 class="text-base font-bold text-white">科技化訓練成效模擬儀表板</h3>
              </div>
              <div class="text-right">
                <div class="text-xs text-slate-400">綜合決策評級</div>
                <div id="hud-total-score" class="text-2xl font-black text-emerald-400">0 <span class="text-xs font-normal text-slate-400">/ 100</span></div>
              </div>
            </div>

            <!-- Budget Bar -->
            <div class="bg-slate-900/80 rounded-xl p-3 border border-slate-800 space-y-1.5">
              <div class="flex justify-between text-xs">
                <span class="text-slate-400">開發與行政資源點數（上限 100 點）</span>
                <span id="hud-budget-text" class="font-mono font-bold text-sky-300">0 / 100 點</span>
              </div>
              <div class="w-full h-2.5 bg-slate-800 rounded-full overflow-hidden">
                <div id="hud-budget-bar" class="h-full bg-sky-500 transition-all duration-300" style="width: 0%"></div>
              </div>
              <div id="hud-budget-warning" class="text-xs text-slate-400">請選擇高投資報酬率（ROI）的科技組合。</div>
            </div>

            <!-- 5 KPI Bars -->
            <div class="space-y-3">
              <div>
                <div class="flex justify-between text-xs mb-1">
                  <span class="text-slate-300 font-medium">1. 表7.12 學習成果適配度</span>
                  <span id="kpi-fit-val" class="font-mono font-bold text-sky-400">0%</span>
                </div>
                <div class="w-full h-2 bg-slate-800 rounded-full overflow-hidden">
                  <div id="kpi-fit-bar" class="h-full bg-sky-400 transition-all duration-300" style="width: 0%"></div>
                </div>
              </div>

              <div>
                <div class="flex justify-between text-xs mb-1">
                  <span class="text-slate-300 font-medium">2. 正面學習環境（練習/回饋/互動）</span>
                  <span id="kpi-env-val" class="font-mono font-bold text-indigo-400">0%</span>
                </div>
                <div class="w-full h-2 bg-slate-800 rounded-full overflow-hidden">
                  <div id="kpi-env-bar" class="h-full bg-indigo-400 transition-all duration-300" style="width: 0%"></div>
                </div>
              </div>

              <div>
                <div class="flex justify-between text-xs mb-1">
                  <span class="text-slate-300 font-medium">3. 訓練轉移與現場支援（EPSS/社群）</span>
                  <span id="kpi-transfer-val" class="font-mono font-bold text-emerald-400">0%</span>
                </div>
                <div class="w-full h-2 bg-slate-800 rounded-full overflow-hidden">
                  <div id="kpi-transfer-bar" class="h-full bg-emerald-400 transition-all duration-300" style="width: 0%"></div>
                </div>
              </div>

              <div>
                <div class="flex justify-between text-xs mb-1">
                  <span class="text-slate-300 font-medium">4. 成本效益與危機防禦力</span>
                  <span id="kpi-roi-val" class="font-mono font-bold text-amber-400">0%</span>
                </div>
                <div class="w-full h-2 bg-slate-800 rounded-full overflow-hidden">
                  <div id="kpi-roi-bar" class="h-full bg-amber-400 transition-all duration-300" style="width: 0%"></div>
                </div>
              </div>
            </div>

            <!-- Live Diagnostic Alerts from Textbook Chapter 7 -->
            <div class="border-t border-slate-800 pt-3">
              <div class="text-xs font-bold text-slate-300 mb-2 flex items-center gap-1.5">
                <i data-lucide="book-open-check" class="w-4 h-4 text-amber-400"></i>
                <span>第7章理論即時診斷回饋：</span>
              </div>
              <ul id="hud-feedback-list" class="space-y-1.5 text-xs text-slate-300 max-h-52 overflow-y-auto custom-scrollbar pr-1">
                <!-- Populated dynamically -->
              </ul>
            </div>

            <button onclick="switchMainView('pitch')" class="w-full py-2.5 rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-xs sm:text-sm shadow-lg shadow-emerald-600/25 transition flex items-center justify-center gap-2">
              <i data-lucide="presentation" class="w-4 h-4"></i>
              <span>一鍵生成小組上台發表簡報看板</span>
            </button>
          </div>

        </div>

      </div>
    </section>

    <!-- ==================== VIEW 2: GROUP PITCH PRESENTATION BOARD ==================== -->
    <section id="view-pitch" class="hidden space-y-6">
      <div class="glass-panel rounded-2xl p-6 border border-emerald-500/40 shadow-2xl space-y-6">
        <div class="flex flex-wrap items-center justify-between gap-4 border-b border-slate-700 pb-4">
          <div>
            <div class="flex items-center gap-2">
              <span class="px-2.5 py-0.5 rounded-full text-xs font-bold bg-emerald-500/20 text-emerald-300 border border-emerald-500/30">課堂第三階段：2.5 分鐘小組提案發表看板</span>
              <span id="pitch-mission-tag" class="text-xs text-sky-400 font-semibold"></span>
            </div>
            <h2 id="pitch-title" class="text-xl sm:text-2xl font-black text-white mt-1"></h2>
          </div>
          <div class="flex items-center gap-3">
            <div class="bg-slate-900 border border-slate-700 rounded-xl px-4 py-2 text-center">
              <div class="text-xs text-slate-400">系統模擬成效總分</div>
              <div id="pitch-score-badge" class="text-2xl font-black text-emerald-400"></div>
            </div>
            <button onclick="copyPitchText()" class="px-4 py-2.5 rounded-xl bg-sky-500 hover:bg-sky-400 text-white font-bold text-xs sm:text-sm flex items-center gap-1.5 shadow">
              <i data-lucide="copy" class="w-4 h-4"></i>
              <span>複製提案摘要與講稿</span>
            </button>
          </div>
        </div>

        <!-- 4-Grid Executive Pitch Canvas -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-5" id="pitch-cards-container">
          <!-- Populated dynamically by renderPitchView() -->
        </div>

        <!-- Auto-Generated 2.5-Minute Oral Pitch Script & Peer Critique Questions -->
        <div class="grid grid-cols-1 lg:grid-cols-12 gap-5">
          <div class="lg:col-span-7 bg-slate-900/90 border border-slate-700 rounded-2xl p-5 space-y-3">
            <div class="flex items-center justify-between">
              <h3 class="text-sm font-bold text-amber-400 flex items-center gap-2">
                <i data-lucide="mic" class="w-4 h-4"></i>
                <span>自動生成 2.5 分鐘小組上台發表講稿（可直接照唸或微調）</span>
              </h3>
              <span class="text-xs text-slate-400">約 450–500 字</span>
            </div>
            <div id="pitch-script-box" class="text-xs sm:text-sm text-slate-200 leading-relaxed space-y-2 whitespace-pre-line bg-slate-950/70 p-4 rounded-xl border border-slate-800"></div>
          </div>

          <div class="lg:col-span-5 bg-slate-900/90 border border-rose-500/30 rounded-2xl p-5 space-y-3">
            <h3 class="text-sm font-bold text-rose-400 flex items-center gap-2">
              <i data-lucide="shield-question" class="w-4 h-4"></i>
              <span>同儕詰問組（Peer Critique）與教師追問防禦題庫</span>
            </h3>
            <p class="text-xs text-slate-400">根據你們目前選擇的科技組合，台下評論組可能會針對以下課本理論盲點發動詰問，請預先準備：</p>
            <ul id="pitch-defense-list" class="space-y-2.5 text-xs text-slate-200"></ul>
          </div>
        </div>
      </div>
    </section>

    <!-- ==================== VIEW 3: TABLE 7.12 & CHAPTER 7 CHEAT SHEET ==================== -->
    <section id="view-matrix" class="hidden space-y-6">
      <div class="glass-panel rounded-2xl p-6 space-y-4">
        <div class="flex flex-wrap items-center justify-between gap-2 border-b border-slate-700 pb-3">
          <div>
            <span class="text-xs font-bold text-sky-400 uppercase">TEXTBOOK REFERENCE (p.301–302)</span>
            <h2 class="text-lg sm:text-xl font-bold text-white">課本表 7.12〈新科技訓練方法之比較〉互動查詢矩陣</h2>
          </div>
          <p class="text-xs text-slate-400">點擊任一訓練方法可高亮檢視其學習成果、學習環境、訓練轉移與成本特性</p>
        </div>

        <div class="overflow-x-auto custom-scrollbar">
          <table class="w-full text-xs text-left border-collapse">
            <thead>
              <tr class="bg-slate-800/90 text-slate-200 border-b border-slate-700">
                <th class="p-3 font-bold">評估維度 ＼ 科技方法</th>
                <th class="p-3 font-bold text-sky-300">線上數位學習 / 網路學習</th>
                <th class="p-3 font-bold">CBT (無網路光碟)</th>
                <th class="p-3 font-bold text-indigo-300">遠距教學 (虛擬教室/直播)</th>
                <th class="p-3 font-bold text-emerald-300">適性訓練 (ITS)</th>
                <th class="p-3 font-bold text-amber-300">模擬和嚴肅遊戲 (VR)</th>
                <th class="p-3 font-bold text-pink-300">行動學習 (App/Podcast)</th>
                <th class="p-3 font-bold text-purple-300">社群媒體 (Wiki/部落格)</th>
                <th class="p-3 font-bold">MOOC (磨課師)</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-slate-800 text-slate-300">
              <tr class="bg-slate-900/50"><td colspan="9" class="px-3 py-1.5 font-bold text-sky-400">【學習成果適配度】</td></tr>
              <tr><td class="p-2.5 font-medium">語文訊息（陳述知識）</td><td class="p-2.5 text-emerald-400 font-bold">是</td><td class="p-2.5">是</td><td class="p-2.5">是</td><td class="p-2.5">是</td><td class="p-2.5">是</td><td class="p-2.5 text-emerald-400 font-bold">是</td><td class="p-2.5">是</td><td class="p-2.5">是</td></tr>
              <tr><td class="p-2.5 font-medium">心智技能（程序概念）</td><td class="p-2.5 text-emerald-400 font-bold">是</td><td class="p-2.5">是</td><td class="p-2.5">是</td><td class="p-2.5 text-emerald-400 font-bold">是</td><td class="p-2.5 text-emerald-400 font-bold">是</td><td class="p-2.5">是</td><td class="p-2.5 text-rose-400">否</td><td class="p-2.5">是</td></tr>
              <tr><td class="p-2.5 font-medium">認知策略（問題解決）</td><td class="p-2.5">是</td><td class="p-2.5">是</td><td class="p-2.5 text-emerald-400 font-bold">是</td><td class="p-2.5 text-emerald-400 font-bold">是</td><td class="p-2.5 text-emerald-400 font-bold">是</td><td class="p-2.5 text-rose-400">否</td><td class="p-2.5">是</td><td class="p-2.5">是</td></tr>
              <tr><td class="p-2.5 font-medium">態度（價值觀與軟實力）</td><td class="p-2.5 text-amber-300">也許</td><td class="p-2.5 text-rose-400">否</td><td class="p-2.5 text-rose-400">否 (需搭配互動)</td><td class="p-2.5 text-rose-400">否</td><td class="p-2.5 text-emerald-400 font-bold">是</td><td class="p-2.5 text-rose-400">否</td><td class="p-2.5 text-rose-400">否</td><td class="p-2.5 text-rose-400">否</td></tr>
              <tr><td class="p-2.5 font-medium">動作技能（實體操作）</td><td class="p-2.5 text-rose-400">否</td><td class="p-2.5 text-rose-400">否</td><td class="p-2.5 text-rose-400">否</td><td class="p-2.5 text-emerald-400 font-bold">是</td><td class="p-2.5 text-emerald-400 font-bold">是</td><td class="p-2.5 text-rose-400">否</td><td class="p-2.5 text-rose-400">否</td><td class="p-2.5 text-rose-400">否</td></tr>
              <tr class="bg-slate-900/50"><td colspan="9" class="px-3 py-1.5 font-bold text-sky-400">【學習環境、訓練轉移與成本】</td></tr>
              <tr><td class="p-2.5 font-medium">目標</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5">中</td><td class="p-2.5 text-emerald-400 font-bold">高</td></tr>
              <tr><td class="p-2.5 font-medium">意義</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5">中</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5">中</td><td class="p-2.5">中</td><td class="p-2.5">中</td></tr>
              <tr><td class="p-2.5 font-medium">練習機會 / 回饋</td><td class="p-2.5">高 / 高</td><td class="p-2.5">高 / 高</td><td class="p-2.5 text-amber-300">低 / 低</td><td class="p-2.5 text-emerald-400 font-bold">高 / 高</td><td class="p-2.5 text-emerald-400 font-bold">高 / 高</td><td class="p-2.5 text-amber-300">低 / 低</td><td class="p-2.5">中 / 高</td><td class="p-2.5">中 / 中</td></tr>
              <tr><td class="p-2.5 font-medium">互動：學習者與內容</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5">中</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5">中</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5 text-emerald-400 font-bold">高</td></tr>
              <tr><td class="p-2.5 font-medium">互動：學習者與講師</td><td class="p-2.5">中</td><td class="p-2.5 text-rose-400">低</td><td class="p-2.5">中</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5">中</td><td class="p-2.5 text-rose-400">低</td><td class="p-2.5">中</td><td class="p-2.5">中</td></tr>
              <tr><td class="p-2.5 font-medium">互動：學習者與其他學員</td><td class="p-2.5">中</td><td class="p-2.5 text-rose-400">低</td><td class="p-2.5">中</td><td class="p-2.5 text-rose-400">低</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5 text-rose-400">低</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5">中</td></tr>
              <tr><td class="p-2.5 font-medium">訓練轉移程度</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5">中</td><td class="p-2.5">中</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5">中</td><td class="p-2.5">中</td><td class="p-2.5">中</td></tr>
              <tr><td class="p-2.5 font-medium">發展成本 / 行政成本</td><td class="p-2.5">高 / 低</td><td class="p-2.5">高 / 低</td><td class="p-2.5">中 / 低</td><td class="p-2.5">高 / 低</td><td class="p-2.5 text-rose-400">高 / 低</td><td class="p-2.5">中 / 低</td><td class="p-2.5">中 / 中</td><td class="p-2.5">高 / 低</td></tr>
              <tr><td class="p-2.5 font-medium">成效</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5">中</td><td class="p-2.5">中</td><td class="p-2.5">?</td><td class="p-2.5 text-emerald-400 font-bold">高</td><td class="p-2.5">?</td><td class="p-2.5">?</td><td class="p-2.5">?</td></tr>
            </tbody>
          </table>
        </div>
      </div>
    </section>

    <!-- ==================== VIEW 4: 50-MINUTE LESSON FLOW GUIDE ==================== -->
    <section id="view-lesson" class="hidden space-y-6">
      <div class="glass-panel rounded-2xl p-6 space-y-5">
        <div class="border-b border-slate-700 pb-3 flex flex-wrap items-center justify-between gap-2">
          <div>
            <span class="text-xs font-bold text-amber-400 uppercase">INSTRUCTOR FACILITATION GUIDE</span>
            <h2 class="text-lg sm:text-xl font-bold text-white">如何將此互動遊戲融入 50 分鐘研究所課堂（四階段運行腳本）</h2>
          </div>
          <span class="text-xs px-3 py-1 rounded-full bg-sky-500/20 text-sky-300 border border-sky-500/30">對應課本 p.286–290「嚴肅遊戲與遊戲化學習」</span>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
          <div class="bg-slate-900/90 border border-slate-700 rounded-xl p-4 space-y-2">
            <div class="flex items-center justify-between">
              <span class="text-xs font-bold px-2 py-0.5 rounded bg-sky-500/20 text-sky-300">00:00 – 08:00 (8分鐘)</span>
              <button onclick="setTimerMinutes(8, '階段一：情境導入')" class="text-xs text-sky-400 hover:underline">啟動 8 分鐘計時</button>
            </div>
            <h3 class="text-sm font-bold text-white">階段一：破冰與危機任務認領</h3>
            <p class="text-xs text-slate-300 leading-relaxed">
              教師投影本戰情室，點出《環航智造》把實體課簡報直接搬上網（Repurposing，p.277）導致 18% 完課率的慘況。將全班以 4–5 人分組，每組指派一個危機職群（維修工程師／跨國專案經理／第一線業務）。
            </p>
          </div>

          <div class="bg-slate-900/90 border border-slate-700 rounded-xl p-4 space-y-2">
            <div class="flex items-center justify-between">
              <span class="text-xs font-bold px-2 py-0.5 rounded bg-amber-500/20 text-amber-300">08:00 – 26:00 (18分鐘)</span>
              <button onclick="setTimerMinutes(18, '階段二：戰情闖關')" class="text-xs text-amber-400 hover:underline">啟動 18 分鐘計時</button>
            </div>
            <h3 class="text-sm font-bold text-white">階段二：四關決策闖關與突發事件</h3>
            <p class="text-xs text-slate-300 leading-relaxed">
              各組操作「1. 互動決策闖關」，依序完成<strong>學習成果診斷 → 100點預算科技配置 → 學習者掌控權設定 → 隨機抽取突發危機卡</strong>。系統即時依據表 7.12 計算分數並給予理論警告，逼使學生放棄單一方法、走向混合式與 EPSS 支援。
            </p>
          </div>

          <div class="bg-slate-900/90 border border-slate-700 rounded-xl p-4 space-y-2">
            <div class="flex items-center justify-between">
              <span class="text-xs font-bold px-2 py-0.5 rounded bg-emerald-500/20 text-emerald-300">26:00 – 44:00 (18分鐘)</span>
              <button onclick="setTimerMinutes(2.5, '階段三：小組提案')" class="text-xs text-emerald-400 hover:underline">啟動 2.5 分鐘計時</button>
            </div>
            <h3 class="text-sm font-bold text-white">階段三：戰情看板發表與同儕詰問</h3>
            <p class="text-xs text-slate-300 leading-relaxed">
              各組切換至「2. 小組發表簡報看板」，直接投影系統生成的四宮格決策畫布與成效雷達，進行 2.5 分鐘顧問簡報；台下對照組運用系統右側生成的「同儕詰問防禦題庫」進行 1.5 分鐘犀利提問。
            </p>
          </div>

          <div class="bg-slate-900/90 border border-slate-700 rounded-xl p-4 space-y-2">
            <div class="flex items-center justify-between">
              <span class="text-xs font-bold px-2 py-0.5 rounded bg-purple-500/20 text-purple-300">44:00 – 50:00 (6分鐘)</span>
              <button onclick="setTimerMinutes(6, '階段四：理論總結')" class="text-xs text-purple-400 hover:underline">啟動 6 分鐘計時</button>
            </div>
            <h3 class="text-sm font-bold text-white">階段四：彙整說明（Debriefing）</h3>
            <p class="text-xs text-slate-300 leading-relaxed">
              呼應課本 p.289「遊戲後向學習者彙整說明能幫助連結模擬經驗與實際工作」，教師點擊「載入課本最佳實務示範」，對比三組職群差異，總結「正面學習環境＋專屬時間空間＋訓練支援科技」三大成功關鍵，並請學員於最後 2 分鐘（或課後）完成「5. 學習目標檢核」6 題。
            </p>
          </div>
        </div>
      </div>
    </section>

    <section id="view-quiz" class="hidden space-y-6">
      <div class="glass-panel rounded-2xl p-6 space-y-4">
        <div class="border-b border-slate-700 pb-3">
          <span class="text-xs font-bold text-emerald-400 uppercase">LEARNING OBJECTIVES CHECK</span>
          <h2 class="text-lg sm:text-xl font-bold text-white">第7章 9 項學習目標涵蓋度與課後檢核</h2>
        </div>
        <ul id="obj-list" class="space-y-2 text-xs"></ul>
        <div id="quiz-box" class="space-y-3"></div>
        <div class="flex items-center justify-between gap-2">
          <span id="quiz-summary" class="text-sm font-bold text-sky-300"></span>
          <button onclick="resetQuiz()" class="text-xs px-3 py-1.5 rounded-lg bg-slate-700 text-slate-200 hover:bg-slate-600">重做</button>
        </div>
      </div>
    </section>
  </main>

  <!-- Classroom QR Code Projection Modal -->
  <div id="qr-modal" class="fixed inset-0 z-50 hidden bg-slate-950/85 backdrop-blur-md flex items-center justify-center p-4">
    <div class="bg-slate-900 border border-sky-500/50 rounded-3xl max-w-lg w-full p-6 sm:p-8 shadow-2xl space-y-5 text-center relative">
      <button onclick="closeQrModal()" class="absolute top-4 right-4 p-2 rounded-xl bg-slate-800 text-slate-400 hover:text-white border border-slate-700" title="關閉視窗">
        <i data-lucide="x" class="w-5 h-5"></i>
      </button>
      <div class="space-y-1">
        <span class="px-3 py-1 rounded-full text-xs font-bold bg-emerald-500/20 text-emerald-300 border border-emerald-500/30">GitHub Pages 課堂連線</span>
        <h3 class="text-xl sm:text-2xl font-black text-white pt-1">請掃描 QR Code 進入決策戰情室</h3>
        <p class="text-xs sm:text-sm text-slate-400">4–5 人一組，可使用手機、平板或筆電開啟同步操作</p>
      </div>

      <!-- QR Code Display Box -->
      <div class="bg-white p-5 rounded-2xl inline-flex flex-col items-center justify-center shadow-inner mx-auto">
        <img id="qr-image" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7" alt="課堂連線 QR Code" class="w-60 h-60 sm:w-64 sm:h-64 object-contain">
      </div>

      <!-- Editable URL Input (auto-detects GitHub Pages URL) -->
      <div class="text-left space-y-1.5">
        <label class="block text-xs font-bold text-sky-400">遊戲網址（部署至 GitHub Pages 後會自動抓取，亦可手動貼上網址）：</label>
        <div class="flex gap-2">
          <input id="qr-url-input" type="text" oninput="updateQrImage(this.value)" placeholder="https://您的帳號.github.io/專案名稱/" class="flex-1 bg-slate-950 border border-slate-700 rounded-xl px-3.5 py-2 text-xs sm:text-sm text-white focus:outline-none focus:border-sky-400 font-mono">
          <button onclick="copyGameUrl()" class="px-3.5 py-2 rounded-xl bg-sky-500 hover:bg-sky-400 text-white text-xs sm:text-sm font-bold shrink-0">複製網址</button>
        </div>
      </div>
    </div>
  </div>

  <!-- Toast Notification -->
  <div id="toast-box" class="fixed bottom-5 right-5 z-50 hidden bg-slate-900 border border-sky-500/60 text-white px-4 py-3 rounded-xl shadow-2xl text-xs sm:text-sm flex items-center gap-2">
    <i data-lucide="check-circle-2" class="w-4 h-4 text-emerald-400"></i>
    <span id="toast-msg"></span>
  </div>

  <script>
    // ==================== CHAPTER 7 GROUNDED GAME DATASET ====================
    const MISSIONS = {
      eng: {
        id: 'eng',
        name: '危機一：全球設備維修工程師（600人）',
        badge: '高風險動作技能 ＋ 複雜排障程序',
        persona: '分佈於全球 18 國製造廠區與客戶據點（共 600 名新進與中階維修工程師），負責新一代高壓氣體模組與 AI 精密機械手臂之現場安裝、定期保養、安全拆裝與緊急故障排除。',
        painPoint: '過去人資部門僅將總部講師 90 分鐘的課堂操作錄影與 300 頁 PDF 手冊直接放上網路平台（課本 p.277 所稱之「再利用 Repurposing」），不僅完課率僅 18%，學員在客戶現場實作失誤率更高達 35%（錯誤操作會引發高壓氣體外洩與嚴重工安傷害），且各國資深技師離職率高，隱性排障經驗嚴重流失。',
        statusDetails: [
          '【組織與地理現況】600 名工程師分散於 18 國，若集中至總部實體訓練中心受訓，機票食宿差旅成本極高且會導致各地產線停擺（p.302 考量條件 2）。',
          '【教材與系統現況】現行線上教材為單向 90 分鐘未切割長片，缺乏動手練習、即時回饋與安全模擬環境；廠區現場亦無即時排障輔助系統。',
          '【任務與風險特性】高壓氣體與機械手臂拆裝屬於「高風險動作技能」與「漫長、困難且資訊密集的排障程序」，一旦操作錯誤會造成嚴重工安傷害與巨額停機賠償（符合課本 p.296 表 7.10 急需訓練支援科技與 p.288 模擬器防範事故之情境）。',
          '【關鍵績效缺口】線上完課率僅 18%（目標 ≥90%）、現場實作失誤率高達 35%（目標 <5%）、資深技師排障經驗留存率不足 20%。'
        ],
        targetOutcomes: ['motor', 'intellectual', 'cognitive'],
        recommendedCore: ['vr_sim', 'flipped'],
        recommendedSupport: ['expert_sys'],
        optimalEnv: {
          structure: 'modular',
          control: 'guided_practice',
          timeSpace: 'learning_lab',
          lmsFeature: 'competency_gap'
        },
        events: [
          {
            id: 'ev_sickness',
            title: '突發狀況 A：學員出現「模擬病（Simulator Sickness）」與新奇感分心！',
            desc: '課本 p.287 & p.289 警告：部分工程師戴上頭盔後出現頭暈嘔吐（模擬病），且許多年輕工程師只顧著在 3D 虛擬世界裡逛街玩耍，忽略了高壓管路安全程序！你們該如何修正方案？',
            options: [
              {
                id: 'opt1',
                text: '提升體感擬真度並延長單次 VR 練習至 3 小時，讓學員習慣眩暈感。',
                impact: { env: -15, transfer: -10, roi: -10 },
                feedback: '錯誤！延長時間會加劇知覺扭曲與模擬病（p.287），且缺乏事後收斂。'
              },
              {
                id: 'opt2',
                text: '改善感官刺激同步率、改為 15–20 分鐘短模組，並在模擬結束後強制執行「講師彙整說明（Debriefing，p.289）」與實體檢核表對照。',
                impact: { env: +18, transfer: +20, roi: +12 },
                feedback: '精準命中課本 p.289 核心原則！遊戲與模擬後必須透過彙整說明（Debriefing）連結虛擬經驗與實際工作，避免新奇感削弱記憶。'
              },
              {
                id: 'opt3',
                text: '全面取消模擬器，改回寄送 300 頁 PDF 維修手冊讓工程師自讀。',
                impact: { fit: -25, env: -20, transfer: -20 },
                feedback: '退回傳統文字再利用（p.277），完全無法訓練動作技能與高風險程序（表7.12）。'
              }
            ]
          },
          {
            id: 'ev_cost',
            title: '突發狀況 B：財務長質疑客製化 VR 模擬開發費高達 25 萬美元（p.289）！',
            desc: '課本 p.289 指出客製化模擬成本介於 20–30 萬美元。財務長要求你們提出具體的成本效益與訓練轉移配套，否則砍半預算！',
            options: [
              {
                id: 'opt1',
                text: '結合「現場排障專家系統（p.296）＋內部 Wiki 共編（仿 Intelpedia，p.283）」，將高成本 VR 僅鎖定於高危核心動作，常規排障交由專家系統支援，並以零停機賠償對比模擬器效益（p.288）。',
                impact: { fit: +12, transfer: +18, roi: +22 },
                feedback: '大師級顧問思維！結合表7.10訓練支援科技（專家系統）與 p.288 直升機模擬器 ROI 論證，完美說服財務長。'
              },
              {
                id: 'opt2',
                text: '改用免費公開的 MOOC（大規模開放式線上課程）教導公司機密機台維修。',
                impact: { fit: -20, transfer: -15, roi: -5 },
                feedback: 'MOOC 完課率僅 10–20%（p.281）且無法訓練動作技能（表7.12），更會洩露企業機密。'
              }
            ]
          }
        ]
      },
      pm: {
        id: 'pm',
        name: '危機二：跨國區域專案經理（80人）',
        badge: '心智技能 ＋ 認知策略 ＋ 跨部門溝通態度',
        persona: '分散於亞洲、歐洲、美洲 18 國分公司的 80 位高潛力區域專案經理，負責帶領跨國跨部門團隊（研發、製造、業務）推動新一代 AI 機台上市專案，需具備「跨部門需求轉譯、衝突解決、優先順序管理與領導決策」等軟實力。',
        painPoint: '若將 80 人集中至總部進行 3 天面對面授課，機票食宿差旅費高達 35 萬美元，且各國專案經理無法長時間離開工作崗位（如同課本 p.260 日產汽車案例）；但改寄發單機自學光碟（CBT）後，學員普遍反映「單向孤單、缺乏跨國同儕人脈建立、無法針對真實部門衝突進行角色扮演與即時回饋」，訓後行為毫無改變。',
        statusDetails: [
          '【組織與時空現況】80 位專案經理橫跨亞、歐、美多個時區，工作日程緊湊，無法離開崗位參加長天數實體集中訓練（p.260 日產汽車、p.288 PPD 案例）。',
          '【教材與互動現況】現行 CBT 自學光碟僅有單向文字與選擇題，缺乏同儕討論、角色扮演與講師即時指導，且曾嘗試將 80 人塞入同一場視訊會議，導致全員被動靜音、無人互動（p.295 遠距教學缺點）。',
          '【任務與職能特性】跨部門需求轉譯、衝突解決與資源配置屬於「認知策略、心智技能與領導態度/軟實力（Soft Skills）」（p.268 拜耳製藥、p.273 DNC 與 p.288 NetApp 案例），必須透過小組合作、個案討論與決策模擬才能有效內化。',
          '【關鍵績效缺口】跨部門需求轉譯滿意度僅 2.9 分（目標 4.0 分）、跨國專案延誤率達 40%，訓後一個月回到工作崗位幾乎未應用所學（訓練轉移低落）。'
        ],
        targetOutcomes: ['cognitive', 'attitude', 'intellectual'],
        recommendedCore: ['virtual_class', 'serious_game'],
        recommendedSupport: ['shared_workspace', 'social_community'],
        optimalEnv: {
          structure: 'modular',
          control: 'guided_practice',
          timeSpace: 'scheduled_block',
          lmsFeature: 'talent_integration'
        },
        events: [
          {
            id: 'ev_crowd',
            title: '突發狀況 A：80 人同時擠進同一間視訊會議室，變成講師單向唸簡報！',
            desc: '人資為了省事，把 80 位跨國經理塞進同一場 3 小時視訊會議，結果沒人開麥克風，都在偷回 Email（p.295 遠距教學缺乏互動之缺點）！你們如何重構？',
            options: [
              {
                id: 'opt1',
                text: '仿照日產汽車（p.260）與 p.294 準則，將虛擬教室每班嚴格限制在 20–25 人以內，時間控制在 60–90 分鐘（p.295），課前先做主管/自我評估，課中運用虛擬白板、投票與分組角色扮演。',
                impact: { fit: +15, env: +22, transfer: +15 },
                feedback: '完全符合課本 p.260 日產汽車案例與 p.294–295 虛擬教室黃金準則（限額 20–25 人、60–90 分鐘、雙向投票與角色扮演）！'
              },
              {
                id: 'opt2',
                text: '規定所有人開鏡頭罰坐 3 小時，並在課後考 100 題是非題。',
                impact: { env: -20, transfer: -15, roi: -10 },
                feedback: '違反成人學習與學習者掌控權（p.267），單向講授與死記是非題無法培養軟實力與認知策略（p.301）。'
              }
            ]
          },
          {
            id: 'ev_transfer',
            title: '突發狀況 B：虛擬教室上完很熱絡，但回到各國部門後依然各做各的！',
            desc: '訓後 1 個月調查發現，跨國專案經理並未將衝突解決技巧應用在跨廠區專案中。該如何強化「訓練轉移」？',
            options: [
              {
                id: 'opt1',
                text: '仿照諾華藥廠（Novartis）三階段混合式方案（p.286），要求學員訓後在「共享工作空間與線上社群」發表最佳實務、完成一項跨國執行方案並與直屬主管面談追蹤，滿一個月再以 LMS 進行保留測驗。',
                impact: { env: +12, transfer: +25, roi: +15 },
                feedback: '極佳！完全扣合 p.286 諾華藥廠「數位加速研討會」三階段混合式學習與主管督導轉移機制！'
              },
              {
                id: 'opt2',
                text: '把虛擬教室的錄影檔重寄一次給所有學員看。',
                impact: { env: -10, transfer: -15, roi: -5 },
                feedback: '重看錄影檔屬於低互動被動接收，無法解決工作現場缺乏主管支持與同儕協作的問題（p.301）。'
              }
            ]
          }
        ]
      },
      sales: {
        id: 'sales',
        name: '危機三：第一線業務與客服代表（1,200人）',
        badge: '語文訊息 ＋ 頻繁更新規格 ＋ 法規合規認證',
        persona: '全球 1,200 名第一線業務代表與客服人員（逾 75% 為習慣使用智慧型手機與社群媒體的千禧與 Z 世代），整日在外奔波差旅與拜訪客戶，需隨時掌握每月更新的 AI 機台產品規格、報價規則與各國資安個資法規（必填合規認證）。',
        painPoint: '業務員絕大多數時間都在差旅與客戶現場，根本沒時間坐在辦公室電腦前上 2 小時線上課；部分主管要求業務利用下班或休假完課引發強烈反彈與拖延（課本 p.279）；且在客戶談判現場遇到罕見規格與複雜合規條款時背不起來，找不到主管或產品專家即時支援。',
        statusDetails: [
          '【人員與工作型態現況】1,200 名外勤業務高度分散且整日移動，僅能依賴隨身智慧型手機或平板電腦利用零碎時間存取資訊（p.291–292 CCBCC 與 Farmers 案例），對長篇文字閱讀極度排斥（p.294 FileNet 案例）。',
          '【系統與時間政策現況】現有線上課程為桌機版網頁，手機開啟需不斷翻轉螢幕且須下載額外外掛程式（Plug-in，p.276），常造成系統當機；公司亦未安排工作日專屬訓練時間（p.279）。',
          '【任務與法規合規特性】產品規格與報價條款更新極為頻繁（表 7.10 仰賴頻繁變更資訊的績效表現），且各國資安法規屬於「強制必修合規訓練」（p.272 連鎖藥妝 HIPAA、p.298–300 LMS 法規追蹤），公司須隨時向主管機關證明全員完訓。',
          '【關鍵績效缺口】法規必修課逾期未完訓率達 45%、客戶現場罕見報價錯誤與求助客服電話量暴增，傳統一年兩次集中業務大會差旅成本過高且資訊傳遞滯後。'
        ],
        targetOutcomes: ['verbal', 'intellectual'],
        recommendedCore: ['mobile_learning', 'webcast', 'online_interactive'],
        recommendedSupport: ['epss'],
        optimalEnv: {
          structure: 'micro_10min',
          control: 'self_paced_no_skip',
          timeSpace: 'scheduled_block',
          lmsFeature: 'compliance_tracking'
        },
        events: [
          {
            id: 'ev_plugin',
            title: '突發狀況 A：業務員用手機點開課程卻當機，抱怨圖片太小還要下載外掛！',
            desc: '課本 p.275–276 & p.292 警告：IT 部門把桌機版 90 分鐘 Flash 課程直接丟到手機上，不僅需要額外安裝昂貴外掛程式（Plug-in），下載極慢且字體微小需不斷翻轉螢幕！',
            options: [
              {
                id: 'opt1',
                text: '依據 p.276 & p.292 原則：改用無需外掛的內建 HTML 互動格式、圖片適配手機小螢幕免翻轉，並仿照 Unisys（p.292）將長課濃縮為「10 分鐘以內」的微學習影片與 Podcast 廣播（仿 Capital One）。',
                impact: { fit: +15, env: +22, transfer: +15 },
                feedback: '完美解決技術障礙！課本 p.292 明確指出行動學習長度不應超過 10 分鐘、免翻轉螢幕，且 p.276 強調應避免需額外授權與易當機的外掛程式（Plug-in）。'
              },
              {
                id: 'opt2',
                text: '要求 1,200 位業務員自費購買高階筆電並利用週末休假在飯店下載完課。',
                impact: { env: -25, transfer: -15, roi: -15 },
                feedback: '嚴重違反課本 p.279 原則：「公司期望學員在休息時間或個人休假完成網路訓練是不切實際的！」'
              }
            ]
          },
          {
            id: 'ev_field',
            title: '突發狀況 B：客戶現場詢問罕見跨國資安合規條款，業務員背不起來當場卡住！',
            desc: '新產品與各國法規細節多達上千條，就算上完線上課，業務員在客戶端談判時仍會遺忘罕見案例（表7.10 罕見且資訊密集的任務）。你們該如何設計支援機制？',
            options: [
              {
                id: 'opt1',
                text: '導入「電子績效支援系統（EPSS，p.297）」與裝置論壇（仿 Verizon，p.282）：在業務平板內建 2 分鐘「Learning Bytes（仿 ADP）」與「七大談判檢核清單 App（仿 SNI）」，以即時績效支援取代死背訓練！',
                impact: { fit: +15, transfer: +25, roi: +20 },
                feedback: '神級決策！完全呼應課本 p.296–297 表7.10 與 EPSS 核心精神：針對罕見、資訊密集且頻繁變更的任務，用即時電子績效支援（EPSS）直接支援現場工作！'
              },
              {
                id: 'opt2',
                text: '每個月舉辦一次隨堂默寫筆試，背不出條文就扣獎金。',
                impact: { env: -18, transfer: -20, roi: -10 },
                feedback: '死背無法應付頻繁變更的資訊密集任務（表7.10），反而造成記憶超載（p.272）。'
              }
            ]
          }
        ]
      }
    };

    const LEARNING_OUTCOMES = [
      { id: 'verbal', name: '語文訊息 (陳述性知識)', desc: '記憶產品規格、法規條文、安全守則等事實知識（表7.4, 7.12）' },
      { id: 'intellectual', name: '心智技能 (程序性知識)', desc: '理解操作步驟、分類規則與標準作業程序 SOP（表7.4, 7.12）' },
      { id: 'cognitive', name: '認知策略 (決策與解題)', desc: '主持會議、跨部門需求轉譯、複雜故障診斷與策略思考（p.301–302）' },
      { id: 'attitude', name: '態度 (價值觀與軟實力)', desc: '改變領導行為、跨文化敏感度、團隊合作與客戶服務熱忱（p.273, 301）' },
      { id: 'motor', name: '動作技能 (實體設備操作)', desc: '精密機械手臂拆裝、高壓管路維修、飛行或醫療器材操作（表7.12）' }
    ];

    const CORE_TECH_METHODS = [
      {
        id: 'online_interactive',
        name: '互動式線上數位學習 (E-Learning)',
        cost: 25,
        tag: '認知結果首選',
        desc: '整合互動影片、分支情境與測驗（表7.3, 7.4）。適合陳述與程序知識，但單獨使用較難訓練動作技能。',
        Ref: 'p.268–274 (Allied Bank / Jiffy Lube)'
      },
      {
        id: 'cbt_repurpose',
        name: '傳統光碟/簡報錄影上網 (CBT / 再利用)',
        cost: 10,
        tag: '低成本高風險陷阱',
        desc: '直接把課堂簡報或長片放上網（Repurposing，p.277）。雖便宜但單向無聊、無同儕互動，完課率極低！',
        Ref: 'p.268, p.277 (反面教材)'
      },
      {
        id: 'virtual_class',
        name: '同步虛擬教室 (Virtual Classroom)',
        cost: 30,
        tag: '跨國軟實力與討論',
        desc: '真人講師連線授課，搭配虛擬白板、投票、分組討論與角色扮演（限額 20–25 人、60–90 分鐘最佳）。',
        Ref: 'p.260 (日產汽車), p.293–295'
      },
      {
        id: 'webcast',
        name: '網路直播 / 研討會 (Webcasting)',
        cost: 20,
        tag: '全球同步新知傳遞',
        desc: '即時直播新產品或政策資訊並開放現場 QA，省下巨額業務會議差旅費（如 FileNet 年省 50 萬美元）。',
        Ref: 'p.294–295 (FileNet 案例)'
      },
      {
        id: 'vr_sim',
        name: '3D 虛擬實境與模擬器 (VR & Simulation)',
        cost: 45,
        tag: '高危動作與決策首選',
        desc: '在零風險逼真環境練習高危險設備拆裝或作戰決策（臨場感高、訓練轉移極高，但開發成本高，需防模擬病）。',
        Ref: 'p.286–289 (BP 石油 / 美軍 / PPD)'
      },
      {
        id: 'serious_game',
        name: '嚴肅遊戲與遊戲化 (Serious Game)',
        cost: 35,
        tag: '激勵競爭與策略扮演',
        desc: '結合積分、徽章、排行榜與經營決策模擬（表7.8, 7.9），適合管理決策、資安防禦與業務競賽。',
        Ref: 'p.288–290 (Ford P2P / Allstate / NetApp)'
      },
      {
        id: 'its',
        name: '適性訓練與智慧教學系統 (ITS)',
        cost: 35,
        tag: '客製化動態調適',
        desc: '依據學員測驗表現與錯誤動態調整內容難易度與練習題（如 LearnSmart 與 NASA 太空人機械手臂訓練）。',
        Ref: 'p.292–293 (NASA ITS)'
      },
      {
        id: 'mobile_learning',
        name: '行動學習與微學習 (Mobile / App / Podcast)',
        cost: 25,
        tag: '外勤隨時隨地 10 分鐘',
        desc: '透過智慧手機或 iPad 傳遞 ≤10 分鐘短片與 Podcast（p.291–292），極適合常在差旅途中的外勤業務。',
        Ref: 'p.290–292 (Farmers / CCBCC / Unisys)'
      },
      {
        id: 'flipped',
        name: '混合式學習：翻轉教室 (Flipped Classroom)',
        cost: 30,
        tag: '線上先修＋實體實作',
        desc: '課前線上看完影片並通過及格測驗，將寶貴的實體教室時間全部用來動手實作、教練指導與同儕回饋。',
        Ref: 'p.285–286 (美髮造型師 / 諾華藥廠)'
      },
      {
        id: 'mooc',
        name: '大規模開放式線上課程 (MOOC)',
        cost: 15,
        tag: '廣泛通識但完課率低',
        desc: 'Coursera/edX 等開放課程，成本低且主題廣，但兩週後易淡出、完課率僅 10–20%，不適合需即時高度互動課。',
        Ref: 'p.279–281 (AT&T / Aquent)'
      }
    ];

    const SUPPORT_TECH_METHODS = [
      {
        id: 'epss',
        name: '電子績效支援系統 (EPSS)',
        cost: 20,
        desc: '在工作現場按需提供「2分鐘操作短片（Learning Bytes）」或「策略檢核清單 App」，直接以即時支援取代死背訓練！',
        Ref: 'p.297 (Sephora / ADP / SNI)'
      },
      {
        id: 'expert_sys',
        name: '專家系統 (Expert System)',
        cost: 25,
        desc: '具備知識庫、推論引擎與使用者介面（p.296），協助較不熟練員工診斷複雜設備異常或醫療/金融決策，避免決策疲勞。',
        Ref: 'p.296–297 (約翰霍普金斯醫院)'
      },
      {
        id: 'wiki',
        name: '企業內部維基與裝置論壇 (Wiki / Forum)',
        cost: 15,
        desc: '讓全球資深技師與員工共同建立、編輯與更新故障排除技巧與 FAQ，留存隱性知識並打造分享文化。',
        Ref: 'p.282–283 (Intelpedia / Verizon)'
      },
      {
        id: 'shared_workspace',
        name: '共享工作空間 (Shared Workspace)',
        cost: 10,
        desc: '使用率最高（42%，圖7.1）的學習社群工具（如 Google Docs / SharePoint），供跨國小組共同編輯專案與交換報告。',
        Ref: 'p.262 圖7.1, p.265'
      },
      {
        id: 'social_community',
        name: '內部學習社群與微網誌 (Social Network)',
        cost: 15,
        desc: '在正式訓練前中後連結學員、導師與專家（p.281），透過標籤搜尋專家（如 EAG 併購整合與 Humana 知識交流）。',
        Ref: 'p.281–284 (Humana / Cisco / EAG)'
      }
    ];

    // ==================== APPLICATION STATE ====================
    let state = {
      mainView: 'game',
      groupName: '第一組：比奇堡顧問團',
      missionId: 'eng',
      currentStage: 1,
      muted: false,
      timerSeconds: 18 * 60,
      timerRunning: false,
      timerInterval: null,
      selections: {},
      submitted: {},
      quiz: {}
    };

    // ==================== 優化新增：工具、表7.12矩陣、HUD 鎖定、學習目標檢核 ====================
    function shuffle(a) { a = [...a]; for (let i = a.length - 1; i > 0; i--) { const j = Math.floor(Math.random() * (i + 1)); [a[i], a[j]] = [a[j], a[i]]; } return a; }
    function esc(t) { return String(t).replace(/[&<>"']/g, c => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c])); }
    function setEvent(sel, m, idx) { sel.eventIdx = idx; sel.eventChoice = null; sel.optOrder = shuffle(m.events[idx].options.map(o => o.id)); }
    Object.keys(MISSIONS).forEach(k => {
      const m = MISSIONS[k];
      const sel = { outcomes: [], coreTech: [], supportTech: [], structure: null, control: null, timeSpace: null, lmsFeature: null };
      setEvent(sel, m, Math.floor(Math.random() * m.events.length));
      state.selections[k] = sel;
    });

    // 依表 7.12：1＝是、0.5＝也許／需搭配、0＝否（順序：語文訊息、心智技能、認知策略、態度、動作技能）
    const OM = a => ({ verbal: a[0], intellectual: a[1], cognitive: a[2], attitude: a[3], motor: a[4] });
    const OUTCOME_MATRIX = {
      online_interactive: OM([1, 1, 1, .5, 0]), cbt_repurpose: OM([1, 1, 1, 0, 0]), virtual_class: OM([1, 1, 1, 0, 0]),
      webcast: OM([1, 1, 1, 0, 0]), vr_sim: OM([1, 1, 1, 1, 1]), serious_game: OM([1, 1, 1, 1, 1]), its: OM([1, 1, 1, 0, 1]),
      mobile_learning: OM([1, 1, 0, 0, 0]), flipped: OM([1, 1, 1, .5, .5]), mooc: OM([1, 1, 1, 0, 0]),
      wiki: OM([1, 0, 1, 0, 0]), social_community: OM([1, 0, 1, 0, 0]), shared_workspace: OM([1, 0, 1, 0, 0])
    };

    // 提交前鎖住分數與理論診斷，避免學生「邊點邊看答案」
    function updateHUD() {
      _updateHUDRaw();
      const sub = state.submitted[state.missionId];
      const demo = document.getElementById('demo-btn');
      if (demo) demo.style.display = sub ? '' : 'none';
      if (sub) return;
      document.getElementById('hud-total-score').innerHTML = '— <span class="text-xs font-normal text-slate-400">/ 100</span>';
      ['fit', 'env', 'transfer', 'roi'].forEach(k => {
        document.getElementById('kpi-' + k + '-val').textContent = '—';
        document.getElementById('kpi-' + k + '-bar').style.width = '0%';
      });
      document.getElementById('hud-feedback-list').innerHTML = '<li class="p-2 rounded-lg bg-slate-900/90 border border-slate-800 leading-relaxed">🔒 完成四關並按「提交方案」後，系統才會依第7章理論公布成績與診斷。請先小組討論，再做決定！</li>';
    }

    function initMatrixHighlight() {
      const tbl = document.querySelector('#view-matrix table'); if (!tbl) return;
      tbl.querySelectorAll('thead th').forEach((th, i) => {
        if (!i) return;
        th.style.cursor = 'pointer'; th.title = '點擊高亮此方法';
        th.onclick = () => {
          const on = th.dataset.on !== '1';
          tbl.querySelectorAll('thead th').forEach(t => { t.dataset.on = '0'; });
          tbl.querySelectorAll('tr').forEach(tr => { if (tr.children.length > 1) [...tr.children].forEach((c, j) => { c.style.background = (on && j === i) ? 'rgba(56,189,248,.18)' : ''; }); });
          th.dataset.on = on ? '1' : '0';
        };
      });
    }

    const OBJECTIVES = [
      ['說明新科技如何影響訓練', 1, '僅隱含於表 7.12；建議課前導讀表 7.1–7.2（p.262–264）'],
      ['評估網路訓練平台', 0, '遊戲未涵蓋 → 以 Q4 補足（表 7.5，p.274–275）'],
      ['運用新科技強化學習與訓練轉移', 2, '關卡 2–4（EPSS、時間空間、LMS）'],
      ['說明數位學習、行動學習與模擬的優缺點', 1, '卡片與危機卡部分涵蓋 → Q5 補足'],
      ['說明社群媒體類型與適用時機', 0, '僅有概括的「社群」卡 → Q2 補足（p.281–284）'],
      ['向主管說明各類遠距教學', 0, '僅虛擬教室、直播 → Q3 補足（p.293–295）'],
      ['建議電子績效支援系統（EPSS）內容', 2, '關卡 2 與危機卡'],
      ['比較傳統與科技化訓練的優缺點', 0, '遊戲未涵蓋 → Q1 與發表詰問補足（p.301–302）'],
      ['說明學習管理系統（LMS）的好處', 1, '關卡 4 僅選一項功能 → Q6 補足（表 7.11）']
    ];
    const QUIZ = [
      { obj: 8, q: '依課本 p.302，哪種情境最適合優先採用新科技訓練？', o: ['員工集中在同一廠區，且訓練時間充裕', '員工分散各地、差旅成本高，且學員能自在使用網路與行動裝置', '預算很低，且員工不熟悉任何科技'], a: 1, e: 'p.302 列出七項考慮條件，包括員工分散各地使差旅成本高、學員能自在使用科技、預算與資源充足、符合公司策略與文化等。' },
      { obj: 5, q: '公司想讓全球資深技師共同累積並隨時更新故障排除技巧與 FAQ，最適合哪種社群媒體工具？', o: ['部落格（單人發布、讀者留言）', '維基（Wiki）', '微部落格（簡短訊息與連結）'], a: 1, e: 'p.282：維基讓多人同時建立、編輯、更新並分享知識（如英特爾 Intelpedia）。' },
      { obj: 6, q: '透過衛星同步播放課程，並讓各分店學員用鍵盤即時回答問題，屬於哪一類遠距教學？', o: ['電話會議（Teleconferencing）', '非同步 Podcast', '互動式遠距教學（IDL）'], a: 2, e: 'p.294：IDL 使用衛星技術播放，學員可用鍵盤作答（如 JCPenney）。' },
      { obj: 2, q: '正式推出線上學習前，下列何者屬於「需求評估」？', o: ['上線後再觀察學員是否抱怨', '確認線上學習與企業需求的關聯，並分析頻寬、記憶體等最低技術需求', '直接採購最昂貴的平台，之後再調整'], a: 1, e: '表 7.5、p.274–275：需求評估含取得管理階層支持、IT 部門參與及技術分析（頻寬、記憶體、處理器速度等）。' },
      { obj: 4, q: '下列何者是模擬與遊戲訓練的主要限制？', o: ['模擬無法訓練動作技能', '客製化開發成本高（約 20–30 萬美元），且可能出現模擬病、學員被新奇感分心', '模擬無法提供練習機會與回饋'], a: 1, e: 'p.287–289：臨場感可能引發模擬病，客製模擬成本高；而表 7.12 顯示模擬的動作技能、練習與回饋皆為「是／高」。' },
      { obj: 9, q: '下列何者是學習管理系統（LMS）的主要好處？', o: ['讓學員自行決定是否完成法規必修課', '追蹤報名與完課、記錄法規必修訓練，並串連績效與人力資本管理', '取代所有課程內容的設計與開發'], a: 1, e: '表 7.11、p.298–300：LMS 自動管理與追蹤訓練活動，可降低差旅等成本，並支援合規與人力資本管理。' }
    ];
    function renderQuiz() {
      const ans = state.quiz;
      const tone = ['bg-rose-500/20 text-rose-300', 'bg-amber-500/20 text-amber-300', 'bg-emerald-500/20 text-emerald-300'];
      const lab = ['缺口', '部分', '已涵蓋'];
      document.getElementById('obj-list').innerHTML = OBJECTIVES.map((o, i) => `<li class="flex items-start gap-2 p-2 rounded-lg bg-slate-900/80 border border-slate-800"><span class="px-2 py-0.5 rounded font-bold shrink-0 ${tone[o[1]]}">${lab[o[1]]}</span><span class="text-slate-200"><strong>目標 ${i + 1}：</strong>${o[0]}<span class="text-slate-400">　${o[2]}</span></span></li>`).join('');
      document.getElementById('quiz-box').innerHTML = QUIZ.map((x, qi) => {
        const done = ans[qi] !== undefined;
        return `<div class="bg-slate-900/80 border border-slate-800 rounded-xl p-4 space-y-2"><div class="text-sm font-bold text-white">Q${qi + 1}. ${x.q} <span class="text-xs text-slate-400">（目標 ${x.obj}）</span></div>${x.o.map((t, oi) => {
          const cls = !done ? 'bg-slate-950/60 border-slate-800 text-slate-300 hover:border-sky-500/50' : (oi === x.a ? 'bg-emerald-950/50 border-emerald-500/50 text-emerald-200' : (ans[qi] === oi ? 'bg-rose-950/50 border-rose-500/50 text-rose-200' : 'bg-slate-950/60 border-slate-800 text-slate-500'));
          return `<button ${done ? 'disabled' : ''} onclick="answerQuiz(${qi},${oi})" class="block w-full text-left p-2.5 rounded-lg border text-xs ${cls}">${t}</button>`;
        }).join('')}${done ? `<div class="text-xs text-amber-300">💡 ${x.e}</div>` : ''}</div>`;
      }).join('');
      const n = Object.keys(ans).length, ok = QUIZ.filter((x, i) => ans[i] === x.a).length;
      const miss = [...new Set(QUIZ.filter((x, i) => ans[i] !== undefined && ans[i] !== x.a).map(x => x.obj))];
      document.getElementById('quiz-summary').textContent = n < QUIZ.length ? `已作答 ${n}/${QUIZ.length} 題` : `完成：${ok}/${QUIZ.length} 題正確。` + (miss.length ? `建議複習學習目標 ${miss.join('、')}。` : '全部檢核通過！');
    }
    function answerQuiz(qi, oi) { playSound('click'); if (state.quiz[qi] === undefined) state.quiz[qi] = oi; renderQuiz(); }
    function resetQuiz() { state.quiz = {}; renderQuiz(); }

    // ==================== WEB AUDIO SYNTHESIZER ====================
    let audioCtx = null;
    function playSound(type) {
      if (state.muted) return;
      try {
        if (!audioCtx) {
          const AudioContextClass = window.AudioContext || window.webkitAudioContext;
          if (AudioContextClass) audioCtx = new AudioContextClass();
        }
        if (!audioCtx) return;
        if (audioCtx.state === 'suspended') audioCtx.resume();
        const osc = audioCtx.createOscillator();
        const gain = audioCtx.createGain();
        osc.connect(gain);
        gain.connect(audioCtx.destination);
        const now = audioCtx.currentTime;
        if (type === 'click') {
          osc.type = 'sine';
          osc.frequency.setValueAtTime(520, now);
          osc.frequency.exponentialRampToValueAtTime(680, now + 0.06);
          gain.gain.setValueAtTime(0.08, now);
          gain.gain.exponentialRampToValueAtTime(0.001, now + 0.06);
          osc.start(now);
          osc.stop(now + 0.06);
        } else if (type === 'success') {
          osc.type = 'triangle';
          osc.frequency.setValueAtTime(587.33, now);
          osc.frequency.setValueAtTime(880, now + 0.08);
          gain.gain.setValueAtTime(0.12, now);
          gain.gain.exponentialRampToValueAtTime(0.001, now + 0.22);
          osc.start(now);
          osc.stop(now + 0.22);
        } else if (type === 'warn') {
          osc.type = 'sawtooth';
          osc.frequency.setValueAtTime(220, now);
          osc.frequency.setValueAtTime(180, now + 0.1);
          gain.gain.setValueAtTime(0.09, now);
          gain.gain.exponentialRampToValueAtTime(0.001, now + 0.2);
          osc.start(now);
          osc.stop(now + 0.2);
        }
      } catch (e) {
        // Ignore audio errors
      }
    }

    function toggleMute() {
      state.muted = !state.muted;
      const btn = document.getElementById('mute-btn');
      btn.innerHTML = state.muted
        ? '<i data-lucide="volume-x" class="w-4 h-4 text-rose-400"></i>'
        : '<i data-lucide="volume-2" class="w-4 h-4"></i>';
      if (window.lucide) lucide.createIcons();
    }

    // ==================== CLASSROOM TIMER ====================
    function formatTime(sec) {
      const m = Math.floor(sec / 60);
      const s = sec % 60;
      return `${String(m).padStart(2, '0')}:${String(s).padStart(2, '0')}`;
    }

    function updateTimerDisplay() {
      const el = document.getElementById('timer-display');
      if (el) el.textContent = formatTime(state.timerSeconds);
    }

    function toggleTimer() {
      playSound('click');
      const btn = document.getElementById('timer-btn');
      if (state.timerRunning) {
        clearInterval(state.timerInterval);
        state.timerRunning = false;
        btn.textContent = '繼續';
      } else {
        state.timerRunning = true;
        btn.textContent = '暫停';
        state.timerInterval = setInterval(() => {
          if (state.timerSeconds > 0) {
            state.timerSeconds--;
            updateTimerDisplay();
          } else {
            clearInterval(state.timerInterval);
            state.timerRunning = false;
            btn.textContent = '開始';
            playSound('success');
            showToast('計時結束！請各組準備切換至簡報看板發表方案。');
          }
        }, 1000);
      }
    }

    function resetTimer() {
      playSound('click');
      clearInterval(state.timerInterval);
      state.timerRunning = false;
      state.timerSeconds = 18 * 60;
      document.getElementById('timer-btn').textContent = '開始';
      updateTimerDisplay();
    }

    function setTimerMinutes(mins, label) {
      playSound('success');
      clearInterval(state.timerInterval);
      state.timerRunning = false;
      state.timerSeconds = mins * 60;
      const lbl = document.getElementById('timer-phase-label');
      if (lbl) lbl.textContent = label;
      document.getElementById('timer-btn').textContent = '開始';
      updateTimerDisplay();
      showToast(`已設定課堂計時器為：${label} (${mins} 分鐘)`);
    }

    // ==================== SCORE & DIAGNOSTIC ENGINE ====================
    function evaluateCurrentMission() {
      const m = MISSIONS[state.missionId];
      const sel = state.selections[state.missionId];
      let feedbacks = [];

      // Calculate Budget Used
      let cost = 0;
      sel.coreTech.forEach(id => {
        const item = CORE_TECH_METHODS.find(t => t.id === id);
        if (item) cost += item.cost;
      });
      sel.supportTech.forEach(id => {
        const item = SUPPORT_TECH_METHODS.find(t => t.id === id);
        if (item) cost += item.cost;
      });

      // 1. Fit Score：依課本表 7.12 矩陣逐項計算（不再比對隱藏答案清單）
      const picked = [...sel.coreTech, ...sel.supportTech];
      const best = o => Math.max(0, ...picked.map(t => (OUTCOME_MATRIX[t] || {})[o] || 0));
      const oName = id => LEARNING_OUTCOMES.find(x => x.id === id).name;
      let coverage = 0;
      m.targetOutcomes.forEach(o => {
        const b = best(o);
        coverage += b / m.targetOutcomes.length;
        if (b === 0) feedbacks.push(`⚠️ 【表 7.12】目標成果「${oName(o)}」：你們選的方法在表 7.12 皆為「否」，無法達成。`);
        else if (b < 1) feedbacks.push(`ℹ️ 【表 7.12】目標成果「${oName(o)}」目前只有「也許／需搭配」，建議加入表 7.12 標示「是」的方法。`);
      });
      const matchedOutcomes = sel.outcomes.filter(o => m.targetOutcomes.includes(o)).length;
      const wrongOutcomes = sel.outcomes.length - matchedOutcomes;
      let fit = 20 + coverage * 50 + (matchedOutcomes / m.targetOutcomes.length) * 20 - wrongOutcomes * 6;
      if (sel.coreTech.includes('cbt_repurpose')) {
        fit -= 22;
        feedbacks.push('⚠️ 【課本 p.277 警告】你們勾選了「傳統光碟/簡報直接上網（再利用 Repurposing）」！把效果不彰的單向教材搬上網依然無效，會導致高輟學率。');
      }

      // 2. Positive Learning Environment Score (Table 7.5, 7.6, Learner Control)
      let env = 40;
      if (sel.structure === 'modular' || sel.structure === 'micro_10min') {
        env += 18;
        if (state.missionId === 'sales' && sel.structure === 'micro_10min') {
          env += 8;
          feedbacks.push('✅ 【p.292 行動設計得分】將行動學習控制在 10 分鐘以內且免翻轉螢幕、免裝昂貴外掛（p.276），大幅提升外勤完課率！');
        }
      } else if (sel.structure === 'long_lecture') {
        env -= 20;
        feedbacks.push('⚠️ 【表 7.5 模組化警告】單次 2 小時不間斷長片會造成記憶超載（p.272）與網路當機（p.275 頻寬限制），應改為簡短模組！');
      }

      if (sel.control === 'guided_practice') {
        env += 20;
        feedbacks.push('✅ 【p.278 學習者掌控權得分】允許學員自訂順序與步調，但「不可跳過練習與回饋」並搭配自我管控（Self-regulation）提示，學習成效最高！');
      } else if (sel.control === 'free_skip') {
        env -= 15;
        feedbacks.push('⚠️ 【p.278 掌控權陷阱】課本 p.278 研究指出：若讓學員隨意跳過實作練習或自己控制回饋數量，反而會降低長期記憶與訓練轉移！');
      } else if (sel.control === 'locked_passive') {
        env -= 12;
        feedbacks.push('⚠️ 【p.267 掌控權不足】完全鎖死進度且無練習互動，學員淪為被動接收者（圖7.2 傳統單向環境）。');
      }

      // 3. Training Transfer & Support Tech (EPSS, Expert System, Time & Space)
      let transfer = 35;
      const matchedSupport = sel.supportTech.filter(s => m.recommendedSupport.includes(s)).length;
      transfer += matchedSupport * 16;

      if (sel.supportTech.includes('epss') && state.missionId === 'sales') {
        transfer += 10;
        feedbacks.push('✅ 【p.297 EPSS 績效支援得分】仿照 ADP「2分鐘 Learning Bytes」與 SNI 談判檢核清單，讓業務在客戶現場即時查詢，完美解決罕見任務記憶負荷！');
      }
      if (sel.supportTech.includes('expert_sys') && state.missionId === 'eng') {
        transfer += 10;
        feedbacks.push('✅ 【p.296 專家系統得分】建置現場排障專家系統＋內部 Wiki（Intelpedia），有效防止資深技師離職造成知識斷層（表7.10）！');
      }
      if (sel.supportTech.length === 0) {
        transfer -= 18;
        feedbacks.push('⚠️ 【表 7.10 訓練支援缺失】未配置任何訓練支援科技（EPSS/專家系統/社群 Wiki），學員回到工作現場遇到問題無人支援，訓練轉移將大幅衰退！');
      }

      if (sel.timeSpace === 'learning_lab' || sel.timeSpace === 'scheduled_block') {
        transfer += 15;
      } else if (sel.timeSpace === 'off_hours') {
        transfer -= 22;
        env -= 15;
        feedbacks.push('⚠️ 【p.279 時間與空間嚴重警告】課本 p.279 強調：「期望學員在上班休息時間或個人休假完成網路訓練是不切實際的！」必須提供專屬訓練時段或學習實驗室。');
      }

      // 4. Cost-Benefit & Crisis Event Defense (ROI & LMS)
      // 成本效益 = 目標成果涵蓋度 ÷ 花費（不再獎勵「花越多越好」）
      let roi = 45 + Math.round(coverage * 30 - cost * 0.15);
      if (cost > 100) {
        roi -= (cost - 100) * 1.2;
        feedbacks.push(`⚠️ 【預算超支警告】目前科技組合耗用 ${cost} 點（上限 100 點），開發成本過高（p.289），請精簡次要工具或善用低成本社群/EPSS 搭配。`);
      }
      if (cost > 0 && coverage < 0.5) feedbacks.push(`⚠️ 【成本效益】已耗用 ${cost} 點，但僅涵蓋目標成果的 ${Math.round(coverage * 100)}%，請回頭對照表 7.12。`);

      if (sel.lmsFeature === m.optimalEnv.lmsFeature) {
        roi += 12;
        transfer += 8;
      }

      // Event impact
      const ev = m.events[sel.eventIdx] || m.events[0];
      const chosenOpt = ev.options.find(o => o.id === sel.eventChoice);
      if (chosenOpt) {
        fit += (chosenOpt.impact.fit || 0);
        env += (chosenOpt.impact.env || 0);
        transfer += (chosenOpt.impact.transfer || 0);
        roi += (chosenOpt.impact.roi || 0);
        feedbacks.unshift(`🎯 【突發危機決策】${chosenOpt.feedback}`);
      }

      // Clamp 0-100
      fit = Math.max(10, Math.min(100, Math.round(fit)));
      env = Math.max(10, Math.min(100, Math.round(env)));
      transfer = Math.max(10, Math.min(100, Math.round(transfer)));
      roi = Math.max(10, Math.min(100, Math.round(roi)));
      const total = Math.round((fit + env + transfer + roi) / 4);

      return { cost, fit, env, transfer, roi, total, feedbacks };
    }

    // ==================== UI RENDERING ====================
    function getMissionCost(missionId) {
      const sel = state.selections[missionId || state.missionId];
      let cost = 0;
      sel.coreTech.forEach(id => {
        const item = CORE_TECH_METHODS.find(t => t.id === id);
        if (item) cost += item.cost;
      });
      sel.supportTech.forEach(id => {
        const item = SUPPORT_TECH_METHODS.find(t => t.id === id);
        if (item) cost += item.cost;
      });
      return cost;
    }

    function renderMissionBrief() {
      const m = MISSIONS[state.missionId];
      const box = document.getElementById('mission-brief-card');
      box.innerHTML = `
        <div class="flex flex-wrap items-center justify-between gap-2 mb-2.5">
          <div class="flex items-center gap-2">
            <span class="px-3 py-1 rounded-md text-xs sm:text-sm font-bold bg-amber-500/20 text-amber-300 border border-amber-500/40">${m.badge}</span>
            <span class="text-xs sm:text-sm text-slate-300">請詳讀個案現況與問題診斷資料，再依序完成下方 4 個關卡決策</span>
          </div>
          <span class="text-xs sm:text-sm font-bold text-sky-400">${esc(state.groupName)}</span>
        </div>
        <h2 class="text-lg sm:text-xl font-bold text-white mb-2">${m.name}</h2>
        <p class="text-sm sm:text-base text-slate-200 mb-3 leading-relaxed"><strong class="text-sky-300">👥 受訓對象與職責特性：</strong>${m.persona}</p>
        <div class="bg-rose-950/45 border border-rose-500/40 rounded-xl p-3.5 text-sm sm:text-base text-rose-100 leading-relaxed">
          <strong class="text-rose-400">🚨 企業當前培訓危機與痛點：</strong>${m.painPoint}
        </div>
      `;
    }

    function updateStepperUI() {
      for (let i = 1; i <= 4; i++) {
        const btn = document.getElementById(`step-btn-${i}`);
        if (!btn) continue;
        if (i === state.currentStage) {
          btn.className = 'p-2.5 rounded-xl border text-left transition flex items-center gap-2 bg-sky-500/25 border-sky-400 text-white shadow-md shadow-sky-500/10';
        } else if (i < state.currentStage) {
          btn.className = 'p-2.5 rounded-xl border text-left transition flex items-center gap-2 bg-emerald-950/40 border-emerald-500/40 text-emerald-200 hover:border-emerald-400';
        } else {
          btn.className = 'p-2.5 rounded-xl border text-left transition flex items-center gap-2 bg-slate-800/70 border-slate-700 text-slate-300 hover:border-slate-500';
        }
      }
      document.getElementById('prev-stage-btn').style.visibility = state.currentStage === 1 ? 'hidden' : 'visible';
      const nextBtn = document.getElementById('next-stage-btn');
      if (state.currentStage === 4) {
        nextBtn.innerHTML = '<span>' + (state.submitted[state.missionId] ? '前往小組發表看板' : '提交方案並公布診斷') + '</span><i data-lucide="presentation" class="w-4 h-4"></i>';
      } else {
        nextBtn.innerHTML = '<span>下一關</span><i data-lucide="arrow-right" class="w-4 h-4"></i>';
      }
    }

    function renderCurrentStage() {
      const m = MISSIONS[state.missionId];
      const sel = state.selections[state.missionId];
      const ws = document.getElementById('stage-workspace');

      if (state.currentStage === 1) {
        ws.innerHTML = `
          <div class="space-y-5">
            <div class="border-b border-slate-700/80 pb-3">
              <span class="text-xs sm:text-sm font-bold text-sky-400 uppercase">STAGE 1 · 需求評估、個案現況與學習成果診斷（對照課本表 7.4、表 7.5 & 表 7.12）</span>
              <h3 class="text-lg sm:text-xl font-bold text-white mt-1">第一關：完整檢視個案問題與現況，並診斷最核心的「目標學習成果」</h3>
              <p class="text-sm text-slate-300 mt-1">在規劃科技化訓練前，必須先完成「需求評估」（課本 p.274–275：包含組織分析、任務分析與人員技術分析）。請小組成員詳讀下方完整現況與問題診斷資料，再勾選 <strong>2–3 項目標學習成果</strong>：</p>
            </div>

            <!-- Complete Problem & Current Status Diagnostic Box -->
            <div class="bg-slate-900/90 border border-sky-500/35 rounded-2xl p-4 sm:p-5 space-y-3">
              <div class="flex items-center justify-between flex-wrap gap-2 border-b border-slate-800 pb-2.5">
                <div class="flex items-center gap-2 text-amber-400 font-bold text-sm sm:text-base">
                  <i data-lucide="file-search" class="w-5 h-5"></i>
                  <span>【個案現況與問題完整診斷報告】${m.name}</span>
                </div>
                <span class="text-xs font-semibold px-2.5 py-1 rounded bg-slate-800 text-sky-300 border border-slate-700">課本 p.274 需求評估 & p.302 科技採用條件</span>
              </div>
              <div class="grid grid-cols-1 gap-2.5 text-sm text-slate-200 leading-relaxed">
                ${(m.statusDetails || []).map(item => `
                  <div class="p-3 rounded-xl bg-slate-950/75 border border-slate-800/90 flex items-start gap-2.5">
                    <span class="text-amber-400 font-bold mt-0.5">▸</span>
                    <span>${item}</span>
                  </div>
                `).join('')}
              </div>
            </div>

            <div class="space-y-2.5">
              <div class="flex items-center justify-between">
                <h4 class="text-sm sm:text-base font-bold text-sky-300">▼ 請根據上述問題與現況，勾選此職群最核心的「目標學習成果」（可複選 1–3 項，已選 ${sel.outcomes.length}/3 項）：</h4>
              </div>
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-3.5">
                ${LEARNING_OUTCOMES.map(o => {
                  const active = sel.outcomes.includes(o.id);
                  return `
                    <div onclick="toggleOutcome('${o.id}')" class="card-selectable cursor-pointer rounded-xl p-4 border ${active ? 'card-selected' : 'bg-slate-900/70 border-slate-700/80'}">
                      <div class="flex items-center justify-between mb-1.5">
                        <span class="text-base font-bold text-white">${o.name}</span>
                        <span class="w-6 h-6 rounded-md flex items-center justify-center text-sm font-bold ${active ? 'bg-sky-400 text-slate-950' : 'bg-slate-800 text-slate-500'}">${active ? '✓' : ''}</span>
                      </div>
                      <p class="text-sm text-slate-300 leading-relaxed">${o.desc}</p>
                    </div>
                  `;
                }).join('')}
              </div>
            </div>
          </div>
        `;
      } else if (state.currentStage === 2) {
        const currentCost = getMissionCost();
        const remainingCost = 100 - currentCost;
        ws.innerHTML = `
          <div class="space-y-5">
            <div class="border-b border-slate-700/80 pb-3 flex flex-wrap items-center justify-between gap-3">
              <div>
                <span class="text-xs sm:text-sm font-bold text-sky-400 uppercase">STAGE 2 · 科技化訓練方法與訓練支援科技配置（硬性預算上限 100 點）</span>
                <h3 class="text-lg sm:text-xl font-bold text-white mt-1">第二關：在 100 點預算限制內，配置「核心科技」＋「訓練支援科技」</h3>
                <p class="text-sm text-slate-300 mt-1">課本 p.285 & p.302 強調：單一科技難以兼顧所有需求，請選擇 <strong>1–3 項核心訓練方法</strong>，並搭配 <strong>1–2 項訓練支援科技（EPSS/專家系統/社群）</strong>。系統已啟用<strong>硬性預算限制（上限 100 點）</strong>，超出剩餘點數的項目將無法選取！</p>
              </div>
              <div class="bg-slate-900 border ${remainingCost < 15 ? 'border-amber-500/60' : 'border-sky-500/50'} rounded-xl px-4 py-2.5 text-right shrink-0">
                <div class="text-xs text-slate-400">目前已用預算 ／ 剩餘可用點數</div>
                <div class="font-mono text-base sm:text-lg font-black ${remainingCost === 0 ? 'text-amber-400' : 'text-sky-300'}">已用 ${currentCost} 點 <span class="text-slate-500">|</span> 剩餘 ${remainingCost} 點</div>
              </div>
            </div>

            <div>
              <h4 class="text-sm font-bold uppercase tracking-wider text-amber-400 mb-3">A. 核心科技化與混合式訓練方法（點擊卡片選擇 1–3 項，已選 ${sel.coreTech.length}/3 項）</h4>
              <div class="grid grid-cols-1 md:grid-cols-2 gap-3.5">
                ${CORE_TECH_METHODS.map(t => {
                  const active = sel.coreTech.includes(t.id);
                  const overBudget = !active && (currentCost + t.cost > 100);
                  return `
                    <div onclick="toggleCoreTech('${t.id}')" class="card-selectable cursor-pointer rounded-xl p-4 border ${active ? 'card-selected' : (overBudget ? 'bg-slate-950/50 border-slate-800/60 opacity-50' : 'bg-slate-900/70 border-slate-700/80')}">
                      <div class="flex items-start justify-between gap-2 mb-1.5">
                        <div>
                          <span class="text-xs font-semibold px-2.5 py-0.5 rounded bg-sky-500/20 text-sky-300 border border-sky-500/30">${t.tag}</span>
                          <h5 class="text-base font-bold text-white mt-1.5">${t.name}</h5>
                        </div>
                        <span class="font-mono text-xs sm:text-sm font-bold px-2.5 py-1 rounded ${overBudget ? 'bg-rose-950/60 text-rose-300 border-rose-500/40' : 'bg-slate-800 text-amber-300 border-slate-700'} border shrink-0">${t.cost} 點${overBudget ? ' (超支)' : ''}</span>
                      </div>
                      <p class="text-sm text-slate-300 leading-relaxed mb-2">${t.desc}</p>
                      <div class="text-xs text-slate-400">📖 課本依據：${t.Ref}</div>
                    </div>
                  `;
                }).join('')}
              </div>
            </div>

            <div class="pt-3 border-t border-slate-800">
              <h4 class="text-sm font-bold uppercase tracking-wider text-emerald-400 mb-3">B. 訓練支援科技與非正式社群共學（表 7.10 強化工作現場轉移，選 1–2 項，已選 ${sel.supportTech.length}/2 項）</h4>
              <div class="grid grid-cols-1 md:grid-cols-2 gap-3.5">
                ${SUPPORT_TECH_METHODS.map(s => {
                  const active = sel.supportTech.includes(s.id);
                  const overBudget = !active && (currentCost + s.cost > 100);
                  return `
                    <div onclick="toggleSupportTech('${s.id}')" class="card-selectable cursor-pointer rounded-xl p-4 border ${active ? 'card-selected' : (overBudget ? 'bg-slate-950/50 border-slate-800/60 opacity-50' : 'bg-slate-900/70 border-slate-700/80')}">
                      <div class="flex items-center justify-between gap-2 mb-1.5">
                        <h5 class="text-base font-bold text-white">${s.name}</h5>
                        <span class="font-mono text-xs sm:text-sm font-bold px-2.5 py-0.5 rounded ${overBudget ? 'bg-rose-950/60 text-rose-300 border-rose-500/40' : 'bg-slate-800 text-emerald-300 border-slate-700'} border shrink-0">${s.cost} 點${overBudget ? ' (超支)' : ''}</span>
                      </div>
                      <p class="text-sm text-slate-300 leading-relaxed mb-1.5">${s.desc}</p>
                      <div class="text-xs text-slate-400">📖 課本依據：${s.Ref}</div>
                    </div>
                  `;
                }).join('')}
              </div>
            </div>
          </div>
        `;
      } else if (state.currentStage === 3) {
        ws.innerHTML = `
          <div class="space-y-5">
            <div class="border-b border-slate-700/80 pb-3">
              <span class="text-xs font-bold text-sky-400 uppercase">STAGE 3 · 建立正面的線上學習環境（課本表 7.5、表 7.6 & p.278–279）</span>
              <h3 class="text-base sm:text-lg font-bold text-white mt-0.5">第三關：設定「課程模組結構」、「學習者掌控權」與「學習時間空間」</h3>
              <p class="text-xs text-slate-400 mt-1">課本 p.301 強調：「沒有任何一種訓練方法本質上優於其他方法；要讓方法有成效，必須建立正面的學習環境！」</p>
            </div>

            <div class="space-y-4">
              <!-- 1. Module Structure -->
              <div class="bg-slate-900/80 p-4 rounded-xl border border-slate-800 space-y-2">
                <label class="block text-xs font-bold text-amber-400">1. 課程模組與介面設計原則（表 7.5 & p.292）：</label>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-2.5">
                  <button onclick="setEnvOption('structure', 'modular')" class="p-3 rounded-xl border text-left text-xs transition ${sel.structure === 'modular' ? 'card-selected text-white' : 'bg-slate-950/60 border-slate-800 text-slate-300'}">
                    <div class="font-bold mb-1">✅ 1–2 小時分段式互動模組</div>
                    <div class="text-slate-400">每個模組自成體系，將練習分配在模組內或之間（表7.6），省略多餘視覺與音效。</div>
                  </button>
                  <button onclick="setEnvOption('structure', 'micro_10min')" class="p-3 rounded-xl border text-left text-xs transition ${sel.structure === 'micro_10min' ? 'card-selected text-white' : 'bg-slate-950/60 border-slate-800 text-slate-300'}">
                    <div class="font-bold mb-1">📱 ≤10 分鐘行動微學習模組</div>
                    <div class="text-slate-400">專為手機/平板小螢幕設計，免翻轉螢幕、免裝外掛程式（p.276, 292），適合外勤人員。</div>
                  </button>
                  <button onclick="setEnvOption('structure', 'long_lecture')" class="p-3 rounded-xl border text-left text-xs transition ${sel.structure === 'long_lecture' ? 'card-selected text-white' : 'bg-slate-950/60 border-slate-800 text-slate-300'}">
                    <div class="font-bold mb-1">❌ 3 小時完整錄影不切割</div>
                    <div class="text-slate-400">將整天實體演講一刀未剪放上網，包含高畫質大型外掛動畫（易造成記憶超載與頻寬當機）。</div>
                  </button>
                </div>
              </div>

              <!-- 2. Learner Control -->
              <div class="bg-slate-900/80 p-4 rounded-xl border border-slate-800 space-y-2">
                <label class="block text-xs font-bold text-sky-400">2. 學習者掌控權（Learner Control）與自我管控設計（課本 p.278）：</label>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-2.5">
                  <button onclick="setEnvOption('control', 'guided_practice')" class="p-3 rounded-xl border text-left text-xs transition ${sel.control === 'guided_practice' ? 'card-selected text-white' : 'bg-slate-950/60 border-slate-800 text-slate-300'}">
                    <div class="font-bold mb-1">✅ 自訂順序步調＋強制練習回饋</div>
                    <div class="text-slate-400">學員可控制授課內容順序與速度，但<strong>不能跳過實作練習</strong>，並提供自我管控（Self-regulation）提示（p.278）。</div>
                  </button>
                  <button onclick="setEnvOption('control', 'self_paced_no_skip')" class="p-3 rounded-xl border text-left text-xs transition ${sel.control === 'self_paced_no_skip' ? 'card-selected text-white' : 'bg-slate-950/60 border-slate-800 text-slate-300'}">
                    <div class="font-bold mb-1">🔖 書籤標記暫停＋課前及格檢定</div>
                    <div class="text-slate-400">護理/外勤人員可隨時暫停並在處理公務後接續上課（p.299），且參加實體課前須通過線上測驗（p.285）。</div>
                  </button>
                  <button onclick="setEnvOption('control', 'free_skip')" class="p-3 rounded-xl border text-left text-xs transition ${sel.control === 'free_skip' ? 'card-selected text-white' : 'bg-slate-950/60 border-slate-800 text-slate-300'}">
                    <div class="font-bold mb-1">❌ 100% 自由跳過練習與回饋</div>
                    <div class="text-slate-400">讓學員自己決定要不要做練習與接收多少回饋（p.278 警告：會減少對教材的長期記憶）。</div>
                  </button>
                </div>
              </div>

              <!-- 3. Time and Space -->
              <div class="bg-slate-900/80 p-4 rounded-xl border border-slate-800 space-y-2">
                <label class="block text-xs font-bold text-emerald-400">3. 提供線上學習的時間與空間政策（課本 p.278–279）：</label>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-2.5">
                  <button onclick="setEnvOption('timeSpace', 'learning_lab')" class="p-3 rounded-xl border text-left text-xs transition ${sel.timeSpace === 'learning_lab' ? 'card-selected text-white' : 'bg-slate-950/60 border-slate-800 text-slate-300'}">
                    <div class="font-bold mb-1">🏢 設立無干擾「學習實驗室」</div>
                    <div class="text-slate-400">在廠區設立專屬學習實驗室與 VR 設備區，讓線上學習不受工作場所電話與雜事干擾（p.279）。</div>
                  </button>
                  <button onclick="setEnvOption('timeSpace', 'scheduled_block')" class="p-3 rounded-xl border text-left text-xs transition ${sel.timeSpace === 'scheduled_block' ? 'card-selected text-white' : 'bg-slate-950/60 border-slate-800 text-slate-300'}">
                    <div class="font-bold mb-1">📅 主管排定工作日 1–2 小時訓練假</div>
                    <div class="text-slate-400">由直屬主管在一般工作日安排專屬「訓練時間」並傳達訓練重要性，提高學習動機（p.279）。</div>
                  </button>
                  <button onclick="setEnvOption('timeSpace', 'off_hours')" class="p-3 rounded-xl border text-left text-xs transition ${sel.timeSpace === 'off_hours' ? 'card-selected text-white' : 'bg-slate-950/60 border-slate-800 text-slate-300'}">
                    <div class="font-bold mb-1">❌ 要求員工用午休或個人休假完課</div>
                    <div class="text-slate-400">要求員工在辦公桌自己找午休或下班時間看課（p.279 警告：模糊工作界線且不切實際）。</div>
                  </button>
                </div>
              </div>
            </div>
          </div>
        `;
      } else if (state.currentStage === 4) {
        const ev = m.events[sel.eventIdx] || m.events[0];
        ws.innerHTML = `
          <div class="space-y-5">
            <div class="border-b border-slate-700/80 pb-3 flex flex-wrap items-center justify-between gap-2">
              <div>
                <span class="text-xs font-bold text-rose-400 uppercase">STAGE 4 · 隨機突發危機應變 ＆ LMS 學習管理系統整合（表 7.11）</span>
                <h3 class="text-base sm:text-lg font-bold text-white mt-0.5">第四關：抽取突發危機事件卡，並設定 LMS 追蹤機制</h3>
              </div>
              <button onclick="drawNextEvent()" class="px-3 py-1.5 rounded-xl bg-rose-500/20 border border-rose-500/40 text-rose-300 hover:bg-rose-500/30 text-xs font-bold flex items-center gap-1.5">
                <i data-lucide="shuffle" class="w-3.5 h-3.5"></i>
                <span>抽換另一張突發危機卡</span>
              </button>
            </div>

            <!-- Crisis Card -->
            <div class="bg-gradient-to-br from-rose-950/60 to-slate-900 border border-rose-500/40 rounded-2xl p-4 sm:p-5 space-y-3">
              <div class="flex items-center gap-2 text-rose-400 text-xs font-bold">
                <i data-lucide="alert-triangle" class="w-4 h-4"></i>
                <span>突發危機挑戰卡（小組討論如何運用課本理論化解）</span>
              </div>
              <h4 class="text-sm sm:text-base font-bold text-white">${ev.title}</h4>
              <p class="text-xs sm:text-sm text-slate-300 leading-relaxed">${ev.desc}</p>

              <div class="space-y-2.5 pt-2">
                ${(sel.optOrder || ev.options.map(o => o.id)).map(id => ev.options.find(o => o.id === id)).map(opt => {
                  const active = sel.eventChoice === opt.id;
                  return `
                    <div onclick="selectEventOption('${opt.id}')" class="card-selectable cursor-pointer p-3.5 rounded-xl border text-xs sm:text-sm ${active ? 'card-selected text-white' : 'bg-slate-900/80 border-slate-700 text-slate-300'}">
                      <div class="flex items-start gap-2.5">
                        <span class="w-5 h-5 rounded-full flex items-center justify-center text-xs font-bold shrink-0 mt-0.5 ${active ? 'bg-sky-400 text-slate-950' : 'bg-slate-800 text-slate-400'}">${active ? '✓' : ''}</span>
                        <div class="space-y-1">
                          <div class="font-semibold">${opt.text}</div>
                          ${active && state.submitted[state.missionId] ? `<div class="text-xs text-amber-300 pt-1 border-t border-slate-700/80">💡 系統理論解析：${opt.feedback}</div>` : ''}
                        </div>
                      </div>
                    </div>
                  `;
                }).join('')}
              </div>
            </div>

            <!-- LMS Integration (Table 7.11) -->
            <div class="bg-slate-900/80 p-4 rounded-xl border border-slate-800 space-y-2.5">
              <label class="block text-xs font-bold text-sky-400">最後一步：選擇「學習管理系統（LMS，表 7.11 & p.298–300）」的核心人力資本整合功能：</label>
              <div class="grid grid-cols-1 md:grid-cols-3 gap-2.5">
                <button onclick="setEnvOption('lmsFeature', 'competency_gap')" class="p-3 rounded-xl border text-left text-xs transition ${sel.lmsFeature === 'competency_gap' ? 'card-selected text-white' : 'bg-slate-950/60 border-slate-800 text-slate-300'}">
                  <div class="font-bold mb-1">🔧 連結職能模型與技能斷層診斷</div>
                  <div class="text-slate-400">仿照 Turner 建築公司（p.299），將 LMS 連結績效評估，分析各廠區工程師技能弱點並配置訓練預算。</div>
                </button>
                <button onclick="setEnvOption('lmsFeature', 'talent_integration')" class="p-3 rounded-xl border text-left text-xs transition ${sel.lmsFeature === 'talent_integration' ? 'card-selected text-white' : 'bg-slate-950/60 border-slate-800 text-slate-300'}">
                  <div class="font-bold mb-1">📈 連結職涯發展與訓後行為追蹤</div>
                  <div class="text-slate-400">仿照 Vanguard（p.299）與諾華（p.286），整合正式/非正式學習資源並追蹤訓後 1 個月專案行為轉移。</div>
                </button>
                <button onclick="setEnvOption('lmsFeature', 'compliance_tracking')" class="p-3 rounded-xl border text-left text-xs transition ${sel.lmsFeature === 'compliance_tracking' ? 'card-selected text-white' : 'bg-slate-950/60 border-slate-800 text-slate-300'}">
                  <div class="font-bold mb-1">🛡️ 自動提醒完課與法規證照到期日</div>
                  <div class="text-slate-400">仿照灰狗巴士（p.271）與 MasTec（p.300），自動推播未完課提醒，並產出主管核准與法規合規到期報告。</div>
                </button>
              </div>
            </div>
          </div>
        `;
      }

      ws.querySelectorAll('.card-selectable').forEach(e => { e.tabIndex = 0; e.setAttribute('role', 'button'); });
      if (window.lucide) lucide.createIcons();
    }

    function _updateHUDRaw() {
      const res = evaluateCurrentMission();
      document.getElementById('hud-total-score').innerHTML = `${res.total} <span class="text-xs font-normal text-slate-400">/ 100</span>`;
      document.getElementById('hud-budget-text').textContent = `${res.cost} / 100 點`;
      const budgetBar = document.getElementById('hud-budget-bar');
      budgetBar.style.width = `${Math.min(100, res.cost)}%`;
      budgetBar.className = res.cost > 100
        ? 'h-full bg-rose-500 transition-all duration-300'
        : (res.cost >= 85 ? 'h-full bg-amber-400 transition-all duration-300' : 'h-full bg-sky-500 transition-all duration-300');
      const bw = document.getElementById('hud-budget-warning');
      if (bw) {
        bw.textContent = res.cost > 100
          ? `⚠️ 已超出 100 點預算上限（超支 ${res.cost - 100} 點），請調整配置！`
          : `目前已用 ${res.cost} 點，尚餘 ${100 - res.cost} 點可用（硬性上限 100 點）。`;
      }

      document.getElementById('kpi-fit-val').textContent = `${res.fit}%`;
      document.getElementById('kpi-fit-bar').style.width = `${res.fit}%`;

      document.getElementById('kpi-env-val').textContent = `${res.env}%`;
      document.getElementById('kpi-env-bar').style.width = `${res.env}%`;

      document.getElementById('kpi-transfer-val').textContent = `${res.transfer}%`;
      document.getElementById('kpi-transfer-bar').style.width = `${res.transfer}%`;

      document.getElementById('kpi-roi-val').textContent = `${res.roi}%`;
      document.getElementById('kpi-roi-bar').style.width = `${res.roi}%`;

      const listEl = document.getElementById('hud-feedback-list');
      listEl.innerHTML = res.feedbacks.map(f => `
        <li class="p-2 rounded-lg bg-slate-900/90 border border-slate-800 leading-relaxed">${f}</li>
      `).join('');
    }

    // ==================== PITCH BOARD GENERATOR ====================
    function renderPitchView() {
      const m = MISSIONS[state.missionId];
      const sel = state.selections[state.missionId];
      const res = evaluateCurrentMission();

      document.getElementById('pitch-mission-tag').textContent = m.name;
      document.getElementById('pitch-title').textContent = `${state.groupName} — 科技化訓練整合解決方案提案`;
      document.getElementById('pitch-score-badge').textContent = `${res.total} 分`;

      const chosenOutcomes = LEARNING_OUTCOMES.filter(o => sel.outcomes.includes(o.id)).map(o => o.name);
      const chosenCore = CORE_TECH_METHODS.filter(t => sel.coreTech.includes(t.id));
      const chosenSupport = SUPPORT_TECH_METHODS.filter(s => sel.supportTech.includes(s.id));

      const structureMap = {
        modular: '1–2 小時分段式互動模組（將練習嵌入模組間，表7.6）',
        micro_10min: '≤10 分鐘行動微學習短片／Podcast（免翻轉螢幕、免裝外掛，p.276, 292）',
        long_lecture: '3 小時完整錄影不切割（⚠️ 易造成記憶超載與當機）'
      };
      const controlMap = {
        guided_practice: '自訂內容順序與步調，但不可跳過實作練習＋提供自我管控提示（p.278）',
        self_paced_no_skip: '支援隨時書籤暫停接續學習（p.299）＋實體課前線上及格檢定（p.285）',
        free_skip: '100% 自由跳過練習與控制回饋數量（⚠️ 課本警告會降低長期記憶）'
      };
      const timeSpaceMap = {
        learning_lab: '於各廠區設立無工作干擾之專屬「學習實驗室」（p.279）',
        scheduled_block: '由直屬主管於工作日排定專屬「1–2 小時訓練時段」，不佔用休假（p.279）',
        off_hours: '要求員工利用午休或個人休假完成（⚠️ 課本警告不切實際）'
      };
      const lmsMap = {
        competency_gap: '連結職能模型與績效評估，自動診斷各廠區技能缺口（仿 Turner 建築，p.299）',
        talent_integration: '整合正式與非正式學習資源，追蹤訓後 1 個月行為轉移（仿諾華/Vanguard，p.286, 299）',
        compliance_tracking: '自動推播未完課提醒，產出各國法規必修完成率與到期日報告（仿灰狗巴士/MasTec，p.271, 300）'
      };

      const ev = m.events[sel.eventIdx] || m.events[0];
      const chosenOpt = ev.options.find(o => o.id === sel.eventChoice);

      const container = document.getElementById('pitch-cards-container');
      container.innerHTML = `
        <div class="bg-slate-900/90 border border-slate-700 rounded-2xl p-5 space-y-2.5">
          <div class="text-xs font-bold text-sky-400 uppercase">1. 問題診斷與目標學習成果（表 7.12）</div>
          <p class="text-xs text-slate-300 leading-relaxed"><strong>痛點根源：</strong>過去單純將實體課簡報與錄影直接搬上網（再利用 Repurposing，p.277），缺乏練習、回饋與人際互動。</p>
          <div class="text-xs text-white font-semibold">本組鎖定之關鍵學習成果：</div>
          <div class="flex flex-wrap gap-1.5">
            ${chosenOutcomes.map(name => `<span class="px-2.5 py-1 rounded-lg bg-sky-500/20 text-sky-300 border border-sky-500/30 text-xs font-bold">${name}</span>`).join('')}
          </div>
        </div>

        <div class="bg-slate-900/90 border border-slate-700 rounded-2xl p-5 space-y-2.5">
          <div class="flex items-center justify-between">
            <span class="text-xs font-bold text-amber-400 uppercase">2. 混合式科技訓練組合（預算耗用 ${res.cost}/100 點）</span>
            <span class="text-xs text-emerald-400 font-mono font-bold">適配度 ${res.fit}%</span>
          </div>
          <div class="space-y-1.5 text-xs">
            <div class="text-slate-400 font-semibold">核心科技訓練方法：</div>
            ${chosenCore.map(c => `<div class="p-2 rounded-lg bg-slate-950/70 border border-slate-800"><strong class="text-amber-300">${c.name}</strong> — <span class="text-slate-300">${c.Ref}</span></div>`).join('')}
            <div class="text-slate-400 font-semibold pt-1">訓練支援科技與社群共學（表 7.10）：</div>
            ${chosenSupport.map(s => `<div class="p-2 rounded-lg bg-slate-950/70 border border-slate-800"><strong class="text-emerald-300">${s.name}</strong> — <span class="text-slate-300">${s.Ref}</span></div>`).join('')}
          </div>
        </div>

        <div class="bg-slate-900/90 border border-slate-700 rounded-2xl p-5 space-y-2">
          <div class="flex items-center justify-between">
            <span class="text-xs font-bold text-indigo-400 uppercase">3. 正面學習環境與學習者掌控權（表 7.5 & 7.6）</span>
            <span class="text-xs text-indigo-300 font-mono font-bold">環境分 ${res.env}%</span>
          </div>
          <ul class="space-y-1.5 text-xs text-slate-200 leading-relaxed">
            <li><strong>・模組與介面設計：</strong>${structureMap[sel.structure]}</li>
            <li><strong>・學習者掌控權（p.278）：</strong>${controlMap[sel.control]}</li>
            <li><strong>・時間與空間配置（p.279）：</strong>${timeSpaceMap[sel.timeSpace]}</li>
          </ul>
        </div>

        <div class="bg-slate-900/90 border border-slate-700 rounded-2xl p-5 space-y-2">
          <div class="flex items-center justify-between">
            <span class="text-xs font-bold text-emerald-400 uppercase">4. 突發危機化解與 LMS 管理機制（表 7.11）</span>
            <span class="text-xs text-emerald-300 font-mono font-bold">轉移分 ${res.transfer}%</span>
          </div>
          <ul class="space-y-1.5 text-xs text-slate-200 leading-relaxed">
            <li><strong>・危機情境：</strong>${ev.title}</li>
            <li><strong>・本組應變對策：</strong>${chosenOpt ? chosenOpt.text : '未選擇'}</li>
            <li><strong>・LMS 人力資本整合：</strong>${lmsMap[sel.lmsFeature]}</li>
          </ul>
        </div>
      `;

      // Generate Oral Pitch Script
      const coreNames = chosenCore.map(c => c.name).join('、') || '科技化訓練';
      const supportNames = chosenSupport.map(s => s.name).join('與') || '訓練支援科技';
      const scriptText = `各位高階主管與顧問同仁好，我們是【${state.groupName}】。針對《環航智造科技》在「${m.name}」面臨的跨國培訓危機，我們診斷後發現，過去失敗的主因是落入了課本第7章 p.277 所說的「再利用（Repurposing）」陷阱——也就是把單向授課簡報直接搬上網，卻忽略了此職群真正需要的學習成果是【${chosenOutcomes.join('、')}】。

對照課本表 7.12，我們在 100 點資源預算內配置了 ${res.cost} 點的高效益混合式組合：
第一，在核心訓練上，我們採用【${coreNames}】，結合正式訓練與互動練習；
第二，為了確保訓練轉移（符合表 7.10 情境），我們搭配了【${supportNames}】，讓員工在工作現場遇到問題時能即時獲得專家系統或績效支援（EPSS），而不必死背所有細節。

第三，在建立正面學習環境（表 7.5 與 p.278–279）方面，我們採取「${structureMap[sel.structure]}」，在賦予學習者掌控權的同時，嚴格要求「${controlMap[sel.control]}」，並由公司「${timeSpaceMap[sel.timeSpace]}」，徹底解決完課率低落的問題。

最後，面對「${ev.title}」的挑戰，我們透過「${chosenOpt ? chosenOpt.text : ''}」成功化解，並藉由 LMS 系統執行「${lmsMap[sel.lmsFeature]}」。經系統模擬，本方案可達到 ${res.total} 分的綜合效益，協助公司在 3 個月內達成全球上市目標！`;

      document.getElementById('pitch-script-box').textContent = scriptText;

      // Generate Peer Critique Questions
      const defenseList = document.getElementById('pitch-defense-list');
      let qList = [
        `<li><strong class="text-rose-300">詰問 1（針對學習者掌控權 p.278）：</strong>「你們賦予學員自訂步調的掌控權，但如果學員為了趕快拿到完課證明而狂點下一頁或過度依賴回饋提示，你們在系統上如何防止記憶力衰退？」<br><span class="text-slate-400">👉 防禦提示：引用 p.278「允許控制順序，但禁止跳過練習且不讓學員控制回饋數量，並加入自我管控回想提示」。</span></li>`,
        `<li><strong class="text-rose-300">詰問 2（針對科技限制與備案 p.275, 295）：</strong>「跨國 18 個據點的網路頻寬不一，若遇到直播中斷、外掛程式無法安裝或模擬器暈眩，你們的替代備案是什麼？」<br><span class="text-slate-400">👉 防禦提示：引用 p.276「採用免外掛內建互動功能、鼓勵非尖峰離線下載」及 p.295「講師準備技術故障備案與現場製作人協助」。</span></li>`,
        `<li><strong class="text-rose-300">詰問 3（針對訓練支援取代訓練 p.297）：</strong>「哪些內容其實根本不需要花錢做線上訓練，直接用 EPSS 電子績效支援系統或專家系統就能取代？」<br><span class="text-slate-400">👉 防禦提示：引用表 7.10「罕見任務、資訊密集且頻繁變更的程序」直接以 EPSS（如 2 分鐘 Learning Bytes 或檢核清單）即時支援即可。</span></li>`
      ];
      const has = id => sel.coreTech.includes(id) || sel.supportTech.includes(id);
      const ex = [];
      if (has('mooc')) ex.push('MOOC 完課率僅 10–20%（p.281），且公司機密不宜公開，你們如何確保學員完成並能應用？');
      if (has('vr_sim')) ex.push('客製化模擬開發約 20–30 萬美元（p.289）並有模擬病風險（p.287）；若預算砍半，哪些情境必須保留？');
      if (has('cbt_repurpose')) ex.push('你們選了再利用（p.277）：憑什麼認為這次不會重蹈低完課率覆轍？');
      if (has('mobile_learning')) ex.push('行動學習適合小螢幕與 10 分鐘內的內容（p.292），複雜的動作技能或軟實力如何靠它達成（表 7.12）？');
      if (['wiki', 'social_community', 'shared_workspace'].some(has)) ex.push('依表 7.7，貴公司的文化與策略是否真的支持社群媒體共學？誰負責內容品質審核（p.284）？');
      ex.push('傳統面授同樣可以有效（p.301–302）。依 p.302 七項條件，你們符合哪幾項才值得投資新科技？混合式（p.285）的比例如何決定？');
      defenseList.innerHTML = qList.join('') + ex.map((t, i) => `<li><strong class="text-rose-300">詰問 ${i + 4}（依本組選擇）：</strong>${t}</li>`).join('');
    }

    // ==================== USER INTERACTION HANDLERS ====================
    function switchMainView(view) {
      if (view === 'pitch' && !state.submitted[state.missionId]) {
        showToast('請先在第四關「提交方案」，再產生發表看板。');
        goToStage(4);
        view = 'game';
      }
      playSound('click');
      state.mainView = view;
      ['game', 'pitch', 'matrix', 'lesson', 'quiz'].forEach(v => {
        const sec = document.getElementById(`view-${v}`);
        const tab = document.getElementById(`tab-${v}`);
        if (v === view) {
          sec.classList.remove('hidden');
          tab.className = 'px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition flex items-center gap-1.5 bg-sky-500 text-white shadow';
        } else {
          sec.classList.add('hidden');
          tab.className = 'px-3 py-1.5 rounded-lg text-xs sm:text-sm font-semibold transition flex items-center gap-1.5 text-slate-300 hover:text-white';
        }
      });
      if (view === 'pitch') {
        renderPitchView();
      }
      if (view === 'quiz') renderQuiz();
      if (window.lucide) lucide.createIcons();
    }

    function updateGroupName(val) {
      state.groupName = val || '未命名顧問組';
      renderMissionBrief();
    }

    function selectMission(missionId) {
      playSound('click');
      state.missionId = missionId;
      state.currentStage = 1;
      renderMissionBrief();
      updateStepperUI();
      renderCurrentStage();
      updateHUD();
      showToast(`已切換至：${MISSIONS[missionId].name}`);
    }

    function goToStage(stageNum) {
      playSound('click');
      state.currentStage = stageNum;
      updateStepperUI();
      renderCurrentStage();
    }

    function prevStage() {
      if (state.currentStage > 1) {
        goToStage(state.currentStage - 1);
      }
    }

    function nextStage() {
      if (state.currentStage < 4) {
        goToStage(state.currentStage + 1);
      } else if (!state.submitted[state.missionId]) {
        const x = state.selections[state.missionId];
        if (!x.outcomes.length || !x.coreTech.length || !x.structure || !x.control || !x.timeSpace || !x.lmsFeature || !x.eventChoice) {
          playSound('warn');
          showToast('尚有未決定項目：成果、核心科技、環境三項、危機對策與 LMS 都需選擇。');
          return;
        }
        state.submitted[state.missionId] = true;
        playSound('success');
        renderCurrentStage(); updateStepperUI(); updateHUD();
        showToast('已提交！請對照右側理論診斷，討論後可修改再檢視。');
      } else {
        playSound('success');
        switchMainView('pitch');
      }
    }

    function toggleOutcome(id) {
      playSound('click');
      const arr = state.selections[state.missionId].outcomes;
      const idx = arr.indexOf(id);
      if (idx >= 0) {
        arr.splice(idx, 1);
      } else {
        if (arr.length >= 3) { playSound('warn'); showToast('學習成果最多選 3 項，請先取消其他項目。'); return; }
        arr.push(id);
      }
      renderCurrentStage();
      updateHUD();
    }

    function toggleCoreTech(id) {
      const arr = state.selections[state.missionId].coreTech;
      const idx = arr.indexOf(id);
      if (idx >= 0) {
        playSound('click');
        arr.splice(idx, 1);
      } else {
        if (arr.length >= 3) {
          playSound('warn');
          showToast('核心科技訓練方法最多選擇 3 項，請先取消其他項目。');
          return;
        }
        const item = CORE_TECH_METHODS.find(t => t.id === id);
        const currentCost = getMissionCost();
        if (item && (currentCost + item.cost > 100)) {
          playSound('warn');
          showToast(`預算不足！選取「${item.name}（${item.cost}點）」將達 ${currentCost + item.cost} 點，超過 100 點上限（目前剩餘 ${100 - currentCost} 點）。請先取消其他高成本項目！`);
          return;
        }
        playSound('click');
        arr.push(id);
      }
      renderCurrentStage();
      updateHUD();
    }

    function toggleSupportTech(id) {
      const arr = state.selections[state.missionId].supportTech;
      const idx = arr.indexOf(id);
      if (idx >= 0) {
        playSound('click');
        arr.splice(idx, 1);
      } else {
        if (arr.length >= 2) {
          playSound('warn');
          showToast('訓練支援與社群科技最多選擇 2 項。');
          return;
        }
        const item = SUPPORT_TECH_METHODS.find(t => t.id === id);
        const currentCost = getMissionCost();
        if (item && (currentCost + item.cost > 100)) {
          playSound('warn');
          showToast(`預算不足！選取「${item.name}（${item.cost}點）」將達 ${currentCost + item.cost} 點，超過 100 點上限（目前剩餘 ${100 - currentCost} 點）。請先取消其他項目！`);
          return;
        }
        playSound('click');
        arr.push(id);
      }
      renderCurrentStage();
      updateHUD();
    }

    function setEnvOption(key, val) {
      playSound('click');
      state.selections[state.missionId][key] = val;
      renderCurrentStage();
      updateHUD();
    }

    function drawNextEvent() {
      playSound('click');
      const m = MISSIONS[state.missionId];
      const sel = state.selections[state.missionId];
      setEvent(sel, m, (sel.eventIdx + 1) % m.events.length);
      renderCurrentStage();
      updateHUD();
      showToast('已抽取新的突發危機事件卡！');
    }

    function selectEventOption(optId) {
      playSound('click');
      state.selections[state.missionId].eventChoice = optId;
      renderCurrentStage();
      updateHUD();
    }

    function loadOptimalDemo() {
      playSound('success');
      const m = MISSIONS[state.missionId];
      const sel = state.selections[state.missionId];
      sel.outcomes = [...m.targetOutcomes];
      sel.coreTech = [...m.recommendedCore];
      sel.supportTech = [...m.recommendedSupport];
      sel.structure = m.optimalEnv.structure;
      sel.control = m.optimalEnv.control;
      sel.timeSpace = m.optimalEnv.timeSpace;
      sel.lmsFeature = m.optimalEnv.lmsFeature;
      const ev = m.events[sel.eventIdx];
      // find best option
      let bestOpt = ev.options[0];
      let bestSum = -999;
      ev.options.forEach(o => {
        const s = (o.impact.fit || 0) + (o.impact.env || 0) + (o.impact.transfer || 0) + (o.impact.roi || 0);
        if (s > bestSum) {
          bestSum = s;
          bestOpt = o;
        }
      });
      sel.eventChoice = bestOpt.id;
      renderCurrentStage();
      updateHUD();
      showToast('已載入第7章課本最佳實務配置！');
    }

    function copyPitchText() {
      const scriptText = document.getElementById('pitch-script-box').textContent;
      const temp = document.createElement('textarea');
      temp.value = scriptText;
      document.body.appendChild(temp);
      temp.select();
      try {
        document.execCommand('copy');
        playSound('success');
        showToast('已複製 2.5 分鐘小組發表講稿與方案摘要！');
      } catch (err) {
        showToast('複製失敗，請手動選取文字複製。');
      }
      document.body.removeChild(temp);
    }

    let toastTimer = null;
    function showToast(msg) {
      const box = document.getElementById('toast-box');
      const txt = document.getElementById('toast-msg');
      txt.textContent = msg;
      box.classList.remove('hidden');
      clearTimeout(toastTimer);
      toastTimer = setTimeout(() => {
        box.classList.add('hidden');
      }, 3200);
    }

    // ==================== QR CODE PROJECTION MODAL ====================
    function openQrModal() {
      playSound('click');
      const modal = document.getElementById('qr-modal');
      const input = document.getElementById('qr-url-input');
      let currentUrl = window.location.href;
      if (!currentUrl || currentUrl.startsWith('about:') || currentUrl.startsWith('blob:') || currentUrl.includes('googleusercontent')) {
        currentUrl = input.value || 'https://your-username.github.io/tech-training-game/';
      }
      input.value = currentUrl;
      updateQrImage(currentUrl);
      modal.classList.remove('hidden');
      if (window.lucide) lucide.createIcons();
    }

    function closeQrModal() {
      playSound('click');
      document.getElementById('qr-modal').classList.add('hidden');
    }

    function updateQrImage(url) {
      const cleanUrl = (url || '').trim() || 'https://github.com/';
      const img = document.getElementById('qr-image');
      img.src = 'https://api.qrserver.com/v1/create-qr-code/?size=320x320&margin=10&data=' + encodeURIComponent(cleanUrl);
    }

    function copyGameUrl() {
      const input = document.getElementById('qr-url-input');
      input.select();
      try {
        document.execCommand('copy');
        playSound('success');
        showToast('已複製遊戲網址！');
      } catch (e) {
        showToast('複製失敗，請手動選取網址。');
      }
    }

    // Initialize on load
    window.onload = function() {
      initMatrixHighlight();
      document.addEventListener("keydown", e => { if ((e.key === "Enter" || e.key === " ") && e.target.classList && e.target.classList.contains("card-selectable")) { e.preventDefault(); e.target.click(); } });
      renderMissionBrief();
      updateStepperUI();
      renderCurrentStage();
      updateHUD();
      updateTimerDisplay();
      if (window.lucide) lucide.createIcons();
    };
  </script>
</body>
</html>
