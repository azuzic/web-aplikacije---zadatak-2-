<template>
  <v-app>
    <v-main>
      
      <div class="main py-4 px-4">
        <div class="inputs">
          <v-text-field
          label="Enter name"
          solo
          dense
          v-model="name"
        ></v-text-field>
        <v-btn
          class="ml-4"
          color="accent"
          elevation="2"
          @click="fetchData(name)"
        > send </v-btn>
        </div>
        <v-data-table
          :headers="headers"
          :items="data"
          class="elevation-1"
        ></v-data-table>
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
        name: "",
        headers: [
          { text: 'Name', align: 'start', sortable: false, value: 'name' },
          { text: 'Country', value: 'country' },
          { text: 'Country Probability', value: 'CProbability' },
          { text: 'Age', value: 'age' },
          { text: 'Gender', value: 'gender' },
          { text: 'Gender Probability', value: 'GProbability' },
        ],
        data: [
        ],
      }
    },
    methods: {
      async fetchData(name) {
        const response1 = await fetch("https://api.agify.io/?name="+name);
        let agify = await response1.json();
        const response2 = await fetch("https://api.genderize.io?name="+name);
        let genderize = await response2.json();
        const response3 = await fetch("https://api.nationalize.io?name="+name);
        let nationalize = await response3.json();
        this.data.push(
          {
            name: name,
            country: agify.age,
            CProbability: nationalize.country[0].country_id,
            age: Math.round(nationalize.country[0].probability * 100) + "%",
            gender: genderize.gender,
            GProbability: Math.round(genderize.probability * 100) + "%"
          }
        )
      } 
    }
  }
</script>

<style scoped lang="scss">
.main {
  width: 100%;
  height: 100%;
  .inputs {
    display: flex;
  }
}
</style>
