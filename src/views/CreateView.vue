<template>
  <div class="create__view-container">
    <create-input-component-vue @submitInput="submitForm($event)" />
    <search-input-component-vue
      @triggerFilter="filterVideoCards($event)"
      @triggerFetch="getPhotoLogsData"
    />
    <!-- ---------------------------------------------------------------- -->
    <div class="table-list">
      <div class="table-list-category">
        <div class="category-table"><p class="image">Image</p></div>
        <div class="category-table"><p class="detail">Details</p></div>
        <div class="category-table"><p class="action">Action</p></div>
      </div>
      <div class="table-list-container">
        <photo-log-create-component-vue
          v-for="photoLogData in arrayOfMatches"
          :photoLogsData="photoLogData"
          @update-photo-log="updatePhotoLogsData($event)"
          @delete-photo-log="deletePhotoLogsData($event)"
          @toggle-modal="getPhotoLogsDataWithId($event)"
        />
      </div>
    </div>
    <!-- ---------------------------------------------------------------- -->
    <div @click="toggleModal()" v-if="modal" class="modal">
      <div class="madal-child-container">
        <photo-log-home-item-vue :photoLogData="photoLogData" />
      </div>
    </div>
  </div>
</template>

<script>
import PhotoLogHomeItemVue from "../components/PhotoLogHomeItem.vue";
import PhotoLogCreateComponentVue from "../components/PhotoLogCreateComponent.vue";
import CreateInputComponentVue from "../components/CreateInputComponent.vue";
import SearchInputComponentVue from "../components/SearchInputComponent.vue";
export default {
  data() {
    return {
      modal: false,
      photoLogData: {
        title: "title update",
        author: "by Ali Asghar",
        sourceLink: "https://images.unsplash.com/",
        websiteName: "unsplash.com",
        imageUrl:
          "https://images.unsplash.com/photo-1474511320723-9a56873867b5?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2072&q=80",
        id: "5eac6d3d-e4db-49e2-b9cf-536bb8522dcf",
      },
      arrayOfPhotoLogs: [],
      arrayOfMatches: [],
    };
  },
  methods: {
    toggleModal() {
      this.modal = !this.modal;
    },
    filterVideoCards(searchString) {
      let matches = [];
      for (let photoLog of this.arrayOfPhotoLogs) {
        if (photoLog.title.toLowerCase().includes(searchString.toLowerCase())) {
          matches.push(photoLog);
        }
      }
      this.arrayOfMatches = matches;
      console.log("running filter");
    },
    async submitForm(event) {
      const response = await fetch("http://localhost:3000/photo-logs", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(event),
      });

      this.getPhotoLogsData();
    },
    async updatePhotoLogsData(event) {
      const response = await fetch(
        `http://localhost:3000/photo-logs/${event.id}`,
        {
          method: "PUT",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(event),
        }
      );

      this.getPhotoLogsData();
    },
    async deletePhotoLogsData(id) {
      const response = await fetch(`http://localhost:3000/photo-logs/${id}`, {
        method: "DELETE",
      });
      this.getPhotoLogsData();
    },
    async getPhotoLogsData() {
      const response = await fetch("http://localhost:3000/photo-logs/");
      const data = await response.json();
      this.arrayOfPhotoLogs = data.photoLogsData;
      this.arrayOfMatches = data.photoLogsData;
    },
    async getPhotoLogsDataWithId(event) {
      const response = await fetch(
        `http://localhost:3000/photo-logs/${event.id}`
      );
      const data = await response.json();
      this.photoLogData = data;
      this.toggleModal();
    },
  },
  computed: {
    chooseArray() {
      if (this.arrayOfMatches === []) {
        return this.arrayOfPhotoLogs;
      } else {
        return this.arrayOfMatches;
      }
    },
  },
  components: {
    CreateInputComponentVue,
    SearchInputComponentVue,
    PhotoLogCreateComponentVue,
    PhotoLogHomeItemVue,
  },
  mounted() {
    this.getPhotoLogsData();
  },
};
</script>

<style scoped>
.modal {
  z-index: 1;
  position: fixed;
  top: 0;
  right: 0;

  width: 100vw;
  height: 100vh;

  background-color: rgba(0, 0, 0, 0.575);

  display: flex;
  justify-content: center;
  align-items: center;
}
.madal-child-container {
  background-color: white;
}
.create__view-container {
  max-width: 1200px;
  margin: 0 auto;
}
.table-list {
  margin: 20px 10px 0 10px;
  height: 100%;

  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 40px 1fr;
}
.table-list-category {
  display: grid;
  grid-template-columns: 0.5fr 1.3fr 0.5fr;
  grid-template-rows: 1fr;

  background-color: rgb(228, 228, 228);
  border: 1px solid rgb(209, 209, 209);
  border-radius: 5px 5px 0 0;
}
.category-table {
  padding: 0 20px;

  display: flex;
  justify-content: center;
  align-items: center;
}
.category-table p {
  color: rgb(84, 84, 84);
  margin: 0;
  font-size: medium;
}

.table-list-container {
  max-height: 100%;
}
@media screen and (max-width: 600px) {
  .category-table p {
    display: none;
  }
}
</style>
