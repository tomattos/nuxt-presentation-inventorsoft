<template>
  <b-navbar variant="info">
    <b-navbar-brand>
      <nuxt-link to="/">
        <img class="logo" src="../../assets/images/logo.png" alt="Logo">
      </nuxt-link>
    </b-navbar-brand>

    <b-navbar-nav class="ml-auto">
      <b-nav-item>
        <b-btn variant="primary"
               ref="btnShow"
               @click="openModal">Start</b-btn>
      </b-nav-item>
    </b-navbar-nav>

    <UserInfoModal />
    <CongradModal />
  </b-navbar>
</template>

<script>
    import UserInfoModal from '../ui/UserInfoModal';
    import CongradModal from '../ui/CongradModal';
    export default {
        name: "Header",
        components: {
            CongradModal,
            UserInfoModal
        },
        methods: {
            openModal() {
                this.$root.$emit('bv::show::modal', 'UserInfoModal');
            }
        }
    }
</script>

<style scoped>
  .logo {
    width: 60px;
    height: auto;
  }
</style>
