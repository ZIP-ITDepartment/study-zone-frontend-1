<template>
    <v-row dense justify="center" align="center">
        <v-col cols="3">
            <v-card>
                <v-card-title>
                    Select Space
                </v-card-title>
                <v-container>
                    <v-row>
                        <v-col cols="12">
                            <v-card hover @click="selectedSpace(1)" color="blue" class="pa-5">
                                <v-list-item>
                                    <v-list-item-avatar size="75px" color="grey"></v-list-item-avatar>
                                    <v-list-item-content>
                                        <v-list-item-title class="headline">Hot Desk</v-list-item-title>
                                        <v-list-item-subtitle>Max. of 1 pax</v-list-item-subtitle>
                                    </v-list-item-content>
                                </v-list-item>
                            </v-card>
                        </v-col>
                        <v-col cols="12">
                            <v-card hover @click="selectedSpace(2)" color="blue" class="pa-5">
                                <v-list-item>
                                    <v-list-item-avatar size="75px" color="grey"></v-list-item-avatar>
                                    <v-list-item-content>
                                        <v-list-item-title class="headline">Private Space</v-list-item-title>
                                        <v-list-item-subtitle>Max. of 2 pax</v-list-item-subtitle>
                                    </v-list-item-content>
                                </v-list-item>
                            </v-card>
                        </v-col>
                        <v-col cols="12">
                            <v-card hover @click="selectedSpace(3)" color="blue" class="pa-5">
                                <v-list-item>
                                    <v-list-item-avatar size="75px" color="grey"></v-list-item-avatar>
                                    <v-list-item-content>
                                        <v-list-item-title class="headline">Conference Space</v-list-item-title>
                                        <v-list-item-subtitle>Max. of 10 pax</v-list-item-subtitle>
                                    </v-list-item-content>
                                </v-list-item>
                            </v-card>
                        </v-col>
                    </v-row>
                </v-container>
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
    export default {
        layout: 'client',
        methods: {
            selectedSpace(id) {
                switch (id) {
                    case 1: 
                        this.$router.push('/client/select-plan/open-desk-space');
                    break;

                    case 2:
                        this.$router.push('/client/select-plan/private-space');
                    break;

                    case 3:
                        this.$router.push('/client/select-plan/conference-space');
                    break;
                }
            }
        }
    }
</script>