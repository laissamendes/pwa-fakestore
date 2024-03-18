<script setup>
  import { useLayout } from '@/composables/layout.js';
  const { layout } = useLayout();

 
</script>

<template>
  <div>
    <component :is="layout" />
    <main>
      <router-view />
    </main>
    <footer style="color: #D5618F; text-align: center;">
      <p>Copyright &copy; 2024</p>
    </footer>
  </div>
</template>