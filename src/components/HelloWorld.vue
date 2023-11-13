<template>
  <div class="hello">
    <div class="box">
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
      <div class="center">
        <div class="center_nr">
          <img src="../assets/2.png">
          <p style="font-weight: 600;"><span style="color:rgb(255, 229, 54) ;"><b>75%</b></span> of the total revenue from the <span style="text-decoration: underline;"> entire</span>  Blasters
            ecosystem is distributed to $BLAST stakers. Stake now to
            claim your share</p>
          <div  @click="connectMetamask"  class="connect">
            CONNECT
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex';
import Web3 from 'web3';
export default {
  
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods:{

    async connectMetamask() {
  
      if (window.ethereum) {
        try {
          // 请求用户授权连接到 Metamask
          await window.ethereum.request({ method: 'eth_requestAccounts' });
          const web3 = new Web3(window.ethereum);

          // 获取当前连接的以太坊账户列表
          const accounts = await web3.eth.getAccounts();
          console.log('当前账户列表:', accounts);
          main()
          // 执行其他与Metamask交互的操作...
          this.$router.push('/about');
        
        } catch (error) {
          console.error('连接到 Metamask 失败:', error);
        }
      } else {
        console.error('未检测到 Metamask 插件');
      }
    },
    // to(){
    //   
    // }
  }
}
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
  width:60px;
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

.center {
  align-items: center;
  background-color: #210e53;
  background-position: 50%;
  background-size: cover;
  display: flex;
  min-height: 100vh;
  justify-content: space-evenly;
}

.center_nr {
  width: 80%;
  height: 40rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20vh;
  /* justify-content: space-around; */
}

.center_nr>img {
  width: 60rem;
}

.center_nr p {
  font-size: 29px;
  color: white;
  width: 65%;
  height: 5rem;
  text-align: center;
}

.connect {
  width: 100px;
  height: 30px;
  text-align: center;
  line-height: 30px;
  background-color: #7752f0;
  border-radius: 10px;
  color: #fff;
  font-size: large;
  font-weight: bolder !important;
  padding: 5px 13px;
  text-shadow: 2px 2px #000;
  transition: .2s ease-in;
}
.connect:hover{
  background-color:rgb(255, 229, 54);
  color: #7752f0;
}
@media screen and (max-width: 768px) {
    .center_nr >img{
      width: 21rem;
    }
    .center_nr p{
      width: 100%;
      text-align: center;
      height: 17rem;
    }
    .head_icon {
      width: 50%
    }
    .head_div {
      width: 95%;
    }
}
</style>
