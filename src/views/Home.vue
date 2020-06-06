<template>
  <div class="home">
    <vue-headful title="Home"
    description="The homepage of hack a music app"/>
    <MenuCustom></MenuCustom>
    <div class="lds-facebook" v-show=!loading><div></div><div></div><div></div></div>
    <p v-show=!loading id="loading"> Loading, please wait...</p>
    <TopTagsTable :tags="tags" v-show=loading></TopTagsTable></TopTagsTable>
    </div>
</template>

<script>
//IMPORTANDO API DEL ARCHIVO /src/api/index.js
import api from '@/api/index.js'
import TopTagsTable from '@/components/TopTagsTable.vue'
import MenuCustom from '@/components/MenuCustom.vue'

export default {
  name: 'Home',
  components: {
    TopTagsTable, MenuCustom
  },
  data(){
    return {
      tags: [],
      loading: false
    }
  },
  mounted () {
    setTimeout(() => {
      this.loading = true
    }, 2000)
  },
  created(){
    api.getTopTags().then(response => (this.tags = response.data.tags.tag));
  }
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
#loading {
  color: white;
  font-size: 1.3rem;
  font-weight: bold;
}
</style>