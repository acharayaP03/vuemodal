<template>
  <div class="relative mx-auto w-auto max-w-2xl">
    <div class="bg-white w-full p-6 flex flex-col">
      <div class="block mb-6">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Culpa amet itaque autem iusto possimus quisquam assumenda quia quo odio sapiente!          
        {{ message }}
`         </div>
      <div class="block w-full flex justify-end">
        <button 
          @click="toggle =!toggle"
          class="btn bg-blue-600 hover:bg-blue-800 px-6 py-2 ml-auto">
          close
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { eventBus } from '../main'
export default {
  name: 'HelloWorld',
  props:['toggleModal'],
  created(){
   eventBus.$on('connectevent', (data) =>{
        console.log(data);
      })  
  },
  data(){
    return{
      modal: this.toggleModal,
      message : null,
    }
  },
  methods:{
    openModal(){
      this.toggleModal = !this.toggleModal;
       eventBus.$on('connectevent', (data) =>{
         console.log('theh')
        this.message = data;
      }) 
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
