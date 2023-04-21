<template>
  <div class="home">

    <div class="chatBox">
      <div class="chatBoxInTheChatBox">
        <h1>{{ this.id }}</h1>
        <div class="chatMessage" v-for="item in messages"><h1 class="chatUser">{{item.user + ': '}}</h1><p class="chatUserMessage">{{item.mensaje}}</p></div>
      </div>
            <div class="chatOptions">
              <input class="messageInput" v-model="inputMessage" type="text">
              <input type="button" v-if="bossAvailable" v-on:click="sendMessage" class="sendButton" value="send">
              <input type="button" v-if="!bossAvailable" disabled class="sendButton" value="send">
            </div>

    </div>
    <section v-if="menuStatus">
       <div class="project">
        <h1>project 1</h1>
        <img class="project1" src="../assets/1.jpg" alt="">
        <p>I developed my first project entirely in JavaScript, with the aim of supporting the Raptoreum community and contributing to the wider crypto ecosystem. it's such an interesting game!. </p>

       </div>
       <div class="project">
        <h1>project 2</h1>
        <img src="../assets/phonefinder.png" alt="">
        <p>Telegram bot with typescript and vue. if you lost your phone, just talk to the phoneFinder bot from anywhere you are and he won't stop sending you messages until you found your phone. try it. it's free!.</p>
       </div>
       <div class="project">
        <h1>project 3</h1>
       </div>
    </section>

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
import { io } from 'socket.io-client';

const socket = io('http://localhost:3000/', {
  withCredentials: false,
  extraHeaders: {
    "Access-Control-Allow-Origin": null
  },
  query: {
    key: 'google'
  }
});


export default {
  name: 'HomeView',
  components: {
    HelloWorld
  },data(){
    return{
      chatStatus:"open chat",
      id:null,
      bossAvailable:true,
      menuStatus:true,
      messages:[],
      inputMessage:""
    }

},created(){
  socket.on('connect',()=>{
  console.log("socket connected")
  console.log("id: ", socket.id)
  localStorage.setItem("id",socket.id)
 this.id=socket.id
 socket.emit("isAvailableOrNot",this.id)
})

},mounted(){
 
  socket.on("isAvailableOrNotResponse",(data)=>{
    if(data=="yes"){
    this.bossAvailable=true

    }else{
      this.bossAvailable=false

    }
  })
socket.on('bossMessage',(datos)=>{
  let message=datos
  this.messages.push({user:"Rodrigo",message:message})
})

},
async destroyed(){
  await socket.emit("socketoff",this.id)
  alert("have a nice one!")
  localStorage.removeItem("id")
}
,
  methods:{
    toggleChat() {

      this.chatStatus = this.chatStatus === "open chat" ? "close chat" : "open chat";  
      if(this.chatStatus=="open chat"){
       this.menuStatus=true
        const arrows = document.querySelectorAll('.arrow');
        arrows.forEach(arrow => arrow.classList.remove('rotated'));
       
          document.querySelector('.chatBox').style.left="-1000000px"
      
       
      
      }else{
        this.menuStatus=false
        const arrows = document.querySelectorAll('.arrow');
        arrows.forEach(arrow => arrow.classList.add('rotated'))
        socket.emit("isAvailableOrNot",this.id)
     
        document.querySelector('.chatBox').style.left="0px"
       
        
    
      }
       
         },
         async sendMessage(){
         if(this.inputMessage==""){
          alert("You cannot leave the message field blank")
         }else{
          await socket.emit('message',JSON.stringify({id:this.id,message:this.inputMessage}))
          this.messages.push({user:"you",mensaje:this.inputMessage})
         }

          
         }
  }
}
</script>
<style scoped>
*{
  box-sizing: border-box;
  margin: 0;
padding: 0;
}
.chatBox{
  background-color: black;
  width: 100vw;
  height:87vh;
  position: absolute;
  bottom: 0;
  left: -100000px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-image: url('../assets/background.png');
  flex-direction: column;
  margin-bottom:13vh;
}
.chatOptions{
  display: flex;
  flex-direction: row;
}
.chatMessage{
  display: flex;
  align-items: center;
  max-width: 100%;
  word-wrap:break-word;
  padding: 1%;
}
.chatUserMessage{
  color: #fff;
  font-size: x-large;
  margin: 0;
  word-wrap:break-word;
  max-width: 70%;
  font-family: 'Ubuntu', sans-serif;
  padding-left:2%;
}
.chatBoxInTheChatBox{
width: 80%;
height: 90%;
background-color: #333;
overflow: scroll;
padding-bottom: 5%;
border: 5px solid red;
}
.chatUser{
  color: #fff;
  font-family: 'Sedgwick Ave Display', cursive;
}
.rotated {
  transform: rotate(180deg);
}
.project img{
  height: 40vh;
  width: 40vh;
  margin: 6%;
}

