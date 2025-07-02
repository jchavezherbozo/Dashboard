<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pace Production Summary</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 10px;
        }
        
        .dashboard {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 15px;
        }
        
        .widget {
            background: white;
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
        }
        
        .widget-header {
            background: linear-gradient(135deg, #4CAF50, #45a049);
            color: white;
            padding: 12px;
            border-radius: 8px;
            margin: -20px -20px 20px -20px;
            font-size: 16px;
            font-weight: bold;
            text-align: center;
        }
        
        .production-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .stat-card {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            border-left: 4px solid;
        }
        
        .stat-card.total { border-left-color: #2196F3; }
        .stat-card.progress { border-left-color: #FF9800; }
        .stat-card.completed { border-left-color: #4CAF50; }
        .stat-card.not-started { border-left-color: #607D8B; }
        
        .stat-number {
            font-size: 32px;
            font-weight: bold;
            color: #333;
            margin-bottom: 5px;
        }
        
        .stat-label {
            font-size: 14px;
            color: #666;
            font-weight: 500;
        }
        
        .visual-chart {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 20px;
            text-align: center;
        }
        
        .pie-visual {
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 20px 0;
        }
        
        .pie-slice {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            position: relative;
            background: conic-gradient(
                #FF9800 0deg 16deg,
                #607D8B 16deg 360deg
            );
            border: 4px solid white;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }
        
        .pie-center {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 18px;
            color: #333;
        }
        
        .legend {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 15px;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 12px;
        }
        
        .legend-color {
            width: 12px;
            height: 12px;
            border-radius: 50%;
        }
        
        .delay-list {
            display: grid;
            gap: 12px;
        }
        
        .delay-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px;
            background: #f8f9fa;
            border-radius: 8px;
            border-left: 4px solid;
        }
        
        .delay-item.rework { border-left-color: #2196F3; }
        .delay-item.labor { border-left-color: #9C27B0; }
        .delay-item.parts { border-left-color: #FFC107; }
        
        .delay-info h4 {
            color: #333;
            font-size: 14px;
            margin-bottom: 3px;
        }
        
        .delay-info p {
            color: #666;
            font-size: 12px;
        }
        
        .delay-count {
            font-size: 24px;
            font-weight: bold;
            color: #333;
            min-width: 40px;
            text-align: center;
        }
        
        .delay-visual {
            display: flex;
            gap: 5px;
            margin-top: 15px;
            height: 60px;
            align-items: end;
            justify-content: center;
        }
        
        .bar {
            width: 40px;
            border-radius: 4px 4px 0 0;
            display: flex;
            align-items: end;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 12px;
            padding-bottom: 5px;
        }
        
        .bar.rework { background: #2196F3; height: 5px; }
        .bar.labor { background: #9C27B0; height: 5px; }
        .bar.parts { background: #FFC107; height: 100%; }
        
        .payment-section {
            text-align: center;
        }
        
        .payment-main {
            background: linear-gradient(135deg, #4CAF50, #45a049);
            color: white;
            padding: 25px;
            border-radius: 12px;
            margin-bottom: 20px;
        }
        
        .payment-amount {
            font-size: 28px;
            font-weight: bold;
            margin-bottom: 8px;
        }
        
        .payment-label {
            font-size: 14px;
            opacity: 0.9;
        }
        
        .payment-breakdown {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }
        
        .payment-item {
            padding: 15px;
            border-radius: 10px;
            text-align: center;
        }
        
        .payment-item.current {
            background: #e3f2fd;
            color: #1976d2;
        }
        
        .payment-item.remaining {
            background: #f3e5f5;
            color: #7b1fa2;
        }
        
        .payment-item h4 {
            margin-bottom: 8px;
            font-size: 14px;
        }
        
        .payment-item .amount {
            font-size: 18px;
            font-weight: bold;
        }
        
        .title {
            text-align: center;
            color: white;
            font-size: 24px;
            font-weight: bold;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
    </style>
</head>
<body>
    <h1 class="title">🏭 Pace Production Summary Dashboard</h1>
    
    <div class="dashboard">
        <!-- Production Snapshot -->
        <div class="widget">
            <div class="widget-header">
                📊 Production Snapshot
            </div>
            
            <div class="production-grid">
                <div class="stat-card total">
                    <div class="stat-number">22</div>
                    <div class="stat-label">Total Buses</div>
                </div>
                
                <div class="stat-card progress">
                    <div class="stat-number">1</div>
                    <div class="stat-label">In Progress</div>
                </div>
                
                <div class="stat-card completed">
                    <div class="stat-number">0</div>
                    <div class="stat-label">Completed</div>
                </div>
                
                <div class="stat-card not-started">
                    <div class="stat-number">21</div>
                    <div class="stat-label">Not Started</div>
                </div>
            </div>
            
            <div class="visual-chart">
                <div class="pie-visual">
                    <div class="pie-slice">
                        <div class="pie-center">22</div>
                    </div>
                </div>
                <div class="legend">
                    <div class="legend-item">
                        <div class="legend-color" style="background: #FF9800;"></div>
                        <span>In Progress (5%)</span>
                    </div>
                    <div class="legend-item">
                        <div class="legend-color" style="background: #607D8B;"></div>
                        <span>Not Started (95%)</span>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Delay Reasons -->
        <div class="widget">
            <div class="widget-header">
                ⚠️ Delay Reasons
            </div>
            
            <div class="delay-list">
                <div class="delay-item rework">
                    <div class="delay-info">
                        <h4>Rework / Quality Issue</h4>
                        <p>Production quality concerns</p>
                    </div>
                    <div class="delay-count">0</div>
                </div>
                
                <div class="delay-item labor">
                    <div class="delay-info">
                        <h4>Labor Shortage</h4>
                        <p>Insufficient workforce</p>
                    </div>
                    <div class="delay-count">0</div>
                </div>
                
                <div class="delay-item parts">
                    <div class="delay-info">
                        <h4>Parts Not Available</h4>
                        <p>Supply chain issues</p>
                    </div>
                    <div class="delay-count">4</div>
                </div>
            </div>
            
            <div class="delay-visual">
                <div class="bar rework">0</div>
                <div class="bar labor">0</div>
                <div class="bar parts">4</div>
            </div>
        </div>
        
        <!-- Payment Status -->
        <div class="widget">
            <div class="widget-header">
                💰 Payment Status
            </div>
            
            <div class="payment-section">
                <div class="payment-main">
                    <div class="payment-amount">$27,019,510.98</div>
                    <div class="payment-label">Total Contract Value</div>
                </div>
                
                <div class="payment-breakdown">
                    <div class="payment-item current">
                        <h4>Current</h4>
                        <div class="amount">$27,019,510.98</div>
                    </div>
                    
                    <div class="payment-item remaining">
                        <h4>Remaining</h4>
                        <div class="amount">$26,719,510.98</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
