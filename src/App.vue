<template>
  <div class="app-wrapper">
    <header>
      <h1>The Ultimate Dashboard</h1>
    </header>
    <div class="content">
      <aside>
        <sidebar>
          <template #default="{page}">   <!--  #default="slotProps" //-->
            <a @click="selectedPage=`${page}`">{{ page }}</a>            <!--  {{ slotProps.page }} //-->
          </template>
        </sidebar>
      </aside>
      <main>
        <small><span class="blue">Dashboard</span> &gt; Overview</small>
        <!-- <Overview v-bind:quantityOfItemsSold='32' :totalSalesValue='197' bestSeller='Vue Hoodie Medium' /> //-->
        <!-- <orders>
          <template #total>
            <sales-total>
              <template #icon>
                <span>&#128176;</span>
              </template>
              <template #default>
                <span class="light-text">$ {{ totalSalesValue }}</span>
              </template>
            </sales-total>
          </template>
          <template #default>
            <div class="order-wrapper">
              <div class="order" v-for="order in orders" :key="order.id">
                <p>Order: {{ order.id }}</p>
                <ul class="ul-orders">
                  <li v-for="(item, index) in order.items" :key="item+index">
                    <p>{{ item.name }} - $ {{ item.price }}</p>
                  </li>
                </ul>
              </div>
            </div>
          </template>
        </orders> -->
        <!--<best-sellers>
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
              <tr v-for="{id, quantity, name, price} in sortedItems" :key="id">
                  <td>{{quantity}}</td>
                  <td>{{name}}</td>
                  <td>{{id}}</td>
                  <td>{{price}}</td>
              </tr>
            </tbody>
          </table>
        </best-sellers>//-->
        <component :is="selectedPage.replace(/\s/, '')"></component>
      </main>
    </div>
    {{ quantityOfItemsSold }}
  </div>
</template>

<script>
import Overview from "./views/Overview";
import Sidebar from "./components/Sidebar";
import Orders from "./views/Orders";
import BestSellers from './views/BestSellers.vue';
import SalesTotal from "./components/SalesTotal";
import {orders} from "../order";

export default {
  name: 'App',
  components: {
    Overview,
    Sidebar,
    Orders,
    BestSellers,
    SalesTotal,
  },
  data() {
    return {
      orders,
      selectedPage: 'Overview'
    }
  },
  provide() {
    return {
      quantityOfItemsSold: this.quantityOfItemsSold,
      totalSalesValue: this.totalSalesValue,
      bestSeller: this.sortedItems[0],
      orders: this.orders
    }
    
  },

  computed: {
    sortedItems() {
      const sortedItems = [];
      this.orders.map((order) => {
        order.items.map((item) =>{
          const itemExists = sortedItems.find((sortedItem) => sortedItem.id === item.id)
          if(itemExists){
            itemExists.quantity ++;
            return;
          }
          const newItem = {
            quantity: 1,
            ...item
          }
          
          sortedItems.push(newItem);
        })
      })

      sortedItems.sort((a, b) => a.quantity > b.quantity ? -1 : 1);
      return sortedItems;
    },
    quantityOfItemsSold() {
      let qty = 0;
      this.sortedItems.map((item) => {
        qty += item.quantity;
      })
      return qty;
    },
    totalSalesValue() {
      let total = 0;
      this.orders.map((order) => {
        order.items.map((item) => {
          total += item.price;
        })
      })
      return total;
    }
  }
};
</script>

<style>
.app-wrapper {
  font-family: 'Roboto', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

header {
  background: white;
  border-top: 1px solid #ddd;
  border-bottom: 1px solid #ddd;
}

header h1 {
  font-size: 1.4rem;
}

.content {
  display: flex;
}

aside {
  flex: 1;
  border-right: 1px solid #ddd;
  min-height: 100vh;
}

main {
  flex: 3;
  padding: 1rem;
}

.blue {
 color: rgb(25, 149, 243);
}

h4 {
  margin: 0;
  padding-bottom: 1.6rem;
}

.light-text {
  font-weight: 300;
}

.stats {
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 1rem;
}

</style>
