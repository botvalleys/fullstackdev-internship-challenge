  <template>

    <body>
      <!-- Navbar อยู่ด้านบนสุดเสมอ -->
      <MenuTop :SValue="coinsValue" />

      <!-- เอาภาพมาเป็นพื้นหลัง -->
      <header class="bgimg" id="home" v-bind:style="{ backgroundImage: 'url(' + image + ')' }">
        <div class="w3-display-middle w3-center">
          <span class="w3-text-white w3-hide-small" style="font-size:100px">Vendor<br>Machine</span>
          <span class="w3-text-white w3-hide-large w3-hide-medium"
            style="font-size:60px"><b>Vendor<br>Machine</b></span>
          <p>
            <a href="#coin" class="w3-button w3-xxlarge w3-black">Put the coins</a>
          </p>
          <p>
            <button @click="minCoinsChange(coins,amount)" class="w3-button w3-xxlarge w3-black">Puts the coins</button>
            <button  class="w3-button w3-xxlarge w3-black">Pcoinsuts the </button>
          </p>
        </div>
      </header>
      <!-- ส่วนของเหรียญ -->
      <div class="w3-container w3-black w3-padding-64 w3-xxlarge" id="coin">
        <div class="w3-content">
          <div class="w3-row"><br>
            <h1 class="w3-center w3-jumbo" style="margin-bottom:64px">Coins</h1>
            <br>

            <div class="w3-quarter">
              <img src="https://f0.pngfuel.com/png/579/386/coin-gold-medal-material-coin-png-clip-art.png" alt="coin10"
                @click="BtInc('coin10')"
                style="width:45%" class="w3-circle w3-hover-opacity">
              <p>Coin10</p>
            </div>
            <div class="w3-quarter">
              <img src="https://f0.pngfuel.com/png/579/386/coin-gold-medal-material-coin-png-clip-art.png" alt="coin5"
                @click="BtInc('coin5')"  
                style="width:45%" class="w3-circle w3-hover-opacity">
              <p>Coin5</p>
            </div>
            <div class="w3-quarter">
              <img src="https://f0.pngfuel.com/png/579/386/coin-gold-medal-material-coin-png-clip-art.png" alt="coin2"
                @click="BtInc('coin2')"
                style="width:45%" class="w3-circle w3-hover-opacity">
              <p>Coin2</p>
            </div>
            <div class="w3-quarter">
              <img src="https://f0.pngfuel.com/png/579/386/coin-gold-medal-material-coin-png-clip-art.png" alt="coin1"
                @click="BtInc('coin1')"
                style="width:45%" class="w3-circle w3-hover-opacity">
              <p>Coin1</p>
            </div>
            <br>

          </div>
          <!--Menu -->

          <div class="w3-content">
            <h1 class="w3-center w3-jumbo" style="margin-bottom:64px">THE MENU</h1>
            <div class="w3-row w3-center w3-border w3-border-dark-grey">
              <div class="w3-col s4 tablink w3-padding-large w3-hover-red w3-red">Soda</div>
            </div>
            <div id="Pizza" class="w3-container menu w3-pa  dding-32 w3-white" style="display: block;"
              v-for="(item,index) in info.data.data" :key="index.id">
              <h1><b>{{item.name}}</b>
                <button class="w3-right w3-tag w3-dark-grey w3-round" @click="Run(item.price)">Buy</button></h1>
              <p class="w3-text-grey">Price : {{item.price}} Bath</p>
              <p class="w3-text-grey">in_stock : {{item.in_stock}} </p>
              <img :src="item.image" alt="coin1" style="width:30%" class="w3-circle w3-hover-opacity">
              <hr>
            </div><br>
          </div>
        </div>

      </div>
      <!-- Footer -->
      <Footer />
    </body>



  </template>

  <script>
    import MenuTop from './components/MenuTop'
    import Footer from './components/Footer'
    import axios from 'axios'
    export default {
      components: {
        MenuTop,
        Footer,
      },
      data() {
        return {
          info: [],
          coins: [15,10,2,1,10,10,10,5,5,5,],
          coinsValue:0,
          amount: 14,
          image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTzNNgo3vK9TypLcxbPzoPABWy04vz9uarbY4fkvr3JTbu8nuVj',
          price: 0.0,
        }
      },
      computed: {
          resultValue(){
            return this.coinsValue
          }
      },
      mounted() {
        axios // ดึงข้อมูล product จากลิ้ง
          .get('https://www.mocky.io/v2/5c77c5b330000051009d64c9')
          .then(response => (this.info = response))
      },
      methods: {
        Run(price) {
          this.amount = this.coinsValue - price;
          this.coins = this.coins.sort((a, b) => a - b);
          console.log(this.coins)
          this. minCoinsChange(this.coins, this.amount)
          
        },
        minCoinsChange(coins, amount) {
          var minChange = [
            [0]
          ];
          if (coins.indexOf(amount) >= 0) {
            return [amount];
          }
          for (var i = 1; i <= amount; i += 1) {
            for (var j = 0; j < coins.length && coins[j] <= amount; j += 1) {
              for (var k = 0; k < minChange.length; k += 1) {
                if (k + coins[j] === i) {
                  if(minChange[k]!= undefined){
                  minChange[i] = minChange[k].concat([coins[j]]);
                }
                }
              }
            }
          }
          var result = minChange[amount];
          if (!result) {
            alert("ยอมแล้วจ้า")
          }
          console.log('last',result)
        },BtInc(coinType){
          if(coinType=='coin10'){
          this.coinsValue  +=10
          }
          if(coinType=='coin5'){
          this.coinsValue  +=5
          }
          if(coinType=='coin2'){
          this.coinsValue  +=2
          }
          if(coinType=='coin1'){
          this.coinsValue  +=1
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
