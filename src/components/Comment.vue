<template>
  <div>
    <div class="card">
      <div class="counter">
        <button>
          <img src="@/assets/icons/icon-plus.svg" />
        </button>
        <span>{{comment.score}}</span>
        <button>
          <img src="@/assets/icons/icon-minus.svg" />
        </button>
      </div>
      <div class="card-content">
        <div class="title">
          <div class="title-content">
            <img class="avatar" :src="getImage(comment.user.image.png)" />
            <div class="username">{{comment.user.username}}</div>
            <div class="date">{{comment.createdAt}}</div>
          </div>

          <div class="action">
            <button>
              <img src="@/assets/icons/icon-reply.svg" />
              <span>Reply</span>
              </button>
          </div>
        </div>
        <div class="content">
          {{comment.content}}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Comment",
  props: {
    comment: Object
  },
  methods:{
    getImage(imgUrl){
      return require('../assets/avatars' + imgUrl);
    }
  }
};
</script>

<style scoped>
.card {
  background: var(--neutral__white);
  max-width: 800px;
  border-radius: 8px;
  display: flex;
  padding: 20px;
  margin: 20px;
}

.counter {
  font-size: 18px;
  font-weight: bold;

  background: var(--neutral__very-light-gray);

  border-radius: 10px;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;

  height: 100px;
  width: 80px;
}

.counter span {
  color: var(--primary__blue);
}

.counter button {
  color: var(--neutral__gray-blue);
  height: 30px;
  border: 0px;
  font-size: 24px;
  font-weight: 900;
  background: var(--neutral__very-light-gray);

  display: flex;
  align-items: center;
  justify-content: center;
}

.card-content {
  margin-left: 20px;
}

.title {
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
  color: var(--neutral__gray-blue);
  font-weight: 500;
}

.action button {
  border: 0;
  font-size: 18px;
  color: var(--primary__blue);
  background: var(--neutral__white);
  font-weight: 600;

  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 5px;
}

.content {
  margin-top: 20px;
  text-align: start;

  color: var(--neutral__gray-blue);
  font-size: 18px;
}


</style>
