<template>
  <div>
    <h1>List of Member</h1>
    <flash-message></flash-message>
    <div v-if="tasks.length > 0">
    <table id="tasks" class="ui celled compact table">
      <thead>
        <tr>
            <th><i class="user icon"></i>Name</th>
            <th><i class="phone icon"></i>Phone Number</th>
            <th><i class="lock open icon"></i></th>
            <th><i class="edit icon"></i></th>
            <th><i class="trash icon"></i></th>
        </tr>
      </thead>
      <tr v-for="(task, i) in tasks" :key="i">
        <td>{{ task.task1 }}</td>
        <td>{{ task.task2 }}</td>
        <td width="75" class="center aligned">
          <router-link :to="{ name: 'show', params: { id: task._id }}">Show</router-link>
        </td>
        <td width="75" class="center aligned">
          <router-link :to="{ name: 'edit', params: { id: task._id }}">Edit</router-link>
        </td>
        <td width="75" class="center aligned" @click.prevent="onDestroy(task._id)">
          <a :href="`/tasks/${task._id}`">Delete</a>
        </td>
      </tr>
    </table>
    </div>
    <div v-else>
        You don't have register yet!.
    </div>
  </div>
</template>
<script>
import { api } from '../helpers/Helpers';
export default {
  name: 'tasks',
  data() {
    return {
      tasks: []
    };
  },
  methods: {
    async onDestroy(id) {
      const sure = window.confirm('Are you sure?');
      if (!sure) return;
      await api.deletetask(id);
      this.flash('deleted sucessfully!', 'success');
      const newtasks = this.tasks.filter(task => task._id !== id);
      this.tasks = newtasks;
    }
  },
  async mounted() {
    this.tasks = await api.gettasks();
  }
};
</script>