<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <a class="navbar-brand" href="#">TaskMate</a>
        <button type="button" class="navbar-toggler" data-toggle="collapse" data-target="#navbarText" aria-controls="navbarText" aria-expanded="false" aria-label="ナビゲーションの切替">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarText">
            <ul class="navbar-nav mr-auto">
                <li class="nav-item active">
                    <router-link to="/" class="ml-3">Top</router-link>
                </li>
                <li class="nav-item">
                    <router-link to="/about" class="ml-3">About</router-link>
                </li>
                <li class="nav-item">
                    <router-link to="/contact" class="ml-3">Contact</router-link>
                </li>
            </ul>
        </div>
    </nav>
</template>