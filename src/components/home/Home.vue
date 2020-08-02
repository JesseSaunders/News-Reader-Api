<template>
  <div>
    <!-- This is a dropdown of my sources -->
    <source-selection v-on:$source-changed="sourceChanged"></source-selection>

    <!-- This displays my articles -->
    <article-list v-bind:source="source"></article-list>
  </div>
</template>

<script>
import SourceSelection from "./SourceSelection.vue";
import ArticleList from "./ArticleList.vue";
export default {
  name: "Home",
  data: function() {
    return {
      source: ''
    };
  },

  components: {
    "source-selection": SourceSelection,
    "article-list": ArticleList
  },

  methods: {
    sourceChanged: function(source) {
      console.log("Home: custom event detected, data is: " + source)
      this.source = source;
    }
  }
};
</script>

<style>
</style>
