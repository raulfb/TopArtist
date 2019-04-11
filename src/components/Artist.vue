<template>
<li>
    <h2><a :href="artist.url" target="_blank">{{ artist.name }}</a></h2>
    <img :src="artist.image[2]"></img>
</li>
</template>

<script>
import getArtists from './api'

export default {

}
</script>

<style>

</style>
