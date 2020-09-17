<template>
    <div>
        <div class="main font-s mt-10">
            <div class="font-weight-bold mb-1 mt-10">
                1. Активное оборудование
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

        <ModalWin v-bind:typeSection="typeSection"/>
    </div>
</template>

<script>
    import ModalWin from "./ModalWin";

    export default {
        name: "ActiveDevice",
        components: { ModalWin },
        data() {
            return {
                typeSection: 1

            }
        }
    }
</script>

<style scoped>

</style>