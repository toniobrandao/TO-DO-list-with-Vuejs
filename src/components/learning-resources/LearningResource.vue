<template>
  <li>
    <base-card>
      <header>
        <h3 class="title">{{ title }}</h3>
        <div class="button-container">
          <base-button
            class="custom-button"
            mode="flat"
            @click="archiveResource(id)"
            >Objetivo Feito</base-button
          >

          <base-button
            class="custom-button"
            mode="flat"
            @click="deleteResource(id)"
            >Deletar</base-button
          >
        </div>
      </header>

      <p class="description">{{ description }}</p>

      <nav v-if="link" class="link-nav">
        <a :href="link">Ver link</a>
      </nav>
    </base-card>
  </li>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
export default {
  components: { BaseButton },
  props: ['id', 'title', 'description', 'link'],
  inject: ['deleteResource', 'archiveResource'],
};
</script>

<style scoped>
base-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
}

.title {
  margin: 0.5rem 0 0.5rem 1rem;
  text-align: center;
}

.description {
  margin: 0.5rem 0 0.5rem 1rem;
}

.link-nav {
  margin-top: 1rem;
  margin-left: 1rem;
}

.button-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%; /* Ensure the container occupies full height */
}
.custom-button {
  width: 150px; /* Adjust the width as needed */
}
li {
  margin: auto;
  max-width: 40rem;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>
