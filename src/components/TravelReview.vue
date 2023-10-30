<template>
    <div class="travel-review col-8 mx-auto">
        <h1>Travel Reviews</h1>
        <div id="carouselExampleControls" class="carousel slide" data-bs-ride="carousel">
            <div class="carousel-inner">
                <div class="carousel-item" v-for="(review, index) in reviews" :key="index" :class="{ active: index === 0 }">
                    <div class="slide-content d-flex flex-column justify-content-between align-items-center">
                    <h3>{{ review.title }}</h3>
                    <p>{{ review.content }}</p>
                    <p>By: {{ review.user }}</p>
                    </div>
                </div>
            </div>
            <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleControls"
                data-bs-slide="prev">
                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Previous</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleControls"
                data-bs-slide="next">
                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Next</span>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            reviews: [
                {
                    title: "Amazing Experience!",
                    content: "Everything we needed before and during the travel were provided promptly. Very good service.",
                    user: "John Doe"
                },
                {
                    title: "Highly Recommended!",
                    content: "Eco-Voyage made travel planning so much simpler and sustainable!",
                    user: "Jane Smith"
                },
                {
                    title: "I love Bali",
                    content: "Everything was top notch. It went beyond our expectations. Thanks Eco-Voyage for helping me enjoy Bali more.",
                    user: "David Johnson"
                },
                {
                    title: "Beautiful Destination",
                    content: "Everything was so perfect that we were able to see all the key destinations of Bali.",
                    user: "Emily Wilson"
                },
                {
                    title: "Memorable Trip",
                    content: "Thanks for helping me create such a well organised itinerary and making the entire trip soo smooth and hassle free.",
                    user: "Michael Brown"
                }
            ]
        };
    }
};
</script>

<style scoped>
.carousel-item {
    padding: 20px;
    border: 1px solid #ccc;
    margin-right: 10px;
}
.carousel-inner {
  /* Set a fixed height for the carousel */
  max-height: 200px; /* Adjust this to your desired height */
}

.slide-content {
    max-height: 200px; /* Set a fixed maximum height for the content */
    overflow-y: auto; /* Add a vertical scrollbar if content exceeds the height */
    padding: 20px;
    border: 1px solid #ccc;
}
.carousel-control-prev-icon,
.carousel-control-next-icon {
  filter: invert(100%);
}
</style>
