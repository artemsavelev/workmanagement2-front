<template>
    <div>
        <v-text-field label="Login" :rules="rules" hide-details="auto"></v-text-field>
        <v-text-field label="Password" :rules="rules" hide-details="auto"></v-text-field>
    </div>
</template>

<script>
    export default {
        name: "auth",
        data: () => ({
            rules: [
                value => !!value || 'Required.',
                value => (value && value.length >= 3) || 'Min 3 characters',
            ],
        }),
    }
</script>

<style scoped>

</style>