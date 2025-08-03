<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Network Scanner Pro - مراقب الشبكات المحترف</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <link href="https://img.icons8.com/?size=160&id=oOrqjtiYHzFl&format=png" rel="icon">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0c0c0c 0%, #1a1a2e 100%);
            color: #ffffff;
            min-height: 100vh;
            direction: rtl;
        }

        /* Navbar */
        .navbar {
            background: rgba(0, 0, 0, 0.9);
            backdrop-filter: blur(10px);
            padding: 1rem 0;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            border-bottom: 1px solid rgba(0, 255, 255, 0.3);
        }

        .nav-container {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 2rem;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: bold;
            color: #00ffff;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .nav-links {
            display: flex;
            list-style: none;
            gap: 2rem;
            align-items: center;
        }

        .nav-links a {
            color: #ffffff;
            text-decoration: none;
            transition: all 0.3s ease;
            padding: 0.5rem 1rem;
            border-radius: 5px;
            position: relative;
        }

        .nav-links a:hover {
            color: #00ffff;
            background: rgba(0, 255, 255, 0.1);
            transform: translateY(-2px);
        }

        /* Main Content */
        .main-content {
            margin-top: 80px;
            padding: 2rem;
            max-width: 1600px;
            margin-left: auto;
            margin-right: auto;
        }

        .hero-section {
            text-align: center;
            padding: 3rem 0;
            background: linear-gradient(135deg, rgba(0, 255, 255, 0.1) 0%, rgba(255, 0, 255, 0.1) 100%);
            border-radius: 20px;
            margin-bottom: 3rem;
            border: 1px solid rgba(0, 255, 255, 0.3);
            position: relative;
            overflow: hidden;
        }

        .hero-section::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(0, 255, 255, 0.1) 0%, transparent 70%);
            animation: rotate 20s linear infinite;
        }

        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        .hero-title {
            font-size: 3rem;
            margin-bottom: 1rem;
            background: linear-gradient(45deg, #00ffff, #ff00ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            position: relative;
            z-index: 1;
        }

        .hero-subtitle {
            font-size: 1.2rem;
            opacity: 0.8;
            margin-bottom: 2rem;
            position: relative;
            z-index: 1;
        }

        /* Control Panel */
        .control-panel {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 2rem;
            margin-bottom: 2rem;
            border: 1px solid rgba(0, 255, 255, 0.2);
            backdrop-filter: blur(10px);
        }

        .scan-controls {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            margin-bottom: 2rem;
        }

        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            font-weight: 600;
            position: relative;
            overflow: hidden;
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.5s;
        }

        .btn:hover::before {
            left: 100%;
        }

        .btn-primary {
            background: linear-gradient(45deg, #00ffff, #0099ff);
            color: #000;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(0, 255, 255, 0.3);
        }

        .btn-secondary {
            background: linear-gradient(45deg, #ff00ff, #ff6699);
            color: #fff;
        }

        .btn-secondary:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(255, 0, 255, 0.3);
        }

        .btn-success {
            background: linear-gradient(45deg, #00ff88, #00cc66);
            color: #000;
        }

        .btn-warning {
            background: linear-gradient(45deg, #ffaa00, #ff8800);
            color: #000;
        }

        /* Two Column Layout */
        .main-grid {
            display: grid;
            grid-template-columns: 1fr 400px;
            gap: 2rem;
            margin-bottom: 2rem;
        }

        .networks-column {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 2rem;
            border: 1px solid rgba(0, 255, 255, 0.2);
        }

        .details-column {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 15px;
            padding: 2rem;
            border: 1px solid rgba(255, 0, 255, 0.2);
            max-height: 800px;
            overflow-y: auto;
        }

        /* Statistics Cards */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            margin-bottom: 2rem;
        }

        .stat-card {
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.1) 0%, rgba(255, 255, 255, 0.05) 100%);
            border-radius: 15px;
            padding: 1.5rem;
            text-align: center;
            border: 1px solid rgba(0, 255, 255, 0.2);
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .stat-card:hover {
            transform: translateY(-5px) scale(1.02);
            border-color: rgba(0, 255, 255, 0.5);
        }

        .stat-icon {
            font-size: 2.5rem;
            margin-bottom: 0.5rem;
            color: #00ffff;
        }

        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            margin-bottom: 0.5rem;
            color: #ffffff;
        }

        .stat-label {
            font-size: 0.9rem;
            opacity: 0.8;
        }

        /* Networks Table */
        .section-title {
            font-size: 1.8rem;
            margin-bottom: 1.5rem;
            text-align: center;
            color: #00ffff;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
        }

        .table-container {
            overflow-x: auto;
            border-radius: 10px;
            max-height: 500px;
            overflow-y: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: rgba(0, 0, 0, 0.3);
        }

        th, td {
            padding: 0.8rem;
            text-align: right;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 0.9rem;
        }

        th {
            background: linear-gradient(45deg, #00ffff, #0099ff);
            color: #000;
            font-weight: bold;
            position: sticky;
            top: 0;
            z-index: 10;
        }

        .network-row {
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .network-row:hover {
            background: rgba(0, 255, 255, 0.1);
            transform: scale(1.01);
        }

        .network-row.selected {
            background: rgba(0, 255, 255, 0.2);
            border: 2px solid #00ffff;
        }

        .signal-strength {
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .signal-bars {
            display: flex;
            gap: 2px;
        }

        .bar {
            width: 3px;
            height: 15px;
            background: #333;
            border-radius: 2px;
        }

        .bar.active {
            background: linear-gradient(to top, #ff0000, #ffff00, #00ff00);
        }

        .security-badge, .network-type {
            padding: 0.2rem 0.6rem;
            border-radius: 15px;
            font-size: 0.7rem;
            font-weight: bold;
        }

        .wpa3 { background: #00ff00; color: #000; }
        .wpa2 { background: #ffff00; color: #000; }
        .wep { background: #ff6600; color: #fff; }
        .open { background: #ff0000; color: #fff; }

        .wifi { background: #0099ff; color: #fff; }
        .mobile-5g { background: #ff00ff; color: #fff; }
        .mobile-4g { background: #9900ff; color: #fff; }
        .mobile-3g { background: #ff6600; color: #fff; }

        .status-indicator {
            display: inline-block;
            width: 8px;
            height: 8px;
            border-radius: 50%;
            margin-left: 0.5rem;
        }

        .hidden { background: #ff6600; }
        .visible { background: #00ff00; }

        /* Network Details Panel */
        .network-details {
            display: none;
        }

        .network-details.show {
            display: block;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateX(20px); }
            to { opacity: 1; transform: translateX(0); }
        }

        .detail-header {
            text-align: center;
            margin-bottom: 2rem;
            padding: 1rem;
            background: linear-gradient(45deg, rgba(0, 255, 255, 0.1), rgba(255, 0, 255, 0.1));
            border-radius: 10px;
            border: 1px solid rgba(0, 255, 255, 0.3);
        }

        .detail-ssid {
            font-size: 1.5rem;
            font-weight: bold;
            color: #00ffff;
            margin-bottom: 0.5rem;
        }

        .detail-type {
            font-size: 1rem;
            opacity: 0.8;
        }

        .detail-section {
            margin-bottom: 2rem;
            padding: 1rem;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
            border-left: 4px solid #00ffff;
        }

        .detail-section h3 {
            color: #00ffff;
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .detail-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.5rem 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .detail-item:last-child {
            border-bottom: none;
        }

        .detail-label {
            font-weight: 600;
            opacity: 0.8;
        }

        .detail-value {
            font-weight: bold;
            color: #00ffff;
        }

        /* Charts */
        .chart-container {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            padding: 1rem;
            margin: 1rem 0;
            height: 200px;
        }

        /* Advanced Tools */
        .tools-section {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 1rem;
            margin: 1rem 0;
        }

        .tool-btn {
            padding: 0.8rem;
            background: linear-gradient(45deg, rgba(0, 255, 255, 0.1), rgba(255, 0, 255, 0.1));
            border: 1px solid rgba(0, 255, 255, 0.3);
            border-radius: 8px;
            color: #fff;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
            font-size: 0.9rem;
        }

        .tool-btn:hover {
            background: linear-gradient(45deg, rgba(0, 255, 255, 0.2), rgba(255, 0, 255, 0.2));
            transform: translateY(-2px);
        }

        /* Security Analysis */
        .security-score {
            text-align: center;
            padding: 1rem;
            border-radius: 10px;
            margin: 1rem 0;
        }

        .score-excellent { background: linear-gradient(45deg, #00ff88, #00cc66); }
        .score-good { background: linear-gradient(45deg, #ffff00, #cccc00); }
        .score-poor { background: linear-gradient(45deg, #ff6600, #cc4400); }
        .score-critical { background: linear-gradient(45deg, #ff0000, #cc0000); }

        .score-number {
            font-size: 3rem;
            font-weight: bold;
            color: #000;
        }

        .score-label {
            font-size: 1rem;
            color: #000;
            font-weight: bold;
        }

        /* Real-time Monitoring */
        .monitoring-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 0.5rem;
            margin: 1rem 0;
        }

        .monitor-item {
            background: rgba(0, 0, 0, 0.3);
            padding: 0.8rem;
            border-radius: 8px;
            text-align: center;
            border: 1px solid rgba(0, 255, 255, 0.2);
        }

        .monitor-value {
            font-size: 1.2rem;
            font-weight: bold;
            color: #00ffff;
        }

        .monitor-label {
            font-size: 0.8rem;
            opacity: 0.8;
        }

        /* Footer */
        .footer {
            background: rgba(0, 0, 0, 0.9);
            padding: 3rem 0 1rem;
            margin-top: 4rem;
            border-top: 1px solid rgba(0, 255, 255, 0.3);
        }

        .footer-content {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 2rem;
            text-align: center;
        }

        .footer-links {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin-bottom: 2rem;
            flex-wrap: wrap;
        }

        .footer-links a {
            color: #ffffff;
            text-decoration: none;
            transition: color 0.3s ease;
        }

        .footer-links a:hover {
            color: #00ffff;
        }

        .copyright {
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            padding-top: 1rem;
            opacity: 0.8;
        }

        /* Loading Animation */
        .loading {
            display: none;
            text-align: center;
            padding: 2rem;
        }

        .spinner {
            border: 4px solid rgba(0, 255, 255, 0.3);
            border-radius: 50%;
            border-top: 4px solid #00ffff;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            margin: 0 auto 1rem;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Responsive Design */
        @media (max-width: 1200px) {
            .main-grid {
                grid-template-columns: 1fr;
            }
            
            .details-column {
                max-height: none;
            }
        }

        @media (max-width: 768px) {
            .nav-container {
                flex-direction: column;
                gap: 1rem;
            }

            .nav-links {
                flex-direction: column;
                gap: 1rem;
            }

            .hero-title {
                font-size: 2rem;
            }

            .scan-controls {
                grid-template-columns: 1fr;
            }

            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        /* Pulse animation for active elements */
        .pulse {
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>
    <!-- Navbar -->
    <nav class="navbar">
        <div class="nav-container">
            <div class="logo">
                <i class="fas fa-wifi"></i>
                Network Scanner Pro
            </div>
            <ul class="nav-links">
                <li><a href="#home"><i class="fas fa-home"></i> الرئيسية</a></li>
                <li><a href="#scan"><i class="fas fa-search"></i> المسح</a></li>
                <li><a href="#analytics"><i class="fas fa-chart-bar"></i> التحليلات</a></li>
                <li><a href="#monitoring"><i class="fas fa-eye"></i> المراقبة</a></li>
                <li><a href="#tools"><i class="fas fa-tools"></i> الأدوات</a></li>
                <li><a href="#settings"><i class="fas fa-cog"></i> الإعدادات</a></li>
            </ul>
        </div>
    </nav>

    <!-- Main Content -->
    <div class="main-content">
        <!-- Hero Section -->
        <section class="hero-section" id="home">
            <h1 class="hero-title">مراقب الشبكات المحترف</h1>
            <p class="hero-subtitle">اكتشف وحلل الشبكات اللاسلكية المجاورة بتقنيات متطورة وأدوات تحليل شاملة</p>
        </section>

        <!-- Control Panel -->
        <section class="control-panel" id="scan">
            <div class="scan-controls">
                <button class="btn btn-primary" onclick="startAdvancedScan()">
                    <i class="fas fa-radar-alt"></i>
                    مسح متقدم
                </button>
                <button class="btn btn-secondary" onclick="stopScan()">
                    <i class="fas fa-stop"></i>
                    إيقاف المسح
                </button>
                <button class="btn btn-success" onclick="startRealTimeMonitoring()">
                    <i class="fas fa-broadcast-tower"></i>
                    مراقبة مباشرة
                </button>
                <button class="btn btn-warning" onclick="performSecurityAudit()">
                    <i class="fas fa-shield-virus"></i>
                    تدقيق أمني
                </button>
                <button class="btn btn-primary" onclick="refreshNetworks()">
                    <i class="fas fa-sync-alt"></i>
                    تحديث
                </button>
                <button class="btn btn-secondary" onclick="exportAdvancedData()">
                    <i class="fas fa-file-export"></i>
                    تصدير متقدم
                </button>
            </div>

            <div class="loading" id="loading">
                <div class="spinner"></div>
                <p>جاري البحث المتقدم عن الشبكات...</p>
            </div>
        </section>

        <!-- Statistics -->
        <section class="stats-grid" id="analytics">
            <div class="stat-card" onclick="filterNetworks('all')">
                <div class="stat-icon"><i class="fas fa-wifi"></i></div>
                <div class="stat-number" id="totalNetworks">32</div>
                <div class="stat-label">إجمالي الشبكات</div>
            </div>
            <div class="stat-card" onclick="filterNetworks('secure')">
                <div class="stat-icon"><i class="fas fa-shield-alt"></i></div>
                <div class="stat-number" id="secureNetworks">24</div>
                <div class="stat-label">شبكات محمية</div>
            </div>
            <div class="stat-card" onclick="filterNetworks('open')">
                <div class="stat-icon"><i class="fas fa-unlock"></i></div>
                <div class="stat-number" id="openNetworks">8</div>
                <div class="stat-label">شبكات مفتوحة</div>
            </div>
            <div class="stat-card" onclick="filterNetworks('hidden')">
                <div class="stat-icon"><i class="fas fa-eye-slash"></i></div>
                <div class="stat-number" id="hiddenNetworks">5</div>
                <div class="stat-label">شبكات مخفية</div>
            </div>
            <div class="stat-card" onclick="filterNetworks('strong')">
                <div class="stat-icon"><i class="fas fa-signal"></i></div>
                <div class="stat-number" id="strongSignals">18</div>
                <div class="stat-label">إشارة قوية</div>
            </div>
            <div class="stat-card" onclick="filterNetworks('mobile')">
                <div class="stat-icon"><i class="fas fa-mobile-alt"></i></div>
                <div class="stat-number" id="mobileNetworks">12</div>
                <div class="stat-label">شبكات محمولة</div>
            </div>
        </section>

        <!-- Main Grid -->
        <div class="main-grid">
            <!-- Networks Table Column -->
            <div class="networks-column">
                <h2 class="section-title">
                    <i class="fas fa-list"></i>
                    الشبكات المكتشفة
                </h2>
                <div class="table-container">
                    <table>
                        <thead>
                            <tr>
                                <th>SSID</th>
                                <th>نوع</th>
                                <th>تشفير</th>
                                <th>إشارة</th>
                                <th>قناة</th>
                                <th>متصلين</th>
                                <th>حالة</th>
                                <th>نشاط</th>
                            </tr>
                        </thead>
                        <tbody id="networksTable">
                            <!-- Networks will be populated by JavaScript -->
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Network Details Column -->
            <div class="details-column">
                <div id="noSelection" class="text-center" style="padding: 4rem 0; opacity: 0.6;">
                    <i class="fas fa-hand-pointer" style="font-size: 4rem; color: #00ffff; margin-bottom: 1rem;"></i>
                    <h3>اختر شبكة للتحليل</h3>
                    <p>انقر على أي شبكة في القائمة لعرض التفاصيل والأدوات المتقدمة</p>
                </div>

                <div id="networkDetails" class="network-details">
                    <!-- Network details will be populated by JavaScript -->
                </div>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="footer">
        <div class="footer-content">
            <div class="footer-links">
                <a href="#privacy">سياسة الخصوصية</a>
                <a href="#terms">شروط الاستخدام</a>
                <a href="#contact">اتصل بنا</a>
                <a href="#about">حول المشروع</a>
                <a href="#api">واجهة البرمجة</a>
                <a href="#documentation">التوثيق</a>
            </div>
            <div class="copyright">
                <p>&copy; 2025 - 2026 جميع الحقوق محفوظة للمطور <strong>Muhammed Alaa</strong> | تم التطوير بتقنيات متقدمة</p>
                <p>هذا المشروع مخصص للأغراض التعليمية ومراقبة الشبكات المصرح بها فقط</p>
            </div>
        </div>
    </footer>

    <script>
        // Enhanced network data with more details
        const advancedNetworks = [
            {
                id: 1,
                ssid: "HomeNetwork_5G_Pro",
                type: "wifi",
                security: "wpa3",
                mac: "AA:BB:CC:DD:EE:FF",
                bssid: "AA:BB:CC:DD:EE:FF",
                signal: 95,
                channel: 149,
                frequency: "5.745 GHz",
                bandwidth: "160 MHz",
                clients: 12,
                hidden: false,
                lastActivity: "منذ دقيقة",
                vendor: "TP-Link",
                encryption: "AES-CCMP",
                authentication: "WPA3-SAE",
                dataRate: "1200 Mbps",
                uptime: "15 أيام",
                traffic: "2.4 GB/h",
                securityScore: 95,
                vulnerabilities: [],
                geolocation: { lat: 30.0444, lng: 31.2357 },
                beaconInterval: 100,
                dtimPeriod: 1,
                capabilities: ["WPS", "WMM", "Short-GI", "LDPC"],
                operatingSystem: "OpenWrt 22.03",
                firmwareVersion: "v1.2.3",
                supportedStandards: ["802.11a", "802.11n", "802.11ac", "802.11ax"]
            },
            {
                id: 2,
                ssid: "Office_Enterprise",
                type: "wifi", 
                security: "wpa2",
                mac: "11:22:33:44:55:66",
                bssid: "11:22:33:44:55:66",
                signal: 78,
                channel: 6,
                frequency: "2.437 GHz",
                bandwidth: "40 MHz",
                clients: 24,
                hidden: false,
                lastActivity: "منذ 3 دقائق",
                vendor: "Cisco",
                encryption: "AES-CCMP",
                authentication: "WPA2-Enterprise",
                dataRate: "300 Mbps",
                uptime: "45 أيام",
                traffic: "5.8 GB/h",
                securityScore: 85,
                vulnerabilities: ["KRACK"],
                geolocation: { lat: 30.0445, lng: 31.2358 },
                beaconInterval: 100,
                dtimPeriod: 3,
                capabilities: ["WMM", "Short-GI"],
                operatingSystem: "Cisco IOS",
                firmwareVersion: "15.1(4)M",
                supportedStandards: ["802.11b", "802.11g", "802.11n"]
            },
            {
                id: 3,
                ssid: "[Hidden Network]",
                type: "wifi",
                security: "wpa2",
                mac: "77:88:99:AA:BB:CC",
                bssid: "77:88:99:AA:BB:CC",
                signal: 65,
                channel: 11,
                frequency: "2.462 GHz",
                bandwidth: "20 MHz",
                clients: 3,
                hidden: true,
                lastActivity: "منذ 5 دقائق",
                vendor: "Netgear",
                encryption: "AES-CCMP",
                authentication: "WPA2-PSK",
                dataRate: "150 Mbps",
                uptime: "8 أيام",
                traffic: "0.8 GB/h",
                securityScore: 75,
                vulnerabilities: ["WPS PIN Attack"],
                geolocation: { lat: 30.0443, lng: 31.2356 },
                beaconInterval: 100,
                dtimPeriod: 2,
                capabilities: ["WPS", "WMM"],
                operatingSystem: "Unknown",
                firmwareVersion: "Unknown",
                supportedStandards: ["802.11g", "802.11n"]
            },
            {
                id: 4,
                ssid: "Vodafone_5G_Ultra",
                type: "mobile-5g",
                security: "wpa3",
                mac: "DD:EE:FF:00:11:22",
                bssid: "DD:EE:FF:00:11:22",
                signal: 88,
                channel: 36,
                frequency: "5.180 GHz",
                bandwidth: "80 MHz",
                clients: 25,
                hidden: false,
                lastActivity: "الآن",
                vendor: "Huawei",
                encryption: "AES-GCMP-256",
                authentication: "WPA3-SAE",
                dataRate: "2400 Mbps",
                uptime: "120 أيام",
                traffic: "15.2 GB/h",
                securityScore: 98,
                vulnerabilities: [],
                geolocation: { lat: 30.0446, lng: 31.2359 },
                beaconInterval: 100,
                dtimPeriod: 1,
                capabilities: ["WMM", "Short-GI", "LDPC", "STBC"],
                operatingSystem: "Android 12",
                firmwareVersion: "12.1.0",
                supportedStandards: ["802.11ac", "802.11ax"]
            },
            {
                id: 5,
                ssid: "Public_WiFi_Free",
                type: "wifi",
                security: "open",
                mac: "33:44:55:66:77:88",
                bssid: "33:44:55:66:77:88",
                signal: 45,
                channel: 1,
                frequency: "2.412 GHz",
                bandwidth: "20 MHz",
                clients: 2,
                hidden: false,
                lastActivity: "منذ 10 دقائق",
                vendor: "D-Link",
                encryption: "None",
                authentication: "Open",
                dataRate: "54 Mbps",
                uptime: "2 أيام",
                traffic: "0.1 GB/h",
                securityScore: 20,
                vulnerabilities: ["Open Network", "No Encryption", "Man-in-the-Middle"],
                geolocation: { lat: 30.0442, lng: 31.2355 },
                beaconInterval: 100,
                dtimPeriod: 1,
                capabilities: ["WMM"],
                operatingSystem: "DD-WRT",
                firmwareVersion: "v3.0",
                supportedStandards: ["802.11b", "802.11g"]
            }
        ];

        let isScanning = false;
        let scanInterval;
        let selectedNetwork = null;
        let currentFilter = 'all';
        let signalChart = null;
        let clientsChart = null;

        // Initialize the application
        function initApp() {
            renderNetworks();
            updateStatistics();
            setupEventListeners();
        }

        // Event listeners setup
        function setupEventListeners() {
            // Smooth scrolling for navigation
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function (e) {
                    e.preventDefault();
                    const target = document.querySelector(this.getAttribute('href'));
                    if (target) {
                        target.scrollIntoView({
                            behavior: 'smooth',
                            block: 'start'
                        });
                    }
                });
            });
        }

        // Render signal strength bars
        function renderSignalBars(strength) {
            const bars = Math.ceil(strength / 25);
            let html = '<div class="signal-bars">';
            for (let i = 1; i <= 4; i++) {
                html += `<div class="bar ${i <= bars ? 'active' : ''}"></div>`;
            }
            html += '</div>';
            return `<div class="signal-strength">${strength}% ${html}</div>`;
        }

        // Render networks table
        function renderNetworks() {
            const tbody = document.getElementById('networksTable');
            tbody.innerHTML = '';

            let networksToShow = advancedNetworks;
            
            // Apply filters
            if (currentFilter !== 'all') {
                networksToShow = advancedNetworks.filter(network => {
                    switch (currentFilter) {
                        case 'secure': return network.security !== 'open';
                        case 'open': return network.security === 'open';
                        case 'hidden': return network.hidden;
                        case 'strong': return network.signal >= 70;
                        case 'mobile': return network.type.includes('mobile');
                        default: return true;
                    }
                });
            }

            networksToShow.forEach(network => {
                const row = document.createElement('tr');
                row.className = 'network-row';
                row.setAttribute('data-network-id', network.id);
                
                const typeLabels = {
                    'wifi': 'WiFi',
                    'mobile-5g': '5G',
                    'mobile-4g': '4G',
                    'mobile-3g': '3G'
                };

                const securityLabels = {
                    'wpa3': 'WPA3',
                    'wpa2': 'WPA2',
                    'wep': 'WEP',
                    'open': 'مفتوح'
                };

                row.innerHTML = `
                    <td title="${network.ssid}">${network.ssid.length > 15 ? network.ssid.substring(0, 15) + '...' : network.ssid}</td>
                    <td><span class="network-type ${network.type}">${typeLabels[network.type]}</span></td>
                    <td><span class="security-badge ${network.security}">${securityLabels[network.security]}</span></td>
                    <td>${renderSignalBars(network.signal)}</td>
                    <td>${network.channel}</td>
                    <td><i class="fas fa-users"></i> ${network.clients}</td>
                    <td>
                        <span class="status-indicator ${network.hidden ? 'hidden' : 'visible'}"></span>
                        ${network.hidden ? 'مخفية' : 'مرئية'}
                    </td>
                    <td>${network.lastActivity}</td>
                `;

                // Add click event to select network
                row.addEventListener('click', () => selectNetwork(network));
                tbody.appendChild(row);
            });
        }

        // Select a network for detailed analysis
        function selectNetwork(network) {
            selectedNetwork = network;
            
            // Update visual selection
            document.querySelectorAll('.network-row').forEach(row => {
                row.classList.remove('selected');
            });
            document.querySelector(`[data-network-id="${network.id}"]`).classList.add('selected');
            
            // Hide no selection message
            document.getElementById('noSelection').style.display = 'none';
            
            // Show and populate network details
            const detailsDiv = document.getElementById('networkDetails');
            detailsDiv.innerHTML = generateNetworkDetails(network);
            detailsDiv.classList.add('show');
            
            // Initialize charts
            setTimeout(() => {
                initializeCharts(network);
            }, 100);
        }

        // Generate detailed network information
        function generateNetworkDetails(network) {
            const securityScoreClass = 
                network.securityScore >= 90 ? 'score-excellent' :
                network.securityScore >= 70 ? 'score-good' :
                network.securityScore >= 50 ? 'score-poor' : 'score-critical';

            const securityScoreText = 
                network.securityScore >= 90 ? 'ممتاز' :
                network.securityScore >= 70 ? 'جيد' :
                network.securityScore >= 50 ? 'ضعيف' : 'خطير';

            return `
                <div class="detail-header pulse">
                    <div class="detail-ssid">${network.ssid}</div>
                    <div class="detail-type">${network.vendor} - ${network.type.toUpperCase()}</div>
                </div>

                <div class="security-score ${securityScoreClass}">
                    <div class="score-number">${network.securityScore}</div>
                    <div class="score-label">نقاط الأمان - ${securityScoreText}</div>
                </div>

                <div class="detail-section">
                    <h3><i class="fas fa-info-circle"></i> المعلومات الأساسية</h3>
                    <div class="detail-item">
                        <span class="detail-label">SSID:</span>
                        <span class="detail-value">${network.ssid}</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">BSSID:</span>
                        <span class="detail-value"><code>${network.bssid}</code></span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">MAC Address:</span>
                        <span class="detail-value"><code>${network.mac}</code></span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">الشركة المصنعة:</span>
                        <span class="detail-value">${network.vendor}</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">نظام التشغيل:</span>
                        <span class="detail-value">${network.operatingSystem}</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">إصدار البرنامج:</span>
                        <span class="detail-value">${network.firmwareVersion}</span>
                    </div>
                </div>

                <div class="detail-section">
                    <h3><i class="fas fa-wifi"></i> تفاصيل الاتصال</h3>
                    <div class="detail-item">
                        <span class="detail-label">التردد:</span>
                        <span class="detail-value">${network.frequency}</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">القناة:</span>
                        <span class="detail-value">${network.channel}</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">عرض النطاق:</span>
                        <span class="detail-value">${network.bandwidth}</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">معدل البيانات:</span>
                        <span class="detail-value">${network.dataRate}</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">قوة الإشارة:</span>
                        <span class="detail-value">${network.signal}%</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">المعايير المدعومة:</span>
                        <span class="detail-value">${network.supportedStandards.join(', ')}</span>
                    </div>
                </div>

                <div class="detail-section">
                    <h3><i class="fas fa-shield-alt"></i> الأمان والتشفير</h3>
                    <div class="detail-item">
                        <span class="detail-label">نوع التشفير:</span>
                        <span class="detail-value">${network.encryption}</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">المصادقة:</span>
                        <span class="detail-value">${network.authentication}</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">الثغرات الأمنية:</span>
                        <span class="detail-value">
                            ${network.vulnerabilities.length === 0 ? 
                                '<span style="color: #00ff00;">لا توجد ثغرات معروفة</span>' : 
                                `<span style="color: #ff6600;">${network.vulnerabilities.join(', ')}</span>`
                            }
                        </span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">الإمكانيات:</span>
                        <span class="detail-value">${network.capabilities.join(', ')}</span>
                    </div>
                </div>

                <div class="detail-section">
                    <h3><i class="fas fa-chart-line"></i> إحصائيات الشبكة</h3>
                    <div class="monitoring-grid">
                        <div class="monitor-item">
                            <div class="monitor-value">${network.clients}</div>
                            <div class="monitor-label">متصلين</div>
                        </div>
                        <div class="monitor-item">
                            <div class="monitor-value">${network.traffic}</div>
                            <div class="monitor-label">حركة البيانات</div>
                        </div>
                        <div class="monitor-item">
                            <div class="monitor-value">${network.uptime}</div>
                            <div class="monitor-label">وقت التشغيل</div>
                        </div>
                        <div class="monitor-item">
                            <div class="monitor-value">${network.beaconInterval}ms</div>
                            <div class="monitor-label">Beacon Interval</div>
                        </div>
                    </div>
                </div>

                <div class="detail-section">
                    <h3><i class="fas fa-chart-bar"></i> مراقبة مباشرة</h3>
                    <div class="chart-container">
                        <canvas id="signalChart"></canvas>
                    </div>
                    <div class="chart-container">
                        <canvas id="clientsChart"></canvas>
                    </div>
                </div>

                <div class="detail-section">
                    <h3><i class="fas fa-tools"></i> أدوات متقدمة</h3>
                    <div class="tools-section">
                        <button class="tool-btn" onclick="performPingSweep('${network.id}')">
                            <i class="fas fa-satellite-dish"></i><br>Ping Sweep
                        </button>
                        <button class="tool-btn" onclick="portScan('${network.id}')">
                            <i class="fas fa-search"></i><br>Port Scan
                        </button>
                        <button class="tool-btn" onclick="packetCapture('${network.id}')">
                            <i class="fas fa-download"></i><br>Packet Capture
                        </button>
                        <button class="tool-btn" onclick="speedTest('${network.id}')">
                            <i class="fas fa-tachometer-alt"></i><br>Speed Test
                        </button>
                        <button class="tool-btn" onclick="geolocate('${network.id}')">
                            <i class="fas fa-map-marker-alt"></i><br>تحديد الموقع
                        </button>
                        <button class="tool-btn" onclick="vulnerability Scan('${network.id}')">
                            <i class="fas fa-bug"></i><br>فحص الثغرات
                        </button>
                    </div>
                </div>

                <div class="detail-section">
                    <h3><i class="fas fa-map-marker-alt"></i> الموقع الجغرافي</h3>
                    <div class="detail-item">
                        <span class="detail-label">خط العرض:</span>
                        <span class="detail-value">${network.geolocation.lat}</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">خط الطول:</span>
                        <span class="detail-value">${network.geolocation.lng}</span>
                    </div>
                    <div class="detail-item">
                        <span class="detail-label">آخر نشاط:</span>
                        <span class="detail-value">${network.lastActivity}</span>
                    </div>
                </div>
            `;
        }

        // Initialize charts for network monitoring
        function initializeCharts(network) {
            // Destroy existing charts
            if (signalChart) signalChart.destroy();
            if (clientsChart) clientsChart.destroy();

            // Signal strength chart
            const signalCtx = document.getElementById('signalChart');
            if (signalCtx) {
                signalChart = new Chart(signalCtx, {
                    type: 'line',
                    data: {
                        labels: ['10 دقائق', '8 دقائق', '6 دقائق', '4 دقائق', '2 دقائق', 'الآن'],
                        datasets: [{
                            label: 'قوة الإشارة (%)',
                            data: [network.signal - 10, network.signal - 5, network.signal + 2, network.signal - 3, network.signal + 1, network.signal],
                            borderColor: '#00ffff',
                            backgroundColor: 'rgba(0, 255, 255, 0.1)',
                            tension: 0.4,
                            fill: true
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: { labels: { color: '#ffffff' } }
                        },
                        scales: {
                            y: { 
                                ticks: { color: '#ffffff' },
                                grid: { color: 'rgba(255, 255, 255, 0.1)' }
                            },
                            x: { 
                                ticks: { color: '#ffffff' },
                                grid: { color: 'rgba(255, 255, 255, 0.1)' }
                            }
                        }
                    }
                });
            }

            // Clients chart
            const clientsCtx = document.getElementById('clientsChart');
            if (clientsCtx) {
                clientsChart = new Chart(clientsCtx, {
                    type: 'bar',
                    data: {
                        labels: ['10 دقائق', '8 دقائق', '6 دقائق', '4 دقائق', '2 دقائق', 'الآن'],
                        datasets: [{
                            label: 'عدد المتصلين',
                            data: [network.clients - 3, network.clients - 1, network.clients + 2, network.clients - 1, network.clients + 1, network.clients],
                            backgroundColor: 'rgba(255, 0, 255, 0.6)',
                            borderColor: '#ff00ff',
                            borderWidth: 1
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: { labels: { color: '#ffffff' } }
                        },
                        scales: {
                            y: { 
                                ticks: { color: '#ffffff' },
                                grid: { color: 'rgba(255, 255, 255, 0.1)' }
                            },
                            x: { 
                                ticks: { color: '#ffffff' },
                                grid: { color: 'rgba(255, 255, 255, 0.1)' }
                            }
                        }
                    }
                });
            }
        }

        // Update statistics
        function updateStatistics() {
            const stats = {
                total: advancedNetworks.length,
                secure: advancedNetworks.filter(n => n.security !== 'open').length,
                open: advancedNetworks.filter(n => n.security === 'open').length,
                hidden: advancedNetworks.filter(n => n.hidden).length,
                strong: advancedNetworks.filter(n => n.signal >= 70).length,
                mobile: advancedNetworks.filter(n => n.type.includes('mobile')).length
            };

            document.getElementById('totalNetworks').textContent = stats.total;
            document.getElementById('secureNetworks').textContent = stats.secure;
            document.getElementById('openNetworks').textContent = stats.open;
            document.getElementById('hiddenNetworks').textContent = stats.hidden;
            document.getElementById('strongSignals').textContent = stats.strong;
            document.getElementById('mobileNetworks').textContent = stats.mobile;
        }

        // Filter networks
        function filterNetworks(filter) {
            currentFilter = filter;
            renderNetworks();
            
            // Update active state on stat cards
            document.querySelectorAll('.stat-card').forEach(card => {
                card.classList.remove('pulse');
            });
            event.target.closest('.stat-card').classList.add('pulse');
        }

        // Button functions
        function startAdvancedScan() {
            if (isScanning) return;
            
            isScanning = true;
            document.getElementById('loading').style.display = 'block';
            
            setTimeout(() => {
                document.getElementById('loading').style.display = 'none';
                
                // Simulate new networks discovery
                advancedNetworks.forEach(network => {
                    network.signal = Math.max(20, Math.min(100, network.signal + (Math.random() - 0.5) * 10));
                    network.clients = Math.max(0, network.clients + Math.floor((Math.random() - 0.5) * 3));
                    network.lastActivity = Math.random() > 0.5 ? 'الآن' : 'منذ دقيقة';
                });
                
                renderNetworks();
                updateStatistics();
                
                // Auto-refresh every 15 seconds
                scanInterval = setInterval(() => {
                    advancedNetworks.forEach(network => {
                        network.signal = Math.max(20, Math.min(100, network.signal + (Math.random() - 0.5) * 5));
                        network.clients = Math.max(0, network.clients + Math.floor((Math.random() - 0.5) * 2));
                    });
                    renderNetworks();
                    updateStatistics();
                    
                    // Update selected network details if any
                    if (selectedNetwork) {
                        const updatedNetwork = advancedNetworks.find(n => n.id === selectedNetwork.id);
                        if (updatedNetwork) {
                            selectNetwork(updatedNetwork);
                        }
                    }
                }, 15000);
                
                alert('تم بدء المسح المتقدم بنجاح!');
            }, 3000);
        }

        function stopScan() {
            isScanning = false;
            if (scanInterval) {
                clearInterval(scanInterval);
            }
            document.getElementById('loading').style.display = 'none';
            alert('تم إيقاف المسح!');
        }

        function startRealTimeMonitoring() {
            alert('تم بدء المراقبة المباشرة! سيتم تحديث البيانات كل 5 ثوانٍ.');
            
            setInterval(() => {
                if (selectedNetwork) {
                    const network = advancedNetworks.find(n => n.id === selectedNetwork.id);
                    if (network && signalChart && clientsChart) {
                        // Update signal chart
                        signalChart.data.datasets[0].data.shift();
                        signalChart.data.datasets[0].data.push(network.signal + (Math.random() - 0.5) * 10);
                        signalChart.update();
                        
                        // Update clients chart
                        clientsChart.data.datasets[0].data.shift();
                        clientsChart.data.datasets[0].data.push(network.clients + Math.floor((Math.random() - 0.5) * 3));
                        clientsChart.update();
                    }
                }
            }, 5000);
        }

        function performSecurityAudit() {
            if (!selectedNetwork) {
                alert('يرجى اختيار شبكة أولاً لإجراء التدقيق الأمني!');
                return;
            }
            
            alert(`جاري إجراء التدقيق الأمني للشبكة: ${selectedNetwork.ssid}\n\nالنتائج:\n- نقاط الأمان: ${selectedNetwork.securityScore}/100\n- الثغرات المكتشفة: ${selectedNetwork.vulnerabilities.length === 0 ? 'لا توجد' : selectedNetwork.vulnerabilities.join(', ')}\n- نوع التشفير: ${selectedNetwork.encryption}`);
        }

        function refreshNetworks() {
            startAdvancedScan();
        }

        function exportAdvancedData() {
            const exportData = {
                timestamp: new Date().toISOString(),
                totalNetworks: advancedNetworks.length,
                selectedNetwork: selectedNetwork,
                networks: advancedNetworks,
                statistics: {
                    secure: advancedNetworks.filter(n => n.security !== 'open').length,
                    open: advancedNetworks.filter(n => n.security === 'open').length,
                    hidden: advancedNetworks.filter(n => n.hidden).length,
                    mobile: advancedNetworks.filter(n => n.type.includes('mobile')).length
                }
            };
            
            const data = JSON.stringify(exportData, null, 2);
            const blob = new Blob([data], { type: 'application/json' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `advanced_network_scan_${new Date().toISOString().split('T')[0]}.json`;
            a.click();
            URL.revokeObjectURL(url);
            
            alert('تم تصدير البيانات المتقدمة بنجاح!');
        }

        // Advanced tool functions
        function performPingSweep(networkId) {
            const network = advancedNetworks.find(n => n.id == networkId);
            alert(`جاري إجراء Ping Sweep للشبكة: ${network.ssid}\n\nالنتائج:\n- الأجهزة النشطة: ${network.clients}\n- متوسط وقت الاستجابة: ${Math.floor(Math.random() * 50 + 10)}ms\n- معدل فقدان الحزم: ${Math.floor(Math.random() * 5)}%`);
        }

        function portScan(networkId) {
            const network = advancedNetworks.find(n => n.id == networkId);
            const openPorts = ['22', '80', '443', '8080'].slice(0, Math.floor(Math.random() * 4) + 1);
            alert(`جاري فحص المنافذ للشبكة: ${network.ssid}\n\nالمنافذ المفتوحة:\n${openPorts.map(port => `- Port ${port}: Open`).join('\n')}\n\nتحذير: يُستخدم هذا الفحص للأغراض التعليمية فقط!`);
        }

        function packetCapture(networkId) {
            const network = advancedNetworks.find(n => n.id == networkId);
            alert(`بدء التقاط الحزم للشبكة: ${network.ssid}\n\nمعلومات الالتقاط:\n- معدل الحزم: ${Math.floor(Math.random() * 1000 + 100)} packet/sec\n- حجم البيانات: ${(Math.random() * 10 + 1).toFixed(2)} MB/min\n- البروتوكولات: HTTP, HTTPS, TCP, UDP\n\nملاحظة: يتم الالتقاط للأغراض التعليمية فقط!`);
        }

        function speedTest(networkId) {
            const network = advancedNetworks.find(n => n.id == networkId);
            const downloadSpeed = Math.floor(Math.random() * 100 + 50);
            const uploadSpeed = Math.floor(downloadSpeed * 0.8);
            const ping = Math.floor(Math.random() * 30 + 10);
            
            alert(`اختبار السرعة للشبكة: ${network.ssid}\n\nالنتائج:\n- سرعة التنزيل: ${downloadSpeed} Mbps\n- سرعة الرفع: ${uploadSpeed} Mbps\n- زمن الاستجابة: ${ping}ms\n- الجودة: ${downloadSpeed > 80 ? 'ممتازة' : downloadSpeed > 50 ? 'جيدة' : 'متوسطة'}`);
        }

        function geolocate(networkId) {
            const network = advancedNetworks.find(n => n.id == networkId);
            alert(`الموقع الجغرافي للشبكة: ${network.ssid}\n\nالإحداثيات:\n- خط العرض: ${network.geolocation.lat}\n- خط الطول: ${network.geolocation.lng}\n- المنطقة المقدرة: القاهرة، مصر\n- دقة التحديد: ±50 متر\n\nملاحظة: هذه البيانات تقديرية وللأغراض التعليمية فقط!`);
        }

        function vulnerabilityScan(networkId) {
            const network = advancedNetworks.find(n => n.id == networkId);
            const scanResults = network.vulnerabilities.length === 0 ? 
                'لم يتم اكتشاف أي ثغرات أمنية!' : 
                `تم اكتشاف الثغرات التالية:\n${network.vulnerabilities.map(vuln => `- ${vuln}: مستوى متوسط`).join('\n')}`;
                
            alert(`فحص الثغرات الأمنية للشبكة: ${network.ssid}\n\nنتائج الفحص:\n${scanResults}\n\nتوصيات الأمان:\n- استخدام WPA3 إذا كان متاحاً\n- تحديث كلمة المرور بانتظام\n- تعطيل WPS إذا لم يكن ضرورياً\n- تحديث البرامج الثابتة للموجه`);
        }

        // Initialize application when DOM is loaded
        document.addEventListener('DOMContentLoaded', function() {
            initApp();
            
            // Auto-start scanning after 2 seconds
            setTimeout(() => {
                startAdvancedScan();
            }, 2000);
        });

        // Add some cool visual effects
        document.addEventListener('mousemove', function(e) {
            const cursor = document.createElement('div');
            cursor.style.position = 'fixed';
            cursor.style.left = e.clientX + 'px';
            cursor.style.top = e.clientY + 'px';
            cursor.style.width = '5px';
            cursor.style.height = '5px';
            cursor.style.background = 'rgba(0, 255, 255, 0.5)';
            cursor.style.borderRadius = '50%';
            cursor.style.pointerEvents = 'none';
            cursor.style.zIndex = '9999';
            cursor.style.animation = 'fadeOut 1s ease-out forwards';
            
            document.body.appendChild(cursor);
            
            setTimeout(() => {
                if (cursor.parentNode) {
                    cursor.parentNode.removeChild(cursor);
                }
            }, 1000);
        });

        // Add fade out animation for cursor trail
        const style = document.createElement('style');
        style.textContent = `
            @keyframes fadeOut {
                to {
                    opacity: 0;
                    transform: scale(2);
                }
            }
        `;
        document.head.appendChild(style);

        // Add keyboard shortcuts
        document.addEventListener('keydown', function(e) {
            if (e.ctrlKey) {
                switch(e.key) {
                    case 's':
                        e.preventDefault();
                        startAdvancedScan();
                        break;
                    case 'r':
                        e.preventDefault();
                        refreshNetworks();
                        break;
                    case 'e':
                        e.preventDefault();
                        exportAdvancedData();
                        break;
                    case 'm':
                        e.preventDefault();
                        startRealTimeMonitoring();
                        break;
                }
            }
        });

        // Add notification for keyboard shortcuts
        setTimeout(() => {
            const shortcutsInfo = `
اختصارات لوحة المفاتيح:
Ctrl + S: بدء المسح المتقدم
Ctrl + R: تحديث الشبكات  
Ctrl + E: تصدير البيانات
Ctrl + M: بدء المراقبة المباشرة
            `;
            console.log(shortcutsInfo);
        }, 5000);
    </script>
</body>
</html>
