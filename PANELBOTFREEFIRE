<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SBR TEAM PANEL - SECURE</title>
    <style>
        body, html {
            margin: 0; padding: 0; height: 100%;
            font-family: 'Arial', sans-serif;
            background-color: #000; color: white;
            overflow: hidden; display: flex;
            justify-content: center; align-items: center;
        }

        /* خلفية البركان والنار */
        .volcano-bg {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: radial-gradient(circle at bottom, #801100 0%, #000000 80%);
            z-index: -2; animation: flame 3s infinite alternate;
        }

        @keyframes flame { from { opacity: 0.6; } to { opacity: 1; } }

        /* تأثير الثلج */
        .snowflakes { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: -1; }

        .container {
            background: rgba(0, 0, 0, 0.9);
            padding: 30px; border-radius: 20px;
            border: 2px solid #ff4500;
            box-shadow: 0 0 30px #ff4500;
            width: 380px; text-align: center; display: none;
        }

        .active { display: block; animation: zoomIn 0.4s; }

        h1 { color: #ff4500; margin-bottom: 5px; text-transform: uppercase; }
        .sub-title { color: #aaa; margin-bottom: 20px; font-size: 0.9rem; }

        input {
            width: 85%; padding: 12px; margin: 10px 0;
            border-radius: 8px; border: 1px solid #333;
            background: #0a0a0a; color: #fff; text-align: center; font-weight: bold;
        }

        button {
            width: 93%; padding: 12px; border: none;
            color: white; font-weight: bold; cursor: pointer;
            border-radius: 8px; transition: 0.3s; margin-top: 10px;
        }

        /* مربعات الستايل الفخم */
        .action-box {
            border: 1px solid #333; padding: 15px;
            margin-bottom: 15px; border-radius: 12px;
            background: rgba(20, 20, 20, 0.5);
        }

        .btn-add { background: linear-gradient(45deg, #004e92, #00d4ff); }
        .btn-remove { background: linear-gradient(45deg, #8b0000, #ff0000); }

        /* منطقة النتيجة المحمية */
        #result {
            margin-top: 20px; font-size: 1.5rem; font-weight: bold;
            padding: 10px; border-radius: 8px; display: none;
        }

        @keyframes zoomIn { from { transform: scale(0.5); opacity: 0; } to { transform: scale(1); opacity: 1; } }
    </style>
</head>
<body>

    <div class="volcano-bg"></div>
    <div class="snowflakes" id="snow"></div>

    <div id="loginPage" class="container active">
        <h1>WELCOME TO PANEL</h1>
        <h2 style="color:red">SBR TEAM</h2>
        <p class="sub-title">بقيادة SBR HAMA</p>
        <input type="text" id="adminUid" placeholder="ENTER YOUR UID">
        <input type="password" id="adminPass" placeholder="ENTER YOUR PASS">
        <button class="btn-add" style="background: #ff4500;" onclick="login()">دخول</button>
    </div>

    <div id="mainPage" class="container">
        <h1>WELCOME TO MY WEB</h1>
        <p class="sub-title">BY: SBR HAMA AND SBR TEAM</p>
        
        <div class="action-box">
            <p style="color:#00d4ff">إرسال بوت (ADD BOT)</p>
            <input type="text" id="targetAdd" placeholder="ID PLAYER">
            <input type="text" id="duration" placeholder="VALIDITY (DAYS)">
            <button class="btn-add" onclick="processBot('add')">ارسال / ENVOYER</button>
        </div>

        <div class="action-box">
            <p style="color:#ff0000">حذف بوت (REMOVE BOT)</p>
            <input type="text" id="targetRemove" placeholder="ID PLAYER">
            <button class="btn-remove" onclick="processBot('remove')">حذف / SUPPRIMER</button>
        </div>

        <div id="result"></div>
    </div>

    <script>
        // البيانات السرية
        const ADMIN_DATA = { uid: "SBR TEAM", pass: "SBR TEAM 90" };
        const GUEST_DATA = { uid: "4321909988", pass: "FAAFAE0BD428C3107A2A69E560B2F37395209F04A86BFA3508D0CD24291250B2" };

        function login() {
            const u = document.getElementById('adminUid').value;
            const p = document.getElementById('adminPass').value;
            if(u === ADMIN_DATA.uid && p === ADMIN_DATA.pass) {
                document.getElementById('loginPage').classList.remove('active');
                document.getElementById('mainPage').classList.add('active');
            } else { alert("ACCESS DENIED!"); }
        }

        async function processBot(mode) {
            const resDiv = document.getElementById('result');
            const targetId = mode === 'add' ? document.getElementById('targetAdd').value : document.getElementById('targetRemove').value;
            
            if(!targetId) { alert("ENTER ID!"); return; }

            resDiv.style.display = "block";
            resDiv.style.color = "#aaa";
            resDiv.innerHTML = "WAITING...";

            const apiBase = mode === 'add' ? 'adding_friend' : 'remove_friend';
            const url = `https://danger-add-friend.vercel.app/${apiBase}?uid=${GUEST_DATA.uid}&password=${GUEST_DATA.pass}&friend_uid=${targetId}`;

            try {
                const response = await fetch(url);
                // نحن لا نهتم بمحتوى الرد، طالما لم يحدث خطأ في الشبكة والسيرفر استجاب
                if(response.ok) {
                    resDiv.innerHTML = "SUCCESS ✅";
                    resDiv.style.color = "#00ff00";
                } else {
                    resDiv.innerHTML = "FAILED ❌";
                    resDiv.style.color = "#ff0000";
                }
            } catch (e) {
                resDiv.innerHTML = "FAILED ❌";
                resDiv.style.color = "#ff0000";
            }
        }

        // إنشاء الثلج
        function createSnow() {
            const snow = document.getElementById('snow');
            for(let i=0; i<40; i++) {
                let s = document.createElement('div');
                s.innerHTML = "❄";
                s.style.position = "absolute";
                s.style.left = Math.random() * 100 + "vw";
                s.style.top = "-20px";
                s.style.color = "#fff";
                s.style.opacity = Math.random();
                s.style.fontSize = (Math.random() * 10 + 10) + "px";
                s.style.animation = `fall ${Math.random()*4+3}s linear infinite`;
                snow.appendChild(s);
            }
        }
        const s = document.createElement('style');
        s.innerHTML = `@keyframes fall { to { transform: translateY(100vh); } }`;
        document.head.appendChild(s);
        createSnow();
    </script>
</body>
</html>
