<template>
  <div>
    <article class="pa3 pa5-ns">
      <h1 class="f4 bold center mw6">Completed Todos</h1>
      <ul class="list pl0 ml0 center mw6 ba b--light-silver br2">
        <li v-for="todo of todos" class="flex items-center ph3 pv3 bb b--light-silver">
          <span class="flex-auto">{{todo.id}}. {{todo.task}}</span>
        </li>
      </ul>
    </article>
  </div>
</template>

<script>
import {mapState} from 'vuex'
import axios from 'axios'

export default {
  async fetch ({store, redirect, error}) {
    try {
      const res = await axios.get('https://todos-cuvsmolowg.now.sh/todos')
      store.commit('init', res.data)
    } catch (err) {
      error({statusCode: 500, message: 'Oops, try again'})
    }
  },
  computed: {
    ...mapState({
      todos: state => state.todos.filter(todo => todo.complete)
    })
  }
}
</script>
