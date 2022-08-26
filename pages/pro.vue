<template>
    <div>
        <h1 class="font-bold text-center text-2xl mt-10 text-green-400">Product Management</h1>
        <div class="  grid grid-cols-2  ">
            <div class="border-black  border-2 m-8 p-8">
                <form @submit="formSubmit" class="bg-green-100 border-green-400 rounded-lg border-2 px-12">
                    <table>
                        <h2 class="text-teal-900 text-xl font-bold pt-6">“Add Product” </h2>
                        <hr />
                        <label class="pt-10 py-10 " for="ProductName">Product Name:</label><br />
                        <input type="text" id="ProductName" name="ProductName" placeholder="" /><br /><br />
                        <label for="Price">Price:</label><br />
                        <input type="number" id="Price" name="Price" placeholder="" /><br /><br />
                        <label for="state">Stock:</label>
                        <select class="p-1" name="Stock" id="Stock">
                            <option value="Available" selected>Available</option>
                            <option value="Out of Stock ">Out of Stock </option>
                        </select><br /><br />
                        <label for="state">Size:</label>
                        <select class="p-1" name="Size" id="Size">
                            <option value="XS">XS</option>
                            <option value="S ">S</option>
                            <option value="M" selected>M</option>
                            <option value="L">L</option>
                            <option value="XL">XL</option>
                        </select><br><br>
                        <label for="Image">Upload Image</label><br><br>
                        <input type="file" id="Image" name="Image"><br><br>
                        <div class="mt-10">
                            <button
                                class="py-1 px-5 mr-5 bg-black hover:bg-blue-400 text-white font-bold text-center rounded-md mb-3"
                                type="submit" @click="formSubmit">Add Product</button>
                            <button
                                class="py-1 px-5 bg-black hover:bg-blue-400 text-white font-bold text-center rounded-md mb-3"
                                type="reset"> Reset </button>
                        </div>
                    </table>
                </form>
            </div>
            <div class="border-black  border-2 m-8 p-8">
                <table class="list">
                    <tr>
                        <!-- <th class="px-4 border-black rounded-lg border-2">id</th> -->
                        <th class="px-4 border-green-400 rounded-lg border-4">ProductName</th>
                        <th class="px-4 border-green-400 rounded-lg border-4">Price</th>
                        <th class="px-4 border-green-400 rounded-lg border-4">Stock</th>
                        <th class="px-4 border-green-400 rounded-lg border-4">Size</th>
                        <th class="px-4 border-green-400 rounded-lg border-4">Image</th>
                        <th class="px-4 border-green-400 rounded-lg border-4">Action</th>
                    </tr>
                    <tr v-for="(item, index) in state.product" v-bind:index="index" :key="item">
                        <td class="px-4 border-green-400 rounded-lg border-4">{{ item.productName }}</td>
                        <td class="px-4 border-green-400 rounded-lg border-4">{{ item.price }}</td>
                        <td class="px-4 border-green-400 rounded-lg border-4">{{ item.stock }}</td>
                        <td class="px-4 border-green-400 rounded-lg border-4">{{ item.size }}</td>
                        <td class="px-4 border-green-400 rounded-lg border-4">
                            <img src="{{item.Image}}" alt="" srcset="">
                        </td>
                        <td class="px-4 border-black rounded-lg border-2">{{ item.Action }}
                            <button class=" mx-3" @click="onDeleteOfBook(item.book_id)">
                                Delete
                            </button>
                            <button class="mx-3" @click="onClickOfEditBook(item.book_id)">
                                Edit
                            </button>
                        </td>
                        <!-- <td class="px-4 border-green-400 rounded-lg border-4">{{ item.Action }}
                            <button class="mx-3 rounded-lg bg-red-600 hover:bg-red-700 text-white w-20"
                                @click="productDelete(index)">
                                Delete
                            </button>
                            <button class="mx-3 rounded-lg bg-green-600 hover:bg-green-600 text-white w-20"
                                @click="onEdit(index)">
                                Edit
                            </button>
                        </td> -->
                    </tr>
                </table>
            </div>
        </div>
        <!-- <p>{{product}}</p> -->
    </div>
</template>
<script setup>
//import { stat } from "fs/promises";

let state = reactive({
    product: []
});
getBookAPI();
// Calling Get API
// function getBooks() {
//   getBookAPI().then((data: any) => {
//     state.product = data;
//   });
// }
// GET API
async function getBookAPI() {
    state.product = await $fetch('http://localhost:8080/feed/allData');
    //console.log(product)

}
// POST API
async function onFormSubmit() {
    const sampleData = {
        "book_id": state.product.length,
        "productName": "maratrhi" + state.product.length,
        "price": "ankita" + state.product.length,
        "stock": 200 + state.product.length,
        "size": "ghjgj" + state.product.length,
        "image": "91001" + state.product.length
    };
    const response = await $fetch('http://localhost:3001/book', {
        method: 'POST',
        body: JSON.stringify(sampleData),
    });
    getBookAPI();
}
// PATCH API
async function onClickOfEditBook(bookId) {
    const sampleData = {
        "id": bookId,
        "book_name": "Shaktiman" + bookId,
        "author": "ankita" + state.product.length,
        "price": 200 + state.product.length,
        "book_image": "ghjgj" + state.product.length,
        "book_number": "91001" + state.product.length
    };
    const response = await $fetch('http://localhost:3001/book/' + bookId, {
        method: 'PATCH',
        body: JSON.stringify(sampleData),
    });
    getBookAPI();
}
// Delete API
async function onDeleteOfBook(bookId) {
    await $fetch('http://localhost:3000/feed' + bookId, {
        method: 'DELETE'
    });
    getBookAPI();
}


// function useFetch(
//     url: "http://localhost:8080/feed/allData",
// )
</script>