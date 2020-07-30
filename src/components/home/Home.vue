<template>
  <h2>Home Page</h2>
</template>

<script>
export default {
  name: "Home",
  data: function() {
    return {
      articles: []
    };
  },

  methods: {
    getArticles: function(source) {
      this.$http
        .get(
          `https://newsapi.org/v2/top-headlines?sources=${source}&apiKey=11494ad6b294452580a9d718e18c3994`
        )
        .then(function(data) {
            this.articles = data.body.articles;
            console.log(this.articles[0].title);
        });
    }
  },

  created: function() {
      const source = "abc-news";
      this.getArticles(source);
  }
};
</script>

<style>
</style>
