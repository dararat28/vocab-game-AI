<Funny game>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <title>เกมจับคู่คำศัพท์</title>
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-NDDPMMML');</script>
<!-- End Google Tag Manager -->
</script>
  <style>
    body { font-family: 'Sarabun', sans-serif; padding: 20px; background: #f0f0f0; }
    h1 { color: #333; }
    #progress-container {
      width: 100%;
      background-color: #ddd;
      border-radius: 12px;
      overflow: hidden;
      margin-bottom: 20px;
      height: 20px;
      box-shadow: inset 0 1px 3px rgba(0,0,0,.2);
    }
    #progress-bar {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, #4caf50, #81c784);
      transition: width 0.5s ease;
    }
    #timer, #score { font-size: 20px; margin: 10px 0; }
    #message { font-size: 22px; color: crimson; margin-top: 5px; min-height: 30px;}
    .container { display: flex; justify-content: space-between; gap: 10px; flex-wrap: wrap; }
    .column {
      width: 45%;
      background: #fff;
      padding: 10px;
      border-radius: 8px;
      min-height: 400px;
    }
    .card {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100px;
      margin: 5px;
      padding: 8px;
      background: #e0e0e0;
      border-radius: 6px;
      cursor: pointer;
      text-align: center;
      font-size: 18px;
      box-sizing: border-box;
      user-select: none;
      opacity: 1;
      transition: opacity 1s ease;
    }
    .card.correct { background: #a5d6a7 !important; cursor: default; }
    .card.wrong { background: #ef9a9a !important; }
    .card.selected { background: #90caf9 !important; }
    img.icon { width: 50px; height: 50px; margin-bottom: 5px; }
    button {
      padding: 8px 16px;
      font-size: 16px;
      cursor: pointer;
      margin-right: 10px;
    }
    .controls {
      margin-bottom: 15px;
    }
    /* หน้าเลือกหมวดคำศัพท์ */
    #categorySelection {
      max-width: 800px;
      margin: 50px auto;
      text-align: center;
      display: grid;
      grid-template-columns: repeat(auto-fit,minmax(180px,1fr));
      gap: 20px;
    }
    #categorySelection button {
      width: 180px;
      padding: 10px;
      font-size: 18px;
      border-radius: 12px;
      border: none;
      cursor: pointer;
      transition: background-color 0.3s ease;
      color: white;
      user-select: none;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }
    #categorySelection button:hover {
      opacity: 0.85;
    }
    #categorySelection button img {
      width: 70px;
      height: 70px;
      margin-bottom: 10px;
      border-radius: 10px;
      object-fit: contain;
    }
    #categorySelection button.color { background-color: #f44336; }
    #categorySelection button.day { background-color: #2196f3; }
    #categorySelection button.animal { background-color: #4caf50; }
    #categorySelection button.number { background-color: #ff9800; }
    #categorySelection button.month { background-color: #9c27b0; }
    #categorySelection button.job { background-color: #607d8b; }

    /* ซ่อนส่วนเกมตอนเลือกหมวด */
    #gameArea { display: none; }
  </style>
