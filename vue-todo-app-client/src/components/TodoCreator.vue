<script setup>
    import { reactive, defineEmits } from 'vue';
    import TodoButton from './TodoButton.vue';

    const emit = defineEmits(["create-todo"])

    //create the state for the todo
    const todoState = reactive({
        todo: '',
        invalid: null,
        errorMessage: "",
    });

    //emit the todo to the parent component
    const createTodo = () => {
        todoState.invalid = null;
        if (todoState.todo !== "") {
            emit('create-todo', todoState.todo);
            todoState.todo = "";
            return
        }
        todoState.invalid = true;
        todoState.errorMessage = "Todo value can't be empty!"
    };

</script>

<template>
    <div class="input-wrap" :class="{ 'input-error': todoState.invalid}">
        <input type="text" v-model="todoState.todo" @keyup.enter="createTodo"/>
        <TodoButton @click="createTodo()" />
    </div>
    <p v-show="todoState.invalid" class="error-message">{{ todoState.errorMessage }}</p>
</template>

<style lang="scss" scoped>

    .input-wrap {
        display: flex;
        flex-direction: column;
        margin: 3% 10%;
        width: 60%;
    }

    .input-error {
        border: 1px red solid;
    }

</style>