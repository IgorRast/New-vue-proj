<template>
  <div>
  <v-data-table
    :headers="headers"
    :items="row"
    hide-default-footer
    class="elevation-1"
    disable-pagination
    
    >
    
  </v-data-table>
  <v-btn depressed v-on:click="addRow">
    Add Row
  </v-btn>
 
  
</div>
</template>

<script>

export default {
data () {
  return {
    headers: [
      {
        text: 'Date',
        align: 'start',
        sortable: false,
        value: 'date',
      },
      { text: 'Number', value: 'number' },
      { text: 'Value', value: 'value' },
     
    ],
    row: [
     
    ],
    
  }
  
},
methods: {
  addRow() {
    let time = new Date()
    this.row.push( {
        date: time.getHours() + ':' + time.getMinutes(),
        number: parseInt(Math.random() * (100 - (-100)) + (-100)),
        value: '1'
      }
    )
  },
 
 
},


}
</script>