</head>
<body>

  <!-- หน้าเลือกหมวดคำศัพท์ -->
  <div id="categorySelection">
    <h1>เลือกหมวดคำศัพท์</h1>

    <button class="color" onclick="selectCategory('color')">
      <img src="https://img.icons8.com/color/96/000000/paint-palette.png" alt="สี" />
      หมวดสี
    </button>

    <button class="day" onclick="selectCategory('day')">
      <img src="https://img.icons8.com/color/96/000000/calendar.png" alt="วัน" />
      หมวดวัน
    </button>

    <button class="animal" onclick="selectCategory('animal')">
      <img src="https://img.icons8.com/color/96/000000/cat.png" alt="สัตว์" />
      หมวดสัตว์
    </button>

    <button class="number" onclick="selectCategory('number')">
      <img src="https://img.icons8.com/?size=100&id=54526&format=png&color=000000" alt="ตัวเลข" />
      หมวดตัวเลข
    </button>

    <button class="month" onclick="selectCategory('month')">
      <img src="https://img.icons8.com/?size=100&id=7724&format=png&color=FD7E14" alt="เดือน" />
      หมวดเดือน
    </button>

    <button class="job" onclick="selectCategory('job')">
      <img src="https://img.icons8.com/color/96/000000/briefcase.png" alt="อาชีพ" />
      หมวดอาชีพ
    </button>

    <button class="Dailyitems" onclick="selectCategory('Dailyitems')">
      <img src="https://img.icons8.com/?size=100&id=9YMO8fBl5NCr&format=png&color=000000" alt="ของใช้ประจำวัน" />
      หมวดของใช้ประจำวัน
    </button>
  </div>

  <!-- หน้าเกมจับคู่คำศัพท์ -->
  <div id="gameArea">
    <h1>📚 เกมจับคู่คำศัพท์</h1>

    <div id="progress-container">
      <div id="progress-bar"></div>
    </div>

    <div id="timer">เวลา: 60 วินาที</div>
    <div id="score">คะแนน: 0</div>
    <div class="controls">
      <button onclick="startGame()">🔁 เล่นใหม่</button>
      <button onclick="togglePause()" id="pauseBtn">⏸️ พัก</button>
      <button onclick="exitGame()" style="background:#f44336; color:white;">⬅️ ออก</button>
    </div>
    <div id="message"></div>
    <div class="container">
      <div class="column" id="englishColumn"></div>
      <div class="column" id="thaiColumn"></div>
    </div>
  </div>

