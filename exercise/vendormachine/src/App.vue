   
   
   
   
   <!-- Code นี้ เขียน โดย นายพสิษฐ์ ทิวารัตนอังกูร 
        ส่วนของ CSS ส่วนใหญ๋ นำมาจาก W3.CSS ครับ 
        ในส่วนของ Test case นะครับ เบื้องต้น ผ่านตาม ที่ Test case ต้องการครับ
        แต่มี กรณี ถ้าหาก หยอดเงิน มา 105 บาท (โดยมี 10 บาท , 5 บาท)
            แล้ว เลือกสินค้า 13 บาท คงเหลือ 92 บาท (105 บาท - 13 บาท)
            จะไม่สามารถคืนตัง 10 บาท * 9 เหรียญ ที่เหลือได้ครับ T-T 
        -->

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
             <br>
             <a class="w3-button w3-xxlarge w3-black">Would to Refund ?</a>
           </p>

         </div>
       </header>
       <!-- ส่วนของเหรียญ -->
       <div class="w3-container w3-black w3-padding-64 w3-xxlarge" id="coin">
         <div class="w3-content">
           <div class="w3-row"><br>
             <h1 class="w3-center w3-jumbo" style="margin-bottom:64px">Coins</h1>
             <br>
             <!-- เหรียญ 10 -->
             <div class="w3-quarter">
               <p>Coin10</p>
               <img
                 src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcT_wIh0gr7owWGDjM84jCZrZugYRK_aEKRQoJAiCPSHujj-uMbV"
                 alt="coin10" @click="BtInc('coin10')" style="width:45%" class="w3-circle w3-hover-opacity">
             </div>
             <!-- เหรียญ 10 -->
             <div class="w3-quarter">
               <p>Coin5</p>
               <img
                 src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcT_wIh0gr7owWGDjM84jCZrZugYRK_aEKRQoJAiCPSHujj-uMbV"
                 alt="coin5" @click="BtInc('coin5')" style="width:45%" class="w3-circle w3-hover-opacity">
             </div>
             <div class="w3-quarter">
               <!-- เหรียญ 2 -->
               <p>Coin2</p>
               <img
                 src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcT_wIh0gr7owWGDjM84jCZrZugYRK_aEKRQoJAiCPSHujj-uMbV"
                 alt="coin2" @click="BtInc('coin2')" style="width:45%" class="w3-circle w3-hover-opacity">
             </div>
             <!-- เหรียญ 1 -->
             <div class="w3-quarter">
               <p>Coin1</p>
               <img
                 src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcT_wIh0gr7owWGDjM84jCZrZugYRK_aEKRQoJAiCPSHujj-uMbV"
                 alt="coin1" @click="BtInc('coin1')" style="width:45%" class="w3-circle w3-hover-opacity">
             </div>
             <br>
             <div>
               <!--ส้่่วนของ Modal มี 3 แบบ-->
               <!-- แบบ 1 กรณี ทำรายการสำเร็จ-->
               <b-modal ref="my-modal" no-close-on-esc no-close-on-backdrop hide-header-close class="no-close-on-esc"
                 hide-footer title="thank you for your service">
                 <div class="d-block ">
                   <h3>You Got this</h3>
                   <h4>{{productSelect}}</h4>
                   <h3>Your Chages Here</h3>
                   <h4>
                     <li v-for="items in coins" :key="items">
                       {{items}}
                     </li>
                   </h4>
                   <b-button class="mt-3" variant="outline-danger" block @click="reset()">Close Me</b-button>
                 </div>
               </b-modal>
               <!-- แบบ 2 กรณี ไม่มีเงินทอนหรือไม่สามารถทอนได้-->
               <b-modal ref="my-modal1" no-close-on-esc no-close-on-backdrop hide-header-close class="no-close-on-esc"
                 hide-footer title="thank you for your service">
                 <div class="d-block ">
                   <h3>
                     <li>No coins to Change</li>
                     <li>Or no coins type to change</li>
                   </h3>
                   <b-button class="mt-3" variant="outline-danger" block @click="reset()">Close Me</b-button>
                 </div>
               </b-modal>
               <!-- แบบ 3 กรณี refund-->
               <b-modal ref="my-modal2" no-close-on-esc no-close-on-backdrop hide-header-close class="no-close-on-esc"
                 hide-footer title="thank you for your service">
                 <div class="d-block " v-for="item in coins" :key="item">
                   <h3>
                     <h2>Your Change</h2>
                     <li>{{item}}</li>
                     <li></li>
                   </h3>
                   <b-button class="mt-3" variant="outline-danger" block @click="reset()">Close Me</b-button>
                 </div>
               </b-modal>
             </div>
           </div>
           <!--Menu -->

           <div class="w3-content">
             <h1 class="w3-center w3-jumbo" style="margin-bottom:64px">THE MENU</h1>
             <div class="w3-row w3-center w3-border w3-border-dark-grey">
               <div class="w3-col s4 tablink w3-padding-large w3-hover-red w3-red">Soda</div>
             </div>
             <div id="Soda" class="w3-container menu w3-pa  dding-32 w3-white" style="display: block;"
               v-for="(item,index) in info.data.data" :key="index.id">
               <h1><b>{{item.name}}</b>
                 <button class="w3-right w3-tag w3-dark-grey w3-round"
                   :hidden="item.in_stock==false || resultValue<item.price"
                   @click="Run(item.price,item.name)">Buy</button>
               </h1>
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
           coins: [],
           coinsValue: 0,
           productSelect: null,
           amount: 0,
           image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTzNNgo3vK9TypLcxbPzoPABWy04vz9uarbY4fkvr3JTbu8nuVj',
           price: 0.0,
         }
       },
       computed: {
         resultValue() {
           return this.coinsValue
         }
       },
       mounted() {
         axios // ดึงข้อมูล product จากลิ้ง
           .get('https://www.mocky.io/v2/5c77c5b330000051009d64c9')
           .then(response => (this.info = response))

       },
       methods: {
         //------- ฟังชั่น ให้ เป็น one click ------
         Run(price, name) {
           this.productSelect = name
           this.amount = this.coinsValue - price;
           this.coins = this.coins.sort((a, b) => a - b);
           console.log(this.coins)
           this.minCoinsChange(this.coins, this.amount)
         },
         //--------  ฟังชั่นทอนเหรียญ ---------
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
                   if (minChange[k] != undefined) {
                     minChange[i] = minChange[k].concat([coins[j]]);
                   }
                 }
               }
             }
           }
           var result = minChange[amount];
           if (!result) {
             this.coinsValue = this.amount
             this.$refs['my-modal1'].show()
           }else{
             this.coins = result.slice(1)
             console.log(this.coins)
             this.$refs['my-modal'].show()
           }
           
         },
         //-----------เพิ่มเหรียญ -----------------------------
         BtInc(coinType) {
           // เหรียญ 10
           if (coinType == 'coin10') {
             this.coinsValue += 10
             this.coins.push(10);
           }
           // เหรียญ 5
           if (coinType == 'coin5') {
             this.coinsValue += 5
             this.coins.push(5);
           }
           // เหรียญ 2
           if (coinType == 'coin2') {
             this.coinsValue += 2
             this.coins.push(2);
           }
           // เหรียญ 1
           if (coinType == 'coin1') {
             this.coinsValue += 1
             this.coins.push(1);
           }
         },
         //ฟังชั่น สำหรับการคืนค่าครับ (ผมมั่นใจว่ามีวิธีที่ดีกว่านี้)
         reset() {
           //ส่วนของ ซ่อน Modal
           if (!this.$refs['my-modal'].hide()) {
             this.$refs['my-modal'].hide()
           }
           else if (!this.$refs['my-modal1'].hide()) {
             this.$refs['my-modal1'].hide()
           }
           else if (!this.$refs['my-modal2'].hide()) {
             this.$refs['my-modal2'].hide()
           }
           // ส่วนของ ตัวแปร
           this.coins = []
           this.coinsValue = 0
           this.productSelect = null
           this.amount = 0
           this.price = 0.0

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
