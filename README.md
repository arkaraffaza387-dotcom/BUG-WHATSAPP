<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WhatsApp Bug Tool</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #1a1a2e, #16213e);
            margin: 0;
            padding: 0;
            color: #fff;
            min-height: 100vh;
        }
        .container {
            max-width: 1100px;
            margin: 20px auto;
            padding: 30px;
            background: rgba(0, 0, 0, 0.9);
            border-radius: 20px;
            box-shadow: 0 0 40px rgba(0, 255, 136, 0.3);
        }
        h1 { text-align: center; margin-bottom: 10px; }
        .premium-header {
            color: #ffd700;
            font-size: 2.5em;
            text-shadow: 0 0 20px #ffd700;
        }
        button {
            width: 100%;
            padding: 16px;
            margin: 6px 0;
            border: none;
            border-radius: 12px;
            font-weight: bold;
            font-size: 16px;
            cursor: pointer;
        }
        .bug-btn {
            background: linear-gradient(145deg, #1e1e2f, #2a2a45);
            border: 1px solid #ffd700;
        }
        .bug-btn:hover {
            background: linear-gradient(145deg, #2a2a45, #3a3a60);
            transform: translateY(-3px);
        }
        input {
            width: 100%;
            padding: 15px;
            margin: 15px 0;
            border-radius: 10px;
            border: 2px solid #ffd700;
            background: rgba(0,0,0,0.7);
            color: white;
            font-size: 16px;
        }
        .error { color: #ff4444; text-align: center; margin: 15px 0; }
        .result { margin: 15px 0; padding: 15px; border-radius: 10px; text-align: center; font-weight: bold; }
        .channel-btn { background: linear-gradient(#25D366, #128C7E); color: white; }
    </style>
</head>
<body>
    <div class="container">
        <!-- LOGIN PAGE -->
        <div id="loginForm">
            <h1>WhatsApp Bug Tool</h1>
            <input type="text" id="username" placeholder="Username">
            <input type="password" id="password" placeholder="Password">
            <button onclick="login()" style="background: #00ff88; color: #000;">Login</button>
            <button onclick="openForm()" class="channel-btn">📢 CREATE AKUN ANDA SEKARANG 100% GRATIS</button>
            <div id="error" class="error"></div>
        </div>

        <!-- FREE PAGE -->
        <div id="freePage" style="display: none;">
            <h1>WhatsApp Bug Tool - Free</h1>
            <button onclick="sendBug()">📤 Send Bug</button>
            <button onclick="forclose()">🔒 Forclose</button>
            <button onclick="ultraLag()">⚡ Ultra Lag</button>
            <button onclick="superLag()">💥 Super Lag</button>
            <button onclick="freeze()">❄️ Freeze Account</button>
            <button onclick="crash()">💣 Crash WhatsApp</button>

            <div style="margin-top: 25px;">
                <label>Target Number (WA):</label>
                <input type="text" id="freeTarget" placeholder="+628xxxxxxxxxx">
            </div>
            <button onclick="logout()" style="background:#ff4444;">Logout</button>
            <div id="freeResult" class="result"></div>
        </div>

        <!-- PREMIUM PAGE (50 BUGS) -->
        <div id="premiumPage" style="display: none;">
            <h1 class="premium-header">🚀 BUG PREMIUM MODE</h1>
            <p style="text-align:center; color:#ffd700;" id="premiumStatus"></p>

            <div style="margin-bottom: 20px;">
                <label>Target Number (WA):</label>
                <input type="text" id="premiumTarget" placeholder="+628xxxxxxxxxx">
            </div>

            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 12px;" id="premiumGrid"></div>

            <button onclick="logout()" style="background:#ff4444; margin-top: 25px;">Logout</button>
            <div id="premiumResult" class="result"></div>
        </div>
    </div>

    <script>
        const allowedUsers = [
            { username: "PRIVATE", password: "PRIVATE", premium: false },
            { username: "AZFER.ID", password: "AZFER.ID", premium: true, premiumExpiresAt: null },   // Unlimited
            // Password diubah dari PRIVATE_AZFER menjadi PRIVATE2
            { username: "PRIVATE2", password: "PRIVATE2", premium: true, premiumExpiresAt: "2026-05-25T03:00:00" }, 
            { username: "PRIVATE3", password: "PRIVATE3", premium: false }
        ];

        let currentUser = null;

        function login() {
            const username = document.getElementById('username').value.trim();
            const password = document.getElementById('password').value.trim();
            const errorEl = document.getElementById('error');

            errorEl.textContent = "";

            const user = allowedUsers.find(u => u.username === username && u.password === password);

            if (!user) {
                errorEl.textContent = "PASSWORD ATAU USERNAME ANDA SALAH MASUKAN YANG BENAR";
                return;
            }

            // Cek kadaluarsa Premium
            if (user.premium && user.premiumExpiresAt) {
                if (new Date(user.premiumExpiresAt) < new Date()) {
                    errorEl.textContent = "Premium Anda telah kadaluarsa!";
                    return;
                }
            }

            currentUser = user;
            document.getElementById('loginForm').style.display = 'none';

            if (user.premium) {
                document.getElementById('premiumPage').style.display = 'block';
                generatePremiumBugs();
                updatePremiumStatus();
            } else {
                document.getElementById('freePage').style.display = 'block';
            }
        }

        function updatePremiumStatus() {
            const el = document.getElementById('premiumStatus');
            if (currentUser.premiumExpiresAt === null) {
                el.innerHTML = "✅ Premium Unlimited (Tak Terbatas)";
            } else {
                const date = new Date(currentUser.premiumExpiresAt);
                el.innerHTML = `⚠️ Premium aktif sampai: ${date.toLocaleString('id-ID')}`;
            }
        }

        function openForm() {
            window.open("https://forms.gle/8xJRC7XRgEaPFwpu5", "_blank");
        }

        function logout() {
            location.reload();
        }

        function checkTarget(id) {
            const target = document.getElementById(id).value.trim();
            if (!target) {
                alert("MOHON ISI NO WHATSAPP YANG INI DI BUG JIKA KOSONG BUG TIDAK BISA TERKIRIM");
                return false;
            }
            return true;
        }

        // ==================== FREE FUNCTIONS ====================
        function freeResult(text) {
            document.getElementById('freeResult').innerHTML = `✅ ${text}`;
        }
        function sendBug() { if(checkTarget('freeTarget')) freeResult("Send Bug Terkirim"); }
        function forclose() { if(checkTarget('freeTarget')) freeResult("Forclose Terkirim"); }
        function ultraLag() { if(checkTarget('freeTarget')) freeResult("Ultra Lag Terkirim"); }
        function superLag() { if(checkTarget('freeTarget')) freeResult("Super Lag Terkirim"); }
        function freeze() { if(checkTarget('freeTarget')) freeResult("Freeze Account Terkirim"); }
        function crash() { if(checkTarget('freeTarget')) freeResult("Crash WhatsApp Terkirim"); }
        function logoutAll() { if(checkTarget('freeTarget')) freeResult("Logout All Device Terkirim"); }
        function banAccount() { if(checkTarget('freeTarget')) freeResult("Ban Account Terkirim"); }

        // ==================== PREMIUM 50 BUGS ====================
        const premiumBugList = [
            "Super Ultimate Lag","Nuclear Crash","Permanent Ban","Account Destroyer",
            "Freeze Forever","Infinite Loop","Ghost Mode","Device Overheat","Mass Logout",
            "Chat Exploder","Media Bomber","Status Killer","Call Crash","Group Destroyer",
            "Number Blocker","Virus Injector","Premium Forclose","Ultra Freeze","System Killer",
            "Data Eraser","WhatsApp Killer","Blue Screen","Lag Machine","Account Hacker Pro",
            "Mass Report","Ban Wave","Session Hijack","OTP Bomber","Profile Destroyer",
            "Link Crash","Sticker Bomb","Voice Crash","Video Killer","Document Destroyer",
            "Location Bomber","Poll Crasher","Reaction Spam","Mention All Crash","Admin Remover",
            "Group Expander","Anti-Delete","Message Flooder","Hidden Ban","Silent Crash",
            "Deep Freeze","Quantum Lag","Black Hole","Ultimate Destroyer","God Mode Bug",
            "Premium Virus X"
        ];

        function generatePremiumBugs() {
            const grid = document.getElementById('premiumGrid');
            grid.innerHTML = '';
            premiumBugList.forEach(bug => {
                const btn = document.createElement('button');
                btn.className = 'bug-btn';
                btn.textContent = bug;
                btn.onclick = () => sendPremiumBug(bug);
                grid.appendChild(btn);
            });
        }

        function sendPremiumBug(bugName) {
            if (!checkTarget('premiumTarget')) return;
            const target = document.getElementById('premiumTarget').value.trim();
            document.getElementById('premiumResult').innerHTML = `🚀 ${bugName} berhasil dikirim ke ${target}`;
        }
    </script>
</body>
</html>

