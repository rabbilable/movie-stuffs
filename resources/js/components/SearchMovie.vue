<template>
  <div id="searc">
    <div
      class="mdl-textfield mdl-js-textfield mdl-textfield--expandable mdl-textfield--floating-label mdl-textfield--align-right"
    >
      <label class="mdl-button mdl-js-button mdl-button--icon" for="fixed-header-drawer-exp">
        <i class="material-icons">search</i>
      </label>
      <div class="mdl-textfield__expandable-holder">
        <input
          class="mdl-textfield__input"
          type="text"
          name="sample"
          id="fixed-header-drawer-exp"
          v-model.trim="searchQuery"
          @keyup.enter="search"
          @blur="searchQuery"
          placeholder="Search for a movie.."
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  // name: 'search',

  data: function() {
    return {
      searchQuery: "",
      results: []
    };
  },

  computed: {
    queryForRouter() {
      return encodeURI(this.searchQuery.replace(/ /g, "+"));
    }
  },

  methods: {
    search() {
      if (!this.searchQuery.length) return;
      this.$router.push({
        name: "search",
        params: { query: this.queryForRouter }
      });
    }
  }
};
</script>

<style>
</style>