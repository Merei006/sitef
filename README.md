<!DOCTYPE html>
<html lang="kk">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Материалдар базасы</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<style>
:root{
  --bg:#eef2f6; --surface:#ffffff; --ink:#14213d; --muted:#5b6679; --line:#d5dce6;
  --brand:#14213d; --brand-ink:#f4f7fb; --accent:#e8a33d; --accent-ink:#14213d; --link:#2563b0;
  --ok:#2f8f5b; --warn:#b4531a; --qr-bg:#ffffff; --qr-fg:#14213d;
  box-sizing:border-box;
  padding-top:env(safe-area-inset-top,0px); padding-bottom:env(safe-area-inset-bottom,0px);
}
@media (prefers-color-scheme: dark){
  :root:not([data-theme="light"]){
    --bg:#0e1626; --surface:#17223a; --ink:#e8edf6; --muted:#9aa7bd; --line:#2a3858;
    --brand:#0a1120; --brand-ink:#e8edf6; --link:#7db4f0; --ok:#5ec48b; --warn:#f0a070;
  }
}
:root[data-theme="dark"]{
  --bg:#0e1626; --surface:#17223a; --ink:#e8edf6; --muted:#9aa7bd; --line:#2a3858;
  --brand:#0a1120; --brand-ink:#e8edf6; --link:#7db4f0; --ok:#5ec48b; --warn:#f0a070;
}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font-family:"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;line-height:1.5;-webkit-text-size-adjust:100%}
button,input,select{font:inherit;color:inherit}
:focus-visible{outline:3px solid var(--accent);outline-offset:2px}
header{background:var(--brand);color:var(--brand-ink)}
.bar{max-width:1080px;margin:0 auto;padding:14px 20px;display:flex;align-items:center;gap:20px;flex-wrap:wrap}
.logo{font-weight:700;font-size:1.15rem;margin-right:auto}
nav{display:flex;gap:4px;flex-wrap:wrap}
nav button{background:none;border:0;color:inherit;opacity:.8;padding:8px 14px;border-radius:8px;cursor:pointer}
nav button:hover{opacity:1;background:rgba(255,255,255,.08)}
nav button[aria-current="page"]{opacity:1;background:rgba(255,255,255,.14);font-weight:600}
main{max-width:1080px;margin:0 auto;padding:36px 20px 64px}
h1{font-size:clamp(2rem,5vw,3.2rem);line-height:1.12;margin:0 0 14px;letter-spacing:-.01em}
h2{font-size:1.5rem;margin:0 0 14px}
p{margin:0 0 14px}
.muted{color:var(--muted)}
.hero{display:grid;grid-template-columns:1.1fr .9fr;gap:40px;align-items:start}
.steps{list-style:none;padding:0;margin:26px 0;display:grid;gap:16px}
.steps li{display:flex;gap:14px;align-items:flex-start}
.steps b{flex:none;width:34px;height:34px;border-radius:50%;background:var(--accent);color:var(--accent-ink);display:grid;place-items:center}
.card{background:var(--surface);border:1px solid var(--line);border-radius:18px;padding:26px}
.qrcard{text-align:center}
.qrwrap{position:relative;width:236px;height:236px;margin:14px auto;display:grid;place-items:center}
.qrbox{background:var(--qr-bg);padding:10px;border-radius:12px;width:236px;height:236px;display:grid;place-items:center}
.qrbox img,.qrbox canvas{max-width:100%;height:auto;display:block}
.ring{position:absolute;inset:-8px;width:calc(100% + 16px);height:calc(100% + 16px);transform:rotate(-90deg);pointer-events:none}
.ring circle{fill:none;stroke-width:4}
.ring .track{stroke:var(--line)}
.ring .prog{stroke:var(--accent);stroke-linecap:round;transition:stroke-dashoffset 1s linear}
.expired{position:absolute;inset:0;background:color-mix(in srgb,var(--surface) 92%,transparent);display:none;flex-direction:column;align-items:center;justify-content:center;gap:10px;border-radius:12px;padding:12px}
.qrwrap.old .expired{display:flex}
.btn{border:0;border-radius:10px;padding:11px 18px;cursor:pointer;font-weight:600}
.btn.primary{background:var(--brand);color:var(--brand-ink)}
.btn.ghost{background:transparent;border:1.5px solid var(--line)}
.btn:hover{filter:brightness(1.1)}
.sec{font-size:.9rem;color:var(--muted)}
.row{display:flex;gap:10px;flex-wrap:wrap;justify-content:center;margin-top:10px}
.note{font-size:.85rem;color:var(--muted);border-top:1px solid var(--line);margin-top:18px;padding-top:12px;text-align:left}
.toolbar{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:20px}
.toolbar input,.toolbar select{background:var(--surface);border:1px solid var(--line);border-radius:10px;padding:10px 12px;min-width:0}
.toolbar input{flex:1 1 220px}
.list{display:grid;grid-template-columns:repeat(auto-fill,minmax(250px,1fr));gap:14px}
.item{background:var(--surface);border:1px solid var(--line);border-radius:14px;padding:18px;display:flex;flex-direction:column;gap:8px}
.item h3{margin:0;font-size:1.05rem}
.tag{display:inline-block;font-size:.8rem;padding:2px 10px;border-radius:99px;border:1px solid var(--line);color:var(--muted)}
.tag.t-жоспар{border-color:var(--link);color:var(--link)}
.tag.t-презентация{border-color:var(--accent);color:var(--warn)}
.tag.t-тапсырма{border-color:var(--ok);color:var(--ok)}
.profile{display:grid;grid-template-columns:280px 1fr;gap:24px}
.avatar{width:84px;height:84px;border-radius:50%;background:var(--accent);color:var(--accent-ink);display:grid;place-items:center;font-size:2rem;font-weight:700;margin-bottom:12px}
.bar-out{height:12px;border-radius:99px;background:var(--line);overflow:hidden;margin:8px 0}
.bar-in{height:100%;background:var(--ok);width:0;transition:width .4s}
.badges{display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:12px;margin-top:10px}
.badge{border:1px dashed var(--line);border-radius:12px;padding:14px;text-align:center;color:var(--muted)}
.badge.on{border:1.5px solid var(--accent);color:var(--ink);background:color-mix(in srgb,var(--accent) 14%,transparent)}
.badge .ic{font-size:1.8rem;display:block}
.task{display:flex;justify-content:space-between;align-items:center;gap:12px;padding:12px 0;border-bottom:1px solid var(--line)}
.task:last-child{border-bottom:0}
.hidden{display:none!important}
.empty{padding:40px 20px;text-align:center}
.toast{position:fixed;left:50%;bottom:calc(24px + env(safe-area-inset-bottom,0px));transform:translateX(-50%);background:var(--brand);color:var(--brand-ink);padding:12px 20px;border-radius:12px;opacity:0;pointer-events:none;transition:opacity .25s;max-width:90vw}
.toast.show{opacity:1}
footer{max-width:1080px;margin:0 auto;padding:0 20px 40px;color:var(--muted);font-size:.85rem}
@media (max-width:820px){
  .hero,.profile{grid-template-columns:1fr}
  main{padding-top:24px}
}
@media (prefers-reduced-motion:reduce){*{transition:none!important}}
</style>
</head>
<body>
<header>
  <div class="bar">
    <div class="logo">Материалдар базасы</div>
    <nav aria-label="Негізгі мәзір">
      <button data-go="home">Басты бет</button>
      <button data-go="catalog">Материалдар</button>
      <button data-go="profile">Профиль</button>
    </nav>
  </div>
