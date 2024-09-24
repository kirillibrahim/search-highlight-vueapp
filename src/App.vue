<template>
  <div id="app" class="container">
    <div class="search-box">
      <input v-model="searchQuery" placeholder="Search" />
      <p>{{ articles.length }} posts were found.</p>
    </div>
    
    <div class="results">
      <div v-for="article in filteredArticles" :key="article.id" class="article">
        <h3 v-html="highlightSearch(article.title)" class="article-title"></h3>
        <p class="date">{{ article.date }}</p>
        <p>{{ article.description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: "",
      articles: [
        {
          id: 1,
          title: "Understanding the difference between grid-template and grid-auto",
          date: "Oct 09, 2018",
          description: "With all the new properties related to CSS Grid Layout...",
        },
        {
          id: 2,
          title: "Recreating the GitHub Contribution Graph with CSS Grid Layout",
          date: "Oct 11, 2019",
          description: "In this post, we recreate the GitHub contribution graph...",
        },
        {
          id: 3,
          title: "Exploring advanced CSS techniques for layout design",
          date: "Jan 05, 2020",
          description: "An in-depth look at modern CSS layout techniques...",
        },
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
    },
  },
  methods: {
    highlightSearch(title) {
      if (!this.searchQuery) return title;
      const regex = new RegExp(`(${this.searchQuery})`, "gi");
      return title.replace(regex, "<mark>$1</mark>");
    },
  },
};
</script>

<style scoped>
.container {
  width: 60%;
  margin: 0 auto;
  font-family: Arial, sans-serif;
}

.search-box {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

.search-box input {
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ddd;
  margin-bottom: 10px;
  width: 100%;
  border-radius: 4px;
}

.search-box p {
  font-size: 14px;
  color: #333;
}

.results {
  display: flex;
  flex-direction: column;
}

.article {
  border-bottom: 1px solid #eee;
  padding: 10px 0;
}

.article-title {
  font-size: 18px;
  color: #333;
  margin: 0 0 5px;
}

.date {
  font-size: 12px;
  color: #888;
}

mark {
  background-color: yellow;
}
</style>
