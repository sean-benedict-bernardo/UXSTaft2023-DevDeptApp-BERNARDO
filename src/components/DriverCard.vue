<script setup>
defineProps(['driver'])

function returnDateStr(birth_date) {
    const age_obj = new Date(birth_date)

    return `${age_obj.getDate()} ${age_obj.toLocaleString('default', { month: 'short' })}. ${age_obj.getFullYear()}`
}

function returnAge(birth_date) {
    const age_obj = new Date(birth_date)
    const date_obj = new Date()

    if (age_obj.getMonth() >= date_obj.getMonth() && age_obj.getDate() >= date_obj.getDate()) {
        return date_obj.getFullYear() - age_obj.getFullYear()
    } else {
        return date_obj.getFullYear() - age_obj.getFullYear() - 1
    }
}

</script>

<template>
    <div class="driver_card">
        <div>
            <h1>{{ driver.givenName }} {{ driver.familyName }}</h1>
            <h3 v-if="`permanentNumber` in driver">Permanent #: {{ driver.permanentNumber }}</h3>
            <h3>Birthday: {{ returnDateStr(driver.dateOfBirth) }} ({{
                returnAge(driver.dateOfBirth)
            }})</h3>
            <h3></h3>
            <h3>Nationality: {{ driver.nationality }} <img style="max-height: 1rem;" :src="driver.country_img"></h3>
            <br>
            <h3><a style="color: white;" :href="driver.url" target="_blank" rel="noopener">Wikipedia Article</a></h3>
        </div>
        <img :src="driver.portrait" :alt="driver.code">
    </div>
</template>

<style scoped>
.driver_card {
    background-color: var(--vt-c-divider-dark-1);
    border: 3px var(--color-main-accent);
    padding: 1rem;
    border-radius: 2rem;

    display: flex;
    flex-direction: row;
    justify-content: space-between;

    color: white;
}

.driver_card>* {
    margin: 0 1rem;

    height: fit-content;
}

.driver_card a {
    color: white;
    text-decoration: underline;
}
.driver_card a:hover {
    background-color: var(--vt-c-divider-dark-1);
}

.driver_card>img {
    max-width: 30%;
    border-radius: 1rem;
}
</style>