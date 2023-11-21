<template>
  <body>
    <header>
      <h1 style="position:absolute; color:white; top: 50%; left: 50%; transform: translate(-50%, -50%);">Welcome to
        Bird Burgers!</h1>
      <img src="img/burger_header.jpeg" id="burger_header">
    </header>

    <section id="burgers">
      <h2>We make the only bird burgers in town!</h2>
      <p>Choose bird borger:</p>

      <div class="wrapper">
        <Burger v-for="burger in burgers" v-bind:burger="burger" v-bind:key="burger.name" />
      </div>
    </section>

    <section id="order_information">
      <h3>Who are you?</h3>
      <p>Provide information for delivery:</p>

      <form>
        <p>
          <label for="fullname">Full name</label><br>
          <input type="text" id="fullname" v-model="fn" required="required" placeholder="First- and Last name">
        </p>
        <p>
          <label for="email">E-mail</label><br>
          <input type="text" id="email" v-model="em" placeholder="E-mail address">
        </p>
        <p>
          <label for="street">Street</label><br>
          <input type="text" id="street" v-model="st" required="required" placeholder="Street name">
        </p>
        <p>
          <label for="house">House number</label><br>
          <input type="text" id="housenumber" v-model="hn" required="required" placeholder="House number">
        </p>

        <p>
          <label for="payment_method">Payment method</label><br>
          <select id="payment_method" v-model="pm">
            <option>Card</option>
            <option>Swish</option>
            <option>Monero</option>
            <option selected="selected">OSRS gp</option>
          </select>
        </p>

        <p>
          <label for="male">Male</label>
          <input type="radio" id="gender" v-model="gender" value="male">

          <label for="female">Female</label>
          <input type="radio" id="gender" v-model="gender" value="female">

          <label for="other">Other</label>
          <input checked type="radio" id="gender" v-model="gender" value="other">
        </p>
      </form>

      <button v-on:click="orderButtonClick">
        <img src="img/submit-button-png-25802.png" style="width: 100px">
      </button>
    </section>

    <hr>
    <footer>
      <div class="footer-content">
        <p>&copy; Bird Burger Company</p>
        <p>Contact us at <a href="mailto:contact@fakeburger.com">contact@birdburger.com</a></p>
      </div>
    </footer>

  </body>
</template>

<script>
import Burger from '../components/OneBurger.vue'
import io from 'socket.io-client'
import menu from '../assets/menu.json'

const socket = io();
const myBurgers = menu; // menu is imported from menu.json

/* function MenuItem(name, kCal, gluten, lactose, img) {
  this.name = name;
  this.kCal = kCal;
  this.gluten = gluten;
  this.lactose = lactose;
  this.img = img;
} */

/* const myBurgers = [
  new MenuItem('Borb burger', 800, true, true, '../../img/burger1.jpeg'),
  new MenuItem('Crazy burger', 2500, true, true, '../../img/crazy_borger.png'),
  new MenuItem('Mmmm burger', 500, true, false, '../../img/sus_borger.png')] */

export default {
  name: 'HomeView',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: myBurgers,
      /*       fn: "",
            em: "",
            st: "",
            hn: "", */
      pm: "OSRS gp",
      gender: "Other"
    }
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random() * 100000);
    },
    orderButtonClick() {
      console.log(
        "Order button clicked",
        this.fn,
        this.em,
        this.st,
        this.hn,
        this.pm,
        this.gender
      )
    },
    addOrder: function (event) {
      var offset = {
        x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top
      };
      socket.emit("addOrder", {
        orderId: this.getOrderNumber(),
        details: {
          x: event.clientX - 10 - offset.x,
          y: event.clientY - 10 - offset.y
        },
        orderItems: ["Beans", "Curry"]
      }
      );
    }
  }
}
</script>

<style>
body {
  font-family: Arial;
  font-size: 1.2em;
}

#burgers {
  background-color: black;
  color: white;
  border: white 2px dotted;
}

button:hover {
  background-color: lawngreen;
  color: white;
  cursor: pointer;
}

section {
  margin: 20px;
  border: black 2px dotted;
  padding: 20px;
}

button {
  margin: 10px;
}

header {
  position: relative;
  margin: 20px;
  height: 300px;
  overflow: hidden;
}

#burger_header {
  opacity: 0.;
  width: auto;
}

.wrapper {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

#map {
  width: 300px;
  height: 300px;
  background-color: red;
}
</style>