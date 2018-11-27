<template>
  <div class="container">

      
       <input type="search" placeholder="Type to search" id="nameField" v-model="search">
      <button v-on:click="loadNews" type="button">search</button>

      <p v-if="loading">Search in progress..</p>

      <div class="lds-spinner"v-if="loading"><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div></div>
       
    <div v-for="article in news">
        <div class="news-item">

       <img v-if="article.urlToimage":src="article.urlToImage"alt="">
      <h3> {{article.title}}</h3>
      <h4>{{article.author}}</h4>
      <blockquote>
      <p>{{article.description}}</p>
      </blockquote>
      <a href="#" target="blank" class="button">Read more</a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

const baseUrl = "https://newsapi.org/v2";
const apiKey = "275e12acb26b4f98a775e901be4ce6db"
const endpoint = "/everything";

 const data ={
  news:[],
  search: '',
  loading: false
}


export default {
  data: function() {
    return data 
     

  },
   created() {
    this.loadNews();
  },

  methods: {
    loadNews(){
      if(this.search.length < 1) {
        return;
      }

      this.loading = true;
      this.news = [];

      let url = baseUrl + endpoint + '?q=' + this.search + '&apiKey=' + apiKey;

  axios.get(url).then(function(response) {
  console.log(response.data.articles)
  data.loading = false;
  data.news = response.data.articles
  }) .catch(function(error) {
      console.log(error.message)
  })
  }
  }
}
</script>
