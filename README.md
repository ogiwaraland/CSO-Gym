CSO Gym
[index.html](https://github.com/user-attachments/files/28526636/index.html)

<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<title>ホームジム トレーニング管理</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
body{font-family:-apple-system,'Hiragino Sans','Yu Gothic UI',sans-serif;background:#1a1a1a;color:#f0ede6;min-height:100vh}
:root{
  --green:#2dbd8c;--green-light:#1a3d30;--green-dark:#a8f0d8;
  --amber:#f0a030;--amber-light:#3d2e0a;--amber-dark:#ffd080;
  --blue:#5090e0;--blue-light:#0e2040;--blue-dark:#a0c8ff;
  --coral:#e06050;--coral-light:#3d1510;--coral-dark:#ffb0a0;
  --purple:#8878e8;--purple-light:#1e1840;--purple-dark:#c8b8ff;
  --bg:#1a1a1a;--surface:#252525;--surface2:#2e2e2e;
  --border:#3a3a3a;--border2:#4a4a4a;
  --text:#f0ede6;--text2:#b0ada6;--text3:#787570;
  --radius:12px;--radius-lg:16px;
}
.app{display:flex;flex-direction:column;min-height:100vh;max-width:1024px;margin:0 auto}

/* HEADER */
.header{background:#202020;border-bottom:1px solid var(--border);padding:16px 20px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:100}
.header h1{font-size:24px;font-weight:700;color:var(--text)}
.header .sub{font-size:16px;color:var(--text3);margin-top:3px}
.header-right{font-size:15px;color:var(--text2);text-align:right;line-height:1.6}

/* TABS */
.tabs{display:flex;background:#202020;border-bottom:1px solid var(--border)}
.tab{flex:1;padding:16px 6px;border:none;background:transparent;font-size:16px;font-weight:600;color:var(--text3);cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:4px;border-bottom:3px solid transparent;transition:all 0.15s}
.tab .tab-icon{font-size:26px}
.tab.active{color:var(--green);border-bottom-color:var(--green)}

/* CONTENT */
.content{padding:16px;flex:1}
.panel{display:none}
.panel.active{display:block}

/* CARDS */
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:16px 18px;margin-bottom:14px}
.card-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:12px}
.card-title{font-size:19px;font-weight:700;color:var(--text)}
.badge{font-size:14px;padding:4px 10px;border-radius:8px;font-weight:600}
.badge-green{background:var(--green-light);color:var(--green-dark)}
.badge-blue{background:var(--blue-light);color:var(--blue-dark)}
.badge-amber{background:var(--amber-light);color:var(--amber-dark)}
.badge-coral{background:var(--coral-light);color:var(--coral-dark)}
.badge-purple{background:var(--purple-light);color:var(--purple-dark)}

/* SECTION TITLE */
.sec-title{font-size:18px;font-weight:700;color:var(--text2);margin:18px 0 10px;display:flex;align-items:center;gap:8px}
.sec-dot{width:10px;height:10px;border-radius:50%;flex-shrink:0}

/* STAT */
.stat-grid{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:16px}
.stat-card{background:var(--surface2);border-radius:var(--radius);padding:14px;text-align:center;border:1px solid var(--border)}
.stat-label{font-size:15px;color:var(--text3);margin-bottom:6px}
.stat-value{font-size:38px;font-weight:700;color:var(--text);line-height:1}
.stat-unit{font-size:15px;color:var(--text3);margin-top:4px}
.week-dots{display:flex;gap:8px;margin-top:8px;justify-content:center}
.week-dot{width:14px;height:14px;border-radius:50%;background:var(--border);border:1px solid var(--border2)}
.week-dot.done{background:var(--green);border-color:var(--green)}

/* DURATION */
.dur-toggle{display:flex;gap:8px;margin-bottom:14px;align-items:center}
.dur-label{font-size:17px;color:var(--text2);font-weight:600}
.dur-btn{padding:12px 28px;border-radius:24px;border:1.5px solid var(--border2);background:transparent;font-size:17px;font-weight:700;cursor:pointer;color:var(--text2);transition:all 0.15s}
.dur-btn.sel{background:var(--blue);color:#fff;border-color:var(--blue)}

/* EXERCISE */
.ex-row{display:flex;align-items:center;gap:12px;padding:10px 0;border-top:1px solid var(--border)}
.ex-row:first-child{border-top:none}
.ex-check{width:34px;height:34px;border-radius:50%;border:2px solid var(--border2);cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;transition:all 0.2s;font-size:15px;font-weight:700}
.ex-check.done{background:var(--green);border-color:var(--green);color:#fff}
.ex-main{flex:1;min-width:0}
.ex-name{font-size:18px;color:var(--text);line-height:1.4;font-weight:500}
.ex-name.done{text-decoration:line-through;color:var(--text3)}
.ex-detail{font-size:15px;color:var(--text3);margin-top:3px}
.ex-caution{font-size:14px;color:var(--coral-dark);background:var(--coral-light);padding:3px 8px;border-radius:6px;white-space:nowrap;flex-shrink:0;font-weight:600}

/* WALK */
.walk-meta{font-size:17px;color:var(--text2);margin-bottom:12px;line-height:1.6}
.walk-controls{display:flex;align-items:center;gap:14px;margin-bottom:12px;flex-wrap:wrap}
.walk-timer{font-size:48px;font-weight:700;color:var(--text);min-width:110px;font-variant-numeric:tabular-nums}
.walk-btn{padding:14px 28px;border-radius:var(--radius);border:none;font-size:18px;font-weight:700;cursor:pointer}
.walk-start{background:var(--green);color:#fff}
.walk-stop{background:var(--coral);color:#fff}
.walk-reset{background:var(--surface2);color:var(--text2);border:1px solid var(--border2)}
.progress-wrap{background:var(--surface2);border-radius:6px;height:10px;overflow:hidden;margin-bottom:8px}
.progress-bar{height:100%;background:var(--green);border-radius:6px;transition:width 0.5s}
.walk-note{font-size:15px;color:var(--text3);line-height:1.5}

/* NOTES */
.notes-area{width:100%;border:1px solid var(--border);border-radius:var(--radius);padding:14px 16px;font-size:18px;font-family:inherit;color:var(--text);background:var(--surface2);resize:vertical;min-height:90px;margin-top:8px}
.notes-area:focus{outline:none;border-color:var(--green)}
.notes-area::placeholder{color:var(--text3)}

/* COMPLETE BTN */
.complete-btn{width:100%;padding:18px;background:var(--green);color:#fff;border:none;border-radius:var(--radius);font-size:19px;font-weight:700;cursor:pointer;margin-top:14px;display:flex;align-items:center;justify-content:center;gap:10px}
.complete-btn:active{opacity:0.85}

/* ADD EXERCISE */
.add-section{background:var(--surface2);border:1.5px dashed var(--border2);border-radius:var(--radius-lg);padding:16px;margin-bottom:14px}
.add-title{font-size:18px;font-weight:700;color:var(--text2);margin-bottom:12px}
.add-form{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.add-input{padding:12px 14px;border:1px solid var(--border2);border-radius:var(--radius);background:var(--surface);color:var(--text);font-size:17px;font-family:inherit}
.add-input:focus{outline:none;border-color:var(--green)}
.add-input::placeholder{color:var(--text3)}
.add-select{padding:12px 14px;border:1px solid var(--border2);border-radius:var(--radius);background:var(--surface);color:var(--text);font-size:17px;font-family:inherit}
.add-btn{grid-column:1/-1;padding:14px;background:var(--blue);color:#fff;border:none;border-radius:var(--radius);font-size:18px;font-weight:700;cursor:pointer}
.add-btn:active{opacity:0.85}
.custom-badge{font-size:11px;padding:2px 7px;border-radius:5px;background:#3a2a50;color:#c8b8ff;font-weight:600;margin-left:6px}

/* SCHEDULE */
.week-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:6px;margin-bottom:18px}
.day-cell{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:10px 4px;text-align:center}
.day-cell.today{border:2px solid var(--green);background:var(--green-light)}
.day-cell.rest{background:var(--surface2)}
.day-name{font-size:14px;color:var(--text3);margin-bottom:4px;font-weight:600}
.day-num{font-size:22px;font-weight:700;color:var(--text)}
.day-type{font-size:12px;margin-top:4px;padding:3px 4px;border-radius:4px;line-height:1.2;font-weight:600}
.day-cell.today .day-type{background:var(--green);color:#fff}
.day-cell.rest .day-type{background:var(--border);color:var(--text3)}
.day-type-normal{background:var(--blue-light);color:var(--blue-dark)}

.program-row{display:flex;align-items:flex-start;gap:14px;padding:12px 0;border-top:1px solid var(--border)}
.program-row:first-child{border-top:none}
.prog-icon{width:44px;height:44px;border-radius:var(--radius);display:flex;align-items:center;justify-content:center;font-size:22px;flex-shrink:0}
.prog-upper{background:var(--blue-light)}
.prog-lower{background:var(--green-light)}
.prog-core{background:var(--amber-light)}
.prog-walk{background:var(--purple-light)}
.prog-rest{background:var(--surface2)}
.prog-content{flex:1}
.prog-day{font-size:15px;color:var(--text3);font-weight:600}
.prog-name{font-size:18px;font-weight:700;color:var(--text);margin:2px 0 4px}
.prog-desc{font-size:15px;color:var(--text2);line-height:1.5}
.prog-time{font-size:15px;color:var(--text3);margin-top:4px;font-weight:600}

.injury-box{background:var(--coral-light);border:1px solid #5a2010;border-radius:var(--radius-lg);padding:16px 18px}
.injury-item{font-size:17px;color:var(--coral-dark);padding:5px 0;line-height:1.6}

/* LIBRARY */
.filter-row{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:14px}
.filter-btn{padding:11px 20px;border-radius:24px;border:1.5px solid var(--border2);background:transparent;font-size:16px;font-weight:600;cursor:pointer;color:var(--text2);transition:all 0.15s}
.filter-btn.sel{background:var(--text);color:#1a1a1a;border-color:var(--text)}
.lib-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:16px 18px;margin-bottom:12px}
.lib-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:8px}
.lib-name{font-size:18px;font-weight:700;color:var(--text)}
.lib-tags{display:flex;gap:5px;flex-wrap:wrap;margin-bottom:8px}
.tag{font-size:11px;padding:3px 8px;border-radius:5px;font-weight:600}
.tag-upper{background:var(--blue-light);color:var(--blue-dark)}
.tag-lower{background:var(--green-light);color:var(--green-dark)}
.tag-core{background:var(--amber-light);color:var(--amber-dark)}
.tag-walk{background:var(--purple-light);color:var(--purple-dark)}
.tag-ball{background:#1a3020;color:#80e8a0}
.tag-mball{background:#2a1a30;color:#d0a0ff}
.tag-dips{background:#0e2a3a;color:#80d0ff}
.tag-roller{background:#1a2a10;color:#a0e060}
.tag-band{background:#2a1040;color:#e0a0ff}
.tag-stretch{background:#0a2a2a;color:#60e0d0}
.lib-desc{font-size:15px;color:var(--text2);line-height:1.6}
.lib-sets{font-size:16px;color:var(--text);font-weight:700;margin-top:8px}

/* HISTORY */
.hist-entry{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:16px 18px;margin-bottom:12px}
.hist-date{font-size:15px;color:var(--text3);font-weight:600}
.hist-title{font-size:19px;font-weight:700;color:var(--text);margin:4px 0 8px}
.hist-stats{display:flex;gap:16px;flex-wrap:wrap}
.hist-stat{font-size:15px;color:var(--text2);font-weight:500}
.stars{display:flex;gap:4px;margin-top:10px;align-items:center}
.star{font-size:32px;cursor:pointer;color:var(--border2);transition:color 0.1s}
.star.filled{color:#f0a030}
.star-label{font-size:15px;color:var(--text3);margin-left:6px;font-weight:600}
.hist-note{font-size:15px;color:var(--text2);margin-top:10px;padding:10px 12px;background:var(--surface2);border-radius:var(--radius);line-height:1.6}
.empty{text-align:center;padding:60px 16px;color:var(--text3)}
.empty-icon{font-size:56px;margin-bottom:14px}
.empty-text{font-size:15px;line-height:1.6}
</style>
</head>
<body>
<div class="app">

<div class="header">
  <div>
    <h1>🏋️ ホームジム トレーニング</h1>
    <div class="sub">怪我に配慮した自宅プログラム</div>
  </div>
  <div class="header-right" id="dateDisplay"></div>
</div>

<div class="tabs">
  <button class="tab active" onclick="switchTab('today','tab0')" id="tab0"><span class="tab-icon">📅</span>今日</button>
  <button class="tab" onclick="switchTab('schedule','tab1')" id="tab1"><span class="tab-icon">🗓️</span>週間</button>
  <button class="tab" onclick="switchTab('library','tab2')" id="tab2"><span class="tab-icon">📋</span>種目</button>
  <button class="tab" onclick="switchTab('mypage','tab3')" id="tab3"><span class="tab-icon">⚙️</span>マイページ</button>
</div>

<div class="content">

<!-- TODAY -->
<div class="panel active" id="panel-today">
  <div style="background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:14px 16px;margin-bottom:14px">
    <div style="font-size:16px;font-weight:700;color:var(--text2);margin-bottom:12px">📊 今日の進捗</div>
    <div id="categoryProgress"></div>
  </div>

  <div class="dur-toggle">
    <span class="dur-label">今日の時間：</span>
    <button class="dur-btn sel" id="dur60" onclick="setDuration(60)">60分</button>
    <button class="dur-btn" id="dur30" onclick="setDuration(30)">30分</button>
  </div>

  <div class="sec-title"><span class="sec-dot" style="background:var(--amber)"></span>ウォームアップ（5分）</div>
  <div class="card" id="card-warmup"></div>

  <div class="sec-title"><span class="sec-dot" style="background:var(--blue)"></span>上半身トレーニング <span class="badge badge-blue" style="margin-left:auto;font-size:11px">猫背改善対応</span></div>
  <div class="card" id="card-upper"></div>

  <div class="sec-title"><span class="sec-dot" style="background:var(--green)"></span>下半身トレーニング <span class="badge badge-green" style="margin-left:auto;font-size:11px">膝・足首配慮</span></div>
  <div class="card" id="card-lower"></div>

  <div class="sec-title"><span class="sec-dot" style="background:var(--amber)"></span>体幹・バランスボール <span class="badge badge-amber" style="margin-left:auto;font-size:11px">腰痛配慮</span></div>
  <div class="card" id="card-core"></div>

  <div class="sec-title"><span class="sec-dot" style="background:var(--purple)"></span>ウォーキング（別メニュー）</div>
  <div class="card">
    <div class="card-header">
      <div class="card-title">ルームランナー ウォーキング</div>
      <span class="badge badge-purple">低衝撃</span>
    </div>
    <div class="walk-meta">目標：<span id="walkTarget">30</span>分 ｜ 傾斜1〜3° ｜ 速度4〜5km/h</div>
    <div class="walk-controls">
      <div class="walk-timer" id="walkTimer">00:00</div>
      <button class="walk-btn walk-start" id="walkBtn" onclick="toggleWalk()">開始</button>
      <button class="walk-btn walk-reset" onclick="resetWalk()">リセット</button>
    </div>
    <div class="progress-wrap"><div class="progress-bar" id="walkBar" style="width:0%"></div></div>
    <div class="walk-note">※ ウォーキングはトレーニング後、または別日に実施推奨。走らないこと。</div>
  </div>

  <div class="sec-title"><span class="sec-dot" style="background:#20a090"></span>ストレッチ・リカバリー（トレーニング後）</div>
  <div class="card">
    <div class="card-header">
      <div class="card-title">フォームローラー ＆ ストレッチポール</div>
      <span class="badge badge-green">毎日推奨</span>
    </div>
    <div class="ex-row" style="flex-wrap:wrap"><div style="display:flex;align-items:center;gap:10px;width:100%"><div class="ex-check" onclick="toggleEx('s0',this)"></div><div class="ex-main"><div class="ex-name">ストレッチポール 背骨リセット</div><div class="ex-detail">5〜10分 仰向けに乗るだけ</div></div><div class="ex-caution">猫背改善</div><div onclick="toggleDesc('desc-s0')" style="font-size:20px;color:var(--text3);cursor:pointer;padding:0 4px;flex-shrink:0">ℹ️</div></div><div id="desc-s0" style="display:none;width:100%;margin-top:6px;padding:10px 12px;background:var(--surface2);border-radius:8px;border-left:3px solid var(--blue);font-size:15px;color:var(--text2);line-height:1.7">ポールを頭から背骨に沿って縦に置き仰向けに乗る。重力で背骨・胸椎が自然に伸びる。猫背・巻き肩改善の基本。5〜10分乗るだけ。毎日やるのがおすすめ。乗り降りはゆっくり行う。</div></div>
    <div class="ex-row" style="flex-wrap:wrap"><div style="display:flex;align-items:center;gap:10px;width:100%"><div class="ex-check" onclick="toggleEx('s1',this)"></div><div class="ex-main"><div class="ex-name">フォームローラー 大腿四頭筋ほぐし</div><div class="ex-detail">左右各60秒</div></div><div class="ex-caution">膝ケア</div><div onclick="toggleDesc('desc-s1')" style="font-size:20px;color:var(--text3);cursor:pointer;padding:0 4px;flex-shrink:0">ℹ️</div></div><div id="desc-s1" style="display:none;width:100%;margin-top:6px;padding:10px 12px;background:var(--surface2);border-radius:8px;border-left:3px solid var(--blue);font-size:15px;color:var(--text2);line-height:1.7">うつ伏せで太ももの前面をローラーの上に乗せてゆっくり転がす。膝への負担を軽減する効果あり。痛い部分では止めて圧をかけるとより効果的。強く転がしすぎないよう注意。</div></div>
    <div class="ex-row" style="flex-wrap:wrap"><div style="display:flex;align-items:center;gap:10px;width:100%"><div class="ex-check" onclick="toggleEx('s2',this)"></div><div class="ex-main"><div class="ex-name">フォームローラー 背中・胸椎ほぐし</div><div class="ex-detail">60秒 × 2セット</div></div><div class="ex-caution">猫背改善</div><div onclick="toggleDesc('desc-s2')" style="font-size:20px;color:var(--text3);cursor:pointer;padding:0 4px;flex-shrink:0">ℹ️</div></div><div id="desc-s2" style="display:none;width:100%;margin-top:6px;padding:10px 12px;background:var(--surface2);border-radius:8px;border-left:3px solid var(--blue);font-size:15px;color:var(--text2);line-height:1.7">仰向けでローラーを背中の中央に置き前後にゆっくり転がす。胸椎の可動域改善・猫背改善に効果的。PC業務後の疲労回復に最適。気持ちよく感じる範囲で行う。</div></div>
    <div class="ex-row" style="flex-wrap:wrap"><div style="display:flex;align-items:center;gap:10px;width:100%"><div class="ex-check" onclick="toggleEx('s3',this)"></div><div class="ex-main"><div class="ex-name">フォームローラー 臀部ほぐし</div><div class="ex-detail">左右各60秒</div></div><div class="ex-caution">腰痛ケア</div><div onclick="toggleDesc('desc-s3')" style="font-size:20px;color:var(--text3);cursor:pointer;padding:0 4px;flex-shrink:0">ℹ️</div></div><div id="desc-s3" style="display:none;width:100%;margin-top:6px;padding:10px 12px;background:var(--surface2);border-radius:8px;border-left:3px solid var(--blue);font-size:15px;color:var(--text2);line-height:1.7">座位でローラーに臀部を乗せて片側ずつ体重をかけながら転がす。梨状筋・臀部の張りをほぐして腰痛改善に効果的。かなり痛い場合は体重を少し逃がして圧を調整する。</div></div>
  </div>

  <div class="sec-title"><span class="sec-dot" style="background:var(--text3)"></span>今日のメモ</div>
  <textarea class="notes-area" id="todayNotes" placeholder="体調・痛みの具合・使用重量など..."></textarea>
  <button class="complete-btn" onclick="completeWorkout()">✓ 今日のトレーニングを終了する</button>
</div>

<!-- SCHEDULE -->
<div class="panel" id="panel-schedule">
  <div class="sec-title" style="margin-top:0"><span class="sec-dot" style="background:var(--green)"></span>週間カレンダー</div>
  <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:10px">
    <button id="btnPrev" onclick="changeWeek(-1)" style="padding:10px 20px;background:var(--surface2);border:1.5px solid var(--border2);border-radius:var(--radius);color:var(--text);font-size:18px;font-weight:700;cursor:pointer">◀ 前の週</button>
    <div id="weekLabel" style="font-size:15px;font-weight:700;color:var(--text2);text-align:center"></div>
    <button id="btnNext" onclick="changeWeek(1)" style="padding:10px 20px;background:var(--surface2);border:1.5px solid var(--border2);border-radius:var(--radius);color:var(--text);font-size:18px;font-weight:700;cursor:pointer">次の週 ▶</button>
  </div>
  <div class="week-grid" id="weekGrid"></div>
  <div id="dayDetail" style="margin-bottom:14px"></div>
  <div class="sec-title"><span class="sec-dot" style="background:var(--blue)"></span>週間プログラム</div>
  <div class="card" id="weeklyProg"></div>
  <div class="sec-title"><span class="sec-dot" style="background:var(--coral)"></span>怪我への対応メモ</div>
  <div class="injury-box" id="injuryBox"></div>
</div>

<!-- LIBRARY -->
<div class="panel" id="panel-library">
  <div class="filter-row">
    <button class="filter-btn sel" onclick="filterLib('all',this)">すべて</button>
    <button class="filter-btn" onclick="filterLib('upper',this)">上半身</button>
    <button class="filter-btn" onclick="filterLib('lower',this)">下半身</button>
    <button class="filter-btn" onclick="filterLib('core',this)">体幹</button>
    <button class="filter-btn" onclick="filterLib('ball',this)">バランスボール</button>
    <button class="filter-btn" onclick="filterLib('mball',this)">ウエイトボール</button>
    <button class="filter-btn" onclick="filterLib('dips',this)">ディップス</button>
    <button class="filter-btn" onclick="filterLib('roller',this)">腹筋ローラー</button>
    <button class="filter-btn" onclick="filterLib('band',this)">ヒップバンド</button>
    <button class="filter-btn" onclick="filterLib('stretch',this)">ストレッチ</button>
    <button class="filter-btn" onclick="filterLib('walk',this)">ウォーキング</button>
  </div>
  <div id="libList"></div>
</div>

<!-- MYPAGE -->
<div class="panel" id="panel-mypage">

  <!-- 違和感・痛みチェック -->
  <div class="sec-title" style="margin-top:0"><span class="sec-dot" style="background:var(--coral)"></span>今日の違和感・痛みチェック</div>
  <div class="card">
    <div style="font-size:14px;color:var(--text3);margin-bottom:12px">各部位の今日の程度を記録（翌日自動リセット）</div>
    <div id="bodyCheck"></div>
  </div>

  <!-- 使用重量メモ -->
  <div class="sec-title"><span class="sec-dot" style="background:var(--blue)"></span>使用重量メモ</div>
  <div class="card">
    <div style="font-size:13px;color:var(--text3);margin-bottom:12px">各種目の現在の重量を記録</div>
    <div id="weightMemoList"></div>
    <div style="display:flex;gap:8px;margin-top:12px">
      <input id="wName" class="add-input" placeholder="種目名" style="flex:1">
      <input id="wKg" class="add-input" placeholder="重量(kg)" style="width:90px">
      <button onclick="addWeightMemo()" style="padding:10px 16px;background:var(--blue);color:#fff;border:none;border-radius:var(--radius);font-size:14px;font-weight:700;cursor:pointer">追加</button>
    </div>
  </div>

  <!-- 思い出しノート -->
  <div class="sec-title"><span class="sec-dot" style="background:var(--amber)"></span>思い出しノート</div>
  <div class="card">
    <div style="font-size:13px;color:var(--text3);margin-bottom:8px">体調・痛み・気づきを記録（上書き保存・容量ゼロ）</div>
    <textarea id="noteArea" class="notes-area" placeholder="例：右膝が少し痛む。ダンベルカールは12kgに上げた。腰は今日は調子良い..."></textarea>
    <button onclick="saveNote()" style="margin-top:10px;width:100%;padding:12px;background:var(--amber);color:#fff;border:none;border-radius:var(--radius);font-size:15px;font-weight:700;cursor:pointer">💾 保存（上書き）</button>
  </div>

  <!-- 目標管理 -->
  <div class="sec-title"><span class="sec-dot" style="background:var(--green)"></span>目標管理</div>
  <div class="card">
    <div style="font-size:13px;color:var(--text3);margin-bottom:12px">現在値と目標を入力（最新値のみ保存）</div>
    <div id="goalList"></div>
  </div>

  <!-- 設備一覧 -->
  <div class="sec-title"><span class="sec-dot" style="background:var(--purple)"></span>設備一覧 <span style="font-size:12px;color:var(--text3);font-weight:400">タップで種目を追加</span></div>
  <div class="card" id="equipList"></div>
  <div id="equipExModal" style="display:none;background:var(--surface);border:2px solid var(--green);border-radius:var(--radius-lg);padding:16px 18px;margin-top:10px">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px">
      <div id="equipModalTitle" style="font-size:16px;font-weight:700;color:var(--text)"></div>
      <button onclick="closeEquipModal()" style="padding:6px 14px;background:var(--surface2);border:1px solid var(--border2);border-radius:8px;color:var(--text2);font-size:13px;font-weight:700;cursor:pointer">✕ 閉じる</button>
    </div>
    <div id="equipExList"></div>
  </div>

</div>

</div>
</div>

<script>
const DAYS_JP=['日','月','火','水','木','金','土'];

const warmupData=[
  {name:'肩回し・首ストレッチ',detail:'前後各10回',caution:null},
  {name:'キャットカウ（四つん這い・背中丸め反らし）',detail:'10回ゆっくり',caution:'腰に注意'},
  {name:'足首回し・ふくらはぎストレッチ',detail:'各方向10秒',caution:'手術後は様子見'},
];
const upperFull=[
  {name:'ダンベル チェストプレス（ベンチ仰向け）',detail:'10kg × 3セット × 10回',caution:null},
  {name:'ダンベル ロウ（片手・ベンチ支持）',detail:'15kg × 3セット × 10回',caution:null},
  {name:'ダンベル ショルダープレス',detail:'7kg × 3セット × 12回',caution:'肩痛時は軽量'},
  {name:'ダンベル カール',detail:'10kg × 3セット × 12回',caution:null},
  {name:'フェイスプル（BARWINGマシン）',detail:'3セット × 15回',caution:'猫背改善'},
  {name:'ケトルベルスイング（低強度）',detail:'12kg × 3セット × 15回',caution:'腰に注意'},
  {name:'ディップス',detail:'自重 × 3セット × 5〜8回',caution:'肩痛時は浅く'},
  {name:'ネガティブ懸垂',detail:'3セット × 5回（5秒下ろす）',caution:'補助つきでもOK'},
  // 大胸筋
  {name:'ダンベル フライ（ベンチ）',detail:'10kg × 3セット × 12回',caution:'大胸筋伸展'},
  {name:'ダンベル インクラインプレス（ベンチ角度上げ）',detail:'10kg × 3セット × 10回',caution:'大胸筋上部'},
  // 上腕二頭筋
  {name:'ハンマーカール',detail:'10kg × 3セット × 12回',caution:'肘固定'},
  {name:'コンセントレーションカール',detail:'10kg × 3セット × 10回',caution:'孤立させて集中'},
  // 上腕三頭筋
  {name:'ダンベル トライセプスエクステンション',detail:'7kg × 3セット × 12回',caution:'肘が開かないよう'},
  {name:'ダンベル キックバック（三頭筋）',detail:'7kg × 3セット × 12回',caution:'肘を高く保つ'},
  // 三角筋
  {name:'ダンベル サイドレイズ',detail:'7kg × 3セット × 15回',caution:'三角筋中部'},
  {name:'ダンベル フロントレイズ',detail:'7kg × 3セット × 12回',caution:'三角筋前部'},
  {name:'ダンベル リアレイズ（前傾）',detail:'7kg × 3セット × 15回',caution:'三角筋後部・猫背改善'},
];
const upperShort=[
  {name:'ダンベル チェストプレス',detail:'10kg × 2セット × 12回',caution:null},
  {name:'ダンベル ロウ',detail:'15kg × 2セット × 12回',caution:null},
  {name:'フェイスプル（BARWINGマシン）',detail:'2セット × 15回',caution:'猫背改善'},
  {name:'ダンベル フライ',detail:'10kg × 2セット × 12回',caution:'大胸筋'},
  {name:'サイドレイズ',detail:'7kg × 2セット × 15回',caution:'三角筋'},
  {name:'トライセプスエクステンション',detail:'7kg × 2セット × 12回',caution:'三頭筋'},
];
const lowerFull=[
  {name:'ハーフスクワット（ダンベル持ち）',detail:'10kg × 3セット × 12回',caution:'痛みは浅めに'},
  {name:'ヒップスラスト（ベンチ使用）',detail:'17kg × 3セット × 12回',caution:'臀部強化'},
  {name:'ヒップヒンジ / RDL',detail:'15kg × 3セット × 10回',caution:'背中まっすぐ'},
  {name:'レッグエクステンション（BARWINGマシン）',detail:'3セット × 15回',caution:'大腿四頭筋'},
  {name:'カーフレイズ（ゆっくり）',detail:'自重 × 3セット × 20回',caution:'足首ゆっくり'},
  {name:'バンド グルートブリッジ',detail:'中強度 × 3セット × 15回',caution:'臀部に効かせる'},
  {name:'バンド クラムシェル',detail:'軽〜中強度 × 3セット × 左右15回',caution:'膝安定'},
];
const lowerShort=[
  {name:'ハーフスクワット（ダンベル）',detail:'10kg × 2セット × 12回',caution:'痛みは浅めに'},
  {name:'ヒップスラスト（ベンチ）',detail:'自重 × 2セット × 15回',caution:'臀部強化'},
  {name:'カーフレイズ',detail:'自重 × 2セット × 20回',caution:'足首ゆっくり'},
  {name:'バンド クラムシェル',detail:'軽強度 × 2セット × 左右15回',caution:'膝安定'},
];
const coreFull=[
  {name:'プランク',detail:'30秒 × 3セット',caution:'腰が下がらないよう'},
  {name:'バードドッグ（対角手足伸ばし）',detail:'左右10回 × 3セット',caution:'腰痛改善'},
  {name:'グルートブリッジ',detail:'3セット × 15回',caution:'腰・臀部強化'},
  {name:'バランスボール 腹筋ロール',detail:'3セット × 10回',caution:'腰注意・ゆっくり'},
  {name:'バランスボール 体幹キープ（座位）',detail:'30秒 × 3セット',caution:'姿勢改善'},
  {name:'ウエイトボール ロシアンツイスト',detail:'10kg × 2セット × 左右10回',caution:'腰注意'},
  {name:'膝つき腹筋ローラー',detail:'3セット × 8回',caution:'腰が反らないよう'},
];
const coreShort=[
  {name:'プランク',detail:'30秒 × 2セット',caution:'腰に注意'},
  {name:'グルートブリッジ',detail:'2セット × 15回',caution:'腰・臀部強化'},
  {name:'バランスボール 体幹キープ（座位）',detail:'30秒 × 2セット',caution:'姿勢改善'},
];

const weeklyData=[
  {day:'月曜日',label:'上半身A + 体幹',dur:'60分',type:'upper',icon:'💪',desc:'胸・背中中心。ダンベル＋BARWINGマシン'},
  {day:'火曜日',label:'下半身A + ウォーキング',dur:'60分',type:'lower',icon:'🦵',desc:'大腿四頭筋・臀部。低衝撃スクワット'},
  {day:'水曜日',label:'体幹 + バランスボール',dur:'30分',type:'core',icon:'🔥',desc:'軽め。姿勢改善・腰痛予防・バランスボール'},
  {day:'木曜日',label:'上半身B + 三角筋・腕',dur:'60分',type:'upper',icon:'💪',desc:'三角筋・二頭筋・三頭筋。ディップス・サイドレイズ'},
  {day:'金曜日',label:'下半身B + ウォーキング',dur:'60分',type:'lower',icon:'🦵',desc:'ふくらはぎ・臀部・体幹の複合'},
  {day:'土曜日',label:'完全休養',dur:'休み',type:'rest',icon:'😴',desc:'畑仕事もOK！軽いストレッチ推奨'},
  {day:'日曜日',label:'ウォーキングのみ（任意）',dur:'30分',type:'walk',icon:'🚶',desc:'ルームランナーでリカバリー歩行'},
];
const injuryItems=[
  '🦵 膝靭帯：スクワットは浅め・ゆっくり。痛みが出たら即中止',
  '🦶 足首：カーフレイズはゆっくり丁寧に。跳ぶ・走る系は禁止',
  '🔙 腰痛：ヒップヒンジ時は背中まっすぐを徹底。重量より形重視',
  '🏃 ランニング禁止：ルームランナーは速歩き（4〜5km/h）のみ',
  '🤸 懸垂：補助つきで週1〜2回まで。無理は禁物',
  '💪 肩・首：ショルダープレスは痛みが出たら軽量に変更',
  '🪑 猫背対策：フェイスプル・バードドッグを毎回必ず実施',
  '⚽ バランスボール：座位から始めて無理なく体幹を鍛える',
  '🩷 ヒップバンド：膝の安定性向上にも効果的。強度は軽→中→強の順で慣らす',
  '🧘 ストレッチポール：毎日乗るだけで猫背・腰痛改善。トレーニング後に必ず実施',
  '🫀 フォームローラー：痛い部分はゆっくり圧をかける。強く転がしすぎない',
];

const libraryData=[
  {name:'ダンベル チェストプレス',cat:'upper',tags:['上半身','胸'],desc:'ベンチに仰向けになりダンベルを押し上げる。大胸筋を鍛える基本種目。',sets:'10〜15kg × 3セット × 10〜12回'},
  {name:'ダンベル ロウ（片手）',cat:'upper',tags:['上半身','背中','猫背改善'],desc:'片手でベンチを支えにダンベルを引き上げる。広背筋・菱形筋を強化し猫背改善に有効。',sets:'15〜17kg × 3セット × 10回'},
  {name:'ダンベル ショルダープレス',cat:'upper',tags:['上半身','肩'],desc:'肩より上にダンベルを押し上げる。肩が痛む場合は7kg以下で行う。',sets:'7〜10kg × 3セット × 12回'},
  {name:'フェイスプル',cat:'upper',tags:['上半身','猫背改善','肩'],desc:'BARWINGマシンでケーブルを顔に向けて引く。巻き肩・猫背の改善に最重要種目。毎回必ず実施。',sets:'3セット × 15回（軽重量・丁寧に）'},
  {name:'ダンベル カール',cat:'upper',tags:['上半身','腕'],desc:'肘を固定してダンベルを曲げる。上腕二頭筋強化。ゆっくり下ろすことで効果アップ。',sets:'10kg × 3セット × 12回'},
  {name:'ケトルベルスイング',cat:'upper',tags:['上半身','全身','有酸素'],desc:'ケトルベルを股間から肩の高さまで振り上げる。全身有酸素＋臀部強化。腰の状態を確認しながら実施。',sets:'12〜16kg × 3セット × 15回'},
  {name:'ハーフスクワット（浅め）',cat:'lower',tags:['下半身','大腿四頭筋','膝配慮'],desc:'膝が痛む場合は浅めのスクワット。椅子から立ち上がる動作からスタートしてもOK。',sets:'ダンベル10kg × 3セット × 12回'},
  {name:'レッグエクステンション',cat:'lower',tags:['下半身','大腿四頭筋'],desc:'BARWINGマシンで脚を伸ばして大腿四頭筋を集中強化。スクワットが辛い場合の代替種目。',sets:'3セット × 15回'},
  {name:'ヒップスラスト',cat:'lower',tags:['下半身','臀部'],desc:'ベンチに肩を乗せ、ダンベルを腰に置いて腰を持ち上げる。臀部強化の最重要種目。膝・腰への負担が少ない。',sets:'自重 → 17〜20kg × 3セット × 12回'},
  {name:'ヒップヒンジ（RDL）',cat:'lower',tags:['下半身','臀部','ハムストリング'],desc:'腰をまっすぐ保ったまま上体を前傾。ハムストリング・臀部・姿勢改善に効果的。背中が丸まらないよう注意。',sets:'15kg × 3セット × 10回'},
  {name:'カーフレイズ',cat:'lower',tags:['下半身','ふくらはぎ','足首配慮'],desc:'つま先立ちをゆっくり繰り返す。ふくらはぎ強化。足首の状態に合わせてゆっくり行う。',sets:'自重 × 3セット × 20回（ゆっくり）'},
  {name:'プランク',cat:'core',tags:['体幹','腰痛予防'],desc:'うつ伏せで肘とつま先で体を支える。腰が下がらないよう注意。腰痛改善の基本種目。',sets:'30秒 × 3セット'},
  {name:'バードドッグ',cat:'core',tags:['体幹','腰痛予防','猫背改善'],desc:'四つん這いで対角線の手足をゆっくり伸ばす。体幹安定・腰痛予防の最重要種目。',sets:'左右各10回 × 3セット'},
  {name:'グルートブリッジ',cat:'core',tags:['体幹','臀部','腰痛予防'],desc:'仰向けで膝を曲げ腰を持ち上げる。臀部と体幹を同時強化。腰痛がある人でも安全に行える。',sets:'3セット × 15回'},
  {name:'バランスボール 体幹キープ（座位）',cat:'ball',tags:['バランスボール','体幹','姿勢改善'],desc:'バランスボールに座って体幹を安定させる。猫背・姿勢改善に効果的。PC作業の合間にもおすすめ。',sets:'30秒 × 3セット'},
  {name:'バランスボール 腹筋ロール',cat:'ball',tags:['バランスボール','体幹','腹筋'],desc:'ボールに前腕を乗せて前後に転がす。腹筋・体幹強化。腰が反らないよう注意。',sets:'3セット × 10回'},
  {name:'バランスボール ヒップリフト',cat:'ball',tags:['バランスボール','臀部','体幹'],desc:'仰向けでボールに足を乗せて腰を持ち上げる。臀部・ハムストリング強化。バランス感覚も鍛えられる。',sets:'3セット × 12回'},
  {name:'バランスボール 背中伸ばし',cat:'ball',tags:['バランスボール','姿勢改善','腰痛予防'],desc:'ボールに背中をあてて後ろに反る。背中・腰のストレッチ。PC業務後の疲労回復に。',sets:'30秒 × 2セット'},
  {name:'メディシンボール スクワット',cat:'mball',tags:['ウエイトボール','下半身','大腿四頭筋'],desc:'10kgボールを胸に抱えてスクワット。膝が痛む場合は浅めに。上半身が安定しやすい。',sets:'10kg × 3セット × 12回'},
  {name:'メディシンボール ロシアンツイスト',cat:'mball',tags:['ウエイトボール','体幹','腹斜筋'],desc:'座位でボールを持ち左右に体をひねる。腹斜筋・体幹強化。腰痛がある場合は軽く回転させる程度でOK。',sets:'10kg × 3セット × 左右10回'},
  {name:'メディシンボール チェストパス（壁）',cat:'mball',tags:['ウエイトボール','上半身','胸'],desc:'壁に向かってボールを押し出す。大胸筋・三頭筋強化。軽い爆発的な動きで筋力・瞬発力向上。',sets:'3セット × 10回'},
  {name:'メディシンボール デッドリフト',cat:'mball',tags:['ウエイトボール','下半身','臀部'],desc:'ボールを床から持ち上げる。臀部・ハムストリング・背中の強化。背中まっすぐを徹底すること。',sets:'10kg × 3セット × 10回'},
  {name:'メディシンボール スラム（低強度）',cat:'mball',tags:['ウエイトボール','全身','有酸素'],desc:'ボールを頭上から床に叩きつける。全身を使う有酸素種目。腰・膝に注意してゆっくり行う。',sets:'3セット × 10回'},
  {name:'ディップス（自重）',cat:'dips',tags:['ディップス','上半身','胸・三頭筋'],desc:'ディップススタンドで体を上下させる。大胸筋下部・上腕三頭筋・肩前部を強化。肘を曲げる角度は90度まで。肩に痛みがある場合は可動域を狭めて行う。',sets:'自重 × 3セット × 5〜8回（できる回数から）'},
  {name:'アシスト懸垂（チューブ補助）',cat:'dips',tags:['ディップス','上半身','背中'],desc:'懸垂マシンで補助を使いながら懸垂。広背筋・上腕二頭筋強化。現在補助つきで5回できるので、少しずつ補助を減らしていく。',sets:'補助つき × 3セット × 5回'},
  {name:'ネガティブ懸垂（ゆっくり下ろす）',cat:'dips',tags:['ディップス','上半身','背中'],desc:'台に乗って懸垂の上の位置からスタートし、ゆっくり5秒かけて下ろす。筋力強化に効果的。懸垂が1回しかできない場合の最適な練習法。',sets:'3セット × 3〜5回（5秒かけて下ろす）'},
  {name:'ハンギングニーレイズ',cat:'dips',tags:['ディップス','体幹','腹筋'],desc:'懸垂マシンにぶら下がり膝を胸に引き寄せる。腹筋・体幹強化。肩・腕への負荷も軽くかかる。腰への負担が少ない。',sets:'3セット × 10〜15回'},
  {name:'L字ハング（キープ）',cat:'dips',tags:['ディップス','体幹','腹筋'],desc:'懸垂マシンにぶら下がり脚を水平に保つ。体幹・腸腰筋の強化。難しければ膝を曲げた状態でもOK。',sets:'15〜30秒 × 3セット'},
  {name:'膝つき腹筋ローラー（初級）',cat:'roller',tags:['腹筋ローラー','体幹','腹筋'],desc:'膝をついた状態でローラーを前に転がして戻す。初心者向け。腰が反らないよう腹に力を入れて行う。腰痛がある場合はまずこちらから。',sets:'3セット × 8〜10回'},
  {name:'腹筋ローラー 壁あてロール',cat:'roller',tags:['腹筋ローラー','体幹','腹筋'],desc:'壁から30〜50cm離れてローラーを転がし壁に当てて戻す。可動域を制限した安全なやり方。腰への負担を最小限に抑えられる。',sets:'3セット × 10回'},
  {name:'腹筋ローラー 立ちロール（上級）',cat:'roller',tags:['腹筋ローラー','体幹','腹筋'],desc:'立った状態からローラーを前に転がす。非常に強度が高い。まずは膝つきで十分な筋力をつけてから挑戦。腰痛時は禁止。',sets:'できる回数 × 3セット（目標5回）'},
  {name:'腹筋ローラー サイドロール',cat:'roller',tags:['腹筋ローラー','体幹','腹斜筋'],desc:'斜め方向にローラーを転がす。腹斜筋・脇腹を強化。まず膝つき正面ができてから追加する。',sets:'左右各5回 × 3セット'},
  {name:'バンド ヒップアブダクション（横歩き）',cat:'band',tags:['ヒップバンド','臀部','太もも'],desc:'バンドを膝上に巻いてカニ歩き。中臀筋・外転筋を強化。膝の安定性向上にも効果的。膝の靭帯ケアにもおすすめ。',sets:'強度：軽〜中 × 3セット × 左右15歩'},
  {name:'バンド グルートブリッジ',cat:'band',tags:['ヒップバンド','臀部','体幹'],desc:'バンドを膝上に巻いてヒップリフト。通常より臀部への負荷が大幅アップ。腰痛予防・美尻づくりに最適。',sets:'強度：中 × 3セット × 15回'},
  {name:'バンド スクワット',cat:'band',tags:['ヒップバンド','下半身','大腿四頭筋'],desc:'バンドを膝上に巻いてスクワット。膝が内側に入るのを防ぐ。膝の安定性向上と臀部の活性化が同時にできる。',sets:'強度：軽〜中 × 3セット × 12回'},
  {name:'バンド クラムシェル',cat:'band',tags:['ヒップバンド','臀部','中臀筋'],desc:'横向きに寝てバンドを膝上に巻き、膝を貝のように開閉する。中臀筋・外旋筋の強化。膝・腰の安定性向上に最適。',sets:'強度：軽〜中 × 3セット × 左右15回'},
  {name:'バンド キックバック（四つん這い）',cat:'band',tags:['ヒップバンド','臀部','ハムストリング'],desc:'四つん這いでバンドを足首に巻き後ろに蹴り上げる。大臀筋・ハムストリング強化。美尻・桃尻づくりの定番種目。',sets:'強度：中〜強 × 3セット × 左右12回'},
  {name:'バンド サイドライイングアブダクション',cat:'band',tags:['ヒップバンド','臀部','太もも'],desc:'横向きに寝てバンドを膝上に巻き、上の脚を持ち上げる。外転筋・中臀筋の集中強化。美脚づくりに効果的。',sets:'強度：中 × 3セット × 左右15回'},
  {name:'フォームローラー 大腿四頭筋ほぐし',cat:'stretch',tags:['フォームローラー','リカバリー','膝ケア'],desc:'うつ伏せで太ももの前面をローラーでほぐす。膝への負担を軽減する効果あり。膝の靭帯が痛む場合のケアに最適。痛い部分は圧を弱めてゆっくり。',sets:'左右各60秒 × 2セット'},
  {name:'フォームローラー 腸脛靭帯ほぐし',cat:'stretch',tags:['フォームローラー','リカバリー','膝ケア'],desc:'横向きで太ももの外側（腸脛靭帯）をほぐす。膝の外側の痛みに効果的。ゆっくり転がして痛い部分で止めて圧をかける。',sets:'左右各60秒 × 2セット'},
  {name:'フォームローラー 背中・胸椎ほぐし',cat:'stretch',tags:['フォームローラー','リカバリー','猫背改善'],desc:'仰向けでローラーを背中の下に置き前後に転がす。胸椎の可動域改善・猫背改善に効果的。PC業務後のケアに最適。',sets:'60秒 × 2セット'},
  {name:'フォームローラー 臀部・梨状筋ほぐし',cat:'stretch',tags:['フォームローラー','リカバリー','腰痛ケア'],desc:'座位でローラーに臀部を乗せてほぐす。梨状筋・臀部の張りをほぐして腰痛改善に効果的。片側ずつ体重をかける。',sets:'左右各60秒 × 2セット'},
  {name:'フォームローラー ふくらはぎほぐし',cat:'stretch',tags:['フォームローラー','リカバリー','足首ケア'],desc:'床に座りふくらはぎの下にローラーを置いてほぐす。足首の柔軟性向上・ふくらはぎの疲労回復に効果的。',sets:'左右各60秒 × 2セット'},
  {name:'ストレッチポール 背骨リセット',cat:'stretch',tags:['ストレッチポール','リカバリー','猫背改善'],desc:'ポールを背骨に沿って縦に置き仰向けに乗る。重力で背骨・胸椎が自然に伸びる。猫背・巻き肩改善の基本。5〜10分乗るだけでOK。',sets:'5〜10分 × 毎日推奨'},
  {name:'ストレッチポール 肩甲骨ほぐし',cat:'stretch',tags:['ストレッチポール','リカバリー','肩こり'],desc:'ポールに仰向けに乗り腕を左右に広げてゆっくり動かす。肩甲骨まわりをほぐす。肩・首の痛みケアに効果的。',sets:'左右各30秒 × 3セット'},
  {name:'ストレッチポール 腰椎ストレッチ',cat:'stretch',tags:['ストレッチポール','リカバリー','腰痛ケア'],desc:'ポールを腰の下に横置きして仰向けに乗る。腰椎のアーチを整える。腰痛持ちに特に効果的。痛みが出たら中止。',sets:'60秒 × 2セット'},
  {name:'ストレッチポール 股関節ストレッチ',cat:'stretch',tags:['ストレッチポール','リカバリー','下半身'],desc:'ポールに仰向けに乗り膝を曲げて左右にゆっくり倒す。股関節・内転筋のストレッチ。下半身トレーニング後のケアに最適。',sets:'左右各30秒 × 3セット'},
  {name:'ダンベル フライ',cat:'upper',tags:['上半身','大胸筋'],desc:'ベンチに仰向けになりダンベルを弧を描くように開閉する。大胸筋の伸展・収縮を最大限に使える種目。チェストプレスと組み合わせると効果的。',sets:'10kg × 3セット × 12回'},
  {name:'ダンベル インクラインプレス',cat:'upper',tags:['上半身','大胸筋上部'],desc:'ベンチを30〜45度に傾けてプレス。大胸筋上部を集中強化。猫背改善・胸の厚みづくりに効果的。',sets:'10kg × 3セット × 10回'},
  {name:'ハンマーカール',cat:'upper',tags:['上半身','上腕二頭筋'],desc:'親指を上に向けた状態でダンベルを曲げる。上腕二頭筋・腕橈骨筋を同時強化。通常カールより腕全体を太くする効果あり。',sets:'10kg × 3セット × 12回'},
  {name:'コンセントレーションカール',cat:'upper',tags:['上半身','上腕二頭筋'],desc:'座位で肘を膝に固定してカール。上腕二頭筋を孤立させて集中的に鍛える。力こぶを作るのに最も効果的な種目。',sets:'10kg × 3セット × 10回'},
  {name:'トライセプスエクステンション',cat:'upper',tags:['上半身','上腕三頭筋'],desc:'頭の後ろでダンベルを持ち肘を伸ばす。上腕三頭筋の長頭を集中強化。二の腕引き締めに効果的。肘が外に開かないよう注意。',sets:'7kg × 3セット × 12回'},
  {name:'ダンベル キックバック（三頭筋）',cat:'upper',tags:['上半身','上腕三頭筋'],desc:'前傾姿勢で肘を高く保ちダンベルを後ろに伸ばす。上腕三頭筋外側頭の強化。肘の位置を固定してゆっくり動かす。',sets:'7kg × 3セット × 12回'},
  {name:'サイドレイズ',cat:'upper',tags:['上半身','三角筋中部'],desc:'肘を少し曲げてダンベルを真横に上げる。三角筋中部を集中強化。肩幅を広くする定番種目。肩の痛みに注意して軽めから始める。',sets:'7kg × 3セット × 15回'},
  {name:'フロントレイズ',cat:'upper',tags:['上半身','三角筋前部'],desc:'ダンベルを正面に肩の高さまで上げる。三角筋前部の強化。猫背の人は特に前部が弱いことが多い。',sets:'7kg × 3セット × 12回'},
  {name:'リアレイズ（前傾）',cat:'upper',tags:['上半身','三角筋後部','猫背改善'],desc:'上体を前傾させてダンベルを横に開く。三角筋後部・菱形筋を強化。猫背・巻き肩の改善に最も効果的な種目のひとつ。',sets:'7kg × 3セット × 15回'},
  {name:'ルームランナー ウォーキング',cat:'walk',tags:['ウォーキング','有酸素','低衝撃'],desc:'傾斜1〜3°、速度4〜5km/hで速歩き。膝・足首への衝撃を最小限に。脂肪燃焼・体力向上に。走らないこと。',sets:'30〜60分 ｜ 週3〜5回'},
];

let duration=60;
let checked={};
let customExercises=JSON.parse(localStorage.getItem('hgCustomEx')||'[]');
let walkOn=false,walkSec=0,walkIv=null;
let wkCnt=parseInt(localStorage.getItem('hgWk')||'0');
let wkMon=localStorage.getItem('hgMon')||'';

function checkNewWeek(){
  const now=new Date();
  const mon=getMondayStr(now);
  if(mon!==wkMon){wkCnt=0;wkMon=mon;localStorage.setItem('hgMon',mon);localStorage.setItem('hgWk','0');}
}
function getMondayStr(d){
  const dt=new Date(d);const day=dt.getDay();
  dt.setDate(dt.getDate()-day+(day===0?-6:1));
  return dt.toDateString();
}

function setDuration(d){
  duration=d;
  document.getElementById('dur60').classList.toggle('sel',d===60);
  document.getElementById('dur30').classList.toggle('sel',d===30);
  renderToday();
}

function getCustomByCategory(cat){
  return customExercises.filter(e=>e.cat===cat);
}


// 種目説明文
const exDescriptions={
  '肩回し・首ストレッチ':'両腕を大きく前回し・後ろ回しに10回ずつ。首はゆっくり左右に倒すだけ。無理に回さない。PC業務で固まった肩・首をほぐすウォームアップ。',
  'キャットカウ（四つん這い・背中丸め反らし）':'四つん這いになり、息を吐きながら背中を丸め（キャット）、息を吸いながら背中を反らす（カウ）。腰痛予防・背骨の柔軟性向上に効果的。腰に痛みがある場合はごく小さい動きから。',
  '足首回し・ふくらはぎストレッチ':'座位または立位で足首をゆっくり大きく回す。手術後は痛みが出ない範囲で行う。ふくらはぎは壁に手をついてアキレス腱を伸ばすストレッチも合わせて行うと効果的。',
  'ダンベル チェストプレス（ベンチ仰向け）':'ベンチに仰向けになりダンベルを肩幅より少し広く持つ。肘を90度に曲げた位置からまっすぐ上に押し上げる。大胸筋・三角筋前部・三頭筋を鍛える基本種目。',
  'ダンベル チェストプレス':'ベンチに仰向けになりダンベルを肩幅より少し広く持つ。肘を90度に曲げた位置からまっすぐ上に押し上げる。大胸筋・三角筋前部・三頭筋を鍛える基本種目。',
  'ダンベル ロウ（片手・ベンチ支持）':'片手でベンチに手をつき体を支える。反対の手でダンベルを床から脇腹に向けて引き上げる。広背筋・菱形筋を強化し猫背改善に効果的。背中をまっすぐ保つこと。',
  'ダンベル ロウ':'片手でベンチに手をつき体を支える。反対の手でダンベルを床から脇腹に向けて引き上げる。広背筋・菱形筋を強化し猫背改善に効果的。背中をまっすぐ保つこと。',
  'ダンベル ショルダープレス':'座位または立位でダンベルを耳の横に持ち、頭上に押し上げる。三角筋全体を鍛える。肩に痛みがある場合は7kg以下・可動域を狭めて行う。首の痛みがある場合は座位で行う。',
  'ダンベル カール':'肘を体の横に固定してダンベルをゆっくり曲げる。上腕二頭筋を集中強化。ゆっくり下ろすことで効果アップ。反動を使わないこと。',
  'フェイスプル（BARWINGマシン）':'ケーブルを顔の高さに設定し、両手で引っ張りながら顔に向けて引く。三角筋後部・菱形筋を強化。巻き肩・猫背の改善に最重要種目。PC業務者は必ず毎回実施。',
  'ケトルベルスイング（低強度）':'足を肩幅に開いてケトルベルを両手で持つ。股関節を折り曲げて前に振り下ろし、股関節を伸ばす力で肩の高さまで振り上げる。全身有酸素＋臀部強化。腰が丸まらないよう注意。',
  'ディップス':'ディップスバーを両手で握り体を支える。肘を曲げてゆっくり体を下げ、押し上げる。大胸筋下部・三頭筋を強化。肩に痛みがある場合は浅めの可動域で行う。',
  'ネガティブ懸垂':'台に乗って懸垂の上の位置からスタート。5秒かけてゆっくり体を下ろす。普通の懸垂ができなくても筋力をつけられる最適な方法。補助つきでもOK。',
  'ダンベル フライ（ベンチ）':'ベンチに仰向けになりダンベルを弧を描くように左右に開き、胸の前で合わせる。大胸筋の伸展・収縮を最大限に使える。チェストプレスと組み合わせると効果的。',
  'ダンベル フライ':'ベンチに仰向けになりダンベルを弧を描くように左右に開き、胸の前で合わせる。大胸筋の伸展・収縮を最大限に使える。チェストプレスと組み合わせると効果的。',
  'ダンベル インクラインプレス（ベンチ角度上げ）':'ベンチを30〜45度に傾けてプレス。大胸筋上部を集中強化。猫背改善・胸の厚みづくりに効果的。通常のプレスより軽い重量から始める。',
  'ハンマーカール':'親指を上に向けた状態（ハンマー持ち）でダンベルを曲げる。上腕二頭筋・腕橈骨筋を同時強化。通常カールより腕全体を太くする効果あり。',
  'コンセントレーションカール':'座位で肘を膝の内側に固定してカール。上腕二頭筋だけを孤立させて集中的に鍛える。力こぶを作るのに最も効果的な種目。反動を使わないこと。',
  'ダンベル トライセプスエクステンション':'頭の後ろでダンベルを持ち肘だけを動かして伸ばす。上腕三頭筋の長頭を集中強化。二の腕引き締めに効果的。肘が外に開かないよう注意。',
  'ダンベル キックバック（三頭筋）':'前傾姿勢で肘を高く保ちダンベルを後ろにゆっくり伸ばす。上腕三頭筋外側頭の強化。肘の位置を固定してゆっくり動かすことが重要。',
  'サイドレイズ':'肘を少し曲げた状態でダンベルを真横に肩の高さまで上げる。三角筋中部を集中強化。肩幅を広くする定番種目。肩の痛みに注意して軽めから始める。',
  'フロントレイズ':'ダンベルを正面に肩の高さまでゆっくり上げる。三角筋前部の強化。猫背の人は特に前部が弱いことが多い。反動を使わず丁寧に。',
  'リアレイズ（前傾）':'上体を45度前傾させてダンベルを横に開く。三角筋後部・菱形筋を強化。猫背・巻き肩の改善に最も効果的な種目のひとつ。軽い重量でも十分効果あり。',
  'ハーフスクワット（ダンベル持ち）':'ダンベルを両手に持ち足を肩幅に開く。膝がつま先方向に向くよう意識しながら浅めに腰を落とす。膝が痛む場合は椅子から立ち上がる動作から始めてもOK。',
  'ヒップスラスト（ベンチ使用）':'ベンチに肩甲骨を乗せ膝を90度に曲げる。ダンベルを腰に置いて腰をまっすぐ持ち上げる。臀部強化の最重要種目。膝・腰への負担が少なく怪我がある人でも安全。',
  'ヒップヒンジ / RDL':'足を肩幅に開きダンベルを太ももに沿わせながら股関節から上体を前傾させる。背中を絶対に丸めないこと。ハムストリング・臀部・姿勢改善に効果的。腰痛がある場合は軽めの重量から。',
  'レッグエクステンション（BARWINGマシン）':'マシンのシートに座り足首をパッドに引っ掛けてゆっくり脚を伸ばす。大腿四頭筋を集中強化。スクワットが辛い場合の代替種目にも最適。',
  'カーフレイズ（ゆっくり）':'立位でゆっくりつま先立ちになり、ゆっくり下ろす。3秒上げ・3秒下げが目安。ふくらはぎ強化。足首の手術後は痛みが出ない範囲でゆっくり行う。段差を使うと効果アップ。',
  'バンド グルートブリッジ':'バンドを膝上に巻いて仰向けになり膝を曲げる。膝を外に広げながら腰をまっすぐ持ち上げる。通常より臀部への負荷が大幅アップ。腰痛予防にも最適。',
  'バンド クラムシェル':'横向きに寝てバンドを膝上に巻く。膝を90度に曲げた状態で上の膝を貝のように開閉する。中臀筋・外旋筋の強化。膝の安定性向上に最適。軽い強度から始める。',
  'プランク':'うつ伏せで肘とつま先で体を支える。腰が下がらないようにお腹に力を入れて保持。腰痛改善の基本種目。最初は15〜20秒からでOK。無理をしない。',
  'バードドッグ（対角手足伸ばし）':'四つん這いになり右手と左足を同時にゆっくり伸ばして3秒キープ。体幹安定・腰痛予防の最重要種目。背中が丸まらないよう鏡で確認しながら行うと効果的。',
  'グルートブリッジ':'仰向けで膝を曲げ足を床につける。腰をまっすぐ持ち上げてお尻を締める。臀部と体幹を同時強化。腰痛がある人でも安全に行える。毎日やっても良い。',
  'デッドバグ':'仰向けで両腕を天井に向け膝を90度に曲げる。対角の手足をゆっくり伸ばして戻す。脊柱安定・体幹強化に効果的。呼吸を止めないように。',
  'バランスボール 腹筋ロール':'ボールに前腕を乗せて床と平行になるように前後に転がす。腹筋・体幹強化。腰が反らないよう腹に力を入れて行う。腰痛がある場合は小さい動きから。',
  'バランスボール 体幹キープ（座位）':'バランスボールに座って足を床につける。骨盤をまっすぐ保ちながら体幹を安定させる。猫背・姿勢改善に効果的。PC作業の椅子代わりに使うのもおすすめ。',
  'ウエイトボール ロシアンツイスト':'座位でボールを両手で持ち体を少し後ろに傾ける。ゆっくり左右に体をひねる。腹斜筋・体幹強化。腰痛がある場合は小さい動きでOK。',
  '膝つき腹筋ローラー':'膝をついた状態でローラーを前に転がし限界まで伸ばして戻す。腹筋・体幹強化。腰が反らないよう腹に力を入れる。腰痛がある場合はまずここから始める。',
  'アシスト懸垂':'チューブや補助を使って懸垂の動作を行う。広背筋・上腕二頭筋強化。現在補助つきで5回できるレベルから少しずつ補助を減らしていく。',
  'ハンギングニーレイズ':'懸垂マシンにぶら下がり膝をゆっくり胸に引き寄せる。腹筋・体幹強化。肩や腕の補助筋にも効果あり。腰への負担が少ない。',
  'L字ハング（キープ）':'懸垂マシンにぶら下がり脚を水平に保つ。体幹・腸腰筋の強化。難しければ膝を曲げた状態でもOK。少しずつ時間を延ばしていく。',
  'フォームローラー 大腿四頭筋ほぐし':'うつ伏せで太ももの前面をローラーの上に乗せてゆっくり転がす。膝への負担を軽減する効果あり。痛い部分では止めて圧をかけるとより効果的。',
  'フォームローラー 背中・胸椎ほぐし':'仰向けでローラーを背中の中央に置き前後に転がす。胸椎の可動域改善・猫背改善に効果的。PC業務後の疲労回復に最適。気持ちよく感じる範囲で行う。',
  'フォームローラー 臀部・梨状筋ほぐし':'座位でローラーに臀部を乗せて片側ずつ体重をかけながら転がす。梨状筋・臀部の張りをほぐして腰痛改善に効果的。',
  'ストレッチポール 背骨リセット':'ポールを頭から背骨に沿って縦に置き仰向けに乗る。重力で背骨・胸椎が自然に伸びる。猫背・巻き肩改善の基本。5〜10分乗るだけ。毎日やるのがおすすめ。',
  'ストレッチポール 肩甲骨ほぐし':'ポールに仰向けに乗り腕をゆっくり左右に広げたり上下に動かす。肩甲骨まわりをほぐす。肩・首の痛みケアに効果的。',
  'バンド ヒップアブダクション（横歩き）':'バンドを膝上に巻いて横歩きする。中臀筋・外転筋を強化。膝の靭帯が痛む場合のリハビリにも使われる種目。',
  'バンド スクワット':'バンドを膝上に巻いてスクワット。膝が内側に入るのを防いで膝の安定性を高める。臀部の活性化にも効果的。',
  'バンド キックバック（四つん這い）':'四つん這いでバンドを足首に巻き後ろにゆっくり蹴り上げる。大臀筋・ハムストリング強化。美尻づくりの定番種目。骨盤が傾かないよう注意。',
  'メディシンボール スクワット':'ボールを両手で胸の前に持ちスクワット。重心が安定しやすく姿勢が整いやすい。大腿四頭筋・臀部強化。膝が痛む場合は浅めに。',
  'メディシンボール ロシアンツイスト':'座位でボールを持ち体を少し後ろに傾けて左右にひねる。腹斜筋・体幹強化。腰痛がある場合は小さい動きでOK。',
  'ハーフスクワット（ダンベル）':'ダンベルを両手に持ち足を肩幅に開く。膝がつま先方向に向くよう意識しながら浅めに腰を落とす。膝が痛む場合は椅子から立ち上がる動作から始めてもOK。深く沈まなくて大丈夫。',
  'カーフレイズ':'立位でゆっくりつま先立ちになり、ゆっくり下ろす。3秒上げ・3秒下げが目安。ふくらはぎ強化。足首の手術後は痛みが出ない範囲でゆっくり行う。段差を使うと効果アップ。',
  'バランスボール ヒップリフト':'仰向けでバランスボールに両足を乗せ腰を持ち上げる。臀部・ハムストリング強化。バランス感覚も同時に鍛えられる。不安定な場合は壁に近い場所で行う。',
  'バランスボール 背中伸ばし':'ボールに背中をあてて後ろにゆっくり反る。背中・腰のストレッチ。PC業務後の疲労回復に最適。気持ちよく感じる範囲で行う。腰痛がある場合は無理に反らない。',
  'メディシンボール チェストパス（壁）':'壁から1〜2m離れて壁に向かってボールを押し出す。大胸筋・三頭筋強化。軽い爆発的な動きで筋力・瞬発力向上。腰・膝に負担がかからない上半身種目。',
  'メディシンボール デッドリフト':'足を肩幅に開きボールを床から持ち上げる。臀部・ハムストリング・背中の強化。背中を絶対に丸めないこと。腰痛がある場合は軽めの動きから。',
  'メディシンボール スラム（低強度）':'ボールを頭上に持ち上げてゆっくり床に置く動作を繰り返す。全身を使う有酸素種目。本来は叩きつけるが膝・腰への負担を考えゆっくり行う。',
  'バンド ヒップアブダクション（横歩き）':'バンドを膝上に巻いて横歩きする。中臀筋・外転筋を強化。膝の靭帯が痛む場合のリハビリにも使われる種目。小さい歩幅からスタート。',
  'バンド スクワット':'バンドを膝上に巻いてスクワット。膝が内側に入るのを防いで膝の安定性を高める。臀部の活性化にも効果的。痛みがある場合は浅めに。',
  'バンド キックバック（四つんaanse い）':'四つん這いでバンドを足首に巻き後ろにゆっくり蹴り上げる。大臀筋・ハムストリング強化。美尻づくりの定番種目。骨盤が傾かないよう注意。',
  'バンド サイドライイングアブダクション':'横向きに寝てバンドを膝上に巻き、上の脚をゆっくり持ち上げる。外転筋・中臀筋の集中強化。膝の安定性向上にも効果的。美脚づくりに効果的。',
  'フォームローラー 腸脛靭帯ほぐし':'横向きで太ももの外側をローラーの上に乗せてゆっくり転がす。膝の外側の痛みに効果的。かなり痛い場合は体重を少し逃がして圧を調整する。',
  'フォームローラー ふくらはぎほぐし':'床に座りふくらはぎの下にローラーを置いてゆっくり転がす。足首の柔軟性向上・ふくらはぎの疲労回復に効果的。足首の手術後のケアにも有用。',
  'ストレッチポール 腰椎ストレッチ':'ポールを腰の下に横置きして仰向けに乗る。腰椎のアーチを整える。腰痛持ちに特に効果的。痛みが出たら即中止。ゆっくり乗り降りすること。',
  'ストレッチポール 股関節ストレッチ':'ポールに仰向けに乗り膝を曲げて左右にゆっくり倒す。股関節・内転筋のストレッチ。下半身トレーニング後のケアに最適。気持ちよく感じる範囲で行う。',
  '膝つき腹筋ローラー（初級）':'膝をついた状態でローラーを前に転がし限界まで伸ばして戻す。腹筋・体幹強化。腰が反らないよう腹に力を入れる。腰痛がある場合はまずここから始める。',
  '腹筋ローラー 壁あてロール':'壁から30〜50cm離れてローラーを転がし壁に当てて戻す。可動域を制限した安全なやり方。腰への負担を最小限に抑えられる。慣れたら壁との距離を伸ばす。',
  '腹筋ローラー 立ちロール（上級）':'立った状態からローラーを前に転がす。非常に強度が高い。まずは膝つきで十分な筋力をつけてから挑戦。腰痛時は絶対に禁止。',
  '腹筋ローラー サイドロール':'膝をついて斜め方向にローラーを転がす。腹斜筋・脇腹を集中強化。まず正面の膝つきローラーができてから追加する種目。',
  'ケトルベル ゴブレットスクワット':'ケトルベルを両手で胸の前に縦に持ちスクワットする。重心が安定しやすく深くしゃがみやすい。大腿四頭筋・臀部強化。膝が痛む場合は浅めに。',
  'ケトルベル デッドリフト':'足を肩幅に開きケトルベルを床から持ち上げる。臀部・ハムストリング・背中の強化。背中を絶対に丸めないこと。ダンベルより安定しやすい。',
  'ケーブルロウ':'BARWINGマシンのケーブルを腹部に向けて引く。広背筋・菱形筋を強化。猫背改善に効果的。背中をまっすぐ保ち肩甲骨を寄せる動作を意識する。',
  'ラットプルダウン':'BARWINGマシンのケーブルを頭上から胸に向けて引き下げる。広背筋を強化。懸垂の補助トレーニングとしても最適。肩甲骨を下げる動作を意識する。',
  'アシスト懸垂':'チューブや補助バンドを使って懸垂の動作を行う。広背筋・上腕二頭筋強化。補助の力を借りることで正しい動作を身につけられる。少しずつ補助を減らしていく。',
  'ハンギングニーレイズ':'懸垂マシンにぶら下がり膝をゆっくり胸に引き寄せる。腹筋・体幹強化。肩や腕の補助筋にも効果あり。腰への負担が少なく怪我がある人でも安全にできる。',
  'L字ハング（キープ）':'懸垂マシンにぶら下がり脚を水平に保つ。体幹・腸腰筋の強化。難しければ膝を曲げた状態でもOK。少しずつ時間を延ばしていく。かなりの体幹強度が必要。',
  'ウォーキング（傾斜1〜3°）':'ルームランナーを傾斜1〜3°に設定して速歩きする。速度は4〜5km/h。膝・足首への衝撃を最小限に抑えながら有酸素運動ができる。走らないこと。脂肪燃焼・体力向上に最も安全な種目。',

  'ダンベル サイドレイズ':'肘を少し曲げた状態でダンベルを真横に肩の高さまで上げる。三角筋中部を集中強化。肩幅を広くする定番種目。肩の痛みに注意して軽めから始める。上げすぎず肩の高さで止めること。',
  'ダンベル フロントレイズ':'ダンベルを正面に肩の高さまでゆっくり上げる。三角筋前部の強化。猫背の人は特に前部が弱いことが多い。反動を使わず丁寧に。肩より高く上げすぎないよう注意。',
  'ダンベル リアレイズ（前傾）':'上体を45度前傾させてダンベルを横に開く。三角筋後部・菱形筋を強化。猫背・巻き肩の改善に最も効果的な種目のひとつ。軽い重量でも十分効果あり。肘を軽く曲げた状態で行う。',
  'ストレッチポール 背骨リセット（縦置き）':'ポールを頭から背骨に沿って縦に置き仰向けに乗る。重力で背骨・胸椎が自然に伸びる。猫背・巻き肩改善の基本。5〜10分乗るだけ。毎日やるのがおすすめ。',
  'フォームローラー 大腿四頭筋':'うつ伏せで太ももの前面をローラーの上に乗せてゆっくり転がす。膝への負担を軽減する効果あり。痛い部分では止めて圧をかけるとより効果的。',
  'フォームローラー 臀部ほぐし':'座位でローラーに臀部を乗せて片側ずつ体重をかけながら転がす。梨状筋・臀部の張りをほぐして腰痛改善に効果的。',

  'ルームランナー ウォーキング':'ルームランナーを傾斜1〜3°に設定して速歩きする。速度は4〜5km/h。膝・足首への衝撃を最小限に抑えながら有酸素運動ができる。走らないこと。脂肪燃焼・体力向上に最も安全な種目。',

};

function renderToday(){
  const up=duration===60?upperFull:upperShort;
  const lo=duration===60?lowerFull:lowerShort;
  const co=duration===60?coreFull:coreShort;
  renderExList('card-warmup',warmupData,'w',[]);
  renderExList('card-upper',up,'u',getCustomByCategory('upper'));
  renderExList('card-lower',lo,'l',getCustomByCategory('lower'));
  renderExList('card-core',[...co,...getCustomByCategory('ball')],'c',getCustomByCategory('core'));
  updateCounts();
  updateWeekDots();
}

function renderExList(id,data,prefix,extra){
  const all=[...data,...extra];
  let html=all.map((e,i)=>{
    const k=prefix+i;
    const done=checked[k];
    const isCustom=i>=data.length;
    const desc=exDescriptions[e.name]||null;
    return `<div class="ex-row" style="flex-wrap:wrap">
      <div style="display:flex;align-items:center;gap:10px;width:100%">
        <div class="ex-check${done?' done':''}" onclick="toggleEx('${k}',this)">${done?'✓':''}</div>
        <div class="ex-main">
          <div class="ex-name${done?' done':''}">${e.name}${isCustom?'<span class="custom-badge">追加</span>':''}</div>
          <div class="ex-detail">${e.detail}</div>
        </div>
        ${e.caution?`<div class="ex-caution">${e.caution}</div>`:''}
        ${desc?`<div onclick="toggleDesc('desc-${k}')" style="font-size:20px;color:var(--text3);cursor:pointer;padding:0 4px;flex-shrink:0" title="説明を見る">ℹ️</div>`:''}
      </div>
      ${desc?`<div id="desc-${k}" style="display:none;width:100%;margin-top:6px;padding:10px 12px;background:var(--surface2);border-radius:8px;border-left:3px solid var(--blue);font-size:13px;color:var(--text2);line-height:1.7">${desc}</div>`:''}
    </div>`;
  }).join('');
  document.getElementById(id).innerHTML=html;
}

function toggleDesc(id){
  const el=document.getElementById(id);
  if(!el)return;
  el.style.display=el.style.display==='none'?'block':'none';
}

function toggleEx(k,el){
  checked[k]=!checked[k];
  el.classList.toggle('done',checked[k]);
  el.textContent=checked[k]?'✓':'';
  const row=el.parentElement;
  const nm=row.querySelector('.ex-name');
  if(nm)nm.classList.toggle('done',checked[k]);
  updateCounts();
}

function updateCounts(){
  updateCategoryProgress();
}

function updateCategoryProgress(){
  const cats=[
    {id:'w', label:'ウォームアップ', icon:'🔥', data:warmupData},
    {id:'u', label:'上半身', icon:'💪', data:duration===60?upperFull:upperShort},
    {id:'l', label:'下半身', icon:'🦵', data:duration===60?lowerFull:lowerShort},
    {id:'c', label:'体幹・ボール', icon:'🏋️', data:duration===60?[...coreFull,...getCustomByCategory('ball')]:coreShort},
    {id:'s', label:'ストレッチ', icon:'🧘', data:[
      {name:'ストレッチポール 背骨リセット'},
      {name:'フォームローラー 大腿四頭筋ほぐし'},
      {name:'フォームローラー 背中・胸椎ほぐし'},
      {name:'フォームローラー 臀部ほぐし'},
    ]},
  ];

  // Count walk
  const walkDone = walkSec > 0;
  const walkTarget = 30 * 60;
  const walkPct = Math.min(100, Math.round((walkSec / walkTarget) * 100));

  let html = cats.map(cat => {
    const total = cat.data.length;
    const done = Array.from({length: total}, (_, i) => checked[cat.id + i]).filter(Boolean).length;
    const pct = total > 0 ? Math.round((done / total) * 100) : 0;
    const color = pct === 100 ? 'var(--green)' : pct > 0 ? 'var(--amber)' : 'var(--border)';
    return `<div style="margin-bottom:10px">
      <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:4px">
        <span style="font-size:15px;font-weight:600;color:var(--text)">${cat.icon} ${cat.label}</span>
        <span style="font-size:15px;font-weight:700;color:${color}">${done} / ${total}</span>
      </div>
      <div style="background:var(--surface2);border-radius:6px;height:10px;overflow:hidden">
        <div style="height:100%;border-radius:6px;background:${color};width:${pct}%;transition:width 0.3s"></div>
      </div>
    </div>`;
  }).join('');

  // Add walking row
  const walkColor = walkSec >= walkTarget ? 'var(--green)' : walkSec > 0 ? 'var(--amber)' : 'var(--border)';
  const walkMin = Math.floor(walkSec / 60);
  html += `<div style="margin-bottom:4px">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:4px">
      <span style="font-size:15px;font-weight:600;color:var(--text)">🚶 ウォーキング</span>
      <span style="font-size:15px;font-weight:700;color:${walkColor}">${walkMin} / 30 分</span>
    </div>
    <div style="background:var(--surface2);border-radius:6px;height:10px;overflow:hidden">
      <div style="height:100%;border-radius:6px;background:${walkColor};width:${walkPct}%;transition:width 0.3s"></div>
    </div>
  </div>`;

  // Stretch uses s0-s3 keys
  const stretchTotal = 4;
  const stretchDone = [0,1,2,3].filter(i => checked['s'+i]).length;
  const stretchPct = Math.round((stretchDone / stretchTotal) * 100);
  const stretchColor = stretchPct === 100 ? 'var(--green)' : stretchPct > 0 ? 'var(--amber)' : 'var(--border)';
  html += `<div style="margin-bottom:4px">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:4px">
      <span style="font-size:15px;font-weight:600;color:var(--text)">🧘 リカバリー</span>
      <span style="font-size:15px;font-weight:700;color:${stretchColor}">${stretchDone} / ${stretchTotal}</span>
    </div>
    <div style="background:var(--surface2);border-radius:6px;height:10px;overflow:hidden">
      <div style="height:100%;border-radius:6px;background:${stretchColor};width:${stretchPct}%;transition:width 0.3s"></div>
    </div>
  </div>`;

  const el = document.getElementById('categoryProgress');
  if(el) el.innerHTML = html;
}


function resetWeekCount(){
  if(!confirm('今週のカウントを0にリセットしますか？'))return;
  wkCnt=0;
  localStorage.setItem('hgWk','0');
  updateWeekDots();
  alert('✅ リセットしました！');
}

function updateWeekDots(){
  // week dots removed - now using category progress
}

function toggleWalk(){
  if(!walkOn){
    walkOn=true;
    document.getElementById('walkBtn').textContent='停止';
    document.getElementById('walkBtn').className='walk-btn walk-stop';
    walkIv=setInterval(()=>{walkSec++;updWalk();updateCategoryProgress();},1000);
  } else {
    walkOn=false;
    document.getElementById('walkBtn').textContent='再開';
    document.getElementById('walkBtn').className='walk-btn walk-start';
    clearInterval(walkIv);
  }
}
function resetWalk(){
  walkOn=false;clearInterval(walkIv);walkSec=0;
  document.getElementById('walkBtn').textContent='開始';
  document.getElementById('walkBtn').className='walk-btn walk-start';
  updWalk();
}
function updWalk(){
  const m=Math.floor(walkSec/60),s=walkSec%60;
  document.getElementById('walkTimer').textContent=pad(m)+':'+pad(s);
  const pct=Math.min(100,Math.round((walkSec/1800)*100));
  document.getElementById('walkBar').style.width=pct+'%';
}
function pad(n){return String(n).padStart(2,'0');}

function completeWorkout(){
  wkCnt=Math.min(5,wkCnt+1);
  localStorage.setItem('hgWk',String(wkCnt));

  // 今日のメモを思い出しノートに日付つきで追記
  const memo=document.getElementById('todayNotes').value.trim();
  if(memo){
    const now=new Date();
    const dateStr=now.getFullYear()+'年'+(now.getMonth()+1)+'月'+now.getDate()+'日（'+['日','月','火','水','木','金','土'][now.getDay()]+'）';
    const existing=localStorage.getItem('hgNote')||'';
    const newEntry='【'+dateStr+'】\n'+memo;
    const updated=newEntry+(existing?'\n\n'+existing:'');
    localStorage.setItem('hgNote',updated);
  }

  checked={};renderToday();resetWalk();
  document.getElementById('todayNotes').value='';
  updateWeekDots();
  alert('✅ 今日のトレーニング終了！\nお疲れ様でした！💪'+(memo?'\n\nメモを思い出しノートに保存しました':''));
}

let weekOffset=0;
function changeWeek(dir){
  const next=weekOffset+dir;
  if(next<-1||next>1){
    alert(next<0?'1週前までしか遡れません':'1週先までしか進めません');
    return;
  }
  weekOffset=next;
  renderWeekGrid();
}
function renderWeekGrid(){
  const today=new Date();
  const dow=today.getDay();
  // 今週の月曜日を基準にoffset週分ずらす
  const monday=new Date(today);
  monday.setDate(today.getDate()-dow+(dow===0?-6:1)+weekOffset*7);

  const labels=['休養','上半身','下半身','体幹','上半身','下半身','歩行'];
  const types=['rest','upper','lower','core','upper','lower','walk'];

  // 週ラベル
  const weekStart=new Date(monday);
  const weekEnd=new Date(monday);weekEnd.setDate(monday.getDate()+6);
  const isCurrent=weekOffset===0;
  const isPast=weekOffset<0;
  const label=isCurrent?'今週':(isPast?`${Math.abs(weekOffset)}週前`:`${weekOffset}週後`);
  document.getElementById('weekLabel').innerHTML=
    `${label}<br><span style="font-size:12px;font-weight:500">${weekStart.getMonth()+1}/${weekStart.getDate()}（月）〜 ${weekEnd.getMonth()+1}/${weekEnd.getDate()}（日）</span>`;
  // ボタンの有効・無効を更新
  const btnPrev=document.getElementById('btnPrev');
  const btnNext=document.getElementById('btnNext');
  if(btnPrev){btnPrev.style.opacity=weekOffset<=-1?'0.3':'1';btnPrev.style.cursor=weekOffset<=-1?'not-allowed':'pointer';}
  if(btnNext){btnNext.style.opacity=weekOffset>=1?'0.3':'1';btnNext.style.cursor=weekOffset>=1?'not-allowed':'pointer';}

  let h='';
  DAYS_JP.forEach((d,i)=>{
    // i=0が日曜なので月曜起点に並べ直す
    const dayIndex=(i+1)%7; // 月=0,火=1,...,日=6
    const dt=new Date(monday);dt.setDate(monday.getDate()+i);
    const isToday=isCurrent&&dt.toDateString()===today.toDateString();
    const isRest=(i===5||i===6);
    const cls=isToday?'today':(isRest?'rest':'');
    const dayLabel=['月','火','水','木','金','土','日'][i];
    h+=`<div class="day-cell ${cls}" onclick="showDayDetail(${i},'${dt.getMonth()+1}/${dt.getDate()}')">
      <div class="day-name">${dayLabel}</div>
      <div class="day-num">${dt.getDate()}</div>
      <div class="day-type">${labels[(i+1)%7]}</div>
    </div>`;
  });
  document.getElementById('weekGrid').innerHTML=h;
  document.getElementById('dayDetail').innerHTML='';
}

const dayPrograms=[
  {label:'上半身A + 体幹',icon:'💪',dur:'60分',desc:'胸・背中中心。ダンベル＋BARWINGマシン',cats:['upper','core']},
  {label:'下半身A + ウォーキング',icon:'🦵',dur:'60分',desc:'大腿四頭筋・臀部。低衝撃スクワット',cats:['lower','walk']},
  {label:'体幹 + バランスボール',icon:'🔥',dur:'30分',desc:'軽め。姿勢改善・腰痛予防・バランスボール',cats:['core','ball','roller','stretch']},
  {label:'上半身B + ディップス',icon:'💪',dur:'60分',desc:'肩・腕・背中。ディップス・ネガティブ懸垂',cats:['upper','dips']},
  {label:'下半身B + ウォーキング',icon:'🦵',dur:'60分',desc:'ふくらはぎ・臀部・体幹の複合',cats:['lower','band','mball']},
  {label:'完全休養',icon:'😴',dur:'休み',desc:'畑仕事もOK！軽いストレッチ推奨',cats:[]},
  {label:'ウォーキングのみ（任意）',icon:'🚶',dur:'30分',desc:'ルームランナーでリカバリー歩行',cats:['walk']},
];

function showDayDetail(dayIdx, dateStr){
  const prog=dayPrograms[dayIdx];
  const relatedCats=prog.cats;
  const customForDay=customExercises.filter(e=>relatedCats.includes(e.cat));

  // 標準種目を組み立て
  const allExercises=[];
  if(relatedCats.includes('upper')){upperFull.forEach(e=>allExercises.push({...e,group:'上半身'}));}
  if(relatedCats.includes('lower')){lowerFull.forEach(e=>allExercises.push({...e,group:'下半身'}));}
  if(relatedCats.includes('core')){coreFull.forEach(e=>allExercises.push({...e,group:'体幹'}));}
  if(relatedCats.includes('walk')){allExercises.push({name:'ルームランナー ウォーキング',detail:'30〜60分 速度4〜5km/h',caution:'走らない',group:'ウォーキング'});}
  customForDay.forEach(e=>allExercises.push({...e,group:'追加種目'}));

  const exHtml=allExercises.map(e=>`
    <div style="display:flex;align-items:center;gap:10px;padding:7px 0;border-top:1px solid var(--border)">
      <div style="font-size:11px;padding:2px 7px;border-radius:5px;background:var(--surface2);color:var(--text3);white-space:nowrap;font-weight:600">${e.group}</div>
      <div style="flex:1">
        <div style="font-size:14px;color:var(--text);font-weight:500">${e.name}</div>
        <div style="font-size:12px;color:var(--text3)">${e.detail}</div>
      </div>
      ${e.caution?`<div style="font-size:11px;color:var(--coral-dark);background:var(--coral-light);padding:2px 7px;border-radius:5px;font-weight:600;white-space:nowrap">${e.caution}</div>`:''}
    </div>`).join('');

  document.getElementById('dayDetail').innerHTML=`
    <div style="background:var(--surface);border:1.5px solid var(--green);border-radius:var(--radius-lg);padding:16px 18px;margin-top:10px">
      <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px">
        <div>
          <div style="font-size:13px;color:var(--text3);font-weight:600">${dateStr} の予定</div>
          <div style="font-size:16px;font-weight:700;color:var(--text);margin-top:2px">${prog.icon} ${prog.label}</div>
        </div>
        <span style="font-size:13px;padding:5px 12px;background:var(--green-light);color:var(--green-dark);border-radius:8px;font-weight:700">⏱ ${prog.dur}</span>
      </div>
      ${exHtml.length>0?exHtml:`<div style="font-size:14px;color:var(--text3);text-align:center;padding:16px">休養日 — しっかり休みましょう！</div>`}
      ${customForDay.length>0?`<div style="margin-top:10px;padding:8px 12px;background:var(--purple-light);border-radius:8px;font-size:12px;color:var(--purple-dark);font-weight:600">➕ 追加種目 ${customForDay.length}件含む</div>`:''}
    </div>`;
}

function renderWeeklyProg(){
  const colors={upper:'prog-upper',lower:'prog-lower',core:'prog-core',walk:'prog-walk',rest:'prog-rest'};
  // カテゴリーと曜日のマッピング
  // 月(1)=upper, 火(2)=lower, 水(3)=core/ball/roller/stretch, 木(4)=upper+dips, 金(5)=lower+band, 土(6)=rest, 日(0)=walk
  const catToDays={
    upper:[0,3],lower:[1,4],core:[2],ball:[2],mball:[1,4],
    dips:[3],roller:[2],band:[1,4],stretch:[0,1,2,3,4],walk:[6]
  };
  const dayNames=['日','月','火','水','木','金','土'];

  document.getElementById('weeklyProg').innerHTML=weeklyData.map((p,idx)=>{
    // 対応カテゴリーのカスタム種目を取得
    const relatedCats=Object.keys(catToDays).filter(cat=>catToDays[cat].includes(idx));
    const customForDay=customExercises.filter(e=>relatedCats.includes(e.cat));
    const customHtml=customForDay.length>0
      ?`<div style="margin-top:8px;padding:6px 10px;background:var(--purple-light);border-radius:8px">
          <div style="font-size:11px;font-weight:700;color:var(--purple-dark);margin-bottom:4px">➕ 追加種目</div>
          ${customForDay.map(e=>`<div style="font-size:12px;color:var(--purple-dark);padding:2px 0">・${e.name}（${e.detail}）</div>`).join('')}
        </div>`
      :'';
    return `<div class="program-row">
      <div class="prog-icon ${colors[p.type]}">${p.icon}</div>
      <div class="prog-content">
        <div class="prog-day">${p.day}</div>
        <div class="prog-name">${p.label}</div>
        <div class="prog-desc">${p.desc}</div>
        <div class="prog-time">⏱ ${p.dur}</div>
        ${customHtml}
      </div>
    </div>`;
  }).join('');
  document.getElementById('injuryBox').innerHTML=injuryItems.map(t=>`<div class="injury-item">${t}</div>`).join('');
}

function renderLibrary(cat){
  const allData=[...libraryData,...customExercises.map(e=>({...e,tags:[e.cat==='upper'?'上半身':e.cat==='lower'?'下半身':e.cat==='ball'?'バランスボール':'体幹','追加種目']}))];
  const data=cat==='all'?allData:allData.filter(e=>e.cat===cat);
  const tc={upper:'tag-upper',lower:'tag-lower',core:'tag-core',walk:'tag-walk',ball:'tag-ball',mball:'tag-mball',dips:'tag-dips',roller:'tag-roller',band:'tag-band',stretch:'tag-stretch'};
  const bc={upper:'badge-blue',lower:'badge-green',core:'badge-amber',walk:'badge-purple',ball:'badge-green',mball:'badge-amber',dips:'badge-blue',roller:'badge-amber',band:'badge-purple',stretch:'badge-green'};
  const bl={upper:'上半身',lower:'下半身',core:'体幹',walk:'歩行',ball:'ボール',mball:'ウエイトB',dips:'ディップス',roller:'腹筋ローラー',band:'ヒップバンド',stretch:'ストレッチ'};
  let html=`<div class="add-section">
    <div class="add-title">➕ 種目を追加する</div>
    <div class="add-form">
      <input class="add-input" id="newName" placeholder="種目名（例：ダンベルフライ）" style="grid-column:1/-1">
      <input class="add-input" id="newDetail" placeholder="セット数・回数（例：3セット×12回）">
      <input class="add-input" id="newCaution" placeholder="注意点（任意）">
      <select class="add-select" id="newCat">
        <option value="upper">上半身</option>
        <option value="lower">下半身</option>
        <option value="core">体幹</option>
        <option value="ball">バランスボール</option>
        <option value="mball">ウエイトボール</option>
        <option value="dips">ディップス・懸垂</option>
        <option value="roller">腹筋ローラー</option>
        <option value="band">ヒップバンド</option>
        <option value="stretch">ストレッチ・リカバリー</option>
      </select>
      <button class="add-btn" onclick="addExercise()">追加する</button>
    </div>
  </div>`;
  html+=data.map((e,idx)=>{
    const isCustom=idx>=libraryData.length||(e.tags&&e.tags.includes('追加種目'));
    return `<div class="lib-card">
      <div class="lib-header">
        <div class="lib-name">${e.name}${isCustom?'<span class="custom-badge">追加</span>':''}</div>
        <span class="badge ${bc[e.cat]||'badge-blue'}">${bl[e.cat]||e.cat}</span>
      </div>
      <div class="lib-tags">${(e.tags||[]).map(t=>`<span class="tag ${tc[e.cat]||'tag-upper'}">${t}</span>`).join('')}</div>
      <div class="lib-desc">${e.desc||''}</div>
      <div class="lib-sets">📋 ${e.sets||e.detail||''}</div>
      ${isCustom?`<button onclick="removeCustomEx(${customExercises.indexOf(e)})" style="margin-top:8px;padding:6px 12px;background:var(--coral-light);color:var(--coral-dark);border:none;border-radius:6px;font-size:12px;font-weight:700;cursor:pointer">削除</button>`:''}
    </div>`;
  }).join('');
  document.getElementById('libList').innerHTML=html;
}

function addExercise(){
  const name=document.getElementById('newName').value.trim();
  const detail=document.getElementById('newDetail').value.trim();
  const caution=document.getElementById('newCaution').value.trim();
  const cat=document.getElementById('newCat').value;
  if(!name){alert('種目名を入力してください');return;}
  customExercises.push({name,detail:detail||'記録なし',caution:caution||null,cat,sets:detail||'記録なし',desc:'追加した種目です',tags:[cat==='upper'?'上半身':cat==='lower'?'下半身':cat==='ball'?'バランスボール':'体幹','追加種目']});
  localStorage.setItem('hgCustomEx',JSON.stringify(customExercises));
  renderLibrary('all');
  renderToday();
  alert('✅ 種目を追加しました！');
}

function removeCustomEx(idx){
  if(!confirm('この種目を削除しますか？'))return;
  customExercises.splice(idx,1);
  localStorage.setItem('hgCustomEx',JSON.stringify(customExercises));
  renderLibrary('all');renderToday();
}

function filterLib(cat,btn){
  document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('sel'));
  btn.classList.add('sel');
  renderLibrary(cat);
}



function switchTab(name,tabId){
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  document.getElementById('panel-'+name).classList.add('active');
  document.getElementById(tabId).classList.add('active');
  if(name==='schedule'){renderWeekGrid();renderWeeklyProg();}
  if(name==='mypage')renderMypage();
  if(name==='library')renderLibrary('all');
}


// ===== MYPAGE =====
const bodyParts=[
  {id:'knee',label:'両膝靭帯',icon:'🦵'},
  {id:'ankle',label:'足首',icon:'🦶'},
  {id:'back',label:'腰',icon:'🔙'},
  {id:'shoulder',label:'肩・首',icon:'💆'},
  {id:'elbow',label:'肘',icon:'💪'},
  {id:'wrist',label:'手首',icon:'🤲'},
];
const goalItems=[
  {id:'weight',label:'体重',unit:'kg'},
  {id:'fat',label:'体脂肪率',unit:'%'},
  {id:'muscle',label:'筋肉量',unit:'kg'},
  {id:'pullup',label:'懸垂回数',unit:'回'},
];
const equipData=[
  {cat:'ダンベル',items:'4kg / 7kg / 10kg / 15kg / 17kg / 20kg'},
  {cat:'ケトルベル',items:'8kg / 12kg / 16kg'},
  {cat:'マシン',items:'BARWINGマシン / ルームランナー'},
  {cat:'器具',items:'可変式トレーニングベンチ / 懸垂マシン＋ディップススタンド'},
  {cat:'ボール類',items:'バランスボール10kg / ウエイトボール10kg'},
  {cat:'ケア用品',items:'フォームローラー / ストレッチポール'},
  {cat:'バンド',items:'ヒップバンド（軽・中・強）/ 腹筋ローラー'},
];

function renderBodyCheck(){
  const today=new Date().toDateString();
  const saved=JSON.parse(localStorage.getItem('hgBody')||'{}');
  const savedDate=localStorage.getItem('hgBodyDate')||'';
  const data=savedDate===today?saved:{};
  const levels=[{v:0,label:'問題なし',color:'var(--green)'},{v:1,label:'違和感あり',color:'var(--amber)'},{v:2,label:'痛みあり',color:'var(--coral)'},{v:3,label:'強い痛み',color:'#cc2200'}];
  document.getElementById('bodyCheck').innerHTML=bodyParts.map(p=>{
    const cur=data[p.id]??0;
    return `<div style="display:flex;align-items:center;gap:10px;padding:8px 0;border-top:1px solid var(--border)">
      <div style="font-size:22px">${p.icon}</div>
      <div style="font-size:15px;font-weight:600;color:var(--text);width:60px">${p.label}</div>
      <div style="display:flex;gap:6px;flex:1">
        ${levels.map(l=>`<button onclick="setBody('${p.id}',${l.v})" style="flex:1;padding:8px 2px;border-radius:8px;border:2px solid ${cur===l.v?l.color:'var(--border2)'};background:${cur===l.v?l.color+'22':'transparent'};color:${cur===l.v?l.color:'var(--text3)'};font-size:12px;font-weight:700;cursor:pointer">${l.label}</button>`).join('')}
      </div>
    </div>`;
  }).join('');
}

function setBody(id,val){
  const today=new Date().toDateString();
  const saved=JSON.parse(localStorage.getItem('hgBody')||'{}');
  const savedDate=localStorage.getItem('hgBodyDate')||'';
  const data=savedDate===today?saved:{};
  data[id]=val;
  localStorage.setItem('hgBody',JSON.stringify(data));
  localStorage.setItem('hgBodyDate',today);
  renderBodyCheck();
}

function renderWeightMemo(){
  const memos=JSON.parse(localStorage.getItem('hgWeightMemo')||'[]');
  const el=document.getElementById('weightMemoList');
  if(!memos.length){el.innerHTML='<div style="font-size:13px;color:var(--text3)">まだ記録がありません</div>';return;}
  el.innerHTML=memos.map((m,i)=>`
    <div style="display:flex;align-items:center;gap:10px;padding:8px 0;border-top:1px solid var(--border)">
      <div style="flex:1;font-size:15px;color:var(--text);font-weight:500">${m.name}</div>
      <div style="font-size:18px;font-weight:700;color:var(--blue-dark)">${m.kg}kg</div>
      <button onclick="removeWeightMemo(${i})" style="padding:5px 10px;background:var(--coral-light);color:var(--coral-dark);border:none;border-radius:6px;font-size:12px;font-weight:700;cursor:pointer">削除</button>
    </div>`).join('');
}

function addWeightMemo(){
  const name=document.getElementById('wName').value.trim();
  const kg=document.getElementById('wKg').value.trim();
  if(!name||!kg){alert('種目名と重量を入力してください');return;}
  const memos=JSON.parse(localStorage.getItem('hgWeightMemo')||'[]');
  const existing=memos.findIndex(m=>m.name===name);
  if(existing>=0)memos[existing].kg=kg;
  else memos.push({name,kg});
  localStorage.setItem('hgWeightMemo',JSON.stringify(memos));
  document.getElementById('wName').value='';
  document.getElementById('wKg').value='';
  renderWeightMemo();
}

function removeWeightMemo(i){
  const memos=JSON.parse(localStorage.getItem('hgWeightMemo')||'[]');
  memos.splice(i,1);
  localStorage.setItem('hgWeightMemo',JSON.stringify(memos));
  renderWeightMemo();
}

function saveNote(){
  const note=document.getElementById('noteArea').value;
  localStorage.setItem('hgNote',note);
  alert('✅ 保存しました！');
}

function loadNote(){
  const note=localStorage.getItem('hgNote')||'';
  const el=document.getElementById('noteArea');
  if(el)el.value=note;
}

function renderGoals(){
  const goals=JSON.parse(localStorage.getItem('hgGoals')||'{}');
  document.getElementById('goalList').innerHTML=goalItems.map(g=>`
    <div style="display:flex;align-items:center;gap:10px;padding:8px 0;border-top:1px solid var(--border)">
      <div style="font-size:14px;font-weight:600;color:var(--text);width:80px">${g.label}</div>
      <div style="flex:1;display:flex;gap:6px;align-items:center">
        <input type="number" placeholder="現在" value="${goals[g.id+'_cur']||''}" onchange="saveGoal('${g.id}_cur',this.value)" style="width:70px;padding:8px;border:1px solid var(--border2);border-radius:8px;background:var(--surface2);color:var(--text);font-size:14px;text-align:center">
        <span style="color:var(--text3);font-size:13px">→ 目標</span>
        <input type="number" placeholder="目標" value="${goals[g.id+'_goal']||''}" onchange="saveGoal('${g.id}_goal',this.value)" style="width:70px;padding:8px;border:1px solid var(--green);border-radius:8px;background:var(--green-light);color:var(--green-dark);font-size:14px;text-align:center">
        <span style="color:var(--text3);font-size:13px">${g.unit}</span>
      </div>
    </div>`).join('');
}

function saveGoal(key,val){
  const goals=JSON.parse(localStorage.getItem('hgGoals')||'{}');
  goals[key]=val;
  localStorage.setItem('hgGoals',JSON.stringify(goals));
}

// 器具ごとの種目マッピング
const equipExercises={
  'ダンベル':[
    {name:'ダンベル チェストプレス',detail:'10kg × 3セット × 10回',cat:'upper',day:'月・木'},
    {name:'ダンベル インクラインプレス',detail:'10kg × 3セット × 10回',cat:'upper',day:'月・木'},
    {name:'ダンベル フライ',detail:'10kg × 3セット × 12回',cat:'upper',day:'月・木'},
    {name:'ダンベル ロウ',detail:'15kg × 3セット × 10回',cat:'upper',day:'月・木'},
    {name:'ダンベル ショルダープレス',detail:'7kg × 3セット × 12回',cat:'upper',day:'月・木'},
    {name:'サイドレイズ',detail:'7kg × 3セット × 15回',cat:'upper',day:'木'},
    {name:'フロントレイズ',detail:'7kg × 3セット × 12回',cat:'upper',day:'木'},
    {name:'リアレイズ',detail:'7kg × 3セット × 15回',cat:'upper',day:'木'},
    {name:'ハンマーカール',detail:'10kg × 3セット × 12回',cat:'upper',day:'木'},
    {name:'コンセントレーションカール',detail:'10kg × 3セット × 10回',cat:'upper',day:'木'},
    {name:'トライセプスエクステンション',detail:'7kg × 3セット × 12回',cat:'upper',day:'木'},
    {name:'ダンベル キックバック（三頭筋）',detail:'7kg × 3セット × 12回',cat:'upper',day:'木'},
    {name:'ヒップヒンジ / RDL',detail:'15kg × 3セット × 10回',cat:'lower',day:'火・金'},
    {name:'ハーフスクワット（ダンベル）',detail:'10kg × 3セット × 12回',cat:'lower',day:'火・金'},
    {name:'ヒップスラスト（ベンチ）',detail:'17kg × 3セット × 12回',cat:'lower',day:'火・金'},
  ],
  'ケトルベル':[
    {name:'ケトルベルスイング',detail:'12kg × 3セット × 15回',cat:'upper',day:'月・木'},
    {name:'ケトルベル ゴブレットスクワット',detail:'12kg × 3セット × 12回',cat:'lower',day:'火・金'},
    {name:'ケトルベル デッドリフト',detail:'16kg × 3セット × 10回',cat:'lower',day:'火・金'},
  ],
  'BARWINGマシン':[
    {name:'フェイスプル',detail:'3セット × 15回',cat:'upper',day:'月・木'},
    {name:'レッグエクステンション',detail:'3セット × 15回',cat:'lower',day:'火・金'},
    {name:'ケーブルロウ',detail:'3セット × 12回',cat:'upper',day:'月・木'},
    {name:'ラットプルダウン',detail:'3セット × 10回',cat:'upper',day:'月・木'},
  ],
  'ルームランナー':[
    {name:'ウォーキング（傾斜1〜3°）',detail:'30〜60分 速度4〜5km/h',cat:'walk',day:'火・金・日'},
  ],
  'トレーニングベンチ':[
    {name:'ダンベル チェストプレス',detail:'10kg × 3セット × 10回',cat:'upper',day:'月・木'},
    {name:'ダンベル インクラインプレス',detail:'10kg × 3セット × 10回',cat:'upper',day:'月・木'},
    {name:'ヒップスラスト（ベンチ）',detail:'17kg × 3セット × 12回',cat:'lower',day:'火・金'},
    {name:'ダンベル ロウ（片手）',detail:'15kg × 3セット × 10回',cat:'upper',day:'月・木'},
  ],
  '懸垂マシン＋ディップス':[
    {name:'アシスト懸垂',detail:'補助つき × 3セット × 5回',cat:'dips',day:'木'},
    {name:'ネガティブ懸垂',detail:'3セット × 5回（5秒下ろす）',cat:'dips',day:'木'},
    {name:'ディップス',detail:'自重 × 3セット × 5〜8回',cat:'dips',day:'木'},
    {name:'ハンギングニーレイズ',detail:'3セット × 10〜15回',cat:'dips',day:'木'},
    {name:'L字ハング',detail:'15〜30秒 × 3セット',cat:'dips',day:'木'},
  ],
  'バランスボール':[
    {name:'バランスボール 体幹キープ（座位）',detail:'30秒 × 3セット',cat:'ball',day:'水'},
    {name:'バランスボール 腹筋ロール',detail:'3セット × 10回',cat:'ball',day:'水'},
    {name:'バランスボール ヒップリフト',detail:'3セット × 12回',cat:'ball',day:'水'},
    {name:'バランスボール 背中伸ばし',detail:'30秒 × 2セット',cat:'ball',day:'水'},
  ],
  'ウエイトボール':[
    {name:'メディシンボール スクワット',detail:'10kg × 3セット × 12回',cat:'mball',day:'火・金'},
    {name:'メディシンボール ロシアンツイスト',detail:'10kg × 3セット × 左右10回',cat:'mball',day:'火・金'},
    {name:'メディシンボール チェストパス',detail:'3セット × 10回',cat:'mball',day:'月・木'},
    {name:'メディシンボール デッドリフト',detail:'10kg × 3セット × 10回',cat:'mball',day:'火・金'},
  ],
  'フォームローラー':[
    {name:'フォームローラー 大腿四頭筋ほぐし',detail:'左右各60秒 × 2セット',cat:'stretch',day:'毎日'},
    {name:'フォームローラー 腸脛靭帯ほぐし',detail:'左右各60秒 × 2セット',cat:'stretch',day:'毎日'},
    {name:'フォームローラー 背中・胸椎ほぐし',detail:'60秒 × 2セット',cat:'stretch',day:'毎日'},
    {name:'フォームローラー 臀部ほぐし',detail:'左右各60秒 × 2セット',cat:'stretch',day:'毎日'},
  ],
  'ストレッチポール':[
    {name:'ストレッチポール 背骨リセット',detail:'5〜10分 乗るだけ',cat:'stretch',day:'毎日'},
    {name:'ストレッチポール 肩甲骨ほぐし',detail:'左右各30秒 × 3セット',cat:'stretch',day:'毎日'},
    {name:'ストレッチポール 腰椎ストレッチ',detail:'60秒 × 2セット',cat:'stretch',day:'毎日'},
    {name:'ストレッチポール 股関節ストレッチ',detail:'左右各30秒 × 3セット',cat:'stretch',day:'毎日'},
  ],
  'ヒップバンド':[
    {name:'バンド ヒップアブダクション横歩き',detail:'軽〜中 × 3セット × 左右15歩',cat:'band',day:'火・金'},
    {name:'バンド グルートブリッジ',detail:'中強度 × 3セット × 15回',cat:'band',day:'火・金'},
    {name:'バンド クラムシェル',detail:'軽〜中 × 3セット × 左右15回',cat:'band',day:'火・金'},
    {name:'バンド キックバック',detail:'中〜強 × 3セット × 左右12回',cat:'band',day:'火・金'},
  ],
  '腹筋ローラー':[
    {name:'膝つき腹筋ローラー（初級）',detail:'3セット × 8〜10回',cat:'roller',day:'水'},
    {name:'腹筋ローラー 壁あてロール',detail:'3セット × 10回',cat:'roller',day:'水'},
    {name:'腹筋ローラー サイドロール',detail:'左右各5回 × 3セット',cat:'roller',day:'水'},
  ],
};

function renderEquip(){
  document.getElementById('equipList').innerHTML=equipData.map(e=>`
    <div onclick="showEquipEx('${e.cat}')" style="display:flex;align-items:center;gap:12px;padding:10px 0;border-top:1px solid var(--border);cursor:pointer;transition:opacity 0.15s" onmousedown="this.style.opacity='0.7'" onmouseup="this.style.opacity='1'">
      <div style="font-size:12px;font-weight:700;color:var(--purple-dark);background:var(--purple-light);padding:4px 10px;border-radius:6px;white-space:nowrap">${e.cat}</div>
      <div style="flex:1;font-size:13px;color:var(--text2);line-height:1.5">${e.items}</div>
      <div style="font-size:18px;color:var(--text3)">›</div>
    </div>`).join('');
}

function showEquipEx(catName){
  // 器具名のキーを特定
  const keyMap={
    'ダンベル':'ダンベル','ケトルベル':'ケトルベル','マシン':'BARWINGマシン',
    '器具':'懸垂マシン＋ディップス','ボール類':'バランスボール',
    'ケア用品':'フォームローラー','バンド':'ヒップバンド'
  };
  // 直接キーを探す
  let exList=equipExercises[catName];
  if(!exList){
    // catNameに含まれるキーを探す
    for(const key of Object.keys(equipExercises)){
      if(catName.includes(key)||key.includes(catName)){exList=equipExercises[key];break;}
    }
  }
  if(!exList||!exList.length){
    alert('この器具の種目データはまだ追加されていません');return;
  }
  document.getElementById('equipModalTitle').textContent='📦 '+catName+' の種目';
  const catColors={upper:'var(--blue-light)',lower:'var(--green-light)',core:'var(--amber-light)',
    ball:'var(--green-light)',mball:'var(--amber-light)',dips:'var(--blue-light)',
    roller:'var(--amber-light)',band:'var(--purple-light)',stretch:'#0a2a2a',walk:'var(--purple-light)'};
  const catTextColors={upper:'var(--blue-dark)',lower:'var(--green-dark)',core:'var(--amber-dark)',
    ball:'var(--green-dark)',mball:'var(--amber-dark)',dips:'var(--blue-dark)',
    roller:'var(--amber-dark)',band:'var(--purple-dark)',stretch:'#60e0d0',walk:'var(--purple-dark)'};
  const catLabels={upper:'上半身',lower:'下半身',core:'体幹',ball:'バランス',
    mball:'ウエイト',dips:'ディップス',roller:'ローラー',band:'バンド',stretch:'ストレッチ',walk:'歩行'};

  document.getElementById('equipExList').innerHTML=exList.map(e=>{
    const alreadyAdded=customExercises.some(c=>c.name===e.name);
    return `<div style="display:flex;align-items:center;gap:10px;padding:10px 0;border-top:1px solid var(--border)">
      <div style="flex:1">
        <div style="font-size:14px;font-weight:600;color:var(--text)">${e.name}</div>
        <div style="font-size:12px;color:var(--text3);margin-top:2px">${e.detail}</div>
        <div style="display:flex;gap:6px;margin-top:4px">
          <span style="font-size:11px;padding:2px 7px;border-radius:5px;background:${catColors[e.cat]};color:${catTextColors[e.cat]};font-weight:600">${catLabels[e.cat]||e.cat}</span>
          <span style="font-size:11px;padding:2px 7px;border-radius:5px;background:var(--surface2);color:var(--text3)">📅 ${e.day}</span>
        </div>
      </div>
      ${alreadyAdded
        ?`<div style="padding:8px 14px;background:var(--surface2);color:var(--text3);border-radius:8px;font-size:12px;font-weight:700">追加済</div>`
        :`<button onclick="addFromEquip('${e.name.replace(/'/g,"\'")}','${e.detail.replace(/'/g,"\'")}','${e.cat}')" style="padding:8px 14px;background:var(--green);color:#fff;border:none;border-radius:8px;font-size:13px;font-weight:700;cursor:pointer;white-space:nowrap">＋ 追加</button>`
      }
    </div>`;
  }).join('');

  document.getElementById('equipExModal').style.display='block';
  document.getElementById('equipExModal').scrollIntoView({behavior:'smooth',block:'nearest'});
}

function addFromEquip(name,detail,cat){
  if(customExercises.some(c=>c.name===name)){alert('すでに追加されています');return;}
  customExercises.push({name,detail,caution:null,cat,sets:detail,desc:'設備一覧から追加した種目',tags:[cat,'追加種目']});
  localStorage.setItem('hgCustomEx',JSON.stringify(customExercises));
  renderToday();
  // ボタンを追加済みに変更
  showEquipEx(document.getElementById('equipModalTitle').textContent.replace('📦 ','').replace(' の種目',''));
  alert('✅ '+name+'\nをスケジュールに追加しました！');
}

function closeEquipModal(){
  document.getElementById('equipExModal').style.display='none';
}

function renderMypage(){
  renderBodyCheck();
  renderWeightMemo();
  loadNote();
  renderGoals();
  renderEquip();
}

function init(){
  checkNewWeek();
  const now=new Date();
  document.getElementById('dateDisplay').innerHTML=
    `${now.getFullYear()}年${now.getMonth()+1}月${now.getDate()}日（${DAYS_JP[now.getDay()]}）`;
  updateWeekDots();renderToday();
}
init();
</script>
</body>
</html>
