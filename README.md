<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Glitchy Neocities Template</title>
    <style>
        @font-face {
            font-family: 'digitalFont';
            src: url('Fonts/HomeVideo.ttf') format('woff');
            font-weight: normal;
            font-style: normal;

        #textGrid {
    position: absolute;
    top: 0;
    left: 0;
    display: grid;
    pointer-events: none;
    user-select: none;
    font-size: 12px;
    color: #00ffcc;
    opacity: 0.1;
    z-index: 0;
}

.text-cell {
    white-space: pre;
    font-family: monospace;
}
.text-cell.hovered {
    color: white;
    font-weight: bold;
    opacity: 1;
}

        }

        body {
            background-color: black;
            color: white;
            font-family: 'digitalFont', sans-serif;
            text-align: center;
            padding: 50px;
        }

        .title-container {
            display: grid;
            grid-template-columns: repeat(19, 50px);
            grid-template-rows: repeat(11, 50px);
            width: 950px;
            height: 550px;
            margin: auto;
            position: relative;
        }

        .title-piece {
            width: 50px;
            height: 50px;
            background-image: url('Images/plastic_logo.png');
            background-size: 950px 550px;
            background-position: center;
        }

        .sticky-image {
            background: none;
            position: fixed;
            bottom: 5%;
            right: 5%;
            width: 20vw;
            height: auto;
            max-width: 100%;
            max-height: 100%;
            transition: transform 0.3s ease;
        }

        .sticky-image img {
            width: 100%;
            height: auto;
            transition: transform 0.3s ease, opacity 0.3s ease;
        }

        @keyframes bounce {
            0% { transform: translateY(-15px); }
            25% { transform: translateY(5px); }
            50% { transform: translateY(-2px); }
            75% { transform: translateY(1px); }
            100% { transform: translateY(0); }
        }

        .sticky-image:hover img {
            animation: bounce 0.26s ease forwards;
            content: url('Images/floatingScroll.png');
        }

        #glitchText {
            font-size: 160%;
            display: inline-block;
            position: relative;
        }

        .glitch {
            display: inline-block;
            font-size: 60px;
            position: relative;
        }

        .tab-container {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-bottom: 20px;
        }
        .tab {
            padding: 10px;
            background: gray;
            color: white;
            cursor: pointer;
            border-radius: 5px;
        }
        .tab:hover {
            background: darkgray;
        }
    </style>
</head>
<body>
    <h1 id="glitchText" class="glitch">PLASTIC RHAPSODY</h1>
    <div class="title-container" id="titleContainer"></div>
    <div id="textGrid"></div>

    <div class="tab-container">
        <div class="tab" onclick="showPage('Home')">Misc Text Page</div>
        <div class="tab" onclick="showPage('Comic')">Webcomic Page</div>
        <div class="tab" onclick="showPage('BlaBla')">Misc Text Page</div>
    </div>

    <div id="Home" class="page">
        <h1>Plastic Rhapsody</h1>
        <h2>Welcome to my webpage</h2>
        <p>CITY GIRL<br>ILLEGAL JOB<br>METAL LEG</p>
    </div>

    <div id="Comic" class="page" style="display:none;">
        <button onclick="prevPage()">Previous</button>
        <img id="comicPage" src="Images/comic1.png" alt="Webcomic Page">
        <button onclick="nextPage()">Next</button>
    </div>

    <div id="BlaBla" class="page" style="display:none;">
        <h2>blablablabla</h2>
        <p>blablablablablablabalbablablabala</p>
    </div>

    <div class="sticky-image">
        <img src="Images/floatingScroll_idle.png" alt="Sticky Image" style="background: transparent;">
    </div>

    <script>
    const HORIZONTAL_IMAGE = {
        src: 'Images/plastic_logo.png',
        width: 950,
        height: 550,
        cols: 19,
        rows: 11
    };

    const VERTICAL_IMAGE = {
        src: 'Images/plastic_logo_vert.png',
        width: 600,
        height: 850,
        cols: 12,
        rows: 17
    };

    const BLINK_SPEED = 80; // Smaller = faster blinking

const HORIZONTAL_IMAGE = {
    src: 'Images/plastic_logo.png',
    width: 950,
    height: 550,
    cols: 19,
    rows: 11
};

const VERTICAL_IMAGE = {
    src: 'Images/plastic_logo_vert.png',
    width: 600,
    height: 850,
    cols: 12,
    rows: 17
};

