<template>
    <div class="container">
        <form @submit.prevent="addData" method="POST">
            <div class="form-group">
                <label for="name">Name</label>
                <input
                    v-model="name"
                    type="text"
                    class="form-control"
                    id="name"
                    placeholder="Enter name"
                />
            </div>
             <div class="form-group">
                <label for="name">Price</label>
                <input
                     v-model="price"
                    type="number"
                    class="form-control"
                    id="price"
                    placeholder="Enter price"
                />
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'addform',
    data(){
        return{
            name : "",
            price : "",
        }
    },
    methods:{
        addData(){
            this.$emit('addData', {
                name: this.name,
                price: this.price,
            })
        }
    }
};
</script>

<style></style>
