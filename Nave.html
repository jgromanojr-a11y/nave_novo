<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Mackgame</title>
    <style>
        /* Estilos CSS do jogo */
        body, html {
            margin: 0;
            padding: 0;
            overflow: hidden;
            background-color: #000;
            font-family: 'Arial', sans-serif;
            color: white;
            touch-action: manipulation; /* Impede zoom duplo toque */
        }

        #game-container {
            position: absolute;
            width: 100%;
            height: 100%;
        }

        canvas {
            display: block;
            width: 100%;
            height: 100%;
        }

        #ui {
            position: absolute;
            bottom: 0;
            width: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 10px;
            box-sizing: border-box;
            user-select: none; /* Impede seleção de texto na UI */
        }

        #stats {
            display: flex;
            justify-content: space-between;
            width: 100%;
            max-width: 600px;
            padding: 5px 20px;
            font-size: 1em;
        }

        #controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
            width: 100%;
            max-width: 600px;
            padding-top: 10px;
        }

        #joystick {
            width: 130px;
            height: 130px;
            background-color: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            position: relative;
            touch-action: none;
        }

        #stick {
            width: 60px;
            height: 60px;
            background-color: rgba(255, 255, 255, 0.5);
            border-radius: 50%;
            position: absolute;
        }

        #pauseBtn, #fireBtn {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            font-size: 1.2em;
            font-weight: bold;
            color: white;
            border: none;
            cursor: pointer;
            touch-action: manipulation;
        }

        #pauseBtn {
            background-color: rgba(50, 50, 50, 0.7);
        }

        #fireBtn {
            background-color: rgba(255, 0, 0, 0.7);
        }

        .overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.5s ease;
            z-index: 10;
        }

        .overlay.show {
            opacity: 1;
            visibility: visible;
        }

        .overlay h1 {
            font-size: 3em;
            margin-bottom: 20px;
        }

        .overlay p {
            font-size: 1.5em;
        }

        .diff-buttons button, #restartBtn {
            font-size: 1.2em;
            padding: 15px 30px;
            margin: 10px;
            cursor: pointer;
            background-color: #333;
            color: white;
            border: 2px solid #555;
            border-radius: 5px;
            transition: background-color 0.3s;
        }

        .diff-buttons button:hover, #restartBtn:hover {
            background-color: #555;
        }

        .diff-buttons {
            display: flex;
            flex-direction: column;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div id="game-container">
        <canvas id="game"></canvas>
    </div>

    <div id="ui">
        <div id="stats">
            <div id="lives">Vidas: 5</div>
            <div id="score">Score: 0</div>
            <div id="diff">Dificuldade: Fácil</div>
        </div>
        <div id="controls">
            <div id="joystick">
                <div id="stick"></div>
            </div>
            <button id="pauseBtn">⏸</button>
            <button id="fireBtn">FOGO</button>
        </div>
    </div>

    <div id="startOverlay" class="overlay show">
        <h1>Mackgame</h1>
        <p>Escolha a Dificuldade</p>
        <div class="diff-buttons">
            <button class="diffBtn" data-diff="easy">Fácil</button>
            <button class="diffBtn" data-diff="medium">Médio</button>
            <button class="diffBtn" data-diff="hard">Difícil</button>
        </div>
    </div>

    <div id="gameOver" class="overlay">
        <h1>Game Over</h1>
        <p id="finalScore">Score: 0</p>
        <button id="restartBtn">Tente Novamente</button>
    </div>

    <script>
        // Código JavaScript do jogo
        (() => {
          // ===== Canvas (HiDPI) =====
          const canvas = document.getElementById('game');
          const ctx = canvas.getContext('2d');
          let W = 0, H = 0, DPR = 1;
          function resize() {
            DPR = Math.max(1, Math.floor(window.devicePixelRatio || 1));
            W = Math.floor(window.innerWidth * DPR);
            H = Math.floor(window.innerHeight * DPR);
            canvas.width = W;
            canvas.height = H;
            canvas.style.width = (W / DPR) + 'px';
            canvas.style.height = (H / DPR) + 'px';
          }
          window.addEventListener('resize', resize, { passive: true });
          resize();

          // ===== UI =====
          const scoreEl = document.getElementById('score');
          const livesEl = document.getElementById('lives');
          const diffEl = document.getElementById('diff');
          const pauseBtn = document.getElementById('pauseBtn');
          const startOverlay = document.getElementById('startOverlay');
          const gameOver = document.getElementById('gameOver');
          const finalScore = document.getElementById('finalScore');
          const restartBtn = document.getElementById('restartBtn');

          document.querySelectorAll('.diffBtn').forEach(b => {
            const startHandler = (e) => {
              e.preventDefault();
              startGame(b.dataset.diff);
              b.removeEventListener('click', clickHandler);
            };
            const clickHandler = () => startGame(b.dataset.diff);

            b.addEventListener('touchstart', startHandler, { passive: false });
            b.addEventListener('click', clickHandler);
          });

          restartBtn.addEventListener('click', () => {
            startOverlay.classList.add('show');
            gameOver.classList.remove('show');
            state.running = false;
          });

          pauseBtn.addEventListener('click', () => {
            if (!state.running) return;
            state.paused = !state.paused;
            pauseBtn.textContent = state.paused ? '▶️' : '⏸';
          });

          // ===== WebAudio (sons) =====
          let audioCtx = null;
          function unlockAudio() {
            if (!audioCtx) {
              audioCtx = new (window.AudioContext || window.webkitAudioContext)();
              const o = audioCtx.createOscillator();
              const g = audioCtx.createGain();
              g.gain.value = 0.0001;
              o.connect(g).connect(audioCtx.destination);
              o.start();
              o.stop(audioCtx.currentTime + 0.01);
            }
          }
          function beep(type = 'square', f = 600, dur = 0.08, vol = 0.2, slide = -300) {
            if (!audioCtx) return;
            const o = audioCtx.createOscillator(), g = audioCtx.createGain();
            o.type = type;
            o.frequency.value = f;
            const t = audioCtx.currentTime;
            g.gain.setValueAtTime(0, t);
            g.gain.linearRampToValueAtTime(vol, t + 0.01);
            g.gain.exponentialRampToValueAtTime(0.0001, t + dur);
            o.connect(g).connect(audioCtx.destination);
            if (slide !== 0) {
              o.frequency.setValueAtTime(f, t);
              o.frequency.exponentialRampToValueAtTime(Math.max(60, f + slide), t + dur);
            }
            o.start(t);
            o.stop(t + dur + 0.02);
          }
          const SFX = {
            shot: () => beep('square', 720, 0.07, 0.20, -400),
            boom: () => {
              beep('triangle', 220, 0.20, 0.25, -120);
              setTimeout(() => beep('triangle', 120, 0.16, 0.18, -30), 60);
            }
          };

          // ===== Controles: Joystick + Fogo =====
          const joyBase = document.getElementById('joystick');
          const joyStick = document.getElementById('stick');
          const fireBtn = document.getElementById('fireBtn');

          let joy = { active: false, dx: 0, dy: 0, radius: 65 };

          function moveStick(x, y) {
            const r = joy.radius;
            const dx = x - r;
            const dy = y - r;
            const dist = Math.sqrt(dx * dx + dy * dy);

            if (dist > r) {
              const angle = Math.atan2(dy, dx);
              joyStick.style.left = `${r + r * Math.cos(angle)}px`;
              joyStick.style.top = `${r + r * Math.sin(angle)}px`;
            } else {
              joyStick.style.left = `${x}px`;
              joyStick.style.top = `${y}px`;
            }
            joy.dx = dx / r;
            joy.dy = dy / r;
          }

          function joyPosFromEvent(e) {
            const t = e.touches ? e.touches[0] : e;
            const r = joyBase.getBoundingClientRect();
            return { x: (t.clientX - r.left), y: (t.clientY - r.top) };
          }
          function joyStart(e) {
            unlockAudio();
            joy.active = true;
            const p = joyPosFromEvent(e);
            moveStick(p.x, p.y);
            e.preventDefault();
          }
          function joyMove(e) {
            if (!joy.active) return;
            const p = joyPosFromEvent(e);
            moveStick(p.x, p.y);
            e.preventDefault();
          }
          function joyEnd() {
            joy.active = false;
            joy.dx = joy.dy = 0;
            joyStick.style.left = '50%';
            joyStick.style.top = '50%';
          }
          joyBase.addEventListener('touchstart', joyStart, { passive: false });
          joyBase.addEventListener('touchmove', joyMove, { passive: false });
          joyBase.addEventListener('touchend', joyEnd, { passive: false });
          joyBase.addEventListener('mousedown', joyStart);
          window.addEventListener('mousemove', joyMove);
          window.addEventListener('mouseup', joyEnd);

          let firing = false;
          fireBtn.addEventListener('touchstart', () => { unlockAudio(); firing = true; }, { passive: true });
          fireBtn.addEventListener('touchend', () => { firing = false; }, { passive: true });
          fireBtn.addEventListener('mousedown', () => { unlockAudio(); firing = true; });
          fireBtn.addEventListener('mouseup', () => { firing = false; });

          // ===== Configurações =====
          const DIFFS = {
            easy: { label: 'Fácil', spawn: 900, speed: 0.16, max: 5 },
            medium: { label: 'Médio', spawn: 650, speed: 0.22, max: 7 },
            hard: { label: 'Difícil', spawn: 420, speed: 0.30, max: 9 },
          };
          const ENEMY_TYPES = [
            { name: 'small', w: 24, h: 22, color: '#ff6363', score: 10, speedMul: 1.0 },
            { name: 'medium', w: 32, h: 28, color: '#ffb84a', score: 20, speedMul: 0.9 },
            { name: 'large', w: 42, h: 36, color: '#7cff84', score: 50, speedMul: 0.75 },
          ];

          // ===== Estado do jogo =====
          const state = {
            running: false,
            paused: false,
            score: 0,
            lives: 5,
            diff: 'easy',
            spawnTimer: 0,
            lastShot: 0,
            time: 0
          };

          const player = { x: W / 2, y: H * 0.85, w: 36 * DPR, h: 44 * DPR, speed: 0.6 };
          const bullets = [];
          const enemies = [];
          const particles = [];

          // Variáveis para as imagens dos planetas
          const planets = [];
          const planetImages = [
              // Imagens de exemplo para a lua e planetas
              // Você pode substituir essas URLs por suas próprias imagens ou URLs de CDN
              // Certifique-se de que as imagens sejam de domínio público ou que você tenha permissão para usá-las.
              // Para simplificar, vou usar placeholders e sugerir que você adicione as URLs reais.
              "https://upload.wikimedia.org/wikipedia/commons/e/e1/FullMoon2010.jpg", // Lua
              "https://upload.wikimedia.org/wikipedia/commons/2/2b/Hubble_Views_Mars_in_Opposition_2016_%28cropped%29.jpg", // Marte
              "https://upload.wikimedia.org/wikipedia/commons/e/ea/Jupiter_and_its_shrunken_Great_Red_Spot.jpg", // Júpiter
              "https://upload.wikimedia.org/wikipedia/commons/thumb/c/c7/Saturn_during_Equinox.jpg/1200px-Saturn_during_Equinox.jpg", // Saturno
              "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d3/Uranus2.jpg/1024px-Uranus2.jpg" // Urano
          ];

          function loadPlanetImages() {
              planetImages.forEach(src => {
                  const img = new Image();
                  img.src = src;
                  img.onload = () => {
                      planets.push({
                          img: img,
                          x: rand(0, W),
                          y: rand(-H, H * 0.6), // Começa fora da tela ou no topo
                          speed: rand(0.01, 0.05) * DPR,
                          size: rand(0.08, 0.25) * W, // Tamanho proporcional à largura da tela
                          opacity: rand(0.3, 0.7)
                      });
                  };
              });
          }

          function reset(d) {
            state.running = true;
            state.paused = false;
            state.score = 0;
            state.lives = 5;
            state.diff = d;
            state.spawnTimer = 0;
            state.lastShot = 0;
            state.time = 0;
            bullets.length = 0;
            enemies.length = 0;
            particles.length = 0;
            player.x = W / 2;
            player.y = H * 0.85;
            diffEl.textContent = 'Dificuldade: ' + DIFFS[d].label;
            livesEl.textContent = 'Vidas: ' + state.lives;
            scoreEl.textContent = 'Score: ' + state.score;
            pauseBtn.textContent = '⏸';
            // Reposiciona os planetas para um novo jogo
            planets.forEach(p => {
                p.x = rand(0, W);
                p.y = rand(-H, H * 0.6);
            });
          }

          // ===== Helpers =====
          function rand(a, b) {
            return a + Math.random() * (b - a);
          }
          function clamp(v, a, b) {
            return Math.max(a, Math.min(b, v));
          }
          function overlap(a, b) {
            return Math.abs(a.x - b.x) * 2 < (a.w + b.w) && Math.abs(a.y - b.y) * 2 < (a.h + b.h);
          }

          // ===== Spawns =====
          function spawnEnemy() {
            if (enemies.length >= DIFFS[state.diff].max) return;
            const t = ENEMY_TYPES[Math.floor(Math.random() * ENEMY_TYPES.length)];
            const e = {
              type: t.name,
              score: t.score,
              color: t.color,
              w: t.w * DPR,
              h: t.h * DPR,
              x: rand(30 * DPR, W - 30 * DPR),
              y: -40 * DPR,
              vy: (DIFFS[state.diff].speed * t.speedMul) * DPR,
              vx: (Math.random() < 0.5 ? -1 : 1) * rand(0.05, 0.12) * DPR
            };
            enemies.push(e);
          }

          // ===== Efeitos =====
          function spawnExplosion(x, y, n = 16, color = '#ffa800') {
            for (let i = 0; i < n; i++) {
              particles.push({
                x,
                y,
                r: rand(1, 3) * DPR,
                life: rand(220, 480),
                vx: Math.cos(i / n * Math.PI * 2) * rand(0.08, 0.35) * DPR,
                vy: Math.sin(i / n * Math.PI * 2) * rand(0.08, 0.35) * DPR,
                color
              });
            }
          }

          // ===== Fluxo =====
          function startGame(d) {
            unlockAudio();
            startOverlay.classList.remove('show');
            gameOver.classList.remove('show');
            reset(d);
            last = performance.now();
          }

          function gameOverNow() {
            state.running = false;
            finalScore.textContent = 'Score: ' + state.score;
            gameOver.classList.add('show');
          }

          // ===== Loop =====
          let last = performance.now();
          function loop(now) {
            const dt = now - last;
            last = now;
            if (!state.running || state.paused) {
              draw();
              requestAnimationFrame(loop);
              return;
            }

            state.time += dt;
            update(dt);
            draw();
            requestAnimationFrame(loop);
          }

          function update(dt) {
            const dx = joy.dx;
            const dy = joy.dy;
            const speed = player.speed * dt * DPR * 0.8;
            player.x += dx * speed * 3.2;
            player.y += dy * speed * 3.2;

            player.x = clamp(player.x, player.w / 2 + 10 * DPR, W - player.w / 2 - 10 * DPR);
            // Permite que a nave suba mais
            player.y = clamp(player.y, player.h / 2 + 10 * DPR, H - player.h / 2 - 10 * DPR);

            if (firing && state.time - state.lastShot > 160) {
              bullets.push({ x: player.x, y: player.y - player.h / 2, w: 6 * DPR, h: 14 * DPR, vy: -0.9 * DPR });
              state.lastShot = state.time;
              SFX.shot();
            }
            for (let i = bullets.length - 1; i >= 0; i--) {
              const b = bullets[i];
              b.y += b.vy * dt;
              if (b.y < -30) bullets.splice(i, 1);
            }

            state.spawnTimer += dt;
            const spawnEvery = DIFFS[state.diff].spawn;
            if (state.spawnTimer > spawnEvery) {
              state.spawnTimer = 0;
              spawnEnemy();
            }

            for (let i = enemies.length - 1; i >= 0; i--) {
              const e = enemies[i];
              e.y += e.vy * dt;
              e.x += e.vx * dt;
              if (e.x < e.w / 2 || e.x > W - e.w / 2) e.vx *= -1;

              for (let j = bullets.length - 1; j >= 0; j--) {
                const b = bullets[j];
                if (overlap({ x: b.x, y: b.y, w: b.w, h: b.h }, e)) {
                  bullets.splice(j, 1);
                  enemies.splice(i, 1);
                  spawnExplosion(e.x, e.y, 18, e.color);
                  SFX.boom();
                  state.score += e.score;
                  scoreEl.textContent = 'Score: ' + state.score;
                  break;
                }
              }
            }

            for (let i = enemies.length - 1; i >= 0; i--) {
              const e = enemies[i];
              if (overlap(e, player)) {
                enemies.splice(i, 1);
                spawnExplosion(player.x, player.y, 24, '#66ffff');
                SFX.boom();
                state.lives -= 1;
                livesEl.textContent = 'Vidas: ' + state.lives;
                if (state.lives <= 0) {
                  gameOverNow();
                  return;
                }
              }

              if (e.y - e.h / 2 > H + 40) enemies.splice(i, 1);
            }

            for (let i = particles.length - 1; i >= 0; i--) {
              const p = particles[i];
              p.x += p.vx * dt;
              p.y += p.vy * dt;
              p.life -= dt;
              p.vy += 0.00015 * dt;
              if (p.life <= 0) particles.splice(i, 1);
            }

            // Atualiza a posição dos planetas
            planets.forEach(p => {
                p.y += p.speed * dt;
                if (p.y > H + p.size / 2) {
                    p.y = -p.size / 2; // Reposiciona no topo
                    p.x = rand(0, W); // Nova posição horizontal
                    p.speed = rand(0.01, 0.05) * DPR; // Nova velocidade
                    p.size = rand(0.08, 0.25) * W; // Novo tamanho
                    p.opacity = rand(0.3, 0.7); // Nova opacidade
                }
            });
          }

          function draw() {
            ctx.clearRect(0, 0, W, H);

            // Desenha estrelas
            for (let i = 0; i < 70; i++) {
              const sx = (i * 97 + (state.time * 0.05)) % W;
              const sy = (i * 131 + (state.time * 0.12)) % H;
              ctx.globalAlpha = 0.35 + ((i % 3) / 10);
              ctx.fillStyle = '#8ff';
              ctx.fillRect(sx, sy, 2 * DPR, 2 * DPR);
            }
            ctx.globalAlpha = 1;

            // Desenha os planetas carregados
            planets.forEach(p => {
                if (p.img.complete) {
                    ctx.save();
                    ctx.globalAlpha = p.opacity;
                    ctx.drawImage(p.img, p.x - p.size / 2, p.y - p.size / 2, p.size, p.size);
                    ctx.restore();
                }
            });

            drawPixelShip(player.x, player.y, player.w, player.h, '#66ffff');
            ctx.fillStyle = '#9ff';
            bullets.forEach(b => {
              roundedRect(b.x - b.w / 2, b.y - b.h / 2, b.w, b.h, 2 * DPR);
              ctx.fill();
            });
            enemies.forEach(e => drawAlien(e.x, e.y, e.w, e.h, e.color));
            particles.forEach(p => {
              ctx.globalAlpha = Math.max(0, p.life / 480);
              ctx.fillStyle = p.color;
              ctx.beginPath();
              ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
              ctx.fill();
              ctx.globalAlpha = 1;
            });
          }

          function roundedRect(x, y, w, h, r) {
            ctx.beginPath();
            ctx.moveTo(x + r, y);
            ctx.arcTo(x + w, y, x + w, y + h, r);
            ctx.arcTo(x + w, y + h, x, y + h, r);
            ctx.arcTo(x, y + h, x, y, r);
            ctx.arcTo(x, y, x + w, y, r);
            ctx.closePath();
          }

          function drawPixel(x, y, color) {
              ctx.fillStyle = color;
              ctx.fillRect(x, y, 1, 1);
          }

          function drawPixelShip(x, y, w, h) {
              ctx.save();
              ctx.translate(x - w / 2, y - h / 2);
              ctx.scale(w / 30, h / 29); // Escala para o tamanho desejado (30x29 pixels)

              // Cores
              const corAzulClaro = '#b9e8ff';
              const corAzulMedio = '#a0d1eb';
              const corAzulEscuro = '#688c9f';
              const corVermelho = '#e55a5a';
              const corCinza = '#a6a6a6';
              const corCinzaEscuro = '#858585';
              const corLaranja = '#f0c055';

              // Função para desenhar pixels (para simplificar a leitura do código)
              const px = (x, y, color) => drawPixel(x, y, color);

              // Desenha o corpo da nave - Linha por linha
              // Base do cockpit
              px(11, 2, corAzulEscuro);
              px(18, 2, corAzulEscuro);
              px(12, 3, corAzulEscuro);
              px(17, 3, corAzulEscuro);
              px(13, 4, corAzulEscuro);
              px(16, 4, corAzulEscuro);
              
              // Cúpula do cockpit
              for (let i = 13; i <= 16; i++) px(i, 2, corAzulClaro);
              for (let i = 12; i <= 17; i++) px(i, 3, corAzulClaro);
              for (let i = 11; i <= 18; i++) px(i, 4, corAzulClaro);
              for (let i = 10; i <= 19; i++) px(i, 5, corAzulClaro);
              for (let i = 9; i <= 20; i++) px(i, 6, corAzulClaro);
              for (let i = 8; i <= 21; i++) px(i, 7, corAzulClaro);
              for (let i = 7; i <= 22; i++) px(i, 8, corAzulClaro);
              for (let i = 6; i <= 23; i++) px(i, 9, corAzulClaro);
              
              // Detalhes da cúpula
              px(11, 5, corAzulMedio);
              px(12, 5, corAzulMedio);
              px(13, 6, corAzulMedio);
              px(14, 6, corAzulMedio);
              px(15, 6, corAzulMedio);
              px(16, 6, corAzulMedio);
              px(17, 7, corAzulMedio);
              px(18, 7, corAzulMedio);
              px(19, 8, corAzulMedio);
              px(20, 8, corAzulMedio);
              px(21, 9, corAzulMedio);
              px(22, 9, corAzulMedio);
              
              px(18, 5, corAzulMedio);
              px(17, 5, corAzulMedio);
              px(16, 6, corAzulMedio);
              px(15, 6, corAzulMedio);
              px(14, 6, corAzulMedio);
              px(13, 6, corAzulMedio);
              px(12, 7, corAzulMedio);
              px(11, 7, corAzulMedio);
              px(10, 8, corAzulMedio);
              px(9, 8, corAzulMedio);
              px(8, 9, corAzulMedio);
              px(7, 9, corAzulMedio);

              // Disco principal (cinza)
              for (let i = 4; i <= 25; i++) px(i, 10, corCinza);
              for (let i = 3; i <= 26; i++) px(i, 11, corCinza);
              for (let i = 2; i <= 27; i++) px(i, 12, corCinza);
              for (let i = 1; i <= 28; i++) px(i, 13, corCinza);
              for (let i = 1; i <= 28; i++) px(i, 14, corCinza);
              
              // Linhas vermelhas
              for (let i = 0; i <= 29; i++) px(i, 15, corVermelho);
              for (let i = 0; i <= 29; i++) px(i, 16, corVermelho);
              for (let i = 0; i <= 29; i++) px(i, 17, corVermelho);
              for (let i = 0; i <= 29; i++) px(i, 18, corVermelho);
              
              // Parte inferior do disco (cinza)
              for (let i = 1; i <= 28; i++) px(i, 19, corCinza);
              for (let i = 1; i <= 28; i++) px(i, 20, corCinza);
              for (let i = 2; i <= 27; i++) px(i, 21, corCinza);
              for (let i = 3; i <= 26; i++) px(i, 22, corCinza);
              for (let i = 4; i <= 25; i++) px(i, 23, corCinza);

              // Detalhes cinza escuro
              px(5, 10, corCinzaEscuro);
              px(24, 10, corCinzaEscuro);
              px(4, 11, corCinzaEscuro);
              px(25, 11, corCinzaEscuro);
              px(3, 12, corCinzaEscuro);
              px(26, 12, corCinzaEscuro);
              px(2, 13, corCinzaEscuro);
              px(27, 13, corCinzaEscuro);
              px(2, 14, corCinzaEscuro);
              px(27, 14, corCinzaEscuro);
              px(2, 19, corCinzaEscuro);
              px(27, 19, corCinzaEscuro);
              px(3, 20, corCinzaEscuro);
              px(26, 20, corCinzaEscuro);
              px(4, 21, corCinzaEscuro);
              px(25, 21, corCinzaEscuro);
              px(5, 22, corCinzaEscuro);
              px(24, 22, corCinzaEscuro);

              // Pernas (trem de pouso)
              // Perna esquerda
              px(4, 24, corLaranja);
              px(4, 25, corCinza);
              px(4, 26, corCinza);
              px(4, 27, corCinza);
              px(4, 28, corCinza);
              px(3, 28, corCinza);
              px(5, 28, corCinza);
              px(3, 27, corCinzaEscuro);
              px(5, 27, corCinzaEscuro);
              
              // Perna direita
              px(25, 24, corLaranja);
              px(25, 25, corCinza);
              px(25, 26, corCinza);
              px(25, 27, corCinza);
              px(25, 28, corCinza);
              px(24, 28, corCinza);
              px(26, 28, corCinza);
              px(24, 27, corCinzaEscuro);
              px(26, 27, corCinzaEscuro);
              
              // Perna central
              px(14, 24, corLaranja);
              px(15, 24, corLaranja);
              px(14, 25, corCinza);
              px(15, 25, corCinza);
              px(14, 26, corCinza);
              px(15, 26, corCinza);
              px(13, 27, corCinza);
              px(14, 27, corCinza);
              px(15, 27, corCinza);
              px(16, 27, corCinza);
              px(13, 28, corCinzaEscuro);
              px(16, 28, corCinzaEscuro);

              ctx.restore();
          }

          function drawAlien(x, y, w, h, color) {
            ctx.save();
            ctx.translate(x, y);

            // Corpo principal do alien
            ctx.fillStyle = color;
            ctx.beginPath();
            ctx.ellipse(0, 0, w / 2, h / 3, 0, 0, Math.PI * 2);
            ctx.fill();

            // Olhos
            ctx.fillStyle = '#fff';
            ctx.beginPath();
            ctx.arc(-w / 4, -h / 6, w / 8, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.arc(w / 4, -h / 6, w / 8, 0, Math.PI * 2);
            ctx.fill();

            // Detalhes nos olhos
            ctx.fillStyle = '#000';
            ctx.beginPath();
            ctx.arc(-w / 4, -h / 6, w / 16, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.arc(w / 4, -h / 6, w / 16, 0, Math.PI * 2);
            ctx.fill();

            // "Antenas" ou detalhes extras
            ctx.strokeStyle = color;
            ctx.lineWidth = 2 * DPR;
            ctx.beginPath();
            ctx.moveTo(-w / 3, -h / 2);
            ctx.lineTo(-w / 4, -h / 3);
            ctx.moveTo(w / 3, -h / 2);
            ctx.lineTo(w / 4, -h / 3);
            ctx.stroke();

            ctx.restore();
          }

          // Carrega as imagens dos planetas ao iniciar
          loadPlanetImages();
          requestAnimationFrame(loop);
        })();
    </script>
</body>
</html>
