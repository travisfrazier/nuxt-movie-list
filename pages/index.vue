<template>
  <div class="container">
    <Header :title="title" />
    <MovieList />
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: 'Movie Watch List',
    }
  },
}
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
  background: #222;
  font-family: 'Lato', sans-serif;
}
button {
  &:hover {
    cursor: pointer;
    color: black;
  }
}

h1,
h2,
h3,
h4,
h5 {
  font-family: 'Modak', cursive;
  font-weight: 400;
}
</style>
