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
    <li>
        <input 
            type="checkbox" 
            :checked="todo.isCompleted"
            @input="$emit('toggle-complete', index)" 
        />
        <div class="todo">
            <input v-if="todo.isEditing" type="text" :value="todo.todo" @input="$emit('updated-todo', index, $event.target.value)"> 
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
</template>


<style lang="scss" scoped>

    li {
        display: flex;
        position: relative;

        .todo {
            color: blue;


            &-completed {
                text-decoration: line-through;
            }
        }
    }

</style>