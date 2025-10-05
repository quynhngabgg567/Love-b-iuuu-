<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tuấn ❤️ Nga</title>
<style>
  html, body {
    margin: 0;
    padding: 0;
    background: black;
    overflow: hidden;
    height: 100%;
    width: 100%;
  }
  canvas {
    position: absolute;
    top: 0;
    left: 0;
  }
  .circle-text {
    position: absolute;
    bottom: 80px;
    width: 100%;
    text-align: center;
    font-family: "Poppins", sans-serif;
    color: pink;
    font-size: 18px;
    animation: rotateText 15s linear infinite;
    white-space: nowrap;
  }
  @keyframes rotateText {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }
  audio {
    display: none;
  }
</style>
</head>
<body>

<canvas id="heart"></canvas>

<div class="circle-text">
  Tuấn ❤️ Nga • Anh yêu em 💕 • Bé iu của anh thêm tuổi mới rồi 😘 • 
  Chúc em luôn xinh đẹp, vui vẻ và hạnh phúc 💖 • 
  Chúc em bé của anh thật mạnh mẽ trên con đường phía trước 💪🌸 • 
  Sau này, em vẫn mãi là một phần đặc biệt trong tim anh ♥️💗 • 
  Cảm ơn vì hai ta đã gặp nhau ở độ tuổi đẹp nhất 🫂💕
</div>

<audio id="music" autoplay loop>
  <source src="https://files.catbox.moe/x6uz1t.mp3" type="audio/mpeg">
</audio>

<script>
const canvas = document.getElementById("heart");
const ctx = canvas.getContext("2d");
let particles = [];
resizeCanvas();

function resizeCanvas() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
}
window.addEventListener("resize", resizeCanvas);

function heartShape(t) {
  const x = 16 * Math.pow(Math.sin(t), 3);
  const y = 13 * Math.cos(t) - 5 * Math.cos(2*t) - 2 * Math.cos(3*t) - Math.cos(4*t);
  return { x, y };
}

function createHeartParticles() {
  particles = [];
  for (let i = 0; i < 300; i++) {
    const t = Math.random() * Math.PI * 2;
    const pos = heartShape(t);
    particles.push({
      x: canvas.width/2,
      y: canvas.height/2,
      tx: canvas.width/2 + pos.x * 20,
      ty: canvas.height/2 - pos.y * 20,
      vx: (Math.random() - 0.5) * 8,
      vy: (Math.random() - 0.5) * 8,
      alpha: 1,
      glow: Math.random() * 2 + 1
    });
  }
}

function animateHeart() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  particles.forEach(p => {
    p.x += (p.tx - p.x) * 0.05;
    p.y += (p.ty - p.y) * 0.05;
    p.alpha -= 0.002;
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.glow, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(255, 105, 180, ${p.alpha})`;
    ctx.shadowColor = "rgba(255, 105, 180, 0.9)";
    ctx.shadowBlur = 15;
    ctx.fill();
  });
}

function explodeHeart() {
  particles.forEach(p => {
    p.vx = (Math.random() - 0.5) * 40;
    p.vy = (Math.random() - 0.5) * 40;
    p.x += p.vx;
    p.y += p.vy;
    p.alpha = 1;
  });
  setTimeout(createHeartParticles, 1000);
}

function loop() {
  animateHeart();
  requestAnimationFrame(loop);
}

createHeartParticles();
loop();
setInterval(explodeHeart, 5000);

document.getElementById("music").volume = 0.7;
</script>

</body>
</html>
