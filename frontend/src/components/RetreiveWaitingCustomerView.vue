<template>

    <v-data-table
        :headers="headers"
        :items="retreiveWaitingCustomer"
        :items-per-page="5"
        class="elevation-1"
    ></v-data-table>

</template>

<script>
    const axios = require('axios').default;

    export default {
        name: 'RetreiveWaitingCustomerView',
        props: {
            value: Object,
            editMode: Boolean,
            isNew: Boolean
        },
        data: () => ({
            headers: [
                { text: "id", value: "id" },
            ],
            retreiveWaitingCustomer : [],
        }),
          async created() {
            var temp = await axios.get(axios.fixUrl('/retreiveWaitingCustomers'))

            temp.data._embedded.retreiveWaitingCustomers.map(obj => obj.id=obj._links.self.href.split("/")[obj._links.self.href.split("/").length - 1])

            this.retreiveWaitingCustomer = temp.data._embedded.retreiveWaitingCustomers;
        },
        methods: {
        }
    }
</script>

