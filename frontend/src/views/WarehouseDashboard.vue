
<script setup>
import {
  Package,
  Boxes,
  AlertTriangle,
  Warehouse,
  ArrowDownToLine,
  ArrowUpFromLine,
  ArrowLeftRight,
  Clock3,
  MapPin,
  Activity
} from 'lucide-vue-next'

const stats = [
  {
    title: 'Total Products',
    value: '4',
    subtitle: 'Registered products',
    icon: Package,
    color: 'teal'
  },
  {
    title: 'Total Stock',
    value: '255 PCS',
    subtitle: 'Current stock quantity',
    icon: Boxes,
    color: 'blue'
  },
  {
    title: 'Low Stock Items',
    value: '0',
    subtitle: 'Below minimum stock',
    icon: AlertTriangle,
    color: 'purple'
  },
  {
    title: 'Total Warehouses',
    value: '3',
    subtitle: 'Registered warehouses',
    icon: Warehouse,
    color: 'orange'
  }
]

const warehouses = [
  {
    code: 'WH001',
    name: 'Raw Material Warehouse',
    location: 'Main Building',
    stock: 255,
    percentage: 100,
    color: 'teal'
  },
  {
    code: 'WH002',
    name: 'Production Warehouse',
    location: 'Production Area',
    stock: 0,
    percentage: 0,
    color: 'blue'
  },
  {
    code: 'WH003',
    name: 'Finished Goods Warehouse',
    location: 'Finished Goods Area',
    stock: 0,
    percentage: 0,
    color: 'purple'
  }
]

const stockItems = [
  {
    code: 'RM001',
    name: 'Steel Plate',
    warehouse: 'WH001',
    quantity: 100,
    unit: 'PCS',
    minimum: 10,
    status: 'Normal'
  },
  {
    code: 'RM002',
    name: 'Aluminium Sheet',
    warehouse: 'WH001',
    quantity: 80,
    unit: 'PCS',
    minimum: 20,
    status: 'Normal'
  },
  {
    code: 'FG001',
    name: 'Finished Product A',
    warehouse: 'WH001',
    quantity: 25,
    unit: 'PCS',
    minimum: 5,
    status: 'Normal'
  },
  {
    code: 'SP001',
    name: 'Bearing 6205',
    warehouse: 'WH001',
    quantity: 50,
    unit: 'PCS',
    minimum: 3,
    status: 'Normal'
  }
]

const movements = [
  { month: 'Jan', incoming: 80, outgoing: 45 },
  { month: 'Feb', incoming: 65, outgoing: 35 },
  { month: 'Mar', incoming: 95, outgoing: 60 },
  { month: 'Apr', incoming: 75, outgoing: 50 },
  { month: 'May', incoming: 110, outgoing: 70 },
  { month: 'Jun', incoming: 90, outgoing: 55 }
]

const transactions = [
  {
    number: 'STK-IN-0001',
    type: 'Stock In',
    product: 'Steel Plate',
    quantity: '+100 PCS',
    warehouse: 'WH001',
    date: '02 Nov 2026',
    status: 'Posted'
  },
  {
    number: 'STK-IN-0001',
    type: 'Stock In',
    product: 'Aluminium Sheet',
    quantity: '+80 PCS',
    warehouse: 'WH001',
    date: '02 Nov 2026',
    status: 'Posted'
  },
  {
    number: 'STK-IN-0001',
    type: 'Stock In',
    product: 'Finished Product A',
    quantity: '+25 PCS',
    warehouse: 'WH001',
    date: '02 Nov 2026',
    status: 'Posted'
  },
  {
    number: 'STK-IN-0001',
    type: 'Stock In',
    product: 'Bearing 6205',
    quantity: '+50 PCS',
    warehouse: 'WH001',
    date: '02 Nov 2026',
    status: 'Posted'
  }
]
</script>

