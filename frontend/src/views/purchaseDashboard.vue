<script setup>
import { computed, ref } from 'vue'
import {
  Chart as ChartJS,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  ArcElement,
  LineController,
  DoughnutController,
  Tooltip,
  Legend,
  Filler
} from 'chart.js'
import { Line, Doughnut } from 'vue-chartjs'
import {
  Wallet,
  ClipboardList,
  Clock3,
  Truck,
  TrendingUp,
  ShoppingCart,
  Search,
  ArrowUpRight,
  PackageCheck,
  Building2,
  CalendarDays
} from 'lucide-vue-next'

ChartJS.register(
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  ArcElement,
  LineController,
  DoughnutController,
  Tooltip,
  Legend,
  Filler
)

const purchaseKpis = [
  {
    label: 'Total Purchase',
    value: 'Rp 95.000.000',
    note: 'Compared with previous period',
    change: '+10.8%',
    icon: Wallet,
    tone: 'teal'
  },
  {
    label: 'Total Purchase Orders',
    value: '42',
    note: 'Orders this period',
    change: '+6.2%',
    icon: ClipboardList,
    tone: 'blue'
  },
  {
    label: 'Pending Purchase Orders',
    value: '8',
    note: 'Waiting for approval',
    change: 'Needs attention',
    icon: Clock3,
    tone: 'amber'
  },
  {
    label: 'Active Suppliers',
    value: '18',
    note: 'Registered suppliers',
    change: '+2 new',
    icon: Truck,
    tone: 'purple'
  }
]

const purchaseLineData = {
  labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
  datasets: [
    {
      label: 'Purchase Amount',
      data: [48, 62, 55, 72, 68, 95],
      borderColor: '#2dd4bf',
      backgroundColor: 'rgba(45, 212, 191, 0.12)',
      borderWidth: 3,
      pointBackgroundColor: '#2dd4bf',
      pointBorderColor: '#0f1e30',
      pointBorderWidth: 2,
      pointRadius: 4,
      pointHoverRadius: 6,
      tension: 0,
      cubicInterpolationMode: 'default',
      fill: true
    },
    {
      label: 'Purchase Budget',
      data: [55, 60, 65, 70, 78, 85],
      borderColor: '#60a5fa',
      backgroundColor: 'transparent',
      borderWidth: 2,
      pointBackgroundColor: '#60a5fa',
      pointBorderColor: '#0f1e30',
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

const purchaseLineOptions = {
  responsive: true,
  maintainAspectRatio: false,
  elements: {
    line: { tension: 0 }
  },
  interaction: {
    mode: 'index',
    intersect: false
  },
  plugins: {
    legend: {
      position: 'top',
      labels: {
        color: '#a8b7ca',
        usePointStyle: true,
        pointStyle: 'circle',
        padding: 18,
        boxWidth: 8
      }
    },
    tooltip: {
      backgroundColor: '#071321',
      titleColor: '#e5edf7',
      bodyColor: '#cbd5e1',
      borderColor: '#34465d',
      borderWidth: 1,
      padding: 12,
      callbacks: {
        label(context) {
          return `${context.dataset.label}: Rp ${context.parsed.y} juta`
        }
      }
    }
  },
  scales: {
    x: {
      ticks: { color: '#8294aa' },
      grid: { color: 'rgba(130, 148, 170, 0.07)' },
      border: { color: '#34465d' }
    },
    y: {
      beginAtZero: true,
      ticks: {
        color: '#8294aa',
        callback(value) { return `Rp ${value} jt` }
      },
      grid: { color: 'rgba(130, 148, 170, 0.12)' },
      border: { display: false }
    }
  }
}

const purchaseStatusData = {
  labels: ['Received', 'Pending', 'Approved', 'Cancelled'],
  datasets: [
    {
      data: [22, 8, 10, 2],
      backgroundColor: ['#2dd4bf', '#fbbf24', '#60a5fa', '#64748b'],
      borderColor: '#122136',
      borderWidth: 4,
      hoverOffset: 7
    }
  ]
}

const purchaseStatusOptions = {
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
        padding: 18,
        boxWidth: 8
      }
    },
    tooltip: {
      backgroundColor: '#071321',
      titleColor: '#e5edf7',
      bodyColor: '#cbd5e1',
      padding: 12
    }
  }
}

