<template>
  <div class="input-container">
    <img class="avatar" :src="getImage(currentUser.image.png)" />
    <textarea rows="4" v-model="newComment" placeholder="Add a comment..."/>
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
    replyToId: String,
  },
  data() {
    return {
      newComment: null,
    };
  },
  methods: {
    getImage(imgUrl) {
      return require("../assets/avatars" + imgUrl);
    },
    send() {

      if(!this.newComment) return;
      this.$emit("send", {
        replyToId: this.replyToId,
        comment: this.newComment,
      });
    },
  },
};
</script>

<style scoped>
.input-container {

  display: grid;
  grid-gap: var(--desktop-margin);
  grid-template-areas: "avatar textarea button";
  grid-template-columns: min-content 1fr min-content;

  width: 100%;
  background: var(--neutral-white);
  border-radius: var(--desktop-borderRadius);
  padding: var(--desktop-padding);
  margin: calc(0.5 * var(--desktop-margin));
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
  .input-container {
    display: grid;
    grid-gap: var(--mobile-margin);
    
    width: -webkit-fill-available;
    background: var(--neutral-white);
    border-radius: var(--mobile-borderRadius);
    padding: var(--mobile-padding);
    margin: var(--mobile-margin);
  }

  textarea{
    grid-area: 1 / 1 / 2 / 4;
  }

  .avatar {
    grid-area: 2 / 1 / 3 / 3;
  }

  button {
    grid-area: 2 / 3 / 3 / 4;
  }


}
</style>
