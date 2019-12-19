<template>
    <v-row justify="center" align="center">
        <v-col cols="4" v-if="step == 1">
            <v-card>
                <v-card-title>
                    <h4>Transaction Type</h4>
                </v-card-title>
                <v-container>
                    <v-row>
                        <v-col cols="12">
                            <v-card @click="selectType('regular')" hover color="blue" class="pa-5">
                                <v-list-item>
                                    <v-list-item-avatar size="75px" color="grey"></v-list-item-avatar>
                                    <v-list-item-content>
                                        <v-list-item-title class="headline">Regular</v-list-item-title>
                                        <v-list-item-subtitle></v-list-item-subtitle>
                                    </v-list-item-content>
                                </v-list-item>
                            </v-card>
                        </v-col>
                        <v-col cols="12">
                            <v-card @click="selectType('subscription')" hover color="blue" class="pa-5">
                                <v-list-item>
                                    <v-list-item-avatar size="75px" color="grey"></v-list-item-avatar>
                                    <v-list-item-content>
                                        <v-list-item-title class="headline">Subscription</v-list-item-title>
                                        <v-list-item-subtitle></v-list-item-subtitle>
                                    </v-list-item-content>
                                </v-list-item>
                            </v-card>
                        </v-col>
                    </v-row>
                </v-container>
            </v-card>
        </v-col>
        <v-col cols="4" v-if="step == 2">
            <v-card v-if="form.type == 'regular'">
                <v-card-title>
                    <h3>SELECT SPACE</h3>
                    <v-spacer></v-spacer>
                    <v-btn @click="step -= 1" text>Go Back</v-btn>
                </v-card-title>
                <v-container>
                    <v-row>
                        <v-col cols="12" v-for="space in spaces" :key="space.id">
                            <v-card hover @click="selectedSpace(space)" color="blue" class="pa-5">
                                <v-list-item>
                                    <v-list-item-avatar size="75px" color="grey"></v-list-item-avatar>
                                    <v-list-item-content>
                                        <v-list-item-title class="headline">{{ space.name }}</v-list-item-title>
                                        <v-list-item-subtitle>Max. of {{ space.capacity }} pax</v-list-item-subtitle>
                                    </v-list-item-content>
                                </v-list-item>
                            </v-card>
                        </v-col>
                    </v-row>
                </v-container>
            </v-card>

            <v-card v-if="form.type == 'subscription'">
                <v-card-title>
                    <h3>Subscription</h3>
                    <v-spacer></v-spacer>
                    <v-btn @click="step -= 1" text>Go Back</v-btn>
                </v-card-title>
                <v-container>
                    <v-row>
                        <v-col cols="12">
                            <v-text-field
                                label="Subscription Code"
                                v-model="form.subscription_code"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="4"></v-col>
                        <v-col cols="12">
                            <v-btn @click="clockMeInNow" color="success" block>Clock In</v-btn>
                        </v-col>
                    </v-row>
                </v-container>
            </v-card>
        </v-col>
        <v-col cols="4" v-if="step == 3">
            <v-card dark>
                <v-card-title>
                    <h3>SELECT PLAN</h3>
                    <v-spacer></v-spacer>
                    <v-btn @click="step -= 1" text>Go Back</v-btn>
                </v-card-title>
                <v-container>
                    <v-row dense>
                        <v-col cols="12">
                            <v-select
                                label="Plans"
                                v-model="form.plan"
                                :items="['HP', 'DP']"
                                placeholder="Select Plan"
                            ></v-select>
                        </v-col>
                        <v-col cols="12" v-if="form.plan == 'HP'">
                            <v-text-field
                                label="No. of Hours"
                                v-model="form.duration"
                                type="number"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field
                                label="No. of Pax"
                                v-model="form.pax"
                                type="number"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-checkbox
                                label="With discount card?"
                                v-model="form.discount"
                            ></v-checkbox>
                        </v-col>
                    </v-row>
                </v-container>
                <v-card-actions>
                    <v-btn @click="clockMeIn()" color="primary" block>{{ form.discount == true ? 'Next' : 'Clock In' }}</v-btn>
                </v-card-actions>
            </v-card>
        </v-col>
        <v-col cols="4" v-if="step == 4">
            <v-card>
                <v-card-title>
                    <h3>Discount Card</h3>
                    <v-spacer></v-spacer>
                    <v-btn @click="step -= 1" text>Go Back</v-btn>
                </v-card-title>
                <v-container>
                    <v-row dense>
                        <v-col cols="12">
                            <v-text-field
                                label="Card Control No."
                                v-model="form.control_no"
                                placeholder="0000-0000-0000"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-btn @click="clockMeInNow" color="primary" block>Clock In</v-btn>
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
        middleware: ['auth'],
        data () {
            return {
                spaces: [],
                form: {
                    subscription_code: '',
                    type: '',
                    space_id: '',
                    pax: 0,
                    duration: 0,
                    plan: '',
                    control_no: '',
                    discount: false,
                },
                step: 1
            }
        },
        async mounted () {
            await this.loadSpaces();
        },
        methods: {
            async loadSpaces () {
                await this.$axios.$get('/space/getAll')
                    .then((response) => {
                        this.spaces = response;
                    })  
            },
            selectedSpace (space) {
                this.form.space_id = space.id;
                this.form.pax = space.capacity;
                this.step += 1;
                alert(this.form.space_id);
            },
            selectType (type) {
                this.form.type = type;
                this.step += 1;
                alert(space);
            },
            async clockMeIn () {
                if (this.form.discount) {
                    this.step += 1;
                } else {
                    await this.$axios.$post('/client/addTransaction', this.form)
                        .then((response) => {
                            alert('Transaction Added');
                            this.$auth.logout();
                        })
                        .catch(error => {
                            alert(error.response.data.message);
                        })
                }
            },
            async clockMeInNow () {
                await this.$axios.$post('/client/addTransaction', this.form)
                    .then((response) => {
                        alert('Transaction Added');
                        this.$auth.logout();
                    })
                    .catch(error => {
                        alert(error.response.data.message);
                    })
            }
        }
    }
</script>