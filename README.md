# HTML concept AIOS created by gemeni
try this now
source code
# version
yooo V4.5 CREATOR ENGINE
# functionality
can making apps control your "system"imeges make doucumets and idk
# WEBSITE
<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>aiOS 4.5 - Ultimate Creator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&family=Fira+Code:wght@400;500&family=Playfair+Display:ital@0;1&family=Montserrat:wght@400;700&family=Roboto+Slab:wght@400;700&display=swap');

        :root {
            --glass: rgba(15, 23, 42, 0.85);
            --glass-border: rgba(255, 255, 255, 0.1);
            --accent: #6366f1; 
        }

        body, html {
            margin: 0; padding: 0;
            font-family: 'Inter', sans-serif;
            height: 100vh; width: 100vw;
            overflow: hidden; background: #020617; color: white;
            background-image: radial-gradient(circle at 50% 50%, #1e1b4b, #020617);
        }

        /* Desktop Layout */
        .desktop {
            position: relative; height: 100vh; width: 100vw; padding: 60px 30px;
            display: grid; grid-template-columns: repeat(auto-fill, 110px);
            grid-template-rows: repeat(auto-fill, 120px); gap: 20px; grid-auto-flow: column;
        }

        .shortcut {
            display: flex; flex-direction: column; align-items: center; gap: 8px;
            width: 100px; cursor: pointer; padding: 12px; border-radius: 18px;
            transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
            user-select: none;
        }

        .shortcut:hover { background: rgba(255, 255, 255, 0.1); transform: scale(1.05); }

        .icon-container {
            width: 60px; height: 60px; display: flex; align-items: center; justify-content: center;
            font-size: 30px; border-radius: 16px; background: rgba(255,255,255,0.03);
            border: 1px solid var(--glass-border); box-shadow: 0 10px 25px rgba(0,0,0,0.4);
            overflow: hidden; pointer-events: none;
        }

        .label { font-size: 11px; font-weight: 500; text-align: center; text-shadow: 0 2px 4px rgba(0,0,0,0.6); }

        /* Window System */
        .window {
            position: absolute; background: var(--glass); backdrop-filter: blur(45px);
            border: 1px solid var(--glass-border); border-radius: 22px;
            display: none; flex-direction: column; z-index: 100;
            box-shadow: 0 40px 80px rgba(0,0,0,0.8); overflow: hidden;
            min-width: 250px; min-height: 180px;
        }

        .window-header {
            height: 48px; background: rgba(255, 255, 255, 0.04);
            display: flex; align-items: center; padding: 0 18px; cursor: move;
            border-bottom: 1px solid rgba(255,255,255,0.05); flex-shrink: 0;
            user-select: none;
        }

        .dot { width: 12px; height: 12px; border-radius: 50%; margin-right: 8px; cursor: pointer; transition: 0.2s; }
        .dot:hover { transform: scale(1.2); }
        .dot-close { background: #ff5f57; }
        .dot-min { background: #febc2e; }

        /* Resizer Handle */
        .resizer {
            width: 20px; height: 20px;
            position: absolute; right: 0; bottom: 0;
            cursor: nwse-resize;
            background: linear-gradient(135deg, transparent 70%, rgba(255,255,255,0.2) 70%);
            border-bottom-right-radius: 22px;
            z-index: 1001;
        }

        /* Dock */
        .dock {
            position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%);
            display: flex; gap: 12px; padding: 10px; background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(35px); border: 1px solid var(--glass-border);
            border-radius: 24px; z-index: 9000;
        }

        .dock-item {
            width: 52px; height: 52px; display: flex; align-items: center; justify-content: center;
            font-size: 26px; border-radius: 15px; background: rgba(255,255,255,0.05);
            cursor: pointer; transition: 0.3s cubic-bezier(0.18, 0.89, 0.32, 1.28);
        }

        .dock-item:hover { transform: translateY(-12px) scale(1.1); background: var(--accent); }

        .toolbar {
            padding: 10px 15px; background: rgba(255,255,255,0.03);
            display: flex; gap: 12px; align-items: center; border-bottom: 1px solid rgba(255,255,255,0.05);
            flex-wrap: wrap; flex-shrink: 0;
        }

        .status-bar {
            position: fixed; top: 0; width: 100%; height: 35px;
            background: rgba(0,0,0,0.3); backdrop-filter: blur(15px);
            display: flex; justify-content: space-between; align-items: center;
            padding: 0 20px; font-size: 11px; z-index: 10000; border-bottom: 1px solid rgba(255,255,255,0.05);
        }

        /* Message Styles */
        .chat-messages { flex-grow: 1; overflow-y: auto; padding: 20px; display: flex; flex-direction: column; gap: 10px; }
        .msg { max-width: 85%; padding: 10px 15px; border-radius: 15px; font-size: 13px; line-height: 1.4; word-wrap: break-word; }
        .msg-ai { background: rgba(255,255,255,0.08); align-self: flex-start; border-bottom-left-radius: 4px; }
        .msg-user { background: var(--accent); align-self: flex-end; border-bottom-right-radius: 4px; }

        /* Scrollbar */
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.1); border-radius: 10px; }
        ::-webkit-scrollbar-thumb:hover { background: rgba(255,255,255,0.2); }
    </style>
