<template>
  <v-layout class="rounded rounded-md">
    
    <v-navigation-drawer 
      v-model="sidebarMenu" 
      app
      floating
      :permanent="sidebarMenu"
      >
        <v-list dense color="primary" dark>
          <v-list-item>
            <v-list-item-title>
                <h3 class="font-weight-thin">Dashboard</h3>
            </v-list-item-title>
          </v-list-item>
        </v-list>
        <v-divider />
        <v-list>
          <v-list-item v-for="item in items" :key="item.title" link :to="item.href" class="d-flex">
            <template v-slot:prepend>
              <v-icon color="primary">{{ item.icon }}</v-icon>
            </template>
            <v-list-item-title class="primary--text">{{ item.title }}</v-list-item-title>
          </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar app color="primary" dark elevation="0">
        <v-app-bar-nav-icon @click.stop="sidebarMenu = !sidebarMenu"></v-app-bar-nav-icon>
        <v-spacer></v-spacer>
        <v-btn @click="toggleTheme" color="white" class="mr-2">
          <v-icon color="white" v-if="!theme.global.current.value.dark">mdi-lightbulb</v-icon>
          <v-icon color="white" v-else>mdi-lightbulb-on</v-icon>
        </v-btn>
        <v-icon class="mr-4">mdi-account</v-icon>
    </v-app-bar>
    <v-main style="min-height: 300px;">
      <div class="pa-4">
        <slot />
      </div>
    </v-main>
  </v-layout>
</template>

<script setup>
  import { ref, computed } from 'vue';
  import { useTheme } from 'vuetify';
  const mode = useColorMode();

  const sidebarMenu = ref(true);
  const theme = useTheme();

  const items = ref([
    { title:"Home", href:"/", icon:"mdi-home-outline" },
  ]);

  function toggleTheme () {
    mode.value = mode.value === "dark" ? "light" : "dark";
    theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'
  };
</script>