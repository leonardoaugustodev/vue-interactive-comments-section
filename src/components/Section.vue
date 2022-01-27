<template>
  <div class="cards">
    <template v-for="comment in comments" :key="comment.id">
      <Comment
        :comment="comment"
        :isOwner="comment.user.username === currentUser.username"
        @update="updateComment"
        @delete="deleteComment"
        @change-score="changeScore"
      />
      <template v-for="reply in comment.replies" :key="reply.id">
        <div class="reply">
          <div class="vertical-line"></div>
          <Comment
            :comment="reply"
            :isOwner="reply.user.username === currentUser.username"
            @update="updateComment"
            @delete="deleteComment"
            @change-score="changeScore"
          />
        </div>
      </template>
    </template>
  </div>
</template>

<script>
import Comment from "./Comment.vue";

export default {
  name: "Section",
  props: {},
  components: {
    Comment,
  },
  data() {
    return {
      currentUser: {
        image: {
          png: "image-juliusomo.png",
          webp: "image-juliusomo.webp",
        },
        username: "juliusomo",
      },
      comments: [
        {
          id: 1,
          content:
            "Impressive! Though it seems the drag feature could be improved. But overall it looks incredible. You've nailed the design and the responsiveness at various breakpoints works really well.",
          createdAt: "1 month ago",
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
          createdAt: "2 weeks ago",
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
              createdAt: "1 week ago",
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
              createdAt: "2 days ago",
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

    deleteComment(e) {
      // const { id } = e;
      // const commentToDelete = this.findCommentById(id);
      console.log("delete", e);
    },

    changeScore(e) {
      const { id, newScore } = e;
      const commentToUpdate = this.findCommentById(id);
      commentToUpdate.score = newScore;
    },
  },
};
</script>

<style scoped>
.cards {
  display: flex;
  flex-direction: column;
  align-items: flex-end;

  width: var(--desktop-maxWidth);
}

.reply {
  display: flex;
  width: calc(100% - 30px);
}

.vertical-line {
  border-left: 4px solid var(--neutral-lightGray);
}

@media (max-width: 375px) {
  .cards {
    width: inherit;
    /* align-items: center; */
  }

  .reply {
    margin-left: 15px;
  }

  .vertical-line {
    border-left: 2px solid var(--neutral-lightGray);
  }
}
</style>
