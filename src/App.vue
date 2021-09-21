<template>
  <div id="app">
    <h1>Min Lista</h1>
    <!-- saveData är cb-funktion som Form.vue kallar o som körs här -> handleSubmit körs här: -->
    <button @click="onClick" v-if="clickNewItem == false">Nytt inlägg</button>
    <Form v-if="clickNewItem == true" @saveData="handleSubmit"/><br />
    <div id="msg-container" v-if="showErrorMsg== true">
      Du måste fylla i alla fält för att kunna spara!
    </div>
    <List :items="items"/>
  </div>
</template>

<script>
import Form from './components/Form.vue';
import List from './components/List.vue';
let crypto = require("crypto");

export default {
  name: 'App',
  data() {
    return{ 
      //states:
      items: [],
      item: {},
      showErrorMsg: false,
      clickNewItem: false,
    }
  },
  created() {
    //get items from lS if lS not empty
    if (JSON.parse(localStorage.getItem("items")) != null) {

      //uppdatera i statet items:
      this.items = JSON.parse(localStorage.getItem("items"));
    } 
  },
  components: 
    { Form, List },
  methods: {
    handleSubmit(evt) {
      evt.preventDefault();

      let randId = crypto.randomBytes(10).toString('hex');
      let newItem = {
          id: randId,
          title: evt.target.title.value, 
          date: evt.target.date.value, 
          text: evt.target.text.value
      }
      this.item=newItem;

      if (newItem.title && newItem.date && newItem.text != "") {
        // console.log("spara", newItem);
        //add newItem to items
        this.items.push(newItem) 
        // console.log("items after push", this.items);

        //sort
        let sortedItems = this.items.sort(function(a,b) {
          return new Date(b.date) - new Date(a.date);
        })
        // console.log("sortedItems", sortedItems);

        //add newItem to items in lS
        localStorage.setItem("items", JSON.stringify(sortedItems));

        this.showErrorMsg = false;

      } else {
        this.showErrorMsg = true;
      }
      // console.log("newItem i app.vue", newItem);
    }, 
    onClick() {
      // console.log("klick skriv nytt inlägg", evt);
      this.clickNewItem = true;
    }

  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#msg-container {
  color: red;
  border: 1px solid red;
}
</style>
