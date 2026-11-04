<script setup>
import { computed, ref } from 'vue'
import {
  Chart as ChartJS,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  LineController,
  DoughnutController,
  ArcElement,
  Tooltip,
  Legend,
  Filler
} from 'chart.js'
import { Line, Doughnut } from 'vue-chartjs'
import {
  DollarSign,
  ShoppingCart,
  Clock3,
  Users,
  TrendingUp,
  Package,
  Search,
  ArrowUpRight,
  FileText,
  CalendarDays,
  CircleCheck,
  Truck,
  Eye
} from 'lucide-vue-next'

ChartJS.register(
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  LineController,
  DoughnutController,
  ArcElement,
  Tooltip,
  Legend,
  Filler
)

const monthlyRevenue = [65, 80, 70, 95, 85, 110]
const monthlyTarget = [70, 75, 80, 85, 90, 100]

const salesLineData = {
  labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
  datasets: [
    {
      label: 'Sales Revenue',
      data: monthlyRevenue,
      borderColor: '#2dd4bf',
      backgroundColor: 'rgba(45, 212, 191, 0.10)',
      borderWidth: 3,
      pointBackgroundColor: '#2dd4bf',
      pointBorderColor: '#0f1d30',
      pointBorderWidth: 2,
      pointRadius: 4,
      pointHoverRadius: 6,
      tension: 0,
      cubicInterpolationMode: 'default',
      fill: true
    },
    {
      label: 'Sales Target',
      data: monthlyTarget,
      borderColor: '#60a5fa',
      backgroundColor: 'transparent',
      borderWidth: 2,
      pointBackgroundColor: '#60a5fa',
      pointBorderColor: '#0f1d30',
      pointBorderWidth: 2,
      pointRadius: 4,
      pointHoverRadius: 6,
      tension: 0,
      cubicInterpolationMode: 'default',
      borderDash: [6, 5],
      fill: false
    }
  ]
}

const salesLineOptions = {
  responsive: true,
  maintainAspectRatio: false,
  animation: { duration: 500 },
  elements: {
    line: { tension: 0, capBezierPoints: false },
    point: { hitRadius: 10 }
  },
  interaction: { mode: 'index', intersect: false },
  plugins: {
    legend: {
      position: 'top',
      align: 'center',
      labels: {
        color: '#a8b7ca',
        usePointStyle: true,
        pointStyle: 'circle',
        boxWidth: 8,
        boxHeight: 8,
        padding: 20,
        font: { family: 'inherit', size: 11 }
      }
    },
    tooltip: {
      backgroundColor: '#071323',
      titleColor: '#e5edf7',
      bodyColor: '#c4d1e0',
      borderColor: '#34465d',
      borderWidth: 1,
      padding: 12,
      displayColors: true,
      callbacks: {
        label(context) {
          return `${context.dataset.label}: Rp ${context.parsed.y} juta`
        }
      }
    }
  },
  scales: {
    x: {
      ticks: { color: '#8294aa', font: { size: 11 } },
      grid: { color: 'rgba(130, 148, 170, 0.07)', drawBorder: false }
    },
    y: {
      beginAtZero: true,
      suggestedMax: 120,
      ticks: {
        stepSize: 20,
        color: '#8294aa',
        font: { size: 11 },
        callback(value) { return `Rp ${value} jt` }
      },
      grid: { color: 'rgba(130, 148, 170, 0.12)', drawBorder: false }
    }
  }
}

const orderStatusData = {
  labels: ['Completed', 'Pending', 'Processing'],
  datasets: [{
    data: [98, 12, 46],
    backgroundColor: ['#2dd4bf', '#fbbf24', '#60a5fa'],
    borderColor: '#122136',
    borderWidth: 4,
    hoverOffset: 7
  }]
}

