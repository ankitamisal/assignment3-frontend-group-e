<template>
  <main class="flex justify-center w-full h-screen">
    <div>
      <form method="post" class="bg-gray-100 border-black rounded-lg border-2 px-12">
        <table>
          <h2 class="text-teal-900 text-xl font-bold pt-6">Book Management</h2>
          <hr />
          <br />
          <label class="pt-10 py-10" for="book-name">Book name:</label><br />
          <input type="text" id="book-name" name="book-name" ref="book_name"
            placeholder="Enter your Book name" /><br /><br />
          <label for="book-price">Book price:</label><br />
          <input type="text" id="book-price" name="book-price" ref="book_price"
            placeholder="Enter Book price" /><br /><br />
          <label for="book-author">Book Author: </label><br />
          <input type="text" id="book-author" name="address" ref="book_author" placeholder="Enter your Aouther" />
          <br /><br />
          <label for="book-number">Book Number: </label><br />
          <input type="number" id="book-number" name="book-number" placeholder="Enter your number" />
          <br /><br />
          <label for="book-image">Book Image: </label><br />
          <input type="file" id="book-image" name="book-image" />
          <br /><br />
          <div>
            <button
              class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
              type="button" @click="onFormSubmit()">
              Submit
            </button>
            <button class="py-1 px-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
              type="reset">
              Reset
            </button>
          </div>
        </table>
      </form>
      <!-- <button class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
        type="submit" @click="getdata">
        Get Data
      </button> -->
      <br />
      <table class="list">
        <thead>
          <tr>
            <th class="px-4 border-black rounded-lg border-2">id</th>
            <th class="px-4 border-black rounded-lg border-2">Book Name</th>
            <th class="px-4 border-black rounded-lg border-2">Book Price</th>
            <th class="px-4 border-black rounded-lg border-2">Book Author</th>
            <th class="px-4 border-black rounded-lg border-2">Book Number</th>
            <th class="px-4 border-black rounded-lg border-2">Book Image</th>
            <th class="px-4 border-black rounded-lg border-2">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) of state.allBooks" :key="item.id">
            <td class="px-4 border-black rounded-lg border-2">{{ item.book_id }}</td>
            <td class="px-4 border-black rounded-lg border-2">{{ item.book_name }}</td>
            <td class="px-4 border-black rounded-lg border-2">{{ item.author }}</td>
            <td class="px-4 border-black rounded-lg border-2">{{ item.price }}</td>
            <td class="px-4 border-black rounded-lg border-2">{{ item.book_number }}</td>
            <td class="px-4 border-black rounded-lg border-2">{{ item.book_image }}</td>
            <td class="px-4 border-black rounded-lg border-2">{{ item.Action }}
              <button class=" mx-3" @click="onDeleteOfBook(item.book_id)">
                Delete
              </button>
              <button class="mx-3" @click="onClickOfEditBook(item.book_id)">
                Edit
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </main>
</template>
<script setup lang="ts">
// let book_name = ref("book_name");
// let book_price = ref("book_price");
// let book_author = ref("book_author")
// const count: any = await $fetch('http://localhost:3001/book');
// async function getdata() {
//   const allData = await $fetch('http://localhost:3001/book');
//   console.log(allData);
// }
// function userDelete(id) {
//   console.log("hiii" + id);
// }
// async function editData(id) {
//   const { data: one } = await useFetch('http://localhost:3001/book/' + id);
//   console.log(one);
// }
let state = reactive({
  allBooks: []
});
getBookAPI();
// Calling Get API
// function getBooks() {
//   getBookAPI().then((data: any) => {
//     state.allBooks = data;
//   });
// }
// GET API
async function getBookAPI() {
  state.allBooks = await $fetch('http://localhost:3001/book');
}
// POST API
async function onFormSubmit() {
  const sampleData = {
    "book_id": state.allBooks.length,
    "book_name": "maratrhi" + state.allBooks.length,
    "author": "ankita" + state.allBooks.length,
    "price": 200 + state.allBooks.length,
    "book_image": "ghjgj" + state.allBooks.length,
    "book_number": "91001" + state.allBooks.length
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
    "book_id": bookId,
    "book_name": "Shaktiman" + bookId,
    "author": "ankita" + state.allBooks.length,
    "price": 200 + state.allBooks.length,
    "book_image": "ghjgj" + state.allBooks.length,
    "book_number": "91001" + state.allBooks.length
  };
  const response = await $fetch('http://localhost:3001/book/' + bookId, {
    method: 'PATCH',
    body: JSON.stringify(sampleData),
  });
  getBookAPI();
}
// Delete API
async function onDeleteOfBook(bookId) {
  await $fetch('http://localhost:3001/book/' + bookId, {
    method: 'DELETE'
  });
  getBookAPI();
}
</script>