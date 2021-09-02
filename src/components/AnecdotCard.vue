<template>
  <div class="container">
    <ol class="bullet">
      <li v-for="anecdot in anecdotes.jokes" :key="anecdot">
          {{anecdot.joke || anecdot.delivery + ' ' + anecdot.setup}}
      </li>
    </ol>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "AnecdotCard",
  data: () => {
    return {
      anecdotes: [],
    };
  },
  mounted() {
    this.getAnecdotes();
  },
  methods: {
    async getAnecdotes() {
      try {
        const response = await axios.get(
          "https://v2.jokeapi.dev/joke/Any?amount=10"
        );
        this.anecdotes = response.data;
        console.log(response.data);
      } catch (e) {
        console.error(e);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.container{
  margin: auto;
  display: flex;
  justify-content: center;
}
ul {

  padding: 0;
  max-width: 300px;
}

li {
  counter-increment: index;
  display: flex;
  align-items: center;
  padding: 12px 0;
  box-sizing: border-box;
}


li::before {
  content: counters(index, ".", decimal-leading-zero);
  font-size: 1.5rem;
  text-align: right;
  font-weight: bold;
  min-width: 50px;
  padding-right: 12px;
  font-variant-numeric: tabular-nums;
  align-self: flex-start;

}

li + li {
  border-top: 1px solid rgba(255, 255, 255, 0.2);
}
</style>
