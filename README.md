# new-year-card-<!DOCTYPE html>
<html lang="hy">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Շնորհավոր Ամանոր Նարեկից</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            background: linear-gradient(135deg, #0a2e5c 0%, #1a1a2e 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
        }
        
        .card {
            width: 100%;
            max-width: 800px;
            height: 600px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            position: relative;
            overflow: hidden;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 30px;
        }
        
        .fireworks {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            z-index: 1;
        }
        
        .firework {
            position: absolute;
            width: 5px;
            height: 5px;
            border-radius: 50%;
            opacity: 0;
        }
        
        .message {
            position: relative;
            z-index: 2;
            opacity: 0;
            transform: translateY(30px);
            transition: all 1.5s ease-out;
        }
        
        .message.visible {
            opacity: 1;
            transform: translateY(0);
        }
        
        .main-title {
            font-size: 3.5em;
            color: #ffd700;
            text-shadow: 0 0 15px rgba(255, 215, 0, 0.7);
            margin-bottom: 30px;
            line-height: 1.2;
        }
        
        .wishes {
            font-size: 1.8em;
            color: #ffffff;
            line-height: 1.6;
            margin-bottom: 30px;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
        }
        
        .signature {
            font-size: 1.5em;
            color: #ff6b6b;
            margin-top: 20px;
            text-shadow: 0 0 10px rgba(255, 107, 107, 0.7);
        }
        
        .new-year-icon {
            font-size: 1.8em;
            margin: 0 10px;
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        
        .snow {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            pointer-events: none;
            z-index: 1;
        }
        
        .snowflake {
            position: absolute;
            background: white;
            border-radius: 50%;
            opacity: 0.8;
        }
        
        @media (max-width: 768px) {
            .card {
                height: 100vh;
                border-radius: 0;
                max-width: 100%;
            }
            
            .main-title {
                font-size: 2.5em;
            }
            
            .wishes {
                font-size: 1.4em;
            }
        }
    </style>
</head>
<body>
    <div class="card">
        <div class="fireworks" id="fireworks"></div>
        <div class="snow" id="snow"></div>
        
        <div class="message" id="message">
            <h1 class="main-title">
                <span class="new-year-icon">🎆</span>
                ՇՆՈՐՀԱՎՈՐ ՆՈՐ ՏԱՐԻ
                <span class="new-year-icon">🎆</span>
            </h1>
            
            <div class="wishes">
                <p>Թող գալիք տարին լցված լինի լույսով, ուրախությամբ և հաջողություններով։</p>
                <p>Թող ձեր սրտերը լցվեն ջերմությամբ,<br>
                տները՝ սիրով ու ուրախությամբ,<br>
                իսկ ճանապարհները՝ հաջողություններով։</p>
            </div>
            
            <div class="signature">
                ✨ Սիրով՝ Նարեկ ✨
            </div>
        </div>
    </div>

    <script>
        function createFireworks() {
            const fireworksContainer = document.getElementById('fireworks');
            const colors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff', '#00ffff', '#ffa500', '#ffffff'];
            
            for (let i = 0; i < 150; i++) {
                setTimeout(() => {
                    const firework = document.createElement('div');
                    firework.className = 'firework';
                    
                    const color = colors[Math.floor(Math.random() * colors.length)];
                    firework.style.backgroundColor = color;
                    firework.style.boxShadow = `0 0 10px ${color}, 0 0 20px ${color}`;
                    
                    const x = Math.random() * 100;
                    const y = Math.random() * 100;
                    firework.style.left = `${x}%`;
                    firework.style.top = `${y}%`;
                    
                    const animationDuration = 1 + Math.random() * 2;
                    firework.style.animation = `fireworkAnimation ${animationDuration}s forwards`;
                    
                    const style = document.createElement('style');
                    style.textContent = `
                        @keyframes fireworkAnimation {
                            0% {
                                transform: translate(0, 0) scale(0);
                                opacity: 1;
                            }
                            50% {
                                opacity: 1;
                            }
                            100% {
                                transform: translate(${Math.random() * 200 - 100}px, ${Math.random() * 200 - 100}px) scale(1);
                                opacity: 0;
                            }
                        }
                    `;
                    document.head.appendChild(style);
                    
                    fireworksContainer.appendChild(firework);
                    
                    setTimeout(() => {
                        firework.remove();
                        style.remove();
                    }, animationDuration * 1000);
                    
                }, i * 50);
            }
            
            setTimeout(() => {
                document.getElementById('message').classList.add('visible');
                setInterval(() => {
                    if (Math.random() > 0.7) {
                        createSingleFirework();
                    }
                }, 1000);
            }, 3000);
        }
        
        function createSingleFirework() {
            const fireworksContainer = document.getElementById('fireworks');
            const colors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff', '#00ffff'];
            
            const firework = document.createElement('div');
            firework.className = 'firework';
            
            const color = colors[Math.floor(Math.random() * colors.length)];
            firework.style.backgroundColor = color;
            firework.style.boxShadow = `0 0 5px ${color}, 0 0 10px ${color}`;
            
            const x = Math.random() * 100;
            const y = Math.random() * 100;
            firework.style.left = `${x}%`;
            firework.style.top = `${y}%`;
            
            const animationDuration = 0.5 + Math.random();
            firework.style.animation = `singleFireworkAnimation ${animationDuration}s forwards`;
            
            const style = document.createElement('style');
            style.textContent = `
                @keyframes singleFireworkAnimation {
                    0% {
                        transform: scale(0);
                        opacity: 1;
                    }
                    100% {
                        transform: scale(1);
                        opacity: 0;
                    }
                }
            `;
            document.head.appendChild(style);
            
            fireworksContainer.appendChild(firework);
            
            setTimeout(() => {
                firework.remove();
                style.remove();
            }, animationDuration * 1000);
        }
        
        function createSnow() {
            const snowContainer = document.getElementById('snow');
            
            for (let i = 0; i < 100; i++) {
                const snowflake = document.createElement('div');
                snowflake.className = 'snowflake';
                
                const size = Math.random() * 5 + 2;
                snowflake.style.width = `${size}px`;
                snowflake.style.height = `${size}px`;
                
                snowflake.style.left = `${Math.random() * 100}%`;
                snowflake.style.top = `${Math.random() * 100}%`;
                
                const animationDuration = 10 + Math.random() * 20;
                snowflake.style.animation = `fall ${animationDuration}s linear infinite`;
                
                snowflake.style.animationDelay = `${Math.random() * 5}s`;
                
                snowContainer.appendChild(snowflake);
            }
            
            const style = document.createElement('style');
            style.textContent = `
                @keyframes fall {
                    0% {
                        transform: translateY(-100px);
                    }
                    100% {
                        transform: translateY(600px);
                    }
                }
            `;
            document.head.appendChild(style);
        }
        
        window.onload = function() {
            createSnow();
            setTimeout(() => {
                createFireworks();
            }, 500);
        };
    </script>
</body>
</html>
