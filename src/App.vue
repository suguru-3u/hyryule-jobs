<template>
  <div class="app">
    <header>
      <div>
        <h1>Hyryule Jobs</h1>
      </div>
      <div>
        <form @submit.prevent>
          Title : <input type="text" v-model="inputTitle"><br>
          location : <input type="text" v-model="inputLocation"><br>
          salary : <input type="text" v-model="inputSalary"><br>
          <button @click="onSubmit()">Registory</button>
        </form>
      </div>
      <div class="order">
        <button @click="handleClick('title')">Order by title</button>
        <button @click="handleClick('salary')">Order by salary</button>
        <button @click="handleClick('location')">Order by location</button>
      </div>
    </header>
    <Joblist :jobs="jobs" :order="order"/>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import Job from './type/job'
import OrderTerm from './type/OrderTerm'
import Joblist from './components/Joblist.vue'

export default defineComponent({
  name: 'App',
  components: {
    Joblist
  },
  setup() {
    // const state = reactive({
    //   name : 'Link',
    //   age : 25 as number | string
    // })

    // retrun {...toRefs(state)}

    // const name = ref('Link')
    // const age = ref< number | string>(25)

    // return { name, age }

    const inputTitle = ref<string>('')
    const inputLocation = ref<string>('')
    const inputSalary = ref<number>(0)

    const jobs = ref<Job[]>([
      { title: 'farm worker', location: 'lon lon ranch', salary: 30000, id: '1'},
      { title: 'quarryman', location: 'death mountain', salary: 40000, id: '2'},
      { title: 'flute player', location: 'the lost woods', salary: 35000, id: '3'},
      { title: 'fisherman', location: 'lake hylia', salary: 21000, id: '4'},
      { title: 'prison guard', location: 'gerudo valley', salary: 32000, id: '5'}
    ])

    const order = ref<OrderTerm>('title')

    const jobCount = ref<string>(String((jobs.value.length + 1 )))

    const onSubmit = (): void  => {
      jobs.value.push(
        { title: inputTitle.value , location: inputLocation.value , salary : inputSalary.value , id : jobCount.value }
      )
    }

    const handleClick = (term: OrderTerm) => {
      order.value = term
    }

    return {jobs, handleClick , order, inputTitle, inputLocation, inputSalary, jobCount, onSubmit}

  },
});
</script>

<style>
  header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
  }
  button {
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  } 
</style>
