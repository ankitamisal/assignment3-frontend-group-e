<template>
  <main class="flex justify-center w-full h-screen ">
    <div>
      <form method="post" class="border-black rounded-lg border-2 px-12">
        <table>
          <h2 class="text-teal-900 text-xl font-bold pt-6">
            Student Management
          </h2>
          <hr />
          <div class="flex flex-wrap -mx-3 mb-6">
            <div class="w-full px-3">
              <label
                class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
                for="fname"
              >
                FirstName
              </label>
              <br />
              <input
                class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-7 mb-3 leading-tight focus:bg-white focus:border-gray-500"
                id="fname"
                v-model="sampleData.FirstName"
                type="text"
                placeholder="First Name"
              />
              <span
                v-for="error in v$.FirstName.$errors"
                :key="error.$uid"
                class="text-red-500"
                >{{ error.$message }}</span
              >
            </div>
          </div>
          <br />
          <div class="">
            <label
              class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
              for="LastName"
            >
              LastName
            </label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-2 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              id="lname"
              v-model="sampleData.LastName"
              type="text"
              placeholder="Last Name"
            />
            <span
              v-for="error in v$.LastName.$errors"
              :key="error.$uid"
              class="text-red-500"
              >{{ error.$message }}</span
            >
          </div>
          <br />
          <div class="flex flex-wrap -mx-3 mb-2">
            <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
              <label
                class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
                for="Stud_gender"
              >
                Gender
              </label>

              <select
                class="dropdown-toggle px-2 py-2 bg-gray-200 text-black font-medium text-xs leading-tight uppercase rounded shadow-md hover:bg-gray-200 hover:shadow-lg focus:bg-gray-200 focus:shadow-lg focus:outline-none focus:ring-0 active:bg-gray-200 active:shadow-lg active:text-black transition duration-150 ease-in-out flex items-center whitespace-nowrap"
                name="department"
                v-model="sampleData.Gender"
              >
                <option value="Male">Male</option>
                <option value="Female">Female</option>
              </select>
              <span
                v-for="error in v$.Gender.$errors"
                :key="error.$uid"
                class="text-red-500"
                >{{ error.$message }}</span
              >
            </div>
          </div>
          <br />
          <div class="flex flex-wrap -mx-3 mb-6">
            <div class="w-full px-3">
              <label
                class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
                for="Stud_email"
              >
                Student_Email
              </label>
              <input
                class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                id="Stud_email"
                v-model="sampleData.Student_Email"
                type="email"
                placeholder="Email"
              />
              <span
                v-for="error in v$.Student_Email.$errors"
                :key="error.$uid"
                class="text-red-500"
                >{{ error.$message }}</span
              >
            </div>
          </div>
          <br />
          <div class="rounded mb-4 shadow appearance-none label-floating">
            <label class="mx-4 text-bold mb-4 font-bold" for="address"
              >Student_Add</label
            >
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              id="address"
              v-model="sampleData.Student_Add"
              type="text"
              placeholder="Address"
            />
            <span
              v-for="error in v$.Student_Add.$errors"
              :key="error.$uid"
              class="text-red-500"
              >{{ error.$message }}</span
            >
          </div>
          <br />

          <!-- <div class="rounded mb-4 shadow appearance-none label-floating">
            <label class="mx-4 text-bold mb-4 font-bold" for="address"
              >Image</label
            >
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              id="address"
              type="file"
              placeholder="Address"/> -->

          <!-- <span
              v-for="error in v$.Image.$errors"
              :key="error.$uid"
              class="text-red-500"
              >{{ error.$message }}</span
            > -->
          <label for="Student_Image">Image: </label
          ><br />
          <input
            type="file"
            id="Student_Image"
            name="Student_Image"
            placeholder="please upload your image"
          />
          <!-- v-model="data.Students.Image" -->
          <br />
          <!-- </div> -->
          <br />
          <div>
            <button
              class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
              type="submit"
              @click="onSubmitForm()"
            >
              {{ State.Submit }}
            </button>
            <button
              class="py-1 px-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
              type="reset"
            >
              Reset
            </button>
          </div>
          <div class="mt-4">
            <!-- <p class="text-red-500">Errors:</p>
            <span v-for="error in v$.$errors" :key="error.$uid">
              {{ error.$property }} - {{ error.$message }} 
              </span>-->
          </div>
        </table>
      </form>
      <hr class="border-4" />
      <div class="flex justify-center">
        <input
          type="text"
          class="rounded-lg flex justify-center m-3 content-center ring-zinc-700 ring-3 px-4"
          name="check"
          id="check"
          v-model="Check1"
          @keyup="getSpecificStudent(Check1)"
          placeholder="find Specific data....."
        />
      </div>
      <br />
      <table class="list">
        <tr>
          <th class="px-4 border-black rounded-lg border-2">id</th>
          <th class="px-4 border-black rounded-lg border-2">FirstName</th>
          <th class="px-4 border-black rounded-lg border-2">LastName</th>
          <th class="px-4 border-black rounded-lg border-2">Gender</th>

          <th class="px-4 border-black rounded-lg border-2">Student_Email</th>

          <th class="px-4 border-black rounded-lg border-2">Student_Add</th>
          <th class="px-4 border-black rounded-lg border-2">Image</th>
          <th class="px-4 border-black rounded-lg border-2">Action</th>
        </tr>
        <tr v-for="item of State.allStud" :key="item.id">
          <td class="px-4 border-black rounded-lg border-2">
            {{ item.id }}
          </td>
          <td class="px-4 border-black rounded-lg border-2">
            {{ item.FirstName }}
          </td>
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
          <td class="px-4 border-black rounded-lg border-2">
            {{ item.Action }}
            <button
              class="mx-3 text-Black font-bold py-2 px-4 rounded-full"
              @click="onDeleteOfStudent(item.id)"
            >
              Delete
            </button>
            <button
              class="mx-3 text-black font-bold py-2 px-4 rounded-full"
              @click="onClickOfEditStudent(item.id)"
            >
              Edit
            </button>
          </td>
        </tr>
      </table>
    </div>
  </main>