const topSuppliers = [
  { code: 'SUP001', name: 'PT Steel Indonesia', category: 'Raw Materials', orders: 12, amount: 'Rp 32.500.000', status: 'Active' },
  { code: 'SUP002', name: 'PT Aluminium Jaya', category: 'Raw Materials', orders: 9, amount: 'Rp 24.000.000', status: 'Active' },
  { code: 'SUP003', name: 'PT Sparepart Makmur', category: 'Spare Parts', orders: 8, amount: 'Rp 18.500.000', status: 'Active' },
  { code: 'SUP004', name: 'CV Teknik Sejahtera', category: 'Tools & Equipment', orders: 7, amount: 'Rp 12.000.000', status: 'Active' }
]

const purchaseOrders = ref([
  { number: 'PO-2026-0042', supplier: 'PT Steel Indonesia', date: '02 Nov 2026', expected: '08 Nov 2026', amount: 'Rp 12.500.000', status: 'Pending' },
  { number: 'PO-2026-0041', supplier: 'PT Aluminium Jaya', date: '01 Nov 2026', expected: '06 Nov 2026', amount: 'Rp 8.750.000', status: 'Approved' },
  { number: 'PO-2026-0040', supplier: 'PT Sparepart Makmur', date: '30 Oct 2026', expected: '04 Nov 2026', amount: 'Rp 5.250.000', status: 'Received' },
  { number: 'PO-2026-0039', supplier: 'CV Teknik Sejahtera', date: '28 Oct 2026', expected: '03 Nov 2026', amount: 'Rp 3.800.000', status: 'Received' },
  { number: 'PO-2026-0038', supplier: 'PT Steel Indonesia', date: '26 Oct 2026', expected: '01 Nov 2026', amount: 'Rp 9.600.000', status: 'Cancelled' }
])

const searchQuery = ref('')
const selectedStatus = ref('All Status')
const statusOptions = ['All Status', 'Pending', 'Approved', 'Received', 'Cancelled']

const filteredPurchaseOrders = computed(() => {
  const query = searchQuery.value.trim().toLowerCase()
  return purchaseOrders.value.filter(order => {
    const matchesQuery = !query ||
      order.number.toLowerCase().includes(query) ||
      order.supplier.toLowerCase().includes(query)
    const matchesStatus = selectedStatus.value === 'All Status' || order.status === selectedStatus.value
    return matchesQuery && matchesStatus
  })
})

function statusClass(status) {
  return `status-${status.toLowerCase()}`
}
</script>

