<template>
  <div class="wrapper">
    <h1 class="fact">{{ displayedFact }}</h1>
    <button class="btn btn-dark btn-lg" @click="getRandomNumber()">
      New fact
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      facts: [],
      ranNumber: 0,
    };
  },
  computed: {
    displayedFact() {
      return this.facts[this.ranNumber];
    },
  },
  methods: {
    async fetchFacts() {
      const res = await fetch("https://cat-fact.herokuapp.com/facts");
      const resJSON = await res.json();
      this.facts = resJSON.map((fact) => fact.text);
    },
    getRandomNumber() {
      let newRandom;
      do {
        newRandom = Math.floor(Math.random() * this.facts.length);
      } while (newRandom == this.ranNumber);

      this.ranNumber = newRandom;
    },
    async onMount() {
      await this.fetchFacts();
      this.getRandomNumber();
    },
  },
  async mounted() {
    await this.onMount();
  },
};
</script>

<style>
#app {
  min-height: 100vh;
  min-width: 100vw;
  background: url("./assets/pattern.png");
  display: flex;
}

.wrapper {
  height: 75vh;
  width: 60vw;
  margin: auto;
  text-align: center;
  background-color: rgba(255, 255, 255, 0.8);
}

.fact {
  margin-top: 1.5rem;
  margin-bottom: 3rem;
  font-size: 55px;
  height: 30%;
}
</style>
