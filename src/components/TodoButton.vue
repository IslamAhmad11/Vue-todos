<template>
    <button>
        <slot>Create</slot>
    </button>
</template>

<script setup>

</script>

<style lang="scss" scoped>
    button{
        padding: 8px 16px;
        border: none;
        font-size: 18px;
        cursor: pointer;
        background-color: #ddd;
    }
</style>