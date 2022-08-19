<template>
  <main class="flex justify-center w-full h-screen">
    <p>{{ swapnil }}</p>
    <div>
      <form method="post" class="bg-gray-100 border-black rounded-lg border-2 px-12">
        <table>
          <h2 class="text-teal-900 text-xl font-bold pt-6">Book Management</h2>
          <hr />
          <br />
          <label class="pt-10 py-10" for="book-name">Book name:</label><br />
          <input type="text" id="book-name" name="book-name" placeholder="Enter your Book name" /><br /><br />
          <label for="book-price">Book price:</label><br />
          <input type="text" id="book-price" name="book-price" placeholder="Enter Book price" /><br /><br />
          <label for="book-author">Book Author: </label><br />
          <input type="text" id="book-author" name="address" placeholder="Enter your Aouther" />
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
              type="submit" @click="formSubmit">
              Submit
            </button>

            <button class="py-1 px-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
              type="reset">
              Reset
            </button>
          </div>
        </table>
      </form>
      <button class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
        type="submit" @click="getdata">
        Get Data
      </button>
      <br />
      <table class="list">
        <tr>
          <th class="px-4 border-black rounded-lg border-2">id</th>
          <th class="px-4 border-black rounded-lg border-2">Book Name</th>
          <th class="px-4 border-black rounded-lg border-2">Book Price</th>
          <th class="px-4 border-black rounded-lg border-2">Book Author</th>
          <th class="px-4 border-black rounded-lg border-2">Book Number</th>
          <th class="px-4 border-black rounded-lg border-2">Book Image</th>
          <th class="px-4 border-black rounded-lg border-2">Action</th>
        </tr>
      </table>
    </div>
  </main>
</template>
<script setup >
let swapnil = [];
async function getdata() {
  await fetch("http://localhost:3001/book")
    .then((data) => {
      return data.json();
    })
    .then((data) => {
      swapnil = data;
      console.log(swapnil);
    }).catch((err) => console.log(err));

}
</script>
