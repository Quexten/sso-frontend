<template>
<v-content>
  <div style="text-align:center; padding-top:20px;">
    <h1 style="font-size: x-large" class="headline mb-0">Signin you in!</h1>
  </div>
</v-content>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
<script>
  export default {
    created: function () {
      this.$store.commit('setPrimaryAuthToken', this.$route.query.token)
      if (this.$store.getters.parsedPrimaryAuthToken.userId !== null) {
        this.$router.push('/signedIn')
      } else {
        this.$router.push('/login/createUser')
      }
    }
  }
</script>
