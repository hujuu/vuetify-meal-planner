<template>
  <v-app>
    <v-main>
      <router-view />
    </v-main>
    <v-footer>
      <span class="text-light-green">My Meal Planner</span>&nbsp;- &copy; {{ new Date().getFullYear() }}
    </v-footer>
  </v-app>
</template>

<script lang="ts" setup>
  //
</script>
