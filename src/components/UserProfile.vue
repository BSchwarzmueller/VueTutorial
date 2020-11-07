<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
      <!-- v-else -->
      <div class="user-profile__follower-count">
        <strong>Followers:</strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile_twoots-wrapper">
      <TwootItem
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
        @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script>
import TwootItem from "./Twootitem";
export default {
  name: "UserProfile",

  components: { TwootItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "_NopeMitchell",
        firstName: "Hans-Peter",
        lastName: "Meier",
        email: "deinemudder@gmx.de",
        isAdmin: true,
        twoots: [
          { id: 1, content: "Hello! My Name is Basti" },
          { id: 2, content: "Hey! Nice tits!" },
          { id: 3, content: "I like cake!" },
          { id: 4, content: "Your mom is fat!" },
        ],
      },
    };
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id) {
      console.log(`Favourite Tweet #${id}`);
    },
  },
  mounted() {
    this.followUser();
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has a new Follower!`);
      }
    },
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
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}
h1 {
  margin: 0;
}
.user-profile__admin-badge {
  background: black;
  border-radius: 5px;
  margin-right: auto;
  padding: 4px;
  color: rgb(123, 212, 50);
  font-weight: bold;
}
.user-profile_twoots-wrapper {
  margin-right: auto;
  padding: 5px;
}
</style>