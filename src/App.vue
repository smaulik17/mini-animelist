<template>
  <div class="main" id="app">
    <div v-for="anime in animelist":key='anime.id'>
      <Anime :anime="anime"/>
    </div>
  </div>
</template>

<script>
import Anime from './components/Anime.vue';
import axios from 'axios';
export default{
  name:"App",
  components:{
    Anime
  },
  data(){
    return{
      animelist:[
              {id:1,title:'Naruto'},
              {id:2,title:'Bleach'},
              {id:3,title:'One piece'},
              {id:4,title:'Attack on Titan'},
              {id:5,title:'My Hero Academia'},
              {id:6,title:'Gode Geass'},
              {id:7,title:'Death Note'},
              {id:8,title:'Sousou no Frieren'},
              {id:9,title:'Fullmetal Alchemist: Brotherhood'},
              {id:10,title:'Hunter x Hunter'},
              {id:11,title:"Monster"},
              {id:12,title:"Kusuriya no Hitorigoto"},
              {id:13,title:"Kimi no Na wa."},
              {id:14,title:"Jujutsu Kaisen"},
              {id:15,title:"Bocchi the Rock!"},
              {id:16,title:"Cowboy Bebop"},
              {id:17,title:"Kimetsu no Yaiba"},
              {id:18,title:"Made in Abyss"},
              {id:19,title:"Mushoku Tensei"},
              {id:20,title:"Cyberpunk: Edgerunners"},
              {id:21,title:"Kenpuu Denki Berserk"},
              {id:22,title:"Kimi no Suizou wo Tabetai"},
              {id:23,title:"Shinseiki Evangelion"},
              {id:24,title:"One Punch Man"},
              {id:25,title:"Dragon Ball"}
              ]
  }
  },
  methods:{
    async getPoster(title){
      try{
        const apiurl=`https://api.jikan.moe/v4/anime?q=${encodeURIComponent(title)}`
        const response=await axios.get(apiurl);

        if(response.data.data.length>0){
          const animedata=response.data.data[0];
          return{
            url:animedata.images.jpg.image_url,
            des:animedata.synopsis,
            rating:animedata.score
          };
        }
        else{
          console.warn(`аниме не найдено на Jikan API: ${title}`);
          return null;
        }
      }catch(error){
        console.error(`ошибка в выборе аниме базы для ${title}:`,error);
        return null;
      }
    }
  },
  async mounted(){
    const updataAnimeList=[];
    for(const anime of this.animelist){
      await new Promise(resolve=>setTimeout(resolve,800))
      const jikandata=await this.getPoster(anime.title);
      if(jikandata){
        updataAnimeList.push({
          ...anime,
          url:jikandata.url,
          des:jikandata.des,
          rating:jikandata.rating
        });
      }else{
        updataAnimeList.push({
          ...anime,
          url:null,
          des:"Описание отсутствует",
          rating:"Рейтинг"
        });
      }
    }
    this.animelist=updataAnimeList;
  }
}
</script>

<style scoped>
.main{
  display:grid;
  grid-template-columns:repeat(5,1fr);
  grid-template-rows:repeat(2,1fr);
  width:1100px;
  gap:50px;
  margin:50px 50px 0px 50px;
}
</style>