<template>
  <section class="pick-section">
    <div class="container">
      <div class="pick-container">
        <div class="pick-container__title">
          <h3 style="margin-bottom: -1.5rem">Vehicle Models</h3>
          <h2 style="margin-bottom: -1.5rem">Rental Fleet</h2>
          <p>
            Choose from a variety of our eco-friendly vehicles to rent for your next
            adventure in Bali
          </p>
        </div>


        <div class="pick-container__car-content">
          <!-- Pick car buttons -->
          <div class="pick-box">
            <button
              :class="coloringButton('btn2')"
              @click="changeCar('Toyota Avanza', 'btn2')"
            >
              Toyota Avanza
            </button>
            <button
              :class="coloringButton('btn3')"
              @click="changeCar('Toyota Kijang', 'btn3')"
            >
              Toyota Kijang Innova
            </button>
            <button
              :class="coloringButton('btn4')"
              @click="changeCar('Toyota Innova', 'btn4')"
            >
              Toyota Innova
            </button>
            <button
              :class="coloringButton('btn5')"
              @click="changeCar('Toyota Agya', 'btn5')"
            >
              Toyota Agya
            </button>
          </div>

          <!-- CarBox content based on selected car -->
          <div v-if="CAR_DATA[selectedCar]" class="box-cars">
            <!-- Car -->
            <div class="pick-car">
              <div v-if="carLoad" class="loader"></div>
              <img
                :src="require(`@/assets/${CAR_DATA[selectedCar].img}`)"
                alt="car_img"
                @load="setCarLoad(false)"
              />
            </div>
            <!-- Description -->
            <div class="pick-description shadow">
              <div class="pick-description__price">
                <span>${{ CAR_DATA[selectedCar].price }}</span
                ><p>/ DAY</p>
              </div>
              <div class="pick-description__table">
                <div class="pick-description__table__col">
                  <span>Model</span>
                  <span>{{ CAR_DATA[selectedCar].model }}</span>
                </div>
                <div class="pick-description__table__col">
                  <span>Mark</span>
                  <span>{{ CAR_DATA[selectedCar].mark }}</span>
                </div>
                <div class="pick-description__table__col">
                  <span>Year</span>
                  <span>{{ CAR_DATA[selectedCar].year }}</span>
                </div>
                <div class="pick-description__table__col">
                  <span>Doors</span>
                  <span>{{ CAR_DATA[selectedCar].doors }}</span>
                </div>
                <div class="pick-description__table__col">
                  <span>CO2 Emission</span>
                  <span>{{ CAR_DATA[selectedCar].co2Emission }}</span>
                </div>
                <div class="pick-description__table__col">
                  <span>Transmission</span>
                  <span>{{ CAR_DATA[selectedCar].transmission }}</span>
                </div>
                <div class="pick-description__table__col">
                  <span>Fuel</span>
                  <span>{{ CAR_DATA[selectedCar].fuel }}</span>
                </div>
              </div>
              <!-- Button CTA -->
              <a class="cta-btn" href="#booking-section">Reserve Now</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
  <CarCalculatorEmissions :co2Emission="computedCO2Emission" /> 
</template>

<script>
import CarCalculatorEmissions from "./CarCalculatorEmissions.vue";
export default {
  components: {
    CarCalculatorEmissions,
  },
  data() {
    return {
      selectedCar: "Toyota Avanza",
      selectedScooter: "Scooter Model 1",
      carLoad: true,
      selectedTab: "car",
    };
  },
  computed: {
    computedCO2Emission() {
      // Compute the CO2 emission value based on CAR_DATA[selectedCar]
      return this.CAR_DATA[this.selectedCar].co2Emission;
    },
    CAR_DATA() {
      return {
        "Toyota Avanza": {
          price: "80 to $100 ",
          img: "toyotaavanza.jpeg",
          model: "Avanza",
          mark: "Toyota",
          year: "2020",
          doors: "6",
          air: "Yes",
          transmission: "Automatic",
          fuel: "Hybrid",
          co2Emission: 172
        },
        "Toyota Kijang": {
          price: "100 to $115",
          img: "kijang.jpeg",
          model: "Kijang",
          mark: "Toyota",
          year: "2007",
          doors: "4/5",
          air: "Yes",
          transmission: "Automatic",
          fuel: "Hybrid",
          co2Emission: 149
        },
        "Toyota Innova": {
          price: "100 to $115",
          img: "innova.png",
          model: "Innova",
          mark: "Toyota",
          year: "2022",
          doors: "7",
          air: "Yes",
          transmission: "Automatic",
          fuel: "Hybrid",
          co2Emission: 131.3
        },
        "Toyota Agya": {
          price: "60 to $75",
          img: "Toyota-Agya-1.jpg",
          model: "Agya",
          mark: "Toyota",
          year: "2021",
          doors: "4",
          air: "Yes",
          transmission: "Automatic",
          fuel: "Hybrid",
          co2Emission: 113,
        },
      };
    },
  },
  methods: {
    changeCar(carName, buttonID) {
      this.selectedCar = carName;
      this.colorBtn = buttonID;
    },
    changeScooter(scooterName, buttonID) {
      this.selectedScooter = scooterName;
      this.colorBtn = buttonID;
    },
    coloringButton(id) {
      return this.selectedCar === id || this.selectedScooter === id
        ? "colored-button"
        : "shadow car-btn";
    },
    setCarLoad(status) {
      this.carLoad = status;
    },
    selectTab(tab) {
      this.selectedTab = tab;
    },
  },
};
</script>

