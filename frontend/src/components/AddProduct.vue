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
            <button class="button is-success" @click="saveProduct">SAVE</button>
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
    methods: {
        //create new product
        async saveProduct () {
            try {
                await axios.post('http://localhost:5000/products',{
                    product_name: this.productname,
                    product_price: this.productPrice
                });
                (this.productname=""),
                (this.productPrice="");
                this.$router.push("/")
            } catch (error) {
                console.log(error)
            }
        }
    },
}
</script>
<style>
</style>