# CSO-Gym
[index.html](https://github.com/user-attachments/files/28371443/index.html)

<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<title>ホームジム トレーニング管理</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
body{font-family:-apple-system,'Hiragino Sans','Yu Gothic UI',sans-serif;background:#f4f3ef;min-height:100vh;color:#2c2c2a}
:root{
  --green:#1D9E75;--green-light:#E1F5EE;--green-dark:#085041;
  --amber:#BA7517;--amber-light:#FAEEDA;--amber-dark:#633806;
  --blue:#185FA5;--blue-light:#E6F1FB;--blue-dark:#0C447C;
  --coral:#993C1D;--coral-light:#FAECE7;--coral-dark:#4A1B0C;
  --purple:#534AB7;--purple-light:#EEEDFE;--purple-dark:#3C3489;
  --gray-light:#F1EFE8;--gray:#5F5E5A;
  --bg:#f4f3ef;--surface:#ffffff;--surface2:#f8f7f4;
  --border:#e0ddd6;--border2:#ccc9c0;
  --text:#2c2c2a;--text2:#5f5e5a;--text3:#888780;
  --radius:10px;--radius-lg:14px;--radius-xl:18px;
}
.app{display:flex;flex-direction:column;min-height:100vh;max-width:1024px;margin:0 auto}

/* HEADER */
.header{background:var(--surface);border-bottom:1px solid var(--border);padding:14px 20px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:100}
.header-left h1{font-size:18px;font-weight:600;color:var(--text)}
.header-left .sub{font-size:12px;color:var(--text3);margin-top:2px}
.header-right{font-size:12px;color:var(--text2);text-align:right;line-height:1.5}

/* TABS */
.tabs{display:flex;background:var(--surface);border-bottom:1px solid var(--border);padding:0 8px}
.tab{flex:1;padding:12px 6px;border:none;background:transparent;font-size:13px;font-weight:500;color:var(--text3);cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:3px;border-bottom:2.5px solid transparent;transition:all 0.15s}
.tab svg{width:20px;height:20px;stroke:currentColor;fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round}
.tab.active{color:var(--green);border-bottom-color:var(--green)}

/* CONTENT */
.content{padding:16px;flex:1;overflow-y:auto}
.panel{display:none}
.panel.active{display:block}

/* CARDS */
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:14px 16px;margin-bottom:12px}
.card-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px}
.card-title{font-size:14px;font-weight:600;color:var(--text)}
.badge{font-size:11px;padding:3px 9px;border-radius:6px;font-weight:500;white-space:nowrap}
.badge-green{background:var(--green-light);color:var(--green-dark)}
.badge-blue{background:var(--blue-light);color:var(--blue-dark)}
.badge-amber{background:var(--amber-light);color:var(--amber-dark)}
.badge-coral{background:var(--coral-light);color:var(--coral-dark)}
.badge-purple{background:var(--purple-light);color:var(--purple-dark)}

/* SECTION TITLE */
.sec-title{font-size:13px;font-weight:600;color:var(--text2);margin:16px 0 8px;display:flex;align-items:center;gap:6px}
.sec-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.dot-green{background:var(--green)}
.dot-blue{background:var(--blue)}
.dot-amber{background:var(--amber)}
.dot-purple{background:var(--purple)}
.dot-coral{background:var(--coral)}

/* STAT CARDS */
.stat-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:14px}
.stat-card{background:var(--surface2);border-radius:var(--radius);padding:12px;text-align:center;border:1px solid var(--border)}
.stat-label{font-size:11px;color:var(--text3);margin-bottom:4px}
.stat-value{font-size:26px;font-weight:700;color:var(--text);line-height:1}
.stat-unit{font-size:11px;color:var(--text3);margin-top:2px}

