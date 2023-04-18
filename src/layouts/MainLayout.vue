<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar class="text-white shadow-2 rounded-borders">
        <q-btn flat label="Tarea 5" to="/" />
        <q-space />
        <div>
          {{ `${user.displayName}` }}
        </div>
        <q-btn class="q-ml-sm" flat round dense>
          <q-icon name="logout" @click="signOut()" />
        </q-btn>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup lang="ts">
import { useAuthStore } from '../stores/auth-store'
import { db, auth } from '../composables/firebase'
import { computed } from 'vue'
import { useRouter } from 'vue-router'

const authStore = useAuthStore()

const router = useRouter()

auth.onAuthStateChanged(user => {
  authStore.fetchUser(user)
})

const user = computed(() => {
  return authStore.user
})

async function signOut () {
  await authStore.logOut()
  router.push('/login')
}
</script>
