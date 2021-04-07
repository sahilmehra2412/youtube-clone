<template>
    <div class="flex" :class="(isChannel)? 'image-channel-div':null">
        <div class="image">
            <img :class="(isChannel)? 'image-channel':null" :src="video.snippet.thumbnails.medium.url" :alt="video.snippet.title">
        </div>
        <div class="info">
            <span class="title-text">{{title}}</span>
            <span class="channel-name">{{video.snippet.channelTitle}}</span>
            <p class="info-text">{{date}}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Video',
    data(){
        return{
            date: null,
            title: null,
            channel: null,
            isChannel: false
        }
    },
    props: {
        video : Object
    },
    methods: {
        formatDate(){
            let date = new Date(this.video.snippet.publishedAt)
            let new_date = new Date(date)
            this.date = new_date.toLocaleDateString(undefined,{month:'short',day:'2-digit',year: 'numeric'});
        },
        decode(str) {
            return str.replace(/&#(\d+);/g, function(match, dec) {
                return String.fromCharCode(dec);
            })
        }
    },
    updated : function(){
        console.log("updated")
        this.formatDate();
    },
    created: function(){
        console.log("created")
        this.title = this.decode(this.video.snippet.title)
        let str = this.video.id.kind;
        let sub_str = str.substring(str.indexOf('#')+1);
        if (sub_str == 'channel'){
            this.isChannel = true
        }
        this.formatDate();
    }
}
</script>

<style scoped>
    .image{
        width: 320px;
    }
    .flex{
        display: flex;
        margin: 5% 1%;
        color: white;
    }
    .title-text{
        font-weight: 600;
    }
    .info{
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        padding: 0 4%;
    }
    .channel-name{
        margin-top: auto;
    }
    .image-channel{
        border-radius: 50%;
        height: 136px;
    }
    .image-channel-div{
        height: 140px;
    }
</style>