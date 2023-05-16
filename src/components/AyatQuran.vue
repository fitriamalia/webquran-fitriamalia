<template>
  <div class="ayat">
    <li v-for="item in ayatQuran">
      <p>{{ item.text_uthmani }}</p>
      <hr>
    </li>

    <footer class="text-black text-center pb-5">
      <p>&copy; 2023 <a href="#" class="text-black fw-bold">Al-Qur'an</a> &middot; Created by Fitri Amalia</p>
    </footer>
  </div>
</template>

<script>
import axios from 'axios';
import { ref } from 'vue';

export default {

  data() {
    return {
      ayatQuran: ref([])
    }
  },

  mounted() {
    this.getAyatQuran()
  },

  methods: {
    getAyatQuran() {
      axios.get(`https://api.quran.com/api/v4/quran/verses/uthmani?chapter_number=${this.$route.params.id}`)
          .then ((response) => {
            console.log(response)
            this.ayatQuran = response.data.verses
          }).catch((err) => {
        console.log(err)
      })
    }
  }
}

</script>

<style>

.ayat {
  text-align: right;
  padding-right: 20pt;
  font-size: 20pt;
  background-color: #74a662;
}

.text-black {
  font-size: 15pt;
}

</style>