<template>
  <div id="app">
    <div class="nav center row">
        <div>

        </div>
      <h5 class="nav-logo mt-sm-1">  <img src="https://image.ibb.co/gRtdex/logo.png" height="55" width="55">  </h5>
      <h1 class="mt-sm-1 pt-sm-1"> Dumb Panda </h1>
       <div class="right pull-right"> <UserInfo v-bind:conn="connection"  v-if="!showLogin"/> </div>
    </div>
    <LoginForm  @after-Click="Connect2SF" v-if="showLogin"/>
    <Alert v-bind:msg="errorMsg" type="error" v-if="showError" />
  </div>
</template>

<script>
import LoginForm from './components/LoginForm.vue'
import UserInfo  from './components/UserInfo.vue'
import Alert     from './components/Alert.vue'
export default {
  name: 'app',
  components: {
      LoginForm,
      UserInfo,
      Alert
  },
  data: function () {
    return {
        connection   : {},
        showError    : false,
        showLogin    : true,
        errorMsg     : ''
    }
  },
  methods: {
      Connect2SF: function (value) {
          var jsforce = require('jsforce');
          var conn = new jsforce.Connection({
              loginUrl : 'https://test.salesforce.com' //defaulting it to Sandboxes
          });
          this.connection = conn;
          conn.login(value.user, value.pass, (err) => {
              err? this.handleError(err) : this.postConnect(conn);
          });
      },

      handleError : function (msg){
          this.errorMsg  = msg.toString();
          this.showError = msg ? true : false;
          console.log(this.errorMsg);
          //console.error(this.errorMsg);
      },

      postConnect : function (conn) {
          this.showLogin  = false;
          this.connection = conn;
          console.log('SFDC Connection: ' , this.connection)
      }
  }
}
</script>

<style>
#app {
  @import url('https://fonts.googleapis.com/css?family=Chicle');
  @import url('https://fonts.googleapis.com/css?family=Open+Sans');
  @import url('https://use.fontawesome.com/releases/v5.0.9/js/all.js');
  @import 'assets/wing.css';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

}
</style>