</template>
<script lang="ts">
import useVuelidate, {
  required,
  minLength,
  email,
  alpha,
  maxLength,
} from "~/utils/vuelidate/useVuelidate";
</script>
<script setup lang="ts">
// import { required, minLength, between } from 'vuelidate/lib/validators';
import { reactive, computed } from "vue";
let Check1: any;
let State = reactive({
  select: true,
  Submit: "submit",
  allStud: [],
  StudDetails: [],
  id: "",
  //errorBack: {},
});
let sampleData = reactive({
  FirstName: "",
  LastName: "",
  Gender: "",
  Student_Email: "",
  Student_Add: "",
  Image: "",
});

const rules = computed(() => {
  return {
    FirstName: {
      required,
      alpha,
      minLength: minLength(3),
      maxLength: maxLength(35),
    },
    LastName: {
      required,
      alpha,
      minLength: minLength(6),
      maxLength: maxLength(12),
    },
    Gender: { required },
    Student_Email: { required, email },
    Student_Add: { required },
  };
});
const v$ = useVuelidate(rules, sampleData);
getStdAPI();
// GET API
async function getStdAPI() {
  State.allStud = await $fetch("http://localhost:3001/student-managment/");
}

async function clearData() {
  sampleData.FirstName = "";
  sampleData.LastName = "";
  sampleData.Gender = "";
  sampleData.Student_Email = "";
  sampleData.Student_Add = "";
  sampleData.Image = "";
}
// POST API
async function onSubmitForm() {
  const result = await v$.value.$validate();

  event.preventDefault();
  if (State.select === true) {
    const response = await $fetch("http://localhost:3001/student-managment/", {
      method: "POST",
      body: JSON.stringify(sampleData),
    });
    alert("data Added successfully...");
  }
  else {
    putData();
    alert("data updated Successfully...");
    State.Submit = "Submit";
  }
  getStdAPI();
  clearData();
}
// PATCH API
async function onClickOfEditStudent(id) {
  State.Submit = "Update";
  State.select = false;
  const studEdit: any = await $fetch(
    "http://localhost:3001/student-managment/" + id
  );
  State.id = studEdit.id;
  console.log(State.id);
  sampleData.FirstName = studEdit.FirstName;
  sampleData.LastName = studEdit.LastName;
  sampleData.Gender = studEdit.Gender;
  sampleData.Student_Email = studEdit.Student_Email;
  sampleData.Student_Add = studEdit.Student_Add;
  sampleData.Image = studEdit.Image;
}

async function putData() {
  const id = State.id;
  const response = await $fetch(
    "http://localhost:3001/student-managment/" + id,
    {
      method: "PATCH",
      body: sampleData,
    }
  );
  getStdAPI();
  clearData();
}
// Delete API
async function onDeleteOfStudent(id) {
  await $fetch("http://localhost:3001/student-managment/" + id, {
    method: "DELETE",
  });
  getStdAPI();
}
async function getSpecificStudent(check: string) {
  console.log("abc");
  if (check != null) {
    State.StudDetails = State.allStud.filter((stdID) => {
      let id1 = check.toString();
      let id2 = stdID.id.toString();
      let FirstName1 = check.toLocaleLowerCase();
      let FirstName2 = stdID.FirstName.toLocaleLowerCase();
      let LastName1 = check.toLocaleLowerCase();
      let LastName2 = stdID.LastName.toLocaleLowerCase();
      let Gender1 = check.toString();
      let Gender2 = stdID.Gender.toString();
      let Student_Email1 = check.toString();
      let Student_Email2 = stdID.Stud_email.toString();
      let Student_Add1 = check.toString();
      let Student_Add2 = stdID.Stud_address.toString();
      if (
        id2.startsWith(id1) ||
        FirstName2.startsWith(FirstName1) ||
        LastName2.startsWith(LastName1) ||
        Gender2.startsWith(Gender1) ||
        Student_Email2.startsWith(Student_Email1) ||
        Student_Add2.startsWith(Student_Add1)
      ) {
        console.log(stdID);
        return stdID;
      }
    });
  }
  if (check == "") {
    State.StudDetails = State.allStud;
  }
}
// const { error: backError, data: posts } = await useFetch(
//   "http://localhost:3001/student-managment/",
//   {
//     method: "POST",
//     body: JSON.stringify(sampleData),
//   }
// );
// State.errorBack = backError;
// console.log(backError);
// console.log(posts);
</script>
