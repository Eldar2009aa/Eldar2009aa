<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Счетчик полезных дел</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1a2a6c, #2c3e50, #4a6491);
            color: #fff;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            overflow-x: hidden;
            position: relative;
        }
        
        body::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, rgba(255,255,255,0.05) 0%, rgba(0,0,0,0.2) 100%);
            z-index: -1;
        }
        
        .counter-container {
            text-align: center;
            padding: 2rem;
            background: rgba(255, 255, 255, 0.12);
            border-radius: 24px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.35);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.18);
            max-width: 90%;
            width: 450px;
            animation: pulse 2s infinite;
            position: relative;
            z-index: 10;
        }
        
        @keyframes pulse {
            0% { box-shadow: 0 0 20px rgba(76, 175, 80, 0.4); }
            50% { box-shadow: 0 0 35px rgba(76, 175, 80, 0.7); }
            100% { box-shadow: 0 0 20px rgba(76, 175, 80, 0.4); }
        }
        
        .counter-title {
            font-size: 2.2rem;
            margin-bottom: 1.5rem;
            color: #e3f2fd;
            text-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
            letter-spacing: 1px;
            font-weight: 300;
        }
        
        .counter-number {
            font-size: 8.5rem;
            font-weight: 800;
            color: #ffffff;
            text-shadow: 0 0 20px rgba(255, 255, 255, 0.7),
                         0 0 40px rgba(76, 175, 80, 0.8),
                         0 0 60px rgba(76, 175, 80, 0.6);
            line-height: 1;
            background: linear-gradient(to bottom, #ffffff, #a5d6a7);
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            transition: all 0.3s ease;
        }
        
        .counter-number:hover {
            transform: scale(1.03);
            text-shadow: 0 0 25px rgba(255, 255, 255, 0.8),
                         0 0 50px rgba(76, 175, 80, 0.9),
                         0 0 70px rgba(76, 175, 80, 0.7);
        }
        
        .counter-label {
            font-size: 1.8rem;
            margin-top: 0.5rem;
            color: #c8e6c9;
            font-weight: 300;
        }
        
        .add-button {
            position: fixed;
            bottom: 35px;
            left: 50%;
            transform: translateX(-50%);
            background: linear-gradient(to right, #43a047, #2e7d32);
            color: white;
            border: none;
            border-radius: 60px;
            padding: 18px 65px;
            font-size: 1.6rem;
            font-weight: 600;
            cursor: pointer;
            box-shadow: 0 6px 25px rgba(0, 0, 0, 0.4),
                        0 0 30px rgba(67, 160, 71, 0.6);
            transition: all 0.3s ease;
            z-index: 20;
            letter-spacing: 1px;
            text-transform: uppercase;
            position: relative;
            overflow: hidden;
        }
        
        .add-button::before {
            content: "";
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(to right, transparent, rgba(255,255,255,0.2), transparent);
            transition: left 0.7s;
        }
        
        .add-button:hover {
            transform: translateX(-50%) scale(1.05);
            box-shadow: 0 8px 30px rgba(0, 0, 0, 0.5),
                        0 0 40px rgba(67, 160, 71, 0.8);
            background: linear-gradient(to right, #4caf50, #388e3c);
        }
        
        .add-button:hover::before {
            left: 100%;
        }
        
        .add-button:active {
            transform: translateX(-50%) scale(0.98);
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.4);
        }
        
        .confetti {
            position: absolute;
            width: 15px;
            height: 15px;
            background-color: #f00;
            border-radius: 50%;
            animation: fall 5s ease-in-out forwards;
            z-index: 5;
        }
        
        @keyframes fall {
            to {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }
        
        .stats-container {
            position: fixed;
            top: 25px;
            right: 30px;
            background: rgba(0, 30, 60, 0.85);
            border-radius: 16px;
            padding: 12px 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
            font-size: 1.1rem;
            z-index: 15;
            border: 1px solid rgba(255, 255, 255, 0.15);
        }
        
        .stats-title {
            font-size: 0.9rem;
            color: #a5d6a7;
            margin-bottom: 3px;
        }
        
        .stats-value {
            font-weight: bold;
            color: #ffffff;
            font-size: 1.3rem;
        }
        
        @media (max-width: 480px) {
            .counter-number {
                font-size: 6.5rem;
            }
            
            .counter-title {
                font-size: 1.8rem;
            }
            
            .counter-label {
                font-size: 1.5rem;
            }
            
            .add-button {
                padding: 16px 45px;
                font-size: 1.4rem;
                bottom: 25px;
            }
            
            .stats-container {
                top: 15px;
                right: 15px;
                padding: 8px 15px;
                font-size: 0.95rem;
            }
        }
    </style>
</head>
<body>
    <div class="counter-container">
        <div class="counter-title">Полезных дел сделано</div>
        <div class="counter-number" id="counter">0</div>
        <div class="counter-label">Отличный результат!</div>
    </div>
    
    <button class="add-button" id="add-button">Добавить дело</button>
    
    <div class="stats-container">
        <div class="stats-title">Сегодня:</div>
        <div class="stats-value" id="today-count">0</div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const counterElement = document.getElementById('counter');
            const todayCounterElement = document.getElementById('today-count');
            const addButton = document.getElementById('add-button');
            
            // Получаем текущую дату для статистики "сегодня"
            const today = new Date().toDateString();
            
            // Инициализация счетчиков
            let totalCount = parseInt(localStorage.getItem('totalCount')) || 0;
            let todayCount = parseInt(localStorage.getItem('todayCount')) || 0;
            let lastCountDate = localStorage.getItem('lastCountDate') || '';
            
            // Сбрасываем счетчик "сегодня" если новый день
            if (lastCountDate !== today) {
                todayCount = 0;
                localStorage.setItem('todayCount', '0');
                localStorage.setItem('lastCountDate', today);
            }
            
            // Обновляем отображение
            counterElement.textContent = totalCount;
            todayCounterElement.textContent = todayCount;
            
            // Функция создания конфетти
            function createConfetti() {
                const colors = ['#FF416C', '#FF4B2B', '#FFD32A', '#38EF7D', '#11998E', '#3498db', '#9b59b6'];
                const confettiCount = 40;
                
                for (let i = 0; i < confettiCount; i++) {
                    const confetti = document.createElement('div');
                    confetti.classList.add('confetti');
                    
                    // Случайное положение вокруг кнопки
                    const buttonRect = addButton.getBoundingClientRect();
                    const x = buttonRect.left + Math.random() * buttonRect.width;
                    const y = buttonRect.top + Math.random() * buttonRect.height;
                    
                    confetti.style.left = `${x}px`;
                    confetti.style.top = `${y}px`;
                    
                    // Случайные цвета и размеры
                    const size = Math.random() * 10 + 8;
                    confetti.style.width = `${size}px`;
                    confetti.style.height = `${size}px`;
                    confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                    
                    // Случайная траектория
                    confetti.style.animationDuration = `${Math.random() * 3 + 2}s`;
                    confetti.style.animationDelay = `${Math.random() * 0.5}s`;
                    confetti.style.transform = `rotate(${Math.random() * 360}deg)`;
                    
                    document.body.appendChild(confetti);
                    
                    // Удаляем конфетти после анимации
                    setTimeout(() => {
                        confetti.remove();
                    }, 5000);
                }
            }
            
            // Обработчик нажатия кнопки
            addButton.addEventListener('click', () => {
                // Увеличиваем счетчики
                totalCount++;
                todayCount++;
                
                // Обновляем отображение с анимацией
                counterElement.textContent = totalCount;
                todayCounterElement.textContent = todayCount;
                
                // Сохраняем в localStorage
                localStorage.setItem('totalCount', totalCount.toString());
                localStorage.setItem('todayCount', todayCount.toString());
                localStorage.setItem('lastCountDate', today);
                
                // Визуальные эффекты
                createConfetti();
                
                // Анимация счетчика
                counterElement.style.transform = 'scale(1.2)';
                setTimeout(() => {
                    counterElement.style.transform = 'scale(1)';
                }, 300);
                
                // Вибрация кнопки (для поддерживаемых устройств)
                if (navigator.vibrate) {
                    navigator.vibrate(50);
                }
            });
            
            // Анимация появления при загрузке
            setTimeout(() => {
                document.querySelector('.counter-container').style.opacity = '1';
                document.querySelector('.counter-container').style.transform = 'scale(1)';
            }, 300);
        });
    </script>
</body>
</html>