<template>
  <div class="purchase-dashboard">
    <section class="page-heading">
      <div>
        <div class="eyebrow"><ShoppingCart :size="15" /> PROCUREMENT OVERVIEW</div>
        <h1>Purchasing Dashboard</h1>
        <p>Monitor purchase spending, supplier performance, and purchase orders.</p>
      </div>
      <div class="period-label"><CalendarDays :size="16" /> January – June 2026</div>
    </section>

    <section class="purchase-kpi-grid">
      <article v-for="item in purchaseKpis" :key="item.label" class="purchase-kpi-card">
        <div class="kpi-topline">
          <span>{{ item.label }}</span>
          <div class="kpi-icon" :class="`tone-${item.tone}`"><component :is="item.icon" :size="21" /></div>
        </div>
        <strong class="kpi-value">{{ item.value }}</strong>
        <div class="kpi-bottomline">
          <small>{{ item.note }}</small>
          <span :class="item.tone === 'amber' ? 'attention-text' : 'positive-text'">{{ item.change }}</span>
        </div>
      </article>
    </section>

    <section class="purchase-chart-grid">
      <article class="purchase-panel purchase-trend-panel">
        <div class="panel-heading">
          <div>
            <h2>Monthly Purchase Performance</h2>
            <p>Purchase spending compared with monthly budget</p>
          </div>
          <TrendingUp class="panel-icon" :size="25" />
        </div>

        <div class="purchase-chart-summary">
          <div>
            <small>Total Purchase</small>
            <strong>Rp 95.000.000</strong>
          </div>
          <span class="growth-indicator"><ArrowUpRight :size="17" /> 10.8%</span>
        </div>

        <div class="purchase-line-chart">
          <Line :data="purchaseLineData" :options="purchaseLineOptions" />
        </div>
      </article>

      <article class="purchase-panel purchase-status-panel">
        <div class="panel-heading">
          <div>
            <h2>Purchase Order Status</h2>
            <p>Overview of current purchase order progress</p>
          </div>
          <ClipboardList class="panel-icon" :size="25" />
        </div>
        <div class="purchase-doughnut-chart">
          <Doughnut :data="purchaseStatusData" :options="purchaseStatusOptions" />
        </div>
        <div class="status-total">Total purchase orders: <strong>42</strong></div>
      </article>
    </section>

    <section class="purchase-panel supplier-panel">
      <div class="panel-heading section-panel-heading">
        <div>
          <h2>Top Suppliers</h2>
          <p>Suppliers ranked by purchase value</p>
        </div>
        <Building2 class="panel-icon" :size="25" />
      </div>

      <div class="table-scroll">
        <table class="purchase-table">
          <thead>
            <tr>
              <th>Supplier</th>
              <th>Category</th>
              <th>Purchase Orders</th>
              <th>Total Purchase</th>
              <th>Status</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="supplier in topSuppliers" :key="supplier.code">
              <td>
                <div class="supplier-name-cell">
                  <span class="supplier-avatar">{{ supplier.code.slice(-2) }}</span>
                  <span><strong>{{ supplier.name }}</strong><small>{{ supplier.code }}</small></span>
                </div>
              </td>
              <td>{{ supplier.category }}</td>
              <td>{{ supplier.orders }}</td>
              <td class="amount-cell">{{ supplier.amount }}</td>
              <td><span class="status-pill status-received">{{ supplier.status }}</span></td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <section class="purchase-panel recent-po-panel">
      <div class="panel-heading section-panel-heading">
        <div>
          <h2>Recent Purchase Orders</h2>
          <p>Latest procurement transactions</p>
        </div>
        <PackageCheck class="panel-icon" :size="25" />
      </div>

      <div class="purchase-table-tools">
        <label class="purchase-search">
          <Search :size="17" />
          <input v-model="searchQuery" type="search" placeholder="Search PO number or supplier..." />
        </label>
        <select v-model="selectedStatus" aria-label="Filter purchase order status">
          <option v-for="status in statusOptions" :key="status" :value="status">{{ status }}</option>
        </select>
      </div>

      <div class="table-scroll">
        <table class="purchase-table">
          <thead>
            <tr>
              <th>PO Number</th>
              <th>Supplier</th>
              <th>Order Date</th>
              <th>Expected Delivery</th>
              <th>Total Amount</th>
              <th>Status</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="order in filteredPurchaseOrders" :key="order.number">
              <td class="po-number">{{ order.number }}</td>
              <td>{{ order.supplier }}</td>
              <td>{{ order.date }}</td>
              <td>{{ order.expected }}</td>
              <td class="amount-cell">{{ order.amount }}</td>
              <td><span class="status-pill" :class="statusClass(order.status)">{{ order.status }}</span></td>
            </tr>
            <tr v-if="filteredPurchaseOrders.length === 0">
              <td colspan="6" class="empty-state">No purchase orders match your search.</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <section class="purchase-summary-grid">
      <article class="purchase-summary-card">
        <div class="summary-icon"><Wallet :size="20" /></div>
        <div><small>Average PO Value</small><strong>Rp 2.261.905</strong><span>Average value per purchase order</span></div>
      </article>
      <article class="purchase-summary-card">
        <div class="summary-icon blue-summary"><Truck :size="20" /></div>
        <div><small>On-time Delivery</small><strong>92.5%</strong><span>Supplier delivery performance</span></div>
      </article>
      <article class="purchase-summary-card">
        <div class="summary-icon amber-summary"><Clock3 :size="20" /></div>
        <div><small>Awaiting Approval</small><strong>8 Orders</strong><span>Purchase orders needing review</span></div>
      </article>
    </section>

    <p class="mock-data-note">Dashboard preview · Sample data for UI development · Not connected to SQLite yet</p>
  </div>
</template>

