<template>
  <div class="topartiststable">
   <ul>
      <li v-for="artist in artists" :key="artist.id">
        <a :href="artist.url"><section>
        <p>ARTIST: {{ artist.name }}</p>
        <p>OYENTES: {{ artist.listeners }}</p>
        </section>
        <img :src='urlImagen + artist.name'></a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TopArtistsTable',
  props: {
    artists: Array
  },
  data(){
    return {
      urlImagen : 'https://source.unsplash.com/random/400x200/?music,genre,'
    }
  }
}
</script>

<style scoped>
.toptagstable {
  
}
ul {
  list-style-type: none;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 0;
}
li {
  margin: 0.334rem;
  position: relative;
  color: white;
  font-weight: bold;
}
a{
    color: white;
  font-weight: bold;
  text-decoration: none;
}
p {
  background-color: rgba(0, 0, 0, 0.288);
}
section {
  min-width: 100%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
img {
  max-width: 300px;
  max-height: 200px;
  border: 5px black solid;
}
</style>
