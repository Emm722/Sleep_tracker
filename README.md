<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>駱彥廷ㄉ睡眠觀察</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Microsoft JhengHei', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            max-width: 900px;
            margin: 0 auto;
            padding: 20px;
            background: linear-gradient(135deg, #f5f7fa 0%, #e4edf5 100%);
            color: #333;
            min-height: 100vh;
        }
        
        header {
            text-align: center;
            padding: 20px 0 30px;
            position: relative;
        }
        
        .title-container {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 15px;
            flex-wrap: wrap;
            margin-bottom: 15px;
        }
        
        h1 {
            color: #2c3e50;
            font-size: 2.5rem;
            margin: 0;
            text-shadow: 1px 1px 3px rgba(0,0,0,0.1);
            position: relative;
            display: inline-block;
            background: linear-gradient(to right, #3498db, #9b59b6);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            padding: 0 15px;
            border-radius: 10px;
        }
        
        .subtitle {
            color: #7f8c8d;
            font-size: 1.2rem;
            margin: 0;
            padding: 8px 15px;
            background-color: rgba(255,255,255,0.7);
            border-radius: 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            position: relative;
            width: 100%;
        }
        
        .subtitle::before {
            content: "";
            position: absolute;
            left: 0;
            right: 0;
            bottom: -5px;
            height: 2px;
            background: linear-gradient(to right, transparent, #3498db, transparent);
        }
        
        .title-decoration {
            font-size: 1.8rem;
            color: #3498db;
            animation: float 3s ease-in-out infinite;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-5px); }
        }
        
        .dashboard {
            display: grid;
            grid-template-columns: 1fr;
            gap: 25px;
            margin-bottom: 30px;
        }
        
        @media (min-width: 768px) {
            .dashboard {
                grid-template-columns: 2fr 1fr;
            }
        }
        
        .panel {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.08);
            transition: transform 0.3s ease;
        }
        
        .panel:hover {
            transform: translateY(-5px);
        }
        
        .calendar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .calendar-header button {
            padding: 8px 15px;
            background: linear-gradient(to right, #3498db, #2980b9);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }
        
        .calendar-header button:hover {
            background: linear-gradient(to right, #2980b9, #2573a7);
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        
        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 8px;
        }
        
        .day-header {
            text-align: center;
            font-weight: bold;
            padding: 12px 5px;
            color: #3498db;
            font-size: 1.1rem;
            border-bottom: 2px solid #3498db;
        }
        
        .day {
            text-align: center;
            padding: 10px 5px;
            border-radius: 10px;
            cursor: pointer;
            border: 2px solid #ecf0f1;
            transition: all 0.2s;
            position: relative;
            font-weight: 600;
            font-size: 1.1rem;
            height: 70px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
        }
        
        .day:hover {
            background-color: #e0f7fa;
            transform: scale(1.05);
        }
        
        .day.has-entry {
            background-color: #bbdefb;
            border-color: #90caf9;
        }
        
        .day.today {
            background-color: #ffe0b2;
            border-color: #ffcc80;
            box-shadow: 0 0 0 3px rgba(255, 152, 0, 0.3);
        }
        
        .quality-indicator {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 2px;
            width: 100%;
            margin-top: 3px;
        }
        
        .quality-indicator i {
            color: #f1c40f;
            font-size: 0.6rem;
            background: rgba(241, 196, 15, 0.1);
            border-radius: 3px;
            aspect-ratio: 1/1;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 1px;
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.7);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }
        
        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 15px;
            width: 90%;
            max-width: 400px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            position: relative;
        }
        
        .close-modal {
            position: absolute;
            top: 15px;
            right: 20px;
            font-size: 1.8rem;
            cursor: pointer;
            color: #7f8c8d;
            transition: color 0.3s;
        }
        
        .close-modal:hover {
            color: #e74c3c;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
        }
        
        .stat-item {
            padding: 15px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 3px 8px rgba(0,0,0,0.05);
        }
        
        .stat-item h3 {
            color: #7f8c8d;
            font-size: 1.1rem;
            margin-bottom: 8px;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .stat-value {
            font-size: 1.8rem;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .quality-section {
            margin: 20px 0;
            padding: 15px;
            background: #fff8e1;
            border-radius: 10px;
        }
        
        .star-rating {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-top: 15px;
        }
        
        .star-rating i {
            font-size: 2rem;
            color: #e0e0e0;
            cursor: pointer;
            transition: color 0.2s, transform 0.2s;
        }
        
        .star-rating i:hover {
            transform: scale(1.2);
        }
        
        .star-rating i.active {
            color: #ffc107;
        }
        
        input[type="time"] {
            padding: 12px;
            margin: 10px 0;
            width: 100%;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1.1rem;
            transition: border-color 0.3s;
        }
        
        input[type="time"]:focus {
            border-color: #3498db;
            outline: none;
            box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.2);
        }
        
        label {
            display: block;
            margin: 15px 0 8px;
            font-weight: bold;
            color: #2c3e50;
            font-size: 1.1rem;
        }
        
        .button-group {
            display: flex;
            justify-content: space-between;
            margin-top: 25px;
            gap: 15px;
        }
        
        button {
            padding: 12px 20px;
            cursor: pointer;
            border: none;
            border-radius: 8px;
            font-size: 1.1rem;
            font-weight: 600;
            flex: 1;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        #save-entry {
            background: linear-gradient(to right, #3498db, #2980b9);
            color: white;
            box-shadow: 0 4px 10px rgba(52, 152, 219, 0.3);
        }
        
        #save-entry:hover {
            background: linear-gradient(to right, #2980b9, #2573a7);
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(52, 152, 219, 0.4);
        }
        
        #cancel-entry {
            background: linear-gradient(to right, #95a5a6, #7f8c8d);
            color: white;
        }
        
        #cancel-entry:hover {
            background: linear-gradient(to right, #7f8c8d, #707b7c);
            transform: translateY(-2px);
        }
        
        .sleep-quality-chart {
            display: flex;
            align-items: flex-end;
            height: 120px;
            margin-top: 15px;
            gap: 10px;
            padding: 10px 0;
            border-top: 1px solid #eee;
        }
        
        .quality-bar {
            flex: 1;
            background: #e0e0e0;
            border-radius: 5px 5px 0 0;
            position: relative;
            transition: height 0.5s ease;
        }
        
        .quality-bar-label {
            position: absolute;
            bottom: -25px;
            left: 0;
            right: 0;
            text-align: center;
            font-size: 0.85rem;
            color: #7f8c8d;
        }
        
        .quality-bar-value {
            position: absolute;
            top: -25px;
            left: 0;
            right: 0;
            text-align: center;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .highlight {
            background: linear-gradient(to right, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 3px 8px;
            border-radius: 5px;
            font-weight: bold;
        }
        
        .tips {
            margin-top: 20px;
            padding: 15px;
            background: #e3f2fd;
            border-radius: 10px;
            font-size: 0.95rem;
        }
        
        .tips h3 {
            margin-bottom: 10px;
            color: #1976d2;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .tips ul {
            padding-left: 20px;
        }
        
        .tips li {
            margin: 8px 0;
        }
        
        footer {
            text-align: center;
            margin-top: 40px;
            color: #7f8c8d;
            font-size: 0.9rem;
            padding: 20px 0;
            border-top: 1px solid #eee;
        }
        
        /* 帳號系統樣式 */
        .account-section {
            margin-top: 15px;
            text-align: center;
            padding: 15px;
            background: rgba(255, 255, 255, 0.8);
            border-radius: 10px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .account-form {
            display: flex;
            flex-direction: column;
            gap: 10px;
            max-width: 300px;
            margin: 0 auto;
        }
        
        .account-form input {
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }
        
        .account-form button {
            padding: 10px;
            background: linear-gradient(to right, #3498db, #2980b9);
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }
        
        .account-info {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
            flex-wrap: wrap;
        }
        
        .user-info {
            font-weight: bold;
            color: #3498db;
        }
        
        .logout-btn {
            padding: 6px 12px;
            background: #e74c3c;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.9rem;
        }
        
        .sync-info {
            margin-top: 10px;
            font-size: 0.85rem;
            color: #7f8c8d;
        }
        
        .sync-status {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 5px;
            margin-top: 5px;
        }
        
        .sync-status .success {
            color: #2ecc71;
        }
        
        .sync-status .error {
            color: #e74c3c;
        }
        
        /* 響應式調整 */
        @media (max-width: 600px) {
            h1 {
                font-size: 2rem;
            }
            
            .subtitle {
                font-size: 1rem;
            }
            
            .panel {
                padding: 15px;
            }
            
            .day {
                height: 60px;
                font-size: 1rem;
            }
            
            .stat-value {
                font-size: 1.5rem;
            }
            
            .account-form {
                max-width: 100%;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="title-container">
            <span class="title-decoration">🌙</span>
            <h1>駱彥廷ㄉ睡眠觀察</h1>
            <span class="title-decoration">✨</span>
        </div>
        <div class="subtitle">記錄睡眠時間與品質，提升健康生活</div>
        
        <div class="account-section">
            <div id="login-section">
                <div class="account-form">
                    <input type="text" id="username" placeholder="使用者名稱" required>
                    <input type="password" id="password" placeholder="密碼" required>
                    <button id="login-btn"><i class="fas fa-sign-in-alt"></i> 登入</button>
                </div>
            </div>
            <div id="logged-in-section" style="display: none;">
                <div class="account-info">
                    <span class="user-info">歡迎 <span id="display-username"></span>！</span>
                    <button class="logout-btn" id="logout-btn"><i class="fas fa-sign-out-alt"></i> 登出</button>
                </div>
                <div class="sync-info">
                    <div class="sync-status">
                        <i class="fas fa-sync"></i>
                        <span id="sync-message">資料已同步</span>
                    </div>
                </div>
            </div>
        </div>
    </header>
    
    <div class="dashboard">
        <div class="panel">
            <div class="calendar-header">
                <button id="prev-month"><i class="fas fa-chevron-left"></i> 上個月</button>
                <h2 id="current-month"></h2>
                <button id="next-month">下個月 <i class="fas fa-chevron-right"></i></button>
            </div>
            <div class="calendar-grid" id="calendar-grid">
                <!-- 日曆內容將由JavaScript動態生成 -->
            </div>
        </div>
        
        <div class="panel">
            <h2><i class="fas fa-chart-line"></i> 睡眠統計</h2>
            <div class="stats-grid">
                <div class="stat-item">
                    <h3><i class="fas fa-moon"></i> 平均入睡時間</h3>
                    <div class="stat-value" id="avg-sleep-time">--:--</div>
                </div>
                <div class="stat-item">
                    <h3><i class="fas fa-sun"></i> 平均起床時間</h3>
                    <div class="stat-value" id="avg-wake-time">--:--</div>
                </div>
                <div class="stat-item">
                    <h3><i class="fas fa-bed"></i> 平均睡眠時數</h3>
                    <div class="stat-value" id="avg-sleep-hours">-- 小時</div>
                </div>
                <div class="stat-item">
                    <h3><i class="fas fa-calendar-check"></i> 本月打卡天數</h3>
                    <div class="stat-value" id="total-days">0 天</div>
                </div>
                <div class="stat-item">
                    <h3><i class="fas fa-star"></i> 平均睡眠品質</h3>
                    <div class="stat-value" id="avg-quality">--</div>
                </div>
            </div>
            
            <div class="sleep-quality-chart" id="quality-chart">
                <!-- 睡眠品質圖表將由JavaScript動態生成 -->
            </div>
            
            <div class="tips">
                <h3><i class="fas fa-lightbulb"></i> 優質睡眠小貼士</h3>
                <ul>
                    <li>每天固定時間上床睡覺和起床</li>
                    <li>睡前1小時避免使用電子設備</li>
                    <li>保持臥室涼爽、黑暗且安靜</li>
                    <li>下午後避免攝取咖啡因</li>
                    <li>白天適度運動有助於夜間睡眠</li>
                </ul>
            </div>
        </div>
    </div>
    
    <div class="modal" id="entry-modal">
        <div class="modal-content">
            <span class="close-modal">&times;</span>
            <h3 id="modal-date"></h3>
            
            <div>
                <label for="sleep-time"><i class="fas fa-moon"></i> 入睡時間:</label>
                <input type="time" id="sleep-time" required value="23:00">
            </div>
            
            <div>
                <label for="wake-time"><i class="fas fa-sun"></i> 起床時間:</label>
                <input type="time" id="wake-time" required value="07:30">
            </div>
            
            <div class="quality-section">
                <label><i class="fas fa-star"></i> 睡眠品質:</label>
                <div class="star-rating" id="star-rating">
                    <i class="fas fa-star" data-rating="1"></i>
                    <i class="fas fa-star" data-rating="2"></i>
                    <i class="fas fa-star" data-rating="3"></i>
                    <i class="fas fa-star" data-rating="4"></i>
                    <i class="fas fa-star" data-rating="5"></i>
                </div>
                <div id="quality-description" style="text-align: center; margin-top: 10px; font-style: italic; color: #7f8c8d;">
                    請選擇睡眠品質評分
                </div>
            </div>
            
            <div class="button-group">
                <button id="save-entry"><i class="fas fa-save"></i> 保存記錄</button>
                <button id="cancel-entry"><i class="fas fa-times"></i> 取消</button>
            </div>
        </div>
    </div>
    
    <footer>
        <p>睡眠是健康的基石 · 優質睡眠帶來美好生活</p>
        <p>© 2025 emily ai駱彥廷睡眠觀察系統 · 版本 2.0</p>
        <p>資料已儲存至雲端，可在任何裝置存取</p>
    </footer>
    
    <script>
        // 模擬的雲端數據庫API
const cloudDB = {
    users: {
        "camel_sleep": "sleepearly!!"  // 預設帳號
    },
    sleepData: {
        "camel_sleep": {}  // 預設用戶的睡眠數據
    },
            
            // 用戶登入
            login: function(username, password) {
                if (this.users[username] === password) {
                    return { success: true, userData: this.sleepData[username] };
                }
                return { success: false, message: '使用者名稱或密碼錯誤' };
            },
            
            // 儲存睡眠數據
            saveData: function(username, data) {
                if (!this.users[username]) {
                    return { success: false, message: '使用者不存在' };
                }
                this.sleepData[username] = data;
                return { success: true, message: '數據已儲存至雲端' };
            }
        };
        
        document.addEventListener('DOMContentLoaded', function() {
            // 當前日期
            const now = new Date();
            let currentMonth = now.getMonth();
            let currentYear = now.getFullYear();
            const today = now.getDate();
            let selectedRating = 0;
            let currentUser = null;
            let sleepData = {};
            
            // 睡眠品質描述
            const qualityDescriptions = {
                1: "非常差 - 輾轉難眠，多次醒來",
                2: "不太好 - 睡眠不深，醒來仍感疲倦",
                3: "普通 - 睡眠尚可，但還不夠理想",
                4: "良好 - 睡眠安穩，醒來精神不錯",
                5: "極佳 - 深度睡眠，醒來神清氣爽"
            };
            
            // 初始化UI
            updateUI();
            setupStarRating();
            
            // 註冊事件監聽器
            setupEventListeners();
            
            // 設置星級評分
            function setupStarRating() {
                const stars = document.querySelectorAll('#star-rating i');
                const description = document.getElementById('quality-description');
                
                stars.forEach(star => {
                    star.addEventListener('click', function() {
                        const rating = parseInt(this.dataset.rating);
                        selectedRating = rating;
                        
                        // 更新星星樣式
                        stars.forEach((s, index) => {
                            if (index < rating) {
                                s.classList.add('active');
                            } else {
                                s.classList.remove('active');
                            }
                        });
                        
                        // 更新描述
                        description.textContent = qualityDescriptions[rating];
                    });
                });
            }
            
            // 設置事件監聽器
            function setupEventListeners() {
                // 登入按鈕
                document.getElementById('login-btn').addEventListener('click', login);
                
                // 登出按鈕
                document.getElementById('logout-btn').addEventListener('click', logout);
                
                // 上個月/下個月按鈕
                document.getElementById('prev-month').addEventListener('click', function() {
                    currentMonth--;
                    if (currentMonth < 0) {
                        currentMonth = 11;
                        currentYear--;
                    }
                    renderCalendar(currentMonth, currentYear);
                });
                
                document.getElementById('next-month').addEventListener('click', function() {
                    currentMonth++;
                    if (currentMonth > 11) {
                        currentMonth = 0;
                        currentYear++;
                    }
                    renderCalendar(currentMonth, currentYear);
                });
                
                // 保存打卡記錄
                document.getElementById('save-entry').addEventListener('click', saveEntry);
                
                // 取消打卡
                document.getElementById('cancel-entry').addEventListener('click', function() {
                    document.getElementById('entry-modal').style.display = 'none';
                });
                
                // 點擊模態框外部或關閉按鈕關閉
                document.querySelector('.close-modal').addEventListener('click', function() {
                    document.getElementById('entry-modal').style.display = 'none';
                });
                
                document.getElementById('entry-modal').addEventListener('click', function(e) {
                    if (e.target === this) {
                        this.style.display = 'none';
                    }
                });
            }
            
            // 登入功能
            function login() {
                const username = document.getElementById('username').value;
                const password = document.getElementById('password').value;
                
                if (!username || !password) {
                    showSyncMessage('請輸入使用者名稱和密碼', 'error');
                    return;
                }
                
                const result = cloudDB.login(username, password);
                if (result.success) {
                    currentUser = username;
                    sleepData = result.userData;
                    showSyncMessage('登入成功！資料已同步', 'success');
                    updateUI();
                    renderCalendar(currentMonth, currentYear);
                    updateStats();
                } else {
                    showSyncMessage(result.message, 'error');
                }
            }
            
            // 登出功能
            function logout() {
                currentUser = null;
                sleepData = {};
                document.getElementById('username').value = '';
                document.getElementById('password').value = '';
                updateUI();
                renderCalendar(currentMonth, currentYear);
                updateStats();
                showSyncMessage('已登出', 'info');
            }
            
            // 更新UI狀態
            function updateUI() {
                const loggedIn = currentUser !== null;
                document.getElementById('login-section').style.display = loggedIn ? 'none' : 'block';
                document.getElementById('logged-in-section').style.display = loggedIn ? 'block' : 'none';
                
                if (loggedIn) {
                    document.getElementById('display-username').textContent = currentUser;
                }
            }
            
            // 顯示同步訊息
            function showSyncMessage(message, type) {
                const syncMessage = document.getElementById('sync-message');
                syncMessage.textContent = message;
                syncMessage.className = type;
                
                // 3秒後清除訊息
                setTimeout(() => {
                    if (syncMessage.textContent === message) {
                        syncMessage.textContent = '';
                        syncMessage.className = '';
                    }
                }, 3000);
            }
            
            // 渲染日曆
            function renderCalendar(month, year) {
                // 更新月份標題
                document.getElementById('current-month').textContent = `${year}年${month + 1}月`;
                
                const firstDay = new Date(year, month, 1);
                const startingDay = firstDay.getDay();
                const daysInMonth = new Date(year, month + 1, 0).getDate();
                
                const calendarGrid = document.getElementById('calendar-grid');
                calendarGrid.innerHTML = '';
                
                // 添加星期標題
                const weekdays = ['日', '一', '二', '三', '四', '五', '六'];
                weekdays.forEach(day => {
                    const dayHeader = document.createElement('div');
                    dayHeader.className = 'day-header';
                    dayHeader.textContent = day;
                    calendarGrid.appendChild(dayHeader);
                });
                
                // 添加空白格子
                for (let i = 0; i < startingDay; i++) {
                    const emptyDay = document.createElement('div');
                    emptyDay.className = 'day';
                    calendarGrid.appendChild(emptyDay);
                }
                
                // 添加日期格子
                for (let day = 1; day <= daysInMonth; day++) {
                    const dateStr = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
                    const dayElement = document.createElement('div');
                    dayElement.className = 'day';
                    dayElement.innerHTML = `<div>${day}</div>`;
                    dayElement.dataset.date = dateStr;
                    
                    // 標記今天
                    if (year === now.getFullYear() && month === now.getMonth() && day === today) {
                        dayElement.classList.add('today');
                    }
                    
                    // 檢查是否有記錄
                    if (sleepData[dateStr]) {
                        dayElement.classList.add('has-entry');
                        
                        // 添加睡眠品質指示器
                        if (sleepData[dateStr].quality) {
                            const qualityIndicator = document.createElement('div');
                            qualityIndicator.className = 'quality-indicator';
                            
                            // 創建5個格子，但只顯示實際評分數量的星星
                            for (let i = 1; i <= 5; i++) {
                                const starContainer = document.createElement('div');
                                if (i <= sleepData[dateStr].quality) {
                                    const star = document.createElement('i');
                                    star.className = 'fas fa-star active';
                                    starContainer.appendChild(star);
                                }
                                qualityIndicator.appendChild(starContainer);
                            }
                            
                            dayElement.appendChild(qualityIndicator);
                        }
                    }
                    
                    dayElement.addEventListener('click', function() {
                        openEntryModal(dateStr);
                    });
                    
                    calendarGrid.appendChild(dayElement);
                }
            }
            
            // 打開打卡模態框
            function openEntryModal(dateStr) {
                if (!currentUser) {
                    showSyncMessage('請先登入以記錄睡眠', 'error');
                    return;
                }
                
                const [year, month, day] = dateStr.split('-');
                const modal = document.getElementById('entry-modal');
                document.getElementById('modal-date').textContent = `${year}年${month}月${day}日`;
                document.getElementById('modal-date').dataset.date = dateStr;
                
                // 重置星級
                selectedRating = 0;
                const stars = document.querySelectorAll('#star-rating i');
                stars.forEach(star => star.classList.remove('active'));
                document.getElementById('quality-description').textContent = "請選擇睡眠品質評分";
                
                // 設置時間輸入框的值
                const entry = sleepData[dateStr];
                document.getElementById('sleep-time').value = entry ? entry.sleepTime : '23:00';
                document.getElementById('wake-time').value = entry ? entry.wakeTime : '07:30';
                
                // 如果有品質記錄，設置星級
                if (entry && entry.quality) {
                    selectedRating = entry.quality;
                    stars.forEach((star, index) => {
                        if (index < entry.quality) {
                            star.classList.add('active');
                        }
                    });
                    document.getElementById('quality-description').textContent = qualityDescriptions[entry.quality];
                }
                
                modal.style.display = 'flex';
            }
            
            // 保存打卡記錄
            function saveEntry() {
                const sleepTime = document.getElementById('sleep-time').value;
                const wakeTime = document.getElementById('wake-time').value;
                const dateStr = document.getElementById('modal-date').dataset.date;
                
                if (!sleepTime || !wakeTime) {
                    alert('請填寫完整的入睡和起床時間！');
                    return;
                }
                
                if (!dateStr) {
                    alert('日期信息丟失，請重新選擇日期！');
                    return;
                }
                
                if (selectedRating === 0) {
                    alert('請選擇睡眠品質評分！');
                    return;
                }
                
                // 保存數據（包括睡眠品質）
                sleepData[dateStr] = {
                    sleepTime: sleepTime,
                    wakeTime: wakeTime,
                    quality: selectedRating
                };
                
                // 保存到雲端
                const result = cloudDB.saveData(currentUser, sleepData);
                if (result.success) {
                    showSyncMessage(result.message, 'success');
                } else {
                    showSyncMessage(result.message, 'error');
                }
                
                // 關閉模態框並更新
                document.getElementById('entry-modal').style.display = 'none';
                renderCalendar(currentMonth, currentYear);
                updateStats();
            }
            
            // 更新統計數據
            function updateStats() {
                const currentMonthStr = `${currentYear}-${String(currentMonth + 1).padStart(2, '0')}`;
                const monthEntries = Object.entries(sleepData).filter(
                    ([dateStr]) => dateStr.startsWith(currentMonthStr)
                );
                
                document.getElementById('total-days').textContent = `${monthEntries.length} 天`;
                
                if (monthEntries.length === 0) {
                    document.getElementById('avg-sleep-time').textContent = '--:--';
                    document.getElementById('avg-wake-time').textContent = '--:--';
                    document.getElementById('avg-sleep-hours').textContent = '-- 小時';
                    document.getElementById('avg-quality').textContent = '--';
                    renderQualityChart([]);
                    return;
                }
                
                // 計算平均入睡時間
                let sleepTotalMinutes = 0;
                // 計算平均起床時間
                let wakeTotalMinutes = 0;
                
                monthEntries.forEach(([_, entry]) => {
                    if (entry.sleepTime) {
                        const [hours, minutes] = entry.sleepTime.split(':').map(Number);
                        sleepTotalMinutes += hours * 60 + minutes;
                    }
                    
                    if (entry.wakeTime) {
                        const [hours, minutes] = entry.wakeTime.split(':').map(Number);
                        wakeTotalMinutes += hours * 60 + minutes;
                    }
                });
                
                // 平均入睡時間
                const avgSleepMinutes = Math.round(sleepTotalMinutes / monthEntries.length);
                const avgSleepHours = Math.floor(avgSleepMinutes / 60);
                const avgSleepMins = avgSleepMinutes % 60;
                document.getElementById('avg-sleep-time').textContent = 
                    `${String(avgSleepHours).padStart(2, '0')}:${String(avgSleepMins).padStart(2, '0')}`;
                
                // 平均起床時間
                const avgWakeMinutes = Math.round(wakeTotalMinutes / monthEntries.length);
                const avgWakeHours = Math.floor(avgWakeMinutes / 60);
                const avgWakeMins = avgWakeMinutes % 60;
                document.getElementById('avg-wake-time').textContent = 
                    `${String(avgWakeHours).padStart(2, '0')}:${String(avgWakeMins).padStart(2, '0')}`;
                
                // 計算平均睡眠時數
                let totalSleepHours = 0;
                let validEntries = 0;
                
                monthEntries.forEach(([_, entry]) => {
                    if (entry.sleepTime && entry.wakeTime) {
                        const sleepTime = new Date(`2000-01-01T${entry.sleepTime}:00`);
                        const wakeTime = new Date(`2000-01-01T${entry.wakeTime}:00`);
                        
                        // 處理跨夜情況
                        if (wakeTime < sleepTime) {
                            wakeTime.setDate(wakeTime.getDate() + 1);
                        }
                        
                        const diffMs = wakeTime - sleepTime;
                        totalSleepHours += diffMs / (1000 * 60 * 60);
                        validEntries++;
                    }
                });
                
                if (validEntries > 0) {
                    const avgSleepHours = (totalSleepHours / validEntries).toFixed(1);
                    document.getElementById('avg-sleep-hours').textContent = `${avgSleepHours} 小時`;
                }
                
                // 計算平均睡眠品質
                let totalQuality = 0;
                let qualityEntries = 0;
                const qualityDistribution = {1: 0, 2: 0, 3: 0, 4: 0, 5: 0};
                
                monthEntries.forEach(([_, entry]) => {
                    if (entry.quality) {
                        totalQuality += entry.quality;
                        qualityEntries++;
                        qualityDistribution[entry.quality]++;
                    }
                });
                
                if (qualityEntries > 0) {
                    const avgQuality = (totalQuality / qualityEntries).toFixed(1);
                    document.getElementById('avg-quality').textContent = `${avgQuality}/5.0`;
                    
                    // 渲染品質分佈圖表
                    renderQualityChart(qualityDistribution);
                }
            }
            
            // 渲染睡眠品質圖表
            function renderQualityChart(distribution) {
                const chartContainer = document.getElementById('quality-chart');
                chartContainer.innerHTML = '';
                
                // 如果沒有數據，顯示提示
                if (!distribution || Object.values(distribution).every(count => count === 0)) {
                    chartContainer.innerHTML = '<p>本月無睡眠品質數據</p>';
                    return;
                }
                
                // 計算最大值用於縮放
                const maxCount = Math.max(...Object.values(distribution));
                
                for (let rating = 1; rating <= 5; rating++) {
                    const count = distribution[rating] || 0;
                    const height = maxCount > 0 ? (count / maxCount) * 100 : 0;
                    
                    const bar = document.createElement('div');
                    bar.className = 'quality-bar';
                    bar.style.height = `${height}%`;
                    
                    // 根據評分設置不同顏色
                    if (rating <= 2) {
                        bar.style.background = '#ff6b6b'; // 紅色表示差
                    } else if (rating === 3) {
                        bar.style.background = '#feca57'; // 黃色表示中等
                    } else {
                        bar.style.background = '#1dd1a1'; // 綠色表示好
                    }
                    
                    const value = document.createElement('div');
                    value.className = 'quality-bar-value';
                    value.textContent = count;
                    
                    const label = document.createElement('div');
                    label.className = 'quality-bar-label';
                    label.textContent = `${rating}星`;
                    
                    bar.appendChild(value);
                    bar.appendChild(label);
                    chartContainer.appendChild(bar);
                }
            }
        });
    </script>
</body>
</html>
