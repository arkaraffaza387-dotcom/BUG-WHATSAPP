<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sedang Dalam Perbaikan</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #f0f0f0; /* Warna latar belakang abu-abu muda */
            font-family: Arial, sans-serif;
            text-align: center;
        }

        .container {
            padding: 20px;
            max-width: 800px;
        }

        .pesan-getar {
            color: red; /* Tulisan berwarna merah */
            font-size: 24px; /* Ukuran huruf */
            font-weight: bold; /* Tebal */
            line-height: 1.5;
            
            /* Animasi getar */
            animation: getar 0.5s infinite;
        }

        /* Definisi animasi getar */
        @keyframes getar {
            0% { transform: translate(1px, 1px) rotate(0deg); }
            10% { transform: translate(-1px, -2px) rotate(-1deg); }
            20% { transform: translate(-3px, 0px) rotate(1deg); }
            30% { transform: translate(3px, 2px) rotate(0deg); }
            40% { transform: translate(1px, -1px) rotate(1deg); }
            50% { transform: translate(-1px, 2px) rotate(-1deg); }
            60% { transform: translate(-3px, 1px) rotate(0deg); }
            70% { transform: translate(3px, 1px) rotate(-1deg); }
            80% { transform: translate(-1px, -1px) rotate(1deg); }
            90% { transform: translate(1px, 2px) rotate(0deg); }
            100% { transform: translate(1px, -2px) rotate(-1deg); }
        }

        /* Agar tampilan rapi di HP */
        @media (max-width: 600px) {
            .pesan-getar {
                font-size: 18px;
            }
        }
    </style>
</head>
<body>

    <div class="container">
        <p class="pesan-getar">
            SERVER WEBSITE SEDANG DI PERBARUI<br>
            MOHON TUNGGU SEBENTAR<br>
            ATAU CHAT ADMIN KAMI BERIKUT NOMORNYA<br>
            0858-8238-2854
        </p>
    </div>

</body>
</html>

