<template>

  <body>
    <!-- Navbar อยู่ด้านบนสุดเสมอ -->
    <div class="w3-top">
      <div class="w3-bar w3-xlarge w3-black w3-opacity w3-hover-opacity-off" id="myNavbar">
        <a href="#" class="w3-bar-item w3-button">HOME</a> <button>Your Coins : {{resultValue}}</button>
        <button>Your Price : {{this.price}}</button>
        <button @click="resultValue()">Your new : {{this.price}}</button>
        <button @click="calculated()">Your</button>
      </div>
    </div>

    <!-- เอาภาพมาเป็นพื้นหลัง -->
    <header class="bgimg" id="home" v-bind:style="{ backgroundImage: 'url(' + image + ')' }">
      <div class="w3-display-middle w3-center">
        <span class="w3-text-white w3-hide-small" style="font-size:100px">Vendor<br>Machine</span>
        <span class="w3-text-white w3-hide-large w3-hide-medium" style="font-size:60px"><b>Vendor<br>Machine</b></span>
        <p><a href="#coin" class="w3-button w3-xxlarge w3-black">Put the coins</a></p>
      </div>
    </header>

    <!-- ส่วนของเหรียญ -->
    <div class="w3-container w3-black w3-padding-64 w3-xxlarge" id="coin">
      <div class="w3-content">
        <div class="w3-row"><br>
          <h1 class="w3-center w3-jumbo" style="margin-bottom:64px">Coins</h1>
          <br>
          <div class="w3-quarter">
            <img src="https://f0.pngfuel.com/png/579/386/coin-gold-medal-material-coin-png-clip-art.png"
              @click="buttInc('coin10')" alt="coin10" style="width:45%" class="w3-circle w3-hover-opacity">
            <p>Coin10</p>
          </div>

          <div class="w3-quarter">
            <img src="https://f0.pngfuel.com/png/579/386/coin-gold-medal-material-coin-png-clip-art.png"
              @click="buttInc('coin5')" alt="coin5" style="width:45%" class="w3-circle w3-hover-opacity">

            <p>Coin5</p>
          </div>

          <div class="w3-quarter">
            <img src="https://f0.pngfuel.com/png/579/386/coin-gold-medal-material-coin-png-clip-art.png"
              @click="buttInc('coin2')" alt="coin2" style="width:45%" class="w3-circle w3-hover-opacity">

            <p>Coin2</p>
          </div>

          <div class="w3-quarter">
            <img src="https://f0.pngfuel.com/png/579/386/coin-gold-medal-material-coin-png-clip-art.png"
              @click="buttInc('coin1')" alt="coin1" style="width:45%" class="w3-circle w3-hover-opacity">

            <p>Coin1</p>
          </div>
          <br>
        </div>
        <!--Menu -->
        <div class="w3-content">

          <h1 class="w3-center w3-jumbo" style="margin-bottom:64px">THE MENU</h1>
          <div class="w3-row w3-center w3-border w3-border-dark-grey">
            <a href="javascript:void(0)" onclick="openMenu(event, 'Pizza');" id="myLink">
              <div class="w3-col s4 tablink w3-padding-large w3-hover-red w3-red">Pizza</div>
            </a>
          </div>

          <div id="Pizza" class="w3-container menu w3-pa  dding-32 w3-white" style="display: block;"
            v-for="(item,index) in info.data.data" :key="index.id">
            <h1><b>{{item.name}}</b>
              <button class="w3-right w3-tag w3-dark-grey w3-round"
                :disabled="resultValue === 0 || resultValue < item.price || item.in_stock != true"
                @click="getValue(item.price)">Buy</button></h1>
                <button class="w3-right w3-tag w3-dark-grey w3-round"
                @click="calculated()">Buy</button>
            <p class="w3-text-grey">Price : {{item.price}} Bath</p>
            <p class="w3-text-grey">in_stock : {{item.in_stock}} </p>
            <img :src="item.image" alt="coin1" style="width:30%" class="w3-circle w3-hover-opacity">
            <hr>
          </div><br>

        </div>
      </div>

    </div>
    <!-- Footer -->
    <footer class="w3-center w3-black w3-padding-48 w3-xxlarge">
      <p>Coding by <a href="https://www.facebook.com/Botvalleys" title="W3.CSS" target="_blank"
          class="w3-hover-text-green">Pasit.tiwa</a></p>
      <p>Thanks for template by <a href="https://www.w3schools.com/w3css/default.asp" title="W3.CSS" target="_blank"
          class="w3-hover-text-green">w3.css</a></p>
    </footer>
  </body>


</template>

