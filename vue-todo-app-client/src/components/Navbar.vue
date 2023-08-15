<script setup>
import { RouterLink } from 'vue-router';


</script>

<template>
    <header>
        <nav class="navbar">
            <div class="navbar-logo"><RouterLink to="/">VUE TODO APP</RouterLink></div>
            <ul class="navbar-routes">
                <RouterLink tag="li" to="/">Home</RouterLink>
                <RouterLink to="/About">About</RouterLink>
            </ul>
        </nav>
    </header>
</template>

<style lang="scss" scoped>

.navbar .router-link-active,
.navbar .router-link-exact-active {
    text-decoration: none;
    cursor: pointer;
}
    .navbar {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background-color: rgb(247, 247, 247);
        height: 100%;
        max-width: 100vw;
        margin-bottom: 30px;

        &-logo {
            padding: 10px;
        }

        &-routes {
            display: flex;
            gap: 10px;
            padding: 10px;

        }
    }

</style>