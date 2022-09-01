<template>
    <main class="flex justify-center w-full h-screen">
        <div>

            <form class=" bg-gray-100 border-black rounded-lg border-2 px-12" method="post" @submit.prevent="Submit">
                <table>
                    <h2 class="text-teal-900 text-xl font-bold pt-6">Employee Management </h2>
                    <hr />
                    <br />
                    <label class="pt-10 py-10" for="emp-name">Emp_FlirstName:</label><br />
                    <input type="text" id="emp-name" name="emp_name" v-model="data.Emp_FirstName">
                    <span v-for="error in v$.Emp_FirstName.$errors" :key="error.$uid" class="text-red-300"><br />
                        {{ error.$message }}
                    </span>
                    <br />
                    <label for="emp-lname">Emp_LastName:</label><br />
                    <input type="text" id="emp-lname" name="emp-lname" placeholder="Enter last name"
                        v-model="data.Emp_LastName" />
                    <br />
                    <span v-for="error in v$.Emp_LastName.$errors" :key="error.$uid" class="text-red-300">
                        {{ error.$message }}
                    </span>
                    <br />
                    <label for="emp-email">Emp_Email: </label><br />
                    <input type="text" id="emp-email" name="emp-email" placeholder="Enter your email"
                        v-model="data.Emp_Email" />
                    <br />
                    <span v-for="error in v$.Emp_Email.$errors" :key="error.$uid" class="text-red-300">
                        {{ error.$message }}
                    </span><br />
                    <label for="emp-address">Emp_Add: </label><br />
                    <input type="text" id="emp-address" name="emp-address" v-model="data.Emp_Add"
                        placeholder="Enter your Addres" />
                    <br />
                    <span v-for="error in v$.Emp_Add.$errors" :key="error.$uid" class="text-red-300">
                        {{ error.$message }}
                    </span>
                    <br />
                    <select
                        class="dropdown-toggle px-2 py-2 bg-gray-200 text-black font-medium text-xs uppercase rounde"
                        name="gender" v-model="data.Emp_Gender">
                        <option value="Male">Male</option>
                        <option value="Female">Female</option>
                    </select>
                    <span v-for="error in v$.Emp_Gender.$errors" :key="error.$uid" class="text-red-500">{{
                            error.$message
                    }}</span>

                    <br /><br />
                    <label for="">Department </label><br />
                    <select
                        class="dropdown-toggle px-2 py-2 bg-gray-200 text-black font-medium text-xs uppercase rounde"
                        multiple name="department" v-model="data.department">
                        <option value="IT">IT</option>
                        <option value="NETWORK">NETWORK</option>
                    </select>
                    <!-- <span v-for="error in v$.department.$errors" :key="error.$uid" class="text-red-500">{{
                            error.$message
                    }}</span> -->

                    <br /><br />
                    <label for="emp-mobnumber">Emp_MobNumber: </label><br />
                    <input type="text" id="emp-mobnumber" name="emp-mobnumber" placeholder="Enter your number"
                        v-model="data.Emp_MobNumber" />

                    <br /><br />
                    <!-- <label for="employee-image">Emp_profile: </label><br />
                    <input type="file" id="book-image" name="employee-image" /> -->
                    <br /><br />
                    <div>
                        <button
                            class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
                            type="button" @click="Submit">
                            Submit
                            {{ empp.Submit }}
                        </button>


                        <button
                            class="py-1 px-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
                            type="reset">
                            Reset
                        </button>
                    </div>
                </table>
            </form>
            <button
                class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
                type="submit">
                GetData
            </button>

            <br />

            <table class="list">
                <tr>
                    <th class="px-4 border-black rounded-lg border-2">id</th>
                    <th class="px-4 border-black rounded-lg border-2">Emp_FirstName</th>
                    <th class="px-4 border-black rounded-lg border-2">Emp_LastName</th>
                    <th class="px-4 border-black rounded-lg border-2">Emp_Email</th>
                    <th class="px-4 border-black rounded-lg border-2">Emp_Add</th>
                    <th class="px-4 border-black rounded-lg border-2">Emp_Gender</th>
                    <th class="px-4 border-black rounded-lg border-2">Emp_MobNumber</th>

                    <!-- <th class="px-4 border-black rounded-lg border-2">Emp_profile</th> -->
                    <th class="px-4 border-black rounded-lg border-2">Action</th>
                </tr>
                <tr v-for="item of empp.allEmp" :key="item.id">

                    <td class="px-4 border-black rounded-lg border-2">
                        {{ item.id }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ item.Emp_FirstName }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ item.Emp_LastName }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ item.Emp_Email }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ item.Emp_Add }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ item.Emp_Gender }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ item.Emp_MobNumber }}
                    </td>
                    <!-- <td class="px-4 border-black rounded-lg border-2">
                        <img src="" alt="not found" style="width:100px;height:100px">{{ item.Emp_profile }}
                    </td> -->
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ item.Action }}
                        <button class="mx-3" @click="onDelete(item.id)">Delete</button>
                        <button class="mx-3" @click="onEdit(item.id)">Edit</button>
                    </td>
                </tr>
            </table>
        </div>
    </main>
