<template>
  <v-table density="compact">
    <thead>
      <tr>
        <th class="text-left">Username</th>
        <th class="text-left">Password</th>
        <th class="text-left">Email</th>
        <th class="text-left">First Name</th>
        <th class="text-left">Last Name</th>
        <th class="text-left">Birth Day</th>
        <th class="text-left">Age</th>
        <th class="text-left">Actions</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="user in users" :key="user.id">
        <td>{{ user.username }}</td>
        <td>{{ user.password }}</td>
        <td>{{ user.email }}</td>
        <td>{{ user.firstName }}</td>
        <td>{{ user.lastName }}</td>
        <td>{{ user.birthDay }}</td>
        <td>{{ user.age }}</td>
        <td class="d-flex align-center ga-2">
          <ModalUpdateUser :user="user" :emit="emit" />
          <ModalDeleteUser :user="user" :emit="emit" />
        </td>
      </tr>
    </tbody>
  </v-table>
</template>
<script setup>
import ModalUpdateUser from "@/components/ModalUpdateUser.vue";
import ModalDeleteUser from "@/components/ModalDeleteUser.vue";

const props = defineProps(["users"]);
const emit = defineEmits(["updateData"]);
</script>
