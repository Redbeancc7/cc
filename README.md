<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>梦核千禧年电脑 - Dreamcore Y2K Desktop</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=VT323&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        :root {
            --dreamcore-pink: #ffb6c1;
            --dreamcore-purple: #dda0dd;
            --dreamcore-blue: #87ceeb;
            --vaporwave-cyan: #00ffff;
            --vaporwave-magenta: #ff00ff;
            --vaporwave-purple: #9b59b6;
            --cyber-green: #00ff00;
            --soft-cream: #fff0f5;
        }
        
        body {
            min-height: 100vh;
            background: linear-gradient(135deg, #1a0a2e 0%, #2d1b4e 25%, #4a2c6a 50%, #1a0a2e 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'VT323', monospace;
            overflow: hidden;
            position: relative;
        }
        
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: 
                repeating-linear-gradient(
                    0deg,
                    transparent,
                    transparent 2px,
                    rgba(255, 182, 193, 0.03) 2px,
                    rgba(255, 182, 193, 0.03) 4px
                );
            pointer-events: none;
            z-index: 1000;
        }
        
        .floating-orbs {
            position: fixed;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }
        
        .orb {
            position: absolute;
            border-radius: 50%;
            filter: blur(60px);
            animation: float 8s ease-in-out infinite;
        }
        
        .orb:nth-child(1) {
            width: 300px;
            height: 300px;
            background: radial-gradient(circle, rgba(255, 182, 193, 0.4) 0%, transparent 70%);
            top: 10%;
            left: 5%;
            animation-delay: 0s;
        }
        
        .orb:nth-child(2) {
            width: 400px;
            height: 400px;
            background: radial-gradient(circle, rgba(221, 160, 221, 0.3) 0%, transparent 70%);
            top: 50%;
            right: 10%;
            animation-delay: -2s;
        }
        
        .orb:nth-child(3) {
            width: 250px;
            height: 250px;
            background: radial-gradient(circle, rgba(0, 255, 255, 0.2) 0%, transparent 70%);
            bottom: 20%;
            left: 20%;
            animation-delay: -4s;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0) scale(1); }
            50% { transform: translateY(-30px) scale(1.1); }
        }
        
        .desktop-container {
            position: relative;
            z-index: 1;
            width: 100%;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        
        .monitor {
            background: linear-gradient(145deg, #d4d4d4 0%, #a8a8a8 50%, #808080 100%);
            border-radius: 30px;
            padding: 25px;
            box-shadow: 
                0 0 0 8px #606060,
                0 0 0 12px #404040,
                0 20px 60px rgba(0, 0, 0, 0.5),
                inset 0 2px 10px rgba(255, 255, 255, 0.3);
            position: relative;
        }
        
        .monitor::before {
            content: 'DREAMCORE™';
            position: absolute;
            bottom: 8px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 12px;
            color: #404040;
            letter-spacing: 3px;
            font-family: 'VT323', monospace;
        }
        
        .screen-bezel {
            background: #1a1a2e;
            border-radius: 15px;
            padding: 15px;
            box-shadow: inset 0 0 30px rgba(0, 0, 0, 0.8);
        }
        
        .screen {
            width: 500px;
            height: 380px;
            background: linear-gradient(180deg, #0d0d1a 0%, #1a1a2e 100%);
            border-radius: 8px;
            position: relative;
            overflow: hidden;
            box-shadow: 
                inset 0 0 100px rgba(255, 182, 193, 0.1),
                0 0 20px rgba(0, 255, 255, 0.2);
        }
        
        .screen::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: repeating-linear-gradient(
                0deg,
                transparent,
                transparent 1px,
                rgba(0, 255, 255, 0.02) 1px,
                rgba(0, 255, 255, 0.02) 2px
            );
            pointer-events: none;
            z-index: 10;
        }
        
        .screen::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: radial-gradient(ellipse at center, transparent 0%, rgba(0, 0, 0, 0.3) 100%);
            pointer-events: none;
            z-index: 11;
        }
        
        .chat-container {
            width: 100%;
            height: 100%;
            padding: 15px;
            display: flex;
            flex-direction: column;
        }
        
        .chat-header {
            background: linear-gradient(90deg, rgba(155, 89, 182, 0.8), rgba(255, 0, 255, 0.6));
            padding: 10px 15px;
            border-radius: 8px 8px 0 0;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .chat-avatar {
            width: 35px;
            height: 35px;
            background: linear-gradient(135deg, #ff6b9d, #c44569);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            box-shadow: 0 0 15px rgba(255, 107, 157, 0.5);
        }
        
        .chat-name {
            color: #fff;
            font-size: 16px;
            text-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
        }
        
        .chat-status {
            color: #00ff00;
            font-size: 12px;
            margin-left: auto;
        }
        
        .chat-messages {
            flex: 1;
            padding: 15px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 12px;
        }
        
        .message {
            max-width: 85%;
            padding: 10px 15px;
            border-radius: 15px;
            font-size: 14px;
            line-height: 1.4;
            animation: messageAppear 0.3s ease;
        }
        
        @keyframes messageAppear {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .message.received {
            background: #000000;
            color: #fff;
            align-self: flex-start;
            border-bottom-left-radius: 5px;
            box-shadow: 
                0 0 15px rgba(0, 255, 255, 0.3),
                inset 0 0 20px rgba(255, 0, 255, 0.1);
        }
        
        .message.sent {
            background: linear-gradient(135deg, rgba(0, 255, 255, 0.3), rgba(255, 0, 255, 0.3));
            color: #fff;
            align-self: flex-end;
            border-bottom-right-radius: 5px;
            box-shadow: 0 0 15px rgba(0, 255, 255, 0.3);
        }
        
        .chat-input-area {
            display: flex;
            gap: 10px;
            padding-top: 10px;
        }
        
        .chat-input {
            flex: 1;
            background: rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(0, 255, 255, 0.3);
            border-radius: 20px;
            padding: 10px 15px;
            color: #fff;
            font-family: 'VT323', monospace;
            font-size: 14px;
            outline: none;
            transition: all 0.3s;
        }
        
        .chat-input:focus {
            border-color: #00ffff;
            box-shadow: 0 0 20px rgba(0, 255, 255, 0.4);
        }
        
        .send-btn {
            background: linear-gradient(135deg, #ff6b9d, #c44569);
            border: none;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s;
            box-shadow: 0 0 15px rgba(255, 107, 157, 0.5);
        }
        
        .send-btn:hover {
            transform: scale(1.1);
            box-shadow: 0 0 25px rgba(255, 107, 157, 0.8);
        }
        
        .send-btn svg {
            width: 20px;
            height: 20px;
            fill: #fff;
        }
        
        .keyboard-container {
            margin-top: 30px;
            perspective: 500px;
        }
        
        .keyboard {
            background: linear-gradient(180deg, #c0c0c0 0%, #a0a0a0 50%, #808080 100%);
            border-radius: 10px;
            padding: 15px;
            box-shadow: 
                0 10px 30px rgba(0, 0, 0, 0.4),
                inset 0 1px 0 rgba(255, 255, 255, 0.5);
            transform: rotateX(5deg);
        }
        
        .keyboard-row {
            display: flex;
            justify-content: center;
            gap: 4px;
            margin-bottom: 4px;
        }
        
        .key {
            background: linear-gradient(180deg, #e8e8e8 0%, #d0d0d0 50%, #b8b8b8 100%);
            border: 1px solid #888;
            border-radius: 5px;
            min-width: 32px;
            height: 32px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
            color: #333;
            cursor: pointer;
            transition: all 0.1s;
            box-shadow: 
                0 3px 0 #666,
                0 4px 5px rgba(0, 0, 0, 0.3);
            font-family: 'VT323', monospace;
        }
        
        .key:hover {
            background: linear-gradient(180deg, #fff 0%, #e8e8e8 50%, #d0d0d0 100%);
        }
        
        .key:active, .key.pressed {
            transform: translateY(2px);
            box-shadow: 
                0 1px 0 #666,
                0 2px 3px rgba(0, 0, 0, 0.3);
            background: linear-gradient(180deg, #d0d0d0 0%, #c0c0c0 50%, #b0b0b0 100%);
        }
        
        .key.space {
            min-width: 180px;
        }
        
        .key.backspace, .key.enter {
            min-width: 60px;
        }
        
        .key.shift {
            min-width: 50px;
        }
        
        .sticky-note {
            position: absolute;
            width: 150px;
            min-height: 100px;
            padding: 15px;
            cursor: grab;
            user-select: none;
            z-index: 100;
            transition: transform 0.2s, box-shadow 0.2s;
            font-family: 'VT323', monospace;
        }
        
        .sticky-note:active {
            cursor: grabbing;
        }
        
        .sticky-note:hover {
            transform: scale(1.05) rotate(0deg) !important;
        }
        
        .sticky-note.dreamcore {
            background: linear-gradient(135deg, #ffb6c1 0%, #dda0dd 100%);
            box-shadow: 
                0 5px 20px rgba(255, 182, 193, 0.5),
                0 0 30px rgba(221, 160, 221, 0.3);
        }
        
        .sticky-note.vaporwave {
            background: linear-gradient(135deg, #00ffff 0%, #ff00ff 100%);
            box-shadow: 
                0 5px 20px rgba(0, 255, 255, 0.5),
                0 0 30px rgba(255, 0, 255, 0.3);
        }
        
        .sticky-note.cyberpunk {
            background: linear-gradient(135deg, #1a1a2e 0%, #4a2c6a 100%);
            border: 2px solid #00ffff;
            box-shadow: 
                0 5px 20px rgba(0, 255, 255, 0.5),
                0 0 30px rgba(255, 0, 255, 0.3),
                inset 0 0 20px rgba(0, 255, 255, 0.1);
        }
        
        .sticky-note.cyberpunk .note-text {
            color: #00ffff;
            text-shadow: 0 0 10px #00ffff;
        }
        
        .sticky-note::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 20px;
            background: rgba(0, 0, 0, 0.1);
            border-radius: inherit;
            border-bottom-left-radius: 0;
            border-bottom-right-radius: 0;
        }
        
        .note-text {
            font-size: 14px;
            color: #333;
            word-wrap: break-word;
            text-shadow: 1px 1px 0 rgba(255, 255, 255, 0.3);
            margin-top: 10px;
        }
        
        .note-time {
            font-size: 10px;
            color: rgba(0, 0, 0, 0.5);
            margin-top: 10px;
            text-align: right;
        }
        
        .sticky-note.cyberpunk .note-time {
            color: rgba(0, 255, 255, 0.7);
        }
        
        .note-glow {
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            border-radius: inherit;
            opacity: 0;
            transition: opacity 0.3s;
            pointer-events: none;
        }
        
        .sticky-note:hover .note-glow {
            opacity: 1;
            animation: glowPulse 1.5s ease-in-out infinite;
        }
        
        @keyframes glowPulse {
            0%, 100% { box-shadow: 0 0 20px rgba(255, 182, 193, 0.8); }
            50% { box-shadow: 0 0 40px rgba(0, 255, 255, 0.8); }
        }
        
        .grid-bg {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-image: 
                linear-gradient(rgba(0, 255, 255, 0.05) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 255, 255, 0.05) 1px, transparent 1px);
            background-size: 50px 50px;
            pointer-events: none;
            z-index: 0;
        }
        
        .stars {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            pointer-events: none;
            z-index: 0;
        }
        
        .star {
            position: absolute;
            width: 2px;
            height: 2px;
            background: #fff;
            border-radius: 50%;
            animation: twinkle 2s ease-in-out infinite;
        }
        
        @keyframes twinkle {
            0%, 100% { opacity: 0.3; }
            50% { opacity: 1; }
        }
        
        .note-spawn-animation {
            animation: noteSpawn 0.5s ease-out;
        }
        
        @keyframes noteSpawn {
            0% {
                opacity: 0;
                transform: scale(0.5) rotate(180deg);
            }
            100% {
                opacity: 1;
                transform: scale(1) rotate(var(--rotation, 0deg));
            }
        }
        
        ::-webkit-scrollbar {
            width: 6px;
        }
        
        ::-webkit-scrollbar-track {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 3px;
        }
        
        ::-webkit-scrollbar-thumb {
            background: linear-gradient(180deg, #ff6b9d, #c44569);
            border-radius: 3px;
        }
        
        .power-led {
            position: absolute;
            bottom: 15px;
            right: 30px;
            width: 8px;
            height: 8px;
            background: #00ff00;
            border-radius: 50%;
            box-shadow: 0 0 10px #00ff00;
            animation: ledBlink 2s ease-in-out infinite;
        }
        
        @keyframes ledBlink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        
        .monitor-stand {
            width: 80px;
            height: 40px;
            background: linear-gradient(180deg, #808080 0%, #606060 100%);
            margin: 0 auto;
            border-radius: 0 0 10px 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .monitor-base {
            width: 150px;
            height: 15px;
            background: linear-gradient(180deg, #606060 0%, #404040 100%);
            margin: 0 auto;
            border-radius: 5px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
    </style>
</head>
<body>
    <div class="grid-bg"></div>
    <div class="floating-orbs">
        <div class="orb"></div>
        <div class="orb"></div>
        <div class="orb"></div>
    </div>
    <div class="stars" id="stars"></div>
    
    <div class="desktop-container" id="desktop">
        <div class="monitor">
            <div class="power-led"></div>
            <div class="screen-bezel">
                <div class="screen">
                    <div class="chat-container">
                        <div class="chat-header">
                            <div class="chat-avatar">♡</div>
                            <span class="chat-name">Dream Entity</span>
                            <span class="chat-status">● 在线</span>
                        </div>
                        <div class="chat-messages" id="chatMessages">
                            <div class="message received">i potato you</div>
                        </div>
                        <div class="chat-input-area">
                            <input type="text" class="chat-input" id="chatInput" placeholder="输入消息..." autocomplete="off">
                            <button class="send-btn" id="sendBtn">
                                <svg viewBox="0 0 24 24">
                                    <path d="M2.01 21L23 12 2.01 3 2 10l15 2-15 2z"/>
                                </svg>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="monitor-stand"></div>
        <div class="monitor-base"></div>
        
        <div class="keyboard-container">
            <div class="keyboard" id="keyboard">
                <div class="keyboard-row">
                    <div class="key" data-key="`">`</div>
                    <div class="key" data-key="1">1</div>
                    <div class="key" data-key="2">2</div>
                    <div class="key" data-key="3">3</div>
                    <div class="key" data-key="4">4</div>
                    <div class="key" data-key="5">5</div>
                    <div class="key" data-key="6">6</div>
                    <div class="key" data-key="7">7</div>
                    <div class="key" data-key="8">8</div>
                    <div class="key" data-key="9">9</div>
                    <div class="key" data-key="0">0</div>
                    <div class="key" data-key="-">-</div>
                    <div class="key" data-key="=">=</div>
                    <div class="key backspace" data-key="Backspace">←</div>
                </div>
                <div class="keyboard-row">
                    <div class="key" data-key="Tab" style="min-width: 45px;">Tab</div>
                    <div class="key" data-key="q">Q</div>
                    <div class="key" data-key="w">W</div>
                    <div class="key" data-key="e">E</div>
                    <div class="key" data-key="r">R</div>
                    <div class="key" data-key="t">T</div>
                    <div class="key" data-key="y">Y</div>
                    <div class="key" data-key="u">U</div>
                    <div class="key" data-key="i">I</div>
                    <div class="key" data-key="o">O</div>
                    <div class="key" data-key="p">P</div>
                    <div class="key" data-key="[">[</div>
                    <div class="key" data-key="]">]</div>
                    <div class="key" data-key="\">\</div>
                </div>
                <div class="keyboard-row">
                    <div class="key" data-key="CapsLock" style="min-width: 55px;">Caps</div>
                    <div class="key" data-key="a">A</div>
                    <div class="key" data-key="s">S</div>
                    <div class="key" data-key="d">D</div>
                    <div class="key" data-key="f">F</div>
                    <div class="key" data-key="g">G</div>
                    <div class="key" data-key="h">H</div>
                    <div class="key" data-key="j">J</div>
                    <div class="key" data-key="k">K</div>
                    <div class="key" data-key="l">L</div>
                    <div class="key" data-key=";">;</div>
                    <div class="key" data-key="'">'</div>
                    <div class="key enter" data-key="Enter">Enter</div>
                </div>
                <div class="keyboard-row">
                    <div class="key shift" data-key="Shift">Shift</div>
                    <div class="key" data-key="z">Z</div>
                    <div class="key" data-key="x">X</div>
                    <div class="key" data-key="c">C</div>
                    <div class="key" data-key="v">V</div>
                    <div class="key" data-key="b">B</div>
                    <div class="key" data-key="n">N</div>
                    <div class="key" data-key="m">M</div>
                    <div class="key" data-key=",">,</div>
                    <div class="key" data-key=".">.</div>
                    <div class="key" data-key="/">/</div>
                    <div class="key shift" data-key="Shift">Shift</div>
                </div>
                <div class="keyboard-row">
                    <div class="key" data-key="Control" style="min-width: 45px;">Ctrl</div>
                    <div class="key" data-key="Alt" style="min-width: 40px;">Alt</div>
                    <div class="key space" data-key=" "></div>
                    <div class="key" data-key="Alt" style="min-width: 40px;">Alt</div>
                    <div class="key" data-key="Control" style="min-width: 45px;">Ctrl</div>
                </div>
            </div>
        </div>
    </div>

    <script>
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();
        
        function playBubbleSound() {
            const oscillator = audioContext.createOscillator();
            const gainNode = audioContext.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioContext.destination);
            
            const frequencies = [800, 1000, 1200, 900, 1100];
            const randomFreq = frequencies[Math.floor(Math.random() * frequencies.length)];
            
            oscillator.frequency.setValueAtTime(randomFreq, audioContext.currentTime);
            oscillator.type = 'sine';
            
            gainNode.gain.setValueAtTime(0.1, audioContext.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.1);
            
            oscillator.start(audioContext.currentTime);
            oscillator.stop(audioContext.currentTime + 0.1);
        }
        
        function createStars() {
            const starsContainer = document.getElementById('stars');
            for (let i = 0; i < 50; i++) {
                const star = document.createElement('div');
                star.className = 'star';
                star.style.left = Math.random() * 100 + '%';
                star.style.top = Math.random() * 100 + '%';
                star.style.animationDelay = Math.random() * 2 + 's';
                starsContainer.appendChild(star);
            }
        }
        createStars();
        
        const chatInput = document.getElementById('chatInput');
        const chatMessages = document.getElementById('chatMessages');
        const sendBtn = document.getElementById('sendBtn');
        const keyboard = document.getElementById('keyboard');
        const desktop = document.getElementById('desktop');
        
        let noteCount = 0;
        
        const keyElements = keyboard.querySelectorAll('.key');
        
        keyElements.forEach(keyEl => {
            keyEl.addEventListener('click', () => {
                const key = keyEl.dataset.key;
                
                if (audioContext.state === 'suspended') {
                    audioContext.resume();
                }
                playBubbleSound();
                
                keyEl.classList.add('pressed');
                setTimeout(() => keyEl.classList.remove('pressed'), 100);
                
                if (key === 'Backspace') {
                    chatInput.value = chatInput.value.slice(0, -1);
                } else if (key === 'Enter') {
                    sendMessage();
                } else if (key.length === 1) {
                    chatInput.value += key.toLowerCase();
                }
                
                chatInput.focus();
            });
        });
        
        document.addEventListener('keydown', (e) => {
            const keyEl = keyboard.querySelector(`[data-key="${e.key}"]`) || 
                          keyboard.querySelector(`[data-key="${e.key.toLowerCase()}"]`);
            
            if (keyEl) {
                if (audioContext.state === 'suspended') {
                    audioContext.resume();
                }
                playBubbleSound();
                keyEl.classList.add('pressed');
            }
        });
        
        document.addEventListener('keyup', (e) => {
            const keyEl = keyboard.querySelector(`[data-key="${e.key}"]`) || 
                          keyboard.querySelector(`[data-key="${e.key.toLowerCase()}"]`);
            
            if (keyEl) {
                keyEl.classList.remove('pressed');
            }
        });
        
        chatInput.addEventListener('input', () => {
            if (audioContext.state === 'suspended') {
                audioContext.resume();
            }
            playBubbleSound();
        });
        
        function sendMessage() {
            const message = chatInput.value.trim();
            if (!message) return;
            
            const messageEl = document.createElement('div');
            messageEl.className = 'message sent';
            messageEl.textContent = message;
            chatMessages.appendChild(messageEl);
            chatMessages.scrollTop = chatMessages.scrollHeight;
            
            createStickyNote(message);
            
            chatInput.value = '';
        }
        
        sendBtn.addEventListener('click', sendMessage);
        
        chatInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                sendMessage();
            }
        });
        
        function createStickyNote(text) {
            noteCount++;
            const note = document.createElement('div');
            
            const styles = ['dreamcore', 'vaporwave', 'cyberpunk'];
            const randomStyle = styles[Math.floor(Math.random() * styles.length)];
            
            note.className = `sticky-note ${randomStyle} note-spawn-animation`;
            
            const rotation = (Math.random() - 0.5) * 20;
            note.style.setProperty('--rotation', `${rotation}deg`);
            
            const monitorRect = document.querySelector('.monitor').getBoundingClientRect();
            const maxX = window.innerWidth - 180;
            const maxY = window.innerHeight - 130;
            
            let randomX, randomY;
            let attempts = 0;
            
            do {
                randomX = Math.random() * maxX;
                randomY = Math.random() * maxY;
                attempts++;
            } while (
                randomX > monitorRect.left - 180 && 
                randomX < monitorRect.right + 30 &&
                randomY > monitorRect.top - 130 && 
                randomY < monitorRect.bottom + 30 &&
                attempts < 20
            );
            
            note.style.left = randomX + 'px';
            note.style.top = randomY + 'px';
            note.style.transform = `rotate(${rotation}deg)`;
            
            const now = new Date();
            const timeStr = now.toLocaleTimeString('zh-CN', { hour: '2-digit', minute: '2-digit' });
            
            note.innerHTML = `
                <div class="note-glow"></div>
                <div class="note-text">${escapeHtml(text)}</div>
                <div class="note-time">${timeStr}</div>
            `;
            
            document.body.appendChild(note);
            
            makeDraggable(note);
        }
        
        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }
        
        function makeDraggable(element) {
            let isDragging = false;
            let startX, startY, initialX, initialY;
            
            element.addEventListener('mousedown', (e) => {
                isDragging = true;
                element.style.zIndex = 1000 + noteCount;
                
                startX = e.clientX;
                startY = e.clientY;
                initialX = element.offsetLeft;
                initialY = element.offsetTop;
                
                element.style.cursor = 'grabbing';
            });
            
            document.addEventListener('mousemove', (e) => {
                if (!isDragging) return;
                
                e.preventDefault();
                
                const deltaX = e.clientX - startX;
                const deltaY = e.clientY - startY;
                
                let newX = initialX + deltaX;
                let newY = initialY + deltaY;
                
                newX = Math.max(0, Math.min(newX, window.innerWidth - element.offsetWidth));
                newY = Math.max(0, Math.min(newY, window.innerHeight - element.offsetHeight));
                
                element.style.left = newX + 'px';
                element.style.top = newY + 'px';
            });
            
            document.addEventListener('mouseup', () => {
                if (isDragging) {
                    isDragging = false;
                    element.style.cursor = 'grab';
                }
            });
        }
        
        chatInput.focus();
    </script>
</body>
</html>
