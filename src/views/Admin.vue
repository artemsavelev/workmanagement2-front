<template>
    <v-card tile>
        <v-tabs v-model="tab"
                :grow="grow"
                background-color="primary"
                dark>
            <v-tab v-for="item in items"
                    :key="item.tab">
                {{ item.tab }}
            </v-tab>
        </v-tabs>

        <v-tabs-items v-model="tab">
            <v-tab-item v-for="item in items"
                        :key="item.tab">
                <v-card flat>
                    <v-card-text>{{ item.content }}</v-card-text>
                </v-card>
            </v-tab-item>
        </v-tabs-items>
    </v-card>
</template>

<script>
    export default {
        name: "Admin",
        data () {
            return {
                tab: null,
                items: [
                    { tab: 'персонал', content: 'Tab 1 Content' },
                    { tab: 'Two', content: 'Tab 2 Content' },
                    { tab: 'Three', content: 'Tab 3 Content' },
                    { tab: 'Four', content: 'Tab 4 Content' },
                ],
                grow: true,
            }
        },
    }
</script>

<style scoped>

</style>