<template>
  <div class="warehouse-dashboard">

    <!-- Header -->
    <section class="page-header">
      <div>
        <h1>Warehouse Dashboard</h1>
        <p>Inventory overview and warehouse operations</p>
      </div>

      <div class="date-label">
        <Clock3 :size="17" />
        02 November 2026
      </div>
    </section>

    <!-- KPI Cards -->
    <section class="stats-grid">
      <div
        v-for="stat in stats"
        :key="stat.title"
        class="stat-card"
      >
        <div class="stat-top">
          <div :class="['stat-icon', stat.color]">
            <component :is="stat.icon" :size="25" />
          </div>
        </div>

        <p>{{ stat.title }}</p>
        <h2>{{ stat.value }}</h2>
        <small>{{ stat.subtitle }}</small>
      </div>
    </section>

    <!-- Warehouse Overview -->
    <section class="panel warehouse-panel">
      <div class="panel-header">
        <div>
          <h2>Warehouse Overview</h2>
          <p>Stock distribution by warehouse</p>
        </div>
        <Warehouse class="teal-icon" :size="23" />
      </div>

      <div class="warehouse-grid">
        <div
          v-for="warehouse in warehouses"
          :key="warehouse.code"
          class="warehouse-card"
        >
          <div class="warehouse-card-top">
            <div class="warehouse-symbol">
              <Warehouse :size="23" />
            </div>
            <span class="warehouse-code">{{ warehouse.code }}</span>
          </div>

          <h3>{{ warehouse.name }}</h3>

          <div class="warehouse-location">
            <MapPin :size="14" />
            {{ warehouse.location }}
          </div>

          <div class="warehouse-stock">
            <strong>{{ warehouse.stock }} PCS</strong>
            <span>Stock Quantity</span>
          </div>

          <div class="progress-track">
            <div
              :class="['progress-fill', warehouse.color]"
              :style="{ width: warehouse.percentage + '%' }"
            ></div>
          </div>
        </div>
      </div>
    </section>

    <!-- Stock Movement -->
    <section class="panel movement-panel">
      <div class="panel-header">
        <div>
          <h2>Stock Movement</h2>
          <p>Monthly stock in vs stock out</p>
        </div>

        <Activity class="teal-icon" :size="23" />
      </div>

      <div class="chart-legend">
        <span><i class="legend-in"></i> Stock In</span>
        <span><i class="legend-out"></i> Stock Out</span>
      </div>

      <div class="movement-chart">
        <div
          v-for="item in movements"
          :key="item.month"
          class="chart-column"
        >
          <div class="bar-group">
            <div
              class="bar bar-in"
              :style="{ height: item.incoming + 'px' }"
              :title="'Stock In: ' + item.incoming"
            ></div>

            <div
              class="bar bar-out"
              :style="{ height: item.outgoing + 'px' }"
              :title="'Stock Out: ' + item.outgoing"
            ></div>
          </div>

          <span>{{ item.month }}</span>
        </div>
      </div>
    </section>

    <!-- Stock Items -->
    <section class="panel stock-panel">
      <div class="panel-header">
        <div>
          <h2>Stock Overview</h2>
          <p>Current inventory by product</p>
        </div>
        <Package class="teal-icon" :size="23" />
      </div>

      <div class="table-wrapper">
        <table>
          <thead>
            <tr>
              <th>Product Code</th>
              <th>Product Name</th>
              <th>Warehouse</th>
              <th>Quantity</th>
              <th>Minimum Stock</th>
              <th>Status</th>
            </tr>
          </thead>

          <tbody>
            <tr
              v-for="item in stockItems"
              :key="item.code"
            >
              <td>{{ item.code }}</td>
              <td class="product-name">{{ item.name }}</td>
              <td>{{ item.warehouse }}</td>
              <td>{{ item.quantity }} {{ item.unit }}</td>
              <td>{{ item.minimum }} {{ item.unit }}</td>
              <td>
                <span class="status-badge">
                  {{ item.status }}
                </span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <!-- Recent Transactions -->
    <section class="panel transaction-panel">
      <div class="panel-header">
        <div>
          <h2>Recent Warehouse Transactions</h2>
          <p>Latest stock movements</p>
        </div>
        <ArrowLeftRight class="teal-icon" :size="23" />
      </div>

      <div class="table-wrapper">
        <table>
          <thead>
            <tr>
              <th>Transaction No.</th>
              <th>Type</th>
              <th>Product</th>
              <th>Quantity</th>
              <th>Warehouse</th>
              <th>Date</th>
              <th>Status</th>
            </tr>
          </thead>

          <tbody>
            <tr
              v-for="(item, index) in transactions"
              :key="index"
            >
              <td>{{ item.number }}</td>
              <td>
                <span class="transaction-type">
                  <ArrowDownToLine :size="14" />
                  {{ item.type }}
                </span>
              </td>
              <td class="product-name">{{ item.product }}</td>
              <td class="quantity-in">{{ item.quantity }}</td>
              <td>{{ item.warehouse }}</td>
              <td>{{ item.date }}</td>
              <td>
                <span class="status-badge">{{ item.status }}</span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <footer class="dashboard-footer">
      Gunawan Brothers ERP
      <span>Warehouse Management Module</span>
    </footer>

  </div>
</template>

<style scoped>
.warehouse-dashboard {
  padding: 38px 46px;
  color: #e2e8f0;
  min-height: 100%;
}

.page-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  margin-bottom: 38px;
}

.page-header h1 {
  font-size: 34px;
  margin-bottom: 10px;
}

.page-header p,
.panel-header p {
  color: #94a3b8;
  font-size: 15px;
}

.date-label {
  display: flex;
  align-items: center;
  gap: 9px;
  padding: 13px 17px;
  background: #17263a;
  border: 1px solid #293b52;
  border-radius: 10px;
  color: #cbd5e1;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 28px;
  margin-bottom: 30px;
}

