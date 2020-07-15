<template>
  <form class="c-search__form" @submit.prevent>
    <input v-model="childMessage" class="c-input" type="text" />
    <button class="c-form__button" @click="searchQuery">Search</button>
  </form>
</template>

<script>
export default {
  name: 'Search',
  data() {
    return {
      childMessage: '',
    }
  },
  methods: {
    searchQuery() {
      this.$emit('onChildToParent', this.childMessage)
    },
  },
}
</script>

<style lang="scss">
.c-search__form {
  display: flex;
  justify-content: center;
  padding-top: 2rem;
  padding-bottom: 2rem;
}
.c-form__button {
  background: green;
  border: none;
  border-radius: 40px;
  color: white;
  padding: 1rem 2.5rem;
  font-size: 1rem;
  font-family: 'Lato', sans-serif;
  font-weight: bold;
}
.c-input {
  border: none;
  border-radius: 40px;
  font-size: 1rem;
  margin-right: 2rem;
  padding: 1rem;
  font-family: 'Lato', sans-serif;
  @media only screen and (max-width: 600px) {
    margin-right: 0.5rem;
  }
}
</style>
