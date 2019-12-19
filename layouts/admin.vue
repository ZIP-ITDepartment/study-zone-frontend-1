<template>
  <v-app>
    <v-navigation-drawer app>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title pa-1">
            Study Zone
          </v-list-item-title>
          <!-- <v-list-item-subtitle>
            subtext
          </v-list-item-subtitle> -->
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list class="pa-0">
        <v-list-item to="/admin/dashboard">
          <v-list-item-icon>
            <v-icon>mdi-view-dashboard</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>Dashboard</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-divider></v-divider>
        <v-subheader>Monitoring</v-subheader>
        <v-list-item to="/admin/monitoring/transactions">
          <v-list-item-icon>
            <v-icon>mdi-table</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>Transactions</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item to="/admin/management/subscriptions">
          <v-list-item-icon>
            <v-icon>mdi-stack-overflow</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>Subscriptions</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        
        <v-divider></v-divider>
        <v-subheader>Management</v-subheader>
        <v-list-item to="/admin/management/cards">
          <v-list-item-icon>
            <v-icon>mdi-card</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>Cards</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <!-- <v-list-item to="/sa/settings/department">
          <v-list-item-icon>
            <v-icon>mdi-chart-timeline-variant</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>Subscriptions</v-list-item-title>
          </v-list-item-content>
        </v-list-item> -->
        <v-list-item to="/admin/management/spaces">
          <v-list-item-icon>
            <v-icon>mdi-stack-overflow</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title>Spaces</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-spacer></v-spacer>
      <v-btn text>Logout</v-btn>
    </v-app-bar>
    <v-content>
      <v-container fluid>
        <router-view></router-view>
      </v-container>
    </v-content>

    <v-footer app>
    </v-footer>
  </v-app>
</template>