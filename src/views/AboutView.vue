<template>
  <div class="about">
    <div class="head">
      <div class="head_div">
        <div class="head_icon">
          <img src="../assets/14.webp">
          <img src="../assets/8.webp">
          <img src="../assets/15.webp">
          <img src="../assets/4.webp">
        </div>
        <img class="head_img" src="../assets/1.webp">
        <div class="head_play">
          <b> play</b>
        </div>
      </div>
    </div>
    <div class="spak">
      <div class="spak_box">
        <img src="../assets/2.png">
        <div class="spak_one">
          <h1>Countdown</h1>
          <div class="spak_two">
            <p>TIME TO NEXT PAYOUT...</p>
            <div class="spak_soon">
              Coming Soon
            </div>
          </div>
          <div>
            <ul class="spak_ul">
              <li>Payouts are sent every 7 days</li>
              <li>You must stake for 7 days in order to become eligible to all future payouts-until you unstake</li>
            </ul>
          </div>
          <div class="sp">
            <h1>Your Wallet</h1>
            <div class="sp_box">
              <p>ADDRESS</p>
              <p>BLAST STAKED</p>
              <p>TIER</p>
              <p>ELIGIBLE?</p>
            </div>
            <div class="sp_input">
              <div class="sp_inbox">
                <p>{{maskedAddress  }}</p>
                <img @click="copyAddress" src="../assets/17.png">
              </div>
              <div class="sp_inbox1">
                0
              </div>
            </div>
            <div class="xuanxk">
              <div class="xuanxk_one">
                <div @click="changeTab('tab1')" :class="{ active: activeTab === 'tab1' }">STAKE</div>
                <div @click="changeTab('tab2')" :class="{ active: activeTab === 'tab2' }">UNSTAKE</div>
              </div>
              <h1 class="xuanxk_two">Amount</h1>
              <div class="tab-content">
                <div v-show="activeTab === 'tab1'">
                  <div class="tab_1">
                    <input>
                    <div class="tab_2">
                      <span>Click once and wait 5-10s</span>
                      <div>UNSTAKE</div>
                    </div>
                  </div>
                </div>
                <div v-show="activeTab === 'tab2'">
                  <div class="tab_1">
                    <input>
                    <div class="tab_2">
                      <span>Click once and wait 5-10s</span>
                      <div>STAKE</div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="bi_tu">
                <img src="../assets/16.png">
              </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Web3 from 'web3';

export default {
  data() {
    return {
      activeTab: 'tab1',
      accountAddress: '',
      maskedAddress: '',
      Address:''
    };
  },
  methods: {
    async loginMetamask() {
      if (window.ethereum) {
        try {
          await window.ethereum.request({ method: 'eth_requestAccounts' });
          const web3 = new Web3(window.ethereum);
          const accounts = await web3.eth.getAccounts();
          
          // 获取第一个账户地址
          const address = accounts[0];
          this.Address=address
          console.log(this.Address)
          // 存储账户地址到 this.accountAddress 变量中
          this.accountAddress = address;
          
          // 生成省略号隐藏的地址
          this.maskedAddress = this.generateMaskedAddress(address);
        } catch (error) {
          console.error('连接到 Metamask 失败:', error);
        }
      } else {
        console.error('未检测到 Metamask 插件');
      }
    },
    generateMaskedAddress(address) {
      const start = address.slice(0, 6); // 截取前 6 位
      const end = address.slice(-4); // 截取后 4 位
      const maskedAddress = `${start}...${end}`; // 加上省略号
      
      return maskedAddress;
    },
    copyAddress() {
      const el = document.createElement('textarea');
      el.value = this.accountAddress;
      document.body.appendChild(el);
      el.select();
      document.execCommand('copy');
      document.body.removeChild(el);
      alert('账户地址已复制！');
    },
    
    changeTab(tab) {
      this.activeTab = tab;
    }
  }
};
</script>
<style>
.head {
  width: 100%;
  height: 6rem;
  background-color: #190e36;
  display: flex;
  justify-content: center;
}

