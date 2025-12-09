<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تطبيقي الشخصي الاحترافي (النسخة النهائية)</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        /* التنسيقات العامة */
        body {
            font-family: 'Tahoma', sans-serif;
            background-color: #f4f6f9;
            margin: 0;
            padding: 0;
            text-align: right;
            line-height: 1.6;
        }
        .container {
            max-width: 900px;
            margin: 30px auto;
            background-color: white;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
        }
        
        /* واجهة التنقل بين الشاشات */
        .app-view {
            display: none;
        }
        .app-view.active {
            display: block;
        }
        
        /* شريط العودة/الخروج */
        .header-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-bottom: 15px;
            margin-bottom: 20px;
            border-bottom: 2px solid #e0e0e0;
        }
        .back-btn {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 15px;
            transition: background-color 0.3s;
        }
        .back-btn:hover {
            background-color: #0056b3;
        }
        
        /* --- تنسيق شاشة Dashboard (الأيقونات) --- */
        #dashboard-view {
            text-align: center;
        }
        .icon-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 25px;
            padding: 20px 0;
        }
        .icon-btn {
            background-color: #ffffff;
            border: 2px solid #ddd;
            border-radius: 10px;
            padding: 20px 10px;
            cursor: pointer;
            text-align: center;
            transition: all 0.3s ease;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.05);
        }
        .icon-btn:hover {
            border-color: #007bff;
            transform: translateY(-5px);
            box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
        }
        .icon-btn i {
            font-size: 40px;
            color: #007bff;
            margin-bottom: 10px;
        }
        .icon-btn p {
            margin: 0;
            font-weight: bold;
            color: #333;
        }
        
        /* --- تنسيق شاشات الملاحظات والتنبيهات --- */
        .notes-list {
            list-style: none;
            padding: 0;
        }
        .note-item {
            background-color: #f8f9fa;
            border-right: 4px solid #007bff;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 6px;
            display: flex;
            flex-direction: column;
        }
        .note-content {
            flex-grow: 1;
            cursor: text;
            outline: none;
            min-height: 20px;
            padding-bottom: 10px;
            border-bottom: 1px dashed #eee;
            margin-bottom: 10px;
        }
        .note-actions {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .action-buttons button {
            padding: 5px 10px;
            border-radius: 4px;
            cursor: pointer;
            border: none;
            font-size: 14px;
            margin-left: 8px;
        }
        .delete-btn { background-color: #dc3545; color: white; }
        .edit-btn { background-color: #ffc107; color: #333; }
        .note-timestamp { font-size: 12px; color: #6c757d; }
        
        /* --- تنسيق شاشة تمارين كمال الأجسام (Gym Tracker) --- */
        .gym-day-section {
            background-color: #e9ecef;
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 8px;
        }
        .gym-day-section h3 {
            color: #333;
            border-bottom: 1px solid #ccc;
            padding-bottom: 5px;
            margin-top: 0;
        }
        .exercise-input-group {
            display: flex;
            gap: 15px;
            margin-bottom: 10px;
            align-items: center;
        }
        .exercise-input-group input[type="text"] {
            flex-grow: 1;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        .add-exercise-btn {
            background-color: #28a745;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
        }
        .exercise-list {
            list-style: none;
            padding: 0;
            margin-top: 10px;
        }
        .exercise-item {
            background-color: white;
            padding: 10px;
            margin-bottom: 5px;
            border-radius: 4px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-left: 3px solid #007bff;
        }
        /* تنسيق ترقيم التمرين */
        .exercise-item strong {
            font-size: 16px;
            color: #333;
        }
    </style>
</head>
<body>

    <div class="container">
        <div id="dashboard-view" class="app-view active">
            <h1 style="color: #007bff;">تطبيقي الشخصي</h1>
            <p style="color: #6c757d;">اختر واحدة من الأيقونات للبدء:</p>
            <div class="icon-grid">
                <div class="icon-btn" onclick="showNotesView('gym-view', 'gymData')">
                    <i class="fas fa-dumbbell"></i>
                    <p>تمارين كمال الأجسام</p>
                </div>
                <div class="icon-btn" onclick="showNotesView('notes-view', 'notes')">
                    <i class="fas fa-sticky-note"></i>
                    <p>ملاحظاتي</p>
                </div>
                <div class="icon-btn" onclick="showNotesView('alerts-view', 'alerts')">
                    <i class="fas fa-bell"></i>
                    <p>تنبيهات مهمة</p>
                </div>
                <div class="icon-btn" onclick="showNotesView('miswak-view', 'miswak')">
                    <i class="fas fa-tooth"></i>
                    <p>مسواك</p>
                </div>
                <div class="icon-btn" onclick="showNotesView('dua-view', 'dua')">
                    <i class="fas fa-mosque"></i>
                    <p>أدعية ونصائح دينية</p>
                </div>
            </div>
        </div>

        <div id="gym-view" class="app-view">
            <div class="header-bar">
                <h2>🏋️‍♂️ تمارين كمال الأجسام</h2>
                <button class="back-btn" onclick="showView('dashboard-view')">العودة للرئيسية</button>
            </div>
            
            <div id="day-one-section" class="gym-day-section">
                <h3>اليوم الأول</h3>
                <div class="exercise-input-group">
                    <input type="text" id="ex1_name" placeholder="اسم التمرين">
                    <input type="text" id="ex1_reps" placeholder="التكرارات"> 
                    <button class="add-exercise-btn" onclick="addGymExercise('day-one')">إضافة</button>
                </div>
                <ul id="day-one-list" class="exercise-list"></ul>
            </div>

            <div id="day-two-section" class="gym-day-section">
                <h3>اليوم الثاني</h3>
                <div class="exercise-input-group">
                    <input type="text" id="ex2_name" placeholder="اسم التمرين">
                    <input type="text" id="ex2_reps" placeholder="التكرارات">
                    <button class="add-exercise-btn" onclick="addGymExercise('day-two')">إضافة</button>
                </div>
                <ul id="day-two-list" class="exercise-list"></ul>
            </div>
            
            <div id="day-three-section" class="gym-day-section">
                <h3>اليوم الثالث</h3>
                <div class="exercise-input-group">
                    <input type="text" id="ex3_name" placeholder="اسم التمرين">
                    <input type="text" id="ex3_reps" placeholder="التكرارات">
                    <button class="add-exercise-btn" onclick="addGymExercise('day-three')">إضافة</button>
                </div>
                <ul id="day-three-list" class="exercise-list"></ul>
            </div>
        </div>
        
        <div id="notes-view" class="app-view">
            <div class="header-bar">
                <h2 id="current-notes-title">ملاحظاتي</h2>
                <button class="back-btn" onclick="showView('dashboard-view')">العودة للرئيسية</button>
            </div>
            
            <textarea id="generalNoteInput" placeholder="اكتب ملاحظتك/تنبيهك/دعوتك الجديدة هنا..."></textarea>
            <button id="addGeneralNoteBtn" class="back-btn" style="background-color: #28a745;">إضافة وحفظ</button>
            <hr style="margin: 20px 0;">

            <ul id="generalNotesList" class="notes-list"></ul>
        </div>
        
        <div id="alerts-view" class="app-view"></div>
        <div id="miswak-view" class="app-view"></div>
        <div id="dua-view" class="app-view"></div>
        
    </div>

    <script>
        // --- متغيرات وأدوات عامة ---
        let currentStorageKey = '';
        const GYM_STORAGE_KEY = 'gymTrackerData';
        
        // --- وظائف عرض الشاشات ---
        function showView(viewId) {
            document.querySelectorAll('.app-view').forEach(view => {
                view.classList.remove('active');
            });
            document.getElementById(viewId).classList.add('active');
        }

        // --- وظيفة عرض شاشة الملاحظات العامة ---
        function showNotesView(viewId, storageKeyName) {
            if (viewId === 'gym-view') {
                 showView('gym-view'); 
                 return;
            }

            currentStorageKey = storageKeyName; 
            const notesView = document.getElementById('notes-view');
            // استخراج اسم الأيقونة من زر لوحة التحكم
            const iconText = document.querySelector(`.icon-btn[onclick*="${viewId}"] p`).textContent;
            document.getElementById('current-notes-title').textContent = iconText;
            const generalNotesList = document.getElementById('generalNotesList');
            generalNotesList.innerHTML = ''; 
            loadNotes(generalNotesList); 
            showView('notes-view'); 
        }

        // --- وظائف الملاحظات (حفظ/تحميل باستخدام localStorage) ---
        function formatTimeAgo(timestamp) {
            const now = Date.now();
            const seconds = Math.floor((now - parseInt(timestamp)) / 1000);
            
            if (seconds < 60) return `منذ ${seconds} ثوانٍ`;
            const minutes = Math.floor(seconds / 60);
            if (minutes < 60) return `منذ ${minutes} دقيقة`;
            const hours = Math.floor(minutes / 60);
            if (hours < 24) return `منذ ${hours} ساعة`;
            const days = Math.floor(hours / 24);
            return `منذ ${days} يومًا`;
        }

        setInterval(() => {
            document.querySelectorAll('.note-item').forEach(item => {
                const timestamp = item.getAttribute('data-timestamp');
                const timeDisplay = item.querySelector('.note-timestamp');
                if (timestamp && timeDisplay) {
                    timeDisplay.textContent = formatTimeAgo(timestamp);
                }
            });
        }, 60000); 

        function saveNotes(listElement) {
            const notesData = [];
            listElement.querySelectorAll('.note-item').forEach(item => {
                const text = item.querySelector('.note-content').textContent;
                const timestamp = item.getAttribute('data-timestamp');
                notesData.push({ text: text, timestamp: timestamp });
            });
            localStorage.setItem(currentStorageKey, JSON.stringify(notesData));
        }

        function createNoteElement(noteObject, listElement) {
            const listItem = document.createElement('li');
            listItem.className = 'note-item';
            listItem.setAttribute('data-timestamp', noteObject.timestamp); 
            
            const contentSpan = document.createElement('span');
            contentSpan.className = 'note-content';
            contentSpan.textContent = noteObject.text;
            contentSpan.setAttribute('contenteditable', 'true'); 
            contentSpan.addEventListener('blur', () => saveNotes(listElement)); 

            const actionsDiv = document.createElement('div');
            actionsDiv.className = 'note-actions';

            const timeSpan = document.createElement('span');
            timeSpan.className = 'note-timestamp';
            timeSpan.textContent = formatTimeAgo(noteObject.timestamp); 
            
            const buttonsDiv = document.createElement('div');
            buttonsDiv.className = 'action-buttons';

            const editButton = document.createElement('button');
            editButton.className = 'edit-btn';
            editButton.textContent = 'تعديل';
            editButton.onclick = () => contentSpan.focus();

            const deleteButton = document.createElement('button');
            deleteButton.className = 'delete-btn';
            deleteButton.textContent = 'حذف';
            deleteButton.onclick = () => {
                listElement.removeChild(listItem);
                saveNotes(listElement); 
            };
            
            buttonsDiv.appendChild(editButton);
            buttonsDiv.appendChild(deleteButton);
            actionsDiv.appendChild(timeSpan);
            actionsDiv.appendChild(buttonsDiv);
            
            listItem.appendChild(contentSpan);
            listItem.appendChild(actionsDiv);
            return listItem;
        }

        function loadNotes(listElement) {
            const storedNotes = localStorage.getItem(currentStorageKey);
            if (storedNotes) {
                const notes = JSON.parse(storedNotes);
                notes.reverse().forEach(noteObject => {
                    listElement.prepend(createNoteElement(noteObject, listElement));
                });
            }
        }

        document.getElementById('addGeneralNoteBtn').addEventListener('click', () => {
            const noteText = document.getElementById('generalNoteInput').value.trim();
            const listElement = document.getElementById('generalNotesList');
            
            if (noteText === "") return;

            const newNoteObject = {
                text: noteText,
                timestamp: Date.now() 
            };

            listElement.prepend(createNoteElement(newNoteObject, listElement)); 
            document.getElementById('generalNoteInput').value = ''; 
            saveNotes(listElement);
        });

        // --- وظائف خاصة بتمارين كمال الأجسام (مع الترقيم) ---
        
        function saveGymData(data) {
            localStorage.setItem(GYM_STORAGE_KEY, JSON.stringify(data));
        }

        function loadGymData() {
            const storedData = localStorage.getItem(GYM_STORAGE_KEY);
            return storedData ? JSON.parse(storedData) : { 'day-one': [], 'day-two': [], 'day-three': [] };
        }

        function renderGymDay(dayKey, data) {
            const listElement = document.getElementById(`${dayKey}-list`);
            listElement.innerHTML = '';
            
            data.forEach((ex, index) => { 
                const item = document.createElement('li');
                item.className = 'exercise-item';
                item.innerHTML = `
                    <span>
                        <strong>${index + 1}. ${ex.name}:</strong> 
                        <span>${ex.reps}</span>
                    </span>
                    <div class="action-buttons">
                        <button class="delete-btn" onclick="deleteGymExercise('${dayKey}', ${index})">حذف</button>
                    </div>
                `;
                listElement.appendChild(item);
            });
        }
        
        function addGymExercise(dayKey) {
            let inputNum;
            if (dayKey === 'day-one') inputNum = 1;
            else if (dayKey === 'day-two') inputNum = 2;
            else if (dayKey === 'day-three') inputNum = 3;
            
            const nameInput = document.getElementById(`ex${inputNum}_name`);
            const repsInput = document.getElementById(`ex${inputNum}_reps`);
            
            const name = nameInput.value.trim();
            const reps = repsInput.value.trim();

            if (!name || !reps) {
                alert("الرجاء إدخال اسم التمرين والتكرارات!");
                return;
            }

            const data = loadGymData();
            data[dayKey].push({ name, reps });
            saveGymData(data);
            renderGymDay(dayKey, data[dayKey]);
            
            nameInput.value = '';
            repsInput.value = '';
        }

        function deleteGymExercise(dayKey, index) {
            if (!confirm("هل أنت متأكد من حذف هذا التمرين؟")) return;
            const data = loadGymData();
            data[dayKey].splice(index, 1);
            saveGymData(data);
            renderGymDay(dayKey, data[dayKey]);
        }
        
        // --- تهيئة التطبيق عند التحميل ---
        window.addEventListener('load', () => {
            const gymData = loadGymData();
            renderGymDay('day-one', gymData['day-one']);
            renderGymDay('day-two', gymData['day-two']);
            renderGymDay('day-three', gymData['day-three']);
        });
    </script>

</body>
</html>
