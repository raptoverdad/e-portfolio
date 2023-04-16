<template>
  <nav>
    <div class="logo"> <img src="./assets/caraNoBackground.png" alt=""></div>
    <div class="routerOptions">
      <router-link to="/">Home</router-link> 
      <router-link to="/about">About</router-link>
    </div>

  </nav>
  <router-view/>
</template>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.logo{
  background-color: #000;
}
.routerOptions{
  display: flex;
  align-items: center;
}
.routerOptions a{
margin: 10%;
}
img{
  height: 25vh;
  width: 25vh;
}
nav {
  padding: 30px;
  display: flex;
  background-color: aqua;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

nav a {
  font-weight: bold;
  color: #2c3e50;

}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
