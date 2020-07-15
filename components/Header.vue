<template>
  <header class="c-header">
    <h1>{{ title }}</h1>
  </header>
</template>

<script>
export default {
  name: 'Header',
  props: {
    title: {
      type: String,
      required: false,
    },
  },
}
</script>

<style lang="scss">
header {
  background-color: #111;
  padding: 20px;
  color: white;
}
h1 {
  margin: 0 auto;
  text-transform: uppercase;
  text-align: center;
  font-size: 3rem;
  @media only screen and (max-width: 450px) {
    font-size: 2rem;
  }
}
</style>
