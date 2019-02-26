<template>
  <div id="app">
    <v-toolbar color="teal lighten-1" app height="100">
      <v-toolbar-title class="display-1 white--text">
        List of products
      </v-toolbar-title>
    </v-toolbar>
    <v-content>
      <v-layout row>
        <v-flex xs12 sm6 offset-sm3>
          <v-card class="mt-3 pa-3">
            <v-list three-line>
              <Product v-bind:product="product" v-bind:key="product.id" v-for="product in products"
                       v-on:remove="removeItem"/>
            </v-list>
            <p class="subheading sort">Sort by</p>
            <v-card-actions class="justify-center">
              <v-btn color="teal lighten-1 white--text" v-on:click="sortProducts('name')">names</v-btn>
              <v-btn color="teal lighten-1 white--text" v-on:click="sortProducts('quantity')">quantity</v-btn>
            </v-card-actions>
          </v-card>
          <Form v-on:added="addToList"/>
        </v-flex>
      </v-layout>
    </v-content>
  </div>
</template>

<script>
    import Product from './components/Product';
    import Form from './components/Form';

    export default {
        name: 'app',
        components: {
            Product,
            Form
        },
        data() {
            return {
                products: [
                    {
                        id: 0,
                        name: 'Cheese',
                        quantity: 1
                    },
                    {
                        id: 1,
                        name: 'Bread',
                        quantity: 3
                    },
                    {
                        id: 2,
                        name: 'Ham',
                        quantity: 2
                    }
                ]
            }
        },
        methods: {
            addToList(product) {
                this.products.push({
                    id: this.products.length,
                    name: product.name,
                    quantity: product.quantity
                });

            },
            removeItem(id) {
                this.products = this.products.filter(el => el.id !== id);

            },
            sortProducts(type) {
                if (type === 'name') {
                    this.products = this.products.sort((a, b) => a.name.localeCompare(b.name));
                }
                else if (type === 'quantity') {
                    this.products = this.products.sort((a, b) => a.quantity - b.quantity)
                }

            }
        }
    }

</script>

<style>
  #app {
    font-family: Roboto, sans-serif;
  }

  .sort {
    text-align: center;
  }

</style>
