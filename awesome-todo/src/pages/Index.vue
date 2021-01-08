<template>
  <q-page padding>
    <ul>
      <li v-for="task in tasks" v-bind:key="task">{{task}}</li>
    </ul>
    <hr>
    <ul>
      <li v-for="(bt, index) in betterTasks" v-bind:key="bt.index"> 
        <div>#{{index}} - {{bt.name}} </div>
        <small>{{bt.dueDate}} - {{bt.dueTime}}</small>
        <button @click="deleteBetterTask(index)">X</button>
      </li>
    </ul>
  </q-page>
</template>

<script>
export default {
  data(){
    return {
      tasks: ['get bananas', 'eat bananas', 'smash bananas'],
      betterTasks:[
        {
          name: 'Go to shop',
          dueDate: '07/01/2020',
          dueTime: '14:00'
        },
        {
          name: 'Get bananas',
          dueDate: '08/01/2020',
          dueTime: '14:00'
        },
        {
          name: 'Go to shot',
          dueDate: '07/01/2020',
          dueTime: '14:00'
        }
      ]
    }
  },
  methods:{
    deleteBetterTask(index){
      this.betterTasks.splice(index, 1)
    }
  }
}
</script>

<style>

</style>