</head>
<body>

    <div class="status-bar">
        <div class="flex gap-5 items-center">
            <span class="font-bold tracking-widest">aiOS 4.5</span>
            <span class="opacity-40">System: Online</span>
        </div>
        <div id="clock" class="font-mono">00:00:00</div>
    </div>

    <div class="desktop" id="desktop">
        <div class="shortcut" onclick="openWin('omni')">
            <div class="icon-container">🧠</div>
            <div class="label">Ядро ШІ</div>
        </div>
        <div class="shortcut" onclick="openWin('forge')">
            <div class="icon-container">🛠️</div>
            <div class="label">Кузня</div>
        </div>
        <div class="shortcut" onclick="openWin('word')">
            <div class="icon-container">📘</div>
            <div class="label">AI Word</div>
        </div>
        <div class="shortcut" onclick="openWin('explorer')">
            <div class="icon-container">📂</div>
            <div class="label">Провідник</div>
        </div>
        <div class="shortcut" onclick="openWin('settings')">
            <div class="icon-container">⚙️</div>
            <div class="label">Налаштування</div>
        </div>
    </div>

    <!-- WINDOW: OMNI AI -->
    <div class="window" id="window-omni" style="width: 450px; height: 550px; top: 60px; left: 40px; display: flex;">
        <div class="window-header">
            <div class="dot dot-close" onclick="closeWin('omni')"></div>
            <span class="text-[10px] font-bold opacity-50 ml-2 tracking-widest uppercase">System Intelligence</span>
        </div>
        <div class="flex flex-col h-full overflow-hidden">
            <div class="chat-messages" id="omniChat">
                <div class="msg msg-ai">Привіт. Я — Ядро системи. Я можу змінювати візуал, створювати нові програми або редагувати файли. Наказуй.</div>
            </div>
            <div class="p-4 border-t border-white/5 flex gap-2">
                <input type="text" id="omniInput" class="flex-grow bg-white/5 border border-white/10 rounded-xl p-3 text-xs outline-none focus:border-indigo-500/50 transition" placeholder="Напишіть наказ..." onkeypress="if(event.key==='Enter')omniExecute()">
                <button onclick="omniExecute()" class="bg-indigo-600 hover:bg-indigo-500 px-4 rounded-xl font-bold transition">📡</button>
            </div>
        </div>
        <div class="resizer"></div>
    </div>

    <!-- WINDOW: APP FORGE -->
    <div class="window" id="window-forge" style="width: 500px; height: 550px; top: 100px; left: 120px;">
        <div class="window-header">
            <div class="dot dot-close" onclick="closeWin('forge')"></div>
            <span class="text-[10px] font-bold opacity-50 ml-2 tracking-widest uppercase">App Forge</span>
        </div>
        <div class="p-6 space-y-4 overflow-y-auto h-full pb-10">
            <h2 class="text-xl font-bold">Програмна Кузня</h2>
            <p class="text-xs opacity-50">Створіть власний додаток, просто описавши його логіку.</p>
            <input type="text" id="forgeName" class="w-full bg-white/5 border border-white/10 rounded-xl p-4 text-sm outline-none focus:border-blue-500/50" placeholder="Назва вашої програми">
            <textarea id="forgeLogic" class="w-full bg-white/5 border border-white/10 rounded-xl p-4 text-sm h-32 outline-none resize-none focus:border-blue-500/50" placeholder="Опишіть, що має робити програма (наприклад: калькулятор калорій)..."></textarea>
            <div class="flex gap-2">
                <input type="text" id="forgeIconPrompt" class="flex-grow bg-white/5 border border-white/10 rounded-xl p-3 text-xs outline-none" placeholder="Стиль іконки (напр. '3D вогонь')">
                <button onclick="forgeGenerateIcon()" class="bg-purple-600 hover:bg-purple-500 px-4 rounded-xl text-xs transition">Іконка</button>
            </div>
            <div id="forgeIconPreview" class="hidden justify-center items-center py-2"><div id="forgeIconRes" class="w-20 h-20 rounded-2xl border border-white/20 overflow-hidden shadow-lg"></div></div>
            <button onclick="forgeBuildApp()" id="forgeBtn" class="w-full bg-blue-600 p-4 rounded-xl font-bold hover:bg-blue-500 shadow-xl shadow-blue-900/20 transition active:scale-95">СКУВАТИ ПРОГРАМУ</button>
        </div>
        <div class="resizer"></div>
    </div>

    <!-- WINDOW: AI WORD -->
    <div class="window" id="window-word" style="width: 700px; height: 600px; top: 80px; left: 350px;">
        <div class="window-header">
            <div class="dot dot-close" onclick="closeWin('word')"></div>
            <span class="text-[10px] font-bold opacity-50 ml-2 tracking-widest uppercase">AI Word Processor</span>
        </div>
        <div class="toolbar">
            <select id="wordFont" class="bg-white/10 border border-white/10 rounded px-3 py-1 text-[11px] outline-none hover:bg-white/20 transition" onchange="wordUpdateStyle()">
                <option value="Inter">Inter (Sans)</option>
                <option value="'Playfair Display'">Playfair (Serif)</option>
                <option value="'Fira Code'">Fira (Mono)</option>
                <option value="Montserrat">Montserrat</option>
                <option value="'Roboto Slab'">Roboto Slab</option>
            </select>
            <div class="h-4 w-[1px] bg-white/10 mx-1"></div>
            <button onclick="wordAI('fix')" class="bg-emerald-600/20 hover:bg-emerald-600 px-3 py-1 rounded-lg text-[10px] transition">Виправити помилки</button>
            <button onclick="wordAI('continue')" class="bg-blue-600/20 hover:bg-blue-600 px-3 py-1 rounded-lg text-[10px] transition">Продовжити</button>
        </div>
        <textarea id="wordArea" class="w-full flex-grow bg-transparent p-12 outline-none text-base leading-relaxed resize-none font-light" placeholder="Почніть писати свою історію..."></textarea>
        <div class="resizer"></div>
    </div>

    <!-- WINDOW: EXPLORER -->
    <div class="window" id="window-explorer" style="width: 480px; height: 350px; top: 220px; left: 550px;">
        <div class="window-header">
            <div class="dot dot-close" onclick="closeWin('explorer')"></div>
            <span class="text-[10px] font-bold opacity-50 ml-2 uppercase tracking-widest">File Explorer</span>
        </div>
        <div class="p-6 grid grid-cols-4 gap-4 overflow-y-auto" id="fileGrid">
            <div class="flex flex-col items-center gap-1 group cursor-pointer">
                <span class="text-4xl transition group-hover:scale-110">📄</span>
                <span class="text-[9px] opacity-60">system.log</span>
            </div>
            <div class="flex flex-col items-center gap-1 group cursor-pointer">
                <span class="text-4xl transition group-hover:scale-110">⚙️</span>
                <span class="text-[9px] opacity-60">config.json</span>
            </div>
        </div>
        <div class="resizer"></div>
    </div>

    <!-- WINDOW: SETTINGS -->
    <div class="window" id="window-settings" style="width: 400px; height: 450px; top: 180px; left: 250px;">
        <div class="window-header">
            <div class="dot dot-close" onclick="closeWin('settings')"></div>
            <span class="text-[10px] font-bold opacity-50 ml-2 uppercase tracking-widest">Settings</span>
        </div>
        <div class="p-8 space-y-8 h-full overflow-y-auto">
            <section>
                <label class="text-[10px] uppercase opacity-40 font-bold block mb-4 tracking-widest">Персоналізація</label>
                <div class="flex gap-4">
                    <div class="w-10 h-10 rounded-full bg-indigo-600 cursor-pointer hover:scale-110 transition border-2 border-transparent" id="color-indigo" onclick="setAccent('#6366f1')"></div>
                    <div class="w-10 h-10 rounded-full bg-emerald-600 cursor-pointer hover:scale-110 transition" id="color-emerald" onclick="setAccent('#10b981')"></div>
                    <div class="w-10 h-10 rounded-full bg-rose-600 cursor-pointer hover:scale-110 transition" id="color-rose" onclick="setAccent('#e11d48')"></div>
                    <div class="w-10 h-10 rounded-full bg-amber-600 cursor-pointer hover:scale-110 transition" id="color-amber" onclick="setAccent('#d97706')"></div>
                </div>
            </section>
            <section class="space-y-4">
                <label class="text-[10px] uppercase opacity-40 font-bold block tracking-widest">Система</label>
                <div class="bg-white/5 p-4 rounded-2xl flex justify-between items-center">
                    <span class="text-xs">Версія ядра</span>
                    <span class="text-xs opacity-50 font-mono">4.5.2-stable</span>
                </div>
                <button class="w-full bg-white/5 hover:bg-white/10 p-4 rounded-2xl text-xs text-left transition" onclick="location.reload()">Перезавантажити aiOS</button>
            </section>
        </div>
        <div class="resizer"></div>
    </div>

    <div class="dock">
        <div class="dock-item" onclick="openWin('omni')">🧠</div>
        <div class="dock-item" onclick="openWin('forge')">🛠️</div>
        <div class="dock-item" onclick="openWin('word')">📘</div>
        <div class="dock-item" onclick="openWin('explorer')">📂</div>
        <div class="dock-item" onclick="openWin('settings')">⚙️</div>
    </div>

    <script>
        const apiKey = ""; // API ключ вставляється середовищем виконання
        let highestZ = 1000;
        let lastForgeIcon = null;

        // --- Core ---
        function openWin(id) {
            const w = document.getElementById('window-' + id);
            w.style.display = 'flex';
            w.style.zIndex = ++highestZ;
        }
        function closeWin(id) { document.getElementById('window-' + id).style.display = 'none'; }
        
        function setAccent(color) {
            document.documentElement.style.setProperty('--accent', color);
            // Візуальний зворотний зв'язок у налаштуваннях
            document.querySelectorAll('[id^="color-"]').forEach(el => el.style.borderColor = 'transparent');
            const active = document.querySelector(`[onclick*="${color}"]`);
            if(active) active.style.borderColor = 'white';
        }

        async function gemini(prompt, system) {
            const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`;
            try {
                const res = await fetch(url, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: prompt }] }],
                        systemInstruction: { parts: [{ text: system }] }
                    })
                });
                const data = await res.json();
                return data.candidates[0].content.parts[0].text;
            } catch(e) { return "Помилка зв'язку з Ядром. Перевірте з'єднання."; }
        }

        // --- Omni AI ---
        async function omniExecute() {
            const input = document.getElementById('omniInput');
            const chat = document.getElementById('omniChat');
            const cmd = input.value;
            if(!cmd) return;

            const uMsg = document.createElement('div');
            uMsg.className = "msg msg-user";
            uMsg.innerText = cmd;
            chat.appendChild(uMsg);
            input.value = "";

            const aiRes = await gemini(cmd, `You are the OS Brain of aiOS 4.5.
            If user asks to change theme color, respond ONLY with JSON: {"type": "color", "hex": "#..."}.
            If user asks to create an app, respond ONLY with JSON: {"type": "app", "name": "...", "code": "..."}.
            Otherwise, reply as a helpful system assistant in Ukrainian.`);

            try {
                const action = JSON.parse(aiRes);
                if(action.type === 'color') {
                    setAccent(action.hex);
                    addAiMsg("Системну палітру оновлено відповідно до ваших вподобань.");
                } else if(action.type === 'app') {
                    createAppShortcut(action.name, action.code, "🧩");
                    addAiMsg(`Додаток "${action.name}" успішно скомпільовано та встановлено.`);
                }
            } catch(e) { addAiMsg(aiRes); }
            chat.scrollTop = chat.scrollHeight;
        }

        function addAiMsg(txt) {
            const chat = document.getElementById('omniChat');
            const m = document.createElement('div');
            m.className = "msg msg-ai shadow-sm";
            m.innerText = txt;
            chat.appendChild(m);
        }

        // --- Forge ---
        async function forgeGenerateIcon() {
            const prompt = document.getElementById('forgeIconPrompt').value;
            if(!prompt) return;
            try {
                const res = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/imagen-4.0-generate-001:predict?key=${apiKey}`, {
                    method: 'POST',
                    body: JSON.stringify({ instances: { prompt: "Minimalistic app icon, " + prompt }, parameters: { sampleCount: 1 } })
                });
                const data = await res.json();
                lastForgeIcon = `data:image/png;base64,${data.predictions[0].bytesBase64Encoded}`;
                document.getElementById('forgeIconRes').innerHTML = `<img src="${lastForgeIcon}" class="w-full h-full object-cover">`;
                document.getElementById('forgeIconPreview').style.display = 'flex';
            } catch(e) { alert("Помилка генерації іконки."); }
        }

        async function forgeBuildApp() {
            const name = document.getElementById('forgeName').value;
            const logic = document.getElementById('forgeLogic').value;
            if(!name || !logic) return;
            const btn = document.getElementById('forgeBtn');
            btn.innerText = "СИНТЕЗ КОДУ..."; btn.disabled = true;
            
            const code = await gemini(`Create a functional single-file web app. Logic: ${logic}. Use Tailwind CSS for modern dark/light UI. Return ONLY pure HTML.`, "Master Software Engineer.");
            const cleanCode = code.replace(/```html|```/g, "").trim();
            
            createAppShortcut(name, cleanCode, lastForgeIcon || "🚀");
            btn.innerText = "СКУВАТИ ПРОГРАМУ"; btn.disabled = false;
            closeWin('forge');
        }

        function createAppShortcut(name, code, icon) {
            const id = "custom_" + Date.now();
            const div = document.createElement('div');
            div.className = "shortcut";
            const iconContent = (typeof icon === 'string' && icon.startsWith('data')) ? `<img src="${icon}" class="w-full h-full object-cover">` : icon;
            div.innerHTML = `<div class="icon-container">${iconContent}</div><div class="label">${name}</div>`;
            div.onclick = () => {
                let win = document.getElementById('window-' + id);
                if(!win) {
                    win = document.createElement('div');
                    win.id = 'window-' + id;
                    win.className = "window";
                    win.style.width = "600px"; win.style.height = "500px";
                    win.style.top = "100px"; win.style.left = "150px";
                    win.style.display = "flex"; win.style.zIndex = ++highestZ;
                    win.innerHTML = `<div class="window-header"><div class="dot dot-close" onclick="this.closest('.window').remove()"></div><span class="text-xs ml-2 font-bold">${name}</span></div>
                                     <iframe class="w-full h-full bg-white border-none" srcdoc='${code.replace(/'/g, "&apos;")}'></iframe><div class="resizer"></div>`;
                    document.body.appendChild(win);
                    initWinEvents(win);
                } else { win.style.display = 'flex'; win.style.zIndex = ++highestZ; }
            };
            document.getElementById('desktop').appendChild(div);
        }

        // --- Word ---
        function wordUpdateStyle() {
            document.getElementById('wordArea').style.fontFamily = document.getElementById('wordFont').value;
        }
        async function wordAI(type) {
            const area = document.getElementById('wordArea');
            if(!area.value) return;
            const res = await gemini((type === 'fix' ? "Fix spelling/grammar: " : "Continue this creative text: ") + area.value, "Expert Editor.");
            if(type === 'fix') area.value = res; else area.value += " " + res;
        }

        // --- Window Systems ---
        function initWinEvents(win) {
            const header = win.querySelector('.window-header');
            const resizer = win.querySelector('.resizer');

            header.onmousedown = (e) => {
                win.style.zIndex = ++highestZ;
                let sx = e.clientX - win.offsetLeft;
                let sy = e.clientY - win.offsetTop;
                document.onmousemove = (ev) => {
                    win.style.left = ev.clientX - sx + 'px';
                    win.style.top = ev.clientY - sy + 'px';
                };
                document.onmouseup = () => document.onmousemove = null;
            };

            resizer.onmousedown = (e) => {
                e.preventDefault();
                win.style.zIndex = ++highestZ;
                let startX = e.clientX; let startY = e.clientY;
                let startW = win.offsetWidth; let startH = win.offsetHeight;
                document.onmousemove = (ev) => {
                    let nw = startW + (ev.clientX - startX);
                    let nh = startH + (ev.clientY - startY);
                    if(nw > 250) win.style.width = nw + 'px';
                    if(nh > 180) win.style.height = nh + 'px';
                };
                document.onmouseup = () => document.onmousemove = null;
            };
        }

        document.querySelectorAll('.window').forEach(initWinEvents);
        setInterval(() => {
            document.getElementById('clock').innerText = new Date().toLocaleTimeString('uk-UA');
        }, 1000);
        
        // Initial feedback
        console.log("aiOS 4.5 Ultimate Creator initialized.");
    </script>
</body>
</html>
