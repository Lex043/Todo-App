<template>
  <div class="mt-10">
    <form
      @submit.prevent="addItem"
      class="flex px-[2rem] md:px-[10rem] lg:px-[9rem]"
      action=""
    >
      <input
        v-model.trim="test"
        class="pl-2 grow outline-none border-2 bg-[rgba(0,0,0,.5)] border-[#67656c] text-white rounded-md text-xs py-[0.5rem] lg:text-lg"
        placeholder="Type what you need to do"
        type="text"
      />
      <button
        :disabled="test === ''"
        class="text-white ml-2 bg-[#67656c] py-[0.5rem] px-[1.5rem] rounded-lg"
        type="submit"
      >
        add
      </button>
    </form>

    <p class="text-white mt-10 font-[mali] lg:text-xl">
      You have {{ todos.length }} tasks left
    </p>

    <ul class="mt-10 px-[2.4rem] md:px-[10.4rem] lg:px-[9.4rem]">
      <li
        class="mt-[3rem] font-[mali] flex justify-between bg-[rgba(0,0,0,.2)] px-[0.5rem] py-[0.5rem] rounded-md text-[#929da1] lg:text-lg"
        v-for="{ id, label } in todos"
        :key="id"
      >
        {{ label }}
        <button
          @click="deleteItem(todos.id)"
          class="text-[#929da1] text-xs lg:text-lg bg-black px-2 py-1 rounded-xl"
        >
          delete
        </button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const test = ref("");

const todos = ref([]);

const addItem = () => {
  if (localStorage.getItem("todos")) {
    todos.value = JSON.parse(localStorage.getItem("todos"));
  }
  todos.value.push({ id: todos.value.length + 1, label: test.value });

  localStorage.setItem("tasks", JSON.stringify(todos.value));

  test.value = "";
};

onMounted(() => {
  if (localStorage.getItem("tasks")) {
    todos.value = JSON.parse(localStorage.getItem("tasks"));
  }
});

const deleteItem = (id) => {
  todos.value.splice(id, 1);
  localStorage.setItem("tasks", JSON.stringify(todos.value));
};
</script>
