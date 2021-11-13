<template>
  <div id="user-profile">
    <br />
    <div class="user-profile__user-panel">
      <h2 class="user-profile__username">@{{ user.username }}</h2>
      <div class="user-profile__admin-batch" v-if="user.isAdmin">Admin</div>
      <div class="user-profile__admin-batch" v-else>User</div>
      <div class="user-profile__follower-count">
        <strong>Followers: </strong>{{ followers }}
        <button @click="followUser">Follow</button>
      </div>
    </div>
    <div class="user-profile__twoots-wrapper">
      <twoot-item
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
        @favourite="toggleFav"
      />
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem.vue";
export default {
  name: "UserProfile",
  components: {
    TwootItem,
  },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "ZevenDutch",
        fname: "Zeven",
        lname: "Dutch",
        email: "zevendutch@gmail.com",
        isAdmin: false,
        twoots: [
          { id: 1, content: "Twotter is amazing" },
          { id: 2, content: "Zeven is rising" },
          { id: 3, content: "Dutch is the new German" },
        ],
      },
    };
  },
  watch: {
    followers(newCount, oldCount) {
      if (oldCount < newCount) {
        console.log(`${this.user.username} has gained a follower`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.fname} ${this.user.lname}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFav(id) {
      console.log(`Favourite Twoot #${id}`);
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-left: 50px;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  width: 200px;
  margin-bottom: 10px;
}

.user-profile__admin-batch {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}

h2 {
  margin: 0;
}
</style>