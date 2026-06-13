<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Копилка — Своя тема | Редактор | Сакура</title>
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

        /* RGB анимация */
        @keyframes rgbBorder {
            0% { box-shadow: 0 0 8px rgba(255,0,0,0.6), 0 0 15px rgba(255,0,0,0.4); border-color: #ff0000; }
            25% { box-shadow: 0 0 8px rgba(0,255,0,0.6), 0 0 15px rgba(0,255,0,0.4); border-color: #00ff00; }
            50% { box-shadow: 0 0 8px rgba(0,0,255,0.6), 0 0 15px rgba(0,0,255,0.4); border-color: #0000ff; }
            75% { box-shadow: 0 0 8px rgba(255,255,0,0.6), 0 0 15px rgba(255,255,0,0.4); border-color: #ffff00; }
            100% { box-shadow: 0 0 8px rgba(255,0,255,0.6), 0 0 15px rgba(255,0,255,0.4); border-color: #ff00ff; }
        }
        body.rgb-mode .container {
            animation: rgbBorder 1.8s infinite alternate;
            border-radius: 32px;
        }

        .container {
            max-width: 780px;
            width: 100%;
            border-radius: 32px;
            padding: 28px 24px;
            transition: background 0.3s ease, box-shadow 0.3s, color 0.2s;
            position: relative;
            z-index: 10;
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

        /* Меню тем */
        .theme-dropdown { position: relative; display: inline-block; }
        .theme-main-btn { background: #3b3b5c; border: none; padding: 10px 20px; border-radius: 40px; font-weight: bold; cursor: pointer; font-size: 14px; color: white; transition: 0.2s; }
        .theme-menu {
            position: absolute; top: 50px; right: 0; background: #1e1e2f; border-radius: 24px; padding: 12px; display: flex; flex-direction: column; gap: 8px;
            min-width: 180px; z-index: 200; box-shadow: 0 10px 25px rgba(0,0,0,0.2); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.2);
            max-height: 450px;
            overflow-y: auto;
        }
        .theme-menu button { background: rgba(255,255,255,0.1); border: none; padding: 8px 12px; border-radius: 30px; color: white; font-weight: 500; cursor: pointer; text-align: left; transition: 0.2s; }
        .theme-menu button:hover { background: rgba(255,255,255,0.3); transform: scale(0.98); }
        .hidden { display: none; }
        .rgb-toggle { background: linear-gradient(45deg, red, blue, green); color: white; border: none; padding: 8px 16px; border-radius: 40px; font-weight: bold; cursor: pointer; font-size: 13px; }

        /* Общие стили */
        .goal-section { margin-bottom: 24px; }
        label { display: block; margin-bottom: 8px; font-weight: 600; font-size: 14px; }
        .goal-input-group { display: flex; gap: 12px; flex-wrap: wrap; }
        input, button { padding: 12px 16px; border-radius: 28px; font-size: 15px; font-family: inherit; transition: var(--transition); }
        button { cursor: pointer; font-weight: 600; border: none; }
        button:active { transform: scale(0.97); }
        .stats { border-radius: 24px; padding: 20px; margin-bottom: 24px; }
        .stat-value { font-size: 28px; font-weight: 800; }
        .progress-bar { width: 100%; height: 32px; background: rgba(0, 0, 0, 0.12); border-radius: 40px; overflow: hidden; margin: 16px 0 4px; }
        .progress-fill { height: 100%; border-radius: 40px; transition: width 0.35s; display: flex; align-items: center; justify-content: center; color: white; font-weight: bold; font-size: 13px; }
        .operations { display: flex; gap: 12px; margin-bottom: 28px; flex-wrap: wrap; }
        .withdraw-btn { background: #ef4444 !important; }
        .wishlist-section { margin: 20px 0 24px; }
        .add-item-form { display: flex; flex-wrap: wrap; gap: 12px; margin-bottom: 18px; }
        .bulk-actions { display: flex; gap: 12px; margin-bottom: 16px; }
        .bulk-buy-btn { background: #f59e0b !important; flex: 1; }
        .items-grid { max-height: 320px; overflow-y: auto; display: flex; flex-direction: column; gap: 12px; }
        .wishlist-item { display: flex; justify-content: space-between; flex-wrap: wrap; padding: 14px 16px; border-radius: 24px; gap: 10px; }
        .quantity-control { display: flex; gap: 8px; margin-top: 6px; align-items: center; }
        .qty-btn { background: #cbd5e1; padding: 4px 10px; border-radius: 30px; font-weight: bold; }
        .mini-progress { height: 12px; background: rgba(0,0,0,0.1); border-radius: 20px; overflow: hidden; margin: 6px 0; }
        .mini-fill { height: 100%; width: 0%; background: #22c55e; }
        .item-actions { display: flex; gap: 8px; }
        .buy-item-btn { background: #22c55e; padding: 6px 14px; font-size: 12px; }
        .del-item-btn { background: #ef4444; padding: 6px 12px; }
        .history-list { max-height: 220px; overflow-y: auto; border-radius: 20px; margin-bottom: 14px; }
        .history-item { padding: 12px 16px; margin-bottom: 8px; border-radius: 18px; display: flex; justify-content: space-between; }
        .reset-btn { width: 100%; margin-top: 6px; background: #94a3b8 !important; }
        .empty-items, .empty-history-message { text-align: center; padding: 24px; font-style: italic; opacity: 0.7; }
        .total-wish-cost { font-weight: 700; padding: 6px 14px; border-radius: 40px; background: rgba(0,0,0,0.05); display: inline-block; }
        .wishlist-header { display: flex; justify-content: space-between; margin-bottom: 16px; flex-wrap: wrap; }

        /* Модальное окно редактора тем */
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
        }
        .editor-panel h3 { margin-bottom: 20px; font-size: 24px; text-align: center; }
        .editor-panel label { display: block; margin: 12px 0 6px; font-weight: 600; }
        .editor-panel input, .editor-panel textarea {
            width: 100%;
            padding: 10px 14px;
            border-radius: 28px;
            border: none;
            background: #2d2a55;
            color: white;
            font-family: monospace;
        }
        .editor-panel textarea { resize: vertical; font-family: monospace; }
        .color-row { display: flex; gap: 12px; flex-wrap: wrap; }
        .color-row input { flex: 1; }
        .editor-buttons { display: flex; gap: 12px; margin-top: 24px; }
        .editor-buttons button { flex: 1; background: #7c3aed; color: white; }
        .effect-checkbox { display: flex; align-items: center; gap: 8px; margin: 10px 0; }
        
        /* Рисованный лепесток сакуры (вертикальное падение) */
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
            0% {
                transform: translateY(-10vh) rotate(0deg);
                opacity: 0.9;
            }
            100% {
                transform: translateY(110vh) rotate(360deg);
                opacity: 0;
            }
        }
        
        /* Кастомные частицы для своей темы */
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

        /* ========== СТАНДАРТНЫЕ ТЕМЫ (ВСЕ РАБОТАЮТ) ========== */
        body.theme-light { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        body.theme-light .container { background: #ffffff; box-shadow: 0 20px 45px rgba(0,0,0,0.25); color: #1e293b; }
        body.theme-light button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn) { background: #667eea; color: white; }
        body.theme-light .stats { background: #f1f5f9; }
        
        body.theme-dark { background: linear-gradient(135deg, #0f172a 0%, #1e1b2e 100%); }
        body.theme-dark .container { background: #1e293b; box-shadow: 0 20px 45px rgba(0,0,0,0.5); color: #f1f5f9; }
        body.theme-dark button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn) { background: #7c3aed; color: white; }
        body.theme-dark .stats { background: #0f172a; }
        
        body.theme-sunset { background: linear-gradient(135deg, #fbc2eb 0%, #a6c1ee 100%); }
        body.theme-sunset .container { background: #fff5f9; color: #831843; }
        body.theme-sunset button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn) { background: #db2777; color: white; }
        body.theme-sunset .stats { background: #fdf2f8; }
        
        body.theme-ocean { background: linear-gradient(135deg, #00c6fb 0%, #005bea 100%); }
        body.theme-ocean .container { background: #eef5ff; color: #0c4a6e; }
        body.theme-ocean button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn) { background: #0284c7; color: white; }
        body.theme-ocean .stats { background: #e0f2fe; }
        
        body.theme-forest { background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%); }
        body.theme-forest .container { background: #f1f9f0; color: #14532d; }
        body.theme-forest button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn) { background: #16a34a; color: white; }
        body.theme-forest .stats { background: #dcfce7; }
        
        body.theme-cosmic { background: linear-gradient(135deg, #2b1b4e 0%, #e956a7 100%); }
        body.theme-cosmic .container { background: #1e1a3a; color: #e9d5ff; }
        body.theme-cosmic button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn) { background: #a855f7; color: white; }
        body.theme-cosmic .stats { background: #2e2359; }
        
        body.theme-desert { background: linear-gradient(135deg, #f5af19 0%, #f12711 100%); }
        body.theme-desert .container { background: #fff5e6; color: #7c2d12; }
        body.theme-desert button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn) { background: #ea580c; color: white; }
        body.theme-desert .stats { background: #ffedd5; }
        
        body.theme-marlboro { background: linear-gradient(135deg, #8b0000 0%, #cc0000 100%); }
        body.theme-marlboro .container { background: #fffaf0; border: 1px solid #b22222; color: #4a2c2c; }
        body.theme-marlboro button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn) { background: #b22222; color: white; }
        body.theme-marlboro .stats { background: #fef3e2; border-left: 6px solid #b22222; }
        
        body.theme-sakura { background: radial-gradient(circle at 10% 20%, #fff0f5, #ffe0e8); }
        body.theme-sakura .container { background: rgba(255, 245, 250, 0.94); backdrop-filter: blur(3px); border: 1px solid #ffb7c5; color: #b34562; }
        body.theme-sakura button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn) { background: #e66a8c; color: white; }
        body.theme-sakura .stats { background: #ffeef4; border-left: 5px solid #f28b9e; }
        
        /* Своя тема (динамическая) */
        body.theme-custom .container { transition: all 0.2s; }
    </style>
</head>
<body class="theme-marlboro">
    <div class="container">
        <div class="header">
            <h1>КОПИЛКА</h1>
            <div style="display: flex; gap: 10px;">
                <button id="rgbToggleBtn" class="rgb-toggle">🌈 RGB режим</button>
                <div class="theme-dropdown">
                    <button id="themeMenuBtn" class="theme-main-btn">🎨 Темы ▼</button>
                    <div id="themeMenu" class="theme-menu hidden">
                        <button data-theme="light">Светлая</button>
                        <button data-theme="dark">Тёмная</button>
                        <button data-theme="sunset">Закат</button>
                        <button data-theme="ocean">Океан</button>
                        <button data-theme="forest">Лес</button>
                        <button data-theme="cosmic">Космос</button>
                        <button data-theme="desert">Пустыня</button>
                        <button data-theme="marlboro">Marlboro</button>
                        <button data-theme="sakura">🌸 Сакура</button>
                        <button id="createCustomThemeBtn" style="background: #f59e0b; color:#1e1a2f;">✨ Создать свою тему</button>
                    </div>
                </div>
            </div>
        </div>

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
            <div class="bulk-actions">
                <button class="bulk-buy-btn" id="bulkBuyBtn">МАССОВЫЕ ПОКУПКИ (купить всё возможное)</button>
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
            <button class="reset-btn" onclick="resetAllData()">Сбросить всё</button>
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
        }
        function saveData() { localStorage.setItem('piggyBankApp', JSON.stringify(piggyData)); }
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
            fill.innerHTML = `${Math.round(percent)}%`;
            renderHistory();
        }
        function getTotalWishCost() { return piggyData.wishItems.reduce((s,i)=> s + (i.price*i.quantity),0); }
        function updateTotalUI() { document.getElementById('totalWishCostSpan').innerHTML = `Общая стоимость: ${getTotalWishCost().toLocaleString()} ₽`; }
        
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
        function bulkBuyAll() {
            if(!piggyData.wishItems.length) return alert('Список пуст');
            let bought=false, spent=0, remaining=[];
            for(let item of piggyData.wishItems) {
                let cost = item.price*item.quantity;
                if(piggyData.saved >= cost) { piggyData.saved -= cost; spent+=cost; bought=true; addHistory('buy_item', cost, `${item.name} x${item.quantity} (массовая)`); }
                else remaining.push(item);
            }
            if(!bought) return alert('Не хватает на любую покупку');
            piggyData.wishItems = remaining;
            saveData();
            updateDisplay();
            renderWishlist();
            alert(`Массовая покупка: потрачено ${spent.toLocaleString()} ₽`);
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
        function resetAllData() {
            if(confirm('Сбросить всё?')){
                piggyData = { goalText:'', goalAmount:100000, saved:0, history:[], wishItems:[] };
                nextItemId=1;
                saveData();
                updateDisplay();
                renderWishlist();
                document.getElementById('goalText').value='';
                document.getElementById('goalAmount').value=100000;
            }
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
        
        // ========== УПРАВЛЕНИЕ ТЕМАМИ (ИСПРАВЛЕНО) ==========
        function stopAllEffects() {
            if(sakuraInterval) { clearInterval(sakuraInterval); sakuraInterval = null; }
            if(customParticleInterval) { clearInterval(customParticleInterval); customParticleInterval = null; }
            document.querySelectorAll('.sakura-petal, .custom-particle').forEach(el => el.remove());
            const customStyle = document.getElementById('customThemeStyle');
            if(customStyle) customStyle.remove();
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
            const themes = ['light', 'dark', 'sunset', 'ocean', 'forest', 'cosmic', 'desert', 'marlboro', 'sakura'];
            themes.forEach(t => document.body.classList.remove(`theme-${t}`));
            if(themeName !== 'custom') {
                document.body.classList.add(`theme-${themeName}`);
                if(themeName === 'sakura') startSakuraEffect();
            }
            localStorage.setItem('piggyTheme', themeName);
        }
        
        // Редактор кастомной темы
        function openThemeEditor() {
            const modal = document.createElement('div');
            modal.className = 'theme-editor-modal';
            modal.innerHTML = `
                <div class="editor-panel">
                    <h3>🎨 Создать свою тему</h3>
                    <label>Фоновое изображение (URL)</label>
                    <input type="text" id="customBgImg" placeholder="https://example.com/background.jpg">
                    <label>Цвет фона (если нет картинки)</label>
                    <input type="color" id="customBgColor" value="#1a1a2e">
                    <label>Цвет контейнера</label>
                    <input type="color" id="customContainerColor" value="#16213e">
                    <label>Цвет кнопок</label>
                    <input type="color" id="customBtnColor" value="#e94560">
                    <label>Цвет текста заголовков</label>
                    <input type="color" id="customTextColor" value="#f1f5f9">
                    <div class="effect-checkbox">
                        <input type="checkbox" id="enableParticles"> <label style="display:inline;">✨ Эффект частиц (парящие точки)</label>
                    </div>
                    <label>Дополнительный CSS-эффект (тень, градиент и т.д.)</label>
                    <textarea id="customCssEffect" rows="2" placeholder="box-shadow: 0 0 20px rgba(255,215,0,0.5); border: 2px solid gold;"></textarea>
                    <div class="editor-buttons">
                        <button id="applyCustomThemeBtn">Применить</button>
                        <button id="closeEditorBtn">Отмена</button>
                    </div>
                </div>
            `;
            document.body.appendChild(modal);
            
            modal.querySelector('#applyCustomThemeBtn').onclick = () => {
                const bgImg = modal.querySelector('#customBgImg').value;
                const bgColor = modal.querySelector('#customBgColor').value;
                const containerColor = modal.querySelector('#customContainerColor').value;
                const btnColor = modal.querySelector('#customBtnColor').value;
                const textColor = modal.querySelector('#customTextColor').value;
                const enableParticles = modal.querySelector('#enableParticles').checked;
                const cssEffect = modal.querySelector('#customCssEffect').value;
                
                stopAllEffects();
                const themes = ['light', 'dark', 'sunset', 'ocean', 'forest', 'cosmic', 'desert', 'marlboro', 'sakura'];
                themes.forEach(t => document.body.classList.remove(`theme-${t}`));
                document.body.classList.add('theme-custom');
                
                if(bgImg) document.body.style.background = `url('${bgImg}') center/cover fixed no-repeat`;
                else document.body.style.background = bgColor;
                
                const container = document.querySelector('.container');
                container.style.background = containerColor;
                container.style.color = textColor;
                
                let styleTag = document.getElementById('customThemeStyle');
                if(!styleTag) { styleTag = document.createElement('style'); styleTag.id = 'customThemeStyle'; document.head.appendChild(styleTag); }
                styleTag.innerHTML = `
                    body.theme-custom .container { background: ${containerColor} !important; color: ${textColor} !important; }
                    body.theme-custom button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn) { background: ${btnColor} !important; color: white; }
                    body.theme-custom .stats, body.theme-custom .wishlist-item, body.theme-custom .history-item { background: ${containerColor}cc !important; }
                    body.theme-custom .goal-text, body.theme-custom .stat-value, body.theme-custom h1 { color: ${textColor} !important; }
                    body.theme-custom .container { ${cssEffect} }
                `;
                
                if(enableParticles) {
                    if(customParticleInterval) clearInterval(customParticleInterval);
                    customParticleInterval = setInterval(() => {
                        if(document.body.classList.contains('theme-custom')) {
                            const particle = document.createElement('div');
                            particle.className = 'custom-particle';
                            const size = 4 + Math.random() * 12;
                            particle.style.width = size + 'px';
                            particle.style.height = size + 'px';
                            particle.style.left = Math.random() * 100 + '%';
                            particle.style.animationDuration = 3 + Math.random() * 5 + 's';
                            particle.style.background = `radial-gradient(circle, ${btnColor}, transparent)`;
                            document.body.appendChild(particle);
                            setTimeout(() => particle.remove(), 6000);
                        }
                    }, 400);
                }
                
                localStorage.setItem('piggyTheme', 'custom');
                localStorage.setItem('customThemeData', JSON.stringify({ bgImg, bgColor, containerColor, btnColor, textColor, cssEffect, enableParticles }));
                modal.remove();
            };
            modal.querySelector('#closeEditorBtn').onclick = () => modal.remove();
        }
        
        function loadCustomTheme() {
            const savedTheme = localStorage.getItem('piggyTheme');
            const customData = localStorage.getItem('customThemeData');
            if(savedTheme === 'custom' && customData) {
                const data = JSON.parse(customData);
                stopAllEffects();
                const themes = ['light', 'dark', 'sunset', 'ocean', 'forest', 'cosmic', 'desert', 'marlboro', 'sakura'];
                themes.forEach(t => document.body.classList.remove(`theme-${t}`));
                document.body.classList.add('theme-custom');
                if(data.bgImg) document.body.style.background = `url('${data.bgImg}') center/cover fixed`;
                else document.body.style.background = data.bgColor;
                const container = document.querySelector('.container');
                container.style.background = data.containerColor;
                container.style.color = data.textColor;
                let styleTag = document.getElementById('customThemeStyle');
                if(!styleTag) { styleTag = document.createElement('style'); styleTag.id = 'customThemeStyle'; document.head.appendChild(styleTag); }
                styleTag.innerHTML = `
                    body.theme-custom .container { background: ${data.containerColor} !important; color: ${data.textColor} !important; }
                    body.theme-custom button:not(.theme-main-btn):not(.rgb-toggle):not(.buy-item-btn):not(.del-item-btn):not(.qty-btn) { background: ${data.btnColor} !important; color: white; }
                    body.theme-custom .stats, body.theme-custom .wishlist-item, body.theme-custom .history-item { background: ${data.containerColor}cc !important; }
                    body.theme-custom .goal-text, body.theme-custom .stat-value, body.theme-custom h1 { color: ${data.textColor} !important; }
                    body.theme-custom .container { ${data.cssEffect || ''} }
                `;
                if(data.enableParticles && !customParticleInterval) {
                    customParticleInterval = setInterval(() => {
                        if(document.body.classList.contains('theme-custom')) {
                            const particle = document.createElement('div');
                            particle.className = 'custom-particle';
                            const size = 4 + Math.random() * 12;
                            particle.style.width = size + 'px';
                            particle.style.height = size + 'px';
                            particle.style.left = Math.random() * 100 + '%';
                            particle.style.animationDuration = 3 + Math.random() * 5 + 's';
                            particle.style.background = `radial-gradient(circle, ${data.btnColor}, transparent)`;
                            document.body.appendChild(particle);
                            setTimeout(() => particle.remove(), 6000);
                        }
                    }, 400);
                }
            }
        }
        
        function loadTheme() {
            let saved = localStorage.getItem('piggyTheme');
            if(saved === 'custom') {
                loadCustomTheme();
            } else if(saved && ['light','dark','sunset','ocean','forest','cosmic','desert','marlboro','sakura'].includes(saved)) {
                setTheme(saved);
            } else {
                setTheme('marlboro');
            }
        }
        
        function toggleRGB() {
            document.body.classList.toggle('rgb-mode');
            const btn = document.getElementById('rgbToggleBtn');
            if(document.body.classList.contains('rgb-mode')) btn.textContent = '🔴 RGB вкл';
            else btn.textContent = '🌈 RGB режим';
        }
        
        document.addEventListener('DOMContentLoaded', () => {
            loadData();
            loadTheme();
            const menuBtn = document.getElementById('themeMenuBtn');
            const menu = document.getElementById('themeMenu');
            menuBtn.addEventListener('click', (e) => { e.stopPropagation(); menu.classList.toggle('hidden'); });
            document.addEventListener('click', (e) => { if(!menu.contains(e.target) && e.target !== menuBtn) menu.classList.add('hidden'); });
            document.querySelectorAll('#themeMenu button[data-theme]').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const theme = btn.dataset.theme;
                    if(theme) setTheme(theme);
                    menu.classList.add('hidden');
                });
            });
            document.getElementById('createCustomThemeBtn').addEventListener('click', () => {
                menu.classList.add('hidden');
                openThemeEditor();
            });
            document.getElementById('rgbToggleBtn').addEventListener('click', toggleRGB);
            document.getElementById('bulkBuyBtn').addEventListener('click', bulkBuyAll);
            document.getElementById('amount').addEventListener('keypress', (e) => { if(e.key === 'Enter') addMoney(); });
        });
        
        window.setGoal = setGoal;
        window.addMoney = addMoney;
        window.withdrawMoney = withdrawMoney;
        window.resetAllData = resetAllData;
        window.addWishItem = addWishItem;
    </script>
</body>
</html>