<style scoped>
.purchase-dashboard {
  min-height: calc(100vh - 68px);
  padding: 30px 32px 42px;
  color: #e5edf7;
  background: #0b1422;
}
.page-heading,
.panel-heading,
.kpi-topline,
.kpi-bottomline,
.purchase-chart-summary,
.purchase-table-tools {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.page-heading { gap: 20px; margin-bottom: 26px; }
.eyebrow { display: flex; align-items: center; gap: 8px; color: #5eead4; font-size: 10px; font-weight: 700; letter-spacing: 1.4px; margin-bottom: 9px; }
.page-heading h1 { margin: 0; color: #edf4fc; font-size: 27px; font-weight: 700; }
.page-heading p, .panel-heading p { margin: 7px 0 0; color: #9aacc2; font-size: 14px; }
.period-label { display: flex; align-items: center; gap: 9px; padding: 10px 13px; border: 1px solid #293b52; border-radius: 10px; color: #a8b7ca; background: #111f32; font-size: 12px; white-space: nowrap; }
.purchase-kpi-grid { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 18px; margin-bottom: 24px; }
.purchase-kpi-card, .purchase-panel, .purchase-summary-card { border: 1px solid #263950; border-radius: 21px; background: #122136; box-shadow: 0 8px 24px rgba(0,0,0,.08); }
.purchase-kpi-card { min-width: 0; padding: 23px 24px 20px; }
.kpi-topline { gap: 10px; color: #a8b7ca; font-size: 13px; }
.kpi-icon { width: 47px; height: 47px; flex: 0 0 47px; display: grid; place-items: center; border-radius: 14px; }
.tone-teal { color: #2dd4bf; background: rgba(45,212,191,.13); }
.tone-blue { color: #60a5fa; background: rgba(96,165,250,.14); }
.tone-amber { color: #fbbf24; background: rgba(251,191,36,.13); }
.tone-purple { color: #c4b5fd; background: rgba(167,139,250,.14); }
.kpi-value { display: block; margin: 19px 0 17px; color: #f1f5fb; font-size: clamp(21px, 2vw, 27px); letter-spacing: -.5px; }
.kpi-bottomline { align-items: flex-start; gap: 8px; color: #8294aa; font-size: 11px; }
.kpi-bottomline small { max-width: 68%; line-height: 1.6; }
.positive-text { color: #2dd4bf; font-weight: 600; white-space: nowrap; }
.attention-text { color: #fbbf24; font-weight: 600; white-space: nowrap; }
.purchase-chart-grid { display: grid; grid-template-columns: minmax(0, 1.55fr) minmax(310px, 1fr); gap: 22px; margin-bottom: 24px; }
.purchase-panel { min-width: 0; padding: 25px 27px; }
.panel-heading { gap: 12px; align-items: flex-start; }
.panel-heading h2 { margin: 0; color: #e7eef8; font-size: 21px; font-weight: 650; }
.panel-heading p { font-size: 13px; }
.panel-icon { flex: 0 0 auto; color: #5eead4; }
.purchase-chart-summary { margin: 26px 0 10px; }
.purchase-chart-summary small { display: block; margin-bottom: 7px; color: #9aacc2; font-size: 12px; }
.purchase-chart-summary strong { color: #f1f5fb; font-size: 27px; }
.growth-indicator { display: flex; align-items: center; gap: 4px; color: #2dd4bf; font-size: 13px; font-weight: 650; }
.purchase-line-chart { position: relative; width: 100%; height: 285px; margin-top: 13px; }
.purchase-status-panel { display: flex; flex-direction: column; }
.purchase-doughnut-chart { position: relative; width: 100%; height: 285px; margin: 20px auto 0; }
.status-total { margin-top: 3px; text-align: center; color: #9aacc2; font-size: 12px; }
.status-total strong { color: #e5edf7; }
.section-panel-heading { margin-bottom: 22px; }
.supplier-panel, .recent-po-panel { margin-bottom: 24px; }
.table-scroll { width: 100%; overflow-x: auto; }
.purchase-table { width: 100%; border-collapse: collapse; text-align: left; white-space: nowrap; }
.purchase-table th { padding: 13px 14px; color: #8294aa; background: #0f1c2e; border-bottom: 1px solid #2a3c52; font-size: 11px; font-weight: 600; }
.purchase-table td { padding: 15px 14px; color: #b7c4d5; border-bottom: 1px solid rgba(52,70,93,.55); font-size: 12px; }
.purchase-table tbody tr:last-child td { border-bottom: 0; }
.purchase-table tbody tr:hover { background: rgba(45,212,191,.035); }
.supplier-name-cell { display: flex; align-items: center; gap: 11px; }
.supplier-avatar { width: 34px; height: 34px; display: grid; place-items: center; border-radius: 10px; color: #5eead4; background: rgba(45,212,191,.12); font-size: 11px; font-weight: 700; }
.supplier-name-cell strong { display: block; color: #e2eaf4; font-size: 12px; font-weight: 600; }
.supplier-name-cell small { display: block; margin-top: 4px; color: #71849b; font-size: 10px; }
.amount-cell { color: #e5edf7 !important; font-weight: 650; }
.status-pill { display: inline-flex; align-items: center; padding: 6px 10px; border-radius: 20px; font-size: 10px; font-weight: 650; }
.status-pending { color: #fbbf24; background: rgba(251,191,36,.12); }
.status-approved { color: #60a5fa; background: rgba(96,165,250,.13); }
.status-received { color: #2dd4bf; background: rgba(45,212,191,.12); }
.status-cancelled { color: #cbd5e1; background: rgba(148,163,184,.13); }
.purchase-table-tools { gap: 12px; margin: -2px 0 18px; }
.purchase-search { display: flex; align-items: center; gap: 9px; width: min(360px, 100%); padding: 10px 12px; border: 1px solid #30445d; border-radius: 9px; color: #8294aa; background: #0e1b2c; }
.purchase-search input { width: 100%; min-width: 0; border: 0; outline: 0; color: #e5edf7; background: transparent; font: inherit; font-size: 12px; }
.purchase-search input::placeholder { color: #71849b; }
.purchase-table-tools select { padding: 10px 12px; border: 1px solid #30445d; border-radius: 9px; outline: 0; color: #b7c4d5; background: #0e1b2c; font: inherit; font-size: 12px; }
.empty-state { padding: 28px !important; text-align: center; color: #8294aa !important; }
.purchase-summary-grid { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 18px; }
.purchase-summary-card { display: flex; align-items: center; gap: 15px; padding: 20px; }
.summary-icon { width: 43px; height: 43px; flex: 0 0 43px; display: grid; place-items: center; border-radius: 13px; color: #2dd4bf; background: rgba(45,212,191,.13); }
.blue-summary { color: #60a5fa; background: rgba(96,165,250,.13); }
.amber-summary { color: #fbbf24; background: rgba(251,191,36,.13); }
.purchase-summary-card small, .purchase-summary-card strong, .purchase-summary-card span { display: block; }
.purchase-summary-card small { color: #9aacc2; font-size: 11px; }
.purchase-summary-card strong { margin: 6px 0; color: #eaf1fa; font-size: 20px; }
.purchase-summary-card span { color: #71849b; font-size: 10px; }
.mock-data-note { margin: 20px 2px 0; color: #657991; text-align: right; font-size: 10px; }

@media (max-width: 1150px) {
  .purchase-kpi-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .purchase-chart-grid { grid-template-columns: minmax(0, 1fr); }
  .purchase-status-panel { min-height: 450px; }
  .purchase-doughnut-chart { max-width: 360px; }
}
@media (max-width: 700px) {
  .purchase-dashboard { padding: 22px 16px 32px; }
  .page-heading { align-items: flex-start; flex-direction: column; }
  .page-heading h1 { font-size: 23px; }
  .purchase-kpi-grid, .purchase-summary-grid { grid-template-columns: minmax(0, 1fr); }
  .purchase-panel { padding: 20px 16px; border-radius: 16px; }
  .panel-heading h2 { font-size: 18px; }
  .purchase-chart-summary strong { font-size: 23px; }
  .purchase-line-chart { height: 250px; }
  .purchase-doughnut-chart { height: 260px; }
  .purchase-table-tools { align-items: stretch; flex-direction: column; }
  .purchase-search { width: 100%; }
  .purchase-table-tools select { width: 100%; }
  .mock-data-note { text-align: left; line-height: 1.5; }
}
</style>
