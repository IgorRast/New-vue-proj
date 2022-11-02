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
    const holidays = [  'Mon Jan 03 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        'Tue Jan 04 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        'Wed Jan 05 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        'Thu Jan 06 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        'Fri Jan 07 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        'Sat Jan 02 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        'Wed Feb 23 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        'Mon Mar 07 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        'tue Mar 08 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        'Mon May 02 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        'Tue May 03 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        'Mon May 09 2022 00:00:00 GMT+0300 (Москва, стандартное время)',
                        'Tue May 10 2022 00:00:00 GMT+0300 (Москва, стандартное время)'

                      ]
    const getBusinessDays = (startDate, endDate) => {
    const start = new Date(startDate);
    console.log(start)
    const end = new Date(endDate);
    const current = start;
    const dates = [];
    
    //const dateFree = dates.filter(x => !holidays.includes(x));

    while (current <= end) {
      if (current.getDay() !== 6 && current.getDay() !== 0) {
        dates.push(new Date(current));
      }

      current.setDate(current.getDate() + 1);
    }

    return dates.filter(function(start){
        return holidays.indexOf(start) < 0;
    });
    
  }

 
const businessDays = getBusinessDays('01-01-2022', '11-31-2022');  
    this.row.push( {
        date: time.getHours() + ':' + time.getMinutes(),
        number: parseInt(Math.random() * (100 - (-100)) + (-100)),
        value: businessDays[Math.floor(Math.random()*businessDays.length)]
      }
    )
  },
 
 
},


}
</script>
