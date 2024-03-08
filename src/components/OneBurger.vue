<template>
  <div>
    <h2>{{ burger.name }}</h2>
    Amount ordered: {{ amountOrdered }}
    <img v-bind:src="burger.img" style="width: 200px;">
    <ul class="allergies">
      <li>{{ burger.kCal }} kcal</li>
      <li v-if="burger.gluten">
        Gluten
      </li>
      <li v-if="burger.lactose">
        Lactose
      </li>
    </ul>
    <button v-on:click="addBurger">
      <img src="img/submit-button-png-25802.png" style="width: 100px">
    </button>
    <button v-on:click="subtractBurger">
      <img src="img/submit-button-png-25802.png" style="width: 100px">
    </button>
  </div>
</template>
  
<script>
export default {
  name: 'OneBurger',
  props: {
    burger: Object
  },
  data: function () {
    return {
      amountOrdered: 0
    }
  },
  methods: {
    addBurger: function () {
      this.amountOrdered += 1;
      this.$emit('burgerOrder', { name: this.burger.name, amount: this.amountOrdered });
    },
    subtractBurger: function () {
      if (this.amountOrdered > 0) {
        this.amountOrdered -= 1;
        this.$emit('burgerOrder', { name: this.burger.name, amount: this.amountOrdered });
      }
    }
  }
}
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.allergies {
  font-weight: bold;
}
</style>
