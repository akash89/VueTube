<template>
    <div>
        <input @input="onInput"/>
    </div>
</template>

<script>
export default {
    name: 'SearchBar',
    methods: {
        onInput: function(event) {
            this.$emit('termChange', event.target.value);
        }
    }
};
</script>

<style scoped>
    div {
        align-self: center;
        width: 100%;
        margin-bottom: 10px;
    }
    input {
        width: 75%;
        border-radius: 2px;
        border: 1px solid #ccc;
        color: #333;
        padding: 10px 12px;
        font-size: 1.1em;
        width: 100%;
    }
</style>

