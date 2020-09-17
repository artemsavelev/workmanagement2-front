<template>
    <div>
        <div class="main font-s pt-10">
            <div class="font-weight-bold mb-1">
                3. Работы
            </div>

            <div class="main-container blue-grey lighten-4">
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

                <div class="main-container-wrapper pa-1 column-100">
                    Стоимость
                </div>

                <div class="main-container-wrapper pa-1 column-200">
                    Комментарий
                </div>
            </div>
        </div>

        <ModalWin v-bind:typeSection="typeSection"
                  v-bind:data="data"/>

    </div>
</template>

<script>
    import ModalWin from "./ModalWin";
    import req from "../store/headers";
    import api from "../api/backendApi";

    export default {
        name: "Work",
        components: { ModalWin },
        data() {
            return {
                typeSection: 3,
                data: []

            }
        },
        mounted() {

            req.requestData(api.API_WORK_URL, 'GET')
                .then(response => response.json())
                .then(json => this.data = json)
        },
    }
</script>

<style scoped>

</style>