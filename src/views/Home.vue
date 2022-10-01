<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0409591">
        <img
          src="https://cdn.mos.cms.futurecdn.net/qupTjdwkfBNCoexeAE6bh4.jpg"
          alt="naruto poster"
          class="featured-img"
        />
        <div class="detail">
          <h3>{{ movies[0]?.Title }}</h3>
          <p>
            Life for former United Nations investigator Gerry Lane and his
            family seems content. Suddenly, the world is plagued by a mysterious
            infection turning whole human populations into rampaging mindless
            zombies. After barely escaping the chaos, Lane is persuaded to go on
            a mission to investigate this disease. What follows is a perilous
            trek around the world where Lane must brave horrific dangers and
            long odds to find answers before human civilization falls.
          </p>
          <p class="mb-0">
            Year: <span>{{ movies[0]?.Year }}</span>
          </p>
          <p class="mb-0">
            Type: <span> {{ movies[0]?.Type }}</span>
          </p>

          <!-- <pre>{{ movies[0] }}</pre> -->
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
            <h3 :title="movie.Title">{{ movie.Title }}</h3>
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
          ` https://www.omdbapi.com/?i=tt3896198&apikey=${env.apikey}&s=${search.value}`
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
        ` https://www.omdbapi.com/?i=tt3896198&apikey=${
          env.apikey
        }&s=${"world war"}`
      )
        .then((response) => response.json())
        .then((data) => {
          console.log(data.Search);
          // console.log(
          //   ` https://www.omdbapi.com/?i=tt3896198&apikey=${env.apikey}&s=${search.value}`
          // );
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
      // object-position: center;

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

      @media (max-width: 768px) {
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
          padding-bottom: 0 !important;
        }

        span {
          font-size: 14px;
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

    @media (max-width: 768px) {
      padding: 8px;
    }

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

        @media (max-width: 768px) {
          padding: 5px 8px;
          font-size: 14px;
        }

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

        @media (max-width: 768px) {
          padding: 5px 8px;
          font-size: 14px;
          max-width: 150px;
        }

        &:active {
          background: #38b070;
        }
        &:hover {
          box-shadow: 3px 3px 3px 2px rgba(0, 0, 0, 0.5);
        }
      }
    }
  }

  .movies-list {
    margin: 0;

    @media (max-width: 500px) {
      margin: 0;
    }

    .movie {
      width: 25%;
      max-width: 200px;
      margin: 0 0.75% 30px;
      box-shadow: 0 0 3px 4px rgba(0, 0, 0, 0.5);
      box-shadow: 3px 3px 3px 2px rgba(0, 0, 0, 0.5);
      transition: 0.4s;

      &:hover {
        filter: brightness(1.1);
        box-shadow: 3px 3px 3px 2px rgba(0, 0, 0, 0.5);
        box-shadow: 0 0 3px 4px rgba(0, 0, 0, 0.5);
      }
      //media
      @media (max-width: 1255px) {
        // width: 250px;
        margin: 0 0.75% 20px;
      }
      //media
      @media (max-width: 855px) {
        max-width: 180px;
      }
      //media
      @media (max-width: 768px) {
        max-width: 168px;
      }

      @media (max-width: 660px) {
        max-width: 145px;
        margin: 0 0.75% 10px;
      }

      @media (max-width: 585px) {
        max-width: 128px;
      }

      @media (max-width: 510px) {
        min-width: 150px;
        min-width: 31%;
        max-width: 215px;
        max-width: 31%;
      }

      @media (max-width: 471px) {
        min-width: 190px;
        min-width: 45%;
        max-width: 200px;
        max-width: 45%;
        margin: 0 1.5% 10px;
      }

      .product-img {
        position: relative;
        width: 100%;
        height: 280px;
        //media
        @media (max-width: 855px) {
          max-height: 220px;
        }

        @media (max-width: 585px) {
          max-height: 180px;
        }

        @media (max-width: 510px) {
          max-height: 200px;
        }

        @media (max-width: 471px) {
          max-height: 50vh;

          // width: 100%;
          // border: 10px solid red;
        }

        @media (max-width: 365px) {
          // max-height: 200px;
          max-height: 40vh;
        }

        @media (max-width: 394px) {
          // width: 100%;
          // max-height: 235px;
          // min-height: 235px;
        }

        img {
          width: 100%;
          height: 100%;
        }

        .type {
          position: absolute;
          padding: 8px 16px;
          background: #43b883;
          color: #fff;
          bottom: 16px;
          left: 0;
          text-transform: capitalize;

          @media (max-width: 855px) {
            // max-height: 220px;
            padding: 3px 10px;
            font-size: 12px;
          }
        }
      }

      .detail {
        padding: 5px;

        background: #496583;
        padding: 16px 8px;
        border-radius: 0 0 8px 8px;
        //media
        @media (max-width: 768px) {
          padding: 8px 8px;
        }
        .year {
          color: #aaa;
          font-size: 14px;
          margin-bottom: 5px;
          //media
          @media (max-width: 768px) {
            font-size: 12px;
          }
        }

        h3 {
          color: #fff;
          font-weight: 600;
          font-size: 18px;
          white-space: nowrap;
          margin-bottom: 0;
          overflow: hidden;

          //media
          @media (max-width: 768px) {
            font-size: 14px;
          }
        }
      }
    }

    // .movie {
    //   padding: 16px 8px;
    //   width: 100%;
    //   max-width: 25%;

    //   @media (max-width: 700px) {
    //     max-width: 33%;
    //   }

    //   @media (max-width: 480px) {
    //     max-width: 49%;
    //   }

    //   @media (max-width: 400px) {
    //     padding: 8px;
    //   }

    //   .movie-link {
    //     height: 100%;

    //     .product-img {
    //       position: relative;
    //       display: block;
    //       // flex-grow: 1;

    //       img {
    //         display: block;
    //         width: 100%;
    //         height: 100%;
    //         object-fit: cover;
    //       }

    //       .type {
    //         position: absolute;
    //         padding: 8px 16px;
    //         background: #43b883;
    //         color: #fff;
    //         bottom: 16px;
    //         left: 0;
    //         text-transform: capitalize;

    //         @media (max-width: 400px) {
    //           padding: 0px 8px;
    //           font-size: 12px;
    //         }
    //       }
    //     }

    //     .detail {
    //       background: #496583;
    //       padding: 16px 8px;
    //       flex: 1 1 100%;
    //       border-radius: 0 0 8px 8px;
    //       overflow: hidden;
    //       max-height: 100px;

    //       @media (max-width: 700px) {
    //         max-height: 88px;
    //       }

    //       @media (max-width: 400px) {
    //         padding: 10px 5px;
    //         max-height: 60px;
    //       }

    //       .year {
    //         color: #aaa;
    //         font-size: 14px;
    //         margin-bottom: 5px;

    //         @media (max-width: 400px) {
    //           font-size: 12px;
    //         }
    //       }

    //       h3 {
    //         color: #fff;
    //         font-weight: 600;
    //         font-size: 18px;
    //         white-space: nowrap;

    //         @media (max-width: 400px) {
    //           font-size: 14px;
    //           margin-bottom: 0;
    //         }
    //       }
    //     }
    //   }
    // }
  }
}
</style>