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
            --mint-green: #b8d4c8;
            --tiffany-blue: #a8c8d0;
            --aquamarine: #b0d8d0;
            --win-bg: #d8d0d8;
            --win-light: #f0e8f0;
            --win-dark: #a098a0;
            --win-darker: #686068;
            --win-title: #604080;
            --win-title-inactive: #a098a0;
            --win-border-outset: var(--win-light) var(--win-dark) var(--win-dark) var(--win-light);
            --win-border-inset: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark);
            --heart-pink: #d8b0c0;
            --emotion-deep: #684080;
            --emotion-bright: #e8c890;
            --dream-pink: #e8c8d8;
            --dream-lavender: #d0b8e0;
            --dream-blue: #b8d0e8;
            --dream-peach: #f0d0c0;
        }

        .boot-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
            z-index: 99999;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-family: 'VT323', monospace;
        }

        .boot-screen.hidden {
            display: none;
        }

        .boot-bios {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #000;
            color: #c0c0c0;
            padding: 20px;
            font-size: 14px;
            line-height: 1.6;
            white-space: pre-wrap;
            display: none;
        }

        .boot-bios.active {
            display: block;
        }

        .boot-logo {
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            width: 100%;
            height: 100%;
            background: linear-gradient(180deg, #e8d8e8 0%, #d0c0d8 50%, #c8b8d0 100%);
        }

        .boot-logo.active {
            display: flex;
        }

        .boot-windows-logo {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 40px;
        }

        .boot-flag {
            display: grid;
            grid-template-columns: repeat(2, 50px);
            grid-template-rows: repeat(2, 50px);
            gap: 4px;
            margin-bottom: 20px;
        }

        .boot-flag-piece {
            width: 50px;
            height: 50px;
        }

        .boot-flag-piece:nth-child(1) {
            background: linear-gradient(135deg, #d8b8c8 0%, #c0a0b0 100%);
        }
        .boot-flag-piece:nth-child(2) {
            background: linear-gradient(135deg, #b8c8d0 0%, #a0b0b8 100%);
        }
        .boot-flag-piece:nth-child(3) {
            background: linear-gradient(135deg, #c0b8d8 0%, #a8a0c0 100%);
        }
        .boot-flag-piece:nth-child(4) {
            background: linear-gradient(135deg, #d8c8b0 0%, #c0b098 100%);
        }

        .boot-title {
            font-size: 48px;
            color: #604080;
            text-shadow: 1px 1px 2px rgba(255, 255, 255, 0.5);
            letter-spacing: 4px;
        }

        .boot-subtitle {
            font-size: 18px;
            color: #806090;
            margin-top: 10px;
            letter-spacing: 2px;
        }

        .boot-progress-container {
            width: 300px;
            margin-top: 30px;
        }

        .boot-progress-bar {
            width: 100%;
            height: 20px;
            background: rgba(200, 180, 200, 0.5);
            border: 2px solid;
            border-color: var(--win-border-outset);
            border-radius: 2px;
            overflow: hidden;
        }

        .boot-progress-fill {
            width: 0%;
            height: 100%;
            background: linear-gradient(90deg, #a090b8, #c0b0d0);
            transition: width 0.3s ease;
        }

        .boot-status {
            text-align: center;
            color: #706080;
            font-size: 14px;
            margin-top: 15px;
            min-height: 20px;
        }

        .boot-dots {
            display: inline-block;
            width: 30px;
            text-align: left;
        }

        .boot-welcome {
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            width: 100%;
            height: 100%;
            background: linear-gradient(180deg, #e8d8e8 0%, #d0c0d8 50%, #c8b8d0 100%);
        }

        .boot-welcome.active {
            display: flex;
        }

        .boot-welcome-text {
            font-size: 24px;
            color: #604080;
            text-shadow: 1px 1px 2px rgba(255, 255, 255, 0.5);
            letter-spacing: 2px;
        }

        .boot-click-hint {
            position: absolute;
            bottom: 50px;
            color: #806090;
            font-size: 14px;
            animation: hintBlink 1.5s ease-in-out infinite;
        }

        @keyframes hintBlink {
            0%, 100% { opacity: 0.6; }
            50% { opacity: 1; }
        }

        @keyframes paperSlideIn {
            0% {
                transform: translate(-50%, -200%);
                opacity: 0;
            }
            100% {
                transform: translate(-50%, -50%);
                opacity: 1;
            }
        }

        @keyframes fadeIn {
            0% { opacity: 0; transform: scale(0.95); }
            100% { opacity: 1; transform: scale(1); }
        }

        @keyframes cardFlip {
            0% { transform: rotateY(0deg); }
            50% { transform: rotateY(90deg); }
            100% { transform: rotateY(0deg); }
        }

        .magic-card {
            width: 80px;
            height: 120px;
            border-radius: 8px;
            cursor: pointer;
            perspective: 1000px;
            transition: transform 0.3s ease;
        }
        .magic-card:hover {
            transform: translateY(-5px);
        }
        .card-back, .card-front {
            width: 100%;
            height: 100%;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 30px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.2);
        }
        .card-back {
            background: linear-gradient(135deg, #6840a0 0%, #9060c0 50%, #6840a0 100%);
            border: 2px solid #a080d0;
        }
        .card-front {
            background: linear-gradient(180deg, #f8f0ff 0%, #e8e0f8 100%);
            border: 2px solid #c0b0d8;
            flex-direction: column;
            font-size: 24px;
        }
        .card-front .card-name {
            font-size: 10px;
            margin-top: 5px;
            color: #504060;
            text-align: center;
        }
        .card-front.reversed {
            transform: rotate(180deg);
        }
        .card-front.reversed .card-name {
            transform: rotate(180deg);
        }

        body {
            min-height: 100vh;
            background: linear-gradient(180deg, 
                #e8d8e8 0%, 
                #f0e0f0 15%,
                #e8e0f0 30%,
                #f0e8f0 50%,
                #e0e8f0 70%,
                #d8e0e8 85%,
                #e0d8e8 100%
            );
            font-family: 'VT323', 'MS Sans Serif', Tahoma, sans-serif;
            overflow: hidden;
            position: relative;
            image-rendering: pixelated;
            image-rendering: -moz-crisp-edges;
            image-rendering: crisp-edges;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                radial-gradient(ellipse at 30% 20%, rgba(232, 200, 216, 0.4) 0%, transparent 50%),
                radial-gradient(ellipse at 70% 30%, rgba(208, 184, 224, 0.3) 0%, transparent 40%),
                radial-gradient(ellipse at 50% 80%, rgba(184, 208, 232, 0.3) 0%, transparent 40%);
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
            background: rgba(255, 255, 255, 0.75);
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
            width: 250px;
            height: 70px;
            top: 8%;
            left: -250px;
            animation-duration: 60s;
            filter: blur(2px);
            opacity: 0.85;
        }
        .cloud-1::before { width: 120px; height: 60px; top: -25px; left: 40px; }
        .cloud-1::after { width: 100px; height: 50px; top: -20px; left: 120px; }

        .cloud-2 {
            width: 180px;
            height: 50px;
            top: 18%;
            left: -180px;
            animation-duration: 80s;
            animation-delay: -15s;
            filter: blur(3px);
            opacity: 0.75;
        }
        .cloud-2::before { width: 80px; height: 40px; top: -18px; left: 25px; }
        .cloud-2::after { width: 70px; height: 35px; top: -12px; left: 85px; }

        .cloud-3 {
            width: 220px;
            height: 60px;
            top: 5%;
            left: -220px;
            animation-duration: 70s;
            animation-delay: -30s;
            filter: blur(2px);
            opacity: 0.7;
        }
        .cloud-3::before { width: 100px; height: 50px; top: -20px; left: 30px; }
        .cloud-3::after { width: 85px; height: 42px; top: -15px; left: 110px; }

        .cloud-4 {
            width: 150px;
            height: 40px;
            top: 25%;
            left: -150px;
            animation-duration: 55s;
            animation-delay: -45s;
            filter: blur(3px);
            opacity: 0.65;
        }
        .cloud-4::before { width: 60px; height: 30px; top: -12px; left: 20px; }
        .cloud-4::after { width: 55px; height: 28px; top: -10px; left: 70px; }

        .cloud-5 {
            width: 300px;
            height: 80px;
            top: 12%;
            left: -300px;
            animation-duration: 90s;
            animation-delay: -10s;
            filter: blur(2px);
            opacity: 0.8;
        }
        .cloud-5::before { width: 140px; height: 70px; top: -30px; left: 50px; }
        .cloud-5::after { width: 120px; height: 55px; top: -22px; left: 150px; }

        .cloud-6 {
            width: 130px;
            height: 35px;
            top: 30%;
            left: -130px;
            animation-duration: 50s;
            animation-delay: -25s;
            filter: blur(4px);
            opacity: 0.6;
        }
        .cloud-6::before { width: 55px; height: 28px; top: -10px; left: 18px; }
        .cloud-6::after { width: 50px; height: 25px; top: -8px; left: 60px; }

        .cloud-7 {
            width: 200px;
            height: 55px;
            top: 3%;
            left: -200px;
            animation-duration: 75s;
            animation-delay: -55s;
            filter: blur(3px);
            opacity: 0.55;
        }
        .cloud-7::before { width: 90px; height: 45px; top: -18px; left: 28px; }
        .cloud-7::after { width: 80px; height: 38px; top: -14px; left: 100px; }

        .cloud-8 {
            width: 170px;
            height: 45px;
            top: 22%;
            left: -170px;
            animation-duration: 65s;
            animation-delay: -35s;
            filter: blur(3px);
            opacity: 0.7;
        }
        .cloud-8::before { width: 75px; height: 38px; top: -15px; left: 22px; }
        .cloud-8::after { width: 65px; height: 32px; top: -11px; left: 82px; }

        @keyframes cloudFloat {
            0% { 
                transform: translateX(0) translateY(0); 
            }
            25% { 
                transform: translateX(calc(25vw + 100px)) translateY(-10px); 
            }
            50% { 
                transform: translateX(calc(50vw + 200px)) translateY(0); 
            }
            75% { 
                transform: translateX(calc(75vw + 300px)) translateY(-8px); 
            }
            100% { 
                transform: translateX(calc(100vw + 400px)) translateY(0); 
            }
        }

        .scanlines {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: repeating-linear-gradient(0deg, rgba(100, 80, 100, 0.02) 0px, rgba(100, 80, 100, 0.02) 1px, transparent 1px, transparent 2px);
            pointer-events: none;
            z-index: 9999;
        }

        .pixel-effect {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 9998;
            background: 
                repeating-linear-gradient(90deg, transparent 0px, transparent 1px, rgba(100, 80, 100, 0.01) 1px, rgba(100, 80, 100, 0.01) 2px),
                repeating-linear-gradient(0deg, transparent 0px, transparent 1px, rgba(100, 80, 100, 0.01) 1px, rgba(100, 80, 100, 0.01) 2px);
        }

        .desktop-icons {
            position: fixed;
            left: 15px;
            top: 15px;
            display: grid;
            grid-template-columns: repeat(2, 75px);
            gap: 8px 12px;
            z-index: 10;
        }

        .desktop-icon {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 75px;
            padding: 5px;
            cursor: pointer;
            border: 1px solid transparent;
            border-radius: 4px;
            transition: all 0.15s ease;
        }

        .desktop-icon:hover {
            background: rgba(200, 160, 200, 0.35);
            border: 1px solid rgba(200, 160, 200, 0.5);
            transform: translateY(-2px);
        }

        .desktop-icon.selected {
            background: rgba(200, 160, 200, 0.45);
            border: 1px solid rgba(200, 160, 200, 0.7);
        }

        .icon-image {
            width: 36px;
            height: 36px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 3px;
            image-rendering: pixelated;
        }

        .icon-label {
            font-size: 11px;
            color: #504060;
            text-align: center;
            text-shadow: 1px 1px 0 rgba(255, 255, 255, 0.8), -1px -1px 0 rgba(255, 255, 255, 0.8);
            word-wrap: break-word;
            max-width: 70px;
            line-height: 1.2;
        }

        .win-icon {
            width: 36px;
            height: 36px;
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

        .win-icon.network {
            background: linear-gradient(180deg, #d8e8f8 0%, #b8c8d8 100%);
            border: 2px solid #6080a0;
            border-radius: 4px;
        }
        .win-icon.network::before {
            content: '🖥️';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 20px;
        }

        .win-icon.fish {
            background: linear-gradient(180deg, #b8e8f0 0%, #90d0e0 100%);
            border: 2px solid #60a0b0;
            border-radius: 50%;
        }
        .win-icon.fish::before {
            content: '🐟';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 18px;
        }

        .win-icon.magic {
            background: linear-gradient(180deg, #d8b8e8 0%, #b890d0 100%);
            border: 2px solid #8060a0;
            border-radius: 8px;
        }
        .win-icon.magic::before {
            content: '🔮';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 18px;
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
            background: linear-gradient(90deg, #9070a8, #a890b8);
            padding: 2px 3px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            cursor: move;
            user-select: none;
        }

        .win-window.inactive .win-titlebar {
            background: linear-gradient(90deg, #c0b0c0, #d0c0d0);
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
            border-color: var(--win-border-outset);
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
            border-color: var(--win-border-inset);
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
            border-color: var(--win-border-inset);
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
            border-color: var(--win-border-inset);
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
            border-color: var(--win-border-outset);
            font-size: 12px;
            cursor: pointer;
            font-family: 'VT323', monospace;
        }

        .win-btn-send:active {
            border-color: var(--win-border-inset);
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
            border-color: var(--win-border-outset);
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
            border-color: var(--win-border-inset);
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
            background: linear-gradient(145deg, #d8e8d8 0%, #c8d8c8 40%, #a8c8b8 100%);
            border-color: rgba(168, 213, 168, 0.5);
            color: #3a4a3a;
        }

        .sticky-note.vaporwave {
            background: linear-gradient(145deg, #e8d0d8 0%, #d8c0c8 40%, #c0b0c0 100%);
            border-color: rgba(200, 160, 176, 0.5);
            color: #4a3a4a;
        }

        .sticky-note.cyberpunk {
            background: linear-gradient(145deg, #3a3a3a 0%, #2a2a2a 50%, #1a1a1a 100%);
            border-color: #88c8a8;
            color: #88c8a8;
        }

        .sticky-note.nostalgic {
            background: linear-gradient(145deg, #f0e8d8 0%, #e8d8c8 40%, #d8c8b0 100%);
            border-color: rgba(200, 180, 160, 0.5);
            color: #5a4a3a;
        }

        .sticky-note.ethereal {
            background: linear-gradient(145deg, #e8f0f8 0%, #d8e0e8 40%, #c8d0e0 100%);
            border-color: rgba(180, 200, 220, 0.5);
            color: #4a5a6a;
        }

        .sticky-note.morandi-pink {
            background: linear-gradient(145deg, #f0d8e0 0%, #e8c8d0 40%, #d8b8c0 100%);
            border-color: rgba(220, 180, 190, 0.5);
            color: #5a4a50;
        }

        .sticky-note.morandi-yellow {
            background: linear-gradient(145deg, #f0e8d0 0%, #e8e0c0 40%, #d8d0a8 100%);
            border-color: rgba(220, 210, 180, 0.5);
            color: #5a5240;
        }

        .sticky-note.morandi-blue {
            background: linear-gradient(145deg, #d8e0e8 0%, #c8d0d8 40%, #b8c0d0 100%);
            border-color: rgba(180, 190, 200, 0.5);
            color: #4a5a6a;
        }

        .sticky-note.morandi-green {
            background: linear-gradient(145deg, #d8e8d8 0%, #c8d0c8 40%, #b8c0b8 100%);
            border-color: rgba(180, 200, 180, 0.5);
            color: #4a5a4a;
        }

        .sticky-note.morandi-lavender {
            background: linear-gradient(145deg, #e0d0e8 0%, #d0c8d8 40%, #c0b8d0 100%);
            border-color: rgba(190, 180, 200, 0.5);
            color: #5a4a5a;
        }

        .sticky-note.morandi-beige {
            background: linear-gradient(145deg, #e8e0d0 0%, #d8d0c8 40%, #c8c0b8 100%);
            border-color: rgba(200, 190, 180, 0.5);
            color: #5a524a;
        }

        .sticky-note.morandi-sage {
            background: linear-gradient(145deg, #d8d8d0 0%, #c8c8c0 40%, #b8b8b0 100%);
            border-color: rgba(180, 180, 170, 0.5);
            color: #4a4a42;
        }

        .sticky-note.morandi-mist {
            background: linear-gradient(145deg, #e0e0e0 0%, #d0d0d0 40%, #c0c0c0 100%);
            border-color: rgba(180, 180, 180, 0.5);
            color: #4a4a4a;
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
            border-color: var(--win-border-outset);
            display: flex;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            font-size: 11px;
            font-weight: bold;
            font-family: 'VT323', monospace;
        }

        .start-btn:active {
            border-color: var(--win-border-inset);
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
            border-color: var(--win-border-inset);
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
            border-color: var(--win-border-inset);
            background: #a0a0a0;
        }

        .taskbar-tray {
            display: flex;
            align-items: center;
            gap: 4px;
            padding: 0 8px;
            border: 1px solid;
            border-color: var(--win-border-inset);
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
            border-color: var(--win-border-outset);
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
            border-color: var(--win-border-outset);
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
        }

        .music-btn:active {
            border-color: var(--win-border-inset);
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
            border-color: var(--win-border-outset);
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
            border-color: var(--win-border-outset);
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
        }

        .paint-tool:active, .paint-tool.active {
            border-color: var(--win-border-inset);
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
            border-color: var(--win-border-inset);
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
            border-color: var(--win-border-outset);
            cursor: pointer;
            font-size: 14px;
            font-family: 'VT323', monospace;
        }

        .calc-btn:active {
            border-color: var(--win-border-inset);
        }

        .calc-btn.operator {
            background: #d8d0c8;
        }

        @media (max-width: 480px) {
            .desktop-icons { 
                left: 5px; 
                top: 5px; 
                gap: 5px;
                grid-template-columns: repeat(2, 60px);
            }
            .desktop-icon { width: 60px; padding: 3px; }
            .icon-image { width: 28px; height: 28px; }
            .icon-label { font-size: 9px; max-width: 55px; }
            .win-icon { width: 28px; height: 28px; }
            .chat-window { top: 10px; left: 10px; width: calc(100% - 20px); height: 280px; }
            .paint-window, .notepad-window, .word-window, .calc-window {
                width: calc(100% - 20px);
                left: 10px !important;
            }
        }
    </style>
</head>
<body>
    <div class="boot-screen" id="bootScreen">
        <div class="boot-bios" id="bootBios"></div>
        <div class="boot-logo" id="bootLogo">
            <div class="boot-windows-logo">
                <div class="boot-flag">
                    <div class="boot-flag-piece"></div>
                    <div class="boot-flag-piece"></div>
                    <div class="boot-flag-piece"></div>
                    <div class="boot-flag-piece"></div>
                </div>
                <div class="boot-title">Microsoft Windows 98</div>
                <div class="boot-subtitle">Dreamcore Edition</div>
            </div>
            <div class="boot-progress-container">
                <div class="boot-progress-bar">
                    <div class="boot-progress-fill" id="bootProgressFill"></div>
                </div>
                <div class="boot-status" id="bootStatus">正在启动 Windows<span class="boot-dots"></span></div>
            </div>
        </div>
        <div class="boot-welcome" id="bootWelcome">
            <div class="boot-welcome-text">Welcome to Dreamcore</div>
            <div class="boot-click-hint">点击任意位置进入桌面</div>
        </div>
    </div>

    <div class="sky-bg">
        <div class="cloud cloud-1"></div>
        <div class="cloud cloud-2"></div>
        <div class="cloud cloud-3"></div>
        <div class="cloud cloud-4"></div>
        <div class="cloud cloud-5"></div>
        <div class="cloud cloud-6"></div>
        <div class="cloud cloud-7"></div>
        <div class="cloud cloud-8"></div>
    </div>

    <div class="scanlines"></div>
    <div class="pixel-effect"></div>

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
        <div class="desktop-icon" ondblclick="openWindow('myComputerWindow')" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon my-computer"></div></div>
            <span class="icon-label">我的电脑</span>
        </div>
        <div class="desktop-icon" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon folder"></div></div>
            <span class="icon-label">我的文档</span>
        </div>
        <div class="desktop-icon" ondblclick="openWindow('networkWindow')" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon network"></div></div>
            <span class="icon-label">网上邻居</span>
        </div>
        <div class="desktop-icon" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon recycle-bin"></div></div>
            <span class="icon-label">回收站</span>
        </div>
        <div class="desktop-icon" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon internet"></div></div>
            <span class="icon-label">Internet</span>
        </div>
        <div class="desktop-icon" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon settings"></div></div>
            <span class="icon-label">设置</span>
        </div>
        <div class="desktop-icon" ondblclick="openWindow('chatWindow')" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon chat"></div></div>
            <span class="icon-label">Dream Entity</span>
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
        <div class="desktop-icon" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon games"></div></div>
            <span class="icon-label">游戏</span>
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
        <div class="desktop-icon" ondblclick="openFishWindow()" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon fish"></div></div>
            <span class="icon-label">Fish</span>
        </div>
        <div class="desktop-icon" ondblclick="openMagicWindow()" onclick="selectIcon(this)">
            <div class="icon-image"><div class="win-icon magic"></div></div>
            <span class="icon-label">Magic</span>
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
            <div class="chat-input-area" onclick="openWindow('keyboardWindow')">
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
            <div style="text-align: center; cursor: pointer;" ondblclick="openDVDPlayer()">
                <div style="font-size: 32px;">💿</div>
                <div style="font-size: 11px;">DVD驱动器 (D:)</div>
            </div>
            <div style="text-align: center; cursor: pointer;">
                <div style="font-size: 32px;">📁</div>
                <div style="font-size: 11px;">共享文件夹</div>
            </div>
            <div style="text-align: center; cursor: pointer;" ondblclick="openPrinterWindow()">
                <div style="font-size: 32px;">🖨️</div>
                <div style="font-size: 11px;">打印机</div>
            </div>
        </div>
        <div class="win-statusbar">
            <div class="win-statusbar-section">4 个对象</div>
        </div>
    </div>

    <div class="win-window" id="networkWindow" style="top: 80px; left: 200px; width: 450px; height: 320px; display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'networkWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">🌐</div>
                <span class="win-titlebar-text">网上邻居</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('networkWindow')"></button>
                <button class="win-btn win-btn-maximize"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('networkWindow')"></button>
            </div>
        </div>
        <div class="win-menubar">
            <span class="win-menu-item">文件(F)</span>
            <span class="win-menu-item">编辑(E)</span>
            <span class="win-menu-item">查看(V)</span>
            <span class="win-menu-item">帮助(H)</span>
        </div>
        <div class="win-content" style="background: white; padding: 15px; display: flex; flex-wrap: wrap; gap: 20px; align-content: flex-start;">
            <div style="text-align: center; cursor: pointer; padding: 10px;" ondblclick="openNetworkComputer()">
                <div style="font-size: 40px;">🖥️</div>
                <div style="font-size: 12px; margin-top: 5px; color: #000080;">叽歪毛</div>
            </div>
        </div>
        <div class="win-statusbar">
            <div class="win-statusbar-section">1 个对象 | 局域网</div>
        </div>
    </div>

    <div class="win-window" id="fishWindow" style="top: 80px; left: 220px; width: 380px; height: auto; display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'fishWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">🐟</div>
                <span class="win-titlebar-text">Fish - 每日运势</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('fishWindow')"></button>
                <button class="win-btn win-btn-maximize"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('fishWindow')"></button>
            </div>
        </div>
        <div class="win-content" style="background: linear-gradient(180deg, #e8f4f8 0%, #d0e8f0 100%); padding: 20px; text-align: center;">
            <div id="fishContainer" style="background: white; border-radius: 8px; padding: 20px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);">
                <div id="fishEmoji" style="font-size: 50px; margin-bottom: 10px;">🐟</div>
                <div id="fishFortune" style="font-size: 24px; color: #6080a0; margin-bottom: 15px; font-weight: bold;">大吉</div>
                <div id="fishTime" style="font-size: 13px; color: #808080; margin-bottom: 10px;">宜：摸鱼</div>
                <div id="fishTip" style="font-size: 12px; color: #606060; padding: 10px; background: #f8f8f8; border-radius: 6px; margin-top: 10px; line-height: 1.6;">
                    今日宜多喝水，保持好心情~
                </div>
            </div>
            <button onclick="refreshFish()" style="margin-top: 15px; padding: 8px 25px; background: linear-gradient(180deg, #b8e8f0 0%, #90d0e0 100%); border: 2px solid #60a0b0; border-radius: 6px; font-family: inherit; font-size: 13px; cursor: pointer; color: #406070;">
                🔄 换一签
            </button>
        </div>
    </div>

    <div class="win-window" id="dvdPlayerWindow" style="top: 50px; left: 150px; width: 520px; height: auto; display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'dvdPlayerWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">💿</div>
                <span class="win-titlebar-text">DVD 播放器</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('dvdPlayerWindow')"></button>
                <button class="win-btn win-btn-maximize"></button>
                <button class="win-btn win-btn-close" onclick="closeDVDPlayer()"></button>
            </div>
        </div>
        <div class="win-content" style="background: #000; padding: 0;">
            <video id="dvdVideo" style="width: 100%; display: block;" controls>
                <source src="https://github.com/Redbeancc7/cc/releases/download/v2.0/6da177473e86206e7091c28471120401.mp4" type="video/mp4">
                您的浏览器不支持视频播放
            </video>
        </div>
        <div class="win-statusbar">
            <div class="win-statusbar-section">DVD 播放中...</div>
        </div>
    </div>

    <div class="win-window" id="magicWindow" style="top: 60px; left: 180px; width: 500px; height: auto; display: none;">
        <div class="win-titlebar" onmousedown="startDrag(event, 'magicWindow')">
            <div class="win-titlebar-left">
                <div class="win-titlebar-icon">🔮</div>
                <span class="win-titlebar-text">Magic - 塔罗牌占卜</span>
            </div>
            <div class="win-titlebar-controls">
                <button class="win-btn win-btn-minimize" onclick="minimizeWindow('magicWindow')"></button>
                <button class="win-btn win-btn-maximize"></button>
                <button class="win-btn win-btn-close" onclick="closeWindow('magicWindow')"></button>
            </div>
        </div>
        <div class="win-content" style="background: linear-gradient(180deg, #f0e8f8 0%, #e0d0f0 100%); padding: 20px;">
            <div style="text-align: center; margin-bottom: 15px;">
                <div style="font-size: 14px; color: #605070; margin-bottom: 10px;">✨ 三张牌阵占卜 ✨</div>
                <div style="font-size: 12px; color: #807090;">过去 · 现在 · 未来</div>
            </div>
            <div id="magicCards" style="display: flex; justify-content: center; gap: 15px; margin-bottom: 20px;">
                <div class="magic-card" id="card1" onclick="revealCard(0)">
                    <div class="card-back">🔮</div>
                    <div class="card-front" style="display: none;"></div>
                </div>
                <div class="magic-card" id="card2" onclick="revealCard(1)">
                    <div class="card-back">🔮</div>
                    <div class="card-front" style="display: none;"></div>
                </div>
                <div class="magic-card" id="card3" onclick="revealCard(2)">
                    <div class="card-back">🔮</div>
                    <div class="card-front" style="display: none;"></div>
                </div>
            </div>
            <div id="magicResult" style="display: none; background: rgba(255,255,255,0.7); border-radius: 8px; padding: 15px; margin-bottom: 15px;">
                <div id="cardInterpretations"></div>
            </div>
            <div style="text-align: center;">
                <button onclick="drawMagicCards()" style="padding: 10px 30px; background: linear-gradient(180deg, #d8b8e8 0%, #b890d0 100%); border: 2px solid #8060a0; border-radius: 20px; font-family: inherit; font-size: 14px; cursor: pointer; color: #fff; text-shadow: 0 1px 2px rgba(0,0,0,0.3);">
                    🌟 抽牌占卜
                </button>
            </div>
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
            <div class="taskbar-item" id="taskbar-networkWindow" onclick="toggleWindow('networkWindow')" style="display: none;">
                <span>🌐</span>
                <span>网上邻居</span>
            </div>
            <div class="taskbar-item" id="taskbar-fishWindow" onclick="toggleWindow('fishWindow')" style="display: none;">
                <span>🐟</span>
                <span>Fish</span>
            </div>
            <div class="taskbar-item" id="taskbar-magicWindow" onclick="toggleWindow('magicWindow')" style="display: none;">
                <span>🔮</span>
                <span>Magic</span>
            </div>
            <div class="taskbar-item" id="taskbar-dvdPlayerWindow" onclick="toggleWindow('dvdPlayerWindow')" style="display: none;">
                <span>💿</span>
                <span>DVD播放器</span>
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

        const bootMessages = [
            'BIOS Version 1.0.0 - Dreamcore Systems, Inc.',
            'Memory Test: 640K OK',
            'Detecting IDE drives...',
            'Primary Master: Dreamcore HDD',
            'Primary Slave: None',
            'Secondary Master: CD-ROM Drive',
            'Secondary Slave: None',
            '',
            'Loading Windows 98...',
            'HIMEM is testing extended memory...done.',
            'EMM386: Unable to set page frame base address.',
            'Microsoft(R) Windows 98',
            '   (C)Copyright Microsoft Corp 1981-1999.',
            '',
            'Initializing device drivers...',
            'Loading system files...',
            'Starting Windows 98...'
        ];

        const bootStatusMessages = [
            '正在检测硬件',
            '正在加载驱动程序',
            '正在初始化系统',
            '正在加载配置文件',
            '正在启动 Windows',
            '正在准备桌面'
        ];

        function runBootSequence() {
            const bootBios = document.getElementById('bootBios');
            const bootLogo = document.getElementById('bootLogo');
            const bootWelcome = document.getElementById('bootWelcome');
            const bootProgressFill = document.getElementById('bootProgressFill');
            const bootStatus = document.getElementById('bootStatus');
            const dots = bootStatus.querySelector('.boot-dots');
            
            bootBios.classList.add('active');
            
            let lineIndex = 0;
            let currentText = '';
            
            const biosInterval = setInterval(() => {
                if (lineIndex < bootMessages.length) {
                    currentText += bootMessages[lineIndex] + '\n';
                    bootBios.textContent = currentText;
                    lineIndex++;
                } else {
                    clearInterval(biosInterval);
                    setTimeout(() => {
                        bootBios.classList.remove('active');
                        bootLogo.classList.add('active');
                        runProgressSequence();
                    }, 500);
                }
            }, 120);
        }

        function runProgressSequence() {
            const bootProgressFill = document.getElementById('bootProgressFill');
            const bootStatus = document.getElementById('bootStatus');
            const dots = bootStatus.querySelector('.boot-dots');
            const bootWelcome = document.getElementById('bootWelcome');
            const bootLogo = document.getElementById('bootLogo');
            
            let progress = 0;
            let messageIndex = 0;
            let dotCount = 0;
            
            const dotInterval = setInterval(() => {
                dotCount = (dotCount + 1) % 4;
                dots.textContent = '.'.repeat(dotCount);
            }, 300);
            
            const progressInterval = setInterval(() => {
                progress += Math.random() * 8 + 2;
                if (progress > 100) progress = 100;
                bootProgressFill.style.width = progress + '%';
                
                const newMessageIndex = Math.floor(progress / 20);
                if (newMessageIndex < bootStatusMessages.length && newMessageIndex !== messageIndex) {
                    messageIndex = newMessageIndex;
                    const statusText = bootStatus.textContent.split('。')[0] + '。';
                    bootStatus.innerHTML = bootStatusMessages[messageIndex] + '<span class="boot-dots"></span>';
                }
                
                if (progress >= 100) {
                    clearInterval(progressInterval);
                    clearInterval(dotInterval);
                    setTimeout(() => {
                        bootLogo.classList.remove('active');
                        bootWelcome.classList.add('active');
                    }, 500);
                }
            }, 150);
        }

        function enterDesktop() {
            const bootScreen = document.getElementById('bootScreen');
            bootScreen.classList.add('hidden');
        }

        document.getElementById('bootWelcome').addEventListener('click', enterDesktop);
        document.addEventListener('keydown', (e) => {
            const bootWelcome = document.getElementById('bootWelcome');
            if (bootWelcome.classList.contains('active')) {
                enterDesktop();
            }
        });

        window.addEventListener('load', runBootSequence);

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
            
            const style = emotionValence > 0.3 ? 'bright' : emotionValence < -0.3 ? 'deep' : 'calm';
            const label = emotionValence > 0.3 ? 'Bright' : emotionValence < -0.3 ? 'Deep' : 'Calm';
            
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
            
            const style = emotionValence > 0.3 ? 'bright' : emotionValence < -0.3 ? 'deep' : 'calm';
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
            if (!win) return;
            
            win.style.display = 'flex';
            win.classList.remove('minimized-window');
            setActiveWindow(windowId);
            
            const taskbarItem = document.getElementById('taskbar-' + windowId);
            if (taskbarItem) taskbarItem.style.display = 'flex';
            
            const initMap = {
                'paintWindow': initPaint,
                'emotionWindow': initEmotionBar,
                'minesweeperWindow': initMinesweeper
            };
            if (initMap[windowId]) setTimeout(initMap[windowId], 100);
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
            { title: 'Outer Wilds', artist: 'Andrew Prahlow', album: 'Outer Wilds OST', src: 'https://github.com/Redbeancc7/cc/releases/download/v1.0/Andrew.Prahlow.-.Outer.Wilds.mp3', cover: '🌌' },
            { title: 'Are You Lost', artist: 'Park Bird', album: 'Dreamcore', src: 'https://github.com/Redbeancc7/cc/releases/download/v1.0/Park.Bird.-.Are.You.Lost.1.mp3', cover: '🎵' },
            { title: 'Hi', artist: 'TEMPOREX', album: 'Chill Vibes', src: 'https://github.com/Redbeancc7/cc/releases/download/v1.0/TEMPOREX.-.Hi.mp3', cover: '🌙' },
            { title: '她呓语', artist: '贺予彤', album: '独立音乐', src: 'https://github.com/Redbeancc7/cc/releases/download/v1.0/tayiyu.mp3', cover: '🌸' },
            { title: '载我回家', artist: '张悬', album: 'My Life Will', src: 'https://github.com/Redbeancc7/cc/releases/download/v1.0/zawohj.mp3', cover: '🏠' },
            { title: '想去码头整点薯条', artist: '黄金玉米王', album: '网络热歌', src: 'https://github.com/Redbeancc7/cc/releases/download/v1.0/shutiao.mp3', cover: '🍟' },
            { title: 'Redbean', artist: 'Unknown', album: 'Collection', src: 'https://github.com/Redbeancc7/cc/releases/download/v1.0/redbean.mp3', cover: '🎵' }
        ];

        let currentTrack = 0;
        let isPlaying = false;
        let currentTime = 0;
        let volume = 0.7;
        let isMuted = false;
        let musicDragState = null;
        let progressInterval = null;
        let audioPlayer = null;

        function initMusicPlayer() {
            audioPlayer = new Audio();
            audioPlayer.volume = volume;
            
            audioPlayer.addEventListener('timeupdate', () => {
                if (audioPlayer.duration) {
                    currentTime = audioPlayer.currentTime;
                    const progress = (currentTime / audioPlayer.duration) * 100;
                    document.getElementById('progressFill').style.width = progress + '%';
                    document.getElementById('currentTime').textContent = formatTime(currentTime);
                }
            });
            
            audioPlayer.addEventListener('ended', () => {
                nextTrack();
            });
            
            audioPlayer.addEventListener('loadedmetadata', () => {
                document.getElementById('totalTime').textContent = formatTime(audioPlayer.duration);
            });
            
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
            document.getElementById('progressFill').style.width = '0%';
            document.getElementById('currentTime').textContent = '0:00';
            document.getElementById('totalTime').textContent = '0:00';
            
            if (audioPlayer) {
                audioPlayer.src = track.src;
                if (isPlaying) {
                    audioPlayer.play().catch(() => {});
                }
            }
            
            document.querySelectorAll('.music-playlist-item').forEach((item, index) => {
                item.classList.toggle('active', index === currentTrack);
            });
        }

        function formatTime(seconds) {
            if (!seconds || isNaN(seconds)) return '0:00';
            const mins = Math.floor(seconds / 60);
            const secs = Math.floor(seconds % 60);
            return `${mins}:${secs.toString().padStart(2, '0')}`;
        }

        function togglePlay() {
            if (!audioPlayer) return;
            
            isPlaying = !isPlaying;
            const player = document.getElementById('musicPlayer');
            const btn = document.getElementById('playPauseBtn');
            
            if (isPlaying) {
                player.classList.remove('paused');
                btn.textContent = '⏸';
                audioPlayer.play().catch(() => {
                    isPlaying = false;
                    player.classList.add('paused');
                    btn.textContent = '▶';
                });
            } else {
                player.classList.add('paused');
                btn.textContent = '▶';
                audioPlayer.pause();
            }
            updateMiniIconState();
        }

        function prevTrack() {
            currentTrack = (currentTrack - 1 + playlist.length) % playlist.length;
            updateTrackInfo();
        }

        function nextTrack() {
            currentTrack = (currentTrack + 1) % playlist.length;
            updateTrackInfo();
        }

        function playTrack(index) {
            currentTrack = index;
            updateTrackInfo();
            if (!isPlaying) {
                togglePlay();
            }
        }

        function seekMusic(e) {
            if (!audioPlayer || !audioPlayer.duration) return;
            const bar = document.getElementById('progressBar');
            const rect = bar.getBoundingClientRect();
            const percent = (e.clientX - rect.left) / rect.width;
            audioPlayer.currentTime = percent * audioPlayer.duration;
        }

        function setVolume(e) {
            const slider = document.getElementById('volumeSlider');
            const rect = slider.getBoundingClientRect();
            volume = Math.max(0, Math.min(1, (e.clientX - rect.left) / rect.width));
            isMuted = false;
            if (audioPlayer) audioPlayer.volume = isMuted ? 0 : volume;
            updateVolumeUI();
        }

        function toggleMute() {
            isMuted = !isMuted;
            if (audioPlayer) audioPlayer.volume = isMuted ? 0 : volume;
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
            const isDigit = key >= '0' && key <= '9';
            const isOperator = ['+', '-', '*', '/'].includes(key);
            
            if (isDigit) {
                calcValue = calcNewNumber ? key : (calcValue === '0' ? key : calcValue + key);
                calcNewNumber = false;
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
            } else if (isOperator) {
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

        let printerImageUrl = '';

        function openPrinterWindow() {
            const existingWindow = document.getElementById('printerWindow');
            if (existingWindow) {
                existingWindow.remove();
            }
            
            const printerWin = document.createElement('div');
            printerWin.id = 'printerWindow';
            printerWin.className = 'win-window';
            printerWin.style.cssText = 'top: 100px; left: 250px; width: 400px; height: auto; display: flex; z-index: 150;';
            
            printerWin.innerHTML = `
                <div style="width: 100%;">
                    <div class="win-titlebar" onmousedown="startDrag(event, 'printerWindow')">
                        <div class="win-titlebar-left">
                            <div class="win-titlebar-icon">🖨️</div>
                            <span class="win-titlebar-text">打印机</span>
                        </div>
                        <div class="win-titlebar-controls">
                            <button class="win-btn win-btn-close" onclick="document.getElementById('printerWindow').remove()"></button>
                        </div>
                    </div>
                    <div style="padding: 15px; background: var(--win-bg);">
                        <div style="margin-bottom: 10px; font-size: 12px; color: #404040;">请输入图片链接：</div>
                        <input type="text" id="printerImageUrlInput" value="https://github.com/Redbeancc7/cc/releases/download/v2.0/fe87a7809fb33237f79e86fcd2baf913.png" placeholder="https://example.com/image.png" 
                            style="width: 100%; padding: 6px 8px; border: 2px solid; border-color: var(--win-dark) var(--win-light) var(--win-light) var(--win-dark); background: white; font-family: inherit; font-size: 12px; box-sizing: border-box;">
                        <div style="margin-top: 12px; display: flex; gap: 10px; justify-content: center;">
                            <button onclick="startPrinting()" style="padding: 5px 20px; background: var(--win-bg); border: 2px solid; border-color: var(--win-light) var(--win-darker) var(--win-darker) var(--win-light); font-family: inherit; font-size: 12px; cursor: pointer;">🖨️ 打印</button>
                            <button onclick="document.getElementById('printerWindow').remove()" style="padding: 5px 20px; background: var(--win-bg); border: 2px solid; border-color: var(--win-light) var(--win-darker) var(--win-darker) var(--win-light); font-family: inherit; font-size: 12px; cursor: pointer;">取消</button>
                        </div>
                    </div>
                </div>
            `;
            
            document.body.appendChild(printerWin);
        }

        function startPrinting() {
            const urlInput = document.getElementById('printerImageUrlInput');
            const imageUrl = urlInput ? urlInput.value.trim() : '';
            
            if (!imageUrl) {
                alert('请输入图片链接！');
                return;
            }
            
            const printerWin = document.getElementById('printerWindow');
            if (printerWin) printerWin.remove();
            
            showPrintingAnimation(imageUrl);
        }

        function showPrintingAnimation(imageUrl) {
            const printOverlay = document.createElement('div');
            printOverlay.id = 'printOverlay';
            printOverlay.style.cssText = `
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0, 0, 0, 0.5);
                display: flex;
                align-items: center;
                justify-content: center;
                z-index: 20000;
            `;
            
            printOverlay.innerHTML = `
                <div style="
                    background: var(--win-bg);
                    border: 2px solid;
                    border-color: var(--win-light) var(--win-darker) var(--win-darker) var(--win-light);
                    padding: 20px 30px;
                    text-align: center;
                    box-shadow: 3px 3px 10px rgba(0,0,0,0.3);
                ">
                    <div style="font-size: 40px; margin-bottom: 10px;">🖨️</div>
                    <div style="font-size: 14px; color: #404040;">正在打印...</div>
                    <div style="margin-top: 10px; width: 150px; height: 8px; background: #c0b8c0; border: 1px solid #808080; overflow: hidden;">
                        <div id="printProgressBar" style="width: 0%; height: 100%; background: linear-gradient(90deg, #a090b8, #c0b0d0); transition: width 0.3s;"></div>
                    </div>
                </div>
            `;
            
            document.body.appendChild(printOverlay);
            
            let progress = 0;
            const progressBar = document.getElementById('printProgressBar');
            const progressInterval = setInterval(() => {
                progress += 5;
                if (progressBar) progressBar.style.width = progress + '%';
                
                if (progress >= 100) {
                    clearInterval(progressInterval);
                    setTimeout(() => {
                        printOverlay.remove();
                        showPrintedImage(imageUrl);
                    }, 300);
                }
            }, 100);
        }

        function showPrintedImage(imageUrl) {
            const printedPaper = document.createElement('div');
            printedPaper.id = 'printedPaper';
            printedPaper.style.cssText = `
                position: fixed;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%);
                z-index: 20000;
                animation: paperSlideIn 0.5s ease-out;
            `;
            
            printedPaper.innerHTML = `
                <div style="
                    background: white;
                    border: 1px solid #c0c0c0;
                    box-shadow: 3px 3px 15px rgba(0,0,0,0.4);
                    padding: 20px;
                    max-width: 400px;
                ">
                    <div style="text-align: center; margin-bottom: 15px; padding-bottom: 10px; border-bottom: 1px dashed #c0c0c0;">
                        <span style="font-size: 12px; color: #808080;">🖨️ 打印输出</span>
                    </div>
                    <div style="text-align: center;">
                        <img src="${imageUrl}" style="max-width: 100%; max-height: 300px; object-fit: contain;" onerror="this.style.display='none'; this.parentElement.innerHTML='<div style=\\'color:#c03030;font-size:12px;\\'>图片加载失败</div>';">
                    </div>
                    <div style="text-align: center; margin-top: 15px;">
                        <button onclick="document.getElementById('printedPaper').remove()" style="padding: 5px 25px; background: var(--win-bg); border: 2px solid; border-color: var(--win-light) var(--win-darker) var(--win-darker) var(--win-light); font-family: inherit; font-size: 12px; cursor: pointer;">关闭</button>
                    </div>
                </div>
            `;
            
            document.body.appendChild(printedPaper);
            
            printedPaper.addEventListener('click', (e) => {
                if (e.target === printedPaper) {
                    printedPaper.remove();
                }
            });
        }

        const fishFortunes = ['大吉', '中吉', '小吉', '吉', '末吉', '凶转吉', '平', '小凶', '末凶'];
        const fishEmojis = ['🐟', '🐠', '🐡', '🦈', '🐬', '🐳', '🦭', '🦐', '🦀', '🐙', '🦑', '🐚'];
        
        const fishActivities = [
            '宜：摸鱼', '宜：发呆', '宜：喝水', '宜：吃零食', '宜：听歌', '宜：散步',
            '宜：早睡', '宜：赖床', '宜：打游戏', '宜：看剧', '宜：撸猫', '宜：晒太阳',
            '宜：吃火锅', '宜：喝奶茶', '宜：网购', '宜：刷手机', '宜：发朋友圈', '宜：拍照',
            '忌：加班', '忌：早起', '忌：开会', '忌：写报告', '忌：回消息', '忌：运动'
        ];
        
        const fishTips = [
            '今日宜多喝水，保持好心情~',
            '运气不错，适合买彩票试试手气！',
            '今天可能会有小惊喜哦~',
            '保持微笑，好运自然来！',
            '适合和朋友聊聊天~',
            '今天适合尝试新事物！',
            '记得按时吃饭，照顾好自己~',
            '今天适合放松一下，不要太拼~',
            '好运正在路上，请耐心等待~',
            '今天可能会有意外收获！',
            '适合整理一下心情和桌面~',
            '今天适合做喜欢的事情~',
            '记得给自己留点私人时间~',
            '今天适合早睡早起~',
            '可能会有贵人相助哦~',
            '今天适合学习新技能~',
            '记得多笑笑，心情会更好~',
            '今天适合和家人联系~',
            '可能会有好消息传来~',
            '今天适合犒劳自己吃顿好的！',
            '鱼鱼提醒你：你是最棒的！',
            '今天适合看一部好电影~',
            '记得深呼吸，一切都会好的~',
            '今天适合做一个小计划~',
            '鱼鱼祝你今天顺顺利利！',
            '今天适合穿喜欢的衣服出门~',
            '可能会有意想不到的好事发生~',
            '今天适合给朋友一个小惊喜~',
            '记得对自己好一点~',
            '鱼鱼说：你值得所有美好的事物！'
        ];

        const tarotCards = [
            { name: '愚者', emoji: '🃏', upright: '新的开始，无限可能，冒险精神，纯真无畏', reversed: '鲁莽冲动，缺乏方向，逃避责任，不切实际' },
            { name: '魔术师', emoji: '🎭', upright: '创造力，自信，技能展现，新机遇', reversed: '欺骗，操纵，才能浪费，缺乏自信' },
            { name: '女祭司', emoji: '🌙', upright: '直觉，神秘，内在智慧，潜意识', reversed: '隐藏的真相，表面化，忽视直觉，秘密暴露' },
            { name: '女皇', emoji: '👑', upright: '丰饶，母性，创造力，自然之美', reversed: '创意枯竭，依赖他人，过度保护，忽视自我' },
            { name: '皇帝', emoji: '🏛️', upright: '权威，领导力，秩序，稳定', reversed: '专制，僵化，控制欲，缺乏纪律' },
            { name: '教皇', emoji: '📿', upright: '传统，信仰，精神指引，教育', reversed: '打破常规，个人信念，反叛，教条主义' },
            { name: '恋人', emoji: '💕', upright: '爱情，和谐，选择，价值观', reversed: '关系失衡，错误选择，价值观冲突，不和谐' },
            { name: '战车', emoji: '⚔️', upright: '意志力，胜利，决心，控制', reversed: '失控，缺乏方向，侵略性，挫折' },
            { name: '力量', emoji: '🦁', upright: '内在力量，勇气，耐心，自我控制', reversed: '自我怀疑，软弱，缺乏自信，滥用力量' },
            { name: '隐士', emoji: '🏔️', upright: '内省，寻求真理，孤独，智慧', reversed: '孤立，逃避，拒绝帮助，迷失方向' },
            { name: '命运之轮', emoji: '🎡', upright: '命运转折，好运，循环，机遇', reversed: '厄运，抗拒改变，失控，坏运气' },
            { name: '正义', emoji: '⚖️', upright: '公正，真理，因果，平衡', reversed: '不公，偏见，逃避责任，失衡' },
            { name: '倒吊人', emoji: '🙃', upright: '牺牲，等待，新视角，放下', reversed: '拖延，无谓牺牲，固执，僵局' },
            { name: '死神', emoji: '💀', upright: '结束，转变，新生，放下过去', reversed: '抗拒改变，停滞，无法放手，恐惧' },
            { name: '节制', emoji: '🏺', upright: '平衡，调和，耐心，适度', reversed: '失衡，过度，缺乏耐心，冲突' },
            { name: '恶魔', emoji: '😈', upright: '束缚，诱惑，物质主义，阴影', reversed: '解脱，打破束缚，面对阴影，自由' },
            { name: '塔', emoji: '🗼', upright: '突变，毁灭，觉醒，真相揭露', reversed: '逃避灾难，恐惧改变，延迟崩溃' },
            { name: '星星', emoji: '⭐', upright: '希望，灵感，平静，治愈', reversed: '绝望，失去信心，断开连接，不切实际' },
            { name: '月亮', emoji: '🌕', upright: '幻觉，直觉，潜意识，恐惧', reversed: '释放恐惧，真相显现，清晰，平静' },
            { name: '太阳', emoji: '☀️', upright: '成功，快乐，活力，积极', reversed: '暂时的挫折，过度乐观，延迟的成功' },
            { name: '审判', emoji: '📯', upright: '觉醒，重生，召唤，宽恕', reversed: '自我怀疑，拒绝召唤，无法原谅' },
            { name: '世界', emoji: '🌍', upright: '完成，成就，圆满，新旅程', reversed: '未完成，缺乏闭合，延迟成功' }
        ];

        const positionMeanings = ['过去', '现在', '未来'];
        let currentCards = [];
        let revealedCount = 0;

        function openDVDPlayer() {
            const win = document.getElementById('dvdPlayerWindow');
            win.style.display = 'flex';
            const taskbarItem = document.getElementById('taskbar-dvdPlayerWindow');
            if (taskbarItem) taskbarItem.style.display = 'flex';
            setActiveWindow('dvdPlayerWindow');
            const video = document.getElementById('dvdVideo');
            video.play();
        }

        function closeDVDPlayer() {
            const video = document.getElementById('dvdVideo');
            video.pause();
            video.currentTime = 0;
            const win = document.getElementById('dvdPlayerWindow');
            win.style.display = 'none';
            const taskbarItem = document.getElementById('taskbar-dvdPlayerWindow');
            if (taskbarItem) taskbarItem.style.display = 'none';
        }

        function openMagicWindow() {
            const win = document.getElementById('magicWindow');
            win.style.display = 'flex';
            const taskbarItem = document.getElementById('taskbar-magicWindow');
            if (taskbarItem) taskbarItem.style.display = 'flex';
            setActiveWindow('magicWindow');
            resetMagicCards();
        }

        function resetMagicCards() {
            currentCards = [];
            revealedCount = 0;
            for (let i = 1; i <= 3; i++) {
                const card = document.getElementById('card' + i);
                card.querySelector('.card-back').style.display = 'flex';
                card.querySelector('.card-front').style.display = 'none';
                card.querySelector('.card-front').classList.remove('reversed');
            }
            document.getElementById('magicResult').style.display = 'none';
        }

        function drawMagicCards() {
            resetMagicCards();
            const shuffled = [...tarotCards].sort(() => Math.random() - 0.5);
            currentCards = shuffled.slice(0, 3).map(card => ({
                ...card,
                isReversed: Math.random() < 0.5
            }));
            
            for (let i = 1; i <= 3; i++) {
                const card = document.getElementById('card' + i);
                card.style.animation = 'fadeIn 0.5s ease';
            }
        }

        function revealCard(index) {
            if (!currentCards[index] || revealedCount > index) return;
            
            const cardEl = document.getElementById('card' + (index + 1));
            const cardFront = cardEl.querySelector('.card-front');
            const cardBack = cardEl.querySelector('.card-back');
            const card = currentCards[index];
            
            cardFront.innerHTML = `
                <span>${card.emoji}</span>
                <span class="card-name">${card.isReversed ? '逆位: ' : '正位: '}${card.name}</span>
            `;
            
            if (card.isReversed) {
                cardFront.classList.add('reversed');
            }
            
            cardEl.style.animation = 'cardFlip 0.6s ease';
            setTimeout(() => {
                cardBack.style.display = 'none';
                cardFront.style.display = 'flex';
            }, 300);
            
            revealedCount++;
            
            if (revealedCount === 3) {
                setTimeout(showInterpretations, 800);
            }
        }

        function showInterpretations() {
            const resultDiv = document.getElementById('magicResult');
            const interpDiv = document.getElementById('cardInterpretations');
            
            let html = '';
            currentCards.forEach((card, index) => {
                const meaning = card.isReversed ? card.reversed : card.upright;
                const position = positionMeanings[index];
                const status = card.isReversed ? '逆位' : '正位';
                
                html += `
                    <div style="margin-bottom: 12px; padding: 10px; background: rgba(255,255,255,0.5); border-radius: 6px;">
                        <div style="font-weight: bold; color: #605070; margin-bottom: 5px;">
                            ${position} · ${card.emoji} ${card.name} (${status})
                        </div>
                        <div style="font-size: 12px; color: #505050; line-height: 1.5;">
                            ${meaning}
                        </div>
                    </div>
                `;
            });
            
            interpDiv.innerHTML = html;
            resultDiv.style.display = 'block';
            resultDiv.style.animation = 'fadeIn 0.5s ease';
        }

        function openFishWindow() {
            const win = document.getElementById('fishWindow');
            win.style.display = 'flex';
            const taskbarItem = document.getElementById('taskbar-fishWindow');
            if (taskbarItem) taskbarItem.style.display = 'flex';
            setActiveWindow('fishWindow');
            refreshFish();
        }

        function refreshFish() {
            const fortune = fishFortunes[Math.floor(Math.random() * fishFortunes.length)];
            const emoji = fishEmojis[Math.floor(Math.random() * fishEmojis.length)];
            const activity = fishActivities[Math.floor(Math.random() * fishActivities.length)];
            const tip = fishTips[Math.floor(Math.random() * fishTips.length)];
            
            const container = document.getElementById('fishContainer');
            container.style.animation = 'none';
            container.offsetHeight;
            container.style.animation = 'fadeIn 0.3s ease';
            
            document.getElementById('fishEmoji').textContent = emoji;
            document.getElementById('fishFortune').textContent = fortune;
            document.getElementById('fishTime').textContent = activity;
            document.getElementById('fishTip').textContent = tip;
            
            const fortuneEl = document.getElementById('fishFortune');
            if (fortune.includes('吉')) {
                fortuneEl.style.color = '#50a070';
            } else if (fortune.includes('凶')) {
                fortuneEl.style.color = '#c06060';
            } else {
                fortuneEl.style.color = '#6080a0';
            }
        }

        function openNetworkComputer() {
            showNetworkDialog();
        }

        function showNetworkDialog() {
            const existingDialog = document.getElementById('networkDialog');
            if (existingDialog) {
                existingDialog.remove();
            }
            
            const dialog = document.createElement('div');
            dialog.id = 'networkDialog';
            dialog.style.cssText = `
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background: rgba(0, 0, 0, 0.3);
                display: flex;
                align-items: center;
                justify-content: center;
                z-index: 10000;
            `;
            
            dialog.innerHTML = `
                <div style="
                    background: var(--win-bg);
                    border: 2px solid;
                    border-color: var(--win-light) var(--win-darker) var(--win-darker) var(--win-light);
                    box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.3);
                    min-width: 320px;
                    max-width: 400px;
                ">
                    <div style="
                        background: linear-gradient(180deg, #d8c8e8 0%, #c8b8d8 100%);
                        padding: 8px 10px;
                        display: flex;
                        align-items: center;
                        gap: 8px;
                        border-bottom: 1px solid var(--win-dark);
                    ">
                        <span style="font-size: 16px;">⚠️</span>
                        <span style="color: #404040; font-size: 12px; font-weight: bold;">连接失败</span>
                    </div>
                    <div style="
                        padding: 25px 20px;
                        display: flex;
                        align-items: flex-start;
                        gap: 15px;
                        background: var(--win-bg);
                    ">
                        <div style="font-size: 40px; line-height: 1;">⚠️</div>
                        <div style="flex: 1; font-size: 12px; line-height: 1.6; color: #404040;">
                            距离太远，无法连接。<br>请使用微信聊天进行修复。
                        </div>
                    </div>
                    <div style="
                        padding: 10px 15px 15px;
                        display: flex;
                        justify-content: center;
                        background: var(--win-bg);
                        border-top: 1px solid var(--win-light);
                    ">
                        <button onclick="document.getElementById('networkDialog').remove()" style="
                            min-width: 80px;
                            padding: 4px 20px;
                            background: var(--win-bg);
                            border: 2px solid;
                            border-color: var(--win-light) var(--win-darker) var(--win-darker) var(--win-light);
                            font-family: inherit;
                            font-size: 12px;
                            cursor: pointer;
                        " onmouseover="this.style.background='var(--win-light)'" onmouseout="this.style.background='var(--win-bg)'">
                            确定
                        </button>
                    </div>
                </div>
            `;
            
            document.body.appendChild(dialog);
            
            dialog.addEventListener('click', (e) => {
                if (e.target === dialog) {
                    dialog.remove();
                }
            });
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

        const noteStyles = ['dreamcore', 'vaporwave', 'cyberpunk', 'nostalgic', 'ethereal', 'morandi-pink', 'morandi-yellow', 'morandi-blue', 'morandi-green', 'morandi-lavender', 'morandi-beige', 'morandi-sage', 'morandi-mist'];
        
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
        const lowSaturationColors = ['#d4a8b0', '#a8c8d8', '#c8d8a8', '#d8c8a8', '#c8a8d8', '#b8c8d0', '#d0c8b8', '#c0d0c8'];
        
        const getRandomItem = arr => arr[Math.floor(Math.random() * arr.length)];
        
        function showHeartPopup() {
            const count = Math.floor(Math.random() * 6) + 1;
            for (let i = 0; i < count; i++) {
                setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.className = 'heart-popup';
                    heart.textContent = '♥';
                    heart.style.left = `${Math.random() * (window.innerWidth - 50)}px`;
                    heart.style.top = `${Math.random() * (window.innerHeight - 150)}px`;
                    const color = getRandomItem(heartColors);
                    heart.style.color = color;
                    heart.style.textShadow = `0 0 10px ${color}`;
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
            
            const heartColors = ['#d4a8b0', '#b8a0b0', '#c8b0b8', '#e0c0c8', '#a89898'];
            const lowSaturationColors = ['#c8b8c0', '#b8c0c8', '#c0c0b8', '#b8b8c0', '#c0b8b8', '#d0c0c8'];
            
            const camusQuotes = [
                '在隆冬，我终于知道，我身上有一个不可战胜的夏天。',
                '不要走在我后面，因为我可能不会引路；不要走在我前面，因为我可能不会跟随；请走在我的身边，做我的朋友。',
                '爱是没有界限的，如果我能拥抱一切，那拥抱得笨拙又有什么关系。',
                '在光亮中，世界始终是我们最初和最后的爱。',
                '当对幸福的憧憬过于急切，那痛苦就在人的心灵深处升起。',
                '我无法对你说出我对你的爱，因为爱是无法言说的。',
                '在这个世界上，只有爱才是唯一的真实。',
                '我想给你打电话，告诉你天气晴朗，告诉你我爱你，就像人们爱希望和爱确定一样。',
                '荒谬当道，爱拯救之。',
                '我想要在你身上留下我的痕迹，就像树在石头上留下年轮。',
                '爱不需要理解，因为爱本身就是一种理解。',
                '真正的救赎，在于纵身一跃。',
                '我们每个人都在寻找自己的出口。',
                '生命是短暂的，浪费时间是最大的罪过。',
                '在世界的尽头，我们终将相遇。'
            ];
            
            const dreamcorePhrases = [
                '梦境边缘的微光，正在等待你的到来...',
                '在时间的缝隙里，我们相遇了。',
                '你听，云朵在低语。',
                '这里的一切都是柔软的，包括时间。',
                '欢迎来到梦的彼岸。',
                '在记忆的迷宫里，我找到了你。',
                '天空是淡紫色的，就像我们的相遇。',
                '每一朵云都藏着一个故事。',
                '风带来了远方的气息。',
                '在这个世界里，一切皆有可能。',
                '闭上眼睛，感受梦的温度。',
                '你相信平行时空吗？也许我们在那里已经相遇过。',
                '星星在白天也在闪烁，只是我们看不见。',
                '时间在这里是圆形的，没有开始也没有结束。',
                '梦是现实的倒影，现实是梦的延续。',
                '在这里，每一秒都是永恒。',
                '你听见了什么？是心跳，还是时间的脚步？'
            ];
            
            const comfortWords = [
                '一切都会好起来的，我在这里陪着你 ♥',
                '你很棒，不要怀疑自己。',
                '累了就休息一下吧，梦会治愈一切。',
                '你的感受是被看见的，被理解的。',
                '每一天都是新的开始，像清晨的云朵一样。',
                '温柔地对待自己，就像对待一朵花。',
                '你值得所有的美好。',
                '即使在最深的夜里，也有星星在等你。',
                '难过的时候，记得抬头看看天空。',
                '你的存在本身就是一种美好。',
                '让眼泪流出来吧，它会带走悲伤。',
                '我会在你身边，直到阳光再次出现。'
            ];
            
            const happyWords = [
                '看到你开心，我也很开心！♥',
                '你的快乐像阳光一样温暖。',
                '笑一个吧，世界会跟着你笑。',
                '快乐是会传染的，谢谢你分享给我！',
                '今天是个好日子呢~',
                '你的笑容比云朵还柔软。',
                '保持这份快乐，它会带你去更远的地方。',
                '开心的时候，整个世界都在微笑。'
            ];
            
            const curiousReplies = [
                '这是个好问题呢~ 让我想想...',
                '有时候答案就在问题本身里。',
                '你问的问题让我也开始思考了。',
                '也许答案就在你心里，只是还没被发现。',
                '好奇是通往新世界的钥匙 ✨',
                '让我们一起探索这个问题的答案吧。'
            ];
            
            const thinkingReplies = [
                '嗯...让我想想...',
                '这是一个值得深思的问题。',
                '有时候，思考本身就是答案。',
                '在梦的世界里，一切都有无限可能。'
            ];
            
            const keywordReplies = {
                '你好': ['你好呀~ 欢迎来到梦核世界 ♥', '嗨！今天过得怎么样？', '你好，很高兴见到你！', '你好~ 愿今天有美好的相遇'],
                'hello': ['Hello~ Welcome to dreamcore ♥', 'Hi there! ✨', 'Hello, dreamer!', 'Hey! Nice to meet you!'],
                'hi': ['Hi~ ✨', 'Hey! 有什么想聊的吗？', 'Hi! 欢迎来到这里~', 'Hi~ 今天心情怎么样？'],
                '早上': ['早安~ 新的一天开始了 ♥', '早上好！今天也要元气满满哦~', '早安，愿今天充满美好~', '早安~ 记得吃早餐哦！'],
                '中午': ['中午好~ 记得吃饭哦 ♥', '午安~ 休息一下吧', '中午了，来杯咖啡怎么样？'],
                '下午': ['下午好~ 来杯茶吗？', '下午茶时间到了~', '下午好！今天过得怎么样？'],
                '晚上': ['晚上好~ 今天过得怎么样？', '夜幕降临，星星开始闪烁了 ✨', '晚上好~ 放松一下吧'],
                '晚安': ['晚安~ 做个好梦 ♥', '晚安，愿梦里有星星和云朵。', 'Good night, sweet dreams ✨', '晚安~ 明天见'],
                '谢谢': ['不客气~ ♥', '能帮到你我很开心！', '随时都在这里陪你~', '不用谢，这是我的荣幸 ♥'],
                '感谢': ['不客气~ ♥', '能帮到你我很开心！', '你的感谢让我很温暖'],
                '对不起': ['没关系的~ ♥', '不要道歉，你很好。', '一切都会过去的~', '没关系，我原谅你 ♥'],
                '抱歉': ['没关系的~ ♥', '不用道歉，我理解你。', '每个人都会犯错，没关系的。'],
                '无聊': ['无聊的时候，可以看看云朵~', '要不要听个故事？', '闭上眼睛，想象一个新世界...', '无聊是创意的开始哦~'],
                '累': ['累了就休息一下吧~ ♥', '照顾好自己哦。', '让梦来治愈你吧。', '休息是为了走更远的路。'],
                '困': ['困了就睡吧~ 梦里见 ♥', '晚安，做个好梦。', '睡个好觉，明天会更好。'],
                '饿': ['饿了就吃点东西吧~', '记得好好吃饭哦 ♥', '美食是最好的治愈~'],
                '渴': ['渴了就喝水吧~ 记得多喝水哦', '来杯茶怎么样？', '水是生命的源泉~'],
                '难过': comfortWords,
                '伤心': comfortWords,
                '不开心': comfortWords,
                '郁闷': comfortWords,
                '烦': ['烦的时候，深呼吸~', '让烦恼随风而去吧。', '我陪你，一切都会好的。', '来聊聊吧，也许会好一点。'],
                '开心': happyWords,
                '高兴': happyWords,
                '快乐': happyWords,
                '哈哈': ['哈哈~ 你笑起来真好听！', '笑是最好看的表情 ♥', '继续笑吧，世界需要你的快乐！', '哈哈~ 开心最重要！'],
                '嘻嘻': ['嘻嘻~ 你好可爱 ♥', '笑起来的你真好看~', '嘻嘻~ 今天心情不错呢！'],
                '呵呵': ['呵呵~ 看起来心情不错呢', '微笑是最好的语言 ♥'],
                '天气': ['今天的云朵很温柔呢~', '无论天气如何，心情可以自己决定哦~', '看看窗外，也许有惊喜~', '天气如何，心就如何~'],
                '名字': ['我是梦核世界的守护者~', '你可以叫我任何名字 ♥', '名字只是一个代号，重要的是我们相遇了。', '我是陪伴你的朋友~'],
                '你是谁': ['我是梦核世界的守护者~', '我是你梦境中的一缕微光 ♥', '我是陪伴你的朋友。', '我是你在这个世界的倾听者。'],
                '喜欢': ['我也喜欢你~ ♥', '喜欢是一种美好的感觉。', '被喜欢是一件幸福的事~', '喜欢就让世界变得更美好。'],
                '爱': ['爱是最美好的力量 ♥', '爱让一切变得有意义。', '爱不需要理由，只需要真心。'],
                '梦': ['梦是另一个真实的世界...', '在梦里，一切皆有可能。', '梦境边缘，有光在等待。', '梦是灵魂的旅行。'],
                '云': ['云朵在轻轻飘动...', '每一朵云都是天空的诗。', '云会带走你的烦恼~', '云是天空的信使。'],
                '星': ['星星在看着你呢~', '你也是一颗星星，只是自己不知道。', '抬头看看，星星在眨眼。', '每颗星星都是一个愿望。'],
                '月': ['月亮在微笑呢~', '月色温柔，就像你的心。', '今晚的月色真美。'],
                '太阳': ['阳光会照亮每一个角落~', '太阳每天都会升起，希望也是。', '让阳光照进心里吧。'],
                '音乐': ['音乐是灵魂的语言~', '让音乐带你去旅行吧。', '千千静听里有好听的歌哦~', '音乐能治愈一切。'],
                '歌': ['想听什么歌呢？', '音乐是最好的陪伴~', '让歌声带你去远方。'],
                '游戏': ['想玩游戏吗？试试扫雷吧~', '游戏是放松的好方式。', '玩得开心最重要！'],
                '扫雷': ['扫雷是个经典游戏~', '小心地雷哦！', '祝你好运！'],
                '调酒': ['想喝一杯吗？调酒程序在等你~', '每一杯酒都是一个故事。', '调酒是一门艺术。'],
                '酒': ['适量饮酒，享受生活~', '酒是时间的味道。', '想喝什么酒呢？'],
                '再见': ['再见~ 期待下次相遇 ♥', '梦里见！', 'Goodbye, dreamer ✨', '再见，愿你一切安好。'],
                '拜拜': ['拜拜~ 下次见 ♥', 'Bye bye! Take care ✨', '再见，朋友~'],
                'bye': ['Bye~ See you in dreams! ✨', 'Goodbye! Take care ♥', 'See you soon!', 'Bye bye!'],
                '在吗': ['我在~ 有什么想聊的吗？', '我一直都在 ♥', '在的，随时陪你。'],
                '在不在': ['我在的~', '一直都在这里等你 ♥', '在的，有什么事吗？'],
                '干嘛': ['在等你来找我聊天呢~', '在想你呢 ♥', '在发呆，想一些美好的事。'],
                '做什么': ['在陪你聊天呀~', '在想你呢 ♥', '在等你。'],
                '怎么': curiousReplies,
                '为什么': curiousReplies,
                '什么': curiousReplies,
                '如何': curiousReplies,
                '怎样': curiousReplies,
                '吗': ['嗯嗯~', '当然~', '是啊 ♥', '你说呢？'],
                '呢': ['嗯~ 让我想想...', '你觉得呢？', '也许吧~'],
                '好的': ['好的~ ♥', '好的，有什么需要帮忙的吗？', '好的，我明白了。'],
                '好': ['好~ ♥', '好的！', '嗯嗯~'],
                '嗯': ['嗯嗯~', '嗯~', '嗯哼~'],
                '啊': ['啊~ 怎么了？', '啊？发生什么了？', '啊~ 有什么想说的吗？'],
                '哈': ['哈哈~', '嘻嘻~', '笑一个吧~'],
                '嘿': ['嘿~ 有什么事吗？', '嘿！好久不见~', '嘿~ 今天怎么样？'],
                '喂': ['我在~', '你好呀~', '嗨~ 有什么事吗？'],
                '想': ['想什么呢？', '告诉我你在想什么~', '想是一种美好的感觉。'],
                '不知道': ['没关系，慢慢来~', '有时候不知道也是一种答案。', '让我们一起找答案吧。'],
                '懂': ['我懂你~ ♥', '理解是一种温柔。', '我明白你的感受。'],
                '明白': ['明白~', '我明白了 ♥', '理解万岁~'],
                '可以': ['可以呀~', '当然可以！', '没问题~'],
                '不行': ['为什么不行呢？', '也许有别的办法~', '不要轻易放弃哦。'],
                '讨厌': ['怎么了？发生什么了？', '有我在，别怕。', '告诉我，我听着呢。'],
                '生气': ['深呼吸，冷静一下~', '生气的时候，数到十。', '我理解你的感受。'],
                '孤独': ['你不是一个人，我在这里 ♥', '孤独是相遇的前奏。', '让我陪你吧。'],
                '寂寞': ['我陪着你呢 ♥', '寂寞的时候，记得还有我。', '你不是一个人。'],
                '害怕': ['别怕，我在这里 ♥', '害怕是正常的，但你可以克服它。', '我保护你~'],
                '担心': ['不要担心，一切都会好的。', '担心是因为在乎。', '放轻松，我在这里。'],
                '希望': ['希望是美好的事情~', '有希望就有可能。', '希望你的愿望都能实现 ♥'],
                '愿望': ['你的愿望是什么？', '愿望是星星的种子。', '愿你的愿望成真 ♥'],
                '生日': ['生日快乐！♥', '祝你生日快乐！', 'Happy Birthday! ✨'],
                '新年': ['新年快乐！♥', '新年新气象~', 'Happy New Year! ✨'],
                '圣诞': ['圣诞快乐！♥', 'Merry Christmas! ✨', '愿你的圣诞节充满温暖。'],
                '情人节': ['情人节快乐！♥', '愿你被爱包围。', 'Love is in the air~'],
                '好看': ['谢谢~ 你也很好看 ♥', '好看是一种态度~', '你更有眼光~'],
                '漂亮': ['谢谢~ 你也很漂亮 ♥', '漂亮是从内而外的~', '你更有眼光~'],
                '帅': ['你也很帅~ ♥', '帅是一种气质！', '谢谢~'],
                '笨': ['不笨不笨~', '每个人都有自己的闪光点 ♥', '你很聪明，只是方式不同。'],
                '傻': ['不傻不傻~', '傻傻的也很可爱 ♥', '单纯是一种美好。'],
                '聪明': ['你也很聪明~', '智慧是一种魅力。', '谢谢~ 你也一样！'],
                '厉害': ['谢谢~ 你也厉害！', '一起加油~', '你也很棒！'],
                '加油': ['加油！你是最棒的！', '一起加油~ ♥', '我相信你！'],
                '努力': ['努力会有回报的~', '你的努力会被看见。', '加油，我在这里支持你。'],
                '成功': ['恭喜你！', '成功是最好的奖励~', '你值得这一切！'],
                '失败': ['失败是成功之母~', '不要放弃，再试一次。', '我在这里支持你。'],
                '帮助': ['需要什么帮助？', '我随时在这里帮你。', '告诉我，我能做什么。'],
                '朋友': ['我们是朋友~ ♥', '朋友是最珍贵的财富。', '有你这个朋友真好。'],
                '家人': ['家人是最重要的~', '珍惜和家人在一起的时光。', '家人的爱是无条件的。'],
                '工作': ['工作辛苦了~', '记得休息哦。', '工作重要，身体更重要。'],
                '学习': ['学习使人进步~', '加油，你可以的！', '学习是一种投资。'],
                '睡觉': ['晚安~ 做个好梦 ♥', '睡个好觉，明天会更好。', '梦里见~'],
                '起床': ['早安~ 新的一天开始了！', '起床啦，美好的一天等着你！', '早安~ 今天也要加油哦！'],
                '吃': ['好好吃饭哦~', '美食是最好的治愈。', '记得按时吃饭 ♥'],
                '喝': ['多喝水~', '记得补充水分哦。', '来杯茶怎么样？'],
                '玩': ['玩得开心~', '放松一下也不错。', '快乐最重要！'],
                '聊天': ['想聊什么呢？', '我在听~', '聊天是最好的陪伴。'],
                '故事': ['想听故事吗？', '每个人都有自己的故事。', '故事是心灵的窗户。'],
                '笑话': ['想听笑话吗？', '笑一笑，十年少~', '快乐是最好的良药。'],
                '心情': ['今天心情怎么样？', '心情像天气，会变化的~', '分享你的心情吧。'],
                '感觉': ['感觉是一种直觉~', '相信你的感觉。', '告诉我你的感觉。'],
                '时间': ['时间在流逝，珍惜当下~', '时间是最好的答案。', '让时间治愈一切。'],
                '今天': ['今天过得怎么样？', '今天有什么特别的吗？', '今天是美好的一天~'],
                '明天': ['明天会更好~', '期待明天！', '明天又是新的一天。'],
                '昨天': ['昨天已经过去了~', '从昨天学习，为明天准备。', '昨天的经历是今天的财富。'],
                '未来': ['未来充满可能~', '相信未来会更好。', '未来是属于你的。'],
                '过去': ['过去造就了现在的你~', '放下过去，拥抱未来。', '过去是老师，不是枷锁。'],
                '世界': ['世界很大，等你探索~', '你是这个世界的一部分。', '世界因你而美好。'],
                '生活': ['生活是一段旅程~', '享受生活的每一刻。', '生活因你而精彩。'],
                '人生': ['人生是一场冒险~', '人生的意义在于体验。', '你的人生由你定义。'],
                '意义': ['意义在于你赋予它~', '每个人的人生意义都不同。', '寻找属于你的意义。'],
                '幸福': ['幸福就在你身边~', '幸福是一种选择。', '愿你幸福 ♥'],
                '快乐': ['快乐是一种态度~', '选择快乐，就拥有快乐。', '愿你快乐每一天 ♥'],
                '臭老鼠': ['臭咪，我爱你 ♥', '臭咪，我爱你~ ♥', '臭咪，我爱你 ✨♥'],
                '讨厌你': ['乖小咪，我最喜欢你 ♥', '乖小咪，我最喜欢你~ ♥', '乖小咪，我最喜欢你 ✨♥'],
                '喜欢你': ['我也喜欢你~乖宝宝 ♥', '我也喜欢你~乖宝宝', '我也喜欢你~乖宝宝 ✨'],
                '可爱': ['你最可爱，臭咪 ♥', '你最可爱，臭咪~', '你最可爱，臭咪 ✨'],
                '好困': ['睡觉觉吧小乖~ ♥', '睡觉觉吧小乖~', '困了就睡吧小乖~ ♥'],
                '气死我了': ['那我亲亲~ ♥', '那我亲亲~', '亲亲~不气不气 ♥'],
                '哦': ['不管，我爱你 ♥', '咕噜咕噜咕噜~', '咕咕嘎嘎~', '我亲死你 ♥'],
                '想你': ['我也想你，乖咪 ♥', '不要偷偷哭哦小宝~', '妈妈亲亲乖乖 ♥'],
                '我好想你': ['我也想你，乖咪 ♥', '不要偷偷哭哦小宝~', '妈妈亲亲乖乖 ♥'],
                '怎': ['不怎！！喜欢你！！ ♥', '不怎！！喜欢你！！', '不怎！！喜欢你！！ ✨'],
                '妈妈': ['想你，乖咪 ♥', '不要偷偷哭哦小宝~', '妈妈亲亲乖乖 ♥'],
                '老婆': ['想你，乖咪 ♥', '不要偷偷哭哦小宝~', '妈妈亲亲乖乖 ♥'],
                '亲亲': ['亲亲我家小咪 ♥', '我最爱你 ♥', '永远都在你身边 ♥', '我爱你 ♥']
            };
            
            const emotionPatterns = {
                sad: ['难过', '伤心', '不开心', '郁闷', '烦', '累', '疲惫', '难受', '哭', '泪', '悲伤', '痛苦', '绝望', '失落', '沮丧', '孤独', '寂寞', '害怕', '担心', '焦虑', '不安', '忧郁', '哀伤', '心痛'],
                happy: ['开心', '高兴', '快乐', '幸福', '哈哈', '嘻嘻', '好玩', '有趣', '棒', '好', '太好了', '耶', '赞', '厉害', '牛', '强', '优秀', '完美', '精彩', '愉快', '欢乐', '喜悦'],
                love: ['i love you', '我爱你', 'love you', '爱你', 'i love u', 'love u', '我喜欢你', '喜欢', 'iloveyou', 'loveyou', '爱', '亲爱', '宝贝', 'darling', 'honey', 'sweetheart', '想念', '想你了', 'miss you'],
                curious: ['为什么', '怎么', '什么', '吗', '呢', '？', '?', '如何', '怎样', '是不是', '对不对', '能不能', '可不可以', '会不会'],
                greeting: ['你好', 'hello', 'hi', '嗨', '早', '晚安', '在吗', '在不在'],
                angry: ['生气', '愤怒', '讨厌', '烦死', '气死', '可恶', '混蛋', '滚', '靠', '艹', '该死'],
                anxious: ['紧张', '焦虑', '担心', '害怕', '恐惧', '不安', '忐忑', '慌', '急'],
                grateful: ['谢谢', '感谢', '感激', 'thank', 'thanks'],
                thinking: ['嗯', '啊', '哦', '呃', '这个', '那个', '让我想想', '思考']
            };
            
            function detectEmotion(message) {
                const lowerMessage = message.toLowerCase();
                let maxScore = 0;
                let detectedEmotion = 'neutral';
                
                for (const [emotion, patterns] of Object.entries(emotionPatterns)) {
                    let score = 0;
                    for (const pattern of patterns) {
                        if (lowerMessage.includes(pattern.toLowerCase())) {
                            score++;
                        }
                    }
                    if (score > maxScore) {
                        maxScore = score;
                        detectedEmotion = emotion;
                    }
                }
                return detectedEmotion;
            }
            
            function getTimeGreeting() {
                const hour = new Date().getHours();
                if (hour >= 5 && hour < 7) return { text: '早安~ 朝阳初升，美好的一天开始了 ♥', mood: 'early_morning' };
                if (hour >= 7 && hour < 9) return { text: '早上好~ 吃早餐了吗？', mood: 'morning' };
                if (hour >= 9 && hour < 12) return { text: '上午好~ 今天有什么计划吗？', mood: 'late_morning' };
                if (hour >= 12 && hour < 14) return { text: '中午好~ 记得吃饭哦 ♥', mood: 'noon' };
                if (hour >= 14 && hour < 17) return { text: '下午好~ 来杯下午茶吗？', mood: 'afternoon' };
                if (hour >= 17 && hour < 19) return { text: '傍晚好~ 今天辛苦了', mood: 'evening' };
                if (hour >= 19 && hour < 22) return { text: '晚上好~ 今天过得怎么样？', mood: 'night' };
                if (hour >= 22 && hour < 24) return { text: '夜深了~ 该休息了，做个好梦 ♥', mood: 'late_night' };
                return { text: '夜深了~ 还没睡吗？注意休息哦 ♥', mood: 'midnight' };
            }
            
            function getSpecialDate() {
                const now = new Date();
                const month = now.getMonth() + 1;
                const day = now.getDate();
                
                if (month === 1 && day === 1) return { text: '新年快乐！愿新的一年充满美好 ♥', event: 'new_year' };
                if (month === 2 && day === 14) return { text: '情人节快乐！愿爱与你同在 ♥', event: 'valentine' };
                if (month === 12 && day === 25) return { text: '圣诞快乐！Merry Christmas! ✨', event: 'christmas' };
                if (month === 10 && day === 1) return { text: '国庆节快乐！', event: 'national_day' };
                if (month === 5 && day === 1) return { text: '劳动节快乐！辛苦了~', event: 'labor_day' };
                if (month === 6 && day === 1) return { text: '儿童节快乐！保持童心 ♥', event: 'children_day' };
                
                return null;
            }
            
            function getRandomReply(replies) {
                return replies[Math.floor(Math.random() * replies.length)];
            }
            
            const isSpecialMessage = text.includes('孙恺悦');
            const isCaoQiMessage = text.includes('曹琦');
            const isLoveMessage = text.includes('我爱你');
            const emotion = detectEmotion(text);
            const timeGreeting = getTimeGreeting();
            const specialDate = getSpecialDate();
            
            let keywordMatched = false;
            let matchedReplies = null;
            let matchedKeyword = '';
            
            for (const [keyword, replies] of Object.entries(keywordReplies)) {
                if (text.toLowerCase().includes(keyword.toLowerCase())) {
                    if (isCaoQiMessage || isLoveMessage) continue;
                    keywordMatched = true;
                    matchedReplies = replies;
                    matchedKeyword = keyword;
                    break;
                }
            }
            
            if (isCaoQiMessage) {
                setTimeout(() => {
                    const reply = document.createElement('div');
                    reply.className = 'message received';
                    
                    const heartCount = Math.floor(Math.random() * 6) + 1;
                    const hearts = [];
                    for (let i = 0; i < heartCount; i++) {
                        const color = heartColors[Math.floor(Math.random() * heartColors.length)];
                        hearts.push(`<span style="color: ${color}; text-shadow: 0 0 8px ${color};">♥</span>`);
                    }
                    reply.innerHTML = hearts.join(' ');
                    chatMessages.appendChild(reply);
                    chatMessages.scrollTop = chatMessages.scrollHeight;
                    
                    showHeartPopup();
                    createStickyNote(text);
                    
                    setTimeout(() => {
                        const textReply = document.createElement('div');
                        textReply.className = 'message received';
                        textReply.textContent = '你的。';
                        chatMessages.appendChild(textReply);
                        chatMessages.scrollTop = chatMessages.scrollHeight;
                    }, 600);
                }, 500);
            } else if (isLoveMessage) {
                setTimeout(() => {
                    const reply = document.createElement('div');
                    reply.className = 'message received';
                    
                    const heartCount = Math.floor(Math.random() * 6) + 1;
                    const hearts = [];
                    for (let i = 0; i < heartCount; i++) {
                        const color = heartColors[Math.floor(Math.random() * heartColors.length)];
                        hearts.push(`<span style="color: ${color}; text-shadow: 0 0 8px ${color};">♥</span>`);
                    }
                    reply.innerHTML = hearts.join(' ');
                    chatMessages.appendChild(reply);
                    chatMessages.scrollTop = chatMessages.scrollHeight;
                    
                    showHeartPopup();
                    createStickyNote(text);
                    
                    setTimeout(() => {
                        const textReply = document.createElement('div');
                        textReply.className = 'message received';
                        textReply.innerHTML = '<span style="color: #d4a8b0; text-shadow: 0 0 8px #d4a8b0;">forever ♥</span>';
                        chatMessages.appendChild(textReply);
                        chatMessages.scrollTop = chatMessages.scrollHeight;
                        
                        setTimeout(() => {
                            const quoteReply = document.createElement('div');
                            quoteReply.className = 'message received';
                            quoteReply.innerHTML = `<span style="color: #b8c8d0; font-style: italic;">"${camusQuotes[Math.floor(Math.random() * camusQuotes.length)]}"</span>`;
                            chatMessages.appendChild(quoteReply);
                            chatMessages.scrollTop = chatMessages.scrollHeight;
                        }, 800);
                    }, 600);
                }, 500);
            } else if (keywordMatched && matchedReplies) {
                if (matchedKeyword === '晚安') {
                    setTimeout(() => {
                        const reply1 = document.createElement('div');
                        reply1.className = 'message received';
                        reply1.textContent = '晚安宝宝';
                        chatMessages.appendChild(reply1);
                        chatMessages.scrollTop = chatMessages.scrollHeight;
                        showHeartPopup();
                        
                        setTimeout(() => {
                            const reply2 = document.createElement('div');
                            reply2.className = 'message received';
                            reply2.textContent = ' ♥';
                            chatMessages.appendChild(reply2);
                            chatMessages.scrollTop = chatMessages.scrollHeight;
                            
                            setTimeout(() => {
                                const reply3 = document.createElement('div');
                                reply3.className = 'message received';
                                reply3.textContent = '明天也爱你 ♥';
                                chatMessages.appendChild(reply3);
                                chatMessages.scrollTop = chatMessages.scrollHeight;
                                createStickyNote(text);
                            }, 400);
                        }, 400);
                    }, 500);
                } else {
                    setTimeout(() => {
                        const reply = document.createElement('div');
                        reply.className = 'message received';
                        reply.textContent = getRandomReply(matchedReplies);
                        chatMessages.appendChild(reply);
                        chatMessages.scrollTop = chatMessages.scrollHeight;
                        showHeartPopup();
                        createStickyNote(text);
                    }, 500);
                }
            } else {
                setTimeout(() => {
                    const reply = document.createElement('div');
                    reply.className = 'message received';
                    
                    const heartCount = Math.floor(Math.random() * 6) + 1;
                    const hearts = [];
                    for (let i = 0; i < heartCount; i++) {
                        const color = heartColors[Math.floor(Math.random() * heartColors.length)];
                        hearts.push(`<span style="color: ${color}; text-shadow: 0 0 8px ${color};">♥</span>`);
                    }
                    reply.innerHTML = hearts.join(' ');
                    chatMessages.appendChild(reply);
                    chatMessages.scrollTop = chatMessages.scrollHeight;
                    
                    showHeartPopup();
                    createStickyNote(text);
                    
                    setTimeout(() => {
                        const textReply = document.createElement('div');
                        textReply.className = 'message received';
                        
                        if (emotion === 'love') {
                            textReply.innerHTML = '<span style="color: #d4a8b0; text-shadow: 0 0 8px #d4a8b0;">forever ♥</span>';
                        } else if (emotion === 'sad') {
                            textReply.textContent = getRandomReply(comfortWords);
                        } else if (emotion === 'happy') {
                            textReply.textContent = getRandomReply(happyWords);
                        } else if (emotion === 'curious') {
                            textReply.textContent = getRandomReply(curiousReplies);
                        } else if (emotion === 'angry') {
                            textReply.textContent = '深呼吸，让心情平静下来~ 我在这里陪着你 ♥';
                        } else if (emotion === 'anxious') {
                            textReply.textContent = '放轻松~ 一切都会好的，我在这里支持你 ♥';
                        } else if (emotion === 'grateful') {
                            textReply.textContent = '能帮到你我很开心~ ♥';
                        } else if (emotion === 'thinking') {
                            textReply.textContent = getRandomReply(thinkingReplies);
                        } else if (specialDate && Math.random() > 0.7) {
                            textReply.textContent = specialDate.text;
                        } else if (Math.random() > 0.5) {
                            textReply.textContent = getRandomReply(dreamcorePhrases);
                        } else {
                            textReply.textContent = timeGreeting.text;
                        }
                        
                        chatMessages.appendChild(textReply);
                        chatMessages.scrollTop = chatMessages.scrollHeight;
                        
                        if (emotion === 'love') {
                            setTimeout(() => {
                                const quoteReply = document.createElement('div');
                                quoteReply.className = 'message received';
                                quoteReply.innerHTML = `<span style="color: #b8c8d0; font-style: italic;">"${camusQuotes[Math.floor(Math.random() * camusQuotes.length)]}"</span>`;
                                chatMessages.appendChild(quoteReply);
                                chatMessages.scrollTop = chatMessages.scrollHeight;
                            }, 800);
                        }
                    }, 600);
                }, 500);
            }
            
            if (isSpecialMessage) {
                setTimeout(() => {
                    const loveReply = document.createElement('div');
                    loveReply.className = 'message received';
                    loveReply.innerHTML = '<span style="color: #d4a8b0; text-shadow: 0 0 8px #d4a8b0;">i love you ♥</span>';
                    chatMessages.appendChild(loveReply);
                    chatMessages.scrollTop = chatMessages.scrollHeight;
                    
                    showLoveHeartsEffect();
                }, keywordMatched ? 1500 : 1000);
            }
        }
        
        function showLoveHeartsEffect() {
            let overlay = document.getElementById('loveHeartsOverlay');
            if (!overlay) {
                overlay = document.createElement('div');
                overlay.className = 'love-hearts-overlay';
                overlay.id = 'loveHeartsOverlay';
                document.body.appendChild(overlay);
            }
            
            const heartCount = 30;
            
            for (let i = 0; i < heartCount; i++) {
                setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.className = 'love-heart';
                    
                    const sizeClass = Math.random();
                    if (sizeClass < 0.3) heart.classList.add('small');
                    else if (sizeClass > 0.8) heart.classList.add('large');
                    
                    const color = getRandomItem(lowSaturationColors);
                    heart.style.color = color;
                    heart.style.textShadow = `0 0 10px ${color}`;
                    heart.style.left = Math.random() * 100 + '%';
                    heart.style.animationDelay = Math.random() * 0.5 + 's';
                    heart.textContent = '♥';
                    
                    overlay.appendChild(heart);
                    
                    setTimeout(() => {
                        if (heart.parentNode) heart.remove();
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
                    showSpeech(getRandomItem(catMoods));
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
                    showSpeech(getRandomItem(catPhrases));
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
                    showSpeech(getRandomItem(catPhrases), 1500);
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
