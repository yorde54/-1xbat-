<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
<title>بوت توقع الطيارة مع الاشتراك والتأكيد - 1xBat</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');

  * {
    box-sizing: border-box;
  }

  body {
    margin: 0; padding: 0;
    font-family: 'Cairo', sans-serif;
    background: linear-gradient(135deg, #0b1a2f, #182c52);
    color: #ddd;
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 100vh;
    user-select: none;
  }

  header {
    width: 100%;
    background: #102c4b;
    text-align: center;
    padding: 15px 0;
    box-shadow: 0 3px 10px #0009;
  }

  header h1 {
    margin: 0;
    font-weight: 700;
    font-size: 1.8rem;
    color: #27d07f;
    letter-spacing: 2px;
  }

  main {
    flex: 1;
    padding: 20px 15px;
    max-width: 360px;
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 15px;
    box-sizing: border-box;
    position: relative;
  }

  /* Initial Payment Info Screen */
  #initialConfirmScreen {
    background: #142f55;
    border-radius: 12px;
    padding: 20px;
    text-align: center;
    box-shadow: 0 0 20px #27d07faa inset;
  }
  #initialConfirmScreen h2 {
    color: #f4c430;
    margin: 0 0 15px 0;
    user-select: text;
  }
  #initialConfirmScreen p {
    margin: 8px 0;
    font-size: 1rem;
    user-select: text;
  }
  #phoneNumberInitial {
    font-weight: 700;
    font-size: 1.3rem;
    color: #27d07f;
    user-select: text;
    margin:12px 0;
  }
  #startToSubscriptionBtn {
    background: #27d07f;
    color: #102a17;
    font-weight: 700;
    padding: 12px 30px;
    border-radius: 25px;
    border:none;
    cursor: pointer;
    font-size: 1.1rem;
    box-shadow: 0 5px 15px #27d07fcc;
    user-select: none;
    transition: background-color 0.3s ease;
  }
  #startToSubscriptionBtn:hover {
    background: #1a8b50;
  }

  /* Subscription packages */
  #subscriptionScreen {
    background: #142f55;
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 0 20px #27d07faa inset;
    text-align: center;
    display: none;
  }

  #subscriptionScreen h2 {
    margin-top: 0;
    color: #f4c430;
    font-weight: 700;
    font-size: 1.5rem;
    margin-bottom: 12px;
    user-select: text;
  }

  .pkg-list {
    list-style: none;
    padding: 0;
    margin: 0 0 15px 0;
    display: flex;
    flex-direction: column;
    gap: 12px;
  }

  .pkg-item {
    background: #1e426f;
    border-radius: 12px;
    padding: 15px 20px;
    cursor: pointer;
    box-shadow: 0 0 10px #27d07f88;
    transition: background-color 0.3s ease;
  }

  .pkg-item:hover,
  .pkg-item.selected {
    background: #27d07f;
    color: #102a17;
    box-shadow: 0 0 20px #27d07fdd;
  }

  .pkg-item > span {
    font-weight: 700;
    font-size: 1.2rem;
    user-select: none;
  }
  .pkg-price {
    font-size: 1rem;
    margin-top: 4px;
    color: #d6d67a;
  }

  #paymentSection {
    margin-top: 15px;
    display: none;
  }
  #paymentInstructions {
    font-size: 1rem;
    user-select: text;
    color: #eee;
  }
  #phoneNumber {
    font-weight: 700;
    color: #27d07f;
    font-size: 1.3rem;
    margin: 8px 0 12px 0;
  }

  #proofInputLabel {
    background: #27d07f;
    color: #102a17;
    padding: 10px 20px;
    border-radius: 25px;
    cursor: pointer;
    display: inline-block;
    margin-bottom: 15px;
    font-weight: 700;
    user-select: none;
  }
  #proofInputLabel:hover {
    background: #1a8b50;
  }
  #proofInput {
    display: none;
  }

  #uploadedProofPreview {
    margin-top: 10px;
    max-width: 100%;
    border-radius: 8px;
    box-shadow: 0 0 10px #27d07faa inset;
    display: none;
  }

  #confirmSubscriptionBtn {
    background: #f4c430;
    border: none;
    color: #1a1210;
    font-weight: 700;
    padding: 14px 30px;
    border-radius: 25px;
    cursor: pointer;
    font-size: 1.1rem;
    box-shadow: 0 5px 15px #f4c430cc;
    user-select: none;
    transition: background-color 0.3s ease;
  }
  #confirmSubscriptionBtn:disabled {
    cursor: not-allowed;
    opacity: 0.6;
  }
  #confirmSubscriptionBtn:hover:not(:disabled) {
    background: #dbac00;
  }

  /* Hidden by default */
  #gameScreen {
    display: none;
    flex-direction: column;
    gap: 15px;
  }

  .multiplier-container {
    background: #142f55;
    border-radius: 12px;
    padding: 25px 15px;
    box-shadow: 0 0 20px #27d07faa inset;
    text-align: center;
  }

  .multiplier-label {
    font-size: 1rem;
    color: #9ee6b8;
    margin-bottom: 8px;
  }

  .multiplier-value {
    font-size: 4rem;
    font-weight: 900;
    color: #27d07f;
    text-shadow: 0 0 10px #27d07fbb;
  }

  .status-message {
    margin-top: 10px;
    font-size: 1.1rem;
    height: 30px;
    color: #eee;
  }

  .botsuggestion {
    margin-top: 8px;
    font-size: 1rem;
    color: #fff6a3;
    text-align: center;
    font-weight: 600;
    user-select: text;
  }

  .controls {
    display: flex;
    gap: 15px;
    justify-content: center;
  }

  button {
    background: #27d07f;
    border: none;
    border-radius: 25px;
    color: #102a17;
    font-weight: 700;
    font-size: 1.1rem;
    padding: 12px 30px;
    cursor: pointer;
    box-shadow: 0 5px 15px #27d07fcc;
    transition: background-color 0.3s ease;
    user-select: none;
  }

  button:disabled {
    cursor: not-allowed;
    background: #555a5a;
    box-shadow: none;
  }

  button:hover:not(:disabled) {
    background: #1a8b50;
    box-shadow: 0 5px 20px #1a8b5077;
  }

  .subscription-timer {
    background: #1e6041;
    color: #d6d67a;
    font-weight: 700;
    padding: 10px 15px;
    border-radius: 10px;
    text-align: center;
    box-shadow: 0 0 15px #d6d67a88 inset;
    font-size: 1.1rem;
    user-select: none;
  }

  .footer-note {
    color: #999;
    font-size: 0.75rem;
    text-align: center;
    padding: 10px 5px 15px;
    user-select: text;
  }

  /* Scrollbar hidden for mobile */
  ::-webkit-scrollbar {
    display: none;
  }

  /* Responsive - fit 600px height, 350px width */
  @media screen and (max-width: 375px) {
    main {
      max-width: 340px;
      padding: 15px;
      gap: 12px;
    }
    .multiplier-value {
      font-size: 3.5rem;
    }
    button {
      font-size: 1rem;
      padding: 11px 25px;
    }
  }
