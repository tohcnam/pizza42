<template>

  <div  class="text-center" v-if="!$auth.isAuthenticated && !$auth.loading">
            <h1>Welcome at Pizza 42!</h1>
            You are not logged in, please log in to order a pizza. 
            <p></p>
  </div>

  <div  class="text-center" v-else-if="$auth.isAuthenticated">
            <h1>Welcome back {{ $auth.user.name }} at Pizza 42!</h1>
            
            <div v-if="$auth.user.email_verified">
              You are successfully logged in, please place an order to get a delicous pizza! 
              <br/><br/><br/>
              <a class="btn btn-lg btn-danger" href="#" @click="orderPizza()">Order Pizza</a>
            </div>
            
            <div v-else-if="!$auth.user.email_verified">
            You are successfully logged in. Before you can place an order, please first verify your Email.  
            </div>
            <p></p>
  </div>
  
</template>

<script>
export default {
  name: "HomeContent",
  install() {
    Vue.prototype.$http = axios;
  },
  methods: {
    async orderPizza() {
      const accessToken = await this.$auth.getTokenSilently({
        aud:'https://dev-rosenfeld.auth0.com/userinfo',
        scope: 'openid email'
      });
      const claims = await this.$auth.getIdTokenClaims();
      console.log(claims.__raw);

      try {
        await this.$http({
          method: 'post',
          //url: 'https://httpbin.org/post',
          url: 'http://localhost:8080/orderPizza',
          data: {
            type: 'salami',
            amount: 3
          },
          headers: {
            Authorization: `Bearer ${claims.__raw}`
          }
        })
        .then(response => {
          console.log(response);
          var message = "Thank you! You ordered " + response.data.amount + " " + response.data.type + " pizzas.";
          alert(message);
        });
      } catch (e) {
        this.apiMessage = `Error: the server responded with '${e.response.status}: ${e.response.statusText}'`;
      }
    }
  }
};  

</script>
