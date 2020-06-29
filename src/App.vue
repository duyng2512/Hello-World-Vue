<template>
  <div id="app">
    <div id="nav">
      <Header />
    </div>
    <router-view />
  </div>
</template>

<script>
import Header from './components/layout/Header.vue';

export default {
  components: {
    Header,
  },
};
</script>

<style></style>
