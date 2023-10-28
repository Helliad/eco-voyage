<template>
  <section class="pick-section">
    <div class="container">
      <div class="pick-container">
        <div class="pick-container__title">
          <h3 style="margin-bottom: -1.5rem">Vehicle Models</h3>
          <h2 style="margin-bottom: -1.5rem">Our rental fleet</h2>
          <p>
            Choose from a variety of our amazing vehicles to rent for your next
            adventure or business trip
          </p>
        </div>
        <div class="tab">
          <button class="btn" :class="{ active: selectedTab === 'car' }" @click="selectTab('car')">
            Cars
          </button>
          <button class="btn" :class="{ active: selectedTab === 'scooter' }" @click="selectTab('scooter')">
            E-Scooters
          </button>
        </div>

        <div class="pick-container__car-content" v-if="selectedTab === 'car'">
          <!-- Pick car buttons -->
          <div class="pick-box">
            <button :class="coloringButton('btn1')" @click="changeCar('VW Golf 6', 'btn1')">
              VW Golf 6
            </button>
            <button :class="coloringButton('btn2')" @click="changeCar('Audi A1 S-Line', 'btn2')">
              Audi A1 S-Line
            </button>
            <button :class="coloringButton('btn3')" @click="changeCar('Toyota Camry', 'btn3')">
              Toyota Camry
            </button>
            <button :class="coloringButton('btn4')" @click="changeCar('BMW 320 ModernLine', 'btn4')">
              BMW 320 ModernLine
            </button>
            <button :class="coloringButton('btn5')" @click="changeCar('Mercedes-Benz GLK', 'btn5')">
              Mercedes-Benz GLK
            </button>
            <button :class="coloringButton('btn6')" @click="changeCar('VW Passat CC', 'btn6')">
              VW Passat CC
            </button>
          </div>

          <!-- CarBox content based on selected car -->
          <div v-if="CAR_DATA[selectedCar]" class="box-cars">
            <!-- Car -->
            <div class="pick-car">
              <div v-if="carLoad" class="loader"></div>
              <img :src="require(`@/assets/${CAR_DATA[selectedCar].img}`)" alt="car_img" @load="setCarLoad(false)" />
            </div>
            <!-- Description -->
            <div class="pick-description shadow">
              <div class="pick-description__price">
                <span>${{ CAR_DATA[selectedCar].price }}</span>/ rent per day
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

        <div class="pick-container__car-content" v-if="selectedTab === 'scooter'">
          <!-- Pick car buttons -->
          <div class="pick-box">
            <button :class="coloringButton('scooter1')" @click="changeScooter('Scooter Model 1', 'scooter1')">
              Scooter Model 1
            </button>
            <button :class="coloringButton('scooter2')" @click="changeScooter('Scooter Model 2', 'scooter2')">
              Scooter Model 2
            </button>
          </div>

          <!-- CarBox content based on selected car -->
          <div v-if="SCOOTER_DATA[selectedScooter]" class="box-cars">
            <!-- Car -->
            <div class="pick-car">
              <div v-if="carLoad" class="loader"></div>
              <img style="width: 350px" :src="require(`@/assets/${SCOOTER_DATA[selectedScooter].img}`)" alt="car_img"
                @load="setCarLoad(false)" />
            </div>
            <!-- Description -->
            <div class="pick-description shadow">
              <div class="pick-description__price">
                <span>${{ SCOOTER_DATA[selectedScooter].price }}</span>/ rent per day
              </div>
              <div class="pick-description__table">
                <div class="pick-description__table__col">
                  <span>Model</span>
                  <span>{{ SCOOTER_DATA[selectedScooter].model }}</span>
                </div>
                <div class="pick-description__table__col">
                  <span>Mark</span>
                  <span>{{ SCOOTER_DATA[selectedScooter].mark }}</span>
                </div>
                <div class="pick-description__table__col">
                  <span>Year</span>
                  <span>{{ SCOOTER_DATA[selectedScooter].year }}</span>
                </div>
                <div class="pick-description__table__col">
                  <span>Doors</span>
                  <span>{{ SCOOTER_DATA[selectedScooter].doors }}</span>
                </div>
                <div class="pick-description__table__col">
                  <span>CO2 Emission</span>
                  <span>{{ SCOOTER_DATA[selectedScooter].co2Emission }}</span>
                </div>
                <div class="pick-description__table__col">
                  <span>Transmission</span>
                  <span>{{ SCOOTER_DATA[selectedScooter].transmission }}</span>
                </div>
                <div class="pick-description__table__col">
                  <span>Fuel</span>
                  <span>{{ SCOOTER_DATA[selectedScooter].fuel }}</span>
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
</template>

