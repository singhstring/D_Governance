<template>
  <v-flex xs6>
    <v-card class="card--flex-toolbar">
      <v-toolbar card class="green">
        <v-toolbar-title class="white--text">Send Message</v-toolbar-title>
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
          <v-list-tile-title>
            Message
          </v-list-tile-title>
          <v-list-tile-content>
  
            <v-text-field label="Type the message here.." single-line v-model.number="message"></v-text-field>
  
          </v-list-tile-content>
        </v-list-tile>
  
        <v-list-tile>
  
          <v-spacer></v-spacer>
  
          <v-list-tile-action>
            <v-btn primary dark @click.native="sendMsg">Send</v-btn>
          </v-list-tile-action>
        </v-list-tile>
  
      </v-list>
  
    </v-card>
  </v-flex>
</template>


<script>
import { CONTRACT } from '../contract'
import _ from 'lodash'
import ipfs from '../ipfs';


export default {
  data () {
    return {
      addr: null,
      message: null
    }
  },

  methods: {
    sendMsg() {

      if (!web3.isAddress(this.addr)) {
        alert('Invalid address!')
        this.addr = null
        return
      }

      console.log('hi0');
      const buffer = Buffer.from(this.message);
      console.log(buffer);
      console.log('hi1');

      ipfs.add(this.buffer, (err, ipfsHash) => {
        console.log(err,ipfsHash);
        console.log('hi2');

        CONTRACT.transferMessage(this.addr,ipfsHash[0].hash, (err, res) => {
          if (!err) {
            console.log(res)
            console.log('hi3');
            this.addr = this.message = null
            return
          }
          console.log(err)
          this.addr = this.message = null
        });

      

      })

    }
  }
}
</script>

