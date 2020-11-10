<template>
  <v-app>
    <v-main>
      <nav-bar></nav-bar>

      <v-container fluid class="fill-height grey lighten-4">
        <todo-list></todo-list>
      </v-container>

    </v-main>
  </v-app>
</template>

<script>
import NavBar from '@/components/common/NavBar.vue';
import TodoList from '@/components/common/TodoList.vue';

export default {
  components: { NavBar, TodoList },
};
</script>
