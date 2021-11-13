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
      <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot">
        <label for="newTwoot"><strong>New Twoot</strong></label>
        <textarea id="newTwoot" rows="4" v-model="newTwootContent"></textarea>
        <div class="user-profile__create-twoot-type">
          <label for="newTwootType"><strong>Type: </strong></label>
          <select id="newTwootType" v-model="selectedTwootType">
            <option
              :value="option.value"
              v-for="(option, index) in twootTypes"
              :key="index"
            >
              {{ option.name }}
            </option>
          </select>
        </div>
        <button>Twoot!</button>
      </form>
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
      newTwootContent: "",
      selectedTwootType: "instant",
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant" },
      ],
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
    createNewTwoot() {
      if (this.newTwootContent && this.selectedTwootType !== "draft") {
        this.user.twoots.unshift({
          id: this.user.twoots.length + 1,
          content: this.newTwootContent,
        });
        this.newTwootContent = "";
      }
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
.user-profile {
  display: flex;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
  margin-top: 20px;
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
  flex-direction: column;
  margin-bottom: 10px;
}

.user-profile__admin-batch {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
  margin-bottom: 10px;
}

.user-profile__follower-count {
  padding-bottom: 10px;
}

.user-profile__create-twoot {
  display: flex;
  flex-direction: column;
  padding-top: 10px;
  border-top: #dfe3e8 1px solid;
  margin-bottom: 10px;
}

.user-profile__create-twoot-type {
  padding-top: 10px;
  padding-bottom: 10px;
}

h2 {
  margin: 0;
}
</style>