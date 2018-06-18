<template>
  <div id="app">
    <!-- <p>{{test}}</p> -->

    <!-- <table class="table table-dark" v-if="plays && plays.length">
      <thead>
        <tr>
          <th scope="col">Numer meczu</th>
          <th scope="col">Drużyna 1</th>
          <th scope="col">Drużyna 2</th>
          <th scope="col">Last</th>
          <th scope="col">Handle</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="play in plays">
          <td scope="row">{{play.id}}</td>
          <td>{{play.team_1}}</td>
          <td>{{play.team_2}}</td>
        </tr>
        <tr>
          <th scope="row">2</th>
          <td>Jacob</td>
          <td>Thornton</td>
          <td>@fat</td>
        </tr>
        <tr>
          <th scope="row">3</th>
          <td>Larry</td>
          <td>the Bird</td>
          <td>@twitter</td>
        </tr>
      </tbody>
    </table> -->


    <!-- <ul v-if="plays && plays.length">
      <li v-for="play in plays">
        <p>
          <strong>{{play.score}}</strong>
        </p>
        <p><strong>{{play.team_1}}</strong></p>
        <p>{{score.body}}</p>
      </li>
    </ul> -->
    <HelloWorld/>
  </div>
</template>

<script>
  // import axios from "axios";
  import HelloWorld from './components/HelloWorld'

  export default {
    name: 'App',
    // data() {
    //   return {
    //     plays: []
    //   }
    // },
    // computed: {
    //   test: function() {
    //     return console.log(this.plays);
    //   }
    // },
    components: {
      HelloWorld
    }
  //   created() {

  //     axios.get("http://localhost:3000/matches")
  //       .then(response => {
  //         this.plays = response.data;
  //       })
  //       .catch(e => {
  //         this.errors.push(e)
  //       })
  //   }
  }
</script>

<style>
</style>