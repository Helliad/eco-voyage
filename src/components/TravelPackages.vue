
<template>
    <h2> Travel Packages </h2>
    <div class="travelpackage row row-cols-1 row-cols-md-3 g-4">
      <div class="col" v-for="(travelPackage, index) in travelPackages" :key="index">
        <div
          class="card h-100"
          @mouseenter="hoveredPackage = index"
          @mouseleave="hoveredPackage = null"
          :class="{ 'hovered': hoveredPackage === index }"
        >
          <img :src="require(`@/assets/${travelPackage.imageUrl}`)" class="card-img-top" alt="...">
          <div class="card-body">
            <h5 class="card-title">{{ travelPackage.title }}</h5>
            <p v-if="hoveredPackage === index" class="card-text">{{ travelPackage.description }}</p>
          </div>
          <div class="card-footer" v-if="hoveredPackage === index">
            <a href="/TravelPackage1" class="btn btn-success">Find out more!</a>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <style>
  .travelpackage {
    margin-top: 15px;
  }
  .card {
    transition: transform 0.2s ease-in-out;
  }
  
  .card.hovered {
    transform: scale(1.05); /* Increase the card size on hover */
  }
  
  .card-footer {
    display: none; /* Hide the card footer by default */
  }
  
  .card.hovered .card-footer {
    display: block; /* Show the card footer when hovered */
  }
  </style>
  
  <script>
  export default {
    data() {
      return {
        hoveredPackage: null, // Initialize to null when no package is hovered
        travelPackages: [
          {
            title: "Day Package",
            description: "This is a wider card with supporting text below...",
            imageUrl: "ubug.png",
            updatedAt: "3 mins ago"
          },
          {
            title: "3 Day Package",
            description: "This card has supporting text below...",
            imageUrl: "Package2.png",
            updatedAt: "3 mins ago"
          },
          {
            title: "2 Day Package",
            description: "This is a wider card with supporting text below...",
            imageUrl: "Package3.png",
            updatedAt: "3 mins ago"
          }
          // Add more travelPackage objects as needed
        ]
      };
    }
  };
  </script>
  
  
  