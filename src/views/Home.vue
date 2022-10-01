<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img
          src="https://wallpaperaccess.com/full/6382993.png"
          alt="naruto poster"
          class="featured-img"
        />
        <div class="detail">
          <h3>Naruto</h3>
          <p>
            Naruto Uzumaki Lorem ipsum dolor sit amet consectetur, adipisicing
            elit. Fuga laudantium non molestiae doloribus omnis inventore earum
            temporibus? Illo, incidunt repellendus?
          </p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input
        type="text"
        placeholder="what are you looking for"
        v-model="search"
      />
      <input type="submit" value="Search" />
    </form>
    <div class="movies-list d-flex flex-wrap justify-content-center">
      <div class="movie rounded" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-img">
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
import { onMounted, ref } from "vue";
import env from "@/env.js";

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(
          ` http://www.omdbapi.com/?i=tt3896198&apikey=${env.apikey}&s=${search.value}`
        )
          .then((response) => response.json())
          .then((data) => {
            // console.log(data.Search);
            movies.value = data.Search;
            search.value = "";
          });
      }
    };
    onMounted(() => {
      fetch(
        ` http://www.omdbapi.com/?i=tt3896198&apikey=${
          env.apikey
        }&s=${"world war"}`
      )
        .then((response) => response.json())
        .then((data) => {
          console.log(data.Search);
          movies.value = data.Search;
          search.value = "";
        });
    });

    return {
      search,
      movies,
      SearchMovies,
    };
  },
};
</script>

<style lang="scss" scoped>
.home {
  .feature-card {
    position: relative;

    .featured-img {
      display: block;
      width: 100%;
      height: 500px;
      object-fit: cover;
      object-position: center;

      position: relative;
      z-index: 0;
    }

    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;

      @media (max-width: 400px) {
        padding: 8px;
      }

      h3 {
        color: #fff;
        margin-bottom: 16px;

        @media (max-width: 400px) {
          font-size: 14px;
        }
      }

      p {
        color: #fff;
        @media (max-width: 400px) {
          font-size: 12px;
        }
      }
    }
  }

  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type="text"] {
        width: 100%;
        color: #fff;
        background: #496583;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;

        &::placeholder {
          color: #f3f3f3;
        }

        &:focus {
          box-shadow: 0 3px 6px rgba(0, 0, 0, 0.2);
        }
      }

      &[type="submit"] {
        width: 100%;
        max-width: 200px;
        background: #42b883;
        padding: 5px 8px;
        border-radius: 8px;
        color: #fff;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;

        &:active {
          background: #38b070;
        }
      }
    }
  }

  .movies-list {
    // display: flex;
    // flex-wrap: wrap;
    margin: 0 8px;

    @media (max-width: 500px) {
      // max-width: 33%;
      margin: 0;
    }

    .movie {
      padding: 16px 8px;
      width: 100%;
      max-width: 25%;

      @media (max-width: 700px) {
        max-width: 33%;
      }

      @media (max-width: 480px) {
        max-width: 49%;
      }

      @media (max-width: 400px) {
        padding: 8px;
      }

      .movie-link {
        height: 100%;

        .product-img {
          position: relative;
          display: block;
          // flex-grow: 1;

          img {
            display: block;
            width: 100%;
            height: 100%;
            object-fit: cover;
          }

          .type {
            position: absolute;
            padding: 8px 16px;
            background: #43b883;
            color: #fff;
            bottom: 16px;
            left: 0;
            text-transform: capitalize;

            @media (max-width: 400px) {
              padding: 0px 8px;
              font-size: 12px;
            }
          }
        }

        .detail {
          background: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0 0 8px 8px;
          overflow: hidden;
          max-height: 100px;

          @media (max-width: 700px) {
            max-height: 88px;
          }

          @media (max-width: 400px) {
            padding: 10px 5px;
            max-height: 60px;
          }

          .year {
            color: #aaa;
            font-size: 14px;
            margin-bottom: 5px;

            @media (max-width: 400px) {
              font-size: 12px;
            }
          }

          h3 {
            color: #fff;
            font-weight: 600;
            font-size: 18px;
            white-space: nowrap;

            @media (max-width: 400px) {
              font-size: 14px;
              margin-bottom: 0;
            }
          }
        }
      }
    }
  }
}
</style>