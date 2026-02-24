<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="description" content="CellNet Security Pro - Análisis de red WiFi, detección de intrusiones y escáner de vulnerabilidades">
    <meta name="theme-color" content="#0a0e27">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    
    <title>CellNet Security Pro | Análisis de Red y Seguridad</title>
    
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>🛡️</text></svg>">
    
    <style>
        :root {
            --primary: #00d4ff;
            --secondary: #0099cc;
            --success: #00ff88;
            --warning: #ffcc00;
            --danger: #ff3366;
            --alert: #ff0066;
            --dark: #0a0e27;
            --darker: #050817;
            --glass: rgba(255, 255, 255, 0.05);
            --glass-border: rgba(255, 255, 255, 0.1);
            --matrix: #00ff41;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            background: var(--darker);
            color: #fff;
            overflow-x: hidden;
            min-height: 100vh;
            position: relative;
        }

        .matrix-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            opacity: 0.03;
            pointer-events: none;
        }

        .bg-animation {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: 
                radial-gradient(circle at 20% 50%, rgba(255, 0, 102, 0.1) 0%, transparent 50%),
                radial-gradient(circle at 80% 80%, rgba(0, 212, 255, 0.1) 0%, transparent 50%);
            animation: bgPulse 8s ease-in-out infinite;
        }

        @keyframes bgPulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.8; }
        }

        .grid-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(rgba(0, 212, 255, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 212, 255, 0.03) 1px, transparent 1px);
            background-size: 50px 50px;
            z-index: -1;
            pointer-events: none;
        }

        header {
            padding: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: linear-gradient(180deg, rgba(10, 14, 39, 0.95) 0%, transparent 100%);
            position: sticky;
            top: 0;
            z-index: 100;
            backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--glass-border);
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 1.5rem;
            font-weight: 700;
            background: linear-gradient(135deg, var(--primary), var(--alert));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .logo-icon {
            width: 40px;
            height: 40px;
            background: linear-gradient(135deg, var(--primary), var(--alert));
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            animation: pulse 2s infinite;
            box-shadow: 0 0 20px rgba(255, 0, 102, 0.3);
        }

        @keyframes pulse {
            0%, 100% { box-shadow: 0 0 0 0 rgba(255, 0, 102, 0.4); }
            50% { box-shadow: 0 0 0 15px rgba(255, 0, 102, 0); }
        }

        .header-status {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .security-badge {
            padding: 8px 16px;
            background: rgba(255, 0, 102, 0.1);
            border: 1px solid rgba(255, 0, 102, 0.3);
            border-radius: 20px;
            font-size: 0.85rem;
            display: flex;
            align-items: center;
            gap: 8px;
            color: var(--alert);
            font-weight: 600;
        }

        .status-badge {
            padding: 8px 16px;
            background: var(--glass);
            border: 1px solid var(--glass-border);
            border-radius: 20px;
            font-size: 0.85rem;
            display: flex;
            align-items: center;
            gap: 8px;
            backdrop-filter: blur(10px);
        }

        .status-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            animation: blink 2s infinite;
        }

        .status-dot.safe { background: var(--success); }
        .status-dot.warning { background: var(--warning); }
        .status-dot.danger { background: var(--danger); animation: blink 0.5s infinite; }

        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.3; }
        }

        .alert-banner {
            background: linear-gradient(90deg, rgba(255, 0, 102, 0.2), rgba(255, 0, 102, 0.1));
            border-left: 4px solid var(--alert);
            padding: 12px 20px;
            margin: 20px;
            border-radius: 8px;
            display: none;
            align-items: center;
            gap: 12px;
            animation: slideIn 0.3s ease;
        }

        .alert-banner.active {
            display: flex;
        }

        @keyframes slideIn {
            from { transform: translateX(-100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .alert-icon {
            font-size: 1.5rem;
            animation: shake 0.5s infinite;
        }

        @keyframes shake {
            0%, 100% { transform: rotate(-5deg); }
            50% { transform: rotate(5deg); }
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .security-dashboard {
            background: linear-gradient(135deg, rgba(255, 0, 102, 0.1), rgba(10, 14, 39, 0.8));
            border: 1px solid rgba(255, 0, 102, 0.3);
            border-radius: 24px;
            padding: 30px;
            margin-bottom: 20px;
            position: relative;
            overflow: hidden;
        }

        .security-dashboard::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--alert), transparent);
            animation: scan 3s linear infinite;
        }

        @keyframes scan {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }

        .dashboard-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            flex-wrap: wrap;
            gap: 20px;
        }

        .security-score {
            text-align: center;
        }

        .score-circle {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            background: conic-gradient(var(--success) 0deg, var(--success) var(--score-deg, 288deg), rgba(255,255,255,0.1) var(--score-deg, 288deg));
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            margin: 0 auto 10px;
        }

        .score-circle::before {
            content: '';
            position: absolute;
            width: 100px;
            height: 100px;
            background: var(--darker);
            border-radius: 50%;
        }

        .score-value {
            position: relative;
            font-size: 2rem;
            font-weight: 700;
            z-index: 1;
        }

        .score-label {
            font-size: 0.9rem;
            color: rgba(255,255,255,0.7);
        }

        .threat-meter {
            background: var(--glass);
            border-radius: 12px;
            padding: 20px;
            margin-top: 20px;
        }

        .threat-bar {
            height: 8px;
            background: rgba(255,255,255,0.1);
            border-radius: 4px;
            overflow: hidden;
            margin: 10px 0;
            position: relative;
        }

        .threat-fill {
            height: 100%;
            border-radius: 4px;
            transition: width 0.5s ease;
            position: relative;
            overflow: hidden;
        }

        .threat-fill::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            animation: shimmer 2s infinite;
        }

        @keyframes shimmer {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }

        .scanner-section {
            background: var(--glass);
            border: 1px solid var(--glass-border);
            border-radius: 24px;
            padding: 30px;
            margin-bottom: 20px;
            backdrop-filter: blur(20px);
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .section-title {
            font-size: 1.3rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .scan-btn {
            background: linear-gradient(135deg, var(--alert), #cc0052);
            border: none;
            padding: 12px 24px;
            border-radius: 25px;
            color: #fff;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 8px;
            box-shadow: 0 5px 20px rgba(255, 0, 102, 0.3);
        }

        .scan-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 30px rgba(255, 0, 102, 0.5);
        }

        .scan-btn.scanning {
            animation: scanning 1s infinite;
            pointer-events: none;
        }

        @keyframes scanning {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.6; }
        }

        .btn {
            padding: 10px 20px;
            border-radius: 20px;
            border: none;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: #fff;
        }

        .btn-danger {
            background: linear-gradient(135deg, var(--danger), #cc0052);
            color: #fff;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(0,0,0,0.3);
        }

        .network-list {
            display: flex;
            flex-direction: column;
            gap: 12px;
            max-height: 400px;
            overflow-y: auto;
        }

        .network-item {
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid var(--glass-border);
            border-radius: 16px;
            padding: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
            cursor: pointer;
        }

        .network-item::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            bottom: 0;
            width: 4px;
            background: var(--success);
            transition: background 0.3s;
        }

        .network-item.danger::before { background: var(--danger); }
        .network-item.warning::before { background: var(--warning); }

        .network-item:hover {
            transform: translateX(5px);
            border-color: var(--primary);
        }

        .network-info {
            flex: 1;
        }

        .network-name {
            font-weight: 600;
            font-size: 1.1rem;
            margin-bottom: 4px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .evil-twin-badge {
            background: var(--danger);
            color: #fff;
            padding: 2px 8px;
            border-radius: 12px;
            font-size: 0.7rem;
            animation: pulse-badge 2s infinite;
        }

        @keyframes pulse-badge {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        .network-details {
            font-size: 0.85rem;
            color: rgba(255,255,255,0.6);
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }

        .security-tag {
            padding: 4px 10px;
            border-radius: 12px;
            font-size: 0.75rem;
            font-weight: 600;
            text-transform: uppercase;
        }

        .security-tag.wpa3 { background: rgba(0, 255, 136, 0.2); color: var(--success); }
        .security-tag.wpa2 { background: rgba(0, 212, 255, 0.2); color: var(--primary); }
        .security-tag.wpa { background: rgba(255, 204, 0, 0.2); color: var(--warning); }
        .security-tag.wep { background: rgba(255, 51, 102, 0.2); color: var(--danger); }
        .security-tag.open { background: rgba(255, 0, 0, 0.3); color: #ff4444; border: 1px solid #ff4444; }

        .signal-strength {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .intrusion-panel {
            background: linear-gradient(135deg, rgba(255, 0, 102, 0.05), transparent);
            border: 1px solid rgba(255, 0, 102, 0.2);
            border-radius: 20px;
            padding: 24px;
            margin-bottom: 20px;
        }

        .packet-visualizer {
            background: #000;
            border-radius: 12px;
            padding: 20px;
            font-family: 'Courier New', monospace;
            font-size: 0.85rem;
            height: 200px;
            overflow: hidden;
            position: relative;
            border: 1px solid rgba(0, 255, 65, 0.3);
            margin-bottom: 20px;
        }

        .packet-line {
            color: var(--matrix);
            margin: 2px 0;
            opacity: 0;
            animation: typeIn 0.3s forwards;
            text-shadow: 0 0 5px var(--matrix);
            font-size: 0.8rem;
        }

        @keyframes typeIn {
            to { opacity: 1; }
        }

        .packet-header { color: var(--primary); }
        .packet-warning { color: var(--warning); }
        .packet-danger { color: var(--danger); }

        .threat-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .threat-item {
            background: rgba(0, 0, 0, 0.4);
            padding: 15px;
            border-radius: 12px;
            border-left: 3px solid var(--danger);
            display: flex;
            justify-content: space-between;
            align-items: center;
            animation: slideIn 0.3s ease;
        }

        .threat-level {
            padding: 4px 12px;
            border-radius: 12px;
            font-size: 0.75rem;
            font-weight: 700;
        }

        .threat-level.high { background: rgba(255, 0, 102, 0.3); color: var(--alert); }
        .threat-level.medium { background: rgba(255, 204, 0, 0.3); color: var(--warning); }
        .threat-level.low { background: rgba(0, 212, 255, 0.3); color: var(--primary); }

        .device-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .device-card {
            background: var(--glass);
            border: 1px solid var(--glass-border);
            border-radius: 16px;
            padding: 20px;
            position: relative;
            overflow: hidden;
            transition: all 0.3s;
        }

        .device-card.suspicious {
            border-color: var(--danger);
            animation: pulse-border 2s infinite;
        }

        @keyframes pulse-border {
            0%, 100% { box-shadow: 0 0 0 0 rgba(255, 51, 102, 0.4); }
            50% { box-shadow: 0 0 20px rgba(255, 51, 102, 0.2); }
        }

        .device-header {
            display: flex;
            justify-content: space-between;
            align-items: start;
            margin-bottom: 10px;
        }

        .device-icon {
            width: 40px;
            height: 40px;
            background: rgba(0, 212, 255, 0.1);
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.3rem;
        }

        .device-status {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: var(--success);
            box-shadow: 0 0 10px var(--success);
        }

        .device-status.suspicious { background: var(--danger); box-shadow: 0 0 10px var(--danger); }

        .device-name {
            font-weight: 600;
            margin-bottom: 4px;
        }

        .device-ip {
            font-size: 0.85rem;
            color: rgba(255,255,255,0.5);
            font-family: monospace;
        }

        .device-traffic {
            margin-top: 10px;
            font-size: 0.8rem;
            color: rgba(255,255,255,0.6);
        }

        .vuln-list {
            margin-top: 15px;
        }

        .vuln-item {
            display: flex;
            align-items: center;
            gap: 15px;
            padding: 15px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 12px;
            margin-bottom: 10px;
            border: 1px solid transparent;
            transition: all 0.3s;
        }

        .vuln-item:hover {
            border-color: var(--primary);
            transform: translateX(5px);
        }

        .vuln-icon {
            width: 40px;
            height: 40px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
        }

        .vuln-icon.critical { background: rgba(255, 0, 102, 0.2); color: var(--alert); }
        .vuln-icon.warning { background: rgba(255, 204, 0, 0.2); color: var(--warning); }
        .vuln-icon.info { background: rgba(0, 212, 255, 0.2); color: var(--primary); }

        .vuln-info { flex: 1; }
        .vuln-title { font-weight: 600; margin-bottom: 2px; }
        .vuln-desc { font-size: 0.85rem; color: rgba(255,255,255,0.6); }

        .action-bar {
            display: flex;
            gap: 10px;
            margin-top: 20px;
            flex-wrap: wrap;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.8);
            z-index: 1000;
            align-items: center;
            justify-content: center;
            padding: 20px;
            backdrop-filter: blur(10px);
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: linear-gradient(135deg, #1a1f3d, #0f1429);
            border: 1px solid var(--glass-border);
            border-radius: 24px;
            padding: 30px;
            max-width: 500px;
            width: 100%;
            max-height: 80vh;
            overflow-y: auto;
            animation: modalIn 0.3s ease;
        }

        @keyframes modalIn {
            from { transform: scale(0.8); opacity: 0; }
            to { transform: scale(1); opacity: 1; }
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .close-btn {
            background: none;
            border: none;
            color: #fff;
            font-size: 1.5rem;
            cursor: pointer;
            opacity: 0.7;
            transition: opacity 0.3s;
        }

        .close-btn:hover { opacity: 1; }

        .detail-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 20px;
        }

        .detail-item {
            background: rgba(0,0,0,0.3);
            padding: 15px;
            border-radius: 10px;
        }

        .detail-item label {
            display: block;
            font-size: 0.8rem;
            color: rgba(255,255,255,0.5);
            margin-bottom: 5px;
            text-transform: uppercase;
        }

        .detail-item value {
            font-size: 1.1rem;
            font-weight: 600;
        }

        .threat-warning {
            background: rgba(255, 0, 102, 0.1);
            border: 1px solid rgba(255, 0, 102, 0.3);
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 20px;
        }

        .threat-warning h3 {
            color: var(--danger);
            margin-bottom: 10px;
        }

        .recommendations {
            background: rgba(0, 212, 255, 0.05);
            border-radius: 12px;
            padding: 15px;
        }

        .recommendations h3 {
            margin-bottom: 10px;
            color: var(--primary);
        }

        .recommendations ul {
            list-style: none;
            padding: 0;
        }

        .recommendations li {
            padding: 5px 0;
            padding-left: 20px;
            position: relative;
        }

        .recommendations li::before {
            content: '→';
            position: absolute;
            left: 0;
            color: var(--primary);
        }

        @media (max-width: 768px) {
            .dashboard-header { flex-direction: column; text-align: center; }
            .device-grid { grid-template-columns: 1fr; }
            .network-item { flex-direction: column; align-items: flex-start; gap: 10px; }
            .detail-grid { grid-template-columns: 1fr; }
            .section-header { flex-direction: column; align-items: flex-start; }
        }

        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: var(--darker); }
        ::-webkit-scrollbar-thumb { background: var(--secondary); border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: var(--primary); }

        .fade-in { animation: fadeIn 0.5s ease; }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255,255,255,.3);
            border-radius: 50%;
            border-top-color: #fff;
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <canvas class="matrix-bg" id="matrixCanvas"></canvas>
    <div class="bg-animation"></div>
    <div class="grid-overlay"></div>

    <header>
        <div class="logo">
            <div class="logo-icon">🛡️</div>
            <span>CellNet Security Pro</span>
        </div>
        <div class="header-status">
            <div class="security-badge" id="securityStatus">
                <span>🔒</span>
                <span>Protegido</span>
            </div>
            <div class="status-badge">
                <span class="status-dot safe" id="statusDot"></span>
                <span id="connectionStatus">Seguro</span>
            </div>
        </div>
    </header>

    <div class="alert-banner" id="alertBanner">
        <span class="alert-icon">⚠️</span>
        <div>
            <strong id="alertTitle">Amenaza Detectada</strong>
            <div id="alertMessage">Se ha detectado actividad sospechosa en tu red</div>
        </div>
    </div>

    <div class="container">
        <div class="security-dashboard fade-in">
            <div class="dashboard-header">
                <div>
                    <h2 style="margin-bottom: 5px;">Panel de Seguridad</h2>
                    <p style="color: rgba(255,255,255,0.6);">Monitoreo de amenazas en tiempo real</p>
                </div>
                <div class="security-score">
                    <div class="score-circle" id="scoreCircle" style="--score-deg: 288deg;">
                        <span class="score-value" id="securityScore">80</span>
                    </div>
                    <div class="score-label">Puntuación de Seguridad</div>
                </div>
            </div>

            <div class="threat-meter">
                <div style="display: flex; justify-content: space-between; margin-bottom: 5px;">
                    <span>Nivel de Amenaza</span>
                    <span id="threatLevelText" style="color: var(--success); font-weight: 600;">Bajo</span>
                </div>
                <div class="threat-bar">
                    <div class="threat-fill" id="threatBar" style="width: 20%; background: linear-gradient(90deg, var(--success), var(--warning));"></div>
                </div>
                <div style="display: flex; justify-content: space-between; margin-top: 15px; font-size: 0.9rem; flex-wrap: wrap; gap: 10px;">
                    <div>🔴 Ataques bloqueados: <strong id="blockedAttacks">0</strong></div>
                    <div>🟡 Intentos sospechosos: <strong id="suspiciousAttempts">0</strong></div>
                    <div>🟢 Dispositivos seguros: <strong id="safeDevices">0</strong></div>
                </div>
            </div>
        </div>

        <div class="scanner-section fade-in">
            <div class="section-header">
                <h3 class="section-title">
                    📡 Escáner de Redes WiFi
                    <span style="font-size: 0.8rem; color: rgba(255,255,255,0.5); font-weight: normal;">(Análisis de seguridad)</span>
                </h3>
                <button class="scan-btn" id="wifiScanBtn" onclick="scanWiFiNetworks()">
                    <span>🔍</span>
                    <span>Escanear Redes</span>
                </button>
            </div>

            <div class="network-list" id="networkList">
                <div style="text-align: center; padding: 40px; color: rgba(255,255,255,0.5);">
                    Presiona "Escanear Redes" para buscar redes WiFi cercanas y analizar su seguridad
                </div>
            </div>
        </div>

        <div class="intrusion-panel fade-in">
            <div class="section-header">
                <h3 class="section-title">🚨 Detección de Intrusiones</h3>
                <button class="btn btn-primary" onclick="startIntrusionDetection()">
                    <span>▶️</span> Iniciar Monitoreo
                </button>
            </div>
            
            <div class="packet-visualizer" id="packetVisualizer">
                <div style="color: rgba(255,255,255,0.3); text-align: center; margin-top: 80px;">
                    Esperando inicio de captura de paquetes...
                </div>
            </div>

            <div class="threat-list" id="threatList">
                <div class="threat-item">
                    <div>
                        <div style="font-weight: 600;">Sistema listo</div>
                        <div style="font-size: 0.85rem; color: rgba(255,255,255,0.6);">No se detectan amenazas activas</div>
                    </div>
                    <span class="threat-level low">NORMAL</span>
                </div>
            </div>
        </div>

        <div class="scanner-section fade-in">
            <div class="section-header">
                <h3 class="section-title">📱 Dispositivos Conectados</h3>
                <button class="btn btn-primary" onclick="scanDevices()">
                    <span>🔄</span> Actualizar
                </button>
            </div>
            
            <div class="device-grid" id="deviceGrid">
                <div style="grid-column: 1/-1; text-align: center; padding: 40px; color: rgba(255,255,255,0.5);">
                    Presiona "Actualizar" para escanear dispositivos en la red
                </div>
            </div>
        </div>

        <div class="scanner-section fade-in">
            <div class="section-header">
                <h3 class="section-title">🔍 Análisis de Vulnerabilidades</h3>
                <button class="btn btn-danger" onclick="runVulnerabilityScan()">
                    <span>⚡</span> Escanear Ahora
                </button>
            </div>

            <div class="vuln-list" id="vulnList">
                <div class="vuln-item">
                    <div class="vuln-icon info">ℹ️</div>
                    <div class="vuln-info">
                        <div class="vuln-title">Escaneo no realizado</div>
                        <div class="vuln-desc">Ejecuta un análisis completo para detectar vulnerabilidades en tu red</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="scanner-section fade-in" style="margin-bottom: 40px;">
            <h3 class="section-title" style="margin-bottom: 20px;">🛡️ Acciones de Protección</h3>
            <div class="action-bar">
                <button class="btn btn-primary" onclick="enableFirewall()">
                    <span>🔥</span> Activar Firewall
                </button>
                <button class="btn btn-primary" onclick="changeMacAddress()">
                    <span>🎭</span> Randomizar MAC
                </button>
                <button class="btn btn-danger" onclick="blockIntruder()">
                    <span>🚫</span> Bloquear Intruso
                </button>
                <button class="btn btn-primary" onclick="encryptTraffic()">
                    <span>🔐</span> Cifrar Tráfico
                </button>
            </div>
        </div>
    </div>

    <div class="modal" id="networkModal" onclick="closeModalOnBackground(event)">
        <div class="modal-content" onclick="event.stopPropagation()">
            <div class="modal-header">
                <h3>Detalles de Red</h3>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <div id="modalBody"></div>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('matrixCanvas');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const chars = '01アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモヤユヨラリルレロワヲン';
        const fontSize = 14;
        const columns = canvas.width / fontSize;
        const drops = [];

        for (let i = 0; i < columns; i++) drops[i] = Math.random() * -100;

        function drawMatrix() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = '#00ff41';
            ctx.font = fontSize + 'px monospace';
            for (let i = 0; i < drops.length; i++) {
                const text = chars[Math.floor(Math.random() * chars.length)];
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);
                if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) drops[i] = 0;
                drops[i]++;
            }
        }
        setInterval(drawMatrix, 50);
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });

        let securityScore = 80;
        let blockedAttacks = 0;
        let suspiciousAttempts = 0;
        let isMonitoring = false;
        let detectedNetworks = [];
        let connectedDevices = [];

        document.addEventListener('DOMContentLoaded', () => {
            initializeSecurity();
            if (window.location.protocol === 'http:') {
                showAlert('Conexión No Segura', 'Estás usando HTTP. El tráfico puede ser interceptado.', 'warning');
                updateSecurityScore(60);
            }
        });

        function initializeSecurity() {
            updateSecurityScore(80);
            document.getElementById('blockedAttacks').textContent = '0';
            document.getElementById('suspiciousAttempts').textContent = '0';
            document.getElementById('safeDevices').textContent = '0';
        }

        function updateSecurityScore(score) {
            securityScore = Math.max(0, Math.min(100, score));
            document.getElementById('securityScore').textContent = securityScore;
            document.getElementById('scoreCircle').style.setProperty('--score-deg', (securityScore * 3.6) + 'deg');
            
            const threatBar = document.getElementById('threatBar');
            const threatText = document.getElementById('threatLevelText');
            
            if (securityScore >= 80) {
                threatBar.style.width = '20%';
                threatBar.style.background = 'linear-gradient(90deg, #00ff88, #00cc66)';
                threatText.textContent = 'Bajo';
                threatText.style.color = '#00ff88';
                document.getElementById('statusDot').className = 'status-dot safe';
                document.getElementById('connectionStatus').textContent = 'Seguro';
            } else if (securityScore >= 50) {
                threatBar.style.width = '50%';
                threatBar.style.background = 'linear-gradient(90deg, #ffcc00, #ff9900)';
                threatText.textContent = 'Medio';
                threatText.style.color = '#ffcc00';
                document.getElementById('statusDot').className = 'status-dot warning';
                document.getElementById('connectionStatus').textContent = 'Precaución';
            } else {
                threatBar.style.width = '90%';
                threatBar.style.background = 'linear-gradient(90deg, #ff3366, #ff0066)';
                threatText.textContent = 'Crítico';
                threatText.style.color = '#ff3366';
                document.getElementById('statusDot').className = 'status-dot danger';
                document.getElementById('connectionStatus').textContent = 'En Peligro';
            }
        }

        function showAlert(title, message, type) {
            const banner = document.getElementById('alertBanner');
            document.getElementById('alertTitle').textContent = title;
            document.getElementById('alertMessage').textContent = message;
            banner.classList.add('active');
            if (type === 'danger') {
                banner.style.borderLeftColor = '#ff3366';
                banner.style.background = 'linear-gradient(90deg, rgba(255, 51, 102, 0.2), rgba(255, 51, 102, 0.1))';
            }
            setTimeout(() => banner.classList.remove('active'), 5000);
        }

        async function scanWiFiNetworks() {
            const btn = document.getElementById('wifiScanBtn');
            const list = document.getElementById('networkList');
            
            btn.classList.add('scanning');
            btn.disabled = true;
            list.innerHTML = '<div style="text-align: center; padding: 40px;"><div class="loading"></div><p style="margin-top: 20px;">Escaneando redes cercanas...</p></div>';

            await new Promise(r => setTimeout(r, 2000));

            detectedNetworks = [
                { ssid: 'MiWiFi_5G', security: 'WPA3', signal: -45, channel: 36, band: '5GHz', vendor: 'RouterCorp', mac: 'A4:5E:60:E8:12:34' },
                { ssid: 'Starbucks_WiFi', security: 'Open', signal: -65, channel: 6, band: '2.4GHz', vendor: 'Public', mac: 'BC:23:45:F1:56:78' },
                { ssid: 'WiFi_Gracias', security: 'WPA2', signal: -72, channel: 11, band: '2.4GHz', vendor: 'NetGear', mac: 'D2:4E:67:A3:89:01' },
                { ssid: 'MOVISTAR_1234', security: 'WPA2', signal: -55, channel: 1, band: '2.4GHz', vendor: 'Movistar', mac: 'E8:AB:CD:EF:12:34' },
                { ssid: 'MiWiFi_5G_EXT', security: 'WPA2', signal: -68, channel: 36, band: '5GHz', vendor: 'RouterCorp', mac: 'FF:FF:FF:FF:FF:FF', isEvilTwin: true },
                { ssid: 'AndroidAP_99', security: 'WPA2', signal: -78, channel: 6, band: '2.4GHz', vendor: 'Mobile', mac: '12:34:56:78:90:AB' },
                { ssid: 'Vodafone-5678', security: 'WPA3', signal: -60, channel: 40, band: '5GHz', vendor: 'Vodafone', mac: 'CD:EF:12:34:56:78' },
                { ssid: 'Free_WiFi', security: 'Open', signal: -50, channel: 6, band: '2.4GHz', vendor: 'Unknown', mac: 'FE:DC:BA:98:76:54', isEvilTwin: true }
            ];

            renderNetworkList();
            btn.classList.remove('scanning');
            btn.disabled = false;
            checkForRogueAPs();
        }

        function renderNetworkList() {
            const list = document.getElementById('networkList');
            list.innerHTML = detectedNetworks.map(network => {
                const riskClass = network.isEvilTwin ? 'danger' : network.security === 'Open' ? 'warning' : '';
                const securityClass = network.security.toLowerCase().replace(/[^a-z0-9]/g, '');
                
                return `
                    <div class="network-item ${riskClass} fade-in" onclick="showNetworkDetails('${network.ssid}')">
                        <div class="network-info">
                            <div class="network-name">
                                ${network.isEvilTwin ? '⚠️ ' : ''}${network.ssid}
                                ${network.isEvilTwin ? '<span class="evil-twin-badge">EVIL TWIN</span>' : ''}
                            </div>
                            <div class="network-details">
                                <span class="security-tag ${securityClass}">${network.security}</span>
                                <span>Canal ${network.channel}</span>
                                <span>${network.band}</span>
                                <span>${network.vendor}</span>
                            </div>
                        </div>
                        <div class="signal-strength">
                            <span style="font-size: 0.9rem; color: rgba(255,255,255,0.6);">${network.signal} dBm</span>
                            <span style="font-size: 1.2rem;">${'📶'.repeat(Math.min(4, Math.max(1, Math.floor((network.signal + 100) / 20)))}</span>
                        </div>
                    </div>
                `;
            }).join('');
        }

        function checkForRogueAPs() {
            const evilTwins = detectedNetworks.filter(n => n.isEvilTwin);
            const openNetworks = detectedNetworks.filter(n => n.security === 'Open');
            
            if (evilTwins.length > 0) {
                showAlert('¡AP Rogue Detectado!', `Se encontraron ${evilTwins.length} redes sospechosas (posibles Evil Twins)`, 'danger');
                updateSecurityScore(securityScore - 30);
                suspiciousAttempts += evilTwins.length;
                document.getElementById('suspiciousAttempts').textContent = suspiciousAttempts;
            }
            
            if (openNetworks.length > 0) {
                showAlert('Redes Abiertas Detectadas', `${openNetworks.length} redes sin cifrado pueden interceptar tu tráfico`, 'warning');
            }
        }

        function showNetworkDetails(ssid) {
            const network = detectedNetworks.find(n => n.ssid === ssid);
            if (!network) return;

            const modal = document.getElementById('networkModal');
            const body = document.getElementById('modalBody');
            
            let advice = '';
            if (network.isEvilTwin) {
                advice = '¡ALERTA! Esta red parece ser un "Evil Twin". Un atacante ha creado una red falsa con nombre similar para robar datos. NO te conectes.';
            } else if (network.security === 'Open') {
                advice = 'Red abierta sin cifrado. Cualquier persona puede interceptar tu tráfico. Evita ingresar contraseñas o datos sensibles.';
            } else if (network.security === 'WEP') {
                advice = 'WEP está obsoleto y roto. Puede crackearse en menos de 5 minutos. Contacta al administrador para actualizar a WPA2 o WPA3.';
            } else {
                advice = 'Configuración segura. WPA2/WPA3 proporciona cifrado AES robusto.';
            }

            body.innerHTML = `
                <div class="detail-grid">
                    <div class="detail-item">
                        <label>Seguridad</label>
                        <value style="color: ${network.isEvilTwin ? '#ff3366' : '#00d4ff'}">${network.security}</value>
                    </div>
                    <div class="detail-item">
                        <label>Señal</label>
                        <value>${network.signal} dBm</value>
                    </div>
                    <div class="detail-item">
                        <label>Canal</label>
                        <value>${network.channel} (${network.band})</value>
                    </div>
                    <div class="detail-item">
                        <label>MAC</label>
                        <value style="font-family: monospace; font-size: 0.9rem;">${network.mac}</value>
                    </div>
                </div>
                
                ${network.isEvilTwin ? `
                    <div class="threat-warning">
                        <h3>⚠️ Amenaza Crítica Detectada</h3>
                        <p>${advice}</p>
                    </div>
                ` : `
                    <div style="background: rgba(0,0,0,0.3); padding: 15px; border-radius: 12px; margin-bottom: 20px;">
                        <p>${advice}</p>
                    </div>
                `}
                
                <button class="btn btn-primary" style="width: 100%;" onclick="closeModal()">Cerrar</button>
            `;
            
            modal.classList.add('active');
        }

        function closeModal() {
            document.getElementById('networkModal').classList.remove('active');
        }

        function closeModalOnBackground(event) {
            if (event.target === document.getElementById('networkModal')) {
                closeModal();
            }
        }

        function startIntrusionDetection() {
            if (isMonitoring) return;
            
            isMonitoring = true;
            const visualizer = document.getElementById('packetVisualizer');
            visualizer.innerHTML = '';

            const packetTypes = [
                { type: 'TCP', src: '192.168.1.100', dst: '142.250.80.46', port: 443, flag: 'SYN', safe: true },
                { type: 'TCP', src: '192.168.1.105', dst: '192.168.1.1', port: 80, flag: 'ACK', safe: true },
                { type: 'UDP', src: '192.168.1.100', dst: '8.8.8.8', port: 53, flag: 'DNS', safe: true },
                { type: 'TCP', src: '45.33.32.156', dst: '192.168.1.100', port: 22, flag: 'SYN', safe: false, threat: 'SSH Brute Force' },
                { type: 'ICMP', src: '192.168.1.1', dst: '192.168.1.100', flag: 'ECHO', safe: true },
                { type: 'TCP', src: '192.168.1.102', dst: '192.168.1.1', port: 8080, flag: 'GET /admin', safe: false, threat: 'Admin Panel Scan' }
            ];

            let packetCount = 0;
            const interval = setInterval(() => {
                if (packetCount > 50) {
                    clearInterval(interval);
                    isMonitoring = false;
                    return;
                }

                const packet = packetTypes[Math.floor(Math.random() * packetTypes.length)];
                const isSuspicious = !packet.safe && Math.random() > 0.7;
                
                addPacketLine(packet, isSuspicious);
                
                if (isSuspicious && packet.threat) {
                    addThreat(packet.threat, 'high');
                    blockedAttacks++;
                    document.getElementById('blockedAttacks').textContent = blockedAttacks;
                    updateSecurityScore(securityScore - 5);
                }
                
                packetCount++;
            }, 200);
        }

        function addPacketLine(packet, isSuspicious) {
            const visualizer = document.getElementById('packetVisualizer');
            const line = document.createElement('div');
            line.className = 'packet-line';
            
            const time = new Date().toLocaleTimeString('es-ES', { hour12: false });
            const colorClass = isSuspicious ? 'packet-danger' : packet.safe ? '' : 'packet-warning';
            
            line.innerHTML = `
                <span class="packet-header">[${time}]</span>
                <span class="${colorClass}">
                    ${packet.type} ${packet.src}:${packet.port} → ${packet.dst} [${packet.flag}]
                    ${isSuspicious ? '⚠️ AMENAZA DETECTADA' : ''}
                </span>
            `;
            
            visualizer.appendChild(line);
            visualizer.scrollTop = visualizer.scrollHeight;
            
            if (visualizer.children.length > 20) {
                visualizer.removeChild(visualizer.firstChild);
            }
        }

        function addThreat(description, level) {
            const list = document.getElementById('threatList');
            const item = document.createElement('div');
            item.className = 'threat-item fade-in';
            
            const time = new Date().toLocaleTimeString('es-ES');
            item.innerHTML = `
                <div>
                    <div style="font-weight: 600; color: ${level === 'high' ? '#ff3366' : '#ffcc00'};">
                        ${description}
                    </div>
                    <div style="font-size: 0.85rem; color: rgba(255,255,255,0.6);">${time}</div>
                </div>
                <span class="threat-level ${level}">${level.toUpperCase()}</span>
            `;
            
            list.insertBefore(item, list.firstChild);
            if (list.children.length > 10) list.removeChild(list.lastChild);
        }

        function scanDevices() {
            const grid = document.getElementById('deviceGrid');
            grid.innerHTML = '<div style="grid-column: 1/-1; text-align: center; padding: 40px;"><div class="loading"></div><p style="margin-top: 20px;">Escaneando dispositivos...</p></div>';
            
            setTimeout(() => {
                connectedDevices = [
                    { name: 'iPhone de Juan', ip: '192.168.1.101', mac: 'A4:5E:60:E8:12:34', type: 'mobile', traffic: '45 MB/s', suspicious: false },
                    { name: 'Smart TV Samsung', ip: '192.168.1.102', mac: 'BC:23:45:F1:56:78', type: 'tv',
