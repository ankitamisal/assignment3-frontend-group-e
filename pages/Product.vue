<template>
  <div>
    <h1 class="font-bold text-center text-2xl mt-10 text-green-400">
      Product Management
    </h1>

    <div class="px-7 text-red-500">
      <ul>
        <li v-for="(error, index) in mydata.serverErrors" :key="index">
          {{ error }}
        </li>
      </ul>
      <!-- <ul>
        <li v-for="(error, index) in mydata.serverErrors" :key="index"></li>
      </ul> -->
    </div>
    <!-- <div class="grid grid-cols-2"> -->
    <div class="border-black border-2 m-8 p-8">
      <!-- @submit="onFormSubmit1()" -->
      <form
        @submit.prevent="onFormSubmit1()"
        class="bg-teal-600 border-green-400 rounded-lg border-2 px-12"
      >
        <table>
          <h2 class="text-black text-center text-xl font-bold pt-6">
            Fill Form For Create Product
          </h2>
          <hr />
          <label class="pt-10 py-10" for="ProductName">Product Name:</label
          ><br />
          <input
            v-model="mydata.product.productName"
            type="text"
            ref="productName"
            id="ProductName"
            name="ProductName"
            placeholder="Enter Product Name"
            class="rounded-md"
          />
          <!-- <span
            v-for="error in v$.productName.$errors"
            :key="error.$uid"
            class="text-red-700"
            >{{ error.$messages }}</span
          > -->
          <span
            v-for="error in v$.productName.$errors"
            :key="error.$uid"
            class="text-red-600"
            >{{ error.$message }}
          </span>

          <br /><br />
          <label for="Price">Price:</label
          ><br />
          <input
            v-model="mydata.product.price"
            type="number"
            ref="price"
            id="Price"
            name="Price"
            placeholder=""
          />
          <span
            v-for="error in v$.price.$errors"
            :key="error.$uid"
            class="text-red-600"
            >{{ error.$message }} </span
          ><br /><br />
          <label for="Stock">Stock:</label>
          <select
            v-model="mydata.product.stock"
            class="p-1"
            name="Stock"
            id="Stock"
            ref="stock"
          >
            <option value="Available" selected>Available</option>
            <option value="OutOfStock">Out of Stock</option>
          </select>
          <span
            v-for="error in v$.stock.$errors"
            :key="error.$uid"
            class="text-red-600"
            >{{ error.$message }} </span
          ><br /><br />
          <label for="Size">Size:</label>

          <!-- <td> -->
          <select
            v-model="mydata.id"
            multiple="true"
            @change="submitUserdataId(mydata.id)"
            class="font-bold sm:w-52 p-2 rounded-md py-2 pr-4 ml-2 mb-2"
          >
            <option v-for="i in mydata.size" :key="i.id" :value="i.id">
              {{ i.id }}.{{ i.size }}
            </option>
          </select>
          {{
            mydata.id
          }}

          <br /><br />
          <label for="Image">Upload Image</label
          ><br /><br />
          <input type="file" id="Image" name="Image" /><br /><br />
          <div class="mt-10">
            <button
              class="py-1 px-5 mr-5 bg-black hover:bg-blue-400 text-white font-bold text-center rounded-md mb-3"
              type="submit"
            >
              Add Product
            </button>
            <!-- \@click="onFormSubmit1()" -->
            <button
              class="py-1 px-5 bg-black hover:bg-blue-400 text-white font-bold text-center rounded-md mb-3"
              type="reset"
            >
              Reset
            </button>
          </div>
        </table>
        <span v-for="error in v$.$errors" :key="error.$uid"
          >{{ error.$property }}----{{ error.$message }}</span
        >
      </form>
    </div>

    <div class="border-black border-2 m-8 p-8">
      <table class="list">
        <tr>
          <!-- <th class="px-4 border-black rounded-lg border-2">id</th> -->
          <th class="px-4 border-green-400 rounded-lg border-4">ProductId</th>
          <th class="px-4 border-green-400 rounded-lg border-4">ProductName</th>
          <th class="px-4 border-green-400 rounded-lg border-4">Price</th>
          <th class="px-4 border-green-400 rounded-lg border-4">Stock</th>
          <th class="px-4 border-green-400 rounded-lg border-4">Size</th>
          <th class="px-4 border-green-400 rounded-lg border-4">Image</th>
          <th class="px-4 border-green-400 rounded-lg border-4">Action</th>
        </tr>
        <tr v-for="item in mydata.allProduct" :key="item.id">
          <!-- <td class="px-4 border-black rounded-lg border-2">{{item.id=i+1}}</td> -->
          <td class="px-4 border-green-400 rounded-lg border-4">
            {{ item.id }}
          </td>
          <td class="px-4 border-green-400 rounded-lg border-4">
            {{ item.productName }}
          </td>
          <td class="px-4 border-green-400 rounded-lg border-4">
            {{ item.price }}
          </td>
          <td class="px-4 border-green-400 rounded-lg border-4">
            {{ item.stock }}
          </td>
          <td class="px-4 border-green-400 rounded-lg border-4">
            {{ item.size }}
          </td>
          <td class="px-4 border-green-400 rounded-lg border-4">
            <img src="{{item.image}}" alt="" srcset="" />
          </td>
          <td class="px-4 border-green-400 rounded-lg border-4">
            {{ item.Action }}
            <button
              class="mx-3 rounded-lg bg-red-600 hover:bg-red-700 text-white w-20"
              @click="onDeleteOfProduct(item.id)"
            >
              Delete
            </button>
            <button
              type="submit"
              class="mx-3 rounded-lg bg-green-600 hover:bg-green-600 text-white w-20"
              @click="editProduct(item.id)"
            >
              Edit
            </button>
          </td>
        </tr>
      </table>
    </div>

    <p>
      {{ mydata.product.statusCode }}
    </p>
  </div>
