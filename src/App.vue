<template>
  <div id="app">
  <input v-model="search" type="text" placeholder="Search..">
  <button v-on:click="loadNews" type="button">search</button>

  <p v-if="loading">please wait..</p>
  

 <div v-for="article in news">
 <img v-if="article.urlToImage" :src="article.urlToImage" alt="">
 <h3>{{article.title}}</h3>
 <h4>{{article.author}}</h4>
 
 <p>
   {{article.description}}
 </p>
 <a class="button" :href="article.url" target="_blank">read more</a>
    
    
    
 </div>
</div>

    

  </div>
</template>

<script>
import axios from "axios"
const baseurl="https://newsapi.org/v2";
const apiKey="22bb3f5d182a4dea9af17695ae560035";
const endpoint="/everything";

const data ={
news:[],
search:"",
loading: false
}
export default {
  data: function() {
    return data;
  },
  created() {
      this.loadNews();
    
  },
  methods:{
  	loadNews(){
      if (this.search.length < 1 ){
        return;

      }
      this.loading = true; 
      this.news = [];
      let url =baseurl+endpoint+'?q='+ this.search + '&apiKey=' + apiKey

    axios.get(url).then(function(response ){
    console.log(response.data.articles)
    data.loading = false;
    data.news = response.data.articles
    }).catch(function(error){
    console.log(error.message)
    })
    }
}
}
</script>
