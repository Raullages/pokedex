<template>
  <div class="container">
    <div class="row form-group">
      <div class="header col-xs-12 text-center">
        <h2>POKÉDEX</h2>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-10 col-sm-10 col-md-10 form-group" >
        <div class="row" v-if="pokemon == ''">
          <div class="col-xs-12 text-left">
            <h1>Choose a Pokemon</h1>
          </div>
        </div>
        <div class="row" v-if="pokemon != ''">
          <div class="col-xs-12 text-center">
            <img :src="pokemon.image" alt="" style="width: 180px; height: 180px">
            <h2>{{pokemon.name.toUpperCase()}}</h2>
          </div>
          <div class="col-xs-12">
            <pk-dados-pokemon :pokemon="pokemon" />
          </div>
        </div>
      </div>
        
      <div class="col-xs-2 col-sm-2 col-md-2">
        <div class="row">
          <pk-lista :lista_pokemons="lista_pokemons" :_height="_height" @click-caracteristica="(item) => caracteristicas(item)" />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
import pkLista from './lista.vue'
import pkDadosPokemon from './dados-pokemon.vue'
export default {
  components: { pkLista, pkDadosPokemon },
  data () {
    return {
      lista_pokemons: [],
      pokemon: '',
    }
  },

  computed: {
    _height () {
      let h = window.innerHeight

      return h
    }
  },
  
  mounted () {
    this.carregaLista().then( item => {
      this.lista_pokemons = item

    })
  },
  
  methods: {

    async carregaLista () {
      let list = []

      let lista = await this.carregaDados('https://pokeapi.co/api/v2/pokemon/?offset=0&limit=50')

      for(let i in lista.data.results){

        list.push(await this.carregaDados(lista.data.results[i].url))

      }

      let lista_completa = list.map((o, index) => {

        for(let i in lista.data.results){
          if(index == i){
            return {
              name: lista.data.results[i].name,
              url: lista.data.results[i].url,
              image: o.data.sprites.front_default,
              dados: o.data
            }
          }
        }

      })

      return lista_completa

    },

    caracteristicas (item) {

      this.pokemon = item

      this.$forceUpdate()

    },

    carregaDados (url) {

      return new Promise((resolve, reject) => {

        axios.get(url).then((lista) => {
          resolve(lista)
        })

      }).catch(err => {
        reject(err)
      })
    },
  }
}
</script>
<style scoped>
.header {
  border: 1px solid #000;
  border-radius: 15px;
  background-color: #343434;
  margin-top: 10px;
  padding: 5px;
}
.header h2 {
  margin: 0px;
  color: #FFF
}

h1{
  margin: 0
}

</style>