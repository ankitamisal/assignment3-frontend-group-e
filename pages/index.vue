<template>
  <nav class="mb-12 bg-indigo-300 text-black flex justify-end text-sm">
    <!-- <div class="px-72 pt-4"><img src="../hicare.png" alt="Logo" width="100" height="50"> </div> -->
    <p class="m-auto text-xl font-bold">Group E Frontend</p>
  </nav>
  <div
    class="p-10 grid grid-cols-1 sm:grid-cols-1 md:grid-cols-3 lg:grid-cols-3 xl:grid-cols-3 gap-5"
  >
    <!--Card book 1-->
    <div class="rounded overflow-hidden shadow-lg">
      <div class="px-6 py-4">
        <div class="font-bold text-xl mb-2">
          <NuxtLink to="/Book" @click="book" class="hover:text-red-600 mr-2">
            Book Management
          </NuxtLink>
        </div>
        <p class="text-gray-700 text-base">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus
          quia, Nonea! Maiores et perferendis eaque, exercitationem praesentium
          nihil.
        </p>
      </div>
    </div>
    <!-- card 2 -->
    <div class="rounded overflow-hidden shadow-lg">
      <div class="px-6 py-4">
        <div class="font-bold text-xl mb-2">
          <NuxtLink to="/User" class="hover:text-red-600 mr-2">
            User Management
          </NuxtLink>
        </div>
        <p class="text-gray-700 text-base">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus
          quia, Nonea! Maiores et perferendis eaque, exercitationem praesentium
          nihil.
        </p>
      </div>
    </div>

    <!-- card 3-->

    <div class="rounded overflow-hidden shadow-lg">
      <div class="px-6 py-4">
        <div class="font-bold text-xl mb-2">
          <NuxtLink to="/Employee" class="hover:text-red-600 mr-2">
            Employee Management
          </NuxtLink>
        </div>
        <p class="text-gray-700 text-base">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus
          quia, Nonea! Maiores et perferendis eaque, exercitationem praesentium
          nihil.
        </p>
      </div>
    </div>

    <!-- card 4 -->

    <div class="rounded overflow-hidden shadow-lg">
      <div class="px-6 py-4">
        <div class="font-bold text-xl mb-2">
          <NuxtLink to="/Student" class="hover:text-red-600 mr-2">
            Student Management
          </NuxtLink>
        </div>
        <p class="text-gray-700 text-base">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus
          quia, Nonea! Maiores et perferendis eaque, exercitationem praesentium
          nihil.
        </p>
      </div>
    </div>

    <!--Card 5-->
    <div class="rounded overflow-hidden shadow-lg">
      <div class="px-6 py-4">
        <div class="font-bold text-xl mb-2">
          <NuxtLink to="/product" class="hover:text-red-600 mr-2">
            Product Management
          </NuxtLink>
        </div>
        <p class="text-gray-700 text-base">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus
          quia, Nonea! Maiores et perferendis eaque, exercitationem praesentium
          nihil.
        </p>
      </div>
    </div>

    <!-- card 6 -->
    <div class="rounded overflow-hidden shadow-lg">
      <div class="px-6 py-4">
        <div class="font-bold text-xl mb-2">
          <NuxtLink to="/Employee" class="hover:text-red-600 mr-2">
            Flite Management
          </NuxtLink>
        </div>
        <p class="text-gray-700 text-base">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatibus quia,
          Nonea! Maiores et perferendis eaque, exercitationem praesentium nihil.
        </p>
      </div>
    </div>
  </div>
</template>
<script setup>
function book() {
  location.href = "http://localhost:3000/Book";
}
</script>
