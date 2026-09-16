<script setup>
import router from '@/router';
import axios from 'axios';
import { ref } from 'vue';
async function logout(){
    try {
        const response= await axios.get("/logout");
        localStorage.removeItem('token');
        router.push("/");
    } catch (error) {
        console.log(error);
    }
}
</script>
<template>
    logged out
</template>