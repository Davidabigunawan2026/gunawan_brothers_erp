
<script setup>
import { ref } from 'vue'

import Sidebar from './components/Sidebar.vue'
import InventoryView from './views/InventoryView.vue'
import ExecutiveDashboard from './views/ExecutiveDashboard.vue'
import AdminDashboard from './views/AdminDashboard.vue'
import WarehouseDashboard from './views/WarehouseDashboard.vue'
import SalesDashboard from './views/SalesDashboard.vue'
import PurchaseDashboard from './views/purchaseDashboard.vue'

const selectedPage = ref('Inventory')


function navigateTo(page) {
  const allowedPages = [
    'Executive Dashboard',
    'Administration Dashboard',
    'Warehouse Dashboard',
    'Sales Dashboard',
    'Purchasing Dashboard',
    'Inventory'
  ]

  if (allowedPages.includes(page)) {
    selectedPage.value = page
  }
}



</script>

<template>
  <div class="app-layout">
    <Sidebar @navigate="navigateTo" />

    <main class="main-content">
      <header class="top-navbar">
        <div class="breadcrumb">
          Gunawan Brothers
          <span>/</span>
          {{ selectedPage }}
        </div>

        <div class="user-profile">
          <span class="user-name">Administrator</span>
          <div class="user-avatar">GB</div>
        </div>
      </header>



      <ExecutiveDashboard
        v-if="selectedPage === 'Executive Dashboard'"
      />

      <AdminDashboard
        v-else-if="selectedPage === 'Administration Dashboard'"
      />

      <WarehouseDashboard
        v-else-if="selectedPage === 'Warehouse Dashboard'"
      />

      <SalesDashboard
        v-else-if="selectedPage === 'Sales Dashboard'"
      />

      <PurchaseDashboard
        v-else-if="selectedPage === 'Purchasing Dashboard'"
      />

      <InventoryView
        v-else-if="selectedPage === 'Inventory'"
      />



    </main>
  </div>
</template>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #0b1422;
}

.app-layout {
  display: flex;
  min-height: 100vh;
  background: #0b1422;
}

.main-content {
  flex: 1;
  min-width: 0;
}

.top-navbar {
  height: 68px;
  padding: 0 28px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #111e30;
  border-bottom: 1px solid #26364b;
}

.breadcrumb {
  color: #cbd5e1;
  font-size: 13px;
}

.breadcrumb span {
  color: #64748b;
  margin: 0 8px;
}

.user-profile {
  display: flex;
  align-items: center;
  gap: 12px;
}

.user-name {
  color: #cbd5e1;
  font-size: 12px;
}

.user-avatar {
  width: 34px;
  height: 34px;
  display: grid;
  place-items: center;
  border-radius: 50%;
  background: #134e4a;
  color: #5eead4;
  font-size: 12px;
  font-weight: bold;
}

@media (max-width: 650px) {
  .top-navbar {
    padding: 0 16px;
  }

  .user-name {
    display: none;
  }
}
</style>
