<template>
 <div class="user-profile">
  <div class="user-profile__user-panel">
   <h1 class="user-profile__username">@{{ user.username }}</h1>

   <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
   
   <div class="user-profile__follower-count">
    <strong>Followers: </strong> {{ followers }}
   </div>

   <form class="user-profile__create-twit" @submit.prevent="createNewTwit" :class="{ '--excedeed': newTwitCharacterCount > 180 }">
     <label for="newTwit"><strong>New Twit</strong> ({{ newTwitCharacterCount }}/180) </label>
     <textarea id="newTwit" rows="4" v-model="newTwitContent"></textarea>

     <div class="user-profile__create-twit-type">
       <label for="newTwitType"><strong>Type: </strong> </label>
       <select id="newTwitType" v-model="selectedTwitType">
         <option :value="option.value" v-for="(option, index) in twitTypes" :key="index">
           {{ option.name }}
         </option>
       </select>
     </div>
     <button>
       Twit!
     </button>
   </form>

  </div>
  <div class="user-profile__twits-wrapper">
   <TwitItem 
    v-for="twit in user.twits" 
    :key="twit.id" 
    :username="user.username" 
    :twit="twit" 
    @favorite="toggleFavorite"
   />
    
  
  </div>
 </div>
</template>

<script>
import TwitItem from "./TwitItem";
// import { reactive } from 'vue';
export default {
 name: 'UserProfile',
//  setup() {
//    const state = reactive({})
//  },
 components: { TwitItem },
  data() {
    return {
      newTwitContent: '',
      selectedTwitType: 'instant',
      twitTypes: [
        { value: 'draft', name: 'Draft'},
        { value: 'instant', name: 'Instant Twit'}
      ],
      followers: 0,
      user: {
        id: 1,
        username: '_RichardWindsor',
        firstName: 'Richard',
        lastName: 'Windsor',
        email: 'rw@pm.me',
        isAdmin: true,
        twits: [ 
        
         {
          id: 1,
          content: 'Twit is amazing!'
         },
         {
          id: 2,
          content: "Subscribe today!"
         }
        ]
      }
    }
  },

  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`)
      }
    }
  },

  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
    newTwitCharacterCount() {
      return this.newTwitContent.length;
    }
  },
  methods: {
    followUser() {
      this.followers++
    },
    toggleFavorite(id) {
      console.log(`Favorited Twit #${id}`);
    },
    createNewTwit() {
      if (this.newTwitContent && this.selectedTwitType !== 'draft') {this.user.twits.unshift (
      {
        id: (this.user.twits.length + 1),
        content: this.newTwitContent,
      })
      this.newTwitContent = ''
      }
    }
  },
  mounted() {
    this.followUser();
  }
}
</script>

<style lang="scss" scoped>
.user-profile {
 display: grid;
 grid-template-columns: 1fr 3fr;
 width: 100%;
 padding: 50px 5%;

  .user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #DFE3E8;

    .user-profile__admin-badge {
    background: goldenrod;
    color: white;
    border-radius: 5px;
    margin-right: auto;
    padding: 0 10px;
    font-weight: bold;
    }
  }

  textarea {
    border: 1px solid #DFE3E8;
    border-radius: 5px;
  }

  h1 {
  margin: 0;
  }

  .user-profile__twits-wrapper {
    display: grid;
    grid-gap: 10 px;
  }

  button {
    padding: 5px 20px;
    margin: auto 0;
    border-radius: 5px;
    border: none;
    background-color: rgba(32, 174, 32, 0.9);
    color: white;
  }

  .user-profile__create-twit {
    border-top: 1px solid #DFE3E8;
    padding-top: 20px;
    display: flex;
    flex-direction: column;

    &.--excedeed {
      color: red;
      // border-color: red;

      button {
        background-color: red;
        border: none;
        color: white;
      }

      textarea {
        border: 1px solid red;
        border-radius: 5px;
  }
    }

  }
}



</style>