<script>
  import axios from 'axios'
  export default {
    props: [

    ],
    data() {
      return {
        image: "https://www.cargill.com/image/1432076966914/hero-carborated-soft-drinks.jpg",
        info: [],
        i: 0,
        j: 0,
        componentKey: 0,
        sum: 0,
        iprice:0,
        iResult10: 0,
        iResult5: 0,
        iResult2: 0,
        iResult1: 0,
        price: 0.0,
        coin: {
          coin10: {
            Value: 10,
            CountCoin: 0,
            CountValue: 0
          },
          coin5: {
            Value: 5,
            CountCoin: 0,
            CountValue: 0
          },
          coin2: {
            Value: 2,
            CountCoin: 0,
            CountValue: 0
          },
          coin1: {
            Value: 1,
            CountCoin: 0,
            CountValue: 0
          }
        }
      }
    },
    computed: {
      resultValue() {
        return ((this.coin.coin10.CountCoin * 10) + (this.coin.coin5.CountCoin * 5) +
          (this.coin.coin2.CountCoin * 2) + (this.coin.coin1.CountCoin * 1))
      }
    },
    mounted() {
      axios // ดึงข้อมูล product จากลิ้ง
        .get('https://www.mocky.io/v2/5c77c5b330000051009d64c9')
        .then(response => (this.info = response))
    },
    methods: {
      getValue(val) {
        this.price = val;
      },
      buttInc(coins) { // เพิ่มเหรียญ จากปุ่ม
        if (coins === 'coin10') {
          this.coin.coin10.CountCoin += 1
          this.coin.coin10.CountValue += 10
        } else if (coins === 'coin5') {
          this.coin.coin5.CountCoin += 1
          this.coin.coin5.CountValue += 5
        } else if (coins === 'coin2') {
          this.coin.coin2.CountCoin += 1
          this.coin.coin2.CountValue += 2
        } else if (coins === 'coin1') {
          this.coin.coin1.CountCoin += 1
          this.coin.coin1.CountValue += 10

        }
      },
      calculated() {
       if (this.price > 0 && this.resultValue > 0) {
          // ตรวจสอบว่ามีเหรียญ 10 หรือไม่ --------
          if (this.coin.coin10.CountCoin > 0) {
            // loop ตามจำนวนเหรียญที่มีเพื่อเอาไปลบกับราคาสินค้า
            for (this.i = this.coin.coin10.CountCoin; this.i >= 0; this.i--) {
               this.iprice = this.price - 10
              // ตรวจสอบว่า ก่อนลูป หรือ หลัง ลูป ยอดเงิน และเหรียญ ยังมีหรือไม่
              if (this.iprice >=  0) {
                // เอาราคาสินค้ามาลบกับเหรียญที่หักออกไป
                this.price = this.price - 10
                this.coin.coin10.CountCoin -= 1
              }
            }
            // ตรวจสอบว่ามีเหรียญ 5 หรือไม่ --------
            if (this.coin.coin5.CountCoin > 0) {
              // loop ตามจำนวนเหรียญที่มีเพื่อเอาไปลบกับราคาสินค้า
              for (this.i = this.coin.coin5.CountCoin; this.i >= 0; this.i--) {
                  this.iprice = this.price - 5
                // ตรวจสอบว่า ก่อนลูป หรือ หลัง ลูป ยอดเงิน และเหรียญ ยังมีหรือไม่
                if (this.iprice >= 0) {
                  // เอาราคาสินค้ามาลบกับเหรียญที่หักออกไป
                  this.price = this.price - 5
                  this.coin.coin5.CountCoin -= 1
                }
              }  
            }
            // ตรวจสอบว่ามีเหรียญ 2 หรือไม่ --------
            if (this.coin.coin2.CountCoin > 0) {
              // loop ตามจำนวนเหรียญที่มีเพื่อเอาไปลบกับราคาสินค้า
              for (this.i = this.coin.coin2.CountCoin; this.i >= 0; this.i--) {
                this.iprice = this.price - 2
                // ตรวจสอบว่า ก่อนลูป หรือ หลัง ลูป ยอดเงิน และเหรียญ ยังมีหรือไม่
                if (this.iprice >= 0 ) {
                  // เอาราคาสินค้ามาลบกับเหรียญที่หักออกไป
                  this.price = this.price - 2
                  this.coin.coin2.CountCoin -= 1
                }
              }
            }
            // ตรวจสอบว่ามีเหรียญ 1 หรือไม่ --------
            if (this.coin.coin1.CountCoin > 0) {
              // loop ตามจำนวนเหรียญที่มีเพื่อเอาไปลบกับราคาสินค้า
              for (this.i = this.coin.coin1.CountCoin; this.i >= 0; this.i--) {
                this.iprice = this.price - 1
                // ตรวจสอบว่า ก่อนลูป หรือ หลัง ลูป ยอดเงิน และเหรียญ ยังมีหรือไม่
                if (this.iprice >= 0) {
                  // เอราคาสินค้ามาลบกับเหรียญที่หักออกไป
                  this.price = this.price - 1
                  this.coin.coin1.CountCoin -= 1
                }
              }
            }
          }
            this.resultValue();
        } if(this.price > 0 && this.resultValue === 0){
          alert("หยอดตัง")
      }
    }
    }
  }

</script>

<style>
  @import "https://www.w3schools.com/w3css/4/w3.css";
  @import "https://fonts.googleapis.com/css?family=Amatic+SC";

  body,
  html {
    height: 100%
  }

  body,
  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    font-family: "Amatic SC", sans-serif
  }

  .menu {
    display: none
  }

  .bgimg {
    min-height: 90%;
    background-repeat: no-repeat;
    background-size: cover;
  }

</style>
