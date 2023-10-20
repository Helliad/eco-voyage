<template>
    <div class="travel-review col-8 mx-auto">
        <h1>Travel Reviews</h1>
        <div id="carouselExampleControls" class="carousel slide" data-bs-ride="carousel row">
            <div class="carousel-inner">
                <div class="carousel-item" v-for="(review, index) in reviews" :key="index" :class="{ active: index === 0 }">
                    <h3>{{ review.title }}</h3>
                    <p>{{ review.content }}</p>
                    <p>By: {{ review.user }}</p>
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
                    title: "Amazing Experience",
                    content: "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
                    user: "John Doe"
                },
                {
                    title: "Highly Recommended",
                    content: "Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.",
                    user: "Jane Smith"
                },
                {
                    title: "Great Service",
                    content: "Nullam id dolor id nibh ultricies vehicula ut id elit.",
                    user: "David Johnson"
                },
                {
                    title: "Beautiful Destination",
                    content: "Donec ullamcorper nulla non metus auctor fringilla.",
                    user: "Emily Wilson"
                },
                {
                    title: "Memorable Trip",
                    content: "Vestibulum id ligula porta felis euismod semper.",
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

.carousel-control-prev-icon,
.carousel-control-next-icon {
  filter: invert(100%);
}
</style>
