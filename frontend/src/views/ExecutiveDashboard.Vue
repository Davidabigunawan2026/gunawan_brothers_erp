
<script setup>
import {
  DollarSign,
  ShoppingCart,
  Boxes,
  TrendingUp,
  TrendingDown,
  ArrowUpRight,
  ArrowDownRight,
  Activity
} from 'lucide-vue-next'

const summaryCards = [
  {
    title: 'Total Revenue',
    value: 'Rp 185.500.000',
    change: '+12.5%',
    icon: DollarSign,
    color: 'teal',
    positive: true
  },
  {
    title: 'Total Purchase',
    value: 'Rp 95.000.000',
    change: '+8.2%',
    icon: ShoppingCart,
    color: 'blue',
    positive: true
  },
  {
    title: 'Inventory Value',
    value: 'Rp 125.750.000',
    change: '+5.4%',
    icon: Boxes,
    color: 'purple',
    positive: true
  },
  {
    title: 'Gross Profit',
    value: 'Rp 90.500.000',
    change: '+15.8%',
    icon: TrendingUp,
    color: 'orange',
    positive: true
  }
]

const transactions = [
  {
    no: 'SO-0001',
    type: 'Sales Order',
    customer: 'PT Maju Jaya',
    amount: 'Rp 25.000.000',
    status: 'Completed'
  },
  {
    no: 'PO-0001',
    type: 'Purchase Order',
    customer: 'PT Steel Indonesia',
    amount: 'Rp 15.000.000',
    status: 'Pending'
  },
  {
    no: 'SO-0002',
    type: 'Sales Order',
    customer: 'PT Sukses Makmur',
    amount: 'Rp 18.500.000',
    status: 'Completed'
  },
  {
    no: 'PO-0002',
    type: 'Purchase Order',
    customer: 'PT Aluminium Jaya',
    amount: 'Rp 12.000.000',
    status: 'Pending'
  }
]

const monthlyData = [
  { month: 'Jan', sales: 65, purchase: 40 },
  { month: 'Feb', sales: 80, purchase: 55 },
  { month: 'Mar', sales: 60, purchase: 45 },
  { month: 'Apr', sales: 90, purchase: 60 },
  { month: 'May', sales: 75, purchase: 50 },
  { month: 'Jun', sales: 100, purchase: 65 }
]
</script>

<template>
  <section class="executive-dashboard">

    <div class="page-header">
      <div>
        <h1>Executive Dashboard</h1>
        <p>Business performance overview</p>
      </div>

      <div class="period-filter">
        <select>
          <option>This Year</option>
          <option>This Month</option>
          <option>Last Month</option>
        </select>
      </div>
    </div>

    <!-- SUMMARY CARDS -->
    <div class="summary-grid">
      <div
        v-for="card in summaryCards"
        :key="card.title"
        class="summary-card"
      >
        <div class="card-top">
          <div class="card-icon" :class="card.color">
            <component :is="card.icon" :size="23" />
          </div>
          <span class="card-change">
            <ArrowUpRight :size="15" />
            {{ card.change }}
          </span>
        </div>

        <p>{{ card.title }}</p>
        <h2>{{ card.value }}</h2>
        <span class="card-description">
          Compared with previous period
        </span>
      </div>
    </div>

    <!-- SALES CHART -->
    <div class="chart-card">
      <div class="section-heading">
        <div>
          <h2>Sales vs Purchase</h2>
          <p>Monthly business performance</p>
        </div>

        <div class="chart-legend">
          <span><i class="sales-dot"></i> Sales</span>
          <span><i class="purchase-dot"></i> Purchase</span>
        </div>
      </div>

      <div class="chart-area">
        <div class="chart-y-labels">
          <span>100</span>
          <span>75</span>
          <span>50</span>
          <span>25</span>
          <span>0</span>
        </div>

        <div class="chart-content">
          <div
            v-for="item in monthlyData"
            :key="item.month"
            class="chart-column"
          >
            <div class="bars">
              <div
                class="bar sales-bar"
                :style="{ height: item.sales + '%' }"
              ></div>

              <div
                class="bar purchase-bar"
                :style="{ height: item.purchase + '%' }"
              ></div>
            </div>
            <span>{{ item.month }}</span>
          </div>
        </div>
      </div>
    </div>

    <!-- RECENT TRANSACTIONS -->
    <div class="transactions-card">
      <div class="section-heading">
        <div>
          <h2>Recent Transactions</h2>
          <p>Latest sales and purchasing activities</p>
        </div>

        <button class="view-all">View All</button>
      </div>

      <div class="table-wrapper">
        <table>
          <thead>
            <tr>
              <th>Document No.</th>
              <th>Type</th>
              <th>Customer / Supplier</th>
              <th>Amount</th>
              <th>Status</th>
            </tr>
          </thead>

          <tbody>
            <tr v-for="item in transactions" :key="item.no">
              <td class="document-no">{{ item.no }}</td>
              <td>{{ item.type }}</td>
              <td>{{ item.customer }}</td>
              <td>{{ item.amount }}</td>
              <td>
                <span
                  class="status"
                  :class="item.status.toLowerCase()"
                >
                  {{ item.status }}
                </span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

  </section>
