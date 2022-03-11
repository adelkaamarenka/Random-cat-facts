<template>
  <h1>{{ displayedFact }}</h1>
  <button @click="getRandomFact()">New fact</button>
</template>

<script>
export default {
  data() {
    return {
      displayedFact: "",
      facts: [],
    };
  },
  methods: {
    async fetchFacts() {
      const res = await fetch("https://cat-fact.herokuapp.com/facts");
      const resJSON = await res.json();
      this.facts = resJSON.map((fact) => fact.text);
    },
    async getRandomFact() {
      this.displayedFact = await this.facts[
        Math.floor(Math.random() * this.facts.length)
      ];
    },
    async onMount() {
      await this.fetchFacts();
      await this.getRandomFact();
    },
  },
  async mounted() {
    await this.onMount();
  },
};
</script>
