<template>
    <v-row>
        <v-col cols="4">
            <v-card color="blue" class="pa-5">
                <v-list-item>
                    <v-list-item-avatar size="75px" color="grey"></v-list-item-avatar>
                    <v-list-item-content>
                        <v-list-item-title class="headline">Our Changing Planet</v-list-item-title>
                        <v-list-item-subtitle>by Kurt Wagner</v-list-item-subtitle>
                    </v-list-item-content>
                </v-list-item>
            </v-card>
        </v-col>
        <v-col cols="4">
            <v-card color="blue" class="pa-5">
                <v-list-item>
                    <v-list-item-avatar size="75px" color="grey"></v-list-item-avatar>
                    <v-list-item-content>
                        <v-list-item-title class="headline">Our Changing Planet</v-list-item-title>
                        <v-list-item-subtitle>by Kurt Wagner</v-list-item-subtitle>
                    </v-list-item-content>
                </v-list-item>
            </v-card>
        </v-col>
        <v-col cols="4">
            <v-card color="blue" class="pa-5">
                <v-list-item>
                    <v-list-item-avatar size="75px" color="grey"></v-list-item-avatar>
                    <v-list-item-content>
                        <v-list-item-title class="headline">Our Changing Planet</v-list-item-title>
                        <v-list-item-subtitle>by Kurt Wagner</v-list-item-subtitle>
                    </v-list-item-content>
                </v-list-item>
            </v-card>
        </v-col>
        <v-col cols="12">
            <v-card>
                <v-card-title>
                    <h3>Clients</h3>
                    <v-spacer></v-spacer>
                    <v-btn icon>
                        <v-icon>mdi-refresh</v-icon>
                    </v-btn>
                </v-card-title>
                <v-data-table
                    :headers="headers"
                    :items="users"
                >
                    <template v-slot:item.actions="{ item }">
                        <add-subscription-modal :user="item" />
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
                    { text: 'User ID', align: 'left', value: 'id' },
                    { text: 'Full name', align: 'center', value: 'name' },
                    { text: 'Email', align: 'center', value: 'email' },
                    { text: 'Organization', align: 'center', value: 'organization' },
                    { text: 'Contact No.', align: 'center', value: 'contact_no' },
                    { text: 'Actions', align: 'center', value: 'actions' }
                ],
                users: []
            }
        },
        async mounted() {
            await this.$axios.$get('/user/getAllUsers')
                .then((response) => {
                    this.users = response;
                })
        },
        methods: {
            
        }
    }
</script>