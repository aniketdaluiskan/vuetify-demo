<template>
  <v-app>
    <v-app-bar color="primary" density="comfortable">
      <v-app-bar-nav-icon
        aria-label="Toggle navigation menu"
        @click="drawer = !drawer"
      />
      <v-toolbar-title>Vuetify UI Demo</v-toolbar-title>
      <v-spacer />
      <v-btn variant="text" aria-label="Go to dashboard">Dashboard</v-btn>
      <v-btn variant="text" aria-label="Go to reports">Reports</v-btn>
      <v-btn variant="text" aria-label="Go to settings">Settings</v-btn>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" temporary aria-label="Primary navigation">
      <v-list nav density="compact">
        <v-list-item title="Dashboard" prepend-icon="mdi-view-dashboard" @click="drawer = false" />
        <v-list-item title="Reports" prepend-icon="mdi-chart-bar" @click="drawer = false" />
        <v-list-item title="Settings" prepend-icon="mdi-cog" @click="drawer = false" />
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <v-container class="py-8" style="max-width: 1100px">
        <h1 class="text-h4 mb-1">Component Showcase</h1>
        <p class="text-body-2 text-medium-emphasis mb-6">
          A single-page reference of common Vuetify inputs, navigation, and data
          display components, wired up with sample state for interaction testing.
        </p>

        <!-- Alerts -->
        <v-alert
          v-if="showInfoAlert"
          type="info"
          variant="tonal"
          closable
          class="mb-6"
          title="Heads up"
          text="This demo page is for exercising UI components and does not submit data anywhere."
          @click:close="showInfoAlert = false"
        />

        <!-- Section: Form Controls -->
        <v-card class="mb-6" elevation="2">
          <v-card-title class="text-h6">Form Controls</v-card-title>
          <v-card-subtitle>Text input, selection, and toggle components</v-card-subtitle>
          <v-card-text>
            <v-form @submit.prevent="onFormSubmit">
              <v-row>
                <v-col cols="12" md="6">
                  <v-text-field
                    v-model="form.fullName"
                    label="Full name"
                    placeholder="Jordan Rivera"
                    prepend-inner-icon="mdi-account"
                    variant="outlined"
                    density="comfortable"
                    :rules="[rules.required]"
                    clearable
                  />
                </v-col>
                <v-col cols="12" md="6">
                  <v-text-field
                    v-model="form.email"
                    label="Email address"
                    type="email"
                    placeholder="jordan.rivera@example.com"
                    prepend-inner-icon="mdi-email"
                    variant="outlined"
                    density="comfortable"
                    :rules="[rules.required, rules.email]"
                    clearable
                  />
                </v-col>
                <v-col cols="12" md="6">
                  <v-select
                    v-model="form.department"
                    :items="departments"
                    label="Department"
                    prepend-inner-icon="mdi-office-building"
                    variant="outlined"
                    density="comfortable"
                  />
                </v-col>
                <v-col cols="12" md="6">
                  <v-slider
                    v-model="form.priority"
                    label="Priority level"
                    :min="1"
                    :max="5"
                    :step="1"
                    thumb-label="always"
                    show-ticks="always"
                  />
                </v-col>
                <v-col cols="12" md="6">
                  <fieldset class="pa-0" style="border: none">
                    <legend class="text-body-2 mb-2">Contact preference</legend>
                    <v-radio-group v-model="form.contactMethod" inline hide-details>
                      <v-radio label="Email" value="email" />
                      <v-radio label="Phone" value="phone" />
                      <v-radio label="No contact" value="none" />
                    </v-radio-group>
                  </fieldset>
                </v-col>
                <v-col cols="12" md="6">
                  <v-checkbox
                    v-model="form.subscribeUpdates"
                    label="Subscribe to product update emails"
                    hide-details
                  />
                  <v-switch
                    v-model="form.enableNotifications"
                    label="Enable desktop notifications"
                    color="primary"
                    hide-details
                  />
                </v-col>
              </v-row>

              <v-card-actions class="px-0">
                <v-btn color="primary" type="submit" variant="elevated">
                  Submit form
                </v-btn>
                <v-btn variant="text" @click="onFormReset">Reset</v-btn>
              </v-card-actions>
            </v-form>
          </v-card-text>
        </v-card>

        <!-- Section: Buttons, Dialog, Menu -->
        <v-card class="mb-6" elevation="2">
          <v-card-title class="text-h6">Buttons, Dialog &amp; Menu</v-card-title>
          <v-card-subtitle>Action triggers, modal dialog, and dropdown menu</v-card-subtitle>
          <v-card-text>
            <div class="d-flex flex-wrap ga-3 mb-4">
              <v-btn color="primary" variant="elevated">Primary</v-btn>
              <v-btn color="secondary" variant="outlined">Secondary</v-btn>
              <v-btn color="success" variant="tonal">Success</v-btn>
              <v-btn color="error" variant="text">Error text</v-btn>
              <v-btn icon="mdi-heart" aria-label="Add to favorites" variant="plain" />
            </div>

            <div class="d-flex flex-wrap ga-3">
              <v-btn variant="outlined" @click="dialogOpen = true">
                Open confirmation dialog
              </v-btn>

              <v-menu>
                <template #activator="{ props: menuProps }">
                  <v-btn variant="outlined" v-bind="menuProps">
                    Open actions menu
                  </v-btn>
                </template>
                <v-list>
                  <v-list-item title="Edit" prepend-icon="mdi-pencil" @click="showSnackbar('Edit selected')" />
                  <v-list-item title="Duplicate" prepend-icon="mdi-content-copy" @click="showSnackbar('Duplicate selected')" />
                  <v-list-item title="Archive" prepend-icon="mdi-archive" @click="showSnackbar('Archive selected')" />
                  <v-divider />
                  <v-list-item title="Delete" prepend-icon="mdi-delete" @click="showSnackbar('Delete selected')" />
                </v-list>
              </v-menu>

              <v-btn variant="outlined" @click="showSnackbar('Sample action completed')">
                Trigger snackbar
              </v-btn>
            </div>

            <v-dialog v-model="dialogOpen" max-width="440" role="alertdialog">
              <v-card>
                <v-card-title class="text-h6">Confirm action</v-card-title>
                <v-card-text>
                  Are you sure you want to proceed with this action? This is a
                  sample modal dialog for UI testing purposes only.
                </v-card-text>
                <v-card-actions>
                  <v-spacer />
                  <v-btn variant="text" @click="dialogOpen = false">Cancel</v-btn>
                  <v-btn
                    color="primary"
                    variant="elevated"
                    @click="confirmDialog"
                  >
                    Confirm
                  </v-btn>
                </v-card-actions>
              </v-card>
            </v-dialog>
          </v-card-text>
        </v-card>

        <!-- Section: Tabs -->
        <v-card class="mb-6" elevation="2">
          <v-card-title class="text-h6">Tabs</v-card-title>
          <v-card-subtitle>Tabbed navigation with panel content</v-card-subtitle>
          <v-tabs v-model="activeTab" color="primary" align-tabs="start">
            <v-tab value="overview">Overview</v-tab>
            <v-tab value="activity">Activity</v-tab>
            <v-tab value="team">Team</v-tab>
          </v-tabs>
          <v-divider />
          <v-window v-model="activeTab">
            <v-window-item value="overview">
              <v-card-text>
                <p>
                  This project tracks quarterly onboarding metrics across three
                  regional teams and surfaces flagged accounts for review.
                </p>
              </v-card-text>
            </v-window-item>
            <v-window-item value="activity">
              <v-card-text>
                <v-list density="compact">
                  <v-list-item title="Report generated" subtitle="2 hours ago" prepend-icon="mdi-file-document" />
                  <v-list-item title="Account flagged for review" subtitle="Yesterday" prepend-icon="mdi-flag" />
                  <v-list-item title="Weekly summary sent" subtitle="3 days ago" prepend-icon="mdi-email-send" />
                </v-list>
              </v-card-text>
            </v-window-item>
            <v-window-item value="team">
              <v-card-text>
                <v-row>
                  <v-col v-for="member in teamMembers" :key="member.id" cols="12" sm="4">
                    <v-card variant="outlined">
                      <v-card-item>
                        <template #prepend>
                          <v-avatar color="primary" size="40">
                            <span class="text-body-2">{{ member.initials }}</span>
                          </v-avatar>
                        </template>
                        <v-card-title class="text-body-1">{{ member.name }}</v-card-title>
                        <v-card-subtitle>{{ member.role }}</v-card-subtitle>
                      </v-card-item>
                    </v-card>
                  </v-col>
                </v-row>
              </v-card-text>
            </v-window-item>
          </v-window>
        </v-card>

        <!-- Section: Accordion -->
        <v-card class="mb-6" elevation="2">
          <v-card-title class="text-h6">Accordion</v-card-title>
          <v-card-subtitle>Expansion panels for grouped, collapsible content</v-card-subtitle>
          <v-card-text>
            <v-expansion-panels variant="accordion">
              <v-expansion-panel
                v-for="panel in faqPanels"
                :key="panel.id"
                :title="panel.question"
                :text="panel.answer"
              />
            </v-expansion-panels>
          </v-card-text>
        </v-card>

        <!-- Section: Data Table -->
        <v-card class="mb-6" elevation="2">
          <v-card-title class="text-h6">Data Table</v-card-title>
          <v-card-subtitle>Sortable table of sample account records</v-card-subtitle>
          <v-card-text>
            <v-data-table
              :headers="tableHeaders"
              :items="tableItems"
              item-value="id"
              density="comfortable"
            >
              <template #item.status="{ item }">
                <v-chip
                  :color="item.status === 'Active' ? 'success' : 'default'"
                  size="small"
                  variant="tonal"
                >
                  {{ item.status }}
                </v-chip>
              </template>
            </v-data-table>
          </v-card-text>
        </v-card>
      </v-container>
    </v-main>

    <v-snackbar v-model="snackbar.open" :timeout="3000" color="primary">
      {{ snackbar.message }}
      <template #actions>
        <v-btn variant="text" @click="snackbar.open = false">Close</v-btn>
      </template>
    </v-snackbar>

    <v-footer app color="grey-lighten-3" class="justify-center text-caption">
      Vuetify Component Demo &mdash; built for UI testing purposes
    </v-footer>
  </v-app>
