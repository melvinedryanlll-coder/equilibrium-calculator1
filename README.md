<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Equilibrium Calculator | ∑Fx=0, ∑Fy=0, ΣM=0</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2980 0%, #26d0ce 100%);
            color: #333;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }
        
        /* Header */
        .header {
            background: linear-gradient(135deg, #2c3e50 0%, #4a6491 100%);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }
        
        .header h1 {
            font-size: 2.8rem;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
        }
        
        .header p {
            font-size: 1.2rem;
            opacity: 0.9;
            max-width: 800px;
            margin: 0 auto 20px;
        }
        
        .equation-badges {
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
        }
        
        .badge {
            background: rgba(255, 255, 255, 0.2);
            padding: 8px 20px;
            border-radius: 30px;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 8px;
            backdrop-filter: blur(10px);
        }
        
        /* Main Layout */
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 0;
            min-height: 600px;
        }
        
        @media (max-width: 1024px) {
            .main-content {
                grid-template-columns: 1fr;
            }
        }
        
        /* Input Section */
        .input-section {
            background: #f8fafc;
            padding: 30px;
            border-right: 1px solid #e5e7eb;
        }
        
        /* Results Section */
        .results-section {
            background: #ffffff;
            padding: 30px;
        }
        
        .section-title {
            color: #2c3e50;
            font-size: 1.8rem;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 3px solid #3b82f6;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        /* Control Buttons */
        .control-buttons {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .btn {
            padding: 14px;
            border: none;
            border-radius: 10px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            font-size: 1rem;
        }
        
        .btn-primary {
            background: #3b82f6;
            color: white;
        }
        
        .btn-primary:hover {
            background: #2563eb;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(59, 130, 246, 0.3);
        }
        
        .btn-success {
            background: #10b981;
            color: white;
        }
        
        .btn-success:hover {
            background: #059669;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(16, 185, 129, 0.3);
        }
        
        .btn-warning {
            background: #f59e0b;
            color: white;
        }
        
        .btn-warning:hover {
            background: #d97706;
            transform: translateY(-2px);
        }
        
        .btn-danger {
            background: #ef4444;
            color: white;
        }
        
        .btn-danger:hover {
            background: #dc2626;
            transform: translateY(-2px);
        }
        
        /* Forces Container */
        .forces-container {
            max-height: 400px;
            overflow-y: auto;
            padding: 10px;
            background: white;
            border-radius: 10px;
            margin-bottom: 25px;
            border: 2px solid #e5e7eb;
        }
        
        .force-card {
            background: #f1f5f9;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 15px;
            border-left: 5px solid #3b82f6;
            transition: all 0.3s;
            position: relative;
        }
        
        .force-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .force-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .force-title {
            font-weight: 700;
            color: #1e293b;
            font-size: 1.2rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .remove-force {
            background: #ef4444;
            color: white;
            border: none;
            width: 32px;
            height: 32px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s;
        }
        
        .remove-force:hover {
            background: #dc2626;
            transform: scale(1.1);
        }
        
        /* Input Grid */
        .input-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }
        
        @media (max-width: 768px) {
            .input-grid {
                grid-template-columns: 1fr;
            }
        }
        
        .input-field {
            display: flex;
            flex-direction: column;
        }
        
        .input-field label {
            margin-bottom: 8px;
            font-weight: 600;
            color: #475569;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        input {
            padding: 12px 15px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 1rem;
            transition: all 0.3s;
        }
        
        input:focus {
            border-color: #3b82f6;
            outline: none;
            box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
        }
        
        /* Pivot Input */
        .pivot-input {
            background: linear-gradient(135deg, #e0f2fe 0%, #f0f9ff 100%);
            padding: 20px;
            border-radius: 10px;
            border: 2px solid #bae6fd;
        }
        
        .pivot-input h3 {
            color: #0369a1;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        /* Equations Display */
        .equations {
            margin-bottom: 30px;
        }
        
        .equation-box {
            background: #f8fafc;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 15px;
            border-left: 5px solid #8b5cf6;
            transition: all 0.3s;
        }
        
        .equation-box:hover {
            transform: translateX(5px);
        }
        
        .equation-title {
            color: #7c3aed;
            font-weight: 700;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .equation-content {
            font-family: 'Courier New', monospace;
            font-size: 1.2rem;
            color: #1e293b;
            font-weight: 500;
        }
        
        /* Results Display */
        .results-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 30px;
        }
        
        @media (max-width: 640px) {
            .results-grid {
                grid-template-columns: 1fr;
            }
        }
        
        .result-card {
            background: linear-gradient(135deg, #dbeafe 0%, #eff6ff 100%);
            padding: 25px;
            border-radius: 10px;
            text-align: center;
            border: 2px solid #bfdbfe;
            transition: all 0.3s;
        }
        
        .result-card:hover {
            border-color: #3b82f6;
            transform: translateY(-3px);
        }
        
        .result-label {
            color: #475569;
            font-size: 1rem;
            font-weight: 600;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .result-value {
            font-size: 2.2rem;
            font-weight: 700;
            color: #1d4ed8;
        }
        
        /* Status Display */
        .status-box {
            background: linear-gradient(135deg, #f0fdf4 0%, #f7fee7 100%);
            padding: 20px;
            border-radius: 10px;
            border: 2px solid #86efac;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        
        .status-content {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .status-icon {
            background: #10b981;
            color: white;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
        }
        
        .status-text h4 {
            color: #065f46;
            margin-bottom: 5px;
            font-size: 1.3rem;
        }
        
        .status-text p {
            color: #047857;
            font-size: 0.95rem;
        }
        
        #balanceIndicator {
            font-size: 2.5rem;
            color: #10b981;
        }
        
        /* Instructions */
        .instructions {
            background: linear-gradient(135deg, #fef3c7 0%, #fffbeb 100%);
            padding: 20px;
            border-radius: 10px;
            margin-top: 25px;
            border-left: 5px solid #f59e0b;
        }
        
        .instructions h3 {
            color: #b45309;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .instructions ol {
            padding-left: 20px;
            margin-bottom: 10px;
        }
        
        .instructions li {
            margin-bottom: 8px;
            color: #78350f;
        }
        
        /* Footer */
        .footer {
            text-align: center;
            padding: 20px;
            color: #64748b;
            font-size: 0.9rem;
            border-top: 1px solid #e5e7eb;
            background: #f8fafc;
        }
        
        /* Animations */
        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        @keyframes highlight {
            0% { background-color: #f8fafc; }
            50% { background-color: #dbeafe; }
            100% { background-color: #f8fafc; }
        }
        
        .highlight {
            animation: highlight 1s ease;
        }
        
        /* Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
            border-radius: 10px;
        }
        
        ::-webkit-scrollbar-thumb {
            background: #94a3b8;
            border-radius: 10px;
        }
        
        ::-webkit-scrollbar-thumb:hover {
            background: #64748b;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <header class="header">
            <h1><i class="fas fa-balance-scale"></i> Equilibrium Calculator</h1>
            <p>Solve static equilibrium problems using ∑Fx=0, ∑Fy=0, ΣM=0. Perfect for engineering students!</p>
            
            <div class="equation-badges">
                <div class="badge"><i class="fas fa-calculator"></i> ∑Fx = 0</div>
                <div class="badge"><i class="fas fa-calculator"></i> ∑Fy = 0</div>
                <div class="badge"><i class="fas fa-calculator"></i> ΣM = 0</div>
            </div>
        </header>

        <!-- Main Content -->
        <div class="main-content">
            <!-- Input Section -->
            <section class="input-section">
                <h2 class="section-title"><i class="fas fa-edit"></i> Input Forces</h2>
                
                <div class="control-buttons">
                    <button class="btn btn-primary" id="addForce">
                        <i class="fas fa-plus"></i> Add Force
                    </button>
                    <button class="btn btn-success" id="calculate">
                        <i class="fas fa-calculator"></i> Calculate
                    </button>
                    <button class="btn btn-warning" id="reset">
                        <i class="fas fa-redo"></i> Reset
                    </button>
                    <button class="btn btn-danger" id="clearAll">
                        <i class="fas fa-trash"></i> Clear All
                    </button>
                </div>
                
                <div class="forces-container" id="forcesContainer">
                    <!-- Force cards go here -->
                </div>
                
                <div class="pivot-input">
                    <h3><i class="fas fa-crosshairs"></i> Pivot Point (Moment Reference)</h3>
                    <div class="input-grid">
                        <div class="input-field">
                            <label for="pivotX"><i class="fas fa-arrows-alt-h"></i> X Position (m)</label>
                            <input type="number" id="pivotX" value="0" step="0.1" placeholder="0">
                        </div>
                        <div class="input-field">
                            <label for="pivotY"><i class="fas fa-arrows-alt-v"></i> Y Position (m)</label>
                            <input type="number" id="pivotY" value="0" step="0.1" placeholder="0">
                        </div>
                    </div>
                </div>
            </section>
            
            <!-- Results Section -->
            <section class="results-section">
                <h2 class="section-title"><i class="fas fa-chart-bar"></i> Results</h2>
                
                <div class="equations">
                    <div class="equation-box" id="equationFx">
                        <div class="equation-title">
                            <i class="fas fa-arrows-alt-h"></i> Horizontal Forces
                        </div>
                        <div class="equation-content">∑Fx = 0: Waiting for input...</div>
                    </div>
                    
                    <div class="equation-box" id="equationFy">
                        <div class="equation-title">
                            <i class="fas fa-arrows-alt-v"></i> Vertical Forces
                        </div>
                        <div class="equation-content">∑Fy = 0: Waiting for input...</div>
                    </div>
                    
                    <div class="equation-box" id="equationM">
                        <div class="equation-title">
                            <i class="fas fa-sync-alt"></i> Moments
                        </div>
                        <div class="equation-content">∑M = 0: Waiting for input...</div>
                    </div>
                </div>
                
                <div class="results-grid">
                    <div class="result-card">
                        <div class="result-label">
                            <i class="fas fa-arrow-right"></i> Horizontal Reaction
                        </div>
                        <div class="result-value" id="resultRx">0.00 N</div>
                    </div>
                    
                    <div class="result-card">
                        <div class="result-label">
                            <i class="fas fa-arrow-up"></i> Vertical Reaction
                        </div>
                        <div class="result-value" id="resultRy">0.00 N</div>
                    </div>
                </div>
                
                <div class="status-box" id="statusBox">
                    <div class="status-content">
                        <div class="status-icon">
                            <i class="fas fa-hourglass-half"></i>
                        </div>
                        <div class="status-text">
                            <h4 id="systemStatus">Ready to Calculate</h4>
                            <p id="systemMessage">Add forces and click Calculate</p>
                        </div>
                    </div>
                    <div id="balanceIndicator">
                        <i class="fas fa-balance-scale"></i>
                    </div>
                </div>
                
                <div class="instructions">
                    <h3><i class="fas fa-info-circle"></i> How to Use</h3>
                    <ol>
                        <li><strong>Add Force</strong>: Click "Add Force" button</li>
                        <li><strong>Enter values</strong>: For each force, enter magnitude (N), angle (°), and position (m)</li>
                        <li><strong>Set Pivot</strong>: Enter pivot point coordinates</li>
                        <li><strong>Calculate</strong>: Click "Calculate" to solve equilibrium equations</li>
                        <li><strong>View Results</strong>: Check reaction forces and system status</li>
                    </ol>
                    <p style="color: #92400e; margin-top: 10px;">
                        <i class="fas fa-lightbulb"></i> <strong>Tip:</strong> Angle 0° = Right, 90° = Up. Counterclockwise moments are positive.
                    </p>
                </div>
            </section>
        </div>
        
        <!-- Footer -->
        <footer class="footer">
            <p>Equilibrium Calculator | ∑Fx=0, ∑Fy=0, ΣM=0 | Engineering Statics Project</p>
            <p>© 2023 | Interactive Web Application</p>
        </footer>
    </div>

    <script>
        // ========== VARIABLES ==========
        let forceCount = 0;
        
        // ========== DOM ELEMENTS ==========
        const forcesContainer = document.getElementById('forcesContainer');
        const addForceBtn = document.getElementById('addForce');
        const calculateBtn = document.getElementById('calculate');
        const resetBtn = document.getElementById('reset');
        const clearAllBtn = document.getElementById('clearAll');
        const pivotXInput = document.getElementById('pivotX');
        const pivotYInput = document.getElementById('pivotY');
        
        // Result elements
        const equationFxEl = document.getElementById('equationFx');
        const equationFyEl = document.getElementById('equationFy');
        const equationMEl = document.getElementById('equationM');
        const resultRxEl = document.getElementById('resultRx');
        const resultRyEl = document.getElementById('resultRy');
        const systemStatusEl = document.getElementById('systemStatus');
        const systemMessageEl = document.getElementById('systemMessage');
        const balanceIndicator = document.getElementById('balanceIndicator');
        const statusBox = document.getElementById('statusBox');
        
        // ========== INITIALIZE ==========
        document.addEventListener('DOMContentLoaded', () => {
            addNewForce(); // Start with one force
            updateStatus('Ready', 'Add forces and click Calculate', 'info');
        });
        
        // ========== EVENT LISTENERS ==========
        addForceBtn.addEventListener('click', addNewForce);
        calculateBtn.addEventListener('click', calculateEquilibrium);
        resetBtn.addEventListener('click', resetCalculator);
        clearAllBtn.addEventListener('click', clearAllForces);
        
        // ========== FUNCTIONS ==========
        
        // Add new force card
        function addNewForce() {
            forceCount++;
            const forceId = `force${forceCount}`;
            
            const forceCard = document.createElement('div');
            forceCard.className = 'force-card';
            forceCard.id = `card-${forceId}`;
            forceCard.style.animation = 'fadeIn 0.5s ease';
            
            // Random color for icon
            const colors = ['#3b82f6', '#8b5cf6', '#10b981', '#f59e0b', '#ef4444'];
            const color = colors[Math.floor(Math.random() * colors.length)];
            
            forceCard.innerHTML = `
                <div class="force-header">
                    <div class="force-title">
                        <i class="fas fa-long-arrow-alt-right" style="color: ${color};"></i>
                        Force F${forceCount}
                    </div>
                    <button class="remove-force" title="Remove this force">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                <div class="input-grid">
                    <div class="input-field">
                        <label for="${forceId}-mag">
                            <i class="fas fa-bolt"></i> Magnitude (N)
                        </label>
                        <input type="number" id="${forceId}-mag" value="100" step="1" min="0">
                    </div>
                    <div class="input-field">
                        <label for="${forceId}-angle">
                            <i class="fas fa-compass"></i> Angle (°)
                        </label>
                        <input type="number" id="${forceId}-angle" value="${(forceCount * 30) % 360}" step="1" min="0" max="360">
                    </div>
                </div>
                <div class="input-grid">
                    <div class="input-field">
                        <label for="${forceId}-x">
                            <i class="fas fa-map-marker-alt"></i> X Position (m)
                        </label>
                        <input type="number" id="${forceId}-x" value="${forceCount}" step="0.1">
                    </div>
                    <div class="input-field">
                        <label for="${forceId}-y">
                            <i class="fas fa-map-marker-alt"></i> Y Position (m)
                        </label>
                        <input type="number" id="${forceId}-y" value="0" step="0.1">
                    </div>
                </div>
            `;
            
            forcesContainer.appendChild(forceCard);
            
            // Add remove button functionality
            const removeBtn = forceCard.querySelector('.remove-force');
            removeBtn.addEventListener('click', () => {
                if (forceCount > 1) {
                    forceCard.style.animation = 'fadeIn 0.5s ease reverse';
                    setTimeout(() => {
                        forceCard.remove();
                        forceCount--;
                        updateForceTitles();
                        updateStatus('Force removed', `${forceCount} force(s) remaining`, 'info');
                    }, 300);
                } else {
                    updateStatus('Cannot remove', 'At least one force required', 'error');
                }
            });
            
            // Input validation
            const inputs = forceCard.querySelectorAll('input');
            inputs.forEach(input => {
                input.addEventListener('input', function() {
                    this.style.borderColor = '#3b82f6';
                    setTimeout(() => {
                        this.style.borderColor = '';
                    }, 1000);
                });
            });
            
            updateStatus('Force added', `Force F${forceCount} ready. Configure values.`, 'success');
            forceCard.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
        }
        
        // Update force titles after removal
        function updateForceTitles() {
            const cards = document.querySelectorAll('.force-card');
            cards.forEach((card, index) => {
                const title = card.querySelector('.force-title');
                title.innerHTML = `<i class="fas fa-long-arrow-alt-right" style="color: #3b82f6;"></i> Force F${index + 1}`;
            });
        }
        
        // Update status display
        function updateStatus(title, message, type) {
            systemStatusEl.textContent = title;
            systemMessageEl.textContent = message;
            
            // Colors based on type
            const colors = {
                success: { bg: '#10b981', border: '#059669', icon: 'fa-check' },
                error: { bg: '#ef4444', border: '#dc2626', icon: 'fa-exclamation-triangle' },
                info: { bg: '#3b82f6', border: '#2563eb', icon: 'fa-info-circle' },
                warning: { bg: '#f59e0b', border: '#d97706', icon: 'fa-exclamation' }
            };
            
            const color = colors[type] || colors.info;
            statusBox.style.borderColor = color.border;
            statusBox.style.background = `linear-gradient(135deg, ${color.bg}20 0%, ${color.border}20 100%)`;
            
            const icon = statusBox.querySelector('.status-icon');
            icon.style.background = color.bg;
            icon.innerHTML = `<i class="fas ${color.icon}"></i>`;
        }
        
        // Main calculation function
        function calculateEquilibrium() {
            // Get pivot point
            const pivotX = parseFloat(pivotXInput.value) || 0;
            const pivotY = parseFloat(pivotYInput.value) || 0;
            
            // Initialize sums
            let sumFx = 0;
            let sumFy = 0;
            let sumM = 0;
            
            // Get all force cards
            const forceCards = document.querySelectorAll('.force-card');
            
            if (forceCards.length === 0) {
                updateStatus('No Forces', 'Add at least one force', 'error');
                return;
            }
            
            let equationsFx = [];
            let equationsFy = [];
            let equationsM = [];
            let valid = true;
            
            // Process each force
            forceCards.forEach((card, index) => {
                const forceNum = index + 1;
                const magInput = card.querySelector(`#force${forceNum}-mag`);
                const angleInput = card.querySelector(`#force${forceNum}-angle`);
                const xInput = card.querySelector(`#force${forceNum}-x`);
                const yInput = card.querySelector(`#force${forceNum}-y`);
                
                // Validate input
                if (!magInput.value || parseFloat(magInput.value) <= 0) {
                    magInput.style.borderColor = '#ef4444';
                    updateStatus('Invalid Input', `Force F${forceNum}: Enter positive magnitude`, 'error');
                    valid = false;
                    return;
                }
                
                const magnitude = parseFloat(magInput.value);
                const angle = parseFloat(angleInput.value) || 0;
                const x = parseFloat(xInput.value) || 0;
                const y = parseFloat(yInput.value) || 0;
                
                // Convert angle to radians
                const angleRad = (angle * Math.PI) / 180;
                
                // Calculate components
                const fx = magnitude * Math.cos(angleRad);
                const fy = magnitude * Math.sin(angleRad);
                
                // Calculate moment
                const dx = x - pivotX;
                const dy = y - pivotY;
                const moment = fx * dy - fy * dx;
                
                // Add to sums
                sumFx += fx;
                sumFy += fy;
                sumM += moment;
                
                // Build equation strings
                equationsFx.push(`${fx >= 0 ? '+' : '-'} ${Math.abs(fx).toFixed(2)}`);
                equationsFy.push(`${fy >= 0 ? '+' : '-'} ${Math.abs(fy).toFixed(2)}`);
                equationsM.push(`${moment >= 0 ? '+' : '-'} ${Math.abs(moment).toFixed(2)}`);
            });
            
            if (!valid) return;
            
            // Calculate reactions
            const Rx = -sumFx;
            const Ry = -sumFy;
            const isBalanced = Math.abs(sumM) < 0.01;
            
            // Display equations
            equationFxEl.querySelector('.equation-content').innerHTML = 
                `∑Fx = 0: ${equationsFx.join(' ')} + Rx = 0`;
            equationFyEl.querySelector('.equation-content').innerHTML = 
                `∑Fy = 0: ${equationsFy.join(' ')} + Ry = 0`;
            equationMEl.querySelector('.equation-content').innerHTML = 
                `∑M = 0: ${equationsM.join(' ')} = <strong>${sumM.toFixed(2)} N·m</strong>`;
            
            // Highlight equations
            [equationFxEl, equationFyEl, equationMEl].forEach(eq => {
                eq.classList.add('highlight');
                setTimeout(() => eq.classList.remove('highlight'), 1000);
            });
            
            // Display results
            resultRxEl.textContent = `${Rx.toFixed(2)} N`;
            resultRyEl.textContent = `${Ry.toFixed(2)} N`;
            
            // Color code results
            resultRxEl.style.color = Math.abs(Rx) > 0.01 ? '#1d4ed8' : '#059669';
            resultRyEl.style.color = Math.abs(Ry) > 0.01 ? '#1d4ed8' : '#059669';
            
            // Update status
            if (isBalanced) {
                updateStatus('System Balanced ✓', 'All equilibrium conditions satisfied', 'success');
                balanceIndicator.innerHTML = '<i class="fas fa-balance-scale" style="color: #10b981;"></i>';
                balanceIndicator.style.animation = 'fadeIn 0.5s ease';
            } else {
                updateStatus('Moment Not Balanced', `Net moment: ${sumM.toFixed(2)} N·m`, 'error');
                balanceIndicator.innerHTML = '<i class="fas fa-balance-scale" style="color: #ef4444;"></i>';
            }
            
            // Visual feedback for pivot
            pivotXInput.style.borderColor = '#10b981';
            pivotYInput.style.borderColor = '#10b981';
            setTimeout(() => {
                pivotXInput.style.borderColor = '';
                pivotYInput.style.borderColor = '';
            }, 1500);
        }
        
        // Reset calculator (keep one force)
        function resetCalculator() {
            // Clear all forces
            forcesContainer.innerHTML = '';
            forceCount = 0;
            
            // Reset pivot
            pivotXInput.value = 0;
            pivotYInput.value = 0;
            
            // Reset results
            equationFxEl.querySelector('.equation-content').textContent = '∑Fx = 0: Waiting for input...';
            equationFyEl.querySelector('.equation-content').textContent = '∑Fy = 0: Waiting for input...';
            equationMEl.querySelector('.equation-content').textContent = '∑M = 0: Waiting for input...';
            
            resultRxEl.textContent = '0.00 N';
            resultRyEl.textContent = '0.00 N';
            resultRxEl.style.color = '#1d4ed8';
            resultRyEl.style.color = '#1d4ed8';
            
            // Add new force
            setTimeout(() => {
                addNewForce();
                updateStatus('Calculator Reset', 'Ready for new calculations', 'info');
                balanceIndicator.innerHTML = '<i class="fas fa-balance-scale" style="color: #6b7280;"></i>';
            }, 300);
        }
        
        // Clear all forces
        function clearAllForces() {
            forcesContainer.innerHTML = '';
            forceCount = 0;
            setTimeout(() => {
                addNewForce();
                updateStatus('All forces cleared', 'New force added. Configure values.', 'warning');
            }, 300);
        }
    </script>
</body>
</html>