.stat-card,
.panel {
  background: #111f32;
  border: 1px solid #26364b;
  border-radius: 18px;
}

.stat-card {
  padding: 27px;
  min-height: 205px;
}

.stat-top {
  margin-bottom: 20px;
}

.stat-icon {
  width: 58px;
  height: 58px;
  border-radius: 15px;
  display: grid;
  place-items: center;
}

.stat-icon.teal {
  background: #104e49;
  color: #5eead4;
}

.stat-icon.blue {
  background: #1e3a60;
  color: #60a5fa;
}

.stat-icon.purple {
  background: #422d62;
  color: #c4b5fd;
}

.stat-icon.orange {
  background: #603d20;
  color: #fdba74;
}

.stat-card p {
  color: #a8b7ca;
  margin-bottom: 10px;
}

.stat-card h2 {
  font-size: 27px;
  margin-bottom: 13px;
}

.stat-card small {
  color: #71839b;
  font-size: 12px;
}

.panel {
  padding: 29px;
  margin-bottom: 28px;
  min-width: 0;
}

.panel-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 27px;
  gap: 15px;
}

.panel-header h2 {
  font-size: 21px;
  margin-bottom: 8px;
}

.teal-icon {
  color: #5eead4;
}

.warehouse-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 20px;
}

.warehouse-card {
  padding: 23px;
  background: #0b1727;
  border: 1px solid #293b52;
  border-radius: 13px;
}

.warehouse-card-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.warehouse-symbol {
  width: 45px;
  height: 45px;
  display: grid;
  place-items: center;
  color: #5eead4;
  background: #104e49;
  border-radius: 11px;
}

.warehouse-code {
  color: #5eead4;
  font-size: 12px;
  font-weight: 700;
}

.warehouse-card h3 {
  font-size: 15px;
  margin-bottom: 12px;
}

.warehouse-location {
  display: flex;
  align-items: center;
  gap: 6px;
  color: #8294aa;
  font-size: 12px;
}

.warehouse-stock {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 26px 0 13px;
}

.warehouse-stock strong {
  font-size: 20px;
}

.warehouse-stock span {
  color: #8294aa;
  font-size: 11px;
}

.progress-track {
  height: 8px;
  background: #26364b;
  border-radius: 10px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  border-radius: 10px;
}

.progress-fill.teal {
  background: #2dd4bf;
}

.progress-fill.blue {
  background: #60a5fa;
}

.progress-fill.purple {
  background: #a78bfa;
}

.chart-legend {
  display: flex;
  justify-content: flex-end;
  gap: 22px;
  color: #a8b7ca;
  font-size: 13px;
  margin-bottom: 20px;
}

.chart-legend span {
  display: flex;
  align-items: center;
  gap: 8px;
}

.chart-legend i {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}

.legend-in {
  background: #2dd4bf;
}

.legend-out {
  background: #60a5fa;
}

.movement-chart {
  height: 210px;
  display: flex;
  align-items: flex-end;
  justify-content: space-around;
  border-bottom: 1px solid #34465d;
  padding: 0 15px;
  gap: 15px;
}

.chart-column {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: center;
  gap: 12px;
  flex: 1;
  color: #8294aa;
  font-size: 12px;
}

.bar-group {
  height: 170px;
  display: flex;
  align-items: flex-end;
  gap: 7px;
}

.bar {
  width: 22px;
  min-height: 0;
  border-radius: 5px 5px 0 0;
}

.bar-in {
  background: #2dd4bf;
}

.bar-out {
  background: #60a5fa;
}

.table-wrapper {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
  white-space: nowrap;
}

th {
  color: #8294aa;
  font-size: 12px;
  padding: 15px 13px;
  border-bottom: 1px solid #293b52;
}

td {
  padding: 17px 13px;
  border-bottom: 1px solid #233247;
  color: #b8c5d6;
  font-size: 13px;
}

.product-name {
  color: #e2e8f0;
  font-weight: 600;
}

.status-badge {
  color: #5eead4;
  background: #104e49;
  padding: 6px 10px;
  border-radius: 20px;
  font-size: 11px;
  font-weight: 600;
}

.transaction-type {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  color: #5eead4;
}

.quantity-in {
  color: #5eead4;
  font-weight: 600;
}

.dashboard-footer {
  display: flex;
  justify-content: space-between;
  color: #71839b;
  font-size: 12px;
  padding: 5px 0 20px;
}

@media (max-width: 1200px) {
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .warehouse-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 650px) {
  .warehouse-dashboard {
    padding: 24px 18px;
  }

  .page-header {
    flex-direction: column;
    align-items: flex-start;
  }

  .page-header h1 {
    font-size: 26px;
  }

  .stats-grid {
    grid-template-columns: 1fr;
    gap: 16px;
  }

  .panel {
    padding: 20px;
  }

  .dashboard-footer {
    flex-direction: column;
    gap: 8px;
  }
}
</style>
