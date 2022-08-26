<template>
  <div class="component">
    <img
      class="component__image"
      :src="photoLogData.imageUrl"
      :alt="photoLogData.title"
    />
    <div class="component__details">
      <div class="component__title">
        <p>{{ photoLogData.title }}</p>
      </div>
      <div class="component__author">
        <p>{{ photoLogData.author }}</p>
      </div>
      <div class="component__source">
        <a :href="photoLogData.sourceLink">{{ photoLogData.websiteName }}</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: ["photoLogData"],
};
</script>

<style scoped>
.component {
  display: flex;
  font-size: 2rem;
  border: solid 2px #000;
  border-radius: 10px;
  padding: 2rem;
  margin: 5rem 2.5rem;
  max-width: 1150px;
  transition: 0.5s;
  transform: scale(1);
}

.component:hover {
  transform: scale(1.05);
  opacity: 1;
}

.component__image {
  width: 45%;
  border-radius: 10px;
}

.component__details {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  gap: 7rem;
  padding: 2rem;
  margin: auto;
}

.component__title {
  font-size: 5rem;
  margin: auto;
}

/* Portrait Mobile 0px ~ 403px */
@media only screen and (max-width: 403px) {
  .component {
    max-width: 400px;
    flex-direction: column;
  }

  .component__image {
    width: 100%;
  }

  .component__source {
    flex-wrap: wrap;
  }
}
</style>
