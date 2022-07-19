<template>
  <div class="container">
    <div id="app">
     <h1 class="title">List of channels</h1>
            <div class="buttons">
              <div class="btn"  v-for="(category,index) in categories" :key="index" @click="activeCategory=category.name" :class="{'active': activeCategory == category.name}">
              {{category.name}}
            </div>
            </div>
              <input class="input" type="search" placeholder="Поиск" v-model="search">
            <div class="channels" v-if="filterByName.length">    
                    <ChannelCard v-for="(channel,index) in filterByName" :key="index" :channel="channel"></ChannelCard>
            </div>
            <div class="loading" v-else-if="loading">
              <img src="../assets/loading.gif" alt="">
            </div>
            <div class="error" v-else-if="!filterByName.length">
              <p>  Ma'lumot topilmadi</p>
            </div>

  </div>
  </div>
</template>

<script>
import ChannelCard from './ChannelCard.vue';
export default {
    components : {
        ChannelCard
    },
  data() {
    return {
      channels: [],
      categories: [
        {
          name: "All"
        },
        {
          name: "Новостные"
        },
        {
          name: "Кино"
        },
        {
          name: "Премиум"
        },
        {
          name: "Познавательные",
        },
        {
          name: "Спорт"
        },
        {
          name: "Музыка"
        },
        {
          name: "Детские"
        },
        {
          name: "Узбекские"
        }
      ],
      activeCategory: "All",
      search: "",
      loading: false,
    }
  },
  computed : {
    filterByName() {
      return this.channels
        .filter((el) => {
          if (this.activeCategory == "All") {
            return this.channels
          } else {
            return el.categories.some((cat) => cat.name == this.activeCategory);
          }
        })
        .filter((el) => {
          return el.name.toLowerCase().includes(this.search.toLowerCase());
        });
   }
  },
  methods : {
   async getApi() {
    try{
      this.loading = true;
      let response = await fetch("https://api.allplay.uz/api/v1/iptv/channels");
      let jsonData = await response.json();
      this.channels = jsonData.data;
    }
    finally{
      this.loading = false
    }
   }
  },
 mounted() {
    this.getApi()
}
}
</script>

<style>
#app .title {
    color: #fff;
    margin-bottom: 1rem;
}
.buttons {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
}
.btn {
    border: none;
    padding: 8px 15px;
    border-radius: 15px;
    cursor: pointer;
    background: #2A2A2A;
    color: #E1E1E1;
    margin: 0 5px;
    font-size: 18px;
    margin-bottom: 2rem;
    text-transform: uppercase;
}
.btn:first-child {
    margin-left: 0;
}

.channels {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    text-align: center;
}
.channel {
    display: inline-block;
    flex-basis: 16%;
    height: 120px;
    margin: 1.2rem 0.5rem;
    margin-left: 0;
    transition: all ease 0.3s;
}
.channel:hover {
    transform: scale(1.05);
}
.channel-img {
    width: 100%;
    height: 100%;
}

.channel-title {
    color: #fff;
}
.input {
    background: #141414;
    border: none;
    color: #686868;
    outline: none;
    padding: 10px;
    font-size: 18px;
}
.buttons .active  {
    background: #f90;
    color: #292929;
}
.loading {
    color: #fff;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 5rem;
}
.error  {
    color: #f90;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 5rem;
    font-size: 20px;
}
</style>
