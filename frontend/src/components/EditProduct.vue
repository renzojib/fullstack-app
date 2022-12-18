<template>
    <div>
        <div class="field">
            <label class="label">Product Name</label>
            <div class="control">
                <input 
                type="text" 
                class="input" 
                placeholder="Product Name" 
                v-model="productname">
            </div>
        </div>
        <div class="field">
            <label class="label">Product Name</label>
            <div class="control">
                <input 
                type="text" 
                class="input" 
                placeholder="Price" 
                v-model="productPrice">
            </div>
        </div>
        <div class="control">
            <button class="button is-success" @click="updateProduct">Update</button>
        </div>
    </div>
</template>
<script>
//import axios
import axios from 'axios'
export default {
    data () {
        return {
            productname: '',
            productPrice: ''
        }
    },
    created () {
        this.getProductById()
    },
    methods: {
        //get product by id
        async getProductById () {
            try {
                const response = await axios.get(
                    `http://localhost:5000/products/${this.$route.params.id}`
                )
                this.productname = response.data.product_name
                this.productPrice = response.data.product_price

            } catch (error) {
                console.log(error)
            }
        },

        //update product
        async updateProduct () {
            try {
                await axios.put(
                    `http://localhost:5000/products/${this.$route.params.id}`,
                    {
                        product_name: this.productname,
                        product_price: this.productPrice,
                    }
                );
                (this.productname =''),
                (this.productPrice='');
                this.$router.push('/')
            } catch (error) {
                console.log(error)
            }
        }
    },
}
</script>
<style>
</style>