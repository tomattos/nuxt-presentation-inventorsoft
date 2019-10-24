<template>
  <div>
    <Playground />
  </div>
</template>

<script>
    import Playground from '../../components/ui/Playground';
    export default {
        name: "player",
        components: {
            Playground
        },
        // validate({ params, query, store }) {
        //     if (!process.server){
        //         const gamers = JSON.parse(localStorage.getItem('users'));
        //         return gamers.some((gamer) => gamer.login === params.player);
        //     }
        //     return true;
        // }
    }
</script>

<style scoped>

</style>
