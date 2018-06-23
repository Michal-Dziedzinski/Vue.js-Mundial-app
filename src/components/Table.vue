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
      <tr v-for="(play, index1) in plays">
        <td scope="row" :class="{'cell--blue' : (play.id==21)}">{{play.id}}</td>
        <td :class="{'cell--green' : (play.score==1)}">{{play.team_1}}</td>
        <td :class="{'cell--green' : (play.score==2)}">{{play.team_2}}</td>
        <td>{{play.score}}</td>
        <td v-for="(user, index2) in users" :class="{'cell--green' : (play.score==user[`match_${index1+1}`])}">{{user[`match_${index1+1}`]}}</td>
        <td>{{counting}}</td>
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
        index: 0,
        sum: []
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
    },
    computed: {
      counting: function (index1, index2) {
        for (let i = 0; i < this.users.length; i++) {
          for (let j = 0; j < this.plays.length; j++) {
            // if (this.plays[i].score == this.users[j]+`.match_${i+1}`) {
            //   console.log('siema');
            // }
            let text = `match_${i+1}`;
            obj = JSON.parse(text);
            console.log(eval(this.users[j].obj));
          }
          // console.log(this.plays[i].score);
        }
      }
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