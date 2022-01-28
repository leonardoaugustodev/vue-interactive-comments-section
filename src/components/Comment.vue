<template>
  <div class="container">
    <div class="card">
      <div class="counter">
        <button @click="changeScore(1)">
          <img src="@/assets/icons/icon-plus.svg" />
        </button>
        <span>{{ comment.score }}</span>
        <button @click="changeScore(-1)">
          <img src="@/assets/icons/icon-minus.svg" />
        </button>
      </div>
      <div class="title">
        <div class="title-content">
          <img class="avatar" :src="getImage(comment.user.image.png)" />
          <div class="username">{{ comment.user.username }}</div>
          <div v-if="isOwner" class="tag">you</div>
          <div class="date">{{ getDate(comment.createdAt) }}</div>
        </div>
      </div>
      <div class="content">
        <div v-if="isEdit" class="content-edit">
          <textarea rows="4" v-model="newComment" />
          <button name="update" @click="handleUpdate">Update</button>
        </div>
        <div v-else>
          <span class="mention">{{
            comment.replyingTo ? `@${comment.replyingTo}` : ""
          }}</span>
          {{ comment.content }}
        </div>
      </div>
      <div class="action">
        <div v-if="isOwner" class="action-buttons">
          <button name="delete" @click="handleDelete" :disabled="isEdit">
            <img src="@/assets/icons/icon-delete.svg" />
            <span>Delete</span>
          </button>
          <button name="edit" @click="edit" :disabled="isEdit">
            <img src="@/assets/icons/icon-edit.svg" />
            <span>Edit</span>
          </button>
        </div>
        <button v-else @click="handleReply">
          <img src="@/assets/icons/icon-reply.svg" />
          <span>Reply</span>
        </button>
      </div>
    </div>
    <template v-for="reply in comment.replies" :key="reply.id">
      <div class="reply">
        <div class="vertical-line"></div>
        <Comment
          :comment="reply"
          :isOwner="reply.user.username === currentUser.username"
          :currentUser="currentUser"
          @update="handleUpdate"
          @delete="handleDelete"
          @change-score="changeScore"
          @reply="handleNewComment"
        />
      </div>
    </template>
    <InputComment
      v-if="showInput"
      :currentUser="currentUser"
      :isReply="true"
      :replyToId="comment.id"
      @send="handleNewComment"
    />
  </div>
</template>

<script>
import InputComment from "./InputComment.vue";
import moment from "moment";

export default {
  name: "Comment",
  props: {
    comment: Object,
    isOwner: Boolean,
    currentUser: Object,
  },
  setup() {
    // const updateComment = function(){};
    // return {updateComment}
  },
  components: {
    InputComment,
  },
  data() {
    return {
      isEdit: false,
      newComment: undefined,
      showInput: false,
    };
  },
  methods: {
    getImage(imgUrl) {
      return require("../assets/avatars" + imgUrl);
    },
    getDate(date) {
      const pastDate = moment(date);
      const duration = moment.duration(pastDate.diff(moment()));
      return duration.humanize(true);
    },
    edit() {
      this.isEdit = true;
      this.newComment = this.comment.content;
    },

    handleUpdate(e) {
      this.$emit("update", {
        id: e.id || this.comment.id,
        comment: e.comment || this.newComment,
      });

      this.isEdit = false;
    },
    handleDelete(e) {
      this.$emit("delete", {
        id: e.id || this.comment.id,
      });
    },
    changeScore(e) {
      this.$emit("change-score", {
        id: e.id ? e.id : this.comment.id,
        newScore: e.id ? e.newScore : this.comment.score + e,
      });
    },
    handleReply() {
      this.showInput = true;
    },
    handleNewComment(e) {
      this.$emit("reply", {
        replyToId: e.comment ? e.replyToId : e.replyToId,
        reply: {
          id: Date.now(),
          content: e.comment ? e.comment : e.reply.content,
          createdAt: new Date(),
          score: 0,
          replyingTo: this.comment.user.username,
          user: this.currentUser,
        },
      });

      this.showInput = false;
    },
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.card {
  display: grid;
  grid-gap: var(--desktop-margin);
  grid-template-areas:
    "counter title action"
    "counter content content";
  grid-template-columns: min-content 1fr 1fr;

  width: 100%;
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

  font-weight: bold;
  font-size: var(--desktop-fontSize);

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;

  height: 100px;
  width: 40px;
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
  width: max-content;
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
  font-size: 0.8em;
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

.content-edit {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: flex-end;
  gap: calc(0.6 * var(--desktop-margin));
}

.mention {
  color: var(--primary-blue);
  font-weight: bold;
}

.action-buttons {
  display: flex;
  gap: var(--desktop-margin);
}

button[name="delete"] {
  color: var(--primary-red);
}

button[name="update"] {
  background: var(--primary-blue);
  color: var(--neutral-white);

  border: 0px;
  border-radius: var(--desktop-borderRadius);
  padding: calc(0.6 * var(--desktop-padding));

  text-transform: uppercase;
  font-weight: bold;
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

.tag {
  background: var(--primary-blue);
  color: var(--neutral-white);

  padding: 2px 4px;
  font-size: 0.8em;
  font-weight: bold;
  border-radius: 2px;
}

.reply {
  display: flex;
  justify-content: space-between;
}

.vertical-line {
  border-left: 4px solid var(--neutral-lightGray);
  margin: 0 25px;
}

@media (max-width: 375px) {
  .card {
    grid-template-areas:
      "title title"
      "content content"
      "counter action";

    grid-template-columns: min-content 1fr;

    flex-direction: column-reverse;

    padding: var(--mobile-padding);
    margin: var(--mobile-margin);
    width: auto;
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

    height: 40px;
    width: 100px;
  }

  .action {
    grid-area: 3 / 2 / 4 / 3;
  }


  .vertical-line {
    border-left: 2px solid var(--neutral-lightGray);
    margin: 0 var(--mobile-margin);
  }
}
</style>
