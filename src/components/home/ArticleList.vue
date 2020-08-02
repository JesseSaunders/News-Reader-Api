<template>
  <div>
    <h1>{{source}}</h1>
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
  data: function() {
    return {
      articles: [],
      message: "I am a message"
    };
  },

  props: {
    source: {
      type: String,
      required: true
    }
  },

  watch: {
    source: function(value) {
      console.log(
        "ArticleList: watcher detected value change (" +
          value +
          "), calling getArticles method..."
      );
      this.getArticles(value);
    }
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
    }
  }
};
</script>

<style>
</style>