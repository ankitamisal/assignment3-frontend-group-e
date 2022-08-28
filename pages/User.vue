<template>
  <main class="flex justify-center w-full h-screen">
    <div>
      <form class="bg-gray-100 border-black rounded-lg border-2 px-12">
        <table>
          <h2 class="text-teal-900 text-xl font-bold pt-6">User Management</h2>
          <hr />
          <br />
          <label>Name :</label
          ><br />
          <input
            type="text"
            v-model="state.user.name"
            id="name"
            name="name"
            placeholder="Enter User name"
            :v="v$.name"
          />
          <span class=" text-red-900" v-for="error in v$.name.$errors" :key="error.$uid"> {{ error.$message }}</span>
          <br /><br />

          <label>Email :</label
          ><br />
          <input
            type="text"
            v-model="state.user.Email"
            id="email"
            name="email"
            placeholder="Enter User Email"
            :v="v$.Email"
          />
          <span v-if="v$.Email.$error"> {{ v$.Email.$error[0].$message }}</span>
          <br /><br />
          <label> State:</label
          ><br />
          <input
            type="text"
            v-model="state.user.State"
            id="state"
            name="state"
            placeholder="Enter your state"
          />
          <span v-if="v$.State.$error"> {{ v$.State.$error[0].$message }}</span>
          <br /><br />

          <label>image </label
          ><br />
          <input
            type="text"
            v-model="state.user.Image"
            id=""
            name="image"
            placeholder="Image"
          />
          <span v-if="v$.Image.$error"> {{ v$.Image.$error[0].$message }}</span>
          <br /><br />
          <!-- <label for="Image">createdAt </label
          ><br />
          <input
            type="text"

            id=""
            name="image"
            placeholder=""
          /> -->
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
      <table class="list">
        <tr>
          <!-- <th class="px-4 border-black rounded-lg border-2">id</th> -->
          <th class="px-4 border-black rounded-lg border-2">id</th>
          <th class="px-4 border-black rounded-lg border-2">name</th>
          <th class="px-4 border-black rounded-lg border-2">Email</th>
          <th class="px-4 border-black rounded-lg border-2">State</th>
          <th class="px-4 border-black rounded-lg border-2">Image</th>
          <th class="px-4 border-black rounded-lg border-2">Action</th>
          <!-- <td class="px-4 border-black rounded-lg border-2">createdAt</td> -->
        </tr>
        <tr v-for="(item, index) in state.allusers" :key="item">
          <!-- <td class="px-4 border-black rounded-lg border-2">{{item.id=i+1}}</td> -->
          <td class="px-4 border-black rounded-lg border-2">
          {{ item.id }}</td>
          <td class="px-4 border-black rounded-lg border-2">
          {{ item.name }}</td>
          <td class="px-4 border-black rounded-lg border-2">
          {{ item.Email }}</td>
          <td class="px-4 border-black rounded-lg border-2">
          {{ item.State }}
          </td>
          <td class="px-4 border-black rounded-lg border-2">
          {{ item.Image }}
          </td>
          <!--  <td class="px-4 border-black rounded-lg border-2">
            {{ item.createdAt }}
          </td> -->
          <td>
            <button
              class="mx-3 bg- rounded bg-blue-500 hover:bg-blue-700"
              @click="onDeleteOfuser(item.id)"
            >
              Delete
            </button>
            <button
              class="mx-3 rounded bg-blue-500 hover:bg-blue-700"
              @click="onClickOfEdituser(item.id)"
            >
              Edit
            </button>
          </td>
        </tr>
      </table>
    </div>
  </main>
</template>

<script setup lang="ts">
import useVuelidate,{
    required,
    email,
    minLength,

} from "~/utils/vuelidate/useVuelidate";
import Vuelidate from 'vuelidate'
import {computed,reactive} from 'vue';

   // name: "User",
// const{data: count} = await useFetch('http://localhost:8080/user')
// let user= count


let state = reactive({
    allusers: [],
    edit : true,
    submit:'',
   id: '',
    user: {

        name: "",
        Email: "",
        State: "",
        Image: ""
    },
});

let sampleData=reactive({
        name: "",
        Email: "",
        State: "",
        Image: ""
});

const rules= computed(()=>{
    return{
    name: {
        required,
        minLength:minLength(3)
    },
    Email: {
        required,
        email
    },
    State: {
        required,
    },
    Image: {
        required
    }
    }
});

const v$ = useVuelidate(rules, state.user);

// let info = {

//     name: "",
//     Email: "",
//     State: "",
//     Image: ""
// };

// const rules = computed(() => {
//         return {

//             name: {
//                 required
//             },
//             Email: {
//                 required,
//                 email
//             },
//             State: {
//                 required
//             },
//             Image: {
//                 required
//             }

//         }
//     }),

// async function login(): Promise < void > {
//         const isUSerCorrect = await v$.value.$validate();
//         if (!isUserCorrect) {

//             return {
//                 state,
//                 v$
//             }
//         }
//         const payload = {
//             ...state.form
//         };

getuserAPI();
// Calling Get API
function getuser() {
    getuserAPI().then((sampleData: any) => {
        state.allusers = sampleData;
    });
}
// GET API
async function getuserAPI() {
    state.allusers = await $fetch("http://localhost:3001/user/");
}
// POST API
async function onFormSubmit() {
      const result=await v$.value.$validate();
      // event.preventDefault()
      if(result==true){
            alert('Allrigt..! We got your details.')
        } else {
            alert('Somthing went wrong, please check your form details.')
        }
    
    //const user = state.user;
    if(state.edit===true)
    {
    const response = await $fetch("http://localhost:3001/user/", {
        method: "POST",
         body: JSON.stringify(state.user),

    });
    getuserAPI();
    
    }else{
        putData();
    }

}

// get by ID
async function onClickOfEdituser(id) {

    const edit = await $fetch("http://localhost:3001/user/" + id);

    state.id = edit.id;
    state.user.name = edit.name;
    state.user.Email = edit.Email;
    state.user.State = edit.State;
    state.user.Image = edit.Image;
    getuserAPI();
    state.edit=false;
}

// PATCH API
async function putData() {
    const response = await $fetch("http://localhost:3001/user/" + state.id, {
        method: "PATCH",
        body: JSON.stringify(state.user),


    });

    state.user.edit=true;

}
//Delete API
async function onDeleteOfuser(id) {
    await $fetch("http://localhost:3001/user/" + id, {
        method: "DELETE",
    });
    getuserAPI();

}
</script>
