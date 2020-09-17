<template>
  <v-container>

<!--    <v-row class="text-center">-->
<!--    </v-row>-->

    <div class="main">

      <div class="main-container">
        <div class="main-container-wrapper pa-1 column-70">
<!--          {{ ordersList.orderId }}-->
        </div>

        <div class="main-container-wrapper pa-1 column-70">
<!--          {{ ordersList.extId }}-->
        </div>

        <div class="main-container-wrapper pa-1 column-100">
          <v-tooltip bottom>
<!--            <template v-slot:activator="{ on }">-->
<!--              <span v-on="on">{{ ordersList.creationDate }}</span>-->
<!--            </template>-->
<!--            <span>Дата создания: {{ ordersList.creationDate }}</span>-->
          </v-tooltip>

        </div>

        <div class="main-container-wrapper pa-1 column-100">
          <v-tooltip bottom>
<!--            <template v-slot:activator="{ on }">-->
<!--              <span v-on="on">{{ ordersList.startDate }}</span>-->
<!--            </template>-->
<!--            <span>Дата начала работ: {{ ordersList.startDate }}</span>-->
          </v-tooltip>
        </div>

        <div class="main-container-wrapper pa-1 column-150">
          <v-tooltip bottom>
<!--            <template v-slot:activator="{ on }">-->
<!--              <span v-on="on">{{ ordersList.workGroup.workGroupList }}</span>-->
<!--            </template>-->
<!--            <span>{{ ordersList.workGroup.workGroupList }}</span>-->
          </v-tooltip>
        </div>

        <div class="main-container-wrapper pa-1 column-200">
<!--                    <span v-for="user in ordersList.users">-->

                    <v-tooltip bottom>
<!--                        <template v-slot:activator="{ on }">-->
<!--                            <span v-on="on"> {{ user.name }}</span>-->
<!--                        </template>-->
<!--                        <span>{{ user.name }}</span>-->
                    </v-tooltip>

<!--                    </span>-->
        </div>

        <div class="main-container-wrapper pa-1 column-200">
          <v-tooltip bottom>
<!--            <template v-slot:activator="{ on }">-->
<!--              <span v-on="on">{{ ordersList.customer }}</span>-->
<!--            </template>-->
<!--            <span>{{ ordersList.customer }}</span>-->
          </v-tooltip>
        </div>

        <div class="main-container-wrapper pa-1 column-200">
          <v-tooltip bottom>
<!--            <template v-slot:activator="{ on }">-->
<!--              <span v-on="on">{{ ordersList.address }}</span>-->
<!--            </template>-->
<!--            <span>{{ ordersList.address }}</span>-->
          </v-tooltip>
        </div>

        <div class="main-container-wrapper pa-1 column-200">
          <v-tooltip bottom>
<!--            <template v-slot:activator="{ on }">-->
<!--              <span v-on="on">{{ ordersList.contact }}</span>-->
<!--            </template>-->
<!--            <span>{{ ordersList.contact }}</span>-->
          </v-tooltip>
        </div>

        <div class="main-container-wrapper pa-1 column-300">
          <v-tooltip bottom>
<!--            <template v-slot:activator="{ on }">-->
<!--              <span v-on="on">{{ ordersList.workDescription }}</span>-->
<!--            </template>-->
<!--            <span>{{ ordersList.workDescription }}</span>-->
          </v-tooltip>
        </div>

        <div class="main-container-wrapper pa-1 column-100">
          <v-tooltip bottom>
<!--            <template v-slot:activator="{ on }">-->
<!--              <span v-on="on">{{ ordersList.endDate }}</span>-->
<!--            </template>-->
<!--            <span>Дата завершения работ: {{ ordersList.endDate }}</span>-->
          </v-tooltip>
        </div>

        <div class="main-container-wrapper pa-1 column-70">
<!--                    <span v-if="ordersList.endDate === null && ordersList.verificationDate === null" class="text-red">-->
                        <v-tooltip bottom>
                            <template v-slot:activator="{ on }">
                                <v-icon color="red darken-1" v-on="on">{{ mdiAlertCircle }}</v-icon>
                            </template>
                            <span>Статус: в работе</span>
                        </v-tooltip>
<!--                    </span>-->

<!--          <span v-else-if="ordersList.verificationDate === null" class="text-green">-->
                        <v-tooltip bottom>
                            <template v-slot:activator="{ on }">
                                <v-icon color="green darken-2" v-on="on">{{ mdiCheck }}</v-icon>
                            </template>
                            <span>Статус: завершено</span>
                        </v-tooltip>
<!--                    </span>-->

<!--          <span v-else-if="ordersList.verificationDate !== null" class="text-green">-->
                        <v-tooltip bottom>
                            <template v-slot:activator="{ on }">
                                <v-icon color="green darken-2" v-on="on">{{ mdiCheckAll }}</v-icon>
                            </template>
                            <span>Статус: проверено</span>
                        </v-tooltip>
<!--                    </span>-->
        </div>

        <div class="main-container-wrapper pa-1 column-100">
<!--          <v-btn x-small icon v-on:click="edit">-->
            <v-icon>edit</v-icon>
<!--          </v-btn>-->
<!--          <v-btn x-small icon v-on:click="del">-->
            <v-icon>close</v-icon>
<!--          </v-btn>-->
        </div>
      </div>
    </div>

  </v-container>
</template>

<script>
    import { mdiAlertCircle, mdiCheck, mdiCheckAll } from '@mdi/js';
    export default {
        name: 'OrderItem',

        data: () => ({
            mdiAlertCircle,
            mdiCheck,
            mdiCheckAll
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