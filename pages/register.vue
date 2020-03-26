<template>
  <div class="auth-page">
    <div class="container page">
      <div class="row">
        <div class="col-md-6 offset-md-3 col-xs-12">
          <h1 class="text-xs-center">Sign up</h1>

          <ul class="error-messages">
            <li v-for="(value,key,i) in errors" :key="i">{{key}}:{{value[0]}}</li>
          </ul>

          <form @submit.prevent="onRegister">
            <fieldset class="form-group">
              <input
                v-model="user.username"
                class="form-control form-control-lg"
                type="text"
                placeholder="Your Name"
              />
            </fieldset>
            <fieldset class="form-group">
              <input
                v-model="user.email"
                class="form-control form-control-lg"
                type="text"
                placeholder="Email"
              />
            </fieldset>
            <fieldset class="form-group">
              <input
                v-model="user.password"
                class="form-control form-control-lg"
                type="password"
                placeholder="Password"
              />
            </fieldset>
            <button class="btn btn-lg btn-primary pull-xs-right">Sign up</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  middleware:'noAuthenticated',
  async asyncData() {
    return {
      user: {
        password: "",
        email: "",
        username: ""
      },
      errors: {}
    };
  },
  data() {
    return {};
  },
  methods: {
    async onRegister() {
      try {
        const user = this.user;
        const { data } = await this.$axios.post("/api/users", { user });
        // console.log(data);
        this.$router.push('/')        
      } catch (error) {
        this.errors=error.response.data.errors;
        console.log(this.errors);
      }
    }
  },
  components: {}
};
</script>

<style lang="scss" scoped>
</style>
