<template>
    <div>
        <input @input="onInput" />
        <!-- v-on:input can be changed to @input with same function -->
    </div>
</template>

<script>
export default {
    name: 'SearchBar',
    methods: {
        onInput: function(event) {
            this.$emit('termChange', event.target.value);
            //trigger event on App parent class
        }
    }
};
</script>

<style scoped>
    input {
        width: 75%;
    }

    div {
        text-align: center;
        margin: 20px;
    }
</style>