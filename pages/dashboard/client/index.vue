<template>
    <v-row justify="center" align="center">
        <v-col cols="5">
            <v-card color="teal">
                <v-card-text>
                    <v-row>
                        <v-col cols="12">
                            <h1>Your transaction have been added! You will go back to login page in 5 seconds</h1>
                        </v-col>
                    </v-row>
                </v-card-text>
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
    export default {
        layout: 'client',
        mounted () {
            setTimeout(() => {
                this.$router.push('/auth/client/login')
            }, 5000)
        }
    }
</script>