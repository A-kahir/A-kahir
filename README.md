<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aymane Kahir Portfolio</title>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            background: #000;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            font-family: Arial, sans-serif;
            color: white;
        }
        .stars {
            position: absolute;
            width: 100%;
            height: 100%;
            z-index: 1;
            transition: transform 2s ease-out, opacity 2s ease-out;
        }
        .star {
            position: absolute;
            background: white;
            border-radius: 50%;
            animation: twinkle var(--duration) infinite;
        }
        @keyframes twinkle {
            0%, 100% { opacity: 0.2; }
            50% { opacity: 1; }
        }
        .meteor {
            position: absolute;
            width: 2px;
            height: 2px;
            background: white;
            transform: rotate(45deg);
            opacity: 0;
        }
        .meteor::before {
            content: '';
            position: absolute;
            width: 50px;
            height: 1px;
            background: linear-gradient(90deg, white, transparent);
            transform: translateX(-100%);
        }
        @keyframes meteor {
            0% {
                opacity: 1;
                transform: translate(0, 0) rotate(45deg);
            }
            100% {
                opacity: 0;
                transform: translate(var(--travel-x), var(--travel-y)) rotate(45deg);
            }
        }
        .welcome-text {
            font-size: 5rem;
            z-index: 2;
            text-align: center;
            opacity: 1;
            transition: opacity 1s ease-out;
            margin: 0;
        }
        .skip-text {
            position: absolute;
            bottom: 2rem;
            font-size: 1.2rem;
            z-index: 2;
            cursor: pointer;
            animation: blink 3s infinite;
        }
        @keyframes blink {
            0%, 100% { opacity: 0.3; }
            50% { opacity: 1; }
        }
        .zoom-out {
            transform: scale(10);
            opacity: 0;
        }
        .fade-out {
            opacity: 0;
        }
    </style>
</head>
<body>
    <div class="stars" id="starsContainer"></div>
    <h1 class="welcome-text" id="welcomeText">Welcome</h1>
    <div class="skip-text" id="skipText">Click to skip</div>
    <script>
        const starsContainer = document.getElementById('starsContainer');
        const numberOfStars = 200;
        for (let i = 0; i < numberOfStars; i++) {
            const star = document.createElement('div');
            star.className = 'star';
            const x = Math.random() * 100;
            const y = Math.random() * 100;
            const size = Math.random() * 2;
            const duration = 2 + Math.random() * 3;
            star.style.left = `${x}%`;
            star.style.top = `${y}%`;
            star.style.width = `${size}px`;
            star.style.height = `${size}px`;
            star.style.setProperty('--duration', `${duration}s`);
            starsContainer.appendChild(star);
        }
        function createMeteor() {
            const meteor = document.createElement('div');
            meteor.className = 'meteor';
            const startX = Math.random() * 100;
            const startY = Math.random() * 100;
            const travelX = 150 + Math.random() * 100;
            const travelY = 150 + Math.random() * 100;
            meteor.style.left = `${startX}%`;
            meteor.style.top = `${startY}%`;
            meteor.style.setProperty('--travel-x', `${travelX}px`);
            meteor.style.setProperty('--travel-y', `${travelY}px`);
            const duration = 1 + Math.random() * 5;
            meteor.style.animation = `meteor ${duration}s linear forwards`;
            starsContainer.appendChild(meteor);
            setTimeout(() => {
                meteor.remove();
            }, duration * 1000);
        }
        setInterval(createMeteor, 4000);
        const welcomeText = document.getElementById('welcomeText');
        const skipText = document.getElementById('skipText');
        const greetings = [
            { text: 'Bonjour', lang: 'fr' },
            { text: 'Hello', lang: 'en' },
            { text: 'مرحباً', lang: 'ar' }
        ];
        let currentGreetingIndex = 0;
        function changeGreeting() {
            welcomeText.classList.add('fade-out');
            setTimeout(() => {
                welcomeText.textContent = greetings[currentGreetingIndex].text;
                welcomeText.lang = greetings[currentGreetingIndex].lang;
                welcomeText.classList.remove('fade-out');
                currentGreetingIndex = (currentGreetingIndex + 1) % greetings.length;
            }, 1000);
        }
        setTimeout(() => {
            setInterval(changeGreeting, 4000);
        }, 4000);
        skipText.addEventListener('click', () => {
            clearInterval(changeGreeting);
            starsContainer.classList.add('zoom-out');
            welcomeText.classList.add('fade-out');
            skipText.classList.add('fade-out');
        });
    </script>
</body>
</html>
