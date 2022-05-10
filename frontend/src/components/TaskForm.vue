<template>
 <form action="#" @submit.prevent="onSubmit">
    <p v-if="errorsPresent" class="error">Please fill out both fields!</p>
    <div class="ui labeled input fluid">
      <div class="ui label">
        <i class="user icon"></i>Name
      </div>
      <input type="text" placeholder="Enter your name ..." v-model="task.task1" />
    </div>
    <div class="ui labeled input fluid">
      <div class="ui label">
   <i class="phone icon"></i> Call
      </div>
      <input type="text" placeholder="Enter Phone number ..." v-model="task.task2" />
    </div>
    <button class="positive ui button">Submit</button>
  </form>
</template>
<script>
export default {
  name: 'task-form',
  props: {
    task: {
      type: Object,
      required: false,
      default: () => {
        return {
          task1: '',
          task2: ''
        };
      }
    }
  },
  data() {
    return {
      errorsPresent: false
    };
  },
  methods: {
    onSubmit: function() {
      if (this.task.task1 === '' || this.task.task2 === '') {
        this.errorsPresent = true;
      } else {
        //  $emit() function that allows you to pass custom events up the component tree.
        this.$emit('createOrUpdate', this.task);
      }
    }
  }
};
</script>
<style scoped>
.error {
  color: red;
}
</style>