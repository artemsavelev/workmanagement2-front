<template>
    <v-container class="pa-0">



        <div class="main">

            <div class="main-container">
                <div class="main-container-wrapper pa-1 column-70">
                    {{ order.id }}
                </div>

                <div class="main-container-wrapper pa-1 column-70">
                    {{ order.extId }}
                </div>

                <div class="main-container-wrapper pa-1 column-100">
                    <v-tooltip bottom>
                        <template v-slot:activator="{ on }">
                            <span v-on="on">{{ order.createdDate }}</span>
                        </template>
                        <span>Дата создания: {{ order.createdDate }}</span>
                    </v-tooltip>

                </div>

                <div class="main-container-wrapper pa-1 column-100">
                    <v-tooltip bottom>
                        <template v-slot:activator="{ on }">
                            <span v-on="on">{{ order.startDate }}</span>
                        </template>
                        <span>Дата начала работ: {{ order.startDate }}</span>
                    </v-tooltip>
                </div>

                <div class="main-container-wrapper pa-1 column-150">
                    <v-tooltip bottom>
                        <template v-slot:activator="{ on }">
                            <span v-on="on">{{ order.workGroup.groupList }}</span>
                        </template>
                        <span>{{ order.workGroup.groupList }}</span>
                    </v-tooltip>
                </div>

                <div class="main-container-wrapper pa-1 column-200">
                    <span v-for="(user, idx) in order.executors" :key="idx">

                    <v-tooltip bottom>
                        <template v-slot:activator="{ on }">
                            <span v-on="on"> {{ user.lastName }},</span>
                        </template>
                        <span>{{ user.lastName }}</span>
                    </v-tooltip>

                    </span>
                </div>

                <div class="main-container-wrapper pa-1 column-300">
                    <v-tooltip bottom>
                        <template v-slot:activator="{ on }">
                            <span v-on="on">{{ order.customer.name }}</span>
                        </template>
                        <span>{{ order.customer.name }}</span>
                    </v-tooltip>
                </div>

                <div class="main-container-wrapper pa-1 column-200">
                    <v-tooltip bottom>
                        <template v-slot:activator="{ on }">
                            <span v-on="on">{{ order.address.name }}</span>
                        </template>
                        <span>{{ order.address.name }}</span>
                    </v-tooltip>
                </div>

                <!--        <div class="main-container-wrapper pa-1 column-200">-->
                <!--          <v-tooltip bottom>-->
                <!--            <template v-slot:activator="{ on }">-->
                <!--              <span v-on="on">{{ order.customer.contacts }}</span>-->
                <!--            </template>-->
                <!--            <span>{{ order.customer.contacts }}</span>-->
                <!--          </v-tooltip>-->
                <!--        </div>-->

                <div class="main-container-wrapper pa-1 column-400">
                    <v-tooltip bottom>
                        <template v-slot:activator="{ on }">
                            <span v-on="on">{{ order.workDescription }}</span>
                        </template>
                        <span>{{ order.workDescription }}</span>
                    </v-tooltip>
                </div>

                <div class="main-container-wrapper pa-1 column-100">
                    <v-tooltip bottom>
                        <template v-slot:activator="{ on }">
                            <span v-on="on">{{ order.endDate }}</span>
                        </template>
                        <span>Дата завершения работ: {{ order.endDate }}</span>
                    </v-tooltip>
                </div>

                <div class="main-container-wrapper pa-1 column-70">
                    <span v-if="order.endDate === null && order.verificationDate === null" class="text-red">
                        <v-tooltip bottom>
                            <template v-slot:activator="{ on }">
                                <v-icon color="red darken-1" v-on="on">{{ mdiAlertCircle }}</v-icon>
                            </template>
                            <span>Статус: в работе</span>
                        </v-tooltip>
                    </span>

                    <span v-else-if="order.verificationDate === null" class="text-green">
                        <v-tooltip bottom>
                            <template v-slot:activator="{ on }">
                                <v-icon color="green darken-2" v-on="on">{{ mdiCheck }}</v-icon>
                            </template>
                            <span>Статус: завершено</span>
                        </v-tooltip>
                    </span>

                    <span v-else-if="order.verificationDate !== null" class="text-green">
                        <v-tooltip bottom>
                            <template v-slot:activator="{ on }">
                                <v-icon color="green darken-2" v-on="on">{{ mdiCheckAll }}</v-icon>
                            </template>
                            <span>Статус: проверено</span>
                        </v-tooltip>
                    </span>
                </div>

                <div class="main-container-wrapper pa-1 column-150">
                    <v-btn icon v-on:click="edit">
                        <v-icon>{{ mdiPencil }}</v-icon>
                    </v-btn>

                    <Estimate v-bind:extId="order.extId"
                              v-bind:customer="order.customer.name"
                              v-bind:address="order.address.name"/>


                    <v-btn icon v-on:click="del">
                        <v-icon>{{ mdiDelete }}</v-icon>
                    </v-btn>
                </div>
            </div>
        </div>

    </v-container>
</template>

<script>
    import { mdiAlertCircle, mdiCheck, mdiCheckAll, mdiPencil, mdiDelete } from '@mdi/js';
    import {mapActions, mapGetters} from "vuex";
    import Estimate from "../views/Estimate";
    export default {
        name: 'OrderItem',
        props: ['order', 'editOrder'],
        computed: {
            ...mapGetters(['allOrders']),


        },
        components: {Estimate},

        methods: {
            ...mapActions(['fetchOrders']),

            edit() {

                console.log(this.order.id)
            },
            del() {

            },


        },



        data: () => ({
            mdiAlertCircle, mdiCheck, mdiCheckAll, mdiPencil, mdiDelete,

            customer: {
                id: 0,
                name: '',
            },
            address: {
                id: 0,
                name: '',
            },
            workGroup: {
                id: 0,
                groupList: '',
            },
            dataOrder: {

            }

        }),


    }
</script>

<style lang="scss">

  .main {
    border-bottom: 1px solid #ccc;
    font-size: small;
  }
  .main-container {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    &-wrapper {
      white-space: nowrap;
      text-overflow: ellipsis;
      overflow: hidden;
    }
  }
  .column-70 {
    width: 70px;
    max-width: 70px;
  }
  .column-100 {
    width: 100px;
    max-width: 100px;
  }
  .column-150 {
    width: 150px;
    max-width: 150px;
  }
  .column-200 {
    width: 200px;
    max-width: 200px;
  }
  .column-300 {
    width: 300px;
    max-width: 300px;
  }
  .column-400 {
    width: 400px;
    max-width: 400px;
  }
  .text-red {
    color: red;
  }
  .text-green {
    color: green;
  }
</style>