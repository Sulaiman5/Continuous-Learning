"# Continuous-Learning" 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nexa ERP Dashboard</title>
</head>
<body style="margin: 0; padding: 0;">

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .dashboard {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    color: #1f2937;
    background: #f3f4f6;
    padding: 24px;
    max-width: 1400px;
    margin: 0 auto;
  }

  /* KPI Cards */
  .kpi-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 20px;
    margin-bottom: 24px;
  }

  .kpi-card {
    background: #ffffff;
    border: 1px solid rgba(0, 0, 0, 0.07);
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
    transition: box-shadow 0.2s;
  }

  .kpi-card:hover {
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  }

  .kpi-icon {
    width: 40px;
    height: 40px;
    border-radius: 6px;
    margin-bottom: 12px;
  }

  .kpi-icon.teal {
    background: linear-gradient(135deg, #0d7ea2 0%, #0a5f7d 100%);
  }

  .kpi-icon.orange {
    background: linear-gradient(135deg, #ff6347 0%, #e5533d 100%);
  }

  .kpi-icon.slate {
    background: linear-gradient(135deg, #475569 0%, #334155 100%);
  }

  .kpi-title {
    font-size: 13px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    color: #64748b;
    font-weight: 600;
    margin-bottom: 8px;
  }

  .kpi-value {
    font-size: 24px;
    font-weight: 700;
    color: #1f2937;
    margin-bottom: 8px;
  }

  .kpi-meta {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 13px;
    color: #64748b;
  }

  /* Badges */
  .badge-ok {
    background: #0d7ea2;
    color: #ffffff;
    padding: 4px 10px;
    border-radius: 12px;
    font-size: 11px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.3px;
  }

  .badge-warn {
    background: #ff6347;
    color: #ffffff;
    padding: 4px 10px;
    border-radius: 12px;
    font-size: 11px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.3px;
  }

  .badge-neutral {
    background: #94a3b8;
    color: #ffffff;
    padding: 4px 10px;
    border-radius: 12px;
    font-size: 11px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.3px;
  }

  .badge-critical {
    background: #dc2626;
    color: #ffffff;
    padding: 4px 10px;
    border-radius: 12px;
    font-size: 11px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.3px;
  }

  .badge-up {
    background: #dcfce7;
    color: #16a34a;
    padding: 3px 8px;
    border-radius: 10px;
    font-size: 12px;
    font-weight: 600;
  }

  .badge-down {
    background: #fee2e2;
    color: #dc2626;
    padding: 3px 8px;
    border-radius: 10px;
    font-size: 12px;
    font-weight: 600;
  }

  /* Card Component */
  .card {
    background: #ffffff;
    border: 1px solid rgba(0, 0, 0, 0.07);
    border-radius: 8px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
    margin-bottom: 20px;
  }

  .card-header {
    padding: 16px 20px;
    border-bottom: 1px solid rgba(0, 0, 0, 0.05);
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .card-title {
    font-size: 15px;
    font-weight: 700;
    color: #1f2937;
    text-transform: uppercase;
    letter-spacing: 0.3px;
  }

  .card-subtitle {
    font-size: 12px;
    color: #94a3b8;
    font-weight: 500;
  }

  .card-body {
    padding: 20px;
  }

  /* Two Column Layouts */
  .two-col {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
    margin-bottom: 24px;
  }

  /* Chart Styles */
  .chart-wrapper {
    margin-top: 16px;
  }

  .chart-legend {
    display: flex;
    gap: 16px;
    margin-bottom: 16px;
  }

  .legend-item {
    display: flex;
    align-items: center;
    gap: 6px;
    font-size: 13px;
    color: #64748b;
  }

  .legend-color {
    width: 12px;
    height: 12px;
    border-radius: 2px;
  }

  /* Pie Chart Styles */
  .pie-chart-container {
    display: flex;
    gap: 32px;
    align-items: center;
    justify-content: center;
  }

  .pie-chart {
    position: relative;
    width: 200px;
    height: 200px;
    border-radius: 50%;
    background: conic-gradient(
      #0d7ea2 0deg 144deg,
      #ff6347 144deg 252deg,
      #475569 252deg 306deg,
      #16a34a 306deg 360deg
    );
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }

  .pie-chart-center {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100px;
    height: 100px;
    border-radius: 50%;
    background: #ffffff;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }

  .pie-total-label {
    font-size: 11px;
    color: #64748b;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    font-weight: 600;
  }

  .pie-total-value {
    font-size: 18px;
    font-weight: 700;
    color: #1f2937;
  }

  .pie-legend {
    display: flex;
    flex-direction: column;
    gap: 12px;
  }

  .pie-legend-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 16px;
    min-width: 200px;
  }

  .pie-legend-label {
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .pie-legend-color {
    width: 16px;
    height: 16px;
    border-radius: 3px;
    flex-shrink: 0;
  }

  .pie-legend-text {
    font-size: 13px;
    color: #1f2937;
    font-weight: 500;
  }

  .pie-legend-value {
    font-size: 14px;
    font-weight: 700;
    color: #1f2937;
  }

  .pie-legend-percent {
    font-size: 12px;
    color: #64748b;
    margin-left: 4px;
  }

  .chart-bars {
    display: flex;
    align-items: flex-end;
    gap: 12px;
    height: 180px;
    padding: 12px 0;
  }

  .chart-bar-group {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
  }

  .chart-bars-inner {
    display: flex;
    gap: 6px;
    width: 100%;
    justify-content: center;
    align-items: flex-end;
    height: 140px;
  }

  .chart-bar {
    width: 20px;
    border-radius: 4px 4px 0 0;
    transition: opacity 0.2s;
  }

  .chart-bar:hover {
    opacity: 0.8;
  }

  .chart-bar.sales {
    background: #0d7ea2;
  }

  .chart-bar.purchase {
    background: #94a3b8;
  }

  .chart-label {
    font-size: 11px;
    color: #64748b;
    font-weight: 500;
  }

  /* Progress Bars */
  .progress-list {
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .progress-item {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .progress-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .progress-label {
    font-size: 13px;
    color: #1f2937;
    font-weight: 600;
  }

  .progress-count {
    font-size: 13px;
    color: #0d7ea2;
    font-weight: 700;
  }

  .progress {
    width: 100%;
    height: 8px;
    background: #e5e7eb;
    border-radius: 4px;
    overflow: hidden;
  }

  .progress-fill {
    height: 100%;
    background: #0d7ea2;
    border-radius: 4px;
    transition: width 0.3s;
  }

  .progress-fill.warn {
    background: #ff6347;
  }

  /* Table Styles */
  .table-wrapper {
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
  }

  .table {
    width: 100%;
    border-collapse: collapse;
    font-size: 14px;
  }

  .table th {
    background: #f9fafb;
    padding: 12px 16px;
    text-align: left;
    font-weight: 600;
    color: #475569;
    font-size: 12px;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    border-bottom: 1px solid #e5e7eb;
  }

  .table td {
    padding: 14px 16px;
    border-bottom: 1px solid #f1f5f9;
    color: #1f2937;
  }

  .table tr:hover {
    background: #f5faff;
  }

  .table tr:last-child td {
    border-bottom: none;
  }

  /* Approval Items */
  .approval-list {
    display: flex;
    flex-direction: column;
    gap: 12px;
    margin-bottom: 24px;
  }

  .approval-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px;
    background: #f9fafb;
    border-radius: 6px;
    border: 1px solid rgba(0, 0, 0, 0.05);
  }

  .approval-info {
    flex: 1;
  }

  .approval-title {
    font-size: 14px;
    font-weight: 600;
    color: #1f2937;
    margin-bottom: 4px;
  }

  .approval-module {
    font-size: 12px;
    color: #64748b;
  }

  .approval-actions {
    display: flex;
    gap: 8px;
    align-items: center;
  }

  /* Task List */
  .task-section {
    margin-top: 24px;
    padding-top: 20px;
    border-top: 1px solid #e5e7eb;
  }

  .task-section-title {
    font-size: 13px;
    font-weight: 700;
    color: #475569;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    margin-bottom: 12px;
  }

  .task-list {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .task-item {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .check-box {
    width: 18px;
    height: 18px;
    border: 2px solid #cbd5e1;
    border-radius: 4px;
    flex-shrink: 0;
    cursor: pointer;
    transition: all 0.2s;
  }

  .check-box:hover {
    border-color: #0d7ea2;
    background: #f0f9ff;
  }

  .task-text {
    font-size: 14px;
    color: #475569;
  }

  /* Timeline */
  .timeline {
    display: flex;
    flex-direction: column;
    gap: 16px;
  }

  .timeline-item {
    display: flex;
    gap: 12px;
    align-items: flex-start;
  }

  .timeline-marker {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background: #0d7ea2;
    margin-top: 4px;
    flex-shrink: 0;
  }

  .timeline-marker.delayed {
    background: #ff6347;
  }

  .timeline-content {
    flex: 1;
  }

  .timeline-title {
    font-size: 14px;
    font-weight: 600;
    color: #1f2937;
    margin-bottom: 4px;
  }

  .timeline-meta {
    display: flex;
    gap: 8px;
    align-items: center;
    font-size: 12px;
    color: #64748b;
  }

  /* Accounting Grid */
  .account-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 16px;
  }

  .account-mini {
    padding: 16px;
    background: #f9fafb;
    border-radius: 6px;
    border: 1px solid rgba(0, 0, 0, 0.05);
  }

  .account-mini-label {
    font-size: 12px;
    color: #64748b;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.3px;
    margin-bottom: 8px;
  }

  .account-mini-value {
    font-size: 20px;
    font-weight: 700;
    color: #1f2937;
    margin-bottom: 6px;
  }

  /* Module Cards */
  .module-grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: 16px;
    margin-top: 24px;
  }

  .module-card {
    background: #ffffff;
    border: 1px solid rgba(0, 0, 0, 0.07);
    border-radius: 8px;
    padding: 20px 16px;
    text-align: center;
    cursor: pointer;
    transition: all 0.2s;
    position: relative;
  }

  .module-card:hover {
    border-color: #0d7ea2;
    box-shadow: 0 4px 12px rgba(13, 126, 162, 0.1);
    transform: translateY(-2px);
  }

  .module-icon {
    width: 48px;
    height: 48px;
    margin: 0 auto 12px;
    border-radius: 8px;
    background: linear-gradient(135deg, #0d7ea2 0%, #0a5f7d 100%);
  }

  .module-name {
    font-size: 14px;
    font-weight: 700;
    color: #1f2937;
    margin-bottom: 6px;
  }

  .module-desc {
    font-size: 11px;
    color: #64748b;
    line-height: 1.4;
  }

  .module-badge {
    position: absolute;
    top: 8px;
    right: 8px;
    background: #ff6347;
    color: #ffffff;
    font-size: 10px;
    font-weight: 700;
    padding: 3px 7px;
    border-radius: 10px;
  }

  /* Responsive */
  @media (max-width: 1024px) {
    .kpi-grid {
      grid-template-columns: repeat(2, 1fr);
    }

    .module-grid {
      grid-template-columns: repeat(4, 1fr);
    }

    .pie-chart-container {
      flex-direction: column;
    }
  }

  @media (max-width: 768px) {
    .dashboard {
      padding: 16px;
    }

    .kpi-grid {
      grid-template-columns: 1fr;
    }

    .two-col {
      grid-template-columns: 1fr;
    }

    .account-grid {
      grid-template-columns: 1fr;
    }

    .module-grid {
      grid-template-columns: repeat(2, 1fr);
    }

    .card-header {
      flex-direction: column;
      align-items: flex-start;
      gap: 8px;
    }

    .pie-chart-container {
      flex-direction: column;
    }
  }

  @media (max-width: 480px) {
    .module-grid {
      grid-template-columns: 1fr;
    }
  }
</style>

<div class="dashboard">
  <!-- A. KPI SUMMARY CARDS -->
  <div class="kpi-grid">
    <div class="kpi-card">
      <div class="kpi-icon teal"></div>
      <div class="kpi-title">Today Sales</div>
      <div class="kpi-value">৳ 2,45,680</div>
      <div class="kpi-meta">
        <span class="badge-up">↑ 12.5%</span>
        <span>vs yesterday</span>
      </div>
    </div>

    <div class="kpi-card">
      <div class="kpi-icon orange"></div>
      <div class="kpi-title">Payables Due</div>
      <div class="kpi-value">৳ 8,92,400</div>
      <div class="kpi-meta">
        <span class="badge-warn">Due Today</span>
      </div>
    </div>

    <div class="kpi-card">
      <div class="kpi-icon teal"></div>
      <div class="kpi-title">Receivables</div>
      <div class="kpi-value">৳ 12,56,300</div>
      <div class="kpi-meta">
        <span class="badge-ok">On Track</span>
      </div>
    </div>

    <div class="kpi-card">
      <div class="kpi-icon slate"></div>
      <div class="kpi-title">Inventory Value</div>
      <div class="kpi-value">৳ 45,23,900</div>
      <div class="kpi-meta">
        <span>2,847 SKUs</span>
      </div>
    </div>
  </div>

  <!-- B. SALES TREND & PRODUCTION STATUS -->
  <div class="two-col">
    <div class="card">
      <div class="card-header">
        <div>
          <div class="card-title">Sales vs Purchase Trend</div>
          <div class="card-subtitle">Last 7 days</div>
        </div>
      </div>
      <div class="card-body">
        <div class="chart-legend">
          <div class="legend-item">
            <div class="legend-color" style="background: #0d7ea2;"></div>
            <span>Sales</span>
          </div>
          <div class="legend-item">
            <div class="legend-color" style="background: #94a3b8;"></div>
            <span>Purchase</span>
          </div>
        </div>
        <div class="chart-bars">
          <div class="chart-bar-group">
            <div class="chart-bars-inner">
              <div class="chart-bar sales" style="height: 65%;"></div>
              <div class="chart-bar purchase" style="height: 48%;"></div>
            </div>
            <div class="chart-label">Mon</div>
          </div>
          <div class="chart-bar-group">
            <div class="chart-bars-inner">
              <div class="chart-bar sales" style="height: 78%;"></div>
              <div class="chart-bar purchase" style="height: 52%;"></div>
            </div>
            <div class="chart-label">Tue</div>
          </div>
          <div class="chart-bar-group">
            <div class="chart-bars-inner">
              <div class="chart-bar sales" style="height: 55%;"></div>
              <div class="chart-bar purchase" style="height: 62%;"></div>
            </div>
            <div class="chart-label">Wed</div>
          </div>
          <div class="chart-bar-group">
            <div class="chart-bars-inner">
              <div class="chart-bar sales" style="height: 88%;"></div>
              <div class="chart-bar purchase" style="height: 71%;"></div>
            </div>
            <div class="chart-label">Thu</div>
          </div>
          <div class="chart-bar-group">
            <div class="chart-bars-inner">
              <div class="chart-bar sales" style="height: 72%;"></div>
              <div class="chart-bar purchase" style="height: 58%;"></div>
            </div>
            <div class="chart-label">Fri</div>
          </div>
          <div class="chart-bar-group">
            <div class="chart-bars-inner">
              <div class="chart-bar sales" style="height: 92%;"></div>
              <div class="chart-bar purchase" style="height: 45%;"></div>
            </div>
            <div class="chart-label">Sat</div>
          </div>
          <div class="chart-bar-group">
            <div class="chart-bars-inner">
              <div class="chart-bar sales" style="height: 68%;"></div>
              <div class="chart-bar purchase" style="height: 55%;"></div>
            </div>
            <div class="chart-label">Sun</div>
          </div>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-header">
        <div class="card-title">Production / Manufacturing Status</div>
      </div>
      <div class="card-body">
        <div class="progress-list">
          <div class="progress-item">
            <div class="progress-header">
              <span class="progress-label">Open Work Orders</span>
              <span class="progress-count">24</span>
            </div>
            <div class="progress">
              <div class="progress-fill" style="width: 100%;"></div>
            </div>
          </div>

          <div class="progress-item">
            <div class="progress-header">
              <span class="progress-label">In Production</span>
              <span class="progress-count">18</span>
            </div>
            <div class="progress">
              <div class="progress-fill" style="width: 75%;"></div>
            </div>
          </div>

          <div class="progress-item">
            <div class="progress-header">
              <span class="progress-label">QC Pending</span>
              <span class="progress-count">7</span>
            </div>
            <div class="progress">
              <div class="progress-fill warn" style="width: 29%;"></div>
            </div>
          </div>

          <div class="progress-item">
            <div class="progress-header">
              <span class="progress-label">Completed (Today)</span>
              <span class="progress-count">12</span>
            </div>
            <div class="progress">
              <div class="progress-fill" style="width: 50%;"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- PIE CHART: REVENUE BREAKDOWN -->
  <div class="card">
    <div class="card-header">
      <div>
        <div class="card-title">Revenue Breakdown by Category</div>
        <div class="card-subtitle">This Month</div>
      </div>
    </div>
    <div class="card-body">
      <div class="pie-chart-container">
        <div class="pie-chart">
          <div class="pie-chart-center">
            <div class="pie-total-label">Total</div>
            <div class="pie-total-value">৳45.9M</div>
          </div>
        </div>
        <div class="pie-legend">
          <div class="pie-legend-item">
            <div class="pie-legend-label">
              <div class="pie-legend-color" style="background: #0d7ea2;"></div>
              <span class="pie-legend-text">Garments</span>
            </div>
            <div>
              <span class="pie-legend-value">৳18.4M</span>
              <span class="pie-legend-percent">(40%)</span>
            </div>
          </div>
          <div class="pie-legend-item">
            <div class="pie-legend-label">
              <div class="pie-legend-color" style="background: #ff6347;"></div>
              <span class="pie-legend-text">Textiles</span>
            </div>
            <div>
              <span class="pie-legend-value">৳13.8M</span>
              <span class="pie-legend-percent">(30%)</span>
            </div>
          </div>
          <div class="pie-legend-item">
            <div class="pie-legend-label">
              <div class="pie-legend-color" style="background: #475569;"></div>
              <span class="pie-legend-text">Accessories</span>
            </div>
            <div>
              <span class="pie-legend-value">৳6.9M</span>
              <span class="pie-legend-percent">(15%)</span>
            </div>
          </div>
          <div class="pie-legend-item">
            <div class="pie-legend-label">
              <div class="pie-legend-color" style="background: #16a34a;"></div>
              <span class="pie-legend-text">Others</span>
            </div>
            <div>
              <span class="pie-legend-value">৳6.9M</span>
              <span class="pie-legend-percent">(15%)</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- C. INVENTORY ALERTS & APPROVALS -->
  <div class="two-col">
    <div class="card">
      <div class="card-header">
        <div class="card-title">Low Stock / Inventory Alerts</div>
      </div>
      <div class="card-body">
        <div class="table-wrapper">
          <table class="table">
            <thead>
              <tr>
                <th>Item</th>
                <th>On Hand</th>
                <th>Reorder Level</th>
                <th>Status</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Cotton Fabric - White</td>
                <td>45 yds</td>
                <td>100 yds</td>
                <td><span class="badge-critical">CRITICAL</span></td>
              </tr>
              <tr>
                <td>Button - Pearl 12mm</td>
                <td>280 pcs</td>
                <td>500 pcs</td>
                <td><span class="badge-warn">LOW</span></td>
              </tr>
              <tr>
                <td>Thread - Navy Blue</td>
                <td>18 rolls</td>
                <td>50 rolls</td>
                <td><span class="badge-critical">CRITICAL</span></td>
              </tr>
              <tr>
                <td>Zipper - 18 inch</td>
                <td>520 pcs</td>
                <td>1000 pcs</td>
                <td><span class="badge-warn">LOW</span></td>
              </tr>
              <tr>
                <td>Packaging Boxes</td>
                <td>1,200 pcs</td>
                <td>800 pcs</td>
                <td><span class="badge-ok">OK</span></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-header">
        <div class="card-title">Approvals & Tasks</div>
      </div>
      <div class="card-body">
        <div class="approval-list">
          <div class="approval-item">
            <div class="approval-info">
              <div class="approval-title">Purchase Order #PO-1023</div>
              <div class="approval-module">Purchase Module</div>
            </div>
            <div class="approval-actions">
              <span class="badge-warn">URGENT</span>
            </div>
          </div>

          <div class="approval-item">
            <div class="approval-info">
              <div class="approval-title">LC Request #LC-7781</div>
              <div class="approval-module">LC Module</div>
            </div>
            <div class="approval-actions">
              <span class="badge-warn">URGENT</span>
            </div>
          </div>

          <div class="approval-item">
            <div class="approval-info">
              <div class="approval-title">Payment Voucher #PV-9912</div>
              <div class="approval-module">Accounts Module</div>
            </div>
            <div class="approval-actions">
              <span class="badge-neutral">Normal</span>
            </div>
          </div>
        </div>

        <div class="task-section">
          <div class="task-section-title">My Tasks Today</div>
          <div class="task-list">
            <div class="task-item">
              <div class="check-box"></div>
              <div class="task-text">Approve Supplier Invoice</div>
            </div>
            <div class="task-item">
              <div class="check-box"></div>
              <div class="task-text">Review QC Report</div>
            </div>
            <div class="task-item">
              <div class="check-box"></div>
              <div class="task-text">Check Negative Stock</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- D. RECENT SALES / POS BILLS -->
  <div class="card">
    <div class="card-header">
      <div class="card-title">Recent Sales / POS Bills</div>
    </div>
    <div class="card-body">
      <div class="table-wrapper">
        <table class="table">
          <thead>
            <tr>
              <th>Invoice #</th>
              <th>Customer</th>
              <th>Amount</th>
              <th>Status</th>
              <th>Channel</th>
              <th>Date</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>INV-2025-3421</td>
              <td>Rahima Fashion House</td>
              <td>৳ 45,600</td>
              <td><span class="badge-ok">Paid</span></td>
              <td>Credit Sales</td>
              <td>28 Oct 2025</td>
            </tr>
            <tr>
              <td>POS-2025-8923</td>
              <td>Walk-in Customer</td>
              <td>৳ 8,400</td>
              <td><span class="badge-ok">Paid</span></td>
              <td>POS</td>
              <td>28 Oct 2025</td>
            </tr>
            <tr>
              <td>INV-2025-3420</td>
              <td>Kazi Garments Ltd</td>
              <td>৳ 1,23,900</td>
              <td><span class="badge-neutral">Partial</span></td>
              <td>Credit Sales</td>
              <td>27 Oct 2025</td>
            </tr>
            <tr>
              <td>INV-2025-3419</td>
              <td>Sheltech Textiles</td>
              <td>৳ 67,200</td>
              <td><span class="badge-warn">Overdue</span></td>
              <td>Credit Sales</td>
              <td>25 Oct 2025</td>
            </tr>
            <tr>
              <td>POS-2025-8922</td>
              <td>Walk-in Customer</td>
              <td>৳ 12,800</td>
              <td><span class="badge-ok">Paid</span></td>
              <td>POS</td>
              <td>28 Oct 2025</td>
            </tr>
            <tr>
              <td>INV-2025-3418</td>
              <td>Bengal Apparels</td>
              <td>৳ 89,500</td>
              <td><span class="badge-ok">Paid</span></td>
              <td>Credit Sales</td>
              <td>27 Oct 2025</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- E. LC PIPELINE & ACCOUNTING SNAPSHOT -->
  <div class="two-col">
    <div class="card">
      <div class="card-header">
        <div class="card-title">LC / Import Pipeline</div>
      </div>
      <div class="card-body">
        <div class="timeline">
          <div class="timeline-item">
            <div class="timeline-marker"></div>
            <div class="timeline-content">
              <div class="timeline-title">PI Issued</div>
              <div class="timeline-meta">
                <span>18 Oct 2025</span>
                <span class="badge-ok">On Time</span>
              </div>
            </div>
          </div>

          <div class="timeline-item">
            <div class="timeline-marker"></div>
            <div class="timeline-content">
              <div class="timeline-title">LC Opened</div>
              <div class="timeline-meta">
                <span>22 Oct 2025</span>
                <span class="badge-ok">On Time</span>
              </div>
            </div>
          </div>

          <div class="timeline-item">
            <div class="timeline-marker"></div>
            <div class="timeline-content">
              <div class="timeline-title">Goods In Transit</div>
              <div class="timeline-meta">
                <span>25 Oct 2025</span>
                <span class="badge-ok">On Time</span>
              </div>
            </div>
          </div>

          <div class="timeline-item">
            <div class="timeline-marker delayed"></div>
            <div class="timeline-content">
              <div class="timeline-title">Customs Clearance</div>
              <div class="timeline-meta">
                <span>Expected: 27 Oct</span>
                <span class="badge-warn">Delayed</span>
              </div>
            </div>
          </div>

          <div class="timeline-item">
            <div class="timeline-marker delayed"></div>
            <div class="timeline-content">
              <div class="timeline-title">To Warehouse</div>
              <div class="timeline-meta">
                <span>Pending</span>
                <span class="badge-warn">Delayed</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-header">
        <div class="card-title">Accounts Snapshot</div>
      </div>
      <div class="card-body">
        <div class="account-grid">
          <div class="account-mini">
            <div class="account-mini-label">Cash in Hand</div>
            <div class="account-mini-value">৳ 3,45,900</div>
            <span class="badge-up">↑ 8.2%</span>
          </div>

          <div class="account-mini">
            <div class="account-mini-label">Bank Balance</div>
            <div class="account-mini-value">৳ 28,92,400</div>
            <span class="badge-up">↑ 3.5%</span>
          </div>

          <div class="account-mini">
            <div class="account-mini-label">This Month Expense</div>
            <div class="account-mini-value">৳ 12,67,200</div>
            <span class="badge-down">↑ 12.8%</span>
          </div>

          <div class="account-mini">
            <div class="account-mini-label">This Month Revenue</div>
            <div class="account-mini-value">৳ 45,89,300</div>
            <span class="badge-up">↑ 15.3%</span>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- F. MODULE QUICK ACCESS -->
  <div class="module-grid">
    <div class="module-card">
      <div class="module-badge">3</div>
      <div class="module-icon"></div>
      <div class="module-name">Sales</div>
      <div class="module-desc">Quotations, Orders, Invoices</div>
    </div>

    <div class="module-card">
      <div class="module-badge">5</div>
      <div class="module-icon"></div>
      <div class="module-name">Purchase</div>
      <div class="module-desc">PO, GRN, Supplier Mgmt</div>
    </div>

    <div class="module-card">
      <div class="module-badge">8</div>
      <div class="module-icon"></div>
      <div class="module-name">Inventory</div>
      <div class="module-desc">Stock, Transfers, Reports</div>
    </div>

    <div class="module-card">
      <div class="module-icon"></div>
      <div class="module-name">Accounts</div>
      <div class="module-desc">Ledger, Vouchers, Reports</div>
    </div>

    <div class="module-card">
      <div class="module-badge">2</div>
      <div class="module-icon"></div>
      <div class="module-name">LC</div>
      <div class="module-desc">Import, Documents, Tracking</div>
    </div>

    <div class="module-card">
      <div class="module-icon"></div>
      <div class="module-name">Manufacturing</div>
      <div class="module-desc">Work Orders, BOM, QC</div>
    </div>

    <div class="module-card">
      <div class="module-icon"></div>
      <div class="module-name">POS</div>
      <div class="module-desc">Point of Sale, Billing</div>
    </div>
  </div>
</div>
</body>
</html>
