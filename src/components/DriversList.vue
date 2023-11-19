<script setup>
defineProps(['driver'])
// <img src="img_src"> 

</script>

<template>
    <div class="driver_list">

    </div>
</template>

<style scoped>
.driver_list {
    background-color: white;
    overflow: scroll;
}

.driver_listitem:hover {
    background-color: var(--vt-c-divider-dark-2)
}

.driver_listitem img {
    display: inline;
    height: 1rem;
    margin: 0 0.5rem;
}
</style>