# Al-HAKABA
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>الحقيبة المهدوية - الإصدار الشامل</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Amiri:wght@400;700&display=swap');
        
        :root {
            --primary: #064e3b; 
            --accent: #fbbf24;  
            --glass: rgba(255, 255, 255, 0.95);
        }

        body {
            margin: 0; padding: 0;
            font-family: 'Amiri', serif;
            background: url('https://images.unsplash.com/photo-1564769662533-4f00a87b4056?q=80&w=1000') no-repeat center center fixed;
            background-size: cover;
            color: #1a1a1a;
        }

        .overlay { background: rgba(0, 20, 10, 0.7); min-height: 100vh; padding: 10px; position: relative; padding-bottom: 80px; }
        .app-container { max-width: 480px; margin: 0 auto; }

        .event-banner {
            background: linear-gradient(90deg, #92400e, #b91c1c);
            color: white; padding: 10px; text-align: center; border-radius: 10px;
            margin-bottom: 10px; font-weight: bold; cursor: pointer;
            box-shadow: 0 4px 10px rgba(0,0,0,0.3); display: none;
        }

        .card {
            background: var(--glass); border-radius: 25px;
            margin-bottom: 15px; padding: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5); border-top: 5px solid var(--accent);
        }

        header h1 { color: white; margin: 0; font-size: 2.2rem; text-shadow: 2px 2px 10px rgba(0,0,0,1); text-align: center; }

        .prayer-row { display: flex; justify-content: space-around; text-align: center; padding: 10px 0; }
        .prayer-row div b { font-size: 1.4rem; color: var(--primary); display: block; }

        /* أزرار اختيار التسبيح */
        .tasbih-selector { display: flex; gap: 8px; margin-bottom: 15px; }
        .mode-btn { flex: 1; padding: 10px; border-radius: 15px; border: 2px solid var(--primary); background: white; color: var(--primary); font-weight: bold; cursor: pointer; font-family: inherit; }
        .mode-btn.active { background: var(--primary); color: white; }

        #counter { font-size: 7rem; font-weight: bold; color: var(--primary); margin: 5px 0; line-height: 1; text-align: center; }
        
        .tap-circle {
            width: 160px; height: 160px;
            background: radial-gradient(circle, var(--primary), #012b21);
            border-radius: 50%; margin: 15px auto;
            display: flex; align-items: center; justify-content: center;
            color: white; font-size: 1.8rem; cursor: pointer;
            border: 8px solid #f0fdf4; transition: 0.1s;
            box-shadow: 0 10px 25px rgba(0,0,0,0.6);
        }
        .tap-circle:active { transform: scale(0.9); }

        .audio-player { 
            background: #fef3c7; border-radius: 15px; padding: 12px; margin-bottom: 15px; 
            display: flex; flex-direction: column; align-items: center; border: 1px solid var(--accent); 
        }
        
        .play-btn { 
            background: var(--primary); color: white; border: none; 
            width: 50px; height: 50px; border-radius: 50%; cursor: pointer;
            font-size: 1.2rem; display: flex; align-items: center; justify-content: center;
        }

        .scroll-content { height: 180px; overflow-y: auto; padding: 15px; background: #fff; border-radius: 15px; line-height: 2.2; font-size: 1.25rem; border: 1px solid #ddd; }
        
        .tabs { display: flex; gap: 8px; margin-bottom: 10px; overflow-x: auto; }
        .tab { background: #eee; border: none; padding: 8px 18px; border-radius: 20px; cursor: pointer; white-space: nowrap; font-family: inherit; font-weight: bold; }
        .tab.active { background: var(--primary); color: white; }

        /* التذييل والحقوق */
        footer { text-align: center; color: white; padding: 20px 10px; font-size: 0.95rem; line-height: 1.6; }
        .copy-accent { color: var(--accent); font-weight: bold; }

        .modal {
            display: none; position: fixed; z-index: 1000; left: 0; top: 0; width: 100%; height: 100%;
            background-color: rgba(0,0,0,0.8);
        }
        .modal-content {
            background-color: white; margin: 15% auto; padding: 20px; border-radius: 20px; width: 85%; max-width: 400px;
        }
        .event-list-item { border-bottom: 1px solid #eee; padding: 10px 0; display: flex; justify-content: space-between; font-weight: bold; }
        .event-list-item span { color: var(--primary); }
        .btn-close { background: var(--primary); color: white; border: none; padding: 10px 20px; border-radius: 10px; width: 100%; margin-top: 15px; cursor: pointer; }
    </style>
</head>
<body>

<div class="overlay">
    <div class="app-container">
        
        <div id="eventBanner" class="event-banner" onclick="showAllEvents()"></div>

        <header>
            <h1>✨ الحقيبة المهدوية</h1>
            <p id="hijriDate" style="color:var(--accent); text-align:center; font-weight:bold; margin-top:5px;"></p>
            <button onclick="showAllEvents()" style="display:block; margin: 10px auto; background: none; border: 1px solid var(--accent); color: white; border-radius: 15px; padding: 5px 15px; cursor: pointer; font-size: 0.9rem;">📅 عرض كل المناسبات</button>
        </header>

        <div class="card">
            <div class="prayer-row">
                <div><small>الفجر</small><b>٠٥:٠٢</b></div>
                <div><small>الظهر</small><b>١٢:١٢</b></div>
                <div><small>المغرب</small><b>١٨:٠٥</b></div>
            </div>
        </div>

        <div class="card" style="text-align:center">
            <div class="tasbih-selector">
                <button id="btnZ" class="mode-btn active" onclick="setTasbihMode('zahra')">تسبيح الزهراء</button>
                <button id="btnH" class="mode-btn" onclick="setTasbihMode('hurr')">تسبيح الحر</button>
            </div>
            <div id="t-name" style="font-weight:bold; color:var(--primary); font-size:1.6rem;">الله أكبر</div>
            <div id="counter">٠</div>
            <div class="tap-circle" onclick="tap()">سبّح</div>
            <button style="background: #fee2e2; color:#b91c1c; border:none; padding:8px 20px; border-radius:10px; font-weight:bold; cursor:pointer;" onclick="resetT()">إعادة العداد</button>
        </div>

        <div class="card">
            <div class="audio-player">
                <div id="currentTrackName" style="font-weight:bold; color:var(--primary); margin-bottom:5px;">قيد القراءة: زيارة عاشوراء</div>
                <button id="playAudio" class="play-btn" onclick="toggleAudio()">▶</button>
            </div>
            
            <div class="tabs">
                <button class="tab active" onclick="loadContent('z1', this)">زيارة عاشوراء</button>
                <button class="tab" onclick="loadContent('z2', this)">زيارة وارث</button>
                <button class="tab" onclick="loadContent('z3', this)">دعاء الفرج</button>
            </div>

            <div id="text-area" class="scroll-content">
                <b>زيارة عاشوراء كاملة:</b><br>
                السَّلامُ عَلَيْكَ يا أَبا عَبْدِاللهِ، السَّلامُ عَلَيْكَ يَا بْنَ رَسُولِ اللهِ...
            </div>
        </div>

        <footer>
            جميع حقوق الطبع والنشر محفوظة لـ <span class="copy-accent">حقيبة المهدي (عج)</span><br>
            المصمم <span class="copy-accent">محمد علي الكعبي</span>
        </footer>
    </div>
</div>

<div id="eventModal" class="modal">
    <div class="modal-content">
        <h2 style="color:var(--primary); border-bottom:2px solid var(--accent);">📅 مناسبات شهر آذار</h2>
        <div id="modalList"></div>
        <button class="btn-close" onclick="closeModal()">إغلاق</button>
    </div>
</div>

<audio id="mainAudio" src="https://media.shiavoice.com/media/sounds/h7m8p.mp3"></audio>

<script>
    // --- قاعدة بيانات المناسبات ---
    const shiaEvents = {
        "3-19": "🌙 ذكرى استشهاد الإمام علي (ع) - عظم الله أجوركم",
        "3-21": "🎉 عيد الفطر المبارك - كل عام وأنتم بخير",
        "3-25": "🌙 ذكرى استشهاد الإمام جعفر الصادق (ع)",
        "3-2": "🎉 ذكرى ولادة الإمام الحجة (عج) - متباركين",
        "3-10": "🌙 وفاة السيدة خديجة الكبرى (ع)"
    };

    function checkEvents() {
        const d = new Date();
        const key = (d.getMonth() + 1) + "-" + d.getDate();
        const banner = document.getElementById('eventBanner');
        if (shiaEvents[key]) {
            banner.innerText = shiaEvents[key];
            banner.style.display = "block";
        }
        document.getElementById('hijriDate').innerText = d.toLocaleDateString('ar-IQ', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
    }

    function showAllEvents() {
        const list = document.getElementById('modalList');
        list.innerHTML = "";
        for (let date in shiaEvents) {
            let item = document.createElement('div');
            item.className = "event-list-item";
            let dParts = date.split('-');
            item.innerHTML = `<span>${dParts[1]} آذار</span> ${shiaEvents[date]}`;
            list.appendChild(item);
        }
        document.getElementById('eventModal').style.display = "block";
    }

    function closeModal() { document.getElementById('eventModal').style.display = "none"; }

    // --- منطق المسبحة المتعددة ---
    let c = 0; 
    let s = 0;
    let currentMode = 'zahra';

    const tasbihData = {
        zahra: { names: ["الله أكبر", "الحمد لله", "سبحان الله"], limits: [34, 33, 33] },
        hurr: { names: ["أستغفر الله", "صلوات محمدية", "يا علي"], limits: [70, 100, 110] }
    };

    function setTasbihMode(mode) {
        currentMode = mode;
        document.getElementById('btnZ').classList.toggle('active', mode === 'zahra');
        document.getElementById('btnH').classList.toggle('active', mode === 'hurr');
        resetT();
    }

    function toArabic(n) { return n.toString().replace(/\d/g, d => "٠١٢٣٤٥٦٧٨٩"[d]); }

    function tap() {
        const data = tasbihData[currentMode];
        c++;
        if (c <= data.limits[s]) {
            document.getElementById('counter').innerText = toArabic(c);
            if (c === data.limits[s]) {
                if(navigator.vibrate) navigator.vibrate([200, 100, 200]);
                if (s < data.names.length - 1) { 
                    s++; c = 0; 
                    document.getElementById('t-name').innerText = data.names[s]; 
                    document.getElementById('counter').innerText = "٠"; 
                } else { 
                    alert("تقبل الله أعمالكم!"); 
                    resetT(); 
                }
            }
        }
        if(navigator.vibrate) navigator.vibrate(40);
    }

    function resetT() { 
        c = 0; s = 0; 
        const data = tasbihData[currentMode];
        document.getElementById('counter').innerText = "٠"; 
        document.getElementById('t-name').innerText = data.names[0]; 
    }

    // --- الصوت والمحتوى ---
    const audioPlayer = document.getElementById('mainAudio');
    const playBtn = document.getElementById('playAudio');

    const audioLibrary = {
        z1: "https://media.shiavoice.com/media/sounds/h7m8p.mp3",
        z2: "https://media.shiavoice.com/media/sounds/3r5t1.mp3",
        z3: "https://media.shiavoice.com/media/sounds/q2w9e.mp3"
    };

    const textLibrary = {
        z1: "<b>زيارة عاشوراء كاملة:</b><br>السَّلامُ عَلَيْكَ يا أَبا عَبْدِاللهِ، السَّلامُ عَلَيْكَ يَا بْنَ رَسُولِ اللهِ، السَّلامُ عَلَيْكَ يَا بْنَ أَمِيرِ الْمُؤْمِنِينَ وَابْنَ سَيِّدِ الْوَصِيِّينَ، السَّلامُ عَلَيْكَ يَا بْنَ فاطِمَةَ سَيِّدَةِ نِساءِ الْعالَمِينَ...",
        z2: "<b>زيارة وارث:</b><br>السَّلامُ عَلَيْكَ يا وارِثَ آدَمَ صَفْوَةِ اللهِ، السَّلامُ عَلَيْكَ يا وارِثَ نُوح نَبِيِّ اللهِ، السَّلامُ عَلَيْكَ يا وارِثَ إِبْراهِيمَ خَلِيلِ اللهِ...",
        z3: "<b>دعاء الفرج:</b><br>اللهم كُن لوليك الحجة بن الحسن، صلواتك عليه وعلى آبائه، في هذه الساعة وفي كل ساعة، ولياً وحافظاً وقائداً وناصراً ودليلاً وعيناً..."
    };

    function toggleAudio() {
        if (audioPlayer.paused) { audioPlayer.play(); playBtn.innerText = "⏸"; }
        else { audioPlayer.pause(); playBtn.innerText = "▶"; }
    }

    function loadContent(key, btn) {
        document.getElementById('text-area').innerHTML = textLibrary[key];
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        btn.classList.add('active');
        audioPlayer.pause();
        audioPlayer.src = audioLibrary[key];
        playBtn.innerText = "▶";
        document.getElementById('currentTrackName').innerText = "قيد القراءة: " + btn.innerText;
    }

    checkEvents();
</script>
</body>
</html>
