<template>
    <v-row justify="center" align="center">
        <v-col cols="3">
            <v-card dark>
                <v-card-title>Study Zone</v-card-title>
                <v-container class="pa-5">
                    <v-form>
                        <v-row dense>
                            <v-col cols="12">
                                <v-text-field
                                    label="Authorization Code"
                                    append-icon="mdi-send"  
                                    @click:append="send"
                                    outlined
                                ></v-text-field>
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
        methods: {
            send () {
                this.$router.push('/dashboard/admin');
            }
        }
    }
</script>