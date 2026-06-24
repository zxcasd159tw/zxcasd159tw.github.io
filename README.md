<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * {
            box-sizing: border-box;
        }
        body {
            margin: 0;
            padding: 0;
            width: 100vw;
            height: 100vh;
            background-color: #f0f2f5;
            font-family: sans-serif;
            overflow: hidden; 
            position: relative;
        }
        #content-wrapper {
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        h1 {
            text-align: center;
            margin-top: 50px;
            color: #333;
            z-index: 5;
            position: relative;
            pointer-events: none; 
        }
        .btn {
            padding: 12px 24px;
            font-size: 18px;
            font-weight: bold;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            white-space: nowrap; 
            position: absolute;
        }
        .btn-yes {
            background-color: #4caf50;
            color: white;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%) scale(1);
            transform-origin: center;
            z-index: 10; 
            transition: transform 0.2s ease; 
        }
        .btn-no {
            background-color: #f44336;
            color: white;
            z-index: 20; 
            transition: left 0.1s ease, top 0.1s ease, transform 0.1s ease; 
        }
        .success-message {
            font-size: 42px;
            text-align: center;
            margin-top: 30vh;
            color: #4caf50;
            font-weight: bold;
            line-height: 1.5;
        }
    </style>
</head>
<body>
    <div id="content-wrapper">
        <h1 id="mainTitle">我可以當你的小情人嗎？</h1>
        <button class="btn btn-yes" id="mainYes" onclick="handleYesClick()">可以</button>
        <button class="btn btn-no" id="firstNo" style="left: calc(50% + 80px); top: 50%; transform: translateY(-50%) scale(1);" onclick="handleNoClick(event)">不行</button>
    </div>
    <script>
        let yesScale = 1.0;
        let noScale = 1.0;
        const noTexts = [
            "不能  😐",
            "想都別想  😜",
            "未達到我的標準 ❌",
            "下輩子吧 🧐",
            "抓不到我吧嘿嘿 🏃‍♂️💨" 
        ];
        let clickCount = 0;
        const mainYes = document.getElementById('mainYes');
        const contentWrapper = document.getElementById('content-wrapper');
        function handleNoClick(event) {
            event.target.remove(); 
            yesScale += 0.6; 
            noScale -= 0.12; 
            if (noScale < 0.4) noScale = 0.4; 
            mainYes.style.transform = `translate(-50%, -50%) scale(${yesScale})`;
            clickCount++;
            createNewNoButton();
        }
        function createNewNoButton() {
            const newNo = document.createElement('button');
            newNo.className = 'btn btn-no';
            moveButtonToRandomPos(newNo);
            let textIndex = clickCount - 1;
            if (clickCount < 5) {
                newNo.innerText = noTexts[textIndex];
                newNo.addEventListener('click', handleNoClick);
            } else {
                newNo.innerText = noTexts[noTexts.length - 1];
                
                newNo.addEventListener('mouseenter', function() {
                    moveButtonToRandomPos(newNo);
                });
            }

            contentWrapper.appendChild(newNo);
        }
        function moveButtonToRandomPos(button) {
            const posX = Math.random() * (window.innerWidth - 250);
            const posY = Math.random() * (window.innerHeight - 150);
            
            button.style.left = `${Math.max(50, posX)}px`;
            button.style.top = `${Math.max(50, posY)}px`;
            button.style.transform = `scale(${noScale})`;
        }
        function handleYesClick() {
            contentWrapper.innerHTML = '<div class="success-message">感謝讚賞！🎉順帶一提我是個小小的繪師，歡迎搜尋追蹤<a href="https://www.pixiv.net/users/5472433" target="_blank">Pixiv：Mepurin</a>😎（<a href="https://www.youtube.com/@Mepurin?sub_confirmation=1" target="_blank">也可以訂閱YouTube頻道喔！</a>）</div>';
        }
