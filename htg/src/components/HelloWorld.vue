<template>
  <v-container fluid>
    <v-slide-y-transition mode="out-in">
      <v-layout column align-center>
        <img src="@/assets/finalfinal.png" alt="Vuetify.js" class="mb-5" style="width: 300px; height: 300px;">

        <v-flex xs12>
          <v-card>
            <v-card-title>
              <div>
                <span class="red--text"><h2>LIVE</h2></span><br>
              </div>
            </v-card-title>
            <v-card-actions>
              <v-layout row wrap>
                <v-alert v-show="matches.length == 0" type="info">
                  Currently there are no live matches.
                </v-alert>
                <v-flex xs6 v-for="(item,index) in matches" :key=item.matchid>
                  <v-card flat>
                    <v-container
                      fixed
                      style="min-height: 0; min-width: 500px;"
                      grid-list-lg
                    >
                      <v-layout row wrap>
                        <v-flex xs12>
                          <v-card>
                            <v-card-title primary-title>
                              <div>
                                <span><h2 class="display-1">{{item.team1}} vs {{item.team2}}</h2></span><br>
                                <v-layout row>
                                  <span><h3>{{item.team1}} - {{item.score1}} / {{item.wick1}}</h3></span><br>
                                  <v-spacer></v-spacer>
                                  <span>Overs: {{item.overs}}</span>
                                </v-layout>
                                <v-layout row>
                                  <span><h3>{{item.team2}} - {{item.score2}} / {{item.wick2}}</h3></span><br>
                                  <v-spacer></v-spacer>
                                  <span>Overs: {{item.overs}}</span>
                                </v-layout>

                              </div>
                            </v-card-title>
                            <v-card-actions>
                              <div class="layout justify-center mb-3">
                                <v-btn dark @click.native.stop="scorecard = true">Scorecard</v-btn>
                              </div>
                            </v-card-actions>
                          </v-card>
                        </v-flex>
                      </v-layout>
                    </v-container>
                  </v-card>
                </v-flex>


              </v-layout>
            </v-card-actions>
          </v-card>
        </v-flex>
      </v-layout>
    </v-slide-y-transition>

    <v-dialog v-model="scorecard" min-width="500">
      <v-card>
        <v-card-title class="headline">
          <span>Scorecard</span><br>
          <v-spacer></v-spacer>
          <span class="red--text"><h6>LIVE</h6></span>
        </v-card-title>
        <br>
        <h4 class="layout justify-center">{{team1}}</h4>
        <v-data-table
          :headers="scorecardHeaders1"
          :items="teams1"
          class="elevation-1"
        >
          <template slot="items" slot-scope="props">
            <td>{{ props.item.name }}</td>
            <td class="text-xs-right">{{ props.item.score }}</td>
            <td class="text-xs-right">{{ props.item.overs }}</td>
            <td class="text-xs-right">{{ props.item.wickets }}</td>
          </template>
        </v-data-table>
        <br>
        <h4 class="layout justify-center">{{team2}}</h4>
        <v-data-table
          :headers="scorecardHeaders2"
          :items="teams2"
          class="elevation-1"
        >
          <template slot="items" slot-scope="props">
            <td>{{ props.item.name }}</td>
            <td class="text-xs-right">{{ props.item.score }}</td>
            <td class="text-xs-right">{{ props.item.overs }}</td>
            <td class="text-xs-right">{{ props.item.wickets }}</td>
          </template>
        </v-data-table>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" flat="flat" @click.native="scorecard = false">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <br>
    <h3 class="display-2 layout justify-center"> Leadboard</h3>
    <v-data-table
      :headers="headers"
      :items="teams"
      class="elevation-1"
    >
      <template slot="items" slot-scope="props">
        <td>{{ props.item.name }}</td>
        <!--<td class="text-xs-right">{{ props.item.name }}</td>-->
        <td class="text-xs-right">{{ props.item.company }}</td>
        <td class="text-xs-right">{{ props.item.played }}</td>
        <td class="text-xs-right">{{ props.item.won }}</td>
        <td class="text-xs-right">{{ props.item.lost }}</td>
        <td class="text-xs-right">{{ props.item.nr }}</td>
      </template>
    </v-data-table>
  </v-container>

</template>

<script>
  let socket = require('socket.io-client')("localhost:3000");
  socket.emit("getTeams", function (err, res) {
    if(err) {return console.log(err)}
    res.forEach((team) => {
      // this.teams.push(team)
      console.log(team);
    })
  })

  socket.emit("getLiveMatches", function (err, res) {
    if(err) {return console.log(err)}
    res.forEach((match) => {
      // this.teams.push(team)
      console.log(match);
    })
  })
  export default {
    data () {
      return {
        team1: "SL",
        team2: "IND",
        score1: 100,
        score2: 50,
        wick1: 2,
        wick2: 10,
        overs: 6,
        matches: ['lol'],
        scorecard: false,
        headers: [
          // {
          //   text: 'Rank',
          //   align: 'left',
          //   sortable: true,
          //   value: 'name'
          // },
          { text: 'Team Name', value: 'name' },
          { text: 'Company Name', value: 'company' },
          { text: 'Played', value: 'played' },
          { text: 'Won', value: 'won' },
          { text: 'Lost', value: 'lost' },
          { text: 'N/R', value: 'nr' }
        ],
        teams: [],
        teams1: [],
        teams2: [],
        scorecardHeaders1: [
          // {
          //   text: 'Rank',
          //   align: 'left',
          //   sortable: true,
          //   value: 'name'
          // },
          { text: 'Player', value: 'name' },
          { text: 'Score', value: 'score' },
          { text: 'Overs', value: 'overs', sortable: false },
          { text: 'Wickets', value: 'wickets' }
        ],

        scorecardHeaders2: [
          // {
          //   text: 'Rank',
          //   align: 'left',
          //   sortable: true,
          //   value: 'name'
          // },
          { text: 'Player', value: 'name' },
          { text: 'Score', value: 'score' },
          { text: 'Overs', value: 'overs', sortable: false },
          { text: 'Wickets', value: 'wickets' }
        ],
      }
    },

    methods: {
      loadLeadboard (){

      }
    }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
