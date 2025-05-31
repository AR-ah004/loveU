
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For Rahaf</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background-color: #fff5f7;
            overflow: hidden;
            font-family: 'Arial', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        
        .container {
            position: relative;
            width: 100vw;
            height: 100vh;
        }
        
        .heart {
            position: absolute;
            width: 12px;
            height: 12px;
            background-color: #ff6b8b;
            border-radius: 50%;
            transform: translate(-50%, -50%);
            opacity: 0;
            animation: fadeIn 0.5s forwards;
            box-shadow: 0 0 10px rgba(255, 107, 139, 0.5);
        }
        
        .message {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
            opacity: 0;
            transition: opacity 2s;
            z-index: 10;
            color: #d23669;
            width: 80%;
            max-width: 600px;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
        }
        
        h1 {
            font-size: 3.5rem;
            margin-bottom: 30px;
            font-weight: 300;
            line-height: 1.3;
        }
        
        p {
            font-size: 2rem;
            margin-top: 40px;
            font-weight: 300;
            font-style: italic;
        }
        
        .signature {
            font-size: 1.8rem;
            margin-top: 20px;
            text-align: right;
            font-family: 'Brush Script MT', cursive;
        }
        
        @keyframes fadeIn {
            to {
                opacity: 0.9;
            }
        }
        
        @keyframes pulse {
            0% { transform: translate(-50%, -50%) scale(1); }
            50% { transform: translate(-50%, -50%) scale(1.03); }
            100% { transform: translate(-50%, -50%) scale(1); }
        }
        
        @keyframes float {
            0% { transform: translate(-50%, -50%) translateY(0px); }
            50% { transform: translate(-50%, -50%) translateY(-10px); }
            100% { transform: translate(-50%, -50%) translateY(0px); }
        }
    </style>
</head>
<body>
    <div class="container" id="container"></div>
    <div class="message" id="message">
        <h1>If I could give you one thing in life, it would be the ability to see yourself through my eyes</h1>
        <p>would you realize how deeply and endlessly I love you. You're the reason my heart beats a little faster, my days feel brighter, and my world makes sense. Loving you isn't just something I do.  
        it's who I am now, because you're the best part of me</p>
        <div class="signature">ur lover Ayham</div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const container = document.getElementById('container');
            const message = document.getElementById('message');
            const heartPoints = generateHeartPoints(window.innerWidth/2, window.innerHeight/2, Math.min(window.innerWidth, window.innerHeight)/3);
            
            // Draw small hearts along the heart path
            heartPoints.forEach((point, index) => {
                setTimeout(() => {
                    createHeart(point.x, point.y, index % 7);
                }, index * 15);
            });
            
            // Show message after animation completes
            setTimeout(() => {
                message.style.opacity = 1;
                message.style.animation = 'float 6s ease-in-out infinite';
                
                // Add some floating hearts after main animation
                setInterval(createFloatingHeart, 800);
            }, heartPoints.length * 15 + 1000);
            
            function createHeart(x, y, colorVariant) {
                const heart = document.createElement('div');
                heart.className = 'heart';
                
                // Soft color variations
                const colors = [
                    '#ff6b8b', '#ff8fab', '#ffb3c1', 
                    '#fcc2d7', '#f8d7e3', '#ff9eb7', 
                    '#fdcedf'
                ];
                heart.style.backgroundColor = colors[colorVariant];
                
                heart.style.left = `${x}px`;
                heart.style.top = `${y}px`;
                
                // Random slight size variation
                const size = 10 + Math.random() * 8;
                heart.style.width = `${size}px`;
                heart.style.height = `${size}px`;
                
                // Random animation delay for a more organic feel
                heart.style.animationDelay = `${Math.random() * 0.5}s`;
                
                container.appendChild(heart);
            }
            
            function createFloatingHeart() {
                const size = 6 + Math.random() * 10;
                const x = Math.random() * window.innerWidth;
                const colors = ['#ff6b8b', '#ff8fab', '#ffb3c1', '#fcc2d7'];
                const color = colors[Math.floor(Math.random() * colors.length)];
                
                const heart = document.createElement('div');
                heart.className = 'heart';
                heart.style.width = `${size}px`;
                heart.style.height = `${size}px`;
                heart.style.left = `${x}px`;
                heart.style.top = `${window.innerHeight + 20}px`;
                heart.style.backgroundColor = color;
                heart.style.opacity = '0.7';
                
                container.appendChild(heart);
                
                // Animate floating up
                const duration = 5000 + Math.random() * 5000;
                heart.animate([
                    { top: `${window.innerHeight + 20}px`, opacity: 0.7 },
                    { top: `-50px`, opacity: 0 }
                ], {
                    duration: duration,
                    easing: 'cubic-bezier(0.4, 0, 0.2, 1)'
                });
                
                // Remove after animation
                setTimeout(() => {
                    heart.remove();
                }, duration);
            }
            
            // Generates points along a heart shape
            function generateHeartPoints(centerX, centerY, size) {
                const points = [];
                const steps = 300; // More points for smoother heart
                
                for (let i = 0; i < steps; i++) {
                    const t = (i / steps) * 2 * Math.PI;
                    // Heart parametric equation
                    const x = centerX + size * (16 * Math.pow(Math.sin(t), 3)) / 16;
                    const y = centerY - size * (13 * Math.cos(t) - 5 * Math.cos(2*t) - 2 * Math.cos(3*t) - Math.cos(4*t)) / 16;
                    
                    // Add some randomness to make it more organic
                    const randX = (Math.random() - 0.5) * 15;
                    const randY = (Math.random() - 0.5) * 15;
                    
                    points.push({
                        x: x + randX,
                        y: y + randY
                    });
                }
                
                return points;
            }
        });
    </script>
</body>
</html>
