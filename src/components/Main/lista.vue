<template>
  <div>
    <transition name="component-fade">
      <div
        class="cards"
        v-if="lista_pokemons.length > 0"
      >
        <div
          class="cards-items"
          :class="{'active': choose.name === item.name}"
          v-for="(item, index) in lista_pokemons"
          :key="index"
        >
          <div>
            <a
              class="cards-items-info"
              href="#"
              @click.prevent="chooseIt(item)"
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
    </transition>  
  </div>
</template>
<script>
export default {
  props: ['lista_pokemons', '_height'],
  
  data() {
    return {
      choose: '',
    }
  },
  methods: {
    chooseIt(item) {
      console.log(item)
      this.choose = item
      this.$emit('click-caracteristica', item)
    } 
  }
}
</script>
<style scoped>
.cards {
  display: flex;
  overflow-x: auto;
}
.cards-items {
  flex: 1 0 150px;
  border: 1px solid #0240b3;
  margin: 5px 5px;
}
.cards-items-info{
  height: 130px;
  padding: 10px 0;
  text-decoration: none;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  border: 1px solid #000;
  align-items: center;
}
.cards-items-info > img {
  max-width: 80px;
  max-height: 80px
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

.active {
  background-color: #ffd00055;
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
component-fade-enter-active, .component-fade-leave-active {
  transition: opacity 1.3s ease;
}
.component-fade-enter, .component-fade-leave-to
/* .component-fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>