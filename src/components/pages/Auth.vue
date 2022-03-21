<template>
  <div class="auth">
      <label>Customer Key</label>
      <br>
      <input name="ckey" v-model="ckey"/>
      <br>
      <br>
      <label>SF URL</label><br>
      <input name="url" v-model="url"/>
      <br>
      <br>
      <label>Redirect URI</label><br>
      <input name="url" v-model="redirect_uri"/>
      <!-- <input />
      <input /> -->
      <br>
      <br>
      <button @click="initoAuth">Authenticate from SF</button>
      <p>{{ JSON.stringify(apijson, null, 2) }}</p>
  </div>
</template>

<script>

export default {
  name: 'Auth',

  components: {
  },

  data() {
    return {
      apijson: {},
      redirect_uri: 'https://sf-access-6d3e2d.netlify.app/auth',
      ckey: '3MVG9riCAn8HHkYWhCjpJsP6M7CogzJaVsFgPuLnx8ubjRUAWxfz2FwveQnigPmuOVM1p2khA_Mmqj03tqzjc',
      url: 'https://ec-expedite-dev-ed.my.salesforce.com/services/oauth2/authorize?',
    };
  },

  methods: {

      async initoAuth() {
        console.log('sdsd', this.$route.query.code);
        // const cKey = '3MVG9riCAn8HHkYWhCjpJsP6M7CogzJaVsFgPuLnx8ubjRUAWxfz2FwveQnigPmuOVM1p2khA_Mmqj03tqzjc';
        // const cSecret = '25D3EAE8C9C5DDE04365A4BF7087115DAA6E0597F79A617A1D5730D7542B7BAF';
        // const url = 'https://ec-expedite-dev-ed.my.salesforce.com/services/oauth2/authorize?';
        // const redirect_uri = 'https://sf-auth-0e7ad6.netlify.app/#/auth';
        this.apijson = {
          cKey: this.ckey,
          url: this.url,
          redirect_uri: this.redirect_uri,
        }
        console.log(this.apijson);
        // const response = await window.salesforceConnector.getoAuthCode(url, cKey, redirect_uri);
        window.location.replace(`${this.url}client_id=${this.ckey}&redirect_uri=${
            encodeURIComponent(this.redirect_uri)
        }&response_type=code`);        
      },

  },

}
</script>

<style scoped>
  input {
    width: 800px;
  }
</style>
