<template>
  <div class="container">
    <!-- start of component -->
    <div v-if="!edit" class="component">
      <img class="component__image" :src="photoLogsData.imageUrl" alt="" />
      <div class="component__details-container">
        <p class="component__details">Title: {{ photoLogsData.title }}</p>
        <p class="component__details">Author: {{ photoLogsData.author }}</p>
        <p class="component__details">From: {{ photoLogsData.websiteName }}</p>
      </div>
      <div class="component__actions">
        <i
          @click="deletePhotoLog(photoLogsData.id)"
          class="fas fa-trash component__delete-btn"
        ></i>

        <i @click="editPhotoLog(photoLogsData)" class="fas fa-pen"></i>
        <i
          @click="showPhotoLog(photoLogsData)"
          class="component__show-btn fas fa-eye"
        ></i>
      </div>
    </div>
    <!-- end of component -->
    <!-- start of edit component-->
    <div v-if="edit" class="edit-component">
      <div class="edit-component__details-container">
        <input
          class="edit-component__edit-input"
          v-model="editData.imageUrl"
          type="text"
        />
        <input
          class="edit-component__edit-input"
          v-model="editData.title"
          type="text"
        />
        <input
          class="edit-component__edit-input"
          v-model="editData.author"
          type="text"
        />
        <input
          class="edit-component__edit-input"
          v-model="editData.websiteName"
          type="text"
        />
        <input
          class="edit-component__edit-input"
          v-model="editData.sourceLink"
          type="text"
        />
      </div>
      <div class="edit-component__actions">
        <i @click="cancel()" class="fas fa-ban edit-component__cancel-btn"></i>
        <i
          @click="emitPhotoLogData(editData)"
          class="fas fa-check edit-component__update-bt"
        ></i>
      </div>
    </div>
    <!-- end of edit component-->
  </div>
</template>

<script>
export default {
  data() {
    return {
      edit: false,
      editData: {},
    };
  },
  methods: {
    editPhotoLog(data) {
      this.editData = {
        title: data.title,
        author: data.author,
        sourceLink: data.sourceLink,
        websiteName: data.websiteName,
        imageUrl: data.imageUrl,
        id: data.id,
      };
      this.edit = true;
      //   this.editData.push(PhotoLogDetails);
      //   console.log(PhotoLogDetails);
    },
    emitPhotoLogData(editData) {
      this.$emit("update-photo-log", editData);
      this.edit = false;
    },
    deletePhotoLog(data) {
      this.$emit("delete-photo-log", data);
    },
    showPhotoLog(data) {
      this.$emit("toggle-modal", data);
    },
    cancel() {
      this.edit = false;
    },
  },
  props: ["photoLogsData"],
};
</script>

<style scoped>
.container {
  width: 100%;
}
.component {
  margin-top: 20px;
  padding: 10px;
  height: 150px;

  display: flex;

  border: 1px solid black;
  border-radius: 5px;
}
.component__image {
  width: 20%;
  height: 100%;

  object-fit: cover;
  border-radius: 5px;
}
.component__details-container {
  box-sizing: border-box;
  padding: 0 20px;
  margin: 0;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  gap: 20px;
  width: 60%;
  height: 100%;
}
.component__edit-input {
  width: 100%;
}
.component__details {
  all: unset;
  margin: 0;
  font-size: small;
}
.component__actions {
  width: 20%;

  display: flex;
  justify-content: center;
  align-items: center;

  gap: 20px;
}
.component__actions i {
  font-size: large;
  color: rgb(6, 64, 255);
}
/* ---------------------------------------------------------------- */
.edit-component {
  margin-top: 20px;
  padding: 10px;
  height: 150px;

  display: flex;
  justify-content: space-between;
  align-items: center;

  border: 1px solid rgb(203, 203, 203);
  border-radius: 5px;
}
.edit-component__details-container {
  box-sizing: border-box;

  margin: 0;
  height: 100%;
  width: 80%;

  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 5px;
}
.edit-component__edit-input {
  padding-left: 10px;
  border: 1px solid rgb(203, 203, 203);
  height: 20%;
  width: 100%;
}
.edit-component__actions {
  height: 100%;
  width: 20%;

  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
}
.edit-component__actions i {
  font-size: large;
  color: rgb(6, 64, 255);
}

@media screen and (max-width: 600px) {
  .component {
    margin-top: 20px;
    padding: 10px;
    height: 400px;

    flex-direction: column;
  }
  .component__image {
    width: 100%;
    height: 40%;
  }
  .component__details-container {
    width: 100%;
    height: 50%;
  }
  .component__actions {
    height: 10%;
    width: 100%;

    gap: 20px;
  }

  /* ---------------------------------------------------------------- */
  .edit-component {
    height: 400px;

    flex-direction: column;
    justify-content: space-between;
    gap: 5px;
  }
  .edit-component__details-container {
    height: 40%;
    width: 100%;
  }
  .edit-component__actions {
    gap: 20px;

    height: 10%;
    width: 100%;
  }
  .edit-component__actions i {
    height: 100%;
  }
}
</style>
