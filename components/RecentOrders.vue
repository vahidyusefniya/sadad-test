<template>
  <div class="mt-5">
    <p class="font-bold">Recent orders ({{ total }})</p>
    <div>
      <v-infinite-scroll :items="users" @load="load" height="500">
        <v-data-table :items="users" :items-length="total" hide-default-footer :headers="headers" :items-per-page="1000" v-model:sort-by="sortBy" />
      </v-infinite-scroll>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'
const itemsPerPage = ref(10)
const page = ref(-1)
const sortBy = ref([{ key: 'id', order: 'asc' }])
const total = ref(0)
const users = ref([])
const headers = ref([
  {
    align: 'start',
    key: 'id',
    title: 'ID'
  },
  {
    align: 'start',
    key: 'firstName',
    title: 'First name'
  },
  { title: 'Last name', key: 'lastName' },
])


const pageCount = computed(() => {
  return Math.ceil(total / itemsPerPage.value)
})

const getUsers = async () => {
  return $fetch(`https://dummyjson.com/users?limit=10&skip=${page.value * 10}`)
}

const load = async ({ done }) => {
  page.value = page.value + 1

  console.log(page.value)
  setTimeout(async () => {
    const res = await getUsers()
    users.value.push(...res.users)
    done('ok')
  }, 1000)
}

</script>
