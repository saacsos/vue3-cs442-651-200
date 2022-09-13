<template>
  <div 
    class="grid grid-cols-2 p-4 mb-4 border-2 border-blue-800 rounded-lg"
  >
    <h3 class="text-xl">{{ reward.name }}</h3>
    <p class="text-5xl">{{ reward.point }}</p>

    <div class="italic">
      <slot></slot>
    </div>

    <div class="text-2xl font-bold">
      <slot name="total_amount"></slot>
    </div>
    
    
    <router-link v-if="url != ''" :to="url">Detail 1</router-link>
    
    <span class="text-blue-700 my-style" 
      :class="url == '' ? '': 'cursor-pointer'"
      @click="onClickButton()">
      Detail 2
    </span>
    <button @click="onClickButton()"
      class="px-2 py-1 border rounded-xl">
      Redeem
    </button>

    <button @click="onClickLike()"
      class="px-2 py-1 border rounded-xl">
      {{ likeCount }} Likes
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      likeCount: 0
    }
  },
  props: {
    reward: Object,
    url: {
      type: String,
      default: ''
    }
  },
  methods: {
    onClickLike() {
      this.likeCount++
    },
    onClickButton() {
      if (this.url != '') {
        this.$router.push(this.url)
      }
    }
  }
}
</script>

<style scoped>
.my-style {
  @apply block p-2 bg-pink-300 w-20;
}
</style>