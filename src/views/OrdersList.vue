<template>
    <div>

        <div>
            <OrderItem v-for="order in allOrders"
                       :key="order.id"
                       v-bind:order="order"
                       v-bind:editOrder="editOrder"/>

        </div>

    </div>
</template>

<script>


    import OrderItem from "../components/OrderItem";
    import {mapActions, mapGetters} from "vuex";


    export default {
        name: "OrdersList",
        computed: mapGetters(['allOrders']),
        components: { OrderItem },


        data: () => ({
            ...mapActions(['fetchOrders']),

            order:[]

        }),
        methods: {
            editOrder(item) {
                this.order = item;
            },


        },
        mounted() {
            this.fetchOrders();
        },


    }
</script>

<style scoped>


</style>