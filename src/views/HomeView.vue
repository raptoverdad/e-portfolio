<template>
  <div class="home">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <div class="chatBox">

    </div>
    <div class="footer" v-on:click="toggleChat()">
      <div class="animation">
        <img class="arrow" src="../assets/flecha1png.png" alt="">
        <img class="arrow" src="../assets/flecha1png.png" alt="">
        <img class="arrow" src="../assets/flecha1png.png" alt="">
      </div>
      <div class="chatTittle">
        <h1 class="chatStatus">{{chatStatus}}</h1>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  },data(){
    return{
      chatStatus:"open chat"
    }

}
,
  methods:{
    toggleChat() {
      this.chatStatus = this.chatStatus === "open chat" ? "close chat" : "open chat";  
      if(this.chatStatus=="open chat"){
        document.querySelector('.arrow')
        const arrows = document.querySelectorAll('.arrow');
        arrows.forEach(arrow => arrow.classList.remove('rotated'));
      }else{
        const arrows = document.querySelectorAll('.arrow');
        arrows.forEach(arrow => arrow.classList.add('rotated'))
      }
       
       
         }
  }
}
</script>
<style scoped>
*{
  box-sizing: border-box;
margin: 0;
}
.chatBox{
  background-color: black;
  width: 100%;
  height:100vh;
  position: absolute;
  bottom: 0;
  left: -1000000px;
}
.rotated {
  transform: rotate(180deg);
}
.footer {
  position: fixed; /* fija la posición del elemento */
  left: 0; /* fija la posición izquierda del elemento a 0 */
  bottom: 0; /* fija la posición inferior del elemento a 0 */
  width: 100%; /* fija el ancho del elemento al 100% del ancho de la pantalla */
  background-color: #000; /* establece un color de fondo */
  color: #fff; /* establece el color de texto */
  padding: 10px; /* añade un relleno para separar el contenido del borde */
  text-align: center; /* alinea el contenido al centro */
}
.footer:hover{
  animation: logoAnimation 2s both infinite;
transition: 1s;
}
.home{
  max-width: 100vw;
  max-height: 100vh;
  overflow: hidden;
}
.chatStatus{
  color: #fff;
  font-family: 'Sedgwick Ave Display', cursive;
}
.arrow{
  height: 5vh;
}
@keyframes logoAnimation {
  0%{
    filter: drop-shadow(0px 0px 0px #000); 
  }50%{
    filter: drop-shadow(0px 0px 20px #f00); 
  }100%{
    filter: drop-shadow(0px 0px 0px #000); 
  }
}

</style>