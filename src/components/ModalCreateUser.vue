<template>
  <v-btn color="grey darken-1" @click="dialog = true">Add User</v-btn>
  <v-dialog
    transition="dialog-bottom-transition"
    v-model="dialog"
    persistent
    scrollable
    width="500"
  >
    <v-card>
      <v-card-title>
        <span class="text-h5">Add User</span>
      </v-card-title>
      <v-form ref="form">
        <v-card-text>
          <v-text-field
            v-model="formData.username"
            label="Username*"
            required
            :rules="[(v) => !!v || 'Username is required']"
          ></v-text-field>
          <v-text-field
            v-model="formData.password"
            label="Password*"
            type="password"
            required
            :rules="[(v) => !!v || 'Password is required']"
          ></v-text-field>
          <v-text-field
            v-model="formData.email"
            label="Email*"
            required
            :rules="[(v) => !!v || 'Email is required']"
          ></v-text-field>
          <v-text-field
            v-model="formData.firstName"
            label="First Name*"
            required
            :rules="[(v) => !!v || 'First Name is required']"
          ></v-text-field>
          <v-text-field
            v-model="formData.lastName"
            label="Last Name*"
            required
            :rules="[(v) => !!v || 'Last Name is required']"
          ></v-text-field>
          <v-text-field
            v-model="formData.birthDay"
            type="date"
            label="Birth Day"
          ></v-text-field>
          <v-text-field v-model="formData.age" label="Age"></v-text-field>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="red" @click="closeDialog"> Close </v-btn>
          <v-btn color="blue" @click="saveAndClose"> Save </v-btn>
        </v-card-actions>
      </v-form>
    </v-card>
  </v-dialog>
</template>

<script setup>
import { reactive, ref } from "vue";
import axios from "axios";

const dialog = ref(false);

const form = ref();

const emit = defineEmits(["updateData"]);

const formData = reactive({
  username: null,
  password: null,
  email: null,
  firstName: null,
  lastName: null,
  age: null,
  birthDay: null,
});

const resetForm = () => {
  formData.username = null;
  formData.password = null;
  formData.email = null;
  formData.firstName = null;
  formData.lastName = null;
  formData.age = null;
  formData.birthDay = null;
};

const closeDialog = () => {
  resetForm();
  emit("updateData");
  dialog.value = false;
};

const saveAndClose = async () => {
  validate();
  try {
    await axios.post("http://localhost:8080/users", formData);
    closeDialog();
  } catch (error) {
    console.error("Error en la solicitud:", error);
  }
};

async function validate() {
  await form.value.validate();
}
</script>
