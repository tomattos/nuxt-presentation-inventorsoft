<template>
  <div>
    <Header />
    <nuxt />
  </div>
</template>
<script>
    import Header from '../components/layout/Header';

    export default {
        components: {
            Header
        }
    }
</script>

<style>
  a {
    text-decoration: none;
  }
</style>
