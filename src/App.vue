<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view/>
    <ul>
      <li v-bind:key="presenter.name + presenter['.key']" v-for="presenter in presenters">
        presenter : {{ presenter['name'] }} subject : {{ presenter['subject'] }} date : {{ presenter['date'] }}
        <button v-on:click="DeleteItem(presenter)"> delete </button>
      </li>
    </ul>
    <input placeholder="presenter" v-model="name" />
    <input placeholder="subject" v-model="subject" />
    <input placeholder="date" v-model="date" />
    <button v-on:click="AddItem">add</button>
  </div>
</template>

<script src="https://www.gstatic.com/firebasejs/4.9.1/firebase.js"></script>
<script>
  // Initialize Firebase
  import firebase from 'firebase'
  var config = {
    apiKey: "AIzaSyD_Ai6FobuWRYWpAJbB4zR3lbwI3PQASFQ",
    authDomain: "test-6dfaf.firebaseapp.com",
    databaseURL: "https://test-6dfaf.firebaseio.com",
    projectId: "test-6dfaf",
    storageBucket: "test-6dfaf.appspot.com",
    messagingSenderId: "644840902354"
  };
  let app = firebase.initializeApp(config);
  let db = app.database()
  let presentersRef = db.ref('presenters')

export default {
  name: 'App',
  firebase: {
    presenters: presentersRef
  },
  methods: {
    AddItem: function () {
      var newkey = Date.now();
      var model = {
        name: this.name,
        subject: this.subject,
        date: this.date
      };
      // console.log(this.presenters);
      db.ref('presenters/' + newkey).set(model);

      // clear
      this.name = this.subject = this.date = '';
    },
    DeleteItem: function(presenter) {
      this.presenters.forEach(element => {
        if( element.name == presenter['name'] &&
            element.subject == presenter['subject'] &&
            element.date == presenter['date']) {
          db.ref('presenters/' + element['.key']).remove();
        }
      });
    }
  },

  data () {
    return {
      name: "",
      subject: "",
      date: ""
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
