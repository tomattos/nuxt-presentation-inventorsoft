<template>
  <div>
    <b-table v-if="gamers"
             striped
             hover
             :items="gamers"></b-table>
    <div v-else class="d-flex align-items-center justify-content-center mt-5">
      <h1>You can be first:)</h1>
    </div>
  </div>
</template>

<script>
export default {
    data() {
        return {
            gamers: []
        }
    },
    mounted() {
        this.gamers = JSON.parse(localStorage.getItem('gamers'));
    }
}
</script>
