<template>
  <v-main>
    <v-app-bar class="px-3" flat density="compact" color="deep-orange-darken-2">
      <v-btn @click="toggleTheme" icon position="absolute">
        <v-icon>{{ darkModeIcon }}</v-icon>
      </v-btn>
      <v-spacer></v-spacer>
      <v-tabs centered>
        <v-tab v-for="link in links" :key="link.name" :to="link.link">
          {{ link.name }}
        </v-tab>
      </v-tabs>
      <v-spacer></v-spacer>
    </v-app-bar>
    <router-view />
  </v-main>
</template>

<script setup>
import { useTheme } from "vuetify";
import { computed } from "vue";

const theme = useTheme();

function toggleTheme() {
  theme.global.name.value = theme.global.current.value.dark ? "light" : "dark";
}

const links = [
  { link: "/", name: "Home" },
  { link: "/users", name: "Users" },
];

const darkModeIcon = computed(() => {
  return theme.global.current.value.dark
    ? "mdi-brightness-7"
    : "mdi-brightness-4";
});
</script>
