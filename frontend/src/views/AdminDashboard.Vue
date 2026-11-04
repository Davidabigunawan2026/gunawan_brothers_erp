
<script setup>
import { ref, computed } from 'vue'

import {
  Users,
  UserCheck,
  ClipboardCheck,
  CalendarCheck,
  Search,
  ShieldCheck,
  Clock3,
  CircleCheck,
  AlertCircle,
  Activity,
  UserPlus,
  FileText
} from 'lucide-vue-next'

const searchQuery = ref('')

const stats = [
  {
    title: 'Total Employees',
    value: '128',
    change: '+8.5%',
    description: 'Compared with previous period',
    icon: Users,
    color: 'teal'
  },
  {
    title: 'Active Users',
    value: '96',
    change: '+5.2%',
    description: 'ERP users currently active',
    icon: UserCheck,
    color: 'blue'
  },
  {
    title: 'Pending Approvals',
    value: '12',
    change: 'Needs attention',
    description: 'Waiting for administrator',
    icon: ClipboardCheck,
    color: 'purple'
  },
  {
    title: 'Attendance Today',
    value: '112',
    change: '87.5%',
    description: 'Employee attendance rate',
    icon: CalendarCheck,
    color: 'orange'
  }
]

const employees = ref([
  {
    id: 'EMP001',
    name: 'Andi Wijaya',
    department: 'Administration',
    position: 'Admin Officer',
    status: 'Active'
  },
  {
    id: 'EMP002',
    name: 'Budi Santoso',
    department: 'Warehouse',
    position: 'Warehouse Staff',
    status: 'Active'
  },
  {
    id: 'EMP003',
    name: 'Citra Lestari',
    department: 'Finance',
    position: 'Finance Officer',
    status: 'Active'
  },
  {
    id: 'EMP004',
    name: 'Dedi Pratama',
    department: 'Sales',
    position: 'Sales Staff',
    status: 'Inactive'
  },
  {
    id: 'EMP005',
    name: 'Eka Saputra',
    department: 'Purchasing',
    position: 'Purchasing Staff',
    status: 'Active'
  }
])

const filteredEmployees = computed(() => {
  const keyword = searchQuery.value.toLowerCase()

  return employees.value.filter(employee =>
    employee.name.toLowerCase().includes(keyword) ||
    employee.id.toLowerCase().includes(keyword) ||
    employee.department.toLowerCase().includes(keyword)
  )
})

const approvals = [
  {
    number: 'APR-001',
    title: 'New Employee Registration',
    requester: 'HR Department',
    date: '02 Nov 2026',
    type: 'Employee'
  },
  {
    number: 'APR-002',
    title: 'User Access Permission',
    requester: 'IT Department',
    date: '02 Nov 2026',
    type: 'Access'
  },
  {
    number: 'APR-003',
    title: 'Employee Leave Request',
    requester: 'Sales Department',
    date: '01 Nov 2026',
    type: 'Leave'
  }
]

const activities = [
  {
    title: 'New employee registered',
    detail: 'Andi Wijaya added to Administration',
    time: '09:30 AM',
    icon: UserPlus,
    color: 'teal'
  },
  {
    title: 'User access updated',
    detail: 'Warehouse user permissions changed',
    time: '10:15 AM',
    icon: ShieldCheck,
    color: 'blue'
  },
  {
    title: 'Document submitted',
    detail: 'Employee registration form submitted',
    time: '11:20 AM',
    icon: FileText,
    color: 'purple'
  }
]
</script>

