<template>
  <the-header title="Quais são suas metas para hoje?"></the-header>
  <the-resources></the-resources>
  <span class="copywrite"
    >&copy;<sup>{{ year }}</sup> Feito por Antônio Brandão Lima</span
  >
</template>

<script>
import TheHeader from './components/layouts/TheHeader.vue';
import TheResources from './components/learning-resources/TheResources.vue';
export default {
  components: {
    TheHeader,
    TheResources,
  },
  data() {
    return { year: new Date().getFullYear() };
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Roboto', sans-serif;
}

body {
  margin: 0;
}

.copywrite {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: #f5f5f5;
  padding: 10px;
  text-align: center;
  font-size: 14px;
  color: #888;
}
</style>
