<template>
  <main class="flex justify-center w-full h-screen">
    <div>
      <form
        method="post"
        class="bg-gray-100 border-black rounded-lg border-2 px-12"
      >
        <table>
          <h2 class="text-teal-900 text-xl font-bold pt-6">
            Student Management
          </h2>
          <hr />
          <br />
          <label class="pt-10 py-10" for="FirstName">FirstName</label
          ><br />
          <input
            type="text"
            id="FirstName"
            name="FirstName"
            placeholder="Enter your Name"
            v-model="sampleData.FirstName"
          /><br /><br />
          <label for="LastName">LastName</label
          ><br />
          <input
            type="text"
            id="LastName"
            name="LastName"
            placeholder="Enter your Last Name"
            v-model="sampleData.LastName"
          /><br /><br />
          <label for="Gender">Gender </label
          ><br />
          <input
            type="text"
            id="Gender"
            name="Gender"
            placeholder="Enter your Gender"
            v-model="sampleData.Gender"
          />
          <br /><br />
          <label for="book-number">Student_Email </label
          ><br />
          <input
            type="Email"
            id="Student_Email"
            name="Student_Email"
            placeholder="Enter your Email"
            v-model="sampleData.Student_Email"
          />
          <br /><br />
          <label for="Student_Add">Student_Add</label
          ><br />
          <input
            type="Email"
            id="Student_Add"
            name="Student_Add"
            placeholder="Enter your address"
            v-model="sampleData.Student_Add"
          />
          <br /><br />
          <label for="Student_Image">Image: </label
          ><br />
          <input
            type="file"
            id="Student_Image"
            name="Student_Image"
            placeholder="please upload your image"
          />
          <!-- v-model="state.Students.Image" -->
          <br /><br />
          <div>
            <button
              class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
              type="submit"
              @click="onFormSubmit()"
            >
              Submit
            </button>
            <button
              class="py-1 px-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
              type="reset"
            >
              Reset
            </button>
          </div>
        </table>
      </form>
      <br />
      <button
        class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
        type="submit"
        @click="getStudentAPI()"
      >
        Get Data
      </button>
      <br />
      <table class="list">
        <tr>
          <th class="px-4 border-black rounded-lg border-2">id</th>
          <th class="px-4 border-black rounded-lg border-2">FirstName</th>
          <th class="px-4 border-black rounded-lg border-2">LastName</th>
          <th class="px-4 border-black rounded-lg border-2">Gender</th>
          <th class="px-4 border-black rounded-lg border-2">Address_Email</th>
          <th class="px-4 border-black rounded-lg border-2">Address_Add</th>
          <th class="px-4 border-black rounded-lg border-2">Image</th>
          <th class="px-4 border-black rounded- lg border-2">Action</th>
        </tr>
        <tr v-for="item of state.allStud" :key="item.id">
          <!-- <td class="px-4 border-black rounded-lg border-2">{{item.id=i+1}}</td> -->
          <td class="px-4 border-black rounded-lg border-2">
            {{ item.id }}
          </td>
          <td class="px-4 border-black rounded-lg border-2">
            {{ item.FirstName }}
          </td>
          <!-- <td class="px-4 border-black rounded-lg border-2">
                        {{ }}
                    </td> -->
          <td class="px-4 border-black rounded-lg border-2">
            {{ item.LastName }}
          </td>
          <td class="px-4 border-black rounded-lg border-2">
            {{ item.Gender }}
          </td>
          <td class="px-4 border-black rounded-lg border-2">
            {{ item.Student_Email }}
          </td>
          <td class="px-4 border-black rounded-lg border-2">
            {{ item.Student_Add }}
          </td>
          <td class="px-4 border-black rounded-lg border-2">
            {{ item.Image }}
          </td>
          <!-- <td class="px-4 border-black rounded-lg border-2">
                        <img src="" alt="not found" style="width:100px;height:100px">
                    </td> -->
          <td class="px-4 border-black rounded-lg border-2">
            {{ item.Action }}
            <button class="mx-3" @click="onDeleteOfStudent(item.id)">
              Delete
            </button>
            <button class="mx-3" @click="onClickOfEditStud(item.id)">
              Edit
            </button>
          </td>
        </tr>
      </table>
    </div>
  </main>
</template>
<script setup lang="ts">
let state = reactive({
  allStud: [],
});
let sampleData = {
  id: null,
  FirstName: "",
  LastName: "",
  Gender: "",
  Student_Email: "",
  Student_Add: "",
  Image: "",
};
getStudentAPI();
// GET API
async function getStudentAPI() {
  state.allStud = await $fetch("http://localhost:3001/student-managment/");
}
// POST API
async function onFormSubmit() {
  //alert("Hello submit function call,,,");
  // stdid: state.allStud.length, 
  // fname: 'vaibhav' + state.allStud.length,
  // lname: 'rahinj' + state.allStud.length,
  // Stud_email: 'v@gmail.com' + state.allStud.length,
  // Stud_gender: 'male' + state.allStud.length,
  // Stud_address: 'ghjgj' + state.allStud.length,
  // await $fetch("http://localhost:8080/product", {
  //   method: "POST",
  //   body: JSON.stringify(mydata.product),
  // };
  await $fetch("http://localhost:3001/student-managment/", {
    method: "POST",
    body: sampleData,
  });
  getStudentAPI();
}
// PATCH API
async function onClickOfEditStud(id) {
  let studEdit = state.allStud.filter((std) => {
    if (std.id == id) {
      sampleData.id = std.id;
      sampleData.FirstName = std.FirstName;
      sampleData.LastName = std.LastName;
      sampleData.Gender = std.Gender;
      sampleData.Student_Email = std.Student_Email;
      sampleData.Student_Add = std.Student_Add;
      return std;
    }
  });
  console.log(studEdit);
  //   sampleBookData.book_id = bookEdit.book_id;
  const response = await $fetch(
    "http://localhost:3001/student-managment/" + id,
    {
      method: "PATCH",
      body: sampleData,
    }
  );
  getStudentAPI();
}
// Delete API
async function onDeleteOfStudent(id) {
  await $fetch("http://localhost:3001/student-managment/" + id, {
    method: "DELETE",
  });
  getStudentAPI();
}
</script>
