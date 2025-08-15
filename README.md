# calculatorKaumatua-Energy-Revenue-
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kaumatua Energy - Investor Relations Dashboard</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
            color: #e2e8f0;
            min-height: 100vh;
            line-height: 1.6;
        }

        .dashboard {
            max-width: 1400px;
            margin: 0 auto;
            padding: 2rem;
        }

        .header {
            text-align: center;
            margin-bottom: 3rem;
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(59, 130, 246, 0.1) 0%, transparent 70%);
            animation: pulse 4s ease-in-out infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); opacity: 0.5; }
            50% { transform: scale(1.1); opacity: 0.8; }
        }

        h1 {
            font-size: 2.5rem;
            font-weight: 700;
            background: linear-gradient(135deg, #3b82f6 0%, #8b5cf6 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            position: relative;
            z-index: 1;
        }

        .subtitle {
            color: #94a3b8;
            font-size: 1.1rem;
            margin-top: 0.5rem;
            position: relative;
            z-index: 1;
        }

        .metrics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.5rem;
            margin-bottom: 3rem;
        }

        .metric-card {
            background: rgba(30, 41, 59, 0.5);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(59, 130, 246, 0.2);
            border-radius: 12px;
            padding: 1.5rem;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .metric-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, #3b82f6 0%, #8b5cf6 100%);
            transform: scaleX(0);
            transition: transform 0.3s ease;
        }

        .metric-card:hover {
            transform: translateY(-2px);
            border-color: rgba(59, 130, 246, 0.4);
            box-shadow: 0 10px 40px rgba(59, 130, 246, 0.1);
        }

        .metric-card:hover::before {
            transform: scaleX(1);
        }

        .metric-label {
            color: #94a3b8;
            font-size: 0.875rem;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .metric-value {
            font-size: 2rem;
            font-weight: 700;
            margin-top: 0.5rem;
            background: linear-gradient(135deg, #60a5fa 0%, #a78bfa 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .metric-change {
            font-size: 0.875rem;
            margin-top: 0.25rem;
            display: flex;
            align-items: center;
            gap: 0.25rem;
        }

        .positive { color: #10b981; }
        .negative { color: #ef4444; }

        .section {
            background: rgba(30, 41, 59, 0.3);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(59, 130, 246, 0.1);
            border-radius: 16px;
            padding: 2rem;
            margin-bottom: 2rem;
        }

        .section-title {
            font-size: 1.5rem;
            font-weight: 600;
            margin-bottom: 1.5rem;
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .timeline-container {
            overflow-x: auto;
            padding: 1rem 0;
        }

        .timeline {
            min-width: 1200px;
            height: 500px;
            position: relative;
            background: rgba(15, 23, 42, 0.5);
            border-radius: 12px;
            padding: 2rem;
        }

        .timeline-item {
            position: absolute;
            min-height: 50px;
            border-radius: 8px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            padding: 0.75rem 1rem;
            font-size: 0.875rem;
            font-weight: 500;
            transition: all 0.3s ease;
            cursor: pointer;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
        }
        .timeline-item.top-label {
    overflow: visible !important;
    position: absolute !important;
}

        .timeline-item.top-label .timeline-item-title {
    position: absolute;
    bottom: 100%;              /* sit above the bar */
    left: 50%;                 /* center horizontally */
    transform: translateX(-50%);
    white-space: nowrap;       /* single line only */
    margin-bottom: 6px;
    font-weight: 700;
    line-height: 1.1;
    pointer-events: none;
}




        .timeline-item:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
            z-index: 10;
        }

        .timeline-item-title {
            font-weight: 600;
            margin-bottom: 0.25rem;
        }

        .timeline-item-date {
            font-size: 0.75rem;
            opacity: 0.9;
        }

        .timeline-grid {
            position: absolute;
            top: 40px;
            left: 0;
            right: 0;
            bottom: 0;
            display: grid;
            grid-template-columns: repeat(48, 1fr);
            opacity: 0.1;
        }

        .timeline-grid-line {
            border-left: 1px solid #3b82f6;
        }

        .timeline-grid-line:nth-child(12n) {
            border-left: 2px solid #3b82f6;
            opacity: 0.3;
        }

        .timeline-years {
            position: absolute;
            top: 10px;
            left: 2rem;
            right: 2rem;
            display: flex;
            justify-content: space-between;
            color: #94a3b8;
            font-size: 0.875rem;
            font-weight: 600;
        }

        .scenario-controls {
            background: rgba(15, 23, 42, 0.5);
            padding: 1.5rem;
            border-radius: 12px;
            margin-bottom: 1.5rem;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
        }

        .control-group {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }

        .control-label {
            font-size: 0.875rem;
            color: #94a3b8;
            text-transform: uppercase;
            letter-spacing: 0.05em;
        }

        .control-input {
            background: rgba(30, 41, 59, 0.5);
            border: 1px solid rgba(59, 130, 246, 0.3);
            color: #e2e8f0;
            padding: 0.5rem;
            border-radius: 6px;
            font-size: 0.875rem;
            transition: all 0.2s ease;
        }

        .control-input:focus {
            outline: none;
            border-color: rgba(59, 130, 246, 0.6);
            background: rgba(59, 130, 246, 0.1);
        }

        .slider-container {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .slider {
            flex: 1;
            -webkit-appearance: none;
            appearance: none;
            height: 6px;
            background: rgba(59, 130, 246, 0.2);
            border-radius: 3px;
            outline: none;
        }

        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 16px;
            height: 16px;
            background: linear-gradient(135deg, #3b82f6 0%, #8b5cf6 100%);
            border-radius: 50%;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .slider::-webkit-slider-thumb:hover {
            transform: scale(1.2);
            box-shadow: 0 0 10px rgba(59, 130, 246, 0.5);
        }

        .slider-value {
            min-width: 60px;
            text-align: right;
            font-weight: 600;
            color: #60a5fa;
        }

        .investor-table-wrapper {
            overflow-x: auto;
            border-radius: 12px;
            border: 1px solid rgba(59, 130, 246, 0.1);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: rgba(15, 23, 42, 0.3);
        }

        th, td {
            padding: 1rem;
            text-align: left;
        }

        th {
            background: rgba(15, 23, 42, 0.8);
            font-weight: 600;
            color: #94a3b8;
            text-transform: uppercase;
            font-size: 0.875rem;
            letter-spacing: 0.05em;
            position: sticky;
            top: 0;
            z-index: 10;
        }

        tbody tr {
            border-top: 1px solid rgba(59, 130, 246, 0.1);
            transition: all 0.2s ease;
        }

        tbody tr:hover {
            background: rgba(59, 130, 246, 0.05);
        }

        .editable {
            background: transparent;
            border: 1px solid transparent;
            padding: 0.5rem;
            border-radius: 4px;
            color: inherit;
            font: inherit;
            width: 100%;
            transition: all 0.2s ease;
        }

        .editable.investor-name {
            min-width: 240px;
        }

        .editable:hover {
            border-color: rgba(59, 130, 246, 0.3);
            background: rgba(59, 130, 246, 0.05);
        }

        .editable:focus {
            outline: none;
            border-color: rgba(59, 130, 246, 0.6);
            background: rgba(59, 130, 246, 0.1);
        }

        select.editable {
            cursor: pointer;
        }

        .status-badge {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            padding: 0.375rem 0.875rem;
            border-radius: 9999px;
            font-size: 0.875rem;
            font-weight: 500;
            white-space: nowrap;
        }

        .status-indicator {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            animation: pulse 2s ease-in-out infinite;
        }

        .status-active {
            background: rgba(34, 197, 94, 0.1);
            color: #22c55e;
        }

        .status-active .status-indicator {
            background: #22c55e;
        }

        .status-pending {
            background: rgba(251, 191, 36, 0.1);
            color: #fbbf24;
        }

        .status-pending .status-indicator {
            background: #fbbf24;
        }

        .status-completed {
            background: rgba(59, 130, 246, 0.1);
            color: #3b82f6;
        }

        .status-completed .status-indicator {
            background: #3b82f6;
        }

        .status-declined {
            background: rgba(239, 68, 68, 0.1);
            color: #ef4444;
        }

        .status-declined .status-indicator {
            background: #ef4444;
        }

        .investment-type {
            display: inline-flex;
            align-items: center;
            padding: 0.375rem 0.875rem;
            background: rgba(139, 92, 246, 0.1);
            color: #a78bfa;
            border-radius: 6px;
            font-size: 0.875rem;
            white-space: nowrap;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: rgba(59, 130, 246, 0.1);
            border-radius: 4px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #3b82f6 0%, #8b5cf6 100%);
            border-radius: 4px;
            transition: width 0.3s ease;
        }

        .investor-name {
            font-weight: 600;
            color: #e2e8f0;
        }

        th:first-child, td:first-child {
            min-width: 250px;
            white-space: nowrap;
        }

        .amount-input {
            font-weight: 600;
            color: #60a5fa;
            width: 120px;
            text-align: right;
        }

        .add-investor-btn {
            background: linear-gradient(135deg, #3b82f6 0%, #8b5cf6 100%);
            color: white;
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            margin-top: 1rem;
        }

        .add-investor-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(59, 130, 246, 0.3);
        }

        .delete-btn {
            background: rgba(239, 68, 68, 0.1);
            color: #ef4444;
            border: 1px solid rgba(239, 68, 68, 0.3);
            padding: 0.25rem 0.75rem;
            border-radius: 6px;
            cursor: pointer;
            font-size: 0.875rem;
            transition: all 0.2s ease;
        }

        .delete-btn:hover {
            background: rgba(239, 68, 68, 0.2);
            border-color: rgba(239, 68, 68, 0.5);
        }

        .total-row {
            background: rgba(59, 130, 246, 0.1);
            font-weight: 700;
        }

        .total-row td {
            padding: 1.25rem 1rem;
            border-top: 2px solid rgba(59, 130, 246, 0.3);
        }

        .icon {
            width: 20px;
            height: 20px;
            display: inline-block;
            vertical-align: middle;
        }

        .chart-container {
            height: 300px;
            margin-top: 1.5rem;
            position: relative;
        }

        .analysis-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.5rem;
            margin-top: 1.5rem;
        }

        .analysis-card {
            background: rgba(15, 23, 42, 0.5);
            border: 1px solid rgba(59, 130, 246, 0.2);
            border-radius: 12px;
            padding: 1.5rem;
        }

        .analysis-title {
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 1rem;
            color: #60a5fa;
        }

        .analysis-metric {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.5rem 0;
            border-bottom: 1px solid rgba(59, 130, 246, 0.1);
        }

        .analysis-metric:last-child {
            border-bottom: none;
        }

        .analysis-label {
            color: #94a3b8;
            font-size: 0.875rem;
        }

        .analysis-value {
            font-weight: 600;
            color: #e2e8f0;
        }

        @media (max-width: 768px) {
            .dashboard {
                padding: 1rem;
            }

            h1 {
                font-size: 2rem;
            }

            .metrics-grid {
                grid-template-columns: 1fr;
            }

            .section {
                padding: 1.5rem;
            }

            table {
                font-size: 0.875rem;
            }

            th, td {
                padding: 0.75rem 0.5rem;
            }

            .amount-input {
                width: 100px;
            }

            .scenario-controls {
                grid-template-columns: 1fr;
            }
        }

        .mt-2 { margin-top: 0.5rem; }
    </style>
    
    
    <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 64 64%22><rect width=%2264%22 height=%2264%22 fill=%22black%22/><text x=%2250%%22 y=%2250%%22 dominant-baseline=%22middle%22 text-anchor=%22middle%22 font-family=%22Arial, sans-serif%22 font-size=%2236%22 fill=%22white%22>K</text></svg>">
    <link rel="alternate icon" type="image/png" href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADElEQVR4nGNgYGAAAAAEAAEL5wKeAAAAAElFTkSuQmCC">
    <link rel="shortcut icon" type="image/png" href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADElEQVR4nGNgYGAAAAAEAAEL5wKeAAAAAElFTkSuQmCC">
    <link rel="apple-touch-icon" href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADElEQVR4nGNgYGAAAAAEAAEL5wKeAAAAAElFTkSuQmCC">
</head>
<body>
    <div class="dashboard">
        <header class="header">
            <h1>Kaumatua Energy</h1>
            <p class="subtitle">Investor Relations Dashboard & Scenario Analysis</p>
        </header>

        <div class="metrics-grid">
            <div class="metric-card">
                <div class="metric-label">Total Target Raise</div>
                <div class="metric-value" id="totalTarget">$40M</div>
                <div class="metric-change positive">
                    <span>↑</span> Phase 2 + Pre-IPO + IPO
                </div>
            </div>
            <div class="metric-card">
                <div class="metric-label">2029 Revenue Target</div>
                <div class="metric-value" id="revenueTarget">$240M</div>
                <div class="metric-change positive">
                    <span>↑</span> 20% growth from 2028
                </div>
            </div>
            <div class="metric-card">
                <div class="metric-label">IPO Valuation Range</div>
                <div class="metric-value" id="valuationRange">$1.2-1.5B</div>
                <div class="metric-change">
                    Base Case Scenario
                </div>
            </div>
            <div class="metric-card">
                <div class="metric-label">Your 11% Stake Value</div>
                <div class="metric-value" id="stakeValue">$132-165M</div>
                <div class="metric-change">
                    <div class="progress-bar">
                        <div class="progress-fill" style="width: 75%"></div>
                    </div>
                </div>
            </div>
        </div>

        <div class="section">
            <h2 class="section-title">
                <svg class="icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M12 2L2 7v10c0 5.55 3.84 10.74 9 12 5.16-1.26 9-6.45 9-12V7l-10-5z"></path>
                </svg>
                IPO Pathway Timeline & Scenario Planning
            </h2>
            
            <div class="scenario-controls">
                <div class="control-group">
                    <label class="control-label">Valuation Scenario</label>
                    <select class="control-input" id="valuationScenario">
                        <option value="conservative">Conservative (18-22x)</option>
                        <option value="base" selected>Base Case (20-25x)</option>
                        <option value="optimistic">Optimistic (25-30x)</option>
                    </select>
                </div>
                <div class="control-group">
                    <label class="control-label">EBITDA Margin (%)</label>
                    <div class="slider-container">
                        <input type="range" class="slider" id="ebitdaMargin" min="30" max="45" value="40" step="1">
                        <span class="slider-value">40%</span>
                    </div>
                </div>
                <div class="control-group">
                    <label class="control-label">Revenue Growth to 2029 (%)</label>
                    <div class="slider-container">
                        <input type="range" class="slider" id="revenueGrowth" min="0" max="300" value="20" step="1">
                        <span class="slider-value">20%</span>
                    </div>
                </div>

                <div class="control-group">
                    <label class="control-label">Customer Growth to 2029 (%)</label>
                    <div class="slider-container">
                        <input type="range" class="slider" id="customerGrowth" min="0" max="300" value="20" step="1">
                        <span class="slider-value">20%</span>
                    </div>
                </div>

                <div class="control-group">
                    <label class="control-label">Dividend Payout Ratio (%)</label>
                    <div class="slider-container">
                        <input type="range" class="slider" id="payoutRatio" min="40" max="70" value="60" step="5">
                        <span class="slider-value">60%</span>
                    </div>
                </div>
                <div class="control-group">
                    <label class="control-label">Phase 2 PIF Investment ($M)</label>
                    <div class="slider-container">
                        <input type="range" class="slider" id="phase2Amount" min="10" max="25" value="15" step="1">
                        <span class="slider-value">$15M</span>
                    </div>
                </div>
                <div class="control-group">
                    <label class="control-label">Capital Deployment ($M)</label>
                    <div class="slider-container">
                        <input type="range" class="slider" id="phase3Amount" min="5" max="20" value="10" step="1">
                        <span class="slider-value">$10M</span>
                    </div>
                </div>
                <div class="control-group">
                    <label class="control-label">Timeline Compression</label>
                    <select class="control-input" id="timelineCompression">
                        <option value="1">Standard Timeline</option>
                        <option value="0.8">20% Faster</option>
                        <option value="1.2">20% Slower</option>
                    </select>
                </div>
            </div>

            <div class="timeline-container">
                <div class="timeline">
                    <div class="timeline-years">
                        <span>2025</span>
                        <span>2026</span>
                        <span>2027</span>
                        <span>2028</span>
                        <span>2029</span>
                    </div>
                    <div class="timeline-grid">
                        <!-- 48 grid lines for 4 years (12 months each) -->
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                        <div class="timeline-grid-line"></div>
                    </div>
                    
                    <div id="timelineItems">
                        <!-- Timeline items will be generated by JavaScript -->
                    </div>
                </div>
            </div>

            <div class="analysis-grid">
                <div class="analysis-card">
                    <div class="analysis-title">IPO Valuation Analysis</div>
                    <div class="analysis-metric">
                        <span class="analysis-label">2029 Revenue Projection</span>
                        <span class="analysis-value" id="revenue2029">$240M</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">EBITDA</span>
                        <span class="analysis-value" id="ebitda2029">$96M</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Net Income</span>
                        <span class="analysis-value" id="netIncome2029">$60M</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Enterprise Value</span>
                        <span class="analysis-value" id="enterpriseValue">$1.2-1.5B</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">P/E Multiple</span>
                        <span class="analysis-value" id="peMultiple">20-25x</span>
                    </div>
                </div>

                <div class="analysis-card">
                    <div class="analysis-title">Your Economic Interest (11%)</div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Stake Value at IPO</span>
                        <span class="analysis-value" id="yourStakeValue">$132-165M</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Annual Dividend Income</span>
                        <span class="analysis-value" id="annualDividend">$3.96-4.95M</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Quarterly Income</span>
                        <span class="analysis-value" id="quarterlyIncome">$990K-1.24M</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Dividend Yield on Value</span>
                        <span class="analysis-value" id="dividendYield">3.0%</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">5-Year Total Return</span>
                        <span class="analysis-value" id="totalReturn">$142-180M</span>
                    </div>
                </div>

                <div class="analysis-card">
                    <div class="analysis-title">Key Milestones</div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Customer Base Target</span>
                        <span class="analysis-value" id="customerTarget">50,000</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Revenue Run Rate</span>
                        <span class="analysis-value" id="revenueRunRate">$96M ARR</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Infrastructure Deployed</span>
                        <span class="analysis-value" id="infrastructure">100 MW</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Geographic Coverage</span>
                        <span class="analysis-value" id="coverage">4 Regions</span>
                    </div>
                </div>

                <div class="analysis-card">
                    <div class="analysis-title">Partner Wealth Distribution</div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Harminder Singh (33.33%)</span>
                        <span class="analysis-value" id="harminderShare">$1.32-1.65M/yr</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Sourabh Sahni (33.33%)</span>
                        <span class="analysis-value" id="sourabhShare">$1.32-1.65M/yr</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Chris Mathews (33.33%)</span>
                        <span class="analysis-value" id="chrisShare">$1.32-1.65M/yr</span>
                    </div>
                    <div class="analysis-metric">
                        <span class="analysis-label">Investment Multiple</span>
                        <span class="analysis-value" id="investmentMultiple">10-15x</span>
                    </div>
                </div>
            </div>
        </div>

        <div class="section">
            <h2 class="section-title">
                <svg class="icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path>
                    <circle cx="9" cy="7" r="4"></circle>
                    <path d="M23 21v-2a4 4 0 0 0-3-3.87"></path>
                    <path d="M16 3.13a4 4 0 0 1 0 7.75"></path>
                </svg>
                Investor Pipeline & Status
            </h2>
            <div class="investor-table-wrapper">
                <h3 style="margin: 0 0 0.75rem 0; color:#e2e8f0;">Pacific Infrastructure Fund (Limited Partnership) — Potential LP Investors (6)</h3>
                <table id="pifLpTable">
                    <thead>
                        <tr>
                            <th>Investor</th>
                            <th>Status</th>
                            <th>Commitment ($M)</th>
                            <th>Notes</th>
                            <th>Progress</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody id="pifLpTableBody"></tbody>
                    <tfoot>
                        <tr class="total-row">
                            <td colspan="2">TOTAL PIF (LP) PIPELINE</td>
                            <td id="totalPifLp" style="text-align:right; color:#60a5fa;">$0M</td>
                            <td colspan="3"></td>
                        </tr>
                    </tfoot>
                </table>

                <button class="add-investor-btn" onclick="addPifLpInvestor()">
                    <svg class="icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <line x1="12" y1="5" x2="12" y2="19"></line>
                        <line x1="5" y1="12" x2="19" y2="12"></line>
                    </svg>
                    Add PIF (LP) Investor
                </button>

                <h3 style="margin: 2rem 0 0.75rem 0; color:#e2e8f0;">Direct Investment into Kaumatua Energy — Potential Investors (4)</h3>
                <table id="directTable">
                    <thead>
                        <tr>
                            <th>Investor</th>
                            <th>Status</th>
                            <th>Amount ($M)</th>
                            <th>Instrument</th>
                            <th>Progress</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody id="directTableBody"></tbody>
                    <tfoot>
                        <tr class="total-row">
                            <td colspan="2">TOTAL DIRECT PIPELINE</td>
                            <td id="totalDirect" style="text-align:right; color:#60a5fa;">$0M</td>
                            <td colspan="3"></td>
                        </tr>
                    </tfoot>
                </table>

                <button class="add-investor-btn" onclick="addDirectInvestor()">
                    <svg class="icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <line x1="12" y1="5" x2="12" y2="19"></line>
                        <line x1="5" y1="12" x2="19" y2="12"></line>
                    </svg>
                    Add Direct Investor
                </button>
            </div>
            <style>
                .mini-badge{display:inline-block;padding:0.2rem 0.55rem;border-radius:9999px;background:rgba(99,102,241,0.12);border:1px solid rgba(99,102,241,0.35);color:#c7d2fe;font-size:.75rem}
            </style>
</div>
        <div class=\"section\">
            <h2 class="section-title">
                <svg class="icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M22 12h-4l-3 9L9 3l-3 9H2"></path>
                </svg>
                Investment Progress by Category
            </h2>
            <div class="chart-container">
                <canvas id="investmentChart"></canvas>
            </div>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <script>
        // Timeline phases data
        const phases = [
            {
                name: "Phase 1: Preparation",
                start: "2025-09",
                end: "2025-12",
                color: "#3b82f6",
                description: "Sep-Dec 2025"
            },
            {
                name: "Phase 2: PIF Investment",
                start: "2026-02",
                end: "2026-04",
                color: "#22c55e",
                description: "Feb-Apr 2026 ($15M)"
            },
            {
                name: "Phase 3: Capital Deployment",
                start: "2026-04",
                end: "2028-12",
                color: "#f97316",
                description: "Apr 2026-Dec 2028 (Deploy $10M)"
            },
            {
                name: "Phase 4: Rapid Growth",
                start: "2026-02",
                end: "2028-12",
                color: "#8b5cf6",
                description: "Feb 2026-Dec 2028"
            },
            {
                name: "Phase 5: Pre-IPO Positioning",
                start: "2028-02",
                end: "2028-12",
                color: "#ec4899",
                description: "Feb-Dec 2028"
            },
            {
                name: "Pre-IPO Placement",
                start: "2028-10",
                end: "2028-11",
                color: "#a16207",
                description: "Oct 2028 (Optional)"
            },
            {
                name: "IPO & NZX Listing",
                start: "2028-12",
                end: "2029-01",
                color: "#ef4444",
                description: "Dec 2028"
            },
            {
                name: "Post-Listing IR",
                start: "2029-01",
                end: "2029-12",
                color: "#6b7280",
                description: "2029 onwards"
            }
        ];

        // Calculate timeline positions
        function calculateTimelinePosition(dateStr, compression = 1) {
            const startDate = new Date('2025-01-01');
            const targetDate = new Date(dateStr);
            const monthsDiff = (targetDate.getFullYear() - startDate.getFullYear()) * 12 + 
                             (targetDate.getMonth() - startDate.getMonth());
            return (monthsDiff * 25 * compression) + 32; // 25px per month, 32px offset
        }

        // Status badge mapping
        const statusClasses = {
            "Active Discussion": "status-active",
            "Due Diligence": "status-active",
            "MOU Negotiation": "status-active",
            "Term Sheet": "status-pending",
            "Initial Contact": "status-pending",
            "Committed": "status-completed",
            "Not Proceeding": "status-declined"
        };

        // Update scenario analysis
        function updateScenarioAnalysis() {
            const scenario = document.getElementById('valuationScenario').value;
            const ebitdaMargin = parseInt(document.getElementById('ebitdaMargin').value);
            const revenueGrowth = parseInt(document.getElementById('revenueGrowth').value);
            const payoutRatio = parseInt(document.getElementById('payoutRatio').value);
            const phase2 = parseInt(document.getElementById('phase2Amount').value);
            const capexDeploy = parseInt(document.getElementById('phase3Amount').value);
            // Customer growth slider
            const customerGrowthEl = document.getElementById('customerGrowth');
            const customerGrowth = customerGrowthEl ? parseInt(customerGrowthEl.value) : 20;
            if (customerGrowthEl) customerGrowthEl.nextElementSibling.textContent = `${customerGrowth}%`;
            
            // Update slider values
            document.querySelector('#ebitdaMargin').nextElementSibling.textContent = `${ebitdaMargin}%`;
            document.querySelector('#revenueGrowth').nextElementSibling.textContent = `${revenueGrowth}%`;
            document.querySelector('#payoutRatio').nextElementSibling.textContent = `${payoutRatio}%`;
            document.querySelector('#phase2Amount').nextElementSibling.textContent = `$${phase2}M`;
            document.querySelector('#phase3Amount').nextElementSibling.textContent = `$${capexDeploy}M`;
            
            // Calculate 2029 revenue based on growth from 2028 baseline of $200M
            const revenue2028 = 200;
            const revenue2029 = revenue2028 * (1 + revenueGrowth / 100);
            document.getElementById('revenue2029').textContent = `$${Math.round(revenue2029)}M`;
            document.getElementById('revenueTarget').textContent = `$${Math.round(revenue2029)}M`;
            
            // Calculate EBITDA and Net Income
            const ebitda = revenue2029 * (ebitdaMargin / 100);
            const netIncome = ebitda * 0.625; // Assuming 62.5% conversion from EBITDA to Net Income
            
            document.getElementById('ebitda2029').textContent = `$${Math.round(ebitda)}M`;
            document.getElementById('netIncome2029').textContent = `$${Math.round(netIncome)}M`;
            
            // Customers based on customer growth from 2028 base
            const customers2028 = 40000;
            const customers2029 = Math.round(customers2028 * (1 + customerGrowth / 100));
            const customerTargetEl = document.getElementById('customerTarget');
            if (customerTargetEl) customerTargetEl.textContent = customers2029.toLocaleString();
            // Valuation ranges based on scenario
            let peMin, peMax, evMultiple;
            switch(scenario) {
                case 'conservative':
                    peMin = 18; peMax = 22;
                    evMultiple = 2.5;
                    break;
                case 'optimistic':
                    peMin = 25; peMax = 30;
                    evMultiple = 4.0;
                    break;
                default: // base case
                    peMin = 20; peMax = 25;
                    evMultiple = 3.25;
            }
            
            // Calculate valuations
            const valuationMin = Math.round(netIncome * peMin);
            const valuationMax = Math.round(netIncome * peMax);
            const valuationMid = Math.round((valuationMin + valuationMax) / 2);
            
            document.getElementById('enterpriseValue').textContent = `$${(valuationMin/1000).toFixed(1)}-${(valuationMax/1000).toFixed(1)}B`;
            document.getElementById('valuationRange').textContent = `$${(valuationMin/1000).toFixed(1)}-${(valuationMax/1000).toFixed(1)}B`;
            document.getElementById('peMultiple').textContent = `${peMin}-${peMax}x`;
            
            // Calculate 11% stake value
            const stakeMin = Math.round(valuationMin * 0.11);
            const stakeMax = Math.round(valuationMax * 0.11);
            
            document.getElementById('yourStakeValue').textContent = `$${stakeMin}-${stakeMax}M`;
            document.getElementById('stakeValue').textContent = `$${stakeMin}-${stakeMax}M`;
            
            // Calculate dividend income
            const totalDividends = netIncome * (payoutRatio / 100);
            const yourDividends = totalDividends * 0.11;
            const annualMin = yourDividends * 0.9; // -10% range
            const annualMax = yourDividends * 1.1; // +10% range
            
            document.getElementById('annualDividend').textContent = `$${annualMin.toFixed(2)}-${annualMax.toFixed(2)}M`;
            document.getElementById('quarterlyIncome').textContent = `$${(annualMin * 250).toFixed(0)}K-${(annualMax * 250).toFixed(0)}K`;
            
            // Calculate dividend yield
            const avgStakeValue = (stakeMin + stakeMax) / 2;
            const dividendYield = (yourDividends / avgStakeValue) * 100;
            document.getElementById('dividendYield').textContent = `${dividendYield.toFixed(1)}%`;
            
            // Calculate total returns (stake value + 5 years of dividends)
            const cumulativeDividends = yourDividends * 4; // ~4 years of dividends
            const totalReturnMin = stakeMin + Math.round(cumulativeDividends * 0.8);
            const totalReturnMax = stakeMax + Math.round(cumulativeDividends * 1.2);
            
            document.getElementById('totalReturn').textContent = `$${totalReturnMin}-${totalReturnMax}M`;
            
            // Update wealth distribution
            const partnerShare = annualMin / 3; // Each partner gets 1/3
            const partnerShareMax = annualMax / 3;
            document.getElementById('harminderShare').textContent = `${partnerShare.toFixed(2)}-${partnerShareMax.toFixed(2)}M/yr`;
            document.getElementById('sourabhShare').textContent = `${partnerShare.toFixed(2)}-${partnerShareMax.toFixed(2)}M/yr`;
            document.getElementById('chrisShare').textContent = `${partnerShare.toFixed(2)}-${partnerShareMax.toFixed(2)}M/yr`;
            
            // Update phase descriptions
            phases[1].description = `Feb-Apr 2026 ($${phase2}M)`;
            phases[2].description = `Apr 2026-Dec 2028 (Deploy $${capexDeploy}M)`;
            
            
            // Re-render timeline to reflect updated descriptions (e.g., Deploy $XM)
            renderTimelineFixed();
    // Update other metrics based on new projections
            updateMilestones(revenue2029);
            // Persist scenario settings on every update
            try { saveSettings(); } catch(e) {}
        }
        
        function updateMilestones(revenue2029) {
            // Current revenue run rate (pathway to 2029)
            const currentRunRate = Math.round(revenue2029 * 0.4); // Assuming 40% of 2029 target by now
            document.getElementById('revenueRunRate').textContent = `$${currentRunRate}M ARR`;

            // Infrastructure based on revenue
            const infrastructure = Math.round((revenue2029 / 240) * 100);
            document.getElementById('infrastructure').textContent = `${infrastructure} MW`;
    // Coverage based on scale
            const regions = revenue2029 > 250 ? '5+ Regions' : '4 Regions';
            document.getElementById('coverage').textContent = regions;
        }

        // Render investor table
        function renderInvestorTable() {
            const tbody = document.getElementById('investorTableBody');
            tbody.innerHTML = '';
            
            investors.forEach((investor, index) => {
                const row = tbody.insertRow();
                row.innerHTML = `
                    <td>
                        <input type="text" class="editable investor-name" value="${investor.name}" 
                               onchange="updateInvestor(${index}, 'name', this.value)"
                               style="min-width: 240px;">
                    </td>
                    <td>
                        <select class="editable" onchange="updateInvestor(${index}, 'status', this.value)">
                            <option value="Initial Contact" ${investor.status === 'Initial Contact' ? 'selected' : ''}>Initial Contact</option>
                            <option value="Active Discussion" ${investor.status === 'Active Discussion' ? 'selected' : ''}>Active Discussion</option>
                            <option value="Due Diligence" ${investor.status === 'Due Diligence' ? 'selected' : ''}>Due Diligence</option>
                            <option value="Term Sheet" ${investor.status === 'Term Sheet' ? 'selected' : ''}>Term Sheet</option>
                            <option value="MOU Negotiation" ${investor.status === 'MOU Negotiation' ? 'selected' : ''}>MOU Negotiation</option>
                            <option value="Committed" ${investor.status === 'Committed' ? 'selected' : ''}>Committed</option>
                            <option value="Not Proceeding" ${investor.status === 'Not Proceeding' ? 'selected' : ''}>Not Proceeding</option>
                        </select>
                        <div class="status-badge ${statusClasses[investor.status]} mt-2">
                            <span class="status-indicator"></span>
                            ${investor.status}
                        </div>
                    </td>
                    <td>
                        <input type="number" class="editable amount-input" value="${investor.amount}" 
                               step="0.1" min="0" onchange="updateInvestor(${index}, 'amount', parseFloat(this.value))">
                    </td>
                    <td>
                        <select class="editable" onchange="updateInvestor(${index}, 'shareClass', this.value)">
                            <option value="Series A Preferred" ${investor.shareClass === 'Series A Preferred' ? 'selected' : ''}>Series A Preferred</option>
                            <option value="Series A Common" ${investor.shareClass === 'Series A Common' ? 'selected' : ''}>Series A Common</option>
                            <option value="Convertible Note" ${investor.shareClass === 'Convertible Note' ? 'selected' : ''}>Convertible Note</option>
                            <option value="Pre-IPO Round" ${investor.shareClass === 'Pre-IPO Round' ? 'selected' : ''}>Pre-IPO Round</option>
                            <option value="Joint Venture" ${investor.shareClass === 'Joint Venture' ? 'selected' : ''}>Joint Venture</option>
                        </select>
                        <div class="investment-type mt-2">${investor.shareClass}</div>
                    </td>
                    <td>
                        <input type="text" class="editable" value="${investor.goal}" 
                               onchange="updateInvestor(${index}, 'goal', this.value)">
                    </td>
                    <td>
                        <div style="display: flex; align-items: center; gap: 0.5rem;">
                            <input type="number" class="editable" style="width: 60px;" value="${investor.progress}" 
                                   min="0" max="100" onchange="updateInvestor(${index}, 'progress', parseInt(this.value))">
                            <span style="font-size: 0.875rem;">%</span>
                            <div class="progress-bar" style="width: 100px;">
                                <div class="progress-fill" style="width: ${investor.progress}%"></div>
                            </div>
                        </div>
                    </td>
                    <td>
                        <button class="delete-btn" onclick="deleteInvestor(${index})">Delete</button>
                    </td>
                `;
            });
            
            updateTotals();
        }

        // Update investor data
        function updateInvestor(index, field, value) {
            investors[index][field] = value;
            renderInvestorTable();
            updateChart();
        }

        // Add new investor
        function addInvestor() {
            investors.push({
                name: "New Investor",
                status: "Initial Contact",
                amount: 0,
                shareClass: "Series A Preferred",
                goal: "To be defined",
                progress: 0
            });
            renderInvestorTable();
            updateChart();
        }

        // Delete investor
        function deleteInvestor(index) {
            if (confirm('Are you sure you want to delete this investor?')) {
                investors.splice(index, 1);
                renderInvestorTable();
                updateChart();
            }
        }

        // Update totals
        function updateTotals() {
            const total = investors.reduce((sum, inv) => sum + inv.amount, 0);
            document.getElementById('totalAmount').textContent = `$${total}M`;
        }

        // Investment Progress Chart
        
        let chart;
        
function updateChart(){
    const ctx = document.getElementById('investmentChart').getContext('2d');
    const pifTotal = (window.pifLpInvestors||[]).reduce((s,i)=>s+(i.amount||0),0);
    const directTotal = (window.directInvestors||[]).reduce((s,i)=>s+(i.amount||0),0);
    const targets = { 'PIF (LP)': 25, 'Direct': 15 };
    if (chart) chart.destroy();
    chart = new Chart(ctx, {
        type: 'bar',
        data: {
            labels: ['PIF (LP)', 'Direct'],
            datasets: [
                { label: 'Target ($M)', data: [targets['PIF (LP)'], targets['Direct']] },
                { label: 'Pipeline / Active ($M)', data: [pifTotal, directTotal] }
            ]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: { legend: { labels: { color: '#e2e8f0', font: { size: 12 } } } },
            scales: {
                y: { beginAtZero: true, grid: { color: 'rgba(148,163,184,0.1)' }, ticks: { color: '#94a3b8' } },
                x: { grid: { display: false }, ticks: { color: '#94a3b8' } }
            }
        }
    });
}


        
        // --- Persistence for scenario controls ---
        const CONTROL_IDS = ['valuationScenario','ebitdaMargin','revenueGrowth','payoutRatio','phase2Amount','phase3Amount','timelineCompression','customerGrowth'];
        function saveSettings() {
            CONTROL_IDS.forEach(id => {
                const el = document.getElementById(id);
                if (!el) return;
                localStorage.setItem('keScenario_' + id, el.value);
            });
        }
        function loadSettings() {
            CONTROL_IDS.forEach(id => {
                const el = document.getElementById(id);
                if (!el) return;
                const saved = localStorage.getItem('keScenario_' + id);
                if (saved !== null) {
                    el.value = saved;
                }
            
        // Attach auto-save to all known controls
        document.addEventListener('DOMContentLoaded', () => {
            (CONTROL_IDS || []).forEach(id => {
                const el = document.getElementById(id);
                if (!el) return;
                const evt = (el.tagName === 'SELECT') ? 'change' : 'input';
                el.addEventListener(evt, () => { try { saveSettings(); } catch(e) {} });
            });
        });
    });
        }


        // ----- Clean rebuilt timeline renderer -----
        function renderTimelineFixed() {
            const timelineItems = document.getElementById('timelineItems');
            const compressionSelect = document.getElementById('timelineCompression');
            const compression = compressionSelect ? parseFloat(compressionSelect.value) : 1;
            if (!timelineItems) return;
            timelineItems.innerHTML = '';
            const baseTop = 60;
            const itemHeight = 50;
            const itemSpacing = 5;
            phases.forEach((phase, index) => {
                const startPos = calculateTimelinePosition(phase.start, compression);
                const endPos = calculateTimelinePosition(phase.end, compression);
                const width = endPos - startPos;
                let adjustedLeft = startPos;
                let adjustedWidth = width;
                // Phase 2: slight left offset
                if (phase.name.startsWith("Phase 2")) {
                    const extra = 12;
                    adjustedLeft = startPos + extra;
                    adjustedWidth = Math.max(8, width - extra);
                }
                // IPO-related: minimum width for visibility
                if (phase.name.includes("IPO")) {
                    const minW = 180;
                    if (adjustedWidth < minW) {
                        const extra = minW - adjustedWidth;
                        adjustedLeft = Math.max(32, adjustedLeft - extra / 2);
                        adjustedWidth = minW;
                    }
                }
                const item = document.createElement('div');
                item.className = 'timeline-item';
                if (phase.name.startsWith("Phase 1") || phase.name.startsWith("Phase 2") || phase.name.includes("IPO")) {
                    item.classList.add('top-label');
                }
                item.style.cssText = `
                    background: ${phase.color};
                    top: ${baseTop + (index % 8) * (itemHeight + itemSpacing)}px;
                    left: ${adjustedLeft}px;
                    width: ${adjustedWidth}px;
                `;
                item.innerHTML = `
                    <div class="timeline-item-title">${phase.name}</div>
                    <div class="timeline-item-date">${phase.description}</div>
                `;
                timelineItems.appendChild(item);
            });
        }


        // --- Categorised investor data & renderers (injected) ---
        window.pifLpInvestors = window.pifLpInvestors || [
            { name: "Pacific Superannuation Fund", status: "Active Discussion", amount: 5, notes: "Anchor LP candidate", progress: 60 },
            { name: "Regional Infrastructure Pool", status: "Due Diligence", amount: 3, notes: "ESG mandate", progress: 45 },
            { name: "Coastal Maritime Fund", status: "Initial Contact", amount: 2, notes: "Logistics angle", progress: 20 },
            { name: "Southern Growth Partners", status: "MOU Negotiation", amount: 4, notes: "Co-invest rights", progress: 55 },
            { name: "Island Capital Partners", status: "Active Discussion", amount: 3, notes: "Climate focus", progress: 35 },
            { name: "Harbour Endowment Trust", status: "Term Sheet", amount: 2, notes: "Seed LP terms", progress: 80 }
        ];
        window.directInvestors = window.directInvestors || [
            { name: "Meridian Energy Ventures", status: "Active Discussion", amount: 5, instrument: "Series A Preferred", progress: 70 },
            { name: "Genesis Energy Innovations", status: "Active Discussion", amount: 4, instrument: "Series A Preferred", progress: 40 },
            { name: "Auckland Regional Holdings", status: "Initial Contact", amount: 8, instrument: "Pre-IPO Round", progress: 15 },
            { name: "Tainui Group Holdings", status: "MOU Negotiation", amount: 6, instrument: "Joint Venture", progress: 55 }
        ];
        // --- Investor persistence ---
        function saveInvestors(){
            try {
                localStorage.setItem('ke_pifLpInvestors', JSON.stringify(window.pifLpInvestors || []));
                localStorage.setItem('ke_directInvestors', JSON.stringify(window.directInvestors || []));
            } catch(e) { /* ignore quota errors */ }
        }
        function loadInvestors(){
            try {
                const pifRaw = localStorage.getItem('ke_pifLpInvestors');
                if (pifRaw) window.pifLpInvestors = JSON.parse(pifRaw);
                const dirRaw = localStorage.getItem('ke_directInvestors');
                if (dirRaw) window.directInvestors = JSON.parse(dirRaw);
            } catch(e) { /* ignore parse errors */ }
        }

        window.statusClasses = window.statusClasses || {
            "Active Discussion": "status-active",
            "Due Diligence": "status-active",
            "MOU Negotiation": "status-active",
            "Term Sheet": "status-pending",
            "Initial Contact": "status-pending",
            "Committed": "status-completed",
            "Not Proceeding": "status-declined"
        };
        function renderPifLpTable(){
            const tbody = document.getElementById('pifLpTableBody');
            if (!tbody) return;
            tbody.innerHTML='';
            pifLpInvestors.forEach((inv, idx) => {
                const row = tbody.insertRow();
                row.innerHTML = `
                    <td><input type="text" class="editable investor-name" value="${inv.name}" onchange="updatePifLp(${idx}, 'name', this.value)"></td>
                    <td>
                        <select class="editable" onchange="updatePifLp(${idx}, 'status', this.value)">
                            <option ${inv.status==='Initial Contact'?'selected':''}>Initial Contact</option>
                            <option ${inv.status==='Active Discussion'?'selected':''}>Active Discussion</option>
                            <option ${inv.status==='Due Diligence'?'selected':''}>Due Diligence</option>
                            <option ${inv.status==='MOU Negotiation'?'selected':''}>MOU Negotiation</option>
                            <option ${inv.status==='Term Sheet'?'selected':''}>Term Sheet</option>
                            <option ${inv.status==='Committed'?'selected':''}>Committed</option>
                            <option ${inv.status==='Not Proceeding'?'selected':''}>Not Proceeding</option>
                        </select>
                        <div class="status-badge ${window.statusClasses[inv.status]||''} mt-2"><span class="status-indicator"></span>${inv.status}</div>
                    </td>
                    <td><input type="number" class="editable amount-input" step="0.1" min="0" value="${inv.amount}" onchange="updatePifLp(${idx}, 'amount', parseFloat(this.value))"></td>
                    <td><input type="text" class="editable" value="${inv.notes||''}" onchange="updatePifLp(${idx}, 'notes', this.value)"></td>
                    <td>
                        <div style="display:flex;align-items:center;gap:.5rem;">
                            <input type="number" class="editable" style="width:60px;" min="0" max="100" value="${inv.progress}" onchange="updatePifLp(${idx}, 'progress', parseInt(this.value))">
                            <span style="font-size:.875rem;">%</span>
                            <div class="progress-bar" style="width: 100px;">
                                <div class="progress-fill" style="width: ${inv.progress}%"></div>
                            </div>
                        </div>
                    </td>
                    <td><button class="delete-btn" onclick="deletePifLp(${idx})">Delete</button></td>
                `;
            });
            const total = (window.pifLpInvestors||[]).reduce((s,i)=>s+(i.amount||0),0);
            const totalEl = document.getElementById('totalPifLp');
            if (totalEl) totalEl.textContent = '$' + total + 'M';
        }
        function updatePifLp(idx, field, value){
            pifLpInvestors[idx][field] = value;
            renderPifLpTable();
            updateChart();
            saveInvestors();
        }
        function deletePifLp(idx){ if(confirm('Delete LP investor?')){ pifLpInvestors.splice(idx,1); renderPifLpTable(); updateChart(); try { saveInvestors(); } catch(e) {} } }
function addPifLpInvestor(){
            pifLpInvestors.push({ name:"New LP", status:"Initial Contact", amount:0, notes:"", progress:0 });
            renderPifLpTable();
            updateChart();
            saveInvestors();
        }
        function renderDirectTable(){
            const tbody = document.getElementById('directTableBody');
            if (!tbody) return;
            tbody.innerHTML='';
            directInvestors.forEach((inv, idx) => {
                const row = tbody.insertRow();
                row.innerHTML = `
                    <td><input type="text" class="editable investor-name" value="${inv.name}" onchange="updateDirect(${idx}, 'name', this.value)"></td>
                    <td>
                        <select class="editable" onchange="updateDirect(${idx}, 'status', this.value)">
                            <option ${inv.status==='Initial Contact'?'selected':''}>Initial Contact</option>
                            <option ${inv.status==='Active Discussion'?'selected':''}>Active Discussion</option>
                            <option ${inv.status==='Due Diligence'?'selected':''}>Due Diligence</option>
                            <option ${inv.status==='MOU Negotiation'?'selected':''}>MOU Negotiation</option>
                            <option ${inv.status==='Term Sheet'?'selected':''}>Term Sheet</option>
                            <option ${inv.status==='Committed'?'selected':''}>Committed</option>
                            <option ${inv.status==='Not Proceeding'?'selected':''}>Not Proceeding</option>
                        </select>
                        <div class="status-badge ${window.statusClasses[inv.status]||''} mt-2"><span class="status-indicator"></span>${inv.status}</div>
                    </td>
                    <td><input type="number" class="editable amount-input" step="0.1" min="0" value="${inv.amount}" onchange="updateDirect(${idx}, 'amount', parseFloat(this.value))"></td>
                    <td>
                        <select class="editable" onchange="updateDirect(${idx}, 'instrument', this.value)">
                            <option ${inv.instrument==='Series A Preferred'?'selected':''}>Series A Preferred</option>
                            <option ${inv.instrument==='Series A Common'?'selected':''}>Series A Common</option>
                            <option ${inv.instrument==='Pre-IPO Round'?'selected':''}>Pre-IPO Round</option>
                            <option ${inv.instrument==='Joint Venture'?'selected':''}>Joint Venture</option>
                            <option ${inv.instrument==='Convertible Note'?'selected':''}>Convertible Note</option>
                        </select>
                        <div class="mini-badge mt-2">${inv.instrument||''}</div>
                    </td>
                    <td>
                        <div style="display:flex;align-items:center;gap:.5rem;">
                            <input type="number" class="editable" style="width:60px;" min="0" max="100" value="${inv.progress}" onchange="updateDirect(${idx}, 'progress', parseInt(this.value))">
                            <span style="font-size:.875rem;">%</span>
                            <div class="progress-bar" style="width: 100px;">
                                <div class="progress-fill" style="width: ${inv.progress}%"></div>
                            </div>
                        </div>
                    </td>
                    <td><button class="delete-btn" onclick="deleteDirect(${idx})">Delete</button></td>
                `;
            });
            const total = (window.directInvestors||[]).reduce((s,i)=>s+(i.amount||0),0);
            const totalEl = document.getElementById('totalDirect');
            if (totalEl) totalEl.textContent = '$' + total + 'M';
        }
        function updateDirect(idx, field, value){
            directInvestors[idx][field] = value;
            renderDirectTable();
            updateChart();
            saveInvestors();
        }
        function deleteDirect(idx){ if(confirm('Delete direct investor?')){ directInvestors.splice(idx,1); renderDirectTable(); updateChart(); try { saveInvestors(); } catch(e) {} } }
function addDirectInvestor(){
            directInvestors.push({ name:"New Direct Investor", status:"Initial Contact", amount:0, instrument:"Series A Preferred", progress:0 });
            renderDirectTable();
            updateChart();
            saveInvestors();
        }
// Event listeners
        document.getElementById('valuationScenario').addEventListener('change', updateScenarioAnalysis);
        document.getElementById('ebitdaMargin').addEventListener('input', updateScenarioAnalysis);
        document.getElementById('revenueGrowth').addEventListener('input', updateScenarioAnalysis);
        document.getElementById('payoutRatio').addEventListener('input', updateScenarioAnalysis);
        document.getElementById('phase2Amount').addEventListener('input', updateScenarioAnalysis);
        document.getElementById('phase3Amount').addEventListener('input', updateScenarioAnalysis);
        const _cg = document.getElementById('customerGrowth'); if (_cg) { _cg.addEventListener('input', updateScenarioAnalysis); }
        document.getElementById('timelineCompression').addEventListener('change', () => { renderTimelineFixed(); try { saveSettings(); } catch(e) {} });
// Initialize
        // Load any saved settings first
        loadSettings();
        loadInvestors();
        renderTimelineFixed();
        renderPifLpTable(); renderDirectTable(); updateChart(); updateScenarioAnalysis();
        // Save immediately so slider labels persist after first paint
        saveSettings();
    </script>
</body>
</html>
