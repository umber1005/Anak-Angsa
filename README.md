<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <title>Game Menetaskan Telur Angsa</title>
  <style>
    body {
      background: #c2f0f7;
      font-family: "Comic Sans MS", cursive, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      overflow: hidden;
      flex-direction: column;
    }

    h1 {
      margin-bottom: 10px;
      color: #333;
    }

    #game-container {
      position: relative;
      width: 500px;
      height: 400px;
      background: #f5f5dc;
      border: 5px solid #888;
      border-radius: 20px;
      box-shadow: 4px 4px 10px rgba(0,0,0,0.3);
      overflow: hidden;
    }

    #goose {
      position: absolute;
      width: 200px;
      bottom: 50px;
      left: 30px;
    }

    #egg {
      position: absolute;
      width: 100px;
      bottom: 40px;
      left: 280px;
      cursor: pointer;
      transition: transform 0.1s;
    }

    #chick {
      position: absolute;
      width: 100px;
      bottom: 40px;
      left: 280px;
      display: none;
    }

    #clicks {
      margin-top: 10px;
      font-size: 18px;
    }

    #message {
      font-size: 20px;
      color: green;
      margin-top: 10px;
    }
  </style>
</head>
<body>

  <h1>Menetaskan Telur Angsa</h1>
  <div id="game-container">
    <img id="goose" src="https://cdn.pixabay.com/photo/2021/08/06/13/23/goose-6526860_1280.png" alt="Induk Angsa" />
    <img id="egg" src="https://cdn.pixabay.com/photo/2016/03/31/20/11/easter-egg-1293512_1280.png" alt="Telur" />
    <img id="chick" src="https://cdn.pixabay.com/photo/2021/04/12/08/47/chick-6169987_1280.png" alt="Anak Angsa" />
  </div>

  <div id="clicks">Tekan telur untuk menetaskan!</div>
  <div id="message"></div>

  <script>
    const egg = document.getElementById("egg");
    const chick = document.getElementById("chick");
    const clicksText = document.getElementById("clicks");
    const message = document.getElementById("message");

    let clicks = 0;
    const maxClicks = 7;

    egg.addEventListener("click", () => {
      clicks++;
      egg.style.transform = "scale(1.05)";
      setTimeout(() => egg.style.transform = "scale(1)", 100);

      if (clicks < maxClicks) {
        clicksText.textContent = `Mengetuk telur... (${clicks}/${maxClicks})`;
      } else {
        egg.style.display = "none";
        chick.style.display = "block";
        message.textContent = "Telur menetas! Lihat, anak angsa lahir!";
        clicksText.textContent = "";
      }
    });
  </script>
</body>
</html>
