<template>
  <div id="app">
      <nav class="nav navbar bg-dark" id="nav">
        <router-link to="/">Home</router-link>
      </nav>
      <div class="mt-1">
        <router-view />
      </div>
  </div>
</template>

<style lang="scss">
#app {
  font-family: 'Verdana', sans-serif;
  background-color: #e2e2e2;
  height: 100vh;
}
</style>
