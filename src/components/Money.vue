<template>
  <div class="tabs">
    <div class="money-tab">
      <h1>Money denomination Program</h1>
      <div class="money-input">
        <input type="number" v-model="money" />
        <br />
        <button class="money-btn" @click="handleMoneyNoteCount">
          Calculate
        </button>
      </div>
      <div class="money-count">
        <div v-if="finalNotes.length">You will have bellow notes</div>
        <div v-for="note in finalNotes" :key="note">
          <p>{{ note }}</p>
        </div>
      </div>
    </div>
    <div class="rate-tab">
      <h1>Student sorted by the rank</h1>
      <table border="1" width="90%">
        <tr>
          <th>Id</th>
          <th>Rating</th>
          <th>Rank</th>
        </tr>
        <tr v-for="item in sorted" :key="item" class="rate-table">
          <td>
            <p class="">{{ item.id }}</p>
          </td>
          <td>
            <p class="">{{ item.rating }}</p>
          </td>
          <td>
            <p class="">{{ item.rank }}</p>
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      money: "",
      availableNotes: [
        "2000",
        "500",
        "200",
        "100",
        "50",
        "20",
        "10",
        "5",
        "2",
        "1",
      ],
      finalNotes: [],
      clients: [
        {
          id: 25,
          rating: 58,
        },
        {
          id: 26,
          rating: 90,
        },
        {
          id: 27,
          rating: 58,
        },
        {
          id: 28,
          rating: 50,
        },
        {
          id: 29,
          rating: 58,
        },
        {
          id: 260,
          rating: 90,
        },
        {
          id: 270,
          rating: 58,
        },
        {
          id: 280,
          rating: 58,
        },
        {
          id: 28,
          rating: 50,
        },
      ],
      sorted: [],
    };
  },
  created() {
    this.calculateRank();
  },
  methods: {
    sortRanking() {
      for (var k = 0; k < this.sorted.length; k++) {
        for (var h = 1; h < this.sorted.length + 1; h++) {
          if (this.sorted[k + h] !== undefined) {
            if (this.sorted[k + h].tie !== true) {
              if (this.sorted[k].rating === this.sorted[h + k].rating) {
                this.sorted[k].rank = k + 1;
                this.sorted[h + k].rank = k + 1;
                this.sorted[k].tie = true;
                this.sorted[h + k].tie = true;
              }
            }
          }
        }
      }
    },

    calculateRank() {
      for (var i = 0; i < this.clients.length; i++) {
        this.sorted.push(this.clients[i]);
      }

      this.sorted.sort(function (a, b) {
        return b.rating - a.rating;
      });

      for (var j = 0; j < this.sorted.length; j++) {
        // original ranking
        this.sorted[j].rank = j + 1;
      }

      this.sortRanking();
      console.log(this.sorted);
    },
    handleMoneyNoteCount() {
      this.finalNotes = [];
      for (let i = 0; i < this.availableNotes.length; i++) {
        let count = this.money / this.availableNotes[i];
        if (parseInt(count) != 0) {
          this.finalNotes.push(
            this.availableNotes[i] + " x " + parseInt(count)
          );
        }
        this.money = this.money - parseInt(count) * this.availableNotes[i];
      }
      console.log(this.finalNotes);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.tabs {
  display: flex;
}
.money-tab,
.rate-tab {
  width: 50%;
  text-align: center;
}
.money-input {
  display: flex;
  justify-content: center;
}
.money-input input {
  width: 40%;
  height: 30px;
  margin-right: 10px;
}
.money-count {
  margin-top: 20px;
}
.money-btn {
  cursor: pointer;
  background-color: #2c3e50;
  color: white;
  border: none;
  border-radius: 4px;
}
.rate-tab tr th {
  padding: 10px 5px;
}
</style>
