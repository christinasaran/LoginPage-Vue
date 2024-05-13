<script setup>
import { ref } from "vue";
import { debounce } from "lodash";

const email = ref("");
const password = ref("");
const validEmail = ref(true);
const showPassword = ref(false);

const validateEmail = debounce(() => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  validEmail.value = emailRegex.test(email.value);
}, 500);

const toggleShowPassword = () => {
  showPassword.value = !showPassword.value;
};
</script>

<template>
  <div class="flex items-center justify-center h-screen">
    <div class="w-1/4 select-none">
      <!-- Header -->
      <div class="text-center mb-12">
        <h1 class="text-3xl font-semibold">Welcome Back!</h1>
        <div class="text-gray-500 font-medium">Let's get you logged in</div>
      </div>
      <!-- Login Body -->
      <div class="flex flex-col space-y-3">
        <input
          v-model="email"
          @input="validateEmail"
          type="email"
          placeholder="Email Address"
          class="focus:outline-none border border-gray-500 rounded-full px-3 py-2 mr-[32px]x"
          :class="{ 'ring-1 ring-red-500 border-red-500': !validEmail }"
        />
        <div class="flex relative">
          <input
            v-model="password"
            :type="!showPassword ? 'password' : 'text'"
            placeholder="Password"
            class="flex-1 focus:outline-none border border-gray-500 rounded-full px-3 py-2"
          />
          <i
            class="fa my-auto mx-2 absolute right-1 top-3.5 z-10 cursor-pointer"
            :class="showPassword ? 'fa-eye-slash' : 'fa-eye'"
            @click="toggleShowPassword"
          ></i>
        </div>
        <p
          class="text-gray-500 font-medium text-right text-xs px-2 cursor-pointer"
        >
          Forgot Password?
        </p>
        <button
          class="font-medium py-2.5 rounded-full bg-black text-white cursor-pointer"
        >
          Login
        </button>
        <div
          class="text-gray-500 text-center text-xs font-medium cursor-pointer"
        >
          Not a member? <span class="pr-2">Register now</span>
        </div>
      </div>
    </div>
    <img src="../../public/login.png" alt="" class="pl-24 w-1/4 h-1/3" />
  </div>
</template>

<style scoped></style>
