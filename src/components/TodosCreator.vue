<template>
    <div class="input-wrap">
        <!-- using v-model directive to sync todo variable up to the input  -->
        <input type="text" v-model="todoState.todo"/>
        <button @click="createTodo()">Creator</button>
    </div>
    <!-- using v-if directive to show error message if we have an error -->
    <!-- <p v-if="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p> -->

    <!-- also we can use v-show for the same purpose of v-if -->
    <p v-show="todoState.invalid" class="err-msg">{{ todoState.errMsg }}</p>

</template>

<script setup>
import { reactive, ref, defineEmits } from 'vue';
// using ref method to make our variable reactive with the input value
    // const todo= ref(" ref test");

    // also we can use reactive to make our variable reactive with the input value
    const todoState = reactive({
        todo: "",
        invalid: null,
        errMsg: "",
    });

    // to emit data from our component to parent component of todosView
    const emit = defineEmits(["create-todo"]);

    const createTodo = () => {
        // reset invalid value
        todoState.invalid = null;

        if(todoState.todo !== ""){
            emit("create-todo", todoState.todo);
            // reset todo value
            todoState.todo = "";
        }else{
            todoState.invalid = true;
            todoState.errMsg = "Todo value cannot be empty";
        }
    }
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
        font-size: 20px;
        font-weight: bold;
        text-align: center;
        color: red;
    }
</style>