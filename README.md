CSO Gym
[index.html](https://github.com/user-attachments/files/28692942/index.html)

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
  --r:12px;--rl:16px;
}
.app{display:flex;flex-direction:column;min-height:100vh;max-width:1024px;margin:0 auto}
.header{background:#202020;border-bottom:1px solid var(--border);padding:16px 20px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:100}
.header h1{font-size:22px;font-weight:700}
.header .sub{font-size:15px;color:var(--text3);margin-top:3px}
.header-right{font-size:14px;color:var(--text2);text-align:right;line-height:1.6}
.tabs{display:flex;background:#202020;border-bottom:1px solid var(--border)}
.tab{flex:1;padding:14px 4px;border:none;background:#242424;font-size:16px;font-weight:800;color:#d8d4c8;cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:4px;border-bottom:4px solid transparent;box-shadow:inset 0 -1px 0 var(--border)}
.tab .ti{font-size:25px;filter:saturate(1.25) brightness(1.12)}
.tab.active{color:#ffffff;background:#20362e;border-bottom-color:var(--green)}
.content{padding:16px;flex:1}
.panel{display:none}.panel.active{display:block}
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);padding:16px 18px;margin-bottom:14px}
.card-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:12px}
.card-title{font-size:17px;font-weight:700}
.badge{font-size:13px;padding:4px 10px;border-radius:8px;font-weight:600}
.bg{background:var(--green-light);color:var(--green-dark)}
.bb{background:var(--blue-light);color:var(--blue-dark)}
.ba{background:var(--amber-light);color:var(--amber-dark)}
.bc{background:var(--coral-light);color:var(--coral-dark)}
.bp{background:var(--purple-light);color:var(--purple-dark)}
.sec{font-size:17px;font-weight:700;color:var(--text2);margin:18px 0 10px;display:flex;align-items:center;gap:8px}
.dot{width:10px;height:10px;border-radius:50%;flex-shrink:0}
/* Progress */
.prog-wrap{background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);padding:14px 16px;margin-bottom:14px}
.prog-title{font-size:16px;font-weight:700;color:var(--text2);margin-bottom:12px}
.prog-row{margin-bottom:10px}
.prog-label{display:flex;justify-content:space-between;margin-bottom:4px}
.prog-name{font-size:15px;font-weight:600}
.prog-val{font-size:15px;font-weight:700}
.prog-bar-bg{background:var(--surface2);border-radius:6px;height:10px;overflow:hidden}
.prog-bar{height:100%;border-radius:6px;transition:width 0.3s}
/* Duration */
.dur-row{display:flex;gap:8px;margin-bottom:14px;align-items:center}
.dur-lbl{font-size:16px;color:var(--text2);font-weight:600}
.dur-btn{padding:11px 26px;border-radius:24px;border:1.5px solid var(--border2);background:transparent;font-size:16px;font-weight:700;cursor:pointer;color:var(--text2)}
.dur-btn.sel{background:var(--blue);color:#fff;border-color:var(--blue)}
/* Exercise */
.ex-row{padding:10px 0;border-top:1px solid var(--border)}
.ex-row:first-child{border-top:none}
.ex-top{display:flex;align-items:center;gap:10px}
.ex-check{width:32px;height:32px;border-radius:50%;border:2px solid var(--border2);cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:16px;font-weight:700;transition:all 0.2s}
.ex-check.done{background:var(--green);border-color:var(--green);color:#fff}
.ex-main{flex:1;min-width:0}
.ex-name{font-size:17px;font-weight:500;line-height:1.4}
.ex-name.done{text-decoration:line-through;color:var(--text3)}
.ex-detail{font-size:14px;color:var(--text3);margin-top:2px}
.ex-caution{font-size:13px;color:var(--coral-dark);background:var(--coral-light);padding:3px 8px;border-radius:6px;white-space:nowrap;flex-shrink:0;font-weight:600}
.ex-info{font-size:20px;cursor:pointer;padding:0 4px;flex-shrink:0;color:var(--text3)}
.ex-desc{display:none;margin-top:8px;padding:10px 12px;background:var(--surface2);border-radius:8px;border-left:3px solid var(--blue);font-size:14px;color:var(--text2);line-height:1.7}
.custom-badge{font-size:11px;padding:2px 7px;border-radius:5px;background:#3a2a50;color:var(--purple-dark);font-weight:600;margin-left:6px}
/* Walk */
.walk-meta{font-size:16px;color:var(--text2);margin-bottom:12px;line-height:1.6}
.walk-row{display:flex;align-items:center;gap:12px;margin-bottom:12px;flex-wrap:wrap}
.walk-timer{font-size:46px;font-weight:700;min-width:110px;font-variant-numeric:tabular-nums}
.wbtn{padding:13px 24px;border-radius:var(--r);border:none;font-size:16px;font-weight:700;cursor:pointer}
.wbtn-s{background:var(--green);color:#fff}
.wbtn-p{background:var(--coral);color:#fff}
.wbtn-r{background:var(--surface2);color:var(--text2);border:1px solid var(--border2)}
.walk-bar-bg{background:var(--surface2);border-radius:6px;height:10px;overflow:hidden;margin-bottom:6px}
.walk-bar{height:100%;background:var(--green);border-radius:6px;transition:width 0.5s}
.walk-note{font-size:14px;color:var(--text3);line-height:1.5}
/* Notes */
.textarea{width:100%;border:1px solid var(--border);border-radius:var(--r);padding:12px 14px;font-size:17px;font-family:inherit;color:var(--text);background:var(--surface2);resize:vertical;min-height:90px}
.textarea:focus{outline:none;border-color:var(--green)}
.textarea::placeholder{color:var(--text3)}
.end-btn{width:100%;padding:17px;background:var(--green);color:#fff;border:none;border-radius:var(--r);font-size:18px;font-weight:700;cursor:pointer;margin-top:14px}
.end-btn:active{opacity:0.85}
/* Schedule */
.week-nav{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px}
.nav-btn{padding:10px 18px;background:var(--surface2);border:1.5px solid var(--border2);border-radius:var(--r);color:var(--text);font-size:17px;font-weight:700;cursor:pointer}
.nav-btn:disabled{opacity:0.3;cursor:not-allowed}
.week-lbl{font-size:15px;font-weight:700;color:var(--text2);text-align:center;line-height:1.6}
.week-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:5px;margin-bottom:14px}
.day-cell{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:8px 3px;text-align:center;cursor:pointer}
.day-cell.today{border:2px solid var(--green);background:var(--green-light)}
.day-cell.rest{background:var(--surface2)}
.day-name{font-size:13px;color:var(--text3);margin-bottom:3px;font-weight:600}
.day-num{font-size:20px;font-weight:700}
.day-type{font-size:10px;margin-top:3px;padding:2px 3px;border-radius:3px;font-weight:600}
.day-cell.today .day-type{background:var(--green);color:#fff}
.day-cell.rest .day-type{background:var(--border);color:var(--text3)}
.prog-row2{display:flex;align-items:flex-start;gap:12px;padding:10px 0;border-top:1px solid var(--border)}
.prog-row2:first-child{border-top:none}
.prog-icon{width:42px;height:42px;border-radius:var(--r);display:flex;align-items:center;justify-content:center;font-size:22px;flex-shrink:0}
.prog-content{flex:1}
.prog-day{font-size:13px;color:var(--text3);font-weight:600}
.prog-nm{font-size:16px;font-weight:700;margin:2px 0 4px}
.prog-dc{font-size:13px;color:var(--text2);line-height:1.5}
.prog-tm{font-size:13px;color:var(--text3);margin-top:4px;font-weight:600}
.inj-box{background:var(--coral-light);border:1px solid #5a2010;border-radius:var(--rl);padding:16px 18px}
.inj-item{font-size:15px;color:var(--coral-dark);padding:5px 0;line-height:1.6}
/* Library */
.filter-row{display:flex;gap:6px;flex-wrap:wrap;margin-bottom:14px}
.fbtn{padding:9px 15px;border-radius:20px;border:1.5px solid var(--border2);background:transparent;font-size:14px;font-weight:600;cursor:pointer;color:var(--text2)}
.fbtn.sel{background:var(--text);color:#1a1a1a;border-color:var(--text)}
.lib-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--rl);padding:14px 16px;margin-bottom:10px}
.lib-hd{display:flex;align-items:center;justify-content:space-between;margin-bottom:6px}
.lib-nm{font-size:16px;font-weight:700}
.lib-tags{display:flex;gap:4px;flex-wrap:wrap;margin-bottom:6px}
.tag{font-size:11px;padding:2px 7px;border-radius:5px;font-weight:600}
.tu{background:var(--blue-light);color:var(--blue-dark)}
.tl{background:var(--green-light);color:var(--green-dark)}
.tc{background:var(--amber-light);color:var(--amber-dark)}
.tw{background:var(--purple-light);color:var(--purple-dark)}
.tb{background:#1a3020;color:#80e8a0}
.tm{background:#2a1a30;color:#d0a0ff}
.td{background:#0e2a3a;color:#80d0ff}
.tr{background:#1a2a10;color:#a0e060}
.tbd{background:#2a1040;color:#e0a0ff}
.ts{background:#0a2a2a;color:#60e0d0}
.lib-desc{font-size:13px;color:var(--text2);line-height:1.6}
.lib-sets{font-size:14px;font-weight:700;margin-top:6px}
/* Mypage */
.add-form{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:10px}
.inp{padding:11px 13px;border:1px solid var(--border2);border-radius:var(--r);background:var(--surface);color:var(--text);font-size:16px;font-family:inherit;width:100%}
.inp:focus{outline:none;border-color:var(--green)}
.inp::placeholder{color:var(--text3)}
.sel-inp{padding:11px 13px;border:1px solid var(--border2);border-radius:var(--r);background:var(--surface);color:var(--text);font-size:16px;font-family:inherit;width:100%}
.abtn{padding:12px;background:var(--blue);color:#fff;border:none;border-radius:var(--r);font-size:16px;font-weight:700;cursor:pointer;width:100%}
.abtn:active{opacity:0.85}
.note-card{background:var(--surface2);border:1px solid var(--border);border-radius:var(--r);padding:12px 14px;margin-bottom:10px}
.note-date{font-size:13px;font-weight:700;color:var(--amber-dark);margin-bottom:6px}
.note-text{font-size:15px;color:var(--text);line-height:1.7;white-space:pre-wrap;word-break:break-all}
.del-btn{padding:5px 12px;background:var(--coral-light);color:var(--coral-dark);border:none;border-radius:6px;font-size:13px;font-weight:700;cursor:pointer}
.goal-row{display:flex;align-items:center;gap:10px;padding:8px 0;border-top:1px solid var(--border)}
.goal-row:first-child{border-top:none}
.goal-lbl{font-size:15px;font-weight:600;width:90px;flex-shrink:0}
.goal-inp{width:75px;padding:8px;border:1px solid var(--border2);border-radius:8px;background:var(--surface2);color:var(--text);font-size:15px;text-align:center}
.goal-inp:focus{outline:none;border-color:var(--green)}
.eq-row{display:flex;align-items:flex-start;gap:10px;padding:10px 0;border-top:1px solid var(--border);cursor:pointer}
.eq-row:first-child{border-top:none}
.eq-cat{font-size:13px;font-weight:700;color:var(--purple-dark);background:var(--purple-light);padding:4px 9px;border-radius:6px;white-space:nowrap;margin-top:2px;flex-shrink:0}
.eq-items{flex:1;font-size:14px;color:var(--text2);line-height:1.6}
.eq-arr{font-size:18px;color:var(--text3)}
.eq-modal{display:none;background:var(--surface);border:2px solid var(--green);border-radius:var(--rl);padding:16px 18px;margin-top:10px}
.eq-modal-hd{display:flex;align-items:center;justify-content:space-between;margin-bottom:12px}
.eq-modal-title{font-size:17px;font-weight:700}
.close-btn{padding:7px 14px;background:var(--surface2);border:1px solid var(--border2);border-radius:8px;color:var(--text2);font-size:14px;font-weight:700;cursor:pointer}
.eq-ex-row{display:flex;align-items:center;gap:10px;padding:10px 0;border-top:1px solid var(--border)}
.eq-ex-row:first-child{border-top:none}
.eq-ex-info{flex:1}
.eq-ex-name{font-size:15px;font-weight:600}
.eq-ex-detail{font-size:13px;color:var(--text3);margin-top:2px}
.eq-ex-tags{display:flex;gap:5px;margin-top:4px}
.add-ex-btn{padding:8px 14px;background:var(--green);color:#fff;border:none;border-radius:8px;font-size:14px;font-weight:700;cursor:pointer;white-space:nowrap;flex-shrink:0}
.added-lbl{padding:8px 14px;background:var(--surface2);color:var(--text3);border-radius:8px;font-size:13px;font-weight:700;flex-shrink:0}
.body-row{display:flex;align-items:center;gap:8px;padding:9px 0;border-top:1px solid var(--border)}
.body-row:first-child{border-top:none}
.body-icon{font-size:22px;flex-shrink:0}
.body-lbl{font-size:15px;font-weight:600;width:80px;flex-shrink:0}
.body-btns{display:flex;gap:5px;flex:1;flex-wrap:wrap}
.body-btn{flex:1;min-width:60px;padding:8px 4px;border-radius:8px;border:2px solid var(--border2);background:transparent;color:var(--text3);font-size:12px;font-weight:700;cursor:pointer}
.week-reset-btn{margin-top:8px;width:100%;padding:8px;background:var(--surface);border:1.5px solid var(--border2);border-radius:8px;color:var(--text3);font-size:14px;font-weight:600;cursor:pointer}

/* Tablet readability refinement */
html,body{-webkit-font-smoothing:subpixel-antialiased;text-rendering:geometricPrecision}
:root{--text:#fffaf1;--text2:#eee6d8;--text3:#d1c7b7;--border:#555047}
.app{background:#181816}
.card,.lib-card,.prog-card{background:#24231f;border-color:#504a42}
.header{position:relative;top:auto;z-index:auto}
.tabs{position:sticky;top:0;z-index:90;height:76px}
.panel-sticky{position:sticky;top:76px;z-index:75;background:#181816;margin:0 -18px 14px;padding:12px 18px 10px;border-bottom:1px solid #504a42;box-shadow:0 8px 14px rgba(0,0,0,.28)}
.panel-sticky .prog-wrap,.panel-sticky .dur-row,.panel-sticky .cycle-note,.panel-sticky .time-note,.panel-sticky .filter-row{margin-bottom:8px}
.panel-sticky .time-note{margin-bottom:0}
.schedule-sticky .sec{margin-top:0}
.schedule-sticky .week-grid{margin-bottom:0}
.library-sticky{padding-bottom:8px}
.library-sticky .filter-row{gap:5px}
.library-sticky .fbtn{padding:7px 11px;font-size:13px;border-radius:7px}
.tab{height:76px;min-height:76px;padding:5px 4px;font-size:17px;color:#f0eadf;text-shadow:none}
.tab .ti{font-size:26px;filter:none}
.tab.active{color:#fff;background:#1f3a31}
.content{padding:18px}
.prog-title{font-size:18px;color:#f0ede6}
.prog-name,.prog-val{font-size:17px}
.prog-bar-bg{height:12px}
.ex-check{width:36px;height:36px}
.ex-name{font-size:19px;font-weight:800;color:#fffaf1}
.ex-detail{font-size:16px;color:#ded4c6}
.ex-desc{font-size:16px;line-height:1.75;color:#f3ebdf;background:#1b1a17;border-color:#625a50}
.lib-nm{font-size:18px}
.lib-desc{font-size:15px;color:#e2d8c9}
.lib-sets{font-size:16px}
.lib-effect{font-size:14px;line-height:1.6;color:#f0e5d6;margin-top:8px;padding:9px 10px;border-left:3px solid var(--green);background:#1b1a17;border-radius:6px}
.body-btn{font-size:13px;min-height:38px}
.time-note{margin:-4px 0 14px;padding:9px 11px;border-left:3px solid var(--amber);background:#1b1a17;color:#efe4d2;border-radius:6px;font-size:13px;line-height:1.55}
.cycle-note{margin:0 0 14px;padding:10px 12px;background:#202a26;border:1px solid #49645a;border-radius:7px;color:#f2ede4;font-size:14px;line-height:1.55}
.cycle-note strong{color:#9de0c3}
.date-tab-icon{width:44px;height:34px;border-radius:7px;background:#f7f0e5;color:#202020;display:grid;place-items:center;font-size:14px;font-weight:900;line-height:1;border-top:6px solid var(--coral);box-shadow:0 1px 0 rgba(0,0,0,.35)}
.tab.active .date-tab-icon{background:#fff;color:#1a1a1a}
.muscle-map{display:flex;flex-wrap:wrap;gap:6px;margin-top:10px}
.muscle-map span{border:1px solid #59534a;background:#181714;color:#bdb4a7;border-radius:6px;padding:6px 4px;text-align:center;font-size:12px;font-weight:800;line-height:1.1}
.muscle-map span:not(.active){display:none}
.muscle-map span.active{color:#141414;border-color:#f2d28b;background:#f2d28b;box-shadow:0 0 0 2px rgba(242,210,139,.12) inset}
.muscle-map .active.muscle-chest{background:#ffb085;border-color:#ffb085}
.muscle-map .active.muscle-back{background:#8fd4ff;border-color:#8fd4ff}
.muscle-map .active.muscle-shoulder{background:#b9d982;border-color:#b9d982}
.muscle-map .active.muscle-arm{background:#f7c7e3;border-color:#f7c7e3}
.muscle-map .active.muscle-core{background:#f4d35e;border-color:#f4d35e}
.muscle-map .active.muscle-glute{background:#b69df8;border-color:#b69df8}
.muscle-map .active.muscle-quad{background:#90e0a6;border-color:#90e0a6}
.muscle-map .active.muscle-calf{background:#7bdff2;border-color:#7bdff2}
.muscle-map .active.muscle-recovery{background:#92ead0;border-color:#92ead0}
.muscle-detail{margin-top:8px;padding:8px 10px;background:#191815;border-left:3px solid #8fd4ff;border-radius:6px;color:#eee6d8;font-size:13px;line-height:1.55}
.muscle-detail strong{color:#fffaf1}
.dash-grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:10px}
.dash-stat{background:#1b1a17;border:1px solid #504a42;border-radius:7px;padding:12px}
.dash-stat strong{display:block;font-size:24px;color:#fffaf1;margin-top:4px}
.dash-label{font-size:13px;color:#d1c7b7}
.balance-row{display:grid;grid-template-columns:58px 1fr 38px;gap:8px;align-items:center;margin:9px 0;font-size:13px}
.balance-track{height:10px;background:#151512;border:1px solid #504a42;border-radius:5px;overflow:hidden}
.balance-fill{height:100%;background:var(--green)}
.control-row{display:grid;grid-template-columns:120px 1fr;gap:10px;align-items:center;margin:10px 0}
.control-row label{font-size:14px;color:#eee6d8}
.mypage-actions{display:flex;flex-wrap:wrap;gap:8px;margin-top:10px}
.mypage-actions button{min-height:42px}
.equip-manage-row{display:flex;justify-content:space-between;gap:10px;align-items:center;padding:9px 0;border-bottom:1px solid #504a42}
.equip-manage-row:last-child{border-bottom:0}
@media(max-width:600px){
  .panel-sticky{top:76px;padding:8px 12px;margin-left:-18px;margin-right:-18px}
  .library-sticky .fbtn{padding:6px 8px;font-size:12px}
  .panel-sticky .time-note{display:none}
  .dash-grid{grid-template-columns:1fr 1fr}
  .control-row{grid-template-columns:1fr}
}
</style>
</head>
<body>
<div class="app">
<div class="header">
  <div><h1>🏋️ ホームジム</h1><div class="sub">怪我に配慮した自宅プログラム</div></div>
  <div class="header-right" id="dateDisp"></div>
</div>
<div class="tabs">
  <button class="tab active" onclick="sw('today','t0')" id="t0"><span class="ti date-tab-icon" id="todayTabDate">--</span>今日</button>
  <button class="tab" onclick="sw('schedule','t1')" id="t1"><span class="ti">🗓️</span>週間</button>
  <button class="tab" onclick="sw('library','t2')" id="t2"><span class="ti">📋</span>種目</button>
  <button class="tab" onclick="sw('mypage','t3')" id="t3"><span class="ti">⚙️</span>マイページ</button>
</div>
<div class="content">

<!-- TODAY -->
<div class="panel active" id="panel-today">
  <div class="panel-sticky today-sticky">
  <div class="prog-wrap" id="catProg"></div>
  <div class="dur-row">
    <span class="dur-lbl">時間：</span>
    <button class="dur-btn" id="d60" onclick="setDur(60)">60分</button>
    <button class="dur-btn sel" id="d30" onclick="setDur(30)">30分</button>
  </div>
  </div>
  <div class="cycle-note" id="cycleNote"></div>
  <div class="time-note">30分は準備運動＋主種目4種目を目安に完了します。60分でも最大7種目まで。痛みがある日は重量・可動域を下げ、種目数より正確なフォームを優先してください。</div>
  <div class="sec"><span class="dot" style="background:var(--green)"></span>朝ベッド <span class="badge bg" style="margin-left:auto;font-size:12px">ウォームアップとは別</span></div>
  <div class="card" id="cm"></div>
  <div class="sec"><span class="dot" style="background:var(--amber)"></span>ウォームアップ（5分）</div>
  <div class="card" id="cw"></div>
  <div class="sec"><span class="dot" style="background:var(--blue)"></span>上半身 <span class="badge bb" style="margin-left:auto;font-size:12px">猫背改善</span></div>
  <div class="card" id="cu"></div>
  <div class="sec"><span class="dot" style="background:var(--green)"></span>下半身 <span class="badge bg" style="margin-left:auto;font-size:12px">膝・足首配慮</span></div>
  <div class="card" id="cl"></div>
  <div class="sec"><span class="dot" style="background:var(--amber)"></span>体幹・ボール <span class="badge ba" style="margin-left:auto;font-size:12px">腰痛配慮</span></div>
  <div class="card" id="cc"></div>
  <div class="sec"><span class="dot" style="background:var(--purple)"></span>ウォーキング（別メニュー）</div>
  <div class="card">
    <div class="card-header"><div class="card-title">ルームランナー ウォーキング</div><span class="badge bp">低衝撃</span></div>
    <div class="walk-meta">目標：30分 ｜ 傾斜1〜3° ｜ 速度4〜5km/h</div>
    <div class="walk-row">
      <div class="walk-timer" id="wTimer">00:00</div>
      <button class="wbtn wbtn-s" id="wBtn" onclick="toggleWalk()">開始</button>
      <button class="wbtn wbtn-r" onclick="resetWalk()">リセット</button>
    </div>
    <div class="walk-bar-bg"><div class="walk-bar" id="wBar" style="width:0%"></div></div>
    <div class="walk-note">※ ウォーキングはトレーニング後または別日に実施。走らないこと。</div>
  </div>
  <div class="sec"><span class="dot" style="background:#20a090"></span>ストレッチ・リカバリー <span class="badge bg" style="margin-left:auto;font-size:12px">毎日推奨</span></div>
  <div class="card" id="cs"></div>
  <button class="end-btn" onclick="endWorkout()">✓ 今日を終了する</button>
</div>

<!-- SCHEDULE -->
<div class="panel" id="panel-schedule">
  <div class="panel-sticky schedule-sticky">
  <div class="sec" style="margin-top:0"><span class="dot" style="background:var(--green)"></span>週間カレンダー</div>
  <div class="week-nav">
    <button class="nav-btn" id="btnPrev" onclick="chgWeek(-1)">◀ 前の週</button>
    <div class="week-lbl" id="wkLbl"></div>
    <button class="nav-btn" id="btnNext" onclick="chgWeek(1)">次の週 ▶</button>
  </div>
  <div class="week-grid" id="wkGrid"></div>
  <div id="dayDetail"></div>
  </div>
  <div class="sec"><span class="dot" style="background:var(--blue)"></span>週間プログラム</div>
  <div class="card" id="wkProg"></div>
  <div class="sec"><span class="dot" style="background:var(--coral)"></span>怪我への対応メモ</div>
  <div class="inj-box" id="injBox"></div>
</div>

<!-- LIBRARY -->
<div class="panel" id="panel-library">
  <div class="panel-sticky library-sticky">
  <div class="filter-row" id="filterRow"></div>
  </div>
  <div id="libList"></div>
</div>

<!-- MYPAGE -->
<div class="panel" id="panel-mypage">
  <div class="sec" style="margin-top:0"><span class="dot" style="background:var(--green)"></span>4週間サイクル</div>
  <div class="card" id="cycleStatus"></div>

  <div class="sec"><span class="dot" style="background:var(--blue)"></span>継続状況</div>
  <div class="dash-grid" id="continuityStats"></div>

  <div class="sec"><span class="dot" style="background:var(--amber)"></span>部位別バランス</div>
  <div class="card" id="balanceStats"></div>

  <div class="sec"><span class="dot" style="background:var(--coral)"></span>4週間の目標</div>
  <div class="card">
    <div class="control-row"><label for="mpGoal">目標</label><input class="inp" id="mpGoal" placeholder="例：週5回を4週間続ける" onchange="saveMySettings()"></div>
    <div class="control-row"><label for="mpWeekly">週の目標回数</label><input class="inp" id="mpWeekly" type="number" min="1" max="7" onchange="saveMySettings()"></div>
    <div class="control-row"><label for="mpPriority">優先部位</label><select class="sel-inp" id="mpPriority" onchange="saveMySettings()"><option>バランス重視</option><option>胸</option><option>背中</option><option>肩</option><option>腕</option><option>体幹</option><option>臀部</option><option>太腿</option><option>脹脛</option></select></div>
  </div>

  <div class="sec"><span class="dot" style="background:var(--purple)"></span>所有器具</div>
  <div class="card">
    <div id="myEquipList"></div>
    <div class="add-form" style="margin-top:10px"><input class="inp" id="newEquip" placeholder="器具名を追加"><button class="abtn" onclick="addMyEquip()">追加</button></div>
  </div>

  <div class="sec"><span class="dot" style="background:var(--text3)"></span>アプリ設定</div>
  <div class="card">
    <div class="control-row"><label for="mpDuration">初期時間</label><select class="sel-inp" id="mpDuration" onchange="saveMySettings()"><option value="30">30分</option><option value="60">60分</option></select></div>
    <div class="control-row"><label for="mpFont">文字サイズ</label><select class="sel-inp" id="mpFont" onchange="saveMySettings()"><option value="1">標準</option><option value="1.1">大きめ</option><option value="1.2">さらに大きめ</option></select></div>
    <div class="mypage-actions"><button class="abtn" onclick="exportAppData()">保存データを書き出す</button><button class="wbtn wbtn-r" onclick="resetAppData()">データを初期化</button></div>
  </div>
</div>

</div><!-- /content -->
</div><!-- /app -->
<script>
const DJ=['日','月','火','水','木','金','土'];

// ===== DATA =====
const morning=[
  {n:'T-ストレッチ',d:'朝ベッドで実施。回数はその日の調子で決める',c:'通常ウォームアップとは別'},
];

const warmup=[
  {n:'肩回し・首ストレッチ',d:'前後各10回',c:null},
  {n:'キャットカウ（四つん這い・背中丸め反らし）',d:'10回ゆっくり',c:'腰に注意'},
  {n:'足首回し・ふくらはぎストレッチ',d:'各方向10秒',c:'手術後は様子見'},
];
const upperF=[
  {n:'T-Betabs',d:'朝ベッドで実施。回数はその日の調子で決める',c:'上半身の先頭'},
  {n:'ダンベル チェストプレス（ベンチ仰向け）',d:'10kg×3セット×10回',c:null},
  {n:'プッシュアップバー腕立て',d:'2〜3セット×できる回数',c:'肩痛時は浅く'},
  {n:'ダンベル ロウ（片手・ベンチ支持）',d:'15kg×3セット×10回',c:null},
  {n:'インクラインベンチ ダンベルロウ',d:'15kg×3セット×10回',c:'背中強化'},
  {n:'ダンベル プルオーバー（ベンチ）',d:'10kg×3セット×12回',c:'広背筋'},
  {n:'ダンベル ショルダープレス',d:'7kg×3セット×12回',c:'肩痛時は軽量'},
  {n:'ダンベル カール',d:'10kg×3セット×12回',c:null},
  {n:'アシスト懸垂（足補助）',d:'3セット×5回',c:'背中強化'},
  {n:'ケトルベルスイング（低強度）',d:'12kg×3セット×15回',c:'腰に注意'},
  {n:'ディップス',d:'自重×3セット×5〜8回',c:'肩痛時は浅く'},
  {n:'ネガティブ懸垂',d:'3セット×5回（5秒下ろす）',c:'補助つきでもOK'},
  {n:'ダンベル フライ（ベンチ）',d:'10kg×3セット×12回',c:'大胸筋'},
  {n:'ダンベル インクラインプレス（ベンチ角度上げ）',d:'10kg×3セット×10回',c:'大胸筋上部'},
  {n:'ハンマーカール',d:'10kg×3セット×12回',c:'肘固定'},
  {n:'コンセントレーションカール',d:'10kg×3セット×10回',c:'集中'},
  {n:'ダンベル トライセプスエクステンション',d:'7kg×3セット×12回',c:'肘が開かないよう'},
  {n:'ダンベル キックバック（三頭筋）',d:'7kg×3セット×12回',c:'肘を高く'},
  {n:'ダンベル サイドレイズ',d:'7kg×3セット×15回',c:'三角筋中部'},
  {n:'ダンベル フロントレイズ',d:'7kg×3セット×12回',c:'三角筋前部'},
  {n:'ダンベル リアレイズ（前傾）',d:'7kg×3セット×15回',c:'猫背改善'},
];
const upperS=[
  {n:'T-Betabs',d:'朝ベッドで実施。回数はその日の調子で決める',c:'上半身の先頭'},
  {n:'ダンベル チェストプレス（ベンチ仰向け）',d:'10kg×2セット×12回',c:null},
  {n:'プッシュアップバー腕立て',d:'2セット×できる回数',c:'肩痛時は浅く'},
  {n:'ダンベル ロウ（片手・ベンチ支持）',d:'15kg×2セット×12回',c:null},
  {n:'インクラインベンチ ダンベルロウ',d:'15kg×2セット×12回',c:'背中強化'},
  {n:'アシスト懸垂（足補助）',d:'2セット×5回',c:'背中強化'},
  {n:'ダンベル フライ（ベンチ）',d:'10kg×2セット×12回',c:'大胸筋'},
  {n:'ダンベル サイドレイズ',d:'7kg×2セット×15回',c:'三角筋'},
  {n:'ダンベル トライセプスエクステンション',d:'7kg×2セット×12回',c:'三頭筋'},
];
const lowerF=[
  {n:'ハーフスクワット（ダンベル持ち）',d:'10kg×3セット×12回',c:'痛みは浅めに'},
  {n:'ヒップスラスト（ベンチ使用）',d:'17kg×3セット×12回',c:'臀部強化'},
  {n:'ヒップヒンジ / RDL',d:'15kg×3セット×10回',c:'背中まっすぐ'},
  {n:'椅子レッグエクステンション（自重）',d:'3セット×15回',c:'大腿四頭筋'},
  {n:'カーフレイズ（ゆっくり）',d:'自重×3セット×20回',c:'足首ゆっくり'},
  {n:'バンド グルートブリッジ',d:'中強度×3セット×15回',c:'臀部強化'},
  {n:'バンド クラムシェル',d:'軽〜中×3セット×左右15回',c:'膝安定'},
];
const lowerS=[
  {n:'ハーフスクワット（ダンベル持ち）',d:'10kg×2セット×12回',c:'痛みは浅めに'},
  {n:'ヒップスラスト（ベンチ使用）',d:'自重×2セット×15回',c:'臀部強化'},
  {n:'カーフレイズ（ゆっくり）',d:'自重×2セット×20回',c:'足首ゆっくり'},
  {n:'バンド クラムシェル',d:'軽強度×2セット×左右15回',c:'膝安定'},
];
const coreF=[
  {n:'プランク',d:'30秒×3セット',c:'腰が下がらないよう'},
  {n:'バードドッグ（対角手足伸ばし）',d:'左右10回×3セット',c:'腰痛改善'},
  {n:'グルートブリッジ',d:'3セット×15回',c:'腰・臀部強化'},
  {n:'デッドバグ',d:'左右10回×2セット',c:'体幹安定'},
  {n:'バランスボール 腹筋ロール',d:'3セット×10回',c:'腰注意'},
  {n:'バランスボール 体幹キープ（座位）',d:'30秒×3セット',c:'姿勢改善'},
  {n:'ウエイトボール ロシアンツイスト',d:'10kg×2セット×左右10回',c:'腰注意'},
  {n:'膝つき腹筋ローラー（初級）',d:'3セット×8回',c:'腰が反らないよう'},
];
const coreS=[
  {n:'プランク',d:'30秒×2セット',c:'腰に注意'},
  {n:'グルートブリッジ',d:'2セット×15回',c:'腰・臀部強化'},
  {n:'バランスボール 体幹キープ（座位）',d:'30秒×2セット',c:'姿勢改善'},
];
const stretchData=[
  {n:'ストレッチポール 背骨リセット',d:'5〜10分 仰向けに乗るだけ',c:'猫背改善',desc:'ポールを頭から背骨に沿って縦に置き仰向けに乗る。重力で背骨・胸椎が自然に伸びる。毎日やるのがおすすめ。乗り降りはゆっくり行う。'},
  {n:'フォームローラー 大腿四頭筋ほぐし',d:'左右各60秒',c:'膝ケア',desc:'うつ伏せで太ももの前面をローラーの上に乗せてゆっくり転がす。膝への負担を軽減する効果あり。痛い部分では止めて圧をかけるとより効果的。'},
  {n:'フォームローラー 背中・胸椎ほぐし',d:'60秒×2セット',c:'猫背改善',desc:'仰向けでローラーを背中の中央に置き前後にゆっくり転がす。胸椎の可動域改善・猫背改善に効果的。PC業務後の疲労回復に最適。'},
  {n:'フォームローラー 臀部ほぐし',d:'左右各60秒',c:'腰痛ケア',desc:'座位でローラーに臀部を乗せて片側ずつ体重をかけながら転がす。梨状筋・臀部の張りをほぐして腰痛改善に効果的。'},
];

const weeklyProg=[
  {day:'月曜日',label:'上半身A + 体幹',dur:'60分',type:'upper',icon:'💪',desc:'胸・背中中心。ダンベル＋懸垂マシン'},
  {day:'火曜日',label:'下半身A + ウォーキング',dur:'60分',type:'lower',icon:'🦵',desc:'大腿四頭筋・臀部。低衝撃スクワット'},
  {day:'水曜日',label:'体幹 + バランスボール',dur:'30分',type:'core',icon:'🔥',desc:'軽め。姿勢改善・腰痛予防・バランスボール'},
  {day:'木曜日',label:'上半身B + 三角筋・腕',dur:'60分',type:'upper',icon:'💪',desc:'三角筋・二頭筋・三頭筋。ディップス・サイドレイズ'},
  {day:'金曜日',label:'下半身B + ウォーキング',dur:'60分',type:'lower',icon:'🦵',desc:'ふくらはぎ・臀部・体幹の複合'},
  {day:'土曜日',label:'ウォーキングのみ',dur:'30分',type:'walk',icon:'🚶',desc:'日曜日と同じく、ルームランナーで低衝撃のリカバリー歩行'},
  {day:'日曜日',label:'ウォーキングのみ',dur:'30分',type:'walk',icon:'🚶',desc:'ルームランナーで低衝撃のリカバリー歩行'},
];
const injuryList=[
  '🦵 膝靭帯：スクワットは浅め・ゆっくり。痛みが出たら即中止',
  '🦶 足首：カーフレイズはゆっくり丁寧に。跳ぶ・走る系は禁止',
  '🔙 腰痛：ヒップヒンジ時は背中まっすぐを徹底。重量より形重視',
  '🏃 ランニング禁止：ルームランナーは速歩き（4〜5km/h）のみ',
  '🤸 懸垂：補助つきで週1〜2回まで。無理は禁物',
  '💪 肩・首：ショルダープレスは痛みが出たら軽量に変更',
  '🪑 猫背対策：インクラインベンチ ダンベルロウ・リアレイズ・バードドッグを優先',
  '🧘 ストレッチポール：毎日乗るだけで猫背・腰痛改善',
  '🩷 ヒップバンド：膝の安定性向上にも効果的。強度は軽→中→強の順で',
];

const exDesc={
  'T-ストレッチ':'朝ベッドで行う専用ストレッチ。通常のウォームアップとは別枠。回数や時間はその日の調子で決める。痛みがある日は可動域を小さくして、呼吸を止めずに行う。',
  'T-Betabs':'朝ベッドで行う上半身用の準備種目。上半身トレーニング日の先頭にも入れる。回数は固定せず、その日の肩・首・腰の調子を見ながら無理のない範囲で行う。',
  '肩回し・首ストレッチ':'両腕を大きく前回し・後ろ回しに10回ずつ。首はゆっくり左右に倒すだけ。無理に回さない。PC業務で固まった肩・首をほぐすウォームアップ。',
  'キャットカウ（四つん這い・背中丸め反らし）':'四つん這いになり、息を吐きながら背中を丸め（キャット）、息を吸いながら背中を反らす（カウ）。腰痛予防・背骨の柔軟性向上に効果的。腰に痛みがある場合はごく小さい動きから。',
  '足首回し・ふくらはぎストレッチ':'座位または立位で足首をゆっくり大きく回す。手術後は痛みが出ない範囲で行う。ふくらはぎは壁に手をついてアキレス腱を伸ばすストレッチも合わせて行うと効果的。',
  'ダンベル チェストプレス（ベンチ仰向け）':'ベンチに仰向けになりダンベルを肩幅より少し広く持つ。肘を90度に曲げた位置からまっすぐ上に押し上げる。大胸筋・三角筋前部・三頭筋を鍛える基本種目。',
  'ダンベル ロウ（片手・ベンチ支持）':'片手でベンチに手をつき体を支える。反対の手でダンベルを床から脇腹に向けて引き上げる。広背筋・菱形筋を強化し猫背改善に効果的。背中をまっすぐ保つこと。',
  'インクラインベンチ ダンベルロウ':'ベンチを30〜45度にして胸を預ける。両手または片手でダンベルを脇腹へ引き、肩甲骨を軽く寄せる。腰に負担をかけず背中を鍛えやすい。',
  'ダンベル プルオーバー（ベンチ）':'ベンチに仰向けになり、ダンベルを胸の上から頭の後ろへゆっくり下ろす。胸を張り、肘を少し曲げたまま広背筋を伸ばして戻す。肩に痛みが出る範囲までは下ろさない。',
  'アシスト懸垂（足補助）':'懸垂マシンにつかまり、足を床や台に軽く置いて補助する。胸を少し張り、肘を下に引く意識で体を上げる。首をすくめず、肩や肘に痛みが出ない範囲で行う。',
  'プッシュアップバー腕立て':'プッシュアップバーを肩幅より少し広く置く。体を一直線に保ち、胸をバーの間へゆっくり下ろして押し上げる。手首の負担を減らしつつ胸・腕を鍛える。肩が痛い日は浅く行う。',
  'ダンベル ショルダープレス':'座位または立位でダンベルを耳の横に持ち、頭上に押し上げる。三角筋全体を鍛える。肩に痛みがある場合は7kg以下・可動域を狭めて行う。',
  'ダンベル カール':'肘を体の横に固定してダンベルをゆっくり曲げる。上腕二頭筋を集中強化。ゆっくり下ろすことで効果アップ。反動を使わないこと。',
  'ケトルベルスイング（低強度）':'足を肩幅に開いてケトルベルを両手で持つ。股関節を折り曲げて前に振り下ろし、股関節を伸ばす力で肩の高さまで振り上げる。全身有酸素＋臀部強化。腰が丸まらないよう注意。',
  'ディップス':'ディップスバーを両手で握り体を支える。肘を曲げてゆっくり体を下げ、押し上げる。大胸筋下部・三頭筋を強化。肩に痛みがある場合は浅めの可動域で行う。',
  'ネガティブ懸垂':'台に乗って懸垂の上の位置からスタート。5秒かけてゆっくり体を下ろす。普通の懸垂ができなくても筋力をつけられる最適な方法。',
  'ダンベル フライ（ベンチ）':'ベンチに仰向けになりダンベルを弧を描くように左右に開き、胸の前で合わせる。大胸筋の伸展・収縮を最大限に使える。チェストプレスと組み合わせると効果的。',
  'ダンベル インクラインプレス（ベンチ角度上げ）':'ベンチを30〜45度に傾けてプレス。大胸筋上部を集中強化。猫背改善・胸の厚みづくりに効果的。',
  'ハンマーカール':'親指を上に向けた状態でダンベルを曲げる。上腕二頭筋・腕橈骨筋を同時強化。通常カールより腕全体を太くする効果あり。',
  'コンセントレーションカール':'座位で肘を膝の内側に固定してカール。上腕二頭筋だけを孤立させて集中的に鍛える。力こぶを作るのに最も効果的な種目。',
  'ダンベル トライセプスエクステンション':'頭の後ろでダンベルを持ち肘だけを動かして伸ばす。上腕三頭筋の長頭を集中強化。二の腕引き締めに効果的。肘が外に開かないよう注意。',
  'ダンベル キックバック（三頭筋）':'前傾姿勢で肘を高く保ちダンベルを後ろにゆっくり伸ばす。上腕三頭筋外側頭の強化。肘の位置を固定してゆっくり動かすことが重要。',
  'ダンベル サイドレイズ':'肘を少し曲げた状態でダンベルを真横に肩の高さまで上げる。三角筋中部を集中強化。肩幅を広くする定番種目。肩の痛みに注意して軽めから始める。',
  'ダンベル フロントレイズ':'ダンベルを正面に肩の高さまでゆっくり上げる。三角筋前部の強化。猫背の人は特に前部が弱いことが多い。反動を使わず丁寧に。',
  'ダンベル リアレイズ（前傾）':'上体を45度前傾させてダンベルを横に開く。三角筋後部・菱形筋を強化。猫背・巻き肩の改善に最も効果的な種目のひとつ。',
  'ハーフスクワット（ダンベル持ち）':'ダンベルを両手に持ち足を肩幅に開く。膝がつま先方向に向くよう意識しながら浅めに腰を落とす。膝が痛む場合は椅子から立ち上がる動作から始めてもOK。',
  'ヒップスラスト（ベンチ使用）':'ベンチに肩甲骨を乗せ膝を90度に曲げる。ダンベルを腰に置いて腰をまっすぐ持ち上げる。臀部強化の最重要種目。膝・腰への負担が少なく怪我がある人でも安全。',
  'ヒップヒンジ / RDL':'足を肩幅に開きダンベルを太ももに沿わせながら股関節から上体を前傾させる。背中を絶対に丸めないこと。ハムストリング・臀部・姿勢改善に効果的。',
  '椅子レッグエクステンション（自重）':'椅子に浅く座り、片脚ずつ膝をゆっくり伸ばして戻す。膝に痛みが出ない範囲で大腿四頭筋を使う。上げ切った所で1秒止め、反動を使わない。',
  'カーフレイズ（ゆっくり）':'立位でゆっくりつま先立ちになり、ゆっくり下ろす。3秒上げ・3秒下げが目安。ふくらはぎ強化。足首の手術後は痛みが出ない範囲でゆっくり行う。',
  'バンド グルートブリッジ':'バンドを膝上に巻いて仰向けになり膝を曲げる。膝を外に広げながら腰をまっすぐ持ち上げる。通常より臀部への負荷が大幅アップ。腰痛予防にも最適。',
  'バンド クラムシェル':'横向きに寝てバンドを膝上に巻く。膝を90度に曲げた状態で上の膝を貝のように開閉する。中臀筋・外旋筋の強化。膝の安定性向上に最適。',
  'プランク':'うつ伏せで肘とつま先で体を支える。腰が下がらないようにお腹に力を入れて保持。腰痛改善の基本種目。最初は15〜20秒からでOK。',
  'バードドッグ（対角手足伸ばし）':'四つん這いになり右手と左足を同時にゆっくり伸ばして3秒キープ。体幹安定・腰痛予防の最重要種目。',
  'グルートブリッジ':'仰向けで膝を曲げ足を床につける。腰をまっすぐ持ち上げてお尻を締める。臀部と体幹を同時強化。腰痛がある人でも安全に行える。',
  'デッドバグ':'仰向けで両腕を天井に向け膝を90度に曲げる。対角の手足をゆっくり伸ばして戻す。脊柱安定・体幹強化に効果的。',
  'バランスボール 腹筋ロール':'ボールに前腕を乗せて前後に転がす。腹筋・体幹強化。腰が反らないよう腹に力を入れる。',
  'バランスボール 体幹キープ（座位）':'バランスボールに座って体幹を安定させる。猫背・姿勢改善に効果的。PC作業の椅子代わりに使うのもおすすめ。',
  'ウエイトボール ロシアンツイスト':'座位でボールを両手で持ち左右に体をひねる。腹斜筋・体幹強化。腰痛がある場合は小さい動きでOK。',
  '膝つき腹筋ローラー（初級）':'膝をついた状態でローラーを前に転がし限界まで伸ばして戻す。腹筋・体幹強化。腰が反らないよう腹に力を入れる。腰痛がある場合はまずここから。',
};

const libData=[
  {n:'T-ストレッチ',cat:'stretch',tags:['朝ベッド','ストレッチ','毎日'],sets:'回数・時間はその日の調子で決める',desc:'朝ベッドで行う専用ストレッチ。通常のウォームアップとは別枠。痛みがある日は可動域を小さくして、呼吸を止めずに行う。'},
  {n:'T-Betabs',cat:'upper',tags:['朝ベッド','上半身','毎日'],sets:'回数はその日の調子で決める',desc:'朝ベッドで行う上半身用の準備種目。上半身トレーニング日の先頭にも入れる。肩・首・腰の調子を見ながら無理のない範囲で行う。'},
  {n:'ダンベル チェストプレス',cat:'upper',tags:['上半身','大胸筋'],sets:'10〜15kg×3セット×10〜12回',desc:'ベンチに仰向けになりダンベルを押し上げる。大胸筋・三頭筋を鍛える基本種目。'},
  {n:'ダンベル インクラインプレス',cat:'upper',tags:['上半身','大胸筋上部'],sets:'10kg×3セット×10回',desc:'ベンチを30〜45度に傾けてプレス。大胸筋上部を集中強化。'},
  {n:'プッシュアップバー腕立て',cat:'upper',tags:['上半身','胸','腕','プッシュアップバー'],sets:'2〜3セット×できる回数',desc:'プッシュアップバーで手首の負担を抑えながら腕立て。胸・三頭筋・体幹を鍛える。肩痛時は浅く。'},
  {n:'ダンベル フライ',cat:'upper',tags:['上半身','大胸筋'],sets:'10kg×3セット×12回',desc:'ダンベルを弧を描くように開閉する。大胸筋の伸展・収縮を最大限に使える。'},
  {n:'ダンベル ロウ（片手）',cat:'upper',tags:['上半身','背中','猫背改善'],sets:'15〜17kg×3セット×10回',desc:'片手でベンチを支えにダンベルを引き上げる。広背筋・菱形筋を強化し猫背改善に有効。'},
  {n:'インクラインベンチ ダンベルロウ',cat:'upper',tags:['上半身','背中','猫背改善'],sets:'15kg×3セット×10回',desc:'胸をベンチに預けてダンベルを引く。腰を守りながら広背筋・菱形筋を鍛える背中の主力種目。'},
  {n:'ダンベル プルオーバー',cat:'upper',tags:['上半身','背中','広背筋'],sets:'10kg×3セット×12回',desc:'ベンチ仰向けでダンベルを頭の後ろへゆっくり下ろす。肩に痛みがない範囲で広背筋を伸ばして使う。'},
  {n:'ダンベル ショルダープレス',cat:'upper',tags:['上半身','肩'],sets:'7〜10kg×3セット×12回',desc:'肩より上にダンベルを押し上げる。三角筋全体を鍛える。'},
  {n:'アシスト懸垂（足補助）',cat:'upper',tags:['上半身','背中','懸垂'],sets:'3セット×5回',desc:'足で補助しながら懸垂動作を練習。広背筋・上腕二頭筋を鍛える。'},
  {n:'サイドレイズ',cat:'upper',tags:['上半身','三角筋中部'],sets:'7kg×3セット×15回',desc:'ダンベルを真横に肩の高さまで上げる。三角筋中部を集中強化。'},
  {n:'フロントレイズ',cat:'upper',tags:['上半身','三角筋前部'],sets:'7kg×3セット×12回',desc:'ダンベルを正面に肩の高さまで上げる。三角筋前部の強化。'},
  {n:'リアレイズ',cat:'upper',tags:['上半身','三角筋後部','猫背改善'],sets:'7kg×3セット×15回',desc:'上体を前傾させてダンベルを横に開く。三角筋後部・菱形筋を強化。'},
  {n:'ダンベル カール',cat:'upper',tags:['上半身','上腕二頭筋'],sets:'10kg×3セット×12回',desc:'肘を固定してダンベルを曲げる。上腕二頭筋強化。'},
  {n:'ハンマーカール',cat:'upper',tags:['上半身','上腕二頭筋'],sets:'10kg×3セット×12回',desc:'親指を上に向けた状態でカール。腕全体を太くする効果あり。'},
  {n:'トライセプスエクステンション',cat:'upper',tags:['上半身','上腕三頭筋'],sets:'7kg×3セット×12回',desc:'頭の後ろでダンベルを持ち肘だけを動かして伸ばす。二の腕引き締め。'},
  {n:'ケトルベルスイング',cat:'upper',tags:['上半身','全身','有酸素'],sets:'12〜16kg×3セット×15回',desc:'全身有酸素＋臀部強化。腰の状態を確認しながら実施。'},
  {n:'ハーフスクワット（浅め）',cat:'lower',tags:['下半身','大腿四頭筋','膝配慮'],sets:'ダンベル10kg×3セット×12回',desc:'膝が痛む場合は浅めのスクワット。椅子から立ち上がる動作からでもOK。'},
  {n:'レッグエクステンション',cat:'lower',tags:['下半身','大腿四頭筋'],sets:'3セット×15回',desc:'椅子に座って片脚ずつ膝を伸ばす。膝に痛みがない範囲で大腿四頭筋をゆっくり使う。'},
  {n:'ヒップスラスト',cat:'lower',tags:['下半身','臀部'],sets:'自重→17〜20kg×3セット×12回',desc:'ベンチに肩を乗せて腰を持ち上げる。臀部強化の最重要種目。'},
  {n:'ヒップヒンジ（RDL）',cat:'lower',tags:['下半身','臀部','ハムストリング'],sets:'15kg×3セット×10回',desc:'背中をまっすぐ保ったまま上体を前傾。ハムストリング・臀部・姿勢改善に効果的。'},
  {n:'カーフレイズ',cat:'lower',tags:['下半身','ふくらはぎ','足首配慮'],sets:'自重×3セット×20回',desc:'つま先立ちをゆっくり繰り返す。ふくらはぎ強化。足首の状態に合わせてゆっくり。'},
  {n:'プランク',cat:'core',tags:['体幹','腰痛予防'],sets:'30秒×3セット',desc:'うつ伏せで肘とつま先で体を支える。腰痛改善の基本種目。'},
  {n:'バードドッグ',cat:'core',tags:['体幹','腰痛予防','猫背改善'],sets:'左右各10回×3セット',desc:'四つん這いで対角線の手足をゆっくり伸ばす。体幹安定・腰痛予防の最重要種目。'},
  {n:'グルートブリッジ',cat:'core',tags:['体幹','臀部','腰痛予防'],sets:'3セット×15回',desc:'仰向けで膝を曲げ腰を持ち上げる。臀部と体幹を同時強化。'},
  {n:'バランスボール 体幹キープ',cat:'ball',tags:['バランスボール','体幹','姿勢改善'],sets:'30秒×3セット',desc:'バランスボールに座って体幹を安定させる。猫背・姿勢改善に効果的。'},
  {n:'バランスボール 腹筋ロール',cat:'ball',tags:['バランスボール','体幹','腹筋'],sets:'3セット×10回',desc:'ボールに前腕を乗せて前後に転がす。腹筋・体幹強化。'},
  {n:'バランスボール ヒップリフト',cat:'ball',tags:['バランスボール','臀部','体幹'],sets:'3セット×12回',desc:'仰向けでボールに足を乗せて腰を持ち上げる。臀部・ハムストリング強化。'},
  {n:'メディシンボール スクワット',cat:'mball',tags:['ウエイトボール','下半身','大腿四頭筋'],sets:'10kg×3セット×12回',desc:'ボールを胸に抱えてスクワット。重心が安定しやすい。'},
  {n:'メディシンボール ロシアンツイスト',cat:'mball',tags:['ウエイトボール','体幹','腹斜筋'],sets:'10kg×3セット×左右10回',desc:'座位でボールを持ち左右に体をひねる。腹斜筋・体幹強化。'},
  {n:'ディップス',cat:'dips',tags:['ディップス','上半身','胸・三頭筋'],sets:'自重×3セット×5〜8回',desc:'ディップスバーで体を上下させる。大胸筋下部・三頭筋強化。'},
  {n:'アシスト懸垂',cat:'dips',tags:['ディップス','上半身','背中'],sets:'補助つき×3セット×5回',desc:'補助を使いながら懸垂。広背筋・上腕二頭筋強化。'},
  {n:'ネガティブ懸垂',cat:'dips',tags:['ディップス','上半身','背中'],sets:'3セット×5回（5秒下ろす）',desc:'5秒かけてゆっくり下ろす。懸垂が少しできない場合の最適な練習法。'},
  {n:'ハンギングニーレイズ',cat:'dips',tags:['ディップス','体幹','腹筋'],sets:'3セット×10〜15回',desc:'ぶら下がり膝を胸に引き寄せる。腹筋・体幹強化。腰への負担が少ない。'},
  {n:'膝つき腹筋ローラー',cat:'roller',tags:['腹筋ローラー','体幹','腹筋'],sets:'3セット×8〜10回',desc:'膝をついた状態でローラーを転がす。腰が反らないよう腹に力を入れる。'},
  {n:'腹筋ローラー 壁あてロール',cat:'roller',tags:['腹筋ローラー','体幹','腹筋'],sets:'3セット×10回',desc:'壁で止めて可動域を制限した安全なやり方。腰への負担を最小限に。'},
  {n:'バンド グルートブリッジ',cat:'band',tags:['ヒップバンド','臀部','体幹'],sets:'中強度×3セット×15回',desc:'バンドを膝上に巻いてヒップリフト。通常より臀部への負荷が大幅アップ。'},
  {n:'バンド クラムシェル',cat:'band',tags:['ヒップバンド','臀部','中臀筋'],sets:'軽〜中×3セット×左右15回',desc:'横向きに寝て膝を貝のように開閉する。中臀筋強化・膝の安定性向上。'},
  {n:'バンド キックバック',cat:'band',tags:['ヒップバンド','臀部','ハムストリング'],sets:'中〜強×3セット×左右12回',desc:'四つん這いでバンドを足首に巻き後ろに蹴り上げる。大臀筋強化。'},
  {n:'ストレッチポール 背骨リセット',cat:'stretch',tags:['ストレッチポール','リカバリー','猫背改善'],sets:'5〜10分 毎日推奨',desc:'ポールを縦に置き仰向けに乗る。重力で背骨・胸椎が自然に伸びる。'},
  {n:'フォームローラー 大腿四頭筋',cat:'stretch',tags:['フォームローラー','リカバリー','膝ケア'],sets:'左右各60秒×2セット',desc:'太ももの前面をローラーでほぐす。膝への負担を軽減する効果あり。'},
  {n:'フォームローラー 背中・胸椎',cat:'stretch',tags:['フォームローラー','リカバリー','猫背改善'],sets:'60秒×2セット',desc:'仰向けでローラーを背中に置き前後に転がす。胸椎の可動域改善・猫背改善。'},
  {n:'ルームランナー ウォーキング',cat:'walk',tags:['ウォーキング','有酸素','低衝撃'],sets:'30〜60分 週3〜5回',desc:'傾斜1〜3°、速度4〜5km/hで速歩き。脂肪燃焼・体力向上。走らないこと。'},
];

const equipData=[
  {cat:'ダンベル',items:'4kg / 7kg / 10kg / 15kg / 17kg / 20kg',key:'ダンベル'},
  {cat:'ケトルベル',items:'8kg / 12kg / 16kg',key:'ケトルベル'},
  {cat:'マシン',items:'懸垂マシン / ルームランナー',key:'マシン'},
  {cat:'器具',items:'可変式トレーニングベンチ / 懸垂マシン＋ディップススタンド / プッシュアップバー',key:'懸垂'},
  {cat:'ボール類',items:'バランスボール / ウエイトボール10kg',key:'ボール'},
  {cat:'ケア用品',items:'フォームローラー / ストレッチポール',key:'ケア'},
  {cat:'バンド',items:'ヒップバンド（軽・中・強）/ 腹筋ローラー',key:'バンド'},
];
const equipEx={
  'ダンベル':[
    {n:'ダンベル チェストプレス',d:'10kg×3セット×10回',cat:'upper',day:'月・木'},
    {n:'ダンベル フライ',d:'10kg×3セット×12回',cat:'upper',day:'月・木'},
    {n:'プッシュアップバー腕立て',d:'2〜3セット×できる回数',cat:'upper',day:'月・木'},
    {n:'ダンベル ロウ',d:'15kg×3セット×10回',cat:'upper',day:'月・木'},
    {n:'インクラインベンチ ダンベルロウ',d:'15kg×3セット×10回',cat:'upper',day:'月・木'},
    {n:'ダンベル プルオーバー',d:'10kg×3セット×12回',cat:'upper',day:'月'},
    {n:'ダンベル ショルダープレス',d:'7kg×3セット×12回',cat:'upper',day:'月・木'},
    {n:'ダンベル サイドレイズ',d:'7kg×3セット×15回',cat:'upper',day:'木'},
    {n:'ダンベル フロントレイズ',d:'7kg×3セット×12回',cat:'upper',day:'木'},
    {n:'ダンベル リアレイズ',d:'7kg×3セット×15回',cat:'upper',day:'木'},
    {n:'ハンマーカール',d:'10kg×3セット×12回',cat:'upper',day:'木'},
    {n:'トライセプスエクステンション',d:'7kg×3セット×12回',cat:'upper',day:'木'},
    {n:'ヒップスラスト',d:'17kg×3セット×12回',cat:'lower',day:'火・金'},
    {n:'ヒップヒンジ / RDL',d:'15kg×3セット×10回',cat:'lower',day:'火・金'},
  ],
  'ケトルベル':[
    {n:'ケトルベルスイング',d:'12kg×3セット×15回',cat:'upper',day:'月・木'},
    {n:'ケトルベル ゴブレットスクワット',d:'12kg×3セット×12回',cat:'lower',day:'火・金'},
  ],
  'マシン':[
    {n:'ルームランナー ウォーキング',d:'30分 速度4〜5km/h',cat:'walk',day:'火・金・土・日'},
  ],
  '懸垂':[
    {n:'アシスト懸垂',d:'補助つき×3セット×5回',cat:'dips',day:'木'},
    {n:'ネガティブ懸垂',d:'3セット×5回',cat:'dips',day:'木'},
    {n:'ディップス',d:'自重×3セット×5〜8回',cat:'dips',day:'木'},
    {n:'ハンギングニーレイズ',d:'3セット×10〜15回',cat:'dips',day:'木'},
  ],
  'ボール':[
    {n:'バランスボール 体幹キープ',d:'30秒×3セット',cat:'ball',day:'水'},
    {n:'バランスボール 腹筋ロール',d:'3セット×10回',cat:'ball',day:'水'},
    {n:'メディシンボール スクワット',d:'10kg×3セット×12回',cat:'mball',day:'火・金'},
    {n:'メディシンボール ロシアンツイスト',d:'10kg×3セット×左右10回',cat:'mball',day:'水'},
  ],
  'ケア':[
    {n:'ストレッチポール 背骨リセット',d:'5〜10分',cat:'stretch',day:'毎日'},
    {n:'フォームローラー 大腿四頭筋',d:'左右各60秒',cat:'stretch',day:'毎日'},
    {n:'フォームローラー 背中・胸椎',d:'60秒×2セット',cat:'stretch',day:'毎日'},
    {n:'フォームローラー 臀部',d:'左右各60秒',cat:'stretch',day:'毎日'},
  ],
  'バンド':[
    {n:'バンド グルートブリッジ',d:'中強度×3セット×15回',cat:'band',day:'火・金'},
    {n:'バンド クラムシェル',d:'軽〜中×3セット×左右15回',cat:'band',day:'火・金'},
    {n:'バンド キックバック',d:'中〜強×3セット×左右12回',cat:'band',day:'火・金'},
    {n:'膝つき腹筋ローラー',d:'3セット×8回',cat:'roller',day:'水'},
    {n:'腹筋ローラー 壁あてロール',d:'3セット×10回',cat:'roller',day:'水'},
  ],
};

const bodyParts=[
  {id:'knee',label:'両膝靭帯',icon:'🦵'},
  {id:'ankle',label:'足首',icon:'🦶'},
  {id:'back',label:'腰',icon:'🔙'},
  {id:'shoulder',label:'肩・首',icon:'💆'},
  {id:'elbow',label:'肘',icon:'💪'},
  {id:'wrist',label:'手首',icon:'🤲'},
];
const painLevels=[
  {v:0,label:'問題なし',color:'var(--green)'},
  {v:1,label:'違和感',color:'var(--amber)'},
  {v:2,label:'痛みあり',color:'var(--coral)'},
  {v:3,label:'強い痛み',color:'#cc2200'},
];
const goalItems=[
  {id:'weight',label:'体重',unit:'kg'},
  {id:'fat',label:'体脂肪率',unit:'%'},
  {id:'muscle',label:'筋肉量',unit:'kg'},
  {id:'pullup',label:'懸垂',unit:'回'},
];

// ===== 4-WEEK ROTATION =====
const cycleNames=['第1週 基礎フォーム','第2週 回数・筋持久力','第3週 片側・安定性','第4週 軽負荷・丁寧な動作'];
const P=(...rows)=>rows.map(([n,d,c=null])=>({n,d,c}));
const rotationPlans=[
  {
    mon:P(['ダンベル チェストプレス（ベンチ仰向け）','3×8〜10回'],['ダンベル ロウ（片手・ベンチ支持）','3×左右10回'],['プッシュアップバー腕立て','2×できる回数'],['アシスト懸垂（足補助）','3×5回'],['ダンベル サイドレイズ','2×12回'],['ダンベル カール','2×10回'],['デッドバグ','左右8回×2']),
    tue:P(['ハーフスクワット（ダンベル持ち）','3×10回','痛みは浅めに'],['ヒップスラスト（ベンチ使用）','3×10回'],['椅子レッグエクステンション（自重）','左右12回×2'],['カーフレイズ（ゆっくり）','3×15回'],['バンド クラムシェル','左右12回×2'],['ヒップヒンジ / RDL','2×10回'],['バードドッグ（対角手足伸ばし）','左右8回×2']),
    wed:P(['プランク','20〜30秒×3'],['バードドッグ（対角手足伸ばし）','左右8回×2'],['グルートブリッジ','2×12回'],['バランスボール 体幹キープ（座位）','30秒×3'],['デッドバグ','左右8回×2']),
    thu:P(['インクラインベンチ ダンベルロウ','3×10回'],['ダンベル インクラインプレス（ベンチ角度上げ）','3×10回'],['ダンベル リアレイズ（前傾）','2×12回'],['ハンマーカール','2×10回'],['ダンベル トライセプスエクステンション','2×10回'],['ネガティブ懸垂','3×3回（5秒下ろす）'],['プランク','20秒×2']),
    fri:P(['ヒップヒンジ / RDL','3×8〜10回'],['ヒップスラスト（ベンチ使用）','3×12回'],['ハーフスクワット（ダンベル持ち）','2×10回'],['カーフレイズ（ゆっくり）','3×15回'],['バンド グルートブリッジ','2×12回'],['椅子レッグエクステンション（自重）','左右12回×2'],['デッドバグ','左右8回×2']),
  },
  {
    mon:P(['プッシュアップバー腕立て','3×8〜15回'],['インクラインベンチ ダンベルロウ','3×12回'],['ダンベル フライ（ベンチ）','2×12〜15回'],['アシスト懸垂（足補助）','3×5〜6回'],['ダンベル フロントレイズ','2×12回'],['ハンマーカール','2×12回'],['バードドッグ（対角手足伸ばし）','左右10回×2']),
    tue:P(['椅子レッグエクステンション（自重）','左右15回×3'],['ヒップスラスト（ベンチ使用）','3×15回'],['ハーフスクワット（ダンベル持ち）','3×12回'],['カーフレイズ（ゆっくり）','3×20回'],['バンド クラムシェル','左右15回×3'],['グルートブリッジ','2×15回'],['プランク','20秒×3']),
    wed:P(['デッドバグ','左右10回×3'],['バランスボール 腹筋ロール','2×8回'],['グルートブリッジ','3×15回'],['ウエイトボール ロシアンツイスト','左右8回×2'],['バランスボール 体幹キープ（座位）','40秒×2']),
    thu:P(['ダンベル プルオーバー（ベンチ）','3×12回'],['ダンベル チェストプレス（ベンチ仰向け）','3×12回'],['ダンベル サイドレイズ','3×15回'],['コンセントレーションカール','左右12回×2'],['ダンベル キックバック（三頭筋）','左右12回×2'],['アシスト懸垂（足補助）','3×5回'],['デッドバグ','左右8回×2']),
    fri:P(['ヒップスラスト（ベンチ使用）','3×15回'],['ヒップヒンジ / RDL','3×12回'],['バンド グルートブリッジ','3×15回'],['カーフレイズ（ゆっくり）','3×20回'],['椅子レッグエクステンション（自重）','左右15回×3'],['バンド クラムシェル','左右15回×2'],['バードドッグ（対角手足伸ばし）','左右10回×2']),
  },
  {
    mon:P(['ダンベル ロウ（片手・ベンチ支持）','左右8回×3'],['ダンベル インクラインプレス（ベンチ角度上げ）','3×8回'],['アシスト懸垂（足補助）','3×4〜5回'],['プッシュアップバー腕立て','2×できる回数'],['ダンベル リアレイズ（前傾）','2×12回'],['ダンベル カール','左右交互10回×2'],['バードドッグ（対角手足伸ばし）','左右8回×2']),
    tue:P(['ハーフスクワット（ダンベル持ち）','3×8回'],['バンド クラムシェル','左右12回×3'],['ヒップスラスト（ベンチ使用）','片脚補助 左右8回×2'],['カーフレイズ（ゆっくり）','片脚補助 左右10回×2'],['ヒップヒンジ / RDL','3×8回'],['椅子レッグエクステンション（自重）','左右12回×2'],['デッドバグ','左右8回×2']),
    wed:P(['バードドッグ（対角手足伸ばし）','左右8回×3'],['デッドバグ','左右8回×3'],['バランスボール 体幹キープ（座位）','30秒×3'],['グルートブリッジ','片脚補助 左右8回×2'],['プランク','20秒×3']),
    thu:P(['インクラインベンチ ダンベルロウ','3×8〜10回'],['ダンベル チェストプレス（ベンチ仰向け）','左右交互8回×3'],['ダンベル ショルダープレス','左右交互8回×2'],['ハンマーカール','左右交互10回×2'],['ダンベル トライセプスエクステンション','2×10回'],['ネガティブ懸垂','3×3回'],['プランク','20秒×2']),
    fri:P(['ヒップヒンジ / RDL','3×8回'],['ヒップスラスト（ベンチ使用）','3×10回'],['バンド クラムシェル','左右12回×3'],['カーフレイズ（ゆっくり）','片脚補助 左右10回×2'],['ハーフスクワット（ダンベル持ち）','2×8回'],['バンド グルートブリッジ','2×12回'],['バードドッグ（対角手足伸ばし）','左右8回×2']),
  },
  {
    mon:P(['ダンベル チェストプレス（ベンチ仰向け）','軽め3×12回（3秒下ろす）'],['インクラインベンチ ダンベルロウ','軽め3×12回'],['プッシュアップバー腕立て','2×余裕を3回残す'],['ダンベル プルオーバー（ベンチ）','軽め2×12回'],['ダンベル サイドレイズ','軽め2×15回'],['ハンマーカール','軽め2×12回'],['デッドバグ','左右8回×2']),
    tue:P(['ハーフスクワット（ダンベル持ち）','軽め3×12回（3秒下ろす）'],['ヒップスラスト（ベンチ使用）','軽め3×12回（上で2秒）'],['椅子レッグエクステンション（自重）','左右15回×2'],['カーフレイズ（ゆっくり）','2×20回'],['バンド クラムシェル','軽め 左右15回×2'],['ヒップヒンジ / RDL','軽め2×10回'],['バードドッグ（対角手足伸ばし）','左右8回×2']),
    wed:P(['プランク','20秒×2'],['バードドッグ（対角手足伸ばし）','左右8回×2'],['グルートブリッジ','2×15回'],['バランスボール 体幹キープ（座位）','30秒×2']),
    thu:P(['ダンベル ロウ（片手・ベンチ支持）','軽め3×12回'],['ダンベル インクラインプレス（ベンチ角度上げ）','軽め3×12回'],['ダンベル リアレイズ（前傾）','軽め2×15回'],['ダンベル カール','軽め2×12回'],['ダンベル キックバック（三頭筋）','軽め2×12回'],['アシスト懸垂（足補助）','2×4回'],['デッドバグ','左右8回×2']),
    fri:P(['ヒップヒンジ / RDL','軽め3×10回（3秒下ろす）'],['ヒップスラスト（ベンチ使用）','軽め3×15回'],['ハーフスクワット（ダンベル持ち）','軽め2×12回'],['カーフレイズ（ゆっくり）','2×20回'],['バンド グルートブリッジ','軽め2×15回'],['椅子レッグエクステンション（自重）','左右15回×2'],['バードドッグ（対角手足伸ばし）','左右8回×2']),
  },
];
function mondayOf(date){const d=new Date(date),day=d.getDay();d.setHours(0,0,0,0);d.setDate(d.getDate()-day+(day===0?-6:1));return d;}
function cycleWeekFor(date){const anchor=new Date(2026,5,1);const diff=Math.floor((mondayOf(date)-anchor)/604800000);return ((diff%4)+4)%4;}
function dayPlanKey(day){return ({1:'mon',2:'tue',3:'wed',4:'thu',5:'fri'})[day]||null;}
function planForDate(date,minutes=dur){const key=dayPlanKey(date.getDay());if(!key)return [];const full=rotationPlans[cycleWeekFor(date)][key]||[];return minutes===30?full.slice(0,4):full.slice(0,7);}

// ===== STATE =====
let dur=30;
let chk={};
let walkOn=false,walkSec=0,walkIv=null;
let customEx=JSON.parse(localStorage.getItem('hgCEx')||'[]');
let wkCnt=parseInt(localStorage.getItem('hgWk')||'0');
let weekOff=0;

// ===== HELPERS =====
function pad(n){return String(n).padStart(2,'0');}
function getNotes(){return JSON.parse(localStorage.getItem('hgNotes')||'[]');}
function saveNotes(n){localStorage.setItem('hgNotes',JSON.stringify(n));}

// ===== TODAY =====
function setDur(d){
  dur=d;
  document.getElementById('d60').classList.toggle('sel',d===60);
  document.getElementById('d30').classList.toggle('sel',d===30);
  renderToday();
}

function getCatCustom(cat){return customEx.filter(e=>e.cat===cat);}

function todayMode(){
  const d=new Date().getDay();
  if(d===6)return 'walk';
  if(d===0)return 'walk';
  if(d===1||d===4)return 'upper';
  if(d===2||d===5)return 'lower';
  return 'core';
}

function setBlockVisible(cardId,visible){
  const card=document.getElementById(cardId);
  if(!card)return;
  const sec=card.previousElementSibling;
  card.style.display=visible?'block':'none';
  if(sec&&sec.classList.contains('sec'))sec.style.display=visible?'flex':'none';
}

function renderToday(){
  const mode=todayMode();
  const now=new Date();
  const plan=planForDate(now,dur);
  const custom=mode==='upper'?getCatCustom('upper'):mode==='lower'?[...getCatCustom('lower'),...getCatCustom('band')]:[...getCatCustom('core'),...getCatCustom('ball'),...getCatCustom('roller')];
  const limit=dur===30?4:7;
  const chosen=custom.length?[...plan.slice(0,Math.max(0,limit-1)),custom[0]]:plan;
  const note=document.getElementById('cycleNote');
  if(note)note.innerHTML='<strong>'+cycleNames[cycleWeekFor(now)]+'</strong>｜'+(dur===30?'主種目4種目・約30分':'最大7種目・約60分');
  renderExBlock('cm',morning,'m',[]);
  renderExBlock('cw',warmup,'w',[]);
  renderExBlock('cu',mode==='upper'?chosen:[],'u',[]);
  renderExBlock('cl',mode==='lower'?chosen:[],'l',[]);
  renderExBlock('cc',mode==='core'?chosen:[],'c',[]);
  renderStretch();
  const durRow=document.querySelector('.dur-row');
  if(durRow)durRow.style.display='flex';
  setBlockVisible('cw',mode!=='rest'&&mode!=='walk');
  setBlockVisible('cu',mode==='upper');
  setBlockVisible('cl',mode==='lower');
  setBlockVisible('cc',mode==='core');
  const walkCard=document.querySelector('.walk-timer')?.closest('.card');
  const walkSecTitle=walkCard?.previousElementSibling;
  if(walkCard){walkCard.style.display=(mode==='walk'||mode==='lower')?'block':'none';}
  if(walkSecTitle&&walkSecTitle.classList.contains('sec'))walkSecTitle.style.display=(mode==='walk'||mode==='lower')?'flex':'none';
  updateProg();
}

function muscleInfo(e){
  const name=((e&&e.n)||'')+' '+((e&&e.cat)||'')+' '+(((e&&e.tags)||[]).join(' '));
  const items=[];
  const add=(key,label)=>{if(!items.some(x=>x.key===key))items.push({key,label});};
  if(/チェスト|フライ|プッシュアップ|ディップス|胸|プレス/.test(name))add('chest','胸');
  if(/ロー|懸垂|ラット|バック|背中|プル|マシンロー/.test(name))add('back','背中');
  if(/ショルダー|サイドレイズ|リアレイズ|肩/.test(name))add('shoulder','肩');
  if(/カール|トライセプス|二頭|三頭|腕/.test(name))add('arm','腕');
  if(/腹|プランク|デッドバグ|バードドッグ|体幹|コア|ローラー|T-Betabs/.test(name))add('core','体幹');
  if(/ヒップ|臀|グルート|ブリッジ|デッドリフト/.test(name))add('glute','臀部');
  if(/スクワット|ランジ|ステップアップ|四頭|大腿|太腿|脚|下半身/.test(name))add('quad','太腿');
  if(/カーフ|ふくらはぎ|脹脛/.test(name))add('calf','脹脛');
  if(/ストレッチ|フォームローラー|リカバリー|ポール|T-ストレッチ/.test(name))add('recovery','回復');
  if(!items.length && /lower|band/.test(name)){add('glute','臀部');add('quad','太腿');}
  if(!items.length && /upper|dips/.test(name)){add('chest','胸');add('shoulder','肩');}
  if(!items.length && /core|ball|mball|roller/.test(name))add('core','体幹');
  return items;
}

function muscleHtml(e){
  const info=muscleInfo(e);
  const detail=detailMuscleInfo(e);
  return '<div class="muscle-map" aria-label="鍛える部位">'+info.map(m=>'<span class="active muscle-'+m.key+'">'+m.label+'</span>').join('')+'</div>'
    +(detail.length?'<div class="muscle-detail"><strong>主に効く筋肉：</strong>'+detail.join('・')+'</div>':'');
}

function detailMuscleInfo(e){
  const name=((e&&e.n)||'')+' '+((e&&e.cat)||'')+' '+(((e&&e.tags)||[]).join(' '));
  const list=[];
  const add=(...names)=>names.forEach(label=>{if(!list.includes(label))list.push(label);});

  if(/インクライン.*プレス/.test(name))add('大胸筋上部','上腕三頭筋','三角筋前部');
  else if(/チェストプレス|プッシュアップ|腕立て/.test(name))add('大胸筋中央部','上腕三頭筋','三角筋前部');
  if(/フライ/.test(name))add('大胸筋');
  if(/ディップス/.test(name))add('大胸筋下部','上腕三頭筋');

  if(/ロウ|ロー（|ローイング/.test(name))add('広背筋','菱形筋','僧帽筋中部','上腕二頭筋');
  if(/懸垂|ラットプル/.test(name))add('広背筋','大円筋','上腕二頭筋');
  if(/プルオーバー/.test(name))add('広背筋','大円筋','大胸筋');
  if(/リアレイズ/.test(name))add('三角筋後部','菱形筋','僧帽筋中部');

  if(/ショルダープレス/.test(name))add('三角筋前部','三角筋中部','上腕三頭筋');
  if(/サイドレイズ/.test(name))add('三角筋中部','棘上筋');
  if(/フロントレイズ/.test(name))add('三角筋前部');

  if(/ハンマーカール/.test(name))add('上腕筋','腕橈骨筋','上腕二頭筋');
  else if(/カール/.test(name))add('上腕二頭筋','上腕筋');
  if(/トライセプスエクステンション/.test(name))add('上腕三頭筋長頭');
  if(/キックバック/.test(name))add('上腕三頭筋外側頭','上腕三頭筋内側頭');

  if(/スクワット|レッグエクステンション/.test(name))add('大腿四頭筋');
  if(/ヒップスラスト|グルートブリッジ|ブリッジ/.test(name))add('大臀筋','中臀筋');
  if(/ヒップヒンジ|RDL|デッドリフト/.test(name))add('ハムストリングス','大臀筋','脊柱起立筋');
  if(/クラムシェル/.test(name))add('中臀筋','小臀筋','深層外旋六筋');
  if(/カーフ/.test(name))add('腓腹筋','ヒラメ筋');
  if(/ケトルベルスイング/.test(name))add('大臀筋','ハムストリングス','脊柱起立筋');

  if(/プランク|ローラー|体幹キープ/.test(name))add('腹横筋','腹直筋','内外腹斜筋');
  if(/デッドバグ/.test(name))add('腹横筋','腹直筋','腸腰筋');
  if(/バードドッグ/.test(name))add('腹横筋','多裂筋','脊柱起立筋','大臀筋');
  if(/ロシアンツイスト/.test(name))add('内腹斜筋','外腹斜筋','腹直筋');

  if(/大腿四頭筋ほぐし/.test(name))add('大腿四頭筋');
  if(/背中・胸椎|背骨リセット/.test(name))add('胸椎周辺','脊柱起立筋','僧帽筋');
  if(/臀部ほぐし/.test(name))add('大臀筋','中臀筋','梨状筋');
  if(/肩回し|首ストレッチ/.test(name))add('僧帽筋上部','肩甲挙筋','胸鎖乳突筋');
  if(/足首回し|ふくらはぎストレッチ/.test(name))add('腓腹筋','ヒラメ筋','足首周辺');
  if(/キャットカウ/.test(name))add('脊柱起立筋','多裂筋','腹部深層筋');
  return list;
}

function effectText(e){
  const info=muscleInfo(e);
  if(info.length===1&&info[0].key==='recovery')return '筋肉を強く追い込むより、関節の可動域と姿勢を整える目的です。硬さを抜いてから動くことで、膝・腰・肩への負担を減らしやすくなります。';
  const detailed=detailMuscleInfo(e);
  const muscles=detailed.length?detailed.slice(0,4).join('・'):info.filter(x=>x.key!=='recovery').map(x=>x.label).join('・');
  if(muscles)return muscles+'を主に使います。狙った部位に力を入れ続け、反動を使わず、痛みのない範囲でゆっくり動かすと効果が出やすくなります。';
  return '姿勢を整え、関節に負担をかけずに体を動かすための種目です。呼吸を止めず、違和感が出る前で止めます。';
}

function enrichedDesc(e){
  const base=exDesc[e.n]||e.desc||e.d||'';
  const extra='<br><br><strong>効く理由：</strong>'+effectText(e)+'<br><strong>やり方の目安：</strong>最初に姿勢を作り、上げる時より下ろす時を少しゆっくりにします。膝・腰・首・肩に痛みが出る角度では行わず、可動域を小さくして継続を優先します。';
  return base?base+extra:extra;
}

function renderExBlock(id,data,prefix,extra){
  const all=[...data,...extra];
  document.getElementById(id).innerHTML=all.map((e,i)=>{
    const k=prefix+i;
    const done=!!chk[k];
    const isC=i>=data.length;
    const desc=enrichedDesc(e);
    return `<div class="ex-row">
      <div class="ex-top">
        <div class="ex-check${done?' done':''}" onclick="toggleChk('${k}',this)">${done?'✓':''}</div>
        <div class="ex-main">
          <div class="ex-name${done?' done':''}">${e.n}${isC?'<span class="custom-badge">追加</span>':''}</div>
          <div class="ex-detail">${e.d}</div>
          ${muscleHtml(e)}
        </div>
        ${e.c?`<div class="ex-caution">${e.c}</div>`:''}
        ${desc?`<div class="ex-info" onclick="toggleDesc('xd-${k}')">ℹ️</div>`:''}
      </div>
      ${desc?`<div class="ex-desc" id="xd-${k}">${desc}</div>`:''}
    </div>`;
  }).join('');
}

function renderStretch(){
  document.getElementById('cs').innerHTML=stretchData.map((e,i)=>{
    const k='s'+i;const done=!!chk[k];
    return `<div class="ex-row">
      <div class="ex-top">
        <div class="ex-check${done?' done':''}" onclick="toggleChk('${k}',this)">${done?'✓':''}</div>
        <div class="ex-main"><div class="ex-name${done?' done':''}">${e.n}</div><div class="ex-detail">${e.d}</div>${muscleHtml(e)}</div>
        ${e.c?`<div class="ex-caution">${e.c}</div>`:''}
        <div class="ex-info" onclick="toggleDesc('xd-${k}')">ℹ️</div>
      </div>
      <div class="ex-desc" id="xd-${k}">${e.desc}</div>
    </div>`;
  }).join('');
}

function toggleChk(k,el){
  chk[k]=!chk[k];
  el.classList.toggle('done',chk[k]);
  el.textContent=chk[k]?'✓':'';
  const row=el.closest('.ex-row');
  if(row){const nm=row.querySelector('.ex-name');if(nm)nm.classList.toggle('done',chk[k]);}
  updateProg();
}

function toggleDesc(id){
  const el=document.getElementById(id);
  if(el)el.style.display=el.style.display==='block'?'none':'block';
}

function updateProg(){
  const up=dur===60?upperF:upperS;
  const lo=dur===60?lowerF:lowerS;
  const co=dur===60?coreF:coreS;
  const mode=todayMode();
  const cats=[
    {id:'m',label:'朝ベッド',icon:'🛏️',total:morning.length,color:'var(--green)'},
    ...(mode!=='rest'&&mode!=='walk'?[{id:'w',label:'ウォームアップ',icon:'🔥',total:warmup.length,color:'var(--amber)'}]:[]),
    ...(mode==='upper'?[{id:'u',label:'上半身',icon:'💪',total:planForDate(new Date(),dur).length,color:'var(--blue)'}]:[]),
    ...(mode==='lower'?[{id:'l',label:'下半身',icon:'🦵',total:planForDate(new Date(),dur).length,color:'var(--green)'}]:[]),
    ...(mode==='core'?[{id:'c',label:'体幹・ボール',icon:'🏋️',total:planForDate(new Date(),dur).length,color:'var(--amber)'}]:[]),
    {id:'s',label:'リカバリー',icon:'🧘',total:stretchData.length,color:'#20a090'},
  ];
  const wMin=Math.floor(walkSec/60);
  const wPct=Math.min(100,Math.round(walkSec/1800*100));
  const wCol=walkSec>=1800?'var(--green)':walkSec>0?'var(--amber)':'var(--border)';

  let h='<div class="prog-title">📊 今日の進捗</div>';
  cats.forEach(cat=>{
    const done=Array.from({length:cat.total},(_,i)=>chk[cat.id+i]).filter(Boolean).length;
    const pct=cat.total>0?Math.round(done/cat.total*100):0;
    const col=pct===100?'var(--green)':pct>0?cat.color:'var(--border)';
    h+=`<div class="prog-row">
      <div class="prog-label"><span class="prog-name">${cat.icon} ${cat.label}</span><span class="prog-val" style="color:${col}">${done} / ${cat.total}</span></div>
      <div class="prog-bar-bg"><div class="prog-bar" style="width:${pct}%;background:${col}"></div></div>
    </div>`;
  });
  if(mode==='walk'||mode==='lower'){
    h+=`<div class="prog-row">
      <div class="prog-label"><span class="prog-name">🚶 ウォーキング</span><span class="prog-val" style="color:${wCol}">${wMin} / 30分</span></div>
      <div class="prog-bar-bg"><div class="prog-bar" style="width:${wPct}%;background:${wCol}"></div></div>
    </div>`;
  }
  document.getElementById('catProg').innerHTML=h;
}

// ===== WALK =====
function toggleWalk(){
  if(!walkOn){
    walkOn=true;
    document.getElementById('wBtn').textContent='停止';
    document.getElementById('wBtn').className='wbtn wbtn-p';
    walkIv=setInterval(()=>{walkSec++;updWalk();updateProg();},1000);
  } else {
    walkOn=false;
    document.getElementById('wBtn').textContent='再開';
    document.getElementById('wBtn').className='wbtn wbtn-s';
    clearInterval(walkIv);
  }
}
function resetWalk(){
  walkOn=false;clearInterval(walkIv);walkSec=0;
  document.getElementById('wBtn').textContent='開始';
  document.getElementById('wBtn').className='wbtn wbtn-s';
  updWalk();updateProg();
}
function updWalk(){
  const m=Math.floor(walkSec/60),s=walkSec%60;
  document.getElementById('wTimer').textContent=pad(m)+':'+pad(s);
  document.getElementById('wBar').style.width=Math.min(100,Math.round(walkSec/1800*100))+'%';
}

// ===== END WORKOUT =====
function endWorkout(){
  const memo='';
  if(memo){
    const now=new Date();
    const ds=now.getFullYear()+'年'+(now.getMonth()+1)+'月'+now.getDate()+'日（'+DJ[now.getDay()]+'）';
    const notes=getNotes();
    notes.unshift({date:ds,text:memo,id:Date.now()});
    if(notes.length>50)notes.pop();
    saveNotes(notes);
  }
  wkCnt=Math.min(5,wkCnt+1);
  localStorage.setItem('hgWk',String(wkCnt));
  const history=JSON.parse(localStorage.getItem('hgHistory')||'[]');
  const dayKey=new Date().toISOString().slice(0,10);
  if(!history.includes(dayKey)){history.push(dayKey);localStorage.setItem('hgHistory',JSON.stringify(history.slice(-120)));}
  chk={};renderToday();resetWalk();
  alert('✅ お疲れ様でした！実施履歴に追加しました');
}

// ===== SCHEDULE =====
function chgWeek(d){
  const n=weekOff+d;
  if(n<-4||n>4){alert(n<0?'4週前までです':'4週先までです');return;}
  weekOff=n;renderSchedule();
}

function renderSchedule(){
  const today=new Date();const dow=today.getDay();
  const mon=new Date(today);mon.setDate(today.getDate()-dow+(dow===0?-6:1)+weekOff*7);
  const sun=new Date(mon);sun.setDate(mon.getDate()+6);
  const lbl=weekOff===0?'今週':weekOff<0?Math.abs(weekOff)+'週前':weekOff+'週後';
  document.getElementById('wkLbl').innerHTML=lbl+'<br><span style="font-size:13px;font-weight:500">'+
    (mon.getMonth()+1)+'/'+mon.getDate()+'（月）〜'+(sun.getMonth()+1)+'/'+sun.getDate()+'（日）</span>';
  document.getElementById('btnPrev').disabled=weekOff<=-4;
  document.getElementById('btnNext').disabled=weekOff>=4;

  const labels=['上半身','下半身','体幹','上半身','下半身','歩行','歩行'];
  let h='';
  for(let i=0;i<7;i++){
    const dt=new Date(mon);dt.setDate(mon.getDate()+i);
    const isToday=weekOff===0&&dt.toDateString()===today.toDateString();
    const isRest=false;
    h+=`<div class="day-cell${isToday?' today':isRest?' rest':''}" onclick="showDay(${i},'${dt.getMonth()+1}/${dt.getDate()}')">
      <div class="day-name">${['月','火','水','木','金','土','日'][i]}</div>
      <div class="day-num">${dt.getDate()}</div>
      <div class="day-type">${labels[i]}</div>
    </div>`;
  }
  document.getElementById('wkGrid').innerHTML=h;
  document.getElementById('dayDetail').innerHTML='';

  const picons={upper:'💪',lower:'🦵',core:'🔥',walk:'🚶',rest:'😴'};
  const pcols={upper:'var(--blue-light)',lower:'var(--green-light)',core:'var(--amber-light)',walk:'var(--purple-light)',rest:'var(--surface2)'};
  const cycleTitle='<div class="cycle-note"><strong>'+cycleNames[cycleWeekFor(mon)]+'</strong>｜筋トレ日は30分4種目／60分最大7種目</div>';
  document.getElementById('wkProg').innerHTML=cycleTitle+weeklyProg.map((p,idx)=>{
    const relCats={0:['upper','core'],1:['lower','walk','band','mball'],2:['core','ball','roller','stretch'],3:['upper','dips'],4:['lower','band','mball'],5:['walk'],6:['walk']}[idx]||[];
    const cEx=customEx.filter(e=>relCats.includes(e.cat));
    const cHtml=cEx.length?`<div style="margin-top:6px;padding:6px 10px;background:var(--purple-light);border-radius:8px;font-size:12px;color:var(--purple-dark);font-weight:600">➕ 追加：${cEx.map(e=>e.n).join('・')}</div>`:'';
    return `<div class="prog-row2">
      <div class="prog-icon" style="background:${pcols[p.type]}">${picons[p.type]}</div>
      <div class="prog-content">
        <div class="prog-day">${p.day}</div>
        <div class="prog-nm">${p.label}</div>
        <div class="prog-dc">${p.desc}</div>
        <div class="prog-tm">⏱ ${p.type==='walk'?30:dur}分</div>
        ${cHtml}
      </div>
    </div>`;
  }).join('');
  document.getElementById('injBox').innerHTML=injuryList.map(t=>`<div class="inj-item">${t}</div>`).join('');
}

const dayProgs=[
  {label:'上半身A + 体幹',icon:'💪',dur:'60分',cats:['upper','core']},
  {label:'下半身A + ウォーキング',icon:'🦵',dur:'60分',cats:['lower','walk','band']},
  {label:'体幹 + バランスボール',icon:'🔥',dur:'30分',cats:['core','ball','roller','stretch']},
  {label:'上半身B + ディップス',icon:'💪',dur:'60分',cats:['upper','dips']},
  {label:'下半身B + ウォーキング',icon:'🦵',dur:'60分',cats:['lower','band','mball']},
  {label:'ウォーキングのみ',icon:'🚶',dur:'30分',cats:['walk']},
  {label:'ウォーキングのみ',icon:'🚶',dur:'30分',cats:['walk']},
];

function showDay(idx,dateStr){
  const p=dayProgs[idx];
  if(!p.cats.length){
    document.getElementById('dayDetail').innerHTML=`<div class="card" style="border-color:var(--green);margin-top:4px"><div style="font-size:16px;font-weight:700;margin-bottom:4px">${p.icon} ${dateStr} ${p.label}</div><div style="font-size:15px;color:var(--text3)">休養日 — しっかり休みましょう！</div></div>`;
    return;
  }
  const allEx=[];
  const today=new Date();const dow=today.getDay();
  const selectedMon=new Date(today);selectedMon.setDate(today.getDate()-dow+(dow===0?-6:1)+weekOff*7);
  const selectedDate=new Date(selectedMon);selectedDate.setDate(selectedMon.getDate()+idx);
  planForDate(selectedDate,dur).forEach(e=>allEx.push({...e,grp:p.cats.includes('upper')?'上半身':p.cats.includes('lower')?'下半身':'体幹'}));
  if(p.cats.includes('walk'))allEx.push({n:'ルームランナー ウォーキング',d:'30〜60分 速度4〜5km/h',c:'走らない',grp:'歩行'});
  if(p.cats.includes('dips')){
    [{n:'アシスト懸垂',d:'補助つき×3セット×5回'},{n:'ディップス',d:'自重×3セット×5〜8回'}].forEach(e=>allEx.push({...e,c:null,grp:'ディップス'}));
  }
  customEx.filter(e=>p.cats.includes(e.cat)).forEach(e=>allEx.push({...e,grp:'追加'}));
  const catCols={upper:'#0e2040',lower:'#1a3d30',core:'#3d2e0a',歩行:'#1e1840',ディップス:'#0e2a3a',追加:'#1e1840'};
  const catTCols={upper:' #a0c8ff',lower:'#a8f0d8',core:'#ffd080',歩行:'#c8b8ff',ディップス:'#80d0ff',追加:'#c8b8ff'};
  const exH=allEx.map(e=>`<div style="display:flex;align-items:center;gap:10px;padding:8px 0;border-top:1px solid var(--border)">
    <div style="font-size:11px;padding:2px 7px;border-radius:5px;background:${catCols[e.grp]||'#1a3d30'};color:${catTCols[e.grp]||'#a8f0d8'};font-weight:700;white-space:nowrap;flex-shrink:0">${e.grp}</div>
    <div style="flex:1"><div style="font-size:15px;font-weight:500">${e.n}</div><div style="font-size:13px;color:var(--text3)">${e.d}</div></div>
    ${e.c?`<div style="font-size:12px;color:var(--coral-dark);background:var(--coral-light);padding:2px 7px;border-radius:5px;font-weight:600;white-space:nowrap">${e.c}</div>`:''}
  </div>`).join('');
  document.getElementById('dayDetail').innerHTML=`<div class="card" style="border-color:var(--green);margin-top:4px">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:10px">
      <div><div style="font-size:13px;color:var(--text3);font-weight:600">${dateStr} の予定</div><div style="font-size:17px;font-weight:700;margin-top:2px">${p.icon} ${p.label}</div></div>
      <span style="padding:6px 12px;background:var(--green-light);color:var(--green-dark);border-radius:8px;font-size:14px;font-weight:700">⏱ ${p.cats.includes('walk')?30:dur}分</span>
    </div>${exH}</div>`;
  document.getElementById('dayDetail').scrollIntoView({behavior:'smooth',block:'nearest'});
}

// ===== LIBRARY =====
const libCats=[
  {id:'all',label:'すべて'},{id:'upper',label:'上半身'},{id:'lower',label:'下半身'},
  {id:'core',label:'体幹'},{id:'ball',label:'バランスボール'},{id:'mball',label:'ウエイトボール'},
  {id:'dips',label:'ディップス'},{id:'roller',label:'腹筋ローラー'},{id:'band',label:'ヒップバンド'},
  {id:'stretch',label:'ストレッチ'},{id:'walk',label:'ウォーキング'},
  {id:'m-chest',label:'胸'},{id:'m-back',label:'背中'},{id:'m-shoulder',label:'肩'},
  {id:'m-arm',label:'腕'},{id:'m-core',label:'体幹'},{id:'m-glute',label:'臀部'},
  {id:'m-quad',label:'太腿'},{id:'m-calf',label:'脹脛'},{id:'m-recovery',label:'回復'},
];
const tagCls={upper:'tu',lower:'tl',core:'tc',walk:'tw',ball:'tb',mball:'tm',dips:'td',roller:'tr',band:'tbd',stretch:'ts'};
const badgeCls={upper:'bb',lower:'bg',core:'ba',walk:'bp',ball:'bg',mball:'ba',dips:'bb',roller:'ba',band:'bp',stretch:'bg'};
const catLbl={upper:'上半身',lower:'下半身',core:'体幹',walk:'歩行',ball:'ボール',mball:'ウエイト',dips:'ディップス',roller:'ローラー',band:'バンド',stretch:'ストレッチ'};

function renderLibrary(cat){
  document.getElementById('filterRow').innerHTML=libCats.map(c=>
    `<button class="fbtn${c.id===cat?' sel':''}" onclick="renderLibrary('${c.id}')">${c.label}</button>`
  ).join('');
  const all=[...libData,...customEx.map(e=>({n:e.n,cat:e.cat,tags:[catLbl[e.cat]||e.cat,'追加種目'],sets:e.d,desc:'追加した種目です',custom:true}))];
  const data=cat==='all'
    ?all
    :cat.startsWith('m-')
      ?all.filter(e=>muscleInfo(e).some(m=>m.key===cat.slice(2)))
      :all.filter(e=>e.cat===cat);
  document.getElementById('libList').innerHTML=data.map((e,idx)=>`
    <div class="lib-card">
      <div class="lib-hd">
        <div class="lib-nm">${e.n}${e.custom?'<span class="custom-badge">追加</span>':''}</div>
        <span class="badge ${badgeCls[e.cat]||'bb'}">${catLbl[e.cat]||e.cat}</span>
      </div>
      <div class="lib-tags">${(e.tags||[]).map(t=>`<span class="tag ${tagCls[e.cat]||'tu'}">${t}</span>`).join('')}</div>
      ${muscleHtml(e)}
      <div class="lib-desc">${e.desc||''}</div>
      <div class="lib-effect">効く理由：${effectText(e)}</div>
      <div class="lib-sets">📋 ${e.sets||''}</div>
      ${e.custom?`<button onclick="removeCustomEx(${customEx.findIndex(c=>c.n===e.n)})" style="margin-top:8px;padding:6px 12px;background:var(--coral-light);color:var(--coral-dark);border:none;border-radius:6px;font-size:13px;font-weight:700;cursor:pointer">🗑 削除</button>`:''}
    </div>`).join('') + `<div class="sec"><span class="dot" style="background:var(--text3)"></span>種目を追加する</div>
  <div class="card">
    <div style="font-size:14px;color:var(--text3);margin-bottom:10px">カテゴリーに合わせてスケジュールに自動反映</div>
    <input class="inp" id="aeName" placeholder="種目名（例：ダンベルフライ）" style="margin-bottom:10px">
    <input class="inp" id="aeDetail" placeholder="セット数・回数（例：3セット×12回）" style="margin-bottom:10px">
    <input class="inp" id="aeCaution" placeholder="注意点（任意）" style="margin-bottom:10px">
    <select class="sel-inp" id="aeCat" style="margin-bottom:10px">
      <option value="upper">上半身</option><option value="lower">下半身</option><option value="core">体幹</option>
      <option value="ball">バランスボール</option><option value="mball">ウエイトボール</option>
      <option value="dips">ディップス</option><option value="roller">腹筋ローラー</option>
      <option value="band">ヒップバンド</option><option value="stretch">ストレッチ</option>
    </select>
    <button class="abtn" onclick="addCustomEx()">追加する</button>
  </div>`;
}

// ===== MYPAGE =====
function renderBodyCheck(){
  const today=new Date().toDateString();
  const saved=JSON.parse(localStorage.getItem('hgBody')||'{}');
  const savedDate=localStorage.getItem('hgBodyDate')||'';
  const data=savedDate===today?saved:{};
  document.getElementById('bodyCheck').innerHTML=bodyParts.map(p=>{
    const cur=data[p.id]??-1;
    return `<div class="body-row">
      <div class="body-icon">${p.icon}</div>
      <div class="body-lbl">${p.label}</div>
      <div class="body-btns">${painLevels.map(l=>`
        <button class="body-btn" onclick="setBody('${p.id}',${l.v})" style="border-color:${cur===l.v?l.color:'var(--border2)'};background:${cur===l.v?l.color+'22':'transparent'};color:${cur===l.v?l.color:'var(--text3)'}">${l.label}</button>
      `).join('')}</div>
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

function renderWMemo(){
  const memos=JSON.parse(localStorage.getItem('hgWMemo')||'[]');
  const el=document.getElementById('wMemoList');
  if(!memos.length){el.innerHTML='<div style="font-size:14px;color:var(--text3);margin-bottom:10px">まだ記録がありません</div>';return;}
  el.innerHTML=memos.map((m,i)=>`
    <div style="display:flex;align-items:center;gap:10px;padding:8px 0;border-top:1px solid var(--border)">
      <div style="flex:1;font-size:16px;font-weight:500">${m.name}</div>
      <div style="font-size:18px;font-weight:700;color:var(--blue-dark)">${m.kg}kg</div>
      <button onclick="removeWMemo(${i})" style="padding:5px 10px;background:var(--coral-light);color:var(--coral-dark);border:none;border-radius:6px;font-size:13px;font-weight:700;cursor:pointer">削除</button>
    </div>`).join('');
}

function addWMemo(){
  const name=document.getElementById('wName').value.trim();
  const kg=document.getElementById('wKg').value.trim();
  if(!name||!kg){alert('種目名と重量を入力してください');return;}
  const memos=JSON.parse(localStorage.getItem('hgWMemo')||'[]');
  const idx=memos.findIndex(m=>m.name===name);
  if(idx>=0)memos[idx].kg=kg;else memos.push({name,kg});
  localStorage.setItem('hgWMemo',JSON.stringify(memos));
  document.getElementById('wName').value='';document.getElementById('wKg').value='';
  renderWMemo();
}

function removeWMemo(i){
  const memos=JSON.parse(localStorage.getItem('hgWMemo')||'[]');
  memos.splice(i,1);localStorage.setItem('hgWMemo',JSON.stringify(memos));renderWMemo();
}

function addNoteManual(){
  const input=document.getElementById('noteInput');
  if(!input||!input.value.trim()){alert('メモを入力してください');return;}
  const now=new Date();
  const ds=now.getFullYear()+'年'+(now.getMonth()+1)+'月'+now.getDate()+'日（'+DJ[now.getDay()]+'）';
  const notes=getNotes();
  notes.unshift({date:ds,text:input.value.trim(),id:Date.now()});
  if(notes.length>50)notes.pop();
  saveNotes(notes);input.value='';
  renderNotes();
}

function deleteNote(id){
  if(!confirm('このメモを削除しますか？'))return;
  saveNotes(getNotes().filter(n=>n.id!==id));renderNotes();
}

function renderNotes(){
  const notes=getNotes();
  const el=document.getElementById('noteList');
  if(!el)return;
  if(!notes.length){el.innerHTML='<div style="font-size:15px;color:var(--text3);text-align:center;padding:20px">まだメモがありません</div>';return;}
  el.innerHTML=notes.map(n=>`
    <div class="note-card">
      <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:6px">
        <div class="note-date">📅 ${n.date}</div>
        <button class="del-btn" onclick="deleteNote(${n.id})">🗑 削除</button>
      </div>
      <div class="note-text">${n.text}</div>
    </div>`).join('');
}

function renderGoals(){
  const goals=JSON.parse(localStorage.getItem('hgGoals')||'{}');
  document.getElementById('goalList').innerHTML=goalItems.map(g=>`
    <div class="goal-row">
      <div class="goal-lbl">${g.label}</div>
      <input type="number" class="goal-inp" placeholder="現在" value="${goals[g.id+'_cur']||''}" onchange="saveGoal('${g.id}_cur',this.value)">
      <span style="color:var(--text3);font-size:14px">→ 目標</span>
      <input type="number" class="goal-inp" placeholder="目標" value="${goals[g.id+'_goal']||''}" onchange="saveGoal('${g.id}_goal',this.value)" style="border-color:var(--green);background:var(--green-light);color:var(--green-dark)">
      <span style="color:var(--text3);font-size:14px">${g.unit}</span>
    </div>`).join('');
}

function saveGoal(key,val){
  const goals=JSON.parse(localStorage.getItem('hgGoals')||'{}');
  goals[key]=val;localStorage.setItem('hgGoals',JSON.stringify(goals));
}

function renderEquip(){
  document.getElementById('equipList').innerHTML=equipData.map(e=>`
    <div class="eq-row" onclick="showEqEx('${e.key}','${e.cat}')">
      <div class="eq-cat">${e.cat}</div>
      <div class="eq-items">${e.items}</div>
      <div class="eq-arr">›</div>
    </div>`).join('');
}

function showEqEx(key,catName){
  const exList=equipEx[key];
  if(!exList){alert('この器具の種目データはありません');return;}
  document.getElementById('eqModalTitle').textContent='📦 '+catName+' の種目';
  document.getElementById('eqExList').innerHTML=exList.map(e=>{
    const added=customEx.some(c=>c.n===e.n);
    return `<div class="eq-ex-row">
      <div class="eq-ex-info">
        <div class="eq-ex-name">${e.n}</div>
        <div class="eq-ex-detail">${e.d}</div>
        <div class="eq-ex-tags">
          <span style="font-size:11px;padding:2px 7px;border-radius:5px;background:${tagCls[e.cat]?'':''};font-weight:600;background:var(--surface2);color:var(--text3)">${catLbl[e.cat]||e.cat}</span>
          <span style="font-size:11px;padding:2px 7px;border-radius:5px;background:var(--surface2);color:var(--text3)">📅 ${e.day}</span>
        </div>
      </div>
      ${added
        ?'<div class="added-lbl">追加済</div>'
        :`<button class="add-ex-btn" onclick="addFromEquip('${e.n.replace(/'/g,"\\'")}','${e.d.replace(/'/g,"\\'")}','${e.cat}','${key}','${catName}')">＋ 追加</button>`
      }
    </div>`;
  }).join('');
  document.getElementById('eqModal').style.display='block';
  document.getElementById('eqModal').scrollIntoView({behavior:'smooth',block:'nearest'});
}

function addFromEquip(name,detail,cat,key,catName){
  if(customEx.some(c=>c.n===name)){alert('すでに追加されています');return;}
  customEx.push({n:name,d:detail,c:null,cat});
  localStorage.setItem('hgCEx',JSON.stringify(customEx));
  renderToday();showEqEx(key,catName);
  alert('✅ '+name+'\nを追加しました！');
}

function closeEqModal(){document.getElementById('eqModal').style.display='none';}

function addCustomEx(){
  const name=document.getElementById('aeName').value.trim();
  const detail=document.getElementById('aeDetail').value.trim();
  const caution=document.getElementById('aeCaution').value.trim();
  const cat=document.getElementById('aeCat').value;
  if(!name){alert('種目名を入力してください');return;}
  if(customEx.some(c=>c.n===name)){alert('同じ名前の種目がすでにあります');return;}
  customEx.push({n:name,d:detail||'記録なし',c:caution||null,cat});
  localStorage.setItem('hgCEx',JSON.stringify(customEx));
  document.getElementById('aeName').value='';document.getElementById('aeDetail').value='';document.getElementById('aeCaution').value='';
  renderToday();alert('✅ 追加しました！');
}

function removeCustomEx(idx){
  if(idx<0)return;
  if(!confirm('この種目を削除しますか？'))return;
  customEx.splice(idx,1);
  localStorage.setItem('hgCEx',JSON.stringify(customEx));
  renderLibrary('all');renderToday();
}

function getMySettings(){
  return {...{goal:'週5回を4週間継続する',weekly:5,priority:'バランス重視',duration:30,font:1},...JSON.parse(localStorage.getItem('hgMySettings')||'{}')};
}
function applyUiScale(scale){
  const value=Number(scale)||1,app=document.querySelector('.app');
  document.documentElement.style.fontSize='16px';
  document.body.style.overflowX='hidden';
  document.body.style.zoom=String(value);
  if(app){
    app.style.zoom='';
    app.style.width='100%';
    app.style.maxWidth='1024px';
  }
}
function saveMySettings(){
  const settings={goal:document.getElementById('mpGoal').value,weekly:Number(document.getElementById('mpWeekly').value)||5,priority:document.getElementById('mpPriority').value,duration:Number(document.getElementById('mpDuration').value),font:Number(document.getElementById('mpFont').value)};
  localStorage.setItem('hgMySettings',JSON.stringify(settings));
  applyUiScale(settings.font);
  dur=settings.duration;setDur(dur);renderMypage();
}
function getCompletionHistory(){return JSON.parse(localStorage.getItem('hgHistory')||'[]');}
function renderCycleStatus(){
  const now=new Date(),idx=cycleWeekFor(now),next=(idx+1)%4;
  document.getElementById('cycleStatus').innerHTML='<div style="font-size:13px;color:var(--text3)">現在のサイクル</div><div style="font-size:21px;font-weight:800;margin:5px 0;color:var(--green)">'+cycleNames[idx]+'</div><div style="font-size:14px;color:var(--text2)">次週：'+cycleNames[next]+'<br>30分は主種目4種目、60分は最大7種目です。</div>';
}
function renderContinuity(){
  const history=getCompletionHistory(),now=new Date(),mon=mondayOf(now);
  const weekCount=history.filter(x=>{const d=new Date(x+'T12:00:00');return d>=mon&&d<new Date(mon.getTime()+604800000)}).length;
  const fourStart=new Date(mon.getTime()-3*604800000);
  const fourCount=history.filter(x=>new Date(x+'T12:00:00')>=fourStart).length;
  const settings=getMySettings(),target=settings.weekly*4,rate=Math.min(100,Math.round(fourCount/target*100));
  const weeks=new Set(history.map(x=>mondayOf(new Date(x+'T12:00:00')).toISOString().slice(0,10)));
  document.getElementById('continuityStats').innerHTML='<div class="dash-stat"><span class="dash-label">今週の実施</span><strong>'+weekCount+' / '+settings.weekly+'</strong></div><div class="dash-stat"><span class="dash-label">4週間達成率</span><strong>'+rate+'%</strong></div><div class="dash-stat"><span class="dash-label">4週間の完了</span><strong>'+fourCount+'回</strong></div><div class="dash-stat"><span class="dash-label">実施した週</span><strong>'+weeks.size+'週</strong></div>';
}
function renderBalance(){
  const now=new Date(),mon=mondayOf(now),counts={chest:0,back:0,shoulder:0,arm:0,core:0,glute:0,quad:0,calf:0};
  for(let i=0;i<5;i++){const d=new Date(mon);d.setDate(mon.getDate()+i);planForDate(d,60).forEach(e=>muscleInfo(e).forEach(m=>{if(m.key in counts)counts[m.key]++;}));}
  const labels={chest:'胸',back:'背中',shoulder:'肩',arm:'腕',core:'体幹',glute:'臀部',quad:'太腿',calf:'脹脛'},max=Math.max(...Object.values(counts),1);
  const low=Object.entries(counts).sort((a,b)=>a[1]-b[1])[0];
  document.getElementById('balanceStats').innerHTML=Object.entries(counts).map(([k,v])=>'<div class="balance-row"><span>'+labels[k]+'</span><div class="balance-track"><div class="balance-fill" style="width:'+Math.round(v/max*100)+'%"></div></div><strong>'+v+'</strong></div>').join('')+'<div class="lib-effect">今週もっとも少ない部位：'+labels[low[0]]+'。4週間全体で均等になるようローテーションします。</div>';
}
function baseEquipment(){
  return equipData.flatMap(e=>e.items.split('/').map(x=>x.trim())).filter(Boolean);
}
function renderMyEquip(){
  const extra=JSON.parse(localStorage.getItem('hgMyEquip')||'[]'),all=[...baseEquipment(),...extra];
  document.getElementById('myEquipList').innerHTML=all.map((x,i)=>'<div class="equip-manage-row"><span>'+x+'</span>'+(i>=baseEquipment().length?'<button class="del-btn" onclick="removeMyEquip('+(i-baseEquipment().length)+')">削除</button>':'<span class="badge bg">登録済</span>')+'</div>').join('');
}
function addMyEquip(){const el=document.getElementById('newEquip'),name=el.value.trim();if(!name)return;const a=JSON.parse(localStorage.getItem('hgMyEquip')||'[]');if(!a.includes(name))a.push(name);localStorage.setItem('hgMyEquip',JSON.stringify(a));el.value='';renderMyEquip();}
function removeMyEquip(i){const a=JSON.parse(localStorage.getItem('hgMyEquip')||'[]');a.splice(i,1);localStorage.setItem('hgMyEquip',JSON.stringify(a));renderMyEquip();}
function exportAppData(){const data={};for(let i=0;i<localStorage.length;i++){const k=localStorage.key(i);if(k&&k.startsWith('hg'))data[k]=localStorage.getItem(k);}const blob=new Blob([JSON.stringify(data,null,2)],{type:'application/json'}),a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download='home-gym-data.json';a.click();URL.revokeObjectURL(a.href);}
function resetAppData(){if(!confirm('トレーニングデータと設定を初期化しますか？'))return;Object.keys(localStorage).filter(k=>k.startsWith('hg')).forEach(k=>localStorage.removeItem(k));location.reload();}
function renderMypage(){
  const s=getMySettings();document.getElementById('mpGoal').value=s.goal;document.getElementById('mpWeekly').value=s.weekly;document.getElementById('mpPriority').value=s.priority;document.getElementById('mpDuration').value=String(s.duration);document.getElementById('mpFont').value=String(s.font);
  renderCycleStatus();renderContinuity();renderBalance();renderMyEquip();
}

// ===== TAB SWITCH =====
function sw(name,tabId){
  window.scrollTo(0,0);
  document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  document.getElementById('panel-'+name).classList.add('active');
  document.getElementById(tabId).classList.add('active');
  if(name==='schedule')renderSchedule();
  if(name==='library')renderLibrary('all');
  if(name==='mypage')renderMypage();
}

// ===== INIT =====
function init(){
  const now=new Date();
  document.getElementById('dateDisp').innerHTML=
    now.getFullYear()+'年'+(now.getMonth()+1)+'月'+now.getDate()+'日（'+DJ[now.getDay()]+'）';
  const todayIcon=document.getElementById('todayTabDate');
  if(todayIcon)todayIcon.textContent=(now.getMonth()+1)+'/'+now.getDate();
  const settings=getMySettings();
  dur=settings.duration;
  applyUiScale(settings.font);
  document.getElementById('d60').classList.toggle('sel',dur===60);
  document.getElementById('d30').classList.toggle('sel',dur===30);
  renderToday();
}
init();
</script>
</body>
</html>