let lastMode = '';

function loadTitleImage() {
    const container = document.getElementById('titleContainer');
    const textGrid = document.getElementById('textGrid');
    const ratio = window.innerWidth / window.innerHeight;
    const isVertical = ratio < 0.5625; // 9:16

    const currentMode = isVertical ? 'vertical' : 'horizontal';
    const image = isVertical ? VERTICAL_IMAGE : HORIZONTAL_IMAGE;

    // Only rebuild grid if mode changed
    if (lastMode !== currentMode || container.childElementCount !== image.cols * image.rows) {
        lastMode = currentMode;
        container.innerHTML = '';
        textGrid.innerHTML = '';

        const cellWidth = image.width / image.cols;
        const cellHeight = image.height / image.rows;

        container.style.gridTemplateColumns = `repeat(${image.cols}, ${cellWidth}px)`;
        container.style.gridTemplateRows = `repeat(${image.rows}, ${cellHeight}px)`;
        container.style.width = `${image.width}px`;
        container.style.height = `${image.height}px`;

        textGrid.style.gridTemplateColumns = `repeat(${image.cols}, ${cellWidth}px)`;
        textGrid.style.gridTemplateRows = `repeat(${image.rows}, ${cellHeight}px)`;
        textGrid.style.width = `${image.width}px`;
        textGrid.style.height = `${image.height}px`;
        textGrid.style.left = container.offsetLeft + 'px';
        textGrid.style.top = container.offsetTop + 'px';

        let delay = 0;

        for (let y = 0; y < image.rows; y++) {
            for (let x = 0; x < image.cols; x++) {
                const delayOffset = 0.001 + (Math.random() * 0.003);

                // Image piece
                setTimeout(() => {
                    const piece = document.createElement('div');
                    piece.classList.add('title-piece');
                    piece.style.width = `${cellWidth}px`;
                    piece.style.height = `${cellHeight}px`;
                    piece.style.backgroundImage = `url('${image.src}')`;
                    piece.style.backgroundSize = `${image.width}px ${image.height}px`;
                    piece.style.backgroundPosition = `-${x * cellWidth}px -${y * cellHeight}px`;

                    // Blink effect
                    if (Math.random() < 0.25) {
                        const blinkCount = Math.floor(Math.random() * 3) + 1;
                        for (let i = 0; i < blinkCount; i++) {
                            const blinkDelay = i * 40;
                            setTimeout(() => piece.style.visibility = 'hidden', blinkDelay);
                            setTimeout(() => piece.style.visibility = 'visible', blinkDelay + 20);
                        }
                    }

                    container.appendChild(piece);
                }, delay * 1000);

                // Text cell
                const textCell = document.createElement('div');
                textCell.className = 'text-cell';
                textCell.innerText = Math.random() < 0.5 ? '   ' : ' . ';
                textCell.dataset.default = textCell.innerText;

                textCell.addEventListener('mouseenter', () => {
                    textCell.innerText = ' █ ';
                    textCell.classList.add('hovered');
                });
                textCell.addEventListener('mouseleave', () => {
                    textCell.innerText = textCell.dataset.default;
                    textCell.classList.remove('hovered');
                });

                textGrid.appendChild(textCell);

                delay += delayOffset;
            }
        }
    }
}


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

    function showPage(page) {
        document.getElementById('Home').style.display = 'none';
        document.getElementById('Comic').style.display = 'none';
        document.getElementById('BlaBla').style.display = 'none';
        document.getElementById(page).style.display = 'block';
    }

    let currentPage = 1;
    function nextPage() {
        currentPage++;
        document.getElementById('comicPage').src = `Images/comic${currentPage}.png`;
    }

    function prevPage() {
        if (currentPage > 1) {
            currentPage--;
            document.getElementById('comicPage').src = `Images/comic${currentPage}.png`;
        }
    }

    function glitchTextEffect() {
        const glitchEl = document.getElementById('glitchText');
        glitchText(glitchEl, glitchEl.textContent);
    }

    window.onload = loadTitleImage;
    window.onresize = loadTitleImage;
    
    window.onload = () => {
        loadTitleImage();
        glitchTextEffect();
    };

    window.onresize = () => {
        loadTitleImage(); // Redraw on resize
    };
</script>

</body>
</html>
