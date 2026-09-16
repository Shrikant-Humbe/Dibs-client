<script setup>
import router from '@/router';
import axios from 'axios';
import { ref } from 'vue';

const user=ref({
    username:'',
    password:''
})
const showPassword = ref(false);

async function login(){
    try {
        const response= await axios.post("/login",user.value);
        console.log(response.data);
         router.push("/")
    } catch (error) {
        console.log(error)
    }
}
</script>
<template>
    <fieldset class="fieldset bg-base-200 border-base-300 rounded-box w-xs border p-4">
  <legend class="fieldset-legend">Login</legend>

  <label class="label" >Email</label>
  <input  type="text"  class="input" placeholder="Email" v-model="user.username" />

  <label class="label">Password</label>
  <div class="password-wrapper">
    <input
      :type="showPassword ? 'text' : 'password'"
      class="input"
      placeholder="Password"
      v-model="user.password"
    />
    <button
      type="button"
      class="eye-btn"
      @click="showPassword = !showPassword"
      :aria-label="showPassword ? 'Hide password' : 'Show password'"
    >
      <!-- Eye icon (visible) -->
      <svg v-if="!showPassword" xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/>
        <circle cx="12" cy="12" r="3"/>
      </svg>
      <!-- Eye-off icon (hidden) -->
      <svg v-else xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M17.94 17.94A10.07 10.07 0 0 1 12 20c-7 0-11-8-11-8a18.45 18.45 0 0 1 5.06-5.94"/>
        <path d="M9.9 4.24A9.12 9.12 0 0 1 12 4c7 0 11 8 11 8a18.5 18.5 0 0 1-2.16 3.19"/>
        <line x1="1" y1="1" x2="23" y2="23"/>
      </svg>
    </button>
  </div>

  <button class="btn btn-neutral mt-4" @click="login">Login</button>
</fieldset>
</template>

<style scoped>
.password-wrapper {
  position: relative;
  display: flex;
  align-items: center;
}

.password-wrapper .input {
  width: 100%;
  padding-right: 2.5rem;
}

.eye-btn {
  position: absolute;
  right: 0.6rem;
  background: none;
  border: none;
  cursor: pointer;
  color: inherit;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.2rem;
  opacity: 0.6;
  transition: opacity 0.2s;
}

.eye-btn:hover {
  opacity: 1;
}
</style>