<template>
  <div id="app">
     <h1 class="titulo">TopArtist.es</h1>
     <br>
     <p>Selecciona el pais del que quieres ver la lista de los artistas más escuchados.</p>
     <br>
    <select class="selector" v-model="selectedCountry">
      <option v-for="country in countries" v-bind:value="country.value">{{ country.name }}</option>
    </select>
    <spinner v-show="loading"></spinner>
    <ul>
      <artist v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid"></artist>
    </ul>
    <p class="footer"> Esta web usa como fuente de sus datos <a href="https://last.fm/">Last.fm</a></p>
  </div>
</template>
<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        {name: 'Alemania', value: 'germany'},
        {name: 'Argentina', value: 'argentina'},
        {name: 'Bélgica', value: 'belgium'},
        {name: 'Brasil', value: 'brazil'},
        {name: 'Bolivia', value: 'bolivia'},
        {name: 'Colombia', value: 'colombia'},
        {name: 'Chile', value: 'chile'},
        {name: 'China', value: 'china'},
        {name: 'España', value: 'spain'},
        {name: 'Ecuador', value: 'ecuador'},
        {name: 'Francia', value: 'france'},
        {name: 'Portugal', value: 'portugal'}   
        ],
        selectedCountry: 'spain',
        loading: true
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshArtist() {
      const self = this
      this.loading = true
      this.artists = []
      getArtists(this.selectedCountry)
      .then(function (artists) {
        self.loading = false
        self.artists = artists
      })
    }
  },
  mounted() {
    this.refreshArtist()
  },
  watch: {
    selectedCountry: function() {
      this.refreshArtist()

    }
  }
}
</script>
<style>
 #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
   color:seagreen;
   text-align: center;
}
h1.titulo {
    margin: 0;
    font-size: 60px;
    color:seagreen;
    margin-top: 0;
    padding-top:0;
    font-weight: bolder;  
}
.titulo{
  background: #201f1f;
  margin-top:0;
  padding-top:0;
  height: 85px;

}
ul {
  list-style-type: none;
  padding-left: 2%;
  padding-right: 1%;
  overflow: hidden;
}
li {
  float: left; 
}
li a {
  display: block;
  text-align: center;
  padding: 16px;
  text-decoration: none;
  color: seagreen;
}
li:hover {
  background-color: #111111;
}
body{
  background:black;
  margin-top:0;
  padding-top: 0;
  margin-left: 0;
  margin-right: 0;
}
.footer{
  font-size: 0.7em;
  color:white;
}
.footer a{
  text-decoration: none;
  color:gray;
}
.selector, p{
  color: seagreen; 
}
.selector{
  width: 15%;
  height: 30px;
}
</style>
