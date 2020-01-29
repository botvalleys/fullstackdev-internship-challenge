<template>
  <div id="app">
    <!-- header -->
    <header>
      <!-- Navbar -->
      <nav class="navbar navbar-light bg-dark">
        <a class="navbar-brand" href="#">
          <img src="https://img1.thaipng.com/20171220/gze/twitter-logo-png-5a3a1851372e76.0876249315137567532269680.jpg"
            width="30" height="30" alt="">
        </a>
      </nav>
    </header>
    <!-- /header -->
    <!-- body -->

    <body>
      <!-- container 1  -->
      {{info.data.data}}
      <div class="A-container">
        <img src="../src/images/Vendor.png" alt="img-main" style="max-width:30.8333333%">
        <!-- container 1  -->
      </div>
      <!--button-->
      <div class="bt-1">
        <button type="button" class="btn btns btn-xl btn-outline-warning">Coin 10 !</button>
        <button type="button" class="btn btns btn-xl btn-outline-warning">Coin 5 !</button>
        <button type="button" class="btn btns btn-xl btn-outline-warning">Coin 2 !</button>
        <button type="button" class="btn btns btn-xl btn-outline-warning">Coin 1 !</button>
      </div>
      <!--/button-->
      <!--container 3-->
      <div class="B-container">
        <div class="card " v-for="(item,index) in info.data.data" :key="index" :src="item.image" style="max-height:50%">
          <div class="sub-contanier">
            <img class="card-img-top" :src="item.image" height="200px" width="50%">
            <div class="card-body">
              <h5 class="card-title">{{item.name}}</h5>
              <p class="card-text">ราคา {{item.price}}</p>
              <button class="btn btn-primary" :disabled="item.in_stock !==true">Buy</button>
            </div>
          </div>
        </div>
      </div>
      <!--container 3-->
    </body>
    <!-- /body -->
  </div>


</template>

