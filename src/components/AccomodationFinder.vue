<template>
        <div class="pick-container__title">
          <h3 style="margin-top: 1rem;">Accomodations Finder</h3>
          <h2>Find the perfect accommodations for your next adventure!</h2>
          <p>
            Search, compare, and book hotels that suit your travel needs       
          </p>
        </div>
  <div class="container mt-5">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <div id="searchInput" class="text-center">
          <input type="text" class="form-control mb-2" v-model="checkIn" placeholder="Check In date" onfocusin="(this.type='date')" onfocusout="(this.type='text')"/>
          <input type="text" class="form-control mb-2" v-model="checkOut" placeholder="Check Out date" onfocusin="(this.type='date')" onfocusout="(this.type='text')"/>
          <input type="text" class="form-control mb-2" v-model="adultNo" placeholder="Number of adults" />
          <input type="text" class="form-control mb-2" v-model="roomNo" placeholder="Number of rooms" />
          <select class="form-select mb-2" v-model="orderSelect">
            <option value="popularity">Popularity</option>
            <option value="class_descending">Stars (5 to 2)</option>
            <option value="class_ascending">Stars (2 to 5)</option>
            <option value="review_score">Guest Review Score</option>
            <option value="price">Price (low to high)</option>
          </select>
          <button class="btn btn-success" @click="getDestination()">Search Accommodations</button>
        </div>
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
                <td>{{ hotel.stars}}</td>
                <td>{{ hotel.accommodation_type_name }}</td>
                <td>{{ hotel.review_score }} ({{ hotel.review_score_word }})</td>
                <td>{{ hotel.emissions }} kg CO2e</td>
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
          'X-RapidAPI-Key': 'c6499acefemsh2f2a7a59a238802p182b7ajsn4dac56ccca3a',
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
        .then(async response => {
          hotelList = response.data.result;
          this.hotels = [];
          //Debug mode
          // let tempHotelList=[]
          // tempHotelList.push(hotelList[0]);
          for (let i in hotelList){
            let currentHotel = hotelList[i];
            let stars = this.getHotelStars(hotelList[i].class);
            currentHotel["stars"] = stars;
            currentHotel["emissions"] = await this.calculateHotelEmissions(stars);
            this.hotels.push(currentHotel);
          }
          this.showTable = true
          this.isLoading = false
          console.log(hotelList) // Update the hotels data property
        })
    },
    getHotelStars(star){
      if(star == 0 || star == 1){
        star = 2;
      }
      return star + ' stars'
    },
    async calculateHotelEmissions(stars){
      const url = 'https://carbonsutra1.p.rapidapi.com/hotel_estimate';
      const options = {
        method: 'POST',
        headers: {
          'content-type': 'application/x-www-form-urlencoded',
          Authorization: 'Bearer fQ98oU704xFvsnXcQLVDbpeCJHPglG1DcxiMLKfpeNEMGumlbzVf1lCI6ZBx',
          'X-RapidAPI-Key': 'c6499acefemsh2f2a7a59a238802p182b7ajsn4dac56ccca3a',
          'X-RapidAPI-Host': 'carbonsutra1.p.rapidapi.com',
        },
        body: new URLSearchParams({
          country_code: 'ID',
          number_of_nights: this.noNights,
          number_of_rooms: this.roomNo,
          city_name: "Bali",
          hotel_rating: stars,
        }),
      };
      try {
        const response = await fetch(url, options);
        const result = await response.text();
        let obj = JSON.parse(result);
        console.log("response: ",obj);

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
#searchInput {
  margin-top: 20px;
}

img {
  width:100px
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

.custom{
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
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>
