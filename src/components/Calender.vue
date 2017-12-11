<template>
<div class="container">
    <div class="col-md-4">
        <calendar 
          :value="value" 
          :disabled-days-of-week="disabled" 
          :format="format"
          :clear-button="clear"
          :placeholder="placeholder"     
          :has-input="false"
          :on-day-click="onDayClick2">
        </calendar>
    </div>
    <div class="col-md-8">
        <div class="col-md-12">
            <button @click="addOccasion()" class="btn btn-primary">Add Occasion</button>
        </div>
        <div class="col-md-4">
            <!-- <input type="date" name="dates" id="dateSheet" min="2018-01-01"> -->
            <div class="dropdown" v-dropdown>
                <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu1" data-toggle="dropdown" 
                aria-haspopup="true" aria-expanded="true">
                    {{eventName}}
                    <span class="caret"></span>
                </button>
                <ul class="dropdown-menu" aria-labelledby="dropdownMenu1">
                    <li v-for="(occasion, index) in occasions" @click="userOccasions(index)" :key="index" 
                    class="list-group-item" >{{occasion.name}}</li>
                </ul>
            </div>
            <input type="text" placeholder="Enter Detail" v-model="name">
        </div>
        <ul class="list-group col-md-12">
            <li v-for="(listOccasion, index) in listOccasions" @click="listItem($event)" :key="index" class="list-group-item">
              {{listOccasion.date}}th/{{listOccasion.month}} : {{listOccasion.eventName}} : {{listOccasion.detail}}
                <button v-on:click="del(index)" class="btn btn-danger btn-xs right">Delete</button>
            </li>
        </ul>
    </div>
    <!-- <button class="btn btn-success" @click="save()">save</button> -->
</div>
</template>
<script>
import Calendar from 'vue2-slot-calendar';
export default {
  components: {
    calendar: Calendar
    },
  data() {
    return {
      name: '',
      eventName: 'Select Event',
      listOccasions:[
          {
            date : '6',
            month: '12',
            eventName: 'Birthday',
            detail: 'Rupesh'
          },
          {
            date : '6',
            month: '1',
            eventName: 'Birthday',
            detail: 'Satyam'
          }
        ],
      occasions: [{name:"Birthday"},{name: 'Aniversiry'},{name: 'Festival'},{name: 'Travel'}],
      date: 'currrent',
      disabled: [],
      value: '',
      format: 'dd-MMM-yyyy',
      clear: true,
      placeholder: 'placeholder is displayed when value is null or empty',
      selectedDate: '',
      userDate: '',
      userMonth: ''
    }
  },
  methods:{
    addOccasion:function(){
      var add = {
            date : this.userDate,
            month: this.userMonth,
            eventName: this.eventName,
            detail: this.name
          }
      this.listOccasions.push(add);
    },
    onDayClick2: function(selectedDate){
      this.selectedDate = selectedDate;
      console.log(this.selectedDate);
      var date = this.selectedDate.getDate();
      var month = (this.selectedDate.getMonth() + 1);
       this.userDate = date;
       this.userMonth = month;
    },
    userOccasions: function(index){
      console.log('Index value',index);
      console.log(this.occasions[index].name);
      var occ = this.occasions[index].name;
      this.eventName = occ;
    },
    save: function(){
      console.log(this.value);
      console.log(this.userselect);
      var m = document.getElementById('usr').value;
      console.log(m);
      console.log(this.listOccasions);
    },
    del:function(index){
            this.listOccasions.splice(index,1);
    }
  }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.open>.dropdown-menu {
    display: block;
    margin-left: 27%;
}
h1, h2 {
  font-weight: normal;
}
a {
  color: #42b983;
}
</style>
