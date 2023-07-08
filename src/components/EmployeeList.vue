<template>
  <main>
    <div class="flex justify-center items-center gap-3 flex-wrap my-10">
      <div
        v-for="employee in employees"
        :key="employee.id"
        class="border-gray-600 border-2 text-center px-8 py-6 bg-teal-400"
      >
        <div>
          <img
            :src="employee.avatar"
            :alt="employee.first_name"
            class="rounded-full"
          />
        </div>
        <div>
          <p class="text-slate-800">
            {{ employee.first_name }} {{ employee.last_name }}
          </p>
          <a
            :href="'mailto:' + employee.email"
            class="text-blue-500 hover:underline hover:text-blue-700"
          >
            Kontakt
          </a>
        </div>
      </div>
    </div>
    <div v-if="pageCount > 1" class="pagination">
      <button @click="loadPage(page - 1)" :disabled="page === 1">
        Föregående
      </button>
      <button @click="loadPage(page + 1)" :disabled="page === pageCount">
        Nästa
      </button>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      employees: [],
      page: 1,
      perPage: 6,
      pageCount: 0,
    };
  },
  methods: {
    async loadPage(page) {
      try {
        const response = await fetch(
          `https://reqres.in/api/users?page=${page}`
        );
        const data = await response.json();
        this.employees = data.data;
        this.page = page;
        this.pageCount = data.total_pages;
      } catch (error) {
        console.error(error);
      }
    },
  },
  mounted() {
    this.loadPage(1);
  },
};
</script>

<style scoped>
.pagination button {
  margin-right: 10px;
  cursor: pointer;
  padding: 5px 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: rgb(45, 175, 236);
}

.pagination button:disabled {
  cursor: not-allowed;
  opacity: 0.6;
}
main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
}

.pagination {
  position: sticky;
  bottom: -2px;
  display: flex;
  justify-content: center;
  align-items: center;

  padding: 10px;
  z-index: 1;
}
</style>
