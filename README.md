<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>比赛积分管理系统</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        :root {
            --primary: #4361ee;
            --secondary: #3a0ca3;
            --success: #4cc9f0;
            --danger: #f72585;
            --warning: #f8961e;
            --light: #f8f9fa;
            --dark: #212529;
            --gray: #6c757d;
        }
        
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            padding: 20px;
            color: var(--dark);
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            color: var(--primary);
            margin-bottom: 10px;
        }
        
        .subtitle {
            color: var(--gray);
            font-size: 1.1rem;
        }
        
        .card {
            background: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            padding: 25px;
            margin-bottom: 25px;
            transition: transform 0.3s ease;
        }
        
        .card:hover {
            transform: translateY(-5px);
        }
        
        .card-title {
            font-size: 1.3rem;
            color: var(--primary);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--dark);
        }
        
        input, select, button {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
            transition: all 0.3s;
        }
        
        input:focus, select:focus {
            outline: none;
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
        }
        
        button {
            background: var(--primary);
            color: white;
            border: none;
            cursor: pointer;
            font-weight: 600;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        button:hover {
            background: var(--secondary);
        }
        
        .btn-danger {
            background: var(--danger);
        }
        
        .btn-danger:hover {
            background: #d1144a;
        }
        
        .btn-success {
            background: var(--success);
        }
        
        .btn-success:hover {
            background: #3aa8d0;
        }
        
        .btn-secondary {
            background: var(--gray);
        }
        
        .btn-secondary:hover {
            background: #5a6268;
        }
        
        .row {
            display: flex;
            flex-wrap: wrap;
            margin: 0 -15px;
        }
        
        .col {
            flex: 1;
            padding: 0 15px;
            min-width: 300px;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        
        th, td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid #eee;
        }
        
        th {
            background: var(--light);
            color: var(--dark);
            font-weight: 600;
        }
        
        tr:hover {
            background: rgba(67, 97, 238, 0.05);
        }
        
        .rank-1 {
            background: rgba(255, 215, 0, 0.1);
        }
        
        .rank-2 {
            background: rgba(192, 192, 192, 0.1);
        }
        
        .rank-3 {
            background: rgba(205, 127, 50, 0.1);
        }
        
        .medal {
            display: inline-block;
            width: 24px;
            height: 24px;
            border-radius: 50%;
            text-align: center;
            line-height: 24px;
            font-weight: bold;
            margin-right: 10px;
        }
        
        .gold {
            background: gold;
            color: #b8860b;
        }
        
        .silver {
            background: silver;
            color: #6c757d;
        }
        
        .bronze {
            background: #cd7f32;
            color: white;
        }
        
        .badge {
            display: inline-block;
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
        }
        
        .badge-admin {
            background: var(--primary);
            color: white;
        }
        
        .badge-user {
            background: var(--light);
            color: var(--dark);
        }
        
        .user-info {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }
        
        .avatar {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: var(--primary);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            font-weight: bold;
        }
        
        .stats {
            display: flex;
            gap: 15px;
        }
        
        .stat {
            text-align: center;
            padding: 10px;
            background: var(--light);
            border-radius: 8px;
            flex: 1;
        }
        
        .stat-value {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--primary);
        }
        
        .stat-label {
            font-size: 0.9rem;
            color: var(--gray);
        }
        
        .tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid #ddd;
        }
        
        .tab {
            padding: 10px 20px;
            cursor: pointer;
            font-weight: 600;
            color: var(--gray);
            border-bottom: 3px solid transparent;
        }
        
        .tab.active {
            color: var(--primary);
            border-bottom: 3px solid var(--primary);
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .page {
            display: none;
        }
        
        .page.active {
            display: block;
        }
        
        .nav-buttons {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }
        
        .admin-only {
            display: none;
        }
        
        .admin-logged-in .admin-only {
            display: block;
        }
        
        .user-logged-in .user-actions {
            display: block;
        }
        
        .user-actions {
            display: none;
        }
        
        @media (max-width: 768px) {
            .col {
                flex: 100%;
            }
            
            .row {
                margin: 0;
            }
            
            .stats {
                flex-direction: column;
            }
            
            .nav-buttons {
                flex-direction: column;
                gap: 10px;
            }
            
            .nav-buttons button {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-trophy"></i> 铁拳相扑锦标赛积分管理系统</h1>
            <p class="subtitle">注册账号，查看积分排名</p>
        </header>
        
        <!-- 登录页面 -->
        <div id="login-page" class="page active">
            <div class="row">
                <div class="col">
                    <div class="card">
                        <h2 class="card-title"><i class="fas fa-sign-in-alt"></i> 用户登录</h2>
                        <div class="form-group">
                            <label for="login-username">用户名</label>
                            <input type="text" id="login-username" placeholder="请输入用户名">
                        </div>
                        <div class="form-group">
                            <label for="login-password">密码</label>
                            <input type="password" id="login-password" placeholder="请输入密码">
                        </div>
                        <button id="login-btn"><i class="fas fa-sign-in-alt"></i> 登录系统</button>
                        <p style="text-align: center; margin-top: 15px;">
                            还没有账号？ <a href="#" id="go-to-register">立即注册</a>
                        </p>
                    </div>
                </div>
                
                <div class="col">
                    <div class="card">
                        <h2 class="card-title"><i class="fas fa-info-circle"></i> 系统说明</h2>
                        <p>1. 每个用户可以注册一个唯一的用户名账号。</p>
                        <p>2. 管理员可以给用户分配积分，积分用于比赛排名。</p>
                        <p>3. 系统会实时更新和显示比赛排名。</p>
                        <p>4. 用户名使用自己的游戏ID，带上后缀。</p>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 注册页面 -->
        <div id="register-page" class="page">
            <div class="row">
                <div class="col">
                    <div class="card">
                        <h2 class="card-title"><i class="fas fa-user-plus"></i> 用户注册</h2>
                        <div class="form-group">
                            <label for="username">用户名</label>
                            <input type="text" id="username" placeholder="请输入唯一的用户名">
                        </div>
                        <div class="form-group">
                            <label for="password">密码</label>
                            <input type="password" id="password" placeholder="请输入密码">
                        </div>
                        <div class="form-group">
                            <label for="confirm-password">确认密码</label>
                            <input type="password" id="confirm-password" placeholder="请再次输入密码">
                        </div>
                        <div class="form-group">
                            <label for="admin-code">管理员代码（可选）</label>
                            <input type="password" id="admin-code" placeholder="请输入管理员代码（如需要）">
                            <small style="color: var(--gray);">只有输入正确管理员代码才能注册为管理员</small>
                        </div>
                        <button id="register-btn"><i class="fas fa-user-plus"></i> 注册账号</button>
                        <div class="nav-buttons">
                            <button class="btn-secondary" id="back-to-login"><i class="fas fa-arrow-left"></i> 返回登录</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 用户主页 -->
        <div id="user-home" class="page">
            <div class="card">
                <div class="user-info">
                    <div class="avatar" id="user-avatar">U</div>
                    <div>
                        <h2 id="user-greeting">欢迎，用户！</h2>
                        <p id="user-role">角色：普通用户</p>
                    </div>
                </div>
                
                <div class="stats">
                    <div class="stat">
                        <div class="stat-value" id="user-points">0</div>
                        <div class="stat-label">当前积分</div>
                    </div>
                    <div class="stat">
                        <div class="stat-value" id="user-rank">-</div>
                        <div class="stat-label">当前排名</div>
                    </div>
                    <div class="stat">
                        <div class="stat-value" id="total-users">0</div>
                        <div class="stat-label">总用户数</div>
                    </div>
                </div>
            </div>
            
            <div class="card">
                <h2 class="card-title"><i class="fas fa-crown"></i> 当前排名</h2>
                <table id="ranking-table">
                    <thead>
                        <tr>
                            <th>排名</th>
                            <th>用户名</th>
                            <th>积分</th>
                        </tr>
                    </thead>
                    <tbody id="ranking-body">
                        <!-- 排名数据将通过JavaScript动态生成 -->
                    </tbody>
                </table>
            </div>
            
            <div class="nav-buttons">
                <button class="btn-secondary" id="user-logout"><i class="fas fa-sign-out-alt"></i> 退出登录</button>
            </div>
        </div>
        
        <!-- 管理员主页 -->
        <div id="admin-home" class="page">
            <div class="card">
                <div class="user-info">
                    <div class="avatar" id="admin-avatar">A</div>
                    <div>
                        <h2 id="admin-greeting">欢迎，管理员！</h2>
                        <p id="admin-role">角色：系统管理员</p>
                    </div>
                </div>
                
                <div class="stats">
                    <div class="stat">
                        <div class="stat-value" id="total-users-admin">0</div>
                        <div class="stat-label">总用户数</div>
                    </div>
                    <div class="stat">
                        <div class="stat-value" id="total-points">0</div>
                        <div class="stat-label">总积分</div>
                    </div>
                    <div class="stat">
                        <div class="stat-value" id="admin-count">1</div>
                        <div class="stat-label">管理员数量</div>
                    </div>
                </div>
            </div>
            
            <div class="row">
                <div class="col">
                    <div class="card">
                        <h2 class="card-title"><i class="fas fa-crown"></i> 当前排名</h2>
                        <table id="admin-ranking-table">
                            <thead>
                                <tr>
                                    <th>排名</th>
                                    <th>用户名</th>
                                    <th>积分</th>
                                </tr>
                            </thead>
                            <tbody id="admin-ranking-body">
                                <!-- 排名数据将通过JavaScript动态生成 -->
                            </tbody>
                        </table>
                    </div>
                </div>
                
                <div class="col">
                    <div class="card">
                        <h2 class="card-title"><i class="fas fa-star"></i> 积分分配</h2>
                        <div class="form-group">
                            <label for="assign-user">选择用户</label>
                            <select id="assign-user">
                                <option value="">-- 请选择用户 --</option>
                                <!-- 用户选项将通过JavaScript动态生成 -->
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="assign-points">积分值</label>
                            <input type="number" id="assign-points" placeholder="请输入积分值" min="1" max="1000">
                        </div>
                        <button id="assign-btn"><i class="fas fa-star"></i> 分配积分</button>
                    </div>
                    
                    <div class="card">
                        <h2 class="card-title"><i class="fas fa-users"></i> 用户管理</h2>
                        <table id="users-table">
                            <thead>
                                <tr>
                                    <th>用户名</th>
                                    <th>角色</th>
                                    <th>积分</th>
                                    <th>操作</th>
                                </tr>
                            </thead>
                            <tbody id="users-body">
                                <!-- 用户数据将通过JavaScript动态生成 -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
            
            <div class="nav-buttons">
                <button class="btn-secondary" id="admin-logout"><i class="fas fa-sign-out-alt"></i> 退出登录</button>
            </div>
        </div>
    </div>

    <script>
        // 模拟数据存储
        let users = JSON.parse(localStorage.getItem('users')) || [
            { id: 1, username: "admin", password: "admin123", role: "admin", points: 0 }
        ];
        
        // 管理员代码
        const ADMIN_CODE = "admin2024";
        
        let currentUser = null;
        
        // DOM元素
        const loginPage = document.getElementById('login-page');
        const registerPage = document.getElementById('register-page');
        const userHome = document.getElementById('user-home');
        const adminHome = document.getElementById('admin-home');
        
        const registerBtn = document.getElementById('register-btn');
        const loginBtn = document.getElementById('login-btn');
        const assignBtn = document.getElementById('assign-btn');
        const rankingBody = document.getElementById('ranking-body');
        const adminRankingBody = document.getElementById('admin-ranking-body');
        const usersBody = document.getElementById('users-body');
        const assignUserSelect = document.getElementById('assign-user');
        const goToRegister = document.getElementById('go-to-register');
        const backToLogin = document.getElementById('back-to-login');
        const userLogout = document.getElementById('user-logout');
        const adminLogout = document.getElementById('admin-logout');
        
        // 初始化页面
        function initPage() {
            updateLocalStorage();
            showPage('login-page');
        }
        
        // 显示特定页面
        function showPage(pageId) {
            // 隐藏所有页面
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            
            // 显示目标页面
            document.getElementById(pageId).classList.add('active');
        }
        
        // 更新本地存储
        function updateLocalStorage() {
            localStorage.setItem('users', JSON.stringify(users));
        }
        
        // 更新排名表格
        function updateRankingTable() {
            // 按积分排序
            const sortedUsers = [...users]
                .filter(user => user.role === 'user')
                .sort((a, b) => b.points - a.points);
            
            rankingBody.innerHTML = '';
            adminRankingBody.innerHTML = '';
            
            sortedUsers.forEach((user, index) => {
                const row = document.createElement('tr');
                const adminRow = document.createElement('tr');
                
                // 添加排名样式
                if (index === 0) {
                    row.classList.add('rank-1');
                    adminRow.classList.add('rank-1');
                } else if (index === 1) {
                    row.classList.add('rank-2');
                    adminRow.classList.add('rank-2');
                } else if (index === 2) {
                    row.classList.add('rank-3');
                    adminRow.classList.add('rank-3');
                }
                
                // 排名列
                const rankCell = document.createElement('td');
                const adminRankCell = document.createElement('td');
                if (index === 0) {
                    rankCell.innerHTML = '<span class="medal gold">1</span> 第一名';
                    adminRankCell.innerHTML = '<span class="medal gold">1</span> 第一名';
                } else if (index === 1) {
                    rankCell.innerHTML = '<span class="medal silver">2</span> 第二名';
                    adminRankCell.innerHTML = '<span class="medal silver">2</span> 第二名';
                } else if (index === 2) {
                    rankCell.innerHTML = '<span class="medal bronze">3</span> 第三名';
                    adminRankCell.innerHTML = '<span class="medal bronze">3</span> 第三名';
                } else {
                    rankCell.textContent = `${index + 1}`;
                    adminRankCell.textContent = `${index + 1}`;
                }
                
                // 用户名列
                const nameCell = document.createElement('td');
                const adminNameCell = document.createElement('td');
                nameCell.textContent = user.username;
                adminNameCell.textContent = user.username;
                
                // 积分列
                const pointsCell = document.createElement('td');
                const adminPointsCell = document.createElement('td');
                pointsCell.textContent = user.points;
                adminPointsCell.textContent = user.points;
                
                row.appendChild(rankCell);
                row.appendChild(nameCell);
                row.appendChild(pointsCell);
                
                adminRow.appendChild(adminRankCell);
                adminRow.appendChild(adminNameCell);
                adminRow.appendChild(adminPointsCell);
                
                rankingBody.appendChild(row);
                adminRankingBody.appendChild(adminRow);
            });
        }
        
        // 更新用户表格
        function updateUsersTable() {
            usersBody.innerHTML = '';
            
            users.forEach(user => {
                const row = document.createElement('tr');
                
                // 用户名
                const nameCell = document.createElement('td');
                nameCell.textContent = user.username;
                
                // 角色
                const roleCell = document.createElement('td');
                const badge = document.createElement('span');
                badge.classList.add('badge');
                if (user.role === 'admin') {
                    badge.classList.add('badge-admin');
                    badge.textContent = '管理员';
                } else {
                    badge.classList.add('badge-user');
                    badge.textContent = '普通用户';
                }
                roleCell.appendChild(badge);
                
                // 积分
                const pointsCell = document.createElement('td');
                pointsCell.textContent = user.points;
                
                // 操作
                const actionCell = document.createElement('td');
                if (user.id !== 1 && user.id !== currentUser.id) { // 不能删除默认管理员和自己
                    const deleteBtn = document.createElement('button');
                    deleteBtn.classList.add('btn-danger');
                    deleteBtn.innerHTML = '<i class="fas fa-trash"></i> 删除';
                    deleteBtn.addEventListener('click', () => deleteUser(user.id));
                    actionCell.appendChild(deleteBtn);
                }
                
                row.appendChild(nameCell);
                row.appendChild(roleCell);
                row.appendChild(pointsCell);
                row.appendChild(actionCell);
                
                usersBody.appendChild(row);
            });
        }
        
        // 更新分配用户下拉框
        function updateAssignUserSelect() {
            assignUserSelect.innerHTML = '<option value="">-- 请选择用户 --</option>';
            
            users.forEach(user => {
                if (user.role === 'user') {
                    const option = document.createElement('option');
                    option.value = user.id;
                    option.textContent = user.username;
                    assignUserSelect.appendChild(option);
                }
            });
        }
        
        // 更新用户主页信息
        function updateUserHome() {
            if (!currentUser) return;
            
            // 更新用户信息
            document.getElementById('user-avatar').textContent = currentUser.username.charAt(0).toUpperCase();
            document.getElementById('user-greeting').textContent = `欢迎，${currentUser.username}！`;
            document.getElementById('user-role').textContent = `角色：${currentUser.role === 'admin' ? '管理员' : '普通用户'}`;
            document.getElementById('user-points').textContent = currentUser.points;
            
            // 计算用户排名
            const sortedUsers = [...users]
                .filter(user => user.role === 'user')
                .sort((a, b) => b.points - a.points);
            
            const userRank = sortedUsers.findIndex(user => user.id === currentUser.id) + 1;
            document.getElementById('user-rank').textContent = userRank > 0 ? userRank : '-';
            
            // 更新统计数据
            document.getElementById('total-users').textContent = users.filter(u => u.role === 'user').length;
        }
        
        // 更新管理员主页信息
        function updateAdminHome() {
            // 更新管理员信息
            document.getElementById('admin-avatar').textContent = currentUser.username.charAt(0).toUpperCase();
            document.getElementById('admin-greeting').textContent = `欢迎，${currentUser.username}！`;
            
            // 更新统计数据
            document.getElementById('total-users-admin').textContent = users.filter(u => u.role === 'user').length;
            document.getElementById('total-points').textContent = users.reduce((sum, user) => sum + user.points, 0);
            document.getElementById('admin-count').textContent = users.filter(u => u.role === 'admin').length;
        }
        
        // 删除用户
        function deleteUser(userId) {
            if (confirm('确定要删除这个用户吗？此操作不可恢复。')) {
                users = users.filter(user => user.id !== userId);
                updateLocalStorage();
                updateUsersTable();
                updateAssignUserSelect();
                updateRankingTable();
                alert('用户已成功删除！');
            }
        }
        
        // 注册功能
        registerBtn.addEventListener('click', function() {
            const username = document.getElementById('username').value.trim();
            const password = document.getElementById('password').value;
            const confirmPassword = document.getElementById('confirm-password').value;
            const adminCode = document.getElementById('admin-code').value;
            
            if (!username || !password || !confirmPassword) {
                alert('请填写所有必填字段！');
                return;
            }
            
            if (password !== confirmPassword) {
                alert('两次输入的密码不一致！');
                return;
            }
            
            // 检查用户名是否已存在
            if (users.some(user => user.username === username)) {
                alert('用户名已存在，请选择其他用户名！');
                return;
            }
            
            // 确定用户角色
            let role = 'user';
            if (adminCode === ADMIN_CODE) {
                role = 'admin';
            } else if (adminCode) {
                alert('管理员代码不正确，将注册为普通用户！');
            }
            
            // 创建新用户
            const newUser = {
                id: users.length > 0 ? Math.max(...users.map(u => u.id)) + 1 : 1,
                username: username,
                password: password,
                role: role,
                points: 0
            };
            
            users.push(newUser);
            updateLocalStorage();
            
            alert(`注册成功！您已注册为${role === 'admin' ? '管理员' : '普通用户'}。`);
            
            // 清空表单并返回登录页面
            document.getElementById('username').value = '';
            document.getElementById('password').value = '';
            document.getElementById('confirm-password').value = '';
            document.getElementById('admin-code').value = '';
            
            showPage('login-page');
        });
        
        // 登录功能
        loginBtn.addEventListener('click', function() {
            const username = document.getElementById('login-username').value.trim();
            const password = document.getElementById('login-password').value;
            
            if (!username || !password) {
                alert('请填写用户名和密码！');
                return;
            }
            
            // 验证用户
            const user = users.find(u => u.username === username && u.password === password);
            
            if (user) {
                currentUser = user;
                alert(`登录成功！欢迎 ${user.username}`);
                
                // 根据用户角色显示相应主页
                if (user.role === 'admin') {
                    updateAdminHome();
                    updateRankingTable();
                    updateUsersTable();
                    updateAssignUserSelect();
                    showPage('admin-home');
                } else {
                    updateUserHome();
                    updateRankingTable();
                    showPage('user-home');
                }
            } else {
                alert('用户名或密码错误！');
            }
            
            // 清空表单
            document.getElementById('login-username').value = '';
            document.getElementById('login-password').value = '';
        });
        
        // 分配积分功能
        assignBtn.addEventListener('click', function() {
            if (!currentUser || currentUser.role !== 'admin') {
                alert('只有管理员可以分配积分！');
                return;
            }
            
            const userId = parseInt(assignUserSelect.value);
            const points = parseInt(document.getElementById('assign-points').value);
            
            if (!userId) {
                alert('请选择用户！');
                return;
            }
            
            if (!points || points <= 0) {
                alert('请输入有效的积分值！');
                return;
            }
            
            // 更新用户积分
            const user = users.find(u => u.id === userId);
            if (user) {
                user.points += points;
                updateLocalStorage();
                alert(`成功给 ${user.username} 分配 ${points} 积分！`);
                
                // 清空表单
                document.getElementById('assign-points').value = '';
                
                // 更新页面
                updateRankingTable();
                updateUsersTable();
                updateAdminHome();
            }
        });
        
        // 页面导航
        goToRegister.addEventListener('click', function(e) {
            e.preventDefault();
            showPage('register-page');
        });
        
        backToLogin.addEventListener('click', function() {
            showPage('login-page');
        });
        
        userLogout.addEventListener('click', function() {
            currentUser = null;
            showPage('login-page');
        });
        
        adminLogout.addEventListener('click', function() {
            currentUser = null;
            showPage('login-page');
        });
        
        // 初始化页面
        initPage();
    </script>
</body>
</html>
