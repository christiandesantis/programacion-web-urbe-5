<template>
  <q-page class="q-pa-md">
    <div class="row justify-around">
      <q-card class="col-md-8">
        <q-tabs
          v-model="tab"
          dense
          class="text-grey"
          active-color="primary"
          indicator-color="primary"
          align="justify"
          narrow-indicator
          >
          <q-tab name="orders" icon="shopping_bag" label="Ordenes de compra" />
          <q-tab name="inventory" icon="inventory" label="Inventario" />
          <q-tab name="production" icon="conveyor_belt" label="Producción" />
          <q-tab name="statistics" icon="bar_chart" label="Estadísticas" />
        </q-tabs>

        <q-separator />

        <q-tab-panels keep-alive v-model="tab" animated>
          <q-tab-panel name="orders">
            <div class="text-h6 q-mb-lg">Ordenes de compra</div>
            <OrdersTable />
          </q-tab-panel>

          <q-tab-panel name="inventory">
            <div class="text-h6 q-mb-lg">Inventario</div>
            <!-- <HistoryList /> -->
          </q-tab-panel>

          <q-tab-panel name="production">
            <div class="text-h6 q-mb-lg">Producción</div>
            <!-- <StatisticsCharts /> -->
          </q-tab-panel>

          <q-tab-panel name="statistics">
            <div class="text-h6 q-mb-lg">Estadísticas</div>
            <!-- <StatisticsCharts /> -->
          </q-tab-panel>
        </q-tab-panels>
      </q-card>
    </div>

  </q-page>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import OrdersTable from '../components/OrdersTable.vue'
// import HistoryList from '../components/HistoryList.vue'
// import StatisticsCharts from '../components/StatisticsCharts.vue'

const tab = ref('orders')

</script>
