<template>
    <v-app id="inspire">
        <v-content>
            <v-container
                    class="fill-height"
                    fluid
            >
                <v-row
                        align="center"
                        justify="center"
                >
                    <v-col
                            cols="12"
                            sm="8"
                            md="4"
                    >
                        <v-card class="elevation-12">
                            <v-toolbar
                                    color="primary"
                                    dark
                                    flat
                            >
                                <v-toolbar-title>Login</v-toolbar-title>
                                <v-spacer/>
                            </v-toolbar>
                            <v-card-text>
                                <v-form>
                                    <v-text-field
                                            label="Login"
                                            name="login"
                                            prepend-icon="person"
                                            type="text"
                                            v-model="username"
                                    />

                                    <v-text-field
                                            id="password"
                                            label="Password"
                                            name="password"
                                            prepend-icon="lock"
                                            type="password"
                                            v-model="password"
                                    />
                                </v-form>
                            </v-card-text>
                            <v-card-actions>
                                <v-spacer/>
                                <v-btn color="primary" @click="onClickLogin">Login</v-btn>
                            </v-card-actions>
                        </v-card>
                        <v-alert v-model="showAlert" :type="alertType" dismissible>
                            {{alertText}}
                        </v-alert>
                    </v-col>
                </v-row>
            </v-container>
        </v-content>
    </v-app>
</template>

<script>
    import router from '../router'
    import {LOGGED_IN} from "../constants/constants";
    export default {
        name: 'login',
        data() {
            return {
                username: "admin",
                password: 'admin',
                alertType:'error',
                alertText:'I\'m an error alert.',
                showAlert:false,
            }
        },
        methods:{
            onClickLogin(){
                if(this.username === "admin" || this.username === "Admin")
                {
                    if(this.password === "admin" || this.password === "Admin"){
                        //success
                        this.showAlert = false;
                        localStorage.setItem(LOGGED_IN,'true');
                        router.push('/home')
                    }
                    else {
                        // check password
                        this.showAlert = true;
                        this.alertText="Check your password ( hint:admin )"
                    }
                }
                else {
                    //check username

                    this.showAlert = true;
                    this.alertText="Check your user name ( hint:admin )"
                }
            }
        },
        mounted() {
            if(localStorage.getItem(LOGGED_IN) === 'true')
            {
                router.push('/home')
            }
        }
    }
</script>
