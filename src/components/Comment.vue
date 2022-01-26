<template>
  <div>
    <div class="card">
      <div class="counter">
        <button>
          <img src="@/assets/icons/icon-plus.svg" />
        </button>
        <span>{{ comment.score }}</span>
        <button>
          <img src="@/assets/icons/icon-minus.svg" />
        </button>
      </div>
      <div class="title">
        <div class="title-content">
          <img class="avatar" :src="getImage(comment.user.image.png)" />
          <div class="username">{{ comment.user.username }}</div>
          <div class="date">{{ comment.createdAt }}</div>
        </div>
      </div>
      <div class="content">
        {{ comment.content }}
      </div>
      <div class="action">
        <button>
          <img src="@/assets/icons/icon-reply.svg" />
          <span>Reply</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Comment",
  props: {
    comment: Object,
  },
  methods: {
    getImage(imgUrl) {
      return require("../assets/avatars" + imgUrl);
    },
  },
};
</script>

<style scoped>
.card {
  display: grid;
  grid-gap: var(--desktop-margin);
  grid-template-areas:
    "counter title action"
    "counter content content";

  width: inherit;
  background: var(--neutral-white);
  border-radius: var(--desktop-borderRadius);
  padding: var(--desktop-padding);
  margin: calc(0.5 * var(--desktop-margin)) calc(0.5 * var(--desktop-margin));
}

.counter {
  grid-area: "counter";
  grid-row: 1 / 3;
  grid-column: 1;

  background: var(--neutral-veryLightGray);
  border-radius: var(--desktop-borderRadius);
  padding: 10px;
  /* margin: 0 10px 0 0; */

  font-weight: bold;
  font-size: var(--desktop-fontSize);

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
}

.counter span {
  color: var(--primary-blue);
}

.counter button {
  color: var(--neutral-grayBlue);
  height: 20px;
  border: 0px;
  font-size: 24px;
  font-weight: 900;
  background: var(--neutral-veryLightGray);

  display: flex;
  align-items: center;
  justify-content: center;
}

.title {
  grid-area: "title";

  grid-row: 1;
  grid-column: 2;

  display: flex;
  justify-content: space-between;
  align-items: center;
}

.title > div {
  margin: 0 5px;
}

.title-content {
  display: flex;
  align-items: center;
  gap: 15px;
}

.avatar {
  width: 36px;
}

.username {
  font-weight: bold;
}

.date {
  color: var(--neutral-grayBlue);
  font-weight: 500;
}

.action {
  grid-area: action;

  grid-row: 1;
  grid-column: 3 / 4;

  justify-self: end;
  align-self: center;
}

.action button {
  border: 0;
  font-size: 18px;
  color: var(--primary-blue);
  background: var(--neutral-white);
  font-weight: 600;

  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 5px;
}

.content {
  grid-area: "content";
  grid-row: 2 / 3;
  grid-column: 2 / 4;

  text-align: start;
  line-height: 1.5;

  color: var(--neutral-grayBlue);
  font-size: 16px;
}

@media (max-width: 375px) {
  .card {
    grid-template-areas:
      "title title"
      "content content"
      "counter action";

    flex-direction: column-reverse;

    padding: var(--mobile-padding);
  }

 .title {
    grid-area: 1 / 1 / 1 / 3;
  }

  .content {
    grid-area: 2 / 1 / 3 / 3;
  }

  .counter {
    grid-area: 3 / 1 / 3 / 2;

    flex-direction: row;
    width: 100px;
  }

  .action {
    grid-area: 3 / 2 / 4 / 3;
  }
}
</style>
