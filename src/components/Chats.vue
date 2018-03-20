<template>
  <v-flex xs12>
    <v-card class="card--flex-toolbar">
      <v-toolbar card class="green">
        <v-toolbar-title class="white--text">Chats</v-toolbar-title>
      </v-toolbar>
  

      <v-list>
      <v-list-tile>
        <v-list-tile-action>
        <v-btn primary dark @click.native="viewChats">
        viewChats</v-btn>
        </v-list-tile-action>
      </v-list-tile>
      </v-list>


      <v-data-table :headers="headers" :items="items" hide-actions class="elevation-1">
        <template slot="items" scope="props">
          <td class="text-xs-left">{{ props.item.tstamp }}</td>
          <td class="text-xs-left">{{ props.item.to }}</td>
          <td class="text-xs-left">{{ props.item.from }}</td>
          <td class="text-xs-left">{{ props.item.message }}</td>
        </template>
      </v-data-table>
  
    </v-card>
  </v-flex>
</template>
<script>
import { CONTRACT } from '../contract'
import ipfs from '../ipfs';

export default {
  data () {
    return {
      headers: [
        { align: 'left', text: 'Time Stamp', value: 'tstamp' },
        { align: 'left', text: 'To', value: 'to' },
        { align: 'left', text: 'From', value: 'from' },
        { align: 'left', text: 'Message', value: 'message' }
      ],
      items: []
    }
  },

  methods: {
    viewChats() {
      
      CONTRACT.getMessage( (err,res) => {
        if(!err) {
        items=[];
          var arrLen= res.length;
          for(var i=0;i<arrLen;i++) {
              var struct_res=res[i];
              ipfs.cat(struct_res.args.ipfsHash, (err2, ret_str) => {
                 if (err2) {
                   console.log(err2);
                 }
                 
                });

                  this.items.push({
                    tstamp: res.args.timestamp,
                    to: res.args._to,
                    from: CONTRACT._eth.coinbase,
                    message: ret_str
        })
          }
        }
        console.log(err)
      } )

      
    }
  }/*,

  mounted () {
    CONTRACT.TransferMessage({}, { fromBlock: 0, toBlock: 'pending' }, (err, res) => {
      if (res.args.to === CONTRACT._eth.coinbase || res.args.from === CONTRACT._eth.coinbase) {
        this.items.push({
          tstamp: res.args.tstamp,
          to: res.args.to,
          from: res.args.from,
          message: res.args.message
        })
      }
    })
  }*/
}
</script>

