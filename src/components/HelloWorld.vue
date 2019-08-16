<template>
  <div class="hello">
    <div class="game" id="game">

    </div>
    <div class="next" id="next">

    </div>
    <div class="info">
      <div>
        已用时: <span id="time">0</span>s
      </div>
      <div>
        已用时: <span id="secound">{{timeZhou}}</span>秒
      </div>
    </div>

    <button @click="stopGame">点击暂停</button>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue, Provide } from 'vue-property-decorator';

@Component
export default class HelloWorld extends Vue {
    @Provide()  nextDivs!: any = [];
    @Provide()  gameDivs!: any = [];
    @Provide()  timeZhou: number = 0;
    @Provide()  gameData:any = [
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    ];
    @Provide()  gameDatas:any = [
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [2, 2, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 2, 2, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    ];
    @Provide()  nextData:any = {
        type: null,
        data: [
            [2, 2, 0, 0],
            [0, 2, 2, 0],
            [0, 0, 0, 0],
            [0, 0, 0, 0],
        ]
    }
    @Provide() speed:number = 1;
    @Provide() cic:any;

    // -----------------------data----------------------------
  startGame () {
      let timeNow = 0; // 当前下落时间
      this.changeNextData();
      const gameDataNow = JSON.parse(JSON.stringify(this.gameData));
      this.cic = setInterval(() => {
          this.timeZhou++;
          this.gameData = JSON.parse(JSON.stringify(gameDataNow));
          for (let i = timeNow; i < (this.nextData.data.length+timeNow-1); i++) {
              for (let j = 0; j < 11; j++) {
                  if (this.nextData.type === 0) {
                      if (timeNow === 18) {
                          console.log('游戏结束')
                          this.refreshGame();
                          this.refreshNext();
                          clearInterval(this.cic)
                          this.startGame()
                      } else {
                          this.refreshGame();
                          this.refreshNext();
                      }
                  }

                  if (this.nextData.type === 2) {
                      if (timeNow === 18) {
                          console.log('游戏结束')
                          this.refreshGame();
                          this.refreshNext();
                          clearInterval(this.cic)
                          this.startGame()
                      } else {
                          this.refreshGame();
                          this.refreshNext();
                      }
                  }

                  if (this.nextData.type === 1) {
                      if (timeNow === 19) {
                          console.log('游戏结束')
                          this.refreshGame();
                          this.refreshNext();
                          clearInterval(this.cic)
                          this.startGame()
                      } else {
                          this.refreshGame();
                          this.refreshNext();
                      }
                  }
                  if (!this.gameData[i][j]) {
                      this.gameData[i][j] = this.gameData[i][j] + this.nextData.data[i-timeNow][j];
                  }
                  console.log(timeNow, 'tiome')

              }
          }
          timeNow++;
      }, 1000)
  };
  changeNextData() {
      let nextType = Math.floor( Math.random()*1 )+1
      console.log(nextType, '????')
      switch (nextType){
          case 4:
              this.nextData = {
                  type: 0,
                  status: 0,
                  data: [
                      [2, 2, 0, 0],
                      [0, 2, 2, 0],
                      [0, 0, 0, 0],
                      [0, 0, 0, 0],
                  ]
              };
              break;
          case 2:
              this.nextData = {
                  type: 1,
                  status: 0,
                  data: [
                      [2, 2, 2, 2],
                      [0, 0, 0, 0],
                      [0, 0, 0, 0],
                      [0, 0, 0, 0],
                  ]
              };
              break;
          case 1:
              this.nextData = {
                  type: 2,
                  status: 0,
                  data: [
                      [2, 2, 0, 0],
                      [2, 2, 0, 0],
                      [0, 0, 0, 0],
                      [0, 0, 0, 0],
                  ]
              };
              break;
      }

  };
  stopGame () {
      switch (this.nextData.type){
          case 1:
              if (this.nextData.status) {
                  this.nextData.data = [
                      [2, 2, 0, 0],
                      [0, 2, 2, 0],
                      [0, 0, 0, 0],
                      [0, 0, 0, 0],
                  ];
                  this.nextData.status = 0
              } else {
                  this.nextData.data = [
                      [0, 2, 0, 0],
                      [2, 2, 0, 0],
                      [2, 0, 0, 0],
                      [0, 0, 0, 0],
                  ];
                  this.nextData.status = 1
              }
          case 2:
              if (!this.nextData.status) {
                  this.nextData.data = [
                      [2, 0, 0, 0],
                      [2, 0, 0, 0],
                      [2, 0, 0, 0],
                      [2, 0, 0, 0],
                  ];
                  this.nextData.status = 1
              } else {
                  this.nextData.data = [
                      [2, 2, 2, 2],
                      [0, 0, 0, 0],
                      [0, 0, 0, 0],
                      [0, 0, 0, 0],
                  ];
                  this.nextData.status = 0
              }

      }
  }

  initGame () {
      for (let i = 0; i < this.gameData.length; i++) {
          let gameDiv = [];
          for (let j = 0; j < this.gameData[0].length; j++) {
              let newNode = document.createElement('div');
              newNode.className = 'none';
              newNode.style.top = (i * 20) + 'px';
              newNode.style.left = (j * 20) + 'px';
              document.getElementById('game').appendChild(newNode)
              gameDiv.push(newNode);
          }
          this.gameDivs.push(gameDiv);
      }
  };
  initNext () {
      for (let i = 0; i < this.nextData.data.length; i++) {
          let nextDiv = [];
          for (let j = 0; j < this.nextData.data[0].length; j++) {
              let newNode = document.createElement('div');
              newNode.className = 'none';
              newNode.style.top = (i * 20) + 'px';
              newNode.style.left = (j * 20) + 'px';
              document.getElementById('next').appendChild(newNode)
              nextDiv.push(newNode);
          }
          this.nextDivs.push(nextDiv);
      }
  }
  refreshGame () {
      for (let i = 0; i < this.gameData.length; i++) {
          for (let j = 0; j < this.gameData[0].length; j++) {
              if (this.gameData[i][j] == 0) {
                  this.gameDivs[i][j].className = 'none';
              } else if (this.gameData[i][j] == 1) {
                  this.gameDivs[i][j].className = 'done';
              } else if (this.gameData[i][j] == 2) {
                  this.gameDivs[i][j].className = 'current';
              }
          }
      }
  };
  refreshNext () {
      for (let i = 0; i < this.nextData.data.length; i++) {
          for (let j = 0; j < this.nextData.data[0].length; j++) {
              if (this.nextData.data[i][j] == 0) {
                  this.nextDivs[i][j].className = 'none';
              } else if (this.nextData.data[i][j] == 1) {
                  this.nextDivs[i][j].className = 'done';
              } else if (this.nextData.data[i][j] == 2) {
                  this.nextDivs[i][j].className = 'current';
              }
          }
      }
  };

  mounted() {
      // this.changeNextData()
      this.initGame()
      this.initNext()
      this.refreshGame()
      this.refreshNext()
      this.startGame()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
  .game{
    width: 200px;
    height: 400px;
    background: #f2faff;
    border-left: 1px solid blue;
    border-right: 1px solid blue;
    border-bottom: 1px solid blue;
    position: absolute;
    top: 10px;
    left: 10px;
    overflow: hidden;
  }
  .next{
    width: 80px;
    height: 80px;
    background: #f2faff;
    position: absolute;
    top: 10px;
    left: 250px;
    border: 1px solid blue;
  }
  .info{
    position: absolute;
    top: 100px;
    left: 250px;
  }
  .none, .current, .done {
    width: 20px;
    height: 20px;
    position: absolute;
    box-sizing: border-box;
  }
  .none{
    background: #f2faff;
  }
  .current{
    background: pink;
    border: 1px solid;
  }
  .done{
    background: gray;
    border: 1px solid black;
  }
</style>
