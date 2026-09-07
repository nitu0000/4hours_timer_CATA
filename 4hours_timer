<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>4時間後の時刻計算</title>
<style>
*{box-sizing:border-box}
body{margin:0;min-height:100vh;
  display:flex;
  justify-content:center;
  align-items:center;
  background:#f4f1ec;
  width: 1420px;
  font-family:Arial,"Noto Sans JP",sans-serif}

.container{width:min(95%,760px);
    padding:28px;background:#fff;
   border-radius:20px;
    box-shadow:0 10px 30px rgba(0,0,0,.1)}
h1{text-align:center;
  margin:0 0 22px;
  font-size:25px}
.tabs{display:flex;
  flex-wrap:wrap;
  gap:8px;justify-content:center;
  margin-bottom:24px}
.tab{padding:10px 15px;border:0;
  border-radius:10px;
  background:#e8e8e8;
  color:#444;
  font-size:14px;
  cursor:pointer}
.tab.active{background:#333;color:#fff}

.input-area{max-width:420px;margin:0 auto 28px;text-align:center}

label{display:block;margin-bottom:9px;font-weight:bold}
input[type=time]{width:100%;padding:14px;font-size:24px;text-align:center;border:2px solid #ddd;border-radius:12px}
.arrow{margin:15px 0;font-size:26px}
.result{padding:18px;background:#f7f7f7;border-radius:15px}
.result-label{font-size:13px;color:#777}
#result{font-size:40px;font-weight:bold;margin-top:5px}
.countdown{margin-top:8px;font-size:15px;color:#666}
h2{font-size:18px;margin:0 0 12px}
.list{display:grid;gap:8px}
.row{display:grid;grid-template-columns:1.2fr .9fr .9fr 1fr;gap:8px;align-items:center;padding:11px 12px;border-radius:10px;background:#f7f7f7}
.row.header{background:transparent;font-size:12px;color:#888;padding-bottom:3px}
.row .name{font-weight:bold}
.row .time,.row .after{text-align:center;font-variant-numeric:tabular-nums}
.row .remaining{text-align:right;font-variant-numeric:tabular-nums}
.empty{color:#aaa}
@media(max-width:600px){
 .container{padding:20px 14px}
 .row{grid-template-columns:1fr 1fr;gap:5px}
 .row.header{display:none}
 .row .remaining{text-align:center}
}
</style>
</head>
<body>
<div class="container">
<h1>4時間後の時刻計算</h1>

<div class="tabs" id="tabs"></div>

<div class="input-area">
<label for="time">開始時刻</label>
<input type="time" id="time">
<div class="arrow">↓</div>
<div class="result">
<div class="result-label">4時間後</div>
<div id="result">--:--</div>
<div class="countdown" id="countdown">残り時間：--:--:--</div>
</div>
</div>

<h2>カテゴリー一覧</h2>
<div class="list">
<div class="row header"><div>カテゴリー</div><div>開始</div><div>4時間後</div><div>残り時間</div></div>
<div id="rows"></div>
</div>
</div>

<script>
const categories=["飛行場","オイルリグ","客船","ヒューメイン","アーティファクト","パシフィック","ユニオン"];
const times={};
let current="飛行場";
const tabs=document.getElementById("tabs");
const input=document.getElementById("time");
const result=document.getElementById("result");
const countdown=document.getElementById("countdown");
const rows=document.getElementById("rows");

categories.forEach((name,i)=>{
 const b=document.createElement("button");
 b.className="tab"+(i===0?" active":"");
 b.textContent=name;
 b.onclick=()=>{
   if(input.value) times[current]=input.value;
   current=name;
   document.querySelectorAll(".tab").forEach(x=>x.classList.remove("active"));
   b.classList.add("active");
   input.value=times[current]||"";
   calculate();
   render();
 };
 tabs.appendChild(b);
});

function add4h(t){
 if(!t) return "";
 const [h,m]=t.split(":").map(Number);
 const total=(h*60+m+240)%(24*60);
 return String(Math.floor(total/60)).padStart(2,"0")+":"+String(total%60).padStart(2,"0");
}

function nextTarget(t){
 const [h,m]=t.split(":").map(Number);
 const now=new Date();
 let target=new Date(now);
 target.setHours(h,m,0,0);
 if(target<=now) target.setDate(target.getDate()+1);
 return target;
}

function remaining(t){
 if(!t) return "--:--:--";
 let ms=nextTarget(add4h(t))-new Date();
 if(ms<0) ms=0;
 const s=Math.floor(ms/1000);
 return String(Math.floor(s/3600)).padStart(2,"0")+":"+String(Math.floor(s%3600/60)).padStart(2,"0")+":"+String(s%60).padStart(2,"0");
}

function calculate(){
 result.textContent=add4h(input.value)||"--:--";
 countdown.textContent=input.value ? "残り時間："+remaining(input.value) : "残り時間：--:--:--";
}

function render(){
 rows.innerHTML="";
 categories.forEach(name=>{
   const t=times[name];
   const row=document.createElement("div");
   row.className="row";
   row.innerHTML=`<div class="name">${name}</div>
   <div class="time">${t||'<span class="empty">未設定</span>'}</div>
   <div class="after">${t?add4h(t):'<span class="empty">--:--</span>'}</div>
   <div class="remaining">${t?remaining(t):'<span class="empty">--:--:--</span>'}</div>`;
   rows.appendChild(row);
 });
}

input.addEventListener("input",()=>{
 times[current]=input.value;
 calculate();
 render();
});

setInterval(()=>{
 calculate();
 render();
},1000);

render();
</script>
</body>
</html>
