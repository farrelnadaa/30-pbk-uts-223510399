<template>
  <div>
    <activity-item
      v-for="(activity, index) in filteredActivities"
      :key="index"
      :activity="activity"
      :toggleCompletion="toggleCompletion"
      :cancelActivity="cancelActivity"
      :deleteActivity="deleteActivity"
    ></activity-item>
  </div>
</template>

<script>
import ActivityItem from "./ActivityItem.vue";

export default {
  components: {
    ActivityItem
  },
  props: {
    activities: Array
  },
  data() {
    return {
      showIncompleteOnly: false
    };
  },
  computed: {
    filteredActivities() {
      if (this.showIncompleteOnly) {
        return this.activities.filter(activity => !activity.completed);
      } else {
        return this.activities;
      }
    }
  },
  methods: {
    toggleCompletion(activity) {
      activity.completed = !activity.completed;
    },
    cancelActivity(activity) {
      const index = this.activities.indexOf(activity);
      if (index !== -1) {
        this.activities.splice(index, 1);
      }
    },
    deleteActivity(activity) {
      const index = this.activities.indexOf(activity);
      if (index !== -1) {
        this.activities.splice(index, 1);
      }
    }
  }
};
</script>
