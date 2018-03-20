<template>
  <v-flex xs6>
    <v-card class="card--flex-toolbar">
      <v-toolbar card class="green">
        <v-toolbar-title class="white--text">Block/Unblock</v-toolbar-title>
      </v-toolbar>
      <v-list>
        <v-list-tile>
          <v-list-tile-title>
            To Address
          </v-list-tile-title>
          <v-list-tile-content>
  
            <v-text-field label="0x00" single-line v-model="addr"></v-text-field>
  
          </v-list-tile-content>
        </v-list-tile>
  
  
        <v-list-tile>
  
          <v-spacer></v-spacer>
  
          <v-list-tile-action>
            <v-btn primary dark @click.native="blockP">Block</v-btn>
          </v-list-tile-action>
        </v-list-tile>


        <v-list-tile>
  
          <v-spacer></v-spacer>
  
          <v-list-tile-action>
            <v-btn primary dark @click.native="unblockP">Unblock</v-btn>
          </v-list-tile-action>
        </v-list-tile>
  
      </v-list>
  
    </v-card>
  </v-flex>
</template>
<script>
import { CONTRACT } from '../contract'
import _ from 'lodash'

export default {
  data () {
    return {
      addr: null,
    }
  },

  methods: {
    blockP () {
      if (!web3.isAddress(this.addr)) {
        alert('Invalid address!')
        this.addr = null
        return
      }

      CONTRACT.blockPerson(this.addr
      , (err, res) => {
        if (!err) {
          console.log(res)
          this.addr = null
          return
        }
        console.log(err)
        this.addr = null
      })
    },

    unblockP () {
      if (!web3.isAddress(this.addr)) {
        alert('Invalid address!')
        this.addr = null
        return
      }

      CONTRACT.unblockPerson(this.addr
      , (err, res) => {
        if (!err) {
          console.log(res)
          this.addr = null
          return
        }
        console.log(err)
        this.addr = null
      })
    }



  }
}
</script>

