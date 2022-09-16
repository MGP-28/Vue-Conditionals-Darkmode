<script setup>
import UserCard from "./components/UserCard.vue";
import ColorModeToggle from "./components/ColorModeToggle.vue";
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
</script>

<template>
  <div class="dm-toggle-container-master">
    <ColorModeToggle />
  </div>
  <div class="contentContainer">
    <UserCard />
  </div>
</template>

<style scoped>
  .dm-toggle-container-master{
    width: 100%;
    height: max-content;
    display: flex;
    justify-content: end;
    align-items: center;
  }
</style>