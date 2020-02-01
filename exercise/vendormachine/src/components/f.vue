<template>
  
</template>

<script>
export default {
methods:{
     makeChange = function(coins) {
  var change, cache = {};
  return change = function(amount) {
    if (!amount) return [];
    if (cache[amount]) return cache[amount].slice(0);
    var min = [], newMin, newAmount;
    coins.forEach(function(coin) {
      if (
        (newAmount = amount - coin) >= 0 &&
        ((newMin = change(newAmount)).length < min.length-1 || !min.length) &&
        (newMin.length || !newAmount)
      )
        min = [coin].concat(newMin);
    });
    return (cache[amount] = min).slice(0);
  }
}
}
}
</script>

<style>

</style>