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
            min-height: 200vh; /* Ensure enough content to scroll */
            overflow: hidden;
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
            position: fixed;
            bottom: 10px;
            right: 10px;
            width: 100px;
            height: 100px;
            background: url('images/image1.png') no-repeat center/cover;
            transition: background 0.3s;
        }
        .sticky-image:hover {
            background: url('images/image2.png') no-repeat center/cover;
        }
        
        .floating-image {
            position: absolute;
            width: 80px;
            height: 80px;
            background: url('Images/floatingScroll.png') no-repeat center/cover;
            pointer-events: none;
        }
        
        @keyframes backgroundMove {
            0% { background-position: 0 0; }
            100% { background-position: -1000px -1000px; }
        }
        body {
            background: url('images/moving-background.png') repeat;
            animation: backgroundMove 30s linear infinite;
        }
        
        .glitch {
            display: inline-block;
            font-size: 24px;
            position: relative;
        }
    </style>
</head>
<body>
    <h1 id="glitchText"></h1>
    
    <div class="tab-container">
        <div class="tab" onclick="showPage('webcomic')">Webcomic Page</div>
        <div class="tab" onclick="showPage('misc')">Misc Text Page</div>
    </div>
    
    <div id="webcomic" class="page">
        <button onclick="prevPage()">Previous</button>
        <img id="comicPage" src="images/comic1.png" alt="Webcomic Page">
        <button onclick="nextPage()">Next</button>
    </div>
    
    <div id="misc" class="page" style="display:none;">
        <p>Miscellaneous text content goes here...</p>
    </div>
    
    <div class="sticky-image"></div>
    <div class="floating-image" id="floatingImage"></div>
    
    <script>
        let currentPage = 1;
        function nextPage() {
            currentPage++;
            document.getElementById('comicPage').src = `images/comic${currentPage}.png`;
        }
        function prevPage() {
            if (currentPage > 1) {
                currentPage--;
                document.getElementById('comicPage').src = `images/comic${currentPage}.png`;
            }
        }
        function showPage(page) {
            document.getElementById('webcomic').style.display = 'none';
            document.getElementById('misc').style.display = 'none';
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
