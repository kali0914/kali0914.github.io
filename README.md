<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>低调的黑客 - 网络安全空间</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --blue: #3498db;
            --red: #e74c3c;
            --pink: #e84393;
            --yellow: #f1c40f;
            --orange: #e67e22;
            --green: #2ecc71;
            --purple: #9b59b6;
            --dark-bg: #0a0e17;
            --light-bg: #1a1f2e;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
            /* 专属光标 */
            cursor: url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzIiIGhlaWdodD0iMzIiIHZpZXdCb3g9IjAgMCAzMiAzMiIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTE2IDZWMjZNMjYgMTZINiIgc3Ryb2tlPSIjMzQ5OEQiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLWxpbmVjYXA9InJvdW5kIi8+CjxjaXJjbGUgY3g9IjE2IiBjeT0iMTYiIHI9IjMiIGZpbGw9IiNmZmZmZmYiLz4KPHBhdGggZD0iTTggOEwyNCAyNE0yNCA4TDggMjQiIHN0cm9rZT0iIzM0OThEIiBzdHJva2Utd2lkdGg9IjEiIHN0cm9rZS1saW5lY2FwPSJyb3VuZCIvPgo8L3N2Zz4='), auto;
        }
        
        /* 特殊元素的光标样式 */
        a, button, .contact-btn, .circular-action-btn, .admin-button, .login-button, 
        .verify-button, .back-to-home, .friend-link-item, .admin-footer-btn a,
        .icon-option, .slider-handle, #closeLogin, #closeAdmin, #exploreBtn, #adminFooterBtn {
            cursor: url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzIiIGhlaWdodD0iMzIiIHZpZXdCb3g9IjAgMCAzMiAzMiIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTggOEwyNCAyNE0yNCA4TDggMjQiIHN0cm9rZT0iI2YxYzQwZiIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbGluZWNhcD0icm91bmQiLz4KPGNpcmNsZSBjeD0iMTYiIGN5PSIxNiIgcj0iNCIgZmlsbD0iI2YxYzQwZiIvPgo8L3N2Zz4='), pointer;
        }
        
        /* 禁用文本选择 */
        body {
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
            user-select: none;
            background-color: var(--dark-bg);
            color: #fff;
            min-height: 100vh;
            overflow-x: hidden;
            transition: background-image 1s ease;
            background-size: cover;
            background-position: center;
            background-attachment: fixed;
            background-repeat: no-repeat;
        }
        
        /* 右键禁用提示框 */
        .right-click-warning {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(231, 76, 60, 0.95);
            color: white;
            padding: 20px 30px;
            border-radius: 10px;
            z-index: 9999;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            border: 2px solid white;
            animation: warningPulse 0.5s;
        }
        
        @keyframes warningPulse {
            0% { transform: translate(-50%, -50%) scale(0.8); opacity: 0; }
            70% { transform: translate(-50%, -50%) scale(1.05); }
            100% { transform: translate(-50%, -50%) scale(1); opacity: 1; }
        }
        
        .right-click-warning i {
            font-size: 2.5rem;
            margin-bottom: 10px;
            display: block;
        }
        
        .right-click-warning p {
            font-size: 1.2rem;
            font-weight: bold;
        }
        
        /* 动态山峰背景类 - 根据北京时间变化 */
        .bg-morning-mountain {
            background-image: linear-gradient(rgba(10, 14, 23, 0.85), rgba(10, 14, 23, 0.9)), url('https://images.unsplash.com/photo-1506905925346-21bda4d32df4?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80') !important;
        }
        
        .bg-noon-mountain {
            background-image: linear-gradient(rgba(10, 14, 23, 0.85), rgba(10, 14, 23, 0.9)), url('https://images.unsplash.com/photo-1464278533981-50106e6176b1?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80') !important;
        }
        
        .bg-afternoon-mountain {
            background-image: linear-gradient(rgba(10, 14, 23, 0.85), rgba(10, 14, 23, 0.9)), url('https://images.unsplash.com/photo-1506905925346-21bda4d32df4?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80') !important;
        }
        
        .bg-evening-mountain {
            background-image: linear-gradient(rgba(10, 14, 23, 0.85), rgba(10, 14, 23, 0.9)), url('https://images.unsplash.com/photo-1519681393784-d120267933ba?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80') !important;
        }
        
        .bg-night-mountain {
            background-image: linear-gradient(rgba(10, 14, 23, 0.85), rgba(10, 14, 23, 0.9)), url('https://images.unsplash.com/photo-1519681393784-d120267933ba?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80') !important;
        }
        
        /* 半透明遮罩增强文字可读性 */
        .page-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(10, 14, 23, 0.7);
            z-index: -1;
        }
        
        /* 主页面样式 */
        #home-page {
            display: none;
            min-height: 100vh;
            text-align: center;
            padding: 40px 20px;
            animation: fadeIn 1s ease;
            position: relative;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .home-container {
            max-width: 800px;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            justify-content: center;
            min-height: 80vh;
            position: relative;
            z-index: 1;
        }
        
        .home-title {
            font-size: 4rem;
            margin-bottom: 10px;
            background: linear-gradient(45deg, var(--blue), var(--green), var(--yellow), var(--orange));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            font-weight: bold;
            line-height: 1.1;
            text-shadow: 0 0 20px rgba(52, 152, 219, 0.3);
        }
        
        .home-subtitle {
            font-size: 1.8rem;
            color: #aaa;
            margin-bottom: 40px;
            position: relative;
            display: inline-block;
            font-weight: 300;
            letter-spacing: 2px;
        }
        
        .home-subtitle:after {
            content: "";
            position: absolute;
            width: 100%;
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--blue), transparent);
            bottom: -15px;
            left: 0;
        }
        
        .home-description {
            font-size: 1.2rem;
            color: #ddd;
            max-width: 600px;
            margin: 0 auto 60px;
            line-height: 1.8;
            padding: 20px;
            border-radius: 15px;
            background: rgba(26, 31, 46, 0.7);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(52, 152, 219, 0.2);
        }
        
        .home-buttons {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 80px;
        }
        
        .circular-action-btn {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 150px;
            height: 150px;
            background: linear-gradient(45deg, var(--blue), var(--pink));
            color: white;
            border-radius: 50%;
            text-decoration: none;
            font-size: 1.5rem;
            font-weight: bold;
            transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            border: none;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(52, 152, 219, 0.3);
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0% { box-shadow: 0 10px 30px rgba(52, 152, 219, 0.3); }
            50% { box-shadow: 0 15px 40px rgba(52, 152, 219, 0.5); }
            100% { box-shadow: 0 10px 30px rgba(52, 152, 219, 0.3); }
        }
        
        .circular-action-btn:before {
            content: "";
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255, 255, 255, 0.1), transparent);
            transform: rotate(45deg);
            transition: all 0.5s;
        }
        
        .circular-action-btn:hover {
            transform: scale(1.1) rotate(5deg);
            box-shadow: 0 20px 50px rgba(52, 152, 219, 0.5);
        }
        
        .circular-action-btn:hover:before {
            transform: rotate(405deg);
        }
        
        .circular-action-btn span {
            position: relative;
            z-index: 1;
        }
        
        .home-stats {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 30px;
            margin-bottom: 60px;
        }
        
        .stat-item {
            background: rgba(26, 31, 46, 0.7);
            border-radius: 15px;
            padding: 20px;
            min-width: 150px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(52, 152, 219, 0.2);
            transition: transform 0.3s;
        }
        
        .stat-item:hover {
            transform: translateY(-5px);
            border-color: var(--blue);
        }
        
        .stat-value {
            font-size: 2.5rem;
            font-weight: bold;
            background: linear-gradient(45deg, var(--blue), var(--pink));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 10px;
        }
        
        .stat-label {
            color: #aaa;
            font-size: 1rem;
        }
        
        /* 主页页脚样式 */
        .home-footer {
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            color: #888;
            font-size: 0.8rem;
        }
        
        .home-footer-content {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
        }
        
        .home-footer-copyright {
            margin-bottom: 10px;
        }
        
        .home-footer-beian {
            display: flex;
            align-items: center;
            gap: 8px;
            color: #aaa;
            font-size: 0.75rem;
        }
        
        .home-footer-admin {
            margin-top: 15px;
        }
        
        .home-footer-admin a {
            display: inline-block;
            background: rgba(26, 31, 46, 0.9);
            color: #aaa;
            padding: 8px 15px;
            border-radius: 10px;
            text-decoration: none;
            font-size: 0.8rem;
            transition: all 0.3s;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .home-footer-admin a:hover {
            color: white;
            background: rgba(52, 152, 219, 0.3);
            border-color: var(--blue);
        }
        
        .police-badge {
            color: #e74c3c;
            font-size: 0.9rem;
        }
        
        /* 探索页面样式 */
        #explore-page {
            display: none;
            min-height: 100vh;
            padding: 20px;
            animation: fadeIn 1s ease;
            position: relative;
        }
        
        .explore-container {
            max-width: 1200px;
            margin: 0 auto;
            position: relative;
            z-index: 1;
            padding-bottom: 60px; /* 为页脚留出空间 */
        }
        
        .explore-header {
            padding: 40px 0 20px;
            text-align: center;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            margin-bottom: 40px;
        }
        
        .explore-title {
            font-size: 2.5rem;
            margin-bottom: 15px;
            color: white;
        }
        
        .back-to-home {
            display: inline-block;
            color: var(--blue);
            text-decoration: none;
            font-size: 1.1rem;
            margin-top: 20px;
            transition: color 0.3s;
            background: rgba(26, 31, 46, 0.7);
            padding: 10px 20px;
            border-radius: 20px;
            border: 1px solid rgba(52, 152, 219, 0.2);
        }
        
        .back-to-home:hover {
            color: var(--pink);
            border-color: var(--pink);
        }
        
        .profile-section {
            background: rgba(26, 31, 46, 0.85);
            border-radius: 15px;
            padding: 40px;
            margin-bottom: 40px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(52, 152, 219, 0.2);
        }
        
        .profile-header {
            display: flex;
            align-items: center;
            gap: 30px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }
        
        .profile-avatar {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            background: linear-gradient(45deg, var(--blue), var(--red), var(--yellow));
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
            border: 4px solid rgba(255, 255, 255, 0.1);
            flex-shrink: 0;
        }
        
        .profile-avatar img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: none;
        }
        
        .profile-avatar i {
            font-size: 3rem;
            color: white;
        }
        
        .profile-info h2 {
            font-size: 2.2rem;
            margin-bottom: 10px;
            color: white;
        }
        
        .profile-info p {
            font-size: 1.2rem;
            color: #aaa;
        }
        
        .profile-content {
            line-height: 1.8;
            color: #ddd;
            font-size: 1.1rem;
        }
        
        .profile-content p {
            margin-bottom: 20px;
        }
        
        /* 安全提示样式 */
        .security-tips-section {
            background: rgba(26, 31, 46, 0.85);
            border-radius: 15px;
            padding: 40px;
            margin-bottom: 40px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(52, 152, 219, 0.2);
        }
        
        .section-title {
            font-size: 2rem;
            margin-bottom: 30px;
            color: #fff;
            position: relative;
            display: inline-block;
        }
        
        .section-title:after {
            content: "";
            position: absolute;
            width: 50%;
            height: 4px;
            background: linear-gradient(90deg, var(--blue), var(--pink));
            bottom: -10px;
            left: 0;
            border-radius: 2px;
        }
        
        .security-tips-list {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
        }
        
        .security-tip-card {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            padding: 25px;
            border-left: 5px solid var(--blue);
            transition: transform 0.3s;
        }
        
        .security-tip-card:hover {
            transform: translateY(-5px);
        }
        
        .security-tip-card h4 {
            color: var(--blue);
            margin-bottom: 15px;
            font-size: 1.3rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .security-tip-card p {
            color: #ddd;
            line-height: 1.6;
        }
        
        /* 联系我样式 - 修改后的样式，只显示联系方式 */
        .contact-section {
            background: rgba(26, 31, 46, 0.85);
            border-radius: 15px;
            padding: 40px;
            margin-bottom: 40px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(52, 152, 219, 0.2);
        }
        
        .contact-buttons-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 25px;
            margin-top: 30px;
        }
        
        .contact-btn {
            display: flex;
            align-items: center;
            background: rgba(26, 31, 46, 0.9);
            border-radius: 15px;
            padding: 20px 30px;
            text-decoration: none;
            color: white;
            font-weight: bold;
            font-size: 1.1rem;
            transition: all 0.3s;
            border: 2px solid transparent;
            min-width: 280px;
            justify-content: flex-start;
            position: relative;
        }
        
        .contact-btn:hover {
            transform: translateY(-5px);
            border-color: var(--blue);
            box-shadow: 0 10px 20px rgba(52, 152, 219, 0.2);
        }
        
        .contact-btn i {
            font-size: 1.8rem;
            margin-right: 15px;
            width: 40px;
        }
        
        .contact-value {
            font-size: 1rem;
            color: #aaa;
            font-weight: normal;
            margin-top: 5px;
        }
        
        /* 友情链接样式 */
        .friend-links-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 20px;
            margin: 40px 0;
            padding: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .friend-links-container h3 {
            width: 100%;
            text-align: center;
            color: #aaa;
            margin-bottom: 20px;
            font-size: 1.2rem;
        }
        
        .friend-link-item {
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--blue);
            text-decoration: none;
            font-size: 1.1rem;
            transition: all 0.3s;
            padding: 10px 20px;
            background: rgba(26, 31, 46, 0.7);
            border-radius: 10px;
            border: 1px solid rgba(52, 152, 219, 0.2);
        }
        
        .friend-link-item:hover {
            color: var(--pink);
            transform: translateY(-3px);
            border-color: var(--blue);
        }
        
        /* 探索页面页脚 */
        .explore-footer {
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            color: #888;
            font-size: 0.8rem;
            text-align: center;
        }
        
        .explore-footer-beian {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            color: #aaa;
            font-size: 0.75rem;
            margin-top: 10px;
        }
        
        /* 管理后台登录模态框 */
        .login-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            z-index: 2000;
            justify-content: center;
            align-items: center;
        }
        
        .login-modal.active {
            display: flex;
        }
        
        .login-box {
            background: rgba(26, 31, 46, 0.95);
            border-radius: 20px;
            padding: 40px;
            width: 100%;
            max-width: 400px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.7);
            border: 1px solid rgba(52, 152, 219, 0.2);
            backdrop-filter: blur(10px);
        }
        
        .login-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
        }
        
        .login-title {
            font-size: 1.8rem;
            color: white;
        }
        
        .close-login {
            background: transparent;
            border: none;
            color: #aaa;
            font-size: 1.5rem;
            cursor: pointer;
            transition: color 0.3s;
        }
        
        .close-login:hover {
            color: white;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #ccc;
        }
        
        .form-group input {
            width: 100%;
            padding: 12px 15px;
            border-radius: 10px;
            background: rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255, 255, 255, 0.1);
            color: white;
            font-size: 1rem;
        }
        
        .form-group input:focus {
            outline: none;
            border-color: var(--blue);
        }
        
        .form-group input:read-only {
            background: rgba(0, 0, 0, 0.7);
            color: #888;
            cursor: not-allowed;
        }
        
        .login-button {
            width: 100%;
            padding: 15px;
            background: linear-gradient(45deg, var(--blue), var(--pink));
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            margin-top: 10px;
        }
        
        .login-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(52, 152, 219, 0.3);
        }
        
        .login-message {
            margin-top: 20px;
            padding: 10px;
            border-radius: 5px;
            text-align: center;
            display: none;
        }
        
        .login-message.error {
            display: block;
            background: rgba(231, 76, 60, 0.2);
            border: 1px solid var(--red);
            color: #ff9999;
        }
        
        .login-message.success {
            display: block;
            background: rgba(46, 204, 113, 0.2);
            border: 1px solid #2ecc71;
            color: #99ffcc;
        }
        
        /* 管理后台页面 */
        .admin-panel {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(10, 14, 23, 0.98);
            z-index: 3000;
            overflow-y: auto;
            padding: 20px;
        }
        
        .admin-panel.active {
            display: block;
        }
        
        .admin-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .admin-title {
            font-size: 2rem;
            color: white;
        }
        
        .close-admin {
            background: transparent;
            border: none;
            color: #aaa;
            font-size: 1.5rem;
            cursor: pointer;
            transition: color 0.3s;
        }
        
        .close-admin:hover {
            color: white;
        }
        
        .admin-content {
            max-width: 1200px;
            margin: 0 auto;
            padding-bottom: 40px;
        }
        
        .admin-section {
            background: rgba(26, 31, 46, 0.9);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 25px;
            border: 1px solid rgba(52, 152, 219, 0.2);
            backdrop-filter: blur(10px);
        }
        
        .admin-section h3 {
            color: var(--blue);
            margin-bottom: 20px;
            font-size: 1.5rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .form-row {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            margin-bottom: 15px;
        }
        
        .form-col {
            flex: 1;
            min-width: 300px;
        }
        
        /* 列表项管理样式 */
        .list-items {
            margin-top: 15px;
        }
        
        .list-item {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 10px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            align-items: center;
        }
        
        .list-item-controls {
            display: flex;
            gap: 10px;
            margin-top: 10px;
            width: 100%;
        }
        
        .admin-button {
            padding: 12px 25px;
            background: linear-gradient(45deg, var(--blue), var(--pink));
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .admin-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.3);
        }
        
        .admin-button.small {
            padding: 8px 15px;
            font-size: 0.9rem;
        }
        
        .admin-button.secondary {
            background: rgba(255, 255, 255, 0.1);
            margin-left: 10px;
        }
        
        .admin-button.danger {
            background: rgba(231, 76, 60, 0.2);
            border: 1px solid var(--red);
        }
        
        .admin-button.success {
            background: rgba(46, 204, 113, 0.2);
            border: 1px solid #2ecc71;
        }
        
        .admin-footer {
            display: flex;
            justify-content: flex-end;
            gap: 15px;
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        /* 管理后台页脚 */
        .admin-panel-footer {
            margin-top: 40px;
            padding-top: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            color: #888;
            font-size: 0.8rem;
            text-align: center;
        }
        
        .admin-panel-footer-beian {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            color: #aaa;
            font-size: 0.75rem;
            margin-top: 10px;
        }
        
        /* 图标选择器 */
        .icon-selector {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 10px;
            max-height: 200px;
            overflow-y: auto;
            padding: 10px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
        }
        
        .icon-option {
            width: 50px;
            height: 50px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(0, 0, 0, 0.3);
            cursor: pointer;
            border: 2px solid transparent;
            transition: all 0.3s;
        }
        
        .icon-option:hover {
            border-color: var(--blue);
            transform: scale(1.1);
        }
        
        .icon-option.selected {
            border-color: var(--blue);
            background: rgba(52, 152, 219, 0.2);
        }
        
        .icon-option i {
            font-size: 1.5rem;
            color: white;
        }
        
        /* 验证页面样式 */
        #verification-page {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
            text-align: center;
            position: relative;
        }
        
        .verification-box {
            background: rgba(26, 31, 46, 0.9);
            border-radius: 20px;
            padding: 40px;
            width: 100%;
            max-width: 500px;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.7);
            border: 1px solid rgba(52, 152, 219, 0.2);
            backdrop-filter: blur(10px);
        }
        
        .verification-logo {
            font-size: 3.5rem;
            margin-bottom: 20px;
            background: linear-gradient(45deg, var(--blue), var(--pink));
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        
        .verification-title {
            font-size: 2rem;
            margin-bottom: 10px;
            color: #fff;
        }
        
        .verification-subtitle {
            color: #aaa;
            margin-bottom: 30px;
            font-size: 1.1rem;
        }
        
        .slider-container {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 25px;
            position: relative;
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .slider-track {
            width: 100%;
            height: 50px;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 8px;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }
        
        .slider-text {
            position: absolute;
            z-index: 2;
            color: rgba(255, 255, 255, 0.8);
            font-weight: bold;
        }
        
        .slider-fill {
            position: absolute;
            left: 0;
            top: 0;
            height: 100%;
            width: 0;
            background: linear-gradient(90deg, var(--blue), var(--pink));
            border-radius: 8px;
            transition: width 0.1s;
        }
        
        .slider-handle {
            position: absolute;
            left: 0;
            top: 0;
            width: 60px;
            height: 100%;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 8px;
            cursor: pointer;
            z-index: 3;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
        }
        
        .slider-handle i {
            color: var(--dark-bg);
            font-size: 1.5rem;
        }
        
        .verification-instruction {
            color: #aaa;
            font-size: 0.9rem;
            margin-bottom: 25px;
        }
        
        .verify-button {
            background: linear-gradient(45deg, var(--blue), var(--pink));
            color: white;
            border: none;
            padding: 15px 40px;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            width: 100%;
            letter-spacing: 1px;
        }
        
        .verify-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(52, 152, 219, 0.3);
        }
        
        /* 验证页面页脚 */
        .verification-footer {
            position: absolute;
            bottom: 20px;
            left: 0;
            width: 100%;
            text-align: center;
            color: #888;
            font-size: 0.8rem;
        }
        
        .verification-footer-beian {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            color: #aaa;
            font-size: 0.75rem;
            margin-top: 5px;
        }
        
        /* 自定义图标上传 */
        .custom-icon-upload {
            margin-top: 15px;
            padding: 15px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 10px;
        }
        
        .custom-icon-preview {
            margin-top: 10px;
            text-align: center;
        }
        
        .custom-icon-preview img {
            width: 50px;
            height: 50px;
            object-fit: contain;
            border-radius: 10px;
            background: rgba(0, 0, 0, 0.3);
            padding: 5px;
            border: 2px solid rgba(52, 152, 219, 0.3);
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .home-title { font-size: 3rem; }
            .home-subtitle { font-size: 1.5rem; }
            .home-description { font-size: 1rem; padding: 15px; }
            .circular-action-btn { width: 120px; height: 120px; font-size: 1.2rem; }
            .explore-title { font-size: 2rem; }
            .profile-header { flex-direction: column; text-align: center; }
            .profile-avatar { width: 100px; height: 100px; }
            .profile-info h2 { font-size: 1.8rem; }
            .contact-btn { min-width: 100%; }
            .verification-box { padding: 30px 20px; }
            .form-col { min-width: 100%; }
            .stat-item { min-width: 120px; }
            .stat-value { font-size: 2rem; }
        }
        
        @media (max-width: 480px) {
            .home-title { font-size: 2.5rem; }
            .home-subtitle { font-size: 1.2rem; }
            .circular-action-btn { width: 100px; height: 100px; font-size: 1rem; }
            .security-tips-list { grid-template-columns: 1fr; }
            .home-stats { gap: 15px; }
            .stat-item { min-width: 100px; padding: 15px; }
            .stat-value { font-size: 1.8rem; }
        }
    </style>
</head>
<body>
    <!-- 右键禁用提示框 -->
    <div class="right-click-warning" id="rightClickWarning">
        <i class="fas fa-ban"></i>
        <p>本站禁止使用右键</p>
    </div>
    
    <!-- 半透明遮罩 -->
    <div class="page-overlay"></div>
    
    <!-- 管理后台登录模态框 -->
    <div class="login-modal" id="loginModal">
        <div class="login-box">
            <div class="login-header">
                <h2 class="login-title" id="loginTitle">管理后台登录</h2>
                <button class="close-login" id="closeLogin">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <div class="form-group">
                <label for="username" id="usernameLabel">用户名</label>
                <input type="text" id="username" placeholder="请输入用户名">
            </div>
            
            <div class="form-group">
                <label for="password" id="passwordLabel">密码</label>
                <input type="password" id="password" placeholder="请输入密码">
            </div>
            
            <button class="login-button" id="loginButton">登录</button>
            
            <div class="login-message" id="loginMessage"></div>
        </div>
    </div>
    
    <!-- 管理后台页面 -->
    <div class="admin-panel" id="adminPanel">
        <div class="admin-content">
            <div class="admin-header">
                <h2 class="admin-title" id="adminTitle">管理后台</h2>
                <button class="close-admin" id="closeAdmin">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <!-- 个人资料管理 -->
            <div class="admin-section">
                <h3><i class="fas fa-user"></i> <span id="profileTitle">个人资料管理</span></h3>
                <div class="form-row">
                    <div class="form-col">
                        <label for="adminName">姓名</label>
                        <input type="text" id="adminName" placeholder="输入您的姓名">
                    </div>
                    <div class="form-col">
                        <label for="adminTagline">标签</label>
                        <input type="text" id="adminTagline" placeholder="输入您的标签">
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-col">
                        <label for="adminAvatar">头像URL</label>
                        <input type="text" id="adminAvatar" placeholder="输入头像图片URL">
                    </div>
                    <div class="form-col">
                        <label for="adminAvatarPreview">头像预览</label>
                        <div style="margin-top: 10px; text-align: center;">
                            <div class="avatar" id="avatarPreview" style="width: 80px; height: 80px; margin: 0 auto;">
                                <img id="avatarImgPreview" src="" alt="头像预览" style="display: none;">
                                <i class="fas fa-user-secret"></i>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="adminDescription">个人描述</label>
                        <textarea id="adminDescription" rows="4" placeholder="输入个人描述" style="width: 100%; padding: 12px 15px; border-radius: 10px; background: rgba(0, 0, 0, 0.3); border: 1px solid rgba(255, 255, 255, 0.1); color: white; font-size: 1rem;"></textarea>
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="newProfileFieldName">新增信息字段名</label>
                        <input type="text" id="newProfileFieldName" placeholder="输入字段名（如：生日、所在地）">
                    </div>
                    <div class="form-col">
                        <label for="newProfileFieldValue">字段值</label>
                        <input type="text" id="newProfileFieldValue" placeholder="输入字段值">
                    </div>
                </div>
                
                <button class="admin-button secondary" id="addProfileFieldBtn">添加个人信息</button>
                
                <div class="list-items" id="profileFieldsList">
                    <!-- 动态生成个人信息字段列表 -->
                </div>
            </div>
            
            <!-- 联系我管理 -->
            <div class="admin-section">
                <h3><i class="fas fa-envelope"></i> <span id="contactSocialTitle">联系我管理</span></h3>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="newContactName">联系名称</label>
                        <input type="text" id="newContactName" placeholder="输入联系名称（如：邮箱、微信等）">
                    </div>
                    <div class="form-col">
                        <label for="newContactValue">联系方式（只显示值）</label>
                        <input type="text" id="newContactValue" placeholder="输入联系方式（如：kali0914@yeah.net）">
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="newContactUrl">实际链接（用户点击后跳转）</label>
                        <input type="text" id="newContactUrl" placeholder="输入实际链接（如：mailto:kali0914@yeah.net）">
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-col">
                        <label>选择图标</label>
                        <div class="icon-selector" id="contactIconSelector">
                            <!-- 图标选项将通过JS动态生成 -->
                        </div>
                    </div>
                </div>
                
                <!-- 自定义图标上传 -->
                <div class="custom-icon-upload">
                    <label for="customIconUrl">或使用自定义图标URL</label>
                    <input type="text" id="customIconUrl" placeholder="输入自定义图标URL">
                    <div class="custom-icon-preview" id="customIconPreview">
                        <!-- 自定义图标预览 -->
                    </div>
                </div>
                
                <button class="admin-button secondary" id="addContactBtn">添加联系信息</button>
                
                <div class="list-items" id="contactItemsList">
                    <!-- 动态生成联系信息列表 -->
                </div>
            </div>
            
            <!-- 安全提示管理 -->
            <div class="admin-section">
                <h3><i class="fas fa-shield-alt"></i> <span id="securityTipsTitle">安全提示管理</span></h3>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="newSecurityTipTitle">提示标题</label>
                        <input type="text" id="newSecurityTipTitle" placeholder="输入提示标题">
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="newSecurityTipContent">提示内容</label>
                        <textarea id="newSecurityTipContent" rows="3" placeholder="输入提示内容" style="width: 100%; padding: 12px 15px; border-radius: 10px; background: rgba(0, 0, 0, 0.3); border: 1px solid rgba(255, 255, 255, 0.1); color: white; font-size: 1rem;"></textarea>
                    </div>
                </div>
                
                <button class="admin-button secondary" id="addSecurityTipBtn">添加安全提示</button>
                
                <div class="list-items" id="securityTipsList">
                    <!-- 动态生成安全提示列表 -->
                </div>
            </div>
            
            <!-- 友情链接管理 -->
            <div class="admin-section">
                <h3><i class="fas fa-link"></i> <span id="friendLinksTitle">友情链接管理</span></h3>
                <div class="form-row">
                    <div class="form-col">
                        <label for="newFriendName">友情链接名称</label>
                        <input type="text" id="newFriendName" placeholder="输入友情链接名称">
                    </div>
                    <div class="form-col">
                        <label for="newFriendUrl">友情链接URL</label>
                        <input type="text" id="newFriendUrl" placeholder="输入友情链接URL">
                    </div>
                </div>
                
                <button class="admin-button secondary" id="addFriendBtn">添加友情链接</button>
                
                <div class="list-items" id="friendItemsList">
                    <!-- 动态生成友情链接列表 -->
                </div>
            </div>
            
            <!-- 主页内容管理 -->
            <div class="admin-section">
                <h3><i class="fas fa-home"></i> <span id="homePageTitle">主页内容管理</span></h3>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="adminHomeDescription">主页描述</label>
                        <textarea id="adminHomeDescription" rows="4" placeholder="输入主页描述内容" style="width: 100%; padding: 12px 15px; border-radius: 10px; background: rgba(0, 0, 0, 0.3); border: 1px solid rgba(255, 255, 255, 0.1); color: white; font-size: 1rem;"></textarea>
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="adminStat1Value">统计1 数值</label>
                        <input type="text" id="adminStat1Value" placeholder="输入统计1的数值">
                    </div>
                    <div class="form-col">
                        <label for="adminStat1Label">统计1 标签</label>
                        <input type="text" id="adminStat1Label" placeholder="输入统计1的标签">
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="adminStat2Value">统计2 数值</label>
                        <input type="text" id="adminStat2Value" placeholder="输入统计2的数值">
                    </div>
                    <div class="form-col">
                        <label for="adminStat2Label">统计2 标签</label>
                        <input type="text" id="adminStat2Label" placeholder="输入统计2的标签">
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="adminStat3Value">统计3 数值</label>
                        <input type="text" id="adminStat3Value" placeholder="输入统计3的数值">
                    </div>
                    <div class="form-col">
                        <label for="adminStat3Label">统计3 标签</label>
                        <input type="text" id="adminStat3Label" placeholder="输入统计3的标签">
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="adminStat4Value">统计4 数值</label>
                        <input type="text" id="adminStat4Value" placeholder="输入统计4的数值">
                    </div>
                    <div class="form-col">
                        <label for="adminStat4Label">统计4 标签</label>
                        <input type="text" id="adminStat4Label" placeholder="输入统计4的标签">
                    </div>
                </div>
            </div>
            
            <!-- 系统设置 -->
            <div class="admin-section">
                <h3><i class="fas fa-cog"></i> <span id="systemTitleAdmin">系统设置</span></h3>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="adminBeianNumber">备案号</label>
                        <input type="text" id="adminBeianNumber" placeholder="输入网站备案号">
                    </div>
                    <div class="form-col">
                        <label for="adminCopyright">版权信息</label>
                        <input type="text" id="adminCopyright" placeholder="输入版权信息">
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="adminLoginTitle">登录页面标题</label>
                        <input type="text" id="adminLoginTitle" placeholder="输入登录页面标题">
                    </div>
                    <div class="form-col">
                        <label for="adminVerifyTitle">验证页面标题</label>
                        <input type="text" id="adminVerifyTitle" placeholder="输入验证页面标题">
                    </div>
                </div>
                
                <div class="form-row">
                    <div class="form-col">
                        <label for="adminRightClickMessage">右键提示信息</label>
                        <input type="text" id="adminRightClickMessage" placeholder="输入右键提示信息" value="本站禁止使用右键">
                    </div>
                </div>
                
                <button class="admin-button" id="saveSystem">保存系统设置</button>
                <button class="admin-button secondary" id="resetAll">恢复默认设置</button>
                <button class="admin-button secondary" id="exportData">导出数据</button>
                <button class="admin-button secondary" id="importData">导入数据</button>
            </div>
            
            <div class="admin-footer">
                <button class="admin-button" id="saveAll">保存所有设置</button>
            </div>
            
            <!-- 管理后台页脚 -->
            <div class="admin-panel-footer">
                <p id="adminCopyrightText">低调的黑客 © 2026 版权所有</p>
                <div class="admin-panel-footer-beian">
                    <i class="fas fa-shield-alt police-badge"></i>
                    <span id="adminBeianNumberText">赣公网安备36010502011814号</span>
                </div>
            </div>
        </div>
    </div>
    
    <!-- 人机验证页面 -->
    <div id="verification-page">
        <div class="verification-box">
            <div class="verification-logo">
                <i class="fas fa-user-secret"></i>
            </div>
            <h1 class="verification-title" id="verifyTitle">身份验证</h1>
            <p class="verification-subtitle" id="verifySubtitle">请完成验证以访问博客</p>
            
            <div class="slider-container">
                <div class="slider-track">
                    <div class="slider-text" id="sliderText">滑动以验证身份</div>
                    <div class="slider-fill" id="sliderFill"></div>
                    <div class="slider-handle" id="sliderHandle">
                        <i class="fas fa-arrow-right"></i>
                    </div>
                </div>
            </div>
            
            <p class="verification-instruction" id="verifyInstruction">向右滑动滑块完成验证</p>
            <button class="verify-button" id="verifyButton" disabled id="verifyBtnText">验证中...</button>
        </div>
        
        <!-- 验证页面页脚 -->
        <div class="verification-footer">
            <p id="verifyCopyright">低调的黑客 © 2026 版权所有</p>
            <div class="verification-footer-beian">
                <i class="fas fa-shield-alt police-badge"></i>
                <span id="verifyBeianNumber">赣公网安备36010502011814号</span>
            </div>
        </div>
    </div>
    
    <!-- 主页面 -->
    <div id="home-page">
        <div class="home-container">
            <h1 class="home-title" id="homeTitle">低调的黑客-网络安全空间</h1>
            <p class="home-subtitle" id="homeSubtitle">守护数字世界的安全</p>
            
            <div class="home-description" id="homeDescription">
                欢迎来到我的网络安全空间。我是一位10后网络安全爱好者，专注于渗透测试、漏洞研究、安全防御与加密技术。在这里，我将分享网络安全知识、技术实践和行业洞察，与您一同探索数字世界的边界。
            </div>
            
            <div class="home-stats" id="homeStats">
                <!-- 动态生成统计信息 -->
            </div>
            
            <div class="home-buttons">
                <button class="circular-action-btn" id="exploreBtn">
                    <span>开始探索</span>
                </button>
            </div>
            
            <!-- 主页页脚 -->
            <div class="home-footer">
                <div class="home-footer-content">
                    <div class="home-footer-copyright" id="homeCopyright">低调的黑客 © 2026 版权所有</div>
                    <div class="home-footer-beian">
                        <i class="fas fa-shield-alt police-badge"></i>
                        <span id="beianNumber">赣公网安备36010502011814号</span>
                    </div>
                    <div class="home-footer-admin">
                        <a href="#" id="adminFooterBtn">
                            <i class="fas fa-user-shield"></i>
                            <span id="adminFooterText">管理后台</span>
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- 探索页面 -->
    <div id="explore-page">
        <div class="explore-container">
            <div class="explore-header">
                <h1 class="explore-title" id="explorePageTitle">低调的黑客 - 网络安全空间</h1>
                <a href="#" class="back-to-home" id="backToHome">
                    <i class="fas fa-arrow-left"></i> 返回主页
                </a>
            </div>
            
            <!-- 个人资料区域 -->
            <div class="profile-section" id="profileSection">
                <!-- 动态生成个人资料 -->
            </div>
            
            <!-- 安全提示区域 -->
            <div class="security-tips-section" id="securityTipsSection">
                <h2 class="section-title" id="securityTipsTitlePage">网络安全小贴士</h2>
                <div class="security-tips-list" id="securityTipsListContainer">
                    <!-- 动态生成安全提示卡片 -->
                </div>
            </div>
            
            <!-- 联系我区域 -->
            <div class="contact-section" id="contactSection">
                <h2 class="section-title" id="contactTitle">联系我</h2>
                <div class="contact-buttons-container" id="contactButtonsContainer">
                    <!-- 动态生成联系我按钮 -->
                </div>
            </div>
            
            <!-- 友情链接区域 -->
            <div class="friend-links-container" id="friendLinksContainer">
                <h3 id="friendTitle">友情链接</h3>
                <!-- 动态生成友情链接 -->
            </div>
            
            <!-- 探索页面页脚 -->
            <div class="explore-footer">
                <p id="exploreCopyright">低调的黑客 © 2026 版权所有</p>
                <div class="explore-footer-beian">
                    <i class="fas fa-shield-alt police-badge"></i>
                    <span id="exploreBeianNumber">赣公网安备36010502011814号</span>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 默认设置 - 保存在代码中
        const defaultSettings = {
            profile: {
                name: "低调的黑客",
                tagline: "网络安全空间",
                avatar: "",
                description: "10后 · 网络安全爱好者\n探索数字世界的边界，守护网络空间的安全。\n专注于渗透测试、漏洞研究、安全防御与加密技术。\n在虚拟与现实之间，寻找技术的诗意。",
                additionalFields: []
            },
            contacts: [
                { 
                    name: "邮箱", 
                    value: "kali0914@yeah.net",
                    url: "mailto:kali0914@yeah.net", 
                    icon: "fas fa-envelope"
                },
                { 
                    name: "微信", 
                    value: "扫描二维码添加",
                    url: "#", 
                    icon: "fab fa-weixin"
                }
            ],
            securityTips: [
                { 
                    title: "密码安全", 
                    content: "定期更换强密码，避免使用简单密码，推荐使用密码管理器生成和存储密码。" 
                },
                { 
                    title: "双重认证", 
                    content: "为重要账户启用双重认证（2FA），增加账户安全性。" 
                },
                { 
                    title: "软件更新", 
                    content: "保持操作系统和软件及时更新，修复安全漏洞。" 
                },
                { 
                    title: "数据备份", 
                    content: "定期备份重要数据，使用云存储和外部硬盘双重备份。" 
                },
                { 
                    title: "警惕钓鱼", 
                    content: "不点击可疑链接，不下载不明附件，谨慎对待索要个人信息的要求。" 
                }
            ],
            friendLinks: [
                { name: "一位苹果软件开发者", url: "https://iamadman.com" }
            ],
            homePage: {
                title: "低调的黑客-网络安全空间",
                subtitle: "守护数字世界的安全",
                description: "欢迎来到我的网络安全空间。我是一位10后网络安全爱好者，专注于渗透测试、漏洞研究、安全防御与加密技术。在这里，我将分享网络安全知识、技术实践和行业洞察，与您一同探索数字世界的边界。",
                stats: [
                    { value: "3+", label: "年安全研究" },
                    { value: "50+", label: "技术文章" },
                    { value: "100+", label: "项目实践" },
                    { value: "∞", label: "探索精神" }
                ]
            },
            system: {
                beianNumber: "赣公网安备36010502011814号",
                copyright: "低调的黑客 © 2026 版权所有",
                loginTitle: "管理后台登录",
                verifyTitle: "身份验证",
                rightClickMessage: "本站禁止使用右键"
            }
        };

        // 图标选项
        const iconOptions = [
            "fas fa-envelope", "fab fa-weixin", "fab fa-qq", "fas fa-phone", "fas fa-comment",
            "fas fa-paper-plane", "fas fa-globe", "fas fa-link", "fas fa-user", "fas fa-users",
            "fas fa-code", "fas fa-terminal", "fas fa-key", "fas fa-shield-alt", "fas fa-lock",
            "fas fa-unlock", "fas fa-bug", "fas fa-microchip", "fas fa-server", "fas fa-network-wired",
            "fas fa-database", "fas fa-mobile", "fab fa-github", "fab fa-telegram", "fab fa-weibo",
            "fab fa-twitter", "fab fa-facebook", "fab fa-instagram", "fab fa-linkedin", "fab fa-youtube"
        ];

        // 当前设置 - 从localStorage加载或使用默认设置
        let currentSettings = {...defaultSettings};
        
        // DOM元素
        const verificationPage = document.getElementById('verification-page');
        const homePage = document.getElementById('home-page');
        const explorePage = document.getElementById('explore-page');
        const sliderHandle = document.getElementById('sliderHandle');
        const sliderFill = document.getElementById('sliderFill');
        const verifyButton = document.getElementById('verifyButton');
        const sliderTrack = document.querySelector('.slider-track');
        const loginModal = document.getElementById('loginModal');
        const closeLogin = document.getElementById('closeLogin');
        const usernameInput = document.getElementById('username');
        const passwordInput = document.getElementById('password');
        const loginButton = document.getElementById('loginButton');
        const loginMessage = document.getElementById('loginMessage');
        const adminPanel = document.getElementById('adminPanel');
        const closeAdmin = document.getElementById('closeAdmin');
        const adminFooterBtn = document.getElementById('adminFooterBtn');
        const exploreBtn = document.getElementById('exploreBtn');
        const backToHome = document.getElementById('backToHome');
        const rightClickWarning = document.getElementById('rightClickWarning');
        
        // 管理后台表单元素
        const adminName = document.getElementById('adminName');
        const adminTagline = document.getElementById('adminTagline');
        const adminAvatar = document.getElementById('adminAvatar');
        const adminDescription = document.getElementById('adminDescription');
        const avatarImgPreview = document.getElementById('avatarImgPreview');
        const avatarPreview = document.getElementById('avatarPreview');
        const adminBeianNumber = document.getElementById('adminBeianNumber');
        const adminCopyright = document.getElementById('adminCopyright');
        const adminLoginTitle = document.getElementById('adminLoginTitle');
        const adminVerifyTitle = document.getElementById('adminVerifyTitle');
        const adminRightClickMessage = document.getElementById('adminRightClickMessage');
        const adminHomeDescription = document.getElementById('adminHomeDescription');
        const adminStat1Value = document.getElementById('adminStat1Value');
        const adminStat1Label = document.getElementById('adminStat1Label');
        const adminStat2Value = document.getElementById('adminStat2Value');
        const adminStat2Label = document.getElementById('adminStat2Label');
        const adminStat3Value = document.getElementById('adminStat3Value');
        const adminStat3Label = document.getElementById('adminStat3Label');
        const adminStat4Value = document.getElementById('adminStat4Value');
        const adminStat4Label = document.getElementById('adminStat4Label');
        
        // 联系我管理表单元素
        const newContactName = document.getElementById('newContactName');
        const newContactValue = document.getElementById('newContactValue');
        const newContactUrl = document.getElementById('newContactUrl');
        const contactIconSelector = document.getElementById('contactIconSelector');
        const customIconUrl = document.getElementById('customIconUrl');
        const customIconPreview = document.getElementById('customIconPreview');
        const addContactBtn = document.getElementById('addContactBtn');
        const contactItemsList = document.getElementById('contactItemsList');
        
        // 个人资料管理
        const newProfileFieldName = document.getElementById('newProfileFieldName');
        const newProfileFieldValue = document.getElementById('newProfileFieldValue');
        const addProfileFieldBtn = document.getElementById('addProfileFieldBtn');
        const profileFieldsList = document.getElementById('profileFieldsList');
        
        // 安全提示管理
        const newSecurityTipTitle = document.getElementById('newSecurityTipTitle');
        const newSecurityTipContent = document.getElementById('newSecurityTipContent');
        const addSecurityTipBtn = document.getElementById('addSecurityTipBtn');
        const securityTipsList = document.getElementById('securityTipsList');
        
        // 友情链接管理
        const newFriendName = document.getElementById('newFriendName');
        const newFriendUrl = document.getElementById('newFriendUrl');
        const addFriendBtn = document.getElementById('addFriendBtn');
        const friendItemsList = document.getElementById('friendItemsList');
        
        // 保存按钮
        const saveSystemBtn = document.getElementById('saveSystem');
        const saveAllBtn = document.getElementById('saveAll');
        const resetAllBtn = document.getElementById('resetAll');
        const exportDataBtn = document.getElementById('exportData');
        const importDataBtn = document.getElementById('importData');
        
        // 页面元素
        const profileSection = document.getElementById('profileSection');
        const securityTipsListContainer = document.getElementById('securityTipsListContainer');
        const contactButtonsContainer = document.getElementById('contactButtonsContainer');
        const friendLinksContainer = document.getElementById('friendLinksContainer');
        
        // 页脚和版权信息元素
        const homeTitle = document.getElementById('homeTitle');
        const homeSubtitle = document.getElementById('homeSubtitle');
        const homeDescription = document.getElementById('homeDescription');
        const homeStats = document.getElementById('homeStats');
        const homeCopyright = document.getElementById('homeCopyright');
        const beianNumber = document.getElementById('beianNumber');
        const adminCopyrightText = document.getElementById('adminCopyrightText');
        const adminBeianNumberText = document.getElementById('adminBeianNumberText');
        const verifyCopyright = document.getElementById('verifyCopyright');
        const verifyBeianNumber = document.getElementById('verifyBeianNumber');
        const exploreCopyright = document.getElementById('exploreCopyright');
        const exploreBeianNumber = document.getElementById('exploreBeianNumber');
        const explorePageTitle = document.getElementById('explorePageTitle');
        const securityTipsTitlePage = document.getElementById('securityTipsTitlePage');
        const contactTitle = document.getElementById('contactTitle');
        const loginTitle = document.getElementById('loginTitle');
        const verifyTitle = document.getElementById('verifyTitle');
        
        let isVerified = false;
        let sliderWidth = 0;
        const trackWidth = sliderTrack.offsetWidth - sliderHandle.offsetWidth;
        
        // 登录凭据
        const ADMIN_USERNAME = 'kali0914';
        const ADMIN_PASSWORD = '@kali0914';
        
        // 选中的图标
        let selectedContactIcon = 'fas fa-envelope';
        let customIconUrlValue = '';
        
        // 初始化
        function init() {
            // 设置基于时间的山峰背景
            setTimeBasedMountainBackground();
            
            // 设置右键禁用
            setupRightClickProtection();
            
            // 加载设置
            loadSettings();
            
            // 初始化图标选择器
            initIconSelector();
            
            // 添加事件监听器
            setupEventListeners();
            
            // 更新所有页面内容
            updateAllPages();
        }
        
        // 设置基于时间的山峰背景
        function setTimeBasedMountainBackground() {
            const now = new Date();
            const hour = now.getHours();
            let bgClass = '';
            
            // 根据北京时间设置山峰背景
            if (hour >= 5 && hour < 9) {
                bgClass = 'bg-morning-mountain'; // 早晨 5:00-8:59
            } else if (hour >= 9 && hour < 12) {
                bgClass = 'bg-noon-mountain'; // 上午 9:00-11:59
            } else if (hour >= 12 && hour < 17) {
                bgClass = 'bg-afternoon-mountain'; // 下午 12:00-16:59
            } else if (hour >= 17 && hour < 20) {
                bgClass = 'bg-evening-mountain'; // 傍晚 17:00-19:59
            } else {
                bgClass = 'bg-night-mountain'; // 夜晚 20:00-4:59
            }
            
            // 为body设置背景类
            document.body.className = bgClass;
            
            // 1小时后再次检查时间
            setTimeout(setTimeBasedMountainBackground, 3600000); // 1小时
        }
        
        // 设置右键禁用保护
        function setupRightClickProtection() {
            // 禁用右键菜单
            document.addEventListener('contextmenu', function(e) {
                e.preventDefault();
                showRightClickWarning();
                return false;
            });
            
            // 禁用文本选择
            document.addEventListener('selectstart', function(e) {
                e.preventDefault();
                return false;
            });
            
            // 禁用拖拽
            document.addEventListener('dragstart', function(e) {
                e.preventDefault();
                return false;
            });
            
            // 禁用复制、剪切、粘贴
            document.addEventListener('copy', function(e) {
                e.preventDefault();
                return false;
            });
            
            document.addEventListener('cut', function(e) {
                e.preventDefault();
                return false;
            });
            
            document.addEventListener('paste', function(e) {
                e.preventDefault();
                return false;
            });
        }
        
        // 显示右键警告
        function showRightClickWarning() {
            rightClickWarning.style.display = 'block';
            
            // 更新警告消息
            const warningMessage = document.querySelector('#rightClickWarning p');
            if (warningMessage) {
                warningMessage.textContent = currentSettings.system.rightClickMessage;
            }
            
            // 3秒后隐藏警告
            setTimeout(function() {
                rightClickWarning.style.display = 'none';
            }, 3000);
        }
        
        // 更新所有页面内容
        function updateAllPages() {
            // 更新主页
            updateHomePage();
            
            // 更新探索页面
            updateExplorePage();
            
            // 更新管理后台表单
            updateAdminForm();
            
            // 更新系统信息
            updateSystemInfo();
        }
        
        // 更新系统信息
        function updateSystemInfo() {
            // 更新备案信息
            beianNumber.textContent = currentSettings.system.beianNumber;
            adminBeianNumberText.textContent = currentSettings.system.beianNumber;
            verifyBeianNumber.textContent = currentSettings.system.beianNumber;
            exploreBeianNumber.textContent = currentSettings.system.beianNumber;
            adminBeianNumber.value = currentSettings.system.beianNumber;
            
            // 更新版权信息
            homeCopyright.textContent = currentSettings.system.copyright;
            adminCopyrightText.textContent = currentSettings.system.copyright;
            verifyCopyright.textContent = currentSettings.system.copyright;
            exploreCopyright.textContent = currentSettings.system.copyright;
            adminCopyright.value = currentSettings.system.copyright;
            
            // 更新页面标题
            loginTitle.textContent = currentSettings.system.loginTitle;
            verifyTitle.textContent = currentSettings.system.verifyTitle;
            adminLoginTitle.value = currentSettings.system.loginTitle;
            adminVerifyTitle.value = currentSettings.system.verifyTitle;
            
            // 更新右键提示信息
            adminRightClickMessage.value = currentSettings.system.rightClickMessage;
        }
        
        // 加载设置
        function loadSettings() {
            const savedSettings = localStorage.getItem('blogSettings');
            if (savedSettings) {
                try {
                    const parsedSettings = JSON.parse(savedSettings);
                    
                    // 合并设置，确保新字段存在
                    currentSettings = {...defaultSettings};
                    
                    // 逐个合并顶级属性
                    if (parsedSettings.profile) {
                        currentSettings.profile = {...currentSettings.profile, ...parsedSettings.profile};
                        // 确保additionalFields存在
                        if (!currentSettings.profile.additionalFields) {
                            currentSettings.profile.additionalFields = [];
                        }
                    }
                    
                    if (parsedSettings.contacts && Array.isArray(parsedSettings.contacts)) {
                        // 兼容旧数据：如果contacts没有value字段，从url中提取
                        currentSettings.contacts = parsedSettings.contacts.map(contact => {
                            if (!contact.value) {
                                // 从url中提取value
                                if (contact.url.startsWith('mailto:')) {
                                    contact.value = contact.url.replace('mailto:', '');
                                } else if (contact.url === '#') {
                                    contact.value = '未配置';
                                } else {
                                    contact.value = contact.url;
                                }
                            }
                            return contact;
                        });
                    }
                    
                    if (parsedSettings.securityTips && Array.isArray(parsedSettings.securityTips)) {
                        currentSettings.securityTips = parsedSettings.securityTips;
                    }
                    
                    if (parsedSettings.friendLinks && Array.isArray(parsedSettings.friendLinks)) {
                        currentSettings.friendLinks = parsedSettings.friendLinks;
                    }
                    
                    if (parsedSettings.homePage) {
                        currentSettings.homePage = {...currentSettings.homePage, ...parsedSettings.homePage};
                    }
                    
                    if (parsedSettings.system) {
                        currentSettings.system = {...currentSettings.system, ...parsedSettings.system};
                    }
                } catch (e) {
                    console.error('加载设置失败:', e);
                    currentSettings = {...defaultSettings};
                }
            } else {
                // 如果没有保存的设置，使用默认设置
                currentSettings = {...defaultSettings};
            }
        }
        
        // 更新主页面
        function updateHomePage() {
            // 更新标题
            homeTitle.textContent = currentSettings.homePage.title;
            homeSubtitle.textContent = currentSettings.homePage.subtitle;
            homeDescription.textContent = currentSettings.homePage.description;
            
            // 更新统计信息
            updateHomeStats();
            
            // 更新系统信息
            updateSystemInfo();
        }
        
        // 更新主页统计信息
        function updateHomeStats() {
            homeStats.innerHTML = '';
            
            if (!currentSettings.homePage.stats || currentSettings.homePage.stats.length === 0) {
                return;
            }
            
            currentSettings.homePage.stats.forEach(stat => {
                const statItem = document.createElement('div');
                statItem.className = 'stat-item';
                
                statItem.innerHTML = `
                    <div class="stat-value">${stat.value}</div>
                    <div class="stat-label">${stat.label}</div>
                `;
                
                homeStats.appendChild(statItem);
            });
        }
        
        // 更新探索页面
        function updateExplorePage() {
            // 更新探索页面标题
            explorePageTitle.textContent = currentSettings.profile.name + " - " + currentSettings.profile.tagline;
            
            // 更新个人资料区域
            updateProfileSection();
            
            // 更新安全提示区域
            updateSecurityTipsSection();
            
            // 更新联系我区域
            updateContactSection();
            
            // 更新友情链接区域
            updateFriendLinksSection();
            
            // 更新系统信息
            updateSystemInfo();
        }
        
        // 更新个人资料区域
        function updateProfileSection() {
            profileSection.innerHTML = '';
            
            // 创建个人资料HTML
            const profileHTML = `
                <div class="profile-header">
                    <div class="profile-avatar" id="profileAvatar">
                        <img id="profileAvatarImg" src="${currentSettings.profile.avatar}" alt="头像">
                        <i class="fas fa-user-secret"></i>
                    </div>
                    <div class="profile-info">
                        <h2>${currentSettings.profile.name}</h2>
                        <p>${currentSettings.profile.tagline}</p>
                    </div>
                </div>
                <div class="profile-content">
                    ${formatDescription(currentSettings.profile.description)}
                    ${generateAdditionalFieldsHTML()}
                </div>
            `;
            
            profileSection.innerHTML = profileHTML;
            
            // 更新头像显示
            const profileAvatarImg = document.getElementById('profileAvatarImg');
            const profileAvatarIcon = document.getElementById('profileAvatar').querySelector('i');
            if (currentSettings.profile.avatar && currentSettings.profile.avatar.trim() !== '') {
                profileAvatarImg.style.display = 'block';
                profileAvatarIcon.style.display = 'none';
            } else {
                profileAvatarImg.style.display = 'none';
                profileAvatarIcon.style.display = 'block';
            }
        }
        
        // 格式化描述文本（将换行符转换为段落）
        function formatDescription(text) {
            if (!text) return '';
            
            const lines = text.split('\n');
            let html = '';
            
            lines.forEach(line => {
                if (line.trim() !== '') {
                    html += `<p>${line}</p>`;
                }
            });
            
            return html;
        }
        
        // 生成附加字段HTML
        function generateAdditionalFieldsHTML() {
            if (!currentSettings.profile.additionalFields || currentSettings.profile.additionalFields.length === 0) {
                return '';
            }
            
            let html = '';
            currentSettings.profile.additionalFields.forEach(field => {
                html += `<p><strong>${field.name}:</strong> ${field.value}</p>`;
            });
            
            return html;
        }
        
        // 更新安全提示区域
        function updateSecurityTipsSection() {
            securityTipsListContainer.innerHTML = '';
            
            if (!currentSettings.securityTips || currentSettings.securityTips.length === 0) {
                securityTipsListContainer.innerHTML = '<p style="color: #aaa; text-align: center;">暂无安全提示</p>';
                return;
            }
            
            currentSettings.securityTips.forEach(tip => {
                const tipCard = document.createElement('div');
                tipCard.className = 'security-tip-card';
                
                tipCard.innerHTML = `
                    <h4><i class="fas fa-shield-alt"></i> ${tip.title}</h4>
                    <p>${tip.content}</p>
                `;
                
                securityTipsListContainer.appendChild(tipCard);
            });
        }
        
        // 更新联系我区域 - 只显示联系方式，不显示URL
        function updateContactSection() {
            contactButtonsContainer.innerHTML = '';
            
            if (!currentSettings.contacts || currentSettings.contacts.length === 0) {
                contactButtonsContainer.innerHTML = '<p style="color: #aaa; text-align: center;">暂无联系信息</p>';
                return;
            }
            
            currentSettings.contacts.forEach(contact => {
                const contactBtn = document.createElement('a');
                contactBtn.href = contact.url === '#' ? 'javascript:void(0)' : contact.url;
                contactBtn.className = 'contact-btn';
                contactBtn.title = contact.name;
                
                // 如果是邮件链接，则不打开新窗口
                if (contact.url.startsWith('mailto:')) {
                    contactBtn.target = '_self';
                } else if (contact.url !== '#') {
                    contactBtn.target = '_blank';
                }
                
                if (contact.url === '#') {
                    contactBtn.addEventListener('click', (e) => {
                        e.preventDefault();
                        showMessage('链接尚未配置', 'error');
                    });
                }
                
                const icon = document.createElement('i');
                if (contact.icon.startsWith('http') || contact.icon.startsWith('data:')) {
                    // 自定义图标
                    const img = document.createElement('img');
                    img.src = contact.icon;
                    img.alt = contact.name;
                    img.style.width = '1.8rem';
                    img.style.height = '1.8rem';
                    icon.appendChild(img);
                } else {
                    // FontAwesome图标
                    icon.className = contact.icon;
                }
                
                contactBtn.appendChild(icon);
                
                const contentDiv = document.createElement('div');
                
                const nameDiv = document.createElement('div');
                nameDiv.textContent = contact.name;
                contentDiv.appendChild(nameDiv);
                
                // 只显示值，不显示URL
                const valueDiv = document.createElement('div');
                valueDiv.className = 'contact-value';
                valueDiv.textContent = contact.value || '未配置';
                contentDiv.appendChild(valueDiv);
                
                contactBtn.appendChild(contentDiv);
                contactButtonsContainer.appendChild(contactBtn);
            });
        }
        
        // 更新友情链接区域
        function updateFriendLinksSection() {
            const container = friendLinksContainer;
            const title = container.querySelector('h3');
            
            // 清空现有内容（除了标题）
            while (container.children.length > 1) {
                container.removeChild(container.lastChild);
            }
            
            if (!currentSettings.friendLinks || currentSettings.friendLinks.length === 0) {
                const emptyMsg = document.createElement('p');
                emptyMsg.style.color = '#aaa';
                emptyMsg.style.textAlign = 'center';
                emptyMsg.style.width = '100%';
                emptyMsg.textContent = '暂无友情链接';
                container.appendChild(emptyMsg);
                return;
            }
            
            currentSettings.friendLinks.forEach(friend => {
                const friendLink = document.createElement('a');
                friendLink.href = friend.url;
                friendLink.className = 'friend-link-item';
                friendLink.target = '_blank';
                friendLink.rel = 'noopener noreferrer';
                
                const icon = document.createElement('i');
                icon.className = 'fas fa-external-link-alt';
                friendLink.appendChild(icon);
                
                const text = document.createElement('span');
                text.textContent = friend.name;
                friendLink.appendChild(text);
                
                container.appendChild(friendLink);
            });
        }
        
        // 更新管理后台表单
        function updateAdminForm() {
            // 个人资料
            adminName.value = currentSettings.profile.name;
            adminTagline.value = currentSettings.profile.tagline;
            adminAvatar.value = currentSettings.profile.avatar;
            adminDescription.value = currentSettings.profile.description;
            
            // 主页内容
            adminHomeDescription.value = currentSettings.homePage.description;
            
            if (currentSettings.homePage.stats && currentSettings.homePage.stats.length >= 4) {
                adminStat1Value.value = currentSettings.homePage.stats[0].value;
                adminStat1Label.value = currentSettings.homePage.stats[0].label;
                adminStat2Value.value = currentSettings.homePage.stats[1].value;
                adminStat2Label.value = currentSettings.homePage.stats[1].label;
                adminStat3Value.value = currentSettings.homePage.stats[2].value;
                adminStat3Label.value = currentSettings.homePage.stats[2].label;
                adminStat4Value.value = currentSettings.homePage.stats[3].value;
                adminStat4Label.value = currentSettings.homePage.stats[3].label;
            }
            
            // 更新头像预览
            updateAvatarPreview();
            
            // 更新个人信息字段列表
            updateProfileFieldsList();
            
            // 更新联系信息列表
            updateContactItemsList();
            
            // 更新安全提示列表
            updateSecurityTipsList();
            
            // 更新友情链接列表
            updateFriendItemsList();
        }
        
        // 初始化图标选择器
        function initIconSelector() {
            contactIconSelector.innerHTML = '';
            iconOptions.forEach(icon => {
                const iconOption = document.createElement('div');
                iconOption.className = 'icon-option';
                if (icon === selectedContactIcon) {
                    iconOption.classList.add('selected');
                }
                
                const iconElement = document.createElement('i');
                iconElement.className = icon;
                iconOption.appendChild(iconElement);
                
                iconOption.addEventListener('click', () => {
                    document.querySelectorAll('#contactIconSelector .icon-option').forEach(opt => {
                        opt.classList.remove('selected');
                    });
                    iconOption.classList.add('selected');
                    selectedContactIcon = icon;
                    customIconUrl.value = '';
                    customIconPreview.innerHTML = '';
                });
                
                contactIconSelector.appendChild(iconOption);
            });
            
            // 自定义图标URL输入事件
            customIconUrl.addEventListener('input', function() {
                customIconUrlValue = this.value;
                updateCustomIconPreview();
            });
        }
        
        // 更新自定义图标预览
        function updateCustomIconPreview() {
            customIconPreview.innerHTML = '';
            
            if (customIconUrlValue && (customIconUrlValue.startsWith('http') || customIconUrlValue.startsWith('data:'))) {
                const img = document.createElement('img');
                img.src = customIconUrlValue;
                img.alt = '自定义图标';
                img.onerror = function() {
                    customIconPreview.innerHTML = '<p style="color: #e74c3c; font-size: 0.8rem;">图片加载失败</p>';
                };
                customIconPreview.appendChild(img);
            }
        }
        
        // 更新头像预览
        function updateAvatarPreview() {
            if (currentSettings.profile.avatar && currentSettings.profile.avatar.trim() !== '') {
                avatarImgPreview.src = currentSettings.profile.avatar;
                avatarImgPreview.style.display = 'block';
                avatarPreview.querySelector('i').style.display = 'none';
            } else {
                avatarImgPreview.style.display = 'none';
                avatarPreview.querySelector('i').style.display = 'block';
            }
        }
        
        // 更新个人信息字段列表
        function updateProfileFieldsList() {
            profileFieldsList.innerHTML = '';
            
            if (!currentSettings.profile.additionalFields || currentSettings.profile.additionalFields.length === 0) {
                profileFieldsList.innerHTML = '<p style="color: #aaa; text-align: center; padding: 15px;">暂无附加信息</p>';
                return;
            }
            
            currentSettings.profile.additionalFields.forEach((field, index) => {
                const item = document.createElement('div');
                item.className = 'list-item';
                
                const fieldInfo = document.createElement('div');
                fieldInfo.style.flex = '1';
                fieldInfo.innerHTML = `
                    <div><strong>${field.name}</strong></div>
                    <div style="color: #aaa; font-size: 0.9rem;">${field.value}</div>
                `;
                
                item.appendChild(fieldInfo);
                
                const controls = document.createElement('div');
                controls.className = 'list-item-controls';
                
                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'admin-button small danger';
                deleteBtn.innerHTML = '<i class="fas fa-trash"></i> 删除';
                deleteBtn.addEventListener('click', () => {
                    currentSettings.profile.additionalFields.splice(index, 1);
                    updateProfileFieldsList();
                    updateProfileSection();
                    showMessage('个人信息字段已删除', 'success');
                });
                
                controls.appendChild(deleteBtn);
                item.appendChild(controls);
                
                profileFieldsList.appendChild(item);
            });
        }
        
        // 更新联系信息列表
        function updateContactItemsList() {
            contactItemsList.innerHTML = '';
            
            if (!currentSettings.contacts || currentSettings.contacts.length === 0) {
                contactItemsList.innerHTML = '<p style="color: #aaa; text-align: center; padding: 15px;">暂无联系信息</p>';
                return;
            }
            
            currentSettings.contacts.forEach((contact, index) => {
                const item = document.createElement('div');
                item.className = 'list-item';
                
                const contactInfo = document.createElement('div');
                contactInfo.style.flex = '1';
                
                let iconHTML = '';
                if (contact.icon.startsWith('http') || contact.icon.startsWith('data:')) {
                    iconHTML = `<img src="${contact.icon}" alt="${contact.name}" style="width: 20px; height: 20px; vertical-align: middle; margin-right: 5px;">`;
                } else {
                    iconHTML = `<i class="${contact.icon}" style="margin-right: 5px;"></i>`;
                }
                
                contactInfo.innerHTML = `
                    <div><strong>${iconHTML} ${contact.name}</strong></div>
                    <div style="color: #aaa; font-size: 0.9rem;">显示值: ${contact.value || '未配置'}</div>
                    <div style="color: #666; font-size: 0.8rem;">实际链接: ${contact.url}</div>
                `;
                
                item.appendChild(contactInfo);
                
                const controls = document.createElement('div');
                controls.className = 'list-item-controls';
                
                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'admin-button small danger';
                deleteBtn.innerHTML = '<i class="fas fa-trash"></i> 删除';
                deleteBtn.addEventListener('click', () => {
                    currentSettings.contacts.splice(index, 1);
                    updateContactItemsList();
                    updateContactSection();
                    showMessage('联系信息已删除', 'success');
                });
                
                controls.appendChild(deleteBtn);
                item.appendChild(controls);
                
                contactItemsList.appendChild(item);
            });
        }
        
        // 更新安全提示列表
        function updateSecurityTipsList() {
            securityTipsList.innerHTML = '';
            
            if (!currentSettings.securityTips || currentSettings.securityTips.length === 0) {
                securityTipsList.innerHTML = '<p style="color: #aaa; text-align: center; padding: 15px;">暂无安全提示</p>';
                return;
            }
            
            currentSettings.securityTips.forEach((tip, index) => {
                const item = document.createElement('div');
                item.className = 'list-item';
                
                const tipInfo = document.createElement('div');
                tipInfo.style.flex = '1';
                tipInfo.innerHTML = `
                    <div><strong>${tip.title}</strong></div>
                    <div style="color: #aaa; font-size: 0.9rem;">${tip.content}</div>
                `;
                
                item.appendChild(tipInfo);
                
                const controls = document.createElement('div');
                controls.className = 'list-item-controls';
                
                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'admin-button small danger';
                deleteBtn.innerHTML = '<i class="fas fa-trash"></i> 删除';
                deleteBtn.addEventListener('click', () => {
                    currentSettings.securityTips.splice(index, 1);
                    updateSecurityTipsList();
                    updateSecurityTipsSection();
                    showMessage('安全提示已删除', 'success');
                });
                
                controls.appendChild(deleteBtn);
                item.appendChild(controls);
                
                securityTipsList.appendChild(item);
            });
        }
        
        // 更新友情链接列表
        function updateFriendItemsList() {
            friendItemsList.innerHTML = '';
            
            if (!currentSettings.friendLinks || currentSettings.friendLinks.length === 0) {
                friendItemsList.innerHTML = '<p style="color: #aaa; text-align: center; padding: 15px;">暂无友情链接</p>';
                return;
            }
            
            currentSettings.friendLinks.forEach((friend, index) => {
                const item = document.createElement('div');
                item.className = 'list-item';
                
                const friendInfo = document.createElement('div');
                friendInfo.style.flex = '1';
                friendInfo.innerHTML = `
                    <div><strong>${friend.name}</strong></div>
                    <div style="color: #aaa; font-size: 0.9rem;">${friend.url}</div>
                `;
                
                item.appendChild(friendInfo);
                
                const controls = document.createElement('div');
                controls.className = 'list-item-controls';
                
                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'admin-button small danger';
                deleteBtn.innerHTML = '<i class="fas fa-trash"></i> 删除';
                deleteBtn.addEventListener('click', () => {
                    currentSettings.friendLinks.splice(index, 1);
                    updateFriendItemsList();
                    updateFriendLinksSection();
                    showMessage('友情链接已删除', 'success');
                });
                
                controls.appendChild(deleteBtn);
                item.appendChild(controls);
                
                friendItemsList.appendChild(item);
            });
        }
        
        // 保存设置到localStorage
        function saveSettings() {
            // 更新当前设置
            currentSettings.profile.name = adminName.value;
            currentSettings.profile.tagline = adminTagline.value;
            currentSettings.profile.avatar = adminAvatar.value;
            currentSettings.profile.description = adminDescription.value;
            
            // 主页内容
            currentSettings.homePage.title = currentSettings.profile.name + "-网络安全空间";
            currentSettings.homePage.subtitle = currentSettings.profile.tagline;
            currentSettings.homePage.description = adminHomeDescription.value;
            
            // 更新统计信息
            currentSettings.homePage.stats = [
                { value: adminStat1Value.value, label: adminStat1Label.value },
                { value: adminStat2Value.value, label: adminStat2Label.value },
                { value: adminStat3Value.value, label: adminStat3Label.value },
                { value: adminStat4Value.value, label: adminStat4Label.value }
            ];
            
            // 系统设置
            currentSettings.system.beianNumber = adminBeianNumber.value;
            currentSettings.system.copyright = adminCopyright.value;
            currentSettings.system.loginTitle = adminLoginTitle.value;
            currentSettings.system.verifyTitle = adminVerifyTitle.value;
            currentSettings.system.rightClickMessage = adminRightClickMessage.value;
            
            // 保存到本地存储
            localStorage.setItem('blogSettings', JSON.stringify(currentSettings));
            
            // 更新所有页面内容
            updateAllPages();
            
            // 显示成功消息
            showMessage('设置已保存！', 'success');
        }
        
        // 显示消息
        function showMessage(text, type) {
            const message = document.createElement('div');
            message.textContent = text;
            message.style.position = 'fixed';
            message.style.top = '20px';
            message.style.right = '20px';
            message.style.background = type === 'success' ? 'rgba(46, 204, 113, 0.9)' : 'rgba(231, 76, 60, 0.9)';
            message.style.color = 'white';
            message.style.padding = '15px 25px';
            message.style.borderRadius = '10px';
            message.style.zIndex = '9999';
            message.style.boxShadow = '0 5px 15px rgba(0, 0, 0, 0.3)';
            
            document.body.appendChild(message);
            
            setTimeout(() => {
                message.remove();
            }, 3000);
        }
        
        // 设置事件监听器
        function setupEventListeners() {
            // 滑块拖动功能
            sliderHandle.addEventListener('mousedown', startDrag);
            sliderHandle.addEventListener('touchstart', startDrag);
            
            // 探索按钮
            exploreBtn.addEventListener('click', function() {
                homePage.style.display = 'none';
                explorePage.style.display = 'block';
            });
            
            // 返回主页按钮
            backToHome.addEventListener('click', function(e) {
                e.preventDefault();
                explorePage.style.display = 'none';
                homePage.style.display = 'block';
            });
            
            // 管理后台功能
            adminFooterBtn.addEventListener('click', function(e) {
                e.preventDefault();
                loginModal.classList.add('active');
                usernameInput.focus();
            });
            
            closeLogin.addEventListener('click', function() {
                loginModal.classList.remove('active');
                resetLoginForm();
            });
            
            // 点击模态框外部关闭
            loginModal.addEventListener('click', function(e) {
                if (e.target === loginModal) {
                    loginModal.classList.remove('active');
                    resetLoginForm();
                }
            });
            
            // 登录功能
            loginButton.addEventListener('click', function() {
                const username = usernameInput.value;
                const password = passwordInput.value;
                
                // 清除之前的信息
                loginMessage.className = 'login-message';
                loginMessage.textContent = '';
                
                // 验证凭据
                if (username === ADMIN_USERNAME && password === ADMIN_PASSWORD) {
                    loginMessage.textContent = '登录成功！正在进入管理后台...';
                    loginMessage.classList.add('success');
                    
                    // 1秒后进入管理后台
                    setTimeout(function() {
                        loginModal.classList.remove('active');
                        resetLoginForm();
                        adminPanel.classList.add('active');
                        homePage.style.display = 'none';
                        explorePage.style.display = 'none';
                        verificationPage.style.display = 'none';
                    }, 1000);
                } else {
                    loginMessage.textContent = '用户名或密码错误！';
                    loginMessage.classList.add('error');
                }
            });
            
            // 按回车键登录
            passwordInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    loginButton.click();
                }
            });
            
            // 关闭管理后台
            closeAdmin.addEventListener('click', function() {
                adminPanel.classList.remove('active');
                homePage.style.display = 'block';
            });
            
            // 头像URL输入事件
            adminAvatar.addEventListener('input', updateAvatarPreview);
            
            // 添加个人信息字段
            addProfileFieldBtn.addEventListener('click', function() {
                const name = newProfileFieldName.value.trim();
                const value = newProfileFieldValue.value.trim();
                
                if (!name || !value) {
                    showMessage('请填写完整的字段信息', 'error');
                    return;
                }
                
                if (!currentSettings.profile.additionalFields) {
                    currentSettings.profile.additionalFields = [];
                }
                
                currentSettings.profile.additionalFields.push({
                    name,
                    value
                });
                
                updateProfileFieldsList();
                updateProfileSection();
                
                newProfileFieldName.value = '';
                newProfileFieldValue.value = '';
                
                showMessage('个人信息字段已添加', 'success');
            });
            
            // 添加联系信息
            addContactBtn.addEventListener('click', function() {
                const name = newContactName.value.trim();
                const value = newContactValue.value.trim();
                const url = newContactUrl.value.trim();
                
                if (!name || !value) {
                    showMessage('请填写完整的联系信息', 'error');
                    return;
                }
                
                // 确定图标
                let icon = selectedContactIcon;
                if (customIconUrlValue) {
                    icon = customIconUrlValue;
                }
                
                currentSettings.contacts.push({
                    name,
                    value,
                    url: url || '#',
                    icon
                });
                
                updateContactItemsList();
                updateContactSection();
                
                newContactName.value = '';
                newContactValue.value = '';
                newContactUrl.value = '';
                customIconUrl.value = '';
                customIconPreview.innerHTML = '';
                
                showMessage('联系信息已添加', 'success');
            });
            
            // 添加安全提示
            addSecurityTipBtn.addEventListener('click', function() {
                const title = newSecurityTipTitle.value.trim();
                const content = newSecurityTipContent.value.trim();
                
                if (!title || !content) {
                    showMessage('请填写完整的安全提示信息', 'error');
                    return;
                }
                
                currentSettings.securityTips.push({
                    title,
                    content
                });
                
                updateSecurityTipsList();
                updateSecurityTipsSection();
                
                newSecurityTipTitle.value = '';
                newSecurityTipContent.value = '';
                
                showMessage('安全提示已添加', 'success');
            });
            
            // 添加友情链接
            addFriendBtn.addEventListener('click', function() {
                const name = newFriendName.value.trim();
                const url = newFriendUrl.value.trim();
                
                if (!name || !url) {
                    showMessage('请填写完整的友情链接信息', 'error');
                    return;
                }
                
                currentSettings.friendLinks.push({
                    name,
                    url
                });
                
                updateFriendItemsList();
                updateFriendLinksSection();
                
                newFriendName.value = '';
                newFriendUrl.value = '';
                
                showMessage('友情链接已添加', 'success');
            });
            
            // 保存按钮事件
            saveSystemBtn.addEventListener('click', function() {
                saveSettings();
            });
            
            saveAllBtn.addEventListener('click', function() {
                saveSettings();
            });
            
            // 重置所有设置
            resetAllBtn.addEventListener('click', function() {
                if (confirm('确定要恢复默认设置吗？这将清除所有自定义设置。')) {
                    currentSettings = {...defaultSettings};
                    localStorage.removeItem('blogSettings');
                    updateAdminForm();
                    updateAllPages();
                    showMessage('已恢复默认设置！', 'success');
                }
            });
            
            // 导出数据
            exportDataBtn.addEventListener('click', function() {
                const dataStr = JSON.stringify(currentSettings, null, 2);
                const dataUri = 'data:application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
                
                const exportFileDefaultName = '博客设置备份.json';
                
                const linkElement = document.createElement('a');
                linkElement.setAttribute('href', dataUri);
                linkElement.setAttribute('download', exportFileDefaultName);
                linkElement.click();
                
                showMessage('设置已导出！', 'success');
            });
            
            // 导入数据
            importDataBtn.addEventListener('click', function() {
                const input = document.createElement('input');
                input.type = 'file';
                input.accept = '.json';
                
                input.onchange = function(e) {
                    const file = e.target.files[0];
                    const reader = new FileReader();
                    
                    reader.onload = function(event) {
                        try {
                            const importedSettings = JSON.parse(event.target.result);
                            currentSettings = importedSettings;
                            localStorage.setItem('blogSettings', JSON.stringify(currentSettings));
                            updateAdminForm();
                            updateAllPages();
                            showMessage('设置已导入！', 'success');
                        } catch (err) {
                            showMessage('导入失败：文件格式不正确', 'error');
                        }
                    };
                    
                    reader.readAsText(file);
                };
                
                input.click();
            });
        }
        
        // 滑块拖动功能
        function startDrag(e) {
            e.preventDefault();
            document.addEventListener('mousemove', onDrag);
            document.addEventListener('touchmove', onDragTouch);
            document.addEventListener('mouseup', stopDrag);
            document.addEventListener('touchend', stopDrag);
        }
        
        function onDrag(e) {
            updateSlider(e.clientX);
        }
        
        function onDragTouch(e) {
            updateSlider(e.touches[0].clientX);
        }
        
        function updateSlider(clientX) {
            const trackRect = sliderTrack.getBoundingClientRect();
            let newWidth = clientX - trackRect.left - (sliderHandle.offsetWidth / 2);
            
            // 限制滑块在轨道范围内
            newWidth = Math.max(0, Math.min(newWidth, trackWidth));
            
            sliderWidth = newWidth;
            sliderHandle.style.left = sliderWidth + 'px';
            sliderFill.style.width = sliderWidth + 'px';
            
            // 检查是否验证成功
            if (sliderWidth >= trackWidth - 5) {
                isVerified = true;
                verifyButton.textContent = '验证成功！正在进入...';
                verifyButton.style.background = "linear-gradient(45deg, #2ecc71, #27ae60)";
                verifyButton.disabled = false;
                
                // 1秒后跳转到主页面
                setTimeout(() => {
                    verificationPage.style.display = 'none';
                    homePage.style.display = 'block';
                }, 1000);
            }
        }
        
        function stopDrag() {
            document.removeEventListener('mousemove', onDrag);
            document.removeEventListener('touchmove', onDragTouch);
            document.removeEventListener('mouseup', stopDrag);
            document.removeEventListener('touchend', stopDrag);
            
            // 如果未验证成功，滑块返回起点
            if (!isVerified && sliderWidth < trackWidth - 5) {
                sliderWidth = 0;
                sliderHandle.style.left = '0';
                sliderFill.style.width = '0';
                verifyButton.textContent = '验证中...';
                verifyButton.disabled = true;
            }
        }
        
        function resetLoginForm() {
            usernameInput.value = '';
            passwordInput.value = '';
            loginMessage.className = 'login-message';
            loginMessage.textContent = '';
        }
        
        // 为验证按钮添加点击事件（备用）
        verifyButton.addEventListener('click', function() {
            if (isVerified) {
                verificationPage.style.display = 'none';
                homePage.style.display = 'block';
            }
        });
        
        // 页面加载完成后初始化
        document.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
