<template>
  <div style="padding: 0">
    <div class="game">
      <div class="container">
        <div class="row">
          <div class="col-xs-12 col-sm-12  col-md-12">
            <h2 class="title">Tic tac toe games</h2>
            <span class="sub-title">Welcome to the best game in the world</span>
            <div class="game-area">
              <span class="players">
                Player 1
                <span class="wins-counter">{{ player1WinCount }}</span>
              </span>
              <board :squares="squares" :winner="winner" @click="click" />
              <span class="players">
                Player 2
                <span class="wins-counter">{{ player2WinCount }}</span>
              </span>
            </div>
          </div>
          <div class="col-xs-12 col-sm-12 ">
            <div class="restart-row">
              <span class="tie" v-if="matchWasTie">Match Was a Tie!</span>
              <button
                v-if="showRestart"
                @click="restart"
                class="restart-button"
              >
                Play Again
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="statics">
      <h2 class="title">Awesome Statictis</h2>
      <span class="sub-title">All statictis in one place</span>
      <div class="container">
        <div class="row">
          <div class="col-xs-12 col-sm-12  col-md-5">
            <h3 class="title">Win Percentage %</h3>
            <div class="percentage-wrapper">
              <div class="each">
                <span class="player-title">Player 1</span>
                <div class="results-wrapper">
                  <div class="win">{{ player1WinPercentage }}%</div>
                  <div class="lose">{{ player1LossPercentage }}%</div>
                </div>
              </div>
              <div class="each">
                <span class="player-title">Player 2</span>
                <div class="results-wrapper">
                  <div class="win">{{ player2WinPercentage }}%</div>
                  <div class="lose">{{ player2LossPercentage }}%</div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-xs-12 col-sm-12  col-md-2"></div>
          <div class="col-xs-12 col-sm-12  col-md-5">
            <h3 class="title">Played Matches</h3>
            <div class="played-matches-wrapper">
              <div
                class="match-circle"
                v-for="n in playedMatches"
                :key="n"
              ></div>
            </div>
            <h3 class="title">Match History</h3>
            <div class="played-matches-wrapper">
              <div class="history-box" v-for="n in resultHistory" :key="n">
                {{ n }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {
    Board: () => import("./Board"),
  },
  name: "game",
  data() {
    return {
      squares: Array(9).fill(null),
      stepNumber: 0,
      currentPlayer: "X",
      winner: null,
      showRestart: false,
      winnerPlayer: "",
      player1WinCount: 0,
      player1LossCount: 0,
      player2WinCount: 0,
      player2LossCount: 0,
      playedMatches: 0,
      player1WinPercentage: 0,
      player2WinPercentage: 0,
      player1LossPercentage: 0,
      player2LossPercentage: 0,
      resultHistory: [],
      matchWasTie: false,
    };
  },
  methods: {
    hasWinner() {
      if (this.winner) return true;
      const squares = this.squares;
      const matches = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];
      for (let i = 0; i < matches.length; i++) {
        const [a, b, c] = matches[i];
        if (
          squares[a] &&
          squares[a] === squares[b] &&
          squares[a] === squares[c]
        ) {
          this.winner = [a, b, c];
          return true;
        }
      }
      return false;
    },
    restart() {
      this.matchWasTie = false;
      this.showRestart = false;
      this.squares = Array(9).fill(null);
      this.stepNumber = 0;
      this.currentPlayer = "X";
      this.winner = null;
    },
    click(i) {
      if (this.squares[i] || this.winner) return;
      this.$set(this.squares, i, this.currentPlayer);
      if (!this.hasWinner()) {
        this.stepNumber++;
        this.currentPlayer = this.currentPlayer === "X" ? "O" : "X";
        if (this.stepNumber == 9) {
          this.calculateWinnerData("tie");
        }
      } else {
        this.winnerPlayer = this.currentPlayer == "X" ? "player1" : "player2";
        this.playedMatches++;
        this.showRestart = true;
        if (this.winnerPlayer == "player1") {
          this.calculateWinnerData("p1");
        } else if (this.winnerPlayer == "player2") {
          this.calculateWinnerData("p2");
        }
      }
    },
    calculateWinnerData(matchState) {
      if (matchState == "p1") {
        this.player1WinCount++;
        this.player2LossCount++;
        this.resultHistory.push("P1");
        this.player1WinPercentage = Math.floor(
          (this.player1WinCount * 100) / this.playedMatches
        );
        this.player1LossPercentage = Math.floor(
          (this.player1LossCount * 100) / this.playedMatches
        );
        this.player2WinPercentage = Math.floor(
          (this.player2WinCount * 100) / this.playedMatches
        );
        this.player2LossPercentage = Math.floor(
          (this.player2LossCount * 100) / this.playedMatches
        );
      } else if (matchState == "p2") {
        this.player2WinCount++;
        this.player1LossCount++;
        this.resultHistory.push("P2");
        this.player2WinPercentage = Math.floor(
          (this.player2WinCount * 100) / this.playedMatches
        );

        this.player1WinPercentage = Math.floor(
          (this.player1WinCount * 100) / this.playedMatches
        );

        this.player1LossPercentage = Math.floor(
          (this.player1LossCount * 100) / this.playedMatches
        );

        this.player2LossPercentage = Math.floor(
          (this.player2LossCount * 100) / this.playedMatches
        );
      } else if (matchState == "tie") {
        this.showRestart = true;
        this.playedMatches++;
        this.resultHistory.push("Tie");
        this.matchWasTie = true;
        this.player1WinPercentage = Math.floor(
          (this.player1WinCount * 100) / this.playedMatches
        );
        this.player1LossPercentage = Math.floor(
          (this.player1LossCount * 100) / this.playedMatches
        );
        this.player2WinPercentage = Math.floor(
          (this.player2WinCount * 100) / this.playedMatches
        );
        this.player2LossPercentage = Math.floor(
          (this.player2LossCount * 100) / this.playedMatches
        );
        this.player2WinPercentage = Math.floor(
          (this.player2WinCount * 100) / this.playedMatches
        );

        this.player1WinPercentage = Math.floor(
          (this.player1WinCount * 100) / this.playedMatches
        );

        this.player1LossPercentage = Math.floor(
          (this.player1LossCount * 100) / this.playedMatches
        );

        this.player2LossPercentage = Math.floor(
          (this.player2LossCount * 100) / this.playedMatches
        );
      }
    },
  },
};
</script>

