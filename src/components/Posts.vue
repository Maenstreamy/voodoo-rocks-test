<template>
  <div class="posts">
    <div class="search">
      <button class="btn"><i class="fa fa-search"></i></button>
      <input
        type="search"
        class="input"
        placeholder="Filter by author..."
        v-model="search"
      />
    </div>
    <div class="cards">
      <div class="card" v-for="post of postsByAuthor" :key="post.body">
        <h2 class="card-title">
          {{ post.title }}
        </h2>
        <p class="card-body">
          {{ post.body }}
        </p>
        <div class="card-author">
          {{ post.author.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Posts",
  data() {
    return {
      search: "",
      posts: [],
    };
  },
  async mounted() {
    const postsResponse = await fetch(
      "http://jsonplaceholder.typicode.com/posts"
    );
    const posts = await postsResponse.json();
    const usersResponse = await fetch(
      "http://jsonplaceholder.typicode.com/users"
    );
    const users = await usersResponse.json();
    this.posts = posts;
    this.posts = this.posts.map((post) => {
      post.author = users.find((user) => user.id === post.userId);
      return post;
    });
  },
  computed: {
    postsByAuthor() {
      return this.posts.filter(
        (item) => item.author.name.indexOf(this.search) !== -1
      );
    },
  },
};
</script>

<style lang="scss">
.search {
  display: flex;
  max-width: 300px;
  width: 100%;
  margin: 0 auto 30px;
}

.btn {
  width: 30px;
  height: 30px;
  background: #fff;
  outline: none;
  border: 1px solid #c0c0c0;
  border-radius: 3px 0 0 3px;
}

.input {
  max-width: 270px;
  width: 100%;
  background: #fff;
  outline: none;
  border: 1px solid #c0c0c0;
  border-radius: 0 3px 3px 0;
}
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  grid-gap: 20px;
}
.card {
  position: relative;
  display: flex;
  flex-direction: column;
  padding: 15px 15px 50px 15px;
  background-color: #fff;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
}
.card-title {
  color: rgb(66, 133, 244);
  margin-bottom: 15px;
  &::first-letter {
    text-transform: uppercase;
  }
}
.card-body {
  margin-bottom: 15px;
  &::first-letter {
    text-transform: uppercase;
  }
}
.card-author {
  position: absolute;
  bottom: 15px;
  color: #a9a9a9;
  font-size: 14px;
}
</style>
