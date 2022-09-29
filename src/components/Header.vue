<template>
  <div>
    <h1 class="text-3xl text-white">{{ h1 }}</h1>
  </div>
</template>

<script setup>
import { ref } from "vue";

const h1 = ref("Todo-App");
</script>
