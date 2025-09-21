<template>
  <div v-if="error">
    <p class="text-4xl">error : {{ error.message }}</p>
  </div>
  <div v-else>
    <FilterUsers v-model="filterInput" />
    <h1 class="text-4xl mb-5">Users:</h1>

    <div
      class="mx-auto grid lg:grid-cols-4 md:grid-cols-3 sm:grid-cols-2 gap-5"
    >
      <div
        v-for="user in filteredSearch"
        :key="user.id"
        class="p-6 bg-primary border-gray-200 text-white rounded-lg shadow-lg shadow-gray-400 hover:bg-hover transition ease-in-out hover:inset-shadow-xl delay-75"
      >
        <h5 class="mb-2 text-xl font-bold tracking-tight">{{ user.name }}</h5>
        <p class="font-normal text-gray-100">phone: {{ user.phone }}</p>
        <p class="font-normal">email: {{ user.email }}</p>
      </div>
    </div>
  </div>
</template>
<script setup>
import { onMounted, ref } from "vue";

import { getUsers } from "@/services/UserService";

const users = ref([]);
const error = ref();
import FilterUsers from "@/components/FilterUsers.vue";

import { useFilterSearch } from "@/composables/useFiltersearch";
const { filteredSearch, filterInput } = useFilterSearch(users);

onMounted(async () => {
  const result = await getUsers();
  users.value = result.data;
  error.value = result.error;
  console.log(Object.keys(result.data).length);
});
</script>
