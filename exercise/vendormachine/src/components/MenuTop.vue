<template>
  <div class="w3-top">
      <div class="w3-bar w3-xlarge w3-black w3-opacity w3-hover-opacity-off" id="myNavbar">
        <a href="#" class="w3-bar-item w3-button">HOME</a> <button>Your Coins : {{SValue}}</button>
      </div>
    </div>
</template>

<script>
export default {
    name:'MenuTop',
    props:['SValue',],
    methods:{
        
    }
}
</script>

<style>

</style>