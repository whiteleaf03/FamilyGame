<template>
  <div id="MakeWord">
    <div class="display">
      <div style="display: flex">
        <div class="button1" style="border: none; background-color: rgba(255,255,255,0)"></div>
        <button class="button1" @click="push('red', 1)">推</button>
        <button class="button1" @click="push('red', 2)">推</button>
        <button class="button1" @click="push('red', 3)">推</button>
        <button class="button1" @click="push('red', 4)">推</button>
      </div>
      <div class="line">
        <div class="box-red" style="padding: 3px; border: none"></div>
        <div class="box-red">{{ board[1][0] }}</div>
        <div class="box-red">{{ board[1][1] }}</div>
        <div class="box-red">{{ board[1][2] }}</div>
        <div class="box-red">{{ board[1][3] }}</div>
      </div>
      <div class="line">
        <div class="box-red" style="padding: 3px; border: none"></div>
        <div class="box-red">{{ board[2][0] }}</div>
        <div class="box-red">{{ board[2][1] }}</div>
        <div class="box-red">{{ board[2][2] }}</div>
        <div class="box-red">{{ board[2][3] }}</div>
      </div>
      <div class="line">
        <div class="box-yellow">{{ board[0][0] }}</div>
        <div class="box-yellow">{{ board[3][0] }}</div>
        <div class="box-yellow">{{ board[3][1] }}</div>
        <div class="box-yellow">{{ board[3][2] }}</div>
        <div class="box-yellow">{{ board[3][3] }}</div>
      </div>
      <div class="line">
        <div class="box-blue" style="padding: 3px; border: none"></div>
        <div class="box-blue">{{ board[4][0] }}</div>
        <div class="box-blue">{{ board[4][1] }}</div>
        <div class="box-blue">{{ board[4][2] }}</div>
        <div class="box-blue">{{ board[4][3] }}</div>
      </div>
      <div class="line">
        <div class="box-blue" style="padding: 3px; border: none"></div>
        <div class="box-blue">{{ board[5][0] }}</div>
        <div class="box-blue">{{ board[5][1] }}</div>
        <div class="box-blue">{{ board[5][2] }}</div>
        <div class="box-blue">{{ board[5][3] }}</div>
      </div>
      <div style="display: flex">
        <div class="button2" style="border: none; background-color: rgba(255,255,255,0)"></div>
        <button class="button2" @click="push('blue', 1)">推</button>
        <button class="button2" @click="push('blue', 2)">推</button>
        <button class="button2" @click="push('blue', 3)">推</button>
        <button class="button2" @click="push('blue', 4)">推</button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "MakeWord",
    data() {
      return {
        initialList: ['Q', 'W', 'R', 'T', 'Y', 'P', 'S', 'D', 'F', 'G', 'H', 'J', 'K', 'L', 'M', 'N', 'B', 'V', 'C', 'X', 'Z'],
        //先行后列
        board: [[''], ['', '', '', ''], ['', '', '', ''], ['', '', '', ''], ['', '', '', ''], ['', '', '', '']],
        position: [2, 2, 2, 2]
      }
    },
    methods: {
      init() {
        this.board = [[''], ['', '', '', ''], ['', '', '', ''], ['', '', '', ''], ['', '', '', ''], ['', '', '', '']]
        this.position = [2, 2, 2, 2]
        let randomInitialList = []
        let randomInitial = ''
        do {
          randomInitial = this.initialList[Math.floor(Math.random() * 21)]
          if (randomInitialList.indexOf(randomInitial) === -1) {
            //该字母不存在 放入
            randomInitialList.push(randomInitial)
          }
        } while (randomInitialList.length < 5)
        this.board[0][0] = randomInitialList[0]
        this.board[3][0] = randomInitialList[1]
        this.board[3][1] = randomInitialList[2]
        this.board[3][2] = randomInitialList[3]
        this.board[3][3] = randomInitialList[4]
      },
      push(team, column) {
        if (team === 'red') {
          let position = this.position[column - 1]
          if (this.position[column - 1] + 1 !== 5) {
            this.position[column - 1] += 1
            this.board[position + 2][column - 1] = this.board[position + 1][column - 1]
            this.board[position + 1][column - 1] = ''
          }
        } else {
          let position = this.position[column - 1]
          if (this.position[column - 1] - 1 !== -1) {
            this.position[column - 1] -= 1
            this.board[position][column - 1] = this.board[position + 1][column - 1]
            this.board[position + 1][column - 1] = ''
          }
        }
        this.check()
      },
      check() {
        if (this.position.toString() === [0, 0, 0, 0].toString()) {
          //蓝队赢
          alert('恭喜蓝队胜利')
          this.init()
        } else if (this.position.toString() === [4, 4, 4, 4].toString()) {
          //红队赢
          alert('恭喜红队胜利')
          this.init()
        }
      }
    },
    mounted() {
      this.init()
    }
  }
</script>

<style scoped>
  #MakeWord {
    display: flex;
    flex-direction: column;
    width: 100%;
  }

  .line {
    flex: 1;
    display: flex;
  }

  .button1 {
    width: 90px;
    height: 90px;
    margin: 15px;
    border: 3px solid #ff0044;
    border-radius: 15px;
    background-color: #ff0044;
    color: white;
    font-size: xx-large;
    line-height: 90px;
    user-select: none;
  }

  .button2 {
    width: 90px;
    height: 90px;
    margin: 15px;
    border: 3px solid deepskyblue;
    border-radius: 15px;
    background-color: deepskyblue;
    color: white;
    font-size: xx-large;
    line-height: 90px;
    user-select: none;
  }

  .box-red {
    width: 84px;
    height: 84px;
    border: 3px solid #ff0044;
    margin: 15px;
    font-size: xxx-large;
    text-align: center;
    line-height: 84px;
    user-select: none;
  }

  .box-yellow {
    width: 84px;
    height: 84px;
    border: 3px solid #ffcc00;
    margin: 15px;
    font-size: xxx-large;
    text-align: center;
    line-height: 84px;
    user-select: none;
  }

  .box-blue {
    width: 84px;
    height: 84px;
    border: 3px solid deepskyblue;
    margin: 15px;
    font-size: xxx-large;
    text-align: center;
    line-height: 84px;
    user-select: none;
  }

  button:active {
    box-shadow: 0 2px 6px 0 rgba(0,0,0,0.2), 0 17px 50px 0 rgba(0,0,0,0.2);
  }
</style>