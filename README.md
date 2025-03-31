<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Neon 3D Editor Premium</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;700;900&display=swap');
        
        :root {
            --neon-blue: #00fffc;
            --neon-pink: #ff00fc;
            --neon-yellow: #fcff00;
            --neon-purple: #9d00ff;
            --glow-speed: 1.8s;
        }
        
        body {
            margin: 0;
            padding: 0;
            background: #0a0a0a;
            font-family: 'Poppins', sans-serif;
            overflow: hidden;
            transition: background 0.5s;
        }
        
        /* Tela Principal - Efeito Aprimorado */
        .main-screen {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            transition: all 0.5s;
            position: relative;
        }
        
        .neon-text {
            color: #fff;
            font-size: 6em;
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: 8px;
            text-shadow: 
                0 0 10px var(--neon-blue),
                0 0 20px var(--neon-blue),
                0 0 40px var(--neon-blue),
                0 0 80px var(--neon-blue),
                0 0 160px var(--neon-blue);
            animation: neon-glow var(--glow-speed) ease-in-out infinite alternate;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            margin: 20px 0;
            min-height: 1.2em;
            cursor: pointer;
            padding: 0 40px;
            text-align: center;
            position: relative;
            z-index: 2;
        }
        
        .neon-text:hover {
            transform: scale(1.08) rotate(-1deg);
            text-shadow: 
                0 0 15px var(--neon-pink),
                0 0 30px var(--neon-pink),
                0 0 60px var(--neon-pink),
                0 0 120px var(--neon-pink),
                0 0 240px var(--neon-pink);
        }
        
        .hint {
            color: rgba(255, 255, 255, 0.5);
            font-size: 1.2em;
            margin-top: 20px;
            text-shadow: 0 0 10px rgba(0, 255, 255, 0.3);
            animation: fadeInOut 3s ease-in-out infinite;
        }
        
        /* Tela de Edição - Estilo Premium */
        .edit-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            display: none;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 100;
            backdrop-filter: blur(10px);
            opacity: 0;
            transition: opacity 0.5s ease-out;
        }
        
        .edit-container {
            width: 90%;
            max-width: 800px;
            padding: 50px;
            background: rgba(10, 10, 10, 0.9);
            border-radius: 25px;
            box-shadow: 0 0 50px rgba(0, 255, 255, 0.5);
            border: 3px solid transparent;
            animation: border-glow 4s linear infinite;
            transform: scale(0.9);
            transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: relative;
            overflow: hidden;
        }
        
        .edit-container::before {
            content: '';
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: linear-gradient(45deg, var(--neon-blue), var(--neon-pink), var(--neon-yellow), var(--neon-purple));
            z-index: -1;
            border-radius: 25px;
            animation: animate 8s linear infinite;
            opacity: 0.7;
        }
        
        .edit-container::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(45deg, var(--neon-blue), var(--neon-pink), var(--neon-yellow), var(--neon-purple));
            z-index: -2;
            border-radius: 25px;
            animation: animate 16s linear infinite;
            opacity: 0.3;
            filter: blur(30px);
        }
        
        .input-group {
            position: relative;
            margin-bottom: 40px;
        }
        
        .input-group input {
            width: 100%;
            padding: 25px;
            font-size: 1.8em;
            background: rgba(255, 255, 255, 0.05);
            border: 2px solid rgba(0, 255, 252, 0.3);
            border-radius: 15px;
            color: #fff;
            outline: none;
            transition: all 0.4s;
            font-weight: 700;
            letter-spacing: 2px;
        }
        
        .input-group input:focus {
            background: rgba(255, 255, 255, 0.1);
            border-color: rgba(0, 255, 252, 0.8);
            box-shadow: 0 0 30px rgba(0, 255, 255, 0.6);
            transform: scale(1.02);
        }
        
        .input-group label {
            position: absolute;
            top: -15px;
            left: 20px;
            background: #0a0a0a;
            padding: 0 15px;
            color: var(--neon-blue);
            font-size: 1.2em;
            text-shadow: 0 0 10px rgba(0, 255, 255, 0.7);
            font-weight: 700;
        }
        
        .btn-container {
            display: flex;
            justify-content: space-between;
            gap: 20px;
        }
        
        .btn {
            padding: 18px 35px;
            background: linear-gradient(45deg, var(--neon-blue), var(--neon-purple));
            border: none;
            border-radius: 12px;
            color: #fff;
            font-size: 1.3em;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 0 20px rgba(0, 255, 255, 0.4);
            flex: 1;
            text-align: center;
            position: relative;
            overflow: hidden;
            z-index: 1;
        }
        
        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: 0.5s;
            z-index: -1;
        }
        
        .btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 0 30px rgba(0, 255, 255, 0.7);
        }
        
        .btn:hover::before {
            left: 100%;
        }
        
        .btn:active {
            transform: translateY(0);
        }
        
        .btn-cancel {
            background: linear-gradient(45deg, #ff3c3c, #ff00fc);
        }
        
        /* Animações Premium */
        @keyframes neon-glow {
            0% {
                text-shadow: 
                    0 0 10px var(--neon-blue),
                    0 0 20px var(--neon-blue),
                    0 0 40px var(--neon-blue),
                    0 0 80px var(--neon-blue),
                    0 0 160px var(--neon-blue);
            }
            25% {
                text-shadow: 
                    0 0 15px var(--neon-pink),
                    0 0 30px var(--neon-pink),
                    0 0 60px var(--neon-pink),
                    0 0 120px var(--neon-pink),
                    0 0 240px var(--neon-pink);
            }
            50% {
                text-shadow: 
                    0 0 12px var(--neon-yellow),
                    0 0 24px var(--neon-yellow),
                    0 0 48px var(--neon-yellow),
                    0 0 96px var(--neon-yellow),
                    0 0 192px var(--neon-yellow);
            }
            75% {
                text-shadow: 
                    0 0 18px var(--neon-purple),
                    0 0 36px var(--neon-purple),
                    0 0 72px var(--neon-purple),
                    0 0 144px var(--neon-purple),
                    0 0 288px var(--neon-purple);
            }
            100% {
                text-shadow: 
                    0 0 10px var(--neon-blue),
                    0 0 20px var(--neon-blue),
                    0 0 40px var(--neon-blue),
                    0 0 80px var(--neon-blue),
                    0 0 160px var(--neon-blue);
            }
        }
        
        @keyframes animate {
            0% {
                filter: hue-rotate(0deg);
            }
            100% {
                filter: hue-rotate(360deg);
            }
        }
        
        @keyframes fadeInOut {
            0%, 100% {
                opacity: 0.5;
            }
            50% {
                opacity: 1;
            }
        }
        
        @keyframes border-glow {
            0% {
                box-shadow: 0 0 30px var(--neon-blue);
                border-color: var(--neon-blue);
            }
            25% {
                box-shadow: 0 0 40px var(--neon-pink);
                border-color: var(--neon-pink);
            }
            50% {
                box-shadow: 0 0 50px var(--neon-yellow);
                border-color: var(--neon-yellow);
            }
            75% {
                box-shadow: 0 0 40px var(--neon-purple);
                border-color: var(--neon-purple);
            }
            100% {
                box-shadow: 0 0 30px var(--neon-blue);
                border-color: var(--neon-blue);
            }
        }
        
        /* Efeito de Partículas Avançado */
        .particles {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }
        
        .particle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: var(--neon-blue);
            border-radius: 50%;
            animation: float linear infinite;
            opacity: 0;
            filter: blur(1px);
        }
        
        @keyframes float {
            0% {
                transform: translateY(100vh) translateX(calc(var(--random-x) * 100px)) scale(0.5);
                opacity: 0;
            }
            20% {
                opacity: var(--particle-opacity);
            }
            80% {
                opacity: var(--particle-opacity);
            }
            100% {
                transform: translateY(-100px) translateX(calc(var(--random-x) * 200px)) scale(1.2);
                opacity: 0;
            }
        }
        
        /* Responsivo Aprimorado */
        @media (max-width: 768px) {
            .neon-text {
                font-size: 3em;
                letter-spacing: 4px;
                padding: 0 20px;
            }
            
            .edit-container {
                padding: 30px;
                border-radius: 15px;
            }
            
            .input-group input {
                font-size: 1.3em;
                padding: 18px;
            }
            
            .btn {
                padding: 15px 25px;
                font-size: 1.1em;
            }
            
            .hint {
                font-size: 1em;
            }
        }
    </style>
