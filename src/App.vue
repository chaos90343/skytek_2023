<script setup>
import axios from 'axios'
import { ref } from 'vue';
import movie from '@/components/movie.vue';

const singleMovieData = ref({});
const multiMovieData = ref([]);
const insert = ref('')
const insert1 = ref('')

const searchApi = async (url) => {
  try {
    const response = await axios.get(url)
    return response.data
  } catch (error) {
    console.error(error)
    return null
  }
}

const searchbtn = async () => {
  const data = await searchApi(`https://www.omdbapi.com/?i=tt3896198&apikey=14e57704&t=${insert.value}`)
  if (data) {
    singleMovieData.value = data;
  } else {
    singleMovieData.value = {};
  }
}

const searchbtnAll = async () => {
  const data = await searchApi(`https://www.omdbapi.com/?i=tt3896198&apikey=14e57704&s=${insert1.value}`)
  if (data && data.Search) {
    multiMovieData.value = data.Search;
  } else {
    multiMovieData.value = [];
  }
}

</script>

<template>
  <div>
    <p>電影查詢表(單筆查詢)</p>
    <div>
      <input v-model="insert">
      <button @click="searchbtn">查詢</button>
    </div>
    <movie v-if="singleMovieData.Title" :moviedata="singleMovieData"></movie>
    <p v-else>查無電影</p>
  </div>
  <div>
    <p>電影查詢表(多筆查詢)</p>
    <div>
      <input v-model="insert1">
      <button @click="searchbtnAll">查詢</button>
    </div>
    <div v-if="multiMovieData.length > 0" v-for="movie in multiMovieData" :key="movie.imdbID">
      <movie :moviedata="movie"></movie>
    </div>
    <p v-else>查無電影</p>
  </div>
</template>
