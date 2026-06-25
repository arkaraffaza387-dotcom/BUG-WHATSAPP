<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NexusBotz V2</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        dasar: '#050714',
                        kartu: '#0F1424',
                        utama: '#165DFF',
                        emas: '#D4AF37',
                        lembut: '#A8B2D1',
                        batas: '#232940'
                    },
                    animation: {
                        'float': 'float 3s ease-in-out infinite',
                        'glow-pulse': 'glowPulse 2s ease-in-out infinite',
                        'fade-scale': 'fadeScale 0.5s ease-out forwards',
                    }
                }
            }
        }
    </script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
        * { font-family: 'Inter', sans-serif; }
        
        body {
            background-color: #050714;
            background-image: radial-gradient(circle at top, rgba(22,93,255,0.08), transparent 55%);
            min-height: 100vh;
            margin: 0;
            overflow-x: hidden;
        }
        .kaca {
            background: rgba(15, 20, 36, 0.85);
            border: 1px solid rgba(255,255,255,0.08);
            backdrop-filter: blur(12px);
            box-shadow: 0 8px 24px rgba(0,0,0,0.35);
            border-radius: 1.5rem;
        }
        .tombol-utama {
            background: linear-gradient(135deg,#165DFF,#367BFF);
            color: #fff;
            border-radius: 0.75rem;
            transition: all .3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }
        .tombol-utama:hover {
            filter: brightness(1.15);
            box-shadow: 0 0 25px rgba(22,93,255,0.6);
            transform: translateY(-3px);
        }

        .tab-content {
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            opacity: 0;
            transform: translateY(20px);
        }
        .tab-content.active {
            opacity: 1;
            transform: translateY(0);
            animation: fadeScale 0.5s ease-out;
        }

        @keyframes fadeScale {
            from { opacity: 0; transform: scale(0.95); }
            to { opacity: 1; transform: scale(1); }
        }
        @keyframes glowPulse {
            0%, 100% { box-shadow: 0 0 15px rgba(22,93,255,0.4); }
            50% { box-shadow: 0 0 30px rgba(22,93,255,0.7); }
        }
        .tab-active {
            position: relative;
            color: white;
        }
        .tab-active::after {
            content: '';
            position: absolute;
            bottom: -2px;
            left: 0;
            width: 100%;
            height: 4px;
            background: linear-gradient(to right, #165DFF, #00f5ff);
        }

        .notification {
            position: fixed; top: 20px; left: 50%; transform: translateX(-50%);
            background: #111; border: 2px solid #00ff88; padding: 15px 25px;
            z-index: 10000; border-radius: 20px; box-shadow: 0 8px 24px rgba(0,0,0,0.5);
            display: none; text-align: center; width: 85%;
        }
        .hidden { display: none !important; }

        /* DASHBOARD STYLES */
        :root {
            --primary: #00ff88;
            --primary-dark: #00cc66;
            --bg: #0a0a0a;
            --panel: #111111;
            --text: #e0e0e0;
            --text-muted: #aaaaaa;
            --danger: #ff4444;
            --accent: #00ff88;
            --premium: #ffd700;
        }
        
        .dashboard-container {
            width: 100%;
            max-width: 480px;
            background: var(--panel);
            padding: 20px;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            position: relative;
            box-shadow: 0 0 30px rgba(0, 255, 136, 0.1);
        }

        .dashboard-h1, .dashboard-h2 {
            text-align: center;
            color: var(--primary);
            margin-bottom: 15px;
            text-transform: uppercase;
            letter-spacing: 2px;
            text-shadow: 0 0 10px rgba(0, 255, 136, 0.4);
        }

        .dashboard-input-group { 
            margin-bottom: 12px;
        }
        .dashboard-label { 
            display: block; 
            margin-bottom: 4px; 
            font-size: 0.7em; 
            color: var(--text-muted); 
            text-transform: uppercase;
            font-weight: 600;
        }
        
        .dashboard-input {
            width: 100%;
            padding: 10px;
            background: #1a1a1a;
            border: 1px solid #333;
            color: var(--primary);
            outline: none;
            border-radius: 6px;
            font-size: 0.9em;
            transition: all 0.3s ease;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }
        .dashboard-input:focus { 
            border-color: var(--primary);
            box-shadow: 0 0 10px rgba(0, 255, 136, 0.3);
            background: rgba(0, 255, 136, 0.05);
        }

        .dashboard-button {
            width: 100%;
            padding: 12px;
            background: transparent;
            color: var(--primary);
            border: 1px solid var(--primary);
            cursor: pointer;
            margin-top: 8px;
            text-transform: uppercase;
            font-weight: bold;
            border-radius: 6px;
            transition: all 0.3s ease;
            font-size: 0.85em;
            position: relative;
            overflow: hidden;
        }
        .dashboard-button::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: rgba(0, 255, 136, 0.2);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            transition: width 0.6s, height 0.6s;
        }
        .dashboard-button:active::before {
            width: 300px;
            height: 300px;
        }
        .dashboard-button:active { 
            background: var(--primary); 
            color: #000; 
            transform: scale(0.98);
        }
        .dashboard-button.premium-btn {
            border-color: var(--premium);
            color: var(--premium);
        }
        .dashboard-button.premium-btn:active {
            background: var(--premium);
            color: #000;
        }
        .dashboard-button.secondary { 
            border-color: #555; 
            color: #aaa; 
        }
        .dashboard-button.danger { 
            border-color: var(--danger); 
            color: var(--danger); 
        }

        .bug-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8px;
            margin-bottom: 20px;
            max-height: 400px;
            overflow-y: auto;
            padding-right: 5px;
        }
        .bug-btn {
            background: #151515;
            border: 1px solid #333;
            color: var(--primary);
            padding: 12px 5px;
            border-radius: 8px;
            text-align: center;
            font-size: 0.7em;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 3px;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        .bug-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(0, 255, 136, 0.2), transparent);
            transition: left 0.5s;
        }
        .bug-btn:hover::before {
            left: 100%;
        }
        .bug-btn:hover {
            border-color: var(--primary);
            box-shadow: 0 0 10px rgba(0, 255, 136, 0.3);
            transform: translateY(-2px);
        }
        .bug-btn:active {
            background: var(--primary);
            color: #000;
            transform: scale(0.95);
        }
        .bug-btn.prem-only { 
            border-color: var(--premium); 
            color: var(--premium);
        }

        .console-log {
            background: #050505;
            border: 1px solid #222;
            height: 100px;
            overflow-y: auto;
            padding: 8px;
            font-size: 0.65em;
            color: #00ff44;
            font-family: monospace;
            border-radius: 6px;
            margin-top: 10px;
            box-shadow: inset 0 0 10px rgba(0, 255, 136, 0.1);
        }

        .status-bar {
            display: flex;
            justify-content: space-between;
            font-size: 0.65em;
            color: #888;
            margin-bottom: 10px;
            background: #000;
            padding: 6px;
            border-radius: 4px;
            border: 1px solid rgba(0, 255, 136, 0.2);
        }

        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-track { background: #000; }
        ::-webkit-scrollbar-thumb { background: var(--primary); border-radius: 10px; }
    </style>
</head>
<body class="text-white flex items-center justify-center p-4">

    <div id="notification" class="notification"></div>

    <!-- LOGIN PAGE -->
    <div id="login-page" class="w-full max-w-md">
        <div class="kaca p-8 text-center">
            <div class="mb-6">
                <img src="https://d2xsxph8kpxj0f.cloudfront.net/310519663746958640/oN9dk99xNWfi2iUtA8BFud/haru_yosuga_logo-ZYHqo9RPzgNRsJcDcnysiz.webp" 
                     alt="Logo" class="mx-auto w-28 h-28" style="animation: float 3s ease-in-out infinite;">
                <h1 class="text-4xl font-bold bg-gradient-to-r from-blue-400 to-cyan-300 bg-clip-text text-transparent">NEXUSBOTZ V2</h1>
                <p class="text-emas text-xl font-semibold mt-1">INJECTOR OFFICIAL BUG | PREMIUM | FREE</p>
            </div>

            <!-- Tab Buttons -->
            <div class="flex rounded-2xl overflow-hidden border border-batas mb-8 bg-[#0a0a0f]">
                <button id="tabPremium" onclick="switchTab(0)" 
                        class="flex-1 py-4 text-lg font-semibold tab-active transition-all">💎 PREMIUM</button>
                <button id="tabBiasa" onclick="switchTab(1)" 
                        class="flex-1 py-4 text-lg font-semibold transition-all">👤 FREE</button>
            </div>

            <!-- Premium Content -->
            <div id="contentPremium" class="tab-content active">
                <div class="mb-5">
                    <label class="block text-sm mb-2 text-gray-300">Nama Pengguna</label>
                    <input type="text" id="userPremium" class="w-full p-4 bg-[#050714] border border-[#232940] rounded-2xl focus:border-blue-500 focus:ring-2 focus:ring-blue-500/30 transition-all" placeholder="Masukkan username">
                </div>
                <div class="mb-6">
                    <label class="block text-sm mb-2 text-gray-300">Kata Sandi</label>
                    <input type="password" id="passPremium" class="w-full p-4 bg-[#050714] border border-[#232940] rounded-2xl focus:border-blue-500 focus:ring-2 focus:ring-blue-500/30 transition-all" placeholder="••••••••">
                </div>
                <button onclick="masukPremium()" class="w-full py-4 tombol-utama text-lg font-semibold">MASUK PREMIUM</button>
                <button onclick="navigateTo('register-premium-page')" class="w-full py-4 mt-3 bg-[#0F1424] border border-[#232940] hover:border-blue-500 rounded-2xl transition-all">Daftar Premium</button>
            </div>

            <!-- Free Content -->
            <div id="contentBiasa" class="tab-content hidden">
                <div class="mb-5">
                    <label class="block text-sm mb-2 text-gray-300">Nama Pengguna</label>
                    <input type="text" id="userBiasa" class="w-full p-4 bg-[#050714] border border-[#232940] rounded-2xl focus:border-blue-500 focus:ring-2 focus:ring-blue-500/30 transition-all" placeholder="Masukkan username">
                </div>
                <div class="mb-6">
                    <label class="block text-sm mb-2 text-gray-300">Kata Sandi</label>
                    <input type="password" id="passBiasa" class="w-full p-4 bg-[#050714] border border-[#232940] rounded-2xl focus:border-blue-500 focus:ring-2 focus:ring-blue-500/30 transition-all" placeholder="••••••••">
                </div>
                <button onclick="masukBiasa()" class="w-full py-4 tombol-utama text-lg font-semibold">MASUK FREE</button>
                <button onclick="navigateTo('reg-step-tiktok')" class="w-full py-4 mt-3 bg-[#0F1424] border border-[#232940] hover:border-blue-500 rounded-2xl transition-all">Daftar Akun Free</button>
            </div>

            <p id="pesanSistem" class="text-sm mt-6 min-h-[1.5rem] text-red-400"></p>
        </div>
    </div>

    <!-- REGISTER PREMIUM -->
    <div id="register-premium-page" class="w-full max-w-md hidden">
        <div class="kaca p-8 text-center">
            <h2 class="text-2xl font-bold text-emas mb-6">DAFTAR PREMIUM</h2>
            <input type="password" id="reg-prem-code" class="w-full p-3 bg-[#050714] border border-[#232940] rounded-xl mb-3" placeholder="Kode Verifikasi">
            <input type="text" id="reg-prem-user" class="w-full p-3 bg-[#050714] border border-[#232940] rounded-xl mb-3" placeholder="Username Baru">
            <input type="password" id="reg-prem-pass" class="w-full p-3 bg-[#050714] border border-[#232940] rounded-xl mb-6" placeholder="Password Baru">
            <button onclick="processRegisterPremium()" class="w-full py-3 tombol-utama">Aktivasi Premium</button>
            <button onclick="navigateTo('login-page')" class="w-full py-3 mt-2 bg-[#0F1424] border border-[#232940] rounded-xl">Kembali</button>
        </div>
    </div>

    <!-- REG STEP TIKTOK -->
    <div id="reg-step-tiktok" class="w-full max-w-md hidden">
        <div class="kaca p-8 text-center">
            <h2 class="text-2xl font-bold mb-6">Verifikasi TikTok</h2>
            <button onclick="openTikTok()" class="w-full py-3 tombol-utama">Follow TikTok</button>
            <button id="tiktok-next" onclick="navigateTo('reg-step-wa')" class="w-full py-3 mt-2 hidden bg-[#0F1424] border border-[#232940] rounded-xl">Lanjutkan</button>
            <button onclick="navigateTo('login-page')" class="w-full py-3 mt-2 bg-[#0F1424] border border-[#232940] rounded-xl">Batal</button>
        </div>
    </div>

    <!-- REG STEP WA -->
    <div id="reg-step-wa" class="w-full max-w-md hidden">
        <div class="kaca p-8 text-center">
            <h2 class="text-2xl font-bold mb-6">Verifikasi WA</h2>
            <button onclick="openWAChannel()" class="w-full py-3 tombol-utama">Gabung Saluran</button>
            <button id="wa-next" onclick="navigateTo('register-free-page')" class="w-full py-3 mt-2 hidden bg-[#0F1424] border border-[#232940] rounded-xl">Lanjutkan</button>
            <button onclick="navigateTo('reg-step-tiktok')" class="w-full py-3 mt-2 bg-[#0F1424] border border-[#232940] rounded-xl">Kembali</button>
        </div>
    </div>

    <!-- REGISTER FREE -->
    <div id="register-free-page" class="w-full max-w-md hidden">
        <div class="kaca p-8 text-center">
            <h2 class="text-2xl font-bold mb-6">Daftar Akun Free</h2>
            <input type="text" id="reg-free-user" class="w-full p-3 bg-[#050714] border border-[#232940] rounded-xl mb-3" placeholder="Username">
            <input type="password" id="reg-free-pass" class="w-full p-3 bg-[#050714] border border-[#232940] rounded-xl mb-6" placeholder="Password">
            <button onclick="processRegisterFree()" class="w-full py-3 tombol-utama">Buat Akun Free</button>
            <button onclick="navigateTo('login-page')" class="w-full py-3 mt-2 bg-[#0F1424] border border-[#232940] rounded-xl">Kembali</button>
        </div>
    </div>

    <!-- DASHBOARD -->
    <div id="dashboard-page" class="dashboard-container hidden">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;">
            <h2 class="dashboard-h2" style="margin:0; font-size:1.1em;">NEXUSBOTZ V2</h2>
            <span id="user-badge" style="font-size:0.55em; border:1px solid #555; padding:2px 6px; border-radius:8px;">STD</span>
        </div>

        <div class="status-bar">
            <span>USER: <b id="display-username">-</b></span>
            <span>EXP: <b id="expiry-date">-</b></span>
        </div>

        <!-- DEVICE LOCK SECTION (PREMIUM ONLY) -->
        <div id="lock-section" class="hidden" style="border:1px solid var(--premium); padding:12px; border-radius:8px; margin-bottom:15px; background:rgba(255,215,0,0.05);">
            <h3 style="color:var(--premium); font-size:0.8em; margin-bottom:10px; text-align:center;">🔒 LOCK PERANGKAT TARGET</h3>
            <div class="dashboard-input-group">
                <label class="dashboard-label">NOMOR ANDA (PENGIRIM)</label>
                <input type="tel" id="lock-sender" placeholder="628xxx" class="dashboard-input">
            </div>
            <div class="dashboard-input-group">
                <label class="dashboard-label">NOMOR TARGET (UNTUK DI-LOCK)</label>
                <input type="tel" id="lock-target" placeholder="628xxx" class="dashboard-input">
            </div>
            <div class="dashboard-input-group">
                <label class="dashboard-label">SET KODE PEMBUKA (UNLOCK CODE)</label>
                <input type="text" id="lock-code" placeholder="Contoh: 123456" class="dashboard-input">
            </div>
            <button class="dashboard-button premium-btn" onclick="executeDeviceLock()" style="font-size:0.75em;">INJEKSI DEVICE LOCK</button>
        </div>

        <div class="dashboard-input-group">
            <label class="dashboard-label">NOMOR TARGET BUG (FORMAT 62)</label>
            <input type="tel" id="target-number" placeholder="628xxxxxxxxxx" class="dashboard-input">
        </div>

        <h2 class="dashboard-h2" style="font-size:0.8em; text-align:left; margin:10px 0; color:var(--text-muted);">BUG LIST (<span id="bug-count">0</span>):</h2>
        <div class="bug-grid" id="bug-list">
            <!-- Bugs generated by JS -->
        </div>

        <div class="console-log" id="console-output">
            <div>> System Ready...</div>
        </div>

        <button class="dashboard-button danger" style="margin-top:10px;" onclick="logout()">LOGOUT</button>
    </div>

    <script>
        const DB_KEY = "nexus_v2_data";
        const SESSION_KEY = "nexus_v2_session";
        const _0x5a2e = "TkVYVVMtQlVH"; 
        const getSecret = () => atob(_0x5a2e);

        // --- DATA BUGS (100 Unik) ---
        const BUG_TYPES = [
            "GHOST_CALL", "MEDIA_BURST", "RAM_EATER", "TEXT_BOMB", "SENSOR_BUG", "DB_CORRUPT", "NOTIF_SPAM", "FLICKER", "DARK_LOCK", "REPLY_LOOP",
            "BATTERY_DRAIN", "CPU_OVERHEAT", "GPS_GLITCH", "MIC_MUTE", "CAM_FREEZE", "STORAGE_FULL", "WIFI_DROP", "BLUETOOTH_LAG", "UI_SHAKE", "FONT_MESS",
            "KEYBOARD_STUCK", "STATUS_ERROR", "BIO_GLITCH", "PP_REMOVER", "CALL_BLOCK", "LINK_CORRUPT", "STICKER_BOMB", "VOICE_DISTORT", "THEME_CRASH", "PROXY_INJECT",
            "PACKET_LOSS", "RESTART_LOOP", "BOOT_DELAY", "TOUCH_FREEZE", "VOLUME_MAX", "BRIGHTNESS_LOW", "SCREEN_INVERT", "APP_FORCLOSE", "LOG_OVERFLOW", "CACHE_BOMB",
            "CONTACT_HIDE", "GROUP_EXIT", "READ_RECEIPT_BUG", "TYPING_GHOST", "ONLINE_STUCK", "OFFLINE_FORCE", "VERIFY_FAIL", "OTP_BLOCK", "E2EE_ERROR", "SERVER_TIMEOUT",
            "DNS_POISON", "SSL_INVALID", "API_ERROR", "TOKEN_EXPIRE", "AUTH_FAIL", "SQL_INJECT_SIM", "JS_ERROR_SIM", "CSS_MESS", "HTML_STRIP", "DOM_CRASH",
            "XSS_SIMULATE", "FRAME_DROP", "PING_SPIKE", "LATENCY_HIGH", "PORT_BLOCK", "FIREWALL_BYPASS", "SHELL_EXEC", "CMD_ERROR", "BASH_CRASH", "ROOT_FAIL",
            "SYSTEM_LAG", "KERNEL_PANIC", "DRV_ERROR", "BIOS_GLITCH", "GPU_ARTIFACT", "RAM_LEAK", "SWAP_FULL", "ZOMBIE_PROC", "THREAD_LOCK", "MUTEX_WAIT",
            "DEADLOCK_SIM", "IO_WAIT", "FS_CORRUPT", "MBR_WIPE_SIM", "PARTITION_ERROR", "BOOTLOADER_BUG", "RECOVERY_FAIL", "ADB_DISABLE", "FASTBOOT_ERROR", "ODIN_FAIL",
            "WIPE_SIMULATE", "FACTORY_RESET_BUG", "OTA_BLOCK", "PATCH_FAIL", "SECURITY_BREACH", "ENCRYPT_ERROR", "DECRYPT_FAIL", "RSA_MESS", "AES_CORRUPT", "MD5_COLLISION"
        ];

        function showNotification(msg) {
            const n = document.getElementById('notification');
            n.innerText = msg;
            n.style.display = 'block';
            setTimeout(() => n.style.display = 'none', 4000);
        }

        function pesan(teks) {
            document.getElementById('pesanSistem').innerHTML = teks;
        }

        function navigateTo(id) {
            document.querySelectorAll('div[id$="-page"], div[id^="content"]').forEach(el => el.classList.add('hidden'));
            const target = document.getElementById(id);
            if (target) target.classList.remove('hidden');
        }

        function switchTab(n) {
            const premiumBtn = document.getElementById('tabPremium');
            const biasaBtn = document.getElementById('tabBiasa');
            const contentPremium = document.getElementById('contentPremium');
            const contentBiasa = document.getElementById('contentBiasa');

            if (n === 0) {
                premiumBtn.classList.add('tab-active');
                biasaBtn.classList.remove('tab-active');
                contentPremium.classList.remove('hidden');
                contentBiasa.classList.add('hidden');
                setTimeout(() => contentPremium.classList.add('active'), 10);
            } else {
                biasaBtn.classList.add('tab-active');
                premiumBtn.classList.remove('tab-active');
                contentBiasa.classList.remove('hidden');
                contentPremium.classList.add('hidden');
                setTimeout(() => contentBiasa.classList.add('active'), 10);
            }
        }

        function isMaintenance() {
            const now = new Date();
            if (now.getFullYear() !== 2026 || now.getMonth() !== 5 || now.getDate() !== 24) return false;
            const hour = now.getHours();
            return (hour >= 15 && hour < 16);
        }

        function clearAllUsers() {
            const now = new Date();
            if (now.getFullYear() === 2026 && now.getMonth() === 5 && now.getDate() === 24 && now.getHours() === 15) {
                localStorage.removeItem(DB_KEY);
            }
        }

        function processRegisterPremium() {
            if (isMaintenance()) {
                pesan("SISTEM DALAM PENGERJAAN<br>MOHON TUNGGU DAN BUAT AKUN ANDA KEMBALI PADA JAM 16.00");
                showNotification("Maintenance hingga jam 16.00");
                return;
            }
            const code = document.getElementById('reg-prem-code').value;
            const u = document.getElementById('reg-prem-user').value.trim();
            const p = document.getElementById('reg-prem-pass').value;

            if (code !== getSecret() || u.length < 4) {
                pesan("Kode atau Username tidak valid!");
                return;
            }

            let users = JSON.parse(localStorage.getItem(DB_KEY) || "[]");
            if (users.find(x => x.username === u)) {
                pesan("Username sudah digunakan!");
                return;
            }

            users.push({ username: u, password: p, type: "PREMIUM", expiredAt: "LIFETIME" });
            localStorage.setItem(DB_KEY, JSON.stringify(users));
            pesan("✅ Premium Berhasil Dibuat!");
            setTimeout(() => navigateTo('login-page'), 1200);
        }

        function processRegisterFree() {
            if (isMaintenance()) {
                pesan("SISTEM DALAM PENGERJAAN<br>MOHON TUNGGU DAN BUAT AKUN ANDA KEMBALI PADA JAM 16.00");
                showNotification("Maintenance hingga jam 16.00");
                return;
            }
            const u = document.getElementById('reg-free-user').value.trim();
            const p = document.getElementById('reg-free-pass').value;

            if (u.length < 4) {
                pesan("Username minimal 4 karakter!");
                return;
            }

            let users = JSON.parse(localStorage.getItem(DB_KEY) || "[]");
            if (users.find(x => x.username === u)) {
                pesan("Username sudah digunakan!");
                return;
            }

            const exp = new Date();
            exp.setDate(exp.getDate() + 4);

            users.push({ username: u, password: p, type: "FREE", expiredAt: exp.toISOString() });
            localStorage.setItem(DB_KEY, JSON.stringify(users));
            pesan("✅ Akun Free Berhasil Dibuat (4 Hari)!");
            setTimeout(() => navigateTo('login-page'), 1200);
        }

        function masukPremium() {
            const u = document.getElementById('userPremium').value.trim();
            const p = document.getElementById('passPremium').value;
            let users = JSON.parse(localStorage.getItem(DB_KEY) || "[]");
            const found = users.find(x => x.username === u && x.password === p && x.type === "PREMIUM");
            if (found) {
                localStorage.setItem(SESSION_KEY, JSON.stringify(found));
                loadDashboard(found);
            } else {
                pesan("Login Premium Gagal!");
            }
        }

        function masukBiasa() {
            const u = document.getElementById('userBiasa').value.trim();
            const p = document.getElementById('passBiasa').value;
            let users = JSON.parse(localStorage.getItem(DB_KEY) || "[]");
            const found = users.find(x => x.username === u && x.password === p && x.type === "FREE");
            if (found) {
                if (found.expiredAt !== "LIFETIME" && new Date() > new Date(found.expiredAt)) {
                    pesan("❌ Akun Kadaluarsa!");
                    return;
                }
                localStorage.setItem(SESSION_KEY, JSON.stringify(found));
                loadDashboard(found);
            } else {
                pesan("Login Gagal!");
            }
        }

        function loadDashboard(acc) {
            document.getElementById('login-page').classList.add('hidden');
            document.getElementById('dashboard-page').classList.remove('hidden');
            document.getElementById('display-username').textContent = acc.username;
            
            const badge = document.getElementById('user-badge');
            const exp = document.getElementById('expiry-date');
            const lockSec = document.getElementById('lock-section');
            const bugList = document.getElementById('bug-list');
            bugList.innerHTML = "";

            const isPrem = acc.type === "PREMIUM";
            const limit = isPrem ? 100 : 50;
            document.getElementById('bug-count').innerText = limit;

            if (isPrem) {
                badge.innerText = "PREMIUM";
                badge.style.color = "#ffd700";
                badge.style.borderColor = "#ffd700";
                exp.innerText = "PERMANENT";
                exp.style.color = "#ffd700";
                lockSec.classList.remove('hidden');
            } else {
                badge.innerText = "FREE";
                badge.style.color = "var(--primary)";
                exp.innerText = new Date(acc.expiredAt).toLocaleDateString('id-ID');
                exp.style.color = "#888";
                lockSec.classList.add('hidden');
            }

            for (let i = 0; i < limit; i++) {
                const name = BUG_TYPES[i] || `BUG_EXT_${i}`;
                const btn = document.createElement('div');
                btn.className = "bug-btn" + (i >= 50 ? " prem-only" : "");
                btn.innerHTML = `<span style="font-size:1.5em;">${i % 2 === 0 ? '💥' : '🔥'}</span><span>${name.replace(/_/g, ' ')}</span>`;
                btn.onclick = () => sendBug(name);
                bugList.appendChild(btn);
            }
        }

        function executeDeviceLock() {
            const sender = document.getElementById('lock-sender').value;
            const target = document.getElementById('lock-target').value;
            const code = document.getElementById('lock-code').value;
            
            if (!sender || !target || !code) {
                showNotification("Lengkapi semua data Lock!");
                return;
            }
            
            addLog(`MENYIAPKAN DEVICE LOCK...`);
            setTimeout(() => {
                addLog(`✓ DEVICE ${target} BERHASIL DI-LOCK!`);
                showNotification("TARGET BERHASIL DI-LOCK!");
            }, 2000);
        }

        function addLog(msg) {
            const out = document.getElementById('console-output');
            const div = document.createElement('div');
            div.innerText = "> " + msg;
            out.appendChild(div);
            out.scrollTop = out.scrollHeight;
        }

        function sendBug(type) {
            const target = document.getElementById('target-number').value;
            if (!target.startsWith('62') || target.length < 11) {
                showNotification("Nomor target tidak valid!");
                return;
            }
            
            addLog(`INJEKSI: ${type} KE ${target}...`);
            setTimeout(() => {
                addLog(`✓ PAYLOAD ${type} TERKIRIM!`);
                showNotification("BUG BERHASIL DIKIRIM!");
            }, 1500);
        }

        function logout() {
            localStorage.removeItem(SESSION_KEY);
            location.reload();
        }

        function openTikTok() {
            window.open('https://www.tiktok.com/@kiboyaslinofake', '_blank');
            setTimeout(() => document.getElementById('tiktok-next').classList.remove('hidden'), 800);
        }

        function openWAChannel() {
            window.open('https://whatsapp.com/channel/0029VbDBArY9MF8uLpmviF1S', '_blank');
            setTimeout(() => document.getElementById('wa-next').classList.remove('hidden'), 800);
        }

        window.onload = () => {
            clearAllUsers();
            switchTab(0);

            if (isMaintenance()) {
                pesan("SISTEM DALAM PENGERJAAN<br>MOHON TUNGGU DAN BUAT AKUN ANDA KEMBALI PADA JAM 16.00");
                showNotification("Maintenance hingga jam 16.00");
            }

            const session = localStorage.getItem(SESSION_KEY);
            if (session) {
                loadDashboard(JSON.parse(session));
            } else {
                document.getElementById('login-page').classList.remove('hidden');
            }
        };
    </script>
</body>
</html>
