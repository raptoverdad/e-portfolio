<template>
  <nav>
    <div class="logo"><div><h1>Rodrigo Miranda</h1></div><div><img src="./assets/caraNoBackground.png" alt=""></div><div><h1>e-portfolio</h1></div></div>
    <div class="routerOptions">
      <router-link to="/">Home</router-link> 
      <router-link to="/about">About</router-link>
    </div>

  </nav>
  <router-view/>
  
</template>

<style scoped>
*{
  box-sizing: border-box;
  margin: 0;
padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;

}

.logo{
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  animation: logoAnimation 2s both infinite;
}
.routerOptions{
  display: flex;
  align-items: center;
  width: 100%;
}
.routerOptions a{
margin: 1%;
color: #f00;
text-decoration: none;
}
img{
  height: 25vh;
  width: 25vh;
  
}
nav {
  display: flex;
  background-color: #000;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: min-content;
  max-width: 100vw;
  overflow: hidden;
}
.logo div{
  background-color: transparent;
  width: 33.3%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Sedgwick Ave Display', cursive;
  font-size: xx-large;
  min-height: min-content;
}
.logo h1{
  color: #fff;
}
.routerOptions{
  width: 100%;
  height: 6vh;
  display: flex;
  justify-content: center;
  font-family: 'Sedgwick Ave Display', cursive;
  font-size: xx-large;
}
nav a.router-link-exact-active {
  color: #fff;
  filter: drop-shadow(0px 0px 20px #f00); 
  text-decoration: overline;
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
  .logo{
    flex-direction: column;
    text-align: center;
  }
  .logo h1{
    
  color: #fff;
  font-size: x-large;
}

}
</style>
