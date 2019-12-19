<template>
    <v-row dense justify="center" align="center">
        <v-col cols="12">
            <v-alert type="info" :value="true">
                <strong>Info!</strong>
            </v-alert>
        </v-col>
        <v-col cols="12">
            <v-card>
                <v-card-title>
                    Space List
                    <v-spacer></v-spacer>
                    <v-btn @click="addDialog = true" color="primary" small>Add Plan</v-btn>
                </v-card-title>
                <v-data-table
                    :headers="headers"
                    :items="datas"
                    disable-sort
                >
                    <template v-slot:item.status="{ item }">
                        <v-icon color="green" v-if="item.status">mdi-check</v-icon>
                        <v-icon color="red" v-else>mdi-close</v-icon>
                    </template>
                    <template v-slot:item.actions="{ item }">
                        <v-btn color="info" small>edit</v-btn>
                        <v-btn color="error" small>delete</v-btn>
                    </template>
                </v-data-table>
            </v-card>
        </v-col>

        <v-dialog v-model="addDialog" persistent max-width="350px">
            <v-card>
                <v-card-title>
                    <h4>Add Space</h4>
                    <v-spacer></v-spacer>
                    <v-btn icon @click="addDialog = false">
                        <v-icon>mdi-close</v-icon>
                    </v-btn>
                </v-card-title>
                <v-container>
                    <v-form>
                        <v-row dense>
                            <v-col cols="12">
                                <v-text-field
                                    label="Name"
                                    v-model="form.name"
                                ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-text-field
                                    label="Description"
                                    v-model="form.description"
                                ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-text-field
                                    label="Rate"
                                    v-model="form.rate"
                                ></v-text-field>
                            </v-col>
                            <v-col cols="12">
                                <v-btn @click="addSpace" block color="primary">Add</v-btn>
                            </v-col>
                        </v-row>
                    </v-form>
                </v-container>
            </v-card>
        </v-dialog>
    </v-row>
</template>

<script>
    export default {
        layout: 'admin',
        data () {
            return {
                addDialog: false,
                headers: [
                    { text: 'Name', align: 'left', value: 'name' },
                    { text: 'Description', align: 'center', value: 'description' },
                    { text: 'Hourly Rate (PHP)', align: 'center', value: 'rate'},
                    { text: 'Daily Rate (PHP)', align: 'center', value: 'daily_rate'},
                    { text: 'Capacity', align: 'center', value: 'capacity' },
                    { text: 'Actions', align: 'center', value: 'actions' }
                ],
                datas: [],
                form: {
                    name: '',
                    description: '',
                    rate: ''
                }
            }
        },
        async mounted () {
            await this.loadSpace();
        },
        methods: {
            async addSpace () {
                await this.$axios.$post('/space/store', this.form)
                    .then((response) => {
                        this.loadSpace();
                    })
            },
            async loadSpace () {
                await this.$axios.$get('/space/getAll')
                .then((response) => {
                    this.datas = response;
                })
                .catch(error => {
                    alert('Something went wrong');
                })
            }
        }
    }
</script>