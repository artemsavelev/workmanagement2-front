<template>
    <v-dialog v-model="dialog" width="80%" scrollable persistent>

        <template v-slot:activator="{ on }" class="mt-10">
            <v-btn v-on="on" small class="mb-10 mt-1" color="primary" tile>добавить</v-btn>
        </template>
        <v-card>

            <v-card-title class="headline grey lighten-2">
                <span class="header-modal">{{formTitle}}</span>


                <v-spacer></v-spacer>
                <v-btn small text tile v-on:click="close">
                    <v-icon>{{ mdiClose }}</v-icon>
                </v-btn>
            </v-card-title>

            <v-card-text>
                <v-container>

                    <div v-if="typeSection === 0">
                        <v-row>
                            <v-col cols="12">
                                <v-textarea
                                        outlined
                                        :auto-grow="true"
                                        rows="4"
                                        name="input-7-4"
                                        label="Виды работ"
                                        value="1.
2.
3."
                                ></v-textarea>

                                <v-textarea
                                        outlined
                                        :auto-grow="true"
                                        rows="3"
                                        name="input-2-4"
                                        label="Примечание"
                                        value="Смета ПРЕДВАРИТЕЛЬНАЯ Конечная цена и материал по согласованию строн могут измениться в большую или меньшую сторону
Цены в данной смете актуальны в течении 5 (пяти ) рабочих дней"
                                ></v-textarea>
                                <v-btn v-on:click="add" small color="primary" tile>add</v-btn>
                            </v-col>
                        </v-row>

                    </div>
                    <div v-else>
                        <v-card-title class="fix">
                            <v-col cols="12">

                                <v-text-field
                                        class="pa-0 ma-0"
                                        dense
                                        label="Поиск"
                                        outlined
                                        v-model="search"/>


                            </v-col>
                        </v-card-title>

                        <v-row>
                            <v-col cols="12" >
                                <div class="main font-s mt-0">
                                    <div class="main-container">
                                        <div class="main-container-wrapper pa-1 column-70">
                                            №
                                        </div>

                                        <div class="main-container-wrapper pa-1 column-700">
                                            Наименование
                                        </div>
                                        <div class="main-container-wrapper pa-1 column-100">
                                            Ед. изм.
                                        </div>
                                        <div class="main-container-wrapper pa-1 column-100">
                                            Кол-во
                                        </div>
                                        <div class="main-container-wrapper pa-1 column-100">
                                            Цена
                                        </div>
                                        <div class="main-container-wrapper pa-1 column-600">
                                            Комментарий
                                        </div>
                                        <div class="main-container-wrapper pa-1 column-70">
                                        </div>
                                    </div>
                                </div>
                            </v-col>
                        </v-row>

                        <v-row>
                            <v-col  cols="12">
                                <div class="main font-s mt-0" v-for="(item, idx) of data"
                                                                :key="item.id">
                                    <div class="main-container">
                                        <div class="main-container-wrapper pa-1 column-70">
                                            {{ idx + 1 }}
                                        </div>

                                        <div class="main-container-wrapper pa-1 column-700">
                                            {{ item.name }}
                                        </div>
                                        <div class="main-container-wrapper pa-1 column-100">
                                            {{ item.dimension }}
                                        </div>

                                        <div class="main-container-wrapper pa-1 column-100">
                                            <input type="text" placeholder="0"/>
                                        </div>

                                        <div class="main-container-wrapper pa-1 column-100">
                                            {{ item.price }}
                                        </div>

                                        <div class="main-container-wrapper pa-1 column-600">
                                            {{ item.note }}
                                        </div>
                                        <div class="main-container-wrapper column-70">
                                            <v-card-actions>
                                                <v-btn v-on:click="add" small color="primary" tile>add</v-btn>
                                            </v-card-actions>
                                        </div>
                                    </div>
                                </div>
                            </v-col>
                        </v-row>
                    </div>


                </v-container>
            </v-card-text>

        </v-card>
    </v-dialog>
</template>

<script>
    import { mdiClose } from '@mdi/js';


    export default {
        name: "ModalWin",
        props: ['typeSection', 'data'],
        data() {
            return {
                mdiClose,
                dialog: false,
                formTitle: '',
                search: '',
                quantity: 0
            }
        },
        methods: {

            add() {
                console.log()
            },
            close() {
                this.dialog = false
            }
        },

    }
</script>

<style scoped>
    input {
        border: 1px solid gray;
        width: 70px;
        border-radius: 3px;
        padding-left: 5px;
        padding-right: 5px;
        text-align: center;
    }



</style>