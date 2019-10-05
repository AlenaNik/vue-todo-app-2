<template>
  <div id="app" class="container">
   <h1 class="title">TODOS</h1>
    <img src="./assets/logo.png" alt="vue logo" class="logo">
    <HelloWorld/>
    <Todo/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import Todo from './components/Todo.list.component';

export default {
  name: 'App',
  components: {
    HelloWorld,
    Todo,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
* {
    margin: 0;
    box-sizing: border-box;
  }
.container {
  max-width: 600px;
  margin: 0 auto;
}
.title {
  display: block;
  margin: 20px auto;
  font-size: 20px;
  color: aliceblue;
}
.logo {
  display: block;
  margin: 20px auto;
  height: 25px;
}

</style>
