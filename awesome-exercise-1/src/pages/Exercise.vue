<template>
  <!--
	Awesome Exercise 1 - Vue.js Basics

	1) Create data properties for name and age - ok
	2) Bind these properties to the two input fields - ok
	3) Display the name and age in the beige box (first line in bold) - ok
	4) Use a computed property to display the age plus 10 years (second line in bold) - ok
	5) Display the number of characters in the name (third line) - ok
	6) Use a filter to display the name in upper case (fourth line) - ok
	7) Only show the beige box if both a name and age have been entered, otherwise, show the red box ("Please enter a name and age.") - ok
	8) Use v-show to only show the error messages next to the fields if the name is longer than 15 characters and the age is greater than 100 - ok
	9) Add the class "error" to the input fields if they break the same rules - ok
	10) When the "Generate Random Person" button is clicked, generated a random name (from an array you create) and a random age from 1 - 100. These new values should be reflected everywhere in the view - ok
	11) Create a directive which auto-focuses the name field when the page loads -ok
	12) Make it so a random person is generated when the page first loads

  -->
  <q-page padding>
    <div class="form q-mb-lg">
      <div class="row q-mb-md">
        <label>Name:</label>
        <input v-model="name" :class="{'error' : nameInvalid}" v-autofocus/>
        <label v-show="nameInvalid" class="error">Please enter 15 characters or less</label>
      </div>

      <div class="row q-mb-md">
        <label>Age:</label>
        <input v-model="age" type="number" :class="{'error' : ageInvalid }" />
        <label v-show="ageInvalid" class="error">Please enter an age between 1 - 100</label>
      </div>

      <div class="row">
        <button @click="generateRandomPersonAndAge">Generate Random Person</button>
      </div>
    </div>
    Name Lenght: {{name.length}} + Age len: {{age.length}}
    <div v-if="name.length && age.length" class="description q-mb-lg">
      <p>
        My name is
        <b>{{name}}</b> and I'm
        <b>{{age}}</b> years old.
      </p>
      <p>
        In 10 years I will be
        <b>{{agePlusTen}}</b>.
      </p>
      <p>
        My name is
        <b>{{name.length}}</b> characters long.
      </p>
      <p>
        My name in uppercase is
        <b>{{ name | nameInUpperCase}}</b>.
      </p>
    </div>
    <div v-else class="no-details">
      <p>Please enter a name and age.</p>
    </div>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      name: "Giovanne",
      age: "25",
      peopleArray: ['Giselle', 'Maria José', 'Yumi', 'Wilson', 'Luiz', 'Leandro', 'Petronio', 'Arthur', 'Ari' ]
    };
  },
  methods: {
    generateRandomPersonAndAge() {
      let pIndex = Math.floor((Math.random() * (this.peopleArray.length - 1)) + 1);
      this.name = this.peopleArray[pIndex];
      this.age = String(Math.floor((Math.random() * 99) + 1));
    },
  },
  computed: {
    agePlusTen() {
      return Number(this.age) + 10;
    },
    nameInvalid(){
      return this.name.length > 15
    },
    ageInvalid(){
      return this.age > 100 || this.age < 1
    }
  },
  filters: {
    nameInUpperCase(value) {
      return value.toUpperCase();
    }
  },
  directives: {
    autofocus: {
      inserted(ele){
        ele.focus();
      }
    }
  },
  mounted(){
    this.generateRandomPersonAndAge();
  }
};
</script>

<style>
.form {
  background: #eee;
  padding: 10px;
}
label {
  min-width: 70px;
}
label.error {
  font-size: 13px;
  color: red;
  margin-left: 5px;
  margin-top: 3px;
}
input {
  border: 1px solid #ccc;
}
input.error {
  border: 1px solid red;
  background: pink;
}
.description {
  background: antiquewhite;
  padding: 20px 20px 7px;
}
.no-details {
  background: lightcoral;
  padding: 20px 20px 7px;
}
</style>
