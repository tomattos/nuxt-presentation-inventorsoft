<template>
  <b-modal id="UserInfoModal"
           title="Create new user"
           hide-footer
           v-model="show"
           @hidden="reset">
    <b-form @submit.prevent="saveInfo">
      <b-form-group label="Login">
        <b-form-input v-model="form.login" />
      </b-form-group>

      <b-btn type="submit" variant="success">Save</b-btn>
    </b-form>
  </b-modal>
</template>

<script>
    export default {
        name: "UserInfoModal",
        data() {
            return {
                show: false,
                form: {
                    login: null
                }
            }
        },
        methods: {
            saveInfo() {
                /* create new user */
                const gamers = JSON.parse(localStorage.getItem('gamers'));
                const newGamer = {
                    login: this.form.login,
                    score: 0,
                    id: gamers !== null ? gamers[gamers.length - 1].id + 1 : 0
                };
                const updatedGamers = JSON.stringify([...gamers || [], newGamer]);

                localStorage.setItem('gamers', updatedGamers);

                /* close modal */
                this.show = false;
                this.$router.push(`/play/${newGamer.login}`);
            },

            reset() {
                this.form.login = null;
            }
        }
    }
</script>

<style scoped>

</style>
