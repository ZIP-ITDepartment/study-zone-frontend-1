<template>
    <v-row dense>
        <v-col cols="12">
            <v-alert type="info" :value="true">
                <strong>Test</strong>
            </v-alert>
        </v-col>
        <v-col cols="12">
            <v-card>
                <v-card-title>Room Rentals</v-card-title>
                <v-data-table
                    :headers="[]"
                    :items="[]"
                    hide-actions
                    class="elevation-1"
                    select-all
                    pagination.sync="pagination"
                    item-key="id"
                    loading="true"
                    search="search"
                >
                    
                </v-data-table>
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
    export default {
        layout: 'admin'   
    }
</script>