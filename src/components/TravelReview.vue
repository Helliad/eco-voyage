<template>
    <div class="travel-review mb-4">
        <h2>Travel Reviews</h2>
        <div class="card-container col-7 mx-auto">
            <div class="card mx-3">
                <div class="card-body">
                    <div class="row">
                        <div class="col-3">
                            <img src="../assets/logo.png" alt="User Photo" class="user-photo">
                        </div>
                        <div class="col-9">
                            <h5 class="card-title">{{ reviews[0].name }}</h5>
                            <p class="card-text">{{ reviews[0].review }}</p>
                            <div class="stars">
                                <span v-for="(star, index) in reviews[0].stars" class="star" :key="index"></span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="card">
                <div class="card-body">
                    <div class="row">
                        <div class="col-3">
                            <img src="../assets/logo.png" alt="User Photo" class="user-photo">
                        </div>
                        <div class="col-9">
                            <h5 class="card-title">{{ reviews[0].name }}</h5>
                            <p class="card-text">{{ reviews[0].review }}</p>
                            <div class="stars">
                                <span v-for="(star, index) in reviews[0].stars" class="star" :key="index"></span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            reviews: [
                {
                    name: "John Doe",
                    review: "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
                    stars: 4
                },
                {
                    name: "Jane Smith",
                    review: "Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.",
                    stars: 5
                }
            ]
        };
    }
};
</script>

<style scoped>
.user-photo {
    width: 100%;
    height: auto;
}

.stars {
    color: gold;
}

.star {
    display: inline-block;
    width: 20px;
    height: 20px;
    background-color: gold;
    margin-right: 5px;
}

.card-container {
    display: flex;
}
</style>
