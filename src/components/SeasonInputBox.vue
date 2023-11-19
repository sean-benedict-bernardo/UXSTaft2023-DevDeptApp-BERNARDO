<script>
import { ref } from 'vue'

const selected_year = ref(0);
const current_year = new Date().getFullYear();

export default {
    name: 'InputBox',
    methods: {
        passEvent() {
            if (selected_year.value > 0 || selected_year.value === "current") {
                this.$emit('passYear', selected_year.value)
            } else {
                alert("Please Select a Season")
            }
        }
    }
}
</script>

<script setup>
let year_arr = []
for (let i = current_year - 1; i >= `1950`; i--) {
    year_arr.push(i);
    if (i % 10 == 0) {
        year_arr.push(-1);
    }
}
</script>

<template>
    <div class="year_select">
        <select v-model="selected_year" style="width: 60%;">
            <option default disabled value="-2">Please select one</option>
            <option value="current">{{ current_year }} (Current)</option>
            <!-- adds a buffer between each decade -->
            <option v-for="x in year_arr" :disabled="(x < 0)">{{ (x > 0) ? x : `--------` }}</option>
        </select>
        <button @click="passEvent" style="width: 40%;">Display Drivers</button>
    </div>
</template> 

<style scoped>
.year_select {
    display: flex;
    width: 100%;
}

select,
button {
    padding: 0.5rem;
    border: 2px solid var(--color-main-accent);
    border-radius: 0rem;
    background-color: var(--color-background);

    color: white;
    font-family: Inter, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Fira Sans', 'Droid Sans', 'Helvetica Neue', sans-serif;
    font-size: 1rem;
}

button:hover {
    background-color: var(--color-background-mute);
}

option {
    padding: 0.25rem;
}
</style>
