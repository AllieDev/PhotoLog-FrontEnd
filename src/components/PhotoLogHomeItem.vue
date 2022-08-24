<template>
  <div class="component">
    <img class="component__image" src="../assets/img/fox.jpg" alt="fox">
    <div class="component__details">
      <div class="component__title">
        <p>Fox</p>
      </div>
      <div class="component__author">
        <p>Author: Ray Hennessy</p>
      </div>
      <div class="component__source">
        <p>Unsplash.com</p>
        <a>https://unsplash.com/photos/xUUZcpQlqpM</a>
      </div>
    </div>
  </div>
  <div class="component">
    <img class="component__image" src="../assets/img/fox.jpg" alt="fox">
    <div class="component__details">
      <div class="component__title">
        <p>Fox</p>
      </div>
      <div class="component__author">
        <p>Author: Ray Hennessy</p>
      </div>
      <div class="component__source">
        <p>Unsplash.com</p>
        <a>https://unsplash.com/photos/xUUZcpQlqpM</a>
      </div>
    </div>
  </div>
  <div class="component">
    <img class="component__image" src="../assets/img/fox.jpg" alt="fox">
    <div class="component__details">
      <div class="component__title">
        <p>Fox</p>
      </div>
      <div class="component__author">
        <p>Author: Ray Hennessy</p>
      </div>
      <div class="component__source">
        <p>Unsplash.com</p>
        <a>https://unsplash.com/photos/xUUZcpQlqpM</a>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {

    }
  },
}
</script>

<style scoped>
.component {
  display: flex;
  font-size: 2rem;
  border: solid 2px #000;
  border-radius: 10px;
  padding: 2rem;
  margin: 5rem auto 0;
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
  margin: auto;
  padding: 2rem;
  height: 40%;
}

.component__title {
  font-size: 5rem;
  margin: auto;
}

.component__source {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}
</style>