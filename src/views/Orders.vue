<template>
    <h3 class="page-title">Orders</h3>
    <slot name="total"></slot>

    <div v-for="order in orders" :key="order.id">
        <table>
            <thead>
                <tr>
                <th>Quantity Sold</th>
                <th>Product Name</th>
                <th>Product Id</th>
                <th>Product Price</th>
                </tr>
            </thead>

            <tbody>
                <tr v-for="item in countItems(order.items)" :key="item.id">
                    <td>{{item.quantity}}</td>
                    <td>{{item.name}}</td>
                    <td>{{item.id}}</td>
                    <td>{{item.price}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        inject: ['orders'],

        computed: {

        },
        methods: {
            countItems(order_items) {
                let reduced_order_items = new Array();

                for (let i = 0; i < order_items.length; i++ ) {
                    let is_there = reduced_order_items.findIndex(x => x.id === order_items[i].id);
                    if ( is_there > -1){
                        reduced_order_items[is_there].quantity += 1;
                    }else {
                        let order = order_items[i];
                        order.quantity = 1;
                        reduced_order_items.push(order);
                    }

                }

                return reduced_order_items;
            }
        }
    };
</script>

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