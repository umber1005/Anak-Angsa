<!DOCTYPE html>
<html>
<head>
  <title>Petualangan Gigi Si Angsa</title>
  <style>
    body { margin: 0; overflow: hidden; background-color: #cceeff; font-family: sans-serif; }
    canvas { display: block; margin: 0 auto; background: #a3d9ff; }
    #questionBox {
      display: none;
      position: absolute;
      top: 30%;
      left: 50%;
      transform: translateX(-50%);
      background: white;
      padding: 20px;
      border: 2px solid #333;
      border-radius: 10px;
      text-align: center;
    }
    button { margin-top: 10px; }
  </style>
</head>
<body>
<canvas id="gameCanvas" width="800" height="400"></canvas>
<div id="questionBox">
  <p id="questionText">Apa yang harus Gigi lakukan?</p>
  <button onclick="answer(true)">Mendengarkan nasihat</button>
  <button onclick="answer(false)">Pergi sendiri saja</button>
</div>
<script>
  const canvas = document.getElementById("gameCanvas");
  const ctx = canvas.getContext("2d");

  const gigi = { x: 50, y: 300, width: 40, height: 40, color: "white" };
  const mud = { x: 300, y: 320, width: 80, height: 30, color: "brown" };
  const home = { x: 750, y: 300, width: 40, height: 40, color: "yellow" };

  let gameOver = false;
  let questionShown = false;

  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    
    // Gigi
    ctx.fillStyle = gigi.color;
    ctx.beginPath();
    ctx.arc(gigi.x, gigi.y, 20, 0, Math.PI * 2);
    ctx.fill();

    // Tanah
    ctx.fillStyle = "#228B22";
    ctx.fillRect(0, 340, canvas.width, 60);

    // Lumpur
    ctx.fillStyle = mud.color;
    ctx.fillRect(mud.x, mud.y, mud.width, mud.height);

    // Rumah
    ctx.fillStyle = home.color;
    ctx.fillRect(home.x, home.y, home.width, home.height);
  }

  function update() {
    if (checkCollision(gigi, mud)) {
      alert("Gigi terjatuh ke lumpur! Coba lagi ya.");
      gigi.x = 50;
    }

    if (checkCollision(gigi, home) && !questionShown) {
      showQuestion();
      questionShown = true;
    }
  }

  function checkCollision(a, b) {
    return a.x < b.x + b.width &&
           a.x + a.width > b.x &&
           a.y < b.y + b.height &&
           a.y + a.height > b.y;
  }

  function showQuestion() {
    document.getElementById("questionBox").style.display = "block";
  }

  function answer(isCorrect) {
    if (isCorrect) {
      alert("Benar! Gigi harus mendengarkan nasihat.");
      location.reload(); // Lanjut ke level berikutnya (bisa ganti jadi level2.html)
    } else {
      alert("Ups, salah. Yuk coba lagi!");
      location.reload();
    }
  }

  document.addEventListener("keydown", (e) => {
    if (gameOver) return;
    if (e.key === "ArrowRight") gigi.x += 10;
    if (e.key === "ArrowLeft") gigi.x -= 10;
    draw();
    update();
  });

  draw();
</script>
</body>
</html>
