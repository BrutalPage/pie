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

    function loadTitleImage() {
        const container = document.getElementById('titleContainer');
        container.innerHTML = ''; // Clear previous content

        const aspectRatio = window.innerWidth / window.innerHeight;
        const isVertical = aspectRatio < 0.5625; // ~9:16

        const image = isVertical ? VERTICAL_IMAGE : HORIZONTAL_IMAGE;
        container.style.gridTemplateColumns = `repeat(${image.cols}, 1fr)`;
        container.style.gridTemplateRows = `repeat(${image.rows}, 1fr)`;
        container.style.width = `${Math.min(window.innerWidth * 0.9, image.width)}px`;
        container.style.height = `${container.style.width.replace('px','') * image.height / image.width}px`;

        let delay = 0;

        for (let y = 0; y < image.rows; y++) {
            for (let x = 0; x < image.cols; x++) {
                const delayOffset = 0.01 + (Math.floor(Math.random() * 3) + 1) * 0.01;

                setTimeout(() => {
                    let piece = document.createElement('div');
                    piece.classList.add('title-piece');
                    piece.style.backgroundImage = `url('${image.src}')`;
                    piece.style.backgroundSize = `${image.width}px ${image.height}px`;
                    piece.style.backgroundPosition = `-${x * (image.width / image.cols)}px -${y * (image.height / image.rows)}px`;

                    // Blinking with 25% chance
                    if (Math.random() < 0.25) {
                        let blinkCount = Math.floor(Math.random() * 3) + 1;
                        for (let i = 0; i < blinkCount; i++) {
                            setTimeout(() => piece.style.visibility = 'hidden', i * (BLINK_SPEED * 2));
                            setTimeout(() => piece.style.visibility = 'visible', i * (BLINK_SPEED * 2) + BLINK_SPEED);
                        }
                    }

                    container.appendChild(piece);
                }, delay * 1000);

                delay += delayOffset;
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
