<template>
  <div class="twoot-item" @click="favTwoot(twoot.id)">
    <div class="user-profile__twoot">
      <div class="twoot-item__user">@{{ username }}</div>
      <div class="twoot-item__content">
        {{ twoot.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TwootItem",
  props: {
    username: {
      type: String,
      required: true,
    },
    twoot: {
      type: Object,
      required: true,
    },
  },
  methods: {
    favTwoot(id){
      this.$emit('favourite', id)
    }
  }
};
</script>

<style>
.twoot-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
  margin-left: 50px;
  margin-right: 50px;
  margin-bottom: 10px;
}

.twoot-item:hover {
  transform: scale(1.1, 1.1);
}

.twoot-item__user {
  font-weight: bold;
}
</style>