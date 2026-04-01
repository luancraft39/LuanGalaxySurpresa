<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LuanGalaxy IA - FULL MENU & LED</title>
    <style>
        :root {
            --primary: #8a2be2; --accent: #fedd00; --blue: #012169;
            --led-color: #bc13fe;
        }

        body {
            margin: 0; padding: 0; font-family: 'Segoe UI', sans-serif;
            background: radial-gradient(circle, #2e004b 0%, #000 100%);
            height: 100vh; overflow: hidden; display: flex;
            flex-direction: column; align-items: center; justify-content: center;
            color: white; transition: 0.3s;
            border: 0px solid transparent; 
            box-sizing: border-box;
        }

        /* TELA DE ROTAÇÃO PARA CELULAR */
        #rotation-overlay {
            display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: #0a001a; z-index: 9999; flex-direction: column;
            align-items: center; justify-content: center; text-align: center; color: white;
        }
        #rotation-overlay img { width: 80px; margin-bottom: 20px; animation: rotateAnim 2s infinite; filter: invert(1); }
        @keyframes rotateAnim { 0% { transform: rotate(0deg); } 50% { transform: rotate(90deg); } 100% { transform: rotate(0deg); } }

        @media (orientation: portrait) and (max-width: 900px) {
            #rotation-overlay { display: flex; }
        }

        #fxCanvas { position: absolute; top: 0; left: 0; pointer-events: none; z-index: 2; }

        /* SISTEMA DE LEDS */
        .led-mode {
            border: 12px solid #bc13fe !important;
            animation: global-rgb 2s linear infinite;
            box-shadow: inset 0 0 20px #bc13fe, 0 0 30px #bc13fe;
        }

        @keyframes global-rgb {
            0% { border-color: #ff0000; box-shadow: inset 0 0 30px #ff0000, 0 0 40px #ff0000; }
            25% { border-color: #bc13fe; box-shadow: inset 0 0 30px #bc13fe, 0 0 40px #bc13fe; }
            50% { border-color: #00ffff; box-shadow: inset 0 0 30px #00ffff, 0 0 40px #00ffff; }
            75% { border-color: #ffff00; box-shadow: inset 0 0 30px #ffff00, 0 0 40px #ffff00; }
            100% { border-color: #ff0000; box-shadow: inset 0 0 30px #ff0000, 0 0 40px #ff0000; }
        }

        /* DJ SETUP */
        #dj-world { display: none; position: absolute; bottom: 140px; z-index: 6; align-items: flex-end; gap: 30px; }
        .speaker-stack {
            width: 100px; height: 220px; background: #111; border: 4px solid #333;
            border-radius: 15px; display: flex; flex-direction: column; align-items: center; justify-content: space-around;
            animation: bass-pulse 0.2s infinite;
        }
        .sub { width: 70px; height: 70px; border-radius: 50%; background: #222; border: 3px solid var(--accent); }
        @keyframes bass-pulse { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.08); } }

        #dj-booth {
            width: 550px; height: 130px; background: #000;
            border: 4px solid #fff; border-radius: 25px; position: relative;
            box-shadow: 0 0 50px var(--primary);
        }
        #dj-booth::before {
            content: 'LUANGALAXY DJ'; position: absolute; width: 100%; text-align: center;
            top: 35%; font-weight: 900; font-size: 28px; color: white; text-shadow: 0 0 20px var(--led-color);
        }

        /* MENU E BOTÕES */
        #btn-categorias {
            position: absolute; top: 30px; left: 30px;
            background: var(--primary); color: white; border: 2px solid var(--accent);
            padding: 12px 25px; border-radius: 30px; cursor: pointer; z-index: 100; font-weight: bold;
        }

        #menu-categorias {
            position: absolute; top: 95px; left: 30px;
            background: rgba(15, 0, 30, 0.98); border: 2px solid var(--primary);
            padding: 20px; border-radius: 15px; display: none; width: 320px; 
            max-height: 75vh; overflow-y: auto; z-index: 99;
        }

        .cat-h { color: var(--accent); font-weight: bold; text-transform: uppercase; display: block; margin-top: 15px; border-bottom: 1px solid #444; padding-bottom: 5px; }
        .cat-i { list-style: none; padding: 0; margin: 8px 0; }
        .cat-i li { padding: 8px; font-size: 14px; cursor: pointer; border-bottom: 1px solid #222; transition: 0.2s; }
        .cat-i li:hover { background: rgba(138, 43, 226, 0.2); color: var(--accent); padding-left: 15px; }

        /* NPC */
        #npc-scene { position: relative; z-index: 5; display: flex; flex-direction: column; align-items: center; margin-bottom: 100px; }
        #npc-img { height: 360px; filter: drop-shadow(0 0 20px var(--primary)); transition: 0.3s; }
        .rave-active { animation: rave-jump 0.3s infinite; filter: hue-rotate(270deg) brightness(1.5) !important; }
        @keyframes rave-jump { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-25px); } }

        #speech-bubble {
            background: white; color: black; padding: 18px 28px; border-radius: 25px;
            font-weight: bold; margin-bottom: 25px; box-shadow: 0 10px 30px rgba(0,0,0,0.7);
        }

        #chat-area { position: absolute; bottom: 30px; width: 90%; max-width: 750px; z-index: 10; }
        #chat-ctrl { 
            display: flex; gap: 15px; background: rgba(0,0,0,0.95); padding: 15px; 
            border-radius: 60px; border: 3px solid var(--primary); 
        }
        #u-input { flex: 1; background: transparent; border: none; color: white; outline: none; font-size: 17px; }
        .btn-s { background: var(--accent); border: none; padding: 10px 30px; border-radius: 30px; cursor: pointer; font-weight: bold; }
    </style>