<script>
  import axios from 'axios';
  export default {
    data() {
      return {
        info: [],
        i: 0,
        sum: 0,
        iResult10: 0,
        iResult5: 0,
        iResult2: 0,
        iResult1: 0,
        price: 15.0,
        coin: {
          coin10: {
            Value: 10,
            CountCoin: 0,
            CountValue: 0,
          },
          coin5: {
            Value: 5,
            CountCoin: 0,
            CountValue: 0,
          },
          coin2: {
            Value: 2,
            CountCoin: 0,
            CountValue: 0,
          },
          coin1: {
            Value: 1,
            CountCoin: 0,
            CountValue: 0,
          },
        },
      }
    },
    computed: {
      resultValue() {
        return ((this.coin.coin10.CountValue + this.coin.coin5.CountValue) +
          (this.coin.coin2.CountValue + this.coin.coin1.CountValue));
      },
      resultCoin: function () {
        return ((this.coin.coin10.CountCoin + this.coin.coin5.CountCoin) +
          (this.coin.coin2.CountCoin + this.coin.coin1.CountCoin));
      },
      resultTotal: function () {
        return this.resultValue - this.price;
      },
    },
    mounted() {
      axios //ดึงข้อมูล product จากลิ้ง
        .get('https://www.mocky.io/v2/5c77c5b330000051009d64c9')
        .then(response => (this.info = response))
    },
    methods: {
      buttInc(coins) { //เพิ่มเหรียญ จากปุ่ม
        if (coins == 'coin10') {
          this.coin.coin10.CountCoin += 1;
          this.coin.coin10.CountValue += 10;
        } else if (coins == 'coin5') {
          this.coin.coin5.CountCoin += 1;
          this.coin.coin5.CountValue += 5;
        } else if (coins == 'coin2') {
          this.coin.coin2.CountCoin += 1;
          this.coin.coin2.CountValue += 2;
        } else if (coins == 'coin1') {
          this.coin.coin1.CountCoin += 1;
          this.coin.coin1.CountValue += 1;
        }

      },
      getTheSelectedOne(number) {
        // then number will be the number
        this.console.log(number)
      },
      refund() { //ฟังชั่น ทอนเงิน
        //ตรวจสอบว่าได้เลือกสินค้าหรือไม่และได้หยอดเหรียญหรือไม่ ----------
        if (this.price > 0 && this.resultValue >= this.price) {
          //ตรวจสอบว่ามีเหรียญ 10 หรือไม่ --------
          if (this.coin.coin10.CountCoin > 0) {
            //loop ตามจำนวนเหรียญที่มีเพื่อเอาไปลบกับราคาสินค้า 
            for (this.i = this.coin.coin10.CountCoin; this.i >= 0; this.i--) {
              //ตรวจสอบว่า ก่อนลูป หรือ หลัง ลูป ยอดเงิน และเหรียญ ยังมีหรือไม่
              if (this.price > 0 && this.coin.coin10.CountCoin > 0) {
                //เอาราคาสินค้ามาลบกับเหรียญที่หักออกไป
                this.price = this.price - 10;
                this.coin.coin10.CountCoin -= 1;
              }
            }
            //ตรวจสอบว่ามีเหรียญ 5 หรือไม่ --------
            if (this.coin.coin5.CountCoin > 0) {
              //loop ตามจำนวนเหรียญที่มีเพื่อเอาไปลบกับราคาสินค้า 
              for (this.i = this.coin.coin5.CountCoin; this.i >= 0; this.i--) {
                //ตรวจสอบว่า ก่อนลูป หรือ หลัง ลูป ยอดเงิน และเหรียญ ยังมีหรือไม่
                if (this.price > 0 && this.coin.coin5.CountCoin > 0) {
                  //เอาราคาสินค้ามาลบกับเหรียญที่หักออกไป
                  this.price = this.price - 5;
                  this.coin.coin5.CountCoin -= 1;

                }
              }
            }
            //ตรวจสอบว่ามีเหรียญ 2 หรือไม่ --------
            if (this.coin.coin2.CountCoin > 0) {
              //loop ตามจำนวนเหรียญที่มีเพื่อเอาไปลบกับราคาสินค้า 
              for (this.i = this.coin.coin2.CountCoin; this.i >= 0; this.i--) {
                //ตรวจสอบว่า ก่อนลูป หรือ หลัง ลูป ยอดเงิน และเหรียญ ยังมีหรือไม่
                if (this.price > 0 && this.coin.coin2.CountCoin > 0) {
                  //เอาราคาสินค้ามาลบกับเหรียญที่หักออกไป
                  this.price = this.price - 2;
                  this.coin.coin5.CountCoin -= 1;

                }
              }
            }
            //ตรวจสอบว่ามีเหรียญ 1 หรือไม่ --------
            if (this.coin.coin1.CountCoin > 0) {
              //loop ตามจำนวนเหรียญที่มีเพื่อเอาไปลบกับราคาสินค้า 
              for (this.i = this.coin.coin1.CountCoin; this.i >= 0; this.i--) {
                //ตรวจสอบว่า ก่อนลูป หรือ หลัง ลูป ยอดเงิน และเหรียญ ยังมีหรือไม่
                if (this.price > 0 && this.coin.coin1.CountCoin > 0) {
                  //เอาราคาสินค้ามาลบกับเหรียญที่หักออกไป
                  this.price = this.price - 1;
                  this.coin.coin5.CountCoin -= 1;

                }
              }
            }
          }
        }
      }
    }
  }
</script>

<style>
  .A-container {
    display: flex;
    justify-content: center;
  }

  .btns {
    display: flex;

  }

  .B-container {
    margin-top: 2rem;
  }

  .btn-xl {
    padding: 18px 70px;
    font-size: 16px;
    border-radius: 102px;
    margin: auto;
  }

  .card {
    float: left;
    max-width: 50%;
  }

  .card-img-top {}
</style>