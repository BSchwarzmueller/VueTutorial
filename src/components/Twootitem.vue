<template>
  <div class="twoot-item" @click="favouriteTwoot(twoot.id)">
    <div clas="twoot-item__user">@{{ username }}</div>
    <div class="twoot-item__content">
      {{ twoot.content }}
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
    favouriteTwoot(id) {
      this.$emit("favourite", id);
    },
  },
};
</script>

<style>
.twoot-item {
  padding: 20px;
  margin: 5px;
  background: white;
  border-radius: 5px;
}
.twoot-item:hover {
  transform: scale(1.1);
}
.twoot-item__user {
  margin-bottom: 5px;
}
.twoot-item__content {
  font-style: italic;
}
</style>