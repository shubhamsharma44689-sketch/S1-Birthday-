# S1-Birthday-<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Happy Birthday Celebration</title>
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; user-select: none; -webkit-tap-highlight-color: transparent; }
    body { background: #0d060a; color: #fff; display: flex; justify-content: center; align-items: center; min-height: 100vh; overflow: hidden; }
    .app-viewport { width: 100%; max-width: 420px; height: 100vh; max-height: 860px; background: #11050a; position: relative; overflow: hidden; display: flex; flex-direction: column; box-shadow: 0 0 40px rgba(255, 64, 129, 0.2); }
    .top-bar { position: absolute; top: 15px; left: 15px; right: 15px; display: flex; justify-content: space-between; z-index: 100; }
    .pill-btn { background: rgba(255, 255, 255, 0.15); backdrop-filter: blur(8px); border: 1px solid rgba(255, 255, 255, 0.2); color: #fff; padding: 6px 14px; border-radius: 20px; font-size: 13px; font-weight: 500; cursor: pointer; }
    .slide { position: absolute; top: 0; left: 0; width: 100%; height: 100%; display: none; flex-direction: column; align-items: center; justify-content: center; padding: 30px 20px 40px 20px; text-align: center; animation: fadeIn 0.5s ease forwards; }
    .slide.active { display: flex; }
    @keyframes fadeIn { from { opacity: 0; transform: scale(0.97); } to { opacity: 1; transform: scale(1); } }
    .prompt-bottom { position: absolute; bottom: 25px; font-size: 13px; color: rgba(255, 255, 255, 0.6); letter-spacing: 0.5px; animation: pulseText 2s infinite; }
    @keyframes pulseText { 0%, 100% { opacity: 0.4; } 50% { opacity: 1; } }
    #slide1 { background: radial-gradient(circle at center, #2e0817 0%, #0d0207 100%); cursor: pointer; }
    .big-heart { font-size: 90px; animation: heartBeat 1.4s infinite; filter: drop-shadow(0 0 25px rgba(255, 75, 120, 0.8)); }
    @keyframes heartBeat { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.18); } }
    .slide1-title { font-size: 32px; font-weight: 700; margin-bottom: 25px; font-family: serif; }
    #slide2 { background: linear-gradient(180deg, #42060e 0%, #1a0105 100%); cursor: pointer; }
    .sub-italic { font-style: italic; color: #ffb3c1; font-size: 18px; margin-bottom: 15px; }
    .main-bday-text { font-size: 44px; font-weight: 900; line-height: 1.1; letter-spacing: 1px; }
    .gold-divider { width: 140px; height: 2px; background: linear-gradient(90deg, transparent, #e0a96d, transparent); margin: 25px auto; }
    #slide3 { background: radial-gradient(circle at top, #3d1024 0%, #0d0207 80%); cursor: pointer; }
    .tree-box { position: relative; width: 240px; height: 240px; margin-bottom: 20px; }
    .tree-trunk { width: 6px; height: 120px; background: #8b5a2b; margin: 0 auto; position: absolute; bottom: 0; left: 50%; transform: translateX(-50%); border-radius: 4px; }
    .tree-foliage { position: absolute; top: 10px; left: 50%; transform: translateX(-50%); font-size: 90px; filter: drop-shadow(0 0 20px rgba(255, 105, 180, 0.6)); animation: heartBeat 2s infinite ease-in-out; }
    .tree-details { background: rgba(255, 255, 255, 0.08); backdrop-filter: blur(10px); padding: 16px 24px; border-radius: 18px; border: 1px solid rgba(255, 255, 255, 0.15); width: 90%; }
    #slide4 { background: #0f050b; }
    .cake-box { font-size: 110px; margin-bottom: 20px; cursor: pointer; position: relative; display: inline-block; }
    .candle-flame { position: absolute; top: 18px; left: 50%; transform: translateX(-50%); font-size: 24px; filter: drop-shadow(0 0 10px #ffea00); animation: flicker 1s infinite alternate; }
    @keyframes flicker { 0% { opacity: 0.8; transform: translateX(-50%) scale(0.9); } 100% { opacity: 1; transform: translateX(-50%) scale(1.2); } }
    #slide5 { background: #0f050b; justify-content: flex-start; padding-top: 65px; }
    .balloon-cluster { display: flex; gap: 12px; margin: 15px 0 20px 0; justify-content: center; }
    .balloon-node { font-size: 40px; cursor: pointer; animation: floatBal 2.4s ease-in-out infinite alternate; }
    @keyframes floatBal { 0% { transform: translateY(0); } 100% { transform: translateY(-10px); } }
    .reasons-list { width: 100%; display: flex; flex-direction: column; gap: 9px; max-height: 380px; overflow-y: auto; }
    .reason-card { background: rgba(255, 255, 255, 0.08); border: 1px solid rgba(255, 200, 150, 0.25); border-radius: 12px; padding: 10px 14px; text-align: left; font-size: 13px; color: #ffeef2; }
    #slide6 { background: #0c0408; }
    .polaroid { background: #fff; padding: 12px 12px 28px 12px; border-radius: 6px; box-shadow: 0 10px 30px rgba(0,0,0,0.6); width: 250px; transform: rotate(-2deg); }
    .polaroid img { width: 100%; height: 250px; object-fit: cover; border-radius: 4px; display: block; }
    .polaroid p { color: #333; font-size: 14px; margin-top: 10px; font-weight: 600; }
    .gallery-nav { display: flex; gap: 15px; margin-top: 25px; }
    #slide7 { background: #11050a; }
    .envelope-wrapper { width: 270px; height: 180px; background: #d4a373; border-radius: 8px; display: flex; align-items: center; justify-content: center; cursor: pointer; }
    .seal-stamp { width: 48px; height: 48px; background: #a33b3b; color: #fff; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 20px; font-weight: 700; }
    .letter-modal { display: none; background: #fff8f0; color: #2b2b2b; width: 95%; max-height: 480px; overflow-y: auto; border-radius: 16px; padding: 24px; text-align: left; font-size: 14px; line-height: 1.6; }
    #slide8 { background: radial-gradient(circle at center, #35081c 0%, #0d0207 100%); }
    .primary-btn { background: linear-gradient(135deg, #ff4d6d, #c9184a); border: none; color: white; padding: 12px 28px; border-radius: 30px; font-size: 15px; font-weight: 600; cursor: pointer; margin-top: 18px; }
    .edit-modal { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.85); z-index: 999; display: none; align-items: center; justify-content: center; padding: 15px; }
    .edit-content { background: #1c0e16; border: 1px solid rgba(255, 255, 255, 0.2); width: 100%; max-width: 380px; max-height: 90vh; overflow-y: auto; border-radius: 20px; padding: 22px; text-align: left; }
    .field-wrap { margin-bottom: 12px; }
    .field-wrap label { display: block; font-size: 12px; color: #aaa; margin-bottom: 4px; }
    .field-wrap input, .field-wrap textarea { width: 100%; background: #2a1522; border: 1px solid #48233b; padding: 8px 12px; border-radius: 8px; color: #fff; font-size: 13px; outline: none; }
  </style>
</head>
<body>

  <div class="app-viewport">
    <div class="top-bar">
      <button class="pill-btn" onclick="openCustomizer()">⚙️ Customize</button>
      <button class="pill-btn" onclick="copyShareLink()">🔗 Copy Link</button>
    </div>

    <!-- Slide 1 -->
    <div class="slide active" id="slide1" onclick="nextSlide(2)">
      <div class="slide1-title">Send this 🫶</div>
      <div class="big-heart">💖</div>
      <div class="prompt-bottom">Tap anywhere to start ✨</div>
    </div>

    <!-- Slide 2 -->
    <div class="slide" id="slide2" onclick="nextSlide(3)">
      <div class="sub-italic">make a wish...</div>
      <div class="main-bday-text">Happy<br>Birthday</div>
      <div class="gold-divider"></div>
      <div style="font-size: 14px; color: #ffb3c1;">to someone worth celebrating</div>
      <div class="prompt-bottom">tap anywhere to continue</div>
    </div>

    <!-- Slide 3 -->
    <div class="slide" id="slide3" onclick="nextSlide(4)">
      <div class="tree-box">
        <div class="tree-foliage">🌸</div>
        <div class="tree-trunk"></div>
      </div>
      <div class="tree-details">
        <div style="font-size: 12px; color: #ff99aa; margin-bottom: 5px;">it's officially your day</div>
        <h2 id="dispTreeName" style="font-size: 24px; margin-bottom: 5px;">Happy Birthday, Tanisha</h2>
        <div id="dispTreeAge" style="font-size: 14px; color: #f8edeb;">and just like that, you're turning 21 ✨</div>
      </div>
      <div class="prompt-bottom">tap anywhere to continue</div>
    </div>

    <!-- Slide 4 -->
    <div class="slide" id="slide4">
      <h3 style="font-size: 20px; margin-bottom: 25px;">First things first 🎂</h3>
      <div class="cake-box" onclick="blowCandle()">
        <span class="candle-flame" id="flameIcon">🔥</span>🎂
      </div>
      <div id="candleInstruction" style="font-size: 14px; color: #ffccd5;">मोमबत्ती बुझाने के लिए केक पर टच करें! 🕯️</div>
      <button class="primary-btn" id="cakeNextBtn" style="display:none;" onclick="nextSlide(5)">Continue ➔</button>
    </div>

    <!-- Slide 5 -->
    <div class="slide" id="slide5">
      <h3 style="font-size: 20px; margin-bottom: 4px;">Pop the balloons 🎈</h3>
      <div style="font-size: 12px; color: #bbb; margin-bottom: 12px;">गुब्बारों को फोड़ें और वजह पढ़ें 💕</div>
      <div class="balloon-cluster">
        <span class="balloon-node" onclick="popBalloon(0, this)">🎈</span>
        <span class="balloon-node" onclick="popBalloon(1, this)">🎈</span>
        <span class="balloon-node" onclick="popBalloon(2, this)">🎈</span>
        <span class="balloon-node" onclick="popBalloon(3, this)">🎈</span>
        <span class="balloon-node" onclick="popBalloon(4, this)">🎈</span>
      </div>
      <div class="reasons-list" id="reasonsList"></div>
      <button class="primary-btn" id="balNextBtn" style="display:none;" onclick="nextSlide(6)">Keep going ✨</button>
    </div>

    <!-- Slide 6 -->
    <div class="slide" id="slide6">
      <h3 style="font-size: 20px; margin-bottom: 16px;">A walk down memory lane 📸</h3>
      <div class="polaroid">
        <img id="dispPhoto" src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=500" alt="Memory">
        <p id="dispPhotoCap">Sweet memories with you 💛</p>
      </div>
      <div class="gallery-nav">
        <button class="pill-btn" onclick="prevPhoto()">◀ Back</button>
        <button class="pill-btn" onclick="nextPhoto()">Next ▶</button>
      </div>
      <button class="primary-btn" onclick="nextSlide(7)">Next ➔</button>
    </div>

    <!-- Slide 7 -->
    <div class="slide" id="slide7">
      <div id="envelopeView">
        <h3 style="font-size: 20px; margin-bottom: 25px;" id="envelopeHeader">One last thing... 💌</h3>
        <div class="envelope-wrapper" onclick="openLetter()">
          <div class="seal-stamp" id="sealLetter">T</div>
        </div>
        <div class="prompt-bottom">Tap envelope to open your letter</div>
      </div>
      <div class="letter-modal" id="letterModal">
        <h4 id="letterGreeting" style="font-size: 18px; color: #b7094c; margin-bottom: 12px;">Dear Birthday Star,</h4>
        <div id="letterContent" style="white-space: pre-wrap;">जन्मदिन की बहुत-बहुत शुभकामनाएँ! आपके साथ बिताया हर पल बेहद कीमती है। ईश्वर आपको दुनिया की हर खुशी और कामयाबी दे।</div>
        <div style="text-align: right; margin-top: 16px; font-weight: bold; color: #b7094c;" id="dispSenderName">— With all my love</div>
        <button class="primary-btn" style="width: 100%; margin-top: 20px;" onclick="nextSlide(8)">Complete Celebration 💖</button>
      </div>
    </div>

    <!-- Slide 8 -->
    <div class="slide" id="slide8">
      <div style="font-size: 65px; margin-bottom: 15px;">🎉🐱🥳</div>
      <h2 style="font-size: 30px; margin-bottom: 8px;">HAPPY BIRTHDAY!</h2>
      <h3 id="dispFinalName" style="color: #ff758f; font-size: 24px; margin-bottom: 25px;">Tanisha</h3>
      <p style="font-size: 14px; color: #ddd; max-width: 280px; margin-bottom: 25px;">May your day be filled with lots of love, laughter, and endless sweet surprises! 🎂✨</p>
      <button class="primary-btn" onclick="replayAll()">Replay From Start 🔁</button>
    </div>
  </div>

  <!-- Customization Modal -->
  <div class="edit-modal" id="customModal">
    <div class="edit-content">
      <h3 style="color:#ff758f; margin-bottom:12px;">⚙️ Customize Celebration</h3>
      <div class="field-wrap">
        <label>Name:</label>
        <input type="text" id="cfgName" value="Tanisha">
      </div>
      <div class="field-wrap">
        <label>Age:</label>
        <input type="number" id="cfgAge" value="21">
      </div>
      <div class="field-wrap">
        <label>Sender Name:</label>
        <input type="text" id="cfgSender" value="Mahi">
      </div>
      <div class="field-wrap">
        <label>5 Reasons (कॉमा से अलग करें):</label>
        <textarea id="cfgReasons" rows="3">Your laugh is my favourite sound,You make ordinary days feel special,My worst days get shorter when you call,The world is kinder with you in it,You always believe in me</textarea>
      </div>
      <div class="field-wrap">
        <label>Letter Message:</label>
        <textarea id="cfgLetter" rows="4">जन्मदिन की बहुत-बहुत शुभकामनाएँ! आपके साथ बिताया हर पल बेहद कीमती है। ईश्वर आपको दुनिया की हर खुशी और कामयाबी दे।</textarea>
      </div>
      <div class="field-wrap">
        <label>Photo URL:</label>
        <input type="text" id="cfgPhoto" value="https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=500">
      </div>
      <div style="display: flex; gap: 8px; margin-top: 15px;">
        <button class="primary-btn" style="flex:1;" onclick="applyCustomData()">Apply & Save</button>
        <button class="pill-btn" onclick="closeCustomizer()">Close</button>
      </div>
    </div>
  </div>

  <script>
    let config = {
      name: "Tanisha",
      age: 21,
      sender: "Mahi",
      reasons: ["Your laugh is my favourite sound 🎵", "You make ordinary days feel special ✨", "My worst days get shorter when you call 📞", "The world is kinder with you in it 🌍", "You always believe in me 💕"],
      letter: "जन्मदिन की बहुत-बहुत शुभकामनाएँ! आपके साथ बिताया हर पल बेहद कीमती है। ईश्वर आपको दुनिया की हर खुशी और कामयाबी दे।",
      photo: "https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=500"
    };

    let poppedCount = 0;
    let photoIndex = 0;
    const samplePhotos = [
      "https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=500",
      "https://images.unsplash.com/photo-1517841905240-472988babdf9?w=500",
      "https://images.unsplash.com/photo-1524504388940-b1c1722653e1?w=500"
    ];

    function showSlide(num) {
      document.querySelectorAll('.slide').forEach(s => s.classList.remove('active'));
      const target = document.getElementById(`slide${num}`);
      if(target) target.classList.add('active');
    }

    function nextSlide(num) {
      showSlide(num);
      if(num === 8) confetti({ particleCount: 150, spread: 80, origin: { y: 0.6 } });
    }

    function blowCandle() {
      const flame = document.getElementById('flameIcon');
      if (flame.style.display !== 'none') {
        flame.style.display = 'none';
        document.getElementById('candleInstruction').innerText = "Make a wish! Wish granted! ✨";
        document.getElementById('cakeNextBtn').style.display = 'inline-block';
        confetti({ particleCount: 80, spread: 60, origin: { y: 0.55 } });
      }
    }

    function popBalloon(index, el) {
      if(el.style.visibility === 'hidden') return;
      el.style.visibility = 'hidden';
      confetti({ particleCount: 30, spread: 45, origin: { y: 0.4 } });
      const list = document.getElementById('reasonsList');
      const item = document.createElement('div');
      item.className = 'reason-card';
      item.innerHTML = `<strong>REASON NO.${index + 1} 💖</strong><br>${config.reasons[index] || "You are truly amazing!"}`;
      list.appendChild(item);
      poppedCount++;
      if(poppedCount >= 5) document.getElementById('balNextBtn').style.display = 'inline-block';
    }

    function nextPhoto() {
      photoIndex = (photoIndex + 1) % samplePhotos.length;
      document.getElementById('dispPhoto').src = (photoIndex === 0 && config.photo) ? config.photo : samplePhotos[photoIndex];
    }
    function prevPhoto() {
      photoIndex = (photoIndex - 1 + samplePhotos.length) % samplePhotos.length;
      document.getElementById('dispPhoto').src = (photoIndex === 0 && config.photo) ? config.photo : samplePhotos[photoIndex];
    }

    function openLetter() {
      document.getElementById('envelopeView').style.display = 'none';
      document.getElementById('letterModal').style.display = 'block';
      confetti({ particleCount: 70, spread: 70, origin: { y: 0.6 } });
    }

    function replayAll() {
      poppedCount = 0;
      document.getElementById('reasonsList').innerHTML = '';
      document.querySelectorAll('.balloon-node').forEach(b => b.style.visibility = 'visible');
      document.getElementById('balNextBtn').style.display = 'none';
      document.getElementById('cakeNextBtn').style.display = 'none';
      document.getElementById('flameIcon').style.display = 'inline';
      document.getElementById('candleInstruction').innerText = "मोमबत्ती बुझाने के लिए केक पर टच करें! 🕯️";
      document.getElementById('envelopeView').style.display = 'block';
      document.getElementById('letterModal').style.display = 'none';
      showSlide(1);
    }

    function parseURL() {
      const p = new URLSearchParams(window.location.search);
      if(p.get('name')) config.name = p.get('name');
      if(p.get('age')) config.age = p.get('age');
      if(p.get('sender')) config.sender = p.get('sender');
      if(p.get('letter')) config.letter = decodeURIComponent(p.get('letter'));
      if(p.get('photo')) config.photo = decodeURIComponent(p.get('photo'));
      if(p.get('reasons')) config.reasons = decodeURIComponent(p.get('reasons')).split('|');
      renderDOM();
    }

    function renderDOM() {
      document.getElementById('dispTreeName').innerText = `Happy Birthday, ${config.name}`;
      document.getElementById('dispTreeAge').innerText = `and just like that, you're turning ${config.age} ✨`;
      document.getElementById('envelopeHeader').innerText = `One last thing, ${config.name}... 💌`;
      document.getElementById('sealLetter').innerText = config.name.charAt(0).toUpperCase();
      document.getElementById('letterGreeting').innerText = `Dear ${config.name},`;
      document.getElementById('letterContent').innerText = config.letter;
      document.getElementById('dispSenderName').innerText = `— With all my love, ${config.sender}`;
      document.getElementById('dispFinalName').innerText = config.name;
      if(config.photo) document.getElementById('dispPhoto').src = config.photo;
    }

    function openCustomizer() {
      document.getElementById('cfgName').value = config.name;
      document.getElementById('cfgAge').value = config.age;
      document.getElementById('cfgSender').value = config.sender;
      document.getElementById('cfgReasons').value = config.reasons.join(', ');
      document.getElementById('cfgLetter').value = config.letter;
      document.getElementById('cfgPhoto').value = config.photo;
      document.getElementById('customModal').style.display = 'flex';
    }
    function closeCustomizer() {
      document.getElementById('customModal').style.display = 'none';
    }
    function applyCustomData() {
      config.name = document.getElementById('cfgName').value.trim() || "Friend";
      config.age = document.getElementById('cfgAge').value.trim() || 20;
      config.sender = document.getElementById('cfgSender').value.trim() || "";
      const rText = document.getElementById('cfgReasons').value.trim();
      if(rText) config.reasons = rText.split(',').map(s => s.trim());
      config.letter = document.getElementById('cfgLetter').value.trim();
      config.photo = document.getElementById('cfgPhoto').value.trim();
      renderDOM();
      closeCustomizer();
    }

    function copyShareLink() {
      const p = n
