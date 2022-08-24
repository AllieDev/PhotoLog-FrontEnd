<template>
  <div class="home-component">
    <photo-log-home-item v-for="photoLogsData in arrayOfPhotoLogs" :key="photoLogsData.title" :photoLogData="photoLogsData"/>
  </div>
</template>

<script>
import PhotoLogHomeItem from "../components/PhotoLogHomeItem.vue";

export default {
  data() {
    return {
      arrayOfPhotoLogs: [],
    }
  },
  components: {
    PhotoLogHomeItem,
  },
  methods: {
    async getPhotoLogs() {
      const response = await fetch("http://www.localhost:3000/photo-logs/");
      const data = await response.json();
      this.arrayOfPhotoLogs = data.photoLogsData;
    }
  },
  mounted() {
    this.getPhotoLogs();
  },
}
</script>

<style scoped>
</style>




