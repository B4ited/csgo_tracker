<template>
  <section>
    <div v-if="loading">
      <h3>Loading...</h3>
    </div>

    <div v-if="error">
      <h1>{{error}}</h1>
      <router-link to="/">Go Back</router-link>
    </div>

    <div v-if="profileData" class="container">
      <h1 class="gamertag">
        <img :src="profileData.platformInfo.avatarUrl" alt class="platform-avatar"/>
        <p> {{profileData.platformInfo.platformUserHandle}}</p>
      </h1>
      <div class="grid">
        <div>
        </div>
        <div>
          <ul>
            <li>
              <h4>Wins</h4>
               {{profileData.segments[0].stats.wins.value}}
            </li>
            <li>
              <h4>K/D</h4>
              {{profileData.segments[0].stats.kd.displayValue}}
            </li>
            <li >
              <h4>Kills</h4>
              {{profileData.segments[0].stats.kills.value}}
            </li>
            <li >
              <h4>Headshots</h4>
            
                {{profileData.segments[0].stats.headshotPct.displayValue}}
            
            </li>
            <li >
              <h4>Time Played</h4>
              
              {{profileData.segments[0].stats.timePlayed.displayValue}}


            </li>
          </ul>
        
        </div>
        <div class="rank">
        
             
          
              
       </div> 
      </div>


      <router-link to="/">Go Back</router-link>
    </div>
  </section>
</template>
<script>


  //var score=0;
  import axios from 'axios';
  

  
  export default{
    name:'Profile',
    data(){
      return{
        loading: false,
        error: null,
        profileData: null
      };
    },
  async created() {
    this.loading = true;
    try {
      const res = await axios.get(
        `/api/v1/profile/${this.$route.params.platform}/${this.$route.params.gamertag}`
      );
      this.profileData = res.data.data;
      console.log(this.profileData);
      var score=this.profileData.segments[0].stats.score.value;
      this.loading = false;


    
     //
    } catch (err) {
      this.loading = false;
      this.error = err.response.data.message;
    }
     console.log(score);
   
     
  }
};
 





</script>

<style>
  <style scoped>
.container {
  background: rgba(0, 0, 0, 0.5);
  color: #fff;
  max-width: 700px;
  margin: 1rem auto;
  padding: 2rem 1.5rem;
  border-radius: 20px;
}

h1.gamertag {
  font-size: 2rem;
  background: rgba(0, 0, 0, 0.6);
  padding: 0.3rem 0.5rem;
  text-align: center;
  border-radius: 20px;
  margin-bottom: 3rem;
  display: flex;
  align-items: center;
}
a {
  display: inline-block;
  margin-top: 2rem;
  border: #fff 2px solid;
  padding: 0.5rem 0.8rem;
}
a:hover {
  border: #ccc 2px solid;
  color: #ccc;
}

.grid {
  display: flex;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 1rem;
}
li {
  background: rgba(0, 0, 0, 0.6);
  padding: 1rem;
  margin-bottom: 0.7rem;
  border-radius: 10px;
}
li p {
  font-size: 2rem;
}
li:first-child p {
  font-size: 1.5rem;
}
li span {
  font-size: 1rem;
  color: #ccc;
}
@media (max-width: 500px) {
  h1 {
    font-size: 1.5rem;
    display: block;
    text-align: center;
  }
  .platform-avatar {
    display: none;
  }
  .grid {
    grid-template-columns: 1fr;
  }
  li p {
    font-size: 1.5rem;
  }
}
.rank{
  margin: auto;
} 
</style>

 <<!-- h2>Lifetime Overview</h2>
          <p> Kills</p>
          {{profileData.segments[0].stats.kills.value}}
           <h2> K/D</h2>
           <p>{{profileData.segments[0].stats.kd.displayValue}}</p> 
          <h2>Wins</h2>
            <p>{{profileData.segments[0].stats.wins.value}}</p>  
          <h2>Headshots %</h2>
          <p>{{profileData.segments[0].stats.headshotPct.displayValue}}</p> 
        </div>
        <router-link to="/">Go Back</router-link> -->