</template>
<script setup lang="ts">
//////////////////////////////////////////////validation//////////////////////////////////////
//import useVuelidate, { required, email } from "~/utils/vuelidate/useVuelidate";
//import useVuelidate, { required, email } from "../utils/vuelidate/useVuelidate";
import useVuelidate from "@vuelidate/core";
import { maxLength, minLength, required, alpha } from "@vuelidate/validators";

//////////////////////////////////////////////////////////////////////////////////////////////

const mydata = reactive({
  allProduct: [],
  product: {
    productName: "",
    price: "",
    stock: "",
  },
  size: [],
  id: [],
  serverErrors: [],
});

var productId;
const rules = computed(() => {
  return {
    productName: {
      required,
      alpha,

      minLenght: minLength(5),
      maxLength: maxLength(15),
    },
    price: { required, maxLength: maxLength(9) },
    stock: { required },
    //size: { required },
  };

  //   //password: { required },
});

const v$ = useVuelidate(rules, mydata.product);

getProductAPI();

// GET API
async function getProductAPI() {
  mydata.allProduct = await $fetch("http://localhost:3001/product/allData");
}
console.log(mydata.allProduct);
getSize();

// GET API
async function getSize() {
  mydata.size = await $fetch("http://localhost:3001/size/allData");
  //console.log(mydata.size);
}
console.log(getSize());

async function onFormSubmit1() {
  const result = await v$.value.$validate();
  if (result) {
    await $fetch("http://localhost:3001/product", {
      method: "POST",
      body: JSON.stringify(mydata.product),
    })
      .then((res) => {
        productId = res.id;
        categoriesApi();
      })
      .catch((error) => {
        console.log(error);
        mydata.serverErrors = error.data.message;
      });
  }
  // }
  getProductAPI();
  getSize();
}

async function editProduct(id) {
  console.log("top console from patch api");
  let productEdit = mydata.allProduct.filter((product) => {
    if (product.id == id) {
      mydata.product.id = product.id;
      mydata.product.productName = product.productName;
      mydata.product.price = product.price;
      mydata.product.stock = product.stock;
      mydata.product.size = product.size;
      return product;
      console.log("patch api");
    }
  });
  console.log(productEdit);
  // const response = await $fetch("http://localhost:3001/product/" + id, {
  //   method: "PATCH",
  //   body: JSON.stringify(mydata.product),
  // });
  getProductAPI();
}
getProductAPI();

async function onDeleteOfProduct(id) {
  await $fetch("http://localhost:3001/product/" + id, {
    method: "DELETE",
  });
  getProductAPI();
}

async function categoriesApi() {
  console.log("product working line no 390", productId);
  console.log(mydata.id);
  mydata.id.forEach((product) => {
    const obj = {
      productPostId: productId,
      productCategoryId: product,
    };
    var response = $fetch("http://localhost:3001/categories", {
      method: "POST",
      body: JSON.stringify(obj),
    }).then((res) => {
      console.log("data", obj);
    });
  });
}
</script>
