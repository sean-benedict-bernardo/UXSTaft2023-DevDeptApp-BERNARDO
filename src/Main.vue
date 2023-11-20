<script setup>
import TopRow from './components/TopRow.vue'
import SeasonInputBox from './components/SeasonInputBox.vue'
import DriverCard from './components/DriverCard.vue'
import DriversListItem from './components/DriversListItem.vue'
import { ref } from 'vue'

const isSelected = ref(false);
const driver_array = ref([]);
const selected_driver = ref();

const driver_nationalities = [
    { country_code: "us", nationality: "American" },
    { country_code: "ar", nationality: "Argentine" },
    { country_code: "au", nationality: "Australian" },
    { country_code: "at", nationality: "Austrian" },
    { country_code: "be", nationality: "Belgian" },
    { country_code: "br", nationality: "Brazilian" },
    { country_code: "gb", nationality: "British" },
    { country_code: "ca", nationality: "Canadian" },
    { country_code: "cl", nationality: "Chilean" },
    { country_code: "cn", nationality: "Chinese" },
    { country_code: "co", nationality: "Colombian" },
    { country_code: "cz", nationality: "Czech" },
    { country_code: "dk", nationality: "Danish" },
    { country_code: "nl", nationality: "Dutch" },
    { country_code: "fi", nationality: "Finnish" },
    { country_code: "fr", nationality: "French" },
    { country_code: "de", nationality: "German" },
    { country_code: "hu", nationality: "Hungarian" },
    { country_code: "in", nationality: "Indian" },
    { country_code: "id", nationality: "Indonesian" },
    { country_code: "ie", nationality: "Irish" },
    { country_code: "it", nationality: "Italian" },
    { country_code: "jp", nationality: "Japanese" },
    { country_code: "lt", nationality: "Liechtensteiner" },
    { country_code: "my", nationality: "Malaysian" },
    { country_code: "mx", nationality: "Mexican" },
    { country_code: "mc", nationality: "Monegasque" },
    { country_code: "ma", nationality: "Moroccan" },
    { country_code: "nz", nationality: "New Zealander" },
    { country_code: "pl", nationality: "Polish" },
    { country_code: "pt", nationality: "Portuguese" },
    { country_code: "zw", nationality: "Rhodesian" },
    { country_code: "ru", nationality: "Russian" },
    { country_code: "za", nationality: "South African" },
    { country_code: "es", nationality: "Spanish" },
    { country_code: "se", nationality: "Swedish" },
    { country_code: "ch", nationality: "Swiss" },
    { country_code: "th", nationality: "Thai" },
    { country_code: "uy", nationality: "Uruguayan" },
    { country_code: "ve", nationality: "Venezuelan" }
]

const headers_standard = {
    method: "GET", // *GET, POST, PUT, DELETE, etc.
    mode: "cors", // no-cors, *cors, same-origin
}

async function fetchDrivers(year) {
    const url_drivers = `https://ergast.com/api/f1/${year}/drivers.json`
    const http_response = await fetch(url_drivers, headers_standard).then((e) => { return e.json() })
    return http_response.MRData.DriverTable.Drivers
}

async function fetchDriverPhoto(wikipedia_uri) {
    // removes domain and placed into URL
    const wikipedia_pageimage_request = `https://en.wikipedia.org/w/api.php?action=query&titles=${wikipedia_uri.replace('http:\/\/en.wikipedia.org\/wiki\/', '')}&origin=*&prop=pageimages&format=json&pithumbsize=500`

    // requests 
    const http_response = await fetch(wikipedia_pageimage_request, headers_standard).then((e) => { return e.json() })

    // wikipedia page IDs are dynamic, hence the need for the keys
    const wiki_pageid = Object.keys(http_response.query.pages);
    const obj = http_response.query.pages[wiki_pageid];

    // returns source if json contains thumbnail image, passes string below for use within DriverCard.vue
    
    return (Object.keys(obj).includes("thumbnail")) ? obj.thumbnail.source : "../assets/driverphoto_unavailable.png";
}

async function renderCard(driverId) {
    selected_driver.value = driver_array.value.find(x => x.driverId === driverId)
    selected_driver.value.portrait = await fetchDriverPhoto(selected_driver.value.url)

    isSelected.value = true;
}

async function getDrivers(year) {
    let season_drivers = await fetchDrivers(year)
    driver_array.value = []

    for (let i = 0; i < season_drivers.length; i++) {
        let driver = season_drivers[i];
        let driver_iso3166 = driver_nationalities.find((e) => e.nationality == driver.nationality);

        // Alex or Alexander, pick a lane
        if (driver.code == "albon") {
            driver.url = "https://en.wikipedia.org/wiki/Alex_Albon"
        }

        driver.country_code = driver_iso3166.country_code
        driver.country_img = `https://flagcdn.com/${driver.country_code}.svg`

        driver_array.value.push(driver)
    }
}
</script>

<template>
    <header>
        <div class="wrapper">
            <img alt="F1 Logo" class="logo" src="./assets/logo.svg" />
            <TopRow />
        </div>

        <h2 style="width: 100%; margin-top: 1rem; text-align: left;">
            Choose an
            <span style="font-style: italic; color: var(--color-main-accent)">F1</span>
            Season, then choose a driver
        </h2>
        <SeasonInputBox @passYear="getDrivers($event)" />

        <div class="driver_listitems">
            <DriversListItem v-for="driver in driver_array" :driver="driver" @dispDriver="renderCard($event)" />
        </div>

    </header>

    <main>
        <DriverCard v-if="isSelected" :driver="selected_driver" />
    </main>
</template>

<style scoped>

header,
main {
    padding: 1rem 0.5rem;

    display: flex;
    place-items: center;
}

header {
    flex-direction: column;
    width: 40vw;
    height: 100vh;
}

main {
    width: 40vw;
}

header>div {
    margin: 1rem 0;
}

.logo {
    height: 2rem;
    margin: 0 1rem;
}

.wrapper {
    margin: 0 5%;
    width: 100%;
    display: flex;
    flex-direction: row;
    place-items: flex-start;
    align-items: center;
    flex-wrap: wrap;
}

.driver_list {
    margin: 0;
    width: 100%;
    border: 2px solid var(--color-main-accent);
}

.driver_listitems {
    width: 100%;
    max-height: 50vh;
    overflow-y: scroll;
}

.driver_listitems::-webkit-scrollbar {
    width: 20px;
}

/* Handle */
.driver_listitems::-webkit-scrollbar-thumb {
    background: var(--color-main-accent);
}

/* Handle on hover */
.driver_listitems::-webkit-scrollbar-thumb:hover {
    background: rgba(240, 0, 0, 0.514);
}


@media (max-width: 1024px) {
    header,
    main {
        width: auto;
        height: fit-content;
        padding: 1rem 0.5rem;

        display: flex;
        flex-direction: column;
    }

    .wrapper {
        flex-direction: column;
    }
}
</style>
