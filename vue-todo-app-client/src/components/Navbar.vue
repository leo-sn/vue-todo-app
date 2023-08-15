<script setup>
import { RouterLink } from 'vue-router';


</script>

<template>
    <header>
        <nav class="navbar">
            <div>TODO APP</div>
            <ul class="navbar-routes">
                <RouterLink to="/">Home</RouterLink>
                <RouterLink to="/About">About</RouterLink>
            </ul>
        </nav>
    </header>
</template>

<style lang="scss" scoped>
    .navbar {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background-color: lightgray;
        height: 100%;
        max-width: 100vw;

        &-routes {
            display: flex;
            gap: 10px;
            padding: 10px;
        }
    }

</style>