<template>
  <div id="mainrole">
    <div v-show="0 ==this.start" @click="gameStart()" id="start"></div>
    <div v-show="1 ==this.restart" @click="gameStart()" id="restart"></div>
    <div class="mainrole">
      <div id="enemy" class="enemybox"></div>
      <div id="player" class="player"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainRole',
  data() {
    return {
      start: 0,
      restart: 0,
      enemynum: -2,
    }
  },
  created() {
    var _this = this;

    //节流用于 space跳跃
    function throttle(func, wait) {
      let previous = 0;
      return function() {
        let now = Date.now();
        let context = this;
        let args = arguments;
        if (now - previous > wait) {
          func.apply(context, args);
          previous = now;
        }
      }
    }

    //如果是空格键则触发跳跃方法
    function pressdown() {
      if (-2 == _this.enemynum){
        return
      }
      if (-1 == _this.enemynum) {
        document.getElementById("player").style.animation = "playerhurt .6s infinite";
        return
      }
      let key = window.event.keyCode;
      if (32 == key) {
        _this.jump()
      }
    }

      //监听按键
      document.onkeydown = throttle(pressdown, 800)
  },
  
  watch: {
    //随机时间生成一个敌人
    enemynum: function () {
      if(-1 == this.enemynum) {
        return
      }
        let timedelay = Math.floor(Math.random()*3+3)*1000
      setTimeout(this.createEnemy,timedelay);
    }
  },

  methods: {
    //随机敌人 
    createEnemy() {
      //let e0 = document.getElementById('player').getBoundingClientRect();  //敌人单位参照
      if (-1 == this.enemynum) {
        return
      }
      let cenemy = document.createElement("div");
      let enemyx = 'enemy' + this.enemynum;
      if (!document.getElementById(enemyx)) {
        cenemy.setAttribute('id',enemyx);
        this.enemynum += 1;
      }
      cenemy.setAttribute('class', 'enemy1 enemy1t');
      let target = document.getElementById('enemy');
      target.appendChild(cenemy);  //添加敌人

      let targetc = document.getElementById(enemyx);
      
      setTimeout(function(){
        
        target.removeChild(targetc); //清除敌人
        },11000)
    },
    //开始函数
    gameStart() {
      this.restart = 0;
      this.start = 1;
      let _this = this;

      this.casestart();

      //this.createEnemy();//创建敌人
      setTimeout(function() {
        window['sI0'] = setInterval(_this.hitControl,30);
      },9000);
    },
    //碰撞事件控制
    hitControl() {
      let eob = document.getElementsByClassName("enemy1 enemy1t");
      if(this.hitTest(eob[0])) {  
        this.gameover(eob);
      }
    },
    //敌人碰撞检测
    hitTest(enemyob) {
      //console.log(enemyob)
      let enemyp = enemyob.getBoundingClientRect(),
          playerp = document.getElementById('player').getBoundingClientRect();

          //以左上角为（0，0）
      let etop = enemyp.top,    //敌人四周
        //  ebottom = enemyp.bottom,
          eleft = enemyp.left,
          eright = enemyp.right,
        //  ptop = playerp.top, //玩家四周
          pbottom = playerp.bottom, 
          pleft = playerp.left*1.1,
          pright = playerp.right*0.9;
      if(eleft < pright && eright > pleft && etop < pbottom) {
        return true
      }  
    },

    //玩家跳跃
    jump() {
      if(-1 == this.enemynum){
        return
      }
      document.getElementById("player").style.animation = "jumpup .4s cubic-bezier(0,0.6,0.6,1)";
      setTimeout(function(){
        document.getElementById("player").style.animation = "jumpdown .4s cubic-bezier(0.6,0,1,0.6)"
        },400);
      setTimeout(function(){
        document.getElementById("player").style.animation = "playerrun .6s infinite"
        },800);
      if(-1 == this.enemynum){
        document.getElementById("player").style.animation = "playerhurt .6s infinite";
      }
    },
    casestart() {
      document.getElementById("enemy").innerHTML = "";
      this.enemynum = 0; 
      document.getElementById("player").style.animation = "playerrun .6s infinite";//启动角色
      document.getElementById("ground").style.animationPlayState = "running"; //启动地板
      document.getElementById("groundrp").style.animationPlayState = "running";
      document.getElementById("groundrp2").style.animationPlayState = "running";
      document.getElementById("groundrp3").style.animationPlayState = "running";
      document.getElementById("groundrp4").style.animationPlayState = "running";
    },
    gameover(eob) {
      this.enemynum = -1;
      clearInterval(window.sI0);
      document.getElementById("player").style.animation = "playerhurt .6s infinite";//角色受伤
      setTimeout(function() {
        for (let i = 0; i<eob.length; i++) {
          eob[i].style.animationPlayState = "paused";
        } 
        document.getElementById("ground").style.animationPlayState = "paused"; //停止地板
        document.getElementById("groundrp").style.animationPlayState = "paused";
        document.getElementById("groundrp2").style.animationPlayState = "paused";
        document.getElementById("groundrp3").style.animationPlayState = "paused";
        document.getElementById("groundrp4").style.animationPlayState = "paused";
        document.getElementById("player").style.animation = "playerhurt .6s infinite";
      },100);
      this.restart = 1;
    },
    cthrottle(func, wait) {
      let previous = 0;
      return function() {
        let now = Date.now();
        let context = this;
        let args = arguments;
        if (now - previous > wait) {
          func.apply(context, args);
          previous = now;
        }
      }
    },
  }
}
</script>

<style scoped>
@import './mainrole.css';

</style>