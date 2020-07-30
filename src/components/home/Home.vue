<template>
  <div>
    <!-- This is a dropdown of my sources -->
    <div>
      <h4>Select a News Source:</h4>
      <select v-on:change="sourceChanged" name id>
        <option>Please select a news source</option>
        <option
          v-for="source in sources"
          v-bind:key="source.id"
          v-bind:value="source.id"
        >{{ source.name }}</option>
      </select>
    </div>

    <!-- This displays my articles -->
    <li v-for="article in articles" v-bind:key="article.id" class="media">
      <div class="media-left">
        <a v-bind:href="article.url" target="_blank">
          <img class="media-object" v-bind:src="article.urlToImage" v-bind:alt="article.title" />
        </a>
      </div>
      <div class="media-body">
        <h4 class="media-heading">
          <a v-bind:href="article.url" target="_blank">{{article.title}}</a>
        </h4>
      </div>
    </li>
  </div>
</template>

<script>
export default {
  name: "Home",
  data: function() {
    return {
      articles: [],
      sources: []
    };
  },

  methods: {
    getArticles: function(source) {
      this.$http
        .get(
          `https://newsapi.org/v2/top-headlines?sources=${source}&apiKey=${process.env.VUE_APP_API_KEY}`
        )
        .then(function(data) {
          this.articles = data.body.articles;
          console.log(this.articles);
        });
    },

    sourceChanged: function(event) {
      this.getArticles(event.target.value)
    }
  },

  created: function() {
    // const source = "abc-news";
    // this.getArticles(source);

    this.$http
      .get(
        `https://newsapi.org/v2/sources?apiKey=${process.env.VUE_APP_API_KEY}`
      )
      .then(function(data) {
        this.sources = data.body.sources;
      });
  }
};
</script>

<style>
</style>
