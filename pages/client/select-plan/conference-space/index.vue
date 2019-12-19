<template>
    <v-row justify="center" align="center">
        <v-col cols="3">
            <v-card dark>
                <v-card-title>
                    <h2>SELECT PLAN</h2>
                </v-card-title>
                <v-container>
                    <v-row dense>
                        <v-col cols="12">
                            <v-select
                                label="Plans"
                                v-model="form.plan"
                                :items="['Hourly Plan', 'Daily Plan']"
                            ></v-select>
                        </v-col>
                        <v-col cols="12" v-if="form.plan == 'Hourly Plan'">
                            <v-text-field
                                label="No. of Hours"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field
                                label="No. of Pax"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-checkbox
                                label="With discount card?"
                                required
                            ></v-checkbox>
                        </v-col>
                    </v-row>
                </v-container>
                <v-card-actions>
                    <v-btn to="/client/dashboard" color="primary" block>Clock In</v-btn>
                </v-card-actions>
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
    export default {
        layout: 'client',
        data () {
            return {
                form: {
                    plan: ''
                }
            }
        }
    }
</script>