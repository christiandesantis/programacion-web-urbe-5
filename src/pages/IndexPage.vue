<template>
  <q-page class="q-pa-md">
    <div class="row text-center">
      <div class="q-ml-auto q-mr-auto">
        <q-icon name="science" color="primary" size="20em" />
      </div>
    </div>
    <div class="row text-center">
      <div class="col-12">
        <h3 class="q-mb-sm">Tarea 5 Programación Web</h3>
      </div>
      <div class="col-12">
        <h5 class="q-ma-none">Laboratorio de productos de limpieza</h5>
      </div>
      <div class="col-12 q-mt-xl">
        <q-btn to="/login" outline color="primary" size="lg" flat label="Iniciar Sesión" />
        <q-btn to="/register" outline color="primary" size="lg" flat label="Registrarse" />
      </div>
    </div>
  </q-page>
</template>

<script setup lang="ts">
import { ref } from 'vue'

</script>
