<template>
  <div class="section-container">
    <div class="cards">
      <template v-for="comment in comments" :key="comment.id">
        <Comment
          :comment="comment"
          :isOwner="comment.user.username === currentUser.username"
          :currentUser="currentUser"
          @update="updateComment"
          @delete="openModal"
          @change-score="changeScore"
          @reply="handleReply"
        />
      </template>
    </div>
    <InputComment
      class="input-comment"
      :currentUser="currentUser"
      :isReply="false"
      @send="handleReply"
    />
  </div>
  <Modal
    class="modal"
    v-if="showDeleteModal"
    :title="'Delete comment'"
    :message="'Are you sure you want to delete this comment? This will remove the comment and can\'t be undone.'"
    :cancelButtonTitle="'No, Cancel'"
    :confirmButtonTitle="'Yes, Delete'"
    @cancel="handleModalCancel"
    @confirm="handleModalConfirm"
  />
</template>

<script>
import Comment from "./Comment.vue";
import Modal from "./Modal.vue";
import InputComment from "./InputComment.vue";

export default {
  name: "Section",
  props: {},
  components: {
    Comment,
    Modal,
    InputComment,
  },
  data() {
    return {
      showDeleteModal: false,
      commentToDelete: {},
      currentUser: {
        image: {
          png: "/image-juliusomo.png",
          webp: "/image-juliusomo.webp",
        },
        username: "juliusomo",
      },
      comments: [
        {
          id: 1,
          content:
            "Impressive! Though it seems the drag feature could be improved. But overall it looks incredible. You've nailed the design and the responsiveness at various breakpoints works really well.",
          createdAt: "2021-12-27T15:54:56Z",
          score: 12,
          user: {
            image: {
              png: "/image-amyrobson.png",
              webp: "/image-amyrobson.webp",
            },
            username: "amyrobson",
          },
          replies: [],
        },
        {
          id: 2,
          content:
            "Woah, your project looks awesome! How long have you been coding for? I'm still new, but think I want to dive into React as well soon. Perhaps you can give me an insight on where I can learn React? Thanks!",
          createdAt: "2022-01-20T15:54:56Z",
          score: 5,
          user: {
            image: {
              png: "/image-maxblagun.png",
              webp: "/image-maxblagun.webp",
            },
            username: "maxblagun",
          },
          replies: [
            {
              id: 3,
              content:
                "If you're still new, I'd recommend focusing on the fundamentals of HTML, CSS, and JS before considering React. It's very tempting to jump ahead but lay a solid foundation first.",
              createdAt: "2022-01-20T15:54:56Z",
              score: 4,
              replyingTo: "maxblagun",
              user: {
                image: {
                  png: "/image-ramsesmiron.png",
                  webp: "/image-ramsesmiron.webp",
                },
                username: "ramsesmiron",
              },
            },
            {
              id: 4,
              content:
                "I couldn't agree more with this. Everything moves so fast and it always seems like everyone knows the newest library/framework. But the fundamentals are what stay constant.",
              createdAt: "2022-01-25T15:54:56Z",
              score: 2,
              replyingTo: "ramsesmiron",
              user: {
                image: {
                  png: "/image-juliusomo.png",
                  webp: "/image-juliusomo.webp",
                },
                username: "juliusomo",
              },
            },
          ],
        },
      ],
    };
  },
  methods: {
    findCommentById(id) {
      const find = (array = [], id) => {
        for (const item of array) {
          const result = item.id === id ? item : find(item.replies, id);
          if (result) return result;
        }
      };

      return find(this.comments, id);
    },

    updateComment(e) {
      const { id, comment } = e;
      const commentToUpdate = this.findCommentById(id);
      commentToUpdate.content = comment;
    },

    openModal(e) {
      const { id } = e;
      this.commentToDelete = this.findCommentById(id);
      this.showDeleteModal = true;
    },

    changeScore(e) {
      const { id, newScore } = e;
      const commentToUpdate = this.findCommentById(id);
      commentToUpdate.score = newScore;
    },

    handleReply(e) {
      const { replyToId, reply } = e;

      const isNewComment = !reply;

      if (isNewComment) {
        this.comments.push({
          id: Date.now(),
          content: e.comment,
          createdAt: new Date(),
          score: 0,
          user: this.currentUser,
        });
      }

      const commentToUpdate = this.findCommentById(replyToId);

      const replies = commentToUpdate.replies || [];
      console.log(replies);

      replies.push(reply);

      commentToUpdate.replies = Object.assign([], replies);
      console.log(commentToUpdate.replies);
    },

    handleModalCancel() {
      this.commentToDelete = {};
      this.showDeleteModal = false;
    },

    handleModalConfirm() {
      this.deleteComment(this.commentToDelete.id);
      this.handleModalCancel();
    },

    deleteComment(id) {
      const deleteItem = (array = [], id) => {
        let index = array.findIndex((item) => item.id === id);
        console.log(id, index);

        if (index >= 0) {
          index = array.splice(index, 1);
          return;
        }

        for (const item of array) {
          deleteItem(item.replies, id);
        }

        return;
      };

      deleteItem(this.comments, id);
    },
  },
};
</script>

<style scoped>
.section-container{
  display: flex;
  flex-direction: column;
  width: var(--desktop-maxWidth);
}

.cards {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
 
}

@media (max-width: 375px) {

  .section-container{
    width: var(--mobile-maxWidth);
    max-width: 375px;
  }
}
</style>
