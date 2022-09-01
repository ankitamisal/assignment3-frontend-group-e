<template>
  <div>
    <h1 class="font-bold text-center text-2xl mt-10 text-green-400">
      Product Management
    </h1>
    <!-- <div class="grid grid-cols-2"> -->
    <div class="border-black border-2 m-8 p-8">
      <!-- @submit="onFormSubmit1()" -->
      <form
        @submit.prevent="onFormSubmit1()"
        class="bg-green-100 border-green-400 rounded-lg border-2 px-12"
      >
        <table>
          <h2 class="text-teal-900 text-xl font-bold pt-6">“Add Product”</h2>
          <hr />
          <label class="pt-10 py-10" for="ProductName">Product Name:</label
          ><br />
          <input
            v-model="mydata.product.productName"
            type="text"
            ref="productName"
            id="ProductName"
            name="ProductName"
            placeholder=""
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
          <select
            v-model="mydata.id"
            class="p-1"
            name="Size"
            id="Size"
            ref="size"
            multiple
          >
            <!-- <option value="XS">XS</option> -->
            <option value="S">S</option>
            <option value="M" selected>M</option>
            <option value="L">L</option>
            <option value="XL">XL</option>
          </select>
          <!-- <span
            v-for="error in v$.size.$errors"
            :key="error.$uid"
            class="text-red-600"
            >{{ error.$message }}
          </span> -->
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

      <!-- </div> -->
      <!-- <p>{{ allProduct }}</p> -->
    </p>
    <!-- <p>{{ message }}</p> -->
  </div>
</template>
<script setup lang="ts">
//////////////////////////////////////////////validation//////////////////////////////////////
//import useVuelidate, { required, email } from "~/utils/vuelidate/useVuelidate";
//import useVuelidate, { required, email } from "../utils/vuelidate/useVuelidate";
import useVuelidate from "@vuelidate/core";
import { maxLength, minLength, required } from "@vuelidate/validators";
// const state = reactive({
//   form: {
//     productName: "",
//     password: "",
//   },
// });

// /**
//  * validation rules
//  */
// const rules = {
//   productName: { required },
//   //password: { required },
// };
// const v$ = useVuelidate(rules, state.form);

// /**
//  * login
//  *
//  * @returns {Promise<void>}
//  */
// async function login(): Promise<void> {
//   const isFormCorrect = await v$.value.$validate();
//   if (!isFormCorrect) {
//     // Show error messages
//     alert("valid valid FirstName");

//     console.log("please enter data in valid formate");
//     return;
//   }

//   //     const payload = { ...state.form };
//   // Call API with payload
// }

//////////////////////////////////////////////////////////////////////////////////////////////
// import { ref } from "vue";
// const productName = ref("");
// const price = ref("");
// const stock = ref("");
// const size = ref("");
// const emp_contact = ref("");
// const emp_salary = ref("");
// const emp_dept = ref("");

// const productName =
const mydata = reactive({
  allProduct: [],
  product: {
    productName: "",
    price: "",
    stock: "",
    size: "",
    // emp_contact: '',
    // emp_salary: '',
    // emp_dept: '',
  },
  sizes: [],
  id: [],
});
// const rules = {
//   productName: { required },
//   price: { required },
//   stock: { required },
//   size: { required },
//   //   //password: { required },
// };
const rules = computed(() => {
  return {
    productName: {
      required,
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
//const v$ = useVuelidate(rules, mydata.product );

/**
 * login
 *
 *
//  */
// async function login(): Promise<void> {
//   const isFormCorrect = await v$.value.$validate();
//   if (!isFormCorrect) {
//     // Show error messages
//     alert("valid valid FirstName");

//     console.log("please enter data in valid formate");
//     return;
//   }

//     const payload = { ...state.form };
// Call API with payload
// }
// const a = async () => {
//   const result = await v$.validate;
// };
getProductAPI();

// GET API
async function getProductAPI() {
  mydata.allProduct = await $fetch("http://localhost:3001/product/allData");
}

getSize();

// GET API
async function getSize() {
  mydata.sizes = await $fetch("localhost:3001/size/allData");
}

//POST API
// async function onFormSubmit1() {
//   console.log(mydata.product);
//   const result = await v$.value.$validate();
//   if (result) {
//     alert("product created");
//   } else {
//     alert("product not created");
//   }
//   await $fetch("http://localhost:3001/product", {
//     method: "POST",
//     body: JSON.stringify(mydata.product),
//   });

//   getProductAPI();
// }

async function onFormSubmit1() {
  try {
    console.log(mydata.product);
    const result = await v$.value.$validate();
    if (result) {
      alert("product created");
    } else {
      alert("product not created");
    }
    await $fetch("http://localhost:3001/product", {
      method: "POST",
      body: JSON.stringify(mydata.product),
    }).then((res) => {
      console.log("id", res.id);
      id = res.id;
      relationalTableValues();
    });
    console.log("hiii amit");
  } catch (err) {
    // document.write();
    console.log({
      statusCode: 404,
      message: "User not found",
    });
  }
  getProductAPI();
}

// async function onFormSubmit1() {
//   const result = await v$.value.$validate();
//   if (isEdit === true) {
//     await $fetch("http://localhost:3001/product/" + id,  {
//       method: "PUT",
//       body: mydata.Book,
//     });
//     isEdit = false;
//     getBookAPI();
//   } else {
//     if (result) {
//       await $fetch("http://localhost:3001/product", {
//         method: "POST",
//         body: mydata.Book,
//       });
//       getUserApi();
//     }
//   }
// // PATCH API

// let edit = mydata.product;
// async function onClickOfEditProduct(id) {
//   const sampleData = {
//     id: id,
//     productName: "Shaktiman" + id,
//     price: "ankita" + mydata.allProduct.length,
//     stock: 200 + mydata.allProduct.length,
//     size: "ghjgj" + mydata.allProduct.length,
//     image: "91001" + mydata.allProduct.length,
//   };
// const response = await $fetch('http://localhost:3001/product/' + id, {
//     method: 'PATCH',
//     body: JSON.stringify(sampleData),
// });
// getBookAPI();
//   getProductAPI();
// }
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
// // Delete API
async function onDeleteOfProduct(id) {
  await $fetch("http://localhost:3001/product/" + id, {
    method: "DELETE",
  });
  getProductAPI();
}

async function relationalTableValues() {
  console.log("studentId", id);
  console.log(state.id);
  state.id.forEach((subid) => {
    const obj = {
      product: id,
      categories: id,
    };
    var response = $fetch("http://localhost:3001/size", {
      method: "POST",
      body: JSON.stringify(obj),
    }).then((res) => {
      console.log("data", obj);
      // studId = res.student_id;
    });
  });
}
</script>
