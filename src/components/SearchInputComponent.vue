<template>
  <div class="search__container">
    <input
      @keydown.enter="sendSearchData"
      v-model="searchString"
      placeholder="🔍 Search by Title"
      class="search__input"
      type="text"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchString: "",
    };
  },
  methods: {
    sendSearchData() {
      if (this.searchString === "") {
        this.$emit("triggerFetch");
      } else {
        this.$emit("triggerFilter", this.searchString);
      }
    },
  },
};
</script>

<style scoped>
.search__container {
  padding: 0 10px;
  margin-top: 20px;
  width: 100%;
}
.search__input {
  font-family: sans-serif;
  box-sizing: border-box;

  padding-left: 10px;

  height: 30px;
  width: 100%;

  border: 1px solid gray;
  border-radius: 5px;
}
</style>
