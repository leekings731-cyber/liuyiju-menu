<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover, user-scalable=no">
    <title>六一居 · 茶膳预定</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: #F5F2EB;
            font-family: 'Georgia', 'Times New Roman', 'Songti SC', '宋体', serif;
            padding-bottom: 100px;
            color: #2C2B28;
        }

        :root {
            --tea-green: #2F5D3A;
            --gold: #C9A96E;
            --dark: #3A3530;
        }

        .hero {
            background: linear-gradient(135deg, #2F5D3A 0%, #1E3A25 100%);
            padding: 48px 24px 40px;
            text-align: center;
            color: white;
            position: relative;
        }

        .hero::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--gold), var(--tea-green), var(--gold));
        }

        .logo-icon {
            font-size: 48px;
            margin-bottom: 8px;
        }

        .hero h1 {
            font-size: 28px;
            letter-spacing: 4px;
            font-weight: 500;
            margin-bottom: 8px;
        }

        .hero .sub {
            font-size: 12px;
            opacity: 0.8;
            letter-spacing: 2px;
        }

        .hero .desc {
            font-size: 14px;
            margin-top: 16px;
            opacity: 0.9;
            font-style: italic;
        }

        .admin-btn {
            position: fixed;
            bottom: 100px;
            right: 20px;
            background: rgba(0,0,0,0.5);
            width: 44px;
            height: 44px;
            border-radius: 22px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 20px;
            cursor: pointer;
            z-index: 200;
            backdrop-filter: blur(4px);
        }

        .admin-modal {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 85%;
            max-width: 340px;
            background: white;
            border-radius: 28px;
            z-index: 500;
            display: none;
            padding: 24px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
        }

        .admin-modal.show {
            display: block;
        }

        .admin-modal h4 {
            font-size: 18px;
            margin-bottom: 20px;
            color: var(--tea-green);
        }

        .admin-modal input, .admin-modal select {
            width: 100%;
            padding: 12px;
            margin-bottom: 16px;
            border: 1px solid #E0D9CE;
            border-radius: 12px;
            font-size: 14px;
            font-family: inherit;
        }

        .admin-modal button {
            width: 100%;
            padding: 12px;
            background: var(--tea-green);
            color: white;
            border: none;
            border-radius: 30px;
            font-size: 16px;
            margin-top: 8px;
        }

        .current-info {
            position: fixed;
            top: 100px;
            right: 12px;
            background: rgba(47,93,58,0.9);
            backdrop-filter: blur(8px);
            padding: 8px 14px;
            border-radius: 30px;
            font-size: 12px;
            color: var(--gold);
            z-index: 100;
            pointer-events: none;
            font-family: monospace;
        }

        .category-nav {
            background: white;
            padding: 12px 16px;
            display: flex;
            gap: 8px;
            overflow-x: auto;
            position: sticky;
            top: 0;
            z-index: 50;
            box-shadow: 0 2px 12px rgba(0,0,0,0.05);
            white-space: nowrap;
        }

        .category-nav::-webkit-scrollbar {
            display: none;
        }

        .cat-item {
            padding: 8px 20px;
            border-radius: 40px;
            font-size: 14px;
            background: #F5F2EB;
            color: #5A5548;
            transition: all 0.2s;
            cursor: pointer;
            font-family: inherit;
        }

        .cat-item.active {
            background: var(--tea-green);
            color: white;
        }

        .menu-container {
            padding: 20px 16px;
        }

        .category-section {
            margin-bottom: 32px;
        }

        .category-title {
            font-size: 20px;
            font-weight: 500;
            color: var(--tea-green);
            padding-left: 8px;
            border-left: 3px solid var(--gold);
            margin-bottom: 20px;
            letter-spacing: 1px;
        }

        .dish-card {
            background: white;
            border-radius: 20px;
            margin-bottom: 20px;
            overflow: hidden;
            box-shadow: 0 4px 16px rgba(0,0,0,0.05);
            transition: transform 0.25s;
        }

        .dish-card:active {
            transform: scale(0.99);
        }

        .img-placeholder {
            width: 100%;
            height: 140px;
            background: linear-gradient(135deg, #E8E0D3, #D4CABC);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--gold);
            font-size: 28px;
        }

        .dish-info {
            padding: 16px;
        }

        .dish-name {
            font-size: 18px;
            font-weight: 600;
            color: var(--dark);
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            margin-bottom: 8px;
        }

        .dish-price {
            color: var(--gold);
            font-weight: 600;
            font-size: 18px;
        }

        .dish-desc {
            font-size: 13px;
            color: #8A8578;
            line-height: 1.4;
            margin-bottom: 14px;
        }

        .add-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .quantity-control {
            display: flex;
            align-items: center;
            gap: 12px;
            background: #F5F2EB;
            border-radius: 30px;
            padding: 4px 8px;
        }

        .qty-btn {
            width: 30px;
            height: 30px;
            border-radius: 15px;
            background: white;
            border: none;
            font-size: 18px;
            font-weight: bold;
            color: var(--tea-green);
            cursor: pointer;
        }

        .qty-num {
            font-size: 16px;
            font-weight: 500;
            min-width: 24px;
            text-align: center;
        }

        .cart-fab {
            position: fixed;
            bottom: 24px;
            right: 20px;
            background: var(--tea-green);
            width: 60px;
            height: 60px;
            border-radius: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 8px 20px rgba(47, 93, 58, 0.4);
            cursor: pointer;
            z-index: 200;
            font-size: 28px;
        }

        .cart-badge {
            position: absolute;
            top: -5px;
            right: -5px;
            background: var(--gold);
            color: #2C2B28;
            border-radius: 20px;
            padding: 2px 8px;
            font-size: 12px;
            font-weight: bold;
            min-width: 22px;
            text-align: center;
        }

        .cart-sidebar {
            position: fixed;
            top: 0;
            right: -100%;
            width: 85%;
            max-width: 360px;
            height: 100vh;
            background: white;
            z-index: 300;
            box-shadow: -4px 0 24px rgba(0,0,0,0.1);
            transition: right 0.3s ease;
            display: flex;
            flex-direction: column;
        }

        .cart-sidebar.open {
            right: 0;
        }

        .cart-header {
            padding: 24px 20px;
            background: var(--tea-green);
            color: white;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .close-cart {
            background: none;
            border: none;
            color: white;
            font-size: 24px;
            cursor: pointer;
        }

        .cart-items {
            flex: 1;
            overflow-y: auto;
            padding: 16px;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 0;
            border-bottom: 1px solid #EFEBE4;
        }

        .cart-item-info {
            flex: 1;
        }

        .cart-item-name {
            font-weight: 500;
            margin-bottom: 4px;
        }

        .cart-item-price {
            font-size: 13px;
            color: var(--gold);
        }

        .cart-item-control {
            display: flex;
            gap: 12px;
            align-items: center;
        }

        .cart-qty-btn {
            width: 28px;
            height: 28px;
            border-radius: 14px;
            border: 1px solid #ddd;
            background: white;
            font-size: 16px;
            cursor: pointer;
        }

        .cart-footer {
            padding: 20px;
            border-top: 1px solid #EFEBE4;
            background: #FDFCF9;
        }

        .cart-total {
            display: flex;
            justify-content: space-between;
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 20px;
        }

        .submit-btn {
            width: 100%;
            background: var(--tea-green);
            color: white;
            border: none;
            padding: 14px;
            border-radius: 40px;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
        }

        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.4);
            z-index: 250;
            display: none;
        }

        .overlay.show {
            display: block;
        }

        /* 图片预览弹窗 */
        .image-preview-modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.9);
            z-index: 600;
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .image-preview-modal.show {
            display: flex;
        }

        .preview-img {
            max-width: 100%;
            max-height: 70vh;
            border-radius: 16px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
        }

        .preview-buttons {
            display: flex;
            gap: 20px;
            margin-top: 30px;
        }

        .preview-buttons button {
            padding: 12px 28px;
            border-radius: 40px;
            border: none;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
        }

        .save-img-btn {
            background: var(--gold);
            color: #2C2B28;
        }

        .close-preview-btn {
            background: white;
            color: #333;
        }

        /* 手机端直接显示的图片模板（用于截图） */
        .booking-card-visible {
            position: fixed;
            left: -9999px;
            top: 0;
            width: 350px;
            background: linear-gradient(145deg, #1E3A25 0%, #2F5D3A 100%);
            border-radius: 28px;
            padding: 24px 20px;
            font-family: 'Georgia', 'Times New Roman', 'Songti SC', serif;
        }

        .booking-card-visible .card-border {
            border: 1px solid rgba(201, 169, 110, 0.3);
            border-radius: 20px;
            padding: 20px 16px;
        }

        .booking-card-visible .logo-area {
            text-align: center;
            margin-bottom: 20px;
        }

        .booking-card-visible .resto-name {
            font-size: 20px;
            letter-spacing: 4px;
            color: var(--gold);
            font-weight: 500;
        }

        .booking-card-visible .resto-sub {
            font-size: 8px;
            color: rgba(201,169,110,0.7);
            letter-spacing: 2px;
            margin-top: 4px;
        }

        .booking-card-visible .divider {
            height: 1px;
            background: linear-gradient(90deg, transparent, var(--gold), transparent);
            margin: 16px 0;
        }

        .booking-card-visible .info-row {
            margin-bottom: 12px;
        }

        .booking-card-visible .info-label {
            font-size: 10px;
            color: rgba(201,169,110,0.7);
            letter-spacing: 1px;
            margin-bottom: 3px;
        }

        .booking-card-visible .info-value {
            font-size: 14px;
            color: #F5F2EB;
            font-weight: 500;
        }

        .booking-card-visible .dish-item {
            display: flex;
            justify-content: space-between;
            font-size: 12px;
            color: #E8E0D3;
            padding: 5px 0;
            border-bottom: 0.5px solid rgba(201,169,110,0.2);
        }

        .booking-card-visible .total-row {
            margin-top: 12px;
            padding-top: 10px;
            border-top: 1px solid rgba(201,169,110,0.4);
            display: flex;
            justify-content: space-between;
            font-size: 16px;
            font-weight: bold;
            color: var(--gold);
        }

        .booking-card-visible .footer-text {
            font-size: 8px;
            text-align: center;
            color: rgba(201,169,110,0.5);
            margin-top: 16px;
        }
    </style>
</head>
<body>

<div class="hero">
    <div class="logo-icon">🍃</div>
    <h1>六一居</h1>
    <div class="sub">LIU YI JU · TEA & CUISINE</div>
    <div class="desc">以茶入馔 · 不时不食 · 预约雅席</div>
</div>

<div class="current-info" id="currentInfoDisplay">⚙️ 点击设置房间号/日期</div>
<div class="admin-btn" id="adminBtn">⚙️</div>

<div class="admin-modal" id="adminModal">
    <h4>🍃 商家预填信息</h4>
    <input type="text" id="roomNumber" placeholder="房间号 / 桌号（如：101 / 牡丹厅）">
    <input type="date" id="serviceDate">
    <select id="serviceTime">
        <option value="午餐 11:30-14:00">午餐 11:30-14:00</option>
        <option value="晚餐 17:30-21:00">晚餐 17:30-21:00</option>
    </select>
    <button id="saveAdminInfo">保存</button>
</div>

<div class="category-nav" id="categoryNav"></div>
<div class="menu-container" id="menuContainer"></div>

<div class="cart-fab" id="cartFab">
    🛒
    <span class="cart-badge" id="cartCount">0</span>
</div>

<div class="overlay" id="overlay"></div>
<div class="cart-sidebar" id="cartSidebar">
    <div class="cart-header">
        <h3>您的选菜</h3>
        <button class="close-cart" id="closeCart">×</button>
    </div>
    <div class="cart-items" id="cartItems"></div>
    <div class="cart-footer">
        <div class="cart-total">
            <span>总计</span>
            <span id="cartTotal">¥0</span>
        </div>
        <button class="submit-btn" id="submitOrderBtn">📸 生成预约图片</button>
    </div>
</div>

<div class="image-preview-modal" id="imagePreviewModal">
    <img class="preview-img" id="previewImg" alt="预约图片">
    <div class="preview-buttons">
        <button class="save-img-btn" id="saveImageBtn">📱 长按图片保存</button>
        <button class="close-preview-btn" id="closePreviewBtn">关闭</button>
    </div>
</div>

<!-- 用于生成图片的隐藏元素 -->
<div id="bookingCardTemplate" class="booking-card-visible"></div>

<script>
    // 菜品数据
    const menuData = {
        "茶膳前味": [
            { id: 1, name: "龙井虾仁冻", desc: "西湖龙井茶香 · 手剥河虾仁", price: 88 },
            { id: 2, name: "普洱卤牛肉", desc: "陈年普洱慢卤 · 牛腱芯", price: 78 },
            { id: 3, name: "抹茶脆皮素鹅", desc: "手工腐皮 · 抹茶盐", price: 58 }
        ],
        "茶香主菜": [
            { id: 4, name: "正山小种熏鸡", desc: "武夷山正山小种 · 烟熏三黄鸡", price: 168 },
            { id: 5, name: "铁观音茶香排骨", desc: "安溪铁观音 · 低温慢煮肋排", price: 158 },
            { id: 6, name: "茉莉花茶蒸鲈鱼", desc: "鲜拆茉莉花 · 粤式蒸鲈鱼", price: 188 }
        ],
        "茶饭主食": [
            { id: 7, name: "白茶松茸炒饭", desc: "福鼎白茶 · 新鲜松茸", price: 68 },
            { id: 8, name: "红茶手工面", desc: "祁门红茶汤底 · 手擀面", price: 48 }
        ],
        "茶点甜品": [
            { id: 9, name: "乌龙茶奶冻", desc: "凤凰单丛 · 手工奶冻", price: 38 },
            { id: 10, name: "桂花九曲红梅糕", desc: "九曲红梅茶粉 · 桂花酿", price: 42 }
        ],
        "精选茗茶": [
            { id: 11, name: "明前龙井", desc: "手工炒制 · 头采", price: 128 },
            { id: 12, name: "老枞水仙", desc: "岩韵花香", price: 98 }
        ]
    };

    let cart = [];
    let adminInfo = { room: '', date: '', time: '晚餐 17:30-21:00' };

    function loadAdminInfo() {
        const saved = localStorage.getItem('liuyiju_admin');
        if (saved) {
            adminInfo = JSON.parse(saved);
            document.getElementById('roomNumber').value = adminInfo.room;
            document.getElementById('serviceDate').value = adminInfo.date;
            document.getElementById('serviceTime').value = adminInfo.time;
        }
        updateAdminDisplay();
    }

    function saveAdminInfo() {
        adminInfo.room = document.getElementById('roomNumber').value;
        adminInfo.date = document.getElementById('serviceDate').value;
        adminInfo.time = document.getElementById('serviceTime').value;
        localStorage.setItem('liuyiju_admin', JSON.stringify(adminInfo));
        updateAdminDisplay();
        document.getElementById('adminModal').classList.remove('show');
        overlay.classList.remove('show');
        alert('预填信息已保存');
    }

    function updateAdminDisplay() {
        const displayDiv = document.getElementById('currentInfoDisplay');
        if (adminInfo.room && adminInfo.date) {
            displayDiv.innerHTML = `🏠 ${adminInfo.room} · ${adminInfo.date} ${adminInfo.time.replace(' ', '')}`;
        } else if (adminInfo.room) {
            displayDiv.innerHTML = `🏠 ${adminInfo.room} · 待设置日期`;
        } else {
            displayDiv.innerHTML = `⚙️ 点击设置房间号/日期`;
        }
    }

    function renderMenu() {
        const categories = Object.keys(menuData);
        const navDiv = document.getElementById('categoryNav');
        const menuDiv = document.getElementById('menuContainer');
        
        navDiv.innerHTML = '';
        menuDiv.innerHTML = '';

        categories.forEach((cat, idx) => {
            const catBtn = document.createElement('div');
            catBtn.className = 'cat-item' + (idx === 0 ? ' active' : '');
            catBtn.innerText = cat;
            catBtn.onclick = () => {
                document.querySelectorAll('.cat-item').forEach(c => c.classList.remove('active'));
                catBtn.classList.add('active');
                document.getElementById(cat).scrollIntoView({ behavior: 'smooth', block: 'start' });
            };
            navDiv.appendChild(catBtn);

            const section = document.createElement('div');
            section.className = 'category-section';
            section.id = cat;
            section.innerHTML = `<div class="category-title">${cat}</div>`;
            
            menuData[cat].forEach(dish => {
                const card = document.createElement('div');
                card.className = 'dish-card';
                card.innerHTML = `
                    <div class="img-placeholder">🍃 ${dish.name.charAt(0)}</div>
                    <div class="dish-info">
                        <div class="dish-name">
                            <span>${dish.name}</span>
                            <span class="dish-price">¥${dish.price}</span>
                        </div>
                        <div class="dish-desc">${dish.desc}</div>
                        <div class="add-row">
                            <div class="quantity-control" data-id="${dish.id}">
                                <button class="qty-btn decr">−</button>
                                <span class="qty-num" id="qty-${dish.id}">0</span>
                                <button class="qty-btn incr">+</button>
                            </div>
                            <span class="add-text">加入选菜</span>
                        </div>
                    </div>
                `;
                section.appendChild(card);
            });
            menuDiv.appendChild(section);
        });
        attachQuantityEvents();
    }

    function attachQuantityEvents() {
        document.querySelectorAll('.quantity-control').forEach(ctrl => {
            const dishId = parseInt(ctrl.dataset.id);
            const decrBtn = ctrl.querySelector('.decr');
            const incrBtn = ctrl.querySelector('.incr');
            const qtySpan = ctrl.querySelector('.qty-num');

            const updateDisplay = () => {
                const item = cart.find(i => i.id === dishId);
                qtySpan.innerText = item ? item.quantity : 0;
                updateCartUI();
            };

            decrBtn.onclick = (e) => {
                e.stopPropagation();
                const idx = cart.findIndex(i => i.id === dishId);
                if (idx !== -1) {
                    if (cart[idx].quantity > 1) cart[idx].quantity--;
                    else cart.splice(idx, 1);
                }
                updateDisplay();
            };

            incrBtn.onclick = (e) => {
                e.stopPropagation();
                const dish = findDishById(dishId);
                const idx = cart.findIndex(i => i.id === dishId);
                if (idx !== -1) cart[idx].quantity++;
                else cart.push({ ...dish, quantity: 1 });
                updateDisplay();
            };
            updateDisplay();
        });
    }

    function findDishById(id) {
        for (let cat of Object.values(menuData)) {
            const found = cat.find(d => d.id === id);
            if (found) return { id: found.id, name: found.name, price: found.price };
        }
        return null;
    }

    function updateCartUI() {
        const totalQty = cart.reduce((sum, i) => sum + i.quantity, 0);
        document.getElementById('cartCount').innerText = totalQty;
        
        const cartItemsDiv = document.getElementById('cartItems');
        const totalPrice = cart.reduce((sum, i) => sum + i.price * i.quantity, 0);
        document.getElementById('cartTotal').innerHTML = `¥${totalPrice}`;
        
        if (cart.length === 0) {
            cartItemsDiv.innerHTML = '<div style="text-align:center; padding:40px; color:#aaa;">暂未选菜<br>点击「+」添加</div>';
            return;
        }
        
        cartItemsDiv.innerHTML = '';
        cart.forEach(item => {
            const itemDiv = document.createElement('div');
            itemDiv.className = 'cart-item';
            itemDiv.innerHTML = `
                <div class="cart-item-info">
                    <div class="cart-item-name">${item.name}</div>
                    <div class="cart-item-price">¥${item.price}</div>
                </div>
                <div class="cart-item-control">
                    <button class="cart-qty-btn" data-id="${item.id}" data-delta="-1">−</button>
                    <span>${item.quantity}</span>
                    <button class="cart-qty-btn" data-id="${item.id}" data-delta="1">+</button>
                </div>
            `;
            cartItemsDiv.appendChild(itemDiv);
        });
        
        document.querySelectorAll('.cart-qty-btn').forEach(btn => {
            btn.onclick = (e) => {
                const id = parseInt(btn.dataset.id);
                const delta = parseInt(btn.dataset.delta);
                const idx = cart.findIndex(i => i.id === id);
                if (idx !== -1) {
                    cart[idx].quantity += delta;
                    if (cart[idx].quantity <= 0) cart.splice(idx, 1);
                }
                updateCartUI();
                attachQuantityEvents();
            };
        });
    }

    const cartFab = document.getElementById('cartFab');
    const cartSidebar = document.getElementById('cartSidebar');
    const overlay = document.getElementById('overlay');
    const closeCart = document.getElementById('closeCart');
    
    function openSidebar() { cartSidebar.classList.add('open'); overlay.classList.add('show'); }
    function closeSidebar() { cartSidebar.classList.remove('open'); overlay.classList.remove('show'); }
    
    cartFab.onclick = openSidebar;
    closeCart.onclick = closeSidebar;
    overlay.onclick = closeSidebar;

    const adminBtn = document.getElementById('adminBtn');
    const adminModal = document.getElementById('adminModal');
    adminBtn.onclick = () => {
        adminModal.classList.add('show');
        overlay.classList.add('show');
    };
    document.getElementById('saveAdminInfo').onclick = saveAdminInfo;

    // 生成图片（使用 dom-to-image 替代 html2canvas，手机端更稳定）
    function generateImage(element) {
        return new Promise((resolve, reject) => {
            // 获取元素的实际尺寸
            const width = element.offsetWidth;
            const height = element.offsetHeight;
            
            // 创建 canvas
            const canvas = document.createElement('canvas');
            canvas.width = width * 2;  // 2倍分辨率，更清晰
            canvas.height = height * 2;
            const ctx = canvas.getContext('2d');
            
            // 绘制背景
            ctx.fillStyle = '#1E3A25';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            
            // 使用 html2canvas 但设置更兼容的参数
            html2canvas(element, {
                scale: 2,
                backgroundColor: '#1E3A25',
                useCORS: false,
                logging: false,
                allowTaint: true,
                foreignObjectRendering: false
            }).then(canvasResult => {
                resolve(canvasResult.toDataURL('image/png'));
            }).catch(err => {
                reject(err);
            });
        });
    }

    const submitBtn = document.getElementById('submitOrderBtn');
    
    submitBtn.onclick = async () => {
        if (cart.length === 0) {
            alert('请先选菜');
            return;
        }
        
        if (!adminInfo.room || !adminInfo.date) {
            alert('请先点击右下角⚙️设置房间号和日期');
            return;
        }
        
        // 显示加载提示
        const originalText = submitBtn.innerText;
        submitBtn.innerText = '⏳ 生成中...';
        submitBtn.disabled = true;
        
        const total = cart.reduce((s, i) => s + i.price * i.quantity, 0);
        
        const dishListHtml = cart.map(item => `
            <div class="dish-item">
                <span>${item.name} x${item.quantity}</span>
                <span>¥${item.price * item.quantity}</span>
            </div>
        `).join('');
        
        const templateHtml = `
            <div class="card-border">
                <div class="logo-area">
                    <div class="logo-icon" style="font-size: 36px;">🍃</div>
                    <div class="resto-name">六一居</div>
                    <div class="resto-sub">LIU YI JU · TEA & CUISINE</div>
                </div>
                <div class="divider"></div>
                <div class="info-row">
                    <div class="info-label">房间 / 雅席</div>
                    <div class="info-value">${escapeHtml(adminInfo.room)}</div>
                </div>
                <div class="info-row">
                    <div class="info-label">用餐日期</div>
                    <div class="info-value">${escapeHtml(adminInfo.date)} · ${escapeHtml(adminInfo.time)}</div>
                </div>
                <div class="divider"></div>
                <div class="info-label" style="margin-bottom: 6px;">所选菜品</div>
                <div style="max-height: 200px; overflow-y: auto;">
                    ${dishListHtml || '<div style="color:#aaa; text-align:center;">暂无菜品</div>'}
                </div>
                <div class="total-row">
                    <span>总计</span>
                    <span>¥${total}</span>
                </div>
                <div class="footer-text">请截图此页面，发送给餐厅管家确认</div>
            </div>
        `;
        
        const templateDiv = document.getElementById('bookingCardTemplate');
        templateDiv.innerHTML = templateHtml;
        
        // 等待DOM渲染完成
        setTimeout(async () => {
            try {
                // 动态加载 html2canvas
                if (typeof html2canvas === 'undefined') {
                    await loadScript('https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js');
                }
                
                const canvas = await html2canvas(templateDiv, {
                    scale: 2,
                    backgroundColor: '#1E3A25',
                    useCORS: false,
                    logging: false,
                    allowTaint: true,
                    foreignObjectRendering: false,
                    windowWidth: templateDiv.scrollWidth,
                    windowHeight: templateDiv.scrollHeight
                });
                
                const imgData = canvas.toDataURL('image/png');
                const previewImg = document.getElementById('previewImg');
                previewImg.src = imgData;
                document.getElementById('imagePreviewModal').classList.add('show');
                closeSidebar();
                
                // 手机端提示长按保存
                const saveBtn = document.getElementById('saveImageBtn');
                saveBtn.innerHTML = '📱 长按图片保存';
                saveBtn.onclick = () => {
                    // 提示用户长按保存
                    alert('请长按上方图片，选择「保存图片」');
                };
                
            } catch (err) {
                console.error('生成图片失败:', err);
                alert('生成图片失败，请稍后重试');
            } finally {
                submitBtn.innerText = originalText;
                submitBtn.disabled = false;
            }
        }, 100);
    };
    
    function escapeHtml(str) {
        if (!str) return '';
        return str.replace(/[&<>]/g, function(m) {
            if (m === '&') return '&amp;';
            if (m === '<') return '&lt;';
            if (m === '>') return '&gt;';
            return m;
        });
    }
    
    function loadScript(src) {
        return new Promise((resolve, reject) => {
            const script = document.createElement('script');
            script.src = src;
            script.onload = resolve;
            script.onerror = reject;
            document.head.appendChild(script);
        });
    }
    
    document.getElementById('closePreviewBtn').onclick = () => {
        document.getElementById('imagePreviewModal').classList.remove('show');
    };
    
    // 初始化
    loadAdminInfo();
    renderMenu();
</script>
<!-- 引入 html2canvas -->
<script src="https://cdn.jsdelivr.net/npm/html2canvas@1.4.1/dist/html2canvas.min.js"></script>
</body>
</html>
