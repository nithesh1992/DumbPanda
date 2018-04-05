<template>
    <div>
        <div class="container row">
            <div class="col-3 pl-sm-1"> <input type="email"    v-model="user"  placeholder="Sandbox Username"/> </div>
            <div class="col-3 pl-sm-1 horizontal-align"> <input type="password" v-model="pass"  placeholder="********"/> </div>
            <div class="right"> <button class='outline' v-on:click="connect" > Connect </button> </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "LoginForm",
        data: function () {
            return {
                user      : '',
                pass      : '',
                showError : false,
                showLogin : true,
                errorMsg  : 'Credentials Cannot be Empty!!'
            }
        },
        methods: {
            connect : function() {
                var credentials = { user: this.user, pass : this.pass};
                this.$emit('after-Click', credentials);
            }
        }
    }
</script>

<style scoped>

</style>