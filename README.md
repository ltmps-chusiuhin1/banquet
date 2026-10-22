<!DOCTYPE html>
<html lang="zh-HK">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>藍循三十周年校慶盆菜宴</title>

    <!-- ================= WhatsApp / 社交媒體分享預覽縮圖設定 ================= -->
    <meta name="description" content="傳承三十載．家宴慶良辰｜2026年11月27日（五）晚上7:00｜藍田循道衞理小學操場">
    <meta property="og:type" content="website">
    <meta property="og:title" content="藍循三十周年校慶盆菜宴">
    <meta property="og:description" content="傳承三十載．家宴慶良辰｜誠邀您共聚藍循，同賀三十周年校慶！">
    <meta property="og:image" content="https://ltmps-30th.github.io/banquet/banner.jpeg">
    <meta property="og:image:secure_url" content="https://ltmps-30th.github.io/banquet/banner.jpeg">
    <meta property="og:image:type" content="image/jpeg">
    <meta property="og:image:width" content="1200">
    <meta property="og:image:height" content="630">
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:image" content="https://ltmps-30th.github.io/banquet/banner.jpeg">
    <link rel="image_src" href="https://ltmps-30th.github.io/banquet/banner.jpeg">
    <!-- ===================================================================== -->

    <!-- 特效庫 -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    
    <!-- 加入 Firebase 官方 SDK (Firestore 版本) -->
    <script src="https://www.gstatic.com/firebasejs/10.5.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/10.5.0/firebase-firestore-compat.js"></script>

    <style>
        :root {
            --primary-blue: #0033A0;
            --deep-blue: #001f60;
            --gold-light: #FFDF73;
            --gold-main: #D4AF37;
            --gold-dark: #AA8C2C;
            --text-dark: #2c3e50;
            --bg-color: #f4f7fb;
            --danger-color: #ff4d4f;
        }

        html, body { 
            margin: 0; padding: 0; 
            width: 100%; height: 100%; 
            background-color: var(--deep-blue);
            overflow: hidden; 
            font-family: 'PingFang HK', 'Microsoft JhengHei', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background: linear-gradient(135deg, var(--deep-blue) 0%, var(--primary-blue) 100%);
            display: flex; justify-content: center; align-items: center;
        }

        /* 隱藏的縮圖層：供部分通訊軟件爬蟲抓取第一張圖作為預覽 */
        #thumb-layer {
            position: absolute;
            width: 0;
            height: 0;
            overflow: hidden;
            opacity: 0;
            pointer-events: none;
            z-index: -1;
        }

        /* ================= 開場進場畫面 (banquet.jpeg) ================= */
        #splash-screen {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-color: var(--deep-blue);
            z-index: 9999;
            display: flex; justify-content: center; align-items: center;
            transition: opacity 1.2s cubic-bezier(0.4, 0, 0.2, 1), visibility 1.2s;
            cursor: pointer;
        }
        #splash-screen.fade-out {
            opacity: 0;
            visibility: hidden;
            pointer-events: none;
        }
        #splash-screen img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            animation: splashZoom 3s ease-out forwards;
        }
        @keyframes splashZoom {
            from { transform: scale(1); }
            to { transform: scale(1.06); }
        }
        /* ============================================================== */

        /* 夜空與流星特效 */
        #particles { position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: 0; pointer-events: none; overflow: hidden;}
        
        .star { 
            position: absolute; background: #ffffff; border-radius: 50%; 
            box-shadow: 0 0 6px #ffffff, 0 0 12px rgba(255,255,255,0.5); 
            animation: twinkle infinite alternate ease-in-out; opacity: 0.2;
        }
        @keyframes twinkle { 0% { opacity: 0.2; transform: scale(0.6); } 100% { opacity: 1; transform: scale(1.2); } }

        .meteor {
            position: absolute; width: 4px; height: 4px; background: #ffffff; border-radius: 50%;
            box-shadow: 0 0 15px 4px rgba(255, 255, 255, 1); opacity: 0; animation: shootingStar linear infinite;
        }
        .meteor::after {
            content: ''; position: absolute; top: 50%; transform: translateY(-50%); right: 100%; 
            width: 250px; height: 2px; background: linear-gradient(to left, rgba(255,255,255,1) 0%, rgba(255,255,255,0) 100%);
        }
        @keyframes shootingStar {
            0% { transform: rotate(135deg) translateX(0); opacity: 0; }
            5% { opacity: 1; }
            35% { transform: rotate(135deg) translateX(250vw); opacity: 0; }
            100% { transform: rotate(135deg) translateX(250vw); opacity: 0; }
        }

        .container {
            width: 95%; max-width: 600px; height: 90vh; background: var(--bg-color);
            border-radius: 24px; box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4);
            position: relative; z-index: 10; overflow: hidden;
            animation: containerEntrance 0.6s cubic-bezier(0.2, 0.8, 0.2, 1) forwards;
        }

        @keyframes containerEntrance { from { opacity: 0; transform: translateY(30px) scale(0.98); } to { opacity: 1; transform: translateY(0) scale(1); } }

        .page {
            position: absolute; top: 0; left: 0; right: 0; bottom: 0;
            opacity: 0; visibility: hidden; transform: translateX(30px);
            transition: all 0.4s cubic-bezier(0.25, 1, 0.5, 1); 
            overflow-y: auto; -webkit-overflow-scrolling: touch; background: var(--bg-color);
        }
        
        .page.active { opacity: 1; visibility: visible; transform: translateX(0); }
        .page::-webkit-scrollbar { display: none; }

        .app-header {
            background: white; padding: 20px; display: flex; align-items: center; justify-content: space-between;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05); position: sticky; top: 0; z-index: 50;
        }
        
        .back-btn {
            background: rgba(0, 51, 160, 0.08); border: none; color: var(--primary-blue); 
            padding: 8px 15px; border-radius: 20px; font-size: 15px; font-weight: bold;
            cursor: pointer; display: flex; align-items: center; gap: 5px; transition: 0.3s;
        }
        .back-btn:active { background: rgba(0, 51, 160, 0.15); transform: scale(0.95); }
        .app-header h2 { font-size: 18px; color: var(--primary-blue); margin: 0; text-align: center; font-weight: 900; }

        .content-area { padding: 25px 20px 40px 20px; }
        
        /* 首頁橫幅與標題設定 */
        .hero-banner { text-align: center; margin-bottom: 20px; margin-top: 5px; }
        .main-banner-img {
            width: 100%;
            height: auto;
            max-height: 220px;
            object-fit: cover;
            border-radius: 16px;
            margin-bottom: 16px;
            box-shadow: 0 6px 20px rgba(0, 51, 160, 0.12);
            display: block;
        }
        .hero-banner h1 { color: var(--primary-blue); font-size: 26px; font-weight: 900; margin-bottom: 8px; }

        .ui-card {
            background: white; border-radius: 16px; padding: 20px; margin-bottom: 20px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.03); border: 1px solid rgba(0,51,160,0.05);
        }
        
        .info-item { margin-bottom: 15px; font-size: 15px; display: flex; align-items: flex-start; border-bottom: 1px dashed #f0f0f0; padding-bottom: 12px; }
        .info-item:last-child { margin-bottom: 0; border-bottom: none; padding-bottom: 0; }
        .icon { width: 32px; height: 32px; background: rgba(212, 175, 55, 0.15); border-radius: 50%; display: flex; justify-content: center; align-items: center; margin-right: 15px; font-size: 14px; flex-shrink: 0; margin-top: 2px; }

        .program-list { margin: 4px 0 0 0; padding-left: 18px; color: #333; font-weight: bold; font-size: 14px; line-height: 1.7; }
        .donation-tier { background: rgba(0, 51, 160, 0.03); border-left: 3px solid var(--gold-main); padding: 8px 12px; border-radius: 6px; margin-top: 6px; font-size: 14px; line-height: 1.5; color: #333; }

        .btn { 
            background: linear-gradient(135deg, var(--gold-main), var(--gold-dark)); color: white; border: none; 
            padding: 16px 20px; border-radius: 30px; font-size: 17px; cursor: pointer; text-align: center; 
            display: block; width: 100%; font-weight: bold; box-shadow: 0 6px 15px rgba(212, 175, 55, 0.3); transition: all 0.3s; 
        }
        .btn:active { transform: translateY(2px); box-shadow: 0 2px 5px rgba(212, 175, 55, 0.3); }
        .btn-add { background: rgba(0, 51, 160, 0.05); color: var(--primary-blue); border: 1.5px dashed var(--primary-blue); margin-top: 12px; box-shadow: none; padding: 12px 20px; font-size: 15px; }
        .btn-add:hover, .btn-add:active { background: rgba(0, 51, 160, 0.1); transform: none; box-shadow: none;}
        .btn-table { background: rgba(212, 175, 55, 0.12); color: var(--gold-dark); border: 1.5px solid var(--gold-main); margin-top: 10px; box-shadow: none; padding: 12px 20px; font-size: 15px; }

        .sticky-bottom { position: sticky; bottom: 20px; z-index: 40; padding: 0 10px; }

        .section-title { font-size: 17px; color: var(--primary-blue); margin-bottom: 15px; font-weight: bold; border-left: 4px solid var(--gold-main); padding-left: 10px; }
        .form-group { margin-bottom: 18px; }
        label { display: block; font-weight: bold; color: #444; font-size: 14px; margin-bottom: 8px; }
        
        input[type="text"], input[type="tel"], input[type="email"], input[type="number"], select, textarea { 
            width: 100%; max-width: 100%; display: block; box-sizing: border-box; 
            padding: 14px 15px; border: 1.5px solid #dce2e8; border-radius: 12px; 
            font-size: 16px; background: #fdfdfd; transition: all 0.3s; 
            -webkit-appearance: none; appearance: none; margin: 0;
        }
        input:focus, select:focus, textarea:focus { border-color: var(--primary-blue); outline: none; background: white; box-shadow: 0 0 0 3px rgba(0, 51, 160, 0.1); }
        
        /* 隱藏數字輸入框預設的上下加減箭咀 (+1 / -1) */
        input[type="number"]::-webkit-outer-spin-button,
        input[type="number"]::-webkit-inner-spin-button {
            -webkit-appearance: none;
            margin: 0;
        }
        input[type="number"] {
            -moz-appearance: textfield;
        }

        select {
            background-image: url("data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%230033A0%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-12.9%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2012.9l128%20127.9c3.6%203.6%207.8%205.4%2012.8%205.4s9.2-1.8%2012.8-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-12.8%200-5-1.9-9.2-5.5-12.8z%22%2F%3E%3C%2Fsvg%3E");
            background-repeat: no-repeat; background-position: right 15px center; background-size: 12px auto; padding-right: 40px;
        }

        .extra-att-row {
            background: rgba(0,51,160,0.02); border: 1px solid #eee; 
            border-radius: 12px; padding: 15px; margin-bottom: 12px; animation: fadeIn 0.3s ease;
        }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(-5px); } to { opacity: 1; transform: translateY(0); } }

        /* 可選擇的付款方式卡片 */
        .payment-option-card {
            border: 1.5px solid #dce2e8; border-radius: 12px; padding: 15px; margin-bottom: 12px;
            background: #fdfdfd; transition: all 0.25s; cursor: pointer; display: block;
        }
        .payment-option-card.selected {
            border-color: var(--primary-blue); background: rgba(0, 51, 160, 0.03);
            box-shadow: 0 4px 12px rgba(0, 51, 160, 0.08);
        }
        .payment-option-header {
            display: flex; align-items: center; font-weight: bold; color: var(--primary-blue); font-size: 16px;
        }
        .payment-option-header input[type="radio"] {
            width: 20px; height: 20px; margin: 0 10px 0 0; cursor: pointer; accent-color: var(--primary-blue);
        }
        .payment-option-details {
            margin-top: 10px; padding-left: 30px; font-size: 14px; line-height: 1.6; color: #555;
        }
        .highlight-note { color: var(--primary-blue); font-size: 13px; font-weight: bold; display: block; margin-top: 6px; background: rgba(212, 175, 55, 0.15); padding: 8px 10px; border-radius: 8px; }

        .file-upload-wrapper { background: white; padding: 25px 20px; border-radius: 12px; border: 2px dashed var(--gold-main); text-align: center; cursor: pointer; position: relative; transition: all 0.3s; }
        .file-upload-wrapper.error-border { border-color: var(--danger-color); background: rgba(255, 77, 79, 0.04); }
        .file-upload-wrapper input[type="file"] { position: absolute; top: 0; left: 0; width: 100%; height: 100%; opacity: 0; cursor: pointer; }
        
        .summary-row { display: flex; justify-content: space-between; margin-bottom: 8px; font-size: 14px; border-bottom: 1px dashed #f0f0f0; padding-bottom: 8px; }
        .summary-row:last-child { border-bottom: none; margin-bottom: 0; padding-bottom: 0; }
        .summary-label { color: #888; width: 38%; }
        .summary-value { color: #333; font-weight: bold; width: 62%; text-align: right; word-break: break-word; }
        
        .total-price-tag { 
            text-align: center; font-size: 19px; color: var(--primary-blue); font-weight: 900; 
            background: rgba(0,51,160,0.05); padding: 15px; border-radius: 12px; border: 1px solid rgba(0,51,160,0.1); 
            margin-bottom: 20px; transition: 0.3s; line-height: 1.5;
        }

        .draft-notice { background: rgba(212, 175, 55, 0.15); color: var(--gold-dark); text-align: center; padding: 12px; font-size: 14px; font-weight: bold; border-radius: 12px; margin-bottom: 15px; display: none; }

        #loading-overlay { 
            position: absolute; top: 0; left: 0; width: 100%; height: 100%; 
            background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(10px); 
            display: flex; justify-content: center; align-items: center; flex-direction: column; 
            z-index: 100; opacity: 0; visibility: hidden; transition: 0.3s; 
        }
        #loading-overlay.show { opacity: 1; visibility: visible; }
        
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
        .loader-ring { 
            width: 55px; height: 55px; 
            border: 5px solid rgba(0, 51, 160, 0.1); 
            border-top-color: var(--primary-blue); border-left-color: var(--gold-main); 
            border-radius: 50%; animation: spin 1s linear infinite; 
        }
        
        @keyframes pulseText { 0%, 100% { opacity: 1; } 50% { opacity: 0.4; } }
        .pulse-text { animation: pulseText 1.5s infinite; }

        @media screen and (max-width: 600px) {
            body { display: block; background: var(--bg-color); }
            .container { width: 100%; height: 100%; max-height: none; border-radius: 0; border: none; box-shadow: none; }
            .page { padding-bottom: calc(40px + env(safe-area-inset-bottom)); }
            .app-header { padding-top: max(20px, env(safe-area-inset-top)); }
        }
    </style>
</head>
<body>

    <!-- 隱藏的 Thumb Layer (確保將完整網址的 banner.jpeg 放在 HTML 第一順位供 WhatsApp 抓取) -->
    <div id="thumb-layer">
        <img src="https://ltmps-30th.github.io/banquet/banner.jpeg" alt="藍循三十周年校慶盆菜宴預覽圖">
    </div>

    <!-- 開場全螢幕圖片 (banquet.jpeg)，停留後自動淡出，點擊亦可直接淡出 -->
    <div id="splash-screen" onclick="hideSplashScreen()">
        <img src="banquet.jpeg" alt="藍循三十周年校慶盆菜宴" onerror="hideSplashScreen()">
    </div>

    <div id="particles"></div>

    <div class="container">
        <!-- 載入中遮罩 -->
        <div id="loading-overlay">
            <div class="loader-ring"></div>
            <h3 style="margin-top: 25px; color: var(--primary-blue); font-size: 18px;">資料上載中...</h3>
            <p class="pulse-text" style="color: #888; font-size: 14px; margin-top: 10px; font-weight:bold;">請勿關閉視窗，這可能需要幾秒鐘 ⏳</p>
        </div>

        <!-- 1. 首頁 -->
        <div id="home-page" class="page active">
            <div class="content-area" style="padding-top: max(20px, env(safe-area-inset-top));">
                <div class="hero-banner">
                    <img src="https://ltmps-30th.github.io/banquet/banner.jpeg" alt="藍循三十周年校慶盆菜宴橫幅" class="main-banner-img" onerror="this.style.display='none';">
                    <h1>藍循三十周年校慶盆菜宴</h1>
                    <p style="color: var(--gold-dark); font-weight: bold; font-size: 18px; margin-bottom: 10px; letter-spacing: 1px;">傳承三十載．家宴慶良辰</p>
                </div>

                <div class="ui-card">
                    <div class="info-item">
                        <div class="icon">📅</div>
                        <div><span style="color:#888; font-size:12px; display:block;">日期</span><strong>2026年11月27日 (五)</strong></div>
                    </div>
                    <div class="info-item">
                        <div class="icon">⏰</div>
                        <div><span style="color:#888; font-size:12px; display:block;">時間</span><strong>晚上 7:00 至 9:00（6:30恭候）</strong></div>
                    </div>
                    <div class="info-item">
                        <div class="icon">📍</div>
                        <div><span style="color:#888; font-size:12px; display:block;">地點</span><strong>藍田循道衞理小學 操場</strong></div>
                    </div>
                    <div class="info-item">
                        <div class="icon">🎉</div>
                        <div style="width:100%;">
                            <span style="color:#888; font-size:12px; display:block;">內容</span>
                            <ul class="program-list">
                                <li>老師獻唱</li>
                                <li>舞蹈表演</li>
                                <li>老師校友心聲分享</li>
                                <li>歡樂大抽獎</li>
                                <li>校慶紀念品義賣</li>
                            </ul>
                        </div>
                    </div>
                    <div class="info-item" style="border:none; padding-bottom:0;">
                        <div class="icon">💝</div>
                        <div style="width:100%;">
                            <span style="color:#888; font-size:12px; display:block;">捐款</span>
                            <div class="donation-tier">
                                <strong>個人：</strong>凡捐款港幣 220 元贈盆菜宴1位及校慶紀念品一份。
                            </div>
                            <div class="donation-tier" style="margin-top:8px;">
                                <strong>團體：</strong>凡捐款港幣 2520 元贈盆菜宴1席（共12位）及校慶紀念品12份。
                            </div>
                        </div>
                    </div>
                </div>

                <div style="text-align:center; color:#888; font-size:13px; margin-bottom: 20px;">
                    備註：如有查詢，請聯絡校務處謝小姐 (電話：23461033)
                </div>
            </div>

            <div class="sticky-bottom">
                <button class="btn" onclick="switchPage('form-page')">立即填寫報名表</button>
            </div>
        </div>

        <!-- 2. 報名表單頁面 -->
        <div id="form-page" class="page">
            <div class="app-header">
                <button class="back-btn" onclick="switchPage('home-page')">❮ 返回</button>
                <h2>報名表</h2>
                <div style="width: 75px;"></div>
            </div>

            <div class="content-area">
                <div id="draft-notice" class="draft-notice">📝 已自動為您載入上次未完成的紀錄</div>

                <form id="registration-form" onsubmit="event.preventDefault(); goToConfirm();">
                    
                    <!-- 第1位出席者 (聯絡人) -->
                    <div class="ui-card">
                        <div class="section-title">第 1 位出席者 (聯絡人)</div>
                        <div class="form-group">
                            <label>聯絡人姓名 *</label>
                            <input type="text" id="contact-name" required placeholder="請輸入姓名" oninput="updateReceiptFromContact(); saveDraft();">
                        </div>
                        <div class="form-group">
                            <label>身份 *</label>
                            <select id="contact-identity" required onchange="toggleOtherInput()">
                                <option value="">請選擇身份</option>
                                <option value="校友 / 校友家人">1. 校友 / 校友家人</option>
                                <option value="其他">2. 其他</option>
                            </select>
                            <input type="text" id="contact-identity-other" placeholder="請註明其他身份" style="display:none; margin-top:10px;" oninput="saveDraft()">
                        </div>
                        <div class="form-group">
                            <label>聯絡電話 *</label>
                            <input type="tel" id="contact-phone" required placeholder="請輸入手提號碼" oninput="saveDraft()">
                        </div>
                        <div class="form-group" style="margin-bottom:0;">
                            <label>電郵地址 (接收確認信及電子收據) *</label>
                            <input type="email" id="contact-email" required placeholder="example@email.com" oninput="saveDraft()">
                        </div>
                    </div>

                    <!-- 其他同行出席者 -->
                    <div class="ui-card">
                        <div class="section-title" style="border-color:var(--primary-blue);">同行出席者 (如有)</div>
                        <p style="font-size:13px; color:#888; margin-bottom:15px;">只需提供姓名。如滿 12 位（1席）將自動以團體捐款 HK$ 2,520 計算。</p>
                        
                        <div id="extra-attendees-container">
                            <!-- JS 動態加入的欄位會出現於此 -->
                        </div>

                        <button type="button" class="btn btn-add" onclick="addAttendee()">+ 增加出席人數 (每位 HK$ 220)</button>
                        <button type="button" class="btn btn-table" onclick="fillFullTable()">🎉 團體包席：一鍵加滿至 12 位 (HK$ 2,520)</button>
                    </div>

                    <!-- 額外捐款 (已移除上下加減箭咀並防止滾輪誤觸) -->
                    <div class="form-group" style="margin-bottom: 20px;">
                        <label style="color:var(--gold-dark); font-size:15px;">💖 額外捐款 (HK$)</label>
                        <input type="number" id="extra-donation" min="0" inputmode="numeric" pattern="[0-9]*" placeholder="填寫金額 (可留空)" oninput="updateTotal(); saveDraft();" onwheel="this.blur()">
                    </div>

                    <div class="total-price-tag" id="display-total">應付總額：HK$ 220 (個人 1 位)</div>

                    <!-- 付款及收據卡片 -->
                    <div class="ui-card">
                        <div class="section-title">收據及付款詳情</div>
                        
                        <div class="form-group" style="margin-bottom:18px;">
                            <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:8px;">
                                <label style="margin:0;">付款收據抬頭 *</label>
                                <label style="font-size:13px; color:var(--primary-blue); cursor:pointer; font-weight:bold; display:flex; align-items:center; margin:0;">
                                    <input type="checkbox" id="same-as-contact-checkbox" onchange="copyContactToReceipt()" style="width:16px; height:16px; margin:0 6px 0 0; cursor:pointer;"> 與聯絡人相同
                                </label>
                            </div>
                            <input type="text" id="receipt-title" required placeholder="請填寫收據抬頭 (例如機構或個人名稱)" oninput="saveDraft()">
                        </div>

                        <!-- 收據特別請求 -->
                        <div class="form-group" style="margin-bottom:22px;">
                            <label>如對收據抬頭有特別請求，請註明</label>
                            <input type="text" id="receipt-request" placeholder="例如：需分開收據或其他備註 (可留空)" oninput="saveDraft()">
                        </div>

                        <!-- 可供選擇的付款方式 -->
                        <div class="form-group" style="margin-bottom:20px;">
                            <label style="font-size:15px; color:var(--primary-blue); margin-bottom:12px;">💳 請選擇付款方式 *</label>
                            
                            <label class="payment-option-card selected" id="pay-card-bank" onclick="selectPaymentMethod('銀行轉帳')">
                                <div class="payment-option-header">
                                    <input type="radio" name="paymentMethod" value="銀行轉帳" checked onchange="selectPaymentMethod('銀行轉帳')">
                                    1. 銀行轉帳（電子轉帳 / 櫃員機轉帳）
                                </div>
                                <div class="payment-option-details">
                                    銀行：滙豐銀行 (銀行編號：004)<br>
                                    戶口號碼：<strong>456-450485-001</strong><br>
                                    戶口名稱：藍田循道衛理小學法團校董會<br>
                                    或 The IMC of Lam Tin Methodist Primary School
                                    <span class="highlight-note">註：請保留電子轉帳的入數截圖 或 櫃員機入數紙照片，並於下方上傳。</span>
                                </div>
                            </label>

                            <label class="payment-option-card" id="pay-card-cheque" onclick="selectPaymentMethod('支票')">
                                <div class="payment-option-header">
                                    <input type="radio" name="paymentMethod" value="支票" onchange="selectPaymentMethod('支票')">
                                    2. 支票
                                </div>
                                <div class="payment-option-details">
                                    支票抬頭：藍田循道衛理小學法團校董會<br>
                                    或 The IMC of Lam Tin Methodist Primary School<br>
                                    支票背面請寫上姓名、電話及「藍循30周年盆菜宴」以資識別。
                                    <span class="highlight-note">註：直接到校遞交或郵寄：九龍藍田平田邨安田街 藍田循道衞理小學 梁校長收</span>
                                </div>
                            </label>

                            <label class="payment-option-card" id="pay-card-cash" onclick="selectPaymentMethod('現金')">
                                <div class="payment-option-header">
                                    <input type="radio" name="paymentMethod" value="現金" onchange="selectPaymentMethod('現金')">
                                    3. 現金
                                </div>
                                <div class="payment-option-details">
                                    直接到校支付現金。請聯絡校務處謝小姐 (電話：23461033)。
                                </div>
                            </label>
                        </div>

                        <div class="form-group" style="margin-bottom:0;" id="upload-group">
                            <label id="upload-label" style="color:var(--danger-color);">上載付款證明 (銀行轉帳必須上載入數截圖或收據) *</label>
                            <div class="file-upload-wrapper" id="file-upload-box">
                                <input type="file" id="payment-proof" accept="image/*" onchange="updateFileName(this)">
                                <div id="file-name-display" style="color:#888;">📁 點擊上載截圖<br><span style="font-size:12px;">(支援 JPG, PNG)</span></div>
                            </div>
                        </div>
                    </div>

                    <button type="submit" id="hidden-submit-btn" style="display:none;"></button>
                </form>
            </div>

            <div class="sticky-bottom">
                <button class="btn" onclick="document.getElementById('hidden-submit-btn').click();">繼續核對資料</button>
            </div>
        </div>

        <!-- 3. 確認與提交頁面 -->
        <div id="confirm-page" class="page">
            <div class="app-header">
                <button class="back-btn" onclick="switchPage('form-page')">❮ 修改</button>
                <h2>確認資料</h2>
                <div style="width: 75px;"></div>
            </div>
            
            <div class="content-area">
                <div id="summary-content">
                    <!-- Javascript 會將填寫的資料注入這裡 -->
                </div>
            </div>

            <div class="sticky-bottom">
                <button class="btn" onclick="submitFinalData()">確認無誤，正式提交</button>
            </div>
        </div>
    </div>

    <script>
        // ================= 開場圖片淡出控制 =================
        function hideSplashScreen() {
            const splash = document.getElementById('splash-screen');
            if (splash && !splash.classList.contains('fade-out')) {
                splash.classList.add('fade-out');
            }
        }
        window.addEventListener('load', () => {
            setTimeout(hideSplashScreen, 1800);
        });
        setTimeout(hideSplashScreen, 3200);
        // ====================================================

        // ================= Firebase (Firestore) 初始化設定 =================
        const firebaseConfig = {
            apiKey: "AIzaSyBr0-oNmRN859g6bfGDVjSdA1brJC8CxNs",
            authDomain: "ltmps-c92a0.firebaseapp.com",
            projectId: "ltmps-c92a0",
            storageBucket: "ltmps-c92a0.firebasestorage.app",
            messagingSenderId: "716255242034",
            appId: "1:716255242034:web:b25a037869d8a9de6f992b"
        };
        firebase.initializeApp(firebaseConfig);
        const db = firebase.firestore();
        // =======================================================

        function createParticles() {
            const container = document.getElementById('particles');
            for(let i = 0; i < 40; i++) {
                let star = document.createElement('div');
                star.className = 'star';
                star.style.left = Math.random() * 100 + 'vw';
                star.style.top = Math.random() * 100 + 'vh';
                star.style.width = Math.random() * 3 + 1 + 'px';
                star.style.height = star.style.width;
                star.style.animationDuration = Math.random() * 3 + 2 + 's';
                star.style.animationDelay = '-' + (Math.random() * 5) + 's';
                container.appendChild(star);
            }
            for(let i = 0; i < 6; i++) {
                let meteor = document.createElement('div');
                meteor.className = 'meteor';
                meteor.style.top = (Math.random() * 60 - 20) + 'vh'; 
                meteor.style.left = (Math.random() * 100 + 10) + 'vw'; 
                meteor.style.animationDuration = (Math.random() * 6 + 10) + 's';
                meteor.style.animationDelay = (Math.random() * 15) + 's';
                container.appendChild(meteor);
            }
            let firstMeteor = document.createElement('div');
            firstMeteor.className = 'meteor';
            firstMeteor.style.top = '-10vh';
            firstMeteor.style.left = '70vw';
            firstMeteor.style.animationDuration = '12s'; 
            firstMeteor.style.animationDelay = '1s';
            container.appendChild(firstMeteor);
        }
        createParticles();

        function switchPage(pageId) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            document.getElementById(pageId).scrollTop = 0;
        }

        function toggleOtherInput() {
            const select = document.getElementById('contact-identity');
            const otherInput = document.getElementById('contact-identity-other');
            if (select.value === '其他') {
                otherInput.style.display = 'block';
                otherInput.required = true;
            } else {
                otherInput.style.display = 'none';
                otherInput.required = false;
                otherInput.value = '';
            }
            saveDraft();
        }

        function copyContactToReceipt() {
            if (document.getElementById('same-as-contact-checkbox').checked) {
                document.getElementById('receipt-title').value = document.getElementById('contact-name').value;
            } else {
                document.getElementById('receipt-title').value = '';
            }
            saveDraft();
        }

        function updateReceiptFromContact() {
            if (document.getElementById('same-as-contact-checkbox').checked) {
                document.getElementById('receipt-title').value = document.getElementById('contact-name').value;
            }
        }

        // 切換付款方式時，動態更新上載證明的必填提示
        function selectPaymentMethod(method) {
            const radios = document.getElementsByName('paymentMethod');
            radios.forEach(r => {
                if (r.value === method) r.checked = true;
            });

            document.getElementById('pay-card-bank').classList.toggle('selected', method === '銀行轉帳');
            document.getElementById('pay-card-cheque').classList.toggle('selected', method === '支票');
            document.getElementById('pay-card-cash').classList.toggle('selected', method === '現金');

            const uploadLabel = document.getElementById('upload-label');
            const uploadBox = document.getElementById('file-upload-box');

            if (method === '銀行轉帳') {
                uploadLabel.innerText = '上載付款證明 (銀行轉帳必須上載入數截圖或收據) *';
                uploadLabel.style.color = 'var(--danger-color)';
            } else {
                uploadLabel.innerText = '上載付款證明 (選擇支票或現金可免填)';
                uploadLabel.style.color = '#444';
                uploadBox.classList.remove('error-border');
            }

            saveDraft();
        }

        function getSelectedPaymentMethod() {
            const checked = document.querySelector('input[name="paymentMethod"]:checked');
            return checked ? checked.value : '銀行轉帳';
        }

        let nextAttId = 2; 

        function addAttendee(name = '') {
            const currentPax = document.querySelectorAll('.extra-att-row').length + 1;
            if(currentPax >= 12) {
                alert('已達每席 12 人上限！');
                return;
            }

            const container = document.getElementById('extra-attendees-container');
            const div = document.createElement('div');
            div.className = 'extra-att-row';
            div.id = 'extra-att-' + nextAttId;
            
            div.innerHTML = `
                <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:8px;">
                    <label style="margin:0; color:var(--primary-blue);">第 <span class="att-num"></span> 位出席者</label>
                    <button type="button" style="background:none; border:none; color:var(--danger-color); font-size:13px; font-weight:bold; cursor:pointer; padding:5px;" onclick="removeAttendee('${div.id}')">✖ 移除</button>
                </div>
                <input type="text" class="extra-att-input" value="${name}" required placeholder="同行者姓名 (如待定可填「待定」)" oninput="saveDraft()">
            `;
            container.appendChild(div);
            nextAttId++;
            
            updateTotal();
            saveDraft();
        }

        function fillFullTable() {
            let currentPax = document.querySelectorAll('.extra-att-row').length + 1;
            if (currentPax >= 12) {
                alert('目前已是 12 人（1席）！');
                return;
            }
            while (currentPax < 12) {
                addAttendee('');
                currentPax++;
            }
        }

        function removeAttendee(id) {
            document.getElementById(id).remove();
            updateTotal();
            saveDraft();
        }

        function calculateMealCost(pax) {
            return (pax === 12) ? 2520 : (pax * 220);
        }

        function updateTotal() {
            const extraRows = document.querySelectorAll('.extra-att-row');
            extraRows.forEach((row, index) => {
                row.querySelector('.att-num').innerText = index + 2; 
            });

            const totalPax = 1 + extraRows.length;
            const mealCost = calculateMealCost(totalPax);
            const extraDonation = parseInt(document.getElementById('extra-donation').value) || 0;
            const totalAmt = mealCost + extraDonation;
            
            let tierDesc = (totalPax === 12) ? `團體 1 席 12 位 $2,520` : `個人 ${totalPax} 位 $${mealCost}`;
            let extraText = extraDonation > 0 ? ` + 額外捐款 $${extraDonation}` : "";
            document.getElementById('display-total').innerText = `應付總額：HK$ ${totalAmt}\n(${tierDesc}${extraText})`;
        }

        function getExtraAttendees() {
            const inputs = document.querySelectorAll('.extra-att-input');
            let names = [];
            inputs.forEach(input => {
                if(input.value.trim() !== '') names.push(input.value.trim());
            });
            return names;
        }

        // ================= 圖片預覽功能 =================
        let previewImageSrc = "";

        function updateFileName(input) {
            const display = document.getElementById('file-name-display');
            const uploadBox = document.getElementById('file-upload-box');
            if (input.files && input.files.length > 0) {
                const file = input.files[0];
                display.innerHTML = `<span style="color:var(--primary-blue); font-weight:bold;">✓ 已選擇：${file.name}</span>`;
                uploadBox.classList.remove('error-border');
                uploadBox.style.borderColor = "var(--primary-blue)";
                
                const reader = new FileReader();
                reader.onload = function(e) {
                    previewImageSrc = e.target.result;
                };
                reader.readAsDataURL(file);

            } else {
                display.innerHTML = '📁 點擊上載截圖<br><span style="font-size:12px;">(支援 JPG, PNG)</span>';
                uploadBox.style.borderColor = "var(--gold-main)";
                previewImageSrc = "";
            }
        }
        // ===============================================

        function goToConfirm() {
            const payment_method = getSelectedPaymentMethod();
            const fileInput = document.getElementById('payment-proof');

            // 【核心防呆驗證】若選擇「銀行轉帳」，強制檢查是否已上載圖片
            if (payment_method === '銀行轉帳' && fileInput.files.length === 0) {
                alert('⚠️ 您選擇了「銀行轉帳」，請先上載入數截圖或櫃員機收據照片方可提交！');
                const uploadBox = document.getElementById('file-upload-box');
                uploadBox.classList.add('error-border');
                document.getElementById('upload-group').scrollIntoView({ behavior: 'smooth', block: 'center' });
                return;
            }

            saveDraft();

            const c_id = document.getElementById('contact-identity').value;
            const c_id_other = document.getElementById('contact-identity-other').value;
            const final_c_id = (c_id === '其他' && c_id_other) ? `其他 (${c_id_other})` : c_id;
            
            const c_name = document.getElementById('contact-name').value;
            const c_phone = document.getElementById('contact-phone').value;
            const c_email = document.getElementById('contact-email').value;
            const receipt_title = document.getElementById('receipt-title').value;
            const receipt_request = document.getElementById('receipt-request').value.trim();
            
            const fileName = fileInput.files.length > 0 ? fileInput.files[0].name : '未上載';

            const extraNames = getExtraAttendees();
            const totalPax = 1 + extraNames.length;
            const mealCost = calculateMealCost(totalPax);
            const extraDonation = parseInt(document.getElementById('extra-donation').value) || 0;
            const totalAmt = mealCost + extraDonation;
            const tierType = (totalPax === 12) ? `團體盆菜宴 (1席12位 HK$ 2,520)` : `個人盆菜宴 (${totalPax}位 HK$ ${mealCost})`;

            let summaryHTML = `
                <div class="ui-card">
                    <h4 style="color:var(--primary-blue); margin-top:0; margin-bottom:15px; border-bottom:2px solid #f0f0f0; padding-bottom:10px;">聯絡人 (第 1 位)</h4>
                    <div class="summary-row"><span class="summary-label">姓名</span><span class="summary-value">${c_name}</span></div>
                    <div class="summary-row"><span class="summary-label">身份</span><span class="summary-value">${final_c_id}</span></div>
                    <div class="summary-row"><span class="summary-label">電話</span><span class="summary-value">${c_phone}</span></div>
                    <div class="summary-row"><span class="summary-label">電郵</span><span class="summary-value">${c_email}</span></div>
                </div>
            `;

            if(extraNames.length > 0) {
                summaryHTML += `<div class="ui-card">
                    <h4 style="color:var(--primary-blue); margin-top:0; margin-bottom:15px; border-bottom:2px solid #f0f0f0; padding-bottom:10px;">同行出席者</h4>`;
                
                extraNames.forEach((name, index) => {
                    summaryHTML += `
                        <div class="summary-row"><span class="summary-label" style="color:#333;">第 ${index + 2} 位</span><span class="summary-value">${name}</span></div>
                    `;
                });
                summaryHTML += `</div>`;
            }

            let requestHtml = `<div class="summary-row"><span class="summary-label">收據特別請求</span><span class="summary-value">${receipt_request || "無"}</span></div>`;

            let donationHtml = extraDonation > 0 
                ? `<div class="summary-row"><span class="summary-label">額外捐款</span><span class="summary-value" style="color:var(--gold-dark);">HK$ ${extraDonation}</span></div>` 
                : "";

            let proofDisplay = `<span style="color:var(--gold-dark);">${fileName}</span>`;
            if (previewImageSrc) {
                proofDisplay += `<br><img src="${previewImageSrc}" style="max-width: 100%; max-height: 250px; margin-top: 12px; border-radius: 8px; border: 1.5px solid #eee; display: block; margin-left: auto;">`;
            }

            summaryHTML += `
                <div class="ui-card">
                    <h4 style="color:var(--primary-blue); margin-top:0; margin-bottom:15px; border-bottom:2px solid #f0f0f0; padding-bottom:10px;">收據及付款詳情</h4>
                    <div class="summary-row"><span class="summary-label">席數類別</span><span class="summary-value">${tierType}</span></div>
                    ${donationHtml}
                    <div class="summary-row"><span class="summary-label">收據抬頭</span><span class="summary-value">${receipt_title}</span></div>
                    ${requestHtml}
                    <div class="summary-row"><span class="summary-label">付款方式</span><span class="summary-value" style="color:var(--primary-blue);">${payment_method}</span></div>
                    <div class="summary-row" style="flex-direction: column; align-items:flex-end; border:none; margin-bottom:0; padding-bottom:0;">
                        <span class="summary-label" style="width:100%; text-align:left; margin-bottom:8px;">付款證明</span>
                        <span class="summary-value" style="width:100%;">${proofDisplay}</span>
                    </div>
                    
                    <div class="total-price-tag" style="margin-top:20px; font-size:18px;">應付總額：HK$ ${totalAmt}</div>
                </div>
            `;

            document.getElementById('summary-content').innerHTML = summaryHTML;
            switchPage('confirm-page');
        }

        const DRAFT_KEY = 'ltmps_gala_30_draft_v11';

        function saveDraft() {
            const extraNames = [];
            document.querySelectorAll('.extra-att-input').forEach(input => extraNames.push(input.value));
            
            const draft = {
                cName: document.getElementById('contact-name').value,
                cIdentity: document.getElementById('contact-identity').value,
                cIdentityOther: document.getElementById('contact-identity-other').value,
                cPhone: document.getElementById('contact-phone').value,
                cEmail: document.getElementById('contact-email').value,
                receiptTitle: document.getElementById('receipt-title').value,
                receiptRequest: document.getElementById('receipt-request').value,
                paymentMethod: getSelectedPaymentMethod(),
                sameAsContactReceipt: document.getElementById('same-as-contact-checkbox').checked,
                extraDonation: document.getElementById('extra-donation').value,
                extraNames: extraNames
            };
            localStorage.setItem(DRAFT_KEY, JSON.stringify(draft));
        }

        function loadDraft() {
            const draftJSON = localStorage.getItem(DRAFT_KEY);
            if (draftJSON) {
                try {
                    const draft = JSON.parse(draftJSON);
                    if (draft.cName) document.getElementById('contact-name').value = draft.cName;
                    if (draft.cIdentity) document.getElementById('contact-identity').value = draft.cIdentity;
                    if (draft.cIdentityOther) document.getElementById('contact-identity-other').value = draft.cIdentityOther;
                    if (draft.cPhone) document.getElementById('contact-phone').value = draft.cPhone;
                    if (draft.cEmail) document.getElementById('contact-email').value = draft.cEmail;
                    if (draft.receiptTitle) document.getElementById('receipt-title').value = draft.receiptTitle;
                    if (draft.receiptRequest) document.getElementById('receipt-request').value = draft.receiptRequest;
                    if (draft.extraDonation) document.getElementById('extra-donation').value = draft.extraDonation;
                    if (draft.paymentMethod) selectPaymentMethod(draft.paymentMethod);
                    
                    if (draft.sameAsContactReceipt !== undefined) {
                        document.getElementById('same-as-contact-checkbox').checked = draft.sameAsContactReceipt;
                    }

                    toggleOtherInput();

                    if (draft.extraNames && Array.isArray(draft.extraNames)) {
                        draft.extraNames.forEach(name => addAttendee(name));
                    }
                    
                    if(draft.cName || (draft.extraNames && draft.extraNames.length > 0)) {
                        document.getElementById('draft-notice').style.display = 'block';
                        setTimeout(() => { document.getElementById('draft-notice').style.display = 'none'; }, 4000);
                    }
                } catch(e) {}
            }
            updateTotal();
        }

        window.addEventListener('DOMContentLoaded', () => {
            loadDraft();     
        });

        function fireConfetti() {
            var end = Date.now() + 4000;
            (function frame() {
                confetti({ particleCount: 5, angle: 60, spread: 55, origin: { x: 0 }, colors: ['#0033A0', '#D4AF37', '#ffffff'] });
                confetti({ particleCount: 5, angle: 120, spread: 55, origin: { x: 1 }, colors: ['#0033A0', '#D4AF37', '#ffffff'] });
                if (Date.now() < end) requestAnimationFrame(frame);
            }());
        }

        function submitFinalData() {
            const fileInput = document.getElementById('payment-proof');
            const paymentMethod = getSelectedPaymentMethod();

            // 二次安全檢查：確保銀行轉帳必定有上載圖片
            if (paymentMethod === '銀行轉帳' && fileInput.files.length === 0) {
                alert('⚠️ 選擇銀行轉帳必須上載付款證明！');
                switchPage('form-page');
                return;
            }

            const extraNames = getExtraAttendees();
            const totalPax = 1 + extraNames.length;
            const mealCost = calculateMealCost(totalPax);
            const extraDonation = parseInt(document.getElementById('extra-donation').value) || 0;
            const totalAmt = mealCost + extraDonation;
            const tierType = (totalPax === 12) ? "團體 (1席12位)" : `個人 (${totalPax}位)`;

            const payload = {
                formType: "校友報名",
                name: document.getElementById('contact-name').value,
                phone: document.getElementById('contact-phone').value,
                email: document.getElementById('contact-email').value,
                
                contactIdentity: document.getElementById('contact-identity').value,
                contactIdentityOther: document.getElementById('contact-identity-other').value,
                receiptTitle: document.getElementById('receipt-title').value,
                receiptRequest: document.getElementById('receipt-request').value.trim() || "無",
                paymentMethod: paymentMethod,
                tierType: tierType,
                pax: totalPax,
                extraDonation: extraDonation,
                totalAmount: totalAmt,
                extraAttendees: JSON.stringify(extraNames)
            };

            if (fileInput.files.length > 0) {
                const file = fileInput.files[0];
                const reader = new FileReader();
                reader.onload = function(event) {
                    payload.fileData = event.target.result.split(',')[1];
                    payload.fileName = file.name;
                    payload.mimeType = file.type;
                    sendFetchAndSaveToFirestore(payload);
                };
                reader.readAsDataURL(file);
            } else {
                sendFetchAndSaveToFirestore(payload);
            }
        }

        function sendFetchAndSaveToFirestore(payload) {
            document.getElementById('loading-overlay').classList.add('show');
            
            const scriptURL = 'https://script.google.com/macros/s/AKfycbx77jeCm1BoEI77qhXHaMB6Q-JjFvSVGEMVTYTboXdhrT1nByZj4OpTOuznWOHUWz1y/exec';

            fetch(scriptURL, {
                method: 'POST',
                redirect: 'follow', 
                headers: { 'Content-Type': 'text/plain;charset=utf-8' },
                body: JSON.stringify(payload)
            })
            .then(response => response.json())
            .then(data => {
                if(data.status === 'success') {
                    
                    const finalIdentity = (payload.contactIdentity === '其他' && payload.contactIdentityOther) 
                        ? `其他 (${payload.contactIdentityOther})` 
                        : payload.contactIdentity;

                    const extraList = JSON.parse(payload.extraAttendees);
                    const extraStr = extraList.length > 0 ? extraList.join(" , ") : "無同行者";

                    // 完整同步寫入 Firestore (包含 receiptRequest 及 paymentMethod)
                    db.collection('registrations').add({
                        timestamp: new Date().toISOString(),
                        formType: payload.formType,
                        contactName: payload.name,
                        contactIdentity: finalIdentity,
                        contactPhone: payload.phone,
                        contactEmail: payload.email,
                        receiptTitle: payload.receiptTitle,
                        receiptRequest: payload.receiptRequest,
                        paymentMethod: payload.paymentMethod,
                        tierType: payload.tierType,
                        pax: payload.pax,
                        extraDonation: payload.extraDonation,
                        totalAmount: payload.totalAmount,
                        extraAttendees: extraStr, 
                        paymentProofUrl: data.fileUrl || "未有上載"
                    })
                    .then(() => {
                        document.getElementById('loading-overlay').classList.remove('show');
                        localStorage.removeItem(DRAFT_KEY); 
                        fireConfetti();
                        setTimeout(() => {
                            alert('🎉 報名成功！我們已發送確認電郵至您的郵箱。');
                            window.location.reload(); 
                        }, 600);
                    })
                    .catch(err => {
                        document.getElementById('loading-overlay').classList.remove('show');
                        alert('🎉 報名成功！確認電郵已寄出。(唯資料庫連線不穩，請聯絡校方核對)');
                        console.error("Firestore Error: ", err);
                    });

                } else {
                    document.getElementById('loading-overlay').classList.remove('show');
                    alert('發生錯誤：' + (data.message || '請稍後再試。'));
                }
            })
            .catch(error => {
                document.getElementById('loading-overlay').classList.remove('show');
                alert('系統連線異常。請確定網路狀態或聯絡校方。');
            });
        }
    </script>
</body>
</html>
