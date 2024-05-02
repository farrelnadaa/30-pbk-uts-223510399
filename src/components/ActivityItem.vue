<template>
  <div class="activity-item">
    <input type="checkbox" v-model="activity.completed" @change="toggleCompletion" />
    <span :class="{ 'completed': activity.completed }">{{ activity.name }}</span>
    <button @click="cancelActivity">Batal</button>
  </div>
</template>

<script>
export default {
  props: {
    activity: Object,
    cancelActivity: Function,
    toggleCompletion: Function
  }
};
</script>

<style scoped>
.activity-item {
  background-color: #333;
  color: #fff;
  padding: 10px;
  margin: 5px 0;
  border-radius: 5px;
}

.completed {
  text-decoration: line-through;
}
</style>