const orderStatusOptions = {
  responsive: true,
  maintainAspectRatio: false,
  cutout: '68%',
  plugins: {
    legend: {
      position: 'bottom',
      labels: {
        color: '#a8b7ca',
        usePointStyle: true,
        pointStyle: 'circle',
        boxWidth: 8,
        boxHeight: 8,
        padding: 18,
        font: { family: 'inherit', size: 11 }
      }
    },
    tooltip: {
      backgroundColor: '#071323',
      titleColor: '#e5edf7',
      bodyColor: '#c4d1e0',
      borderColor: '#34465d',
      borderWidth: 1,
      padding: 12
    }
  }
}

const kpis = [
  {
    label: 'Total Revenue',
    value: 'Rp 185.500.000',
    note: 'Compared with previous period',
    change: '+12.5%',
    icon: DollarSign,
    tone: 'teal'
  },
  {
    label: 'Total Orders',
    value: '156',
    note: 'Orders this period',
    change: '+8.2%',
    icon: ShoppingCart,
    tone: 'blue'
  },
  {
    label: 'Pending Orders',
    value: '12',
    note: 'Waiting for processing',
    change: 'Needs attention',
    icon: Clock3,
    tone: 'amber'
  },
  {
    label: 'Total Customers',
    value: '48',
    note: 'Registered customers',
    change: '+4 new',
    icon: Users,
    tone: 'purple'
  }
]

const topProducts = ref([
  { code: 'FG001', name: 'Finished Product A', category: 'Finished Goods', sold: 420, revenue: 'Rp 63.000.000', stock: 'Healthy' },
  { code: 'RM001', name: 'Steel Plate', category: 'Raw Material', sold: 315, revenue: 'Rp 47.250.000', stock: 'Healthy' },
  { code: 'RM002', name: 'Aluminium Sheet', category: 'Raw Material', sold: 240, revenue: 'Rp 36.000.000', stock: 'Low stock' },
  { code: 'SP001', name: 'Bearing 6205', category: 'Sparepart', sold: 180, revenue: 'Rp 27.000.000', stock: 'Healthy' }
])

const salesOrders = ref([
  { no: 'SO-2026-0156', customer: 'PT Maju Bersama', date: '02 Nov 2026', amount: 'Rp 12.500.000', status: 'Completed' },
  { no: 'SO-2026-0155', customer: 'CV Sumber Teknik', date: '02 Nov 2026', amount: 'Rp 8.750.000', status: 'Processing' },
  { no: 'SO-2026-0154', customer: 'PT Karya Industri', date: '01 Nov 2026', amount: 'Rp 15.200.000', status: 'Pending' },
  { no: 'SO-2026-0153', customer: 'UD Sentosa', date: '01 Nov 2026', amount: 'Rp 6.400.000', status: 'Completed' },
  { no: 'SO-2026-0152', customer: 'PT Cipta Logam', date: '31 Oct 2026', amount: 'Rp 9.850.000', status: 'Processing' }
])

const searchQuery = ref('')
const filteredOrders = computed(() => {
  const query = searchQuery.value.trim().toLowerCase()
  if (!query) return salesOrders.value
  return salesOrders.value.filter(order =>
    `${order.no} ${order.customer} ${order.status}`.toLowerCase().includes(query)
  )
})

const statusClass = status => status.toLowerCase().replaceAll(' ', '-')
</script>

