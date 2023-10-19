<template>
    <div class="landingpage">
        <div class="jumbotron position-relative">
            <img src="..\..\src\assets\jumbotron_img.png" alt="Image description">
            <div class="position-absolute top-0 translate-middle text-start rounded shadow p-3 " id="jumbo-text">
                <h1 class="display-4">Discover Bali's Natural Wonders</h1>
                <p class="lead">And Preserve Its Future</p>
                <!-- <hr class="my-4">
                <p>Feel free to explore and learn more about Vue.js.</p>
                <a class="btn btn-primary btn-lg" href="#" role="button">Learn more</a> -->
            </div>
        </div>
    </div>
</template>

<style>
.jumbotron {
    background-color: #f8f9fa;
}

.jumbotron img {
    width: 100%;
}

#jumbo-text{
    margin-top: 20%;
    margin-left:40%;
    color:rgb(240, 240, 240);
    background-color:  rgba(63, 74, 84, 0.2);
}


</style>