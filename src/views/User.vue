<template>
  <v-container>
    <v-row>
      <v-col>
        <ModalCreateUser @updateData="fetchAllUsers" />
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <UserComponent @updateData="fetchAllUsers" :users="users" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import ModalCreateUser from "@/components/ModalCreateUser.vue";
import UserComponent from "@/components/UserComponent.vue";

const users = ref([]);

const fetchAllUsers = async () => {
  try {
    const response = await axios.get(
      "http://localhost:8080/users?detailed=true"
    );
    users.value = response.data;
  } catch (error) {
    console.error("Error fetching data:", error);
  }
};

onMounted(fetchAllUsers);
</script>
