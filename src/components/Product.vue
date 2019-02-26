<template>
  <div>
  <v-list-tile><span>{{product.name}}</span> ({{product.quantity}})
    <v-spacer></v-spacer>
    <v-btn flat color="red lighten-1" v-on:click="$emit('remove', product.id)">Delete</v-btn>
  </v-list-tile>
    <v-divider></v-divider>
  </div>

</template>

<script>
    export default {
        name: 'Product',
        props: {
            product: {
                type: Object,
                default: () => {
                }
            }
        }


    }
</script>

<style scoped>

</style>
