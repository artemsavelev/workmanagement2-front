<template>
    <v-dialog v-if="profile" v-model="dialog" scrollable width="1000">

        <template v-slot:activator="{ on }" class="mt-10">
            <v-btn dark v-on="on" text tile>CREATE</v-btn>
        </template>
        <v-card>

            <v-card-title class="headline grey lighten-2">
                <span class="header-modal">{{formTitle}}</span>
            </v-card-title>

            <v-card-text>
                <v-container>

                    <v-row>
                        <v-col cols="12" sm="6" md="4">
                            <v-text-field
                                    dense
                                    label="Номер заявки"
                                    v-model="extId"/>
                        </v-col>

                        <v-col cols="12" sm="6" md="4">
                            <v-menu v-model="menuStartDate"
                                    :close-on-content-click="false"
                                    :nudge-right="40"
                                    transition="scale-transition"
                                    offset-y
                                    min-width="100px">

                                <template v-slot:activator="{ on }">
                                    <v-text-field v-model="startDate"
                                                  label="Дата начала работ"
                                                  dense
                                                  readonly
                                                  v-on="on">
                                    </v-text-field>
                                </template>

                                <v-date-picker
                                        v-model="startDate"
                                        @input="menuStartDate = false">
                                </v-date-picker>
                            </v-menu>
                        </v-col>

                        <v-col cols="12" sm="6" md="4">
                            <v-menu v-model="menuStartTime"
                                    :close-on-content-click="false"
                                    :nudge-right="40"
                                    transition="scale-transition"
                                    offset-y
                                    min-width="100px">

                                <template v-slot:activator="{ on }">
                                    <v-text-field v-model="startTime"
                                                  label="Время начала работ"
                                                  dense
                                                  readonly
                                                  v-on="on">
                                    </v-text-field>
                                </template>

                                <v-time-picker
                                        v-model="startTime"
                                        format="24hr"
                                        @input="menuStartTime = false">
                                </v-time-picker>
                            </v-menu>
                        </v-col>

                        <v-col cols="12" sm="6" md="6">
                            <v-autocomplete v-model="users"
                                            :items="executors"
                                            label="Исполнители"
                                            item-text="lastName"
                                            item-value="userId"
                                            dense
                                            required
                                            multiple>
                            </v-autocomplete>
                        </v-col>

                        <v-col cols="12" sm="6" md="6">
                            <v-autocomplete v-model="workGroup.id"
                                            :items="group"
                                            label="Тип работ"
                                            item-text="groupList"
                                            item-value="id"
                                            dense
                                            required>
                            </v-autocomplete>
                        </v-col>

                        <v-col cols="12" sm="6" md="4">
                            <v-text-field
                                    dense
                                    label="Заказчик"
                                    v-model="customer"/>
                        </v-col>

                        <v-col cols="12" sm="6" md="4">
                            <v-text-field
                                    dense
                                    label="Контакт"
                                    />
                        </v-col>

                        <v-col cols="12" sm="6" md="4">
                            <v-text-field
                                    dense
                                    label="Адрес"
                                    v-model="address" />
                        </v-col>
                    </v-row>

                    <v-text-field
                            dense
                            label="Описание работ"
                            v-model="workDescription" />

                    <v-row>
                        <v-col cols="12" sm="6" md="6">
                            <v-menu v-model="menuEndDate"
                                    :close-on-content-click="false"
                                    :nudge-right="40"
                                    transition="scale-transition"
                                    offset-y
                                    min-width="100px">

                                <template v-slot:activator="{ on }">
                                    <v-text-field v-model="endDate"
                                                  label="Дата завершения работ"
                                                  dense
                                                  readonly
                                                  v-on="on">
                                    </v-text-field>
                                </template>

                                <v-date-picker
                                        v-model="endDate"
                                        @input="menuEndDate = false">
                                </v-date-picker>
                            </v-menu>
                        </v-col>

                        <v-col cols="12" sm="6" md="6">
                            <v-menu v-model="menuEndTime"
                                    :close-on-content-click="false"
                                    :nudge-right="40"
                                    transition="scale-transition"
                                    offset-y
                                    min-width="100px">

                                <template v-slot:activator="{ on }">
                                    <v-text-field v-model="endTime"
                                                  label="Время завершения работ"
                                                  dense
                                                  readonly
                                                  v-on="on">
                                    </v-text-field>
                                </template>

                                <v-time-picker
                                        v-model="endTime"
                                        format="24hr"
                                        @input="menuEndTime = false">
                                </v-time-picker>
                            </v-menu>
                        </v-col>
                    </v-row>

                </v-container>
                <v-card-actions>
                    <v-btn v-on:click="save" color="primary" class="mr-2" tile>save</v-btn>
                    <v-btn v-on:click="close" color="primary" tile>close</v-btn>
                </v-card-actions>
            </v-card-text>

        </v-card>
    </v-dialog>

