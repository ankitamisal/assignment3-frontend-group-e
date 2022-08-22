<template>
<main class="flex justify-center w-full h-screen">
    <div>
        <form @submit="formSubmit" class="bg-gray-100 border-black rounded-lg border-2 px-12">
            <table>
                <h2 class="text-teal-900 text-xl font-bold pt-6">User Management</h2>
                <hr />
                <br />
                <label class="pt-10 py-10 " for="firstname">User ID :</label><br />
                <input type="number" v-model="user.id" id="id" name="id" placeholder="Enter User Id" /><br /><br />
                <label for="lastname">Name :</label><br />
                <input type="text" v-model="user.name" id="name" name="name" placeholder="Enter User name" /><br /><br />
                <label for="address"> State: </label><br />
                <input type="text" v-model="user.State" id="state" name="state" placeholder="Enter your state" />
                <br /><br />
                <label for="image">Image </label><br />
                <input type="text" v-model="user.Image" id="" name="image" placeholder="" />
                <br /><br />
                <div>
                    <button class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3" type="submit" @click="formSubmit"> Submit </button>
                    <button class="py-1 px-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3" type="reset"> Reset </button>
                </div>
            </table>
        </form>
        <table class="list">
            <tr>
                <!-- <th class="px-4 border-black rounded-lg border-2">id</th> -->
                <th class="px-4 border-black rounded-lg border-2">user Id</th>
                <th class="px-4 border-black rounded-lg border-2">Name</th>
                <th class="px-4 border-black rounded-lg border-2">State</th>
                <th class="px-4 border-black rounded-lg border-2">Image No</th>

            </tr>
            <tr v-for="(item,index) in user" :key="user.id">
                <!-- <td class="px-4 border-black rounded-lg border-2">{{item.id=i+1}}</td> -->
                <td class="px-4 border-black rounded-lg border-2">{{item.id}}</td>
                <td class="px-4 border-black rounded-lg border-2">{{item.name}}</td>
                <td class="px-4 border-black rounded-lg border-2">{{item.State}}</td>
                <td class="px-4 border-black rounded-lg border-2">{{item.Image}}</td>
                <td>
                    <button class="mx-3" @click="userDelete(item.index)">
                        Delete
                    </button>
                    <button class="mx-3" @click="on(item.index)">
                        Edit
                    </button>
                </td>
            </tr>
        </table>
    </div>
</main>
</template>

<script setup lang="ts">

       
const{data: count} = await useFetch('http://localhost:8080/user')
let user= count
</script>
