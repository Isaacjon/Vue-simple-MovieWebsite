<template>
  <div class="movie-detail d-flex flex-wrap flex-sm-nowrap gap-4">
    <img :src="movie?.Poster" alt="movie poster" class="featured-img" />
    <div class="texts d-inline">
      <h2 class="">{{ movie?.Title }}</h2>
      <span class="d-flex gap-4">
        <p><span> &#9733; </span> {{ movie?.Ratings[0]?.Value }}</p>
        <p>{{ movie?.Runtime }}</p>
      </span>
      <p>{{ movie?.Plot }}</p>
      <div class="infos">
        <p class=""><span> Country: </span> {{ movie?.Year }}</p>
        <p class=""><span>Genre: </span>{{ movie?.Genre }}</p>
        <p class=""><span>Release: </span>{{ movie?.Released }}</p>
        <p class=""><span>Director: </span>{{ movie?.Director }}</p>
        <p class=""><span>BoxOffice: </span>{{ movie?.BoxOffice }}</p>
        <p class=""><span>Actors: </span>{{ movie?.Actors }}</p>
        <p class=""><span>Language: </span>{{ movie?.Language }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount, onMounted } from "vue";
import { useRoute } from "vue-router";
import env from "@/env.js";
export default {
  setup() {
    const movie = ref({});
    const width = ref("10");
    const height = ref("10");
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `https://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`
      )
        .then((res) => res.json())
        .then((data) => {
          movie.value = data;
          // console.log(data);
        });
    });

    onMounted(() => {
      // console.log("beforemount ", window.outerHeight);
      window.outerHeight = height;
      window.outerWidth = width;
    });
    return {
      movie,
    };
  },
};
</script>

<style lang="scss" scoped>
.movie-detail {
  padding: 16px;

  h2 {
    color: #fff;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
  }

  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 16px;
    max-height: 300px;

    @media (max-width: 576px) {
      max-width: 100%;
      max-height: 100%;
      max-height: 250px;
    }
  }

  p {
    color: #fff;
    font-size: 18px;
    line-height: 1.4;
  }

  .texts {
    width: 100%;
    max-width: 60%;

    @media (max-width: 576px) {
      max-width: 100%;
      p {
        font-size: 14px;
        margin-bottom: 10px;
      }
    }
  }
  .infos {
    span {
      display: inline-block;
      width: 80px;
      margin-right: 10px;
      color: #aba9a9;
    }
  }
}
</style>