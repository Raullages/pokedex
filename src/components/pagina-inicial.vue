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
          <div class="col-xs-12 text-center" style="display:flex; align-items: center; justify-content: center">
            <h1>Choose a Pokemon</h1>
          </div>
        </div>
        <div class="row" v-if="pokemon != ''">
          <div class="col-xs-12 text-center">
            <img :src="pokemon.image" alt="" style="width: 180px; height: 180px">
            <h2>{{pokemon.name.toUpperCase()}}</h2>
          </div>
          <div class="col-xs-12">
            <table class="table table-condensed">
              <tbody>
                <tr>
                  <td>
                    <div>
                      <label>Species:</label>
                      {{pokemon.dados.species.name.toUpperCase()}}
                    </div>
                    <hr>
                    <div>
                      <label>Types:</label>
                      <span class="label label-info" style="margin-right: 5px" v-for="(it, idx) in pokemon.dados.types" :key="idx">
                        {{it.type.name.toUpperCase()}}
                      </span>
                    </div>
                    <hr>
                    <div>
                      <label>Abilities:</label>
                      <span class="label label-primary" style="margin-right: 5px" v-for="(ability, idxAbility) in pokemon.dados.abilities" :key="idxAbility">
                        {{ability.ability.name}}
                      </span>
                    </div>
                    <hr>
                    <div>
                      <label>Base Experience:</label>
                      {{pokemon.dados.base_experience}}
                    </div>
                    <hr>
                     <div>
                      <label>Height:</label>
                      {{pokemon.dados.height}}
                    </div>
                    <hr>
                    <div>
                      <label>Weight:</label>
                      {{pokemon.dados.weight}}kg
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
        
      <div class="col-xs-2 col-sm-2 col-md-2">
        <div class="row">
          <div class="col-xs-12 lista-pokemon" :style="{'height': _height - 80 + 'px'}" v-if="lista_pokemons.length > 0">
              <ul v-for="(item, index) in lista_pokemons" :key="index">
                <li>
                  <a href="#" @click.prevent="caracteristicas(item, index)">
                    <img :src="item.image" alt="" style="width: 41px; height: 40px">
                    <span class="hidden-xs hidden-sm visible-md-* visible-lg-*">
                      {{item.name}}
                    </span>
                  </a>
                </li>
              </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
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

      let lista = await this.carregaDados('https://pokeapi.co/api/v2/pokemon/?offset=0&limit=200')
      let poks = []

      for(let i in lista.data.results){

        poks.push(await this.carregaDados(lista.data.results[i].url))

      }

      let lista_completa = poks.map((o, index) => {

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

    caracteristicas (item, index) {

      this.pokemon = item
      console.log(this.pokemon)

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

.lista-pokemon {
  background-color: #343434;
  border-radius: 10px;
  padding: 0px;
  margin: 0px;
  overflow-y: scroll;
  overflow-x: hidden;
}

.lista-pokemon ul {
  padding: 15px 0;
}

.lista-pokemon ul li {
  list-style: none;
  padding: 0;
}

.lista-pokemon ul li a{
  position: absolute;
  width: 100%;
  background-color: #343434;
  text-decoration: none;
  border:1px solid #343434;
  box-sizing: border-box;
  color: #FFF
}

.lista-pokemon ul li a:hover{
  border:1px solid #343434b2;
}

hr{
  margin: 5px 0;
}

</style>