<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Glitchy Neocities Template</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
        
        body {
            background-color: black;
            color: white;
            font-family: 'Brush Script MT', cursive;
            text-align: center;
            padding: 50px;
        }
        
        .glitch {
            display: inline-block;
            font-size: 24px;
            position: relative;
        }
        
        .grid-container {
            display: grid;
            grid-template-columns: repeat(6, 1fr);
            grid-template-rows: repeat(6, 1fr);
            gap: 0;
            justify-content: center;
            margin-top: 20px;
            width: 600px;
            height: 600px;
            margin: auto;
        }
        
        .reveal-box {
            width: 100px;
            height: 100px;
            background: white;
            position: relative;
            overflow: hidden;
            cursor: pointer;
        }
        
        .hidden-image {
            width: 100%;
            height: 100%;
            background: red;
            position: absolute;
            top: 0;
            left: 0;
            opacity: 0;
        }
        
        @keyframes blink {
            0% { opacity: 1; }
            50% { opacity: 0; }
            100% { opacity: 1; }
        }
    </style>
</head>
<body>
    <h1 id="glitchText"></h1>
    
    <div class="grid-container" id="grid"></div>
    
    <script>
        function glitchText(element, text) {
            element.innerHTML = '';
            text.split('').forEach(letter => {
                let span = document.createElement('span');
                span.setAttribute('data-char', letter);
                span.innerText = letter;
                element.appendChild(span);
                
                setInterval(() => {
                    if (Math.random() < 0.003) {
                        span.innerText = Math.random().toString(36).charAt(2);
                        setTimeout(() => {
                            span.innerText = letter;
                        }, 10);
                    }
                }, 5);
            });
        }
        
        const glitchElement = document.getElementById('glitchText');
        glitchText(glitchElement, "CITY GIRL / ILLEGAL JOB / SHOTGUN LEG");

        const grid = document.getElementById('grid');
        const boxes = [];

        for (let i = 0; i < 6; i++) {
            boxes[i] = [];
            for (let j = 0; j < 6; j++) {
                const box = document.createElement('div');
                box.classList.add('reveal-box');
                const hiddenImage = document.createElement('div');
                hiddenImage.classList.add('hidden-image');
                box.appendChild(hiddenImage);
                grid.appendChild(box);
                boxes[i][j] = box;
            }
        }

        function blinkEffect(element, times) {
            let count = 0;
            function blink() {
                if (count >= times) {
                    element.style.opacity = 1;
                    return;
                }
                element.style.opacity = element.style.opacity === '0' ? '1' : '0';
                count++;
                setTimeout(blink, 15);
            }
            blink();
        }

        function getNeighbors(x, y) {
            let neighbors = [];
            for (let dx = -1; dx <= 1; dx++) {
                for (let dy = -1; dy <= 1; dy++) {
                    if (dx === 0 && dy === 0) continue;
                    let nx = x + dx;
                    let ny = y + dy;
                    if (nx >= 0 && nx < 6 && ny >= 0 && ny < 6) {
                        neighbors.push(boxes[nx][ny]);
                    }
                }
            }
            return neighbors;
        }

        boxes.forEach((row, x) => {
            row.forEach((box, y) => {
                box.addEventListener('mouseenter', () => {
                    let blinkTimes = Math.floor(Math.random() * 8) + 3;
                    blinkEffect(box.firstChild, blinkTimes);
                    getNeighbors(x, y).forEach(neighbor => {
                        let neighborBlinkTimes = Math.floor(Math.random() * 8) + 3;
                        blinkEffect(neighbor.firstChild, neighborBlinkTimes);
                    });
                });
            });
        });
    </script>
</body>
</html>
