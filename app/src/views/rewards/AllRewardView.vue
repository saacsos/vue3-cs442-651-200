<template>
  <section class="mx-8">
    <h1 class="text-3xl text-yellow-700">{{ title }}</h1>

    <div v-for="reward in rewards"
         :key="reward.id"
         class="grid grid-cols-2 p-4 mb-4 border-2 border-blue-800 rounded-lg"
    >
      <h3 class="text-xl">{{ reward.name }}</h3>
      <p class="text-5xl">{{ reward.point }}</p>
      <button v-on:click="selectReward(reward)"
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
      rewards: null
    }
  },
  methods: {
    selectReward(reward) {
      this.selected = reward
      console.table(this.selected)
    }
  },
  async mounted() {
    console.log("mounted")
    const url = "http://localhost/api/rewards"
    // const response = axios.get(url)
    //           .then((responseData) => {
    //             this.rewards = responseData.data.data
    //           })

    // Non-Blocking I/O
    // Asynchronous Language
      // 1. Callback -> Hell Loop
      // 2. Promise -> Hell Loop
      // 3. async-await

    try {
      const response = await axios.get(url)
      if (response.status === 200) {
        this.rewards = response.data.data
      } else {
        console.error(response.status)
      }
    } catch (error) {
      console.error(error.message)
      this.selected = error.message
    }
  }
}
</script>

<style>

</style>