<style scoped>
.pick-section {
  padding: 5rem 0;
  background: white;
}

.pick-container {
  display: flex;
  flex-direction: column;
}

.pick-container__title {
  margin: 0 auto;
  text-align: center;
  color: #000; /* Replace with your text color */
  max-width: 50rem;
}

.pick-container__title p {
  font-size: 16px; /* Replace with your font size */
  font-family: Arial, sans-serif; /* Replace with your font-family */
  color: #888; /* Replace with your text color */
  line-height: 1.5;
}

.pick-container__title h3 {
  font-size: 24px; /* Replace with your font size */
  font-family: Arial, sans-serif; /* Replace with your font-family */
  font-weight: 500;
}

.pick-container__title h2 {
  font-size: 32px; /* Replace with your font size */
  font-family: Arial, sans-serif; /* Replace with your font-family */
  margin: 0.5rem 0 1rem 0;
}

.pick-container__car-content {
  display: flex;
  justify-content: space-between;
  gap: 1rem;
}

@media (max-width: 1050px) {
  .pick-container__car-content {
    flex-direction: column;
    gap: 5rem;
  }
}

.pick-box {
  display: flex;
  flex-direction: column;
  gap: 0.7rem;
}

.pick-box button {
  font-weight: 600;
  border: none;
  cursor: pointer;
  padding: 1rem 2rem;
  background-color: #e9e9e9;
  transition: all 0.2s;
  text-align: left;
}

.pick-box button:hover {
  background-color: #42b983; /* Replace with your desired hover background color */
  color: white;
}

.pick-car {
  width: 40rem;
  position: relative;
}

@media (max-width: 700px) {
  .pick-car {
    width: 100%;
  }
}

.pick-car img {
  width: 100%;
  margin-top: 6rem;
}

.pick-description {
  width: 25rem;
  border-radius: 10px;
  background: white;
}

.pick-description__price {
  width: 100%;
  background-color: #42b983; /* Replace with your desired background color */
  font-size: 1.8rem;
  display: flex;
  align-items: center;
  gap: 1.5rem;
  color: white;
  padding: 0.3rem 1rem;
  white-space: nowrap;
}

.pick-description__price span {
  font-size: 2.8rem;
  font-weight: 700;
}

.pick-description__table {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto;
  font-size: 1.4rem;
}

.pick-description__table__col {
  display: grid;
  grid-template-columns: 1fr 1fr;
  text-align: center;
  grid-template-rows: auto;
  padding: 0.4rem 0.5rem;
  border-bottom: 2px solid #706f7b;
  border-right: 2px solid #706f7b;
  border-left: 2px solid #706f7b;
}

.pick-description__table__col span:nth-child(1) {
  border-right: 2px solid #706f7b;
}

.cta-btn {
  font-size: 2rem;
  text-transform: uppercase;
  text-decoration: none;
  font-weight: 600;
  color: white;
  font-family: Arial, sans-serif; /* Replace with your font-family */
  background-color: #42b983; /* Replace with your desired background color */
  padding: 1rem 1rem;
  display: flex;
  width: 100%;
  justify-content: center;
  transition: all 0.3s;
}

.cta-btn:hover {
  background-color: #e9381d;
}

.box-cars {
  gap: 1rem;
  display: flex;
  justify-content: space-between;
}
.car-btn {
  border-radius: 10px;
}

@media (max-width: 1200px) {
  .box-cars {
    gap: 2rem;
  }
}

@media (max-width: 700px) {
  .box-cars {
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 5rem;
  }
}

.colored-button {
  background-color: #42b983 !important;
  color: white;
}

.loader {
  width: 48px;
  height: 48px;
  border: 5px solid #00000042;
  border-bottom-color: #ff3d00;
  border-radius: 50%;
  display: inline-block;
  box-sizing: border-box;
  animation: rotation 1s linear infinite;
  position: absolute;
  transform: translate(-50%, -50%);
  top: 40%;
  right: 43%;
}

@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.tab {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 1rem;
}

.tab button {
  font-weight: 600;
  border: none;
  cursor: pointer;
  padding: 0.5rem 1rem;
  background-color: #e9e9e9;
  transition: all 0.2s;
  text-align: center;
}

.tab button.active {
  background-color: #42b983;
  color: white;
}
</style>
