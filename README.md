
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KuroFinX | Winter Dev</title>
    <style>
        :root {
            --bg-color: #050505;
            --card-bg: rgba(15, 15, 15, 0.9); /* Leicht transparent für den Schnee-Effekt */
            --text-color: #e0e0e0;
            --accent-color: #8833ff; 
            --glow: rgba(136, 51, 255, 0.5);
        }

        body {
            font-family: 'Segoe UI', Roboto, sans-serif;
            background: #050505;
            color: var(--text-color);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            overflow: hidden; /* Verhindert Scrollbars durch den Schnee */
        }

        /* Schnee-Container */
        #snow-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .snowflake {
            position: absolute;
            top: -10px;
            color: white;
            user-select: none;
            z-index: 0;
            opacity: 0.8;
            filter: blur(1px);
        }

        /* Sound Button */
        #sound-toggle {
            position: fixed;
            top: 20px;
            right: 20px;
            background: var(--card-bg);
            border: 1px solid var(--accent-color);
            color: var(--text-color);
            padding: 10px;
            border-radius: 50%;
            cursor: pointer;
            z-index: 100;
            box-shadow: 0 0 10px var(--glow);
            font-family: monospace;
        }

        .container {
            width: 100%;
            max-width: 380px;
            padding: 20px;
            text-align: center;
            position: relative;
            z-index: 10;
        }

        .profile-header {
            margin-bottom: 35px;
            animation: fadeInDown 0.8s ease-out;
        }

        .profile-img {
            width: 100px;
            height: 100px;
            border-radius: 24px;
            border: 2px solid var(--accent-color);
            margin-bottom: 15px;
            box-shadow: 0 0 20px var(--glow);
            object-fit: cover;
        }

        h1 {
            font-size: 1.6rem;
            margin: 0;
            letter-spacing: 2px;
            text-transform: uppercase;
        }

        .dev-tag {
            font-family: 'Courier New', monospace;
            color: var(--accent-color);
            font-size: 0.8rem;
            background: rgba(136, 51, 255, 0.1);
            padding: 4px 10px;
            border-radius: 6px;
            display: inline-block;
            margin-top: 8px;
        }

        .links {
            display: flex;
            flex-direction: column;
            gap: 14px;
        }

        .link-card {
            background: var(--card-bg);
            border: 1px solid #1a1a1a;
            padding: 18px;
            text-decoration: none;
            color: var(--text-color);
            border-radius: 14px;
            font-weight: 500;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            display: flex;
            justify-content: space-between;
            align-items: center;
            backdrop-filter: blur(5px); /* Glaseffekt */
        }

        .link-card:hover {
            border-color: var(--accent-color);
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.5), 0 0 10px var(--glow);
            background: rgba(25, 25, 25, 0.9);
        }

        .link-card span {
            font-size: 0.7rem;
            opacity: 0.4;
            font-family: 'Courier New', monospace;
        }

        .footer {
            margin-top: 40px;
            font-size: 0.7rem;
            font-family: 'Courier New', monospace;
            opacity: 0.3;
        }

        @keyframes fadeInDown {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes fall {
            to { transform: translateY(105vh); }
        }
    </style>
</head>
<body>

<!-- Audio Element (Ersetze den Link durch deine Sound-Datei) -->
<audio id="bg-music" loop>
    <source src="https://files.catbox.moe/qmfv5p.mp3" type="audio/mpeg">
</audio>

<button id="sound-toggle">🔈</button>

<div id="snow-container"></div>

<div class="container">
    <div class="profile-header">
        <img src="https://files.catbox.moe/z6m5ee.jpg" alt="KuroFinX" class="profile-img">
        <h1>KuroFinX</h1>
        <div class="dev-tag">root@kurofinx:~# winter_mode --on</div>
    </div>

    <div class="links">
        <a href="https://guns.lol/kurofinx" class="link-card" target="_blank">
            GUNS.LOL <span>/identity</span>
        </a>
        <a href="https://discord.gg/2XxmRSPs6G" class="link-card" target="_blank">
            DISCORD <span>/connect</span>
        </a>
        <a href="https://www.youtube.com/@kurofinx" class="link-card" target="_blank">
            YOUTUBE <span>/source</span>
        </a>
        <a href="https://www.instagram.com/kurofinx" class="link-card" target="_blank">
            INSTAGRAM <span>/logs</span>
        </a>
        <a href="https://tiktok.com/@kurofinx" class="link-card" target="_blank">
            TIKTOK <span>/exec</span>
        </a>
    </div>

    <div class="footer">
        &gt; status: snowing<br>
        &gt; 2026 // KUROFINX_DEV
    </div>
</div>

<script>
    // Schnee-Effekt
    function createSnowflake() {
        const container = document.getElementById('snow-container');
        const snowflake = document.createElement('div');
        const size = Math.random() * 5 + 2 + 'px';
        
        snowflake.classList.add('snowflake');
        snowflake.innerText = '•'; // Du kannst auch '❄' nutzen
        snowflake.style.left = Math.random() * 100 + 'vw';
        snowflake.style.fontSize = size;
        snowflake.style.animation = `fall ${Math.random() * 3 + 2}s linear forwards`;
        
        container.appendChild(snowflake);
        
        setTimeout(() => {
            snowflake.remove();
        }, 5000);
    }

    setInterval(createSnowflake, 100);

    // Audio-Logik
    const music = document.getElementById('bg-music');
    const btn = document.getElementById('sound-toggle');
    let isPlaying = false;

    btn.onclick = () => {
        if (isPlaying) {
            music.pause();
            btn.innerText = '🔈';
        } else {
            music.play();
            btn.innerText = '🔊';
        }
        isPlaying = !isPlaying;
    };
</script>

</body>
</html>