</style>
</head>
<body>
<header>
  <h1>بوت توقع الطيارة - الاشتراك والتأكيد</h1>
</header>
<main>

  <section id="initialConfirmScreen" aria-live="polite" aria-atomic="true">
    <h2>قبل الدخول، من فضلك أكد إجراء الإيداع</h2>
    <p>للتأكد من اشتراكك وتفعيل الدخول للبوot، يرجى إرسال رسالة على رقم فودافون التالي بعبارة:</p>
    <p><strong>"لقد قمت بالإيداع، الرجاء التفعيل"</strong></p>
    <div id="phoneNumberInitial">01551297210</div>
    <p>بعد الإرسال، اضغط على الزر أدناه للانتقال لاختيار الباقة والدفع.</p>
    <button id="startToSubscriptionBtn" aria-label="الانتقال لاختيار باقة الاشتراك">اذهب لاختيار الباقة والدفع</button>
  </section>

  <section id="subscriptionScreen" aria-live="polite" aria-atomic="true" tabindex="0" aria-label="شاشة اختيار باقة الاشتراك">
    <h2>اختر باقة الاشتراك بالساعات</h2>
    <ul class="pkg-list" role="list">
      <li class="pkg-item" tabindex="0" data-hours="3" data-price="150" aria-label="اشتراك 3 ساعات بسعر 150 جنيه">
        <span>3 ساعات</span>
        <div class="pkg-price">150 جنيه</div>
      </li>
      <li class="pkg-item" tabindex="0" data-hours="5" data-price="300" aria-label="اشتراك 5 ساعات بسعر 300 جنيه">
        <span>5 ساعات</span>
        <div class="pkg-price">300 جنيه</div>
      </li>
      <li class="pkg-item" tabindex="0" data-hours="10" data-price="450" aria-label="اشتراك 10 ساعات بسعر 450 جنيه">
        <span>10 ساعات</span>
        <div class="pkg-price">450 جنيه</div>
      </li>
      <li class="pkg-item" tabindex="0" data-hours="24" data-price="2300" aria-label="اشتراك 24 ساعة بسعر 2300 جنيه">
        <span>24 ساعة</span>
        <div class="pkg-price">2300 جنيه</div>
      </li>
      <li class="pkg-item" tabindex="0" data-hours="100" data-price="5000" aria-label="اشتراك 100 ساعة بسعر 5000 جنيه">
        <span>100 ساعة</span>
        <div class="pkg-price">5000 جنيه</div>
      </li>
    </ul>

    <div id="paymentSection" style="display:none;">
      <p id="paymentInstructions">يرجى إرسال المبلغ المختار إلى رقم فودافون:</p>
      <div id="phoneNumber">01551297210</div>
      <p>بعد الدفع، يرجى رفع صورة إثبات الدفع باستخدام الزر أدناه</p>
      <label for="proofInput" id="proofInputLabel" tabindex="0" aria-label="رفع صورة إثبات الدفع">رفع صورة إثبات الدفع</label>
      <input type="file" id="proofInput" accept="image/*" aria-describedby="proofDescription" />
      <img id="uploadedProofPreview" aria-hidden="true" alt="معاينة صورة إثبات الدفع" />
      <button id="confirmSubscriptionBtn" disabled aria-disabled="true" aria-label="تأكيد الاشتراك">تأكيد الاشتراك</button>
    </div>
  </section>

  <section id="gameScreen" aria-live="polite" aria-atomic="true" tabindex="0" aria-label="شاشة لعبة توقع الطيارة">
    <div class="subscription-timer" aria-live="polite" aria-atomic="true" id="subscriptionTimer" aria-label="الوقت المتبقي للاشتراك">
      لم يتم الاشتراك بعد
    </div>

    <div class="multiplier-container" role="region" aria-live="polite" aria-atomic="true">
      <div class="multiplier-label">المضاعف الحالي</div>
      <div id="multiplier" class="multiplier-value">1.00x</div>
      <div class="status-message" id="statusMessage">اضغط "ابدأ" لبدء اللعبة</div>
      <div class="botsuggestion" id="botSuggestion"></div>
    </div>

    <div class="controls">
      <button id="startBtn" aria-label="بدء الجولة" disabled>ابدأ</button>
      <button id="stopBtn" aria-label="توقف" disabled>توقف</button>
    </div>
  </section>
