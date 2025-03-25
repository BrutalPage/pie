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
            background: none;
            position: fixed;
            bottom: 5%; /* Adjusts dynamically based on screen size */
            right: 5%;
            width: 10vw; /* Responsive width based on viewport */
            height: auto; /* Maintains aspect ratio */
            
            max-width: 100%;
            max-height: 100%;
            
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
    
    <div class="tab-container">
        <div class="tab" onclick="showPage('Home')">Webcomic Page</div>
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
    </script>
</body>
</html>
