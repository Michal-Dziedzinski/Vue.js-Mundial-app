<template>
  <table class="table table-dark" v-if="plays && plays.length">
    <thead>
      <tr>
        <th scope="col">Numer meczu</th>
        <th scope="col">Drużyna 1</th>
        <th scope="col">Drużyna 2</th>
        <th scope="col">Wynik</th>
        <th scope="col" v-for="user in users">{{user.name}}</th>
        <!-- <th></th> -->
      </tr>
    </thead>
    <tbody>
      <tr v-for="(play, index) in plays">
        <td scope="row" :class="{'cell--blue' : (play.id==19)}">{{play.id}}</td>
        <td :class="{'cell--green' : (play.score==1)}">{{play.team_1}}</td>
        <td :class="{'cell--green' : (play.score==2)}">{{play.team_2}}</td>
        <td>{{play.score}}</td>
        <td v-for="user in users" :class="{'cell--green' : (play.score==user[`match_${index+1}`])}">{{user[`match_${index+1}`]}}</td>
        <!-- <td>{{users[1].match_2}}</td>
        <td>{{users[2].match_3}}</td> -->
      </tr>
      <!-- <tr>
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
        </tr> -->
    </tbody>
  </table>
</template>

<script>
  import axios from "axios";

  export default {
    name: 'Table',
    data() {
      return {
        plays: [],
        users: [],
        index: 0
      }
    },
    created() {
      axios.get("http://localhost:3000/matches")
        .then(response => {
          this.plays = response.data;
        })
        .catch(e => {
          this.errors.push(e)
        })
      axios.get("http://localhost:3000/users")
        .then(response => {
          this.users = response.data;
        })
        .catch(e => {
          this.errors.push(e)
        })
    }
    
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
  @import "../assets/scss/main.scss";

  .cell{
    &--green{
      background-color: $color-green;
    }
    &--blue{
      background-color: $color-blue;
    }
  }
</style>