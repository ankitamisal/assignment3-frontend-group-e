
<template>
  <main class="flex justify-center w-full h-screen">
    <div>
      <div id="from" style="display:none">
        <form method="post" class="bg-gray-100 border-black rounded-lg border-2 px-12 ">
          <table>
            <h2 class="text-teal-900 text-xl font-bold pt-6">Book Management</h2>
            <hr />
            <br />
            <label class="pt-10 py-10" for="book-name">Book name:</label><br />
            <input type="text" id="book-name" name="book-name" v-model="state.data.book_name"
              placeholder="Enter your Book name" />
            <span v-for="error in v$.book_name.$errors" :key="error.$uid" class=" text-red-700">{{  error.$message 
              }}</span>
            <br /><br />

            <label for="book-price">Book price:</label><br />
            <input type="number" id="book-price" name="book-price" v-model="state.data.price"
              placeholder="Enter Book price" />
            <span v-for="error in v$.price.$errors" :key="error.$uid" class=" text-red-700">{{  error.$message 
              }}</span>
            <br /><br />
            <label for="book-author">Book Author: </label><br />
            <input type="text" id="book-author" name="address" v-model="state.data.author"
              placeholder="Enter your Aouther" />
            <span v-for="error in v$.author.$errors" :key="error.$uid" class=" text-red-700">{{  error.$message 
              }}</span>


            <br /><br />
            <label for="book-number">Book Number: </label><br />
            <input type="number" id="book-number" name="book-number" v-model="state.data.book_number"
              placeholder="Enter your number" />
            <span v-for="error in v$.book_number.$errors" :key="error.$uid" class=" text-red-700">{{  error.$message 
              }}</span>

            <br /><br />
            <label for="language">Select Language :</label>
            <select name="language" id="language" v-model="state.Language" multiple>
              <option disabled value=""> select language</option>
              <option value="Marathi ">Marathi</option>
              <option value="English">English</option>
              <option value="Hindi">Hindi</option>
            </select>
            <div>
              <button
                class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
                type="button" @click="onFormSubmit()">
                {{  state.Submit  }}
              </button>

              <button class="py-1 px-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
                @click="recet1()">
                Reset
              </button>
            </div>
          </table>
        </form>
      </div>
      <!-- <button class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
        type="submit" @click="getdata">
        Get Data
      </button> -->
      <br /><button class=" m-auto hover:bg-green-600" @click="adddata()">Add Data</button>
      <div>{{  state.errorBack  }}</div>

      <table class="list">
        <thead>
          <tr>
            <th class="px-4 border-black rounded-lg border-2">id</th>
            <th class="px-4 border-black rounded-lg border-2">Book Name</th>
            <th class="px-4 border-black rounded-lg border-2">Book Price</th>
            <th class="px-4 border-black rounded-lg border-2">Book Author</th>
            <th class="px-4 border-black rounded-lg border-2">Language</th>
            <th class="px-4 border-black rounded-lg border-2">Book Number</th>
            <!-- <th class="px-4 border-black rounded-lg border-2">Book Image</th> -->
            <th class="px-4 border-black rounded-lg border-2">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) of state.allBooks" :key="item.id">
            <td class="px-4 border-black rounded-lg border-2">{{  item.book_id  }}</td>
            <td class="px-4 border-black rounded-lg border-2">{{  item.book_name  }}</td>
            <td class="px-4 border-black rounded-lg border-2">{{  item.author  }}</td>
            <td class="px-4 border-black rounded-lg border-2">{{  item.price  }}</td>
            <td class="px-4 border-black rounded-lg border-2">{{  state.Language  }}</td>
            <td class="px-4 border-black rounded-lg border-2">{{  item.book_number  }}</td>
            <!-- <td class="px-4 border-black rounded-lg border-2">{{ item.book_image }}</td> -->
            <td class="px-4 border-black rounded-lg border-2">{{  item.Action  }}
              <button class="mx-3 hover:bg-red-600  " @click="onDeleteOfBook(item.book_id)">
                Delete
              </button>
              <button class="mx-3 hover:bg-green-600" @click="onClickOfEditBook(item.book_id)">
                Edit
              </button>
            </td>
          </tr>
        </tbody>
      </table>


    </div>
  </main>
