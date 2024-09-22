<template>
  <div id="app">
    <input v-model="searchQuery" placeholder="Search..." />

    <div v-for="article in filteredArticles" :key="article.id" class="article">
      <p v-html="highlightSearch(article.title)"></p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: "",
      articles: [
        { id: 1, title: "Understanding the difference between grid-template and grid-auto" },
        { id: 2, title: "Recreating the GitHub Contribution Graph with CSS Grid Layout" },
        { id: 3, title: "Getting started with Vue.js and building your first app" },
        { id: 4, title: "Advanced techniques in React using hooks and context" },
      ],
    };
  },
  computed: {
    filteredArticles() {
      if (!this.searchQuery) return this.articles;
      const query = this.searchQuery.toLowerCase();
      return this.articles.filter(article =>
        article.title.toLowerCase().includes(query)
      );
    }
  },
  methods: {
    highlightSearch(title) {
      if (!this.searchQuery) return title;
      const regex = new RegExp(`(${this.searchQuery})`, "gi");
      return title.replace(regex, "<mark>$1</mark>");
    }
  }
};
</script>

<style>
input {
  display: block;
  margin-bottom: 20px;
  padding: 10px;
  width: 300px;
}

.article {
  margin-bottom: 15px;
}

mark {
  background-color: yellow;
}
</style>
