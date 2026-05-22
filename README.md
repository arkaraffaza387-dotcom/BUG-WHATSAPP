<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WhatsApp Bug Tool - Private Access</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #1a1a2e, #16213e);
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: #fff;
        }
        .container {
            background: rgba(0, 0, 0, 0.85);
            padding: 35px;
            border-radius: 15px;
            box-shadow: 0 0 30px rgba(0, 255, 136, 0.3);
            width: 400px;
            text-align: center;
        }
        h1 {
            color: #00ff88;
            text-shadow: 0 0 15px #00ff88;
            margin-bottom: 25px;
        }
        .form-group {
            margin-bottom: 20px;
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
            padding: 14px;
            border: 2px solid #00ff88;
            border-radius: 8px;
            background: rgba(0, 0, 0, 0.7);
            color: white;
            font-size: 16px;
        }
        button {
            width: 100%;
            padding: 13px;
            background: linear-gradient(135deg, #00ff88, #00cc66);
            color: #000;
            border: none;
            border-radius: 8px;
            font-weight: bold;
            font-size: 15px;
            cursor: pointer;
            margin: 6px 0;
        }
        button:hover {
            background: linear-gradient(135deg, #00cc66, #00ff88);
        }
        .error { color: #ff4444; margin-top: 15px; font-weight: bold; min-height: 30px; }
        .success { color: #00ff88; margin-top: 10px; font-weight: bold; }
        .info { color: #ffee00; margin-top: 15px; font-size: 0.95em; }
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
            <button onclick="clearSavedLogin()" class="clear-btn">Hapus Data Login Tersimpan</button>
            <div id="error" class="error"></div>
        </div>

        <!-- BUG TOOL -->
        <div id="bugTool" style="display: none;">
            <h1>WhatsApp Bug Tool</h1>
            
            <div class="form-group">
                <label>Target Number:</label>
                <input type="text" id="targetNumber" placeholder="+628xxxxxxxxxx">
            </div>
            <div class="form-group">
                <label>Message (Opsional):</label>
                <input type="text" id="message" placeholder="Pesan bug">
            </div>

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
            
            <button onclick="logout()" style="background: #ff4444; margin-top: 15px;">Logout</button>
            
            <div id="bugResult" class="success"></div>
            <div id="expiryInfo" class="info"></div>
        </div>
    </div>

    <script>
        const allowedUsers = [
            { username: "PRIVATE", password: "PRIVATE", expiresAt: "2026-05-23T00:00:00" },
            { username: "AZFER.ID", password: "AZFER.ID", expiresAt: null },
            { username: "PRIVATE2", password: "PRIVATE_AZFER", expiresAt: "2026-05-24T18:00:00" }   // Diubah sesuai permintaan
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

            localStorage.setItem('whatsappBugLogin', JSON.stringify({
                username: username,
                expiresAt: user.expiresAt
            }));

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
                infoEl.innerHTML = `✅ <strong>${data.username}</strong> - Permanent Account`;
            } else {
                const expiryDate = new Date(data.expiresAt);
                infoEl.innerHTML = `⚠️ <strong>${data.username}</strong> - Kadaluarsa: ${expiryDate.toLocaleString('id-ID')}`;
            }
        }

        function logout() {
            localStorage.removeItem('whatsappBugLogin');
            location.reload();
        }

        function clearSavedLogin() {
            localStorage.removeItem('whatsappBugLogin');
            alert("✅ Data login tersimpan telah dihapus.");
            location.reload();
        }

        // Bug Functions
        function sendBug() { trigger("Send Bug", "berhasil dikirim"); }
        function forclose() { trigger("Forclose", "telah ditutup paksa"); }
        function ultraLag() { trigger("Ultra Lag", "ultra lag berat"); }
        function superLag() { trigger("Super Lag", "super lag ekstrem"); }
        function freeze() { trigger("Freeze Account", "terfreeze"); }
        function crash() { trigger("Crash WhatsApp", "crash"); }
        function logoutAll() { trigger("Logout All Device", "semua device logout"); }
        function banAccount() { trigger("Ban Account", "akun di-ban"); }
        function virus() { trigger("Virus Spread", "virus menyebar"); }
        function infinite() { trigger("Infinite Message", "pesan tak berhenti"); }

        function trigger(type, status) {
            const target = document.getElementById('targetNumber').value || "-";
            document.getElementById('bugResult').textContent = `${type} → ${target}`;
            setTimeout(() => alert(`${type} berhasil dikirim ke ${target}\nStatus: ${status}`), 700);
        }

        window.onload = function() {};
    </script>
</body>
</html>
