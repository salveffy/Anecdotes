<template>
  <div class="container">
    <ol class="bullet">
      <li
        v-for="anecdot in searchResultData"
        :key="anecdot.id"
        :class="{ white: statusLike[anecdot.id] }"
      >
        {{ anecdot.joke || anecdot.delivery + " " + anecdot.setup }}
        <button class="btnLike" @click="activLike(anecdot.id)">Like</button>
      </li>
    </ol>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "AnecdotCard",
  props: ["searchData"],
  data: () => ({
    anecdotes: [],
    statusLike: {},
  }),
  mounted() {
    this.getAnecdotes();
  },
  methods: {
    async getAnecdotes() {
      try {
        const response = await axios.get(
          "https://v2.jokeapi.dev/joke/Any?amount=10"
        );
        this.anecdotes = response.data.jokes;
        console.log(response.data.jokes);
      } catch (e) {
        console.error(e);
      }
    },
    activLike(id) {
      this.$set(this.statusLike, id, !this.statusLike[id]);
    },
  },
  computed: {
    searchResultData() {
      return this.anecdotes.filter((item) => {
        return Object.values(item).some((m) =>
          m.toString().includes(this.searchData)
        );
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
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
  color: white;
  text-align: center;

}

li::before {
  content: counters(index, ".", decimal-leading-zero);
  font-size: 1.5rem;
  text-align: right;
  font-weight: bold;
  min-width: 50px;
  padding-right: 12px;
  font-variant-numeric: tabular-nums;
  align-self: center;
}

li + li {
  border-top: 1px solid rgba(255, 255, 255, 0.2);
}
.btnLike {
  background-color:white; /* Green */
  border: none;
  color: black;
  padding: 4px 16px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 20px;
  cursor: pointer;
  border-radius: 50px;
}
.white {
  background-color: white;
  color: black;
}
</style>
