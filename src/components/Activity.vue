<template>
  <v-container fill-height>
    <v-row align-center>
      <v-slide-y-transition>
        <v-card-text class="text-center display-3 mb-3 hei" v-show="show">
          WHAT IS SIEYOR DOING NOW?
        </v-card-text>
      </v-slide-y-transition>
    </v-row>
    <v-row>
      <v-card-actions class="max-width justify-center">
      <v-btn
              elevation="2"
              class="purple"
              style="width: 70%;height: 70px"
              @click="loadActivity"
      >{{ this.checked ? 'CHECK AGAIN' : 'CHECK' }}</v-btn>
      </v-card-actions>
    </v-row>
    <v-row>
      <v-card-text>
        <v-card-text class="text-center display-1 mb-3" v-show="show">
          {{this.type}} <p v-if="type == 'LISTENING'">TO</p>
        </v-card-text>
        <v-card-text style="width: 100%" v-show="show">
          <Roller class="max-width text-center display-3 roller" :transition="3" :charList=this.charList :text=this.name ></Roller>
        </v-card-text>
        <v-card-text class="text-center display-1 mb-3" v-show="show">
          {{this.action}}
        </v-card-text>
      </v-card-text>
    </v-row>
  </v-container>
</template>

<script>
  import Roller from "vue-roller";

  const axios = require('axios');

  export default {
    name: 'Activity',
    components:{
      Roller
    },
    data: () => ({
      show: false,
      checked: false,
      action: "",
      type: "",
      name: "",
      charList: ['0','1','2','3','4','5','6','7','8','9',
              'A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','X','Y','Z',
        'a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','x','y','z']
    }),
    mounted() {
      setTimeout(() => this.show = true, 500);
    },
    methods:{
       async loadActivity(){
         this.action =  ''
         this.type = ''
         this.name  = ''
         this.loadSteam()
         this.checked = true


      },

      async loadSteam(){
        const response = await axios
                .get('https://roachbot-296601.ue.r.appspot.com/users')

        const status = response.data.status[0];
        this.name = status.name.toUpperCase()
        setTimeout(() => {
            this.type = status.type.toUpperCase()
            this.action = status.action.toUpperCase().replace(";",",")
        }, 3000);

      },
    }
  }
</script>
<style scoped>
    .slide-fade-enter-active,
    .slide-fade-leave-active {
        transition: all 1s cubic-bezier(1, 0.5, 0.8, 1);
    }

    .slide-fade-enter-from,
    .slide-fade-leave-to {
        transform: translateX(30px);
        opacity: 0;
    }
    .roller .rollerBlock {
        font-family: "Open Sans", sans-serif;
        font-size: 2em;
        margin: 20px;
        width: auto;
    }
    .max-width {
        width: 100%;
    }
    .height{
        height: 200px;
    }


</style>
