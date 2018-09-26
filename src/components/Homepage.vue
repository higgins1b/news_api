<template>
    <div>
        <div>
            <h1 style="margin-top: 5%; margin-bottom: 3%;">News.</h1>
            <div class="row">
                <div v-for="article in articles" class="col-md-3" style="margin-right: 5%; margin-bottom: 5%;">
                    <b-card :title="article.title"
                            :img-src="article.urlToImage"
                            img-alt="Image"
                            img-top
                            tag="article"
                            class="mb-2 h-100">
                        <p class="card-text">
                            {{truncate(article.description)}}
                        </p>
                        <a :href="article.url" target="_blank" class="card-link">Read Full Story</a>
                    </b-card>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import Truncate from 'truncate'

export default {
  data: function () {
    return {
      articles: {}
    }
  },
  methods: {
    loadArticles: function () {
      var url = 'https://newsapi.org/v2/top-headlines?country=us&apiKey=' + '036b827042e7412b8e22608cf307b6d4'

      axios.get(url).then(response => {
        this.articles = response.data.articles
      })
    },
    truncate: function (description) {
      return Truncate(description, 100)
    }
  },
  mounted () {
    this.loadArticles()
  }
  // name: 'Homepage'
}
</script>
