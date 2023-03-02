<script setup lang="ts">
import ChampionRow from "../components/ChampionRow.vue" 
</script>

<template>
  <main id="champion-guess" class="px-3">
   <form id="cform" action="#" @submit.prevent="btnclick">
    <div class="form-group">
      <label for="exampleInputEmail1">Champion</label>
      <input v-model="guessedchampion" id="champ" type="text" class="form-control" aria-describedby="emailHelp" placeholder="Champion">
    </div>
    <button class="btn btn-primary" id="sform">Submit</button>
  </form>
  <table id="chlist" style="width: 100%;">
    <ChampionRow :selectedchampion="selectedchampionobj" v-for="champion in showedchampions" :champion="champion"/>
  </table>
</main>
</template>
<script lang="ts">
  import champions from "./champions.json"
  var champs = {};
  var champ_names = [];
  export default {
    data() {
      return {
        guessedchampion: "",
        selectedchampion: "",
        selectedchampionobj: null,
        showedchampions: [],
      }
    },
    components: {ChampionRow},
    methods: {
      btnclick() {
        if(this.selectedchampion == ""){
          this.selectedchampion = champ_names[Math.floor(Math.random() * champ_names.length)];
          this.selectedchampionobj = champs[this.selectedchampion];
          console.log(this.selectedchampionobj);
        }
        if(this.guessedchampion != $("#champ").val()){
          this.guessedchampion = $("#champ").val();
        }
        if(this.selectedchampion == this.guessedchampion){
          alert("congrats!!!");
        }
        if(champ_names.includes(this.guessedchampion)){
          this.showedchampions.unshift(champs[this.guessedchampion]);
          console.log(this.showedchampions);
        }else{
          alert(this.guessedchampion +" wrong champ")
        }
        // alert(this.selectedchampion);
      }
    },
    mounted(){
      champions.forEach(function(item){
        champ_names.push(item["name"]);
        champs[item["name"]] = item;
        $("#champ").autocomplete({
          source: champ_names
        });
      });
    }
  }
</script>

