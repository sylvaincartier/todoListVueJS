<template>
    <div>
        <carrousel>
          <carrousel-slide v-for="n in slides" :index="n-1">
            <div class="textCarrousel">Slide {{n}}</div>
            <img :src="'https://picsum.photos/id/' + 100 + n + '/630/300'" width="100%'">
          </carrousel-slide>
        </carrousel>
        <button @click="addSlide">Ajouter un Slide</button>
        <button @click="removeSlide">Supprimer un Slide</button>
        <todos v-model="todos"></todos>
        <todos v-model="todos"></todos>
        <todos></todos>
        <button @click="addTodo">Ajouter une tâche</button>
    </div>
</template>

<script>
import Todos from './components/Todos'
import Carrousel from './components/carrousel/Carrousel'
import CarrouselSlide from './components/carrousel/CarrouselSlide'

export default {
  name: 'App',
  data () {
    return {
      slides: 5,
      todos: [{
        name: 'Demo',
        completed: true
      }]
    }
  },
  methods: {
    addTodo () {
      this.todos.push({
        name: 'Jean',
        completed: false
      })
    },
    addSlide () {
      this.slides++
    },
    removeSlide () {
      this.slides--
    }
  },
  components: {
    Todos,
    Carrousel,
    CarrouselSlide
  }
}
</script>

<style>
  .textCarrousel {
    position: absolute;
    left: 0;
    right: 0;
    text-align: center;
    top: 50%;
    color: #FFF;
    font-size: 16px;
  }

</style>
