<template>
  <div>
    <v-toolbar
  dense
  elevation="4"
  flat
>
<v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
<v-toolbar-title>Menu</v-toolbar-title>
</v-toolbar>
<v-navigation-drawer
      app
      left
      absolute
      temporary
      v-model="drawer"
    >
    <v-list-item-group>
        
        <v-list-item >
          <v-list-item-title  @click="changeTableA">Show Table A</v-list-item-title>
        </v-list-item>
        <v-list-item >
          <v-list-item-title @click="changeTableB">Show Table B</v-list-item-title>
        </v-list-item>  
        <v-list-item >
          <v-list-item-title @click="changeTableC">Show Table C </v-list-item-title>
        </v-list-item>
        
      </v-list-item-group>
      
  </v-navigation-drawer>
  <v-data-table v-if="showTableA"
    :headers="headers"
    :items="row"
    hide-default-footer
    class="elevation-1"
    disable-pagination
    
    >
    
  </v-data-table>
  <v-data-table v-else-if="showTableB"
    :headers="headersB"
    :items="rowB"
    hide-default-footer
    class="elevation-1"
    disable-pagination
    
    >
    
  </v-data-table>
  <v-data-table v-else-if="showTableC"
    :headers="headersC"
    :items="rowC"
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
    showTableA: true,
    showTableB: false,
    showTableC: false,
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
    headersB: [
      {
        text: 'B',
        align: 'start',
        sortable: false,
        value: 'date',
      },
      { text: 'B', value: 'number' },
      { text: 'B', value: 'value' },
     
    ],
    rowB: [
     
    ],
    headersC: [
      {
        text: 'C',
        align: 'start',
        sortable: false,
        value: 'date',
      },
      { text: 'C', value: 'number' },
      { text: 'C', value: 'value' },
     
    ],
    rowC: [
     
    ],
    drawer: false,

    
  }
  
},
methods: {
  addRow() {
    let time = new Date()
    const holidays = [  new Date('Mon Jan 03 2022 00:00:00 GMT+0300 (Москва, стандартное время)'),
        new Date('Tue Jan 04 2022 00:00:00 GMT+0300 (Москва, стандартное время)'),
        new Date(  'Wed Jan 05 2022 00:00:00 GMT+0300 (Москва, стандартное время)'),
                        // 'Thu Jan 06 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        // 'Fri Jan 07 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        // 'Sat Jan 02 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        // 'Wed Feb 23 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        // 'Mon Mar 07 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        // 'tue Mar 08 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        // 'Mon May 02 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        // 'Tue May 03 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        // 'Mon May 09 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        // 'Tue May 10 2022 00:00:00 GMT+0300 (Москва, стандартное время)'

                      ]
    const getBusinessDays = (startDate, endDate) => {
    const start = new Date(startDate);
    
    const end = new Date(endDate);
    
    const dates = [];
    
    //const dateFree = dates.filter(x => !holidays.includes(x));
    //holidays.indexOf(current) > -1
    while (start <= end) {
      console.log(new Date(start))
      const match = holidays.find(d => d.getTime() === start.getTime())
      const hasMatch = !!match;
      if (start.getDay() !== 6 && start.getDay() !== 0 && !hasMatch) {
        dates.push(new Date(start));
      }

      start.setDate(start.getDate() + 1);
    }

    return dates
    
    
  }

 
const businessDays = getBusinessDays('01-01-2022', '01-10-2022');  
    this.row.push( {
        date: time.getHours() + ':' + time.getMinutes(),
        number: parseInt(Math.random() * (100 - (-100)) + (-100)),
        value: businessDays[Math.floor(Math.random()*businessDays.length)]
      }
    )
  },
changeTableB() { 
  
  this.showTableB = true
  this.showTableA = false
  this.showTableC = false
  
  
},
changeTableA() { 
  this.showTableB = false
  this.showTableA = true
  this.showTableC = false
  
},
changeTableC() { 
  this.showTableB = false
  this.showTableA = false
  this.showTableC = true
},


 
},


}
</script>
