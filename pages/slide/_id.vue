<template>
  <v-container>
    <v-layout class="temp" row wrap>


      <v-flex md12 xs12>
        <!--<v-layout align-space-around justify-space-around  row fill-height fill-width wrap>-->
        <!--<v-flex md12 xs4>-->
        <!--<v-btn color="success">Normal</v-btn>-->
        <!--</v-flex>-->
        <!--<v-flex md12 xs4>-->
        <!--<v-btn color="success">Success</v-btn>-->
        <!--</v-flex>-->
        <!--<v-flex md12 xs4>-->
        <!--<v-btn color="success">Success</v-btn>-->
        <!--</v-flex>-->

        <!--<v-btn color="success">Success</v-btn>-->
        <!--<v-btn color="success">Success</v-btn>-->
        <!--<v-btn color="success">Success</v-btn>-->
        <!--<v-btn color="success">Success</v-btn>-->
        <!--<v-btn color="success">Success</v-btn>-->
        <!--<v-btn color="success">Success</v-btn>-->
        <!--<v-btn color="success">Success</v-btn>-->
        <!--<v-btn color="success">Success</v-btn>-->
        <!--<v-layout align-space-around justify-space-around  row fill-height fill-width>-->
        <!--<v-btn color="success">Previous</v-btn>-->
        <!--<v-btn color="success">Mark</v-btn>-->
        <!--<v-btn color="success">Next</v-btn>-->
        <!--</v-layout>-->

        <!--</v-layout>-->

        <v-item-group>
          <v-container grid-list-md>
            <v-layout wrap>
              <!--{{$route.params.id}}-->

              <v-flex
                v-for="n in Active"
                :key="n"
                xs3
                md3
              >
                <v-item>
                  <v-card class="d-flex align-center card-custom" dark
                          @click="give_label(n)">
                    <div width=100% height=100% style="text-align:center">
                      {{n}}
                    </div>
                  </v-card>
                </v-item>
              </v-flex>
            </v-layout>
          </v-container>
        </v-item-group>



      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  import * as Buffer from "vuetify";

  const axios = require('axios');

  export default {
    data: () => ({

      cors:"https://cors-anywhere.herokuapp.com/",
      sperm_image:null,
      username:"",
      Active:[],
      label: "",
      imageno:"",
      slide:"",
      image_name:"",
      current_slide:""
    }),
    watch:{


    },

    created(){
      console.log("Created")
      this.give_slides()
    },
    methods: {
      give_slides:function()
      {
        const get_sli = 'https://shafieelabdatalabeling.tk/getslides';
        this.username =  this.$route.params.id,
          axios.post(this.cors+get_sli, {headers: {
              'Content-Type': 'application/json',
              'Access-Control-Allow-Origin': '*',
              'Access-Control-Allow-Headers': 'Origin, X-Requested-With, Content-Type, Accept'

            }})

            .then((response) => {
              console.log(response)
              this.Active =  response.data.slides.split(";")
              // var res = response.data.user

              // dispatch({type: FOUND_USER, data: response.data[0]})
            })
            .catch((error) => {
              this.resp= error
              console.error(error)

              // dispatch({type: ERROR_FINDING_USER})
            })


      },
      give_label:function(temp){
        this.current_slide = temp
        this.$router.push({ path: `/slide/${this.current_slide}/${this.username}` })
      }


    },


  }

</script>

<style>

  .card-custom{
    height: 100px;
  }
  @media (max-width: 425px) {
    .temp{
      flex-direction: column
    }
    .card-custom{
      height: 30px;
    }

    .image{
      /* object-fit: cover; */
      /* max-height: 60vh; */
      /* height: 30px; */
      /* width: 30px; */
      /* width: 100v÷w; */
    }
  }
  .image{
    /* object-fit: cover; */
    /* max-height: 60vh; */
    /* height: 80vh; */
    /* width: 80vh; */
    /* width: 100v÷w; */
  }





</style>
