<template>
  <v-btn color="blue" size="small" @click="dialog = true">
    <v-icon icon="mdi-pencil" style="font-size: 20px" />
  </v-btn>
  <v-dialog
    transition="dialog-bottom-transition"
    v-model="dialog"
    persistent
    scrollable
    width="500"
  >
    <v-card>
      <v-card-title>
        <span class="text-h5">Update User</span>
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
import { reactive, ref, watchEffect } from "vue";
import axios from "axios";

const dialog = ref(false);

const props = defineProps(["user", "emit"]);

const form = ref();

const formData = reactive({
  username: props.user.username,
  password: props.user.password,
  email: props.user.email,
  firstName: props.user.firstName,
  lastName: props.user.lastName,
  age: props.user.age,
  birthDay: props.user.birthDay,
});

watchEffect(() => {
  Object.assign(formData, props.user);
});

const closeDialog = () => {
  props.emit("updateData");
  dialog.value = false;
};

const saveAndClose = async () => {
  validate();
  try {
    await axios.put(`http://localhost:8080/users/${props.user.id}`, formData);
    closeDialog();
  } catch (error) {
    console.error("Error en la solicitud:", error);
  }
};

async function validate() {
  await form.value.validate();
}
</script>
