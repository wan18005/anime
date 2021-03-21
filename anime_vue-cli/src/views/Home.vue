<template>
<!-- default naturo poster-->  
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">  <!-- default naturo id-->
        <img src="https://i.pinimg.com/originals/8d/75/42/8d75425d53111dbf7e2423b1ddba4245.jpg" alt="Naruto Poster" class="featured-img" />
        <div class="detail">
          <h3>Naruto</h3> 
          <p>Many years ago, in the hidden village of Konoha, lived a great demon fox. When it swung one of it's nine tails, a tsunami occurred. The fourth hokage sealed this demon fox inside a boy in exchange for his own life. Naruto was that boy, and he grew up with no family, and the villagers hated him thinking that he himself was the demon fox. Naruto's dream is to become Hokage, and have the villagers acknowledge him.</p>
        </div>
      </router-link>
  </div>
<!-- Search bar -->  
    <form @submit.prevent="SearchMovies()" class="search-box">
    <input type="text" placeholder="What show are you looking for? " v-model="search"/>
    <input type="submit" value="Search" />
    </form>
<!-- List -->  
<div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
</div>
</template>

<script>
// @ is an alias to /src
import { ref } from 'vue';
import env from '@/env.js'
export default {
   setup () {
    const search = ref("");
    const movies = ref([]);
    const SearchMovies = () => {
      if (search.value !=""){
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`) // fetch api ${ from the env.js we have created} and set s to the search value
        .then(response =>response.json())// return as a json file
        .then(data => {
          movies.value = data.Search;
          search.value = "";
        });
      }
    }
    return {
      search, 
      movies,
      SearchMovies
    }

  }
}
</script>


<style lang="scss">
.home {
  .feature-card {
    position: relative;
    // cover
    .featured-img 
    {
      display: block;
      width: 50%;
      height: 50%;
      object-fit: cover;
      position: relative;
      margin-left: auto;
      margin-right:auto;

    }
    // detail in image
    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;
      // title
      h3 {
        color:#FFF;
        margin-bottom: 16px;
        text-align: center;
      }
      // paragraph
      p {
        color: #FFF;
      }
    }
  }
  // search box style
  .search-box 
  {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 20px;
    // 
    input 
    {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;
      &[type="text"] {
        width: 100%;
        color: #FFF;
        background-color: #496583;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;
        &::placeholder {
          color: #f3f3f3;
          text-align: center;
        }
        &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }
      }
      &[type="submit"] {
        width: 100%;
        max-width: 300px;
        background-color: #010008;
        padding: 16px;
        border-radius: 8px;
        color: #FFF;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;
        &:active {
          background-color: #3B8070;
        }
      }
    }
  }
  //movie list 
  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 10px 8px;
    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;
      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;
        .product-image {
          position: relative;
          display: block;
          img {
            display: block;
            width: 100%;
            height: 500px;
            object-fit: cover;
          }
          // little box in side movie
          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #010008;
            color: #FFF;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }
        // detail box 
        .detail {
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;
          .year {
            color: #FFF;
            font-size: 18px;
          }
          h3 {
            color: #FFF;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>