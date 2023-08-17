<script setup>
    import { reactive, defineEmits } from 'vue';
    import TodoButton from './TodoButton.vue';
    import { Icon } from '@iconify/vue';

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
        <input type="text" v-model="todoState.todo" 
        @keyup.enter="createTodo" 
        :class="{'input-wrap-error': todoState.invalid}">
        <Icon v-show="todoState.invalid" class="error-icon" icon="mingcute:warning-line" color="red" width="22" height="22" />
        <TodoButton @click="createTodo()" />
    </div>
    <p v-show="todoState.invalid" class="error-message">{{ todoState.errorMessage }}</p>
</template>

<style lang="scss" scoped>

    .input-wrap {
        display: flex;
        margin: 10px 10% 5px 10% ;
        width: 90%;
        min-width: 150px;
        border: 1px solid rgb(112, 187, 112);
        border-radius: 20px;
        padding: 5px;

        &-error {
            padding-left: 30px;
        }
    }
    
    input {
        position: relative;
        border: none;
        width: 100%;
        padding-left: 10px;
    
        &:focus {
                outline: none;
        }
    }

    .input-error {
        border: 1px red solid;
    }

    .error-icon {
        position: absolute;
        margin-left: 2px;
        margin-top: 1.5px;
    }

    .error-message {
        color: rgb(255, 43, 43);
        font-size: 12px;
        position: absolute;
        top: 160px;
    }

</style>