<template>
    <main class="flex justify-center w-full h-screen">
        <div>
            <form method="post" class="bg-gray-100 border-black rounded-lg border-2 px-12">
                <table>
                    <h2 class="text-teal-900 text-xl font-bold pt-6">Student Management</h2>
                    <hr />
                    <br />
                    <label class="pt-10 py-10" for="FirstName">FirstName</label><br />
                    <input type="text" id="FirstName" name="FirstName" placeholder="Enter your Name" /><br /><br />
                    <label for="LastName">LastName</label><br />
                    <input type="text" id="LastName" name="LastName" placeholder="Enter your Last Name" /><br /><br />
                    <label for="Gender">Gender </label><br />
                    <input type="text" id="Gender" name="Gender" placeholder="Enter your Gender" />
                    <br /><br />
                    <label for="book-number">Student_Email </label><br />
                    <input type="Email" id="Student_Email" name="Student_Email" placeholder="Enter your Email" />
                    <br /><br />
                    <label for="Student_Add">Student_Add</label><br />
                    <input type="Email" id="Student_Add" name="Student_Add" placeholder="Enter your address" />
                    <br /><br />
                    <label for="Studetn_Image">Image: </label><br />
                    <input type="file" id="Student_Image" name="Student_Image" placeholder="please upload your image" />
                    <br /><br />
                    <div>
                        <button
                            class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
                            type="submit" @click="formSubmit">
                            Submit
                        </button>
                        <button
                            class="py-1 px-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
                            type="reset">
                            Reset
                        </button>
                    </div>
                </table>
            </form>
            <br>
            <button
                class="py-1 px-5 mr-5 bg-blue-500 hover:bg-blue-700 text-white font-bold text-center rounded-md mb-3"
                type="submit" @click="getdata()">
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
                    <th class="px-4 border-black rounded-lg border-2">Action</th>
                </tr>
                <tr v-for="(Student, index) in Student " :key="Student.id">
                    <!-- <td class="px-4 border-black rounded-lg border-2">{{item.id=i+1}}</td> -->
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ Student.id }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ Student.FirstName }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ Student.LastName }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ Student.Gender }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ Student.Student_Email }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ Student.Student_Add }}
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ Student.Images}}
                    </td>

                    <td class="px-4 border-black rounded-lg border-2">
                        <img src="" alt="not found" style="width:100px;height:100px">
                    </td>
                    <td class="px-4 border-black rounded-lg border-2">
                        {{ Student.Action }}
                        <button class="mx-3" @click="userDelete(index)">Delete</button>
                        <button class="mx-3" @click="on(index)">Edit</button>
                    </td>
                </tr>
            </table>
        </div>
    </main>
</template>
<script setup lang="ts" >
let Student=[];
async function getdata() {
    console.log('hi');
    await fetch("http://localhost:3001/student-managment")
        .then((data) => {
            return data.json();
        })
        .then((data) => {
            Student = data;
        }).catch((err) => console.log(err));
    console.log(Student);
}
</script>