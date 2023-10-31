<template>
  <div id="searchInput">
    <input type="text" id="text" placeholder="Enter a location">
    <input type="text" id="checkIn" placeholder="Check-In(YYYY-MM-DD)">
    <input type="text" id="checkOut" placeholder="Check-Out(YYYY-MM-DD)">
    <input type="text" id="adultNo" placeholder="Number of adults">
    <input type="text" id="roomNo" placeholder="Number of rooms">
    <select id="orderSelect">
      <option value="popularity">Popularity</option>
      <option value="class_descending">Stars (5 to 1)</option>
      <option value="class_ascending">Stars (1 to 5)</option>
      <option value="review_score">Guest Review Score</option>
      <option value="price">Price (low to high)</option>
    </select>
    <button id="searchButton" @click="getDestination">Search Accommodations</button>
  </div>

  <table id="table" class="table table-success">

  </table>
</template>
  
<script>
import axios from "axios";

export default {
  // mounted() {
  //   this.loadGoogleMaps(() => {
  //     this.initMap();
  //   });
  // },
  methods: {
    getPropertiesList(dest, dest_type, checkIn, checkOut, adultNo, roomNo, orderSelect) { //get properties/list
      var hotelList = [];
      axios.get('https://apidojo-booking-v1.p.rapidapi.com/properties/list', {
        headers: {
          'X-RapidAPI-Key': '7ec1836d98msha8273f8dc08549fp1d3979jsn0e2c99c4ef62',
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
          hotelList = response.data.result
          console.log(hotelList)
          document.getElementById('table').innerHTML = '';
          var heading1 = document.createElement('th');
          heading1.textContent = 'Name';
          var heading2 = document.createElement('th');
          heading2.textContent = 'Rating';
          var heading3 = document.createElement('th');
          heading3.textContent = 'Type';
          var heading4 = document.createElement('th');
          heading4.textContent = 'Review Score';
          var heading5 = document.createElement('th');
          heading5.textContent = 'Link to Book';
          var headerRow = document.createElement('tr');
          headerRow.appendChild(heading1);
          headerRow.appendChild(heading2);
          headerRow.appendChild(heading3);
          headerRow.appendChild(heading4);
          headerRow.appendChild(heading5);
          document.getElementById('table').appendChild(headerRow);
          for (var i = 0; i < hotelList.length; i++) {
            var hotelName = hotelList[i].hotel_name;
            var hotelClass = hotelList[i].class;
            var hotelLink = hotelList[i].url;
            var hotelType = hotelList[i].accommodation_type_name;
            var hotelScore = hotelList[i].review_score;
            var hotelScoreWord = hotelList[i].review_score_word;
            console.log(hotelName);
            console.log(hotelClass);
            var row = document.createElement('tr');
            var name = document.createElement('td');
            var star = document.createElement('td');
            var link = document.createElement('td');
            var type = document.createElement('td');
            var score = document.createElement('td');
            name.textContent = hotelName;
            if (hotelClass == 0) {
              star.textContent = '1 stars';
            } else {
              star.textContent = hotelClass + ' stars';
            }
            var linkElement = document.createElement('a');
            linkElement.href = hotelLink;
            linkElement.textContent = 'Book Now!';
            linkElement.target = '_blank';
            type.textContent = hotelType;
            link.appendChild(linkElement);
            score.textContent = hotelScore + ' (' + hotelScoreWord + ')'
            row.appendChild(name);
            row.appendChild(star);
            row.appendChild(type);
            row.appendChild(score);
            row.appendChild(link);
            document.getElementById('table').appendChild(row);
          }
        })
    },
    getDestination() { //get locations/autocomplete
      const url = 'https://apidojo-booking-v1.p.rapidapi.com/locations/auto-complete';
      var location = document.getElementById('text').value;
      var checkIn = document.getElementById('checkIn').value;
      var checkOut = document.getElementById('checkOut').value;
      var adultNo = document.getElementById('adultNo').value;
      var roomNo = document.getElementById('roomNo').value;
      var orderSelect = document.getElementById('orderSelect').value;

      axios.get(url, {
        headers: {
          'X-RapidAPI-Key': '7ec1836d98msha8273f8dc08549fp1d3979jsn0e2c99c4ef62',
          'X-RapidAPI-Host': 'apidojo-booking-v1.p.rapidapi.com'
        },
        params: {
          text: location,
          languagecode: 'en-us'
        }
      })
        .then(response => {
          var stuff = response.data
          var dest = stuff[0].dest_id;
          var searchType = stuff[0].dest_type;
          this.getPropertiesList(dest, searchType, checkIn, checkOut, adultNo, roomNo, orderSelect);
        })
    },
  },
};

// function getPropertiesList(dest, dest_type, checkIn, checkOut, adultNo, roomNo, orderSelect) { //get properties/list
//   var hotelList = [];
//   axios.get('https://apidojo-booking-v1.p.rapidapi.com/properties/list', {
//     headers: {
//       'X-RapidAPI-Key': '7ec1836d98msha8273f8dc08549fp1d3979jsn0e2c99c4ef62',
//       'X-RapidAPI-Host': 'apidojo-booking-v1.p.rapidapi.com'
//     },
//     params: {
//       offset: '0',
//       arrival_date: checkIn,
//       departure_date: checkOut,
//       guest_qty: adultNo,
//       dest_ids: dest,
//       room_qty: roomNo,
//       search_type: dest_type,
//       order_by: orderSelect,
//       languagecode: 'en-us',
//       travel_purpose: 'leisure',
//     }
//   })
//     .then(response => {
//       hotelList = response.data.result
//       console.log(hotelList)
//       document.getElementById('table').innerHTML = '';
//       var heading1 = document.createElement('th');
//       heading1.textContent = 'Name';
//       var heading2 = document.createElement('th');
//       heading2.textContent = 'Rating';
//       var heading3 = document.createElement('th');
//       heading3.textContent = 'Type';
//       var heading4 = document.createElement('th');
//       heading4.textContent = 'Review Score';
//       var heading5 = document.createElement('th');
//       heading5.textContent = 'Link to Book';
//       var headerRow = document.createElement('tr');
//       headerRow.appendChild(heading1);
//       headerRow.appendChild(heading2);
//       headerRow.appendChild(heading3);
//       headerRow.appendChild(heading4);
//       headerRow.appendChild(heading5);
//       document.getElementById('table').appendChild(headerRow);
//       for (var i = 0; i < hotelList.length; i++) {
//         var hotelName = hotelList[i].hotel_name;
//         var hotelClass = hotelList[i].class;
//         var hotelLink = hotelList[i].url;
//         var hotelType = hotelList[i].accommodation_type_name;
//         var hotelScore = hotelList[i].review_score;
//         var hotelScoreWord = hotelList[i].review_score_word;
//         console.log(hotelName);
//         console.log(hotelClass);
//         var row = document.createElement('tr');
//         var name = document.createElement('td');
//         var star = document.createElement('td');
//         var link = document.createElement('td');
//         var type = document.createElement('td');
//         var score = document.createElement('td');
//         name.textContent = hotelName;
//         if (hotelClass == 0) {
//           star.textContent = '1 stars';
//         } else {
//           star.textContent = hotelClass + ' stars';
//         }
//         var linkElement = document.createElement('a');
//         linkElement.href = hotelLink;
//         linkElement.textContent = 'Book Now!';
//         linkElement.target = '_blank';
//         type.textContent = hotelType;
//         link.appendChild(linkElement);
//         score.textContent = hotelScore + ' (' + hotelScoreWord + ')'
//         row.appendChild(name);
//         row.appendChild(star);
//         row.appendChild(type);
//         row.appendChild(score);
//         row.appendChild(link);
//         document.getElementById('table').appendChild(row);
//       }
//     })
// }

// function getDestination() { //get locations/autocomplete
//   const url = 'https://apidojo-booking-v1.p.rapidapi.com/locations/auto-complete';
//   var location = document.getElementById('text').value;
//   var checkIn = document.getElementById('checkIn').value;
//   var checkOut = document.getElementById('checkOut').value;
//   var adultNo = document.getElementById('adultNo').value;
//   var roomNo = document.getElementById('roomNo').value;
//   var orderSelect = document.getElementById('orderSelect').value;

//   axios.get(url, {
//     headers: {
//       'X-RapidAPI-Key': '7ec1836d98msha8273f8dc08549fp1d3979jsn0e2c99c4ef62',
//       'X-RapidAPI-Host': 'apidojo-booking-v1.p.rapidapi.com'
//     },
//     params: {
//       text: location,
//       languagecode: 'en-us'
//     }
//   })
//     .then(response => {
//       var stuff = response.data
//       var dest = stuff[0].dest_id;
//       var searchType = stuff[0].dest_type;
//       getPropertiesList(dest, searchType, checkIn, checkOut, adultNo, roomNo, orderSelect);
//     })
// }



let btn = document.getElementById('searchButton'); //enter button to click
document.addEventListener('keypress', (event) => {
  let keyCode = event.keyCode ? event.keyCode : event.which;
  if (keyCode === 13) {
    btn.click();
  }

});
</script>
  
<style scoped>
#table {
  text-align: center;
}

#searchButton {
  margin: 0 auto;
  display: block;
}

#orderSelect {
  margin: 0 auto;
  display: block;
}

#searchInput {
  text-align: center;
  margin-top: 150px;
}

input {
  margin: 0 auto;
  display: inline-flex;
}

tr {
  background-color: lightgreen;
  border: 1px solid black;
  border-collapse: collapse;
}

a:link {
  background-color: transparent;
}
</style>
  
  