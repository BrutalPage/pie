<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Glitchy Neocities Template</title>
    <style>
        body {
            background-color: black;
            color: white;
            font-family: monospace;
            text-align: center;
            padding: 20px;
        }

        .title-container {
            display: grid;
            margin: auto;
            position: relative;
        }

        .title-piece {
            background-size: contain;
            background-repeat: no-repeat;
        }

        #textField {
            font-family: monospace;
            white-space: pre;
            text-align: left;
            margin-top: 40px;
            line-height: 1.2;
            display: inline-block;
        }

        .char {
            display: inline-block;
            transition: background 0.2s;
        }

        .char:hover {
            color: #00FF00;
        }
    </style>
</head>
<body>
    <h1 id="glitchText">PLASTIC RHAPSODY</h1>
    <div class="title-container" id="titleContainer"></div>
    <div id="textField"></div>

    <script>
        const H_IMG = {
            src: 'Images/plastic_logo.png',
            width: 950,
            height: 550
        };

        const V_IMG = {
            src: 'Images/plastic_logo_vert.png',
            width: 600,
            height: 850
        };

        const container = document.getElementById('titleContainer');
        const glitchText = document.getElementById('glitchText');

        function isVerticalRatio() {
            const ratio = window.innerHeight / window.innerWidth;
            return ratio > (9 / 16);
        }

        function loadTitleImage() {
            const { width: imgW, height: imgH, src } = isVerticalRatio() ? V_IMG : H_IMG;

            // Clear container only on ratio change
            container.innerHTML = '';

            // Determine size per tile
            const cols = Math.floor(imgW / 50);
            const rows = Math.floor(imgH / 50);
            const pieceW = imgW / cols;
            const pieceH = imgH / rows;

            container.style.gridTemplateColumns = `repeat(${cols}, ${pieceW}px)`;
            container.style.gridTemplateRows = `repeat(${rows}, ${pieceH}px)`;
            container.style.width = `${imgW}px`;
            container.style.height = `${imgH}px`;

            let delay = 0;
            let index = 0;
            for (let y = 0; y < rows; y++) {
                for (let x = 0; x < cols; x++) {
                    setTimeout(() => {
                        const piece = document.createElement('div');
                        piece.classList.add('title-piece');
                        piece.style.width = `${pieceW}px`;
                        piece.style.height = `${pieceH}px`;
                        piece.style.backgroundImage = `url(${src})`;
                        piece.style.backgroundPosition = `-${x * pieceW}px -${y * pieceH}px`;

                        container.appendChild(piece);

                        // Blink effect
                        if (Math.random() < 0.25) {
                            const blinkCount = Math.floor(Math.random() * 3) + 1;
                            for (let i = 0; i < blinkCount; i++) {
                                setTimeout(() => piece.style.visibility = 'hidden', i * 60);
                                setTimeout(() => piece.style.visibility = 'visible', i * 60 + 30);
                            }
                        }
                    }, delay);
                    delay += 10;
                    index++;
                }
            }
        }

        function fillTextField() {
            const textField = document.getElementById('textField');
            textField.innerHTML = '';
            const cols = 50;
            const rows = 20;
            const chars = [' ', '.', ' ', ' ', '.', ' '];

            for (let y = 0; y < rows; y++) {
                let line = '';
                for (let x = 0; x < cols; x++) {
                    const char = document.createElement('span');
                    char.classList.add('char');
                    char.innerText = chars[Math.floor(Math.random() * chars.length)];
                    char.onmouseenter = () => { char.innerText = '█'; };
                    char.onmouseleave = () => {
                        char.innerText = chars[Math.floor(Math.random() * chars.length)];
                    };
                    textField.appendChild(char);
                }
                textField.appendChild(document.createElement('br'));
            }
        }

        window.onload = () => {
            loadTitleImage();
            fillTextField();
        };

        window.onresize = () => {
            if (isVerticalRatio()) {
                loadTitleImage();
            }
        };
    </script>
</body>
</html>
