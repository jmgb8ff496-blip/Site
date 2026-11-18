<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="theme-color" content="#0a0a12">
<title>SONIQ</title>
<style>
:root{--bg:#0a0a12;--card:rgba(255,255,255,.06);--line:rgba(255,255,255,.1);--tx:#fff;--mut:rgba(255,255,255,.55);--g:#39ff88;--p:#8b5cf6;--y:#ffd23f;color-scheme:dark;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root{--bg:#0a0a12}}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
body{margin:0;background:var(--bg);color:var(--tx);font-family:-apple-system,"SF Pro Display",system-ui,"Helvetica Neue",Arial,sans-serif;min-height:100vh;overflow-x:hidden}
.bg{position:fixed;inset:0;z-index:0;overflow:hidden;pointer-events:none}
.blob{position:absolute;border-radius:50%;filter:blur(70px);opacity:.45;animation:float 14s ease-in-out infinite alternate}
.b1{width:60vmax;height:60vmax;background:var(--ac,var(--p));transition:background 1.4s;top:-20vmax;left:-20vmax}
.b2{width:50vmax;height:50vmax;background:var(--g);bottom:-18vmax;right:-15vmax;animation-delay:-5s;opacity:.3}
.b3{width:35vmax;height:35vmax;background:var(--y);top:40%;left:55%;animation-delay:-9s;opacity:.18}
@keyframes float{to{transform:translate(8vmax,6vmax) scale(1.2) rotate(40deg)}}
.app{position:relative;z-index:1;max-width:480px;margin:0 auto;padding:16px 20px 40px}
header{display:flex;justify-content:space-between;align-items:center;animation:in .8s both}
.logo{font-weight:800;font-size:24px;letter-spacing:4px;background:linear-gradient(90deg,var(--g),var(--y),var(--p));-webkit-background-clip:text;background-clip:text;color:transparent;background-size:200%;animation:shine 6s linear infinite}
@keyframes shine{to{background-position:200% 0}}
.add{border:1px solid var(--line);background:var(--card);color:var(--tx);padding:10px 16px;border-radius:99px;font-size:14px;font-weight:600;backdrop-filter:blur(12px);-webkit-backdrop-filter:blur(12px);transition:transform .2s}
.add:active{transform:scale(.94)}
.stage{position:relative;margin:26px auto 8px;width:min(78vw,340px);aspect-ratio:1;animation:in .9s .1s both}
.ring{position:absolute;inset:-14px;border-radius:50%;background:conic-gradient(var(--g),var(--y),var(--p),var(--g));filter:blur(22px);opacity:.35;animation:spin 8s linear infinite;transition:opacity .6s}
.playing .ring{opacity:.8}
.disc{position:absolute;inset:0;border-radius:50%;overflow:hidden;box-shadow:0 20px 60px rgba(0,0,0,.6),0 0 0 6px rgba(255,255,255,.06);animation:spin 18s linear infinite;animation-play-state:paused;background:#111;transition:transform .5s cubic-bezier(.2,.8,.2,1)}
.playing .disc{animation-play-state:running;transform:scale(1.03)}
.disc img{width:100%;height:100%;object-fit:cover;display:block}
.disc::after{content:"";position:absolute;left:50%;top:50%;width:17%;height:17%;transform:translate(-50%,-50%);border-radius:50%;background:var(--bg);box-shadow:0 0 0 5px rgba(255,255,255,.15)}
@keyframes spin{to{transform:rotate(360deg)}}
.hint{text-align:center;color:var(--mut);font-size:12px;margin-top:4px}
canvas{display:block;width:100%;height:70px;margin-top:14px}
.info{text-align:center;margin-top:6px;min-height:62px}
.title{font-size:24px;font-weight:800;letter-spacing:-.4px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.artist{color:var(--mut);margin-top:4px;font-size:15px}
.fade{animation:pop .5s both}
@keyframes pop{from{opacity:0;transform:translateY(8px)}}
.bar{margin-top:18px}
.track{position:relative;height:6px;background:rgba(255,255,255,.12);border-radius:9px;touch-action:none}
.fill{position:absolute;left:0;top:0;bottom:0;width:0;border-radius:9px;background:linear-gradient(90deg,var(--g),var(--y),var(--p))}
.knob{position:absolute;top:50%;width:16px;height:16px;border-radius:50%;background:#fff;transform:translate(-50%,-50%);box-shadow:0 0 14px var(--g);left:0}
.times{display:flex;justify-content:space-between;color:var(--mut);font-size:12px;margin-top:10px;font-variant-numeric:tabular-nums}
.ctrl{display:flex;justify-content:center;align-items:center;gap:26px;margin-top:14px}
.ctrl button{border:0;background:none;color:var(--tx);width:54px;height:54px;border-radius:50%;display:grid;place-items:center;transition:transform .2s}
.ctrl button:active{transform:scale(.88)}
.ctrl svg{width:30px;height:30px;fill:currentColor}
.ctrl .play{width:76px;height:76px;background:linear-gradient(135deg,var(--g),var(--y));color:#0a0a12;box-shadow:0 10px 36px rgba(57,255,136,.4)}
.playing .play{animation:pulse 2s ease-in-out infinite}
@keyframes pulse{50%{box-shadow:0 10px 50px rgba(139,92,246,.7)}}
.play svg{width:34px;height:34px}
h3{margin:32px 0 10px;font-size:13px;letter-spacing:1.5px;text-transform:uppercase;color:var(--mut)}
.row{display:flex;align-items:center;gap:12px;padding:10px;border-radius:16px;background:var(--card);border:1px solid var(--line);margin-bottom:8px;backdrop-filter:blur(12px);-webkit-backdrop-filter:blur(12px);animation:in .6s both;transition:transform .2s,border-color .3s}
.row:active{transform:scale(.98)}
.row.on{border-color:var(--g);box-shadow:0 0 24px rgba(57,255,136,.18)}
.row img{width:48px;height:48px;border-radius:12px;object-fit:cover}
.row .t{flex:1;min-width:0}.row b{display:block;font-size:15px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}.row small{color:var(--mut)}
.eq{display:none;gap:3px;align-items:flex-end;height:18px}
.on.live .eq{display:flex}
.eq i{width:3px;background:var(--y);border-radius:2px;animation:eq .8s ease-in-out infinite alternate}
.eq i:nth-child(2){animation-delay:-.3s;background:var(--g)}.eq i:nth-child(3){animation-delay:-.6s;background:var(--p)}
@keyframes eq{from{height:4px}to{height:18px}}
@keyframes in{from{opacity:0;transform:translateY(18px)}}
.app{padding-bottom:150px}
.view{display:none}.view.show{display:block;animation:in .5s both}
.hi{font-size:30px;font-weight:800;letter-spacing:-.8px;margin:22px 0 4px}.sub{color:var(--mut);margin:0 0 18px}
.tiles{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.tile{padding:16px;border-radius:20px;border:1px solid var(--line);transition:transform .2s;min-height:84px}.tile:active{transform:scale(.96)}
.tile b{display:block;font-size:16px}.tile small{color:rgba(255,255,255,.7);font-size:12px}
.t1{background:linear-gradient(135deg,rgba(139,92,246,.7),rgba(139,92,246,.15))}.t2{background:linear-gradient(135deg,rgba(57,255,136,.55),rgba(57,255,136,.1))}
.t3{background:linear-gradient(135deg,rgba(255,210,63,.6),rgba(255,210,63,.1))}.t4{background:var(--card)}
.cards{display:flex;gap:12px;overflow-x:auto;margin:0 -20px;padding:0 20px 6px;scrollbar-width:none}.cards::-webkit-scrollbar{display:none}
.card{flex:0 0 140px;animation:in .6s both;transition:transform .2s}.card:active{transform:scale(.95)}
.card img{width:140px;height:140px;border-radius:20px;object-fit:cover;display:block;box-shadow:0 10px 30px rgba(0,0,0,.5)}
.card b{display:block;margin-top:8px;font-size:14px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}.card small{color:var(--mut);font-size:12px}
.sbox{display:flex;align-items:center;gap:10px;background:var(--card);border:1px solid var(--line);border-radius:16px;padding:0 14px;margin-top:12px;transition:border-color .3s,box-shadow .3s}
.sbox:focus-within{border-color:var(--p);box-shadow:0 0 24px rgba(139,92,246,.35)}
.sbox input{flex:1;background:none;border:0;outline:0;color:var(--tx);font-size:16px;padding:14px 0;font-family:inherit}
.chips,.seg{display:flex;gap:8px;margin:14px 0}
.chips button,.seg button{border:1px solid var(--line);background:var(--card);color:var(--mut);padding:8px 14px;border-radius:99px;font-size:13px;font-weight:600;transition:all .25s}
.chips button.on,.seg button.on{background:linear-gradient(135deg,var(--g),var(--y));color:#0a0a12;border-color:transparent}
.empty{text-align:center;color:var(--mut);padding:30px 10px;font-size:14px}
.hb{border:0;background:none;color:var(--mut);font-size:22px;padding:6px;transition:transform .2s}.hb.f{color:var(--g);text-shadow:0 0 12px var(--g)}.hb:active{transform:scale(1.4)}
.heart{position:absolute;right:0;top:0;border:0;background:none;color:var(--mut);font-size:28px;transition:transform .2s}.heart.f{color:var(--g);text-shadow:0 0 14px var(--g)}.heart:active{transform:scale(1.4)}
.info{position:relative}.title{padding:0 36px}
.tabs{position:fixed;left:50%;transform:translateX(-50%);bottom:0;width:min(100%,480px);display:flex;justify-content:space-around;padding:8px 8px calc(8px + env(safe-area-inset-bottom,0px));background:rgba(10,10,18,.75);backdrop-filter:blur(22px);-webkit-backdrop-filter:blur(22px);border-top:1px solid var(--line);z-index:5}
.tabs button{border:0;background:none;color:var(--mut);display:flex;flex-direction:column;align-items:center;gap:3px;font-size:11px;font-weight:600;padding:4px 14px;transition:color .3s,transform .2s}
.tabs button:active{transform:scale(.9)}
.tabs svg{width:24px;height:24px;fill:none;stroke:currentColor;stroke-width:2;stroke-linecap:round;stroke-linejoin:round}
.tabs button.on{color:var(--g)}.tabs button.on svg{filter:drop-shadow(0 0 8px var(--g))}
.mini{position:fixed;left:50%;transform:translateX(-50%);bottom:calc(68px + env(safe-area-inset-bottom,0px));width:min(calc(100% - 24px),456px);display:none;align-items:center;gap:12px;padding:8px 12px 10px 8px;border-radius:18px;background:rgba(30,26,50,.8);border:1px solid var(--line);backdrop-filter:blur(20px);-webkit-backdrop-filter:blur(20px);z-index:5;overflow:hidden}
.mini.show{display:flex;animation:pop .4s both}
.mini img{width:44px;height:44px;border-radius:12px;object-fit:cover}.mini .t{flex:1;min-width:0}.mini b{display:block;font-size:14px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}.mini small{color:var(--mut)}
.mini button{border:0;width:42px;height:42px;border-radius:50%;background:linear-gradient(135deg,var(--g),var(--y));display:grid;place-items:center}.mini svg{width:20px;height:20px;fill:#0a0a12}
.mini .mf{position:absolute;left:0;bottom:0;height:3px;width:0;background:linear-gradient(90deg,var(--g),var(--y),var(--p))}
.wave{display:flex;align-items:center;gap:14px;padding:18px;border-radius:24px;margin-bottom:12px;background:linear-gradient(120deg,rgba(139,92,246,.6),rgba(57,255,136,.4),rgba(255,210,63,.5));background-size:200% 200%;animation:wv 8s ease infinite;border:1px solid var(--line);transition:transform .2s}
.wave:active{transform:scale(.97)}.wave b{font-size:20px;display:block}.wave small{color:rgba(255,255,255,.8)}
.wave span{margin-left:auto;flex:0 0 46px;height:46px;border-radius:50%;background:#fff;color:#0a0a12;display:grid;place-items:center;font-size:18px}
.orb{flex:0 0 46px;height:46px;border-radius:50%;background:radial-gradient(circle at 30% 30%,#fff,var(--y) 35%,var(--g) 65%,var(--p));animation:orb 3s ease-in-out infinite;box-shadow:0 0 30px rgba(255,210,63,.6)}
@keyframes wv{50%{background-position:100% 50%}}@keyframes orb{50%{transform:scale(1.18) rotate(20deg)}}
.ov{position:fixed;inset:0;background:rgba(0,0,0,.55);z-index:30;display:none;align-items:flex-end;justify-content:center;backdrop-filter:blur(4px);-webkit-backdrop-filter:blur(4px)}
.ov.show{display:flex;animation:fd .25s both}@keyframes fd{from{opacity:0}}
.sh{width:min(100%,480px);background:#17142a;border-radius:26px 26px 0 0;border:1px solid var(--line);padding:10px 18px calc(20px + env(safe-area-inset-bottom,0px));max-height:80vh;overflow:auto;animation:up .35s cubic-bezier(.2,.8,.2,1) both}
@keyframes up{from{transform:translateY(100%)}}
.grab{width:40px;height:4px;border-radius:9px;background:rgba(255,255,255,.25);margin:0 auto 12px}.sh h4{margin:0 0 12px;font-size:17px;text-align:center}
.sb{display:block;width:100%;text-align:left;border:0;background:var(--card);color:var(--tx);font-size:16px;padding:15px 16px;border-radius:14px;margin-bottom:8px;font-family:inherit}
.sb.acc{background:linear-gradient(135deg,var(--g),var(--y));color:#0a0a12;font-weight:700;text-align:center}.sb.red{color:#ff6b6b}
.si{display:block;width:100%;background:var(--card);border:1px solid var(--line);color:var(--tx);font-size:16px;padding:14px;border-radius:14px;margin-bottom:10px;outline:0;font-family:inherit}.si:focus{border-color:var(--p)}
.plh{margin-bottom:12px}.plh h2{margin:6px 0 2px;font-size:26px}.plh small{color:var(--mut)}.bk{border:0;background:none;color:var(--g);font-size:15px;padding:0}
.pa{display:flex;gap:8px;margin-top:12px}.pa button{border:1px solid var(--line);background:var(--card);color:var(--tx);padding:10px 14px;border-radius:99px;font-weight:600}.pa .go{background:linear-gradient(135deg,var(--g),var(--y));color:#0a0a12;border:0}
.plus{flex:0 0 48px;width:48px;height:48px;border-radius:12px;display:grid;place-items:center;font-size:24px;background:rgba(255,255,255,.08)}.card.add .plus{width:140px;height:140px;border-radius:20px;border:1px dashed var(--line);font-size:34px}
.hb.mo{font-size:20px;color:var(--tx)}
.disc{border-radius:30px!important;animation:none!important;box-shadow:0 24px 70px rgba(0,0,0,.65),0 0 0 1px rgba(255,255,255,.12)}
.disc::after{display:none}
.ring{border-radius:44px;background:var(--ac,var(--p));animation:glow 4s ease-in-out infinite alternate;transition:opacity .6s,background 1.4s}
@keyframes glow{from{transform:scale(.97)}to{transform:scale(1.07)}}
.wave{position:relative;display:flex;align-items:center;gap:14px;padding:22px 20px;min-height:136px;overflow:hidden;border-radius:28px;margin-bottom:14px;background:linear-gradient(135deg,#2b1570,#10353a 60%,#3a3210);border:1px solid rgba(255,255,255,.14);box-shadow:0 14px 40px rgba(139,92,246,.3);animation:none;transition:transform .2s,box-shadow .6s}
.wave::before{content:"";position:absolute;right:-40px;top:-50px;width:200px;height:200px;border-radius:50%;background:radial-gradient(circle,var(--y),var(--g) 50%,transparent 70%);opacity:.45;filter:blur(10px);animation:orb 4s ease-in-out infinite}
.wv{position:absolute;left:0;bottom:0;width:200%;height:65%;pointer-events:none;animation:slide 10s linear infinite}
.wv.b{height:50%;animation-duration:7s;animation-direction:reverse}
.w1{fill:rgba(57,255,136,.25)}.w2{fill:rgba(255,210,63,.2)}
@keyframes slide{to{transform:translateX(-50%)}}
.wave.live .wv{animation-duration:3.5s}.wave.live .wv.b{animation-duration:2.6s}
.wave.live{box-shadow:0 14px 56px rgba(57,255,136,.45)}
.wt{position:relative;z-index:1;min-width:0;flex:1}.wt b{display:block;font-size:23px;margin:5px 0;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.wt small{display:block;color:rgba(255,255,255,.75);font-size:12px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}.wt small:first-child{letter-spacing:2px;color:var(--y);font-weight:700}
.wb{position:relative;z-index:1;flex:0 0 64px;height:64px;border-radius:50%;background:#fff;display:grid;place-items:center;box-shadow:0 0 0 0 rgba(255,255,255,.5)}
.wb svg{width:28px;height:28px;fill:#0a0a12}
.wave.live .wb{animation:ripple 1.6s ease-out infinite}
@keyframes ripple{to{box-shadow:0 0 0 24px rgba(255,255,255,0)}}
input[type=file]{position:fixed;left:0;top:0;width:1px;height:1px;opacity:0;pointer-events:none}
.ctrl2{display:flex;gap:8px;justify-content:center;margin-top:12px;flex-wrap:wrap}
.ctrl2 button{border:1px solid var(--line);background:var(--card);color:var(--mut);padding:9px 13px;border-radius:99px;font-size:13px;font-weight:600;transition:all .25s}
.ctrl2 button.on{color:#0a0a12;background:linear-gradient(135deg,var(--g),var(--y));border-color:transparent}
.hb.del{font-size:16px}.hb.del.arm{color:#ff6b6b;font-size:13px;font-weight:700}
.toast{position:fixed;left:50%;top:calc(14px + env(safe-area-inset-top,0px));transform:translate(-50%,-20px);background:rgba(30,26,50,.92);border:1px solid var(--g);color:#fff;padding:11px 18px;border-radius:99px;font-size:14px;font-weight:600;opacity:0;pointer-events:none;transition:all .35s;z-index:20;max-width:90vw;box-shadow:0 0 30px rgba(57,255,136,.3)}
.toast.show{opacity:1;transform:translate(-50%,0)}
</style>
</head>
<body>
<div class="bg"><div class="blob b1"></div><div class="blob b2"></div><div class="blob b3"></div></div>
<div class="app" id="app">
  <header><div class="logo">SONIQ</div><button class="add" id="addBtn">＋ Добавить музыку</button></header>
  <section class="view show" id="v-home">
    <h2 class="hi" id="hello"></h2><p class="sub">Что послушаем сегодня?</p>
    <div class="wave" id="wave"><svg class="wv a" viewBox="0 0 800 120" preserveAspectRatio="none"><path class="w1" d="M0 60 Q100 10 200 60 T400 60 T600 60 T800 60 V120 H0Z"/></svg><svg class="wv b" viewBox="0 0 800 120" preserveAspectRatio="none"><path class="w2" d="M0 75 Q100 115 200 75 T400 75 T600 75 T800 75 V120 H0Z"/></svg><div class="wt"><small>SONIQ · МОЯ ВОЛНА</small><b id="wt">Настройся на волну</b><small id="ws">Бесконечный микс из всей музыки</small></div><div class="wb"><svg id="wi" viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></div></div>
    <div class="tiles">
      <div class="tile t1" data-a="fav"><b>♥ Избранное</b><small id="nFav"></small></div>
      <div class="tile t2" data-a="up"><b>⬆ Мои загрузки</b><small id="nUp"></small></div>
      <div class="tile t3" data-a="mix"><b>⚡ Микс</b><small>Случайный трек</small></div>
      <div class="tile t4" data-a="add"><b>＋ Добавить</b><small>Свои файлы</small></div>
    </div>
    <h3>Плейлисты</h3><div class="cards" id="plCards"></div>
    <h3>Для тебя</h3><div class="cards" id="cards"></div>
    <h3>Недавно играло</h3><div id="recent"></div>
  </section>
  <section class="view" id="v-search">
    <h2 class="hi">Поиск</h2>
    <div class="sbox"><span>🔍</span><input id="q" type="search" placeholder="Трек или исполнитель" autocomplete="off"></div>
    <div class="chips"><button class="on" data-f="all">Все</button><button data-f="syn">SONIQ</button><button data-f="up">Мои</button></div>
    <div id="sList"></div>
  </section>
  <section class="view" id="v-lib">
    <h2 class="hi">Коллекция</h2>
    <div class="seg"><button data-s="pl">Плейлисты</button><button data-s="fav">Избранное</button><button data-s="up">Загрузки</button><button data-s="all">Все треки</button></div>
    <div id="libList"></div>
  </section>
  <section class="view" id="v-player">
  <div class="stage"><div class="ring"></div><div class="disc" id="disc"><img id="cover" alt=""></div></div>
  
  <canvas id="viz" width="600" height="140"></canvas>
  <div class="info"><button class="heart" id="heart">♡</button><div class="title" id="title">SONIQ</div><div class="artist" id="artist">Выбери трек</div></div>
  <div class="bar"><div class="track" id="seek"><div class="fill" id="fill"></div><div class="knob" id="knob"></div></div>
    <div class="times"><span id="cur">0:00</span><span id="dur">0:00</span></div></div>
  <div class="ctrl">
    <button id="prev" aria-label="Назад"><svg viewBox="0 0 24 24"><path d="M6 6h2v12H6zM9.5 12 18 18V6z"/></svg></button>
    <button class="play" id="play" aria-label="Играть"><svg id="pi" viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></button>
    <button id="next" aria-label="Вперёд"><svg viewBox="0 0 24 24"><path d="M16 6h2v12h-2zM6 18l8.5-6L6 6z"/></svg></button>
  </div>
  <div class="ctrl2"><button id="shuf">🔀 Перемешать</button><button id="rep">🔁 Повтор</button><button id="sleep">🌙 Таймер</button><button id="more">⋯ Ещё</button></div>
  <h3>Очередь</h3>
  <div id="list"></div>
  </section>
</div>
<div class="mini" id="mini"><img id="mimg" alt=""><div class="t"><b id="mt"></b><small id="ma"></small></div><button id="mplay" aria-label="Играть"><svg id="mpi" viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg></button><div class="mf" id="mfill"></div></div>
<div class="ov" id="ov"><div class="sh" id="sh"></div></div>
<div class="toast" id="toast"></div>
<nav class="tabs">
  <button class="on" id="t-home" data-t="home"><svg viewBox="0 0 24 24"><path d="M3 11l9-8 9 8v10h-6v-6H9v6H3z"/></svg>Главная</button>
  <button id="t-search" data-t="search"><svg viewBox="0 0 24 24"><circle cx="11" cy="11" r="7"/><path d="M20 20l-4-4"/></svg>Поиск</button>
  <button id="t-lib" data-t="lib"><svg viewBox="0 0 24 24"><path d="M4 6h16M4 12h16M4 18h9"/></svg>Коллекция</button>
  <button id="t-player" data-t="player"><svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="9"/><path d="M10 8.5v7l5.5-3.5z"/></svg>Плеер</button>
</nav>
<input type="file" id="fAudio" accept="audio/*,.mp3,.m4a,.aac,.wav,.flac,.ogg,.opus" multiple>
<input type="file" id="fImg" accept="image/*">
<script>
(function(){
var $=function(i){return document.getElementById(i)};
var G='#39ff88',P='#8b5cf6',Y='#ffd23f';
var ctx,master,an,tracks=[],cur=-1,playing=false;
var step=0,nextT=0,startCtx=0,timer=null;
var PLAY='<path d="M8 5v14l11-7z"/>',PAUSE='<path d="M7 5h4v14H7zM13 5h4v14h-4z"/>';

function cover(seed){
  var c=document.createElement('canvas');c.width=c.height=400;var x=c.getContext('2d');
  var cols=[G,P,Y,'#ffffff'];var r=function(n){seed=(seed*9301+49297)%233280;return seed/233280*n};
  x.fillStyle='#0b0b14';x.fillRect(0,0,400,400);
  for(var i=0;i<6;i++){var cx=r(400),cy=r(400),rad=90+r(150);
    var g=x.createRadialGradient(cx,cy,0,cx,cy,rad);var col=cols[i%3];
    g.addColorStop(0,col+'dd');g.addColorStop(1,col+'00');x.fillStyle=g;x.fillRect(0,0,400,400)}
  x.strokeStyle='rgba(255,255,255,.35)';x.lineWidth=2;
  for(i=0;i<5;i++){x.beginPath();x.arc(200,200,40+i*38,0,7);x.stroke()}
  return c.toDataURL('image/jpeg',.85)
}
function mtof(n){return 440*Math.pow(2,(n-69)/12)}
var SYN=[
 {title:'Neon Night',artist:'SONIQ',bpm:104,root:45,prog:[0,-4,-2,-5],arp:[0,7,12,15,12,7,3,7],wave:'sawtooth',seed:11},
 {title:'Lime Dream',artist:'SONIQ',bpm:122,root:48,prog:[0,5,3,7],arp:[0,4,7,12,16,12,7,4],wave:'triangle',seed:77}
];
SYN.forEach(function(s){s.type='synth';s.uid='syn-'+s.seed;s.sd=60/s.bpm/4;s.total=16*s.prog.length*6;s.dur=s.total*s.sd;s.cover=cover(s.seed);tracks.push(s)});

function init(){
  if(ctx){if(ctx.state!=='running')ctx.resume();return}
  ctx=new(window.AudioContext||window.webkitAudioContext)();
  master=ctx.createGain();master.gain.value=.8;an=ctx.createAnalyser();an.fftSize=128;an.smoothingTimeConstant=.82;
  master.connect(an);an.connect(ctx.destination)
}
function tone(type,f,t,d,v,cut){
  var o=ctx.createOscillator(),g=ctx.createGain(),fl=ctx.createBiquadFilter();
  o.type=type;o.frequency.value=f;fl.type='lowpass';fl.frequency.value=cut;
  g.gain.setValueAtTime(0,t);g.gain.linearRampToValueAtTime(v,t+.01);g.gain.exponentialRampToValueAtTime(.0001,t+d);
  o.connect(fl);fl.connect(g);g.connect(master);o.start(t);o.stop(t+d+.05)
}
function noise(t,d,v,hp){
  var b=ctx.createBuffer(1,ctx.sampleRate*d,ctx.sampleRate),a=b.getChannelData(0);
  for(var i=0;i<a.length;i++)a[i]=Math.random()*2-1;
  var s=ctx.createBufferSource(),g=ctx.createGain(),f=ctx.createBiquadFilter();
  s.buffer=b;f.type='highpass';f.frequency.value=hp;g.gain.setValueAtTime(v,t);g.gain.exponentialRampToValueAtTime(.0001,t+d);
  s.connect(f);f.connect(g);g.connect(master);s.start(t)
}
function sched(s,n,t){
  var ch=s.root+s.prog[Math.floor(n/16)%s.prog.length],k=n%16;
  if(k%4===0){var o=ctx.createOscillator(),g=ctx.createGain();o.frequency.setValueAtTime(140,t);o.frequency.exponentialRampToValueAtTime(40,t+.15);
    g.gain.setValueAtTime(.9,t);g.gain.exponentialRampToValueAtTime(.001,t+.25);o.connect(g);g.connect(master);o.start(t);o.stop(t+.3)}
  if(k%2===1)noise(t,.05,.12,7000);
  if(k===4||k===12)noise(t,.14,.22,1800);
  if(k===0||k===6||k===10)tone('sine',mtof(ch-12),t,s.sd*5,.5,500);
  if(k===0)[0,3,7].forEach(function(i){tone(s.wave,mtof(ch+12+i),t,s.sd*15,.07,1400)});
  tone(s.wave,mtof(ch+12+s.arp[n%s.arp.length]),t,s.sd*1.8,.13,3200)
}
function tick(){
  var s=tracks[cur];if(!s||s.type!=='synth')return;
  while(nextT<ctx.currentTime+.15&&step<s.total){sched(s,step,nextT);nextT+=s.sd;step++}
}
function pos(){var s=tracks[cur];if(!s)return 0;return s.type==='synth'?Math.max(0,Math.min(s.dur,ctx.currentTime-startCtx)):s.audio.currentTime}
function stopAll(){
  clearInterval(timer);tracks.forEach(function(t){if(t.audio)t.audio.pause()})
}
function startSynth(off){
  var s=tracks[cur];step=Math.round(off/s.sd);nextT=ctx.currentTime+.05;startCtx=ctx.currentTime-step*s.sd;
  clearInterval(timer);timer=setInterval(tick,25)
}
function load(i){
  init();stopAll();cur=i;recent=[i].concat(recent.filter(function(x){return x!==i}));var s=tracks[i];
  if(s.type==='file'&&!s.src){s.src=ctx.createMediaElementSource(s.audio);s.src.connect(master)}
  $('cover').src=s.cover;applyColor(s.cover);$('title').textContent=s.title;$('artist').textContent=s.artist;
  $('dur').textContent=fmt(s.dur);
  [].forEach.call(document.querySelectorAll('.info>div'),function(e){e.classList.remove('fade');void e.offsetWidth;e.classList.add('fade')});
  if(s.type==='synth')startSynth(0);else{s.audio.currentTime=0;s.audio.play()}
  setPlaying(true);renderList()
}
function toggle(){
  if(cur<0){load(0);return}
  init();var s=tracks[cur];
  if(playing){
    if(s.type==='synth'){clearInterval(timer);step=Math.round(pos()/s.sd)}else s.audio.pause();
    setPlaying(false)
  }else{
    if(s.type==='synth')startSynth(step*s.sd);else s.audio.play();
    setPlaying(true)
  }
  renderList()
}
function setPlaying(v){playing=v;$('app').classList.toggle('playing',v);$('pi').innerHTML=$('mpi').innerHTML=v?PAUSE:PLAY;updWave()}
function go(d){if(!tracks.length)return;var q=curQ(),p=q.indexOf(cur);load(q[(p+d+q.length)%q.length])}
function fmt(t){t=Math.max(0,t|0);return(t/60|0)+':'+('0'+t%60).slice(-2)}

var favs=[],recent=[],seg='fav',q='',flt='all',view='home';
try{favs=JSON.parse(localStorage.getItem('wavefav')||'[]')}catch(e){}
function key(t){return t.title+'|'+t.artist}
function isFav(t){return favs.indexOf(key(t))>-1}
function toggleFav(t){var k=key(t),i=favs.indexOf(k);if(i>-1)favs.splice(i,1);else favs.push(k);try{localStorage.setItem('wavefav',JSON.stringify(favs))}catch(e){}renderList()}
function rowEl(i,n){
  var t=tracks[i],r=document.createElement('div');
  r.className='row'+(i===cur?' on':'')+(playing?' live':'');r.style.animationDelay=Math.min(n,8)*.05+'s';
  r.innerHTML='<img alt=""><div class="t"><b></b><small></small></div><div class="eq"><i></i><i></i><i></i></div><button class="hb'+(isFav(t)?' f':'')+'">'+(isFav(t)?'♥':'♡')+'</button>';
  r.insertAdjacentHTML('beforeend','<button class="hb mo">⋯</button>');r.querySelector('.mo').onclick=function(e){e.stopPropagation();trackSheet(i)};if(0){var del=r.querySelector('.del');
    del.onclick=function(e){e.stopPropagation();if(del.dataset.arm){removeTrack(i)}else{del.dataset.arm='1';del.textContent='Удалить?';del.classList.add('arm');setTimeout(function(){del.dataset.arm='';del.textContent='🗑';del.classList.remove('arm')},2500)}}}
  r.querySelector('img').src=t.cover;r.querySelector('b').textContent=t.title;r.querySelector('small').textContent=t.artist;
  r.querySelector('.hb').onclick=function(e){e.stopPropagation();toggleFav(t)};
  r.onclick=function(){if(i===cur){toggle()}else{queue=null;waveMode=false;load(i)}};return r
}
function fill(id,arr,empty){var l=$(id);l.innerHTML='';if(!arr.length){l.innerHTML='<div class="empty">'+empty+'</div>';return}arr.forEach(function(i,n){l.appendChild(rowEl(i,n))})}
function all(){return tracks.map(function(_,i){return i})}
function libIdx(){return all().filter(function(i){var t=tracks[i];return seg==='all'||(seg==='fav'&&isFav(t))||(seg==='up'&&t.type==='file')})}
function searchIdx(){var v=q.trim().toLowerCase();return all().filter(function(i){var t=tracks[i];if(flt==='up'&&t.type!=='file')return false;if(flt==='syn'&&t.type!=='synth')return false;return !v||(t.title+' '+t.artist).toLowerCase().indexOf(v)>-1})}
function home(){
  var h=new Date().getHours();$('hello').textContent=h<5?'Доброй ночи':h<12?'Доброе утро':h<18?'Добрый день':'Добрый вечер';
  $('nFav').textContent=tracks.filter(isFav).length+' треков';$('nUp').textContent=tracks.filter(function(t){return t.type==='file'}).length+' треков';
  var c=$('cards');c.innerHTML='';
  tracks.forEach(function(t,i){var d=document.createElement('div');d.className='card';d.style.animationDelay=i*.06+'s';d.innerHTML='<img alt=""><b></b><small></small>';
    d.querySelector('img').src=t.cover;d.querySelector('b').textContent=t.title;d.querySelector('small').textContent=t.artist;d.onclick=function(){load(i)};c.appendChild(d)});
  plHome();fill('recent',recent.slice(0,5),'Включи трек — и здесь появится история')
}
function mini(){var t=tracks[cur];$('mini').classList.toggle('show',cur>=0&&view!=='player');if(t){$('mimg').src=t.cover;$('mt').textContent=t.title;$('ma').textContent=t.artist}}
function setView(v){view=v;['home','search','lib','player'].forEach(function(n){$('v-'+n).classList.toggle('show',n===v);$('t-'+n).classList.toggle('on',n===v)});window.scrollTo(0,0);renderList()}
function renderList(){
  fill('list',all(),'');if(seg==='pl'){plRender()}else fill('libList',libIdx(),seg==='fav'?'Нажми ♡ у трека, чтобы добавить в избранное':'Здесь пока пусто');fill('sList',searchIdx(),'Ничего не найдено');home();mini();
  var t=tracks[cur],f=t&&isFav(t);$('heart').textContent=f?'♥':'♡';$('heart').classList.toggle('f',!!f);
  [].forEach.call(document.querySelectorAll('[data-s]'),function(b){b.classList.toggle('on',b.dataset.s===seg)});
  [].forEach.call(document.querySelectorAll('[data-f]'),function(b){b.classList.toggle('on',b.dataset.f===flt)})
}
var shuf=false,rep=0,sleepT=null,sleepIdx=0,db=null;
function toast(m){var e=$('toast');e.textContent=m;e.classList.add('show');clearTimeout(toast.t);toast.t=setTimeout(function(){e.classList.remove('show')},2800)}
function dbOpen(cb){try{var r=indexedDB.open('wave',1);r.onupgradeneeded=function(){r.result.createObjectStore('tr',{keyPath:'id'})};r.onsuccess=function(){db=r.result;cb()};r.onerror=function(){cb()};if(navigator.storage&&navigator.storage.persist)navigator.storage.persist()}catch(e){cb()}}
function dbPut(rec){if(!db)return;try{db.transaction('tr','readwrite').objectStore('tr').put(rec)}catch(e){toast('Не удалось сохранить трек')}}
function dbDel(id){if(!db)return;try{db.transaction('tr','readwrite').objectStore('tr').delete(id)}catch(e){}}
function dbAll(cb){if(!db)return cb([]);try{var q=db.transaction('tr').objectStore('tr').getAll();q.onsuccess=function(){cb(q.result||[])};q.onerror=function(){cb([])}}catch(e){cb([])}}
function makeFileTrack(rec){
  var a=new Audio(URL.createObjectURL(rec.blob));a.preload='metadata';
  var t={type:'file',uid:rec.id,id:rec.id,rec:rec,audio:a,title:rec.title,artist:rec.artist||'Моя музыка',dur:rec.dur||0,cover:rec.coverBlob?URL.createObjectURL(rec.coverBlob):rec.cover};
  a.onloadedmetadata=function(){if(a.duration&&isFinite(a.duration)){t.dur=a.duration;if(!rec.dur){rec.dur=t.dur;dbPut(rec)}}renderList();if(tracks[cur]===t)$('dur').textContent=fmt(t.dur)};
  a.onerror=function(){toast('Не удалось прочитать «'+t.title+'» — возможно, формат не поддерживается')};
  a.onended=function(){next(true)};tracks.push(t);return t
}
function removeTrack(i){
  var t=tracks[i];if(!t||t.type!=='file')return;
  if(i===cur){stopAll();setPlaying(false);cur=-1}else if(i<cur)cur--;
  recent=recent.filter(function(x){return x!==i}).map(function(x){return x>i?x-1:x});
  try{t.audio.pause();URL.revokeObjectURL(t.audio.src)}catch(e){}
  dbDel(t.id);tracks.splice(i,1);
  if(cur<0){$('cover').src=tracks[0].cover;$('title').textContent=tracks[0].title;$('artist').textContent=tracks[0].artist;$('dur').textContent=fmt(tracks[0].dur)}
  toast('Трек удалён');renderList()
}
function next(auto){
  if(auto&&rep===2){load(cur);return}
  var q=curQ();if(shuf&&q.length>1){var n;do{n=q[Math.floor(Math.random()*q.length)]}while(n===cur);load(n);return}
  if(auto&&rep===0&&cur===q[q.length-1]){stopAll();setPlaying(false);step=0;renderList();return}
  go(1)
}
function sleepCycle(){
  var o=[0,15,30,60],b=$('sleep');sleepIdx=(sleepIdx+1)%4;clearTimeout(sleepT);var m=o[sleepIdx];
  b.classList.toggle('on',!!m);b.textContent=m?'🌙 '+m+' мин':'🌙 Таймер';
  if(m){toast('Остановлю музыку через '+m+' мин');sleepT=setTimeout(function(){if(playing)toggle();toast('Таймер сна: музыка остановлена');sleepIdx=0;b.classList.remove('on');b.textContent='🌙 Таймер'},m*60000)}
}
var pls=[],openPl=null,queue=null;try{pls=JSON.parse(localStorage.getItem('soniqpl')||'[]')}catch(e){}
function savePl(){try{localStorage.setItem('soniqpl',JSON.stringify(pls))}catch(e){}}
function getPl(id){return pls.filter(function(p){return p.id===id})[0]}
function idxOf(u){for(var i=0;i<tracks.length;i++)if(tracks[i].uid===u)return i;return -1}
function plIdx(p){return p.ids.map(idxOf).filter(function(x){return x>-1})}
function curQ(){return(queue&&queue.indexOf(cur)>-1)?queue:all()}
function applyColor(src){var im=new Image();im.onload=function(){try{var c=document.createElement('canvas');c.width=c.height=8;var x=c.getContext('2d');x.drawImage(im,0,0,8,8);var d=x.getImageData(0,0,8,8).data,r=0,g=0,b=0,n=0;for(var i=0;i<d.length;i+=4){if(Math.max(d[i],d[i+1],d[i+2])-Math.min(d[i],d[i+1],d[i+2])>40){r+=d[i];g+=d[i+1];b+=d[i+2];n++}}if(n)document.documentElement.style.setProperty('--ac','rgb('+(r/n|0)+','+(g/n|0)+','+(b/n|0)+')')}catch(e){}};im.src=src}
function openSheet(title,build){var sh=$('sh');sh.innerHTML='<div class="grab"></div><h4></h4>';sh.querySelector('h4').textContent=title;build(sh);$('ov').classList.add('show')}
function closeSheet(){$('ov').classList.remove('show')}
function btn(sh,txt,fn,cls){var b=document.createElement('button');b.className='sb '+(cls||'');b.textContent=txt;b.onclick=fn;sh.appendChild(b);return b}
function inp(v,ph){var e=document.createElement('input');e.className='si';e.value=v;e.placeholder=ph;return e}
function nameSheet(title,val,cb){openSheet(title,function(sh){var e=inp(val,'Название');sh.appendChild(e);btn(sh,'Сохранить',function(){var v=e.value.trim();if(!v)return;closeSheet();cb(v)},'acc');setTimeout(function(){e.focus()},300)})}
function editSheet(i){var t=tracks[i];openSheet('Изменить трек',function(sh){var a=inp(t.title,'Название'),b=inp(t.artist,'Исполнитель');sh.appendChild(a);sh.appendChild(b);
  btn(sh,'Сохранить',function(){var was=isFav(t),old=key(t);t.title=a.value.trim()||t.title;t.artist=b.value.trim()||t.artist;t.rec.title=t.title;t.rec.artist=t.artist;dbPut(t.rec);
    if(was){favs[favs.indexOf(old)]=key(t);try{localStorage.setItem('wavefav',JSON.stringify(favs))}catch(e){}}
    closeSheet();if(cur===i){$('title').textContent=t.title;$('artist').textContent=t.artist}renderList()},'acc')})}
function plPick(i){var t=tracks[i];openSheet('В плейлист',function(sh){
  pls.forEach(function(p){btn(sh,p.name+' · '+p.ids.length,function(){if(p.ids.indexOf(t.uid)<0)p.ids.push(t.uid);savePl();closeSheet();toast('Добавлено в «'+p.name+'»');renderList()})});
  btn(sh,'＋ Новый плейлист',function(){nameSheet('Новый плейлист','',function(v){pls.push({id:'p'+Date.now(),name:v,ids:[t.uid]});savePl();toast('Создан «'+v+'»');renderList()})},'acc')})}
function trackSheet(i){var t=tracks[i];openSheet(t.title,function(sh){
  btn(sh,isFav(t)?'♥ Убрать из любимых':'♡ В любимые',function(){toggleFav(t);closeSheet()});
  btn(sh,'＋ Добавить в плейлист',function(){plPick(i)});
  if(openPl&&seg==='pl'&&view==='lib')btn(sh,'− Убрать из этого плейлиста',function(){var p=getPl(openPl);p.ids=p.ids.filter(function(u){return u!==t.uid});savePl();closeSheet();renderList()});
  if(t.type==='file'){btn(sh,'✎ Изменить название',function(){editSheet(i)});btn(sh,'🖼 Сменить обложку',function(){closeSheet();imgFor=i;$('fImg').click()});btn(sh,'🗑 Удалить трек',function(){closeSheet();removeTrack(i)},'red')}
  btn(sh,'Закрыть',closeSheet)})}
function plHome(){var c=$('plCards');c.innerHTML='';
  pls.forEach(function(p,n){var ix=plIdx(p),d=document.createElement('div');d.className='card';d.innerHTML='<img alt=""><b></b><small></small>';d.querySelector('img').src=ix.length?tracks[ix[0]].cover:cover(n*53+5);d.querySelector('b').textContent=p.name;d.querySelector('small').textContent=ix.length+' треков';d.onclick=function(){openPl=p.id;seg='pl';setView('lib')};c.appendChild(d)});
  var a=document.createElement('div');a.className='card add';a.innerHTML='<div class="plus">＋</div><b>Создать</b><small>Новый плейлист</small>';a.onclick=newPl;c.appendChild(a)}
function newPl(){nameSheet('Новый плейлист','',function(v){pls.push({id:'p'+Date.now(),name:v,ids:[]});savePl();renderList()})}
function plRender(){
  var l=$('libList');l.innerHTML='';var p=openPl&&getPl(openPl);
  if(p){
    var ix=plIdx(p),h=document.createElement('div');h.className='plh';
    h.innerHTML='<button class="bk">‹ Плейлисты</button><h2></h2><small></small><div class="pa"><button class="go">▶ Слушать</button><button class="ed">✎ Название</button><button class="rm">🗑</button></div>';
    h.querySelector('h2').textContent=p.name;h.querySelector('small').textContent=ix.length+' треков';
    h.querySelector('.bk').onclick=function(){openPl=null;renderList()};
    h.querySelector('.go').onclick=function(){if(ix.length){queue=ix.slice();load(ix[0])}};
    h.querySelector('.ed').onclick=function(){nameSheet('Название плейлиста',p.name,function(v){p.name=v;savePl();renderList()})};
    h.querySelector('.rm').onclick=function(){openSheet('Удалить «'+p.name+'»?',function(sh){btn(sh,'Удалить плейлист',function(){pls=pls.filter(function(x){return x!==p});savePl();openPl=null;closeSheet();renderList()},'red');btn(sh,'Отмена',closeSheet)})};
    l.appendChild(h);
    if(!ix.length)l.insertAdjacentHTML('beforeend','<div class="empty">Пусто. Нажми ⋯ у любого трека → «Добавить в плейлист»</div>');
    ix.forEach(function(i,n){var r=rowEl(i,n);r.onclick=function(){queue=ix.slice();if(i===cur)toggle();else load(i)};l.appendChild(r)})
  }else{
    var nb=document.createElement('div');nb.className='row';nb.innerHTML='<div class="plus">＋</div><div class="t"><b>Новый плейлист</b></div>';nb.onclick=newPl;l.appendChild(nb);
    pls.forEach(function(q,n){var ix=plIdx(q),r=document.createElement('div');r.className='row';r.innerHTML='<img alt=""><div class="t"><b></b><small></small></div><span style="color:var(--mut)">›</span>';
      r.querySelector('img').src=ix.length?tracks[ix[0]].cover:cover(n*53+5);r.querySelector('b').textContent=q.name;r.querySelector('small').textContent=ix.length+' треков';r.onclick=function(){openPl=q.id;renderList()};l.appendChild(r)})
  }
}
var imgFor=-1,waveMode=false;
function updWave(){var on=waveMode&&playing&&cur>=0,t=tracks[cur];$('wave').classList.toggle('live',on);$('wi').innerHTML=on?PAUSE:PLAY;
  $('wt').textContent=waveMode&&t?t.title:'Настройся на волну';$('ws').textContent=waveMode&&t?(playing?'Играет · ':'Пауза · ')+t.artist:'Бесконечный микс из всей музыки'}
function dec(a,e){try{return new TextDecoder(e===3?'utf-8':e===0?'windows-1251':'utf-16').decode(a).split(String.fromCharCode(0)).join('').trim()}catch(x){return ''}}
function embCover(f,cb){
  var r=new FileReader(),m={};
  r.onload=function(){try{
    var d=new Uint8Array(r.result),n=d.length,p,mk=function(s){return new Blob([s],{type:s[0]===137?'image/png':'image/jpeg'})};
    if(d[0]===73&&d[1]===68&&d[2]===51){
      var v=d[3],end=Math.min(n,10+(((d[6]&127)<<21)|((d[7]&127)<<14)|((d[8]&127)<<7)|(d[9]&127)));p=10;
      while(p+10<end){
        var id=String.fromCharCode(d[p],d[p+1],d[p+2],d[p+3]),fs=v===4?(((d[p+4]&127)<<21)|((d[p+5]&127)<<14)|((d[p+6]&127)<<7)|(d[p+7]&127)):(d[p+4]*16777216+(d[p+5]<<16)+(d[p+6]<<8)+d[p+7]);
        if(!fs||p+10+fs>n)break;
        if(id==='TIT2')m.title=dec(d.subarray(p+11,p+10+fs),d[p+10]);
        if(id==='TPE1')m.artist=dec(d.subarray(p+11,p+10+fs),d[p+10]);
        if(id==='APIC'){var q=p+11,en=d[p+10];while(d[q])q++;q+=2;
          if(en===1||en===2){while(d[q]||d[q+1])q+=2;q+=2}else{while(d[q])q++;q++}
          var s=d.subarray(q,p+10+fs);if(s.length>100)m.b=mk(s)}
        p+=10+fs
      }
    }else{
      for(var i=0;i<n-12;i++)if(d[i]===99&&d[i+1]===111&&d[i+2]===118&&d[i+3]===114){
        for(var j=i;j<i+40;j++)if(d[j]===100&&d[j+1]===97&&d[j+2]===116&&d[j+3]===97){
          var sz=d[j-4]*16777216+(d[j-3]<<16)+(d[j-2]<<8)+d[j-1],s2=d.subarray(j+12,j-4+sz);if(s2.length>100)m.b=mk(s2);break}
        break}
    }
  }catch(x){}cb(m)};
  r.onerror=function(){cb(m)};r.readAsArrayBuffer(f.slice(0,4194304))
}
function renderOld(){
  var l=$('list');l.innerHTML='';
  tracks.forEach(function(t,i){
    var r=document.createElement('div');r.className='row'+(i===cur?' on':'')+(playing?' live':'');r.style.animationDelay=i*.07+'s';
    r.innerHTML='<img src="'+t.cover+'" alt=""><div class="t"><b></b><small></small></div><div class="eq"><i></i><i></i><i></i></div><small>'+fmt(t.dur)+'</small>';
    r.querySelector('b').textContent=t.title;r.querySelector('small').textContent=t.artist;
    r.onclick=function(){i===cur?toggle():load(i)};l.appendChild(r)
  })
}
$('addBtn').onclick=function(){$('fAudio').click()};
$('fAudio').onchange=function(e){
  var fs=[].slice.call(e.target.files);e.target.value='';
  if(!fs.length)return;
  fs.forEach(function(f,n){
    var rec={id:Date.now()+'-'+n,title:f.name.replace(/\.[^.]+$/,''),artist:'Моя музыка',blob:f,dur:0,cover:cover(Date.now()%1000+n*37),added:Date.now()+n};
    embCover(f,function(m){if(m.b)rec.coverBlob=m.b;if(m.title)rec.title=m.title;if(m.artist)rec.artist=m.artist;makeFileTrack(rec);dbPut(rec);renderList()})
  });
  seg='up';toast('Добавлено треков: '+fs.length);setView('lib')
};

$('fImg').onchange=function(e){
  var f=e.target.files[0];if(!f||imgFor<0)return;
  var tt=tracks[imgFor];tt.cover=URL.createObjectURL(f);if(tt.rec){tt.rec.coverBlob=f;dbPut(tt.rec)}if(imgFor===cur){$('cover').src=tt.cover;applyColor(tt.cover)}renderList();e.target.value=''
};
$('play').onclick=toggle;$('next').onclick=function(){next(false)};$('prev').onclick=function(){go(-1)};
var sk=$('seek'),drag=false;
function seekTo(ev){
  if(cur<0)return;var r=sk.getBoundingClientRect(),p=Math.max(0,Math.min(1,(ev.clientX-r.left)/r.width)),s=tracks[cur];
  if(s.type==='synth'){step=Math.round(p*s.dur/s.sd);startCtx=ctx.currentTime-step*s.sd;nextT=ctx.currentTime+.05}else s.audio.currentTime=p*s.dur
}
sk.addEventListener('pointerdown',function(e){drag=true;seekTo(e)});
window.addEventListener('pointermove',function(e){if(drag)seekTo(e)});
window.addEventListener('pointerup',function(){drag=false});

var cv=$('viz'),c2=cv.getContext('2d'),data=new Uint8Array(64),lv=new Array(32).fill(0);
function frame(){
  requestAnimationFrame(frame);
  var W=cv.width,H=cv.height;c2.clearRect(0,0,W,H);
  if(an&&playing)an.getByteFrequencyData(data);
  var g=c2.createLinearGradient(0,0,W,0);g.addColorStop(0,G);g.addColorStop(.5,Y);g.addColorStop(1,P);c2.fillStyle=g;
  var bw=W/32;
  for(var i=0;i<32;i++){
    var v=playing?data[i+1]/255:0;lv[i]+=(v-lv[i])*.25;
    var h=Math.max(4,lv[i]*H);var x=i*bw+3;
    c2.beginPath();c2.roundRect?c2.roundRect(x,H-h,bw-6,h,6):c2.rect(x,H-h,bw-6,h);c2.fill()
  }
  if(cur>=0){
    var s=tracks[cur],p=pos(),d=s.dur||1,pc=Math.min(1,p/d)*100;
    $('fill').style.width=pc+'%';$('mfill').style.width=pc+'%';$('knob').style.left=pc+'%';$('cur').textContent=fmt(p);
    if(playing&&s.type==='synth'&&p>=s.dur-.02)next(true)
  }
}
$('cover').src=tracks[0].cover;$('title').textContent=tracks[0].title;$('artist').textContent=tracks[0].artist;$('dur').textContent=fmt(tracks[0].dur);
$('heart').onclick=function(){if(cur>=0)toggleFav(tracks[cur])};
[].forEach.call(document.querySelectorAll('[data-t]'),function(b){b.onclick=function(){setView(b.dataset.t)}});
[].forEach.call(document.querySelectorAll('[data-s]'),function(b){b.onclick=function(){seg=b.dataset.s;openPl=null;renderList()}});
[].forEach.call(document.querySelectorAll('[data-f]'),function(b){b.onclick=function(){flt=b.dataset.f;renderList()}});
[].forEach.call(document.querySelectorAll('[data-a]'),function(b){b.onclick=function(){var a=b.dataset.a;
  if(a==='fav'||a==='up'){seg=a;setView('lib')}else if(a==='mix'){load(Math.floor(Math.random()*tracks.length))}else $('fAudio').click()}});
$('q').oninput=function(){q=this.value;fill('sList',searchIdx(),'Ничего не найдено')};
$('mini').onclick=function(){setView('player')};
$('mplay').onclick=function(e){e.stopPropagation();toggle()};
$('shuf').onclick=function(){shuf=!shuf;this.classList.toggle('on',shuf)};
$('rep').onclick=function(){rep=(rep+1)%3;this.classList.toggle('on',rep>0);this.textContent=rep===2?'🔂 Один':rep===1?'🔁 Все':'🔁 Повтор'};
$('sleep').onclick=sleepCycle;
$('more').onclick=function(){if(cur>=0)trackSheet(cur);else toast('Сначала включи трек')};
$('ov').onclick=function(e){if(e.target===this)closeSheet()};
$('wave').onclick=function(){if(waveMode&&cur>=0){toggle();return}waveMode=true;shuf=true;$('shuf').classList.add('on');queue=null;load(Math.floor(Math.random()*tracks.length));toast('Моя волна запущена')};
renderList();frame();
dbOpen(function(){dbAll(function(rs){rs.sort(function(a,b){return a.added-b.added}).forEach(makeFileTrack);if(rs.length)renderList()})});
})();
</script>
</body>
</html>