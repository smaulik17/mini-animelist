<template>
    <div>
        <img class="img" :src="anime.url" :alt="anime.title">
        <h2 class="title">{{ anime.title }}</h2>
        
        <p class="des">
            <span class="des2">Description:</span>{{ "\n" + anime.des }}
        </p>
        <a href="#" @click.prevent="changeFlag" class="showmore">More details/Hide</a>
    </div>
</template>

<script>
export default{
    name:'Anime.vue',
    props:{
        anime:{
            type:Object,
            required:true
        }
    },
    data(){
        return{
            flag:false
        };
    },
    methods:{
        changeFlag(){
            this.flag=!this.flag;
        }
    }
}
</script>

<style scoped>
.img{
    width:190px;
    height:300px;
    object-fit:cover;
    border:1px solid black;
}
.des{
    transition:height 0.3s ease;
    max-height:55px;
    margin-bottom:5px;
    margin-left:5px;
    overflow:hidden;
    text-overflow:ellipsis;
}
.des2{
    margin-left:5px;
    font-size:15px;
    color:rgb(189, 52, 73);
}
.showmore{
    margin-left:15px;
    width:30px;
    color:purple;
    cursor:pointer;
}
.rating,.title{
    margin-left:5px;
}
.main div{
  min-height:545px;
  border:1px solid black;
  box-sizing:border-box;
  padding:0px;
  margin:0px;
}
</style>