<template>
  <div class="admin-dashboard">

    <!-- Page Header -->
    <section class="page-header">
      <div>
        <h1>Administration Dashboard</h1>
        <p>Company administration and employee overview</p>
      </div>

      <div class="header-actions">
        <span class="date-label">
          <CalendarCheck :size="17" />
          02 November 2026
        </span>
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

          <span class="stat-change">
            {{ stat.change }}
          </span>
        </div>

        <p class="stat-title">{{ stat.title }}</p>
        <h2>{{ stat.value }}</h2>
        <small>{{ stat.description }}</small>
      </div>
    </section>

    <!-- Main Content -->
    <section class="content-grid">

      <!-- Employee Management -->
      <div class="panel employee-panel">
        <div class="panel-header">
          <div>
            <h2>Employee Management</h2>
            <p>Employee directory and account status</p>
          </div>

          <button class="primary-btn">
            <UserPlus :size="17" />
            Add Employee
          </button>
        </div>

        <div class="search-box">
          <Search :size="18" />
          <input
            v-model="searchQuery"
            type="text"
            placeholder="Search employee, ID or department..."
          />
        </div>

        <div class="table-wrapper">
          <table>
            <thead>
              <tr>
                <th>Employee</th>
                <th>Department</th>
                <th>Position</th>
                <th>Status</th>
              </tr>
            </thead>

            <tbody>
              <tr
                v-for="employee in filteredEmployees"
                :key="employee.id"
              >
                <td>
                  <div class="employee-info">
                    <div class="employee-avatar">
                      {{ employee.name.charAt(0) }}
                    </div>

                    <div>
                      <strong>{{ employee.name }}</strong>
                      <small>{{ employee.id }}</small>
                    </div>
                  </div>
                </td>

                <td>{{ employee.department }}</td>
                <td>{{ employee.position }}</td>

                <td>
                  <span
                    :class="[
                      'status-badge',
                      employee.status.toLowerCase()
                    ]"
                  >
                    {{ employee.status }}
                  </span>
                </td>
              </tr>

              <tr v-if="filteredEmployees.length === 0">
                <td colspan="4" class="empty-state">
                  No employees found.
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>

      <!-- Pending Approvals -->
      <div class="panel approval-panel">
        <div class="panel-header">
          <div>
            <h2>Pending Approvals</h2>
            <p>Requests awaiting review</p>
          </div>

          <span class="approval-count">
            {{ approvals.length }}
          </span>
        </div>

        <div class="approval-list">
          <div
            v-for="approval in approvals"
            :key="approval.number"
            class="approval-item"
          >
            <div class="approval-icon">
              <AlertCircle :size="19" />
            </div>

            <div class="approval-info">
              <strong>{{ approval.title }}</strong>
              <small>{{ approval.number }} · {{ approval.type }}</small>
              <small>{{ approval.requester }}</small>
            </div>

            <span class="approval-date">
              {{ approval.date }}
            </span>
          </div>
        </div>

        <button class="view-all-btn">
          View All Approvals
        </button>
      </div>

    </section>

    <!-- Bottom Section -->
    <section class="bottom-grid">

      <!-- Recent Activities -->
      <div class="panel activity-panel">
        <div class="panel-header">
          <div>
            <h2>Recent Activities</h2>
            <p>Latest administration activities</p>
          </div>

          <Activity :size="21" class="muted-icon" />
        </div>

        <div class="activity-list">
          <div
            v-for="activity in activities"
            :key="activity.title"
            class="activity-item"
          >
            <div :class="['activity-icon', activity.color]">
              <component :is="activity.icon" :size="18" />
            </div>

            <div class="activity-info">
              <strong>{{ activity.title }}</strong>
              <small>{{ activity.detail }}</small>
            </div>

            <span class="activity-time">
              {{ activity.time }}
            </span>
          </div>
        </div>
      </div>

      <!-- System Overview -->
      <div class="panel system-panel">
        <div class="panel-header">
          <div>
            <h2>System Overview</h2>
            <p>ERP account and system status</p>
          </div>

          <ShieldCheck :size="22" class="system-icon" />
        </div>

        <div class="system-row">
          <div class="system-label">
            <UserCheck :size="18" />
            <span>Active Accounts</span>
          </div>
          <strong>96 / 128</strong>
        </div>

        <div class="progress-track">
          <div class="progress-fill accounts"></div>
        </div>

        <div class="system-row">
          <div class="system-label">
            <CircleCheck :size="18" />
            <span>System Status</span>
          </div>
          <span class="system-online">Operational</span>
        </div>

        <div class="system-row">
          <div class="system-label">
            <Clock3 :size="18" />
            <span>Last System Update</span>
          </div>
          <strong>Today, 08:00</strong>
        </div>

      </div>

    </section>

    <footer class="dashboard-footer">
      Gunawan Brothers ERP
      <span>Administration Module</span>
    </footer>

  </div>
</template>

<style scoped>
.admin-dashboard {
  padding: 38px 46px;
  color: #e2e8f0;
  min-height: 100%;
}

.page-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 38px;
  gap: 20px;
}

.page-header h1 {
  font-size: 34px;
  margin-bottom: 10px;
  font-weight: 700;
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
  margin-bottom: 36px;
}

.stat-card,
.panel {
  background: #111f32;
  border: 1px solid #26364b;
  border-radius: 18px;
}

.stat-card {
  padding: 30px;
  min-height: 225px;
}

.stat-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 26px;
}

.stat-icon {
  width: 62px;
  height: 62px;
  border-radius: 16px;
  display: flex;
  justify-content: center;
  align-items: center;
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

.stat-change {
  color: #5eead4;
  font-size: 13px;
  font-weight: 600;
}

.stat-title {
  color: #a8b7ca;
  font-size: 15px;
  margin-bottom: 12px;
}

.stat-card h2 {
  font-size: 29px;
  margin-bottom: 18px;
}

.stat-card small {
  color: #71839b;
  font-size: 12px;
}

.content-grid {
  display: grid;
  grid-template-columns: 1.65fr 1fr;
  gap: 28px;
  margin-bottom: 28px;
}

.panel {
  padding: 30px;
  min-width: 0;
}

.panel-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 15px;
  margin-bottom: 27px;
}

.panel-header h2 {
  font-size: 21px;
  margin-bottom: 8px;
}

.primary-btn {
  display: flex;
  align-items: center;
  gap: 9px;
  padding: 12px 16px;
  background: #0f766e;
  color: white;
  border: none;
  border-radius: 9px;
  font-weight: 600;
  cursor: pointer;
}

