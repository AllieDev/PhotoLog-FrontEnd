<template>
  <div>
    <form class="form">
      <input
        maxlength="30"
        v-model="title"
        placeholder="Title*"
        :class="['form__title-input', 'input', titleInputErrorClass]"
        type="text"
      />

      <input
        maxlength="20"
        v-model="author"
        placeholder="Author*"
        :class="['form__author-name-input', 'input', authorInputErrorClass]"
        type="text"
      />
      <input
        v-model="imageUrl"
        placeholder="Image URL*"
        :class="['form__image-url-input', 'input', imageUrlInputErrorClass]"
        type="text"
      />

      <input
        maxlength="20"
        v-model="websiteName"
        placeholder="Name of the website*"
        :class="['form__site-name-input', 'input', websiteNameInputErrorClass]"
        type="text"
      />
      <input
        v-model="sourceLink"
        placeholder="Source link*"
        :class="['form__site-link-input', 'input', sourceLinkInputErrorClass]"
        type="text"
      />

      <div class="form__btn-container">
        <button @click="validateFrom()" class="form__button" type="button">
          Add
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import anime from "animejs";
export default {
  data() {
    return {
      title: "",
      author: "",
      imageUrl: "",
      websiteName: "",
      sourceLink: "",
      formValid: false,
    };
  },
  methods: {
    validateFrom() {
      if (
        !this.title ||
        !this.author ||
        !this.imageUrl ||
        !this.websiteName ||
        !this.sourceLink
      ) {
        this.formValid = true;
        anime({
          targets: ".form",
          translateX: [0, -15, 15, 0],
          duration: 200,
          easing: "easeInOutSine",
        });
      } else {
        this.$emit("submitInput", {
          title: this.title,
          author: this.author,
          imageUrl: this.imageUrl,
          websiteName: this.websiteName,
          sourceLink: this.sourceLink,
        });

        this.title = "";
        this.author = "";
        this.imageUrl = "";
        this.websiteName = "";
        this.sourceLink = "";
      }
    },
  },
  computed: {
    titleInputErrorClass() {
      if (this.formValid) {
        return { "form__input-error": !this.title };
      }
    },
    authorInputErrorClass() {
      if (this.formValid) {
        return { "form__input-error": !this.author };
      }
    },
    imageUrlInputErrorClass() {
      if (this.formValid) {
        return { "form__input-error": !this.imageUrl };
      }
    },
    websiteNameInputErrorClass() {
      if (this.formValid) {
        return { "form__input-error": !this.websiteName };
      }
    },
    sourceLinkInputErrorClass() {
      if (this.formValid) {
        return { "form__input-error": !this.sourceLink };
      }
    },
  },
};
</script>

<style scoped>
.form {
  padding: 10px;
  /* margin-top: 20px; */
  margin: 20px 10px 0 10px;
  height: 120px;

  display: grid;
  grid-template-columns: 1fr 1fr 0.5fr;
  grid-template-rows: 1fr 1fr 1fr;

  grid-template-areas:
    "title title btn-container"
    "author image-url btn-container"
    "website-name source-link btn-container";

  gap: 7px;

  background-color: rgb(228, 228, 228);
  border: 1px solid rgb(209, 209, 209);
  border-radius: 5px;
}
.input {
  box-sizing: border-box;

  padding-left: 10px;

  width: 100%;
  height: 100%;

  border: none;
  border-radius: 5px;
}
.form__title-input {
  grid-area: title;
}
.form__author-name-input {
  grid-area: author;
}
.form__image-url-input {
  grid-area: image-url;
}
.form__site-name-input {
  grid-area: website-name;
}
.form__site-link-input {
  grid-area: source-link;
}
.form__btn-container {
  grid-area: btn-container;

  display: flex;
  justify-content: center;
  align-items: center;
}
.form__input-error {
  background-color: rgb(255, 248, 248);
  border: 1px solid red;
}
.form__button {
  font-size: small;

  width: 70%;
  height: 40px;

  color: white;
  background-color: rgb(14, 94, 255);

  border: none;
  border-radius: 5px;
}
@media screen and (max-width: 600px) {
  .form {
    height: 150px;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr 1fr;

    grid-template-areas:
      "title title"
      "author image-url"
      "website-name source-link"
      "btn-container btn-container";
  }
  .form__button {
    width: 100%;
    height: 30px;
  }
}
</style>
