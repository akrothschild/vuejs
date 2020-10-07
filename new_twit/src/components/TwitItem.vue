<template>
 <div class="twit-item" @click="favoriteTwit(twit.id)">
  <div class="user-profile__twit">
   <div class="twit-item__user">
    @{{ username }}
   </div>
   <div class="twit-item__content">
    {{ twit.content }}
   </div>
  </div>
 </div>
</template>

<script>
export default {
 name: "TwitItem",
 props: {

  username: {
   type: String,
   required: true,
  },
 
  twit: {
   type: Object,
   required: true,
  }
 },

 methods: {
  favoriteTwit(id) {
   this.$emit('favorite', id)
  }
 }
}
</script>

<style lang="scss" scoped>
.twit-item {
 padding: 20px;
 background-color: white;
 border-radius: 5px;
 border: 1px solid #DFE3E8;
 box-sizing: border-box;
 cursor: pointer;
 transition: all 0.25s ease;

// .twit-item:hover
 &:hover { 
  transform: scale(1.1, 1.1);
 }

  .twit-item__user {
   font-weight: bold;
  }
}




</style>