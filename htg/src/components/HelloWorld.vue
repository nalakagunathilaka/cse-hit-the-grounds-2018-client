<template>
  <v-container fluid>
    <v-slide-y-transition mode="out-in">
      <v-layout column align-center>
        <img src="@/assets/logo.png" alt="Vuetify.js" class="mb-5">

        <v-flex xs12>
          <v-card>
            <v-card-title>
              <div>
                <span class="red--text"><h2>LIVE</h2></span><br>
              </div>
            </v-card-title>
            <v-card-actions>
              <v-layout row wrap>
                <v-flex xs3>
                  <v-card>
                    <v-card-title primary-title>
                      <div class="headline">Unlimited music now</div>
                      <div>Listen to your favorite artists and albums whenever and wherever, online and offline.</div>
                    </v-card-title>
                    <v-card-actions>
                      <v-btn flat dark>Listen now</v-btn>
                    </v-card-actions>
                  </v-card>
                </v-flex>
                <v-flex xs12>
                  <v-card>
                    <v-container fluid grid-list-lg>
                      <v-layout row>
                        <v-flex xs7>
                          <div>
                            <div class="headline">Supermodel</div>
                            <div>Foster the People</div>
                          </div>
                        </v-flex>
                        <v-flex xs5>
                          <v-card-media
                            src="/static/doc-images/cards/foster.jpg"
                            height="125px"
                            contain
                          ></v-card-media>
                        </v-flex>
                      </v-layout>
                    </v-container>
                  </v-card>
                </v-flex>
                <v-flex xs12>
                  <v-card>
                    <v-container fluid grid-list-lg>
                      <v-layout row>
                        <v-flex xs7>
                          <div>
                            <div class="headline">Halycon Days</div>
                            <div>Ellie Goulding</div>
                          </div>
                        </v-flex>
                        <v-flex xs5>
                          <v-card-media
                            src="/static/doc-images/cards/halcyon.png"
                            height="125px"
                            contain
                          ></v-card-media>
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
  </v-container>
</template>

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