</template>

<script setup>
import { reactive, ref } from 'vue'

const drawer = ref(false)
const showInfoAlert = ref(true)
const dialogOpen = ref(false)
const activeTab = ref('overview')

const departments = ['Engineering', 'Customer Success', 'Sales', 'Operations', 'Finance']

const form = reactive({
  fullName: '',
  email: '',
  department: 'Engineering',
  priority: 3,
  contactMethod: 'email',
  subscribeUpdates: true,
  enableNotifications: false,
})

const rules = {
  required: (value) => !!value || 'This field is required.',
  email: (value) => /.+@.+\..+/.test(value) || 'Enter a valid email address.',
}

const snackbar = reactive({
  open: false,
  message: '',
})

function showSnackbar(message) {
  snackbar.message = message
  snackbar.open = true
}

function onFormSubmit() {
  showSnackbar('Form submitted successfully (demo only, no data is sent).')
}

function onFormReset() {
  form.fullName = ''
  form.email = ''
  form.department = 'Engineering'
  form.priority = 3
  form.contactMethod = 'email'
  form.subscribeUpdates = true
  form.enableNotifications = false
}

function confirmDialog() {
  dialogOpen.value = false
  showSnackbar('Action confirmed.')
}

const teamMembers = [
  { id: 1, name: 'Alex Chen', role: 'Product Manager', initials: 'AC' },
  { id: 2, name: 'Morgan Lee', role: 'UX Designer', initials: 'ML' },
  { id: 3, name: 'Sam Patel', role: 'Engineering Lead', initials: 'SP' },
]

