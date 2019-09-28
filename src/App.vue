<template>
  <div id="app" class="container">
    <img src="./assets/logo.png" class="logo">
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
.logo {
  display: block;
  margin: 20px auto;
  height: 75px;
}

</style>