<template>
  <main class="sales-dashboard">
    <header class="page-heading">
      <div>
        <span class="eyebrow">SALES MANAGEMENT</span>
        <h1>Sales Dashboard</h1>
        <p>Monitor revenue, customer activity, and sales order performance.</p>
      </div>
      <div class="heading-actions">
        <span class="period-chip"><CalendarDays :size="15" /> November 2026</span>
      </div>
    </header>

    <section class="kpi-grid" aria-label="Sales key performance indicators">
      <article v-for="item in kpis" :key="item.label" class="kpi-card">
        <div class="kpi-topline">
          <span>{{ item.label }}</span>
          <span class="kpi-icon" :class="item.tone"><component :is="item.icon" :size="19" /></span>
        </div>
        <strong class="kpi-value">{{ item.value }}</strong>
        <div class="kpi-footer">
          <span>{{ item.note }}</span>
          <span class="kpi-change" :class="item.tone">{{ item.change }}</span>
        </div>
      </article>
    </section>

    <section class="chart-grid">
      <article class="panel revenue-panel">
        <div class="panel-header">
          <div>
            <h2>Monthly Sales Performance</h2>
            <p>Sales revenue compared with monthly target</p>
          </div>
          <TrendingUp class="teal-icon" :size="24" />
        </div>

        <div class="chart-summary">
          <div>
            <small>Total Revenue</small>
            <strong>Rp 185.500.000</strong>
          </div>
          <span class="growth-label"><ArrowUpRight :size="17" /> 12.5%</span>
        </div>

        <div class="sales-chart">
          <Line :data="salesLineData" :options="salesLineOptions" />
        </div>
      </article>

      <article class="panel status-panel">
        <div class="panel-header">
          <div>
            <h2>Sales Order Status</h2>
            <p>Overview of current order progress</p>
          </div>
          <ShoppingCart class="teal-icon" :size="24" />
        </div>
        <div class="status-chart">
          <Doughnut :data="orderStatusData" :options="orderStatusOptions" />
        </div>
        <p class="total-orders">Total orders: <strong>156</strong></p>
      </article>
    </section>

    <section class="panel table-panel">
      <div class="panel-header table-heading">
        <div>
          <h2>Top Selling Products</h2>
          <p>Products with the highest sales volume</p>
        </div>
        <Package class="teal-icon" :size="23" />
      </div>
      <div class="table-wrap">
        <table>
          <thead>
            <tr>
              <th>Product</th>
              <th>Category</th>
              <th class="number-cell">Qty Sold</th>
              <th class="number-cell">Sales Revenue</th>
              <th>Stock Status</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="product in topProducts" :key="product.code">
              <td>
                <div class="product-cell">
                  <span class="product-mark"><Package :size="16" /></span>
                  <span><strong>{{ product.name }}</strong><small>{{ product.code }}</small></span>
                </div>
              </td>
              <td>{{ product.category }}</td>
              <td class="number-cell">{{ product.sold.toLocaleString('en-US') }}</td>
              <td class="number-cell revenue-cell">{{ product.revenue }}</td>
              <td><span class="stock-status" :class="product.stock === 'Low stock' ? 'low' : 'healthy'">{{ product.stock }}</span></td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <section class="panel table-panel orders-panel">
      <div class="panel-header table-heading">
        <div>
          <h2>Recent Sales Orders</h2>
          <p>Latest customer orders and fulfillment progress</p>
        </div>
        <div class="order-tools">
          <label class="search-box">
            <Search :size="16" />
            <input v-model="searchQuery" type="search" placeholder="Search order or customer..." />
          </label>
          <FileText class="teal-icon desktop-icon" :size="22" />
        </div>
      </div>
      <div class="table-wrap">
        <table>
          <thead>
            <tr>
              <th>Sales Order</th>
              <th>Customer</th>
              <th>Order Date</th>
              <th class="number-cell">Amount</th>
              <th>Status</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="order in filteredOrders" :key="order.no">
              <td><strong class="order-number">{{ order.no }}</strong></td>
              <td>{{ order.customer }}</td>
              <td>{{ order.date }}</td>
              <td class="number-cell revenue-cell">{{ order.amount }}</td>
              <td><span class="status-pill" :class="statusClass(order.status)"><CircleCheck v-if="order.status === 'Completed'" :size="13" /><Truck v-else-if="order.status === 'Processing'" :size="13" /><Clock3 v-else :size="13" />{{ order.status }}</span></td>
            </tr>
            <tr v-if="filteredOrders.length === 0">
              <td colspan="5" class="empty-state"><Eye :size="17" /> No sales orders match your search.</td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="table-footer">Showing {{ filteredOrders.length }} of {{ salesOrders.length }} recent orders</div>
    </section>
  </main>
</template>

<style scoped>
.sales-dashboard {
  width: 100%;
  min-width: 0;
  padding: 30px 32px 40px;
  color: #e5edf7;
  box-sizing: border-box;
}

