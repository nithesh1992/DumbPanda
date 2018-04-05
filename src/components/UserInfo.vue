<template>
        <div>
           <div class="col"><h6> Connected as  {{user.Name}}</h6> </div>
        </div>
</template>

<script>
    export default {
        name: "UserInfo",
        props: {
            conn: Object
        },
        data: function () {
            return {
                con       : this.conn,
                user      : this.getUserDetails()
            }
        },
        methods: {
            getUserDetails : function() {
                var connection = this.conn;
                var query = "SELECT Id, Username, Name, CompanyName FROM User WHERE Id = \'" + connection.userInfo.id + "\'";
                console.log('Query: ', query);
                connection.query(query, (err, result) => {
                    if (err) { return console.error(err); }
                    console.log("total : " + result.totalSize);
                    console.log("fetched : " , result);
                    this.user = result.records[0];
                    console.log('User', this.user);
                });
            }
        }
    }
</script>

<style scoped>

</style>