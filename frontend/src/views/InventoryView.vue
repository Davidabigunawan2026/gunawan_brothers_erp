
<script setup>
import {
  Package,
  Boxes,
  Warehouse,
  AlertTriangle,
  Search,
  ArrowDownToLine,
  ArrowUpFromLine,
  MoreHorizontal
} from 'lucide-vue-next'

import { ref, computed } from 'vue'

const searchQuery = ref('')

const stockItems = ref([
  {
    id: 1,
    code: 'RM001',
    name: 'Steel Plate',
    category: 'Raw Material',
    warehouse: 'WH001',
    quantity: 100,
    unit: 'PCS',
    minStock: 10,
    status: 'In Stock'
  },
  {
    id: 2,
    code: 'RM002',
    name: 'Aluminium Sheet',
    category: 'Raw Material',
    warehouse: 'WH001',
    quantity: 80,
    unit: 'PCS',
    minStock: 20,
    status: 'In Stock'
  },
  {
    id: 3,
    code: 'FG001',
    name: 'Finished Product A',
    category: 'Finished Goods',
    warehouse: 'WH001',
    quantity: 25,
    unit: 'PCS',
    minStock: 5,
    status: 'In Stock'
  },
  {
    id: 4,
    code: 'SP001',
    name: 'Bearing 6205',
    category: 'Spare Part',
    warehouse: 'WH001',
    quantity: 50,
    unit: 'PCS',
    minStock: 3,
    status: 'In Stock'
  }
])

const filteredItems = computed(() => {
  const keyword = searchQuery.value.toLowerCase()

  return stockItems.value.filter(item =>
    item.code.toLowerCase().includes(keyword) ||
    item.name.toLowerCase().includes(keyword)
  )
})

const totalStock = computed(() =>
  stockItems.value.reduce((total, item) => total + item.quantity, 0)
)
</script>

<template>
  <div class="inventory-page">

    <!-- Page Header -->
    <div class="page-header">
      <div>
        <h1>Inventory Overview</h1>
        <p>Manage and monitor your inventory stock</p>
      </div>

      <div class="header-actions">
        <button class="btn btn-outline">
          <ArrowDownToLine :size="17" />
          Export
        </button>

        <button class="btn btn-primary">
          <ArrowUpFromLine :size="17" />
          Stock In
        </button>
      </div>
    </div>

    <!-- Summary Cards -->
    <div class="summary-grid">

      <div class="summary-card">
        <div class="card-icon teal">
          <Package :size="22" />
        </div>
        <div class="card-info">
          <span>Total Products</span>
          <h2>{{ stockItems.length }}</h2>
          <small>Registered products</small>
        </div>
      </div>

      <div class="summary-card">
        <div class="card-icon blue">
          <Boxes :size="22" />
        </div>
        <div class="card-info">
          <span>Total Stock</span>
          <h2>{{ totalStock.toLocaleString() }}</h2>
          <small>Total quantity in PCS</small>
        </div>
      </div>

      <div class="summary-card">
        <div class="card-icon purple">
          <Warehouse :size="22" />
        </div>
        <div class="card-info">
          <span>Warehouses</span>
          <h2>3</h2>
          <small>Registered warehouses</small>
        </div>
      </div>

      <div class="summary-card">
        <div class="card-icon orange">
          <AlertTriangle :size="22" />
        </div>
        <div class="card-info">
          <span>Low Stock</span>
          <h2>0</h2>
          <small>Products below minimum</small>
        </div>
      </div>

    </div>

    <!-- Stock Table -->
    <section class="stock-section">

      <div class="section-header">
        <div>
          <h2>Stock Overview</h2>
          <p>Current inventory balances</p>
        </div>

        <div class="search-box">
          <Search :size="17" />
          <input
            v-model="searchQuery"
            type="text"
            placeholder="Search product..."
          />
        </div>
      </div>

      <div class="table-wrapper">
        <table>
          <thead>
            <tr>
              <th>Product Code</th>
              <th>Product Name</th>
              <th>Category</th>
              <th>Warehouse</th>
              <th>Quantity</th>
              <th>Min. Stock</th>
              <th>Status</th>
              <th></th>
            </tr>
          </thead>

          <tbody>
            <tr v-for="item in filteredItems" :key="item.id">
              <td class="product-code">{{ item.code }}</td>
              <td class="product-name">{{ item.name }}</td>
              <td>{{ item.category }}</td>
              <td>{{ item.warehouse }}</td>
              <td class="quantity">
                {{ item.quantity }} {{ item.unit }}
              </td>
              <td>{{ item.minStock }} {{ item.unit }}</td>
              <td>
                <span class="status-badge">
                  {{ item.status }}
                </span>
              </td>
              <td>
                <button class="more-btn" title="More options">
                  <MoreHorizontal :size="19" />
                </button>
              </td>
            </tr>

            <tr v-if="filteredItems.length === 0">
              <td colspan="8" class="empty-state">
                No products found.
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <div class="table-footer">
        Showing {{ filteredItems.length }} of {{ stockItems.length }} products
      </div>

    </section>

  </div>
