<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Копилка — Своя тема | Редактор | Сакура | Массовые покупки</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --transition: all 0.25s cubic-bezier(0.2, 0.9, 0.4, 1.1);
        }

        body {
            font-family: 'Segoe UI', 'Roboto', system-ui, sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            transition: background 0.3s ease, color 0.2s;
            position: relative;
            overflow-x: hidden;
        }

        /* ====== CSS-ГЕОМЕТРИЯ ====== */
        body.theme-geometric::before,
        body.theme-waves::before,
        body.theme-dots::before,
        body.theme-stripes::before,
        body.theme-triangles::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        body.theme-geometric::before {
            background-image: 
                repeating-linear-gradient(45deg, rgba(255,255,255,0.06) 0px, rgba(255,255,255,0.06) 2px, transparent 2px, transparent 12px),
                repeating-linear-gradient(-45deg, rgba(255,255,255,0.06) 0px, rgba(255,255,255,0.06) 2px, transparent 2px, transparent 12px);
        }

        body.theme-waves::before {
            background: 
                repeating-linear-gradient(90deg, transparent, transparent 40px, rgba(255,255,255,0.05) 40px, rgba(255,255,255,0.05) 41px),
                repeating-linear-gradient(0deg, transparent, transparent 40px, rgba(255,255,255,0.05) 40px, rgba(255,255,255,0.05) 41px);
            animation: waveMove 12s linear infinite;
        }
        @keyframes waveMove {
            0% { transform: translateX(0) translateY(0); }
            100% { transform: translateX(40px) translateY(40px); }
        }

        body.theme-dots::before {
            background-image: radial-gradient(circle, rgba(255,255,255,0.12) 1.5px, transparent 1.5px);
            background-size: 28px 28px;
        }

        body.theme-stripes::before {
            background: repeating-linear-gradient(45deg, transparent, transparent 18px, rgba(255,255,255,0.06) 18px, rgba(255,255,255,0.06) 20px);
        }

        body.theme-triangles::before {
            background-image: 
                linear-gradient(30deg, rgba(255,255,255,0.06) 12%, transparent 12.5%, transparent 87%, rgba(255,255,255,0.06) 87.5%),
                linear-gradient(150deg, rgba(255,255,255,0.06) 12%, transparent 12.5%, transparent 87%, rgba(255,255,255,0.06) 87.5%),
                linear-gradient(30deg, rgba(255,255,255,0.06) 12%, transparent 12.5%, transparent 87%, rgba(255,255,255,0.06) 87.5%),
                linear-gradient(150deg, rgba(255,255,255,0.06) 12%, transparent 12.5%, transparent 87%, rgba(255,255,255,0.06) 87.5%);
            background-size: 70px 120px;
            background-position: 0 0, 0 0, 35px 60px, 35px 60px;
        }

        /* ====== RGB АНИМАЦИЯ (исправлена) ====== */
        @keyframes rgbBorder {
            0% { 
                box-shadow: 0 0 15px rgba(255,0,0,0.8), 0 0 30px rgba(255,0,0,0.4), inset 0 0 15px rgba(255,0,0,0.2);
                border-color: #ff0000;
            }
            16% { 
                box-shadow: 0 0 15px rgba(255,255,0,0.8), 0 0 30px rgba(255,255,0,0.4), inset 0 0 15px rgba(255,255,0,0.2);
                border-color: #ffff00;
            }
            33% { 
                box-shadow: 0 0 15px rgba(0,255,0,0.8), 0 0 30px rgba(0,255,0,0.4), inset 0 0 15px rgba(0,255,0,0.2);
                border-color: #00ff00;
            }
            50% { 
                box-shadow: 0 0 15px rgba(0,255,255,0.8), 0 0 30px rgba(0,255,255,0.4), inset 0 0 15px rgba(0,255,255,0.2);
                border-color: #00ffff;
            }
            66% { 
                box-shadow: 0 0 15px rgba(0,0,255,0.8), 0 0 30px rgba(0,0,255,0.4), inset 0 0 15px rgba(0,0,255,0.2);
                border-color: #0000ff;
            }
            83% { 
                box-shadow: 0 0 15px rgba(255,0,255,0.8), 0 0 30px rgba(255,0,255,0.4), inset 0 0 15px rgba(255,0,255,0.2);
                border-color: #ff00ff;
            }
            100% { 
                box-shadow: 0 0 15px rgba(255,0,0,0.8), 0 0 30px rgba(255,0,0,0.4), inset 0 0 15px rgba(255,0,0,0.2);
                border-color: #ff0000;
            }
        }
        body.rgb-mode .container {
            animation: rgbBorder 2.5s ease-in-out infinite;
            border-radius: 32px;
            border: 3px solid #ff0000;
            position: relative;
            z-index: 10;
        }
        /* Отключаем геометрические эффекты в RGB режиме, чтобы не мешали */
        body.rgb-mode.theme-geometric::before,
        body.rgb-mode.theme-waves::before,
        body.rgb-mode.theme-dots::before,
        body.rgb-mode.theme-stripes::before,
        body.rgb-mode.theme-triangles::before {
            opacity: 0.3;
        }

        .container {
            max-width: 860px;
            width: 100%;
            border-radius: 32px;
            padding: 28px 24px;
            transition: background 0.3s ease, box-shadow 0.3s, color 0.2s, border 0.3s ease;
            position: relative;
            z-index: 10;
            border: 3px solid transparent;
        }

        .header {
            display: flex;
            justify-content: center;
            align-items: center;
            margin-bottom: 28px;
            flex-wrap: wrap;
            gap: 16px;
            position: relative;
        }
        h1 {
            font-size: 32px;
            font-weight: 800;
            letter-spacing: -0.5px;
            text-align: center;
            flex: 1;
        }

        .theme-dropdown { position: relative; display: inline-block; }
        .theme-main-btn { background: #3b3b5c; border: none; padding: 10px 20px; border-radius: 40px; font-weight: bold; cursor: pointer; font-size: 14px; color: white; transition: 0.2s; }
        .theme-menu {
            position: absolute; top: 50px; right: 0; background: #1e1e2f; border-radius: 24px; padding: 12px; display: flex; flex-direction: column; gap: 8px;
            min-width: 200px; z-index: 200; box-shadow: 0 10px 25px rgba(0,0,0,0.2); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.2);
            max-height: 450px;
            overflow-y: auto;
        }
        .theme-menu button { background: rgba(255,255,255,0.1); border: none; padding: 8px 12px; border-radius: 30px; color: white; font-weight: 500; cursor: pointer; text-align: left; transition: 0.2s; }
        .theme-menu button:hover { background: rgba(255,255,255,0.3); transform: scale(0.98); }
        .hidden { display: none; }
        .rgb-toggle { 
            background: linear-gradient(45deg, #ff0000, #ffff00, #00ff00, #00ffff, #0000ff, #ff00ff); 
            color: white; 
            border: none; 
            padding: 8px 16px; 
            border-radius: 40px; 
            font-weight: bold; 
            cursor: pointer; 
            font-size: 13px;
            background-size: 300% 300%;
            animation: rgbBtn 3s ease-in-out infinite;
            transition: 0.3s;
        }
        @keyframes rgbBtn {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        .rgb-toggle:hover { transform: scale(1.05); }
        .rgb-toggle.active { 
            box-shadow: 0 0 20px rgba(255,0,0,0.5), 0 0 40px rgba(0,255,0,0.3), 0 0 60px rgba(0,0,255,0.2);
        }

        .tabs {
            display: flex;
            gap: 8px;
            margin-bottom: 28px;
            border-bottom: 2px solid rgba(0,0,0,0.1);
            padding-bottom: 8px;
            flex-wrap: wrap;
        }
        .tab-btn {
            background: transparent !important;
            color: inherit !important;
            font-size: 15px;
            font-weight: 600;
            padding: 8px 16px;
            border-radius: 40px;
            transition: 0.2s;
            opacity: 0.7;
            min-height: 44px;
        }
        .tab-btn.active {
            opacity: 1;
            background: rgba(128,128,128,0.2) !important;
            box-shadow: 0 2px 6px rgba(0,0,0,0.05);
        }
        .tab-content {
            display: none;
            animation: fade 0.25s ease;
        }
        .tab-content.active-tab {
            display: block;
        }
        @keyframes fade {
            from { opacity: 0; transform: translateY(6px);}
            to { opacity: 1; transform: translateY(0);}
        }

        .goal-section { margin-bottom: 24px; }
        label { display: block; margin-bottom: 8px; font-weight: 600; font-size: 14px; }
        .goal-input-group { display: flex; gap: 12px; flex-wrap: wrap; }
        input, button { padding: 12px 16px; border-radius: 28px; font-size: 15px; font-family: inherit; transition: var(--transition); min-height: 44px; }
        button { cursor: pointer; font-weight: 600; border: none; }
        button:active { transform: scale(0.97); }
        .stats { border-radius: 24px; padding: 20px; margin-bottom: 24px; }
        .stat-value { font-size: 28px; font-weight: 800; }
        
        .progress-bar { 
            width: 100%; 
            height: 32px; 
            background: rgba(0, 0, 0, 0.15); 
            border-radius: 40px; 
            overflow: hidden; 
            margin: 16px 0 4px;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);
        }
        .progress-fill { 
            height: 100%; 
            border-radius: 40px; 
            transition: width 0.5s ease; 
            display: flex; 
            align-items: center; 
            justify-content: center; 
            color: white; 
            font-weight: 800; 
            font-size: 14px;
            text-shadow: 0 1px 3px rgba(0,0,0,0.4);
            width: 0%;
        }

        .operations { display: flex; gap: 12px; margin-bottom: 28px; flex-wrap: wrap; }
        .withdraw-btn { background: #ef4444 !important; }
        .wishlist-section { margin: 20px 0 24px; }
        .add-item-form { display: flex; flex-wrap: wrap; gap: 12px; margin-bottom: 18px; }
        .items-grid { max-height: 320px; overflow-y: auto; display: flex; flex-direction: column; gap: 12px; -webkit-overflow-scrolling: touch; }
        .wishlist-item { display: flex; justify-content: space-between; flex-wrap: wrap; padding: 14px 16px; border-radius: 24px; gap: 10px; }
        .quantity-control { display: flex; gap: 8px; margin-top: 6px; align-items: center; }
        .qty-btn { background: #cbd5e1; padding: 4px 12px; border-radius: 30px; font-weight: bold; min-height: 36px; min-width: 36px; }
        .mini-progress { height: 12px; background: rgba(0,0,0,0.1); border-radius: 20px; overflow: hidden; margin: 6px 0; }
        .mini-fill { height: 100%; width: 0%; background: #22c55e; }
        .item-actions { display: flex; gap: 8px; flex-wrap: wrap; }
        .buy-item-btn { background: #22c55e; padding: 6px 14px; font-size: 12px; min-height: 36px; }
        .del-item-btn { background: #ef4444; padding: 6px 12px; min-height: 36px; }
        .history-list { max-height: 220px; overflow-y: auto; border-radius: 20px; margin-bottom: 14px; -webkit-overflow-scrolling: touch; }
        .history-item { padding: 12px 16px; margin-bottom: 8px; border-radius: 18px; display: flex; justify-content: space-between; flex-wrap: wrap; gap: 8px; }
        .reset-btn { width: 100%; margin-top: 6px; background: #94a3b8 !important; }
        .empty-items, .empty-history-message { text-align: center; padding: 24px; font-style: italic; opacity: 0.7; }
        .total-wish-cost { font-weight: 700; padding: 6px 14px; border-radius: 40px; background: rgba(0,0,0,0.05); display: inline-block; }
        .wishlist-header { display: flex; justify-content: space-between; margin-bottom: 16px; flex-wrap: wrap; }

        .bulk-progress-wrapper {
            background: rgba(0,0,0,0.06);
            border-radius: 40px;
            padding: 8px 8px 8px 18px;
            margin: 14px 0 18px;
            display: flex;
            align-items: center;
            gap: 14px;
            flex-wrap: wrap;
            border: 1px solid rgba(255,255,255,0.08);
        }
        .bulk-progress-track {
            flex: 1;
            min-width: 140px;
            height: 28px;
            background: rgba(0,0,0,0.15);
            border-radius: 40px;
            overflow: hidden;
            position: relative;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);
        }
        .bulk-progress-fill {
            height: 100%;
            border-radius: 40px;
            transition: width 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            width: 0%;
            display: flex;
            align-items: center;
            justify-content: flex-end;
            padding-right: 10px;
            font-size: 13px;
            font-weight: 800;
            color: white;
            text-shadow: 0 1px 3px rgba(0,0,0,0.5);
            white-space: nowrap;
        }
        .bulk-progress-label {
            font-weight: 600;
            font-size: 14px;
            min-width: 100px;
            color: inherit !important;
        }
        .bulk-progress-label .highlight {
            font-weight: 800;
            font-size: 16px;
            color: inherit !important;
        }

        .bulk-select-all {
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            gap: 12px;
            flex-wrap: wrap;
            justify-content: space-between;
        }
        .bulk-actions-bar {
            display: flex;
            gap: 12px;
            align-items: center;
            flex-wrap: wrap;
        }
        .bulk-buy-confirm { background: #f59e0b !important; padding: 10px 20px; }
        .bulk-clear { background: #64748b !important; }
        .bulk-item {
            display: flex;
            align-items: center;
            gap: 14px;
            background: rgba(0,0,0,0.03);
            padding: 12px 16px;
            border-radius: 24px;
            margin-bottom: 10px;
            transition: 0.1s;
            flex-wrap: wrap;
        }
        .bulk-item input[type="checkbox"] {
            width: 24px;
            height: 24px;
            cursor: pointer;
            accent-color: #f59e0b;
            transform: scale(1);
            margin: 0;
            min-width: 24px;
        }
        .bulk-item-info { flex: 2; min-width: 120px; }
        .bulk-item-name { font-weight: 700; font-size: 16px; }
        .bulk-item-details { font-size: 13px; opacity: 0.8; }
        .bulk-item-cost { font-weight: 800; font-size: 16px; min-width: 110px; text-align: right; }
        .bulk-status { font-size: 13px; background: rgba(0,0,0,0.1); border-radius: 30px; padding: 4px 12px; }
        .bulk-status.ok { background: rgba(34,197,94,0.25); color: #16a34a; }
        .bulk-status.need { background: rgba(239,68,68,0.2); color: #dc2626; }

        .reset-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.75);
            backdrop-filter: blur(8px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 4000;
            padding: 20px;
        }
        .reset-panel {
            background: #1e1a2f;
            border-radius: 48px;
            padding: 28px;
            max-width: 420px;
            width: 100%;
            color: white;
            box-shadow: 0 25px 45px rgba(0,0,0,0.5);
            border: 1px solid rgba(255,255,255,0.2);
        }
        .reset-panel h3 { font-size: 22px; margin-bottom: 16px; text-align: center; }
        .reset-panel label {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 10px 0;
            border-bottom: 1px solid rgba(255,255,255,0.06);
            font-weight: 500;
            cursor: pointer;
            font-size: 15px;
        }
        .reset-panel label:last-child { border-bottom: none; }
        .reset-panel input[type="checkbox"] {
            width: 20px;
            height: 20px;
            accent-color: #ef4444;
            cursor: pointer;
        }
        .reset-panel .reset-buttons {
            display: flex;
            gap: 12px;
            margin-top: 20px;
        }
        .reset-panel .reset-buttons button {
            flex: 1;
            padding: 12px;
            border-radius: 28px;
            font-weight: 600;
        }
        .reset-panel .reset-buttons .btn-confirm { background: #ef4444; color: white; }
        .reset-panel .reset-buttons .btn-cancel { background: #64748b; color: white; }

        .author-section {
            text-align: center;
            padding: 20px 0;
        }
        .author-section .avatar {
            font-size: 72px;
            margin-bottom: 12px;
        }
        .author-section h3 {
            font-size: 24px;
            margin-bottom: 8px;
        }
        .author-section p {
            opacity: 0.8;
            margin-bottom: 20px;
            font-size: 15px;
        }
        .author-links {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 12px;
            margin-top: 16px;
        }
        .author-links a {
            display: inline-block;
            padding: 10px 20px;
            border-radius: 40px;
            background: rgba(255,255,255,0.1);
            color: inherit;
            text-decoration: none;
            font-weight: 600;
            transition: 0.2s;
            border: 1px solid rgba(255,255,255,0.1);
            min-height: 44px;
        }
        .author-links a:hover {
            background: rgba(255,255,255,0.2);
            transform: translateY(-2px);
        }
        .author-links a .link-icon {
            margin-right: 6px;
        }

        .theme-editor-modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.85);
            backdrop-filter: blur(12px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 3000;
            padding: 20px;
        }
        .editor-panel {
            background: #1e1a2f;
            border-radius: 48px;
            padding: 28px;
            max-width: 500px;
            width: 100%;
            color: white;
            box-shadow: 0 25px 45px rgba(0,0,0,0.5);
            border: 1px solid rgba(255,255,255,0.2);
            max-height: 90vh;
            overflow-y: auto;
        }
        .editor-panel h3 { margin-bottom: 20px; font-size: 24px; text-align: center; }
        .editor-panel label { display: block; margin: 12px 0 6px; font-weight: 600; }
        .editor-panel input, .editor-panel textarea, .editor-panel select {
            width: 100%;
            padding: 10px 14px;
            border-radius: 28px;
            border: none;
            background: #2d2a55;
            color: white;
            font-family: monospace;
        }
        .editor-panel select { appearance: auto; }
        .editor-panel textarea { resize: vertical; font-family: monospace; }
        .editor-buttons { display: flex; gap: 12px; margin-top: 24px; flex-wrap: wrap; }
        .editor-buttons button { flex: 1; background: #7c3aed; color: white; min-height: 44px; }
        .effect-checkbox { display: flex; align-items: center; gap: 8px; margin: 10px 0; }
        
        .sakura-petal {
            position: fixed;
            pointer-events: none;
            z-index: 9999;
            width: 12px;
            height: 12px;
            background: #ffb7c5;
            border-radius: 100% 0% 100% 0%;
            transform: rotate(45deg);
            box-shadow: -1px -1px 3px rgba(255, 160, 180, 0.4);
            animation: fallDown linear forwards;
            opacity: 0.85;
        }
        .sakura-petal::before {
            content: "";
            position: absolute;
            width: 6px;
            height: 6px;
            background: #ff99aa;
            border-radius: 50%;
            top: 3px;
            left: 3px;
            opacity: 0.6;
        }
        @keyframes fallDown {
            0% { transform: translateY(-10vh) rotate(0deg); opacity: 0.9; }
            100% { transform: translateY(110vh) rotate(360deg); opacity: 0; }
        }
        
        .custom-particle {
            position: fixed;
            pointer-events: none;
            z-index: 9998;
            background: radial-gradient(circle, rgba(255,200,100,0.7), transparent);
            border-radius: 50%;
            animation: floatUp linear forwards;
        }
        @keyframes floatUp {
            0% { transform: translateY(100vh) scale(0); opacity: 0.8; }
            100% { transform: translateY(-10vh) scale(1.2); opacity: 0; }
        }

        /* Адаптивность */
        @media (max-width: 600px) {
            .container { padding: 16px 12px; }
            h1 { font-size: 24px; }
            .header { gap: 10px; }
            .tabs { gap: 4px; }
            .tab-btn { font-size: 13px; padding: 6px 12px; min-height: 38px; }
            input, button { font-size: 14px; padding: 10px 12px; min-height: 44px; }
            .stat-value { font-size: 22px; }
            .goal-input-group { flex-direction: column; }
            .goal-input-group input { width: 100%; }
            .operations { flex-direction: column; }
            .operations input { width: 100%; }
            .add-item-form { flex-direction: column; }
            .add-item-form input { width: 100%; }
            .bulk-progress-wrapper { padding: 8px 12px; }
            .bulk-progress-label { font-size: 13px; min-width: 70px; }
            .bulk-item { flex-wrap: wrap; gap: 8px; }
            .bulk-item-cost { min-width: 80px; font-size: 14px; }
            .author-links a { font-size: 13px; padding: 8px 14px; }
            .reset-panel { padding: 20px; }
        }
        @media (min-width: 601px) and (max-width: 1024px) {
            .container { padding: 20px 16px; }
        }
        @media (hover: none) {
            .theme-menu button:hover { transform: none; background: rgba(255,255,255,0.1); }
            .author-links a:hover { transform: none; background: rgba(255,255,255,0.1); }
        }

        /* ====== ТЕМЫ ОФОРМЛЕНИЯ ====== */
        body.theme-light { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        body.theme-light .container { background: #ffffff; box-shadow: 0 20px 45px rgba(0,0,0,0.25); color: #1e293b; }
        body.theme-light button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #667eea; color: white; }
        body.theme-light .stats { background: #f1f5f9; }
        body.theme-light .progress-fill { background: linear-gradient(90deg, #a78bfa, #8b5cf6, #7c3aed); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-light .progress-fill.complete { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-light .bulk-progress-fill { background: linear-gradient(90deg, #60a5fa, #3b82f6, #2563eb); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-light .bulk-progress-fill.ready { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }
        
        body.theme-dark { background: linear-gradient(135deg, #0f172a 0%, #1e1b2e 100%); }
        body.theme-dark .container { background: #1e293b; box-shadow: 0 20px 45px rgba(0,0,0,0.5); color: #f1f5f9; }
        body.theme-dark button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #7c3aed; color: white; }
        body.theme-dark .stats { background: #0f172a; }
        body.theme-dark .progress-fill { background: linear-gradient(90deg, #f472b6, #ec4899, #db2777); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; box-shadow: 0 0 20px rgba(236,72,153,0.4); }
        body.theme-dark .progress-fill.complete { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; box-shadow: 0 0 20px rgba(34,197,94,0.4); }
        body.theme-dark .bulk-progress-fill { background: linear-gradient(90deg, #a78bfa, #8b5cf6, #7c3aed); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; box-shadow: 0 0 20px rgba(139,92,246,0.3); }
        body.theme-dark .bulk-progress-fill.ready { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; box-shadow: 0 0 20px rgba(34,197,94,0.4); }
        
        body.theme-sunset { background: linear-gradient(135deg, #fbc2eb 0%, #a6c1ee 100%); }
        body.theme-sunset .container { background: #fff5f9; color: #831843; }
        body.theme-sunset button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #db2777; color: white; }
        body.theme-sunset .stats { background: #fdf2f8; }
        body.theme-sunset .progress-fill { background: linear-gradient(90deg, #fb923c, #f97316, #ea580c); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-sunset .progress-fill.complete { background: linear-gradient(90deg, #fbbf24, #f59e0b, #d97706); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-sunset .bulk-progress-fill { background: linear-gradient(90deg, #f472b6, #ec4899, #db2777); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-sunset .bulk-progress-fill.ready { background: linear-gradient(90deg, #fbbf24, #f59e0b, #d97706); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }
        
        body.theme-ocean { background: linear-gradient(135deg, #00c6fb 0%, #005bea 100%); }
        body.theme-ocean .container { background: #eef5ff; color: #0c4a6e; }
        body.theme-ocean button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #0284c7; color: white; }
        body.theme-ocean .stats { background: #e0f2fe; }
        body.theme-ocean .progress-fill { background: linear-gradient(90deg, #38bdf8, #0ea5e9, #0284c7); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-ocean .progress-fill.complete { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-ocean .bulk-progress-fill { background: linear-gradient(90deg, #7dd3fc, #38bdf8, #0ea5e9); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-ocean .bulk-progress-fill.ready { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }
        
        body.theme-forest { background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%); }
        body.theme-forest .container { background: #f1f9f0; color: #14532d; }
        body.theme-forest button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #16a34a; color: white; }
        body.theme-forest .stats { background: #dcfce7; }
        body.theme-forest .progress-fill { background: linear-gradient(90deg, #4ade80, #22c55e, #16a34a); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-forest .progress-fill.complete { background: linear-gradient(90deg, #fbbf24, #f59e0b, #d97706); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-forest .bulk-progress-fill { background: linear-gradient(90deg, #86efac, #4ade80, #22c55e); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-forest .bulk-progress-fill.ready { background: linear-gradient(90deg, #fbbf24, #f59e0b, #d97706); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }
        
        body.theme-cosmic { background: linear-gradient(135deg, #2b1b4e 0%, #e956a7 100%); }
        body.theme-cosmic .container { background: #1e1a3a; color: #e9d5ff; }
        body.theme-cosmic button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #a855f7; color: white; }
        body.theme-cosmic .stats { background: #2e2359; }
        body.theme-cosmic .progress-fill { background: linear-gradient(90deg, #c084fc, #a855f7, #7c3aed); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; box-shadow: 0 0 25px rgba(168,85,247,0.4); }
        body.theme-cosmic .progress-fill.complete { background: linear-gradient(90deg, #fbbf24, #f59e0b, #d97706); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; box-shadow: 0 0 25px rgba(245,158,11,0.4); }
        body.theme-cosmic .bulk-progress-fill { background: linear-gradient(90deg, #e879f9, #d946ef, #c026d3); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; box-shadow: 0 0 20px rgba(217,70,239,0.3); }
        body.theme-cosmic .bulk-progress-fill.ready { background: linear-gradient(90deg, #fbbf24, #f59e0b, #d97706); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; box-shadow: 0 0 25px rgba(245,158,11,0.4); }
        
        body.theme-desert { background: linear-gradient(135deg, #f5af19 0%, #f12711 100%); }
        body.theme-desert .container { background: #fff5e6; color: #7c2d12; }
        body.theme-desert button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #ea580c; color: white; }
        body.theme-desert .stats { background: #ffedd5; }
        body.theme-desert .progress-fill { background: linear-gradient(90deg, #fcd34d, #f59e0b, #d97706); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-desert .progress-fill.complete { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-desert .bulk-progress-fill { background: linear-gradient(90deg, #fdba74, #fb923c, #f97316); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-desert .bulk-progress-fill.ready { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }
        
        body.theme-marlboro { background: linear-gradient(135deg, #8b0000 0%, #cc0000 100%); }
        body.theme-marlboro .container { background: #fffaf0; border: 1px solid #b22222; color: #4a2c2c; }
        body.theme-marlboro button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #b22222; color: white; }
        body.theme-marlboro .stats { background: #fef3e2; border-left: 6px solid #b22222; }
        body.theme-marlboro .progress-fill { background: linear-gradient(90deg, #f87171, #ef4444, #dc2626); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-marlboro .progress-fill.complete { background: linear-gradient(90deg, #fcd34d, #f59e0b, #d97706); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-marlboro .bulk-progress-fill { background: linear-gradient(90deg, #fca5a5, #f87171, #ef4444); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-marlboro .bulk-progress-fill.ready { background: linear-gradient(90deg, #fcd34d, #f59e0b, #d97706); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }
        
        body.theme-sakura { background: radial-gradient(circle at 10% 20%, #fff0f5, #ffe0e8); }
        body.theme-sakura .container { background: rgba(255, 245, 250, 0.94); backdrop-filter: blur(3px); border: 1px solid #ffb7c5; color: #b34562; }
        body.theme-sakura button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #e66a8c; color: white; }
        body.theme-sakura .stats { background: #ffeef4; border-left: 5px solid #f28b9e; }
        body.theme-sakura .progress-fill { background: linear-gradient(90deg, #f9a8d4, #f472b6, #ec4899); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-sakura .progress-fill.complete { background: linear-gradient(90deg, #fcd34d, #fbbf24, #f59e0b); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-sakura .bulk-progress-fill { background: linear-gradient(90deg, #fbcfe8, #f9a8d4, #f472b6); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-sakura .bulk-progress-fill.ready { background: linear-gradient(90deg, #fcd34d, #fbbf24, #f59e0b); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }

        body.theme-midnight { background: linear-gradient(135deg, #0c0c1d 0%, #1a1a3e 50%, #2d1b4e 100%); }
        body.theme-midnight .container { background: rgba(20, 20, 50, 0.95); border: 1px solid rgba(100, 80, 200, 0.3); color: #c8b8ff; }
        body.theme-midnight button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #4a3a7a; color: white; }
        body.theme-midnight .stats { background: rgba(30, 20, 60, 0.6); border-left: 5px solid #7c5cbf; }
        body.theme-midnight .progress-fill { background: linear-gradient(90deg, #7c5cbf, #a78bfa, #7c5cbf); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-midnight .progress-fill.complete { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-midnight .bulk-progress-fill { background: linear-gradient(90deg, #7c5cbf, #a78bfa, #7c5cbf); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-midnight .bulk-progress-fill.ready { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }

        body.theme-aurora { background: linear-gradient(135deg, #1a472a 0%, #2d6b4e 30%, #1a4a6b 60%, #2d1b4e 100%); }
        body.theme-aurora .container { background: rgba(20, 40, 35, 0.95); border: 1px solid rgba(80, 200, 150, 0.2); color: #b8e8d8; }
        body.theme-aurora button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #2a7a5a; color: white; }
        body.theme-aurora .stats { background: rgba(30, 60, 50, 0.5); border-left: 5px solid #4ab89a; }
        body.theme-aurora .progress-fill { background: linear-gradient(90deg, #4ab89a, #6dd5b8, #4ab89a); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-aurora .progress-fill.complete { background: linear-gradient(90deg, #fbbf24, #f59e0b, #d97706); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-aurora .bulk-progress-fill { background: linear-gradient(90deg, #4ab89a, #6dd5b8, #4ab89a); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-aurora .bulk-progress-fill.ready { background: linear-gradient(90deg, #fbbf24, #f59e0b, #d97706); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }

        body.theme-lavender { background: linear-gradient(135deg, #e8d5f5 0%, #d4b8e8 50%, #c49ae0 100%); }
        body.theme-lavender .container { background: rgba(255, 248, 255, 0.95); border: 1px solid #c49ae0; color: #4a2d6b; }
        body.theme-lavender button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #9b6bc4; color: white; }
        body.theme-lavender .stats { background: rgba(235, 215, 245, 0.5); border-left: 5px solid #b88ad4; }
        body.theme-lavender .progress-fill { background: linear-gradient(90deg, #b88ad4, #d4a8e8, #b88ad4); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-lavender .progress-fill.complete { background: linear-gradient(90deg, #fbbf24, #f59e0b, #d97706); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-lavender .bulk-progress-fill { background: linear-gradient(90deg, #b88ad4, #d4a8e8, #b88ad4); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-lavender .bulk-progress-fill.ready { background: linear-gradient(90deg, #fbbf24, #f59e0b, #d97706); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }

        body.theme-cherry { background: linear-gradient(135deg, #4a0e1a 0%, #8b1a2e 40%, #cc2244 100%); }
        body.theme-cherry .container { background: rgba(60, 15, 25, 0.95); border: 1px solid #cc2244; color: #ffc8d4; }
        body.theme-cherry button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #cc2244; color: white; }
        body.theme-cherry .stats { background: rgba(80, 20, 35, 0.5); border-left: 5px solid #ff4470; }
        body.theme-cherry .progress-fill { background: linear-gradient(90deg, #ff4470, #ff6b8a, #ff4470); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-cherry .progress-fill.complete { background: linear-gradient(90deg, #fbbf24, #f59e0b, #d97706); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-cherry .bulk-progress-fill { background: linear-gradient(90deg, #ff4470, #ff6b8a, #ff4470); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-cherry .bulk-progress-fill.ready { background: linear-gradient(90deg, #fbbf24, #f59e0b, #d97706); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }

        body.theme-geometric { background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%); }
        body.theme-geometric .container { background: rgba(20, 25, 50, 0.92); border: 1px solid rgba(100, 150, 255, 0.15); color: #d0d8ff; }
        body.theme-geometric button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #2a4a7a; color: white; }
        body.theme-geometric .stats { background: rgba(30, 40, 70, 0.5); border-left: 5px solid #4a8aff; }
        body.theme-geometric .progress-fill { background: linear-gradient(90deg, #4a8aff, #7aafff, #4a8aff); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-geometric .progress-fill.complete { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-geometric .bulk-progress-fill { background: linear-gradient(90deg, #4a8aff, #7aafff, #4a8aff); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-geometric .bulk-progress-fill.ready { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }

        body.theme-waves { background: linear-gradient(135deg, #0d1b2a 0%, #1b3a4b 50%, #0d2b3e 100%); }
        body.theme-waves .container { background: rgba(15, 30, 45, 0.92); border: 1px solid rgba(80, 200, 220, 0.15); color: #b8e8f0; }
        body.theme-waves button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #1a5a6a; color: white; }
        body.theme-waves .stats { background: rgba(20, 50, 60, 0.5); border-left: 5px solid #4ac8e0; }
        body.theme-waves .progress-fill { background: linear-gradient(90deg, #4ac8e0, #7ad8f0, #4ac8e0); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-waves .progress-fill.complete { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-waves .bulk-progress-fill { background: linear-gradient(90deg, #4ac8e0, #7ad8f0, #4ac8e0); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-waves .bulk-progress-fill.ready { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }

        body.theme-dots { background: linear-gradient(135deg, #1a1a2e 0%, #2d1b3a 50%, #1a1a2e 100%); }
        body.theme-dots .container { background: rgba(30, 20, 45, 0.92); border: 1px solid rgba(180, 120, 220, 0.15); color: #d8c8f0; }
        body.theme-dots button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #4a2a7a; color: white; }
        body.theme-dots .stats { background: rgba(40, 25, 60, 0.5); border-left: 5px solid #8a5ac8; }
        body.theme-dots .progress-fill { background: linear-gradient(90deg, #8a5ac8, #ba8ae8, #8a5ac8); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-dots .progress-fill.complete { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-dots .bulk-progress-fill { background: linear-gradient(90deg, #8a5ac8, #ba8ae8, #8a5ac8); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-dots .bulk-progress-fill.ready { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }

        body.theme-stripes { background: linear-gradient(135deg, #1a1a2e 0%, #1a2a3a 50%, #1a1a2e 100%); }
        body.theme-stripes .container { background: rgba(25, 35, 50, 0.92); border: 1px solid rgba(200, 180, 100, 0.15); color: #e8e0c8; }
        body.theme-stripes button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #4a5a2a; color: white; }
        body.theme-stripes .stats { background: rgba(40, 50, 30, 0.5); border-left: 5px solid #b8b84a; }
        body.theme-stripes .progress-fill { background: linear-gradient(90deg, #b8b84a, #d8d86a, #b8b84a); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-stripes .progress-fill.complete { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-stripes .bulk-progress-fill { background: linear-gradient(90deg, #b8b84a, #d8d86a, #b8b84a); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-stripes .bulk-progress-fill.ready { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }

        body.theme-triangles { background: linear-gradient(135deg, #0d0d2b 0%, #1a1a3a 50%, #2d0d2b 100%); }
        body.theme-triangles .container { background: rgba(20, 15, 40, 0.92); border: 1px solid rgba(255, 100, 150, 0.15); color: #f0c8d8; }
        body.theme-triangles button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: #6a2a4a; color: white; }
        body.theme-triangles .stats { background: rgba(50, 20, 40, 0.5); border-left: 5px solid #e85a8a; }
        body.theme-triangles .progress-fill { background: linear-gradient(90deg, #e85a8a, #f08aaa, #e85a8a); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-triangles .progress-fill.complete { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-triangles .bulk-progress-fill { background: linear-gradient(90deg, #e85a8a, #f08aaa, #e85a8a); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-triangles .bulk-progress-fill.ready { background: linear-gradient(90deg, #34d399, #22c55e, #16a34a); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }

        body.theme-custom .progress-fill { background: var(--custom-progress, linear-gradient(90deg, #8b5cf6, #ec4899, #f59e0b)); background-size: 200% 100%; animation: shimmer 3s ease-in-out infinite; }
        body.theme-custom .progress-fill.complete { background: var(--custom-progress-complete, linear-gradient(90deg, #22c55e, #16a34a, #15803d)); background-size: 200% 100%; animation: shimmer 2s ease-in-out infinite; }
        body.theme-custom .bulk-progress-fill { background: var(--custom-bulk-progress, linear-gradient(90deg, #8b5cf6, #ec4899, #f59e0b)); background-size: 300% 100%; animation: bulkShimmer 4s ease-in-out infinite; }
        body.theme-custom .bulk-progress-fill.ready { background: var(--custom-bulk-ready, linear-gradient(90deg, #22c55e, #16a34a, #15803d)); background-size: 200% 100%; animation: bulkShimmer 2s ease-in-out infinite; }
        body.theme-custom .container { transition: all 0.2s; }

        @keyframes shimmer {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        @keyframes bulkShimmer {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
    </style>
</head>
<body class="theme-marlboro">
    <div class="container">
        <div class="header">
            <h1>КОПИЛКА</h1>
            <div style="display: flex; gap: 10px; flex-wrap: wrap;">
                <button id="rgbToggleBtn" class="rgb-toggle">🌈 RGB режим</button>
                <div class="theme-dropdown">
                    <button id="themeMenuBtn" class="theme-main-btn">Темы ▼</button>
                    <div id="themeMenu" class="theme-menu hidden">
                        <button data-theme="light">Светлая</button>
                        <button data-theme="dark">Тёмная</button>
                        <button data-theme="sunset">Закат</button>
                        <button data-theme="ocean">Океан</button>
                        <button data-theme="forest">Лес</button>
                        <button data-theme="cosmic">Космос</button>
                        <button data-theme="desert">Пустыня</button>
                        <button data-theme="marlboro">Marlboro</button>
                        <button data-theme="sakura">🌸Сакура</button>
                        <button data-theme="midnight">🌙Полночь</button>
                        <button data-theme="aurora">Северное сияние</button>
                        <button data-theme="lavender">Лаванда</button>
                        <button data-theme="cherry">Вишня</button>
                        <button data-theme="geometric">Геометрия</button>
                        <button data-theme="waves">Волны</button>
                        <button data-theme="dots">Точки</button>
                        <button data-theme="stripes">Полосы</button>
                        <button data-theme="triangles">Треугольники</button>
                        <button id="createCustomThemeBtn" style="background: #f59e0b; color:#1e1a2f;">Создать свою тему</button>
                    </div>
                </div>
            </div>
        </div>

        <div class="tabs">
            <button class="tab-btn active" data-tab="main">Основное</button>
            <button class="tab-btn" data-tab="bulk">Массовые покупки</button>
            <button class="tab-btn" data-tab="author">👤 Автор</button>
        </div>

        <!-- Вкладка Основное -->
        <div id="tab-main" class="tab-content active-tab">
            <div class="goal-section">
                <label>Финансовая цель</label>
                <div class="goal-input-group">
                    <input type="text" id="goalText" placeholder="Название цели" maxlength="55">
                    <input type="number" id="goalAmount" placeholder="Сумма" step="1000" value="100000">
                    <button onclick="setGoal()">Установить</button>
                </div>
            </div>

            <div class="stats">
                <div class="goal-text" id="goalDisplay">Цель: не задана</div>
                <div class="stat-item">
                    <div class="stat-label">Накоплено</div>
                    <div class="stat-value" id="savedAmount">0 ₽</div>
                </div>
                <div class="stat-item">
                    <div class="stat-label">Осталось до цели</div>
                    <div class="stat-value" id="remainingAmount">0 ₽</div>
                </div>
                <div class="progress-bar">
                    <div class="progress-fill" id="progressFill">0%</div>
                </div>
            </div>

            <div class="operations">
                <input type="number" id="amount" placeholder="Введите сумму" step="100">
                <button onclick="addMoney()">Добавить</button>
                <button onclick="withdrawMoney()" class="withdraw-btn">Снять</button>
            </div>

            <div class="wishlist-section">
                <div class="wishlist-header">
                    <span class="wishlist-title">Список покупок</span>
                    <span class="total-wish-cost" id="totalWishCostSpan">Общая стоимость: 0 ₽</span>
                </div>
                <div class="add-item-form">
                    <input type="text" id="itemName" placeholder="Название предмета">
                    <input type="number" id="itemPrice" placeholder="Цена за шт." value="50000" step="1000">
                    <button onclick="addWishItem()">Добавить предмет</button>
                </div>
                <div class="items-grid" id="wishlistContainer">
                    <div class="empty-items">Список покупок пуст</div>
                </div>
            </div>

            <div class="history-block">
                <div class="history-title">История операций</div>
                <div class="history-list" id="historyList">
                    <div class="empty-history-message">История пуста</div>
                </div>
                <button class="reset-btn" onclick="openResetModal()">Сбросить всё</button>
            </div>
        </div>

        <!-- Вкладка Массовые покупки -->
        <div id="tab-bulk" class="tab-content">
            <div style="margin-bottom: 16px;">
                <h3 style="font-size: 20px;">Выберите товары для массовой покупки</h3>
                <p style="margin-top: 4px; opacity: 0.7;">Отметьте нужные позиции — прогресс покажет, сколько средств хватит</p>
            </div>

            <div class="bulk-progress-wrapper" id="bulkProgressWrapper">
                <span class="bulk-progress-label">Доступно: <span class="highlight" id="bulkSavedDisplay">0</span> ₽</span>
                <div class="bulk-progress-track">
                    <div class="bulk-progress-fill" id="bulkProgressFill" style="width: 0%;">0%</div>
                </div>
                <span class="bulk-progress-label">нужно: <span class="highlight" id="bulkNeedDisplay">0</span> ₽</span>
            </div>

            <div id="bulkListContainer" class="bulk-list-area">
                <div class="empty-items">Загрузка...</div>
            </div>
            <div class="bulk-select-all" id="bulkSelectPanel" style="display: none;">
                <div class="bulk-actions-bar">
                    <button id="selectAllBtn" class="bulk-clear" style="background: #334155;">Выбрать всё</button>
                    <button id="deselectAllBtn" class="bulk-clear" style="background: #475569;">Снять всё</button>
                </div>
                <button id="bulkBuySelectedBtn" class="bulk-buy-confirm">Купить выбранные</button>
            </div>
        </div>

        <!-- Вкладка Автор -->
        <div id="tab-author" class="tab-content">
            <div class="author-section">
                <div class="avatar">By NekoSploit</div>
                <h3>Автор проекта</h3>
                <p>Создано от души для удобного управления финансами</p>
                <p style="font-size: 14px; opacity: 0.6;">Благодарю за использование! Если вам понравилось — поддержите звёздочкой на GitHub ⭐</p>
                <div class="author-links">
                    <a href="https://github.com/ExploitRunner2" target="_blank" rel="noopener noreferrer">
                        <span class="link-icon">on</span> GitHub
                    </a>
                    <a href="https://www.youtube.com/@Kayako_San" target="_blank" rel="noopener noreferrer">
                        <span class="link-icon">on</span> YouTube
                    </a>
                    <a href="https://t.me/Kayako_San" target="_blank" rel="noopener noreferrer">
                        <span class="link-icon">on</span> Telegram
                    </a>
                    <a href="https://vk.com/kayako_san" target="_blank" rel="noopener noreferrer">
                        <span class="link-icon">on</span> VK
                    </a>
                </div>
            </div>
        </div>
    </div>

    <script>
        let piggyData = {
            goalText: '',
            goalAmount: 100000,
            saved: 0,
            history: [],
            wishItems: []
        };
        let nextItemId = 1;
        let sakuraInterval = null;
        let customParticleInterval = null;

        function loadData() {
            const stored = localStorage.getItem('piggyBankApp');
            if (stored) {
                try {
                    const parsed = JSON.parse(stored);
                    piggyData = parsed;
                    if (!Array.isArray(piggyData.history)) piggyData.history = [];
                    if (!Array.isArray(piggyData.wishItems)) piggyData.wishItems = [];
                    if (piggyData.wishItems.length && !piggyData.wishItems[0].hasOwnProperty('quantity')) {
                        piggyData.wishItems = piggyData.wishItems.map(item => ({ ...item, quantity: item.quantity || 1 }));
                    }
                } catch(e) {}
            }
            if (!piggyData.wishItems) piggyData.wishItems = [];
            if (piggyData.wishItems.length) nextItemId = Math.max(...piggyData.wishItems.map(i=>i.id),0)+1;
            updateDisplay();
            renderWishlist();
            renderBulkList();
            updateBulkProgress();
        }
        function saveData() { localStorage.setItem('piggyBankApp', JSON.stringify(piggyData)); renderBulkList(); updateBulkProgress(); }
        function addHistory(type, amount, comment='') {
            piggyData.history.unshift({ type, amount, date: new Date().toLocaleString('ru-RU'), comment });
            if (piggyData.history.length > 35) piggyData.history.pop();
            saveData();
            renderHistory();
        }
        function renderHistory() {
            const container = document.getElementById('historyList');
            if (!piggyData.history.length) { container.innerHTML = '<div class="empty-history-message">История пуста</div>'; return; }
            container.innerHTML = '';
            for(let item of piggyData.history) {
                let amountStr = '';
                if(item.type === 'add') amountStr = `+ ${item.amount.toLocaleString()} ₽`;
                else if(item.type === 'withdraw') amountStr = `- ${item.amount.toLocaleString()} ₽`;
                else if(item.type === 'buy_item') amountStr = `Покупка ${item.comment} : -${item.amount.toLocaleString()} ₽`;
                else amountStr = `Цель: ${item.amount.toLocaleString()} ₽ (${item.comment})`;
                const div = document.createElement('div');
                div.className = `history-item`;
                div.innerHTML = `<span class="history-date">${item.date}</span><span class="history-amount">${amountStr}</span>`;
                container.appendChild(div);
            }
        }
        function updateDisplay() {
            const goalSpan = document.getElementById('goalDisplay');
            if(piggyData.goalText?.trim()) goalSpan.innerHTML = `Цель: ${piggyData.goalText} — ${piggyData.goalAmount.toLocaleString()} ₽`;
            else goalSpan.innerHTML = `Цель: ${piggyData.goalAmount.toLocaleString()} ₽`;
            document.getElementById('savedAmount').innerHTML = `${piggyData.saved.toLocaleString()} ₽`;
            const remaining = Math.max(0, piggyData.goalAmount - piggyData.saved);
            document.getElementById('remainingAmount').innerHTML = `${remaining.toLocaleString()} ₽`;
            let percent = Math.min(100, (piggyData.saved / piggyData.goalAmount) * 100);
            const fill = document.getElementById('progressFill');
            fill.style.width = `${percent}%`;
            fill.textContent = `${Math.round(percent)}%`;
            if (percent >= 100) {
                fill.classList.add('complete');
            } else {
                fill.classList.remove('complete');
            }
            renderHistory();
            updateBulkProgress();
        }
        function getTotalWishCost() { return piggyData.wishItems.reduce((s,i)=> s + (i.price*i.quantity),0); }
        function updateTotalUI() { document.getElementById('totalWishCostSpan').innerHTML = `Общая стоимость: ${getTotalWishCost().toLocaleString()} ₽`; }
        
        function updateBulkProgress() {
            const saved = piggyData.saved || 0;
            const selectedItems = getSelectedItems();
            let totalSelectedCost = 0;
            for(let item of selectedItems) {
                totalSelectedCost += item.price * item.quantity;
            }
            const need = Math.max(0, totalSelectedCost - saved);
            const percent = totalSelectedCost > 0 ? Math.min(100, (saved / totalSelectedCost) * 100) : 0;

            document.getElementById('bulkSavedDisplay').textContent = saved.toLocaleString();
            document.getElementById('bulkNeedDisplay').textContent = need.toLocaleString();
            const fill = document.getElementById('bulkProgressFill');
            fill.style.width = percent + '%';
            fill.textContent = totalSelectedCost > 0 ? Math.round(percent) + '%' : '0%';
            if (percent >= 100 && totalSelectedCost > 0) {
                fill.classList.add('ready');
            } else {
                fill.classList.remove('ready');
            }
        }

        function renderWishlist() {
            const container = document.getElementById('wishlistContainer');
            if(!piggyData.wishItems.length) { container.innerHTML = '<div class="empty-items">Список покупок пуст</div>'; updateTotalUI(); return; }
            container.innerHTML = '';
            for(let item of piggyData.wishItems) {
                const totalPrice = item.price * item.quantity;
                const canBuy = piggyData.saved >= totalPrice;
                const div = document.createElement('div');
                div.className = 'wishlist-item';
                div.innerHTML = `
                    <div class="item-info">
                        <div class="item-name">${escapeHtml(item.name)}</div>
                        <div class="item-price">${item.price.toLocaleString()} ₽ / шт.</div>
                        <div class="quantity-control">
                            <button class="qty-btn" data-id="${item.id}" data-delta="-1">-</button>
                            <span class="qty-value">${item.quantity} шт.</span>
                            <button class="qty-btn" data-id="${item.id}" data-delta="1">+</button>
                        </div>
                    </div>
                    <div class="item-progress">
                        <div>Общая стоимость: ${totalPrice.toLocaleString()} ₽</div>
                        <div class="mini-progress"><div class="mini-fill" style="width: ${Math.min(100, (piggyData.saved/totalPrice)*100)}%"></div></div>
                        <div>Нужно: ${Math.max(0,totalPrice-piggyData.saved).toLocaleString()} ₽</div>
                    </div>
                    <div class="item-actions">
                        <button class="buy-item-btn" data-id="${item.id}" ${canBuy ? '' : 'disabled'} style="${canBuy ? '' : 'opacity:0.5'}">Купить</button>
                        <button class="del-item-btn" data-id="${item.id}">Удалить</button>
                    </div>
                `;
                container.appendChild(div);
            }
            document.querySelectorAll('.qty-btn').forEach(btn => btn.addEventListener('click', (e) => { let id=parseInt(btn.dataset.id), delta=parseInt(btn.dataset.delta); changeQuantity(id,delta); }));
            document.querySelectorAll('.buy-item-btn').forEach(btn => btn.addEventListener('click', (e) => buySingleItem(parseInt(btn.dataset.id))));
            document.querySelectorAll('.del-item-btn').forEach(btn => btn.addEventListener('click', (e) => deleteWishItem(parseInt(btn.dataset.id))));
            updateTotalUI();
            renderBulkList();
            updateBulkProgress();
        }
        
        function renderBulkList() {
            const container = document.getElementById('bulkListContainer');
            const panel = document.getElementById('bulkSelectPanel');
            if(!container) return;
            if(!piggyData.wishItems.length) {
                container.innerHTML = '<div class="empty-items">Список покупок пуст. Добавьте предметы на вкладке "Основное".</div>';
                if(panel) panel.style.display = 'none';
                updateBulkProgress();
                return;
            }
            if(panel) panel.style.display = 'flex';
            container.innerHTML = '';
            piggyData.wishItems.forEach(item => {
                const totalPrice = item.price * item.quantity;
                const canBuy = piggyData.saved >= totalPrice;
                const div = document.createElement('div');
                div.className = 'bulk-item';
                div.setAttribute('data-id', item.id);
                div.innerHTML = `
                    <input type="checkbox" class="bulk-checkbox" data-id="${item.id}" id="chk_${item.id}">
                    <div class="bulk-item-info">
                        <div class="bulk-item-name">${escapeHtml(item.name)}</div>
                        <div class="bulk-item-details">${item.quantity} шт × ${item.price.toLocaleString()} ₽</div>
                    </div>
                    <div class="bulk-item-cost">${totalPrice.toLocaleString()} ₽</div>
                    <div class="bulk-status ${canBuy ? 'ok' : 'need'}">${canBuy ? 'доступно' : `не хватает ${(totalPrice - piggyData.saved).toLocaleString()}₽`}</div>
                `;
                container.appendChild(div);
            });
            document.querySelectorAll('.bulk-checkbox').forEach(cb => {
                cb.addEventListener('change', () => { updateBulkButtonState(); updateBulkProgress(); });
            });
            updateBulkButtonState();
            updateBulkProgress();
        }
        
        function updateBulkButtonState() { /* визуально */ }
        
        function getSelectedItems() {
            const checkboxes = document.querySelectorAll('.bulk-checkbox:checked');
            const selectedIds = Array.from(checkboxes).map(cb => parseInt(cb.dataset.id));
            return piggyData.wishItems.filter(item => selectedIds.includes(item.id));
        }
        
        function bulkBuySelected() {
            const selected = getSelectedItems();
            if(selected.length === 0) return alert('Выберите хотя бы один товар для покупки');
            let totalCost = 0;
            let boughtItems = [];
            let remainingItems = [...piggyData.wishItems];
            for(let item of selected) {
                const cost = item.price * item.quantity;
                if(piggyData.saved >= totalCost + cost) {
                    totalCost += cost;
                    boughtItems.push(item);
                } else {
                    alert(`Не хватает средств для "${item.name}" (нужно ${cost.toLocaleString()} ₽). Пополните копилку или выберите меньше товаров.`);
                    return;
                }
            }
            if(totalCost === 0) return alert('Нет доступных для покупки выбранных товаров');
            piggyData.saved -= totalCost;
            for(let bought of boughtItems) {
                addHistory('buy_item', bought.price * bought.quantity, `${bought.name} x${bought.quantity} (массовая покупка)`);
                remainingItems = remainingItems.filter(i => i.id !== bought.id);
            }
            piggyData.wishItems = remainingItems;
            saveData();
            updateDisplay();
            renderWishlist();
            renderBulkList();
            updateBulkProgress();
            alert(`Куплено ${boughtItems.length} товаров на сумму ${totalCost.toLocaleString()} ₽`);
            if(piggyData.saved >= piggyData.goalAmount) showAchievementModal();
        }
        
        function changeQuantity(id, delta) {
            const idx = piggyData.wishItems.findIndex(i=>i.id===id);
            if(idx===-1) return;
            let newQ = piggyData.wishItems[idx].quantity+delta;
            if(newQ<1) return;
            piggyData.wishItems[idx].quantity = newQ;
            saveData();
            renderWishlist();
        }
        function addWishItem() {
            let name = document.getElementById('itemName').value.trim();
            let price = parseFloat(document.getElementById('itemPrice').value);
            if(!name) return alert('Введите название');
            if(isNaN(price)||price<=0) price=1000;
            piggyData.wishItems.push({ id: nextItemId++, name, price, quantity:1 });
            saveData();
            renderWishlist();
            document.getElementById('itemName').value='';
            document.getElementById('itemPrice').value='';
            addHistory('add',0,`добавлен предмет: ${name}`);
        }
        function deleteWishItem(id) { piggyData.wishItems = piggyData.wishItems.filter(i=>i.id!==id); saveData(); renderWishlist(); addHistory('withdraw',0,'удалён предмет'); }
        function buySingleItem(id) {
            const item = piggyData.wishItems.find(i=>i.id===id);
            if(!item) return;
            const cost = item.price*item.quantity;
            if(piggyData.saved<cost) return alert(`Не хватает: ${cost.toLocaleString()} ₽`);
            piggyData.saved -= cost;
            addHistory('buy_item', cost, `${item.name} x${item.quantity}`);
            piggyData.wishItems = piggyData.wishItems.filter(i=>i.id!==id);
            saveData();
            updateDisplay();
            renderWishlist();
            if(piggyData.saved >= piggyData.goalAmount) showAchievementModal();
        }
        function setGoal() {
            let text = document.getElementById('goalText').value;
            let amt = parseFloat(document.getElementById('goalAmount').value);
            if(text.trim()) piggyData.goalText = text.trim();
            if(!isNaN(amt) && amt>0) piggyData.goalAmount = amt;
            saveData();
            updateDisplay();
            addHistory('goal', piggyData.goalAmount, piggyData.goalText||'цель');
            if(piggyData.saved >= piggyData.goalAmount) showAchievementModal();
        }
        function addMoney() {
            let amt = parseFloat(document.getElementById('amount').value);
            if(isNaN(amt)||amt<=0) return alert('Сумма >0');
            let before = piggyData.saved;
            piggyData.saved += amt;
            saveData();
            updateDisplay();
            addHistory('add', amt);
            document.getElementById('amount').value='';
            renderWishlist();
            if(before < piggyData.goalAmount && piggyData.saved >= piggyData.goalAmount) showAchievementModal();
        }
        function withdrawMoney() {
            let amt = parseFloat(document.getElementById('amount').value);
            if(isNaN(amt)||amt<=0) return alert('Введите сумму');
            if(amt > piggyData.saved) return alert('Недостаточно');
            piggyData.saved -= amt;
            saveData();
            updateDisplay();
            addHistory('withdraw', amt);
            document.getElementById('amount').value='';
            renderWishlist();
        }
        
        function openResetModal() {
            const modal = document.createElement('div');
            modal.className = 'reset-modal';
            modal.id = 'resetModal';
            modal.innerHTML = `
                <div class="reset-panel">
                    <h3>Сброс настроек</h3>
                    <p style="opacity:0.7; margin-bottom:16px; text-align:center;">Выберите, что именно хотите сбросить:</p>
                    <label><input type="checkbox" id="resetGoal" checked> Финансовую цель</label>
                    <label><input type="checkbox" id="resetSaved" checked> Накопления</label>
                    <label><input type="checkbox" id="resetHistory" checked> Историю операций</label>
                    <label><input type="checkbox" id="resetWishlist" checked> Список покупок</label>
                    <label><input type="checkbox" id="resetTheme" checked> Тему оформления (к стандартной)</label>
                    <div class="reset-buttons">
                        <button class="btn-cancel" onclick="closeResetModal()">Отмена</button>
                        <button class="btn-confirm" onclick="confirmReset()">Сбросить</button>
                    </div>
                </div>
            `;
            document.body.appendChild(modal);
            modal.addEventListener('click', (e) => {
                if (e.target === modal) closeResetModal();
            });
        }
        function closeResetModal() {
            const modal = document.getElementById('resetModal');
            if (modal) modal.remove();
        }
        function confirmReset() {
            const resetGoal = document.getElementById('resetGoal').checked;
            const resetSaved = document.getElementById('resetSaved').checked;
            const resetHistory = document.getElementById('resetHistory').checked;
            const resetWishlist = document.getElementById('resetWishlist').checked;
            const resetTheme = document.getElementById('resetTheme').checked;

            if (resetGoal) {
                piggyData.goalText = '';
                piggyData.goalAmount = 100000;
                document.getElementById('goalText').value = '';
                document.getElementById('goalAmount').value = 100000;
            }
            if (resetSaved) {
                piggyData.saved = 0;
            }
            if (resetHistory) {
                piggyData.history = [];
            }
            if (resetWishlist) {
                piggyData.wishItems = [];
                nextItemId = 1;
            }
            if (resetTheme) {
                localStorage.removeItem('piggyTheme');
                localStorage.removeItem('customThemeData');
                setTheme('marlboro');
            }

            saveData();
            updateDisplay();
            renderWishlist();
            closeResetModal();
            alert('Сброс выполнен!');
        }

        function showAchievementModal() {
            if(document.querySelector('.achievement-modal')) return;
            const modal = document.createElement('div');
            modal.className = 'achievement-modal';
            modal.style.cssText = 'position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.7); backdrop-filter:blur(8px); display:flex; align-items:center; justify-content:center; z-index:2000;';
            modal.innerHTML = `<div style="background:white; border-radius:48px; padding:32px; text-align:center; max-width:380px;"><div style="font-size:48px;">🏆</div><h2>Цель достигнута!</h2><p>${piggyData.goalText||'Цель'} — ${piggyData.goalAmount.toLocaleString()} ₽<br>Накоплено: ${piggyData.saved.toLocaleString()} ₽</p><button id="closeModalBtn" style="padding:12px 24px; border-radius:40px; background:#b22222; color:white; border:none;">Продолжить</button></div>`;
            document.body.appendChild(modal);
            document.getElementById('closeModalBtn').onclick = () => modal.remove();
        }
        function escapeHtml(str) { return str.replace(/[&<>]/g, function(m){ if(m==='&') return '&amp;'; if(m==='<') return '&lt;'; if(m==='>') return '&gt;'; return m;}); }
        
        function stopAllEffects() {
            if(sakuraInterval) { clearInterval(sakuraInterval); sakuraInterval = null; }
            if(customParticleInterval) { clearInterval(customParticleInterval); customParticleInterval = null; }
            document.querySelectorAll('.sakura-petal, .custom-particle').forEach(el => el.remove());
            const customStyle = document.getElementById('customThemeStyle');
            if(customStyle) customStyle.remove();
            document.body.classList.remove('theme-geometric', 'theme-waves', 'theme-dots', 'theme-stripes', 'theme-triangles');
            document.body.classList.remove('theme-custom');
            document.body.style.background = '';
            const container = document.querySelector('.container');
            container.style.background = '';
            container.style.color = '';
        }
        function startSakuraEffect() {
            if(sakuraInterval) clearInterval(sakuraInterval);
            function createPetal() {
                if(!document.body.classList.contains('theme-sakura')) return;
                const petal = document.createElement('div');
                petal.classList.add('sakura-petal');
                const size = 10 + Math.random() * 12;
                petal.style.width = size + 'px';
                petal.style.height = size + 'px';
                petal.style.left = Math.random() * 100 + '%';
                petal.style.animationDuration = 4 + Math.random() * 6 + 's';
                petal.style.opacity = 0.5 + Math.random() * 0.4;
                const hue = 340 + Math.random() * 15;
                petal.style.background = `hsl(${hue}, 80%, 75%)`;
                document.body.appendChild(petal);
                setTimeout(() => { if(petal && petal.remove) petal.remove(); }, 9000);
            }
            sakuraInterval = setInterval(createPetal, 350);
        }
        function setTheme(themeName) {
            stopAllEffects();
            // Сначала убираем все классы тем
            const allThemes = ['light', 'dark', 'sunset', 'ocean', 'forest', 'cosmic', 'desert', 'marlboro', 'sakura', 
                              'midnight', 'aurora', 'lavender', 'cherry', 'geometric', 'waves', 'dots', 'stripes', 'triangles', 'custom'];
            allThemes.forEach(t => document.body.classList.remove(`theme-${t}`));
            
            if(themeName !== 'custom') {
                document.body.classList.add(`theme-${themeName}`);
                if(themeName === 'sakura') startSakuraEffect();
            } else {
                document.body.classList.add('theme-custom');
            }
            localStorage.setItem('piggyTheme', themeName);
        }
        
        function openThemeEditor() {
            const modal = document.createElement('div');
            modal.className = 'theme-editor-modal';
            modal.innerHTML = `
                <div class="editor-panel">
                    <h3>Создать свою тему</h3>
                    <label>Фоновое изображение (URL)</label>
                    <input type="text" id="customBgImg" placeholder="https://example.com/background.jpg">
                    <label>Цвет фона</label>
                    <input type="color" id="customBgColor" value="#1a1a2e">
                    <label>Цвет контейнера</label>
                    <input type="color" id="customContainerColor" value="#16213e">
                    <label>Цвет кнопок</label>
                    <input type="color" id="customBtnColor" value="#e94560">
                    <label>Цвет текста</label>
                    <input type="color" id="customTextColor" value="#f1f5f9">
                    <label>Цвет прогресс-бара (основной)</label>
                    <input type="color" id="customProgressColor" value="#8b5cf6">
                    <label>Цвет прогресс-бара (массовые)</label>
                    <input type="color" id="customBulkColor" value="#ec4899">
                    <label>Геометрический эффект</label>
                    <select id="customGeoEffect">
                        <option value="none">Без эффекта</option>
                        <option value="geometric">Геометрия</option>
                        <option value="waves">Волны</option>
                        <option value="dots">Точки</option>
                        <option value="stripes">Полосы</option>
                        <option value="triangles">Треугольники</option>
                    </select>
                    <div class="effect-checkbox">
                        <input type="checkbox" id="enableParticles"> <label style="display:inline;">Эффект частиц</label>
                    </div>
                    <label>Доп. CSS эффект</label>
                    <textarea id="customCssEffect" rows="2"></textarea>
                    <div class="editor-buttons">
                        <button id="applyCustomThemeBtn">Применить</button>
                        <button id="closeEditorBtn">Отмена</button>
                    </div>
                </div>
            `;
            document.body.appendChild(modal);
            modal.querySelector('#applyCustomThemeBtn').onclick = () => {
                const data = {
                    bgImg: modal.querySelector('#customBgImg').value,
                    bgColor: modal.querySelector('#customBgColor').value,
                    containerColor: modal.querySelector('#customContainerColor').value,
                    btnColor: modal.querySelector('#customBtnColor').value,
                    textColor: modal.querySelector('#customTextColor').value,
                    progressColor: modal.querySelector('#customProgressColor').value,
                    bulkColor: modal.querySelector('#customBulkColor').value,
                    geoEffect: modal.querySelector('#customGeoEffect').value,
                    cssEffect: modal.querySelector('#customCssEffect').value,
                    enableParticles: modal.querySelector('#enableParticles').checked
                };
                stopAllEffects();
                const allThemes = ['light', 'dark', 'sunset', 'ocean', 'forest', 'cosmic', 'desert', 'marlboro', 'sakura', 
                                  'midnight', 'aurora', 'lavender', 'cherry', 'geometric', 'waves', 'dots', 'stripes', 'triangles'];
                allThemes.forEach(t => document.body.classList.remove(`theme-${t}`));
                document.body.classList.add('theme-custom');
                if(data.bgImg) document.body.style.background = `url('${data.bgImg}') center/cover fixed`;
                else document.body.style.background = data.bgColor;
                const container = document.querySelector('.container');
                container.style.background = data.containerColor;
                container.style.color = data.textColor;
                
                if(data.geoEffect !== 'none') {
                    document.body.classList.add(`theme-${data.geoEffect}`);
                }
                
                document.documentElement.style.setProperty('--custom-progress', `linear-gradient(90deg, ${data.progressColor}, ${adjustColor(data.progressColor, 20)}, ${adjustColor(data.progressColor, 40)})`);
                document.documentElement.style.setProperty('--custom-progress-complete', `linear-gradient(90deg, #22c55e, #16a34a, #15803d)`);
                document.documentElement.style.setProperty('--custom-bulk-progress', `linear-gradient(90deg, ${data.bulkColor}, ${adjustColor(data.bulkColor, 30)}, ${adjustColor(data.bulkColor, 50)})`);
                document.documentElement.style.setProperty('--custom-bulk-ready', `linear-gradient(90deg, #22c55e, #16a34a, #15803d)`);
                
                let styleTag = document.getElementById('customThemeStyle');
                if(!styleTag) { styleTag = document.createElement('style'); styleTag.id = 'customThemeStyle'; document.head.appendChild(styleTag); }
                styleTag.innerHTML = `
                    body.theme-custom .container { background: ${data.containerColor} !important; color: ${data.textColor} !important; }
                    body.theme-custom button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn):not(.tab-btn) { background: ${data.btnColor} !important; color: white; }
                    body.theme-custom .container { ${data.cssEffect} }
                `;
                if(data.enableParticles && !customParticleInterval) customParticleInterval = setInterval(() => { if(document.body.classList.contains('theme-custom')) { const p = document.createElement('div'); p.className = 'custom-particle'; p.style.cssText = `width:6px;height:6px;left:${Math.random()*100}%;animation-duration:${3+Math.random()*5}s;background:radial-gradient(circle, ${data.btnColor}, transparent)`; document.body.appendChild(p); setTimeout(()=>p.remove(),5000); } }, 400);
                localStorage.setItem('piggyTheme', 'custom');
                localStorage.setItem('customThemeData', JSON.stringify(data));
                modal.remove();
            };
            modal.querySelector('#closeEditorBtn').onclick = () => modal.remove();
        }
        
        function adjustColor(hex, percent) {
            let r = parseInt(hex.slice(1,3), 16);
            let g = parseInt(hex.slice(3,5), 16);
            let b = parseInt(hex.slice(5,7), 16);
            r = Math.min(255, Math.max(0, r + percent));
            g = Math.min(255, Math.max(0, g + percent));
            b = Math.min(255, Math.max(0, b + percent));
            return `#${r.toString(16).padStart(2, '0')}${g.toString(16).padStart(2, '0')}${b.toString(16).padStart(2, '0')}`;
        }
        
        function loadTheme() {
            let saved = localStorage.getItem('piggyTheme');
            if(saved === 'custom') {
                const customData = localStorage.getItem('customThemeData');
                if(customData) {
                    const data = JSON.parse(customData);
                    document.documentElement.style.setProperty('--custom-progress', `linear-gradient(90deg, ${data.progressColor}, ${adjustColor(data.progressColor, 20)}, ${adjustColor(data.progressColor, 40)})`);
                    document.documentElement.style.setProperty('--custom-progress-complete', `linear-gradient(90deg, #22c55e, #16a34a, #15803d)`);
                    document.documentElement.style.setProperty('--custom-bulk-progress', `linear-gradient(90deg, ${data.bulkColor}, ${adjustColor(data.bulkColor, 30)}, ${adjustColor(data.bulkColor, 50)})`);
                    document.documentElement.style.setProperty('--custom-bulk-ready', `linear-gradient(90deg, #22c55e, #16a34a, #15803d)`);
                    if(data.geoEffect && data.geoEffect !== 'none') {
                        document.body.classList.add(`theme-${data.geoEffect}`);
                    }
                }
                setTheme('custom');
            } else if(saved && ['light','dark','sunset','ocean','forest','cosmic','desert','marlboro','sakura',
                               'midnight','aurora','lavender','cherry','geometric','waves','dots','stripes','triangles'].includes(saved)) {
                setTheme(saved);
            } else {
                setTheme('marlboro');
            }
        }
        
        function toggleRGB() { 
            document.body.classList.toggle('rgb-mode'); 
            const btn = document.getElementById('rgbToggleBtn'); 
            if(document.body.classList.contains('rgb-mode')) {
                btn.textContent = '🔴 RGB вкл';
                btn.classList.add('active');
            } else {
                btn.textContent = '🌈 RGB режим';
                btn.classList.remove('active');
            }
        }
        
        document.addEventListener('DOMContentLoaded', () => {
            loadData(); loadTheme();
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
                    btn.classList.add('active');
                    document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active-tab'));
                    document.getElementById(`tab-${btn.dataset.tab}`).classList.add('active-tab');
                    if(btn.dataset.tab === 'bulk') { renderBulkList(); updateBulkProgress(); }
                });
            });
            const menuBtn = document.getElementById('themeMenuBtn'), menu = document.getElementById('themeMenu');
            menuBtn.addEventListener('click', (e) => { e.stopPropagation(); menu.classList.toggle('hidden'); });
            document.addEventListener('click', (e) => { if(!menu.contains(e.target) && e.target !== menuBtn) menu.classList.add('hidden'); });
            document.querySelectorAll('#themeMenu button[data-theme]').forEach(btn => btn.addEventListener('click', () => { setTheme(btn.dataset.theme); menu.classList.add('hidden'); }));
            document.getElementById('createCustomThemeBtn').addEventListener('click', () => { menu.classList.add('hidden'); openThemeEditor(); });
            document.getElementById('rgbToggleBtn').addEventListener('click', toggleRGB);
            document.getElementById('bulkBuySelectedBtn')?.addEventListener('click', bulkBuySelected);
            document.getElementById('selectAllBtn')?.addEventListener('click', () => { document.querySelectorAll('.bulk-checkbox').forEach(cb => { cb.checked = true; }); updateBulkProgress(); });
            document.getElementById('deselectAllBtn')?.addEventListener('click', () => { document.querySelectorAll('.bulk-checkbox').forEach(cb => { cb.checked = false; }); updateBulkProgress(); });
            document.getElementById('amount').addEventListener('keypress', (e) => { if(e.key === 'Enter') addMoney(); });
            updateBulkProgress();
            
            window.setGoal = setGoal;
            window.addMoney = addMoney;
            window.withdrawMoney = withdrawMoney;
            window.resetAllData = openResetModal;
            window.addWishItem = addWishItem;
            window.openResetModal = openResetModal;
            window.closeResetModal = closeResetModal;
            window.confirmReset = confirmReset;
        });
    </script>
</body>
</html>
