<template>
  <div class="tile">
    <div class="tile-head">
      <div class="left-head">
        <h3>My Bikes</h3>
        <button
          v-show="showBikes == true"
          style="align-self: center"
          class="remove"
          @click="showBikes = !showBikes"
        >
          ^
        </button>
        <button
          v-show="showBikes == false"
          style="align-self: center"
          class="remove"
          @click="showBikes = !showBikes"
        >
          v
        </button>
      </div>
      <button class="bikes-btn" @click="showBikeForm = !showBikeForm">
        Add Bikes
      </button>
    </div>
    <new-bike-form class="form" v-show="showBikeForm" />
    <div class="tile-content">
      <div
        class="display-content"
        v-show="showBikes"
        v-for="bike in userBikes"
        :key="bike.userId"
      >
        <div class="bike-tiles">
          {{ bike.bikeName }} | {{ bike.type }} |
          {{ bike.bikeDescription }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import bikeService from "../../services/BikeService.js";
import newBikeForm from "../forms/NewBikeForm.vue";
export default {
  name: "bikes",
  components: {
    newBikeForm,
  },
  data() {
    return {
      showBikes: true,
      showBikeForm: false,
      userBikes: [
        {
          bikeId: "",
          userId: "",
          type: "",
          bikeName: "",
          bikeWeight: "",
          bikeDescription: "",
        },
      ],
    };
  },
  methods: {
    loadBikes() {
      bikeService.getUserBikes().then((response) => {
        this.userBikes = response.data;
      });
    },
  },
  mounted() {
    this.loadBikes();
    console.log(this.userBikes);
  },
};
</script>

<style scoped>
.left-head {
  display: flex;
  flex-direction: row;
}
.remove {
  display: inline-block;
  color: darkslategray;
  padding: 6px 6px;
  height: 26px;
  font-weight: bolder;
  font-size: 14px;
  background-color: #9bcea8;
  border-color: white;
  border-radius: 4px;
  margin-right: 280px auto;
}

.remove:hover {
  background-image: linear-gradient(rgb(0 0 0/40%) 0 0);
}
.tile {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  margin: 12px;
  background-color: #9bcea8;
  background-repeat: no-repeat;
  background-size: 100% 100%;
  background-image: blur;
  border-radius: 8px;
  width: 94%;
  height: auto;
  padding: 6px;
}
.tile-head {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.tile h3 {
  text-align: left;
  padding: 6px;
}

.tile-content {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
.display-content {
  display: flex;
  flex-direction: row;
  width: fit-content;
  flex-wrap: wrap;
  margin: 6px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 2px 10px 20px darkgray;
  padding: 6px;
  text-align: left;
}
.form {
  margin: 6px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 2px 10px 20px darkgray;
  padding: 6px;
  text-align: left;
  width: fit-content;
}
/* .form {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
} */
.bikes-btn {
  margin: 6px;
  background-color: white;
  border-block-style: none;
  box-shadow: 2px 10px 20px darkgray;
  border-radius: 8px;
  text-align: center;
}
</style>