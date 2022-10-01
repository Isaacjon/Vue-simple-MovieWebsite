<template>
  <header>
    <router-link to="/">
      <h1><span>Vue</span>Movies</h1>
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
</template>

<script>
export default {
  name: "App",
  components: {},
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  &::selection {
    background: transparentize($color: #42b883, $amount: 0.5);
  }
}

body {
  background: #35495e;
  font-family: "Fira Sans", sans-serif;
}

a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background: #2c3d4e;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.1);
  width: 100%;
  overflow: hidden;
}

h1 {
  color: #fff;
  font-size: 28px;

  span {
    color: #42b883;
  }
}
</style>
