<template>
    <div>
        <input placeholder="Search" v-model="q" type="text">
        <button @click="getVideo"><i class="fa fa-search"></i></button>
        <Video v-for="video in youtube_object" :key="video.id.videoId" :video="video"></Video>
    </div>
</template>

<script>

import Video from './Video'
import {api_key} from './_creds'

export default {
    name: 'Videos',
    data () {
        return{
            q : null,
            youtube_object : null,
            api_key : api_key
        }
    },
    methods: {
        getVideo () {
            if (this.q==null){
                return;
            }
            let url = `https://youtube.googleapis.com/youtube/v3/search?part=snippet&q=${this.q}&key=${this.api_key}&maxResults=20`
            fetch(url).then(response=>{
                return response.json()
            }).then(data=>{
                this.youtube_object = data.items
            })
        }
    },
    components: {
        Video
    },
    created(){
        console.log(this.api_key);
    }

}
</script>

<style scoped>
    input{
        width: 25%;
        caret-color: #e1e1e1;
        background: #121212;
        height: 2rem;
        border: none;
        outline: palegreen;
        color: #e1e1e1;
    }
    button{
        height: 2rem;
        border: none;
        background: #454545;
        color: rgba(255, 255, 255, 0.5);
    }
    i{
        width: 3rem;
    }
    input::placeholder{
        color: rgba(255, 255, 255, 0.5);
    }
    input:focus{
        outline: #e1e1e1 2px;
    }
</style>