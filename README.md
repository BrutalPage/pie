<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Glitchy Neocities Template</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
        @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
        
        @font-face {
            font-family: 'digitalFont';
            src: url('Fonts/HomeVIdeo.ttf') format('woff1');
            font-weight: normal;
            font-style: normal;
        }

        /* header stuff */
        header {
        display: none;
        }
        
        h1, h2, h3 {
            border-bottom: none;
            text-decoration: none;
        }
        /* header stuff end */

        
        body {
            background-color: black;
            color: white;
            font-family: 'digitalFont', sans-serif;
            text-align: center;
            padding: 50px;
            overflow: hidden;
        
        }
            @font-face {
            font-family: 'digitalFont'; /*a name to be used later*/
            src: url('Font/HomeVideo.ttf'); /*URL to font*/
        }
            .classname {
            font-family: 'digitalFont';
        }

        .title-container {
            display: grid;
            grid-template-columns: repeat(10, 1fr);
            grid-template-rows: repeat(10, 1fr);
            width: 20vw;
            height: auto;

            max-width: 100%;
            max-height: 100%;

            image-rendering: optimizeSpeed;             /* STOP SMOOTHING, GIVE ME SPEED  */
            image-rendering: -moz-crisp-edges;          /* Firefox                        */
            image-rendering: -o-crisp-edges;            /* Opera                          */
            image-rendering: -webkit-optimize-contrast; /* Chrome (and eventually Safari) */
            image-rendering: pixelated;                 /* Universal support since 2021   */
            image-rendering: optimize-contrast;         /* CSS3 Proposed                  */
            -ms-interpolation-mode: nearest-neighbor;   /* IE8+                           */
            
            margin: auto;
            position: relative;
        }
        .title-piece {
            width: 50px;
            height: 50px;
            background-size: 500px 500px;
            opacity: 0;
            transition: opacity 0.02s;
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
        
        .sticky-image {
            background: none;
            position: fixed;
            bottom: 5%; /* Adjusts dynamically based on screen size */
            right: 5%;
            width: 20vw; /* Responsive width based on viewport */
            height: auto; /* Maintains aspect ratio */
            
            max-width: 100%;
            max-height: 100%;

           image-rendering: optimizeSpeed;             /* STOP SMOOTHING, GIVE ME SPEED  */
            image-rendering: -moz-crisp-edges;          /* Firefox                        */
            image-rendering: -o-crisp-edges;            /* Opera                          */
            image-rendering: -webkit-optimize-contrast; /* Chrome (and eventually Safari) */
            image-rendering: pixelated;                 /* Universal support since 2021   */
            image-rendering: optimize-contrast;         /* CSS3 Proposed                  */
            -ms-interpolation-mode: nearest-neighbor;   /* IE8+                           */
            
            transition: transform 0.3s ease;
        }
        
        .sticky-image img {
            width: 100%;
            height: auto;
            transition: transform 0.3s ease, opacity 0.3s ease;
        }
        
        /* Bounce Animation */
        @keyframes bounce {
            0% { transform: translateY(-15); }
            25% { transform: translateY(5px); }
            50% { transform: translateY(-2); }
            75% { transform: translateY(1px); }
            100% { transform: translateY(0); }
        }

        .sticky-image:hover img {
            animation: bounce 0.26s ease forwards; /* Apply bounce effect on hover */
            content: url('Images/floatingScroll.png'); /* Change image on hover */
        }
        
        .glitch {
            display: inline-block;
            font-size: 24px;
            position: relative;
        }
        
        #misc {
            text-align: center;
        }
        #misc h1 {
            font-size: 64px;
            margin-bottom: 10px;
        }
        #misc h2 {
            font-size: 24px;
            margin-bottom: 20px;
        }
        #misc p {
            font-size: 18px;
            line-height: 1.5;
        }
    </style>
</head>
<body>
    <h1 id="glitchText"></h1>

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
    
    <div id="Comic" class="page">
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
        function showPage(page) {
            document.getElementById('Home').style.display = 'none';
            document.getElementById('Comic').style.display = 'none';
            document.getElementById('BlaBla').style.display = 'none';
            document.getElementById(page).style.display = 'block';
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
        
        const glitchElement = document.getElementById('glitchText');
        glitchText(glitchElement, "PLASTIC RHAPSODY");
        
        function loadTitleImage() {
            const container = document.getElementById('titleContainer');
            for (let y = 0; y < 10; y++) {
                for (let x = 0; x < 10; x++) {
                    let piece = document.createElement('div');
                    piece.classList.add('title-piece');
                    piece.style.backgroundImage = "url('Images/plastic_logo.png')";
                    piece.style.backgroundPosition = `-${x * 50}px -${y * 50}px`;
                    container.appendChild(piece);
                }
            }
        }
        
        window.onload = loadTitleImage;
        
    </script>
</body>
</html>