</head>
<body>
    <div class="particles" id="particles"></div>
    
    <!-- Tela Principal -->
    <div class="main-screen" id="mainScreen">
        <div id="displayText" class="neon-text">NEON 3D</div>
        <div class="hint">Clique no texto para editar</div>
    </div>
    
    <!-- Tela de Edição -->
    <div class="edit-screen" id="editScreen">
        <div class="edit-container">
            <div class="input-group">
                <label for="textInput">EDITAR TEXTO NEON</label>
                <input type="text" id="textInput" placeholder="DIGITE SEU TEXTO...">
            </div>
            <div class="btn-container">
                <button id="saveBtn" class="btn">SALVAR</button>
                <button id="cancelBtn" class="btn btn-cancel">CANCELAR</button>
            </div>
        </div>
    </div>

    <script>
        // Criar partículas flutuantes avançadas
        const particlesContainer = document.getElementById('particles');
        const particleCount = 80;
        
        for (let i = 0; i < particleCount; i++) {
            const particle = document.createElement('div');
            particle.classList.add('particle');
            
            const posX = Math.random() * 100;
            const duration = Math.random() * 15 + 10;
            const delay = Math.random() * 10;
            const size = Math.random() * 4 + 1;
            const opacity = Math.random() * 0.7 + 0.3;
            const colors = ['#00fffc', '#ff00fc', '#fcff00', '#9d00ff'];
            const color = colors[Math.floor(Math.random() * colors.length)];
            
            particle.style.left = `${posX}%`;
            particle.style.width = `${size}px`;
            particle.style.height = `${size}px`;
            particle.style.background = color;
            particle.style.animationDuration = `${duration}s`;
            particle.style.animationDelay = `${delay}s`;
            particle.style.setProperty('--random-x', Math.random() * 4 - 2);
            particle.style.setProperty('--particle-opacity', opacity);
            
            particlesContainer.appendChild(particle);
        }
        
        // Elementos da interface
        const displayText = document.getElementById('displayText');
        const mainScreen = document.getElementById('mainScreen');
        const editScreen = document.getElementById('editScreen');
        const textInput = document.getElementById('textInput');
        const saveBtn = document.getElementById('saveBtn');
        const cancelBtn = document.getElementById('cancelBtn');
        
        // Efeito de digitação inicial
        function typeWriter(text, element, speed, callback) {
            let i = 0;
            element.textContent = '';
            
            function typing() {
                if (i < text.length) {
                    element.textContent += text.charAt(i);
                    i++;
                    setTimeout(typing, speed);
                } else if (callback) {
                    callback();
                }
            }
            
            typing();
        }
        
        // Abrir tela de edição com animação
        function openEditor() {
            mainScreen.style.filter = 'blur(5px) brightness(0.7)';
            editScreen.style.display = 'flex';
            setTimeout(() => {
                editScreen.style.opacity = '1';
                document.querySelector('.edit-container').style.transform = 'scale(1)';
            }, 10);
            textInput.value = displayText.textContent;
            setTimeout(() => textInput.focus(), 500);
        }
        
        // Fechar tela de edição com animação
        function closeEditor() {
            editScreen.style.opacity = '0';
            document.querySelector('.edit-container').style.transform = 'scale(0.9)';
            setTimeout(() => {
                editScreen.style.display = 'none';
                mainScreen.style.filter = 'none';
            }, 500);
        }
        
        // Eventos
        displayText.addEventListener('click', openEditor);
        
        saveBtn.addEventListener('click', function() {
            const newText = textInput.value.trim().toUpperCase() || 'NEON 3D';
            typeWriter(newText, displayText, 50);
            closeEditor();
        });
        
        cancelBtn.addEventListener('click', closeEditor);
        
        // Permitir salvar com Enter e escapar com ESC
        textInput.addEventListener('keydown', function(e) {
            if (e.key === 'Enter') {
                saveBtn.click();
            } else if (e.key === 'Escape') {
                closeEditor();
            }
        });
        
        // Fechar ao clicar fora do container de edição
        editScreen.addEventListener('click', function(e) {
            if (e.target === editScreen) {
                closeEditor();
            }
        });
        
        // Efeito de digitação inicial
        window.addEventListener('load', function() {
            typeWriter('NEON 3D', displayText, 150);
        });
    </script>
</body>
</html>
</html>
