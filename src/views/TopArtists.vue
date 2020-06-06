<template>
  <div class="topartists">
    <vue-headful title="Top Artists"
    description="The top music artists in spain"/>
    <MenuCustom></MenuCustom>
    <div class="lds-facebook" v-show=!loading><div></div><div></div><div></div></div>
    <p v-show=!loading id="loading"> Loading, please wait...</p>
    <!--BARRA DE BÚSQUEDA POR NAME, GENDER, STATUS E ID-->
    <label for="bySearch" v-show="loading">
      Busca un artista: 
    <input v-model="search" type="search" name="bySearch" placeholder="Búsqueda...">
  </label>
    <TopArtistsTable :artists="filteredArtists" v-show="loading"></TopArtistsTable>
  </div>
</template>

<script>
//IMPORTANDO API DEL ARCHIVO /src/api/index.js
import api from '@/api/index.js'

import TopArtistsTable from '@/components/TopArtistsTable.vue'

import MenuCustom from '@/components/MenuCustom.vue'

export default {
  name: 'TopArtists',
  components: {
    TopArtistsTable, MenuCustom
  },
  data(){
    return {
      artists: [],
      loading: false,
      search: ''
    }
  },
  created(){
    api.getArtists().then(response => (this.artists = response.data.topartists.artist))
  },
  mounted () {
    setTimeout(() => {
      this.loading = true
    }, 2000)
  },
  computed: {
    filteredArtists(){
      // SI SEARCH ESTÁ VACÍO
      if(!this.search) {
        return this.artists
      }
      // SI SEARCH TIENE ALGO...
      return this.artists.filter( artist =>
        (artist.name.toLowerCase().includes(this.search.toLowerCase())
      ))
    }
  },
}
</script>

<style>
.lds-facebook {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-facebook div {
  display: inline-block;
  position: absolute;
  left: 8px;
  width: 16px;
  background: #fff;
  animation: lds-facebook 1.2s cubic-bezier(0, 0.5, 0.5, 1) infinite;
}
.lds-facebook div:nth-child(1) {
  left: 8px;
  animation-delay: -0.24s;
}
.lds-facebook div:nth-child(2) {
  left: 32px;
  animation-delay: -0.12s;
}
.lds-facebook div:nth-child(3) {
  left: 56px;
  animation-delay: 0;
}
@keyframes lds-facebook {
  0% {
    top: 8px;
    height: 64px;
  }
  50%, 100% {
    top: 24px;
    height: 32px;
  }
}
label {
  color: white;
  font-size: 1.3rem;
  font-weight: bold;
}
input {
  height: 1.8rem;
}
#loading {
  color: white;
  font-size: 1.3rem;
  font-weight: bold;
}
</style>