<script>
  // คำศัพท์แบ่งหมวด พร้อมรูปประกอบ
  const vocabularyByCategory = {
    color: [
      {en:"red", th:"สีแดง", img:"https://img.icons8.com/?size=100&id=24801&format=png&color=FA5252"},
      {en:"blue", th:"สีน้ำเงิน", img:"https://img.icons8.com/?size=100&id=24801&format=png&color=228BE6"},
      {en:"green", th:"สีเขียว", img:"https://img.icons8.com/?size=100&id=24801&format=png&color=40C057"},
      {en:"yellow", th:"สีเหลือง", img:"https://img.icons8.com/?size=100&id=24801&format=png&color=FAB005"},
      {en:"black", th:"สีดำ", img:"https://img.icons8.com/?size=100&id=24801&format=png&color=1A1A1A"},
      {en:"Brown", th:"สีน้ำตาล", img:"https://img.icons8.com/?size=100&id=24801&format=png&color=a52a2a"},
      {en:"Gray", th:"สีเทา", img:"https://img.icons8.com/?size=100&id=24801&format=png&color=808080"},
      {en:"Purple", th:"สีม่วง", img:"https://img.icons8.com/?size=100&id=24801&format=png&color=800080"},
      {en:"Orange", th:"สีส้ม", img:"https://img.icons8.com/?size=100&id=24801&format=png&color=ffa500"},
      {en:"Pink", th:"สีชมพู", img:"https://img.icons8.com/?size=100&id=24801&format=png&color=ff69b4"},
      {en:"white", th:"สีขาว", img:"https://img.icons8.com/?size=100&id=24801&format=png&color=FFFFFF"}
    ],
    day: [
      {en:"Monday", th:"วันจันทร์", img:"https://img.icons8.com/color/96/000000/monday.png"},
      {en:"Tuesday", th:"วันอังคาร", img:"https://img.icons8.com/color/96/000000/tuesday.png"},
      {en:"Wednesday", th:"วันพุธ", img:"https://img.icons8.com/color/96/000000/wednesday.png"},
      {en:"Thursday", th:"วันพฤหัสบดี", img:"https://img.icons8.com/color/96/000000/thursday.png"},
      {en:"Friday", th:"วันศุกร์", img:"https://img.icons8.com/color/96/000000/friday.png"},
      {en:"Saturday", th:"วันเสาร์", img:"https://img.icons8.com/color/96/000000/saturday.png"},
      {en:"Sunday", th:"วันอาทิตย์", img:"https://img.icons8.com/color/96/000000/sunday.png"}
    ],
    animal: [
      {en:"dog", th:"สุนัข", img:"https://img.icons8.com/color/96/000000/dog.png"},
      {en:"cat", th:"แมว", img:"https://img.icons8.com/color/96/000000/cat.png"},
      {en:"bird", th:"นก", img:"https://img.icons8.com/color/96/000000/bird.png"},
      {en:"fish", th:"ปลา", img:"https://img.icons8.com/color/96/000000/fish.png"},
      {en:"elephant", th:"ช้าง", img:"https://img.icons8.com/color/96/000000/elephant.png"},
      {en:"tiger", th:"เสือ", img:"https://img.icons8.com/color/96/000000/tiger.png"}
    ],
    number: [
      {en:"one", th:"หนึ่ง", img:"https://img.icons8.com/color/96/000000/1-circle.png"},
      {en:"two", th:"สอง", img:"https://img.icons8.com/color/96/000000/2-circle.png"},
      {en:"three", th:"สาม", img:"https://img.icons8.com/color/96/000000/3-circle.png"},
      {en:"four", th:"สี่", img:"https://img.icons8.com/color/96/000000/4-circle.png"},
      {en:"five", th:"ห้า", img:"https://img.icons8.com/color/96/000000/5-circle.png"},
      {en:"six", th:"หก", img:"https://img.icons8.com/color/96/000000/6-circle.png"}
    ],
    month: [
      {en:"January", th:"มกราคม", img:"https://img.icons8.com/color/96/000000/january.png"},
      {en:"February", th:"กุมภาพันธ์", img:"https://img.icons8.com/color/96/000000/february.png"},
      {en:"March", th:"มีนาคม", img:"https://img.icons8.com/color/96/000000/march.png"},
      {en:"April", th:"เมษายน", img:"https://img.icons8.com/color/96/000000/april.png"},
      {en:"May", th:"พฤษภาคม", img:"https://img.icons8.com/color/96/000000/may.png"},
      {en:"June", th:"มิถุนายน", img:"https://img.icons8.com/color/96/000000/june.png"},
      {en:"July", th:"กรกฎาคม", img:"https://img.icons8.com/color/96/000000/july.png"},
      {en:"August", th:"สิงหาคม", img:"https://img.icons8.com/color/96/000000/august.png"},
      {en:"September", th:"กันยายน", img:"https://img.icons8.com/color/96/000000/september.png"},
      {en:"October", th:"ตุลาคม", img:"https://img.icons8.com/color/96/000000/october.png"},
      {en:"November", th:"พฤศจิกายน", img:"https://img.icons8.com/color/96/000000/november.png"},
      {en:"December", th:"ธันวาคม", img:"https://img.icons8.com/color/96/000000/december.png"}
    ],
    job: [
      {en:"doctor", th:"หมอ", img:"https://img.icons8.com/color/96/000000/doctor-male.png"},
      {en:"teacher", th:"ครู", img:"https://img.icons8.com/color/96/000000/teacher.png"},
      {en:"engineer", th:"วิศวกร", img:"https://img.icons8.com/color/96/000000/engineer.png"},
      {en:"police", th:"ตำรวจ", img:"https://img.icons8.com/?size=100&id=23311&format=png&color=000000"},
      {en:"chef", th:"พ่อครัว", img:"https://img.icons8.com/color/96/000000/chef-hat.png"},
      {en:"Nurse", th:"พยาบาล", img:"https://img.icons8.com/?size=100&id=23303&format=png&color=000000"},
      {en:"Architect", th:"สถาปนิก", img:"https://img.icons8.com/?size=100&id=wvDZbOqaJ5xa&format=png&color=000000"},
      {en:"Firefighter", th:"นักดับเพลิง", img:"https://img.icons8.com/?size=100&id=AxzqSDqBZTtk&format=png&color=000000"},
      {en:"Driver", th:"คนขับรถ", img:"https://img.icons8.com/?size=100&id=15127&format=png&color=000000"},
      {en:"Pilot", th:"นักบิน", img:"https://img.icons8.com/?size=100&id=6kMO9OR3DURb&format=png&color=000000"},
      {en:"Hairdresser", th:"ช่างทำผม", img:"https://img.icons8.com/?size=100&id=qGrhqZVFf9Lv&format=png&color=000000"},
      {en:"Artist", th:"ศิลปิน", img:"https://img.icons8.com/?size=100&id=bQsb7zpH7aip&format=png&color=000000"},
      {en:"Musician", th:"นักดนตรี", img:"https://img.icons8.com/?size=100&id=bQsb7zpH7aip&format=png&color=000000"},
      {en:"Office worker", th:"พนักงานออฟฟิศ", img:"https://img.icons8.com/?size=100&id=12313&format=png&color=000000"},
      {en:"Scientist", th:"นักวิทยาศาสตร์", img:"https://img.icons8.com/?size=100&id=axF5ww-Dydb8&format=png&color=000000"},
      {en:"Lawyer", th:"ทนายความ", img:"https://img.icons8.com/?size=100&id=gzPnHDuFZxQe&format=png&color=000000"},
      {en:"Accountant", th:"นักบัญชี", img:"https://img.icons8.com/?size=100&id=W9yu3iQzV6yb&format=png&color=000000"},
      {en:"Programmer", th:"โปรแกรมเมอร์", img:"https://img.icons8.com/?size=100&id=UF--CfaVggaW&format=png&color=000000"},
      {en:"farmer", th:"ชาวนา", img:"https://img.icons8.com/?size=100&id=7Nv2j8eVXfbQ&format=png&color=000000"}
    ],
    Dailyitems: [
      {en:"Chair", th:"เก้าอี้", img:"https://img.icons8.com/?size=100&id=26126&format=png&color=000000"},
      {en:"Table", th:"โต๊ะ", img:"https://img.icons8.com/?size=100&id=12841&format=png&color=000000"},
      {en:"Bed", th:"เตียงนอน", img:"https://img.icons8.com/?size=100&id=tBfPbOPEAOl5&format=png&color=000000"},
      {en:"Pillow", th:"หมอน", img:"https://img.icons8.com/?size=100&id=WNbFmwUYKJUk&format=png&color=000000"},
      {en:"Towel", th:"ผ้าขนหนู", img:"https://img.icons8.com/?size=100&id=65870&format=png&color=000000"},
      {en:"Mirror", th:"กระจก", img:"https://img.icons8.com/?size=100&id=vhClVTMTuM-7&format=png&color=000000"},
      {en:"Clock", th:"นาฬิกา", img:"https://img.icons8.com/?size=100&id=PDgJoygWSQQF&format=png&color=000000"},
      {en:"Television", th:"โทรทัศน์", img:"https://img.icons8.com/?size=100&id=hR36FNBgrSwz&format=png&color=000000"},
      {en:"Fan", th:"พัดลม", img:"https://img.icons8.com/?size=100&id=4ayVrb75leay&format=png&color=000000"},
      {en:"Air conditioner", th:"เครื่องปรับอากาศ", img:"https://img.icons8.com/?size=100&id=12384&format=png&color=000000"},
      {en:"Refrigerator", th:"ตู้เย็น", img:"https://img.icons8.com/?size=100&id=12822&format=png&color=000000"},
      {en:"Microwave", th:"ไมโครเวฟ", img:"https://img.icons8.com/?size=100&id=66304&format=png&color=000000"},
      {en:"Washing machine", th:"เครื่องซักผ้า", img:"https://img.icons8.com/?size=100&id=f6dhmPnk2Nsj&format=png&color=000000"},
      {en:"Lamp", th:"โคมไฟ", img:"https://img.icons8.com/?size=100&id=80486&format=png&color=000000"},
      {en:"Toothbrush", th:"แปรงสีฟัน", img:"https://img.icons8.com/?size=100&id=80486&format=png&color=000000"},
      {en:"Toothpaste", th:"ยาสีฟัน", img:"https://img.icons8.com/?size=100&id=QMRWchOPLiSf&format=png&color=000000"},
      {en:"Soap", th:"สบู่", img:"https://img.icons8.com/?size=100&id=7HbRucZ6zhMo&format=png&color=000000"},
      {en:"Shampoo", th:"แชมพู", img:"https://img.icons8.com/?size=100&id=6FNF24Ite4FM&format=png&color=000000"},
      {en:"Bag", th:"กระเป๋า", img:"https://img.icons8.com/?size=100&id=vv0bEW7EQ0G9&format=png&color=000000"},
      {en:"Pen", th:"ปากกา", img:"https://img.icons8.com/?size=100&id=Vk1hVre0P58T&format=png&color=000000"},
      {en:"Notebook", th:"สมุด", img:"https://img.icons8.com/?size=100&id=B3ueFHOl3rWJ&format=png&color=000000"},
      {en:"Scissors", th:"กรรไกร", img:"https://img.icons8.com/?size=100&id=51850&format=png&color=000000"},
      {en:"Broom", th:"ไม้กวาด", img:"https://img.icons8.com/?size=100&id=LXsgrpCUK59c&format=png&color=000000"},
      {en:"Bucket", th:"ถังน้ำ", img:"https://img.icons8.com/?size=100&id=81378&format=png&color=000000"},
      {en:"Comb", th:"หวี", img:"https://img.icons8.com/?size=100&id=65853&format=png&color=000000"}
    ]
  };

  let selectedCategory = null;
  let vocabulary = [];
  let selected = [];
  let matchDict = [];
  let used = [];
  let timeLeft = 60;
  let timerInterval = null;
  let gameOver = false;
  let score = 0;
  let paused = false;
  const maxScore = 100; // คะแนนเต็มสำหรับ progress bar

  function selectCategory(cat){
    selectedCategory = cat;
    vocabulary = vocabularyByCategory[cat];
    document.getElementById("categorySelection").style.display = "none";
    document.getElementById("gameArea").style.display = "block";
    startGame();
  }

  function exitGame(){
    // หยุดเวลาและรีเซ็ตสถานะ
    clearInterval(timerInterval);
    gameOver = true;
    paused = false;
    score = 0;
    selectedCategory = null;
    vocabulary = [];
    selected = [];
    matchDict = [];
    used = [];

    // ซ่อนเกม และแสดงหน้าเลือกหมวด
    document.getElementById("gameArea").style.display = "none";
    document.getElementById("categorySelection").style.display = "block";

    // ล้างข้อความสถานะ
    document.getElementById("message").textContent = "";
  }

  function shuffle(arr) {
    return arr.slice().sort(() => Math.random() - 0.5);
  }

  function startGame(){
    selected = [];
    matchDict = [];
    used = [];
    gameOver = false;
    score = 0;
    paused = false;
    clearInterval(timerInterval);
    timeLeft = 60;

    updateProgressBar();

    document.getElementById("pauseBtn").textContent = "⏸️ พัก";
    document.getElementById("score").textContent = "คะแนน: 0";
    document.getElementById("message").textContent = "";
    document.getElementById("timer").textContent = `เวลา: ${timeLeft} วินาที`;

    timerInterval = setInterval(updateTimer, 1000);
    loadInitialPairs();
  }

  function togglePause(){
    if(gameOver) return;
    paused = !paused;
    document.getElementById("pauseBtn").textContent = paused ? "▶️ เล่นต่อ" : "⏸️ พัก";
  }

  function updateTimer(){
    if (paused || gameOver) return;
    timeLeft--;
    document.getElementById("timer").textContent = `เวลา: ${timeLeft} วินาที`;
    if(timeLeft <= 0){
      clearInterval(timerInterval);
      gameOver = true;
      document.getElementById("message").textContent = "⏰ หมดเวลาแล้ว!";
    }
  }

  function loadInitialPairs(){
    const initial = shuffle(vocabulary).slice(0, 5);
    used = initial.map(i => i.en);
    matchDict = [...initial];

    const enCol = document.getElementById("englishColumn");
    const thCol = document.getElementById("thaiColumn");
    enCol.innerHTML = "";
    thCol.innerHTML = "";

    const enList = shuffle(initial);
    const thList = shuffle(initial);

    enList.forEach(item => addCard(item, 'en'));
    thList.forEach(item => addCard(item, 'th'));
  }

  function addCard(item, type) {
    const col = document.getElementById(type === 'en' ? 'englishColumn' : 'thaiColumn');
    const d = document.createElement("div");
    d.className = "card";
    if (type === 'en') {
      d.textContent = item.en;
      d.onclick = () => handleSelect(d, item.en, "en");
      d.dataset.val = item.en;
    } else {
      d.innerHTML = `<img src="${item.img}" class="icon"><div>${item.th}</div>`;
      d.onclick = () => handleSelect(d, item.th, "th");
      d.dataset.val = item.th;
    }
    d.dataset.type = type;
    col.appendChild(d);
    return d;
  }

  function handleSelect(el, val, type){
    if(gameOver || paused || el.classList.contains("correct")) return;

    if(selected.some(s => s.el === el)) return;

    if(selected.length === 1){
      const first = selected[0];
      if(first.type === type){
        document.querySelectorAll(".card").forEach(c => c.classList.remove("selected"));
        selected = [];
        el.classList.add("selected");
        selected.push({el, val, type});
        return;
      }
    }

    el.classList.add("selected");
    selected.push({el, val, type});

    if(selected.length === 2){
      const [a, b] = selected;
      const isMatch = matchDict.some(p =>
        (p.en === a.val && p.th === b.val) ||
        (p.en === b.val && p.th === a.val)
      );

      if(isMatch){
        a.el.classList.add("correct");
        b.el.classList.add("correct");
        document.getElementById("message").textContent = "🎉 เก่งมาก!";

        setTimeout(() => {
          let enWord = (a.type === 'en') ? a.val : b.val;

          matchDict = matchDict.filter(item => item.en !== enWord);
          used = used.filter(u => u !== enWord);

          replaceCardWithNewWord(a.el, b.el);

          score += 10;
          document.getElementById("score").textContent = `คะแนน: ${score}`;
          updateProgressBar();
          document.getElementById("message").textContent = "";

        }, 1000);
      } else {
        document.getElementById("message").textContent = "❌ ผิดแล้ว ลองใหม่!";
        a.el.classList.add("wrong");
        b.el.classList.add("wrong");
        setTimeout(() => {
          a.el.classList.remove("wrong", "selected");
          b.el.classList.remove("wrong", "selected");
          document.getElementById("message").textContent = "";
        }, 800);
      }
      selected = [];
    }
  }

  function replaceCardWithNewWord(enCard, thCard){
    const remaining = vocabulary.filter(v => !used.includes(v.en));
    if(remaining.length === 0){
      enCard.remove();
      thCard.remove();
      return;
    }
    const newItem = shuffle(remaining)[0];
    used.push(newItem.en);
    matchDict.push(newItem);

    enCard.style.opacity = 0;
    thCard.style.opacity = 0;

    setTimeout(() => {
      enCard.textContent = newItem.en;
      enCard.classList.remove("correct", "selected", "wrong");
      enCard.dataset.val = newItem.en;
      enCard.onclick = () => handleSelect(enCard, newItem.en, "en");

      thCard.innerHTML = `<img src="${newItem.img}" class="icon"><div>${newItem.th}</div>`;
      thCard.classList.remove("correct", "selected", "wrong");
      thCard.dataset.val = newItem.th;
      thCard.onclick = () => handleSelect(thCard, newItem.th, "th");

      enCard.style.transition = "opacity 1s ease";
      thCard.style.transition = "opacity 1s ease";
      enCard.style.opacity = 1;
      thCard.style.opacity = 1;
    }, 1000);
  }

  function updateProgressBar() {
    const progressPercent = Math.min((score / maxScore) * 100, 100);
    const progressBar = document.getElementById("progress-bar");
    progressBar.style.width = progressPercent + "%";
  }
</script>
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-NDDPMMML"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
</body>
</html>
