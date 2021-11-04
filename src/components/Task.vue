<template>
  <div
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task.text }}
      <i @click="$emit('delete-task', task.id)" class="close">x</i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>
<script>
export default {
  name: "Task",
  props: {
    task: Object,
  }
};
</script>

<style scoped>
.task {
  background: lightgray;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.close {
  color: red;
}
</style>
