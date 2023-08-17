<script setup>
import { Icon } from '@iconify/vue';

const props = defineProps({
    todo: {
        type: Object,
        required: true,
    },
    index: {
        type: Number,
        required: true
    }
});

defineEmits(['toggle-complete', 'edit-todo', 'updated-todo', 'delete-todo'])

</script>

<template>
    <div class="todo-wrap">
        <li>
            <input 
                type="checkbox" 
                :checked="todo.isCompleted"
                @input="$emit('toggle-complete', index)"
            />
            <div class="todo">
                <input 
                    v-if="todo.isEditing"
                    class="todo-enabled"
                    type="text" 
                    :value="todo.todo" 
                    @input="$emit('updated-todo', index, $event.target.value)"
                /> 
                <span v-else :class="{ 'todo-completed': todo.isCompleted }">
                    {{ todo.todo }}
                </span>
            </div>
        </li>
        <div class="todo-actions">
            <Icon 
                v-if="todo.isEditing" 
                class="icon" 
                icon="ph:check-circle" 
                color="#41b080" 
                width="22" 
                height="22" 
                @click="$emit('edit-todo', index)"
            />
            <Icon 
                v-else 
                class="icon" 
                icon="ph:pencil-fill" 
                color="#41b080" 
                width="22" 
                height="22" 
                @click="$emit('edit-todo', index)"
            />
            <Icon 
                class="icon" 
                icon="ph:trash" 
                color="#f95e5e" 
                width="22" 
                height="22" 
                @click="$emit('delete-todo', todo.id)"
            />
        </div>
    </div>
</template>


<style lang="scss" scoped>

    .todo-wrap {
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: fit-content;
        padding: 5px 10px;
        width: 100%;

        gap: 5px;

        .todo-actions {
            display: none;
        }


        &:hover {
            border-radius: 7px;
            background-color: rgb(204, 204, 204, 0.25);
            .todo-actions {
                display: flex;
                height: 100%;
                align-items: center;
            }      
        }

        input[type=checkbox] {
            width: 22px;
            height: 22px;
            border-radius: 100%;
            border: 1px solid rgb(196, 196, 196);
            appearance: none;
            -webkit-appearance: none;
            outline: none;
            cursor: pointer;

            &:checked {
                background-color: rgb(112, 187, 112);
                border: 1px solid rgb(112, 187, 112);
            }

        }
    }

    li {
        height: fit-content;
        display: flex;
        gap: 10px;
        width: 85%;


        input {
                min-width: 22px;
            }


        .todo {
            // width: 100%;
            align-items: center;
            width: 100%;

            input {
                width: 100%;
            }

            textarea {
                width: 100%;
                height: fit-content;
                resize: none;
                border: 1px solid rgb(196, 196, 196);
                border-radius: 5px;
                padding: 0 10px;
                outline: none;
            }


            span {
                max-width: 50%;
                font-size: 12px;
                color: rgb(36, 36, 36)
            }

            &-enabled {
                // min-width: 100%;
            }

            &-completed {
                text-decoration: line-through;
            }
        }
    }

    .todo-actions {
        display: flex;
    }

</style>