</template>

<style scoped>
.inventory-page {
  color: #e2e8f0;
  padding: 28px;
  min-height: 100%;
}

.page-header,
.section-header,
.header-actions {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
}

.page-header {
  margin-bottom: 28px;
}

.page-header h1 {
  font-size: 25px;
  margin: 0 0 7px;
  color: #f8fafc;
}

.page-header p,
.section-header p {
  margin: 0;
  color: #94a3b8;
  font-size: 13px;
}

.header-actions {
  justify-content: flex-end;
}

.btn {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 10px 15px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 13px;
  font-weight: 600;
}

.btn-outline {
  background: #17263a;
  border: 1px solid #334155;
  color: #cbd5e1;
}

.btn-primary {
  background: #14b8a6;
  border: 1px solid #14b8a6;
  color: #062b2a;
}

.summary-grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 18px;
  margin-bottom: 28px;
}

.summary-card {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 21px;
  background: #111e30;
  border: 1px solid #26364b;
  border-radius: 12px;
}

.card-icon {
  width: 46px;
  height: 46px;
  display: grid;
  place-items: center;
  border-radius: 10px;
}

.teal {
  color: #5eead4;
  background: #134e4a;
}

.blue {
  color: #60a5fa;
  background: #1e3a5f;
}

.purple {
  color: #c4b5fd;
  background: #3b2d61;
}

.orange {
  color: #fdba74;
  background: #633d24;
}

.card-info span {
  color: #94a3b8;
  font-size: 12px;
}

.card-info h2 {
  font-size: 25px;
  color: #f8fafc;
  margin: 5px 0;
}

.card-info small {
  color: #64748b;
  font-size: 11px;
}

.stock-section {
  background: #111e30;
  border: 1px solid #26364b;
  border-radius: 12px;
  overflow: hidden;
}

.section-header {
  padding: 22px;
}

.section-header h2 {
  margin: 0 0 6px;
  font-size: 17px;
  color: #f8fafc;
}

.search-box {
  display: flex;
  align-items: center;
  gap: 9px;
  background: #0b1422;
  border: 1px solid #334155;
  border-radius: 8px;
  padding: 9px 12px;
  color: #94a3b8;
}

.search-box input {
  background: transparent;
  border: none;
  outline: none;
  color: #e2e8f0;
  width: 180px;
}

.search-box input::placeholder {
  color: #64748b;
}

.table-wrapper {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
  white-space: nowrap;
}

th {
  background: #17263a;
  color: #94a3b8;
  font-size: 11px;
  font-weight: 600;
  text-align: left;
  padding: 14px 18px;
}

td {
  padding: 16px 18px;
  border-bottom: 1px solid #26364b;
  color: #cbd5e1;
  font-size: 12px;
}

.product-code {
  color: #5eead4;
  font-weight: 600;
}

.product-name {
  color: #f1f5f9;
  font-weight: 600;
}

.quantity {
  color: #5eead4;
  font-weight: 600;
}

.status-badge {
  background: #123e37;
  color: #5eead4;
  padding: 5px 9px;
  border-radius: 20px;
  font-size: 10px;
}

.more-btn {
  display: grid;
  place-items: center;
  border: none;
  background: transparent;
  color: #94a3b8;
  cursor: pointer;
}

.empty-state {
  text-align: center;
  color: #94a3b8;
  padding: 30px;
}

.table-footer {
  padding: 15px 20px;
  color: #64748b;
  font-size: 11px;
}

@media (max-width: 1100px) {
  .summary-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (max-width: 650px) {
  .inventory-page {
    padding: 16px;
  }

  .page-header {
    align-items: flex-start;
    flex-direction: column;
  }

  .summary-grid {
    grid-template-columns: 1fr;
  }

  .section-header {
    align-items: flex-start;
    flex-direction: column;
  }

  .search-box,
  .search-box input {
    width: 100%;
  }
}
</style>
