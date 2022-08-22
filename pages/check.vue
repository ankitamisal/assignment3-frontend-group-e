<template>
    <div class="container mx-auto">
        <p v-for="mountain in moutains" :key="mountain.productName" :product="mountain"></p>
        <p>{{ moutains }}</p>
    </div>
</template>
<script>
export default {
    async fetch() {
        this.moutains = await fetch('http://localhost:8080/feed/allData').then((data) => console.log(data));
    },
    data() {
        return {
            moutains: []
        }
    }
}




</script>