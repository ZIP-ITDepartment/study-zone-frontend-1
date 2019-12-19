<template>
    <v-row justify="center" align="center">
        <v-col cols="3">
            <v-card dark>
                <v-card-title class="flex">
                    <v-row justify="center" align="center">
                        <h1>Study Zone</h1>
                    </v-row>
                </v-card-title>
                <v-container class="pa-5">
                    <v-form>
                        <v-row dense>
                            <v-col cols="12">
                                <v-text-field
                                    v-model.trim="form.name"
                                    label="Full Name"
                                    type="text"
                                    prepend-icon="mdi-pencil"
                                    dense
                                ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-text-field
                                    v-model="form.organization"
                                    label="School/Company/Organization"
                                    type="text"
                                    prepend-icon="mdi-school"
                                    dense
                                ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-text-field
                                    v-model.trim="form.contact_no"
                                    label="Contact No."
                                    type="text"
                                    prepend-icon="mdi-phone"
                                    dense
                                ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-text-field
                                    v-model.trim="form.email"
                                    label="Email"
                                    type="email"
                                    prepend-icon="mdi-mail"
                                    dense
                                ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-text-field
                                    v-model.trim="form.password"
                                    label="Password"
                                    type="password"
                                    prepend-icon="mdi-lock"
                                    dense
                                ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-btn @click="register" color="info" block>create account</v-btn>
                            </v-col>
                            <v-col cols="12">
                                <v-btn to="/auth/client/login" color="success" block>I already have an account</v-btn>
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
                form: {
                    name: '',
                    organization: '',
                    contact_no: '',
                    email: '',
                    password: ''
                },
                errors: []
            }
        },
        methods: {
            register () {
                this.$axios.$post('/auth/register', this.form)
                    .then((response) => {
                        this.$router.push('/client/auth/login');
                        alert(response.data)
                    })
                    .catch(error => {
                        this.errors = [];
                        this.errors.push(error.response.data.errors);
                        console.log(this.errors);
                    })
            }
        }
    }
</script>