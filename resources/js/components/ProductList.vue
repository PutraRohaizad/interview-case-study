<template>
    <div>
        <div class="container">
            <div id="message" class="alert alert-success" hidden>
                Success
                <button
                    type="button"
                    class="close"
                    data-dismiss="alert"
                    aria-label="Close"
                >
                    <span aria-hidden="true">&times;</span>
                </button>
            </div>
            <br />
            <br />
            <br />
            <table
                class="table table-card table-hover table-striped table-bordered"
            >
                <thead>
                    <tr>
                        <th scope="col">#</th>
                        <th scope="col">Name</th>
                        <th scope="col">Price</th>
                        <th scope="col">Action</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(product, index) in products" :key="product.id">
                        <th scope="row">{{ index + 1 }}</th>
                        <td>{{ product.name }}</td>
                        <td>{{ product.price }}</td>
                        <td>
                            <button
                                class="btn btn-danger"
                                type="button"
                                @click.prevent="deleteData(product.id)"
                            >
                                Delete
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>
            <add-form v-on:addData="addData($event)"></add-form>
        </div>
    </div>
</template>

<script>
export default {
    name: "productlist",
    // props: ["products"],
    data() {
        return {
            products: ""
        };
    },
    created() {
        this.fetchData();
    },
    methods: {
        fetchData() {
            axios
                .get(`/fetch`)
                .then(res => (this.products = res.data))
                .catch(err => console.log(err));
        },
        deleteData(id) {
            axios
                .post(`/delete-product-list/${id}`)
                .then(res => {
                    const message = document.querySelector("#message");
                    // console.log(res);
                    message.hidden = false;
                    this.fetchData();
                })
                .catch(err => console.log(err));
        },
        addData(object) {

            axios
                .post("/add-product-list", {
                    body: {
                        name: object.name,
                        price: object.price,
                    }
                })
                .then(res => {

                   
                    const message = document.querySelector("#message");
                    message.hidden = false;
                    this.fetchData();
                })
                .catch(err => console.log(err));
        }
    }
};
</script>

<style></style>
