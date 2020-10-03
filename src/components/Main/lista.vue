<template>
  <div>
    <div
      class="cards"
      v-if="lista_pokemons.length > 0"
    >
      <div
        class="cards-items"
        v-for="(item, index) in lista_pokemons"
        :key="index"
      >
        <div>
          <a
            class="cards-items-info"
            href="#"
            @click.prevent="$emit('click-caracteristica', item)"
          >
            <img
              :src="item.image"
              alt=""
            >
            <span class="text-style hidden-xs hidden-sm visible-md-* visible-lg-*">
              {{item.name}}
            </span>
          </a>
        </div>
      </div>
    </div>
    <div v-else class="carregando">
      <h3>Loading...</h3>
    </div>
  </div>
</template>
<script>
export default {
  props: ['lista_pokemons', '_height'],
}
</script>
<style scoped>
.cards {
  display: flex;
  max-width: 1280px;
  overflow-x: auto;
  margin: 0 auto;
}
.cards-items {
  flex: 1 0 150px;
  border: 2px solid #0240b3;
  margin: 5px 5px;
  padding: 5px 0;
}
.cards-items-info{
  text-decoration: none;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.cards-items:hover{
  background-color: #ffd00055

}

.carregando {
  text-align: center;
}
.carregando h3{
  font-family: PokemonSolid;
  text-shadow: 1px 2px 1px #ffd000;
  color: #0240b3;
}

::-webkit-scrollbar-track {
  visibility: visible;
  width: 3px;
  background-color: #f0f0f0;
}
::-webkit-scrollbar {
  visibility: visible;
  height: 6px;
  width: 4px;
  background: #f0f0f0;
}
::-webkit-scrollbar-thumb {
  visibility: visible;
  background: #ffd000;
  border-radius: 3px;
}
</style>