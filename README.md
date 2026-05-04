# AURA-AI<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Zenith AI</title>
    <style>
        /* --- 1. CLEAN & PEACEFUL DESIGN (PORTRAIT) --- */
        * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        
        body { 
            font-family: 'Segoe UI', sans-serif; 
            background-color: #ffffff; 
            height: 100vh; 
            display: flex; 
            flex-direction: column;
            overflow: hidden; /* Sidha phone ke liye lock */
        }

        /* --- 2. HEADER & GLOWING ICON --- */
        .header { 
            padding: 15px 20px; 
            display: flex; 
            justify-content: space-between; 
            align-items: center; 
            border-bottom: 1px solid #f1f5f9;
            background: white;
        }
        
        .logo { font-weight: bold; color: #0284c7; font-size: 20px; display: flex; align-items: center; gap: 8px; }
        
        /* FEATURE: GLOWING AI ICON */
        .ai-glow { 
            width: 10px; height: 10px; background: #0284c7; border-radius: 50%; 
            box-shadow: 0 0 8px #0284c7; animation: pulse 2s infinite; 
        }
        @keyframes pulse { 0% { opacity: 0.5; } 50% { opacity: 1; } 100% { opacity: 0.5; } }

        .menu-btn { font-size: 22px; background: none; border: none; cursor: pointer; color: #64748b; }

        /* --- 3. CHAT DISPLAY --- */
        #chat-container { flex: 1; padding: 20px; overflow-y: auto; display: flex; flex-direction: column; gap: 15px; }
        .ai-msg { background: #f0f9ff; padding: 12px 16px; border-radius: 18px 18px 18px 5px; max-width: 85%; align-self: flex-start; color: #334155; font-size: 15px; }
        .user-msg { background: #0284c7; color: white; padding: 12px 16px; border-radius: 18px 18px 5px 18px; max-width: 85%; align-self: flex-end; font-size: 15px; }

        /* --- 4. INPUT SECTION --- */
        .input-box { padding: 15px; display: flex; gap: 10px; background: white; border-top: 1px solid #f1f5f9; }
        input { flex: 1; border: 1px solid #e2e8f0; border-radius: 25px; padding: 12px 20px; outline: none; font-size: 16px; background: #f8fafc; }
        #send-btn { background: #0284c7; color: white; width: 45px; height: 45px; border-radius: 50%; border: none; font-size: 18px; }

        /* --- 5. SETTINGS PANEL (SIDEBAR) --- */
        .settings-panel {
            position: fixed; top: 0; right: -100%; width: 75%; height: 100%; 
            background: white; box-shadow: -5px 0 15px rgba(0,0,0,0.1);
            transition: 0.3s; z-index: 200; padding: 40px 20px;
        }
        .settings-panel.open { right: 0; }
        .settings-item { padding: 15px 0; border-bottom: 1px solid #f1f5f9; color: #334155; font-size: 16px; list-style: none; cursor: pointer; }
        .close-btn { position: absolute; top: 15px; left: 15px; font-size: 28px; color: #64748b; cursor: pointer; }
    </style>
</head>
<body>

    <header class="header">
        <div class="logo"><div class="ai-glow"></div> Zenith AI</div>
        <button class="menu-btn" onclick="toggleMenu()">☰</button>
    </header>

    <!-- Sidebar Settings -->
    <div id="settings" class="settings-panel">
        <div class="close-btn" onclick="toggleMenu()">×</div>
        <h2 style="margin-bottom: 25px; color: #0284c7;">Settings</h2>
        <li class="settings-item" onclick="newChat()">➕ New Chat</li>
        <li class="settings-item" onclick="deleteHistory()">🗑️ Delete All Chats</li>
        <li class="settings-item" onclick="alert('Privacy Policy: Your data stays on your phone. Zenith AI does not store your chats.')">🛡️ Privacy Policy</li>
    </div>

    <main id="chat-container">
        <div class="ai-msg">🕊️ Swagat hai! Main Zenith AI hoon. Ekdam fresh aur saaf chatting ke liye taiyaar?</div>
    </main>

    <div class="input-box">
        <input type="text" id="user-input" placeholder="Message Zenith AI..." autocomplete="off">
        <button id="send-btn" onclick="sendMessage()">➤</button>
    </div>

    <script>
        function toggleMenu() { document.getElementById('settings').classList.toggle('open'); }

        function sendMessage() {
            const input = document.getElementById('user-input');
            const container = document.getElementById('chat-container');
            if (input.value.trim()) {
                // User message
                const uMsg = document.createElement('div');
                uMsg.className = 'user-msg';
                uMsg.innerText = input.value;
                container.appendChild(uMsg);

                // AI Response
                setTimeout(() => {
                    const aMsg = document.createElement('div');
                    aMsg.className = 'ai-msg';
                    aMsg.innerText = "Zenith AI is processing... 🕊️";
                    container.appendChild(aMsg);
                    container.scrollTop = container.scrollHeight;
                }, 700);

                input.value = "";
                container.scrollTop = container.scrollHeight;
            }
        }

        function newChat() {
            if(confirm("Nayi chat shuru karein?")) {
                document.getElementById('chat-container').innerHTML = '<div class="ai-msg">Nayi shuruat! Main aapki kaise madad kar sakta hoon?</div>';
                toggleMenu();
            }
        }

        function deleteHistory() {
            if(confirm("Saari history mita dein?")) {
                localStorage.clear();
                location.reload();
            }
        }

        // Enter key support
        document.getElementById('user-input').addEventListener("keypress", (e) => {
            if (e.key === "Enter") sendMessage();
        });
    </script>
</body>
</html>
