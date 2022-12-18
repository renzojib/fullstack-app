<template>
    <div>
        <router-link :to="{name:'Create'}" class="button is-success mt-5">Add New</router-link>
        <table class="table is-striped is-bordered mt-2 is-fullwidth">
            <thead>
                <th>Product Name</th>
                <th>Price</th>
                <th class="has-text-centered">Actions</th>
            </thead>
            <tbody>
                <tr v-for="item in items" :key="item.produc_id">
                    <td>
                        {{item.product_name}}
                    </td>
                    <td>
                        {{item.product_price}}
                    </td>
                    <td class="has-text-centered">
                        <router-link :to="{name:'Edit', params:{id:item.produc_id}}" class="button is-info is-small">Edit</router-link>
                        <a class="button is-danger is-small" @click="deleteProduct(item.produc_id)">Delete</a>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
//import axios
import axios from "axios";
export default {
    data () {
        return {
            items: []
        }
    },
    created() {
        this.getProducts();
    },
    methods: {
        //get all products
        async getProducts () {
            try {
                const response = await axios.get("http://localhost:5000/products")
                this.items=response.data
            } catch (error) {
                console.log(error)
            }
        },

        //delete product
        async deleteProduct(id) {
            try {
                await axios.delete(`http://localhost:5000/products/${id}`)
                this.getProducts()
            } catch (error) {

            }
        }
    },

}
</script>

<style>
</style>