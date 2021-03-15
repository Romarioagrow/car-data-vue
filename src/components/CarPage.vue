<template>
  <v-container>
    <h1>Car Page</h1>

    <v-list v-for="carItem in carsList" :key="carItem.postId">

      <v-card>
        <v-card-actions>
          <v-list-item three-line>
            <v-list-item-content>
              <v-img contain :src="resolveFirstImage(carItem.featuredImages)" max-height="150"
              ></v-img>
              <v-list-item-title>
                {{ carItem.title }}
              </v-list-item-title>
              <v-list-item-subtitle>
                {{ carItem.carName }}
              </v-list-item-subtitle>
              <v-list-item-action>
                <v-list-item-subtitle>
                {{ carItem.previewText }}
              </v-list-item-subtitle>
              </v-list-item-action>

            </v-list-item-content>
          </v-list-item>
        </v-card-actions>
      </v-card>
    </v-list>

  </v-container>
</template>

<script>
import axios from "axios";
export default {
  props: {
    msg: String
  },
  data() {
    return {
      loadListUrl: 'https://drivn.com/api/feed',
      carsList: [],
    }
  },
  created() {

    this.loadCardList()

  },
  methods: {
    loadCardList() {
      axios.get(this.loadListUrl).then(response => {
        console.log('response', response)

        if (response && response.data) {
          response.data.forEach(carPostObject => {
            console.log(carPostObject.item)

            if (carPostObject && carPostObject.item) {
              this.carsList.push(carPostObject.item)
            }
          })

        } else {
          console.log('Error with received data')
        }
      })
    },
    resolveFirstImage(featuredImages) {
      return featuredImages ? featuredImages[0].url : '';
    }
  },

}
</script>

<style scoped>
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