.head_icon {
  width: 14%;
  height: 100%;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.head_icon>img {
  width: 42px;
  height: 42px;
}

.head_div {
  width: 80%;
  /* border: 1px red solid; */
  display: flex;
  justify-content: space-between;
  align-items: center;

}

.head_img {
  width: 34px;
  height: 43px;
}

.head_play {
  /* width: 120px; */
  width: 60px;
  height: 30px;
  /* color: white; */
  border-radius: 10px;
  box-shadow: -3px 1px 18px -1px rgba(199, 50, 50, .71) !important;
  color: #000;
  font-size: larger;
  font-weight: bolder;
  padding: 3px 25px;
  text-align: center !important;
  /* width: 100px; */
  line-height: 30px;
  background-color: rgb(255, 229, 54);
}

.spak {
  align-items: center;
  background-color: #210e53;
  background-position: 50%;
  background-size: cover;
  display: flex;
  min-height: 100vh;
  justify-content: space-evenly;
}

.spak_box {
  width: 60%;
  height: 120rem;
  /* border: 1px red solid; */
  font-weight: 900;
  display: flex;
  flex-direction: column;
    align-items: center;
}

.spak_box>img {
  width: 60rem;
  margin-top: 10vh;
}

.spak_one>h1 {
  color: white;
  /* font-weight: 900; */
  padding: 1.5rem 0;
}

.spak_two {
  width: 60rem;
  height: 12rem;
  background-color: #322068;
  border-radius: 13px;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.spak_two>p {
  width: 100%;
  height: 2.5rem;
  font-size: 20px;
  line-height: 2.5rem;
  color: white;
  font-family: 800;
  /* border:1px red solid;   */
}

.spak_soon {
  display: flex;
  width: 90%;
  height: 5rem;
  border-radius: 10px;
  background-color: rgb(54, 38, 100);
  font-size: 4rem;
  color: white;
  justify-content: center;
  align-items: center;
}

.spak_ul {
  width: 58rem;
  height: 9rem;
  background-color: #322068;
  margin-top: 2rem;
  border-radius: 10px;
  display: flex;
  color: white;
  flex-direction: column
}

.spak_ul li {
  padding-top: 1rem;
  font-size: 1.4rem;
  line-height: 1.5rem;
  font-weight: 900;
}

.sp {
  width: 60rem;
  height: 60rem;
  /* border: 1px red solid; */
}

.sp>h1 {
  color: white;
  margin-top: 2rem;
  margin-left: 1rem
}

.sp_box {
  width: 95%;
  display: flex;
  justify-content: space-between;
  margin: 0 auto;
  color: rgb(125, 113, 153)
}

.sp_input {
  width: 100%;
  height: 4rem;
  /* border: 1px red solid; */
  display: flex;
  align-items: center;
}

.sp_inbox {
  width: 16rem;
  height: 2.5rem;
  display: flex;
  align-items: center;
  color: white;
  background-color: #2c1c5d;
  border-radius: 10px;
}

.sp_inbox1 {
  width: 18rem;
  height: 2.5rem;
  display: flex;
  align-items: center;
  color: white;
  background-color: #2c1c5d;
  margin-left: 2rem;
  border-radius: 10px;
  padding-left: 1rem;
}

.xuanxk {
  width: 100%;
  height: 18rem;
  /* border: 1px red solid; */
  display: flex;
  flex-direction: column;
  background-color: #2c1c5d;

}

.xuanxk_one {
  display: flex;
}

.xuanxk_one>div {
  background-color: #201051;
  color: #7d7199;
  border: 1px #7d7199 solid;
  text-align: center;
  line-height: 3rem;
  width: 8rem;
  height: 3rem;
  color: white;
  margin-left: 1rem;
  margin-top: 1rem;
  border-radius: 10px;
  background-color: rgb(65, 51, 109);

  /* border-bottom-color: rgb(255, 255, 255); */
}

.xuanxk_two {
  color: #7d7199;
  margin-left: 1rem;
}

.xuanxk_one>div:hover {
  background-color: #2c1c5d;
  ;
  opacity: 0.6;
}

.tab_1 {
  width: 95%;
  height: 4rem;
  /* border: none; */
  margin: 0 auto;
  display: flex;
  align-items: center
}

.tab_1 input {
  border: none;
  border-radius: 10px;
  box-shadow: none;
  width: 70%;
  height: 3rem;
  background-color: rgb(24, 10, 59);
}
.sp_inbox >img{
    width: 2rem;
    height: 2rem;
}
.tab_2 {
  width: 40%;
  height: 4rem;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  /* justify-content: space-around; */
  position: relative;
}

.tab_2 span {
  position: absolute;
  top: -45%;
}

.tab_2 div {
  width: 14rem;
  height: 3rem;
  border-radius: 15px;
  background-color: #fce45c;
  text-align: center;
  line-height: 3rem;
  text-align: center !important;
  text-shadow: 2px 3px 2px #000;
  font-size: 27px;
  font-weight: bolder !important;
  box-shadow: 0 5px 0 rgba(225, 228, 47, .2) !important;
}
.bi_tu{
  width: 100%;
  height: 23rem;
  /* border: 1px saddlebrown solid;   */
  background-color: rgb(54, 38, 101);
  margin-top: 2rem;
  border-radius: 10px;
  padding-top: 2rem;
  padding-left: 2rem;
}
.sp_inbox p{
  width: 13rem;
  height: 100%;
}
.bi_tu>img{
    width:80%;
    height: auto;
}
@media screen and (max-width: 600px) {
  .head_div{
    width: 90%;
  }
  .head_icon{
    width: 46%;
  }
  .spak_box{
    width: 80%;
  }
  .spak_box>img {
      width: 19rem;
  }
  .spak_one>h1 {
    text-align: center;
  }
  .spak_two{
    width: 19rem;
  }
  .spak_soon{
    font-size: 2rem;
  }
  .spak_ul{
    width: 17rem;
    height: 19rem;
    justify-content: space-around;
  }
  .sp>h1{
    font-size: 3rem;
  }
  .sp_box{
    width:5rem;
      margin-left: 1rem;
      font-size: 0.9rem;
  }
  .sp_input {
    width: 94%;
  }
  .sp{
    width: 21rem;
  }
  .xuanxk_one{  
    flex-direction: column;
  }
  .xuanxk{
    width: 93%;
    height: 24rem;
  }
  .tab_1{
    flex-direction: column;
    height: 10rem;
    justify-content: space-between;
  } 
  .tab_1 input{
    width: 90%;
  }
  .tab_2 span{
    width:10rem;
    display: block;
    top: -55%;
    text-align: center;
  }
  .bi_tu{
    width: 83%;
    height: 9rem;
  }
  .unstake_btn {
        margin-top: 1rem;
        margin-left: 0;
  }
  .bi_tu>img {
    width: 90%;
  }
} 
  </style>