</head>
<body id="site-main">

    <div id="rotation-overlay">
        <img src="https://cdn-icons-png.flaticon.com/512/625/625944.png" alt="Rotate">
        <h2>VIRE SEU CELULAR</h2>
        <p>Para uma experiência completa, use o modo paisagem.</p>
    </div>

    <canvas id="fxCanvas"></canvas>
    <audio id="phonkMusic" src="https://files.catbox.moe/9m30t6.mp4"></audio>

    <div id="dj-world">
        <div class="speaker-stack"><div class="sub"></div><div class="sub"></div></div>
        <div id="dj-booth"></div>
        <div class="speaker-stack"><div class="sub"></div><div class="sub"></div></div>
    </div>

    <button id="btn-categorias" onclick="toggleMenu()">📂 MENU LENDÁRIO</button>
    <div id="menu-categorias"></div>

    <div id="npc-scene">
        <div id="speech-bubble">Tudo pronto, Fundador. Mande o comando /phonkgalaxy!</div>
        <img src="https://files.catbox.moe/kjdwkl.png" alt="LuanGalaxy" id="npc-img">
    </div>

    <div id="chat-area">
        <div id="chat-ctrl">
            <input type="text" id="u-input" placeholder="Digite um comando..." autocomplete="off">
            <button class="btn-s" onclick="sendMessage()">ENVIAR</button>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('fxCanvas');
        const ctx = canvas.getContext('2d');
        const music = document.getElementById('phonkMusic');
        const site = document.getElementById('site-main');
        const npc = document.getElementById('npc-img');
        const dj = document.getElementById('dj-world');
        const menu = document.getElementById('menu-categorias');
        const inputField = document.getElementById('u-input');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        // TODAS AS SUAS PERGUNTAS DE VOLTA AQUI:
        const db = {
            "👤 Identidade": [
                { q: "Quem é você?", r: "Eu sou o LuanGalaxy, fundador do Lendário Studio e criador do Lendário OS!" },
                { q: "Qual seu nome real?", r: "No mundo dev eu sou o LuanGalaxy, o mestre do Lendário Studio!" }
            ],
            "🎮 Studio & Jogos": [
                { q: "O que é Lendário Studio?", r: "É o meu estúdio oficial de desenvolvimento de jogos e sistemas web!" },
                { q: "Fale sobre o Lendário Dash", r: "O Lendário Dash v10.1 é um dos meus projetos de maior sucesso!" }
            ],
            "💻 Tecnologia": [
                { q: "O que é o Lendário OS?", r: "É o sistema operacional que eu desenvolvi para rodar 100% no navegador!" },
                { q: "O que é JavaScript?", r: "É a linguagem principal que eu uso para dar vida a tudo aqui!" }
            ],
            "⌨️ Comandos Secretos": [
                { q: "/phonkgalaxy", r: "LEDS ATIVADOS! O SITE AGORA ESTÁ EM MODO RAVE ROXO!" },
                { q: "/clima", r: "Em Ji-Paraná o clima é de muito trabalho e inovação!" },
                { q: "/versao", r: "LuanGalaxy IA v2026.4 | LED Border Edition" }
            ]
        };

        function initMenu() {
            menu.innerHTML = "";
            for (const [cat, items] of Object.entries(db)) {
                const title = document.createElement('span'); title.className = 'cat-h'; title.innerText = cat;
                menu.appendChild(title);
                const list = document.createElement('ul'); list.className = 'cat-i';
                items.forEach(item => {
                    const li = document.createElement('li'); li.innerText = item.q;
                    li.onclick = () => { inputField.value = item.q; sendMessage(); };
                    list.appendChild(li);
                });
                menu.appendChild(list);
            }
        }

        let particles = [];
        let effectsActive = false;

        class Particle {
            constructor(x, y, color, speed) {
                this.x = x; this.y = y; this.color = color;
                this.size = Math.random() * 5 + 1;
                this.speedX = (Math.random() - 0.5) * speed;
                this.speedY = (Math.random() - 0.5) * speed;
                this.life = 1.0;
                this.decay = Math.random() * 0.02 + 0.01;
            }
            update() { this.x += this.speedX; this.y += this.speedY; this.life -= this.decay; }
            draw() {
                ctx.globalAlpha = this.life;
                ctx.fillStyle = this.color;
                ctx.beginPath(); ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2); ctx.fill();
            }
        }

        function createFirework() {
            if (!effectsActive) return;
            const x = Math.random() * canvas.width;
            const y = Math.random() * (canvas.height * 0.6);
            const colors = ['#bc13fe', '#8a2be2', '#00ffff', '#ffffff'];
            const color = colors[Math.floor(Math.random() * colors.length)];
            for (let i = 0; i < 30; i++) particles.push(new Particle(x, y, color, 12));
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            if (effectsActive && Math.random() > 0.95) createFirework();
            particles.forEach((p, i) => {
                p.update(); p.draw();
                if (p.life <= 0) particles.splice(i, 1);
            });
            requestAnimationFrame(animate);
        }
        animate();

        function toggleMenu() { menu.style.display = menu.style.display === 'block' ? 'none' : 'block'; }

        function sendMessage() {
            const val = inputField.value.trim();
            const bubble = document.getElementById('speech-bubble');
            if (!val) return;

            if (val.toLowerCase() === "/phonkgalaxy") {
                music.play();
                effectsActive = true;
                site.classList.add('led-mode');
                dj.style.display = 'flex';
                npc.classList.add('rave-active');
                bubble.innerText = "SISTEMA DE LEDS E FOGOS ATIVADO COM SUCESSO! 🟣⚡";
            } else {
                let found = false;
                for (const cat in db) {
                    const item = db[cat].find(i => i.q.toLowerCase() === val.toLowerCase());
                    if (item) { bubble.innerText = item.r; found = true; break; }
                }
                if (!found) bubble.innerText = "Comando não reconhecido. Use o menu lateral!";
            }
            inputField.value = "";
            menu.style.display = 'none';
        }

        initMenu();
        inputField.addEventListener("keypress", (e) => { if (e.key === "Enter") sendMessage(); });
        window.addEventListener('resize', () => { canvas.width = window.innerWidth; canvas.height = window.innerHeight; });
    </script>
</body>
</html>
