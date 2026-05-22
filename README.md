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
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            color: #fff;
        }
        .container {
            background: rgba(0, 0, 0, 0.9);
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 0 30px rgba(0, 255, 136, 0.3);
            width: 100%;
            max-width: 420px;
            text-align: center;
        }
        h1 {
            color: #00ff88;
            text-shadow: 0 0 15px #00ff88;
            margin-bottom: 25px;
        }
        .form-group {
            margin-bottom: 15px;
            text-align: left;
        }
        label {
            display: block;
            margin-bottom: 8px;
            color: #00ff88;
            font-weight: bold;
        }
        input {
            width: 100%;
            padding: 15px;
            border: 2px solid #00ff88;
            border-radius: 8px;
            background: rgba(0, 0, 0, 0.7);
            color: white;
            font-size: 16px;
        }
        button {
            width: 100%;
            padding: 16px;
            background: linear-gradient(135deg, #00ff88, #00cc66);
            color: #000;
            border: none;
            border-radius: 10px;
            font-weight: bold;
            font-size: 16px;
            cursor: pointer;
            margin: 8px 0;
        }
        button:hover {
            background: linear-gradient(135deg, #00cc66, #00ff88);
        }
        .error { 
            color: #ff4444; 
            margin: 15px 0; 
            font-weight: bold; 
            min-height: 28px;
        }
        .success { 
            color: #00ff88; 
            margin: 15px 0; 
            font-weight: bold; 
        }
        .info { 
            color: #ffee00; 
            margin-top: 20px; 
            font-size: 0.95em; 
        }
        .clear-btn {
            background: #ff4444 !important;
            color: white;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>WhatsApp Bug Tool</h1>
        
        <!-- LOGIN FORM -->
        <div id="loginForm">
            <div class="form-group">
                <label>Username:</label>
                <input type="text" id="username" placeholder="Masukkan username">
            </div>
            <div class="form-group">
                <label>Password:</label>
                <input type="password" id="password" placeholder="Masukkan password">
            </div>
            <button onclick="login()">Login</button>
            <button onclick="clearSavedLogin()" class="clear-btn">Hapus Data Login</button>
            <div id="error" class="error"></div>
        </div>

        <!-- BUG TOOL -->
        <div id="bugTool" style="display: none;">
            <h1>WhatsApp Bug Tool</h1>
            
            <!-- Menu Bug -->
            <button onclick="sendBug()">📤 Send Bug</button>
            <button onclick="forclose()">🔒 Forclose</button>
            <button onclick="ultraLag()">⚡ Ultra Lag</button>
            <button onclick="superLag()">💥 Super Lag</button>
            <button onclick="freeze()">❄️ Freeze Account</button>
            <button onclick="crash()">💣 Crash WhatsApp</button>
            <button onclick="logoutAll()">🚪 Logout All Device</button>
            <button onclick="banAccount()">🚫 Ban Account</button>
            <button onclick="virus()">☣️ Virus Spread</button>
            <button onclick="infinite()">♾️ Infinite Message</button>
            <button onclick="deleteChat()">🗑️ Delete Chat</button>
            <button onclick="blockReport()">🚫 Block & Report</button>
            <button onclick="accountHacker()">🔓 Account Hacker</button>
            <button onclick="massMessage()">📨 Mass Message</button>

            <!-- No WA di paling bawah -->
            <div class="form-group" style="margin-top: 25px;">
                <label>Target Number (WA):</label>
                <input type="text" id="targetNumber" placeholder="+628xxxxxxxxxx">
            </div>

            <button onclick="logout()" style="background: #ff4444; margin-top: 10px;">Logout</button>
            
            <div id="bugResult" class="success"></div>
            <div id="expiryInfo" class="info"></div>
        </div>
    </div>

    <script>
        const allowedUsers = [
            { username: "PRIVATE", password: "PRIVATE", expiresAt: "2026-05-23T00:00:00" },
            { username: "AZFER.ID", password: "AZFER.ID", expiresAt: null },
            { username: "PRIVATE2", password: "PRIVATE_AZFER", expiresAt: "2026-05-24T18:00:00" },
            { username: "PRIVATE3", password: "PRIVATE3", expiresAt: "2026-06-01T00:00:00" }
        ];

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

            if (user.expiresAt && new Date(user.expiresAt) < new Date()) {
                errorEl.textContent = "Akun ini sudah kadaluarsa!";
                return;
            }

            localStorage.setItem('whatsappBugLogin', JSON.stringify({ username, expiresAt: user.expiresAt }));

            document.getElementById('loginForm').style.display = 'none';
            document.getElementById('bugTool').style.display = 'block';
            updateExpiryInfo();
        }

        function updateExpiryInfo() {
            const infoEl = document.getElementById('expiryInfo');
            const saved = localStorage.getItem('whatsappBugLogin');
            if (!saved) return;
            const data = JSON.parse(saved);
            
            if (data.expiresAt === null) {
                infoEl.innerHTML = `✅ <strong>${data.username}</strong> - Permanent`;
            } else {
                const date = new Date(data.expiresAt);
                infoEl.innerHTML = `⚠️ <strong>${data.username}</strong> - Kadaluarsa: ${date.toLocaleString('id-ID')}`;
            }
        }

        function logout() {
            localStorage.removeItem('whatsappBugLogin');
            location.reload();
        }

        function clearSavedLogin() {
            localStorage.removeItem('whatsappBugLogin');
            alert("Data login telah dihapus.");
            location.reload();
        }

        // Validasi No WA
        function checkTargetNumber() {
            const target = document.getElementById('targetNumber').value.trim();
            if (!target) {
                document.getElementById('bugResult').style.color = "#ff4444";
                document.getElementById('bugResult').textContent = "MOHON ISI NO WHATSAPP YANG INI DI BUG JIKA KOSONG BUG TIDAK BISA TERKIRIM";
                return false;
            }
            return true;
        }

        function trigger(type, status) {
            const target = document.getElementById('targetNumber').value.trim();
            document.getElementById('bugResult').style.color = "#00ff88";
            document.getElementById('bugResult').textContent = `${type} → ${target}`;
            setTimeout(() => {
                alert(`${type} berhasil ke ${target}\nStatus: ${status}`);
            }, 600);
        }

        // Bug Functions
        function sendBug() { if(checkTargetNumber()) trigger("Send Bug", "berhasil dikirim"); }
        function forclose() { if(checkTargetNumber()) trigger("Forclose", "telah ditutup"); }
        function ultraLag() { if(checkTargetNumber()) trigger("Ultra Lag", "ultra lag"); }
        function superLag() { if(checkTargetNumber()) trigger("Super Lag", "super lag"); }
        function freeze() { if(checkTargetNumber()) trigger("Freeze", "terfreeze"); }
        function crash() { if(checkTargetNumber()) trigger("Crash", "crash"); }
        function logoutAll() { if(checkTargetNumber()) trigger("Logout All", "logout semua device"); }
        function banAccount() { if(checkTargetNumber()) trigger("Ban Account", "akun di-ban"); }
        function virus() { if(checkTargetNumber()) trigger("Virus", "virus menyebar"); }
        function infinite() { if(checkTargetNumber()) trigger("Infinite", "pesan infinite"); }
        function deleteChat() { if(checkTargetNumber()) trigger("Delete Chat", "chat dihapus"); }
        function blockReport() { if(checkTargetNumber()) trigger("Block & Report", "diblokir"); }
        function accountHacker() { if(checkTargetNumber()) trigger("Account Hacker", "di-hack"); }
        function massMessage() { if(checkTargetNumber()) trigger("Mass Message", "massal terkirim"); }

        window.onload = function() {};
    </script>
</body>
</html>
