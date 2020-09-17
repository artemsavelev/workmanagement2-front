<template>
    <div class="wrapper-root">


        <div class="wrapper-list">

            <OrderItem />
        </div>

    </div>
</template>

<script>

    import OrderItem from "../components/OrderItem";


    export default {
        name: "OrderList",

        components: { OrderItem },


        data: () => ({
            //
        }),
    }
</script>

<style scoped>

</style>