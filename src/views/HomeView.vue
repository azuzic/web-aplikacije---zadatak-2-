<template>
  <v-app>
    <v-main>
      
      <div class="main flex items-center justify-center">
        
      </div>

    </v-main>
  </v-app>
</template>

<script>
  export default {
    name: 'Home',

    components: {
    },

    data() { 
      return {
        commits: [],
        comm: Object,
        hide: false
      }
    },
    async created() {
      const response = await fetch("https://api.github.com/repos/vuejs/vue/commits");
      this.commits = await response.json();
      this.commits = this.commits.slice(0, 10)
    },
    methods: {
      btn() {
        this.hide = !this.hide;
      }
    }
  }
</script>

<style scoped lang="scss">
.main {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
