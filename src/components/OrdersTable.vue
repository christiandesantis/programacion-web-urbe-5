<template>
  <div class="q-pa-md">
    <q-table
      :rows="rows"
      :columns="columns"
      row-key="name"
    >
      <template #body-cell-actions="props">
        <div>
          <q-btn class="block q-ml-auto q-mr-auto" icon="check" @click="editRow(props.row)" />
        </div>
      </template>
    </q-table>
    <q-page-sticky osition="bottom-right" :offset="[16, 16]">
      <q-btn fab icon="add" @click="formDialog = true" rounded glossy color="primary" size="lg" :disable="false"/>
    </q-page-sticky>
  </div>

  <q-dialog v-model="formDialog">
    <q-card class="q-pa-md">
      <q-card-section class="row items-center">
        <div class="text-h6">Agregar orden de compra</div>
      </q-card-section>
      <q-form @submit.prevent="onSubmit">
        <q-card-section>
            <q-select
              class="q-mt-sm"
              filled
              v-model="selectName"
              :options="nameOptions"
              label="Seleccionar producto"
              color="primary"
              />

              <q-input filled class="q-mt-md" color="primary" v-model="quantity" :label="`${selectName === null ? 'Cantidad' : `Cantidad en ${selectName['units']}`}`" />
        </q-card-section>
        <q-card-actions align="right">
          <q-btn flat v-close-popup color="grey-7" class="q-mr-sm" label="Cancelar"></q-btn>
          <q-btn flat type="submit" color="primary" icon="save" label="Guardar"></q-btn>
        </q-card-actions>
      </q-form>
    </q-card>
  </q-dialog>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { db, auth } from '../composables/firebase'
import { collection, deleteDoc, doc, getDocs, setDoc } from 'firebase/firestore'

const formDialog = ref(false)

const columns = [
  { name: 'name', align: 'center', label: 'Nombre', field: 'name', sortable: true },
  { name: 'quantity', label: 'Cantidad', field: 'quantity', sortable: true },
  { name: 'units', label: 'Unidades', field: 'units', sortable: true },
  { name: 'actions', align: 'end', label: 'Acciones', field: 'actions' }
]

const rows = ref([
  {
    name: 'Amoníaco cuaternario',
    units: 'kg',
    quantity: 10,
    actions: ''
  }
])

const selectName = ref(null)
const quantity = ref(0)
const nameOptions = ref([
  { label: 'Amoníaco cuaternario', units: 'kg', value: 1 },
  { label: 'Cloruro de benzalconio', units: 'kg', value: 2 },
  { label: 'Alcohol etílico', units: 'litros', value: 3 },
  { label: 'Lauril éter sulfato de sodio', units: 'gramos', value: 4 }
])

function editRow (row: any) {
//   console.log(row)
}

async function onSubmit () {
  const collectionsRef = collection(db, `${auth.currentUser?.uid}`)
  await setDoc(doc(collectionsRef, 'orders'), {
    name: selectName.value?.label ?? '',
    units: selectName.value?.units ?? '',
    quantity: quantity.value
  })
}
</script>