</template>

<script lang="ts">
import useVuelidate, {
  required,
  minLength,
  alpha,
  maxLength,
} from '~/utils/vuelidate/useVuelidate';
</script>


<script setup lang="ts">
let state = reactive({
  Submit: "Submit",
  select: true,
  allBooks: [],
  book_id: "",
  data: {
    book_name: "",
    author: "",
    price: "",
    book_number: ""

  },
  errorBack: '',
  Language: [],
  getLanguage: {}
});



const rules = computed(() => {
  return {
    book_name: {
      required,
      alpha,
      minLength: minLength(3),
      maxLength: maxLength(35),
    },
    author: {
      required,
      alpha,
      minLength: minLength(3),
      maxLength: maxLength(35),
    },
    price: { required },
    book_number: { required }
  };
});
const v$ = useVuelidate(rules, state.data);

function adddata() {
  document.getElementById("from").style.display = "block";
}


getBookAPI();

// Calling Get API
// function getBooks() {
//   getBookAPI().then((data: any) => {
//     state.allBooks = data;
//   });
// }


// GET API
async function getBookAPI() {
  let res: any = await $fetch('http://localhost:3001/language');
  state.Language = res;


  state.allBooks = await $fetch('http://localhost:3001/book');

}

function clareData() {

  state.data.book_name = "";
  state.data.author = "";
  state.data.price = "";
  state.data.book_number = "";
  state.book_id = "";
}

function recet1() {
  clareData();
  state.Submit = "Submit";
  state.select = true;
}

// POST API
async function onFormSubmit() {
  console.log(state.Language);

  console.log(state.select);

  const result = await v$.value.$validate();
  if (result === true) {

    // const { error: backError, data: posts } = await useFetch('http://localhost:3001/book', { method: 'POST', body: JSON.stringify(state.data) })

    // state.errorBack = backError;


    if (state.select === true) {
      const sampleData = state.data;
      const response = await $fetch('http://localhost:3001/book', {
        method: 'POST',
        body: JSON.stringify(sampleData),
      });

      let language = { Language: state.Language }
      const respons = await $fetch('http://localhost:3001/language', {
        method: 'POST',
        body: JSON.stringify(language),
      });

      getBookAPI();
      clareData();
      alert("Data added successfully:");
      document.getElementById("from").style.display = "none";


    } else {
      let bookId = state.book_id;
      putData(bookId);
      alert(`data update successfully ${bookId}`);
      clareData();
      state.select = true;
      getBookAPI();
      document.getElementById("from").style.display = "none";
    }
  }

  // PATCH API

}

async function onClickOfEditBook(bookId) {
  document.getElementById("from").style.display = "block";
  location.href = "#from";
  state.Submit = "Update"
  state.select = false;
  const edit: any = await $fetch('http://localhost:3001/book/' + bookId)
  state.data.book_name = edit.book_name;
  state.data.author = edit.author;
  state.data.price = edit.price;
  state.data.book_number = edit.book_number;
  state.book_id = edit.book_id;
}
async function putData(bookId) {
  state.Submit = "Submit";
  state.select = true;
  const sample = state.data;
  const response = await $fetch('http://localhost:3001/book/' + bookId, {
    method: 'PATCH',
    body: JSON.stringify(sample),
  });
  getBookAPI();
  document.getElementById("from").style.display = "none";
  clareData();
}

// Delete API
async function onDeleteOfBook(bookId) {
  const delet = confirm(`do you want delete this id ${bookId}`);
  if (delet == true) {
    await $fetch('http://localhost:3001/book/' + bookId, {
      method: 'DELETE'
    });

    getBookAPI();
    alert(`id ${bookId} was deleted`);
  }
}

</script>


