<script>
  import axios from 'axios'

  export default {
    created() {
      axios
        .get('https://inshorts.deta.dev/news?category=all')
        .then((response) => {
          this.articles = response.data
        })
        .catch((error) => {
          console.error(error)
        })
    },
    data() {
      return {
        articles: null,
        message: null
      }
    }
  }
</script>

<template>
  <h1>Home</h1>

  <ol v-if="articles">
    <li :key="article.id" v-for="article in articles.data.slice(0, 20)">
      <p>
        <span
          style="
            font-size: 22px;
            font-weight: normal;
            font-family: 'Times New Roman', Times, serif;
          "
        >
          {{ article.title }}</span
        >
      </p>
      <p id="maintext">{{ article.content }}</p>
      <img v-if="article.imageUrl" :src="article.imageUrl" />
      <p v-if="!article.imageUrl">Image not available</p>
      <p>{{ article.date }}</p>
      <a :href="article.readMoreUrl">{{ article.readMoreUrl }}</a>
      <p v-if="!article.readMoreUrl">No more info</p>
    </li>
  </ol>
</template>

<style>
  img {
    margin-top: 30px;
    max-width: 100%;
  }

  ol {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
  li {
    list-style-type: none;
    padding: 30px;
    overflow: hidden;
  }

  @media (max-width: 1180px) {
    body {
      padding-right: 40px;
    }
    ol {
      display: grid;
      grid-template-columns: 100%;
    }
    li {
      list-style-type: none;
    }
  }
</style>