.footer {
  position: fixed; /* fija la posición del elemento */
  left: 0; /* fija la posición izquierda del elemento a 0 */
  bottom: 0; /* fija la posición inferior del elemento a 0 */
  max-width:100vw ;
  background-color: #000; /* establece un color de fondo */
  color: #fff; /* establece el color de texto */
  padding: 6px; /* añade un relleno para separar el contenido del borde */
  text-align: center; /* alinea el contenido al centro */
  height: 13vh;
  animation: logoAnimation 2s both infinite;
  min-width: 100vw;
}
.footer:hover{

transition: 1s;
}
.chatOptions input{
  font-family: 'Ubuntu', sans-serif;
  font-size: xx-large;
}
.home{
  max-width: 100vw;
  max-height: 100vh;
  overflow: hidden;
  margin: 0;
  padding: 0;
  left: 0;
}
.chatStatus{
  color: #fff;
  font-family: 'Sedgwick Ave Display', cursive;
}
.project{
  padding-top: 5%;
  display:flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  color: #f00;
  text-align: center;
  font-size: x-large;
  font-family: 'Ubuntu', sans-serif;
  width: 100%;
}
.project1{
  height: 40vh;
   min-width: 55vh;
}
.arrow{
  height: 5vh;
}
section{
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 0px; /*The space between grid containers*/
  grid-auto-rows:minmax(100vh,min-content);
  animation: background 3s infinite;
  background-color: #fff;
  width: 100%;
 overflow-x: hidden;
}
/* boton y caja de texto */
.sendButton{
  background-color: rgb(255, 0, 0);
  color: rgb(0, 0, 0);
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
}

.messageInput {
  border: 2px solid gray;
  border-radius: 5px;
  padding: 10px;
  font-size: 16px;
  width: 300px;
}
p{
  color: #000;
}

/* Cambio de estilo cuando el botón está en estado "hover" */
.sendButton:hover {
  background-color: lightblue;
  cursor: pointer;
}

/* Cambio de estilo cuando la caja de texto está enfocada */
.messageInput:focus {
  border: 2px solid blue;
  outline: none;
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

@media (max-width: 1200px) {
  section{
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  grid-auto-rows:repeat(3,minmax(100vh,min-content));
  animation: background 3s infinite;
  background-color: #fff;
  max-width: 100%;
 overflow-x: hidden;
 border:solid 5px #000;
}
.home{
  width: 100%;
  max-height: min-content;
  overflow: hidden;
}
.project img{
  height: 30vh;
  width: 30vh;
  margin: 4%;
}
section{
  width: 100%;
}
.project1{
  height: 40%;
   min-width: 80%;
}
.project p{
  font-size: 3vh;
  padding: 10%;
}
.chatOptions{
  display: flex;
  flex-direction: column;
}
.chatMessage{
  padding: 4%;
}
.chatBoxInTheChatBox{
width: 90%;
height: 70%;
background-color: #333;
overflow: scroll;
padding-bottom: 5%;
}
}

@media (max-width: 800px) {
  section{
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  grid-auto-rows:repeat(3,minmax(100vh,min-content));
  animation: background 3s infinite;
  background-color: #fff;
  max-width: 100%;
 overflow-x: hidden;
 border:solid 5px #000;
}
.home{
  width: 100%;
  max-height: min-content;
  overflow: hidden;
}
.project img{
  height: 30vh;
  width: 30vh;
  margin: 4%;
}
section{
  width: 100%;
}
.project1{
  height: 40%;
   min-width: 80%;
}
.project p{
  font-size: 3vh;
  padding: 10%;
}
.chatOptions{
  display: flex;
  flex-direction: column;
}
.chatMessage{
  padding: 4%;
}
.chatBoxInTheChatBox{
width: 100%;
height: 50%;
background-color: #333;
overflow: scroll;
margin: 0%;
}
.chatBox{
  background-color: black;
  width: 100vw;
  height:100vh;
  position: absolute;
  bottom: 0;
  left: -100000px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url('../assets/background.png');
  flex-direction: column;
  margin-bottom:-13vh;
  padding-bottom: 10%;
}
.chatOptions input{
  width: 97vw;
}
}

</style>