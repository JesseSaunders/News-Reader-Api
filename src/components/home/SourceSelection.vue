<template>
  <div>
    <h4>Select a News Source:</h4>
    <select v-on:change="emitSourceChangedEvent" name id>
      <option>Please select a news source</option>
      <option
        v-for="source in sources"
        v-bind:key="source.id"
        v-bind:value="source.id"
      >{{ source.name }}</option>
    </select>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      sources: []
    };
  },

  methods: {
      emitSourceChangedEvent: function(event) {
          console.log("sourceSelector: is emitting custom event...")
          this.$emit("$source-changed", event.target.value)
      }
  },

  created: function() {
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