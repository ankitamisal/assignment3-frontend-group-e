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
            v-model="state.Students.FirstName"
          /><br /><br />
          <label for="LastName">LastName</label
          ><br />
          <input
            type="text"
            id="LastName"
            name="LastName"
            placeholder="Enter your Last Name"
            v-model="state.Students.LastName"
          /><br /><br />
          <label for="Gender">Gender </label
          ><br />
          <input
            type="text"
            id="Gender"
            name="Gender"
            placeholder="Enter your Gender"
            v-model="state.Students.Gender"
          />
          <br /><br />
          <label for="book-number">Student_Email </label
          ><br />
          <input
            type="Email"
            id="Student_Email"
            name="Student_Email"
            placeholder="Enter your Email"
            v-model="state.Students.Student_Email"
          />
          <br /><br />
          <label for="Student_Add">Student_Add</label
          ><br />
          <input
            type="Email"
            id="Student_Add"
            name="Student_Add"
            placeholder="Enter your address"
            v-model="state.Students.Student_Add"
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
              @click="onFormSubmit"
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
        <tr v-for="(item, index) of state.allStudent" :key="item.id">
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
            <button class="mx-3" @click="onDeleteStudent(item.id)">
              Delete
            </button>
            <button class="mx-3" @click="onClickOfEditBook(item.id)">
              Edit
            </button>
          </td>
        </tr>
      </table>
    </div>
  </main>
</template>
<script setup lang="ts">
// let Student=[];
// async function getdata() {
//     console.log('hi');
//     await fetch("http://localhost:3001/student-managment")
//         .then((data) => {
//             return data.json();
//         })
//         .then((data) => {
//             Student = data;
//         }).catch((err) => console.log(err));
//     console.log(Student);
//}
// const { data: count } = await $fetch('http://localhost:3001/student-managment')
// let student = count
let state = reactive({
  allStudent: [],
  Students: {
    FirstName: "",
    LastName: "",
    Gender: "",
    Student_Email: "",
    Student_Add: " ",
    Image: "",
  },
});
getStudentAPI();
// Calling Get API
// function getBooks() {
//   getBookAPI().then((data: any) => {
//     state.allBooks = data;
//   });
// }
// GET API
async function getStudentAPI() {
  state.allStudent = await $fetch("http://localhost:3001/student-managment/");
}
// POST API
async function onFormSubmit() {
  // const studentData = {
  //     "id" :  state.allStudent.length,
  //     "FirstName": "Vishal" + state.allStudent.length,
  //     "LastName": "shinde" + state.allStudent.length,
  //     "Gender": "m" + state.allStudent.length,
  //     "Student_Email": "shindev05@gmail.com" + state.allStudent.length,
  //     "Student_Add": "pune" + state.allStudent.length,
  //     "Image": "" + state.allStudent.length
  // };
  const response = await $fetch("http://localhost:3001/student-managment", {
    method: "POST",
    body: JSON.stringify(state.Students),
  });
  getStudentAPI();
}
// PATCH API
async function onClickOfEditBook(id) {
  // const studentData = {
  //     "id": id , //+ state.allStudent.length,
  //     "FirstName": "Vishal" +state.allStudent.length,
  //     "LastName": "shinde" + state.allStudent.length,
  //     "Gender": "m" + state.allStudent.length,
  //     "Student_Email": "shindev05@gmail.com" + state.allStudent.length,
  //     "Student_Add": "pune" + state.allStudent.length
  // };
  const response = await $fetch(
    "http://localhost:3001/student-managment/" + id,
    {
      method: "PATCH",
      body: JSON.stringify(state.Students),
    }
  );
  getStudentAPI();
}
// Delete API
async function onDeleteStudent(id) {
  await $fetch("http://localhost:3001/student-managment/" + id, {
    method: "DELETE",
  });
  getStudentAPI();
}
</script>
