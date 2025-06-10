<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>駱彥廷ㄉ睡覺觀察</title>
    <style>
        body {
            font-family: 'Microsoft JhengHei', Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        h1 {
            color: #333;
            text-align: center;
            margin-bottom: 30px;
        }
        .calendar {
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }
        .calendar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 10px;
        }
        .day-header {
            text-align: center;
            font-weight: bold;
            padding: 5px;
        }
        .day {
            text-align: center;
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
        }
        .day:hover {
            background-color: #e0e0e0;
        }
        .day.has-entry {
            background-color: #e3f2fd;
        }
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background: white;
            padding: 20px;
            border-radius: 10px;
            width: 300px;
        }
        .stats {
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .stat-item {
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <h1>駱彥廷ㄉ睡覺觀察</h1>
    
    <div class="calendar">
        <div class="calendar-header">
            <button id="prev-month">上個月</button>
            <h2 id="current-month">2023年11月</h2>
            <button id="next-month">下個月</button>
        </div>
        <div class="calendar-grid" id="calendar-grid">
            <!-- 日曆內容將由JavaScript動態生成 -->
        </div>
    </div>
    
    <div class="stats">
        <h2>睡眠統計</h2>
        <div class="stat-item">
            <strong>平均入睡時間:</strong> <span id="avg-sleep-time">--:--</span>
        </div>
        <div class="stat-item">
            <strong>平均睡眠時數:</strong> <span id="avg-sleep-hours">-- 小時</span>
        </div>
    </div>
    
    <div class="modal" id="entry-modal">
        <div class="modal-content">
            <h3 id="modal-date">2023年11月15日</h3>
            <div>
                <label for="sleep-time">入睡時間:</label>
                <input type="time" id="sleep-time" required>
            </div>
            <div>
                <label for="wake-time">起床時間:</label>
                <input type="time" id="wake-time" required>
            </div>
            <button id="save-entry">保存</button>
            <button id="cancel-entry">取消</button>
        </div>
    </div>
    
    <script>
        // 這裡將放置JavaScript代碼
    </script>
</body>
</html>
