<template>
  <div id="app">
    <div class="container">
      <div class="search_container">
        <p class="search_title">Enter a search word</p>
        <input
          v-model="searchData"
          class="search_input"
          type="text"
          placeholder="Search"
        />
      </div>
    </div>
    <AnecdotCard :searchData="searchData" />
  </div>
</template>

<script>
import AnecdotCard from "./components/AnecdotCard.vue";

export default {
  name: "App",
  data: () => ({
    searchData: "",
  }),
  components: {
    AnecdotCard,
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  background-color: black;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}

.container {
  margin: auto;
  display: flex;
  justify-content: center;
}
.search_title {
  font-size: 22px;
  font-weight: 900;
  text-align: center;
  color: #ffffff;
}

.search_input {
  width: 100%;
  padding: 12px 24px;
  background-color: transparent;
  font-size: 14px;
  line-height: 18px;
  color: #ffffff;
  border: 1px solid #ffffff;
  outline: none;
  border-radius: 50px;
}
</style>
