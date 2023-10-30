<template>
    <div class="pick-container__title" style="padding-top: 60px;">
        <h2 style="margin-bottom: -1.5rem">Recommended Eco-friendly Locations</h2>
          <p>
            Choose from one of our compiled sustainable locations to visit for your next
            adventure!
          </p>
        </div>
    <div class="container">
      <div class="card" v-for="(activity, index) in activities" :key="index">
        <a :href="activity.url" target="_blank">
          <img :src="activity.image" :alt="activity.title" style="margin-bottom: -1.5rem"/>
          <div class="card-content">
            <h2 class="card-title">{{ activity.title }}</h2>
          </div>
        </a>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        activities: [
          {
            title: "Spiritual Guidance with Traditional Balinese Healer",
            url:
              "https://www.seeksophie.com/experiences/bali-1-hr-private-reading-with-balinese-healer-oe6z2ekdzn",
              image: "locations/healer.png",
          },
          {
            title: "Munduk: Ancient Jungle Trekking and Remote Waterfalls Adventure",
            url:
              "https://www.seeksophie.com/experiences/bali-full-day-jungle-trekking-and-canoeing-in-tamblingan-lake-banyumala-waterfalls-bali-munduk-o035r874z9",
            image: "locations/munduk.png",
          },
          {
            title: "Make Your Own Silver Jewellery from Scratch in Sidemen",
            url:
              "https://www.seeksophie.com/experiences/bali-make-your-own-silver-jewellery-in-sidemen-o9g5883p5n",
            image: "locations/sidemen.png",
          },
          {
            title: "Saving Bali's Sea Turtles: Join the Conservation Effort",
            url:
              "https://www.seeksophie.com/experiences/bali-bali-sea-turtle-experience-conservation-and-connection-with-ancient-marine-life-oxp5wy3vzr",
            image: "locations/turtle.png",
          },
          {
            title: "Mt Batur Sunrise Jeep | Hot Springs & ATV Add-ons",
            url: "https://www.seeksophie.com/experiences/bali-sunrise-jeep-adventure-tour-oxp5w7xvzr",
            image: "locations/atv.png",
          },
          {
            title: "Fireflies Safari with Local Conservationist",
            url:
              "https://www.seeksophie.com/experiences/bali-fireflies-night-safari-with-the-local-conservationist-oxp5w10vzr",
            image: "locations/fireflies.png",
          },
          {
            title: "Private Mt Batur Sunrise Trek | Unique Route & Boat Ride",
            url: "https://www.seeksophie.com/experiences/bali-caldera-trek-boat-ride-o9g584gpzn",
            image: "locations/batur.png",
          },
          {
            title: "Journey to Mystical Bali Temples with Balinese Healer",
            url:
              "https://www.seeksophie.com/experiences/bali-1-day-tamblingan-jungle-spiritual-journey-oogz4k7x51",
            image: "locations/healer.png",
          },
          {
            title: "Nusa Penida Highlights & Snorkelling | Small Group Trip",
            url:
              "https://www.seeksophie.com/experiences/bali-explore-nusa-penida-small-group-bali-hotel-transfer-omwjy7mxjl",
            image: "locations/snorkel.png",
          },
          {
            title: "Melukat Balinese Purification Ceremony",
            url:
              "https://www.seeksophie.com/experiences/bali-a-balinese-soul-purification-ceremony-ol2zeo0e57",
            image: "locations/purification.png",
          },
        ],
      };
    },
  };
  </script>
  
  <style scoped>
    .container {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-around;
    }
    .card {
      width: calc(40%);
      background-color: #fff;
      border: 1px solid #ccc;
      border-radius: 5px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      margin: 5px;
    }
    .card img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      border-top-left-radius: 5px;
      border-top-right-radius: 5px;
    }
    .card-content {
      padding: 10px;
    }
    .card-title {
      font-size: 20px;
      margin: 0;
    }
    a:link {
  text-decoration: none;
}
  </style>
  
  