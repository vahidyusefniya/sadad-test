<script setup>
  function showLog() {
    console.log("ok")
  }
</script>
<template>
  <v-col>
    <v-row>
      <v-col cols="12">
        <StatusCard />
      </v-col>
      <v-col cols="12">
        <RecentOrders />
      </v-col>
    </v-row>
  </v-col>
</template>