<style lang="scss">
.statics {
  background: white;
  padding-top: 45px;
  padding-bottom: 45px;
  .title {
    text-align: center;
  }
  .sub-title {
    text-align: center;
    display: block;
    margin: 10px auto;
    margin-bottom: 45px;
  }
  .percentage-wrapper {
    padding: 20px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    margin-top: 30px;
    @media (max-width: 768px) {
      margin-bottom: 30px;
    }
    .each {
      display: flex;
      flex-direction: column;
      justify-content: center;
      .player-title {
        text-align: center;
        margin-bottom: 30px;
        font-size: 20px;
        font-weight: 100;
      }
      .results-wrapper {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        font-size: 24px;
        font-weight: bold;
        color: white;
        width: 200px;
        @media (max-width: 768px) {
          width: auto;
          font-size: 16px;
        }
        .win {
          border-radius: 50%;
          background-color: #50cb93;
          width: 90px;
          height: 90px;
          text-align: center;
          padding-top: 28px;
          @media (max-width: 768px) {
            width: 45px;
            height: 45px;
            padding-top: 12px;
            margin-right: 10px;
          }
        }
        .lose {
          border-radius: 50%;
          background-color: #ff5c5b;
          width: 90px;
          height: 90px;
          text-align: center;
          padding-top: 28px;
          @media (max-width: 768px) {
            width: 45px;
            height: 45px;
            padding-top: 12px;
          }
        }
      }
    }
  }
  .played-matches-wrapper {
    padding: 20px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    height: 100px;
    .match-circle {
      width: 30px;
      height: 30px;
      background: #ff5c5b;
      border-radius: 50%;
      margin-right: 5px;
    }
    .history-box {
      border: 1px solid #ededed;
      text-align: center;
      margin-right: 10px;
      width: 40px;
      height: 40px;
      padding-top: 7px;
    }
  }
}
.game {
  background: #ededed;
  padding-top: 45px;
  padding-bottom: 45px;
  .title {
    text-align: center;
  }
  .sub-title {
    text-align: center;
    display: block;
    margin: 10px auto;
  }
}
.game-area {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  margin-top: 45px;
  margin-bottom: 45px;
  @media (max-width: 768px) {
    flex-direction: column;
    justify-content: space-between;
  }
}
.game-box {
  display: flex;
  flex-wrap: wrap;
  width: 204px;
  height: 204px;
}
.restart-row {
  text-align: center;
  .restart-button {
    display: block;
    margin: 0 auto;
    outline: none;
    border: none;
    background: #ff5c5b;
    color: white;
    border-radius: 2px;
    padding: 10px 20px;
  }
  .tie {
    color: #ff5c5b;
    margin-bottom: 30px;
  }
}
.players {
  font-weight: normal;
  color: gray;
  font-size: 24px;
  text-align: center;
  .wins-counter {
    font-weight: bold;
    display: block;
    margin: 10px auto;
    font-size: 50px;
  }
}
</style>