.primary-btn:hover {
  background: #0d9488;
}

.search-box {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 13px 16px;
  background: #0b1727;
  border: 1px solid #293b52;
  border-radius: 9px;
  color: #8294aa;
  margin-bottom: 22px;
}

.search-box input {
  width: 100%;
  background: transparent;
  border: none;
  outline: none;
  color: #e2e8f0;
  font-size: 14px;
}

.search-box input::placeholder {
  color: #71839b;
}

.table-wrapper {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
  white-space: nowrap;
  text-align: left;
}

th {
  color: #8294aa;
  font-size: 12px;
  font-weight: 600;
  padding: 15px 12px;
  border-bottom: 1px solid #293b52;
}

td {
  padding: 17px 12px;
  border-bottom: 1px solid #233247;
  color: #b8c5d6;
  font-size: 13px;
}

.employee-info {
  display: flex;
  align-items: center;
  gap: 12px;
}

.employee-avatar {
  width: 37px;
  height: 37px;
  background: #164e63;
  color: #5eead4;
  border-radius: 10px;
  display: grid;
  place-items: center;
  font-weight: 700;
}

.employee-info strong,
.employee-info small {
  display: block;
}

.employee-info strong {
  color: #e2e8f0;
  margin-bottom: 4px;
}

.employee-info small {
  color: #71839b;
  font-size: 11px;
}

.status-badge {
  padding: 6px 10px;
  border-radius: 20px;
  font-size: 11px;
  font-weight: 600;
}

.status-badge.active {
  color: #5eead4;
  background: #104e49;
}

.status-badge.inactive {
  color: #fca5a5;
  background: #512c36;
}

.empty-state {
  text-align: center;
  padding: 30px;
  color: #94a3b8;
}

.approval-count {
  background: #513b25;
  color: #fdba74;
  border-radius: 9px;
  padding: 8px 13px;
  font-weight: 700;
}

.approval-item {
  display: flex;
  align-items: flex-start;
  gap: 13px;
  padding: 19px 0;
  border-bottom: 1px solid #293b52;
}

.approval-icon {
  color: #fdba74;
  background: #49351f;
  padding: 10px;
  border-radius: 10px;
}

.approval-info {
  flex: 1;
  min-width: 0;
}

.approval-info strong,
.approval-info small {
  display: block;
}

.approval-info strong {
  font-size: 13px;
  margin-bottom: 7px;
}

.approval-info small {
  color: #8294aa;
  font-size: 11px;
  margin-bottom: 5px;
}

.approval-date {
  color: #71839b;
  font-size: 10px;
  white-space: nowrap;
}

.view-all-btn {
  width: 100%;
  margin-top: 22px;
  padding: 12px;
  border: 1px solid #0f766e;
  border-radius: 9px;
  background: transparent;
  color: #5eead4;
  cursor: pointer;
}

.view-all-btn:hover {
  background: #104e49;
}

.bottom-grid {
  display: grid;
  grid-template-columns: 1.5fr 1fr;
  gap: 28px;
}

.activity-item {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 16px 0;
  border-bottom: 1px solid #293b52;
}

.activity-icon {
  padding: 11px;
  border-radius: 10px;
}

.activity-icon.teal {
  background: #104e49;
  color: #5eead4;
}

.activity-icon.blue {
  background: #1e3a60;
  color: #60a5fa;
}

.activity-icon.purple {
  background: #422d62;
  color: #c4b5fd;
}

.activity-info {
  flex: 1;
}

.activity-info strong,
.activity-info small {
  display: block;
}

.activity-info strong {
  font-size: 13px;
  margin-bottom: 6px;
}

.activity-info small {
  color: #8294aa;
  font-size: 12px;
}

.activity-time {
  color: #71839b;
  font-size: 11px;
  white-space: nowrap;
}

.muted-icon {
  color: #5eead4;
}

.system-icon {
  color: #5eead4;
}

.system-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  margin: 22px 0 14px;
  font-size: 13px;
}

.system-label {
  display: flex;
  align-items: center;
  gap: 10px;
  color: #a8b7ca;
}

.system-label svg {
  color: #5eead4;
}

.system-row strong {
  color: #e2e8f0;
}

.progress-track {
  height: 9px;
  border-radius: 10px;
  background: #26364b;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  width: 75%;
  background: #2dd4bf;
  border-radius: 10px;
}

.system-online {
  color: #5eead4;
  background: #104e49;
  padding: 6px 10px;
  border-radius: 20px;
  font-size: 11px;
}

.dashboard-footer {
  display: flex;
  justify-content: space-between;
  color: #71839b;
  font-size: 12px;
  padding: 30px 0 10px;
}

@media (max-width: 1200px) {
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .content-grid,
  .bottom-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 650px) {
  .admin-dashboard {
    padding: 24px 18px;
  }

  .page-header {
    align-items: flex-start;
    flex-direction: column;
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

  .panel-header {
    align-items: flex-start;
    flex-wrap: wrap;
  }

  .dashboard-footer {
    flex-direction: column;
    gap: 8px;
  }
}
</style>
