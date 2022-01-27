<template>
  <div class="card">
    <img class="avatar" :src="getImage(currentUser.image.png)" />
    <textarea rows="4" v-model="newComment" />
    <button name="send" @click="send">
      {{ isReply ? "Reply" : "Send" }}
    </button>
  </div>
</template>

<script>
export default {
  name: "InputComment",
  props: {
    currentUser: Object,
    isReply: Boolean,
    replyToId: String
  },
  data() {
    return {
      newComment: undefined,
    };
  },
  methods: {
    getImage(imgUrl) {
      return require("../assets/avatars" + imgUrl);
    },
    send() {
      this.$emit("send", {
        replyToId: this.replyToId,
        comment: this.newComment,
      });
    },
  },
};
</script>

<style scoped>
div.card {
  display: grid;
  grid-gap: var(--desktop-margin);
  grid-template-areas: "avatar textarea button";
  grid-template-columns: min-content 1fr min-content;

  width: 100%;
  background: var(--neutral-white);
  border-radius: var(--desktop-borderRadius);
  padding: var(--desktop-padding);
  margin: calc(0.5 * var(--desktop-margin)) calc(0.5 * var(--desktop-margin));
}

.avatar {
  width: 36px;
}

button {
  background: var(--primary-blue);
  color: var(--neutral-white);

  border: 0px;
  border-radius: var(--desktop-borderRadius);
  padding: calc(0.6 * var(--desktop-padding));

  text-transform: uppercase;
  font-weight: bold;

  height: min-content;
}

button:disabled {
  opacity: 0.5;
  cursor: default;
}

button:disabled:hover {
  filter: none;
}

textarea {
  width: 100%;
  border-radius: var(--desktop-borderRadius);
  padding: 10px;
  resize: none;

  outline: none;
  border: 1px solid rgba(var(--rgb-blue), 0.5);
}

textarea:focus {
  outline: none;
  border: 1px solid var(--primary-blue);
}

@media (max-width: 375px) {
  /* .card {
    grid-template-areas:
      "title title"
      "content content"
      "counter action";

    flex-direction: column-reverse;

    padding: var(--mobile-padding);
  } */
}
</style>
