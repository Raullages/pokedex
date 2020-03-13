<template>
    <div class="col-xs-12 lista-pokemon" :style="{'height': _height - 80 + 'px'}" v-if="lista_pokemons.length > 0">
        <ul v-for="(item, index) in lista_pokemons" :key="index">
        <li>
            <a href="#" @click.prevent="$emit('click-caracteristica', item)">
            <img :src="item.image" alt="" style="width: 41px; height: 40px">
            <span class="hidden-xs hidden-sm visible-md-* visible-lg-*">
                {{item.name}}
            </span>
            </a>
        </li>
        </ul>
    </div>
</template>
<script>
export default {
    props: ['lista_pokemons', '_height'],
    data () {
        return {

        }
    }
}
</script>
<style scoped>

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
</style>