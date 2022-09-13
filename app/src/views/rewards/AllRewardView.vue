<template>
  <section class="mx-8">
    <h1 class="text-3xl text-yellow-700">{{ title }}</h1>

    <div v-if="error != null">
      {{ error }}
    </div>

    <div v-for="reward in rewards"
         :key="reward.id"
         class="grid grid-cols-2 p-4 mb-4 border-2 border-blue-800 rounded-lg"
    >
      <h3 class="text-xl">{{ reward.name }}</h3>
      <p class="text-5xl">{{ reward.point }}</p>
      <RouterLink :to="`rewards/${reward.id}`">Detail</RouterLink>
      <button @click="selectReward(reward)"
         class="px-2 py-1 border rounded-xl"
      >
        Redeem
      </button>
    </div>
    
    {{ selected }}
  </section>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      title: "Reward List",
      selected: null,
      rewards: null,
      error: null
    }
  },
  methods: {
    selectReward(reward) {
      this.$router.push({
        name: 'rewards.show', 
        params: { id: reward.id }
      })
    }
  },
  async mounted() {
    console.log("mounted")
    this.error = null
    const url = "http://localhost/api/rewards"

    try {
      const response = await axios.get(url)
      if (response.status === 200) {
        this.rewards = response.data.data
      } else {
        console.error(response.status)
      }
    } catch (error) {
      this.error = error.message
    }
  }
}
</script>

<style>

</style>