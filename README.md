<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Budget Baon | Student Tracker</title>
    <style>
        :root {
            --navy: #1a2a4e;
            --off-white: #f4f1f0;
            --white: #ffffff;
            --gray: #666;
            --light-border: #e0e0e0;
        }

        body {
            font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
            background-color: var(--off-white);
            margin: 0;
            color: var(--navy);
        }

        /* Navigation */
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 25px 8%;
            background: var(--off-white);
        }

        .logo { font-size: 28px; font-weight: 800; cursor: pointer; color: var(--navy); }

        nav a {
            margin: 0 15px;
            text-decoration: none;
            color: var(--navy);
            font-size: 13px;
            text-transform: uppercase;
            letter-spacing: 1px;
            cursor: pointer;
            font-weight: 600;
        }

        .sign-in {
            background: var(--navy);
            color: white;
            padding: 10px 28px;
            border-radius: 4px;
            border: none;
            cursor: pointer;
            font-weight: bold;
        }

        /* Hero Section */
        .hero-container {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 40px 8% 80px 8%;
            gap: 40px;
        }

        .hero-text { flex: 1; }
        .hero-text h1 { font-size: 56px; margin: 0 0 20px 0; line-height: 1.1; letter-spacing: -1px; }
        .hero-text p { font-size: 20px; color: var(--gray); margin-bottom: 40px; }

        .hero-image {
            flex: 1;
            display: flex;
            justify-content: flex-end;
        }

        .hero-image img {
            width: 100%;
            max-width: 550px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        /* Feature Cards */
        .features-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 25px;
            padding: 0 8% 60px 8%;
        }

        .feature-card {
            background: white;
            padding: 35px;
            border-radius: 12px;
            cursor: pointer;
            transition: transform 0.2s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.03);
        }

        .feature-card:hover { transform: translateY(-5px); }
        .feature-card h3 { margin: 0 0 10px 0; font-size: 20px; }
        .feature-card p { margin: 0; color: var(--gray); font-size: 15px; }

        /* General Section Layout */
        .page-section { display: none; padding: 60px 8%; max-width: 1000px; margin: 0 auto; }
        .page-section.active { display: block; }
        .content-box { background: white; padding: 45px; border-radius: 12px; box-shadow: 0 4px 25px rgba(0,0,0,0.05); }

        /* Auth Modal */
        .modal { display: none; position: fixed; z-index: 2000; left: 0; top: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); justify-content: center; align-items: center; }
        .modal-content { background: white; padding: 40px; border-radius: 12px; width: 320px; text-align: center; }
        .modal-content input { width: 100%; padding: 12px; margin: 10px 0; border: 1px solid #ddd; border-radius: 6px; box-sizing: border-box; }

        /* Tracker Table Styles */
        .tracker-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 25px; }
        .controls { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 15px; margin-bottom: 25px; }
        .controls input { padding: 12px; border: 1px solid #ddd; border-radius: 6px; }
        table { width: 100%; border-collapse: collapse; }
        th { background: #fcfcfc; text-align: left; padding: 15px; border-bottom: 2px solid var(--off-white); color: var(--gray); font-size: 12px; text-transform: uppercase; }
        td { padding: 15px; border-bottom: 1px solid #f0f0f0; }
        .savings-footer { margin-top: 30px; font-size: 22px; font-weight: bold; color: var(--navy); }
    </style>
</head>
<body>

    <div id="authModal" class="modal">
        <div class="modal-content">
            <h2 id="modalTitle">Sign In</h2>
            <div id="loginFields">
                <input type="text" id="usernameInput" placeholder="Name">
                <input type="email" id="emailInput" placeholder="Email">
                <button class="sign-in" style="width:100%; margin-top:10px;" onclick="handleAuth()">Continue</button>
            </div>
            <button onclick="closeModal()" style="background:none; border:none; margin-top:15px; cursor:pointer; color:var(--gray);">Cancel</button>
        </div>
    </div>

    <header>
        <div class="logo" onclick="showPage('home')">Budget Baon</div>
        <nav>
            <a onclick="showPage('home')">Home</a>
            <a onclick="showPage('calculator')">Calculator</a>
            <a onclick="showPage('tracker')">Tracker</a>
            <a onclick="showPage('tips')">Tips</a>
            <a onclick="showPage('about')">About</a>
        </nav>
        <button id="navAuthBtn" class="sign-in" onclick="openModal()">Sign In</button>
    </header>

    <main id="home" class="page-section active" style="padding: 0; max-width: 100%;">
        <section class="hero-container">
            <div class="hero-text">
                <h1 id="welcomeHeading">MANAGING STUDENTS ALLOWANCES</h1>
                <p>Track it. Save it. Own your budget.</p>
                <div style="display: flex; gap: 15px;">
                    <button class="sign-in" style="padding: 16px 40px; font-size: 16px;" onclick="showPage('tracker')">Start Tracking</button>
                    <button style="background:white; border: 1px solid #ccc; padding: 16px 40px; border-radius:4px; font-weight:bold; cursor:pointer;" onclick="showPage('about')">About</button>
                </div>
            </div>
            <div class="hero-image">
                <img src="https://images.unsplash.com/photo-1554224155-6726b3ff858f?auto=format&fit=crop&w=800&q=80" alt="Budget Planner">
            </div>
        </section>

        <section class="features-grid">
            <div class="feature-card" onclick="showPage('tracker')">
                <h3>Allowance Tracker</h3>
                <p>Log your daily spending and keep an eye on your balance.</p>
            </div>
            <div class="feature-card" onclick="showPage('tips')">
                <h3>Saving Tips</h3>
                <p>Practical hacks to make your allowance last longer.</p>
            </div>
            <div class="feature-card" onclick="showPage('calculator')">
                <h3>Budget Calculator</h3>
                <p>Calculate daily expenses and see how much money you can save.</p>
            </div>
        </section>
    </main>

    <section id="calculator" class="page-section">
        <div class="content-box">
            <h2 style="margin-top:0">BUDGET CALCULATOR</h2>
            <p>What's your weekly allowance?</p>
            <input type="number" id="weeklyAllowance" style="width:100%; padding:15px; margin-bottom:25px; border:1px solid #ddd; border-radius:6px; box-sizing:border-box;" placeholder="Type here">
            
            <p>List your planned expenses:</p>
            <table style="margin-bottom:25px;">
                <tr><td>Food</td><td><input type="number" id="foodCost" style="width:100%; border:none; outline:none;" placeholder="₱ 0.00"></td></tr>
                <tr><td>Transport</td><td><input type="number" id="transportCost" style="width:100%; border:none; outline:none;" placeholder="₱ 0.00"></td></tr>
                <tr><td>Extras</td><td><input type="number" id="extrasCost" style="width:100%; border:none; outline:none;" placeholder="₱ 0.00"></td></tr>
            </table>

            <p>Your suggested daily budget:</p>
            <div style="border: 1px solid #ccc; padding: 20px; width: 220px; font-size: 28px; font-weight: bold; margin-bottom: 25px;">₱ <span id="dailyResult">0.00</span></div>
            <button class="sign-in" style="width:100%" onclick="calculateDaily()">Calculate</button>
        </div>
    </section>

    <section id="tracker" class="page-section">
        <div class="content-box">
            <div class="tracker-header">
                <div style="border: 1px solid #000; padding: 6px 16px; font-weight: bold; text-transform: uppercase; font-size: 13px;">Allowance Tracker</div>
                <button onclick="addEntry()" style="cursor:pointer; background: white; border: 1px solid #000; padding: 8px 16px; font-weight:bold;">+ Add Expense</button>
            </div>

            <div class="controls">
                <input type="date" id="dateInput">
                <input type="text" id="itemInput" placeholder="Item Name">
                <input type="number" id="costInput" placeholder="Cost (₱)">
                <input type="number" id="initialAllowance" placeholder="Set Weekly Allowance" onchange="updateTable()">
            </div>

            <table>
                <thead>
                    <tr><th>DATE</th><th>Item</th><th>Cost</th><th>Remaining Balance</th></tr>
                </thead>
                <tbody id="trackerBody"></tbody>
            </table>

            <div class="savings-footer">This week's savings: ₱ <span id="savingsValue">0.00</span></div>
            <button onclick="clearTracker()" style="margin-top:30px; background:none; border:none; color:red; cursor:pointer; font-size:12px; text-decoration:underline;">Clear Data</button>
        </div>
    </section>

    <section id="about" class="page-section">
        <div class="content-box">
            <h2 style="margin-top:0">ABOUT BUDGET BAON</h2>
            <p style="font-size: 18px; line-height: 1.6; color: var(--gray);">Budget Baon is designed to help young people manage their daily allowance through simple tools, tips, and interactive features. Our main goals are to help students manage their allowance and take control of their spending habits. Whether you’re saving for a goal or just trying to make your baon last until Friday.</p>
            <hr style="border:0; border-top:1px solid #eee; margin:30px 0;">
            <h3>Contact us in the following:</h3>
            <ul style="line-height:2; color: var(--gray);">
                <li><b>Phone: 0965-3562-998</li>

<li>Email: budgetbaon67@gmail.com</li>
<li>FB: Budget Baon Managing Student Allowances</li>
            </ul>
        </div>
    </section>

    <section id="tips" class="page-section">
        <div class="content-box">
            <h2 style="margin-top:0">SAVING TIPS</h2>
            <div style="display:grid; gap:20px;">
                <div style="padding:15px; border-left:4px solid var(--navy); background:#f9f9f9;">
                    <b>Baon is Better:</b>Bringing your own rice and water saves ~₱50/day.
                </div>
                <div style="padding:15px; border-left:4px solid var(--navy); background:#f9f9f9;">
                    <b>Walk more:</b>  If it's just a few blocks, skip the trike.
                </div>
                <div style="padding:15px; border-left:4px solid var(--navy); background:#f9f9f9;">
                    <b>Student Discounts:</b> Always show your ID for fare and other expenses.
                </div>
 <div style="padding:15px; border-left:4px solid var(--navy); background:#f9f9f9;">
                    <b>Save Your Change:</b>Small coins and change can add up.
</div>

 <div style="padding:15px; border-left:4px solid var(--navy); background:#f9f9f9;">
                    <b>Wait 24 Hours:</b> Before buying a "want", sleep on it. You'll usually realize you don't need it.
                </div>

                </div>

            </div>
        </div>
    </section>

    <script>
        // PAGE NAVIGATION
        function showPage(pageId) {
            document.querySelectorAll('.page-section').forEach(sec => sec.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            window.scrollTo(0,0);
        }

        // AUTH LOGIC
        let currentUser = localStorage.getItem('budgetUser') || null;
        function openModal() { document.getElementById('authModal').style.display = 'flex'; }
        function closeModal() { document.getElementById('authModal').style.display = 'none'; }
        
        function handleAuth() {
            const name = document.getElementById('usernameInput').value;
            if(name) {
                currentUser = name;
                localStorage.setItem('budgetUser', name);
                updateUI();
                closeModal();
            }
        }

        function updateUI() {
            if(currentUser) {
                document.getElementById('welcomeHeading').innerText = "WELCOME, " + currentUser.toUpperCase();
                document.getElementById('navAuthBtn').innerText = "Sign Out";
                document.getElementById('navAuthBtn').onclick = () => {
                    localStorage.removeItem('budgetUser');
                    location.reload();
                };
            }
        }

        // CALCULATOR LOGIC
        function calculateDaily() {
            const allow = parseFloat(document.getElementById('weeklyAllowance').value) || 0;
            const expenses = (parseFloat(document.getElementById('foodCost').value) || 0) + 
                             (parseFloat(document.getElementById('transportCost').value) || 0) + 
                             (parseFloat(document.getElementById('extrasCost').value) || 0);
            const daily = (allow - expenses) / 5;
            document.getElementById('dailyResult').innerText = daily > 0 ? daily.toFixed(2) : "0.00";
        }

        // TRACKER LOGIC
        let expenses = JSON.parse(localStorage.getItem('savedExpenses')) || [];
        
        window.onload = () => {
            updateUI();
            document.getElementById('initialAllowance').value = localStorage.getItem('savedAllowance') || "";
            updateTable();
        };

        function addEntry() {
            const date = document.getElementById('dateInput').value;
            const item = document.getElementById('itemInput').value;
            const cost = parseFloat(document.getElementById('costInput').value);
            if (!date || !item || isNaN(cost)) return alert("Please fill all fields!");

            expenses.push({ date, item, cost });
            localStorage.setItem('savedExpenses', JSON.stringify(expenses));
            updateTable();
            document.getElementById('itemInput').value = '';
            document.getElementById('costInput').value = '';
        }

        function updateTable() {
            const tbody = document.getElementById('trackerBody');
            const allowance = parseFloat(document.getElementById('initialAllowance').value) || 0;
            localStorage.setItem('savedAllowance', allowance);
            tbody.innerHTML = '';
            let balance = allowance;
            expenses.forEach(ex => {
                balance -= ex.cost;
                tbody.innerHTML += `<tr><td>${ex.date}</td><td>${ex.item}</td><td>₱${ex.cost.toFixed(2)}</td><td>₱${balance.toFixed(2)}</td></tr>`;
            });
            document.getElementById('savingsValue').innerText = balance.toFixed(2);
        }

        function clearTracker() {
            if(confirm("Clear all records?")) {
                expenses = [];
                localStorage.removeItem('savedExpenses');
                updateTable();
            }
        }
    </script>
</body>
</html>
