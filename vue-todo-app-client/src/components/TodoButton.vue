<script setup>

</script>

<template>
        
        <button @click="">
            <slot>Create</slot>
        </button>
</template>


<style lang="scss" scoped>

    button {
        background-color: rgb(168, 237, 168);
        border-radius: 20px;
        border: none;
        padding: 5px 10px;
        min-width: 100px;
        color: black;

        &:hover {
            background-color: rgb(149, 210, 149);
            cursor: pointer;
        }

        &:active {
            background-color: rgb(115, 178, 117);
        }
    }

</style>