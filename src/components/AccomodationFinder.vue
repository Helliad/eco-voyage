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
      <div class="col-md-6 col-sm-12">
        <div id="searchInput" class="text-center">
            <div class="row ">
              <div class="col-md-6 mb-4 text-start">
                <label for="checkIn" class="form-label text-start fs-6">Check In date:</label>
                <input type="date" id="checkIn" class="form-control" v-model="checkIn"  :min="minCheckInDate"
                  placeholder="Select Check In date" />
              </div>
              <div class="col-md-6 mb-4 text-start">
                <label for="checkOut" class="form-label text-start fs-6">Check Out date:</label>
                <input type="date" id="checkOut" class="form-control" v-model="checkOut" :min="checkIn" 
                  placeholder="Select Check Out date" />
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
        </div>
      </div>
      <div class="col-md-6 col-sm-12">
        <div class="mt-12 mt-lg-0 position-relative">

          <img src="..\..\src\assets\Accomodation.jpeg" alt="online course"
            class="img-fluid rounded-4 w-100 z-1 position-relative">

        </div>
      </div>
    </div>
    <div class="row mt-4 justify-content-center">
      <div class="col-lg-8 col-md-12">
        <div class="text-center">
          <div class="loading-animation" v-if="isLoading">
            <div class="spinner"></div>
          </div>
          <table v-if="showTable" class="table table-hover table-success">
            <thead>
              <tr>
                <th class="custom" colspan="2" id="hotelTable">Accomodation
                </th>
                <th class="custom sortable-header">Rating
                </th>
                <!-- <th class="custom">Review Score
                </th> -->
                <th class="custom">Type
                </th>
                <th class="custom sortable-header">Review Score
                </th>
                <!-- <th class="custom">Review Score
                </th> -->
                <th class="custom sortable-header" @click="sortTable('emissions')">Emissions
                  <span v-if="sortBy === 'emissions'">
                    <span v-if="sortDirection == 'asc'">&#9650;</span>
                    <span v-else-if="sortDirection == 'desc'">&#9660;</span>
                  <!-- <i v-if="sortBy == 'emissions'" class="fas fa-sort-{{sortDirection === 'asc' ? 'up' : 'down'}}"></i> -->
                  </span>
                  <span v-else>&#9650;&#9660;</span> <!-- Double-sided arrow icon -->
                </th>
                <th class="custom">Book Now</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(hotel, index) in hotels" :key="index">
                <td><img :src='hotel.main_photo_url'></td>
                <td>{{ hotel.hotel_name }}</td>
                <td>{{ hotel.stars }}</td>
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
      hotelID: '',
      showTable: false,
      isLoading: false,
      noNights: '',
      hotelEmissionResult: '',
      minCheckInDate: '',
      sortDirection: 'asc',
      sortBy: null
    };
  },
  mounted() {
    const today = new Date();
    today.setDate(today.getDate() + 1); // Set minimum checkIn date as tomorrow
    this.minCheckInDate = today.toISOString().split('T')[0];
  },
  watch: {
    checkIn(newDate) {
      if (newDate && this.checkOut && newDate > this.checkOut) {
        this.checkOut = '';
      }
    },
    checkOut(newDate) {
      if (newDate && this.checkIn && newDate < this.checkIn) {
        this.checkIn = '';
      }
    }
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
          'X-RapidAPI-Key': 'ec30787aecmsha7e44713edd7b72p1739d0jsn0344ed976c69',
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
          // console.log('hi')
        })
    },
    getPropertiesList(dest, dest_type, checkIn, checkOut, adultNo, roomNo, orderSelect) {
      var hotelList = [];
      axios.get('https://apidojo-booking-v1.p.rapidapi.com/properties/list', {
        headers: {
          'X-RapidAPI-Key': 'ec30787aecmsha7e44713edd7b72p1739d0jsn0344ed976c69',
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
          // tempHotelList.push(hotelList[1]);
          // tempHotelList.push(hotelList[2]);
          for (let i in hotelList) {
            let currentHotel = hotelList[i];
            let stars = this.getHotelStars(hotelList[i].class);
            currentHotel["stars"] = stars;
            currentHotel["emissions"] = await this.calculateHotelEmissions(stars);
            this.hotels.push(currentHotel);
          }
          this.showTable = true
          this.isLoading = false
          // console.log('hi') // Update the hotels data property
        })
    },
    getHotelStars(star) {
      if (star == 0 || star == 1) {
        star = 2;
      }
      return star + ' stars'
    },
    async calculateHotelEmissions(stars) {
      const url = 'https://carbonsutra1.p.rapidapi.com/hotel_estimate';
      const options = {
        method: 'POST',
        headers: {
          'content-type': 'application/x-www-form-urlencoded',
          Authorization: 'Bearer fQ98oU704xFvsnXcQLVDbpeCJHPglG1DcxiMLKfpeNEMGumlbzVf1lCI6ZBx',
          'X-RapidAPI-Key': 'ec30787aecmsha7e44713edd7b72p1739d0jsn0344ed976c69',
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
        // console.log("response: ", obj);

        let carbonEmissions = obj.data.co2e_kg;
        return carbonEmissions
      } catch (error) {
        console.error(error);
        return 0
      }
    },
    sortTable(column) {
      // If a different column is clicked, set the sorting column and direction
      if (column !== this.sortBy) {
        this.sortBy = column;
        this.sortDirection = "asc";
      } 
      else {
        // If the same column is clicked, toggle the sorting direction
        this.sortDirection = this.sortDirection == "asc" ? "desc" : "asc";
      }

      // Sort the hotels based on the selected column and direction
      this.hotels.sort((a, b) => {
        const aValue = a[column];
        const bValue = b[column];
        if (this.sortDirection == "asc") {
          return aValue < bValue ? -1 : 1;
        } else {
          return aValue > bValue ? -1 : 1;
        }
      });
    }
},
};
</script>

<style scoped>
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
th.sortable-header span {
  margin-left: 4px;
  font-size: 12px;
  vertical-align: middle;
}

/* Add some styles to the double-sided arrow to make it more prominent */

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}
</style>
