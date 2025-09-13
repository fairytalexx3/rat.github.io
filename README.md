<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>HAPPY BIRTHDAY</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css"/>
  <style>
    html, body { margin: 0; padding: 0; height: 100%; overflow: hidden; }
    #fireworks { position: fixed; top: 0; left: 0; z-index: 0; }
    #typewriter span, #typewriter2 span { opacity: 0; animation: fadeIn 0.05s forwards; }
    @keyframes fadeIn { to { opacity: 1; } }
  </style>
</head>
<body
  style="background-image: url(https://images.unsplash.com/photo-1530273973427-22351773250c?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3);
         background-size: cover; background-position: center;"
  class="flex justify-center h-screen items-center relative"
>
  <canvas id="fireworks"></canvas>

  <div id="kartu"
    class="bg-white border px-10 py-8 border-4 border-gray-300 shadow-lg shadow-blue-300 rounded-xl text-center animate__animated animate__backInDown m-8 w-80 relative z-10">
    <h1 class="text-3xl">Happy Birthday</h1>
    <h1 class="text-4xl text-blue-500 font-bold animate__animated animate__pulse animate__infinite">KAMU</h1>
    <button class="p-2 bg-blue-600 text-white rounded mt-5 hover:bg-blue-900 transition ease-in w-full animate__animated animate__delay-1s animate__tada"
      onclick="ubahKartu()">Klik Disini!</button>
  </div>

  <audio id="lagu" autoplay loop preload="auto">
    <source src="multonih.mp3" type="audio/mpeg" />
  </audio>

  <script src="https://cdn.jsdelivr.net/npm/@tsparticles/confetti@3.0.3/tsparticles.confetti.bundle.min.js"></script>
  <script>
    confetti({ particleCount: 100, spread: 70, origin: { y: 0.6 } });

    let kartu = document.getElementById("kartu");
    const pesan = [
      "Selamat ulang tahun, Semoga makin banyak kebahagiaan 🎉",
      "Rezeki lancar dan semua impian jadi kenyataan 🙏",
      "Semoga kita terus bareng-bareng, seru-seruan, saling dukung ❤️",
      `<h2 class='text-xl font-bold mb-3'>Hadiah 🎁</h2><p class='text-red-600 font-semibold'>Eh ternyata hadiahnya PRANK 🤣🤣</p>`,
      `<h2 class="text-xl font-bold mb-3">Harapanku buat kamu kedepannya</h2><p id="typewriter"></p>`,
      `<p id="typewriter2"></p>`
    ];
    let indexPesan = 0;

    function ubahKartu() {
      const audio = document.getElementById("lagu");
      if (audio && audio.paused) audio.play();
      tampilkanPesan();
    }

    function tampilkanPesan() {
      // slide harapan
      if (indexPesan === 4) {
        kartu.innerHTML = `
          <h1 class="text-xl font-bold mb-4">Harapanku buat kamu kedepannya</h1>
          <div id="typewriter" class="text-left text-sm leading-relaxed"></div>
          <button class="p-2 bg-blue-600 text-white rounded mt-5 hover:bg-blue-900 transition ease-in w-full"
            onclick="selanjutnya()">Selanjutnya</button>
        `;
        typeWriterEffect("selamat ulang tahun kamu!🎉 semoga di usia yang baru ini,kamu selalu diberi kesehatan, kebahagiaan,dan kekuatan untuk meraih setiap mimpi, ingat bertambahnya usia bukan sekadar angka,tapi kesempatan baru untuk jadi versi terbaik diri, sehat-sehat ya kamu", "typewriter");
        return;
      }

      // slide penutup
      if (indexPesan === 5) {
        kartu.innerHTML = `
          <div id="typewriter2" class="text-sm leading-relaxed"></div>
          <div class="mt-6 text-center font-semibold">- Dari : Seseorang -</div>
          <button class="p-2 bg-slate-600 text-white rounded mt-5 hover:bg-slate-900 transition ease-in w-full"
            onclick="refresh()">Tutup</button>
        `;
        typeWriterEffect("sekali lagi selamat ulang tahun,semoga setiap detik di hidupmu selalu dipenuhi kebahagiaan dan berkah yang tak pernah putus", "typewriter2");
        return;
      }

      // slide 3
      if (indexPesan === 2) {
        kartu.innerHTML = `
          <h1 class="font-semibold animate__animated animate__zoomIn">${pesan[indexPesan]}</h1>
          <button class="p-2 bg-blue-600 text-white rounded mt-5 hover:bg-blue-900 transition ease-in w-full"
            onclick="selanjutnya()">Selanjutnya</button>
          <button class="p-2 bg-pink-600 text-white rounded mt-3 hover:bg-pink-900 transition ease-in w-full"
            onclick="lompatHadiah()">Hadiah 🎁</button>
        `;
        return;
      }

      // slide prank
      if (indexPesan === 3) {
        kartu.innerHTML = `
          <div class="animate__animated animate__zoomIn">${pesan[indexPesan]}</div>
          <button class="p-2 bg-blue-600 text-white rounded mt-5 hover:bg-blue-900 transition ease-in w-full"
            onclick="selanjutnya()">Selanjutnya</button>
        `;
        return;
      }

      // default (slide 1 & 2)
      kartu.innerHTML = `
        <h1 class="font-semibold animate__animated animate__zoomIn">${pesan[indexPesan]}</h1>
        <button class="p-2 bg-blue-600 text-white rounded mt-5 hover:bg-blue-900 transition ease-in w-full"
          onclick="selanjutnya()">Selanjutnya</button>
      `;
    }

    function selanjutnya() {
      if (indexPesan === 2 || indexPesan === 3) {
        indexPesan = 4; // dari slide 3 atau prank → langsung ke harapan
      } else {
        indexPesan++;
      }
      if (indexPesan >= pesan.length) indexPesan = pesan.length - 1;
      tampilkanPesan();
    }

    function lompatHadiah() {
      indexPesan = 3;
      tampilkanPesan();
    }

    function refresh() {
      const audio = document.getElementById("lagu");
      if (audio) { audio.pause(); audio.currentTime = 0; }
      location.reload();
    }

    function typeWriterEffect(text, elementId) {
      const container = document.getElementById(elementId);
      container.innerHTML = "";
      text.split("").forEach((char, i) => {
        let span = document.createElement("span");
        span.textContent = char;
        span.style.animationDelay = `${i * 0.05}s`;
        container.appendChild(span);
      });
    }

    // fireworks
    const canvas = document.getElementById('fireworks');
    const ctx = canvas.getContext('2d');
    function resizeCanvas(){ canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
    resizeCanvas(); window.addEventListener('resize', resizeCanvas);

    let fireworks = [], particles = [];
    class Firework { constructor(x,y,targetY,color){ this.x=x; this.y=y; this.targetY=targetY; this.color=color; this.speed=5; }
      update(){ this.y-=this.speed; if(this.y<=this.targetY){ this.explode(); return true; } this.draw(); return false; }
      draw(){ ctx.beginPath(); ctx.arc(this.x,this.y,2,0,Math.PI*2); ctx.fillStyle=this.color; ctx.fill(); }
      explode(){ for(let i=0;i<60;i++){ particles.push(new Particle(this.x,this.y,this.color)); } } }
    class Particle { constructor(x,y,color){ this.x=x; this.y=y; this.color=color; this.speed=Math.random()*5+1; this.angle=Math.random()*Math.PI*2; this.alpha=1; this.decay=Math.random()*0.02+0.01; }
      update(){ this.x+=Math.cos(this.angle)*this.speed; this.y+=Math.sin(this.angle)*this.speed; this.alpha-=this.decay; this.draw(); return this.alpha<=0; }
      draw(){ ctx.save(); ctx.globalAlpha=this.alpha; ctx.beginPath(); ctx.arc(this.x,this.y,2,0,Math.PI*2); ctx.fillStyle=this.color; ctx.fill(); ctx.restore(); } }
    function animate(){ ctx.fillStyle='rgba(0,0,0,0.2)'; ctx.fillRect(0,0,canvas.width,canvas.height);
      if(Math.random()<0.04){ let x=Math.random()*canvas.width; let color=`hsl(${Math.random()*360},100%,50%)`; fireworks.push(new Firework(x,canvas.height,Math.random()*canvas.height/2,color)); }
      for(let i=fireworks.length-1;i>=0;i--){ if(fireworks[i].update()) fireworks.splice(i,1); }
      for(let i=particles.length-1;i>=0;i--){ if(particles[i].update()) particles.splice(i,1); }
      requestAnimationFrame(animate); }
    animate();
    canvas.addEventListener('click',(e)=>{ let x=e.clientX; let color=`hsl(${Math.random()*360},100%,50%)`; fireworks.push(new Firework(x,canvas.height,e.clientY,color)); });
  </script>
</body>
</html>
