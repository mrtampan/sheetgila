<template>
  <div id="app">
        <div ref="spreadsheet"></div>
        <div><input type="button" value="Add new row" @click="() => spreadsheet.insertRow()" /></div>
        <div><input type="button" value="Add new Column" @click="() => spreadsheet.insertColumn()" /></div>
        <div><button @click="getData">Get Data</button></div>
  </div>
</template>

<script>
import jexcel from 'jexcel'
import 'jexcel/dist/jexcel.css'

export default {
  name: 'App',
  data() {
    return {
      items: [
          ['Jazz', 'Honda', '2019-02-12', '', true, '$ 2.000,00', '#777700'],
          ['Civic', 'Honda', '2018-07-11', '', true, '$ 4.000,01', '#007777']
      ],
      options: {
        allowToolbar:true,
        columns: [
          { type: 'text', title: 'Artis', width: '120px' },
          { type: 'dropdown', title: 'Make', width: '250px', source: [ 'Alfa Romeo', 'Audi', 'Bmw' ] },
          { type: 'calendar', title: 'Available', width: '250px' },
          { type: 'image', title: 'Photo', width: '120px' },
          { type: 'checkbox', title: 'Stock', width: '80px' },
          { type: 'numeric', title: 'Price', width: '100px', mask: '$ #.##,00', decimal: ',' },
          { type: 'color', width: '100px', render: 'square' }
        ]        
      }
      }
    },
  methods:{
    spreadsheet() {
      this.options.data = this.items
      let spreadsheet = jexcel(this.$refs.spreadsheet, this.options)
      // console.log(spreadsheet)
      Object.assign(this, { spreadsheet })
    },
    getData(){
      console.log(this.spreadsheet)
      console.log(this.items)
    }
  },
  mounted: function () {
    this.spreadsheet()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
</style>
