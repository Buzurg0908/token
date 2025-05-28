<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>CryptoGame Bot</title>
    <style>
        :root {
            --primary: #6c5ce7;
            --secondary: #a29bfe;
            --accent: #fd79a8;
            --dark: #2d3436;
            --light: #f5f6fa;
            --success: #00b894;
            --warning: #fdcb6e;
            --danger: #d63031;
        }
        
        @font-face {
            font-family: 'GameFont';
            src: url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
        }
        
        body {
            font-family: 'Press Start 2P', cursive;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #1e1e2f, #2d2d4d);
            color: white;
            min-height: 100vh;
            overflow-x: hidden;
            letter-spacing: 1px;
        }
        
        .container {
            max-width: 100%;
            padding: 15px;
            box-sizing: border-box;
            padding-bottom: 80px;
        }
        
        .header {
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            color: white;
            padding: 20px;
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            position: relative;
            overflow: hidden;
        }
        
        .header::after {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" preserveAspectRatio="none"><path fill="rgba(255,255,255,0.05)" d="M0,0 L100,0 L100,100 L0,100 Z" /></svg>');
            opacity: 0.3;
        }
        
        .nav {
            display: flex;
            justify-content: space-around;
            background: rgba(44, 44, 84, 0.9);
            backdrop-filter: blur(10px);
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            padding: 12px 0;
            box-shadow: 0 -5px 15px rgba(0,0,0,0.3);
            z-index: 100;
            border-top: 1px solid rgba(255,255,255,0.1);
        }
        
        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-decoration: none;
            color: var(--light);
            font-size: 10px;
            transition: all 0.3s ease;
            position: relative;
            padding: 5px 10px;
            border-radius: 15px;
        }
        
        .nav-item.active {
            color: var(--accent);
            transform: translateY(-5px);
        }
        
        .nav-item.active::before {
            content: "";
            position: absolute;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 6px;
            height: 6px;
            background: var(--accent);
            border-radius: 50%;
            box-shadow: 0 0 10px var(--accent);
        }
        
        .nav-icon {
            font-size: 20px;
            margin-bottom: 5px;
            transition: all 0.3s ease;
        }
        
        .nav-item.active .nav-icon {
            transform: scale(1.2);
            text-shadow: 0 0 10px var(--accent);
        }
        
        .card {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.2);
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255,255,255,0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 25px rgba(0,0,0,0.3);
        }
        
        .card::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, var(--primary), var(--accent));
        }
        
        .btn {
            background: linear-gradient(45deg, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 50px;
            font-size: 14px;
            width: 100%;
            cursor: pointer;
            font-family: 'Press Start 2P', cursive;
            text-transform: uppercase;
            letter-spacing: 1px;
            transition: all 0.3s ease;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            position: relative;
            overflow: hidden;
        }
        
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(0,0,0,0.3);
        }
        
        .btn:active {
            transform: translateY(1px);
        }
        
        .btn::after {
            content: "";
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(rgba(255,255,255,0.1), rgba(255,255,255,0));
            transform: rotate(30deg);
        }
        
        .btn-success {
            background: linear-gradient(45deg, var(--success), #55efc4);
        }
        
        .btn-danger {
            background: linear-gradient(45deg, var(--danger), #ff7675);
        }
        
        .btn-warning {
            background: linear-gradient(45deg, var(--warning), #ffeaa7);
            color: var(--dark);
        }
        
        .page {
            display: none;
            animation: fadeIn 0.5s ease;
        }
        
        .page.active {
            display: block;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .token-card {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            margin: 10px 0;
            background: rgba(255,255,255,0.05);
            border-radius: 10px;
            transition: all 0.3s ease;
            border-left: 3px solid var(--primary);
        }
        
        .token-card:hover {
            background: rgba(255,255,255,0.1);
            transform: translateX(5px);
        }
        
        .token-info {
            flex: 1;
        }
        
        .token-name {
            font-weight: bold;
            font-size: 16px;
            color: var(--accent);
            margin-bottom: 5px;
        }
        
        .token-creator {
            color: var(--secondary);
            font-size: 10px;
            opacity: 0.8;
        }
        
        .token-price {
            font-weight: bold;
            color: var(--warning);
            font-size: 14px;
        }
        
        .balance-card {
            background: linear-gradient(135deg, #6c5ce7, #a29bfe);
            color: white;
            padding: 20px;
            border-radius: 15px;
            text-align: center;
            margin-bottom: 20px;
            position: relative;
            overflow: hidden;
            box-shadow: 0 10px 20px rgba(108, 92, 231, 0.3);
        }
        
        .balance-card::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" preserveAspectRatio="none"><path fill="rgba(255,255,255,0.1)" d="M0,0 L100,0 L100,100 L0,100 Z" /></svg>');
        }
        
        .balance-amount {
            font-size: 36px;
            font-weight: bold;
            margin: 15px 0;
            text-shadow: 0 2px 5px rgba(0,0,0,0.3);
        }
        
        .input-field {
            width: 100%;
            padding: 12px 15px;
            margin: 10px 0;
            border: none;
            border-radius: 50px;
            background: rgba(255,255,255,0.1);
            color: white;
            font-family: 'Press Start 2P', cursive;
            font-size: 12px;
            border: 1px solid rgba(255,255,255,0.2);
        }
        
        .input-field:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 10px rgba(253, 121, 168, 0.5);
        }
        
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
        }
        
        .particle {
            position: absolute;
            background: rgba(255,255,255,0.5);
            border-radius: 50%;
            animation: float 15s infinite linear;
        }
        
        @keyframes float {
            0% { transform: translateY(0) rotate(0deg); opacity: 0; }
            10% { opacity: 1; }
            90% { opacity: 1; }
            100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
        }
        
        /* Анимация пульсации для важных элементов */
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .pulse {
            animation: pulse 2s infinite;
        }
        
        /* Стили для модальных окон */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.8);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s ease;
            backdrop-filter: blur(5px);
        }
        
        .modal.active {
            opacity: 1;
            pointer-events: all;
        }
        
        .modal-content {
            background: linear-gradient(135deg, #2d2d4d, #1e1e2f);
            border-radius: 20px;
            padding: 25px;
            width: 90%;
            max-width: 400px;
            max-height: 90vh;
            overflow-y: auto;
            box-shadow: 0 15px 30px rgba(0,0,0,0.4);
            border: 1px solid rgba(255,255,255,0.1);
            position: relative;
        }
        
        .modal-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            color: var(--accent);
            font-size: 20px;
            cursor: pointer;
        }
        
        /* Стили для формы создания токена */
        .form-group {
            margin-bottom: 15px;
        }
        
        .form-label {
            display: block;
            margin-bottom: 8px;
            color: var(--secondary);
            font-size: 12px;
        }
        
        /* Эффект неонового свечения */
        .glow-effect {
            position: relative;
        }
        
        .glow-effect::after {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            border-radius: inherit;
            box-shadow: 0 0 15px var(--primary);
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .glow-effect:hover::after {
            opacity: 0.7;
        }
        
        /* Новые стили для форм пополнения и вывода */
        .payment-methods {
            display: flex;
            justify-content: space-between;
            margin: 15px 0;
        }
        
        .payment-method {
            width: 48%;
            padding: 10px;
            border-radius: 10px;
            background: rgba(255,255,255,0.1);
            border: 1px solid rgba(255,255,255,0.2);
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .payment-method.active {
            border-color: var(--accent);
            background: rgba(253, 121, 168, 0.2);
        }
        
        .payment-method i {
            font-size: 24px;
            margin-bottom: 5px;
        }
        
        .qr-code {
            width: 150px;
            height: 150px;
            margin: 15px auto;
            background: white;
            display: flex;
            align-items: center;
            justify-content: center;
            color: black;
        }
        
        /* Стили для списка транзакций */
        .transaction-list {
            margin-top: 15px;
        }
        
        .transaction-item {
            display: flex;
            justify-content: space-between;
            padding: 10px;
            margin-bottom: 8px;
            background: rgba(255,255,255,0.05);
            border-radius: 8px;
            font-size: 10px;
        }
        
        .transaction-type {
            font-weight: bold;
        }
        
        .transaction-amount {
            font-weight: bold;
        }
        
        .transaction-positive {
            color: var(--success);
        }
        
        .transaction-negative {
            color: var(--danger);
        }
        
        .transaction-date {
            font-size: 8px;
            color: var(--secondary);
            opacity: 0.7;
        }

        /* Стили для сообщений об ошибках */
        .error-message {
            color: var(--danger);
            font-size: 10px;
            margin-top: 5px;
            display: none;
        }
        
        /* Стили для сообщений аутентификации */
        .auth-message {
            margin-top: 15px;
            font-size: 10px;
            text-align: center;
            display: none;
        }
        
        .auth-message.success {
            color: var(--success);
        }
        
        .auth-message.error {
            color: var(--danger);
        }
        
        .auth-message.warning {
            color: var(--warning);
        }
        
        .auth-message.info {
            color: var(--secondary);
        }
    </style>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
</head>
<body>
    <!-- Анимированные частицы фона -->
    <div class="particles" id="particles"></div>
    
    <div class="header glow-effect">
        CRYPTO GAME BOT
    </div>
    
    <div class="container">
        <!-- Главная страница -->
        <div id="home-page" class="page">
            <div class="balance-card pulse">
                <p>YOUR BALANCE</p>
                <div class="balance-amount" id="user-balance">$0.00</div>
                <button class="btn btn-success" id="add-funds-btn">ADD FUNDS</button>
            </div>
            
            <div class="card">
                <h2>YOUR TOKENS <i class="fas fa-coins" style="color: var(--warning);"></i></h2>
                <div id="user-tokens-list">
                    <div style="text-align: center; padding: 20px 0;">
                        <i class="fas fa-lock" style="font-size: 40px; opacity: 0.5;"></i>
                        <p>Please login to view your tokens</p>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Кошелек -->
        <div id="wallet-page" class="page">
            <div class="card">
                <h2><i class="fas fa-wallet"></i> WALLET</h2>
                <div class="balance-amount" style="font-size: 24px;" id="wallet-balance">$0.00</div>
                
                <button class="btn btn-success" style="margin-bottom: 10px;" id="deposit-btn">
                    <i class="fas fa-plus-circle"></i> DEPOSIT
                </button>
                <button class="btn btn-danger" id="withdraw-btn">
                    <i class="fas fa-minus-circle"></i> WITHDRAW
                </button>
            </div>
            
            <div class="card">
                <h2><i class="fas fa-history"></i> TRANSACTIONS</h2>
                <div id="transactions-container" class="transaction-list">
                    <div style="text-align: center; padding: 20px 0;">
                        <i class="fas fa-lock" style="font-size: 40px; opacity: 0.5;"></i>
                        <p>Please login to view transactions</p>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Маркетплейс -->
        <div id="marketplace-page" class="page">
            <div class="card">
                <h2><i class="fas fa-store"></i> TOKEN MARKETPLACE</h2>
                <div id="marketplace-tokens-list">
                    <div style="text-align: center; padding: 20px 0;">
                        <i class="fas fa-lock" style="font-size: 40px; opacity: 0.5;"></i>
                        <p>Please login to view marketplace</p>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Профиль -->
        <div id="profile-page" class="page active">
            <div class="card" id="auth-section">
                <h2><i class="fas fa-user-astronaut"></i> AUTHENTICATION</h2>
                
                <div class="form-group">
                    <input type="text" id="username" placeholder="USERNAME" class="input-field">
                    <div id="username-error" class="error-message">Username must be at least 3 characters</div>
                </div>
                
                <div class="form-group">
                    <input type="password" id="password" placeholder="PASSWORD" class="input-field">
                    <div id="password-error" class="error-message">Password must be at least 6 characters</div>
                </div>
                
                <button class="btn" id="login-btn">
                    <i class="fas fa-sign-in-alt"></i> LOGIN
                </button>
                
                <button class="btn btn-success" id="register-btn" style="margin-top: 10px;">
                    <i class="fas fa-user-plus"></i> REGISTER
                </button>

                <div id="auth-message" class="auth-message"></div>
            </div>
            
            <div class="card" id="profile-section" style="display: none;">
                <h2><i class="fas fa-user-ninja"></i> PROFILE</h2>
                
                <div style="text-align: center; margin: 20px 0;">
                    <div style="width: 80px; height: 80px; background: var(--primary); border-radius: 50%; margin: 0 auto 15px; display: flex; align-items: center; justify-content: center; font-size: 30px;">
                        <i class="fas fa-user"></i>
                    </div>
                    <div id="profile-username" style="font-size: 16px; margin-bottom: 5px;">USERNAME</div>
                    <div id="profile-join-date" style="font-size: 10px; color: var(--secondary);">Joined just now</div>
                </div>
                
                <button class="btn btn-danger" id="logout-btn">
                    <i class="fas fa-sign-out-alt"></i> LOGOUT
                </button>
                
                <button class="btn btn-warning" id="create-token-btn" style="margin-top: 10px;">
                    <i class="fas fa-plus-circle"></i> CREATE TOKEN
                </button>
            </div>
        </div>
    </div>
    
    <!-- Навигация -->
    <div class="nav">
        <a href="#" class="nav-item" data-page="home-page">
            <i class="fas fa-home nav-icon"></i>
            <span>Home</span>
        </a>
        <a href="#" class="nav-item" data-page="wallet-page">
            <i class="fas fa-wallet nav-icon"></i>
            <span>Wallet</span>
        </a>
        <a href="#" class="nav-item" data-page="marketplace-page">
            <i class="fas fa-store nav-icon"></i>
            <span>Market</span>
        </a>
        <a href="#" class="nav-item active" data-page="profile-page">
            <i class="fas fa-user nav-icon"></i>
            <span>Profile</span>
        </a>
    </div>
    
    <!-- Модальное окно создания токена -->
    <div class="modal" id="create-token-modal">
        <div class="modal-content">
            <button class="modal-close">&times;</button>
            <h2><i class="fas fa-magic"></i> CREATE TOKEN</h2>
            
            <form id="token-creation-form">
                <div class="form-group">
                    <label class="form-label">TOTAL SUPPLY</label>
                    <input type="number" class="input-field" placeholder="1000000" required>
                </div>
                
                <div class="form-group">
                    <label class="form-label">TOKEN NAME</label>
                    <input type="text" class="input-field" placeholder="MY_GAME_TOKEN" required>
                </div>
                
                <div class="form-group">
                    <label class="form-label">DESCRIPTION</label>
                    <textarea class="input-field" style="height: 80px;" placeholder="Describe your project..." required></textarea>
                </div>
                
                <div class="form-group">
                    <label class="form-label">DISTRIBUTION PLAN</label>
                    <textarea class="input-field" style="height: 80px;" placeholder="How will tokens be distributed?" required></textarea>
                </div>
                
                <button type="submit" class="btn btn-success">
                    <i class="fas fa-check-circle"></i> CREATE
                </button>
            </form>
        </div>
    </div>
    
    <!-- Модальное окно пополнения баланса -->
    <div class="modal" id="deposit-modal">
        <div class="modal-content">
            <button class="modal-close">&times;</button>
            <h2><i class="fas fa-coins"></i> DEPOSIT FUNDS</h2>
            
            <div class="form-group">
                <label class="form-label">AMOUNT (USD)</label>
                <input type="number" class="input-field" placeholder="100.00" id="deposit-amount" required>
            </div>
            
            <div class="form-group">
                <label class="form-label">PAYMENT METHOD</label>
                <div class="payment-methods">
                    <div class="payment-method active" data-method="crypto">
                        <i class="fab fa-bitcoin"></i>
                        <div>Crypto</div>
                    </div>
                    <div class="payment-method" data-method="card">
                        <i class="fas fa-credit-card"></i>
                        <div>Card</div>
                    </div>
                </div>
            </div>
            
            <div id="crypto-deposit" class="deposit-method">
                <div class="form-group">
                    <label class="form-label">SELECT CRYPTO</label>
                    <select class="input-field" id="crypto-currency">
                        <option value="BTC">Bitcoin (BTC)</option>
                        <option value="ETH">Ethereum (ETH)</option>
                        <option value="USDT">Tether (USDT)</option>
                        <option value="TON">Toncoin (TON)</option>
                    </select>
                </div>
                
                <div class="qr-code">
                    <i class="fas fa-qrcode" style="font-size: 50px;"></i>
                </div>
                
                <div class="form-group">
                    <label class="form-label">WALLET ADDRESS</label>
                    <input type="text" class="input-field" value="1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa" readonly id="wallet-address">
                    <button class="btn" style="margin-top: 10px; padding: 8px;" onclick="copyToClipboard('wallet-address')">
                        <i class="fas fa-copy"></i> COPY ADDRESS
                    </button>
                </div>
                
                <div style="font-size: 10px; color: var(--secondary); text-align: center; margin-top: 15px;">
                    Send only <span id="selected-crypto">BTC</span> to this address
                </div>
            </div>
            
            <div id="card-deposit" class="deposit-method" style="display: none;">
                <div class="form-group">
                    <label class="form-label">CARD NUMBER</label>
                    <input type="text" class="input-field" placeholder="1234 5678 9012 3456" required>
                </div>
                
                <div style="display: flex; gap: 10px;">
                    <div class="form-group" style="flex: 1;">
                        <label class="form-label">EXPIRY DATE</label>
                        <input type="text" class="input-field" placeholder="MM/YY" required>
                    </div>
                    <div class="form-group" style="flex: 1;">
                        <label class="form-label">CVV</label>
                        <input type="text" class="input-field" placeholder="123" required>
                    </div>
                </div>
                
                <div class="form-group">
                    <label class="form-label">CARDHOLDER NAME</label>
                    <input type="text" class="input-field" placeholder="John Doe" required>
                </div>
            </div>
            
            <button class="btn btn-success" id="confirm-deposit">
                <i class="fas fa-check"></i> CONFIRM DEPOSIT
            </button>
        </div>
    </div>
    
    <!-- Модальное окно вывода средств -->
    <div class="modal" id="withdraw-modal">
        <div class="modal-content">
            <button class="modal-close">&times;</button>
            <h2><i class="fas fa-money-bill-wave"></i> WITHDRAW FUNDS</h2>
            
            <div class="form-group">
                <label class="form-label">AMOUNT (USD)</label>
                <input type="number" class="input-field" placeholder="100.00" id="withdraw-amount" required>
                <div style="font-size: 10px; color: var(--secondary);">Available: $<span id="available-balance">0.00</span></div>
            </div>
            
            <div class="form-group">
                <label class="form-label">WITHDRAWAL METHOD</label>
                <select class="input-field" id="withdraw-method">
                    <option value="crypto">Crypto Wallet</option>
                    <option value="bank">Bank Transfer</option>
                </select>
            </div>
            
            <div id="crypto-withdraw">
                <div class="form-group">
                    <label class="form-label">SELECT CURRENCY</label>
                    <select class="input-field" id="withdraw-crypto">
                        <option value="BTC">Bitcoin (BTC)</option>
                        <option value="ETH">Ethereum (ETH)</option>
                        <option value="USDT">Tether (USDT)</option>
                        <option value="TON">Toncoin (TON)</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label class="form-label">WALLET ADDRESS</label>
                    <input type="text" class="input-field" placeholder="Enter your wallet address" id="withdraw-address" required>
                </div>
                
                <div style="font-size: 10px; color: var(--warning); margin-bottom: 15px;">
                    <i class="fas fa-exclamation-circle"></i> Minimum withdrawal: $10.00
                </div>
            </div>
            
            <div id="bank-withdraw" style="display: none;">
                <div class="form-group">
                    <label class="form-label">BANK ACCOUNT NUMBER</label>
                    <input type="text" class="input-field" placeholder="Enter your account number" required>
                </div>
                
                <div class="form-group">
                    <label class="form-label">BANK NAME</label>
                    <input type="text" class="input-field" placeholder="Enter bank name" required>
                </div>
                
                <div class="form-group">
                    <label class="form-label">SWIFT CODE</label>
                    <input type="text" class="input-field" placeholder="Enter SWIFT code" required>
                </div>
                
                <div style="font-size: 10px; color: var(--warning); margin-bottom: 15px;">
                    <i class="fas fa-exclamation-circle"></i> Bank transfers may take 3-5 business days
                </div>
            </div>
            
            <button class="btn btn-success" id="confirm-withdraw">
                <i class="fas fa-paper-plane"></i> REQUEST WITHDRAWAL
            </button>
        </div>
    </div>
    
    <script>
        // Состояние приложения
        const appState = {
            isAuthenticated: false,
            currentUser: null,
            users: {}, // Хранилище пользователей
            balance: 0,
            tokens: [],
            marketplaceTokens: [
                { name: "DRAGON COIN", price: 0.10, creator: "@dragon_game", description: "RPG game currency" },
                { name: "SPACE GOLD", price: 0.25, creator: "@space_adventure", description: "Space exploration game" },
                { name: "RACING FUEL", price: 0.15, creator: "@fast_racing", description: "Car racing game" }
            ],
            transactions: []
        };

        // Инициализация частиц фона
        function initParticles() {
            const particlesContainer = document.getElementById('particles');
            const particleCount = 30;
            
            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.classList.add('particle');
                
                const size = Math.random() * 5 + 2;
                const posX = Math.random() * 100;
                const delay = Math.random() * 15;
                const duration = Math.random() * 10 + 10;
                
                particle.style.width = `${size}px`;
                particle.style.height = `${size}px`;
                particle.style.left = `${posX}%`;
                particle.style.bottom = `-${size}px`;
                particle.style.animationDelay = `${delay}s`;
                particle.style.animationDuration = `${duration}s`;
                particle.style.opacity = Math.random() * 0.5 + 0.1;
                
                particlesContainer.appendChild(particle);
            }
        }
        
        // Навигация по страницам
        function setupNavigation() {
            const navItems = document.querySelectorAll('.nav-item');
            
            navItems.forEach(item => {
                item.addEventListener('click', function(e) {
                    e.preventDefault();
                    
                    // Если пользователь не авторизован, перенаправляем на страницу профиля
                    if (!appState.isAuthenticated && this.getAttribute('data-page') !== 'profile-page') {
                        showAuthMessage('Please login first', 'warning');
                        document.querySelector('.nav-item[data-page="profile-page"]').click();
                        return;
                    }
                    
                    navItems.forEach(navItem => navItem.classList.remove('active'));
                    this.classList.add('active');
                    
                    document.querySelectorAll('.page').forEach(page => {
                        page.classList.remove('active');
                    });
                    
                    const pageId = this.getAttribute('data-page');
                    document.getElementById(pageId).classList.add('active');
                });
            });
        }
        
        // Управление модальными окнами
        function setupModals() {
            // Обработчики для всех кнопок открытия модальных окон
            document.getElementById('create-token-btn')?.addEventListener('click', () => {
                if (!appState.isAuthenticated) {
                    showAuthMessage('Please login first', 'warning');
                    return;
                }
                document.getElementById('create-token-modal').classList.add('active');
            });
            
            document.querySelectorAll('#deposit-btn, #add-funds-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    if (!appState.isAuthenticated) {
                        showAuthMessage('Please login first', 'warning');
                        return;
                    }
                    document.getElementById('deposit-modal').classList.add('active');
                });
            });
            
            document.getElementById('withdraw-btn')?.addEventListener('click', () => {
                if (!appState.isAuthenticated) {
                    showAuthMessage('Please login first', 'warning');
                    return;
                }
                document.getElementById('withdraw-modal').classList.add('active');
            });
            
            // Закрытие модальных окон
            document.querySelectorAll('.modal-close').forEach(btn => {
                btn.addEventListener('click', () => {
                    btn.closest('.modal').classList.remove('active');
                });
            });
            
            // Закрытие по клику вне окна
            document.querySelectorAll('.modal').forEach(modal => {
                modal.addEventListener('click', (e) => {
                    if (e.target === modal) {
                        modal.classList.remove('active');
                    }
                });
            });
        }
        
        // Показать сообщение об аутентификации
        function showAuthMessage(message, type = 'info') {
            const authMessage = document.getElementById('auth-message');
            authMessage.textContent = message;
            authMessage.style.display = 'block';
            
            // Очищаем предыдущие классы
            authMessage.className = 'auth-message';
            
            // Добавляем соответствующий класс
            authMessage.classList.add(type);
            
            // Скрываем сообщение через 5 секунд
            setTimeout(() => {
                authMessage.style.display = 'none';
            }, 5000);
        }
        
        // Валидация формы
        function validateAuthForm(username, password) {
            let isValid = true;
            
            // Валидация имени пользователя
            if (username.length < 3) {
                document.getElementById('username-error').style.display = 'block';
                isValid = false;
            } else {
                document.getElementById('username-error').style.display = 'none';
            }
            
            // Валидация пароля
            if (password.length < 6) {
                document.getElementById('password-error').style.display = 'block';
                isValid = false;
            } else {
                document.getElementById('password-error').style.display = 'none';
            }
            
            return isValid;
        }
        
        // Регистрация пользователя
        function registerUser(username, password) {
            // Проверяем, существует ли уже пользователь
            if (appState.users[username]) {
                showAuthMessage('Username already exists', 'error');
                return false;
            }
            
            // Создаем нового пользователя
            appState.users[username] = {
                username: username,
                password: password, // В реальном приложении пароль должен быть хеширован!
                balance: 100, // Начальный баланс для новых пользователей
                tokens: [
                    { name: "GAME COIN", amount: 10000, creator: "You" },
                    { name: "PREMIUM", amount: 5000, creator: "You" }
                ],
                joinDate: new Date(),
                transactions: [
                    { type: 'initial', amount: 100, date: new Date().toLocaleString() }
                ]
            };
            
            return true;
        }
        
        // Аутентификация пользователя
        function loginUser(username, password) {
            const user = appState.users[username];
            
            // Проверяем существование пользователя и пароль
            if (!user || user.password !== password) {
                showAuthMessage('Invalid username or password', 'error');
                return false;
            }
            
            // Устанавливаем текущего пользователя
            appState.currentUser = user;
            appState.isAuthenticated = true;
            
            // Обновляем состояние приложения для текущего пользователя
            appState.balance = user.balance;
            appState.tokens = [...user.tokens];
            appState.transactions = [...user.transactions];
            
            return true;
        }
        
        // Выход пользователя
        function logoutUser() {
            appState.isAuthenticated = false;
            appState.currentUser = null;
            appState.balance = 0;
            appState.tokens = [];
            appState.transactions = [];
            
            // Переключаем на страницу профиля
            document.querySelector('.nav-item[data-page="profile-page"]').click();
        }
        
        // Обновление UI после входа/выхода
        function updateAuthUI() {
            const authSection = document.getElementById('auth-section');
            const profileSection = document.getElementById('profile-section');
            
            if (appState.isAuthenticated) {
                authSection.style.display = 'none';
                profileSection.style.display = 'block';
                
                // Обновляем данные профиля
                document.getElementById('profile-username').textContent = appState.currentUser.username;
                document.getElementById('profile-join-date').textContent = `Joined ${formatJoinDate(appState.currentUser.joinDate)}`;
                
                // Обновляем баланс и данные
                updateBalanceDisplays();
                renderUserTokens();
                renderMarketplaceTokens();
                renderTransactions();
                
                // Показываем сообщение об успешном входе
                showAuthMessage(`Welcome back, ${appState.currentUser.username}!`, 'success');
            } else {
                authSection.style.display = 'block';
                profileSection.style.display = 'none';
                
                // Сбрасываем поля ввода
                document.getElementById('username').value = '';
                document.getElementById('password').value = '';
                
                // Очищаем сообщения об ошибках
                document.getElementById('username-error').style.display = 'none';
                document.getElementById('password-error').style.display = 'none';
                
                // Очищаем данные на страницах
                document.getElementById('user-tokens-list').innerHTML = `
                    <div style="text-align: center; padding: 20px 0;">
                        <i class="fas fa-lock" style="font-size: 40px; opacity: 0.5;"></i>
                        <p>Please login to view your tokens</p>
                    </div>
                `;
                
                document.getElementById('transactions-container').innerHTML = `
                    <div style="text-align: center; padding: 20px 0;">
                        <i class="fas fa-lock" style="font-size: 40px; opacity: 0.5;"></i>
                        <p>Please login to view transactions</p>
                    </div>
                `;
                
                document.getElementById('marketplace-tokens-list').innerHTML = `
                    <div style="text-align: center; padding: 20px 0;">
                        <i class="fas fa-lock" style="font-size: 40px; opacity: 0.5;"></i>
                        <p>Please login to view marketplace</p>
                    </div>
                `;
            }
        }
        
        // Форматирование даты регистрации
        function formatJoinDate(date) {
            const now = new Date();
            const diff = now - new Date(date);
            const days = Math.floor(diff / (1000 * 60 * 60 * 24));
            
            if (days === 0) return 'today';
            if (days === 1) return 'yesterday';
            if (days < 7) return `${days} days ago`;
            if (days < 30) return `${Math.floor(days / 7)} weeks ago`;
            return `${Math.floor(days / 30)} months ago`;
        }
        
        // Инициализация Telegram WebApp
        function initTelegramWebApp() {
            if (window.Telegram && window.Telegram.WebApp) {
                Telegram.WebApp.expand();
                
                const user = Telegram.WebApp.initDataUnsafe?.user;
                if (user) {
                    // Автоматическая регистрация/вход через Telegram
                    const username = `user_${user.id}`;
                    const password = Math.random().toString(36).substring(2, 10);
                    
                    if (!appState.users[username]) {
                        registerUser(username, password);
                    }
                    
                    if (loginUser(username, password)) {
                        updateAuthUI();
                    }
                }
                
                Telegram.WebApp.BackButton.onClick(() => {
                    // Логика кнопки "назад"
                });
            }
        }
        
        // Отправка данных в бота
        function sendDataToBot(data) {
            if (window.Telegram && window.Telegram.WebApp) {
                Telegram.WebApp.sendData(JSON.stringify(data));
            } else {
                console.log('Данные для отправки:', data);
                alert('В реальном Telegram WebApp эти данные были бы отправлены боту:\n' + JSON.stringify(data, null, 2));
            }
        }
        
        // Копирование в буфер обмена
        function copyToClipboard(elementId) {
            const element = document.getElementById(elementId);
            element.select();
            document.execCommand('copy');
            
            const originalText = element.value;
            element.value = 'Copied!';
            setTimeout(() => {
                element.value = originalText;
            }, 2000);
        }
        
        // Настройка методов оплаты
        function setupPaymentMethods() {
            document.querySelectorAll('.payment-method').forEach(method => {
                method.addEventListener('click', function() {
                    document.querySelectorAll('.payment-method').forEach(m => m.classList.remove('active'));
                    this.classList.add('active');
                    
                    const methodType = this.getAttribute('data-method');
                    document.querySelectorAll('.deposit-method').forEach(form => {
                        form.style.display = 'none';
                    });
                    document.getElementById(`${methodType}-deposit`).style.display = 'block';
                });
            });
            
            document.getElementById('crypto-currency')?.addEventListener('change', function() {
                document.getElementById('selected-crypto').textContent = this.value;
            });
            
            document.getElementById('withdraw-method')?.addEventListener('change', function() {
                document.getElementById('crypto-withdraw').style.display = 
                    this.value === 'crypto' ? 'block' : 'none';
                document.getElementById('bank-withdraw').style.display = 
                    this.value === 'bank' ? 'block' : 'none';
            });
        }
        
        // Обновление отображения баланса
        function updateBalanceDisplays() {
            const balance = appState.balance.toFixed(2);
            document.querySelectorAll('#user-balance, #wallet-balance, #available-balance').forEach(el => {
                el.textContent = `$${balance}`;
            });
        }
        
        // Добавление транзакции
        function addTransaction(type, amount, details = {}) {
            const transaction = {
                id: Date.now(),
                type,
                amount,
                date: new Date().toLocaleString(),
                ...details
            };
            
            appState.transactions.unshift(transaction);
            
            // Обновляем транзакции пользователя
            if (appState.isAuthenticated) {
                appState.currentUser.transactions.unshift(transaction);
                appState.currentUser.balance = appState.balance;
            }
            
            renderTransactions();
            
            return transaction;
        }
        
        // Отрисовка списка транзакций
        function renderTransactions() {
            const container = document.getElementById('transactions-container');
            if (!container) return;
            
            container.innerHTML = '';
            
            if (appState.transactions.length === 0) {
                container.innerHTML = `
                    <div style="text-align: center; padding: 20px 0;">
                        <i class="fas fa-clock" style="font-size: 40px; opacity: 0.5;"></i>
                        <p>No transactions yet</p>
                    </div>
                `;
                return;
            }
            
            appState.transactions.forEach(transaction => {
                const transactionEl = document.createElement('div');
                transactionEl.className = 'transaction-item';
                
                const isPositive = transaction.type === 'deposit' || transaction.type === 'token_sale' || transaction.type === 'initial';
                const amountClass = isPositive ? 'transaction-positive' : 'transaction-negative';
                const amountPrefix = isPositive ? '+' : '-';
                
                transactionEl.innerHTML = `
                    <div>
                        <div class="transaction-type">${transaction.type.replace('_', ' ').toUpperCase()}</div>
                        <div class="transaction-date">${transaction.date}</div>
                        ${transaction.token ? `<div style="font-size: 8px; color: var(--secondary);">${transaction.token}</div>` : ''}
                    </div>
                    <div class="transaction-amount ${amountClass}">${amountPrefix}$${transaction.amount.toFixed(2)}</div>
                `;
                
                container.appendChild(transactionEl);
            });
        }
        
        // Отрисовка токенов пользователя
        function renderUserTokens() {
            const container = document.getElementById('user-tokens-list');
            if (!container) return;
            
            container.innerHTML = '';
            
            if (appState.tokens.length === 0) {
                container.innerHTML = `
                    <div style="text-align: center; padding: 20px 0;">
                        <i class="fas fa-coins" style="font-size: 40px; opacity: 0.5;"></i>
                        <p>You don't have any tokens yet</p>
                    </div>
                `;
                return;
            }
            
            appState.tokens.forEach(token => {
                const tokenEl = document.createElement('div');
                tokenEl.className = 'token-card';
                tokenEl.innerHTML = `
                    <div class="token-info">
                        <div class="token-name">${token.name}</div>
                        <div class="token-creator">${token.creator}</div>
                    </div>
                    <div class="token-price">${token.amount.toLocaleString()}</div>
                `;
                container.appendChild(tokenEl);
            });
        }
        
        // Отрисовка токенов на маркетплейсе
        function renderMarketplaceTokens() {
            const container = document.getElementById('marketplace-tokens-list');
            if (!container) return;
            
            container.innerHTML = '';
            
            appState.marketplaceTokens.forEach(token => {
                const tokenEl = document.createElement('div');
                tokenEl.className = 'token-card';
                tokenEl.innerHTML = `
                    <div class="token-info">
                        <div class="token-name">${token.name}</div>
                        <div class="token-creator">${token.creator}</div>
                        <div style="font-size: 10px; color: var(--secondary);">${token.description}</div>
                    </div>
                    <div>
                        <div class="token-price">$${token.price.toFixed(2)}</div>
                        <button class="btn buy-token-btn" style="padding: 5px 10px; font-size: 10px; margin-top: 5px;" 
                                data-name="${token.name}" data-price="${token.price}">
                            BUY
                        </button>
                    </div>
                `;
                container.appendChild(tokenEl);
            });
            
            // Назначение обработчиков для кнопок покупки
            document.querySelectorAll('.buy-token-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    if (!appState.isAuthenticated) {
                        showAuthMessage('Please login first', 'warning');
                        return;
                    }
                    
                    const tokenName = this.getAttribute('data-name');
                    const tokenPrice = parseFloat(this.getAttribute('data-price'));
                    
                    if (appState.balance < tokenPrice) {
                        alert('Not enough balance to buy this token!');
                        return;
                    }
                    
                    // Уменьшаем баланс
                    appState.balance -= tokenPrice;
                    appState.currentUser.balance = appState.balance;
                    updateBalanceDisplays();
                    
                    // Добавляем токен пользователю или увеличиваем количество, если уже есть
                    const existingToken = appState.tokens.find(t => t.name === tokenName);
                    if (existingToken) {
                        existingToken.amount += 1;
                        
                        // Обновляем токен у пользователя
                        const userToken = appState.currentUser.tokens.find(t => t.name === tokenName);
                        if (userToken) {
                            userToken.amount += 1;
                        }
                    } else {
                        appState.tokens.push({
                            name: tokenName,
                            amount: 1,
                            creator: "Purchased"
                        });
                        
                        appState.currentUser.tokens.push({
                            name: tokenName,
                            amount: 1,
                            creator: "Purchased"
                        });
                    }
                    
                    // Добавляем транзакцию
                    addTransaction('token_purchase', tokenPrice, {
                        token: tokenName
                    });
                    
                    // Обновляем отображение токенов
                    renderUserTokens();
                    
                    alert(`Successfully purchased ${tokenName} for $${tokenPrice.toFixed(2)}!`);
                });
            });
        }
        
        // Обработка форм пополнения и вывода
        function setupTransactionForms() {
            // Пополнение баланса
            document.getElementById('confirm-deposit')?.addEventListener('click', function(e) {
                e.preventDefault();
                
                if (!appState.isAuthenticated) {
                    showAuthMessage('Please login first', 'warning');
                    return;
                }
                
                const amount = parseFloat(document.getElementById('deposit-amount').value);
                if (!amount || amount <= 0) {
                    alert('Please enter a valid amount');
                    return;
                }
                
                const method = document.querySelector('.payment-method.active').getAttribute('data-method');
                let data;
                
                if (method === 'crypto') {
                    const currency = document.getElementById('crypto-currency').value;
                    const address = document.getElementById('wallet-address').value;
                    
                    data = {
                        action: 'deposit_crypto',
                        amount: amount,
                        currency: currency,
                        address: address
                    };
                } else {
                    data = {
                        action: 'deposit_card',
                        amount: amount
                    };
                }
                
                // Обновляем баланс
                appState.balance += amount;
                appState.currentUser.balance = appState.balance;
                updateBalanceDisplays();
                
                // Добавляем транзакцию
                addTransaction('deposit', amount);
                
                sendDataToBot(data);
                document.getElementById('deposit-modal').classList.remove('active');
                alert(`Deposit request for $${amount.toFixed(2)} has been sent!`);
            });
            
            // Вывод средств
            document.getElementById('confirm-withdraw')?.addEventListener('click', function(e) {
                e.preventDefault();
                
                if (!appState.isAuthenticated) {
                    showAuthMessage('Please login first', 'warning');
                    return;
                }
                
                const amount = parseFloat(document.getElementById('withdraw-amount').value);
                if (!amount || amount <= 0) {
                    alert('Please enter a valid amount');
                    return;
                }
                
                if (amount < 10) {
                    alert('Minimum withdrawal amount is $10');
                    return;
                }
                
                if (amount > appState.balance) {
                    alert('Not enough balance for this withdrawal');
                    return;
                }
                
                const method = document.getElementById('withdraw-method').value;
                let data;
                
                if (method === 'crypto') {
                    const address = document.getElementById('withdraw-address').value;
                    if (!address) {
                        alert('Please enter your wallet address');
                        return;
                    }
                    
                    const currency = document.getElementById('withdraw-crypto').value;
                    data = {
                        action: 'withdraw_crypto',
                        amount: amount,
                        currency: currency,
                        address: address
                    };
                } else {
                    data = {
                        action: 'withdraw_bank',
                        amount: amount
                    };
                }
                
                // Обновляем баланс
                appState.balance -= amount;
                appState.currentUser.balance = appState.balance;
                updateBalanceDisplays();
                
                // Добавляем транзакцию
                addTransaction('withdrawal', amount);
                
                sendDataToBot(data);
                document.getElementById('withdraw-modal').classList.remove('active');
                alert(`Withdrawal request for $${amount.toFixed(2)} has been sent!`);
            });
        }
        
        // Инициализация при загрузке
        document.addEventListener('DOMContentLoaded', () => {
            initParticles();
            setupNavigation();
            setupModals();
            setupPaymentMethods();
            setupTransactionForms();
            initTelegramWebApp();
            
            // Обработка входа
            document.getElementById('login-btn')?.addEventListener('click', () => {
                const username = document.getElementById('username').value.trim();
                const password = document.getElementById('password').value;
                
                if (!validateAuthForm(username, password)) return;
                
                if (loginUser(username, password)) {
                    updateAuthUI();
                }
            });
            
            // Обработка регистрации
            document.getElementById('register-btn')?.addEventListener('click', () => {
                const username = document.getElementById('username').value.trim();
                const password = document.getElementById('password').value;
                
                if (!validateAuthForm(username, password)) return;
                
                if (registerUser(username, password)) {
                    if (loginUser(username, password)) {
                        updateAuthUI();
                        showAuthMessage('Registration successful! Welcome!', 'success');
                    }
                }
            });
            
            // Обработка выхода
            document.getElementById('logout-btn')?.addEventListener('click', () => {
                logoutUser();
                updateAuthUI();
                showAuthMessage('You have been logged out', 'info');
            });
            
            // Обработка создания токена
            document.getElementById('token-creation-form')?.addEventListener('submit', (e) => {
                e.preventDefault();
                
                if (!appState.isAuthenticated) {
                    showAuthMessage('Please login first', 'warning');
                    return;
                }
                
                const form = e.target;
                const tokenData = {
                    action: 'create_token',
                    totalSupply: form[0].value,
                    name: form[1].value,
                    description: form[2].value,
                    distribution: form[3].value
                };
                
                // Добавляем новый токен
                const newToken = {
                    name: tokenData.name,
                    amount: parseInt(tokenData.totalSupply),
                    creator: "You"
                };
                
                appState.tokens.push(newToken);
                appState.currentUser.tokens.push(newToken);
                
                // Обновляем отображение
                renderUserTokens();
                
                sendDataToBot(tokenData);
                document.getElementById('create-token-modal').classList.remove('active');
                alert('Token created successfully!');
                
                // Сбрасываем форму
                form.reset();
            });
            
            // Инициализация данных
            updateAuthUI();
        });
    </script>
</body>
</html>
