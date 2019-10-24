<template>
  <b-modal id="CongradModal"
           hide-footer
           v-model="show">
    <h3>Congratulation you kill Humster.<br /> Try one more time if you want!</h3>

    <b-btn @click="emitOneMoreTime">Try</b-btn>
  </b-modal>
</template>

<script>
    export default {
        name: "CongradModal",

        data() {
            return {
                show: false
            }
        },

        methods: {
            emitOneMoreTime() {
                this.show = false;
                this.$root.$emit('oneMoreTime');
            }
        }
    }
</script>

<style scoped>

</style>
