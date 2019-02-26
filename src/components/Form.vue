<template>
  <v-card class="mt-3">
    <form @submit.prevent="onSubmit()">
      <v-text-field label="product"
                   name="product"
                    class="ml-5 mr-5"
                   v-model="newProduct.name"
                   v-validate="'required'"></v-text-field>
      <v-text-field label="quantity"
                   name="quantity"
                    class="ml-5 mr-5"
                   v-model="newProduct.quantity"
                   v-validate="'required|min_value: 1'"></v-text-field>
      <div class="text-xs-right">
        <v-btn flat color="green lighten-1" type=submit>Add product</v-btn>
      </div>
      <div class="error text--red text--lighten-1 pa-2" v-show="errors.has('product') && touched">
        {{errors.first('product')}}
      </div>
      <div class="error text--red text--lighten-1 pa-2" v-show="errors.has('quantity') && touched">
        {{errors.first('quantity')}}
      </div>
    </form>
  </v-card>
</template>

<script>
    export default {
        name: 'Form',
        data() {
            return {
                newProduct: {
                    name: '',
                    quantity: null
                },
                touched: false
            }
        },
        methods: {
            onSubmit() {
                this.$validator.validateAll().then(result => {
                    if (!result) {
                        this.touched = true;
                        return;
                    }
                    this.$emit('added', this.newProduct);
                    this.newProduct.name = '';
                    this.newProduct.quantity = null;
                    this.touched = false;

                });
                // this.$validator.reset();
            }
        }

    }

</script>

<style scoped>
  .error {
    color: red;
    text-align: center;
    width: 100%;
  }

</style>