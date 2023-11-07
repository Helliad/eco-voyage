<template>
  <div class="container my-5">
    <div class="travel-package">
      <img src="https://via.placeholder.com/400" alt="Travel Package Image" class="travel-package-image">
      <div class="travel-package-details">
        <h1 class="travel-package-title">{{ packageName }}</h1>
        <p class="travel-package-description">{{ packageDescription }}</p>
      </div>
    </div>
    <div class="activities">
      <h2>Activities</h2>
      <div class="activity">
        <h1>{{ activity1Name }}</h1>
        <div class="activity-description">
          <p>Time: 7.30PM - 2.00PM</p>
          <p><strong>Only cooking school with its own organic farm - so you truly have farm-to-table cooking!</strong></p>
          <p>Visit to the local farmers market where you can learn about local produce (for morning session)</p>
          <p>Great for families!</p>
          <p>Bali Farm Cooking School offers a truly special and immersive experience for those looking to learn about
            Balinese cuisine and culture. What sets this cooking school apart is its commitment to organic farming
            practices and its own farm that supplies fresh ingredients for the cooking classes.</p>
          <p>Led by friendly and knowledgeable local chefs, guests not only learn how to prepare traditional Balinese
            dishes, but also get to experience the entire process of where their food comes from - from visiting the
            morning market to observing daily life in Bali's countryside market, to touring the organic farm and
            harvesting fresh ingredients.</p>
          <p>Suitable for all ages, this experience is perfect for families and anyone who wants to learn important
            cooking skills and appreciate the natural resources that nourish our bodies.</p>
        </div>
        <div>
    <button @click="showModal1 = true" class="btn btn-success">Regular Menu</button>
    <button @click="showModal2 = true" class="btn btn-success">Vegan Menu</button><br>
    <a href = "https://www.seeksophie.com/experiences/bali-farm-tour-and-cooking-class-morning-session-o14jnmn85q" class="btn btn-success">Reserve Now!</a>

    <!-- Modal -->
    <div v-if="showModal1" class="modal">
      <div class="modal-content">
        <span class="close" @click="showModal1 = false">&times;</span>
           <p>Base Gede (Traditional spices paste)</p>
            <p>Sayur Urab (mix green salad with coconut and spice)</p>
            <p>Opor Ayam (Balinese Chicken curry)</p>
            <p>Sate Lilit (Traditional Balinese Kebab made with Pork meat and Balinese spice)</p>
            <p>Tuna Sambal Matah (Tuna with Raw Sauce)</p>
            <p>Tempe Asam Manis (Sweet Sour Tempe)</p>
            <p>Pisang Goreng (Our Banana fritters with coconut and melted palm sugar) or Black rice pudding</p>
      </div>
    </div>
    <div v-if="showModal2" class="modal">
      <div class="modal-content">
        <span class="close" @click="showModal2 = false">&times;</span>
        <p>Base Gede (Traditional spices paste)</p>
        <p>Gado Gado (Steamed vegetables with traditional peanut sauce)</p>
        <p>Opor Tempe (Balinese tempe curry)</p>
        <p>Bergedel (fried corn with Balinese spice)</p>
        <p>Tempe Asam Manis (Sweet Sour Tempe)</p>
        <p>Tum Bambu (Young Bambu wrap in Banana Leave)</p>
        <p>Pisang Goreng (Our Banana fritters with coconut and melted palm sugar)</p>
      </div>
    </div>
  </div>
      </div>
      <div class="activity">
        <h3>{{ activity2Name }}</h3>
        <!-- Add content for Activity 2 here if needed -->
      </div>
    </div>
    <div class="last-updated">
      Last updated: {{ lastUpdated }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showModal1: false,
      showModal2: false,
      review: "",
      packageName: 'Travel Package 1',
      packageDescription: 'This is a sample travel package description.',
      activity1Name: 'Farm-to-Table Balinese Cooking | With Visit to Local Market',
      activity2Name: 'Activity 2',
      lastUpdated: '3 days ago',
    };
  },
  methods: {
    submitReview() {
      // Handle the review submission, e.g., send to an API or log to the console
      console.log(this.review);
      this.review = ""; // Reset the textarea
      this.showModal = false; // Close the modal
    }
  },

};
</script>

<style scoped>
.modal {
  display: block; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}

/* Modal Content */
.modal-content {
  background-color: #fefefe;
  margin: 15% auto; /* 15% from the top and centered */
  padding: 20px;
  border: 1px solid #888;
  width: 80%; /* Could be more or less, depending on screen size */
}

/* The Close Button */
.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
.travel-package {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.travel-package-image {
  max-width: 400px;
  max-height: 300px;
  object-fit: cover;
  margin-right: 20px;
}

.travel-package-title {
  font-size: 24px;
  margin-bottom: 10px;
}

.travel-package-description {
  font-size: 16px;
}

.activities {
  margin-bottom: 20px;
}

.activity {
  border: 1px solid #e1e1e1;
  padding: 10px;
  margin-bottom: 10px;
}

.activity h3 {
  font-size: 18px;
  margin-bottom: 5px;
}

.last-updated {
  text-align: right;
  font-size: 14px;
}

.activity-description {
  text-align: left;
}
</style>
