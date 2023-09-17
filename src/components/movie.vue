<script setup>
import { ref, onMounted, watch, defineProps } from 'vue';

const props = defineProps({
  moviedata: Object, 
});
  
const moviedata = ref({
  Title:'',
  Poster:'',
  year:'',
  imdbID:'',
  Released:''
});
  
watch(() => props.moviedata, (newVal) => {
  moviedata.value = newVal;
});
  
</script>

<template>
  <div>
    <p>電影名稱: {{ moviedata.Title }}</p>
    <p>上映日期: {{ moviedata.Released || moviedata.year }}</p>
    <p>IMDB_ID: {{ moviedata.imdbID }}</p>
    <img :src="moviedata.Poster" alt="Movie Poster" />
  </div>
</template>







