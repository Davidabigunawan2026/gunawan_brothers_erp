
<script setup>
import { ref } from 'vue'

import {
  LayoutDashboard,
  Package,
  ShoppingCart,
  Receipt,
  Users,
  ChartNoAxesCombined,
  Settings,
  Boxes,
  ChevronDown,
  List,
  ArrowDownToLine,
  ArrowUpFromLine,
  ArrowLeftRight,
  SlidersHorizontal,
  ClipboardList,
  Warehouse,
  BriefcaseBusiness
} from 'lucide-vue-next'

const dashboardOpen = ref(true)
const inventoryOpen = ref(true)
const emit = defineEmits(['navigate'])

const dashboardItems = [
  { name: 'Executive Dashboard', icon: LayoutDashboard },
  { name: 'Administration Dashboard', icon: ClipboardList },
  { name: 'Warehouse Dashboard', icon: Warehouse },
  { name: 'Sales Dashboard', icon: Receipt },
  { name: 'Purchasing Dashboard', icon: ShoppingCart }
]

const inventoryItems = [
  { name: 'Stock List', icon: List },
  { name: 'Stock In', icon: ArrowDownToLine },
  { name: 'Stock Out', icon: ArrowUpFromLine },
  { name: 'Stock Transfer', icon: ArrowLeftRight },
  { name: 'Stock Adjustment', icon: SlidersHorizontal }
]

const menuItems = [
  { name: 'Customers & Suppliers', icon: Users },
  { name: 'Reports', icon: ChartNoAxesCombined },
  { name: 'Settings', icon: Settings }
]
</script>

<template>
  <aside class="sidebar">

    <div class="brand">
      <Boxes :size="30" />
      <span>GUNAWAN BROTHERS</span>
    </div>

    <div class="menu-title">MAIN MENU</div>

    <nav>

      <!-- DASHBOARD MENU -->
      <div>
        <button
          class="menu-item menu-toggle"
          @click="dashboardOpen = !dashboardOpen"
        >
          <LayoutDashboard :size="20" />
          <span>Dashboard</span>

          <ChevronDown
            class="chevron"
            :class="{ rotated: dashboardOpen }"
            :size="16"
          />
        </button>


        <div v-if="dashboardOpen" class="submenu">

          <a
            v-for="item in dashboardItems"
            :key="item.name"
            href="#"
            class="submenu-item"
            @click.prevent="emit('navigate', item.name)"
          >
            <component :is="item.icon" :size="17" />
            <span>{{ item.name }}</span>
          </a>

        </div>
      </div>


      <!-- INVENTORY MENU -->
      <div>
        <button
          class="menu-item menu-toggle"

          @click="
            inventoryOpen = !inventoryOpen;
            emit('navigate', 'Inventory')
          "

        >
          <Package :size="20" />
          <span>Inventory</span>

          <ChevronDown
            class="chevron"
            :class="{ rotated: inventoryOpen }"
            :size="16"
          />
        </button>

        <div v-if="inventoryOpen" class="submenu">
          <a
            v-for="item in inventoryItems"
            :key="item.name"
            href="#"
            class="submenu-item"
          >
            <component :is="item.icon" :size="17" />
            <span>{{ item.name }}</span>
          </a>
        </div>
      </div>

      <!-- OTHER MENUS -->
      <a
        v-for="item in menuItems"
        :key="item.name"
        href="#"
        class="menu-item"
      >
        <component :is="item.icon" :size="20" />
        <span>{{ item.name }}</span>
      </a>

    </nav>

    <div class="sidebar-footer">
      Gunawan Brothers ERP v1.0
    </div>

  </aside>
</template>

<style scoped>
.sidebar {
  width: 250px;
  min-height: 100vh;
  background: #101d32;
  color: #cbd5e1;
  padding: 24px 16px;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
}

.brand {
  display: flex;
  align-items: center;
  gap: 12px;
  color: #5eead4;
  font-weight: 700;
  font-size: 15px;
  margin-bottom: 45px;
}

.menu-title {
  color: #64748b;
  font-size: 11px;
  font-weight: 700;
  margin-bottom: 15px;
  letter-spacing: 1.5px;
}

nav {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.menu-item {
  width: 100%;
  display: flex;
  align-items: center;
  gap: 13px;
  padding: 12px;
  border: none;
  border-radius: 8px;
  background: transparent;
  color: #94a3b8;
  text-decoration: none;
  font: inherit;
  font-size: 14px;
  text-align: left;
  cursor: pointer;
  transition: 0.2s;
}

.menu-item:hover,
.submenu-item:hover {
  background: #20344e;
  color: #5eead4;
}

.menu-toggle .chevron {
  margin-left: auto;
  transition: transform 0.2s;
}

.menu-toggle .chevron.rotated {
  transform: rotate(180deg);
}

.submenu {
  margin: 5px 0 8px 22px;
  padding-left: 14px;
  border-left: 1px solid #334155;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.submenu-item {
  display: flex;
  align-items: center;
  gap: 11px;
  padding: 10px;
  border-radius: 7px;
  color: #94a3b8;
  font-size: 13px;
  text-decoration: none;
  transition: 0.2s;
}

.sidebar-footer {
  margin-top: auto;
  padding-top: 25px;
  color: #64748b;
  font-size: 11px;
}
</style>