</header>

<main>
  <!-- Басты бет -->
  <section id="view-home" class="hero">
    <div>
      <h1>Қош келдіңіз!</h1>
      <p class="muted" style="font-size:1.15rem">Мұғалімнің жоспарлары, презентациялары мен тапсырмалары бір жерде. Барлық пән үшін.</p>
      <ol class="steps">
        <li><b>1</b><span>QR кодты телефонмен сканерлеңіз</span></li>
        <li><b>2</b><span>Аккаунтыңызға автоматты түрде кіресіз</span></li>
        <li><b>3</b><span>Профильде ұпайларыңыз бен белгілеріңізді көресіз</span></li>
      </ol>
      <button class="btn ghost" id="pwBtn">Логин арқылы кіру</button>
    </div>

    <div class="card qrcard" aria-live="polite">
      <h2 style="margin-bottom:4px">QR код арқылы кіру</h2>
      <p class="muted" style="margin:0">Камераны кодқа бағыттаңыз</p>
      <div class="qrwrap" id="qrwrap">
        <svg class="ring" viewBox="0 0 100 100" aria-hidden="true"><circle class="track" cx="50" cy="50" r="48"/><circle class="prog" id="prog" cx="50" cy="50" r="48" stroke-dasharray="301.6" stroke-dashoffset="0"/></svg>
        <div class="qrbox" id="qr" role="img" aria-label="Кіру үшін QR код"></div>
        <div class="expired"><b>Код ескірді</b><button class="btn primary" id="renew">Жаңа код алу</button></div>
      </div>
      <p class="sec" id="timer">Код 60 секунд жарамды</p>
      <div class="row">
        <button class="btn primary" id="scanDemo">Сканерледім (демо)</button>
        <button class="btn ghost" id="renew2">Жаңа код алу</button>
      </div>
      <p class="note">Бұл сайт үлгісі: кіру логикасы осы браузердің ішінде жұмыс істейді. Нақты телефоннан кіру үшін токенді тексеретін сервер (мысалы, Flask) керек.</p>
    </div>
  </section>

  <!-- Материалдар -->
  <section id="view-catalog" class="hidden">
    <h2>Материалдар</h2>
    <p class="muted">Әртүрлі пәндің үлгі деректері көрсетілген. Нақты бағдарламада бұл тізім деректер базасынан келеді.</p>
    <div class="toolbar">
      <input id="q" type="search" placeholder="Атауы бойынша іздеу" aria-label="Іздеу">
      <select id="fSubj" aria-label="Пән"><option value="">Барлық пән</option><option>Информатика</option><option>Математика</option><option>Қазақ тілі</option><option>Жаратылыстану</option><option>Дүниетану</option></select>
      <select id="fGrade" aria-label="Сынып"><option value="">Барлық сынып</option><option>1</option><option>2</option><option>3</option><option>4</option><option>5</option><option>6</option><option>7</option><option>8</option><option>9</option><option>10</option><option>11</option></select>
      <select id="fType" aria-label="Түрі"><option value="">Барлық түрі</option><option>жоспар</option><option>презентация</option><option>тапсырма</option></select>
    </div>
    <div class="list" id="list"></div>
    <div class="empty muted hidden" id="none">Ештеңе табылмады. Іздеу сөзін өзгертіп көріңіз.</div>
  </section>

  <!-- Профиль -->
  <section id="view-profile" class="hidden">
    <div class="card empty" id="noauth">
      <h2>Профильді көру үшін кіріңіз</h2>
      <p class="muted">Басты беттегі QR кодты сканерлеңіз.</p>
      <button class="btn primary" data-go="home">Басты бетке өту</button>
    </div>
    <div class="profile hidden" id="auth">
      <div class="card">
        <div class="avatar" id="av">?</div>
        <h2 id="nick" style="margin-bottom:2px"></h2>
        <p class="sec" id="sid"></p>
        <button class="btn ghost" id="logout">Шығу</button>
        <p class="note">Жүйе оқушының аты-жөнін сақтамайды: тек лақап ат пен анонимді нөмір.</p>
      </div>
      <div class="card">
        <h2>Прогресс</h2>
        <p><b id="pts">0</b> ұпай · келесі белгіге дейін: <span id="next"></span></p>
        <div class="bar-out" role="progressbar" aria-valuemin="0" aria-valuemax="100" id="pb"><div class="bar-in" id="pbi"></div></div>
        <h2 style="margin-top:22px">Белгілер</h2>
        <div class="badges" id="badges"></div>
        <h2 style="margin-top:22px">Тапсырмалар</h2>
        <div id="tasks"></div>
        <p class="note">Ұпай нәтиже үшін ғана емес, әрекет үшін де беріледі. Басқа оқушылармен рейтинг жасалмайды.</p>
      </div>
    </div>
  </section>