</template>

<style scoped>
.executive-dashboard {
  padding: 32px 36px;
  color: #e2e8f0;
}

.page-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 30px;
  gap: 16px;
}

.page-header h1 {
  margin: 0 0 8px;
  font-size: 27px;
}

.page-header p,
.section-heading p {
  color: #94a3b8;
  margin: 0;
  font-size: 14px;
}

.period-filter select {
  background: #17263a;
  color: #cbd5e1;
  border: 1px solid #334155;
  border-radius: 8px;
  padding: 11px 14px;
}

.summary-grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 22px;
  margin-bottom: 28px;
}

.summary-card,
.chart-card,
.transactions-card {
  background: #111e30;
  border: 1px solid #26364b;
  border-radius: 14px;
}

.summary-card {
  padding: 23px;
}

.card-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 22px;
}

.card-icon {
  width: 48px;
  height: 48px;
  border-radius: 12px;
  display: grid;
  place-items: center;
}

.teal {
  background: #134e4a;
  color: #5eead4;
}

.blue {
  background: #1e3a5f;
  color: #60a5fa;
}

.purple {
  background: #3b2d5b;
  color: #c4b5fd;
}

.orange {
  background: #633c20;
  color: #fdba74;
}

.card-change {
  color: #5eead4;
  font-size: 12px;
  display: flex;
  align-items: center;
}

.summary-card p {
  color: #94a3b8;
  font-size: 13px;
  margin: 0 0 9px;
}

.summary-card h2 {
  font-size: 21px;
  margin: 0 0 13px;
}

.card-description {
  color: #64748b;
  font-size: 11px;
}

.chart-card,
.transactions-card {
  padding: 25px;
  margin-bottom: 25px;
}

.section-heading {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 15px;
  margin-bottom: 30px;
}

.section-heading h2 {
  font-size: 19px;
  margin: 0 0 7px;
}

.chart-legend {
  display: flex;
  gap: 18px;
  font-size: 12px;
  color: #94a3b8;
}

.chart-legend span {
  display: flex;
  align-items: center;
  gap: 7px;
}

.chart-legend i {
  width: 9px;
  height: 9px;
  border-radius: 50%;
}

.sales-dot {
  background: #2dd4bf;
}

.purchase-dot {
  background: #60a5fa;
}

.chart-area {
  height: 230px;
  display: flex;
  gap: 15px;
}

.chart-y-labels {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  color: #64748b;
  font-size: 11px;
  padding-bottom: 20px;
}

.chart-content {
  flex: 1;
  display: flex;
  justify-content: space-around;
  align-items: stretch;
  border-bottom: 1px solid #334155;
  background: repeating-linear-gradient(
    to bottom,
    transparent 0,
    transparent 24%,
    #26364b 25%,
    transparent 25.5%
  );
}

.chart-column {
  width: 11%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-end;
  gap: 9px;
}

.bars {
  height: 100%;
  display: flex;
  align-items: flex-end;
  gap: 5px;
}

.bar {
  width: 15px;
  min-height: 2px;
  border-radius: 5px 5px 0 0;
}

.sales-bar {
  background: #2dd4bf;
}

.purchase-bar {
  background: #60a5fa;
}

.chart-column span {
  color: #94a3b8;
  font-size: 11px;
}

.table-wrapper {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
  white-space: nowrap;
  font-size: 13px;
}

th {
  background: #192a40;
  color: #94a3b8;
  text-align: left;
  padding: 15px;
}

td {
  padding: 17px 15px;
  border-bottom: 1px solid #26364b;
}

.document-no {
  color: #5eead4;
  font-weight: bold;
}

.status {
  padding: 6px 10px;
  border-radius: 20px;
  font-size: 11px;
}

.completed {
  background: #134e4a;
  color: #5eead4;
}

.pending {
  background: #633c20;
  color: #fdba74;
}

.view-all {
  padding: 9px 15px;
  background: #1e3a5f;
  border: 0;
  border-radius: 7px;
  color: #93c5fd;
  cursor: pointer;
}

@media (max-width: 1100px) {
  .summary-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (max-width: 650px) {
  .executive-dashboard {
    padding: 22px 16px;
  }

  .summary-grid {
    grid-template-columns: 1fr;
  }

  .page-header {
    align-items: flex-start;
    flex-direction: column;
  }
}
</style>
