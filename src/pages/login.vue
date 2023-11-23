<template>
  <h1 class="text-center font-bold text-3xl pt-20">Login Page</h1>
  <div class="flex justify-center p-4 w-full">
    <div class="w-[600px] flex flex-col gap-2">
      <input type="text" required v-model="username" class="border p-4" placeholder="Username" />
      <input type="password" required v-model="password" class="border p-4" placeholder="Password" />
      <button @click="onLogin()" :disabled="!isFormValid" class="bg-blue-500 text-white py-2 px-3 hover:brightness-90 duration-150">Login</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useRouter } from "vue-router";
import { useAuthStore } from "@/stores/auth";
import Swal from "sweetalert2";

const auth = useAuthStore();
const username = ref("");
const password = ref("");
const router = useRouter();

// Check if both username and password are not empty
const isFormValid = () => {
  return username.value.trim() !== "" && password.value.trim() !== "";
};

const onLogin = () => {
  if (isFormValid()) {
    auth.login(username.value); // You may adjust this part according to your authentication logic
    router.push("/");
  } else {
    // Handle invalid login attempt, e.g., show an error message with SweetAlert2
    Swal.fire({
      icon: "error",
      title: "Invalid Login",
      text: "Please enter username and password",
    });
  }
};
</script>
