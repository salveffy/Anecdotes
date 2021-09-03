<template>
  <div class="container">
    <ol class="bullet">
      <li
        v-for="anecdot in searchResultData"
        :key="anecdot.id"
        :class="{ white: statusLike[anecdot.id] }"
      >
        {{ anecdot.joke || anecdot.delivery + " " + anecdot.setup }}
        <button
          class="btnLike"
          v-on:click="onLike = !onLike"
          @click="activLike(anecdot.id), setLocStor(anecdot)"
        >
          Like
        </button>
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
    onLike: false,
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
      } catch (e) {
        console.error(e);
      }
    },
    activLike(id) {
      this.$set(this.statusLike, id, !this.statusLike[id]);
    },
    setLocStor(anecdot) {
      localStorage.setItem(anecdot.id, JSON.stringify(anecdot));
      this.onLike = false;
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
ol {
  padding: 0;
  width: 50%;
}

li {
  counter-increment: index;
  display: flex;
  align-items: center;
  padding: 12px 0;
  box-sizing: border-box;
  color: white;
  text-align: center;
  justify-content: space-between;
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
  background-color: white; /* Green */
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

@media (max-width: 1000px) {
  ol {
    padding: 0;
    width: 100%;
  }
  @media (max-width: 480px) {
    ol {
      padding: 0;
      width: 60%;
    }
    li {
      flex-direction: column;
      margin: 10px;
    }
    li::before {
      padding-right: 20px;
      padding-bottom: 10px;
    }
    .btnLike {
      margin-top: 15px;
    }
  }
}
</style>
