<template>
    <div class="card card-primary" :class="{'card-payex': theme == 'payex'}" style="max-width: 240px;">
        <div class="card-img">
            <img :src="avatar" alt />
            <div class="icon-container">
                <img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fs3.amazonaws.com%2Fapollo-docs-1.x%2Fimages%2Fslack.png&f=1&nofb=1"
                    v-if="icons.slack">
                <img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fcdn0.iconfinder.com%2Fdata%2Ficons%2Ftraffic%2F500%2Fva0032-512.png&f=1&nofb=1"
                    v-if="icons.phone">
                <img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fcdn3.iconfinder.com%2Fdata%2Ficons%2Fminiglyphs%2F500%2F063-512.png&f=1&nofb=1"
                    v-if="icons.email">
            </div>
        </div>
        <header class="card-header">
            <h3>{{ name }}</h3>
            <p> {{ email }} </p>
            <p> {{ role }} </p>
        </header>
        <div class="card-body">
            <p>{{ bio }}</p>
        </div>
    </div>
</template>
<script>
    export default {
        props: ["theme", "avatar", "icons", "name", "email", "role", "bio"]
    }
</script>
<style>
    .card {
        border: 1px dotted gray;
    }

    .card .card-img {
        position: relative;
    }

    .card .card-img img {
        object-fit: contain;
    }

    .card-payex.card.card-primary {
        background-color: #fff;
    }

    .card-payex.card.card-primary .card-header {
        border-top: 7px solid #2da944;
    }

    .card-payex.card.card-primary .card-header:after {
        content: none;
    }

    .icon-container {
        position: absolute;
        right: 0;
        top: 0;
        padding: 6px;
        background-color: #ffffffa3;
    }

    .card .card-img .icon-container img {
        height: 28px;
        width: 28px;

    }
</style>