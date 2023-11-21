<template>
  <div>
    <h2>{{ burger.name }}</h2>
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
  }
}

</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.allergies {
  font-weight: bold;
}
</style>