<script>
export default {
  data() {
    return {
      selectedCar: "VW Golf 6",
      selectedScooter: "Scooter Model 1",
      carLoad: true,
      selectedTab: "car",
    };
  },
  computed: {
    CAR_DATA() {
      return {
        "VW Golf 6": {
          price: "37",
          img: "golf6.jpg",
          model: "Golf 6",
          mark: "Volkswagen",
          year: "2008",
          doors: "4/5",
          air: "Yes",
          transmission: "Manual",
          fuel: "Diesel",
          co2Emission: this.getRandomCO2Value(),
        },
        "Audi A1 S-Line": {
          price: "45",
          img: "audia1.jpg",
          model: "Audi",
          mark: "A1",
          year: "2012",
          doors: "4/5",
          air: "Yes",
          transmission: "Manual",
          fuel: "Gasoline",
          co2Emission: this.getRandomCO2Value(),
        },
        "Toyota Camry": {
          price: "30",
          img: "toyotacamry.jpg",
          model: "Camry",
          mark: "Toyota",
          year: "2006",
          doors: "4/5",
          air: "Yes",
          transmission: "Automatic",
          fuel: "Hybrid",
          co2Emission: this.getRandomCO2Value(),
        },
        "BMW 320 ModernLine": {
          price: "35",
          img: "bmw320.jpg",
          model: "320",
          mark: "BMW",
          year: "2012",
          doors: "4/5",
          air: "Yes",
          transmission: "Manual",
          fuel: "Diesel",
          co2Emission: this.getRandomCO2Value(),
        },
        "Mercedes-Benz GLK": {
          price: "50",
          img: "benz.jpg",
          model: "Benz GLK",
          mark: "Mercedes",
          year: "2006",
          doors: "4/5",
          air: "Yes",
          transmission: "Manual",
          fuel: "Diesel",
          co2Emission: this.getRandomCO2Value(),
        },
        "VW Passat CC": {
          price: "25",
          img: "passatcc.jpg",
          model: "Passat CC",
          mark: "Volkswagen",
          year: "2008",
          doors: "4/5",
          air: "Yes",
          transmission: "Automatic",
          fuel: "Gasoline",
          co2Emission: this.getRandomCO2Value(),
        },
      };
    },
    SCOOTER_DATA() {
      return {
        "Scooter Model 1": {
          price: "10",
          img: "scooter-1.png",
          model: "Scooter Model 1",
          brand: "Scooter Brand 1",
          year: "2022",
          maxSpeed: "25 km/h",
          battery: "36V Lithium",
          co2Emission: this.getRandomCO2Value(),
        },
        "Scooter Model 2": {
          price: "12",
          img: "scooter-2.png",
          model: "Scooter Model 2",
          brand: "Scooter Brand 2",
          year: "2023",
          maxSpeed: "30 km/h",
          battery: "48V Lithium",
          co2Emission: this.getRandomCO2Value(),
        },
        // Add more e-scooter data here...
      };
    },
  },
  methods: {
    getRandomCO2Value() {
      return (Math.random() * (200 - 50) + 50).toFixed(2); // Random value between 50 and 200
    },
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
  color: #000;
  /* Replace with your text color */
  max-width: 50rem;
}

.pick-container__title p {
  font-size: 16px;
  /* Replace with your font size */
  font-family: Arial, sans-serif;
  /* Replace with your font-family */
  color: #888;
  /* Replace with your text color */
  line-height: 1.5;
}

.pick-container__title h3 {
  font-size: 24px;
  /* Replace with your font size */
  font-family: Arial, sans-serif;
  /* Replace with your font-family */
  font-weight: 500;
}

.pick-container__title h2 {
  font-size: 32px;
  /* Replace with your font size */
  font-family: Arial, sans-serif;
  /* Replace with your font-family */
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
  background-color: #42b983;
  /* Replace with your desired hover background color */
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
  background-color: #42b983;
  /* Replace with your desired background color */
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
  font-family: Arial, sans-serif;
  /* Replace with your font-family */
  background-color: #42b983;
  /* Replace with your desired background color */
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
