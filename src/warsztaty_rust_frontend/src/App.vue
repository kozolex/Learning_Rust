<script lang="ts">
import { ref } from 'vue';
import { warsztaty_rust_backend } from 'declarations/warsztaty_rust_backend/index';

export default {
  data() {
    return {
      greeting: '',
      wpisy: [],
    }
  },
  methods: {
    async handleSubmit(e) {
      e.preventDefault();
      const target = e.target;
      const name = target.querySelector('#name').value;
      await warsztaty_rust_backend.greet(name).then((response) => {
        this.greeting = response;
      });
    },
    async pobierzWpisy() {
      const wpisy = await warsztaty_rust_backend.pobierz_wpisy()
      this.wpisy = wpisy
    },
  },
  async mounted() {
      await this.pobierzWpisy()
  }
}
</script>

<template>
  <main>
    <img src="/logo2.svg" alt="DFINITY logo" />
    <br />
    <br />
    <form action="#" @submit="handleSubmit">
      <label for="name">Enter your name: &nbsp;</label>
      <input id="name" alt="Name" type="text" />
      <button type="submit">Click Me!</button>
    </form>
    <section id="greeting">{{ greeting }}</section>
    <div>{{ wpisy }}</div>
  </main>
</template>