<template>
  <div>
    <!--<router-link v-if="user === null" to="/login" title="Login">-->
    <router-link to="/login" title="Login">
    <i class="fas fa-user-circle user my-2 fa-2x"></i>
    </router-link>
  </div>
</template>

<script>
export default {
  name: 'LoggedIn',
  data () {
    return {
      customer: {}
    }
  },
  methods: {
    logoutToggle () {
      var logoutBtn = document.getElementById('logout')
      if (logoutBtn.style.display === 'none') {
        logoutBtn.style.display = 'inline-block'
      } else {
        logoutBtn.style.display = 'none'
      }
    },
    userLogout () {
      let customerId = localStorage.getItem('customerId')
      this.$api.get('logout' + customerId)
        .then(res => {
          // localStorage.removeItem('customerId')
          this.$router.push('/logout')
        })
    }
  },
  mounted () {
    let customerId = localStorage.getItem('customerId')
    // console.log(customerId)
    this.$api.get('customer-info/' + customerId)
      .then(res => {
        // console.log(res)
        this.customer = res.data
      })
  }
}
</script>

<style scoped>
  .user-login {
    font-size: 18px;
    cursor: pointer;
  }
  .logout {
    display: none;
    padding: 5px 30px;
    font-size: 14px;
    font-weight: bold;
    /*cursor: pointer;*/
  }
</style>
