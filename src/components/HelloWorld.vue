<template>
  <div class="hello">
    <h1>SpaceX Ships</h1>
    <p class="type_text">Type: <select v-model="type">
      <option label="All"></option>
      <option value="Cargo">Cargo</option>
      <option value="High Speed Craft">High Speed Craft</option>
      <option value="Tug">Tug</option>
      <option value="Barge">Barge</option>
    </select></p>
      <ApolloQuery :query="require('../graphql/Ships.gql')" :variables="{limit, type}">
        <template v-slot="{result:{loading, error, data} }">
          <div v-if="data">
            <div class="data_container">
              <div class="header">
              <p>Picture</p>
              <p>Name</p>
              <p>Type</p>
              <p>Weight kg</p>
              <p>Year built</p>
              <p>Weight lbs</p>
            </div>
            <div class="ship_container" v-for="ship in data.ships" :key="ship.id">
              <div><img :src="ship.image"></div>
              <p>{{ship.name}}</p>
              <p>{{ship.type}}</p>
              <p>{{ship.weight_kg}}</p>
              <p>{{ship.year_built}}</p>
              <p>{{ship.weight_lbs}}</p>
            </div>
            </div>
          </div>
        </template>
      </ApolloQuery>
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  data() {
    return {
      limit: 20,
      type: ""
    };
  },
  props: {
    msg: String
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

select {
  margin-bottom: 20px;
  height: 50px;
  padding: 5px;
  font-size: 20px;
  font-weight: bold;
  border: 2px solid orange;
}

a { cursor: pointer; }
        .pagination {
           justify-content: center;
           flex-wrap: wrap;
        }

.ship_container, .header {
  display: grid;
  grid-template-columns: 150px 150px 150px 150px 150px 150px;
  grid-column-gap: 50px;
  align-items: center;
  justify-content: space-evenly;
  width: fit-content;
  height: 150px;
}

.type_text {
  font-weight: bold;
  color: black;
  text-align: left;
  margin-left: 350px;
}

.ship_container {
  background-color: #42b983;
  border: 2px solid white;
}

.data_container {
  display: flex;
  align-items: center;
  flex-direction: column;
}

.header {
  margin-bottom: 2px;
  background-color: orange;
  height: 100px;
}

img {
  width: 150px;
  height: 150px;
}

p {
  font-size: 20px; 
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
