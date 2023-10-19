<template>
    <h2> Sustainable Itinerary Planner</h2>
    <div class="row row-cols-2 row-cols-md-4" id="card-deck">
        <a class="col mb-4" href="#">
            <div class="card" id="card1">
                <img src="../assets/QuickLinks/hotel.png" class="card-img-top" alt="hotels">
                <div class="card-body">
                    <h5 class="card-title">Accomodations</h5>
                    <!-- <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p> -->
                </div>
            </div>
        </a>
        <a class="col mb-4"  href="#">
            <div class="card"  id="card2">
                <img src="../assets/QuickLinks/activities.png" class="card-img-top" alt="activities">
                <div class="card-body" >
                    <h5 class="card-title">Activities</h5>
                    <!-- <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p> -->
                </div>
            </div>
        </a>
        <a class="col mb-4" href="#">
            <div class="card" id="card3">
                <img src="../assets/QuickLinks/vehicles.png" class="card-img-top" alt="vehicles">
                <div class="card-body">
                    <h5 class="card-title">Eco-Vehicles</h5>
                    <!-- <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p> -->
                </div>
            </div>
        </a>
        <a class="col mb-4" href="#">
            <div class="card" id="card4">
                <img src="../assets/QuickLinks/flights.png" class="card-img-top" alt="flights">
                <div class="card-body">
                    <h5 class="card-title">Choose a flight</h5>
                    <!-- <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p> -->
                </div>
            </div>
        </a>
    </div>
</template>

<style>
h2{
    padding: 30px 0px;
}

#card-deck {
    width: 70%;
    margin: 0 auto;
}

#card-deck a {
    text-decoration: none;
    color: #000;
}

#card-deck div img{
    width: 100px;
    margin: 0 auto;
    padding: 15px;
    padding-bottom: 0px;
}

#card1{
    border: 3px #B57373 solid;
    border-radius: 15px;
}

#card2{
    border: 3px #FFC12E solid;
    border-radius: 15px;
}

#card3{
    border: 3px #1AB35A solid;
    border-radius: 15px;
}

#card4{
    border: 3px #AD5DC9 solid;
    border-radius: 15px;
}
</style>