<template>
    <h1>User profile</h1>
</template>
<script setup>
import { useRoute } from "vue-router"
const route =  useRoute()
const { user_id} = route.user_id
</script>