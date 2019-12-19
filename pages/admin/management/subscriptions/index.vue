<template>
    <v-row justify="center" align="center">
        <v-col cols="4">
            <v-card color="blue" class="pa-5">
                <v-list-item>
                    <v-list-item-avatar size="75px" color="black">
                        <v-icon size="50">mdi-cash-100</v-icon>
                    </v-list-item-avatar>
                    <v-list-item-content>
                        <v-list-item-title class="headline">{{ totalNoOfSubscription }}</v-list-item-title>
                        <v-list-item-subtitle>Total Number of Subscriptions</v-list-item-subtitle>
                    </v-list-item-content>
                </v-list-item>
            </v-card>
        </v-col>
        <v-col cols="4">
            <v-card color="blue" class="pa-5">
                <v-list-item>
                    <v-list-item-avatar size="75px" color="black">
                        <v-icon size="50">mdi-cash-100</v-icon>
                    </v-list-item-avatar>
                    <v-list-item-content>
                        <v-list-item-title class="headline">{{ totalSubscriptionRevenue }}</v-list-item-title>
                        <v-list-item-subtitle>Total Number of Sold Cards</v-list-item-subtitle>
                    </v-list-item-content>
                </v-list-item>
            </v-card>
        </v-col>
        <v-col cols="4">
            <v-card color="blue" class="pa-5">
                <v-list-item>
                    <v-list-item-avatar size="75px" color="black">
                        <v-icon size="50">mdi-cash-100</v-icon>
                    </v-list-item-avatar>
                    <v-list-item-content>
                        <v-list-item-title class="headline">{{ totalActiveSubscription }}</v-list-item-title>
                        <v-list-item-subtitle>Total Number of Sold Cards</v-list-item-subtitle>
                    </v-list-item-content>
                </v-list-item>
            </v-card>
        </v-col>
        <v-col cols="12">
            <v-card>
                <v-card-title>
                    <h3>Subscription</h3>
                    <v-spacer></v-spacer>
                    <v-btn icon>
                        <v-icon>mdi-refresh</v-icon>
                    </v-btn>
                </v-card-title>
                <v-data-table
                    :headers="headers"
                    :items="subscriptions"
                    disable-sort
                >
                    <template v-slot:item.status="{ item }">
                        <v-chip v-if="item.status" color="green" small>Active</v-chip>
                        <v-chip v-else color="error" small>Inactive</v-chip>
                    </template>
                </v-data-table>
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
    import AddSubscriptionModal from '@/components/admin/subscription/AddSubscriptionModal.vue';
    export default {
        layout: 'admin',
        components: {
            AddSubscriptionModal
        },
        data () {
            return {
                headers: [
                    { text: 'Code', align: 'left', value: 'subscription_code' },
                    { text: 'Space', align: 'center', value: 'space.name' },
                    { text: 'Plan', align: 'center', value: 'plan'},
                    { text: 'Client', align: 'center', value: 'user.name' },
                    { text: 'Date Registered', align: 'center', value: 'date_registered'  },
                    { text: 'Date Expired', align: 'center', value: 'date_expired' },
                    { text: 'Price', align: 'center', value: 'price' },
                    { text: 'Status', align: 'center', value: 'status' },
                ],
                subscriptions: []
            }
        },
        computed: {
            totalNoOfSubscription () {
                return this.subscriptions.length;
            },
            totalSubscriptionRevenue () {
                var temp = 0;

                this.subscriptions.map(s => {
                    temp += s.price;
                });

                return temp;
            },
            totalActiveSubscription () {
                return this.subscriptions.filter(s => s.status == true).length;
            }
        },
        async mounted() {
            await this.$axios.$get('/subscription/getAllSubs')
                .then((response) => {
                    this.subscriptions = response;
                })
        },
    }
</script>