</template>

<script>

    import req from '../store/headers';
    import api from "../api/backendApi";
    import {mapActions, mapGetters} from "vuex";

    export default {
        name: "OrderForm",
        computed: {
            ...mapGetters(['profile']),

            formTitle() {
                return this.editedIndex === -1 ? 'Добавление записи' : 'Редактирование записи '
            },
        },
        data() {
            return {

                dialog: false,
                orderId: '',
                extId: '',
                customer: {
                    id: '',
                    contacts: []
                },
                address: {
                    id: '',
                },
                workDescription: '',
                creationDate: '',
                // datepicker
                startDate: new Date().toISOString().substr(0, 10),
                startTime: new Date().getHours() + ':' + new Date().getMinutes(),

                menuStartDate: false,
                menuStartTime: false,

                endDate: null,
                endTime: null,

                menuEndDate: false,
                menuEndTime: false,

                executors: [],
                users: [],
                userId: '',

                group: [],
                workGroup: {
                    id: '',
                    groupList: '',
                },
                editedIndex: -1
            };
        },

        methods: {
            ...mapActions(['addOrder', 'addOrderMutation']),
            save() {

                //console.log(this.startDate + ' ' + this.startTime + ':' + new Date().getSeconds() + '-0300')

                const order = {
                    // id: this.id,
                    extId: this.extId,
                    startDate: this.startDate + 'T' + this.startTime + ':' + new Date().getSeconds() + '.' + new Date().getMilliseconds() + '+0000',
                    workGroup: {
                        id: this.workGroup.id,
                        // groupList: this.groupList,
                    },
                    executors: [],
                    customer: {
                        id: this.customer,
                        // name: this.customer.name,
                        contacts: []
                    },
                    address: {
                        id: this.address
                    },
                    workDescription: this.workDescription,
                    // endDate: this.endDate + ' ' + this.endTime + ':' + new Date().getSeconds(),
                };

                this.addOrder(order);
                console.log(order);

            },
            close() {
                this.dialog = false;
            }
        },
        watch: {

            orderVal(newVal){

                this.dialog = true;
                this.id = newVal.id;
                this.extId = newVal.extId;
                this.creationDate = newVal.creationDate;
                this.startDate = newVal.startDate;
                this.endDate = newVal.endDate;
                this.verificationName = newVal.verificationName;
                this.verificationDate = newVal.verificationDate;
                this.workGroup.id = newVal.workGroup.id;
                this.workGroup.groupList = newVal.workGroup.groupList;
                this.workDescription = newVal.workDescription;
                this.executors = newVal.executors;
                this.customer.id = newVal.customer.id;
                this.customer.name = newVal.customer.name;
                this.customer.contacts = newVal.customer.contacts;
                this.editedIndex = this.id
            }




        },

        mounted() {

            req.requestData(api.API_GROUP_URL, 'GET')
                .then(response => response.json())
                .then(json => this.group = json);

            req.requestData(api.API_USER_URL, 'GET')
                .then(response => response.json())
                .then(json => this.executors = json)
        },
    }




</script>

<style scoped lang="scss">
    .container-form {
        margin: auto 0;
    }

</style>