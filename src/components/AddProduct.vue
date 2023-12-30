<template>
    <div id="addForm">
        <form @submit="handleAdd">
            <div class="form-group">
                <label for="id">Category Id</label>
                <input v-model="product.categoryId" class="form-control" type="text" id="id">
            </div>
            <div class="form-group">
                <label for="id">Product Name</label>
                <input v-model="product.productName" class="form-control" type="text" id="id">
            </div>
            <div class="form-group">
                <label for="id">Quantity Per Unit</label>
                <input v-model="product.quantityPerUnit" class="form-control" type="text" id="id">
            </div>
            <div class="form-group">
                <label for="id">Unit Price</label>
                <input v-model="product.unitPrice" class="form-control" type="text" id="id">
            </div>
            <div class="form-group">
                <label for="id">Units In Stock</label>
                <input v-model="product.unitsInStock" class="form-control" type="text" id="id">
            </div>
            <button type="submit" class="btn btn-sm btn-success">Add</button>
        </form>
    </div>
</template>

<script>
export default {
    name:'add-product',
    data(){
        return{
            product:{
                id: '',
                categoryId: '',
                productName: '',
                quantityPerUnit: '',
                unitPrice: '',
                unitsInStock: '',
            }
        }
    },
    methods:{
        handleAdd(){
            this.$emit("add:product", this.product)
        }
    }
}
</script>

<style scoped>
    #addForm{
        margin: 100px;
    }
</style>