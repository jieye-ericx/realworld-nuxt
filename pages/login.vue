<template>
  <div class="auth-page">
    <div class="container page">
      <div class="row">
        <div class="col-md-6 offset-md-3 col-xs-12">
          <h1 class="text-xs-center">Sign in</h1>
          <p class="text-xs-center">
            <nuxt-link to="/register">Have an account?</nuxt-link>
          </p>

          <ul class="error-messages">
            <li v-for="(value,key,i) in errors" :key="i">{{key}}:{{value[0]}}</li>
          </ul>

          <form @submit.prevent="onLogin">
            <fieldset class="form-group">
              <input v-model="user.email" class="form-control form-control-lg" type="text" placeholder="Email" />
            </fieldset>
            <fieldset class="form-group">
              <input v-model="user.password" class="form-control form-control-lg" type="password" placeholder="Password" />
            </fieldset>
            <button class="btn btn-lg btn-primary pull-xs-right">Sign in</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// process.server是Nuxt提供的api，判断当前环境
const Cookie = process.client ? require("js-cookie") : undefined;

export default {
  middleware:'noAuthenticated',
  async asyncData() {
    return {
      user: {
        password: "",
        email: ""
      },
      errors: {}
    };
  },
  data() {
    return {};
  },
  components: {},
  methods: {
    async onLogin() {
      try {
        const user = this.user;
        const { data } = await this.$axios.post("/api/users/login", { user });       
        Cookie.set('user',data.user)
        this.$store.commit('setUser',data.user)      
        this.$router.push('/')  
      } catch (error) {
        // this.errors=error.response.data.errors;
        console.log(error);
      }
    }
  },
};
</script>

<style lang="scss" scoped>
</style>
