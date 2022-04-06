<template>
    <nav>
        <ul>
            <li v-for="page in pages" :key="page">
                <slot :page="page"></slot>
            </li>
        </ul>
    </nav>
</template>

<script>
export default {
    data() {
        return {
            pages: ['Overview', 'Orders', 'Best Sellers']
        }
    }
}
</script>

<style scoped>
    ul {
        list-style: none;
        padding: 0;
    }

    li {
        padding: 10px 0;
        cursor: pointer;
    }

    li:hover {
        color:#ff0000;
    }
</style>
