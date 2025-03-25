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
            grid-template-columns: repeat(10, 50px);
            grid-template-rows: repeat(10, 50px);
            width: 500px;
            height: 500px;
            margin: auto;
            position: relative;
        }

        .title-piece {
            width: 50px;
            height: 50px;
            background-image: url('Images/plastic_logo.png');
            background-size: 500px 500px;
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
        }
    </style>
</head>
<body>
    <h1 id="glitchText"></h1>
    <div class="title-container" id="titleContainer"></div>

    <div class="sticky-image">
        <img src="Images/floatingScroll_idle.png" alt="Sticky Image" style="background: transparent;">
    </div>

    <script>
        function loadTitleImage() {
            const container = document.getElementById('titleContainer');
            for (let y = 0; y < 10; y++) {
                for (let x = 0; x < 10; x++) {
                    let piece = document.createElement('div');
                    piece.classList.add('title-piece');
                    piece.style.backgroundPosition = `-${x * 50}px -${y * 50}px`;
                    container.appendChild(piece);
                }
            }
        }

        window.onload = loadTitleImage;
    </script>
</body>
</html>
