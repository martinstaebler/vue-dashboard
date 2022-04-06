<template>
    <article class="stats">
        <h4>Sales Total <span>&#128176;</span></h4>
        <span class="light-text">&euro; {{ totalSalesValue }}</span>
    </article>
</template>


<script>
    export default {
        inject: ['totalSalesValue']
    }
</script>
<style scoped>

</style>