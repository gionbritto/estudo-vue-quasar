<template>
  <q-page padding>
    <button style="position:absolute; right: 10px" @click="counter++">{{counter}}</button>
    <input
      v-model="message"
      @keyup.esc="clearMessage"
      @keyup.enter="alertMessage"
      v-autofocus
      :style="errorStyle"
      ref="messageInput"
    />

    <button @click="clearMessage">Clear</button>

    <div>{{message.length}}</div>

    <input 
      v-model="message2"
      :class="{'error' : message2.length > 22}" 
      />

    <h5 v-if="message.length" class="border-gray">{{ message }}</h5>
    <h6 v-else>No message entered :((</h6>

    <hr />

    <p>Uppercase message: {{ messageUppercase }}</p>
    <p>lowercase message: {{message | messageLowercase}}</p>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      message: "i love vuejs so hard!",
      message2: '',
      counter: 0
    };
  },
  computed: {
    messageUppercase() {
      console.log("message was fired");
      return this.message.toUpperCase();
    },
    errorStyle() {
      if (this.message.length > 22) {
        return {
          color: "red",
          background: "pink"
        };
      }
    }
  },
  methods: {
    clearMessage() {
      this.message = "";
    },
    handleKeyup(e) {
      console.log(e);
      if (e.keyCode === 27) {
        this.clearMessage();
      } else if (e.keyCode === 13) {
        this.alertMessage();
      }
    },
    alertMessage() {
      alert(this.message);
    }
  },
  filters: {
    messageLowercase(value) {
      return value.toLowerCase();
    }
  },
  directives: {
    autofocus: {
      inserted(el) {
        el.focus();
      }
    }
  },
  mounted() {
    console.log(this.$refs);
    this.$refs.messageInput.className = "bg-green";
  }
};
</script>

<style>
.border-gray {
  border: 1px solid grey;
}
input,
button {
  font-size: 23px;
}
.error {
  color: red;
  background: pink;
}
</style>
