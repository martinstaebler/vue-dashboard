<template>
    <h3 class="page-title">Orders</h3>
    <slot name="total"></slot>
    <section>
        <slot name="default"></slot>
    </section>
</template>

<style scoped>
    .ul-orders {
        list-style: none;
        font-style: italic;
    }

    .order {
        padding: 10px;
        margin: 10px;
        border: 1px solid #ddd;
        border-radius: 5px;
    }
</style>