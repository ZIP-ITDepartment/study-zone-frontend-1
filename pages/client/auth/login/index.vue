<template>
    <v-row justify="center" align="center">
        <v-col cols="3">
            <v-card dark :loading="loading">
                <v-card-title  class="text-xs-center">
                    <h1>STUDY ZONE</h1>
                </v-card-title>
                <v-container class="pa-5">
                    <v-form>
                        <v-row dense>
                            <v-col cols="12">
                                <v-text-field
                                    label="Email"
                                    type="email"
                                    prepend-icon="mdi-mail"
                                    dense
                                    v-model="form.email"
                                ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-text-field
                                    label="Password"
                                    type="password"
                                    prepend-icon="mdi-lock"
                                    dense
                                    v-model="form.password"
                                ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-btn color="info" block @click="clockIn">Login</v-btn>
                            </v-col>
                            <v-col cols="12">
                                <v-btn to="/client/auth/register" color="success" block>I dont have an account</v-btn>
                            </v-col>
                        </v-row>
                    </v-form>
                </v-container>
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
    export default {
        layout: 'auth',
        data () {
            return {
                loading: false,
                form: {
                    email: '',
                    password: ''
                }
            }
        },
        methods: {
            clockIn () {
                this.loading = true;
                this.$auth.loginWith('local', {
                    data: this.form
                }).then((response) => {
                    this.loading = false;
                    this.$router.push('/client/dashboard');
                })
            }
        }
    }
</script>