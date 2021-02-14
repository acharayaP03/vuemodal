<template>
  <div class="home">
    <button class="btn p-4 bg-pink-500 hover:bg-pink-700" @click="sendEventMessage">Open Modal</button>

    <!-- Modal Background -->
    <div 
      v-if="toggleModal"
      class="fixed overflow-x-hidden overscroll-y-auto inset-0 flex justify-center items-center z-50"
    >
      <modal :toggle="toggle"></modal>
    </div>
    <div v-if="toggleModal" class="absolute inset-0 z-40 opacity-25 bg-black"></div>
  </div>
</template>

<script>
import { eventBus } from '../main'
import Modal from '@/components/Modal';
export default {
  name: 'Home',
  props:['toggle'],
  data(){
    return{
      toggleModal: false,
      connection: null,
    }
  },
  created(){
    console.log("Starting Connection to Websocket Server");
    this.connection = new WebSocket("wss://echo.websocket.org");

    //when connection is open 
    this.connection.onopen = function(event){
      console.log(event);
      console.log("Successfully connected to the echo WebSocket Server")
    }

    this.connection.onmessage = function(event){
      console.log(event)
    }
  },
  methods:{
    sendMessage(message){
      console.log(message);
      this.connection.send(message)
    },
    sendEventMessage(){
      this.toggleModal = !this.toggleModal
      eventBus.$emit('connectevent', 'Successfully connected to the echo WebSocket Server')
    }
  },
  components:{
    Modal
  },

}
</script>
