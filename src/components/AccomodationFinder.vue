<template>
  <div class="pick-container__title">
    <h2 style="margin-top: 1rem;">Accomodations Finder</h2>
    <h4>Find the perfect accommodations for your next adventure!</h4>
    <p>
      Search, compare, and book hotels that suit your travel needs
    </p>
  </div>
  <div class="container mt-5">
    <div class="row justify-content-center ">
      <div class="col-md-6 ">
        <div id="searchInput" class="text-center">
          <form @submit.prevent="getDestination" class="text-start">
            <div class="row ">
              <div class="col-md-6 mb-4 text-start">
                <label for="checkIn" class="form-label text-start fs-6">Check In date:</label>
                <input type="date" id="checkIn" class="form-control" v-model="checkIn" placeholder="Select Check In date"/>
              </div>
              <div class="col-md-6 mb-4 text-start">
                <label for="checkOut" class="form-label text-start fs-6">Check Out date:</label>
                <input type="date" id="checkOut" class="form-control" v-model="checkOut"
                  placeholder="Select Check Out date"/>
              </div>
            </div>
            <label for="adultNo" class="form-label text-start fs-6">Number of adults:</label>
            <input type="number" id="adultNo" class="form-control mb-4" v-model="adultNo"
              placeholder="Enter the number of adults" />
            <label for="roomNo" class="form-label text-start fs-6">Number of rooms:</label>
            <input type="text" id="roomNo" class="form-control mb-4" v-model="roomNo"
              placeholder="Enter the number of rooms" />
            <label for="orderSelect" class="form-label text-start fs-6">Sort by:</label>
            <select id="orderSelect" class="form-select mb-4" v-model="orderSelect">
              <option value="popularity">Popularity</option>
              <option value="class_descending">Stars (5 to 2)</option>
              <option value="class_ascending">Stars (2 to 5)</option>
              <option value="review_score">Guest Review Score</option>
              <option value="price">Price (low to high)</option>
            </select>
            <button class="btn btn-success" @click="getDestination">Search Accommodations</button>
          </form>
        </div>
      </div>
      <div class="col-md-6">
        
      </div>
    </div>
    <div class="row mt-4 justify-content-center">
      <div class="col-md-8">
        <div class="text-center">
          <div v-if="isLoading" class="loading-animation">
            <div class="spinner"></div>
          </div>
          <table v-if="showTable" class="table table-hover table-success">
            <thead>
              <tr>
                <th class="custom" colspan="2">Accomodation</th>
                <th class="custom">Rating</th>
                <th class="custom">Type</th>
                <th class="custom">Review Score</th>
                <th class="custom">Emissions</th>
                <th class="custom">Book Now</th>  
              </tr>
            </thead>
            <tbody>
              <tr v-for="(hotel, index) in hotels" :key="index">
                <td><img :src='hotel.main_photo_url'></td>
                <td>{{ hotel.hotel_name }}</td>
                <td>{{ getHotelStars(hotel.class) }}</td>
                <td>{{ hotel.accommodation_type_name }}</td>
                <td>{{ hotel.review_score }} ({{ hotel.review_score_word }})</td>
                <td>{{ calculateHotelEmissions(hotel.room_qty, this.noNights) }} kg CO2e</td>
                <td><a :href="hotel.url" target="_blank" class="btn btn-success btn-sm">Book Now</a></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      checkIn: '',
      checkOut: '',
      adultNo: '',
      roomNo: '',
      orderSelect: 'popularity',
      hotels: [],
      hotelEmissions: '',
      hotelID:'',
      showTable: false,
      isLoading: false,
      noNights:'',
      hotelEmissionResult:''
    };
  },
  methods: {
    getDestination() {
      this.isLoading = true
      const checkInDate = new Date(this.checkIn);
      const checkOutDate = new Date(this.checkOut);
      const oneDay = 24 * 60 * 60 * 1000; // One day in milliseconds
      this.noNights = Math.round(
        (checkOutDate - checkInDate) / oneDay
      );
      const url = 'https://apidojo-booking-v1.p.rapidapi.com/locations/auto-complete';

      axios.get(url, {
        headers: {
          'X-RapidAPI-Key': '92fdebb2a2mshc4244c6bda5b0cfp16b5cejsneee1d6ef82d1',
          'X-RapidAPI-Host': 'apidojo-booking-v1.p.rapidapi.com'
        },
        params: {
          text: 'Bali',
          languagecode: 'en-us'
        }
      })
        .then(response => {
          var stuff = response.data;
          var dest = stuff[0].dest_id;
          var searchType = stuff[0].dest_type;
          this.getPropertiesList(dest, searchType, this.checkIn, this.checkOut, this.adultNo, this.roomNo, this.orderSelect);
        })
    },
    getPropertiesList(dest, dest_type, checkIn, checkOut, adultNo, roomNo, orderSelect) {
      var hotelList = [];
      axios.get('https://apidojo-booking-v1.p.rapidapi.com/properties/list', {
        headers: {
          'X-RapidAPI-Key': '92fdebb2a2mshc4244c6bda5b0cfp16b5cejsneee1d6ef82d1',
          'X-RapidAPI-Host': 'apidojo-booking-v1.p.rapidapi.com'
        },
        params: {
          offset: '0',
          arrival_date: checkIn,
          departure_date: checkOut,
          guest_qty: adultNo,
          dest_ids: dest,
          room_qty: roomNo,
          search_type: dest_type,
          order_by: orderSelect,
          languagecode: 'en-us',
          travel_purpose: 'leisure',
        }
      })
        .then(response => {
          hotelList = response.data.result;
          this.hotels = hotelList;
          this.showTable = true
          this.isLoading = false
          console.log(hotelList) // Update the hotels data property
        })
    },
    getHotelStars(star) {
      if (star == 0 || star == 1) {
        star = 2;
      }
      return star + ' stars'
    },
    async calculateHotelEmissions(){
      const url = 'https://carbonsutra1.p.rapidapi.com/hotel_estimate';
      const options = {
        method: 'POST',
        headers: {
          'content-type': 'application/x-www-form-urlencoded',
          Authorization: 'Bearer fQ98oU704xFvsnXcQLVDbpeCJHPglG1DcxiMLKfpeNEMGumlbzVf1lCI6ZBx',
          'X-RapidAPI-Key': '92fdebb2a2mshc4244c6bda5b0cfp16b5cejsneee1d6ef82d1',
          'X-RapidAPI-Host': 'carbonsutra1.p.rapidapi.com',
        },
        body: new URLSearchParams({
          country_code: 'ID',
          number_of_nights: 2,
          number_of_rooms: 2,
          city_name: "Bali",
        }),
      };


      try {
        const response = await fetch(url, options);
        const result = await response.text();
        let obj = JSON.parse(result);
        let carbonEmissions = obj.data.co2e_kg;
        return carbonEmissions
      } catch (error) {
        console.error(error);
        return 0
      }
    }
  },
};
</script>

<style scoped>
/* Add your custom CSS styles here */

label{
  font-size: small !important;
  margin-bottom: 0;
}

#searchInput {
  margin-top: 20px;
}

img {
  width: 100px
}

th {
  background-color: #007BFF;
  color: white;
}

tr {
  background-color: #f5f5f5;
}

tr:nth-child(even) {
  background-color: #e3e3e3;
}

a {
  color: white;
}

a:hover {
  text-decoration: none;
}

.custom {
  background-color: green;
}

.loading-animation {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
}

.spinner {
  border: 4px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  border-top: 4px solid #007BFF;
  width: 30px;
  height: 30px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}</style>
