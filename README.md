<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dreamcore Computer - 梦核电脑</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=VT323&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --mint-green: #a8d5a8;
            --tiffany-blue: #9ec5c0;
            --aquamarine: #a8ddd4;
            --win-bg: #c0c0c0;
            --win-light: #ffffff;
            --win-dark: #808080;
            --win-darker: #404040;
            --win-title: #000080;
            --win-title-inactive: #808080;
        }

        body {
            min-height: 100vh;
            background: linear-gradient(180deg, 
                #b8d4e8 0%, 
                #c8dce8 20%,
                #d8e4ec 40%,
                #e0e8ec 60%,
                #e8ece8 80%,
                #d8e0d8 100%
            );
            font-family: 'VT323', 'MS Sans Serif', Tahoma, sans-serif;
            overflow: hidden;
            position: relative;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                radial-gradient(ellipse at 30% 20%, rgba(255, 255, 255, 0.4) 0%, transparent 50%),
                radial-gradient(ellipse at 70% 30%, rgba(255, 255, 255, 0.3) 0%, transparent 40%);
            pointer-events: none;
            z-index: 0;
        }

        .sky-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
            overflow: hidden;
        }

        .cloud {
            position: absolute;
            background: rgba(255, 255, 255, 0.7);
            border-radius: 50%;
            filter: blur(2px);
            animation: cloudFloat linear infinite;
        }

        .cloud::before, .cloud::after {
            content: '';
            position: absolute;
            background: inherit;
            border-radius: inherit;
        }

        .cloud-1 {
            width: 200px;
            height: 60px;
            top: 8%;
            left: -200px;
            animation-duration: 80s;
            filter: blur(3px);
            opacity: 0.8;
        }
        .cloud-1::before { width: 100px; height: 50px; top: -20px; left: 30px; }
        .cloud-1::after { width: 80px; height: 40px; top: -15px; left: 100px; }

        .cloud-2 {
            width: 150px;
            height: 45px;
            top: 15%;
            left: -150px;
            animation-duration: 100s;
            animation-delay: -20s;
            filter: blur(4px);
            opacity: 0.6;
        }
        .cloud-2::before { width: 70px; height: 35px; top: -15px; left: 20px; }
        .cloud-2::after { width: 60px; height: 30px; top: -10px; left: 70px; }

        .cloud-3 {
            width: 180px;
            height: 50px;
            top: 5%;
            left: -180px;
            animation-duration: 90s;
            animation-delay: -40s;
            filter: blur(5px);
            opacity: 0.5;
        }
        .cloud-3::before { width: 90px; height: 45px; top: -18px; left: 25px; }
        .cloud-3::after { width: 70px; height: 35px; top: -12px; left: 90px; }

        .cloud-4 {
            width: 120px;
            height: 35px;
            top: 20%;
            left: -120px;
            animation-duration: 70s;
            animation-delay: -60s;
            filter: blur(6px);
            opacity: 0.4;
        }
        .cloud-4::before { width: 50px; height: 25px; top: -10px; left: 15px; }
        .cloud-4::after { width: 45px; height: 22px; top: -8px; left: 55px; }

        @keyframes cloudFloat {
            from { transform: translateX(0); }
            to { transform: translateX(calc(100vw + 300px)); }
        }

        .scanlines {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: repeating-linear-gradient(0deg, rgba(0, 0, 0, 0.02) 0px, rgba(0, 0, 0, 0.02) 1px, transparent 1px, transparent 2px);
            pointer-events: none;
            z-index: 9999;
        }

        .desktop-icons {
            position: fixed;
            left: 20px;
            top: 20px;
            display: grid;
            grid-template-columns: repeat(2, 85px);
            gap: 12px 16px;
            z-index: 10;
        }

        .desktop-icon {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 85px;
            padding: 6px;
            cursor: pointer;
            border: 1px solid transparent;
            border-radius: 4px;
            transition: all 0.15s ease;
        }

        .desktop-icon:hover {
            background: rgba(100, 150, 200, 0.35);
            border: 1px solid rgba(100, 150, 200, 0.5);
            transform: translateY(-2px);
        }

        .desktop-icon.selected {
            background: rgba(100, 150, 200, 0.45);
            border: 1px solid rgba(100, 150, 200, 0.7);
        }

        .icon-image {
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 4px;
            image-rendering: pixelated;
        }

        .icon-label {
            font-size: 12px;
            color: #3a3a3a;
            text-align: center;
            text-shadow: 1px 1px 0 rgba(255, 255, 255, 0.8), -1px -1px 0 rgba(255, 255, 255, 0.8);
            word-wrap: break-word;
            max-width: 80px;
            line-height: 1.3;
        }

        .win-icon {
            width: 40px;
            height: 40px;
            position: relative;
        }

        .win-icon.my-computer {
            background: linear-gradient(135deg, #c0c0c0 0%, #a0a0a0 100%);
            border: 2px solid #808080;
            border-radius: 2px;
        }
        .win-icon.my-computer::before {
            content: '';
            position: absolute;
            top: 4px;
            left: 4px;
            right: 4px;
            height: 14px;
            background: linear-gradient(180deg, #000080 0%, #1084d0 100%);
            border-radius: 2px;
        }
        .win-icon.my-computer::after {
            content: '';
            position: absolute;
            bottom: 4px;
            left: 6px;
            right: 6px;
            height: 8px;
            background: #d0d0d0;
            border: 1px solid #808080;
        }

        .win-icon.recycle-bin {
            background: linear-gradient(180deg, #e8e8e8 0%, #c8c8c8 100%);
            border: 2px solid #a0a0a0;
            border-radius: 0 0 6px 6px;
        }
        .win-icon.recycle-bin::before {
            content: '';
            position: absolute;
            top: 2px;
            left: 6px;
            right: 6px;
            height: 3px;
            background: #808080;
            border-radius: 1px;
        }
        .win-icon.recycle-bin::after {
            content: '';
            position: absolute;
            top: 6px;
            left: 5px;
            right: 5px;
            bottom: 3px;
            background: repeating-linear-gradient(90deg, #c0c0c0 0px, #c0c0c0 2px, #a0a0a0 2px, #a0a0a0 3px);
        }

        .win-icon.folder {
            background: linear-gradient(180deg, #f0d878 0%, #d8b848 100%);
            border: 2px solid #a08030;
            border-radius: 2px;
        }
        .win-icon.folder::before {
            content: '';
            position: absolute;
            top: -2px;
            left: 0;
            width: 14px;
            height: 6px;
            background: linear-gradient(180deg, #f0d878 0%, #d8b848 100%);
            border: 2px solid #a08030;
            border-bottom: none;
            border-radius: 2px 2px 0 0;
        }

        .win-icon.notepad {
            background: linear-gradient(180deg, #f8f8f8 0%, #e0e0e0 100%);
            border: 2px solid #808080;
            border-radius: 1px;
        }
        .win-icon.notepad::before {
            content: '';
            position: absolute;
            top: 3px;
            left: 3px;
            right: 3px;
            bottom: 3px;
            background: repeating-linear-gradient(180deg, transparent 0px, transparent 3px, #a8d8f8 3px, #a8d8f8 4px);
        }

        .win-icon.paint {
            background: linear-gradient(180deg, #f8f8f8 0%, #e0e0e0 100%);
            border: 2px solid #808080;
            border-radius: 1px;
            overflow: hidden;
        }
        .win-icon.paint::before {
            content: '';
            position: absolute;
            top: 3px;
            left: 3px;
            right: 3px;
            bottom: 3px;
            background: linear-gradient(45deg, #f8a8a8 25%, transparent 25%), linear-gradient(-45deg, #a8f8a8 25%, transparent 25%), linear-gradient(135deg, #a8a8f8 25%, transparent 25%), linear-gradient(-135deg, #f8f8a8 25%, transparent 25%);
            background-size: 8px 8px;
        }

        .win-icon.calculator {
            background: linear-gradient(180deg, #d8e8d8 0%, #b8c8b8 100%);
            border: 2px solid #808080;
            border-radius: 2px;
        }
        .win-icon.calculator::before {
            content: '';
            position: absolute;
            top: 3px;
            left: 3px;
            right: 3px;
            height: 8px;
            background: #a8d8a8;
            border: 1px solid #808080;
        }
        .win-icon.calculator::after {
            content: '';
            position: absolute;
            bottom: 2px;
            left: 2px;
            right: 2px;
            height: 12px;
            background: repeating-linear-gradient(90deg, #c0c0c0 0px, #c0c0c0 4px, #a0a0a0 4px, #a0a0a0 5px);
        }

        .win-icon.internet {
            background: linear-gradient(180deg, #e8f0f8 0%, #c8d8e8 100%);
            border: 2px solid #808080;
            border-radius: 50%;
        }
        .win-icon.internet::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 16px;
            height: 16px;
            border: 2px solid #0080ff;
            border-radius: 50%;
        }
        .win-icon.internet::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 6px;
            height: 6px;
            background: #0080ff;
            border-radius: 50%;
        }

        .win-icon.games {
            background: linear-gradient(180deg, #f0e8d8 0%, #d8c8a8 100%);
            border: 2px solid #808080;
            border-radius: 2px;
        }
        .win-icon.games::before {
            content: '♠♥';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 8px;
            color: #c03030;
        }

        .win-icon.help {
            background: linear-gradient(180deg, #f8f0d8 0%, #e8d8b0 100%);
            border: 2px solid #808080;
            border-radius: 2px;
        }
        .win-icon.help::before {
            content: '?';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 16px;
            font-weight: bold;
            color: #000080;
        }

        .win-window {
            position: absolute;
            background: var(--win-bg);
            border: 2px solid;
            border-color: var(--win-light) var(--win-darker) var(--win-darker) var(--win-light);
            box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.3);
            display: flex;
            flex-direction: column;
            min-width: 200px;
            min-height: 150px;
        }

        .win-window.active {
            z-index: 100;
        }

        .win-titlebar {
            background: linear-gradient(90deg, var(--win-title), #1084d0);
            padding: 2px 3px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            cursor: move;
            user-select: none;
        }

        .win-window.inactive .win-titlebar {
            background: linear-gradient(90deg, var(--win-title-inactive), #a0a0a0);
        }

        .win-titlebar-left {
            display: flex;
            align-items: center;
            gap: 4px;
            overflow: hidden;
        }

        .win-titlebar-icon {
            width: 16px;
            height: 16px;
            flex-shrink: 0;
        }

        .win-titlebar-text {
            color: white;
            font-size: 12px;
            font-weight: bold;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .win-titlebar-controls {
            display: flex;
            gap: 2px;
        }

        .win-btn {
            width: 16px;
            height: 14px;
            background: var(--win-bg);
            border: 1px solid;
            border-color: var(--win-light) var(--win-dark) var(--win-dark) var(--win-light);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 9px;
            font-weight: bold;
            cursor: pointer;
            padding: 0;
            font-family: 'Marlett', sans-serif;
        }

        .win-btn:active {
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
        }

        .win-btn-minimize::after { content: '▬'; font-size: 7px; }
        .win-btn-maximize::after { content: '□'; font-size: 10px; }
        .win-btn-close {
            background: #c0c0c0;
        }
        .win-btn-close::after { content: '✕'; font-size: 8px; }

        .win-menubar {
            background: var(--win-bg);
            padding: 2px 0;
            border-bottom: 1px solid var(--win-dark);
            display: flex;
            gap: 0;
        }

        .win-menu-item {
            padding: 2px 8px;
            font-size: 12px;
            cursor: pointer;
        }

        .win-menu-item:hover {
            background: var(--win-title);
            color: white;
        }

        .win-content {
            flex: 1;
            background: white;
            border: 2px solid;
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
            margin: 2px;
            overflow: hidden;
            display: flex;
            flex-direction: column;
        }

        .win-statusbar {
            background: var(--win-bg);
            padding: 2px 4px;
            font-size: 11px;
            border-top: 1px solid var(--win-dark);
            display: flex;
            gap: 4px;
        }

        .win-statusbar-section {
            border: 1px solid;
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
            padding: 1px 4px;
            flex: 1;
        }

        .chat-window {
            top: 80px;
            left: 120px;
            width: 380px;
            height: 350px;
        }

        @media (min-width: 768px) {
            .chat-window {
                width: 450px;
                height: 400px;
                top: 60px;
                left: 150px;
            }
        }

        .chat-content {
            flex: 1;
            display: flex;
            flex-direction: column;
            background: #1a1a1a;
        }

        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 10px;
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .chat-messages::-webkit-scrollbar {
            width: 16px;
        }

        .chat-messages::-webkit-scrollbar-track {
            background: #c0c0c0;
            border: 1px solid #808080;
        }

        .chat-messages::-webkit-scrollbar-thumb {
            background: #c0c0c0;
            border: 2px solid;
            border-color: #ffffff #808080 #808080 #ffffff;
        }

        .message {
            max-width: 85%;
            padding: 6px 10px;
            font-size: 13px;
            line-height: 1.3;
            animation: messageAppear 0.2s ease-out;
            position: relative;
            font-family: 'VT323', monospace;
        }

        .message::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            border-radius: inherit;
            pointer-events: none;
        }

        @keyframes messageAppear {
            from { opacity: 0; transform: translateY(5px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .message.received {
            background: linear-gradient(145deg, #5a5a5a, #3a3a3a);
            color: #e0e0e0;
            align-self: flex-start;
            border-radius: 12px 12px 12px 4px;
            box-shadow: 
                0 2px 8px rgba(0, 0, 0, 0.3),
                inset 0 1px 0 rgba(255, 255, 255, 0.1),
                inset 0 -1px 0 rgba(0, 0, 0, 0.2);
        }

        .message.received::before {
            background: linear-gradient(135deg, rgba(255,255,255,0.05) 0%, transparent 50%);
        }

        .message.sent {
            background: linear-gradient(145deg, var(--tiffany-blue), var(--aquamarine));
            color: #2a2a2a;
            align-self: flex-end;
            border-radius: 12px 12px 4px 12px;
            box-shadow: 
                0 2px 8px rgba(0, 0, 0, 0.15),
                inset 0 1px 0 rgba(255, 255, 255, 0.3),
                inset 0 -1px 0 rgba(0, 0, 0, 0.1);
        }

        .message.sent::before {
            background: linear-gradient(135deg, rgba(255,255,255,0.2) 0%, transparent 50%);
        }

        .chat-input-area {
            display: flex;
            gap: 4px;
            padding: 6px;
            background: #2a2a2a;
            border-top: 1px solid #404040;
        }

        .chat-input {
            flex: 1;
            background: #1a1a1a;
            border: 2px solid;
            border-color: #404040 #606060 #606060 #404040;
            padding: 4px 8px;
            color: var(--mint-green);
            font-family: 'VT323', monospace;
            font-size: 14px;
            outline: none;
        }

        .chat-input::placeholder {
            color: rgba(168, 213, 168, 0.5);
        }

        .win-btn-send {
            width: auto;
            padding: 2px 12px;
            background: var(--win-bg);
            border: 2px solid;
            border-color: var(--win-light) var(--win-dark) var(--win-dark) var(--win-light);
            font-size: 12px;
            cursor: pointer;
            font-family: 'VT323', monospace;
        }

        .win-btn-send:active {
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
        }

        .keyboard-window {
            width: auto;
        }

        .keyboard-content {
            background: var(--win-bg);
            padding: 8px;
        }

        .keyboard-row {
            display: flex;
            justify-content: center;
            gap: 3px;
            margin-bottom: 3px;
        }

        .osk-key {
            min-width: 32px;
            height: 32px;
            background: var(--win-bg);
            border: 2px solid;
            border-color: var(--win-light) var(--win-dark) var(--win-dark) var(--win-light);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 11px;
            color: #000;
            cursor: pointer;
            user-select: none;
            font-family: 'VT323', monospace;
        }

        .osk-key:active, .osk-key.pressed {
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
            background: #a0a0a0;
        }

        .osk-key.space {
            min-width: 160px;
        }

        .osk-key.backspace, .osk-key.enter {
            min-width: 55px;
        }

        .osk-key.shift, .osk-key.caps {
            min-width: 45px;
        }

        .osk-key.ctrl, .osk-key.alt {
            min-width: 40px;
        }

        .osk-key.tab {
            min-width: 45px;
        }

        .sticky-note {
            position: absolute;
            width: 130px;
            min-height: 100px;
            padding: 10px;
            font-family: 'VT323', monospace;
            font-size: 12px;
            cursor: grab;
            z-index: 50;
            animation: noteAppear 0.4s ease-out;
            border: 2px solid;
        }

        .sticky-note:active { cursor: grabbing; }

        @keyframes noteAppear {
            from { opacity: 0; transform: scale(0.8); }
            to { opacity: 1; transform: scale(1); }
        }

        .sticky-note.dreamcore {
            background: linear-gradient(135deg, #c8d8c8, #b8c8c8);
            border-color: rgba(168, 213, 168, 0.5);
            color: #3a4a3a;
        }

        .sticky-note.vaporwave {
            background: linear-gradient(135deg, #d8c0c8, #c0d0d8);
            border-color: rgba(200, 160, 176, 0.5);
            color: #4a3a4a;
        }

        .sticky-note.cyberpunk {
            background: linear-gradient(135deg, #2a2a2a, #3a3a3a);
            border-color: #88c8a8;
            color: #88c8a8;
        }

        .sticky-note.nostalgic {
            background: linear-gradient(135deg, #e8d8c8, #d8c8b8);
            border-color: rgba(200, 180, 160, 0.5);
            color: #5a4a3a;
        }

        .sticky-note.ethereal {
            background: linear-gradient(135deg, #d8e0e8, #c8d0d8);
            border-color: rgba(180, 200, 220, 0.5);
            color: #4a5a6a;
        }

        .sticky-note-time {
            font-size: 9px;
            opacity: 0.6;
            margin-bottom: 4px;
        }

        .sticky-note-content {
            word-wrap: break-word;
            line-height: 1.3;
        }

        .sticky-note-close {
            position: absolute;
            top: 2px;
            right: 4px;
            background: none;
            border: none;
            cursor: pointer;
            font-size: 12px;
            opacity: 0.5;
        }

        .sticky-note-close:hover { opacity: 1; }

        .heart-popup {
            position: fixed;
            font-size: 28px;
            animation: heartFloat 2s ease-out forwards;
            pointer-events: none;
            z-index: 9999;
        }

        @keyframes heartFloat {
            0% { opacity: 1; transform: translateY(0) scale(1); }
            100% { opacity: 0; transform: translateY(-80px) scale(1.3); }
        }

        .taskbar {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            height: 28px;
            background: var(--win-bg);
            border-top: 2px solid var(--win-light);
            display: flex;
            align-items: center;
            padding: 2px 4px;
            z-index: 1000;
        }

        .start-btn {
            height: 22px;
            padding: 0 6px;
            background: var(--win-bg);
            border: 2px solid;
            border-color: var(--win-light) var(--win-dark) var(--win-dark) var(--win-light);
            display: flex;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            font-size: 11px;
            font-weight: bold;
            font-family: 'VT323', monospace;
        }

        .start-btn:active {
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
        }

        .start-btn img {
            width: 16px;
            height: 16px;
        }

        .taskbar-windows {
            flex: 1;
            display: flex;
            gap: 2px;
            margin-left: 8px;
            overflow: hidden;
        }

        .taskbar-item {
            height: 22px;
            min-width: 120px;
            max-width: 160px;
            padding: 0 8px;
            background: var(--win-bg);
            border: 2px solid;
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
            display: flex;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            font-size: 11px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }

        .taskbar-item.active {
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
            background: #a0a0a0;
        }

        .taskbar-tray {
            display: flex;
            align-items: center;
            gap: 4px;
            padding: 0 8px;
            border: 1px solid;
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
            height: 20px;
            font-size: 11px;
        }

        .minimized-window {
            display: none !important;
        }

        .music-player {
            position: fixed;
            top: 15px;
            right: 15px;
            width: 280px;
            background: var(--win-bg);
            border: 2px solid;
            border-color: var(--win-light) var(--win-dark) var(--win-dark) var(--win-light);
            box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.2);
            z-index: 200;
            font-size: 11px;
        }

        .music-player-header {
            background: linear-gradient(90deg, #000080, #1084d0);
            padding: 2px 4px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            cursor: move;
        }

        .music-player-title {
            color: white;
            font-size: 11px;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 4px;
        }

        .music-player-body {
            padding: 8px;
        }

        .music-cover-area {
            display: flex;
            gap: 10px;
            margin-bottom: 8px;
        }

        .music-cover {
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #4080c0, #2060a0);
            border: 1px solid #808080;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            flex-shrink: 0;
        }

        .music-info {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            overflow: hidden;
        }

        .music-title {
            font-weight: bold;
            font-size: 12px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            margin-bottom: 2px;
        }

        .music-artist {
            color: #606060;
            font-size: 10px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .music-album {
            color: #808080;
            font-size: 10px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .music-progress-container {
            margin-bottom: 8px;
        }

        .music-progress-bar {
            width: 100%;
            height: 12px;
            background: #e0e0e0;
            border: 1px solid #808080;
            cursor: pointer;
            position: relative;
        }

        .music-progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #000080, #1084d0);
            width: 0%;
            transition: width 0.1s;
        }

        .music-time {
            display: flex;
            justify-content: space-between;
            font-size: 10px;
            color: #606060;
            margin-top: 2px;
        }

        .music-controls {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 4px;
            margin-bottom: 8px;
        }

        .music-btn {
            width: 28px;
            height: 24px;
            background: var(--win-bg);
            border: 2px solid;
            border-color: var(--win-light) var(--win-dark) var(--win-dark) var(--win-light);
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
        }

        .music-btn:active {
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
        }

        .music-btn.play-pause {
            width: 36px;
        }

        .music-volume-container {
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .music-volume-icon {
            font-size: 14px;
            cursor: pointer;
        }

        .music-volume-slider {
            flex: 1;
            height: 12px;
            background: #e0e0e0;
            border: 1px solid #808080;
            cursor: pointer;
            position: relative;
        }

        .music-volume-fill {
            height: 100%;
            background: linear-gradient(90deg, #008000, #00a000);
            width: 70%;
        }

        .music-playlist {
            max-height: 80px;
            overflow-y: auto;
            border: 1px solid #808080;
            background: white;
            margin-top: 8px;
        }

        .music-playlist-item {
            padding: 4px 6px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 6px;
            font-size: 10px;
        }

        .music-playlist-item:hover {
            background: #e0e0e0;
        }

        .music-playlist-item.active {
            background: #000080;
            color: white;
        }

        .music-playlist-item-num {
            width: 20px;
            color: #808080;
        }

        .music-playlist-item.active .music-playlist-item-num {
            color: #a0c0ff;
        }

        .music-visualizer {
            display: flex;
            align-items: flex-end;
            justify-content: center;
            gap: 2px;
            height: 20px;
            margin-top: 8px;
        }

        .music-bar {
            width: 4px;
            background: linear-gradient(180deg, #000080, #1084d0);
            animation: musicBar 0.5s ease-in-out infinite alternate;
        }

        .music-bar:nth-child(1) { animation-delay: 0s; height: 8px; }
        .music-bar:nth-child(2) { animation-delay: 0.1s; height: 14px; }
        .music-bar:nth-child(3) { animation-delay: 0.2s; height: 10px; }
        .music-bar:nth-child(4) { animation-delay: 0.3s; height: 16px; }
        .music-bar:nth-child(5) { animation-delay: 0.4s; height: 12px; }
        .music-bar:nth-child(6) { animation-delay: 0.2s; height: 8px; }
        .music-bar:nth-child(7) { animation-delay: 0.1s; height: 14px; }
        .music-bar:nth-child(8) { animation-delay: 0.3s; height: 10px; }

        @keyframes musicBar {
            from { height: 4px; }
            to { height: 20px; }
        }

        .music-player.paused .music-bar {
            animation: none;
            height: 4px;
        }

        .music-player.minimized .music-player-body {
            display: none;
        }

        .music-player.minimized {
            width: auto;
        }

        .music-player.minimized .music-player-header {
            padding: 2px 8px;
        }

        .music-mini-icon {
            position: fixed;
            bottom: 40px;
            right: 15px;
            width: 50px;
            height: 50px;
            background: linear-gradient(135deg, #4080c0, #2060a0);
            border: 2px solid;
            border-color: var(--win-light) var(--win-dark) var(--win-dark) var(--win-light);
            border-radius: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            cursor: pointer;
            z-index: 10000;
            box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.3);
        }

        .music-mini-icon:hover {
            background: linear-gradient(135deg, #5090d0, #3070b0);
        }

        .music-mini-icon.playing::after {
            content: '';
            position: absolute;
            top: -3px;
            right: -3px;
            width: 10px;
            height: 10px;
            background: #00ff00;
            border-radius: 50%;
            border: 1px solid #008000;
            animation: pulse 1s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.7; transform: scale(0.8); }
        }

        .alien-cat {
            position: fixed;
            bottom: 40px;
            right: 80px;
            width: 80px;
            height: 90px;
            z-index: 9999;
            cursor: pointer;
            user-select: none;
        }

        .alien-cat-body {
            position: relative;
            width: 100%;
            height: 100%;
        }

        .cat-head {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 55px;
            height: 45px;
            background: linear-gradient(135deg, #a8e6cf, #88d4ab);
            border-radius: 50% 50% 45% 45%;
            box-shadow: 0 2px 10px rgba(168, 230, 207, 0.5);
        }

        .cat-ear {
            position: absolute;
            top: -12px;
            width: 18px;
            height: 25px;
            background: linear-gradient(135deg, #a8e6cf, #88d4ab);
            border-radius: 50% 50% 0 0;
        }

        .cat-ear.left {
            left: 3px;
            transform: rotate(-15deg);
        }

        .cat-ear.right {
            right: 3px;
            transform: rotate(15deg);
        }

        .cat-ear-inner {
            position: absolute;
            top: 5px;
            left: 50%;
            transform: translateX(-50%);
            width: 8px;
            height: 12px;
            background: #ffb6c1;
            border-radius: 50% 50% 0 0;
        }

        .cat-eye {
            position: absolute;
            top: 15px;
            width: 16px;
            height: 18px;
            background: #000;
            border-radius: 50%;
            overflow: hidden;
        }

        .cat-eye.left {
            left: 10px;
        }

        .cat-eye.right {
            right: 10px;
        }

        .cat-eye::before {
            content: '';
            position: absolute;
            top: 3px;
            left: 3px;
            width: 6px;
            height: 6px;
            background: white;
            border-radius: 50%;
        }

        .cat-eye::after {
            content: '';
            position: absolute;
            bottom: 2px;
            left: 50%;
            transform: translateX(-50%);
            width: 8px;
            height: 10px;
            background: linear-gradient(180deg, #00ff88, #00cc66);
            border-radius: 50%;
            animation: eyeGlow 2s ease-in-out infinite;
        }

        @keyframes eyeGlow {
            0%, 100% { opacity: 0.8; }
            50% { opacity: 1; }
        }

        .cat-nose {
            position: absolute;
            top: 28px;
            left: 50%;
            transform: translateX(-50%);
            width: 8px;
            height: 6px;
            background: #ffb6c1;
            border-radius: 50%;
        }

        .cat-mouth {
            position: absolute;
            top: 33px;
            left: 50%;
            transform: translateX(-50%);
            width: 12px;
            height: 6px;
            border: 2px solid #88d4ab;
            border-top: none;
            border-radius: 0 0 50% 50%;
        }

        .cat-whisker {
            position: absolute;
            top: 30px;
            width: 20px;
            height: 2px;
            background: #88d4ab;
        }

        .cat-whisker.left-1 { left: -15px; transform: rotate(-10deg); }
        .cat-whisker.left-2 { left: -15px; top: 35px; transform: rotate(5deg); }
        .cat-whisker.right-1 { right: -15px; transform: rotate(10deg); }
        .cat-whisker.right-2 { right: -15px; top: 35px; transform: rotate(-5deg); }

        .cat-body-main {
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 45px;
            height: 50px;
            background: linear-gradient(135deg, #a8e6cf, #88d4ab);
            border-radius: 45% 45% 50% 50%;
        }

        .cat-tail {
            position: absolute;
            bottom: 10px;
            right: -15px;
            width: 30px;
            height: 10px;
            background: linear-gradient(90deg, #88d4ab, #a8e6cf);
            border-radius: 10px;
            transform-origin: left center;
            animation: tailWag 1s ease-in-out infinite;
        }

        @keyframes tailWag {
            0%, 100% { transform: rotate(-10deg); }
            50% { transform: rotate(10deg); }
        }

        .cat-antenna {
            position: absolute;
            top: -20px;
            width: 2px;
            height: 15px;
            background: #88d4ab;
        }

        .cat-antenna.left {
            left: 15px;
            transform: rotate(-20deg);
        }

        .cat-antenna.right {
            right: 15px;
            transform: rotate(20deg);
        }

        .cat-antenna::after {
            content: '';
            position: absolute;
            top: -6px;
            left: -4px;
            width: 10px;
            height: 10px;
            background: radial-gradient(circle, #00ff88, #00cc66);
            border-radius: 50%;
            animation: antennaGlow 1.5s ease-in-out infinite;
        }

        @keyframes antennaGlow {
            0%, 100% { box-shadow: 0 0 5px #00ff88; }
            50% { box-shadow: 0 0 15px #00ff88, 0 0 25px #00ff88; }
        }

        .alien-cat:hover .cat-head {
            animation: headBob 0.3s ease-in-out;
        }

        @keyframes headBob {
            0%, 100% { transform: translateX(-50%) rotate(0deg); }
            25% { transform: translateX(-50%) rotate(-5deg); }
            75% { transform: translateX(-50%) rotate(5deg); }
        }

        .alien-cat.clicked .cat-eye::after {
            animation: eyeSparkle 0.5s ease-out;
        }

        @keyframes eyeSparkle {
            0% { transform: translateX(-50%) scale(1); }
            50% { transform: translateX(-50%) scale(1.5); background: #fff; }
            100% { transform: translateX(-50%) scale(1); }
        }

        .alien-cat.double-clicked {
            animation: catJump 0.5s ease-out;
        }

        @keyframes catJump {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }

        .alien-cat.right-clicked .cat-body-main {
            animation: catSpin 0.6s ease-out;
        }

        @keyframes catSpin {
            0% { transform: translateX(-50%) rotate(0deg); }
            100% { transform: translateX(-50%) rotate(360deg); }
        }

        .cat-speech {
            position: absolute;
            top: -45px;
            left: 50%;
            transform: translateX(-50%);
            background: white;
            padding: 6px 12px;
            border-radius: 10px;
            font-size: 11px;
            white-space: nowrap;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
            opacity: 0;
            transition: opacity 0.3s;
            pointer-events: none;
            z-index: 10;
        }

        .cat-speech::after {
            content: '';
            position: absolute;
            bottom: -8px;
            left: 50%;
            transform: translateX(-50%);
            border-left: 8px solid transparent;
            border-right: 8px solid transparent;
            border-top: 8px solid white;
        }

        .cat-speech.show {
            opacity: 1;
        }

        .cat-paw {
            position: absolute;
            bottom: 5px;
            width: 15px;
            height: 12px;
            background: #a8e6cf;
            border-radius: 50%;
        }

        .cat-paw.left {
            left: 5px;
        }

        .cat-paw.right {
            right: 5px;
        }

        .alien-cat.walking {
            animation: catWalk 0.3s ease-in-out infinite;
        }

        @keyframes catWalk {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-3px); }
        }

        .alien-cat.walking .cat-paw.left {
            animation: pawMove 0.3s ease-in-out infinite;
        }

        .alien-cat.walking .cat-paw.right {
            animation: pawMove 0.3s ease-in-out infinite 0.15s;
        }

        @keyframes pawMove {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-5px); }
        }

        .cat-star {
            position: absolute;
            font-size: 10px;
            animation: starFloat 2s ease-in-out infinite;
            pointer-events: none;
        }

        @keyframes starFloat {
            0%, 100% { opacity: 0; transform: translateY(0) scale(0); }
            50% { opacity: 1; transform: translateY(-20px) scale(1); }
        }

        .love-hearts-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 9998;
            overflow: hidden;
        }

        .love-heart {
            position: absolute;
            font-size: 24px;
            opacity: 0;
            animation: loveHeartFloat 4s ease-out forwards;
            pointer-events: none;
        }

        @keyframes loveHeartFloat {
            0% {
                opacity: 0.7;
                transform: translateY(100vh) scale(0.5) rotate(0deg);
            }
            50% {
                opacity: 0.5;
            }
            100% {
                opacity: 0;
                transform: translateY(-20vh) scale(1.2) rotate(20deg);
            }
        }

        .love-heart.small {
            font-size: 16px;
            animation-duration: 3s;
        }

        .love-heart.large {
            font-size: 36px;
            animation-duration: 5s;
        }

        @media (max-width: 480px) {
              .music-player {
                  width: 200px;
                  right: 10px;
                  top: 10px;
              }
              .music-cover {
                  width: 45px;
                  height: 45px;
                  font-size: 18px;
              }
              .music-btn {
                  width: 24px;
                  height: 20px;
                  font-size: 10px;
              }
              .music-mini-icon {
                  width: 40px;
                  height: 40px;
                  font-size: 20px;
                  bottom: 35px;
                  right: 10px;
              }
              .alien-cat {
                  width: 60px;
                  height: 70px;
                  right: 60px;
                  bottom: 35px;
              }
              .cat-head {
                  width: 42px;
                  height: 35px;
              }
              .cat-ear {
                  width: 14px;
                  height: 20px;
              }
              .cat-eye {
                  width: 12px;
                  height: 14px;
              }
              .cat-body-main {
                  width: 35px;
                  height: 40px;
              }
          }

        .win-icon.word {
            background: linear-gradient(180deg, #2855a5 0%, #1a3d7a 100%);
            border: 2px solid #0f2d5c;
            border-radius: 2px;
            position: relative;
        }
        .win-icon.word::before {
            content: 'W';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 18px;
            font-weight: bold;
            color: white;
        }

        .win-icon.excel {
            background: linear-gradient(180deg, #1d6f42 0%, #0f4d2d 100%);
            border: 2px solid #0a3d1f;
            border-radius: 2px;
            position: relative;
        }
        .win-icon.excel::before {
            content: 'X';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 18px;
            font-weight: bold;
            color: white;
        }

        .win-icon.media {
            background: linear-gradient(180deg, #f0a030 0%, #d08020 100%);
            border: 2px solid #a06010;
            border-radius: 2px;
            position: relative;
        }
        .win-icon.media::before {
            content: '▶';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 14px;
            color: white;
        }

        .win-icon.settings {
            background: linear-gradient(180deg, #808080 0%, #606060 100%);
            border: 2px solid #404040;
            border-radius: 2px;
            position: relative;
        }
        .win-icon.settings::before {
            content: '⚙';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 16px;
            color: white;
        }

        .paint-window, .notepad-window, .word-window, .calc-window {
            width: 400px;
            height: 320px;
        }

        .paint-canvas {
            flex: 1;
            background: white;
            cursor: crosshair;
        }

        .paint-tools {
            display: flex;
            gap: 4px;
            padding: 4px;
            background: var(--win-bg);
            border-bottom: 1px solid var(--win-dark);
        }

        .paint-tool {
            width: 24px;
            height: 24px;
            background: var(--win-bg);
            border: 2px solid;
            border-color: var(--win-light) var(--win-dark) var(--win-dark) var(--win-light);
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
        }

        .paint-tool:active, .paint-tool.active {
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
        }

        .color-palette {
            display: flex;
            gap: 2px;
            padding: 4px;
            background: var(--win-bg);
        }

        .color-swatch {
            width: 16px;
            height: 16px;
            border: 1px solid #808080;
            cursor: pointer;
        }

        .notepad-textarea {
            flex: 1;
            border: none;
            resize: none;
            font-family: 'VT323', monospace;
            font-size: 14px;
            padding: 4px;
            outline: none;
        }

        .word-textarea {
            flex: 1;
            border: none;
            resize: none;
            font-family: 'VT323', serif;
            font-size: 14px;
            padding: 8px;
            outline: none;
            line-height: 1.6;
        }

        .calc-display {
            background: #c8d8c8;
            border: 2px solid;
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
            margin: 4px;
            padding: 8px;
            text-align: right;
            font-size: 20px;
            font-family: 'VT323', monospace;
        }

        .emotion-bar-window {
            width: 360px;
            height: 400px;
        }

        .emotion-bar-container {
            background: linear-gradient(180deg, #1a1010 0%, #0a121a 50%, #050505 100%);
            height: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
            transition: background 1s;
            font-family: 'VT323', monospace;
            overflow: hidden;
            box-sizing: border-box;
        }

        .emotion-bar-container.bright { background: linear-gradient(180deg, #2a1810 0%, #1a1010 100%); }
        .emotion-bar-container.calm { background: linear-gradient(180deg, #0a121a 0%, #050510 100%); }
        .emotion-bar-container.deep { background: linear-gradient(180deg, #050505 0%, #000000 100%); }

        .emotion-mixing-view, .emotion-result-view {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            width: 100%;
            height: 100%;
            box-sizing: border-box;
        }

        .emotion-glass {
            position: relative;
            width: 80px;
            height: 115px;
            margin-bottom: 25px;
            flex-shrink: 0;
        }

        .emotion-glass-frame {
            position: absolute;
            inset: 0;
            border: 2px solid rgba(255,255,255,0.25);
            border-radius: 12px 12px 45px 45px;
            backdrop-filter: blur(6px);
            box-shadow: 
                0 8px 32px rgba(0,0,0,0.4),
                inset 0 1px 0 rgba(255,255,255,0.1);
        }

        .emotion-liquid {
            position: absolute;
            bottom: 0;
            width: 100%;
            border-radius: 0 0 43px 43px;
            transition: height 0.5s, background 1s;
            opacity: 0.85;
        }

        .emotion-liquid.bright {
            background: linear-gradient(to top, #fbbf24, #f472b6, #fb923c);
            box-shadow: 0 0 20px rgba(251, 191, 36, 0.3);
        }
        .emotion-liquid.calm {
            background: linear-gradient(to top, #a5f3fc, #93c5fd, #818cf8);
            box-shadow: 0 0 20px rgba(165, 243, 252, 0.3);
        }
        .emotion-liquid.deep {
            background: linear-gradient(to top, #581c87, #312e81, #000000);
            box-shadow: 0 0 20px rgba(88, 28, 135, 0.3);
        }

        .emotion-wave {
            position: absolute;
            bottom: 0;
            width: 100%;
            height: 100%;
            border-radius: 0 0 43px 43px;
            opacity: 0.25;
            animation: emotionWave 4s ease-in-out infinite;
        }

        .emotion-wave.bright { background: linear-gradient(to top, #fbbf24, #f472b6); }
        .emotion-wave.calm { background: linear-gradient(to top, #a5f3fc, #93c5fd); }
        .emotion-wave.deep { background: linear-gradient(to top, #581c87, #312e81); }

        @keyframes emotionWave {
            0%, 100% { border-radius: 40% 60% 60% 40%; transform: rotate(0deg); }
            50% { border-radius: 60% 40% 40% 60%; transform: rotate(3deg); }
        }

        .emotion-slider-container {
            width: 100%;
            max-width: 240px;
            margin-bottom: 20px;
            flex-shrink: 0;
        }

        .emotion-slider-track {
            position: relative;
            height: 4px;
            background: linear-gradient(90deg, rgba(88,28,135,0.5), rgba(255,255,255,0.15), rgba(251,191,36,0.5));
            border-radius: 4px;
            margin-bottom: 10px;
        }

        .emotion-slider-dot {
            position: absolute;
            top: 50%;
            transform: translate(-50%, -50%);
            width: 16px;
            height: 16px;
            background: linear-gradient(135deg, #ffffff, #e8e8e8);
            border-radius: 50%;
            box-shadow: 0 0 15px rgba(255,255,255,0.7), 0 2px 6px rgba(0,0,0,0.3);
            transition: left 0.1s;
        }

        .emotion-slider-input {
            position: absolute;
            width: 100%;
            height: 24px;
            opacity: 0;
            cursor: pointer;
            top: -10px;
        }

        .emotion-labels {
            display: flex;
            justify-content: space-between;
            font-size: 11px;
            letter-spacing: 0.2em;
            color: rgba(255,255,255,0.5);
            text-transform: uppercase;
            font-weight: 500;
        }

        .emotion-labels span:first-child { color: rgba(139, 92, 246, 0.8); }
        .emotion-labels span:last-child { color: rgba(251, 191, 36, 0.8); }

        .emotion-btn {
            padding: 12px 28px;
            border-radius: 30px;
            background: linear-gradient(135deg, rgba(255,255,255,0.15), rgba(255,255,255,0.05));
            border: 1px solid rgba(255,255,255,0.25);
            backdrop-filter: blur(10px);
            color: rgba(255,255,255,0.85);
            font-size: 12px;
            letter-spacing: 0.15em;
            cursor: pointer;
            transition: all 0.3s ease;
            font-family: 'VT323', monospace;
            flex-shrink: 0;
            text-transform: uppercase;
        }

        .emotion-btn:hover {
            border-color: rgba(255,255,255,0.5);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255,255,255,0.15);
        }

        .emotion-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }

        .emotion-ripple {
            position: absolute;
            width: 50px;
            height: 50px;
            border: 1px solid rgba(255,255,255,0.2);
            border-radius: 50%;
            animation: emotionRipple 2s ease-out infinite;
        }

        @keyframes emotionRipple {
            0% { transform: scale(1); opacity: 0.5; }
            100% { transform: scale(2.5); opacity: 0; }
        }

        .emotion-result {
            text-align: center;
            color: white;
            width: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: flex-start;
            padding-top: 10px;
        }

        .emotion-result-title {
            font-size: 16px;
            font-style: italic;
            letter-spacing: 0.08em;
            margin-bottom: 3px;
            background: linear-gradient(90deg, #a5f3fc, #f472b6);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .emotion-result-subtitle {
            font-size: 8px;
            letter-spacing: 0.2em;
            color: rgba(255,255,255,0.35);
            text-transform: uppercase;
            margin-bottom: 10px;
        }

        .emotion-bottle {
            position: relative;
            width: 40px;
            height: 65px;
            margin: 0 auto 10px;
            background: rgba(255,255,255,0.03);
            border: 1px solid rgba(255,255,255,0.12);
            border-radius: 10px 10px 5px 5px;
            overflow: hidden;
            box-shadow: 0 3px 15px rgba(0,0,0,0.3);
        }

        .emotion-bottle-liquid {
            position: absolute;
            inset: 0;
            opacity: 0.5;
            animation: bottleFloat 6s ease-in-out infinite;
        }

        @keyframes bottleFloat {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-4px); }
        }

        .emotion-recipe-card {
            background: linear-gradient(135deg, rgba(255,255,255,0.08), rgba(255,255,255,0.02));
            backdrop-filter: blur(20px);
            border-radius: 12px;
            padding: 10px 12px;
            border: 1px solid rgba(255,255,255,0.1);
            width: 100%;
            max-width: 240px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.2);
        }

        .emotion-recipe-title {
            font-size: 8px;
            letter-spacing: 0.15em;
            color: rgba(255,255,255,0.4);
            text-transform: uppercase;
            margin-bottom: 8px;
            font-weight: bold;
            text-align: center;
            padding-bottom: 6px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .emotion-recipe-item {
            margin-bottom: 6px;
            padding: 2px 0;
        }

        .emotion-recipe-item-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2px;
        }

        .emotion-recipe-item-label {
            font-size: 8px;
            color: rgba(255,255,255,0.4);
            text-transform: uppercase;
            letter-spacing: 0.08em;
        }

        .emotion-recipe-item-value {
            font-size: 11px;
            color: rgba(255,255,255,0.9);
        }

        .emotion-recipe-item-desc {
            font-size: 8px;
            color: rgba(255,255,255,0.25);
            font-style: italic;
        }

        .emotion-progress-bar {
            height: 2px;
            background: rgba(255,255,255,0.1);
            margin-top: 4px;
            border-radius: 1px;
            overflow: hidden;
        }

        .emotion-progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #8b5cf6, #f472b6);
            transition: width 0.5s;
            border-radius: 1px;
        }

        .emotion-result-btns {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 6px;
            margin-top: 10px;
        }

        .emotion-result-btn {
            padding: 8px;
            border-radius: 8px;
            font-size: 8px;
            letter-spacing: 0.08em;
            text-transform: uppercase;
            cursor: pointer;
            transition: all 0.3s ease;
            font-family: 'VT323', monospace;
        }

        .emotion-result-btn.secondary {
            background: rgba(255,255,255,0.05);
            border: 1px solid rgba(255,255,255,0.15);
            color: rgba(255,255,255,0.7);
        }

        .emotion-result-btn.secondary:hover {
            background: rgba(255,255,255,0.1);
            border-color: rgba(255,255,255,0.25);
            transform: translateY(-1px);
        }

        .emotion-result-btn.primary {
            background: linear-gradient(135deg, #ffffff, #f5f5f5);
            border: none;
            color: #1a1a1a;
            font-weight: bold;
            box-shadow: 0 2px 10px rgba(255,255,255,0.2);
        }

        .emotion-result-btn.primary:hover {
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(255,255,255,0.3);
        }

        .win-icon.emotion {
            background: linear-gradient(180deg, #581c87 0%, #312e81 100%);
            border: 2px solid #1e1b4b;
            border-radius: 2px;
            position: relative;
        }
        .win-icon.emotion::before {
            content: '🍸';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 18px;
        }

        .win-icon.chat {
            background: linear-gradient(180deg, #1a3a2a 0%, #0d2a1a 100%);
            border: 2px solid #0a1f12;
            border-radius: 2px;
            position: relative;
        }
        .win-icon.chat::before {
            content: '💬';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 18px;
        }

        .win-icon.minesweeper {
            background: linear-gradient(180deg, #c0c0c0 0%, #a0a0a0 100%);
            border: 2px solid #808080;
            border-radius: 2px;
            position: relative;
        }
        .win-icon.minesweeper::before {
            content: '💣';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 18px;
        }

        .minesweeper-window {
            width: 280px;
            height: 360px;
        }

        .minesweeper-container {
            background: #c0c0c0;
            padding: 6px;
            height: 100%;
            box-sizing: border-box;
            display: flex;
            flex-direction: column;
        }

        .minesweeper-header {
            background: #c0c0c0;
            border: 2px solid;
            border-color: #808080 #ffffff #ffffff #808080;
            padding: 4px;
            margin-bottom: 6px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .minesweeper-counter {
            background: #000;
            color: #ff0000;
            font-family: 'VT323', monospace;
            font-size: 20px;
            padding: 2px 4px;
            min-width: 40px;
            text-align: center;
            border: 1px solid #808080;
        }

        .minesweeper-face {
            width: 26px;
            height: 26px;
            background: #c0c0c0;
            border: 2px solid;
            border-color: #ffffff #808080 #808080 #ffffff;
            cursor: pointer;
            font-size: 14px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .minesweeper-face:active {
            border-color: #808080 #ffffff #ffffff #808080;
        }

        .minesweeper-board {
            flex: 1;
            display: grid;
            gap: 0;
            border: 3px solid;
            border-color: #808080 #ffffff #ffffff #808080;
            background: #c0c0c0;
        }

        .mine-cell {
            width: 20px;
            height: 20px;
            background: #c0c0c0;
            border: 2px solid;
            border-color: #ffffff #808080 #808080 #ffffff;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
            font-weight: bold;
            cursor: pointer;
            font-family: 'VT323', monospace;
        }

        .mine-cell:active {
            border-color: #808080 #ffffff #ffffff #808080;
        }

        .mine-cell.revealed {
            border: 1px solid #808080;
            background: #c0c0c0;
            cursor: default;
        }

        .mine-cell.flagged::after {
            content: '🚩';
            font-size: 10px;
        }

        .mine-cell.mine {
            background: #ff0000;
        }

        .mine-cell.mine::after {
            content: '💣';
            font-size: 12px;
        }

        .mine-cell.num-1 { color: #0000ff; }
        .mine-cell.num-2 { color: #008000; }
        .mine-cell.num-3 { color: #ff0000; }
        .mine-cell.num-4 { color: #000080; }
        .mine-cell.num-5 { color: #800000; }
        .mine-cell.num-6 { color: #008080; }
        .mine-cell.num-7 { color: #000000; }
        .mine-cell.num-8 { color: #808080; }

        .calc-buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 2px;
            padding: 4px;
        }

        .calc-btn {
            height: 32px;
            background: var(--win-bg);
            border: 2px solid;
            border-color: var(--win-light) var(--win-dark) var(--win-dark) var(--win-light);
            cursor: pointer;
            font-size: 14px;
            font-family: 'VT323', monospace;
        }

        .calc-btn:active {
            border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
        }

        .calc-btn.operator {
            background: #d8d0c8;
        }

        @media (max-width: 480px) {
            .desktop-icons { 
                left: 8px; 
                top: 8px; 
                gap: 8px;
                grid-template-columns: repeat(2, 65px);
            }
            .desktop-icon { width: 65px; padding: 4px; }
            .icon-image { width: 32px; height: 32px; }
            .icon-label { font-size: 10px; max-width: 60px; }
            .win-icon { width: 32px; height: 32px; }
            .chat-window { top: 10px; left: 10px; width: calc(100% - 20px); height: 280px; }
            .paint-window, .notepad-window, .word-window, .calc-window {
                width: calc(100% - 20px);
                left: 10px !important;
            }
        }
    </style>
</head>
<body>
    <div class="sky-bg">
        <div class="cloud cloud-1"></div>
        <div class="cloud cloud-2"></div>
        <div class="cloud cloud-3"></div>
        <div class="cloud cloud-4"></div>
    </div>

    <div class="scanlines"></div>

    <div class="music-player paused" id="musicPlayer" style="display: none;">
        <div class="music-player-header" onmousedown="startMusicDrag(event)">
            <div class="music-player-title">
                <span>🎵</span>
                <span>千千静听</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeMusicPlayer()"></button>
                <button class="win-btn win-btn-close" onclick="toggleMusicPlayer()"></button>
            </div>
        </div>
        <div class="music-player-body">
            <div class="music-cover-area">
                <div class="music-cover" id="musicCover">🎵</div>
                <div class="music-info">
                    <div class="music-title" id="musicTitle">梦核漫游</div>
                    <div class="music-artist" id="musicArtist">未知艺术家</div>
                    <div class="music-album" id="musicAlbum">梦核精选集</div>
                </div>
            </div>
            <div class="music-progress-container">
                <div class="music-progress-bar" id="progressBar" onclick="seekMusic(event)">
                    <div class="music-progress-fill" id="progressFill"></div>
                </div>
                <div class="music-time">
                    <span id="currentTime">0:00</span>
                    <span id="totalTime">3:45</span>
                </div>
            </div>
            <div class="music-controls">
                <button class="music-btn" onclick="prevTrack()">⏮</button>
                <button class="music-btn play-pause" id="playPauseBtn" onclick="togglePlay()">▶</button>
                <button class="music-btn" onclick="nextTrack()">⏭</button>
            </div>
            <div class="music-volume-container">
                <span class="music-volume-icon" id="volumeIcon" onclick="toggleMute()">🔊</span>
                <div class="music-volume-slider" id="volumeSlider" onclick="setVolume(event)">
                    <div class="music-volume-fill" id="volumeFill"></div>
                </div>
            </div>
            <div class="music-visualizer">
                <div class="music-bar"></div>
                <div class="music-bar"></div>
                <div class="music-bar"></div>
                <div class="music-bar"></div>
                <div class="music-bar"></div>
                <div class="music-bar"></div>
                <div class="music-bar"></div>
                <div class="music-bar"></div>
            </div>
            <div class="music-playlist" id="musicPlaylist"></div>
        </div>
    </div>

    <div class="music-mini-icon" id="musicMiniIcon" onclick="restoreMusicPlayer()">🎵</div>

    <div class="alien-cat" id="alienCat">
        <div class="cat-speech" id="catSpeech">喵~</div>
        <div class="alien-cat-body">
            <div class="cat-head">
                <div class="cat-antenna left"></div>
                <div class="cat-antenna right"></div>
                <div class="cat-ear left">
                    <div class="cat-ear-inner"></div>
                </div>
                <div class="cat-ear right">
                    <div class="cat-ear-inner"></div>
                </div>
                <div class="cat-eye left"></div>
                <div class="cat-eye right"></div>
                <div class="cat-nose"></div>
                <div class="cat-mouth"></div>
                <div class="cat-whisker left-1"></div>
                <div class="cat-whisker left-2"></div>
                <div class="cat-whisker right-1"></div>
                <div class="cat-whisker right-2"></div>
            </div>
            <div class="cat-body-main">
                <div class="cat-paw left"></div>
                <div class="cat-paw right"></div>
            </div>
            <div class="cat-tail"></div>
        </div>
    </div>

    <div class="desktop-icons">
        <div class="desktop-icon" ondblclick="openWindow('chatWindow')" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon chat"></div></div>
            <span class="icon-label">Dream Entity</span>
        </div>
        <div class="desktop-icon" ondblclick="openWindow('myComputerWindow')" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon my-computer"></div></div>
            <span class="icon-label">我的电脑</span>
        </div>
        <div class="desktop-icon" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon recycle-bin"></div></div>
            <span class="icon-label">回收站</span>
        </div>
        <div class="desktop-icon" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon folder"></div></div>
            <span class="icon-label">我的文档</span>
        </div>
        <div class="desktop-icon" ondblclick="openWindow('notepadWindow')" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon notepad"></div></div>
            <span class="icon-label">记事本</span>
        </div>
        <div class="desktop-icon" ondblclick="openWindow('paintWindow')" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon paint"></div></div>
            <span class="icon-label">画图</span>
        </div>
        <div class="desktop-icon" ondblclick="openWindow('calcWindow')" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon calculator"></div></div>
            <span class="icon-label">计算器</span>
        </div>
        <div class="desktop-icon" ondblclick="openWindow('minesweeperWindow')" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon minesweeper"></div></div>
            <span class="icon-label">扫雷</span>
        </div>
        <div class="desktop-icon" ondblclick="openWindow('emotionWindow')" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon emotion"></div></div>
            <span class="icon-label">情绪调酒</span>
        </div>
        <div class="desktop-icon" ondblclick="openWindow('wordWindow')" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon word"></div></div>
            <span class="icon-label">Word</span>
        </div>
        <div class="desktop-icon" ondblclick="openWindow('excelWindow')" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon excel"></div></div>
            <span class="icon-label">Excel</span>
        </div>
        <div class="desktop-icon" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon settings"></div></div>
            <span class="icon-label">设置</span>
        </div>
        <div class="desktop-icon" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon internet"></div></div>
            <span class="icon-label">Internet</span>
        </div>
        <div class="desktop-icon" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon games"></div></div>
            <span class="icon-label">游戏</span>
        </div>
    </div>

    <div class="win-window chat-window" id="chatWindow" style="display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'chatWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">💬</div>
                <span class="win-titlebar-text">Dream Entity - 聊天</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('chatWindow')"></button>
                <button class="win-btn win-btn-maximize"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('chatWindow')"></button>
            </div>
        </div>
        <div class="win-menubar">
            <span class="win-menu-item">文件(F)</span>
            <span class="win-menu-item">编辑(E)</span>
            <span class="win-menu-item">查看(V)</span>
            <span class="win-menu-item">帮助(H)</span>
        </div>
        <div class="win-content chat-content">
            <div class="chat-messages" id="chatMessages">
                <div class="message received">i potato you</div>
            </div>
            <div class="chat-input-area" ondblclick="openWindow('keyboardWindow')">
                <input type="text" class="chat-input" id="chatInput" placeholder="输入消息..." autocomplete="off">
                <button class="win-btn-send" id="sendBtn">发送</button>
            </div>
        </div>
        <div class="win-statusbar">
            <div class="win-statusbar-section">就绪</div>
            <div class="win-statusbar-section" style="flex: 0; width: 60px;">在线</div>
        </div>
    </div>

    <div class="win-window keyboard-window" id="keyboardWindow" style="top: 280px; left: 120px; display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'keyboardWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">⌨</div>
                <span class="win-titlebar-text">屏幕键盘</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('keyboardWindow')"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('keyboardWindow')"></button>
            </div>
        </div>
        <div class="keyboard-content" id="keyboard">
            <div class="keyboard-row">
                <div class="osk-key" data-key="`">`</div>
                <div class="osk-key" data-key="1">1</div>
                <div class="osk-key" data-key="2">2</div>
                <div class="osk-key" data-key="3">3</div>
                <div class="osk-key" data-key="4">4</div>
                <div class="osk-key" data-key="5">5</div>
                <div class="osk-key" data-key="6">6</div>
                <div class="osk-key" data-key="7">7</div>
                <div class="osk-key" data-key="8">8</div>
                <div class="osk-key" data-key="9">9</div>
                <div class="osk-key" data-key="0">0</div>
                <div class="osk-key" data-key="-">-</div>
                <div class="osk-key" data-key="=">=</div>
                <div class="osk-key backspace" data-key="Backspace">←</div>
            </div>
            <div class="keyboard-row">
                <div class="osk-key tab" data-key="Tab">Tab</div>
                <div class="osk-key" data-key="q">Q</div>
                <div class="osk-key" data-key="w">W</div>
                <div class="osk-key" data-key="e">E</div>
                <div class="osk-key" data-key="r">R</div>
                <div class="osk-key" data-key="t">T</div>
                <div class="osk-key" data-key="y">Y</div>
                <div class="osk-key" data-key="u">U</div>
                <div class="osk-key" data-key="i">I</div>
                <div class="osk-key" data-key="o">O</div>
                <div class="osk-key" data-key="p">P</div>
                <div class="osk-key" data-key="[">[</div>
                <div class="osk-key" data-key="]">]</div>
                <div class="osk-key" data-key="\">\</div>
            </div>
            <div class="keyboard-row">
                <div class="osk-key caps" data-key="CapsLock">Caps</div>
                <div class="osk-key" data-key="a">A</div>
                <div class="osk-key" data-key="s">S</div>
                <div class="osk-key" data-key="d">D</div>
                <div class="osk-key" data-key="f">F</div>
                <div class="osk-key" data-key="g">G</div>
                <div class="osk-key" data-key="h">H</div>
                <div class="osk-key" data-key="j">J</div>
                <div class="osk-key" data-key="k">K</div>
                <div class="osk-key" data-key="l">L</div>
                <div class="osk-key" data-key=";">;</div>
                <div class="osk-key" data-key="'">'</div>
                <div class="osk-key enter" data-key="Enter">回车</div>
            </div>
            <div class="keyboard-row">
                <div class="osk-key shift" data-key="Shift">Shift</div>
                <div class="osk-key" data-key="z">Z</div>
                <div class="osk-key" data-key="x">X</div>
                <div class="osk-key" data-key="c">C</div>
                <div class="osk-key" data-key="v">V</div>
                <div class="osk-key" data-key="b">B</div>
                <div class="osk-key" data-key="n">N</div>
                <div class="osk-key" data-key="m">M</div>
                <div class="osk-key" data-key=",">,</div>
                <div class="osk-key" data-key=".">.</div>
                <div class="osk-key" data-key="/">/</div>
                <div class="osk-key shift" data-key="Shift">Shift</div>
            </div>
            <div class="keyboard-row">
                <div class="osk-key ctrl" data-key="Control">Ctrl</div>
                <div class="osk-key alt" data-key="Alt">Alt</div>
                <div class="osk-key space" data-key=" ">空格</div>
                <div class="osk-key alt" data-key="Alt">Alt</div>
                <div class="osk-key ctrl" data-key="Control">Ctrl</div>
            </div>
        </div>
    </div>

    <div class="win-window paint-window" id="paintWindow" style="top: 100px; left: 200px; display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'paintWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">🎨</div>
                <span class="win-titlebar-text">画图</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('paintWindow')"></button>
                <button class="win-btn win-btn-maximize"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('paintWindow')"></button>
            </div>
        </div>
        <div class="win-menubar">
            <span class="win-menu-item">文件(F)</span>
            <span class="win-menu-item">编辑(E)</span>
            <span class="win-menu-item">查看(V)</span>
            <span class="win-menu-item">图像(I)</span>
            <span class="win-menu-item">颜色(C)</span>
            <span class="win-menu-item">帮助(H)</span>
        </div>
        <div class="paint-tools">
            <div class="paint-tool active" data-tool="brush" title="画笔">✏</div>
            <div class="paint-tool" data-tool="eraser" title="橡皮">🧽</div>
            <div class="paint-tool" data-tool="fill" title="填充">🪣</div>
            <div class="paint-tool" data-tool="line" title="直线">📏</div>
        </div>
        <div class="color-palette" id="colorPalette"></div>
        <div class="win-content">
            <canvas class="paint-canvas" id="paintCanvas"></canvas>
        </div>
        <div class="win-statusbar">
            <div class="win-statusbar-section">工具: 画笔</div>
        </div>
    </div>

    <div class="win-window notepad-window" id="notepadWindow" style="top: 120px; left: 250px; display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'notepadWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">📝</div>
                <span class="win-titlebar-text">记事本</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('notepadWindow')"></button>
                <button class="win-btn win-btn-maximize"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('notepadWindow')"></button>
            </div>
        </div>
        <div class="win-menubar">
            <span class="win-menu-item">文件(F)</span>
            <span class="win-menu-item">编辑(E)</span>
            <span class="win-menu-item">格式(O)</span>
            <span class="win-menu-item">查看(V)</span>
            <span class="win-menu-item">帮助(H)</span>
        </div>
        <div class="win-content">
            <textarea class="notepad-textarea" placeholder="在此输入文字..."></textarea>
        </div>
    </div>

    <div class="win-window word-window" id="wordWindow" style="top: 80px; left: 300px; display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'wordWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">📄</div>
                <span class="win-titlebar-text">Microsoft Word</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('wordWindow')"></button>
                <button class="win-btn win-btn-maximize"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('wordWindow')"></button>
            </div>
        </div>
        <div class="win-menubar">
            <span class="win-menu-item">文件(F)</span>
            <span class="win-menu-item">编辑(E)</span>
            <span class="win-menu-item">视图(V)</span>
            <span class="win-menu-item">插入(I)</span>
            <span class="win-menu-item">格式(O)</span>
            <span class="win-menu-item">工具(T)</span>
            <span class="win-menu-item">帮助(H)</span>
        </div>
        <div class="win-content">
            <textarea class="word-textarea" placeholder="在此输入文档内容..."></textarea>
        </div>
        <div class="win-statusbar">
            <div class="win-statusbar-section">第 1 页</div>
        </div>
    </div>

    <div class="win-window calc-window" id="calcWindow" style="top: 100px; left: 350px; display: none; width: 240px; height: auto;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'calcWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">🔢</div>
                <span class="win-titlebar-text">计算器</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('calcWindow')"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('calcWindow')"></button>
            </div>
        </div>
        <div class="calc-display" id="calcDisplay">0</div>
        <div class="calc-buttons">
            <button class="calc-btn" onclick="calcInput('C')">C</button>
            <button class="calc-btn" onclick="calcInput('CE')">CE</button>
            <button class="calc-btn" onclick="calcInput('←')">←</button>
            <button class="calc-btn operator" onclick="calcInput('/')">÷</button>
            <button class="calc-btn" onclick="calcInput('7')">7</button>
            <button class="calc-btn" onclick="calcInput('8')">8</button>
            <button class="calc-btn" onclick="calcInput('9')">9</button>
            <button class="calc-btn operator" onclick="calcInput('*')">×</button>
            <button class="calc-btn" onclick="calcInput('4')">4</button>
            <button class="calc-btn" onclick="calcInput('5')">5</button>
            <button class="calc-btn" onclick="calcInput('6')">6</button>
            <button class="calc-btn operator" onclick="calcInput('-')">−</button>
            <button class="calc-btn" onclick="calcInput('1')">1</button>
            <button class="calc-btn" onclick="calcInput('2')">2</button>
            <button class="calc-btn" onclick="calcInput('3')">3</button>
            <button class="calc-btn operator" onclick="calcInput('+')">+</button>
            <button class="calc-btn" onclick="calcInput('±')">±</button>
            <button class="calc-btn" onclick="calcInput('0')">0</button>
            <button class="calc-btn" onclick="calcInput('.')">.</button>
            <button class="calc-btn operator" onclick="calcInput('=')">=</button>
        </div>
    </div>

    <div class="win-window" id="myComputerWindow" style="top: 80px; left: 180px; width: 450px; height: 300px; display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'myComputerWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">💻</div>
                <span class="win-titlebar-text">我的电脑</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('myComputerWindow')"></button>
                <button class="win-btn win-btn-maximize"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('myComputerWindow')"></button>
            </div>
        </div>
        <div class="win-menubar">
            <span class="win-menu-item">文件(F)</span>
            <span class="win-menu-item">编辑(E)</span>
            <span class="win-menu-item">查看(V)</span>
            <span class="win-menu-item">帮助(H)</span>
        </div>
        <div class="win-content" style="background: white; padding: 10px; display: flex; flex-wrap: wrap; gap: 20px; align-content: flex-start;">
            <div style="text-align: center; cursor: pointer;">
                <div style="font-size: 32px;">💾</div>
                <div style="font-size: 11px;">本地磁盘 (C:)</div>
            </div>
            <div style="text-align: center; cursor: pointer;">
                <div style="font-size: 32px;">💿</div>
                <div style="font-size: 11px;">DVD驱动器 (D:)</div>
            </div>
            <div style="text-align: center; cursor: pointer;">
                <div style="font-size: 32px;">📁</div>
                <div style="font-size: 11px;">共享文件夹</div>
            </div>
            <div style="text-align: center; cursor: pointer;">
                <div style="font-size: 32px;">🖨️</div>
                <div style="font-size: 11px;">打印机</div>
            </div>
        </div>
        <div class="win-statusbar">
            <div class="win-statusbar-section">4 个对象</div>
        </div>
    </div>

    <div class="win-window" id="excelWindow" style="top: 90px; left: 280px; width: 420px; height: 280px; display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'excelWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">📊</div>
                <span class="win-titlebar-text">Microsoft Excel</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('excelWindow')"></button>
                <button class="win-btn win-btn-maximize"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('excelWindow')"></button>
            </div>
        </div>
        <div class="win-menubar">
            <span class="win-menu-item">文件(F)</span>
            <span class="win-menu-item">编辑(E)</span>
            <span class="win-menu-item">视图(V)</span>
            <span class="win-menu-item">插入(I)</span>
            <span class="win-menu-item">格式(O)</span>
        </div>
        <div class="win-content" style="background: white; overflow: auto;">
            <table style="border-collapse: collapse; width: 100%; font-size: 12px;">
                <tr style="background: #e0e0e0;">
                    <th style="border: 1px solid #808080; padding: 2px 6px; width: 30px;"></th>
                    <th style="border: 1px solid #808080; padding: 2px 6px;">A</th>
                    <th style="border: 1px solid #808080; padding: 2px 6px;">B</th>
                    <th style="border: 1px solid #808080; padding: 2px 6px;">C</th>
                    <th style="border: 1px solid #808080; padding: 2px 6px;">D</th>
                </tr>
                <tr><td style="border: 1px solid #808080; padding: 2px 6px; background: #e0e0e0;">1</td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td></tr>
                <tr><td style="border: 1px solid #808080; padding: 2px 6px; background: #e0e0e0;">2</td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td></tr>
                <tr><td style="border: 1px solid #808080; padding: 2px 6px; background: #e0e0e0;">3</td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td></tr>
                <tr><td style="border: 1px solid #808080; padding: 2px 6px; background: #e0e0e0;">4</td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td></tr>
                <tr><td style="border: 1px solid #808080; padding: 2px 6px; background: #e0e0e0;">5</td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td><td style="border: 1px solid #808080; padding: 2px 6px;"></td></tr>
            </table>
        </div>
        <div class="win-statusbar">
            <div class="win-statusbar-section">就绪</div>
        </div>
    </div>

    <div class="win-window emotion-bar-window" id="emotionWindow" style="top: 30px; left: 200px; display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'emotionWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">🍸</div>
                <span class="win-titlebar-text">情绪调酒</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('emotionWindow')"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('emotionWindow')"></button>
            </div>
        </div>
        <div class="win-content" style="padding: 0;">
            <div class="emotion-bar-container" id="emotionContainer">
                <div id="emotionMixingView" class="emotion-mixing-view">
                    <div class="emotion-glass">
                        <div class="emotion-glass-frame"></div>
                        <div class="emotion-liquid calm" id="emotionLiquid" style="height: 50%;"></div>
                        <div class="emotion-wave calm" id="emotionWave"></div>
                    </div>
                    <div class="emotion-slider-container">
                        <div class="emotion-slider-track">
                            <div class="emotion-slider-dot" id="emotionDot" style="left: 50%;"></div>
                            <input type="range" min="-100" max="100" value="0" class="emotion-slider-input" id="emotionSlider">
                        </div>
                        <div class="emotion-labels">
                            <span>Deep</span>
                            <span id="emotionStatus">Calm</span>
                            <span>Bright</span>
                        </div>
                    </div>
                    <button class="emotion-btn" id="emotionBtn" onclick="startEmotionMixing()">
                        开始调制你的特调情绪饮品
                    </button>
                </div>
                <div id="emotionResultView" style="display: none;" class="emotion-result-view emotion-result">
                    <div class="emotion-result-title" id="emotionDrinkName">午夜可可 · 轻酿版</div>
                    <div class="emotion-result-subtitle">Midnight Cacao Mild</div>
                    <div class="emotion-bottle">
                        <div class="emotion-bottle-liquid calm" id="emotionBottleLiquid"></div>
                    </div>
                    <div class="emotion-recipe-card">
                        <div class="emotion-recipe-title">你的情绪配方</div>
                        <div class="emotion-recipe-item">
                            <div class="emotion-recipe-item-header">
                                <span class="emotion-recipe-item-label">基酒</span>
                                <span class="emotion-recipe-item-value" id="emotionBase">Deep Liquor</span>
                            </div>
                            <div class="emotion-recipe-item-desc" id="emotionBaseDesc">带一点沉稳与深色调</div>
                        </div>
                        <div class="emotion-recipe-item">
                            <div class="emotion-recipe-item-header">
                                <span class="emotion-recipe-item-label">前调</span>
                                <span class="emotion-recipe-item-value" id="emotionTopNote">柠檬皮 · 迷迭香</span>
                            </div>
                            <div class="emotion-recipe-item-desc" id="emotionTopNoteDesc">来自你语句中的紧绷与急促</div>
                        </div>
                        <div class="emotion-recipe-item">
                            <div class="emotion-recipe-item-header">
                                <span class="emotion-recipe-item-label">浓度</span>
                                <span class="emotion-recipe-item-value" id="emotionConcentration">0.63 中度酿制</span>
                            </div>
                            <div class="emotion-progress-bar">
                                <div class="emotion-progress-fill" id="emotionProgress" style="width: 63%;"></div>
                            </div>
                        </div>
                        <div class="emotion-recipe-item">
                            <div class="emotion-recipe-item-header">
                                <span class="emotion-recipe-item-label">体感</span>
                                <span class="emotion-recipe-item-value" id="emotionBodyFeeling">Tight 紧绷</span>
                            </div>
                        </div>
                        <div class="emotion-result-btns">
                            <button class="emotion-result-btn secondary" onclick="resetEmotion()">再调一杯</button>
                            <button class="emotion-result-btn primary" onclick="closeWindow('emotionWindow')">完成</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="win-window minesweeper-window" id="minesweeperWindow" style="top: 50px; left: 150px; display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'minesweeperWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">💣</div>
                <span class="win-titlebar-text">扫雷</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('minesweeperWindow')"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('minesweeperWindow')"></button>
            </div>
        </div>
        <div class="win-content" style="padding: 0;">
            <div class="minesweeper-container">
                <div class="minesweeper-header">
                    <div class="minesweeper-counter" id="mineCount">010</div>
                    <div class="minesweeper-face" id="mineFace" onclick="initMinesweeper()">😊</div>
                    <div class="minesweeper-counter" id="mineTimer">000</div>
                </div>
                <div class="minesweeper-board" id="mineBoard"></div>
            </div>
        </div>
    </div>

    <div class="taskbar">
        <button class="start-btn">
            <span style="font-size: 14px;">🪟</span>
            开始
        </button>
        <div class="taskbar-windows">
            <div class="taskbar-item" id="taskbar-chatWindow" onclick="toggleWindow('chatWindow')" style="display: none;">
                <span>💬</span>
                <span>Dream Entity</span>
            </div>
            <div class="taskbar-item" id="taskbar-paintWindow" onclick="toggleWindow('paintWindow')" style="display: none;">
                <span>🎨</span>
                <span>画图</span>
            </div>
            <div class="taskbar-item" id="taskbar-notepadWindow" onclick="toggleWindow('notepadWindow')" style="display: none;">
                <span>📝</span>
                <span>记事本</span>
            </div>
            <div class="taskbar-item" id="taskbar-wordWindow" onclick="toggleWindow('wordWindow')" style="display: none;">
                <span>📄</span>
                <span>Word</span>
            </div>
            <div class="taskbar-item" id="taskbar-calcWindow" onclick="toggleWindow('calcWindow')" style="display: none;">
                <span>🔢</span>
                <span>计算器</span>
            </div>
            <div class="taskbar-item" id="taskbar-myComputerWindow" onclick="toggleWindow('myComputerWindow')" style="display: none;">
                <span>💻</span>
                <span>我的电脑</span>
            </div>
            <div class="taskbar-item" id="taskbar-excelWindow" onclick="toggleWindow('excelWindow')" style="display: none;">
                <span>📊</span>
                <span>Excel</span>
            </div>
            <div class="taskbar-item" id="taskbar-emotionWindow" onclick="toggleWindow('emotionWindow')" style="display: none;">
                <span>🍸</span>
                <span>情绪调酒</span>
            </div>
            <div class="taskbar-item" id="taskbar-minesweeperWindow" onclick="toggleWindow('minesweeperWindow')" style="display: none;">
                <span>💣</span>
                <span>扫雷</span>
            </div>
            <div class="taskbar-item" id="taskbar-keyboardWindow" onclick="toggleWindow('keyboardWindow')" style="display: none;">
                <span>⌨</span>
                <span>屏幕键盘</span>
            </div>
        </div>
        <div class="taskbar-tray">
            <span id="taskbarTime">00:00</span>
        </div>
    </div>

    <script>
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();
        
        function playMechanicalKeySound() {
            const now = audioContext.currentTime;
            
            const clickOsc = audioContext.createOscillator();
            const clickGain = audioContext.createGain();
            const clickFilter = audioContext.createBiquadFilter();
            
            clickFilter.type = 'highpass';
            clickFilter.frequency.value = 2000;
            
            clickOsc.type = 'square';
            clickOsc.frequency.setValueAtTime(800 + Math.random() * 400, now);
            clickOsc.frequency.exponentialRampToValueAtTime(200, now + 0.015);
            
            clickGain.gain.setValueAtTime(0.15, now);
            clickGain.gain.exponentialRampToValueAtTime(0.001, now + 0.02);
            
            clickOsc.connect(clickFilter);
            clickFilter.connect(clickGain);
            clickGain.connect(audioContext.destination);
            
            clickOsc.start(now);
            clickOsc.stop(now + 0.02);
            
            const clackOsc = audioContext.createOscillator();
            const clackGain = audioContext.createGain();
            
            clackOsc.type = 'triangle';
            clackOsc.frequency.setValueAtTime(150 + Math.random() * 50, now + 0.01);
            
            clackGain.gain.setValueAtTime(0.08, now + 0.01);
            clackGain.gain.exponentialRampToValueAtTime(0.001, now + 0.05);
            
            clackOsc.connect(clackGain);
            clackGain.connect(audioContext.destination);
            
            clackOsc.start(now + 0.01);
            clackOsc.stop(now + 0.05);
        }

        let highestZIndex = 100;
        const windows = {};
        let dragState = null;

        let emotionValence = 0;
        let emotionAnalyzing = false;

        const emotionDrinks = [
            { name: '午夜可可 · 轻酿版', subtitle: 'Midnight Cacao Mild', base: 'Deep Liquor', baseDesc: '带一点沉稳与深色调' },
            { name: '晨曦蜜桃 · 微醺', subtitle: 'Dawn Peach Tipsy', base: 'Bright Spirit', baseDesc: '明亮而温暖的基调' },
            { name: '静谧海洋 · 纯酿', subtitle: 'Silent Ocean Pure', base: 'Calm Wave', baseDesc: '平静而深邃的底蕴' },
            { name: '星尘幻想 · 特调', subtitle: 'Stardust Fantasy', base: 'Dream Essence', baseDesc: '梦幻般的轻盈感' },
            { name: '暮光玫瑰 · 轻柔', subtitle: 'Twilight Rose Soft', base: 'Gentle Petal', baseDesc: '温柔而浪漫的芬芳' }
        ];

        const emotionTopNotes = [
            { name: '柠檬皮 · 迷迭香', desc: '来自你语句中的紧绷与急促' },
            { name: '薰衣草 · 蜂蜜', desc: '来自你内心的柔软与渴望' },
            { name: '橙花 · 佛手柑', desc: '来自你思绪中的明亮与希望' },
            { name: '雪松 · 琥珀', desc: '来自你深处的沉稳与力量' },
            { name: '茉莉 · 香草', desc: '来自你情感的细腻与温柔' },
            { name: '薄荷 · 青柠', desc: '来自你心境的清新与活力' }
        ];

        const emotionBodyFeelings = [
            { name: 'Tight 紧绷', desc: '需要放松' },
            { name: 'Soft 柔和', desc: '温暖舒适' },
            { name: 'Fresh 清新', desc: '轻盈通透' },
            { name: 'Deep 深沉', desc: '内敛厚重' },
            { name: 'Warm 温暖', desc: '安心治愈' },
            { name: 'Cool 清凉', desc: '冷静平和' }
        ];

        function initEmotionBar() {
            const slider = document.getElementById('emotionSlider');
            if (!slider) return;
            
            slider.addEventListener('input', (e) => {
                emotionValence = parseInt(e.target.value) / 100;
                updateEmotionUI();
            });
        }

        function updateEmotionUI() {
            const liquid = document.getElementById('emotionLiquid');
            const wave = document.getElementById('emotionWave');
            const dot = document.getElementById('emotionDot');
            const container = document.getElementById('emotionContainer');
            const status = document.getElementById('emotionStatus');
            
            const height = (emotionValence + 1) * 40 + 20;
            liquid.style.height = height + '%';
            
            const dotPos = (emotionValence + 1) * 50;
            dot.style.left = dotPos + '%';
            
            let style = 'calm';
            let label = 'Calm';
            
            if (emotionValence > 0.3) {
                style = 'bright';
                label = 'Bright';
            } else if (emotionValence < -0.3) {
                style = 'deep';
                label = 'Deep';
            }
            
            liquid.className = 'emotion-liquid ' + style;
            wave.className = 'emotion-wave ' + style;
            container.className = 'emotion-bar-container ' + style;
            status.textContent = emotionAnalyzing ? 'Capturing Essence...' : label;
        }

        function startEmotionMixing() {
            if (emotionAnalyzing) return;
            
            emotionAnalyzing = true;
            const btn = document.getElementById('emotionBtn');
            btn.disabled = true;
            btn.textContent = '正在调和你的情绪基酒...';
            
            updateEmotionUI();
            
            setTimeout(() => {
                emotionAnalyzing = false;
                btn.disabled = false;
                showEmotionResult();
            }, 2000);
        }

        function showEmotionResult() {
            document.getElementById('emotionMixingView').style.display = 'none';
            document.getElementById('emotionResultView').style.display = 'block';
            
            const drink = emotionDrinks[Math.floor(Math.random() * emotionDrinks.length)];
            const topNote = emotionTopNotes[Math.floor(Math.random() * emotionTopNotes.length)];
            const bodyFeeling = emotionBodyFeelings[Math.floor(Math.random() * emotionBodyFeelings.length)];
            
            document.getElementById('emotionDrinkName').textContent = drink.name;
            document.getElementById('emotionBase').textContent = drink.base;
            document.getElementById('emotionBaseDesc').textContent = drink.baseDesc;
            document.getElementById('emotionTopNote').textContent = topNote.name;
            document.getElementById('emotionTopNoteDesc').textContent = topNote.desc;
            document.getElementById('emotionBodyFeeling').textContent = bodyFeeling.name;
            
            const concentration = (Math.random() * 0.5 + 0.3).toFixed(2);
            document.getElementById('emotionConcentration').textContent = concentration + ' 中度酿制';
            document.getElementById('emotionProgress').style.width = (concentration * 100) + '%';
            
            let style = 'calm';
            if (emotionValence > 0.3) style = 'bright';
            else if (emotionValence < -0.3) style = 'deep';
            
            const bottleLiquid = document.getElementById('emotionBottleLiquid');
            bottleLiquid.className = 'emotion-bottle-liquid ' + style;
        }

        function resetEmotion() {
            document.getElementById('emotionMixingView').style.display = 'block';
            document.getElementById('emotionResultView').style.display = 'none';
            document.getElementById('emotionBtn').textContent = '开始调制你的特调情绪饮品';
        }

        function selectIcon(el) {
            document.querySelectorAll('.desktop-icon').forEach(i => i.classList.remove('selected'));
            el.classList.add('selected');
        }

        function openWindow(windowId) {
            const win = document.getElementById(windowId);
            if (win) {
                win.style.display = 'flex';
                win.classList.remove('minimized-window');
                setActiveWindow(windowId);
                
                const taskbarItem = document.getElementById('taskbar-' + windowId);
                if (taskbarItem) taskbarItem.style.display = 'flex';
                
                if (windowId === 'paintWindow') {
                    setTimeout(initPaint, 100);
                }
                if (windowId === 'emotionWindow') {
                    setTimeout(initEmotionBar, 100);
                }
                if (windowId === 'minesweeperWindow') {
                    setTimeout(initMinesweeper, 100);
                }
            }
        }

        let paintCanvas, paintCtx, isPainting = false, currentColor = '#000000', currentTool = 'brush';

        function initPaint() {
            paintCanvas = document.getElementById('paintCanvas');
            if (!paintCanvas) return;
            
            const container = paintCanvas.parentElement;
            paintCanvas.width = container.clientWidth - 4;
            paintCanvas.height = container.clientHeight - 4;
            paintCtx = paintCanvas.getContext('2d');
            paintCtx.fillStyle = 'white';
            paintCtx.fillRect(0, 0, paintCanvas.width, paintCanvas.height);
            
            const palette = document.getElementById('colorPalette');
            if (palette && palette.children.length === 0) {
                const colors = ['#000000', '#ffffff', '#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff', '#00ffff', '#808080', '#800000', '#008000', '#000080', '#808000', '#800080', '#008080', '#c0c0c0'];
                colors.forEach(c => {
                    const swatch = document.createElement('div');
                    swatch.className = 'color-swatch';
                    swatch.style.background = c;
                    swatch.onclick = () => {
                        currentColor = c;
                        document.querySelectorAll('.color-swatch').forEach(s => s.style.outline = 'none');
                        swatch.style.outline = '2px solid #000080';
                    };
                    palette.appendChild(swatch);
                });
            }
            
            paintCanvas.onmousedown = (e) => { isPainting = true; draw(e); };
            paintCanvas.onmousemove = (e) => { if (isPainting) draw(e); };
            paintCanvas.onmouseup = () => isPainting = false;
            paintCanvas.onmouseleave = () => isPainting = false;
        }

        function draw(e) {
            if (!paintCtx) return;
            const rect = paintCanvas.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;
            
            paintCtx.beginPath();
            paintCtx.arc(x, y, currentTool === 'eraser' ? 10 : 3, 0, Math.PI * 2);
            paintCtx.fillStyle = currentTool === 'eraser' ? 'white' : currentColor;
            paintCtx.fill();
        }

        document.querySelectorAll('.paint-tool').forEach(tool => {
            tool.onclick = () => {
                document.querySelectorAll('.paint-tool').forEach(t => t.classList.remove('active'));
                tool.classList.add('active');
                currentTool = tool.dataset.tool;
            };
        });

        let calcValue = '0';
        let calcOperator = '';
        let calcNewNumber = true;

        const playlist = [
            { title: '梦核漫游', artist: '梦境旅者', album: '梦核精选集', duration: 225, cover: '🎵' },
            { title: '云端漫步', artist: '云朵诗人', album: '天空之城', duration: 198, cover: '☁️' },
            { title: '薄荷夏日', artist: '清凉微风', album: '夏日回忆', duration: 240, cover: '🌿' },
            { title: '像素世界', artist: '复古玩家', album: '8-bit Dreams', duration: 180, cover: '🎮' },
            { title: '星河漫步', artist: '宇宙旅人', album: '银河系漫游指南', duration: 210, cover: '✨' }
        ];

        let currentTrack = 0;
        let isPlaying = false;
        let currentTime = 0;
        let volume = 0.7;
        let isMuted = false;
        let musicDragState = null;
        let progressInterval = null;

        function initMusicPlayer() {
            const playlistEl = document.getElementById('musicPlaylist');
            playlist.forEach((track, index) => {
                const item = document.createElement('div');
                item.className = 'music-playlist-item' + (index === 0 ? ' active' : '');
                item.onclick = () => playTrack(index);
                item.innerHTML = `
                    <span class="music-playlist-item-num">${index + 1}.</span>
                    <span>${track.title}</span>
                `;
                playlistEl.appendChild(item);
            });
            updateTrackInfo();
        }

        function updateTrackInfo() {
            const track = playlist[currentTrack];
            document.getElementById('musicTitle').textContent = track.title;
            document.getElementById('musicArtist').textContent = track.artist;
            document.getElementById('musicAlbum').textContent = track.album;
            document.getElementById('musicCover').textContent = track.cover;
            document.getElementById('totalTime').textContent = formatTime(track.duration);
            document.getElementById('progressFill').style.width = '0%';
            currentTime = 0;
            document.getElementById('currentTime').textContent = '0:00';
            
            document.querySelectorAll('.music-playlist-item').forEach((item, index) => {
                item.classList.toggle('active', index === currentTrack);
            });
        }

        function formatTime(seconds) {
            const mins = Math.floor(seconds / 60);
            const secs = Math.floor(seconds % 60);
            return `${mins}:${secs.toString().padStart(2, '0')}`;
        }

        function togglePlay() {
            isPlaying = !isPlaying;
            const player = document.getElementById('musicPlayer');
            const btn = document.getElementById('playPauseBtn');
            
            if (isPlaying) {
                player.classList.remove('paused');
                btn.textContent = '⏸';
                startProgress();
            } else {
                player.classList.add('paused');
                btn.textContent = '▶';
                stopProgress();
            }
            updateMiniIconState();
        }

        function startProgress() {
            stopProgress();
            progressInterval = setInterval(() => {
                const track = playlist[currentTrack];
                currentTime++;
                if (currentTime >= track.duration) {
                    nextTrack();
                    return;
                }
                const progress = (currentTime / track.duration) * 100;
                document.getElementById('progressFill').style.width = progress + '%';
                document.getElementById('currentTime').textContent = formatTime(currentTime);
            }, 1000);
        }

        function stopProgress() {
            if (progressInterval) {
                clearInterval(progressInterval);
                progressInterval = null;
            }
        }

        function prevTrack() {
            currentTrack = (currentTrack - 1 + playlist.length) % playlist.length;
            updateTrackInfo();
            if (isPlaying) startProgress();
        }

        function nextTrack() {
            currentTrack = (currentTrack + 1) % playlist.length;
            updateTrackInfo();
            if (isPlaying) startProgress();
        }

        function playTrack(index) {
            currentTrack = index;
            updateTrackInfo();
            if (!isPlaying) togglePlay();
            else startProgress();
        }

        function seekMusic(e) {
            const bar = document.getElementById('progressBar');
            const rect = bar.getBoundingClientRect();
            const percent = (e.clientX - rect.left) / rect.width;
            const track = playlist[currentTrack];
            currentTime = Math.floor(percent * track.duration);
            document.getElementById('progressFill').style.width = (percent * 100) + '%';
            document.getElementById('currentTime').textContent = formatTime(currentTime);
        }

        function setVolume(e) {
            const slider = document.getElementById('volumeSlider');
            const rect = slider.getBoundingClientRect();
            volume = Math.max(0, Math.min(1, (e.clientX - rect.left) / rect.width));
            isMuted = false;
            updateVolumeUI();
        }

        function toggleMute() {
            isMuted = !isMuted;
            updateVolumeUI();
        }

        function updateVolumeUI() {
            const fill = document.getElementById('volumeFill');
            const icon = document.getElementById('volumeIcon');
            if (isMuted || volume === 0) {
                fill.style.width = '0%';
                icon.textContent = '🔇';
            } else {
                fill.style.width = (volume * 100) + '%';
                icon.textContent = volume < 0.5 ? '🔉' : '🔊';
            }
        }

        function toggleMusicPlayer() {
            const player = document.getElementById('musicPlayer');
            const miniIcon = document.getElementById('musicMiniIcon');
            player.style.display = player.style.display === 'none' ? 'block' : 'none';
            if (player.style.display === 'none') {
                miniIcon.style.display = 'flex';
            } else {
                miniIcon.style.display = 'none';
            }
        }

        function minimizeMusicPlayer() {
            const player = document.getElementById('musicPlayer');
            const miniIcon = document.getElementById('musicMiniIcon');
            player.classList.add('minimized');
            player.style.display = 'none';
            miniIcon.style.display = 'flex';
            updateMiniIconState();
        }

        function restoreMusicPlayer() {
            const player = document.getElementById('musicPlayer');
            const miniIcon = document.getElementById('musicMiniIcon');
            player.classList.remove('minimized');
            player.style.display = 'block';
            miniIcon.style.display = 'none';
        }

        function updateMiniIconState() {
            const miniIcon = document.getElementById('musicMiniIcon');
            if (isPlaying) {
                miniIcon.classList.add('playing');
            } else {
                miniIcon.classList.remove('playing');
            }
        }

        function startMusicDrag(e) {
            if (e.target.closest('.win-titlebar-controls')) return;
            e.preventDefault();
            const player = document.getElementById('musicPlayer');
            musicDragState = {
                startX: e.clientX,
                startY: e.clientY,
                origX: player.offsetLeft,
                origY: player.offsetTop
            };
            document.addEventListener('mousemove', onMusicDrag);
            document.addEventListener('mouseup', stopMusicDrag);
        }

        function onMusicDrag(e) {
            if (!musicDragState) return;
            const player = document.getElementById('musicPlayer');
            const dx = e.clientX - musicDragState.startX;
            const dy = e.clientY - musicDragState.startY;
            player.style.left = (musicDragState.origX + dx) + 'px';
            player.style.top = (musicDragState.origY + dy) + 'px';
            player.style.right = 'auto';
        }

        function stopMusicDrag() {
            musicDragState = null;
            document.removeEventListener('mousemove', onMusicDrag);
            document.removeEventListener('mouseup', stopMusicDrag);
        }

        function calcInput(key) {
            const display = document.getElementById('calcDisplay');
            
            if (key >= '0' && key <= '9') {
                if (calcNewNumber) {
                    calcValue = key;
                    calcNewNumber = false;
                } else {
                    calcValue = calcValue === '0' ? key : calcValue + key;
                }
            } else if (key === '.') {
                if (!calcValue.includes('.')) {
                    calcValue += '.';
                    calcNewNumber = false;
                }
            } else if (key === 'C') {
                calcValue = '0';
                calcOperator = '';
                calcNewNumber = true;
            } else if (key === 'CE') {
                calcValue = '0';
                calcNewNumber = true;
            } else if (key === '←') {
                calcValue = calcValue.length > 1 ? calcValue.slice(0, -1) : '0';
            } else if (key === '±') {
                calcValue = (parseFloat(calcValue) * -1).toString();
            } else if (['+', '-', '*', '/'].includes(key)) {
                calcOperator = key;
                calcValue = calcValue + ' ' + key + ' ';
                calcNewNumber = true;
            } else if (key === '=') {
                try {
                    calcValue = eval(calcValue).toString();
                } catch {
                    calcValue = 'Error';
                }
                calcNewNumber = true;
            }
            
            display.textContent = calcValue;
        }

        function initWindows() {
            document.querySelectorAll('.win-window').forEach(win => {
                windows[win.id] = {
                    element: win,
                    minimized: false,
                    position: { x: parseInt(win.style.left) || win.offsetLeft, y: parseInt(win.style.top) || win.offsetTop }
                };
            });
        }

        function setActiveWindow(windowId) {
            document.querySelectorAll('.win-window').forEach(w => {
                w.classList.remove('active');
                w.classList.add('inactive');
            });
            
            const win = document.getElementById(windowId);
            if (win) {
                win.classList.remove('inactive');
                win.classList.add('active');
                win.style.zIndex = ++highestZIndex;
            }
            
            updateTaskbar();
        }

        function startDrag(e, windowId) {
            if (e.target.closest('.win-titlebar-controls')) return;
            
            e.preventDefault();
            setActiveWindow(windowId);
            
            const win = document.getElementById(windowId);
            const rect = win.getBoundingClientRect();
            
            dragState = {
                windowId,
                startX: e.clientX,
                startY: e.clientY,
                origX: rect.left,
                origY: rect.top
            };
            
            document.addEventListener('mousemove', onDrag);
            document.addEventListener('mouseup', stopDrag);
        }

        function onDrag(e) {
            if (!dragState) return;
            
            const win = document.getElementById(dragState.windowId);
            const dx = e.clientX - dragState.startX;
            const dy = e.clientY - dragState.startY;
            
            let newX = dragState.origX + dx;
            let newY = dragState.origY + dy;
            
            newX = Math.max(0, Math.min(newX, window.innerWidth - 100));
            newY = Math.max(0, Math.min(newY, window.innerHeight - 100));
            
            win.style.left = newX + 'px';
            win.style.top = newY + 'px';
        }

        function stopDrag() {
            dragState = null;
            document.removeEventListener('mousemove', onDrag);
            document.removeEventListener('mouseup', stopDrag);
        }

        function minimizeWindow(windowId) {
            const win = document.getElementById(windowId);
            win.classList.add('minimized-window');
            if (windows[windowId]) windows[windowId].minimized = true;
            updateTaskbar();
        }

        function restoreWindow(windowId) {
            const win = document.getElementById(windowId);
            win.classList.remove('minimized-window');
            if (windows[windowId]) windows[windowId].minimized = false;
            setActiveWindow(windowId);
        }

        function closeWindow(windowId) {
            const win = document.getElementById(windowId);
            win.style.display = 'none';
            const taskbarItem = document.getElementById('taskbar-' + windowId);
            if (taskbarItem) taskbarItem.style.display = 'none';
            updateTaskbar();
        }

        function toggleWindow(windowId) {
            const win = document.getElementById(windowId);
            if (win.classList.contains('minimized-window')) {
                restoreWindow(windowId);
            } else {
                setActiveWindow(windowId);
            }
        }

        function updateTaskbar() {
            const items = document.querySelectorAll('.taskbar-item');
            items.forEach(item => {
                const windowId = item.getAttribute('onclick')?.match(/'(\w+)'/)?.[1];
                if (windowId) {
                    const win = document.getElementById(windowId);
                    if (win.classList.contains('active') && !win.classList.contains('minimized-window')) {
                        item.classList.add('active');
                    } else {
                        item.classList.remove('active');
                    }
                }
            });
        }

        function updateTaskbarTime() {
            const now = new Date();
            const hours = now.getHours().toString().padStart(2, '0');
            const minutes = now.getMinutes().toString().padStart(2, '0');
            document.getElementById('taskbarTime').textContent = `${hours}:${minutes}`;
        }

        const chatInput = document.getElementById('chatInput');
        const chatMessages = document.getElementById('chatMessages');
        const sendBtn = document.getElementById('sendBtn');
        const keyboard = document.getElementById('keyboard');

        const noteStyles = ['dreamcore', 'vaporwave', 'cyberpunk', 'nostalgic', 'ethereal'];
        
        function getCurrentTime() {
            const now = new Date();
            return `${now.getHours().toString().padStart(2, '0')}:${now.getMinutes().toString().padStart(2, '0')}:${now.getSeconds().toString().padStart(2, '0')}`;
        }
        
        let noteZIndex = 500;
        
        function createStickyNote(text) {
            const note = document.createElement('div');
            const style = noteStyles[Math.floor(Math.random() * noteStyles.length)];
            const time = getCurrentTime();
            
            note.className = `sticky-note ${style}`;
            note.style.zIndex = ++noteZIndex;
            
            const maxX = window.innerWidth - 180;
            const maxY = window.innerHeight - 150;
            
            note.style.left = `${Math.max(100, Math.random() * maxX)}px`;
            note.style.top = `${Math.max(50, Math.random() * maxY)}px`;
            
            note.innerHTML = `
                <span class="sticky-note-time">${time}</span>
                <button class="sticky-note-close">×</button>
                <div class="sticky-note-content">${text}</div>
            `;
            
            document.body.appendChild(note);
            makeDraggable(note);
            
            note.querySelector('.sticky-note-close').addEventListener('click', () => {
                note.remove();
            });
        }
        
        function makeDraggable(element) {
            let isDragging = false;
            let startX, startY, origX, origY;
            
            element.addEventListener('mousedown', (e) => {
                if (e.target.classList.contains('sticky-note-close')) return;
                isDragging = true;
                startX = e.clientX;
                startY = e.clientY;
                origX = element.offsetLeft;
                origY = element.offsetTop;
                element.style.zIndex = ++noteZIndex;
            });
            
            document.addEventListener('mousemove', (e) => {
                if (!isDragging) return;
                element.style.left = (origX + e.clientX - startX) + 'px';
                element.style.top = (origY + e.clientY - startY) + 'px';
            });
            
            document.addEventListener('mouseup', () => {
                isDragging = false;
            });
        }
        
        const heartColors = ['#e8a0a8', '#a8c8d8', '#c8d8a8', '#d8c8a8', '#c8a8d8', '#d8a8c8', '#a8d8c8', '#d8d8a8'];
        
        function getRandomHeartColor() {
            return heartColors[Math.floor(Math.random() * heartColors.length)];
        }
        
        function showHeartPopup() {
            const count = Math.floor(Math.random() * 6) + 1;
            for (let i = 0; i < count; i++) {
                setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.className = 'heart-popup';
                    heart.textContent = '♥';
                    heart.style.left = `${Math.random() * (window.innerWidth - 50)}px`;
                    heart.style.top = `${Math.random() * (window.innerHeight - 150)}px`;
                    heart.style.color = getRandomHeartColor();
                    heart.style.textShadow = `0 0 10px ${heart.style.color}`;
                    document.body.appendChild(heart);
                    setTimeout(() => heart.remove(), 2000);
                }, i * 80);
            }
        }
        
        function sendMessage() {
            const text = chatInput.value.trim();
            if (!text) return;
            
            const userMessage = document.createElement('div');
            userMessage.className = 'message sent';
            userMessage.textContent = text;
            chatMessages.appendChild(userMessage);
            
            chatInput.value = '';
            chatMessages.scrollTop = chatMessages.scrollHeight;
            
            const isSpecialMessage = text.includes('孙恺悦');
            const lovePatterns = ['i love you', '我爱你', 'love you', '爱你', 'i love u', 'love u', '我喜欢你', '喜欢', 'iloveyou', 'loveyou'];
            const isLoveMessage = lovePatterns.some(pattern => text.toLowerCase().includes(pattern.toLowerCase()));
            
            const camusQuotes = [
                '在隆冬，我终于知道，我身上有一个不可战胜的夏天。',
                '不要走在我后面，因为我可能不会引路；不要走在我前面，因为我可能不会跟随；请走在我的身边，做我的朋友。',
                '爱是没有界限的，如果我能拥抱一切，那拥抱得笨拙又有什么关系。',
                '在光亮中，世界始终是我们最初和最后的爱。',
                '当对幸福的憧憬过于急切，那痛苦就在人的心灵深处升起。',
                '我无法对你说出我对你的爱，因为爱是无法言说的。',
                '在这个世界上，只有爱才是唯一的真实。',
                '我想给你打电话，告诉你天气晴朗，告诉你我爱你，就像人们爱希望和爱确定一样。',
                '我讨厌距离,阴影·痛苦、下雨。\n我想要明亮的日子,\n和你一起,靠着大海和沙滩\n我想要奇幻的天空,我想要的国度,\n但是要和你在一起,和你在一起。',
                '荒谬当道，爱拯救之。',
                '我想要在你身上留下我的痕迹，就像树在石头上留下年轮。',
                '爱不需要理解，因为爱本身就是一种理解。'
            ];
            
            setTimeout(() => {
                const reply = document.createElement('div');
                reply.className = 'message received';
                const heartCount = Math.floor(Math.random() * 6) + 1;
                const hearts = [];
                for (let i = 0; i < heartCount; i++) {
                    const color = getRandomHeartColor();
                    hearts.push(`<span style="color: ${color}; text-shadow: 0 0 8px ${color};">♥</span>`);
                }
                reply.innerHTML = hearts.join(' ');
                chatMessages.appendChild(reply);
                chatMessages.scrollTop = chatMessages.scrollHeight;
                
                showHeartPopup();
                createStickyNote(text);
                
                if (isLoveMessage) {
                    setTimeout(() => {
                        const foreverReply = document.createElement('div');
                        foreverReply.className = 'message received';
                        foreverReply.innerHTML = '<span style="color: #d4a8b0; text-shadow: 0 0 8px #d4a8b0;">forever ♥</span>';
                        chatMessages.appendChild(foreverReply);
                        chatMessages.scrollTop = chatMessages.scrollHeight;
                        
                        setTimeout(() => {
                            const quoteReply = document.createElement('div');
                            quoteReply.className = 'message received';
                            const randomQuote = camusQuotes[Math.floor(Math.random() * camusQuotes.length)];
                            quoteReply.innerHTML = `<span style="color: #b8c8d0; font-style: italic;">"${randomQuote}"</span>`;
                            chatMessages.appendChild(quoteReply);
                            chatMessages.scrollTop = chatMessages.scrollHeight;
                        }, 800);
                    }, 600);
                }
                
                if (isSpecialMessage) {
                    setTimeout(() => {
                        const loveReply = document.createElement('div');
                        loveReply.className = 'message received';
                        loveReply.innerHTML = '<span style="color: #d4a8b0; text-shadow: 0 0 8px #d4a8b0;">i love you ♥</span>';
                        chatMessages.appendChild(loveReply);
                        chatMessages.scrollTop = chatMessages.scrollHeight;
                        
                        showLoveHeartsEffect();
                    }, 800);
                }
            }, 500);
        }
        
        function showLoveHeartsEffect() {
            let overlay = document.getElementById('loveHeartsOverlay');
            if (!overlay) {
                overlay = document.createElement('div');
                overlay.className = 'love-hearts-overlay';
                overlay.id = 'loveHeartsOverlay';
                document.body.appendChild(overlay);
            }
            
            const lowSaturationColors = [
                '#d4a8b0',
                '#a8c8d8',
                '#c8d8a8',
                '#d8c8a8',
                '#c8a8d8',
                '#b8c8d0',
                '#d0c8b8',
                '#c0d0c8'
            ];
            
            const heartCount = 30;
            
            for (let i = 0; i < heartCount; i++) {
                setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.className = 'love-heart';
                    
                    const sizeClass = Math.random();
                    if (sizeClass < 0.3) {
                        heart.classList.add('small');
                    } else if (sizeClass > 0.8) {
                        heart.classList.add('large');
                    }
                    
                    const color = lowSaturationColors[Math.floor(Math.random() * lowSaturationColors.length)];
                    heart.style.color = color;
                    heart.style.textShadow = `0 0 10px ${color}`;
                    heart.style.left = Math.random() * 100 + '%';
                    heart.style.animationDelay = Math.random() * 0.5 + 's';
                    heart.textContent = '♥';
                    
                    overlay.appendChild(heart);
                    
                    setTimeout(() => {
                        if (heart.parentNode) {
                            heart.remove();
                        }
                    }, 5500);
                }, i * 100);
            }
        }
        
        sendBtn.addEventListener('click', sendMessage);
        
        chatInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') sendMessage();
        });
        
        keyboard.addEventListener('click', (e) => {
            const key = e.target.closest('.osk-key');
            if (!key) return;
            
            const keyValue = key.dataset.key;
            
            if (audioContext.state === 'suspended') audioContext.resume();
            playMechanicalKeySound();
            
            key.classList.add('pressed');
            setTimeout(() => key.classList.remove('pressed'), 80);
            
            if (keyValue === 'Backspace') {
                chatInput.value = chatInput.value.slice(0, -1);
            } else if (keyValue === 'Enter') {
                sendMessage();
            } else if (keyValue.length === 1) {
                chatInput.value += keyValue.toLowerCase();
            }
            
            chatInput.focus();
            setActiveWindow('chatWindow');
        });
        
        document.addEventListener('keydown', (e) => {
            const keyElement = keyboard.querySelector(`[data-key="${e.key}"]`) || 
                              keyboard.querySelector(`[data-key="${e.key.toLowerCase()}"]`);
            
            if (keyElement) {
                if (audioContext.state === 'suspended') audioContext.resume();
                playMechanicalKeySound();
                keyElement.classList.add('pressed');
            }
        });
        
        document.addEventListener('keyup', (e) => {
            const keyElement = keyboard.querySelector(`[data-key="${e.key}"]`) || 
                              keyboard.querySelector(`[data-key="${e.key.toLowerCase()}"]`);
            if (keyElement) keyElement.classList.remove('pressed');
        });
        
        document.querySelectorAll('.win-window').forEach(win => {
            win.addEventListener('mousedown', () => setActiveWindow(win.id));
        });

        document.addEventListener('click', () => {
            if (audioContext.state === 'suspended') audioContext.resume();
        }, { once: true });

        initWindows();
        initMusicPlayer();
        initAlienCat();
        updateTaskbarTime();
        setInterval(updateTaskbarTime, 1000);

        let mineBoard = [];
        let mineRows = 9;
        let mineCols = 9;
        let mineTotal = 10;
        let mineFlags = 0;
        let mineRevealed = 0;
        let mineGameOver = false;
        let mineTimerInterval = null;
        let mineSeconds = 0;

        function initMinesweeper() {
            mineBoard = [];
            mineFlags = 0;
            mineRevealed = 0;
            mineGameOver = false;
            mineSeconds = 0;
            
            if (mineTimerInterval) {
                clearInterval(mineTimerInterval);
                mineTimerInterval = null;
            }
            
            document.getElementById('mineTimer').textContent = '000';
            document.getElementById('mineCount').textContent = String(mineTotal).padStart(3, '0');
            document.getElementById('mineFace').textContent = '😊';
            
            const board = document.getElementById('mineBoard');
            board.style.gridTemplateColumns = `repeat(${mineCols}, 20px)`;
            board.innerHTML = '';
            
            for (let r = 0; r < mineRows; r++) {
                mineBoard[r] = [];
                for (let c = 0; c < mineCols; c++) {
                    mineBoard[r][c] = { mine: false, revealed: false, flagged: false, count: 0 };
                    
                    const cell = document.createElement('div');
                    cell.className = 'mine-cell';
                    cell.dataset.row = r;
                    cell.dataset.col = c;
                    cell.onclick = () => revealCell(r, c);
                    cell.oncontextmenu = (e) => { e.preventDefault(); toggleFlag(r, c); };
                    board.appendChild(cell);
                }
            }
            
            let placed = 0;
            while (placed < mineTotal) {
                const r = Math.floor(Math.random() * mineRows);
                const c = Math.floor(Math.random() * mineCols);
                if (!mineBoard[r][c].mine) {
                    mineBoard[r][c].mine = true;
                    placed++;
                }
            }
            
            for (let r = 0; r < mineRows; r++) {
                for (let c = 0; c < mineCols; c++) {
                    if (!mineBoard[r][c].mine) {
                        let count = 0;
                        for (let dr = -1; dr <= 1; dr++) {
                            for (let dc = -1; dc <= 1; dc++) {
                                const nr = r + dr, nc = c + dc;
                                if (nr >= 0 && nr < mineRows && nc >= 0 && nc < mineCols && mineBoard[nr][nc].mine) {
                                    count++;
                                }
                            }
                        }
                        mineBoard[r][c].count = count;
                    }
                }
            }
        }

        function getCell(r, c) {
            return document.querySelector(`.mine-cell[data-row="${r}"][data-col="${c}"]`);
        }

        function revealCell(r, c) {
            if (mineGameOver || mineBoard[r][c].revealed || mineBoard[r][c].flagged) return;
            
            if (!mineTimerInterval) {
                mineTimerInterval = setInterval(() => {
                    mineSeconds++;
                    document.getElementById('mineTimer').textContent = String(Math.min(mineSeconds, 999)).padStart(3, '0');
                }, 1000);
            }
            
            const cell = getCell(r, c);
            mineBoard[r][c].revealed = true;
            mineRevealed++;
            cell.classList.add('revealed');
            
            if (mineBoard[r][c].mine) {
                cell.classList.add('mine');
                gameOver(false);
                return;
            }
            
            if (mineBoard[r][c].count > 0) {
                cell.textContent = mineBoard[r][c].count;
                cell.classList.add(`num-${mineBoard[r][c].count}`);
            } else {
                for (let dr = -1; dr <= 1; dr++) {
                    for (let dc = -1; dc <= 1; dc++) {
                        const nr = r + dr, nc = c + dc;
                        if (nr >= 0 && nr < mineRows && nc >= 0 && nc < mineCols) {
                            revealCell(nr, nc);
                        }
                    }
                }
            }
            
            if (mineRevealed === mineRows * mineCols - mineTotal) {
                gameOver(true);
            }
        }

        function toggleFlag(r, c) {
            if (mineGameOver || mineBoard[r][c].revealed) return;
            
            const cell = getCell(r, c);
            mineBoard[r][c].flagged = !mineBoard[r][c].flagged;
            cell.classList.toggle('flagged');
            
            mineFlags += mineBoard[r][c].flagged ? 1 : -1;
            document.getElementById('mineCount').textContent = String(mineTotal - mineFlags).padStart(3, '0');
        }

        function gameOver(won) {
            mineGameOver = true;
            if (mineTimerInterval) {
                clearInterval(mineTimerInterval);
                mineTimerInterval = null;
            }
            
            document.getElementById('mineFace').textContent = won ? '😎' : '😵';
            
            if (!won) {
                for (let r = 0; r < mineRows; r++) {
                    for (let c = 0; c < mineCols; c++) {
                        if (mineBoard[r][c].mine) {
                            const cell = getCell(r, c);
                            cell.classList.add('revealed', 'mine');
                        }
                    }
                }
            }
        }

        function initAlienCat() {
            const cat = document.getElementById('alienCat');
            const speech = document.getElementById('catSpeech');
            let clickTimeout = null;
            let lastClickTime = 0;

            const catPhrases = [
                '喵~', '喵喵!', '*眨眼*', '你好呀~', 
                '想摸摸我吗?', '外星猫报到!', '咕噜咕噜~',
                '我在看着你哦', '带我回家吧~', '喵呜~'
            ];

            const catMoods = [
                '开心~', '困了...', '想吃小鱼干', '想玩耍!',
                '有点无聊...', '心情很好!', '想被摸摸头'
            ];

            function showSpeech(text, duration = 2000) {
                speech.textContent = text;
                speech.classList.add('show');
                setTimeout(() => {
                    speech.classList.remove('show');
                }, duration);
            }

            function createStar() {
                const star = document.createElement('div');
                star.className = 'cat-star';
                star.textContent = '✨';
                star.style.left = Math.random() * 60 + 10 + 'px';
                star.style.top = Math.random() * 30 + 'px';
                star.style.animationDelay = Math.random() * 0.5 + 's';
                cat.appendChild(star);
                setTimeout(() => star.remove(), 2000);
            }

            cat.addEventListener('click', (e) => {
                const now = Date.now();
                
                if (now - lastClickTime < 300) {
                    clearTimeout(clickTimeout);
                    cat.classList.add('double-clicked');
                    showSpeech(catMoods[Math.floor(Math.random() * catMoods.length)]);
                    for (let i = 0; i < 3; i++) {
                        setTimeout(createStar, i * 200);
                    }
                    setTimeout(() => cat.classList.remove('double-clicked'), 500);
                    lastClickTime = 0;
                    return;
                }
                
                lastClickTime = now;
                
                clickTimeout = setTimeout(() => {
                    cat.classList.add('clicked');
                    showSpeech(catPhrases[Math.floor(Math.random() * catPhrases.length)]);
                    createStar();
                    setTimeout(() => cat.classList.remove('clicked'), 500);
                }, 300);
            });

            cat.addEventListener('contextmenu', (e) => {
                e.preventDefault();
                cat.classList.add('right-clicked');
                showSpeech('转圈圈~!', 1500);
                for (let i = 0; i < 5; i++) {
                    setTimeout(createStar, i * 100);
                }
                setTimeout(() => cat.classList.remove('right-clicked'), 600);
            });

            setInterval(() => {
                if (Math.random() > 0.7) {
                    const randomPhrase = catPhrases[Math.floor(Math.random() * catPhrases.length)];
                    showSpeech(randomPhrase, 1500);
                }
            }, 15000);

            cat.addEventListener('mouseenter', () => {
                if (Math.random() > 0.5) {
                    showSpeech('来玩吧~', 1000);
                }
            });
        }
    </script>
</body>
</html>
