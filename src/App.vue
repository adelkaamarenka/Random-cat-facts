<template>
  <h1>{{ displayedFact }}</h1>
  <button @click="incrementId()">New fact</button>
</template>

<script>
export default {
  data() {
    return {
      id: 0,
      facts: [],
      factsText: [],
    };
  },
  methods: {
    async fetchFacts() {
      const res = await fetch("https://cat-fact.herokuapp.com/facts");
      this.facts = await res.json();
      this.factsText = this.facts.map((fact) => fact.text);
    },
    incrementId() {
      if (this.id < this.factsText.length - 1) {
        this.id++;
      } else {
        this.id = 0;
      }
    },
  },
  mounted() {
    this.fetchFacts();
  },
  computed: {
    displayedFact() {
      return this.factsText[this.id];
    },
  },
};
</script>