/* DURATION TOGGLE */
.dur-toggle{display:flex;gap:6px;margin-bottom:12px;align-items:center}
.dur-label{font-size:13px;color:var(--text2)}
.dur-btn{padding:7px 18px;border-radius:20px;border:1px solid var(--border2);background:transparent;font-size:13px;font-weight:500;cursor:pointer;color:var(--text2);transition:all 0.15s}
.dur-btn.sel{background:var(--blue);color:#fff;border-color:var(--blue)}

/* EXERCISE ROWS */
.ex-row{display:flex;align-items:center;gap:10px;padding:8px 0;border-top:1px solid var(--border)}
.ex-row:first-child{border-top:none}
.ex-check{width:24px;height:24px;border-radius:50%;border:1.5px solid var(--border2);cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;transition:all 0.2s;font-size:13px}
.ex-check.done{background:var(--green);border-color:var(--green);color:#fff}
.ex-main{flex:1;min-width:0}
.ex-name{font-size:13px;color:var(--text);line-height:1.3}
.ex-name.done{text-decoration:line-through;color:var(--text3)}
.ex-detail{font-size:11px;color:var(--text3);margin-top:2px}
.ex-caution{font-size:10px;color:var(--coral);background:var(--coral-light);padding:2px 6px;border-radius:4px;white-space:nowrap;flex-shrink:0}

/* WALK SECTION */
.walk-meta{font-size:12px;color:var(--text3);margin-bottom:10px}
.walk-controls{display:flex;align-items:center;gap:12px;margin-bottom:10px}
.walk-timer{font-size:32px;font-weight:700;color:var(--text);min-width:90px;font-variant-numeric:tabular-nums}
.walk-btn{padding:10px 20px;border-radius:var(--radius);border:none;font-size:14px;font-weight:600;cursor:pointer}
.walk-start{background:var(--green);color:#fff}
.walk-stop{background:var(--coral);color:#fff}
.walk-reset{background:var(--surface2);color:var(--text2);border:1px solid var(--border)}
.progress-wrap{background:var(--surface2);border-radius:4px;height:8px;overflow:hidden;margin-bottom:6px}
.progress-bar{height:100%;background:var(--green);border-radius:4px;transition:width 0.5s}
.walk-note{font-size:11px;color:var(--text3)}

/* NOTES */
.notes-area{width:100%;border:1px solid var(--border);border-radius:var(--radius);padding:10px 12px;font-size:13px;font-family:inherit;color:var(--text);background:var(--surface);resize:vertical;min-height:80px;margin-top:6px}
.notes-area:focus{outline:none;border-color:var(--green)}

/* COMPLETE BTN */
.complete-btn{width:100%;padding:14px;background:var(--green);color:#fff;border:none;border-radius:var(--radius);font-size:15px;font-weight:600;cursor:pointer;margin-top:12px;display:flex;align-items:center;justify-content:center;gap:8px}
.complete-btn:active{opacity:0.85;transform:scale(0.99)}

/* SCHEDULE */
.week-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:5px;margin-bottom:16px}
.day-cell{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:7px 3px;text-align:center;cursor:pointer}
.day-cell.today{border:2px solid var(--green);background:var(--green-light)}
.day-cell.rest{background:var(--surface2)}
.day-name{font-size:10px;color:var(--text3);margin-bottom:3px}
.day-num{font-size:15px;font-weight:600;color:var(--text)}
.day-type{font-size:9px;margin-top:3px;padding:2px 3px;border-radius:3px;line-height:1.2}
.day-cell.today .day-type{background:var(--green);color:#fff}
.day-cell.rest .day-type{background:var(--gray-light);color:var(--gray)}
.day-type-normal{background:#e8f0fb;color:var(--blue-dark)}

.program-row{display:flex;align-items:flex-start;gap:12px;padding:10px 0;border-top:1px solid var(--border)}
.program-row:first-child{border-top:none}
.prog-icon{width:38px;height:38px;border-radius:var(--radius);display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0}
.prog-upper{background:var(--blue-light)}
.prog-lower{background:var(--green-light)}
.prog-core{background:var(--amber-light)}
.prog-walk{background:var(--purple-light)}
.prog-rest{background:var(--gray-light)}
.prog-content{flex:1}
.prog-day{font-size:12px;color:var(--text3)}
.prog-name{font-size:14px;font-weight:600;color:var(--text);margin:1px 0 3px}
.prog-desc{font-size:12px;color:var(--text2);line-height:1.4}
.prog-time{font-size:11px;color:var(--text3);margin-top:3px}

.injury-box{background:var(--coral-light);border:1px solid #f0997b;border-radius:var(--radius-lg);padding:14px 16px}
.injury-item{font-size:13px;color:var(--coral-dark);padding:4px 0;line-height:1.5}

/* LIBRARY */
.filter-row{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:12px}
.filter-btn{padding:7px 14px;border-radius:20px;border:1px solid var(--border2);background:transparent;font-size:12px;cursor:pointer;color:var(--text2);transition:all 0.15s}
.filter-btn.sel{background:var(--text);color:#fff;border-color:var(--text)}
.lib-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:14px 16px;margin-bottom:10px}
.lib-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:6px}
.lib-name{font-size:14px;font-weight:600;color:var(--text)}
.lib-tags{display:flex;gap:4px;flex-wrap:wrap;margin-bottom:6px}
.tag{font-size:10px;padding:2px 7px;border-radius:4px}
.tag-upper{background:var(--blue-light);color:var(--blue-dark)}
.tag-lower{background:var(--green-light);color:var(--green-dark)}
.tag-core{background:var(--amber-light);color:var(--amber-dark)}
.tag-walk{background:var(--purple-light);color:var(--purple-dark)}
.tag-caution{background:var(--coral-light);color:var(--coral-dark)}
.lib-desc{font-size:12px;color:var(--text2);line-height:1.5}
.lib-sets{font-size:12px;color:var(--text);font-weight:600;margin-top:6px}

/* HISTORY */
.hist-entry{background:var(--surface);border:1px solid var(--border);border-radius:var(--radius-lg);padding:14px 16px;margin-bottom:10px}
.hist-date{font-size:11px;color:var(--text3)}
.hist-title{font-size:15px;font-weight:600;color:var(--text);margin:3px 0 6px}
.hist-stats{display:flex;gap:14px;flex-wrap:wrap}
.hist-stat{font-size:12px;color:var(--text2)}
.stars{display:flex;gap:3px;margin-top:8px;align-items:center}
.star{font-size:22px;cursor:pointer;color:#d3d1c7;transition:color 0.1s}
.star.filled{color:#EF9F27}
.star-label{font-size:11px;color:var(--text3);margin-left:4px}
.hist-note{font-size:12px;color:var(--text2);margin-top:8px;padding:8px 10px;background:var(--surface2);border-radius:var(--radius);line-height:1.5}
.empty{text-align:center;padding:48px 16px;color:var(--text3)}
.empty-icon{font-size:48px;margin-bottom:12px}
.empty-text{font-size:14px}

/* WEEK PROGRESS */
.week-dots{display:flex;gap:6px;margin-top:6px}
.week-dot{width:12px;height:12px;border-radius:50%;background:var(--border);border:1px solid var(--border2)}
.week-dot.done{background:var(--green);border-color:var(--green)}

@media(max-width:600px){
  .header{padding:12px 14px}
  .content{padding:12px}
  .walk-timer{font-size:26px}
}
</style>
</head>
<body>
<div class="app">

<!-- HEADER -->
<div class="header">
  <div class="header-left">
    <h1>🏋️ ホームジム トレーニング</h1>
    <div class="sub">怪我に配慮した自宅プログラム</div>
  </div>
  <div class="header-right" id="dateDisplay"></div>
</div>

<!-- TABS -->
<div class="tabs">
  <button class="tab active" onclick="switchTab('today','tab0')" id="tab0">
    <svg viewBox="0 0 24 24"><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg>
    今日
  </button>
  <button class="tab" onclick="switchTab('schedule','tab1')" id="tab1">
    <svg viewBox="0 0 24 24"><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/><line x1="8" y1="14" x2="8" y2="14" stroke-width="2"/><line x1="12" y1="14" x2="12" y2="14" stroke-width="2"/><line x1="16" y1="14" x2="16" y2="14" stroke-width="2"/></svg>
    週間
  </button>
  <button class="tab" onclick="switchTab('library','tab2')" id="tab2">
    <svg viewBox="0 0 24 24"><line x1="8" y1="6" x2="21" y2="6"/><line x1="8" y1="12" x2="21" y2="12"/><line x1="8" y1="18" x2="21" y2="18"/><circle cx="3" cy="6" r="1" fill="currentColor"/><circle cx="3" cy="12" r="1" fill="currentColor"/><circle cx="3" cy="18" r="1" fill="currentColor"/></svg>
    種目
  </button>
  <button class="tab" onclick="switchTab('history','tab3')" id="tab3">
    <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>
    記録
  </button>
</div>

<div class="content">

<!-- TODAY -->
<div class="panel active" id="panel-today">
  <div class="stat-grid">
    <div class="stat-card">
      <div class="stat-label">今週のトレーニング</div>
      <div class="stat-value" id="weekCount">0</div>
      <div class="stat-unit">/ 5 回</div>
      <div class="week-dots" id="weekDots"></div>
    </div>
    <div class="stat-card">
      <div class="stat-label">今日の完了種目</div>
      <div class="stat-value" id="doneCount">0</div>
      <div class="stat-unit">種目完了</div>
    </div>
  </div>

  <div class="dur-toggle">
    <span class="dur-label">今日の時間：</span>
    <button class="dur-btn sel" id="dur60" onclick="setDuration(60)">60分</button>
    <button class="dur-btn" id="dur30" onclick="setDuration(30)">30分</button>
  </div>

  <div class="sec-title"><span class="sec-dot dot-amber"></span>ウォームアップ（5分）</div>
  <div class="card" id="card-warmup"></div>

  <div class="sec-title"><span class="sec-dot dot-blue"></span>上半身トレーニング <span class="badge badge-blue" style="margin-left:auto">猫背改善対応</span></div>
  <div class="card" id="card-upper"></div>

  <div class="sec-title"><span class="sec-dot dot-green"></span>下半身トレーニング <span class="badge badge-green" style="margin-left:auto">膝・足首配慮</span></div>
  <div class="card" id="card-lower"></div>

  <div class="sec-title"><span class="sec-dot dot-amber"></span>体幹トレーニング <span class="badge badge-amber" style="margin-left:auto">腰痛配慮</span></div>
  <div class="card" id="card-core"></div>

  <!-- WALKING -->
  <div class="sec-title"><span class="sec-dot dot-purple"></span>ウォーキング（別メニュー）</div>
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

  <div class="sec-title"><span class="sec-dot" style="background:var(--text3)"></span>今日のメモ</div>
  <textarea class="notes-area" id="todayNotes" placeholder="体調・痛みの具合・使用重量など..."></textarea>

  <button class="complete-btn" onclick="completeWorkout()">✓ トレーニング完了として記録する</button>
</div>

<!-- SCHEDULE -->
<div class="panel" id="panel-schedule">
  <div class="sec-title" style="margin-top:0"><span class="sec-dot dot-green"></span>今週のカレンダー</div>
  <div class="week-grid" id="weekGrid"></div>

  <div class="sec-title"><span class="sec-dot dot-blue"></span>週間プログラム（月〜日）</div>
  <div class="card" id="weeklyProg"></div>

  <div class="sec-title"><span class="sec-dot dot-coral"></span>怪我への対応メモ</div>
  <div class="injury-box" id="injuryBox"></div>
</div>

<!-- LIBRARY -->
<div class="panel" id="panel-library">
  <div class="filter-row">
    <button class="filter-btn sel" onclick="filterLib('all',this)">すべて</button>
    <button class="filter-btn" onclick="filterLib('upper',this)">上半身</button>
    <button class="filter-btn" onclick="filterLib('lower',this)">下半身</button>
    <button class="filter-btn" onclick="filterLib('core',this)">体幹</button>
    <button class="filter-btn" onclick="filterLib('walk',this)">ウォーキング</button>
  </div>
  <div id="libList"></div>
</div>

<!-- HISTORY -->
<div class="panel" id="panel-history">
  <div id="histList"></div>
</div>

</div><!-- /content -->
</div><!-- /app -->

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
];
const upperShort=[
  {name:'ダンベル チェストプレス',detail:'10kg × 2セット × 12回',caution:null},
  {name:'ダンベル ロウ',detail:'15kg × 2セット × 12回',caution:null},
  {name:'フェイスプル（BARWINGマシン）',detail:'2セット × 15回',caution:'猫背改善'},
];
const lowerFull=[
  {name:'ハーフスクワット（ダンベル持ち）',detail:'10kg × 3セット × 12回',caution:'痛みは浅めに'},
  {name:'ヒップスラスト（ベンチ使用）',detail:'17kg × 3セット × 12回',caution:'臀部強化'},
  {name:'ヒップヒンジ / RDL',detail:'15kg × 3セット × 10回',caution:'背中まっすぐ'},
  {name:'レッグエクステンション（BARWINGマシン）',detail:'3セット × 15回',caution:'大腿四頭筋'},
  {name:'カーフレイズ（ゆっくり）',detail:'自重 × 3セット × 20回',caution:'足首ゆっくり'},
];
const lowerShort=[
  {name:'ハーフスクワット（ダンベル）',detail:'10kg × 2セット × 12回',caution:'痛みは浅めに'},
  {name:'ヒップスラスト（ベンチ）',detail:'自重 × 2セット × 15回',caution:'臀部強化'},
  {name:'カーフレイズ',detail:'自重 × 2セット × 20回',caution:'足首ゆっくり'},
];
const coreFull=[
  {name:'プランク',detail:'30秒 × 3セット',caution:'腰が下がらないよう'},
  {name:'バードドッグ（対角手足伸ばし）',detail:'左右10回 × 3セット',caution:'腰痛改善'},
  {name:'グルートブリッジ',detail:'3セット × 15回',caution:'腰・臀部強化'},
  {name:'デッドバグ',detail:'左右10回 × 2セット',caution:'体幹安定'},
];
const coreShort=[
  {name:'プランク',detail:'30秒 × 2セット',caution:'腰に注意'},
  {name:'グルートブリッジ',detail:'2セット × 15回',caution:'腰・臀部強化'},
];

const weeklyData=[
  {day:'月曜日',label:'上半身A + 体幹',dur:'60分',type:'upper',icon:'💪',desc:'胸・背中中心。ダンベル＋BARWINGマシン'},
  {day:'火曜日',label:'下半身A + ウォーキング',dur:'60分',type:'lower',icon:'🦵',desc:'大腿四頭筋・臀部。低衝撃スクワット'},
  {day:'水曜日',label:'体幹 + ウォーキング',dur:'30分',type:'core',icon:'🔥',desc:'軽め。姿勢改善・腰痛予防中心'},
  {day:'木曜日',label:'上半身B + 体幹',dur:'60分',type:'upper',icon:'💪',desc:'肩・腕・背中。猫背改善フェイスプル'},
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
];
const libraryData=[
  {name:'ダンベル チェストプレス',cat:'upper',tags:['上半身','胸'],desc:'ベンチに仰向けになりダンベルを押し上げる。大胸筋を鍛える基本種目。可変ベンチの角度を変えれば上部・下部も狙える。',sets:'10〜15kg × 3セット × 10〜12回'},
  {name:'ダンベル ロウ（片手）',cat:'upper',tags:['上半身','背中','猫背改善'],desc:'片手でベンチを支えにダンベルを引き上げる。広背筋・菱形筋を強化し猫背改善に有効。背中をまっすぐ保つ。',sets:'15〜17kg × 3セット × 10回'},
  {name:'ダンベル ショルダープレス',cat:'upper',tags:['上半身','肩'],desc:'肩より上にダンベルを押し上げる。三角筋強化。肩が痛む場合は7kg以下・可動域を狭めて行う。',sets:'7〜10kg × 3セット × 12回'},
  {name:'フェイスプル（BARWINGマシン）',cat:'upper',tags:['上半身','猫背改善','肩'],desc:'ケーブルを顔に向けて引く。巻き肩・猫背の改善に最重要種目。PC業務者に強く推奨。毎回必ず実施。',sets:'3セット × 15回（軽重量・丁寧に）'},
  {name:'ダンベル カール',cat:'upper',tags:['上半身','腕'],desc:'肘を固定してダンベルを曲げる。上腕二頭筋強化。ゆっくり下ろすことで効果アップ。',sets:'10kg × 3セット × 12回'},
  {name:'ケトルベルスイング',cat:'upper',tags:['上半身','全身','有酸素'],desc:'ケトルベルを股間から肩の高さまで振り上げる。全身有酸素＋臀部強化。腰の状態を確認しながら実施。',sets:'12〜16kg × 3セット × 15回'},
  {name:'ハーフスクワット（浅め）',cat:'lower',tags:['下半身','大腿四頭筋','膝配慮'],desc:'膝が痛む場合は浅めのスクワット。椅子から立ち上がる動作からスタートしてもOK。膝をつま先方向に向ける。',sets:'ダンベル10kg × 3セット × 12回'},
  {name:'レッグエクステンション',cat:'lower',tags:['下半身','大腿四頭筋'],desc:'BARWINGマシンで脚を伸ばして大腿四頭筋を集中強化。スクワットが辛い場合の代替種目にも。',sets:'3セット × 15回'},
  {name:'ヒップスラスト',cat:'lower',tags:['下半身','臀部'],desc:'ベンチに肩を乗せ、ダンベルを腰に置いて腰を持ち上げる。臀部強化の最重要種目。膝・腰への負担が少ない。',sets:'自重 → 17〜20kg × 3セット × 12回'},
  {name:'ヒップヒンジ（RDL）',cat:'lower',tags:['下半身','臀部','ハムストリング'],desc:'腰をまっすぐ保ったまま上体を前傾。ハムストリング・臀部・姿勢改善に効果的。背中が丸まらないよう注意。',sets:'15kg × 3セット × 10回'},
  {name:'カーフレイズ',cat:'lower',tags:['下半身','ふくらはぎ','足首配慮'],desc:'つま先立ちをゆっくり繰り返す。ふくらはぎ強化。足首の状態に合わせてゆっくり行う。段差を使うと効果的。',sets:'自重 × 3セット × 20回（ゆっくり）'},
  {name:'プランク',cat:'core',tags:['体幹','腰痛予防'],desc:'うつ伏せで肘とつま先で体を支える。腰が下がらないよう注意。腰痛改善の基本種目。お腹に力を入れて保持。',sets:'30秒 × 3セット'},
  {name:'バードドッグ',cat:'core',tags:['体幹','腰痛予防','猫背改善'],desc:'四つん這いで対角線の手足をゆっくり伸ばす。体幹安定・腰痛予防の最重要種目。ゆっくり丁寧に。',sets:'左右各10回 × 3セット'},
  {name:'グルートブリッジ',cat:'core',tags:['体幹','臀部','腰痛予防'],desc:'仰向けで膝を曲げ腰を持ち上げる。臀部と体幹を同時強化。腰痛がある人でも安全に行える。',sets:'3セット × 15回'},
  {name:'デッドバグ',cat:'core',tags:['体幹','腰痛予防'],desc:'仰向けで対角の手足をゆっくり伸ばす。脊柱安定に効果的。呼吸を止めないように。無理のない範囲で。',sets:'左右各10回 × 2セット'},
  {name:'ルームランナー ウォーキング',cat:'walk',tags:['ウォーキング','有酸素','低衝撃'],desc:'傾斜1〜3°、速度4〜5km/hで速歩き。膝・足首への衝撃を最小限に。脂肪燃焼・体力向上・気分転換に。走ってはいけない。',sets:'30〜60分 ｜ 週3〜5回'},
];

let duration=60;
let checked={};
let walkOn=false,walkSec=0,walkIv=null;
let hist=JSON.parse(localStorage.getItem('hgHist')||'[]');
let wkCnt=parseInt(localStorage.getItem('hgWk')||'0');
let wkMon=localStorage.getItem('hgMon')||'';

function checkNewWeek(){
  const now=new Date();
  const mon=getMondayStr(now);
  if(mon!==wkMon){wkCnt=0;wkMon=mon;localStorage.setItem('hgMon',mon);localStorage.setItem('hgWk','0');}
}
function getMondayStr(d){
  const dt=new Date(d);
  const day=dt.getDay();
  const diff=dt.getDate()-day+(day===0?-6:1);
  dt.setDate(diff);
  return dt.toDateString();
}

function setDuration(d){
  duration=d;
  document.getElementById('dur60').classList.toggle('sel',d===60);
  document.getElementById('dur30').classList.toggle('sel',d===30);
  renderToday();
}

function renderToday(){
  const up=duration===60?upperFull:upperShort;
  const lo=duration===60?lowerFull:lowerShort;
  const co=duration===60?coreFull:coreShort;
  renderExList('card-warmup',warmupData,'w');
  renderExList('card-upper',up,'u');
  renderExList('card-lower',lo,'l');
  renderExList('card-core',co,'c');
  updateCounts();
  updateWeekDots();
}

function renderExList(id,data,prefix){
  document.getElementById(id).innerHTML=data.map((e,i)=>{
    const k=prefix+i;
    const done=checked[k];
    return `<div class="ex-row">
      <div class="ex-check${done?' done':''}" onclick="toggleEx('${k}',this)">${done?'✓':''}</div>
      <div class="ex-main">
        <div class="ex-name${done?' done':''}">${e.name}</div>
        <div class="ex-detail">${e.detail}</div>
      </div>
      ${e.caution?`<div class="ex-caution">${e.caution}</div>`:''}
    </div>`;
  }).join('');
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
  const cnt=Object.values(checked).filter(Boolean).length;
  document.getElementById('doneCount').textContent=cnt;
}

function updateWeekDots(){
  let h='';
  for(let i=0;i<5;i++) h+=`<div class="week-dot${i<wkCnt?' done':''}"></div>`;
  document.getElementById('weekDots').innerHTML=h;
  document.getElementById('weekCount').textContent=wkCnt;
}

function toggleWalk(){
  if(!walkOn){
    walkOn=true;
    document.getElementById('walkBtn').textContent='停止';
    document.getElementById('walkBtn').className='walk-btn walk-stop';
    walkIv=setInterval(()=>{walkSec++;updWalk();},1000);
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
  const done=Object.values(checked).filter(Boolean).length;
  const all=warmupData.length+(duration===60?upperFull.length+lowerFull.length+coreFull.length:upperShort.length+lowerShort.length+coreShort.length);
  const note=document.getElementById('todayNotes').value;
  hist.unshift({date:new Date().toLocaleDateString('ja-JP'),dur:duration,done:done,total:all,walk:Math.floor(walkSec/60),note:note,stars:0});
  if(hist.length>50)hist.pop();
  localStorage.setItem('hgHist',JSON.stringify(hist));
  wkCnt=Math.min(5,wkCnt+1);
  localStorage.setItem('hgWk',String(wkCnt));
  checked={};
  renderToday();
  resetWalk();
  document.getElementById('todayNotes').value='';
  alert('✅ トレーニングを記録しました！お疲れ様でした！');
  switchTab('history','tab3');
  renderHistory();
}

function renderWeekGrid(){
  const today=new Date();
  const dow=today.getDay();
  const types=['rest','upper','lower','core','upper','lower','walk'];
  const labels=['休養','上半身','下半身','体幹','上半身','下半身','歩行'];
  let h='';
  DAYS_JP.forEach((d,i)=>{
    const dt=new Date(today);dt.setDate(today.getDate()+(i-dow));
    const cls=i===dow?'today':(i===0||i===6?'rest':'');
    h+=`<div class="day-cell ${cls}">
      <div class="day-name">${d}</div>
      <div class="day-num">${dt.getDate()}</div>
      <div class="day-type">${labels[i]}</div>
    </div>`;
  });
  document.getElementById('weekGrid').innerHTML=h;
}

function renderWeeklyProg(){
  const icons={upper:'💪',lower:'🦵',core:'🔥',walk:'🚶',rest:'😴'};
  const colors={upper:'prog-upper',lower:'prog-lower',core:'prog-core',walk:'prog-walk',rest:'prog-rest'};
  document.getElementById('weeklyProg').innerHTML=weeklyData.map(p=>`
    <div class="program-row">
      <div class="prog-icon ${colors[p.type]}">${icons[p.type]}</div>
      <div class="prog-content">
        <div class="prog-day">${p.day}</div>
        <div class="prog-name">${p.label}</div>
        <div class="prog-desc">${p.desc}</div>
        <div class="prog-time">⏱ ${p.dur}</div>
      </div>
    </div>`).join('');
  document.getElementById('injuryBox').innerHTML=injuryItems.map(t=>`<div class="injury-item">${t}</div>`).join('');
}

function renderLibrary(cat){
  const data=cat==='all'?libraryData:libraryData.filter(e=>e.cat===cat);
  const tc={upper:'tag-upper',lower:'tag-lower',core:'tag-core',walk:'tag-walk'};
  const bc={upper:'badge-blue',lower:'badge-green',core:'badge-amber',walk:'badge-purple'};
  const bl={upper:'上半身',lower:'下半身',core:'体幹',walk:'歩行'};
  document.getElementById('libList').innerHTML=data.map(e=>`
    <div class="lib-card">
      <div class="lib-header">
        <div class="lib-name">${e.name}</div>
        <span class="badge ${bc[e.cat]}">${bl[e.cat]}</span>
      </div>
      <div class="lib-tags">${e.tags.map(t=>`<span class="tag ${tc[e.cat]}">${t}</span>`).join('')}</div>
      <div class="lib-desc">${e.desc}</div>
      <div class="lib-sets">📋 ${e.sets}</div>
    </div>`).join('');
}

function filterLib(cat,btn){
  document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('sel'));
  btn.classList.add('sel');
  renderLibrary(cat);
}

function renderHistory(){
  const el=document.getElementById('histList');
  if(!hist.length){
    el.innerHTML='<div class="empty"><div class="empty-icon">🏆</div><div class="empty-text">まだ記録がありません。<br>最初のトレーニングを完了しましょう！</div></div>';
    return;
  }
  el.innerHTML=hist.map((h,idx)=>`
    <div class="hist-entry">
      <div class="hist-date">${h.date}</div>
      <div class="hist-title">${h.dur}分トレーニング — ${h.done}/${h.total}種目完了</div>
      <div class="hist-stats">
        <span class="hist-stat">⏱ ${h.dur}分</span>
        <span class="hist-stat">🚶 ウォーキング${h.walk}分</span>
        ${h.note?'<span class="hist-stat">📝 メモあり</span>':''}
      </div>
      <div class="stars" id="st-${idx}">
        ${[1,2,3,4,5].map(s=>`<span class="star${h.stars>=s?' filled':''}" onclick="rateStar(${idx},${s})">★</span>`).join('')}
        <span class="star-label">達成度</span>
      </div>
      ${h.note?`<div class="hist-note">${h.note}</div>`:''}
    </div>`).join('');
}

function rateStar(idx,s){
  hist[idx].stars=s;
  localStorage.setItem('hgHist',JSON.stringify(hist));
  renderHistory();
}

function switchTab(name,tabId){
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  document.getElementById('panel-'+name).classList.add('active');
  document.getElementById(tabId).classList.add('active');
  if(name==='schedule'){renderWeekGrid();renderWeeklyProg();}
  if(name==='history')renderHistory();
  if(name==='library')renderLibrary('all');
}

function init(){
  checkNewWeek();
  const now=new Date();
  document.getElementById('dateDisplay').innerHTML=
    `${now.getFullYear()}年${now.getMonth()+1}月${now.getDate()}日（${DAYS_JP[now.getDay()]}）`;
  updateWeekDots();
  renderToday();
  renderLibrary('all');
}
init();
</script>
</body>
</html>
