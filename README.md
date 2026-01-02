<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>147自測網站入口</title>
  <link rel="icon" type="image/jpeg" href="OIP.jpg" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@500;600;700&display=swap" rel="stylesheet" />

  <style>
    :root{
      --bg0:#060915;
      --bg1:#0a1330;
      --bg2:#081027;
      --card: rgba(255,255,255,.06);
      --card2: rgba(255,255,255,.08);
      --stroke: rgba(255,255,255,.14);
      --txt:#eaf1ff;
      --muted:#cfe0ffcc;
      --muted2:#cfe0ff88;
      --accent:#8dd7ff;
      --accent2:#b6b2ff;
      --ok:#a7ffd9;
      --warn:#ffd49a;

      --radius:18px;
      --shadow: 0 14px 34px rgba(0,0,0,.38);
      --shadow2: 0 10px 24px rgba(0,0,0,.30);

      --sidebarW: 280px;
      --gap: 14px;
    }

    *{ box-sizing:border-box; }
    html,body{ height:100%; }
    body{
      margin:0;
      color:var(--txt);
      font-family:"Microsoft JhengHei", system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      background:
        radial-gradient(1200px 700px at 18% 0%, rgba(141,215,255,.12), transparent 60%),
        radial-gradient(1000px 700px at 110% 18%, rgba(182,178,255,.14), transparent 60%),
        linear-gradient(145deg, var(--bg0) 0%, var(--bg1) 55%, var(--bg2) 100%);
      overflow-x:hidden;
    }

    /* 星星 */
    canvas#space{
      position:fixed;
      inset:0;
      z-index:0;
      pointer-events:none;
      opacity:.9;
    }

    /* 版面容器 */
    .app{
      position:relative;
      z-index:2;
      max-width: 1800px;
      margin: 0 auto;
      padding: 18px;
      display:grid;
      grid-template-columns: var(--sidebarW) 1fr;
      gap: var(--gap);
      min-height:100vh;
    }

    /* 玻璃卡感（不做 heavy blur，省電） */
    .panel{
      background: linear-gradient(180deg, rgba(255,255,255,.08), rgba(255,255,255,.04));
      border: 1px solid var(--stroke);
      border-radius: var(--radius);
      box-shadow: var(--shadow2);
      overflow:hidden;
    }

    /* Sidebar */
    .side{
      position: sticky;
      top: 18px;
      align-self:start;
      padding: 14px;
    }
    .brand{
      display:flex;
      gap:10px;
      align-items:center;
      padding: 10px 10px 12px;
      border-radius: 16px;
      background: rgba(255,255,255,.06);
      border: 1px solid rgba(255,255,255,.12);
    }
    .logo{
      width:42px;height:42px;
      border-radius:14px;
      background:
        radial-gradient(18px 18px at 30% 30%, rgba(255,255,255,.35), transparent 65%),
        linear-gradient(135deg, rgba(141,215,255,.45), rgba(182,178,255,.38));
      box-shadow: 0 10px 22px rgba(0,0,0,.35);
      flex:0 0 auto;
    }
    .brand h1{
      margin:0;
      font-size:16px;
      letter-spacing:.6px;
      font-family:"Noto Serif TC","Microsoft JhengHei",serif;
    }
    .brand .sub{
      margin-top:2px;
      font-size:12px;
      color:var(--muted);
      opacity:.95;
    }

    .metaRow{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      margin: 12px 0 10px;
    }
    .pill{
      display:inline-flex;
      align-items:center;
      gap:8px;
      padding: 10px 12px;
      border-radius: 999px;
      background: rgba(255,255,255,.06);
      border: 1px solid rgba(255,255,255,.12);
      box-shadow: 0 8px 18px rgba(0,0,0,.28);
      font-weight:800;
      font-size:12px;
      color: var(--txt);
      max-width:100%;
      line-height:1;
    }
    .pill .mut{ color:var(--muted); font-weight:700; }

    .searchBox{
      margin: 10px 0 12px;
      padding: 10px;
      border-radius: 16px;
      background: rgba(255,255,255,.06);
      border: 1px solid rgba(255,255,255,.12);
    }
    .searchBox label{
      display:block;
      font-size:12px;
      color:var(--muted);
      margin: 0 0 8px;
      font-weight:800;
      letter-spacing:.4px;
    }
    .searchBox input{
      width:100%;
      padding: 12px 12px;
      border-radius: 14px;
      border: 1px solid rgba(255,255,255,.18);
      background: rgba(10,16,40,.35);
      color:#fff;
      outline:none;
      font-size:14px;
    }
    .searchBox input::placeholder{ color: rgba(233,238,251,.75); }

    .filters{
      display:grid;
      gap:10px;
      margin-top: 10px;
    }
    .filterTitle{
      font-size:12px;
      color:var(--muted);
      font-weight:900;
      letter-spacing:.4px;
      padding: 0 4px;
    }
    .chips{
      display:flex;
      flex-wrap:wrap;
      gap:8px;
    }
    .chip{
      cursor:pointer;
      user-select:none;
      border:none;
      padding: 9px 12px;
      border-radius: 999px;
      font-weight:900;
      font-size:12.5px;
      color:#0b112a;
      background: linear-gradient(135deg, rgba(232,243,255,1), rgba(232,255,247,1));
      box-shadow: 0 10px 20px rgba(121,180,255,.20);
      opacity:.92;
      transition: transform .12s ease, opacity .12s ease;
    }
    .chip:hover{ transform: translateY(-1px); opacity:1; }
    .chip.active{
      outline: 2px solid rgba(207,227,255,.55);
      opacity:1;
    }

    .sideNote{
      margin-top: 12px;
      padding: 12px 12px;
      border-radius: 16px;
      background: rgba(255,255,255,.05);
      border: 1px dashed rgba(255,255,255,.16);
      color: var(--muted);
      font-size: 12.5px;
      line-height: 1.55;
    }
    .kbd{
      display:inline-block;
      padding: 1px 7px;
      border-radius: 8px;
      border: 1px solid rgba(255,255,255,.18);
      background: rgba(255,255,255,.06);
      color: var(--txt);
      font-weight:900;
      font-size: 11px;
      margin: 0 2px;
    }

    /* Main */
    .main{
      padding: 14px;
    }

    .topBar{
      display:flex;
      align-items:flex-end;
      justify-content:space-between;
      gap:12px;
      flex-wrap:wrap;
      padding: 8px 8px 10px;
    }
    .titleWrap h2{
      margin:0;
      font-size: 22px;
      letter-spacing:.6px;
      font-family:"Noto Serif TC","Microsoft JhengHei",serif;
      background: linear-gradient(120deg, #eaf4ff, #b3c6ff 40%, #d7fcef 70%, #e9dcff 100%);
      -webkit-background-clip:text;
      color:transparent;
      text-shadow: 0 10px 28px rgba(130,177,255,.22);
    }
    .titleWrap p{
      margin:6px 0 0;
      color: var(--muted);
      font-size: 13px;
      font-weight:700;
    }

    .statRow{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      justify-content:flex-end;
      align-items:center;
    }
    .stat{
      padding: 9px 12px;
      border-radius: 999px;
      background: rgba(255,255,255,.06);
      border: 1px solid rgba(255,255,255,.12);
      box-shadow: 0 10px 22px rgba(0,0,0,.26);
      font-weight:900;
      font-size:12px;
      color: var(--txt);
    }
    .stat b{ color:#fff; }
    .stat .mini{ color: var(--muted); font-weight:800; margin-left:6px; }

    .sections{
      display:grid;
      gap: 14px;
      padding: 6px;
    }

    .section{
      border-radius: var(--radius);
      background: rgba(255,255,255,.05);
      border: 1px solid rgba(255,255,255,.12);
      overflow:hidden;
      box-shadow: var(--shadow2);
    }
    .sectionHead{
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:10px;
      padding: 12px 14px;
      background: linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      border-bottom: 1px solid rgba(255,255,255,.10);
    }
    .sectionHead .name{
      font-weight:1000;
      letter-spacing:.6px;
      color:#fff;
      font-size: 13px;
      opacity:.95;
    }
    .sectionHead .count{
      font-weight:1000;
      color: var(--muted);
      font-size: 12px;
    }

    .grid{
      display:grid;
      gap: 12px;
      padding: 12px;
      grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    }

    .item{
      position:relative;
      border-radius: 16px;
      background: rgba(255,255,255,.06);
      border: 1px solid rgba(255,255,255,.12);
      box-shadow: 0 12px 26px rgba(0,0,0,.28);
      overflow:hidden;
      transition: transform .14s ease, border-color .14s ease, box-shadow .14s ease;
      min-height: 86px;
    }
    .item:hover{
      transform: translateY(-2px);
      border-color: rgba(207,227,255,.35);
      box-shadow: 0 16px 34px rgba(0,0,0,.38);
    }

    .itemInner{
      padding: 14px 14px 12px;
      display:flex;
      gap:12px;
      align-items:flex-start;
      justify-content:space-between;
    }

    .itemTitle{
      margin:0;
      font-size: 16px;
      letter-spacing:.2px;
      font-weight:900;
      line-height:1.25;
    }
    .itemMeta{
      margin-top: 7px;
      font-size: 12px;
      color: var(--muted);
      font-weight:800;
      display:flex;
      gap:8px;
      flex-wrap:wrap;
      opacity:.95;
    }
    .tag{
      display:inline-flex;
      gap:6px;
      align-items:center;
      padding: 4px 9px;
      border-radius: 999px;
      background: rgba(255,255,255,.06);
      border: 1px solid rgba(255,255,255,.10);
      color: var(--muted);
      font-weight:900;
      font-size: 11px;
    }

    .actions{
      display:flex;
      flex-direction:column;
      gap:8px;
      align-items:flex-end;
      flex:0 0 auto;
      margin-left: 10px;
    }
    .go{
      display:inline-flex;
      align-items:center;
      gap:8px;
      text-decoration:none;
      color:#0b112a;
      font-weight:1000;
      font-size: 12.5px;
      padding: 9px 12px;
      border-radius: 12px;
      background: linear-gradient(135deg, rgba(232,243,255,1), rgba(232,255,247,1));
      box-shadow: 0 10px 22px rgba(121,180,255,.22);
      transition: transform .12s ease;
      white-space:nowrap;
    }
    .go:hover{ transform: translateY(-1px); }
    .fav{
      cursor:pointer;
      user-select:none;
      border:none;
      padding: 7px 10px;
      border-radius: 12px;
      background: rgba(255,255,255,.06);
      border: 1px solid rgba(255,255,255,.12);
      color: var(--txt);
      font-weight:1000;
      font-size: 12px;
    }
    .fav.on{
      border-color: rgba(141,215,255,.45);
      box-shadow: 0 10px 22px rgba(141,215,255,.12);
    }

    .empty{
      padding: 18px;
      border-radius: 16px;
      background: rgba(255,255,255,.05);
      border: 1px dashed rgba(255,255,255,.16);
      color: var(--muted);
      font-weight:800;
      text-align:center;
      margin: 10px;
    }

    footer{
      grid-column: 1 / -1;
      text-align:center;
      color: rgba(231,238,255,.78);
      font-size: 12.5px;
      padding: 14px 8px 22px;
      text-shadow: 0 10px 26px rgba(0,0,0,.45);
    }

    /* 手機：sidebar 變成上方區塊 */
    @media (max-width: 960px){
      .app{
        grid-template-columns: 1fr;
      }
      .side{
        position:relative;
        top:auto;
      }
    }

    /* 減少動態 */
    @media (prefers-reduced-motion: reduce){
      .item, .chip, .go{ transition:none; }
      canvas#space{ display:none; }
    }
  </style>
</head>

<body>
  <canvas id="space" aria-hidden="true"></canvas>

  <div class="app">
    <!-- Sidebar -->
    <aside class="panel side" aria-label="側欄">
      <div class="brand">
        <div class="logo" aria-hidden="true"></div>
        <div>
          <h1>147自測網站入口</h1>
          <div class="sub">分流站｜保留原網址與名稱</div>
        </div>
      </div>

      <div class="metaRow" aria-label="資訊">
        <div class="pill" id="clockPill">🕒 <span class="mut">載入中…</span></div>
        <div class="pill" id="weatherPill">⏳ <span class="mut">天氣讀取中…</span></div>
      </div>

      <div class="searchBox">
        <label for="q">搜尋（按 <span class="kbd">/</span> 直接輸入）</label>
        <input id="q" type="search" placeholder="搜尋：M1 / M9 / 147 / CAA / 技藝…" autocomplete="off" />
      </div>

      <div class="filters">
        <div class="filterTitle">分類篩選</div>
        <div class="chips" id="chips">
          <!-- JS 注入 -->
        </div>
      </div>

      <div class="sideNote">
        <div style="font-weight:1000; color:#fff; margin-bottom:6px;">快捷鍵</div>
        <div>• <span class="kbd">/</span> 聚焦搜尋　• <span class="kbd">Esc</span> 清空搜尋</div>
        <div style="margin-top:8px; color:var(--muted2);">
          提示：可用「收藏」固定常用測驗；最近開啟會自動記錄。
        </div>
      </div>
    </aside>

    <!-- Main -->
    <main class="panel main" aria-label="內容">
      <div class="topBar">
        <div class="titleWrap">
          <h2>147自測網站</h2>
          <p>147自主測驗平台 ✈️｜請在左側搜尋或點分類。</p>
        </div>
        <div class="statRow" aria-label="統計">
          <div class="stat" id="statTotal">總數 <b>0</b><span class="mini">項</span></div>
          <div class="stat" id="statShown">顯示 <b>0</b><span class="mini">項</span></div>
          <div class="stat" id="statFav">收藏 <b>0</b><span class="mini">項</span></div>
        </div>
      </div>

      <div class="sections" id="sections">
        <!-- JS 注入 -->
      </div>

      <div class="empty" id="empty" style="display:none;">
        找不到符合的項目（試試看縮短關鍵字或切回「全部」）
      </div>
    </main>

    <footer>
      © 2025 航機系 008 沈崑宸 | Powered by GitHub Pages | 如果你覺得這網頁很棒可以請我喝飲料真的 | ig:kun.chen.0826
    </footer>
  </div>

  <script>
    /* =========================
       1) 你的「名稱 + 網址」完全保留
       ========================= */
    var DATA = [
      // 147入學考
      {section:'147', group:'147入學考', title:'📘 ALL-入學考', url:'https://hisausage7.github.io/147/', keywords:'147 入學考 入學 ALL'},
      {section:'147', group:'147入學考', title:'📘 M6-入學考', url:'https://hisausage7.github.io/147in-M6/', keywords:'147 入學考 入學 M6'},
      {section:'147', group:'147入學考', title:'📘 M7-入學考', url:'https://hisausage7.github.io/147in-M7/', keywords:'147 入學考 入學 M7'},
      {section:'147', group:'147入學考', title:'📘 M10-入學考', url:'https://hisausage7.github.io/147in/', keywords:'147 入學考 入學 M10'},

      // 147校內考
      {section:'internal', group:'147校內考', title:'⚙️ M1-校內考', url:'https://hisausage7.github.io/147M1/', keywords:'M1 校內考 147M1'},
      {section:'internal', group:'147校內考', title:'⚙️ M3-校內考(建置中)', url:'https://www.youtube.com/watch?v=dQw4w9WgXcQ&list=RDdQw4w9WgXcQ&start_radio=1', keywords:'M3 校內考 147M3 建置中'},
      {section:'internal', group:'147校內考', title:'⚙️ M6-校內考(無6.3及6.11)', url:'https://hisausage7.github.io/147M6/', keywords:'M6 校內考 147M6 無6.3 無6.11'},
      {section:'internal', group:'147校內考', title:'⚙️ M9-校內考', url:'https://hisausage7.github.io/147M9/', keywords:'M9 校內考 147M9'},
      {section:'internal', group:'147校內考', title:'⚙️ M10-校內考(建置中)', url:'https://www.youtube.com/watch?v=dQw4w9WgXcQ&list=RDdQw4w9WgXcQ&start_radio=1', keywords:'M10 校內考 147M10 建置中'},
      {section:'internal', group:'147校內考', title:'⚙️ M15-校內考', url:'https://hisausage7.github.io/147M15/', keywords:'M15 校內考 147M15'},

      // 147期中/末考（你原本 data-section 也是 internal，我照樣分一群）
      {section:'internal', group:'147期中/末考', title:'⚙️ M6-期末考', url:'https://hisausage7.github.io/147-M6mid/', keywords:'M6 期中考 147M6mid'},
      {section:'internal', group:'147期中/末考', title:'⚙️ M15-期末考', url:'https://hisausage7.github.io/M15-mid/', keywords:'M15 期末考 M15-mid'},

      // 147CAA
      {section:'caa', group:'147CAA', title:'🛩️ M1-CAA', url:'https://hisausage7.github.io/147CAA-M1/', keywords:'CAA 民航 147CAA M1'},
      {section:'caa', group:'147CAA', title:'🛩️ M9-CAA', url:'https://hisausage7.github.io/147CAA-M9/', keywords:'CAA 民航 147CAA M9'},

      // 技藝競賽
      {section:'skill', group:'技藝競賽', title:'🛠️ M1 技藝競賽', url:'https://hisausage7.github.io/skill-M1/', keywords:'技能 檢定 skill M1 1'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M2 技藝競賽', url:'https://hisausage7.github.io/skill-M2/', keywords:'技能 檢定 skill M2 2'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M3 技藝競賽', url:'https://hisausage7.github.io/skill-M3/', keywords:'技能 檢定 skill M3 3'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M4 技藝競賽', url:'https://hisausage7.github.io/skill-M4/', keywords:'技能 檢定 skill M4 4'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M5 技藝競賽', url:'https://hisausage7.github.io/skill-M5/', keywords:'技能 檢定 skill M5 5'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M6 技藝競賽', url:'https://hisausage7.github.io/skill-M6/', keywords:'技能 檢定 skill M6 6'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M7 技藝競賽', url:'https://hisausage7.github.io/skill-M7/', keywords:'技能 檢定 skill M7 7'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M8 技藝競賽', url:'https://hisausage7.github.io/skill-M8/', keywords:'技能 檢定 skill M8 8'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M9 技藝競賽', url:'https://hisausage7.github.io/skill-M9/', keywords:'技能 檢定 skill M9 9'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M10 技藝競賽', url:'https://hisausage7.github.io/skill-M10/', keywords:'技能 檢定 skill M10 10'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M11A 技藝競賽', url:'https://hisausage7.github.io/skill-M11A/', keywords:'技能 檢定 skill M11A 11A'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M11B 技藝競賽', url:'https://hisausage7.github.io/skill-M11B/', keywords:'技能 檢定 skill M11B 11B'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M12 技藝競賽', url:'https://hisausage7.github.io/skill-M12/', keywords:'技能 檢定 skill M12 12'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M13 技藝競賽', url:'https://hisausage7.github.io/skill-M13/', keywords:'技能 檢定 skill M13 13'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M14 技藝競賽', url:'https://hisausage7.github.io/skill-M14/', keywords:'技能 檢定 skill M14 14'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M15 技藝競賽', url:'https://hisausage7.github.io/skill-M15/', keywords:'技能 檢定 skill M15 15'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M16 技藝競賽', url:'https://hisausage7.github.io/skill-M16/', keywords:'技能 檢定 skill M16 16'},
      {section:'skill', group:'技藝競賽', title:'🛠️ M17 技藝競賽', url:'https://hisausage7.github.io/skill-M17/', keywords:'技能 檢定 skill M17 17'}
    ];

    /* =========================
       2) 狀態：篩選 / 收藏 / 最近
       ========================= */
    var FILTERS = [
      {id:'all',  label:'全部'},
      {id:'147',  label:'147入學考'},
      {id:'internal', label:'147校內相關'},
      {id:'caa',  label:'147CAA'},
      {id:'skill',label:'技藝競賽'},
      {id:'fav',  label:'收藏'}
    ];

    var LS_FAV = 'portal_favs_v1';
    var LS_REC = 'portal_recent_v1';

    function loadJSON(key, fallback){
      try{
        var raw = localStorage.getItem(key);
        if(!raw) return fallback;
        var obj = JSON.parse(raw);
        return obj || fallback;
      }catch(e){
        return fallback;
      }
    }
    function saveJSON(key, obj){
      try{ localStorage.setItem(key, JSON.stringify(obj)); }catch(e){}
    }

    var favs = loadJSON(LS_FAV, {});   // {url:true}
    var recent = loadJSON(LS_REC, []); // [{url,title,ts}]

    var state = {
      activeFilter: 'all',
      query: ''
    };

    /* =========================
       3) UI 建立
       ========================= */
    var $chips = document.getElementById('chips');
    var $sections = document.getElementById('sections');
    var $q = document.getElementById('q');
    var $empty = document.getElementById('empty');
    var $statTotal = document.getElementById('statTotal');
    var $statShown = document.getElementById('statShown');
    var $statFav = document.getElementById('statFav');

    function el(tag, cls){
      var n = document.createElement(tag);
      if(cls) n.className = cls;
      return n;
    }

    function buildChips(){
      $chips.innerHTML = '';
      for(var i=0;i<FILTERS.length;i++){
        (function(f){
          var b = el('button','chip');
          b.type = 'button';
          b.setAttribute('data-id', f.id);
          b.textContent = f.label;
          if(f.id === state.activeFilter) b.classList.add('active');
          b.addEventListener('click', function(){
            state.activeFilter = f.id;
            buildChips();
            render();
          });
          $chips.appendChild(b);
        })(FILTERS[i]);
      }
    }

    function groupBy(arr, keyFn){
      var map = {};
      for(var i=0;i<arr.length;i++){
        var k = keyFn(arr[i]);
        if(!map[k]) map[k]=[];
        map[k].push(arr[i]);
      }
      return map;
    }

    function isFav(item){
      return !!favs[item.url];
    }

    function addRecent(item){
      try{
        var now = Date.now();
        // 先移除同 url
        var next = [];
        for(var i=0;i<recent.length;i++){
          if(recent[i] && recent[i].url !== item.url) next.push(recent[i]);
        }
        next.unshift({url:item.url, title:item.title, ts: now});
        // 保留前 8
        if(next.length > 8) next = next.slice(0,8);
        recent = next;
        saveJSON(LS_REC, recent);
      }catch(e){}
    }

    function matchItem(item){
      // filter
      if(state.activeFilter === 'fav'){
        if(!isFav(item)) return false;
      }else if(state.activeFilter !== 'all'){
        if(item.section !== state.activeFilter) return false;
      }
      // search
      var q = (state.query||'').toLowerCase().trim();
      if(!q) return true;
      var hay = (item.title + ' ' + item.keywords + ' ' + item.group).toLowerCase();
      return hay.indexOf(q) > -1;
    }

    function renderItem(item){
      var box = el('div','item');
      var inner = el('div','itemInner');

      var left = el('div');
      var h = el('h3','itemTitle');
      h.textContent = item.title;

      var meta = el('div','itemMeta');
      // 顯示兩個 tag：群組 / section
      var t1 = el('span','tag'); t1.textContent = item.group;
      var t2 = el('span','tag');
      t2.textContent = (item.section==='147'?'147入學考': item.section==='internal'?'校內/期中末': item.section==='caa'?'CAA':'技藝競賽');
      meta.appendChild(t1);
      meta.appendChild(t2);

      left.appendChild(h);
      left.appendChild(meta);

      var acts = el('div','actions');

      var a = el('a','go');
      a.href = item.url;
      a.target = '_blank';
      a.rel = 'noopener';
      a.textContent = '進入測驗 ↗';
      a.addEventListener('click', function(){
        addRecent(item);
        // 小 ripple 點綴（超輕量）
        try{
          var r = el('div');
          r.style.cssText =
            'position:absolute;inset:auto;left:12px;bottom:10px;width:8px;height:8px;border-radius:50%;' +
            'background:rgba(255,255,255,.9);filter:blur(1px);opacity:.9;pointer-events:none;transition:transform .55s ease, opacity .55s ease;';
          box.appendChild(r);
          setTimeout(function(){ r.style.transform='translateX(18px) scale(1.6)'; r.style.opacity='0'; }, 10);
          setTimeout(function(){ if(r && r.parentNode) r.parentNode.removeChild(r); }, 600);
        }catch(e){}
        // 讓新分頁開啟，不阻擋
      });

      var f = el('button','fav');
      f.type = 'button';
      function syncFavBtn(){
        var on = isFav(item);
        if(on){
          f.classList.add('on');
          f.textContent = '★ 已收藏';
        }else{
          f.classList.remove('on');
          f.textContent = '☆ 收藏';
        }
      }
      syncFavBtn();
      f.addEventListener('click', function(e){
        e.preventDefault();
        e.stopPropagation();
        if(isFav(item)) delete favs[item.url];
        else favs[item.url] = true;
        saveJSON(LS_FAV, favs);
        syncFavBtn();
        renderStats(); // 更新統計
        // 若目前在「收藏」濾鏡，按下後要即時刷新
        if(state.activeFilter === 'fav') render();
      });

      acts.appendChild(a);
      acts.appendChild(f);

      inner.appendChild(left);
      inner.appendChild(acts);
      box.appendChild(inner);
      return box;
    }

    function renderStats(){
      var total = DATA.length;
      var favCount = 0;
      for(var k in favs){ if(favs.hasOwnProperty(k) && favs[k]) favCount++; }
      var shown = 0;
      for(var i=0;i<DATA.length;i++){ if(matchItem(DATA[i])) shown++; }

      $statTotal.innerHTML = '總數 <b>'+ total +'</b><span class="mini">項</span>';
      $statShown.innerHTML = '顯示 <b>'+ shown +'</b><span class="mini">項</span>';
      $statFav.innerHTML = '收藏 <b>'+ favCount +'</b><span class="mini">項</span>';
    }

    function render(){
      $sections.innerHTML = '';
      $empty.style.display = 'none';

      // 先做兩個特殊區：收藏 / 最近
      var list = [];
      for(var i=0;i<DATA.length;i++){
        if(matchItem(DATA[i])) list.push(DATA[i]);
      }

      renderStats();

      // 如果有搜尋/篩選，仍然可以顯示「最近」但只在 all/fav? 這邊：all 時才顯示
      if(state.activeFilter === 'all' && (state.query||'').trim()===''){
        // 收藏區（有才顯示）
        var favItems = [];
        for(var i=0;i<DATA.length;i++){
          if(isFav(DATA[i])) favItems.push(DATA[i]);
        }
        if(favItems.length){
          $sections.appendChild(renderSection('★ 收藏', favItems));
        }

        // 最近區
        var recItems = [];
        for(var r=0;r<recent.length;r++){
          var ru = recent[r] && recent[r].url;
          if(!ru) continue;
          for(var j=0;j<DATA.length;j++){
            if(DATA[j].url === ru){
              recItems.push(DATA[j]);
              break;
            }
          }
        }
        if(recItems.length){
          $sections.appendChild(renderSection('⏱️ 最近開啟', recItems));
        }
      }

      // 依 group 分段
      var grouped = groupBy(list, function(it){ return it.group; });
      var order = ['147入學考','147校內考','147期中/末考','147CAA','技藝競賽'];

      var appended = 0;
      for(var o=0;o<order.length;o++){
        var name = order[o];
        if(grouped[name] && grouped[name].length){
          $sections.appendChild(renderSection(name, grouped[name]));
          appended += grouped[name].length;
        }
      }

      // 其他未列入 order 的 group
      for(var g in grouped){
        if(!grouped.hasOwnProperty(g)) continue;
        var found = false;
        for(var o2=0;o2<order.length;o2++){ if(order[o2]===g){ found=true; break; } }
        if(found) continue;
        if(grouped[g] && grouped[g].length){
          $sections.appendChild(renderSection(g, grouped[g]));
          appended += grouped[g].length;
        }
      }

      if(appended === 0){
        $empty.style.display = 'block';
      }
    }

    function renderSection(title, items){
      var wrap = el('section','section');

      var head = el('div','sectionHead');
      var nm = el('div','name'); nm.textContent = title;
      var ct = el('div','count'); ct.textContent = items.length + ' 項';
      head.appendChild(nm);
      head.appendChild(ct);

      var grid = el('div','grid');
      for(var i=0;i<items.length;i++){
        grid.appendChild(renderItem(items[i]));
      }

      wrap.appendChild(head);
      wrap.appendChild(grid);
      return wrap;
    }

    /* =========================
       4) 事件綁定
       ========================= */
    buildChips();

    $q.addEventListener('input', function(){
      state.query = $q.value || '';
      render();
    });

    document.addEventListener('keydown', function(e){
      // '/' 聚焦搜尋（避免在 input 裡再觸發）
      if(e.key === '/' && document.activeElement !== $q){
        e.preventDefault();
        $q.focus();
        return;
      }
      // ESC 清空
      if(e.key === 'Escape'){
        if(document.activeElement === $q){
          $q.value = '';
          state.query = '';
          $q.blur();
          render();
        }else{
          // 不是在 input，也清空一次搜尋
          if(($q.value||'')!==''){
            $q.value='';
            state.query='';
            render();
          }
        }
      }
    });

    /* =========================
       5) 時鐘 / 天氣（臺中）
       ========================= */
    (function(){
      var el = document.getElementById('clockPill');
      function pad(n){ return (n<10?'0':'')+n; }
      function tick(){
        try{
          var d = new Date();
          var days = ['日','一','二','三','四','五','六'];
          var s = d.getFullYear()+'/'+pad(d.getMonth()+1)+'/'+pad(d.getDate())+' (週'+days[d.getDay()]+') '+pad(d.getHours())+':'+pad(d.getMinutes())+':'+pad(d.getSeconds());
          el.innerHTML = '🕒 <span class="mut">'+ s +'</span>';
        }catch(e){}
      }
      tick();
      setInterval(tick, 1000);
    })();

    (function(){
      var pill = document.getElementById('weatherPill');
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
        var item = map[code] || {e:(isNight?'🌙':'☀️'), t:'天氣'};
        if(isNight && (code===0 || code===1)) item.e='🌙';
        return item;
      }
      function fetchTaichung(){
        // 台中座標（你原本這組）
        var lat = 24.067337599276396;
        var lon = 120.71470802813444;
        var url = 'https://api.open-meteo.com/v1/forecast?latitude='+lat+'&longitude='+lon+'&current=temperature_2m,weather_code,is_day';
        fetch(url).then(function(res){
          if(!res.ok) throw new Error('network');
          return res.json();
        }).then(function(data){
          var cur = data.current || {};
          var code = (cur.weather_code!=null?cur.weather_code:0);
          var temp = Math.round(cur.temperature_2m!=null?cur.temperature_2m:0);
          var isNight = (cur.is_day===0);
          var m = wxMap(code, isNight);
          pill.innerHTML = m.e + ' <span class="mut">臺中｜'+ m.t +'・'+ temp +'°C</span>';
        }).catch(function(){
          pill.innerHTML = '⚠️ <span class="mut">天氣取得失敗</span>';
        });
      }
      fetchTaichung();
    })();

    /* =========================
       6) 星星（更省電：低頻刷新）
       ========================= */
    (function(){
      var canvas = document.getElementById('space');
      var ctx = canvas && canvas.getContext ? canvas.getContext('2d') : null;
      if(!canvas || !ctx) return;

      var w=0,h=0,stars=[];
      var timer=null;

      function resize(){
        w = canvas.width = window.innerWidth || 800;
        h = canvas.height = window.innerHeight || 600;
        initStars();
        draw();
      }

      function starCount(){
        var area = (w*h)/1e5;
        var n = Math.floor(area * 3.3);
        if(n < 180) n = 180;
        if(n > 1200) n = 1200;
        return n;
      }

      function initStars(){
        stars.length = 0;
        var n = starCount();
        for(var i=0;i<n;i++){
          stars.push({
            x: Math.random()*w,
            y: Math.random()*h,
            r: Math.random()*1.4 + 0.2,
            a: 0.25 + Math.random()*0.7,
            tw: (Math.random()*0.015 + 0.004)
          });
        }
      }

      function draw(){
        ctx.clearRect(0,0,w,h);
        for(var i=0;i<stars.length;i++){
          var s = stars[i];
          s.a += (Math.random()-0.5)*s.tw;
          if(s.a < 0.18) s.a = 0.18;
          if(s.a > 0.95) s.a = 0.95;
          ctx.globalAlpha = s.a;
          ctx.fillStyle = '#fff';
          ctx.beginPath();
          ctx.arc(s.x, s.y, s.r, 0, Math.PI*2);
          ctx.fill();
        }
        ctx.globalAlpha = 1;
      }

      function start(){
        if(timer) return;
        // 12fps：更省電
        timer = setInterval(draw, 1000/12);
      }
      function stop(){
        if(timer){ clearInterval(timer); timer=null; }
      }

      window.addEventListener('resize', resize, {passive:true});
      document.addEventListener('visibilitychange', function(){
        if(document.hidden) stop();
        else start();
      });

      var prefersReduce = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
      resize();
      if(!prefersReduce) start();
    })();

    /* =========================
       7) 初次渲染
       ========================= */
    render();
  </script>
</body>
</html>
