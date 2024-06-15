<template>
    <div class="input-wrap">
        <!-- using v-model directive to sync todo variable up to the input  -->
        <input type="text" v-model="todo"/>
        <!-- <input type="text" v-model="todoState.todo"/> -->
        <button>Creator</button>
    </div>
    <p>{{ todo }}</p>
    <!-- <p>{{ todoState.todo }}</p> -->
</template>

<script setup>
import { reactive, ref } from 'vue';
// using ref method to make our variable reactive with the input value
    const todo= ref(" ref test");
    // also we can use reactive to make our variable reactive with the input value
    // const todoState = reactive({todo: "reactive test",});
</script>

<style lang="scss" scoped>
    .input-wrap {
        display: flex;
        transition: 250ms ease;
        border: 2px solid #41b080;

        &.input-err {
            border-color: red;
        }

        &:focus-within {
            box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
            0 -2px 4px -2px rgb(0 0 0 / 0.1);
        }

        input {
            width: 100%;
            padding: 8px 6px;
            border: none;

            &:focus {
            outline: none;
            }
        }
        }

        .err-msg {
        margin-top: 6px;
        font-size: 12px;
        text-align: center;
        color: red;
    }
</style>