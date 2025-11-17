
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>147自測網站入口</title>
    <link rel="icon" type="image/jpeg" href="OIP.jpg" />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@500;600;700&display=swap"
      rel="stylesheet"
    />
    <style>
      :root{
        --txt:#ffffff; --muted:#e9eefb;
        --card-bg: rgba(255,255,255,.10);
        --card-stroke: rgba(255,255,255,.24);
        --glass: none; /* 省電：移除強背濾 */
        --radius: 16px; --shadow: 0 8px 24px rgba(0,0,0,.36);
        --btn1:#e8f3ff; --btn2:#e8fff7;
        --aurora-o:.6; --stars-o:.85;
        --bg-1:#070b1a; --bg-2:#0b1230;
      }

      .sr-only{
        position:absolute;
        width:1px;
        height:1px;
        padding:0;
        margin:-1px;
        overflow:hidden;
        clip:rect(0,0,0,0);
        white-space:nowrap;
        border:0;
      }

      /* ===== 左上語錄 ===== */
      .quote-box{
        position:fixed;
        top:14px;
        left:14px;
        z-index:6;
        max-width:clamp(220px, 26vw, 2560px);
        padding:12px 16px;
        border-radius:16px;
        color:#0f1530;
        background:linear-gradient(135deg,#ffffff,#f2f6ff);
        border:1px solid rgba(255,255,255,.6);
        box-shadow:0 12px 26px rgba(0,0,0,.2);
        font-family:"Noto Serif TC","Microsoft JhengHei", system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
        font-weight:600;
        line-height:1.45;
        letter-spacing:.2px;
      }
      .quote-text{ font-size:clamp(13px,1.2vw,16px); }
      .quote-author{
        display:block;
        margin-top:6px;
        font-size:clamp(11px,.95vw,13px);
        color:#2a3555;
        opacity:.75;
        text-align:right;
        font-weight:700;
      }
      @media (max-width:640px){
        .quote-box{
          max-width:min(88vw,2560px);
          left:10px;
          right:10px;
          opacity:.95;
        }
      }

      html, body{ min-height:100%; }
      body{
        margin:0;
        color:var(--txt);
        font-family:"Microsoft JhengHei", system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
        text-align:center;
        overflow-y:auto;        /* 允許上下捲動 */
        overflow-x:auto;        /* 若真的溢出，還是可以橫向捲動 */
        -webkit-overflow-scrolling:touch;
        background:
          radial-gradient(1200px 600px at 15% 0%, #5ecbff1a, transparent 60%),
          radial-gradient(900px 700px at 110% 20%, #b79dff1e, transparent 60%),
          linear-gradient(140deg, var(--bg-1) 0%, var(--bg-2) 55%, var(--bg-1) 100%);
      }

      .aurora{
        position:fixed;
        inset:-20%;
        background:
          radial-gradient(50% 120% at 20% 20%, #7cf3d022 0%, transparent 60%),
          radial-gradient(60% 100% at 80% 0%, #82b1ff22 0%, transparent 60%),
          radial-gradient(60% 120% at 50% 120%, #c6a4ff1e 0%, transparent 60%);
        filter: blur(36px);
        pointer-events:none;
        z-index:0;
        opacity:var(--aurora-o);
      }

      canvas#space{
        position:fixed;
        inset:0;
        z-index:0;
        pointer-events:none;
        opacity:var(--stars-o);
      }

     .wrap{
  position:relative;
  z-index:2;

  /* 關鍵兩行：不超過螢幕、但上限拉寬一點 */
  width:100%;
  max-width:2600px;   /* 想更寬可以 1800px，看你喜歡 */

  margin-inline:auto;
  padding-block: clamp(120px, 16vh, 160px) clamp(80px, 10vh, 160px);
  padding-inline: clamp(10px, 4vw, 32px);
  box-sizing:border-box;
  text-align:left;
}

      h1{
        margin:0 0 8px;
        font-size:clamp(28px,4vw,44px);
        letter-spacing:.5px;
        background:linear-gradient(120deg,#eaf4ff,#b3c6ff 40%,#d7fcef 70%,#e9dcff 100%);
        -webkit-background-clip:text;
        color:transparent;
        text-shadow:0 6px 26px rgba(130,177,255,.28);
        text-align:center;
      }
      .subtitle{
        margin:0 0 6px;
        font-size:clamp(14px,2.1vw,18px);
        color:var(--muted);
        opacity:.95;
        text-align:center;
      }

      .header-row{
        display:flex;
        gap:10px;
        justify-content:center;
        align-items:center;
        flex-wrap:wrap;
        margin-top:6px;
      }
      #clock,#weather{
        display:inline-flex;
        align-items:center;
        gap:8px;
        padding:10px 18px;
        border-radius:999px;
        font-weight:800;
        color:#0f1530;
        background:linear-gradient(135deg,#ffffff,#f2f6ff);
        box-shadow:0 8px 18px rgba(0,0,0,.25);
        margin:10px 0 8px;
        position:relative;
        overflow:hidden;
        line-height:1;
        max-width:100%;
        font-size:13px;
      }

      .modebar{
        display:flex;
        gap:10px;
        justify-content:center;
        align-items:center;
        flex-wrap:wrap;
        margin:8px 0 12px;
      }
      .chip{
        cursor:pointer;
        border:none;
        padding:8px 14px;
        border-radius:999px;
        font-weight:800;
        color:#0b112a;
        background:linear-gradient(135deg,var(--btn1),var(--btn2));
        box-shadow:0 8px 18px rgba(121,180,255,.28);
      }
      .chip.active{outline:2px solid #cfe3ff88}

      .hint{
        margin:6px 0 14px;
        color:#e9eefb;
        opacity:.85;
        font-size:13px;
        text-align:center;
      }

      .toolbar{
        display:flex;
        gap:12px;
        justify-content:space-between;
        align-items:center;
        padding:6px 6px 12px;
        flex-wrap:wrap;
        margin-top:6px;
      }
      .tabs{
        display:flex;
        gap:8px;
        flex-wrap:wrap;
      }
      .tab{
        cursor:pointer;
        border:none;
        padding:9px 14px;
        border-radius:999px;
        font-weight:800;
        color:#0b112a;
        background:linear-gradient(135deg,var(--btn1),var(--btn2));
        box-shadow:0 8px 18px rgba(121,180,255,.28);
        opacity:.95;
      }
      .tab.active{outline:2px solid #cfe3ff88;opacity:1}
      .search{
        min-width:220px;
        padding:10px 14px;
        border-radius:12px;
        border:1px solid rgba(255,255,255,.35);
        background:rgba(255,255,255,.12);
        color:#fff;
      }
      .search::placeholder{color:#e9eefbcc}

      .section-block{
        margin-top:18px;
      }
      .section-title{
        margin:0 6px 10px;
        color:#eaf2ff;
        opacity:.9;
        font-size:14px;
        letter-spacing:.6px;
      }

      .grid{
        display:grid;
        gap:16px;
        padding:0 6px;
        grid-template-columns:repeat(auto-fit, minmax(240px, 1fr));
      }

      .card{
        position:relative;
        overflow:hidden;
        border-radius:16px;
        padding:18px 16px 16px;
        background:rgba(255,255,255,.08);
        box-shadow:var(--shadow);
        outline:1px solid var(--card-stroke);
        transition:transform .15s,box-shadow .15s,outline-color .15s;
      }
      .card:hover{
        transform:translateY(-3px);
        outline-color:#cfe3ff88;
        box-shadow:0 12px 28px rgba(0,0,0,.42);
      }
      .card h3{
        margin:0 0 10px;
        font-size:clamp(18px,2.2vw,22px);
      }

      .btn{
        display:inline-block;
        text-decoration:none;
        color:#0b112a;
        font-weight:800;
        padding:10px 18px;
        border-radius:12px;
        background:linear-gradient(135deg,#e8f3ff,#e8fff7);
        box-shadow:0 8px 20px rgba(121,180,255,.32);
        transition:transform .12s ease;
      }
      .btn:hover{transform:translateY(-1px);}

      footer{
        position:static;
        margin:24px auto 14px;
        font-size:12.5px;
        color:#e7eeffcc;
        text-shadow:0 6px 22px rgba(0,0,0,.5);
        z-index:3;
        text-align:center;
        padding-inline:12px;
        box-sizing:border-box;
      }

      .hidden{display:none!important}
      .theme-day  { --bg-1:#142b40; --bg-2:#3a5e7c; --aurora-o:.18; }
      .theme-dusk { --bg-1:#1b0e2a; --bg-2:#ff9f7a; --aurora-o:.35; }
      .theme-night{ --bg-1:#070b1a; --bg-2:#0b1230; --aurora-o:.55; }

      @media (min-width: 1024px){
        .wrap{
          padding-top: 140px; /* 避免被語錄卡到 */
        }
      }
      @media (min-width: 1440px){
        .wrap{
          padding-top: 160px;
        }
        .quote-box{
          max-width: 420px;
          top: 20px;
          left: 24px;
        }
      }
    </style>
  </head>
  <body class="theme-night" id="bodyRoot">
    <div id="quoteBox" class="quote-box" aria-live="polite">
      <span class="quote-text">載入語錄中…</span>
      <span class="quote-author"></span>
    </div>

    <div class="aurora" aria-hidden="true"></div>
    <canvas id="space" aria-hidden="true"></canvas>

    <div class="wrap">
      <h1>147自測網站</h1>
      <p class="subtitle">147自主測驗平台 ✈️｜請選擇要測驗的章節：</p>

      <div class="header-row">
        <div id="clock" role="timer" aria-live="polite" aria-label="現在時間"></div>
        <div id="weather" aria-live="polite">
          <span class="wx-emoji">⏳</span><span class="wx-t">讀取中…</span>
        </div>
      </div>

      <div class="modebar" role="group" aria-label="主題">
        <button class="chip chip-theme" data-theme="theme-day" aria-pressed="false" aria-label="切換為白天">☀️ 白天</button>
        <button class="chip chip-theme" data-theme="theme-dusk" aria-pressed="false" aria-label="切換為黃昏">🌇 黃昏</button>
        <button class="chip chip-theme active" data-theme="theme-night" aria-pressed="true" aria-label="切換為夜晚">🌙 夜晚</button>
      </div>

      <p class="hint">|版權及源代碼所屬航機系008沈崑宸 | 建議使用電腦版網頁</p>

      <div class="toolbar">
        <div class="tabs" id="tabs" role="tablist" aria-label="篩選分類">
          <button class="tab active" data-filter="all" role="tab" aria-selected="true">全部</button>
          <button class="tab" data-filter="147" role="tab" aria-selected="false">147入學考</button>
          <button class="tab" data-filter="internal" role="tab" aria-selected="false">147校內考</button>
          <button class="tab" data-filter="caa" role="tab" aria-selected="false">147CAA</button>
          <button class="tab" data-filter="skill" role="tab" aria-selected="false">技藝競賽</button>
        </div>
        <label for="search" class="sr-only">搜尋</label>
        <input id="search" class="search" type="search" placeholder="搜尋：M1 / M9 / 147…" />
      </div>

      <!-- ===== 區塊：標題 + GRID 一起包起來，方便整塊隱藏 ===== -->

      <div class="section-block" data-section="147">
        <div class="section-title">147入學考</div>
        <div class="grid">
          <div class="card" data-group="147" data-keywords="147 入學考 入學 ALL">
            <h3>📘 ALL-入學考</h3>
            <a href="https://hisausage7.github.io/147/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="147" data-keywords="147 入學考 入學 M6">
            <h3>📘 M6-入學考</h3>
            <a href="https://hisausage7.github.io/147in-M6/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="147" data-keywords="147 入學考 入學 M7">
            <h3>📘 M7-入學考</h3>
            <a href="https://hisausage7.github.io/147in-M7/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="147" data-keywords="147 入學考 入學 M10">
            <h3>📘 M10-入學考</h3>
            <a href="https://hisausage7.github.io/147in/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
        </div>
      </div>

      <div class="section-block" data-section="internal">
        <div class="section-title">147校內考</div>
        <div class="grid">
          <div class="card" data-group="internal" data-keywords="M1 校內考 147M1">
            <h3>⚙️ M1-校內考</h3>
            <a href="https://hisausage7.github.io/147M1/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="internal" data-keywords="M3 校內考 147M3 建置中">
            <h3>⚙️ M3-校內考(建置中)</h3>
            <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ&list=RDdQw4w9WgXcQ&start_radio=1" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="internal" data-keywords="M6 校內考 147M6 無6.3 無6.11">
            <h3>⚙️ M6-校內考(無6.3及6.11)</h3>
            <a href="https://hisausage7.github.io/147M6/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="internal" data-keywords="M9 校內考 147M9">
            <h3>⚙️ M9-校內考</h3>
            <a href="https://hisausage7.github.io/147M9/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="internal" data-keywords="M10 校內考 147M10 建置中">
            <h3>⚙️ M10-校內考(建置中)</h3>
            <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ&list=RDdQw4w9WgXcQ&start_radio=1" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="internal" data-keywords="M15 校內考 147M15">
            <h3>⚙️ M15-校內考</h3>
            <a href="https://hisausage7.github.io/147M15/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
        </div>
      </div>

      <div class="section-block" data-section="internal">
        <div class="section-title">147期中考</div>
        <div class="grid">
          <div class="card" data-group="internal" data-keywords="M6 期中考 147M6mid">
            <h3>⚙️ M6-期中考</h3>
            <a href="https://hisausage7.github.io/147-M6mid/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
        </div>
      </div>

      <div class="section-block" data-section="caa">
        <div class="section-title">147CAA</div>
        <div class="grid">
          <div class="card" data-group="caa" data-keywords="CAA 民航 147CAA M9">
            <h3>🛩️ M9-CAA</h3>
            <a href="https://hisausage7.github.io/147CAA-M9/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
        </div>
      </div>

      <div class="section-block" data-section="skill">
        <div class="section-title">技藝競賽</div>
        <div class="grid">
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M1 1">
            <h3>🛠️ M1 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M1/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M2 2">
            <h3>🛠️ M2 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M2/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M3 3">
            <h3>🛠️ M3 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M3/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M4 4">
            <h3>🛠️ M4 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M4/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M5 5">
            <h3>🛠️ M5 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M5/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M6 6">
            <h3>🛠️ M6 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M6/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M7 7">
            <h3>🛠️ M7 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M7/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M8 8">
            <h3>🛠️ M8 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M8/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M9 9">
            <h3>🛠️ M9 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M9/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M10 10">
            <h3>🛠️ M10 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M10/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M11A 11A">
            <h3>🛠️ M11A 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M11A/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M11B 11B">
            <h3>🛠️ M11B 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M11B/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M12 12">
            <h3>🛠️ M12 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M12/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M13 13">
            <h3>🛠️ M13 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M13/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M14 14">
            <h3>🛠️ M14 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M14/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M15 15">
            <h3>🛠️ M15 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M15/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M16 16">
            <h3>🛠️ M16 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M16/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
          <div class="card" data-group="skill" data-keywords="技能 檢定 skill M17 17">
            <h3>🛠️ M17 技藝競賽</h3>
            <a href="https://hisausage7.github.io/skill-M17/" class="btn" target="_blank" rel="noopener">進入測驗</a>
          </div>
        </div>
      </div>
    </div>

    <footer>
      © 2025 航機系 008 沈崑宸 | Powered by GitHub Pages | 如果你覺得這網頁很棒可以請我喝飲料真的 | ig:kun.chen.0826
    </footer>

    <script>
      // ===== 時鐘 =====
      (function(){
        function updateClock(){
          try{
            var el=document.getElementById('clock');
            if(!el) return;
            var now=new Date();
            var days=['日','一','二','三','四','五','六'];
            var d=now.getFullYear()+'/'+('0'+(now.getMonth()+1)).slice(-2)+'/'+('0'+now.getDate()).slice(-2)+' (週'+days[now.getDay()]+')';
            var t=now.toLocaleTimeString('zh-TW',{hour12:false});
            el.textContent='📅 '+d+'　🕒 '+t;
          }catch(e){}
        }
        updateClock();
        setInterval(updateClock,1000);
      })();

      // ===== 主題切換 =====
      (function(){
        var themeButtons=document.querySelectorAll('.chip-theme');
        function setTheme(name){
          document.body.classList.remove('theme-day','theme-dusk','theme-night');
          document.body.classList.add(name);
          for(var i=0;i<themeButtons.length;i++){
            var b=themeButtons[i];
            var active=(b.getAttribute('data-theme')===name);
            if(active){
              b.classList.add('active');
              b.setAttribute('aria-pressed','true');
            } else{
              b.classList.remove('active');
              b.setAttribute('aria-pressed','false');
            }
          }
        }
        for(var i=0;i<themeButtons.length;i++){
          (function(btn){
            btn.addEventListener('click', function(){
              setTheme(btn.getAttribute('data-theme'));
            });
          })(themeButtons[i]);
        }
        setTheme('theme-night');

        var autoLite = (window.matchMedia && (window.matchMedia('(max-width: 768px)').matches || window.matchMedia('(prefers-reduced-motion: reduce)').matches));
        if(autoLite){ document.body.classList.add('lite'); }
      })();

      // ===== 天氣（臺中） =====
      (function(){
        var weatherEl=document.getElementById('weather'); if(!weatherEl) return;
        var wxEmojiEl = weatherEl.querySelector('.wx-emoji');
        var wxTextEl  = weatherEl.querySelector('.wx-t');
        function wxMap(code,isNight){
          var map={
            0:{e:'☀️',t:'晴朗'},
            1:{e:'🌤️',t:'多雲時晴'},
            2:{e:'⛅',t:'陰晴不定'},
            3:{e:'☁️',t:'多雲'},
            45:{e:'🌫️',t:'霧'},
            48:{e:'🌫️',t:'霧'},
            51:{e:'🌦️',t:'細雨'},
            53:{e:'🌦️',t:'毛毛雨'},
            55:{e:'🌧️',t:'小雨'},
            56:{e:'🌧️',t:'凍雨'},
            57:{e:'🌧️',t:'凍雨'},
            61:{e:'🌧️',t:'小雨'},
            63:{e:'🌧️',t:'中雨'},
            65:{e:'🌧️',t:'大雨'},
            66:{e:'🌧️',t:'凍雨'},
            67:{e:'🌧️',t:'凍雨'},
            71:{e:'🌨️',t:'小雪'},
            73:{e:'🌨️',t:'中雪'},
            75:{e:'❄️',t:'大雪'},
            77:{e:'🌨️',t:'霙/雪粒'},
            80:{e:'🌦️',t:'陣雨'},
            81:{e:'🌧️',t:'陣雨'},
            82:{e:'🌧️',t:'豪雨'},
            85:{e:'🌨️',t:'陣雪'},
            86:{e:'❄️',t:'大陣雪'},
            95:{e:'⛈️',t:'雷雨'},
            96:{e:'⛈️',t:'雷雨冰雹'},
            99:{e:'⛈️',t:'強雷雹'}
          };
          var item=map[code]||{e:isNight?'🌙':'☀️',t:'天氣'};
          if(isNight&&(code===0||code===1)) item.e='🌙';
          return item;
        }
        function fetchTaichung(){
          var lat=24.067337599276396, lon=120.71470802813444;
          var url='https://api.open-meteo.com/v1/forecast?latitude='+lat+'&longitude='+lon+'&current=temperature_2m,weather_code,is_day';
          fetch(url).then(function(res){
            if(!res.ok) throw new Error('network');
            return res.json();
          }).then(function(data){
            var cur=data.current||{};
            var code=(cur.weather_code!=null?cur.weather_code:0);
            var temp=Math.round(cur.temperature_2m!=null?cur.temperature_2m:0);
            var isNight=(cur.is_day===0);
            var m=wxMap(code,isNight);
            wxEmojiEl.textContent=m.e;
            wxTextEl.innerText='臺中｜'+m.t+'・'+temp+'°C';
          }).catch(function(){
            wxEmojiEl.textContent='⚠️';
            wxTextEl.innerText='天氣取得失敗';
          });
        }
        fetchTaichung();
      })();

      // ===== 篩選 + 搜尋 =====
      (function(){
        var tabs=document.getElementById('tabs');
        var sectionBlocks=(function(n){ return n?Array.prototype.slice.call(n):[]; })(document.querySelectorAll('.section-block'));
        var cards=(function(n){ return n?Array.prototype.slice.call(n):[]; })(document.querySelectorAll('.card'));
        var search=document.getElementById('search');

        function applyFilter(){
          if(!tabs) return;
          var activeEl=tabs.querySelector('.tab.active');
          var activeTab=activeEl?activeEl.getAttribute('data-filter'):'all';
          var q=(search && search.value ? search.value : '').trim().toLowerCase();

          for(var i=0;i<cards.length;i++){
            var c=cards[i];
            var group=c.getAttribute('data-group');
            var kw=(c.getAttribute('data-keywords')||'').toLowerCase();
            var byTab=(activeTab==='all')||(group===activeTab);
            var bySearch=(q==='') || kw.indexOf(q)>-1 || c.textContent.toLowerCase().indexOf(q)>-1;
            if(byTab && bySearch){
              c.classList.remove('hidden');
            } else{
              c.classList.add('hidden');
            }
          }

          for(var j=0;j<sectionBlocks.length;j++){
            var block=sectionBlocks[j];
            var cs=block.querySelectorAll('.card');
            var visible=false;
            for(var k=0;k<cs.length;k++){
              if(!cs[k].classList.contains('hidden')){
                visible=true;
                break;
              }
            }
            if(visible){
              block.classList.remove('hidden');
            } else{
              block.classList.add('hidden');
            }
          }
        }

        if(tabs){
          tabs.addEventListener('click', function(e){
            var t=e.target;
            if(!t.classList.contains('tab')) return;
            var all=tabs.querySelectorAll('.tab');
            for(var i=0;i<all.length;i++){
              all[i].classList.remove('active');
              all[i].setAttribute('aria-selected','false');
            }
            t.classList.add('active');
            t.setAttribute('aria-selected','true');
            applyFilter();
          });
        }
        if(search){ search.addEventListener('input', applyFilter); }
        applyFilter();
      })();

      // ===== 左上語錄 =====
      (function(){
        try{
          var box=document.getElementById('quoteBox'); if(!box) return;
          var QUOTES=[
            {t:'把難的事情分解，把簡單的事情做到極致。',a:'工科小訣竅'},
            {t:'今天的每一步，都是明天的底氣。',a:'日常自勉'},
            {t:'先求正確，再求快速。',a:'系統工程'},
            {t:'你所浪費的今天，是別人無比渴望的明天。',a:'箴言'},
            {t:'資料先乾淨，結果才可信。',a:'實驗室守則'},
            {t:'遇到BUG先別急，觀察、重現、再下手。',a:'除錯心法'},
            {t:'把複雜留給自己，把簡單留給使用者。',a:'產品思維'},
            {t:'不怕走得慢，只怕停下來。',a:'行動力'},
            {t:'一分耕耘，一分收穫；多一分復盤，多兩分進步。',a:'學習論'},
            {t:'清楚的目標，比盲目的努力更重要。',a:'聚焦'},
            {t:'先完成，再完美；先可用，再好用。',a:'工程實務'},
            {t:'求知若渴，虛心若愚。',a:'致敬'}
          ];
          var last=parseInt(localStorage.getItem('lastQuote')||'-1',10);
          var idx=Math.floor(Math.random()*QUOTES.length);
          if(QUOTES.length>1 && idx===last){
            idx=(idx+1)%QUOTES.length;
          }
          localStorage.setItem('lastQuote', String(idx));
          var q=QUOTES[idx];
          var qt=box.querySelector('.quote-text');
          var qa=box.querySelector('.quote-author');
          if(qt) qt.textContent='“'+q.t+'”';
          if(qa) qa.textContent='— '+q.a;
        }catch(e){}
      })();
    </script>

    <!-- 星星 + Ripple -->
    <script>
      (function(){
        var canvas=document.getElementById('space');
        var ctx = canvas && canvas.getContext ? canvas.getContext('2d') : null;
        var w=0,h=0, stars=[]; var running=false; var timer=null;

        function density(){
          var lite = document.body.classList.contains('lite');
          var area = (w*h)/1e5;
          var base = lite ? 2.2 : 4.5;
          return Math.max(120, Math.min(1600, (area*base)|0));
        }
        function resize(){
          if(!canvas||!ctx) return;
          w=canvas.width=window.innerWidth||800;
          h=canvas.height=window.innerHeight||600;
          init();
        }
        function init(){
          stars.length=0;
          var n=density();
          for(var i=0;i<n;i++){
            stars.push({
              x:Math.random()*w,
              y:Math.random()*h,
              r:Math.random()*1.5+0.2,
              a:0.35+Math.random()*0.5,
              v:(Math.random()*0.02+0.005)
            });
          }
          draw();
        }
        function draw(){
          if(!ctx) return;
          ctx.clearRect(0,0,w,h);
          for(var i=0;i<stars.length;i++){
            var s=stars[i];
            s.a += (Math.random()-0.5)*s.v;
            if(s.a<0.2) s.a=0.2;
            if(s.a>0.95) s.a=0.95;
            ctx.globalAlpha=s.a;
            ctx.fillStyle='#fff';
            ctx.beginPath();
            ctx.arc(s.x,s.y,s.r,0,Math.PI*2);
            ctx.fill();
          }
          ctx.globalAlpha=1;
        }
        function start(){
          if(timer) return;
          running=true;
          timer = setInterval(function(){
            if(!running) return;
            draw();
          }, 1000/24);
        }
        function stop(){
          running=false;
          if(timer){
            clearInterval(timer);
            timer=null;
          }
        }

        window.addEventListener('resize', resize, {passive:true});
        document.addEventListener('visibilitychange', function(){
          if(document.hidden) stop();
          else{
            draw();
            start();
          }
        });
        var prefersReduce = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
        resize();
        if(!prefersReduce){ start(); }
      })();

      (function(){
        function attachRipple(el){
          if(!el) return;
          el.addEventListener('click', function(e){
            var rect=el.getBoundingClientRect();
            var d=Math.max(rect.width, rect.height);
            var x=e.clientX-rect.left-d/2;
            var y=e.clientY-rect.top-d/2;
            var ink=document.createElement('span');
            ink.style.cssText='position:absolute;border-radius:50%;transform:scale(0);opacity:.65;background:rgba(255,255,255,.7);pointer-events:none;left:'+x+'px;top:'+y+'px;width:'+d+'px;height:'+d+'px;transition:transform .55s ease, opacity .55s ease';
            el.style.position='relative';
            el.style.overflow='hidden';
            el.appendChild(ink);
            requestAnimationFrame(function(){
              ink.style.transform='scale(1)';
              ink.style.opacity='0';
            });
            setTimeout(function(){
              if(ink.parentNode) ink.parentNode.removeChild(ink);
            }, 600);
          }, {passive:true});
        }
        var btns=document.querySelectorAll('.btn, .card');
        for(var i=0;i<btns.length;i++){ attachRipple(btns[i]); }

        document.addEventListener('click', function(e){
          if(e.target.closest('.btn,.card')) return;
          var n = (document.body.classList.contains('lite')? 6:10);
          for(var i=0;i<n;i++){
            var d=document.createElement('div');
            var size=6+Math.random()*4;
            d.style.cssText='position:fixed;left:'+e.clientX+'px;top:'+e.clientY+'px;width:'+size+'px;height:'+size+'px;border-radius:50%;background:rgba(255,255,255,.9);filter:blur(1px);pointer-events:none;transition:transform .7s ease, opacity .7s ease;opacity:1;';
            document.body.appendChild(d);
            (function(el){
              var ang=Math.random()*6.283;
              var dist=30+Math.random()*70;
              var dx=Math.cos(ang)*dist;
              var dy=Math.sin(ang)*dist;
              requestAnimationFrame(function(){
                el.style.transform='translate('+dx+'px,'+dy+'px) scale(.9)';
                el.style.opacity='0';
              });
              setTimeout(function(){
                if(el.parentNode) el.parentNode.removeChild(el);
              }, 720);
            })(d);
          }
        }, {passive:true});
      })();
    </script>
  </body>
</html>

