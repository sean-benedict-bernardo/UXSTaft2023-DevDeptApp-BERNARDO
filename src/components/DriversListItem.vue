<script setup>
defineProps(['driver'])
</script>

<template>
    <a href="javascript:;" @click="$emit('dispDriver', driver.driverId)" :id="driver.driverId">
        <h3 class="driver_listitem">
            <img :src="driver.country_img">
            {{ driver.code }} <span v-if="`code` in driver">|</span>
            {{ driver.givenName }} {{ driver.familyName }}
        </h3>
    </a>
</template>

<style scoped>
.driver_listitem {
    background-color: var(--vt-c-divider-dark-1);
    border: 3px var(--color-main-accent);
    border-radius: 2rem;

    padding: 1rem;
    margin: 1rem;

    color: white;
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