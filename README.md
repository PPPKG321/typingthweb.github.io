# typingthweb.github.io

<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>แบบทดสอบการพิมพ์ภาษาไทย</title>
  <style>
    body {
      font-family: 'Sarabun', sans-serif;
      background: #f0f0f0;
      padding: 2rem;
      text-align: center;
    }
    h1 {
      color: #0074D9;
    }
    #text-display {
      font-size: 1.2rem;
      background: #fff;
      border: 1px solid #ddd;
      padding: 1rem;
      margin: 1rem auto;
      max-width: 600px;
      border-radius: 8px;
    }
    #input-box {
      width: 80%;
      padding: 1rem;
      font-size: 1rem;
      margin-top: 1rem;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    #result, #timer {
      margin-top: 1rem;
      font-size: 1.1rem;
    }
    button {
      padding: 0.5rem 1rem;
      font-size: 1rem;
      margin-top: 1rem;
      background-color: #0074D9;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>แบบทดสอบการพิมพ์ภาษาไทย</h1>
  <div id="text-display">คำจะปรากฏที่นี่</div>
  <input type="text" id="input-box" placeholder="เริ่มพิมพ์ที่นี่..." />
  <div id="timer">เวลาที่ใช้: 0 วินาที</div>
  <div id="result"></div>
  <button onclick="startTest()">เริ่มใหม่</button>

  <script>
    const thaiWords = ["ความรัก", "ประเทศไทย", "ภาษาไทย", "เด็กดี", "ธรรมชาติ", "สุขภาพ", "ความคิด", "ครอบครัว", "การเดินทาง", "อนาคต"];
    const textDisplay = document.getElementById("text-display");
    const inputBox = document.getElementById("input-box");
    const result = document.getElementById("result");
    const timerDisplay = document.getElementById("timer");

    let startTime, intervalId;
    let currentWord = "";

    function startTest() {
      currentWord = thaiWords[Math.floor(Math.random() * thaiWords.length)];
      textDisplay.innerText = currentWord;
      inputBox.value = "";
      result.innerText = "";
      timerDisplay.innerText = "เวลาที่ใช้: 0 วินาที";
      startTime = null;
      clearInterval(intervalId);
      inputBox.focus();
    }

    inputBox.addEventListener("focus", () => {
      if (!startTime) {
        startTime = new Date();
        intervalId = setInterval(() => {
          let now = new Date();
          let elapsed = Math.floor((now - startTime) / 1000);
          timerDisplay.innerText = `เวลาที่ใช้: ${elapsed} วินาที`;
        }, 1000);
      }
    });

    inputBox.addEventListener("input", () => {
      if (inputBox.value === currentWord) {
        let endTime = new Date();
        let timeTaken = (endTime - startTime) / 1000;
        let words = currentWord.length / 5;
        let wpm = Math.round((words / timeTaken) * 60);
        result.innerText = `คุณพิมพ์ได้ ${wpm} คำต่อนาที`;
        clearInterval(intervalId);
      }
    });

    // เริ่มครั้งแรกเมื่อโหลด
    window.onload = startTest;
  </script>
</body>
</html>
