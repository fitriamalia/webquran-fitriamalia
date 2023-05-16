<template>

  <div class="surah">
    <h1 class="title"><u>List Surah</u></h1>
    <li v-for="item in listSurah">
      <h3>{{ item.id + '. ' + item.name_simple + ' (' + item.translated_name.name + ')'
      + ' | ' + item.verses_count + ' Ayat' }}</h3>
      <h2 class="name_arabic">{{ item.name_arabic }}</h2>
      <router-link :to="{name: 'surah', params: {id: item.id}}" class="baca">Baca Surah</router-link> <hr>
    </li>

    <footer class="text-black text-center pb-5">
      <p>&copy; 2023 <a href="#" class="text-black fw-bold">Al-Qur'an</a> &middot; Created by Fitri Amalia</p>
    </footer>
  </div>
</template>

<script>
import axios from 'axios'
import { ref } from 'vue'

export default {

  data() {
    return {
      listSurah: ref([])
    }
  },

  mounted() {
    this.getListSurah()
  },

  methods: {
    getListSurah() {
      axios.get('https://api.quran.com/api/v4/chapters?language=id')
          .then((response) => {
            console.log(response)
            this.listSurah = response.data.chapters
          }).catch ((err) => {
        console.log(err)
      })
    }
  }
}

</script>

<style>

.surah {
  background-color: #76a973;
}

li {
  list-style: none;
  padding-left: 20pt;
  padding-top: 20pt;
}

.title {
  text-align: center;
  font-weight: bold;
  text-transform: uppercase;
  font-size: 35pt;
}

.name_arabic {
  float: right;
  padding-right: 20pt;
}

.baca {
  font-size: 15pt;
  padding-left: 420pt;
  -webkit-text-fill-color: white;
}

.text-black {
  font-size: 15pt;
}

</style>