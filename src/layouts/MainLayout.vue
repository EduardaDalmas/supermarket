<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar color="cyan-3">
        <q-toolbar-title> Supermarket </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'MainLayout',

  components: {},

  setup() {
    return {};
  },
});
</script>
