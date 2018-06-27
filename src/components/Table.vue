<template>
  <table class="table table-dark" v-if="plays && plays.length">
    <thead>
      <tr>
        <th scope="col">Numer meczu</th>
        <th scope="col">Drużyna 1</th>
        <th scope="col">Drużyna 2</th>
        <th scope="col">Wynik</th>
        <th scope="col" v-for="user in users">{{user.name}}</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(play, index) in plays">
        <td scope="row">{{play.id}}</td>
        <td :class="{'cell--green' : (play.score==1)}">{{play.team_1}}</td>
        <td :class="{'cell--green' : (play.score==2)}">{{play.team_2}}</td>
        <td class="bold">{{play.score}}</td>
        <td v-for="user in users" :class="{'cell--green' : (play.score==user[`match_${index+1}`])}">{{user[`match_${index+1}`]}}</td>
      </tr>
      <tr class="cell--blue">
        <td colspan="4">Suma:</td>
        <td v-for="(user, index) in users">{{sumUp[index]}}</td>
      </tr>
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
        sumUp: []
      }
    },
    methods: {
      counting: function () {
        for (let i = 0; i < this.users.length; i++) {
          let sum = 0;
          for (let j = 0; j < this.plays.length; j++) {
            if (this.plays[j].score === Number(this.users[i][`match_${j+1}`])) {
              sum++;
            }
          }
          this.sumUp[i] = sum;
          console.log(this.sumUp[i]);
        }
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
          this.counting();
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

  .cell {
    &--green {
      background-color: $color-green;
    }
    &--blue {
      background-color: $color-blue;
    }
  }
</style>