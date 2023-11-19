<script setup>
import { ref } from 'vue'
const ribbon_links = ref([
    { name: "README.md", link: "../../README.md" },
    { name: "Source Code", link: "https://github.com" }
])

</script>

<template>
    <div class="greetings">
        <h3> The F1 Driver's Paddock </h3>
        <a v-for="links in ribbon_links" v-bind:href="links.link" target="_blank" rel="noopener">{{ links.name }}</a>
    </div>
</template>

<style scoped>
h1 {
    font-weight: 500;
    font-size: 2.6rem;
    position: relative;
    top: -10px;
}

h3 {
    font-size: 1.2rem;
}

.greetings a {
    padding: 0 0.5rem;
    border: 0 0.5rem;
    border-left-style: solid;
}

.greetings h1,
.greetings h3 {
    display: flex;
    text-align: center;
}

@media (min-width: 1024px) {

    .greetings h1,
    .greetings h3 {
        text-align: left;
    }
}
</style>
