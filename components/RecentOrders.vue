<template>
  <div class="mt-5">
    <p class="font-bold">Recent orders ({{ total }})</p>
    <div>
      <v-infinite-scroll :items="users" @load="load" height="500">
        <v-data-table :items="users" :items-length="total" hide-default-footer :headers="headers" :items-per-page="1000" v-model:sort-by="sortBy" />
        <template v-slot:empty>
          <v-alert type="info">No more items!</v-alert>
        </template>
      </v-infinite-scroll>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
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
const getUsers = async () => {
  return $fetch(`https://dummyjson.com/users?limit=10&skip=${page.value * 10}`)
}

const load = async ({ done }) => {
  if(page.value * 10 < total.value){
    page.value = page.value + 1
  
    setTimeout(async () => {
      const res = await getUsers()
      users.value.push(...res.users)
      total.value = res.total
      done('ok')
    }, 1000)
  }else{
    done('empty')
  }
}

</script>