</main>
<footer>Материалдар базасы · барлық пән мұғалімдеріне арналған үлгі бет</footer>
<div class="toast" id="toast" role="status"></div>

<script>
(function(){
  var TTL=60, tokens={}, timerId=null, left=TTL;
  var NAMES1=["Көк","Алтын","Күміс","Жас","Батыл","Шапшаң","Ақылды","Жарқын"];
  var NAMES2=["Тұлпар","Бүркіт","Арыстан","Сұңқар","Жолбарыс","Қыран","Барыс","Құлан"];
  var TASKS=[{id:"t1",t:"Математика: қосу жаттығуы",p:10},{id:"t2",t:"Қазақ тілі: сөздік диктант",p:10},{id:"t3",t:"Информатика: алгоритм ойыны",p:15},{id:"t4",t:"Жаратылыстану: өсімдік бөліктері",p:10}];
  var BADGES=[{n:"Бастаушы",at:10,ic:"🌱"},{n:"Белсенді",at:30,ic:"⚡"},{n:"Шебер",at:60,ic:"🛠️"},{n:"Жұлдыз",at:100,ic:"⭐"}];
  var MATS=[
    {t:"Файлдар және қапшықтар",s:"Информатика",g:2,ty:"жоспар"},{t:"Файлдар және қапшықтар",s:"Информатика",g:2,ty:"тапсырма"},
    {t:"Ақпарат өлшем бірлігі",s:"Информатика",g:7,ty:"презентация"},
    {t:"Қосу және алу",s:"Математика",g:2,ty:"жоспар"},{t:"Бөлшектер",s:"Математика",g:5,ty:"тапсырма"},{t:"Теңдеулер",s:"Математика",g:7,ty:"презентация"},
    {t:"Сөз таптары",s:"Қазақ тілі",g:4,ty:"жоспар"},{t:"Сөздік диктант",s:"Қазақ тілі",g:3,ty:"тапсырма"},
    {t:"Өсімдік бөліктері",s:"Жаратылыстану",g:3,ty:"презентация"},{t:"Жыл мезгілдері",s:"Дүниетану",g:2,ty:"тапсырма"}
  ];
  var $=function(id){return document.getElementById(id)};
  var mem={}; // қор: localStorage жұмыс істемесе де сайт жұмыс істейді
  function load(){try{var v=localStorage.getItem("mb_user");return v?JSON.parse(v):null}catch(e){return mem.user||null}}
  function save(u){try{if(u)localStorage.setItem("mb_user",JSON.stringify(u));else localStorage.removeItem("mb_user")}catch(e){mem.user=u}}
  function toast(m){var t=$("toast");t.textContent=m;t.classList.add("show");clearTimeout(toast.i);toast.i=setTimeout(function(){t.classList.remove("show")},2400)}

  // ---- токен
  function newToken(){var a=new Uint8Array(16);(window.crypto||window.msCrypto).getRandomValues(a);var s="";for(var i=0;i<a.length;i++)s+=String.fromCharCode(a[i]);return btoa(s).replace(/\+/g,"-").replace(/\//g,"_").replace(/=+$/,"")}
  function checkToken(t){var it=tokens[t];if(!it||it.used||Date.now()-it.t>TTL*1000)return false;it.used=true;return true}
  var current=null;
  function renderQR(){
    current=newToken();tokens[current]={t:Date.now(),used:false};
    var url=location.href.split("#")[0]+"#scan="+current;
    var box=$("qr");box.innerHTML="";
    try{new QRCode(box,{text:url,width:210,height:210,colorDark:"#14213d",colorLight:"#ffffff",correctLevel:QRCode.CorrectLevel.M})}
    catch(e){box.textContent="QR кітапханасы жүктелмеді. Интернет байланысын тексеріңіз."}
    $("qrwrap").classList.remove("old");left=TTL;tick(true);
    clearInterval(timerId);timerId=setInterval(tick,1000);
  }
  function tick(first){
    if(first!==true)left--;
    var prog=$("prog");prog.style.strokeDashoffset=String(301.6*(1-left/TTL));
    if(left<=0){clearInterval(timerId);$("qrwrap").classList.add("old");$("timer").textContent="Код ескірді. Жаңа код алыңыз";return}
    $("timer").textContent="Код "+left+" секунд жарамды";
  }
  function login(){
    var u=load();
    if(!u){u={id:"S-"+newToken().slice(0,6).toUpperCase(),nick:NAMES1[Math.floor(Math.random()*8)]+" "+NAMES2[Math.floor(Math.random()*8)],pts:0,done:[]};save(u)}
    go("profile");toast("Сәтті кірдіңіз");
  }
  function scan(){
    if(!current||$("qrwrap").classList.contains("old")){toast("Код ескірген. Жаңа код алыңыз");return}
    if(checkToken(current)){login()}else{toast("Токен жарамсыз немесе қолданылған");}
  }
  // сілтеме арқылы келгенде (#scan=...)
  function fromHash(){var m=location.hash.match(/scan=([\w-]+)/);if(!m)return;
    if(checkToken(m[1])){history.replaceState(null,"",location.pathname+location.search);login()}else{toast("Токен жарамсыз, ескірген немесе басқа құрылғыда жасалған")}}

  // ---- көріністер
  function go(v){
    ["home","catalog","profile"].forEach(function(x){$("view-"+x).classList.toggle("hidden",x!==v)});
    document.querySelectorAll("nav button").forEach(function(b){if(b.dataset.go===v)b.setAttribute("aria-current","page");else b.removeAttribute("aria-current")});
    if(v==="profile")renderProfile();
    if(v==="catalog")renderList();
    window.scrollTo(0,0);
  }
  function renderList(){
    var q=$("q").value.trim().toLowerCase(),g=$("fGrade").value,sj=$("fSubj").value,ty=$("fType").value,box=$("list");box.innerHTML="";var n=0;
    MATS.forEach(function(m){
      if(q&&m.t.toLowerCase().indexOf(q)<0)return;if(sj&&m.s!==sj)return;if(g&&String(m.g)!==g)return;if(ty&&m.ty!==ty)return;n++;
      var d=document.createElement("div");d.className="item";
      var h=document.createElement("h3");h.textContent=m.t;
      var s=document.createElement("span");s.className="tag t-"+m.ty;s.textContent=m.ty;
      var p=document.createElement("p");p.className="muted";p.style.margin="0";p.textContent=m.s+" · "+m.g+"-сынып";
      var b=document.createElement("button");b.className="btn ghost";b.textContent="Ашу";b.onclick=function(){toast("Үлгі: нақты жүйеде файл немесе сілтеме ашылады")};
      d.appendChild(h);d.appendChild(s);d.appendChild(p);d.appendChild(b);box.appendChild(d);
    });
    $("none").classList.toggle("hidden",n>0);
  }
  function renderProfile(){
    var u=load();$("noauth").classList.toggle("hidden",!!u);$("auth").classList.toggle("hidden",!u);if(!u)return;
    $("av").textContent=u.nick.charAt(0);$("nick").textContent=u.nick;$("sid").textContent="Анонимді нөмір: "+u.id;$("pts").textContent=u.pts;
    var nxt=BADGES.filter(function(b){return b.at>u.pts})[0];
    $("next").textContent=nxt?(nxt.at-u.pts)+" ұпай ("+nxt.n+")":"барлық белгі алынды";
    var pct=nxt?Math.round(u.pts/nxt.at*100):100;$("pbi").style.width=pct+"%";$("pb").setAttribute("aria-valuenow",pct);
    var bd=$("badges");bd.innerHTML="";
    BADGES.forEach(function(b){var on=u.pts>=b.at;var d=document.createElement("div");d.className="badge"+(on?" on":"");d.innerHTML='<span class="ic"></span><b></b><div class="sec"></div>';d.children[0].textContent=on?b.ic:"🔒";d.children[1].textContent=b.n;d.children[2].textContent=b.at+" ұпай";bd.appendChild(d)});
    var tk=$("tasks");tk.innerHTML="";
    TASKS.forEach(function(t){var done=u.done.indexOf(t.id)>=0;var r=document.createElement("div");r.className="task";var s=document.createElement("span");s.textContent=t.t+" (+"+t.p+" ұпай)";var b=document.createElement("button");b.className="btn "+(done?"ghost":"primary");b.disabled=done;b.textContent=done?"Орындалды":"Орындадым";
      b.onclick=function(){var x=load();if(x.done.indexOf(t.id)>=0)return;x.done.push(t.id);x.pts+=t.p;save(x);renderProfile();toast("+"+t.p+" ұпай");};
      r.appendChild(s);r.appendChild(b);tk.appendChild(r)});
  }

  // ---- оқиғалар
  document.querySelectorAll("[data-go]").forEach(function(b){b.addEventListener("click",function(){go(b.dataset.go)})});
  $("renew").onclick=renderQR;$("renew2").onclick=renderQR;$("scanDemo").onclick=scan;
  $("pwBtn").onclick=function(){toast("Мұғалім парольмен кіреді. Бұл бөлім серверді қажет етеді")};
  $("logout").onclick=function(){save(null);go("home");toast("Шықтыңыз")};
  ["q","fSubj","fGrade","fType"].forEach(function(id){$(id).addEventListener("input",renderList)});
  renderQR();fromHash();if(!location.hash)go("home");
})();
</script>
</body>
</html>
