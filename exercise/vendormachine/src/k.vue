<template>
<div>
    <button @click="MinimumCoinChange(cointypes)"></button>
</div>
</template>

<script>
  var cointypes = [1, 2, 5, 10],
    coinnames = ["1bath", "2bath", "3bath", "4bath"],
    coinChanger = new MinimumCoinChange(cointypes);
    coinChanger.displayResults(36);
  export default {
    methods: {
      MinimumCoinChange(cointypes) {
        //save the coin types in coins
        this.coins = cointypes;
        this.numCoinTypes = this.coins.length;
      },generateCoins: function(amount) {
        var finalresult = [],
            totalAmount = amount;
        //loop through the coin types. for each type find how many 
        //of the amount you can get 
        for (var i = 0; i < this.numCoinTypes; i++) {
            //first get the value of the coin type
            var currentTypeValue = this.coins[i],
            //count the number of that type of coin. if there are two 25 cents
            //then the count is two
            typeCount = Math.floor(totalAmount / currentTypeValue);
            //push the coin into result
            finalresult.push(typeCount);
            //update the total amount so on the next iteration we can find the right
            //type count
            totalAmount -= (currentTypeValue * typeCount);
        }
        //return the final results
        return finalresult;
    },displayResults: function(amount){
        var results = this.generateCoins(amount);
        console.log(results);
        for(var i = 0; i < results.length; i++) {
            console.log('There are(is) ', results[i], ' ', coinnames[i]);
        }
    },
    }

  }

</script>

<style>

</style>
