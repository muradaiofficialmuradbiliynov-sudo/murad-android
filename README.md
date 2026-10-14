<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MURAD OS - Voice Launcher</title>
    <style>
        body {
            background-color: #0d021a;
            color: #00ffcc;
            font-family: 'Courier New', Courier, monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            border: 2px solid #a100ff;
            box-shadow: 0 0 15px #a100ff;
            padding: 25px;
            border-radius: 12px;
            text-align: center;
            width: 85%;
            max-width: 400px;
            background: rgba(13, 2, 26, 0.9);
        }
        h1 {
            color: #fff;
            text-shadow: 0 0 8px #a100ff;
            margin-bottom: 5px;
        }
        .status {
            color: #00ff00;
            font-size: 0.85em;
            margin-bottom: 15px;
        }
        .terminal {
            background: #000;
            border: 1px solid #00ffcc;
            padding: 10px;
            height: 160px;
            overflow-y: auto;
            text-align: left;
            font-size: 0.8em;
            margin-bottom: 15px;
            border-radius: 5px;
        }
        button {
            background: #a100ff;
            color: white;
            border: none;
            padding: 12px 20px;
            font-size: 0.95em;
            font-weight: bold;
            border-radius: 8px;
            cursor: pointer;
            box-shadow: 0 0 10px #a100ff;
            width: 100%;
        }
        button:active {
            transform: scale(0.98);
        }
    </style>
</head>
<body>

<div class="container">
    <h1>MURAD OS</h1>
    <div class="status">[ VOICE LAUNCHER ACTIVE ]</div>

    <div class="terminal" id="terminal">
        > Murad OS Launcher initialized...<br>
        > Press 'LISTEN' and speak.<br>
    </div>

    <button onclick="startListening()">🎤 DINLE / KOMUT VER</button>
</div>

<script>
    const terminal = document.getElementById('terminal');

    function log(text) {
        terminal.innerHTML += `> ${text}<br>`;
        terminal.scrollTop = terminal.scrollHeight;
    }

    function startListening() {
        const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;

        if (!SpeechRecognition) {
            log("Hata: Tarayıcınız ses tanımayı desteklemiyor.");
            return;
        }

        const recognition = new SpeechRecognition();
        recognition.lang = 'tr-TR'; // Türkçe ses tanıma

        log("Dinleniyor... Konuşun.");

        recognition.onresult = function(event) {
            const command = event.results[0][0].transcript.toLowerCase();
            log(`Algılandı: "${command}"`);
            executeCommand(command);
        };

        recognition.onerror = function(event) {
            log("Ses Hatası: " + event.error);
        };

        recognition.start();
    }

    function executeCommand(cmd) {
        if (cmd.includes("instagram")) {
            log("Instagram açılıyor...");
            setTimeout(() => { window.location.href = "https://instagram.com"; }, 1000);
        } else if (cmd.includes("youtube")) {
            log("YouTube açılıyor...");
            setTimeout(() => { window.location.href = "https://youtube.com"; }, 1000);
        } else if (cmd.includes("tiktok")) {
            log("TikTok açılıyor...");
            setTimeout(() => { window.location.href = "https://tiktok.com"; }, 1000);
        } else if (cmd.includes("sistem") || cmd.includes("durum")) {
            log("Sistem durumu: %100 Çalışıyor. Murad OS Hazır.");
        } else {
            log("Komut anlaşılamadı. Şunları deneyin: 'Instagram', 'TikTok', 'YouTube', 'Sistem'.");
        }
    }
</script>

</body>
</html>
