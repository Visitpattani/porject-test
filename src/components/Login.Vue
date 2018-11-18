<template>
    <div>
        <div class="row">
            <div class="col s2 m4"></div>
            <div class="col s8 m4 login">
                <div class="card z-depth-2" style="padding: 30px;">
                    <h3>Login</h3>
                    <div class="row">
                        <div class="col-sm-2"></div>
                        <div class="col-sm-8">
                            <input type="text" v-model="email" placeholder="Email">
                            <input type="password" v-model="password" placeholder="Password">
                        </div>
                        <div class="col-sm-4"></div>
                         <div class="col m12" style="margin-top: 10px">
                        
                    </div>   
                                      
                    </div>
                     <a class="button is-rounded blue lighten-3 wave-light wave-effect btn-large" style="width:30%;margin:auto"  v-on:click="login">submit</a>
                    <p style="margin-top:30px">You don't have an account ? You can create one <router-link to="/sign-up">create one</router-link></p>
                </div>
            </div>
            <div class="col m4">

            </div>
        </div>
        
    </div>
</template>

<script>
    import firebase from 'firebase'
    export default {
        name: 'Login',
        data: function () {
            return {
                email: '',
                password: ''
            }
        },
        methods: {
            login: function () {
                firebase.auth().signInWithEmailAndPassword(this.email, this.password).then(
                    (user) => {
                        alert('Well done! You are now connected')
                        this.$router.replace('board')
                    },
                    function (err) {
                        alert('Oops. ' + err.message)
                    }
                )
            }
        }
    }
</script>
<style scoped>
    .login {
        margin-top: 30px;
        background-color: white;
        margin-top: 30vh;
    }
    input {
        margin: 10px 0;
        width: 20%;
        padding: 15px;
    }
    button {
        margin-top: 20px;
        width: 10%;
        cursor: pointer;
    }
</style>
