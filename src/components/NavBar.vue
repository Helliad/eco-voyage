<template>
    <nav class="navbar navbar-expand-lg fixed-top">
        <a class="navbar-brand ps-4" href="#">ECO-VOYAGE BALI</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav"
            aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav ml-auto">
                <li class="nav-item">
                    <router-link class="nav-link" to="/">Home</router-link>
                </li>
                <li class="nav-item">
                    <router-link class="nav-link" to="/calculator">Emissions Calculator</router-link>
                </li>
                <!-- <li class="nav-item">
                    <a class="nav-link" href="#">Chat with us</a>
                </li> -->
            </ul>
        </div>
    </nav>
</template>

<style>
.navbar-brand {
    font-weight: bold;
    font-size: 1.5rem;
}

.navbar-nav .nav-link {
    font-size: 1.2rem;
}

.navbar {
    background-color: rgba(193, 227, 255, 0.8);
}

/* 
.navbar a{
    color: rgb(225, 225, 225);
} */

.navbar-nav {
    margin-left: auto;
}
</style>
<script>
</script>