<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KrisCOIN</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=M+PLUS+Rounded+1c:wght@400;500;700&display=swap&subset=cyrillic">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        body {
            margin: 0;
            font-family: 'M PLUS Rounded 1c', sans-serif;
            background: #121212;
            color: #e0e0e0;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
            overflow: hidden;
        }

        .header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100px;
            background: rgba(18, 18, 18, 0.8);
            backdrop-filter: blur(10px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 10;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.6);
            padding: 0 10px;
            box-sizing: border-box;
        }

        .header h1 {
            font-size: 4rem;
            color: #e0e0e0;
            background: linear-gradient(135deg, #8a2be2, #6a0dad);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin: 0;
        }

        .clicker {
            margin-top: 120px; /* Уменьшено для меньших экранов */
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            width: 100%;
            height: calc(100vh - 120px);
            position: relative;
        }

        .clicker-button {
            background: linear-gradient(135deg, #8a2be2, #6a0dad);
            border: none;
            border-radius: 50%;
            color: #e0e0e0;
            width: 150px; /* Уменьшено для мобильных устройств */
            height: 150px; /* Уменьшено для мобильных устройств */
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.8);
            cursor: pointer;
            transition: background 0.3s ease, transform 0.3s ease;
        }

        .clicker-button:hover {
            background: linear-gradient(135deg, #9b4de0, #7b3ecb);
            transform: scale(1.05);
        }

        .clicker-counter {
            position: absolute;
            right: 10px; /* Уменьшено для мобильных устройств */
            top: 10px; /* Уменьшено для мобильных устройств */
            background: rgba(18, 18, 18, 0.8);
            border-radius: 10px;
            padding: 10px 15px; /* Уменьшено для мобильных устройств */
            color: #e0e0e0;
            font-size: 1.2rem; /* Уменьшено для мобильных устройств */
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.6);
        }

        .background-shapes {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            overflow: hidden;
            z-index: 0;
            filter: blur(10px);
        }

        .circle {
            position: absolute;
            background: linear-gradient(135deg, #8a2be2, #6a0dad);
            border-radius: 50%;
            opacity: 0.3;
            animation: moveAndResize 30s infinite;
        }

        @keyframes moveAndResize {
            0% {
                transform: translate(0, 0) scale(1);
                width: 80px;
                height: 80px;
            }
            25% {
                transform: translate(50px, 20px) scale(1.2);
                width: 100px;
                height: 100px;
            }
            50% {
                transform: translate(-30px, -50px) scale(1.5);
                width: 120px;
                height: 120px;
            }
            75% {
                transform: translate(-20px, 30px) scale(1.2);
                width: 100px;
                height: 100px;
            }
            100% {
                transform: translate(0, 0) scale(1);
                width: 80px;
                height: 80px;
            }
        }

        .telegram-button {
            position: absolute;
            bottom: 20px;
            right: 20px;
            width: 50px; /* Уменьшено для мобильных устройств */
            height: 50px; /* Уменьшено для мобильных устройств */
            background: linear-gradient(135deg, #8a2be2, #6a0dad);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.8);
            cursor: pointer;
            transition: background-color 0.3s ease, transform 0.3s ease;
        }

        .telegram-button:hover {
            background: linear-gradient(135deg, #9b4de0, #7b3ecb);
            transform: scale(1.1);
        }

        .fa-telegram {
            color: white;
            font-size: 20px; /* Уменьшено для мобильных устройств */
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>KrisCOIN</h1>
    </div>

    <div class="background-shapes" id="backgroundShapes"></div>

    <div class="clicker">
        <button class="clicker-button" id="clickButton">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-star" style="width: 60%; height: 60%; color: #e0e0e0;">
                <path d="M12 2l3.09 6.26L22 9.27l-5 4.87L18.18 21 12 17.27 5.82 21 7 14.14 2 9.27l6.91-1.01L12 2z"></path>
            </svg>
        </button>
        <div class="clicker-counter" id="counter">Клики: 0</div>
    </div>

    <a href="https://t.me/kris_kovidov" target="_blank" class="telegram-button">
        <i class="fab fa-telegram"></i>
    </a>

    <script>
        let clickCount = 0;
        const clickButton = document.getElementById('clickButton');
        const counter = document.getElementById('counter');

        clickButton.addEventListener('click', () => {
            clickCount++;
            counter.textContent = `Клики: ${clickCount}`;
        });

        function getRandom(min, max) {
            return Math.floor(Math.random() * (max - min + 1)) + min;
        }

        function createCircle() {
            const circle = document.createElement('div');
            circle.className = 'circle';
            const size = getRandom(80, 200); /* Уменьшено для мобильных устройств */
            circle.style.width = `${size}px`;
            circle.style.height = `${size}px`;
            circle.style.top = `${getRandom(0, 100)}%`;
            circle.style.left = `${getRandom(0, 100)}%`;
            circle.style.transform = `rotate(${getRandom(0, 360)}deg)`;

            document.getElementById('backgroundShapes').appendChild(circle);

            circle.style.animationDuration = `${getRandom(10, 30)}s`;
        }

        for (let i = 0; i < 20; i++) {
            createCircle();
        }
    </script>
</body>
</html>
