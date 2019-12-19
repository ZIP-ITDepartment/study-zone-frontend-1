<template>
    <v-row justify="center" align="center">
        <v-col cols="4">
            <v-card color="blue" class="pa-5">
                <v-list-item>
                    <v-list-item-avatar size="75px" color="black">
                        <v-icon size="50">mdi-cash-100</v-icon>
                    </v-list-item-avatar>
                    <v-list-item-content>
                        <v-list-item-title class="headline">{{ totalSoldCards }}</v-list-item-title>
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
                        <v-list-item-title class="headline">{{ totalNoOfCards }}</v-list-item-title>
                        <v-list-item-subtitle>Total Registered Card</v-list-item-subtitle>
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
                        <v-list-item-title class="headline">{{ totalActiveCards }}</v-list-item-title>
                        <v-list-item-subtitle>Total Active Cards</v-list-item-subtitle>
                    </v-list-item-content>
                </v-list-item>
            </v-card>
        </v-col>
        <v-col cols="12">
            <v-card>
                <v-card-title>
                    Card List
                    <v-spacer></v-spacer>
                    <add-card-modal />
                </v-card-title>
                <v-data-table
                    :headers="headers"
                    :items="cards"
                    disable-sort
                >
                    <template v-slot:item.discount="{ item }">
                        <i>{{ item.discount }}%</i>
                    </template>
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
    </v-row>
</template>

<script>
    import AddCardModal from '@/components/admin/card/AddCardModal.vue';
    export default {
        layout: 'admin',
        components: {
            AddCardModal
        },
        data () {
            return {
                headers: [
                    { text: 'Control #', align: 'left', value: 'control_no' },
                    { text: 'Type', align: 'center', value: 'type'},
                    { text: 'Date Activated', align: 'center', value: 'date_activated' },
                    { text: 'Date of Expiration', align: 'center', value: 'date_expired' },
                    { text: 'Discount (%)', align: 'center', value: 'discount' },
                    { text: 'Price', align: 'center', value: 'price' },
                    { text: 'Status', align: 'center', value: 'status' },
                    { text: 'Actions', align: 'center', value: 'actions' }
                ],
                cards: []
            }
        },
        computed: {
            totalSoldCards () {
                var temp = 0;
                
                this.cards.map(c => {
                    temp += c.price
                });

                return temp;
            },
            totalNoOfCards () {
                return this.cards.length;
            },
            totalActiveCards () {
                return this.cards.filter(c => c.status == true).length
            }
        },
        async mounted () {
            await this.$axios.$get('/card/getAllCards')
                .then((response) => {
                    this.cards = response
                })
                .catch(error => {
                    alert('Something wen\'t wrong');
                })
        }
    }
</script>