const faqPanels = [
  {
    id: 1,
    question: 'How often is data refreshed?',
    answer: 'Sample data on this page is static and does not refresh automatically.',
  },
  {
    id: 2,
    question: 'Can I export the table data?',
    answer: 'Export is not wired up in this demo; the table is for display and interaction testing only.',
  },
  {
    id: 3,
    question: 'Who can access this page?',
    answer: 'This is a standalone demo page with no authentication or access control.',
  },
]

const tableHeaders = [
  { title: 'Account', key: 'account' },
  { title: 'Owner', key: 'owner' },
  { title: 'Region', key: 'region' },
  { title: 'Status', key: 'status' },
  { title: 'Renewal Date', key: 'renewal' },
]

const tableItems = [
  { id: 1, account: 'Northwind Traders', owner: 'Alex Chen', region: 'West', status: 'Active', renewal: '2026-01-15' },
  { id: 2, account: 'Contoso Ltd.', owner: 'Morgan Lee', region: 'East', status: 'Active', renewal: '2026-03-02' },
  { id: 3, account: 'Fabrikam Inc.', owner: 'Sam Patel', region: 'Central', status: 'At Risk', renewal: '2025-11-20' },
  { id: 4, account: 'Globex Corporation', owner: 'Alex Chen', region: 'South', status: 'Active', renewal: '2026-05-11' },
  { id: 5, account: 'Initech', owner: 'Morgan Lee', region: 'West', status: 'At Risk', renewal: '2025-12-01' },
]
</script>
