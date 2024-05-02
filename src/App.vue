<template>
  <div id="app" class="app-container">
    <h1 class="app-title">Aplikasi Kegiatan</h1>
    <input type="text" v-model="newActivity" placeholder="Tambahkan kegiatan..." class="app-input" @keyup.enter="addActivity" />
    <button @click="addActivity" class="app-button">Tambah</button>
    <input type="checkbox" v-model="showIncompleteOnly" class="app-checkbox" /> Hanya Tampilkan Belum Selesai
    <activity-list :activities="filteredActivities" :toggleCompletion="toggleCompletion" :cancelActivity="cancelActivity" :deleteActivity="deleteActivity"></activity-list>
  </div>
</template>

<script>
import ActivityList from "./components/ActivityList.vue";

export default {
  components: {
    ActivityList
  },
  data() {
    return {
      newActivity: "",
      showIncompleteOnly: false,
      activities: []
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
    addActivity() {
      if (this.newActivity.trim() !== "") {
        this.activities.push({ name: this.newActivity, completed: false });
        this.newActivity = "";
      }
    },
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

<style>
.app-container {
  font-family: Arial, sans-serif;
  margin-top: 2rem;
  text-align: center;
  background-color: #685f5f;
  color: #fff;
  padding: 20px;
  border-radius: 10px;
}

.app-title {
  margin-bottom: 20px;
}

.app-input {
  padding: 10px;
  margin-bottom: 10px;
  border: none;
  border-radius: 5px;
}

.app-button {
  padding: 10px 20px;
  background-color: #8d959e;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.app-button:hover {
  background-color: #57e15b;
}

.app-checkbox {
  margin-left: 10px;
}
</style>