.page-heading {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  gap: 20px;
  margin-bottom: 26px;
}
.eyebrow { display: block; margin-bottom: 8px; color: #2dd4bf; font-size: 10px; font-weight: 700; letter-spacing: 1.6px; }
.page-heading h1 { margin: 0; color: #e8eef8; font-size: 27px; font-weight: 700; letter-spacing: -.5px; }
.page-heading p { margin: 8px 0 0; color: #91a3b9; font-size: 14px; }
.period-chip { display: inline-flex; align-items: center; gap: 8px; padding: 10px 13px; border: 1px solid #2b4058; border-radius: 9px; color: #b8c7d9; background: #122136; font-size: 12px; white-space: nowrap; }

.kpi-grid { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 18px; margin-bottom: 24px; }
.kpi-card, .panel { min-width: 0; border: 1px solid #263a52; border-radius: 20px; background: #122136; box-shadow: 0 8px 24px rgba(0, 0, 0, .08); }
.kpi-card { padding: 20px 21px 18px; }
.kpi-topline, .kpi-footer { display: flex; align-items: center; justify-content: space-between; gap: 10px; }
.kpi-topline { color: #9aacc1; font-size: 13px; }
.kpi-icon { display: grid; width: 38px; height: 38px; place-items: center; border-radius: 11px; }
.kpi-icon.teal { color: #2dd4bf; background: rgba(45, 212, 191, .12); }
.kpi-icon.blue { color: #60a5fa; background: rgba(96, 165, 250, .12); }
.kpi-icon.amber { color: #fbbf24; background: rgba(251, 191, 36, .12); }
.kpi-icon.purple { color: #c4b5fd; background: rgba(196, 181, 253, .12); }
.kpi-value { display: block; margin: 15px 0 14px; color: #edf3fb; font-size: clamp(20px, 1.7vw, 25px); font-weight: 700; letter-spacing: -.4px; white-space: nowrap; }
.kpi-footer { align-items: flex-start; color: #7f93aa; font-size: 11px; line-height: 1.5; }
.kpi-change { flex-shrink: 0; font-size: 11px; font-weight: 600; }
.kpi-change.teal, .kpi-change.blue { color: #2dd4bf; }
.kpi-change.amber { color: #fbbf24; }
.kpi-change.purple { color: #c4b5fd; }

.chart-grid { display: grid; grid-template-columns: minmax(0, 1.55fr) minmax(310px, 1fr); gap: 22px; margin-bottom: 24px; }
.panel { padding: 25px 26px; }
.panel-header { display: flex; align-items: flex-start; justify-content: space-between; gap: 18px; }
.panel-header h2 { margin: 0; color: #e5edf7; font-size: 21px; font-weight: 650; letter-spacing: -.3px; }
.panel-header p { margin: 7px 0 0; color: #9aacc1; font-size: 13px; }
.teal-icon { flex-shrink: 0; color: #2dd4bf; }
.chart-summary { display: flex; align-items: flex-end; justify-content: space-between; gap: 16px; margin: 25px 0 4px; }
.chart-summary small { display: block; margin-bottom: 8px; color: #9aacc1; font-size: 12px; }
.chart-summary strong { color: #edf3fb; font-size: 27px; font-weight: 700; letter-spacing: -.4px; }
.growth-label { display: inline-flex; align-items: center; gap: 4px; padding-bottom: 5px; color: #2dd4bf; font-size: 13px; font-weight: 700; white-space: nowrap; }
.sales-chart { position: relative; width: 100%; height: 290px; margin-top: 14px; }
.status-chart { position: relative; width: min(100%, 290px); height: 270px; margin: 22px auto 5px; }
.total-orders { margin: 0; color: #9aacc1; text-align: center; font-size: 12px; }
.total-orders strong { color: #dce7f4; font-weight: 650; }

.table-panel { margin-bottom: 24px; padding-bottom: 12px; }
.table-heading { align-items: center; margin-bottom: 21px; }
.order-tools { display: flex; align-items: center; gap: 16px; }
.search-box { display: flex; align-items: center; gap: 8px; width: min(270px, 34vw); padding: 9px 11px; border: 1px solid #30445d; border-radius: 9px; color: #8294aa; background: #0d1a2b; }
.search-box input { width: 100%; min-width: 0; border: 0; outline: 0; color: #dce7f4; background: transparent; font: inherit; font-size: 11px; }
.search-box input::placeholder { color: #71849b; }
.table-wrap { width: 100%; overflow-x: auto; }
table { width: 100%; border-collapse: collapse; text-align: left; white-space: nowrap; }
thead th { padding: 12px 13px; border-bottom: 1px solid #2a3e56; color: #8294aa; font-size: 10px; font-weight: 650; letter-spacing: .65px; text-transform: uppercase; }
tbody td { padding: 14px 13px; border-bottom: 1px solid rgba(52, 70, 93, .55); color: #aebdd0; font-size: 12px; }
tbody tr:last-child td { border-bottom: 0; }
tbody tr:hover { background: rgba(255, 255, 255, .018); }
.number-cell { text-align: right; }
.product-cell { display: flex; align-items: center; gap: 10px; }
.product-mark { display: grid; width: 32px; height: 32px; place-items: center; border-radius: 9px; color: #2dd4bf; background: rgba(45, 212, 191, .1); }
.product-cell strong { display: block; color: #dce7f4; font-size: 12px; font-weight: 600; }
.product-cell small { display: block; margin-top: 4px; color: #71849b; font-size: 10px; }
.revenue-cell { color: #dce7f4; font-weight: 600; }
.stock-status, .status-pill { display: inline-flex; align-items: center; gap: 5px; padding: 5px 9px; border-radius: 20px; font-size: 10px; font-weight: 600; }
.stock-status.healthy { color: #2dd4bf; background: rgba(45, 212, 191, .1); }
.stock-status.low { color: #fbbf24; background: rgba(251, 191, 36, .1); }
.order-number { color: #60a5fa; font-size: 11px; font-weight: 650; }
.status-pill.completed { color: #2dd4bf; background: rgba(45, 212, 191, .1); }
.status-pill.processing { color: #60a5fa; background: rgba(96, 165, 250, .1); }
.status-pill.pending { color: #fbbf24; background: rgba(251, 191, 36, .1); }
.table-footer { padding: 12px 13px 3px; border-top: 1px solid rgba(52, 70, 93, .45); color: #71849b; font-size: 10px; }
.empty-state { padding: 24px; color: #8294aa; text-align: center; }
.empty-state svg { margin-right: 7px; vertical-align: middle; }

@media (max-width: 1200px) {
  .kpi-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .chart-grid { grid-template-columns: minmax(0, 1.3fr) minmax(280px, 1fr); }
  .kpi-value { font-size: 22px; }
}
@media (max-width: 900px) {
  .sales-dashboard { padding: 24px 20px 32px; }
  .chart-grid { grid-template-columns: 1fr; }
  .status-chart { height: 250px; }
}
@media (max-width: 600px) {
  .sales-dashboard { padding: 19px 13px 28px; }
  .page-heading { align-items: flex-start; flex-direction: column; }
  .page-heading h1 { font-size: 23px; }
  .kpi-grid { grid-template-columns: 1fr 1fr; gap: 10px; }
  .kpi-card { padding: 15px 13px; border-radius: 14px; }
  .kpi-topline { font-size: 11px; }
  .kpi-icon { width: 32px; height: 32px; }
  .kpi-value { margin: 12px 0; font-size: 17px; }
  .kpi-footer { flex-direction: column; gap: 3px; font-size: 10px; }
  .panel { padding: 19px 15px; border-radius: 15px; }
  .panel-header h2 { font-size: 18px; }
  .panel-header p { font-size: 11px; }
  .chart-summary strong { font-size: 22px; }
  .sales-chart { height: 245px; }
  .status-chart { height: 225px; }
  .table-heading { align-items: flex-start; flex-direction: column; }
  .order-tools { width: 100%; }
  .search-box { width: 100%; }
  .desktop-icon { display: none; }
}
</style>