</main>

<div class="footer-note">
  نسخة تجريبية لمحاكاة "طياره" فقط. لا تستخدم أموال حقيقية.
</div>

<script>
  (function(){
    // Initial screens and buttons
    const initialConfirmScreen = document.getElementById('initialConfirmScreen');
    const startToSubscriptionBtn = document.getElementById('startToSubscriptionBtn');
    const subscriptionScreen = document.getElementById('subscriptionScreen');
    const paymentSection = document.getElementById('paymentSection');
    const proofInput = document.getElementById('proofInput');
    const uploadedProofPreview = document.getElementById('uploadedProofPreview');
    const confirmSubscriptionBtn = document.getElementById('confirmSubscriptionBtn');
    const gameScreen = document.getElementById('gameScreen');

    // Game elements
    const multiplierSpan = document.getElementById('multiplier');
    const statusMessage = document.getElementById('statusMessage');
    const botSuggestion = document.getElementById('botSuggestion');
    const startBtn = document.getElementById('startBtn');
    const stopBtn = document.getElementById('stopBtn');
    const subscriptionTimer = document.getElementById('subscriptionTimer');

    // Subscription related
    const pkgItems = [...document.querySelectorAll('.pkg-item')];
    let selectedPackage = null;
    let proofUploaded = false;
    let subscriptionEnd = null;
    let subscriptionTimerInterval = null;

    // Game state
    let gameRunning = false;
    let multiplier = 1.00;
    let crashPoint = 0;
    let animationFrameId = null;
    let startTime = 0;
    let cashedOut = false;

    // Prevent access to game or subscription without initial confirmation
    let initialConfirmed = false;

    // Show subscription screen after initial confirm
    startToSubscriptionBtn.addEventListener('click', () => {
      initialConfirmed = true;
      initialConfirmScreen.style.display = 'none';
      subscriptionScreen.style.display = 'block';
    });

    // Package selection 
    pkgItems.forEach(item => {
      item.addEventListener('click', () => {
        pkgItems.forEach(i => i.classList.remove('selected'));
        item.classList.add('selected');
        selectedPackage = {
          hours: Number(item.getAttribute('data-hours')),
          price: Number(item.getAttribute('data-price'))
        };
        paymentSection.style.display = 'block';
        proofInput.value = '';
        uploadedProofPreview.style.display = 'none';
        confirmSubscriptionBtn.disabled = true;
        confirmSubscriptionBtn.setAttribute('aria-disabled', 'true');
        proofUploaded = false;
      });
      item.addEventListener('keydown', e => {
        if (e.key === "Enter" || e.key === " ") {
          e.preventDefault();
          item.click();
        }
      });
    });

    // Proof upload handling
    proofInput.addEventListener('change', function(event){
      const file = event.target.files[0];
      if (file && file.type.startsWith('image/')) {
        const reader = new FileReader();
        reader.onload = function(e) {
          uploadedProofPreview.src = e.target.result;
          uploadedProofPreview.style.display = 'block';
          confirmSubscriptionBtn.disabled = false;
          confirmSubscriptionBtn.setAttribute('aria-disabled', 'false');
          proofUploaded = true;
        }
        reader.readAsDataURL(file);
      } else {
        uploadedProofPreview.style.display = 'none';
        confirmSubscriptionBtn.disabled = true;
        confirmSubscriptionBtn.setAttribute('aria-disabled', 'true');
        proofUploaded = false;
      }
    });

    confirmSubscriptionBtn.addEventListener('click', () => {
      if (!proofUploaded) return;
      if (!selectedPackage) {
        alert("يرجى اختيار باقة اشتراك أولاً");
        return;
      }
      confirmSubscriptionBtn.disabled = true;
      confirmSubscriptionBtn.textContent = 'جار التحقق...';

      // Simulate server verification delay + activate subscription
      setTimeout(() => {
        let now = new Date();
        if (subscriptionEnd && subscriptionEnd > now) {
          subscriptionEnd = new Date(subscriptionEnd.getTime() + selectedPackage.hours * 3600 * 1000);
        } else {
          subscriptionEnd = new Date(now.getTime() + selectedPackage.hours * 3600 * 1000);
        }

        confirmSubscriptionBtn.textContent = 'تم التأكيد! الاشتراك مفعل';
        subscriptionScreen.style.display = 'none';
        gameScreen.style.display = 'flex';
        startBtn.disabled = false;
        stopBtn.disabled = true;

        paymentSection.style.display = 'none';
        proofInput.value = '';
        uploadedProofPreview.style.display = 'none';
        pkgItems.forEach(i => i.classList.remove('selected'));
        selectedPackage = null;
        proofUploaded = false;
        updateSubscriptionTimer();

        if (subscriptionTimerInterval) clearInterval(subscriptionTimerInterval);
        subscriptionTimerInterval = setInterval(updateSubscriptionTimer, 1000);
      }, 2500);
    });

    // Subscription timer update
    function updateSubscriptionTimer() {
      if (!subscriptionEnd) {
        subscriptionTimer.textContent = "لم يتم الاشتراك بعد";
        disableGameControls();
        return false;
      }
      let now = new Date();
      let diffMs = subscriptionEnd - now;
      if (diffMs <= 0) {
        subscriptionTimer.textContent = "انتهى الاشتراك";
        subscriptionEnd = null;
        disableGameControls();
        alert("انتهى اشتراكك، يرجى التجديد للعب.");
        subscriptionScreen.style.display = 'block';
        gameScreen.style.display = 'none';
        return false;
      }
      let diffSec = Math.floor(diffMs / 1000);
      let h = Math.floor(diffSec / 3600);
      let m = Math.floor((diffSec % 3600) / 60);
      let s = diffSec % 60;
      subscriptionTimer.textContent = `الوقت المتبقي في الاشتراك: ${h} ساعة ${m} دقيقة ${s} ثانية`;
      enableGameControls();
      return true;
    }

    // Enable / Disable game controls
    function disableGameControls() {
      startBtn.disabled = true;
      stopBtn.disabled = true;
    }
    function enableGameControls() {
      if (!gameRunning) startBtn.disabled = false;
      stopBtn.disabled = gameRunning;
    }

    // Game functions
    function pickCrashPoint() {
      let r = Math.random();
      let crash = Math.floor((1 / r) * 100) / 100;
      if (crash < 1) crash = 1;
      if (crash > 10) crash = 10;
      return crash;
    }

    function updateMultiplier(timestamp) {
      if (!startTime) startTime = timestamp;
      let elapsed = (timestamp - startTime) / 1000;
      multiplier = 1 + Math.pow(1.15, elapsed);
      multiplierSpan.textContent = multiplier.toFixed(2) + 'x';

      if (multiplier >= crashPoint) {
        multiplierSpan.textContent = crashPoint.toFixed(2) + 'x';
        statusMessage.textContent = "انتهت الجولة: الطيارة انفجرت عند " + crashPoint.toFixed(2) + "x.";
        gameRunning = false;
        startBtn.disabled = false;
        stopBtn.disabled = true;
        cancelAnimationFrame(animationFrameId);
      } else {
        animationFrameId = requestAnimationFrame(updateMultiplier);
      }
    }

    function startGame() {
      if (!initialConfirmed) {
        alert("يرجى تأكيد الإيداع والانتقال لاختيار الاشتراك أولاً.");
        return;
      }
      if (!updateSubscriptionTimer()) return;
      gameRunning = true;
      multiplier = 1.00;
      startTime = 0;
      cashedOut = false;
      crashPoint = pickCrashPoint();
      multiplierSpan.textContent = multiplier.toFixed(2) + 'x';
      statusMessage.textContent = "الطيارة تقلع...";
      botSuggestion.textContent = "البوت يتوقع أن الطيارة ستضرب عند: " + crashPoint.toFixed(2) + "x";
      startBtn.disabled = true;
      stopBtn.disabled = false;
      animationFrameId = requestAnimationFrame(updateMultiplier);
    }

    function stopGame() {
      if (!gameRunning || cashedOut) return;
      cashedOut = true;
      gameRunning = false;
      cancelAnimationFrame(animationFrameId);
      statusMessage.textContent = "توقفت عند المضاعف " + multiplier.toFixed(2) + "x. توقع ناجح!";
      startBtn.disabled = false;
      stopBtn.disabled = true;
    }

    // Attach event listeners
    startBtn.addEventListener('click', startGame);
    stopBtn.addEventListener('click', stopGame);

    // Initialize UI states
    subscriptionScreen.style.display = 'none';
    gameScreen.style.display = 'none';
  })();
</script>
</body>
</html>