</template>
<script setup lang="ts">
import useVuelidate, {
    required, minLength, email
} from '~/utlis/vuelidate/useVuelidate';
import { computed, reactive } from 'vue'
const { data: count } = await useFetch('http://localhost:3001/Employeee/')
let emp: any = count;
let empp = reactive({
    allEmp: [],
    select: true,
    Submit: '',
    id: ""
});
let data = reactive({
    id: null,
    Emp_FirstName: '',
    Emp_LastName: '',
    Emp_Email: '',
    Emp_Add: '',
    Emp_Gender: '',
    Emp_MobNumber: '',
    department: ''
});
const rules = computed(() => {
    return {
        //  id: null,
        Emp_FirstName: { required, minLength: minLength(4) },
        Emp_LastName: { required },
        Emp_Email: { required, email },
        Emp_Add: { required },
        Emp_Gender: { required },
        Emp_MobNumber: { required },
    }
});
const v$ = useVuelidate(rules, data);
getApi();
async function getApi() {
    empp.allEmp = await $fetch('http://localhost:3001/Employeee');
}
//create new employee
// POST API
async function Submit() {
    //  alert('hrll')
    const result = await v$.value.$validate()
    event.preventDefault();
    if (empp.select === true) {
        const response = await $fetch('http://localhost:3001/Employeee/', {
            method: 'POST',
            body: data
        });
        alert('form subbmitted successfully')
    }
    else {
        putData();
        alert('data updated...yahhhhhhhh')
        empp.Submit = "Submit";
    }
    // await $fetch('http://localhost:3001/Employeee/', {
    //     method: 'POST',
    //     body: data
    // });
    getApi();
}
// PATCH API
async function onEdit(id: number) {
    // const sampleData = {
    //     "id": id,
    //     "Emp_FirstName": "sai" + empp.allEmp.length,
    //     "Emp_LastName": "ankita" + empp.allEmp.length,
    //     "Emp_Email": "sai@gmai.com" + empp.allEmp.length,
    //     "Emp_Add": "ghjgj" + empp.allEmp.length,
    //     "Emp_Gender": "M" + empp.allEmp.length,
    //     "Emp_profile": "" + empp.allEmp.length,
    // };
    empp.Submit = "Update";
    empp.select = false;
    const editEmp: any = await $fetch('http://localhost:3001/Employeee/' + id,);
    data.id = editEmp.id;
    //let empEdit = empp.allEmp.filter((employ) => {
    // if (employ.id == id) {
    data.id = editEmp.id;
    data.Emp_FirstName = editEmp.Emp_FirstName;
    data.Emp_LastName = editEmp.Emp_LastName;
    data.Emp_Email = editEmp.Emp_Email;
    data.Emp_Add = editEmp.Emp_Add;
    data.Emp_Gender = editEmp.Emp_Gender;
    //return employ;
}
// });
// console.log(empEdit);
async function putData() {
    const id = data.id;
    const response = await $fetch('http://localhost:3001/Employeee/' + id,
        {
            method: "PATCH",
            body: data,
        }
    );
    getApi();
}
// Delete API
async function onDelete(id: number) {
    await $fetch('http://localhost:3001/Employeee/' + id, {
        method: 'DELETE'
    })
    getApi();
}
</script>