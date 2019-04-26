<template>
  <v-container>
    <v-layout class="temp" row wrap>
      <v-flex md6 xs12>
        <img class="image" :src="sperm_image" :aspect-ratio="1"  alt="">
        </img>

        <!--{{slide_id}}-->
        <!--{{user_id}}-->

      </v-flex>
      <v-flex md6 xs12>
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
              <v-flex
                v-for="n in 12"
                :key="n"
                xs3
                md3
              >
                <v-item>
                  <v-card class="d-flex align-center card-custom" dark
                          @click="give_label(n)">
                    <div width=100% height=100% style="text-align:center">
                      {{Active[n]}}
                    </div>
                  </v-card>
                </v-item>
              </v-flex>
            </v-layout>
          </v-container>
        </v-item-group>

        <v-item-group>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex
                v-for="n in 3"
                :key="n"
                xs4
                md4
              >
                <v-item>
                  <v-card class="d-flex align-center card-custom" dark
                          @click="toggleon(Active1[n])">
                    <div width=100% height=100% style="text-align:center">
                      {{Active1[n]}}
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

      Active:["Saab", "Volvo", "BMW","Saab", "Volvo", "BMW","Saab", "Volvo", "BMW","Saab", "Volvo", "BMW", "Audi"],
      Active1: ["chuck","Previous", "Not Sperm", "Next"],
      label: "",
      imageno:"",
      slide:"",
      image_name:"",
      slide_id:"",
      user_id:""
    }),
    watch:{

      image_name: function () {

        this.get_image(this.image_name)


      }

    },



    created(){
      this.image_name= this.getimagenumber()

      this.slide_id=  this.$route.params.slideid
      this.user_id = this.$route.params.id


    },
    methods: {
      give_label:function(temp){

        console.log(temp)

        let data = {
          'username': this.$route.params.id,
          'image_name': this.image_name,
          "label": temp-1,
          "comment":""
        }

        const get_label = 'https://shafieelabdatalabeling.tk/give_label';


        axios.post(this.cors+get_label, data, {headers: {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Headers': 'Origin, X-Requested-With, Content-Type, Accept'

          }})

          .then((response) => {

            if(response.data.response){

              console.log("success")
              this.sperm_image = ""
              this.image_name= this.getimagenumber()

            }
            // var res = response.data.user






            // dispatch({type: FOUND_USER, data: response.data[0]})
          })
          .catch((error) => {
            this.resp= error
            console.error(error)

            // dispatch({type: ERROR_FINDING_USER})
          })


      },
      getimagenumber:function () {


        console.log(this.$route.params.id)
        let data = {
          'username': this.$route.params.id,
          'slide': this.$route.params.slideid
        }

        const get_image_number_url = 'https://shafieelabdatalabeling.tk/get_image_number';

        // this.$route.params


        axios.post(this.cors+get_image_number_url, data, {headers: {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Headers': 'Origin, X-Requested-With, Content-Type, Accept'

          }})

          .then((response) => {

            if(response.data.response){

              console.log("success")

              this.image_name = response.data.image_name
              return response.data.image_name

            }
            // var res = response.data.user






            // dispatch({type: FOUND_USER, data: response.data[0]})
          })
          .catch((error) => {
            this.resp= error
            console.error(error)

            // dispatch({type: ERROR_FINDING_USER})
          })


      },

      get_image:function (image_name) {


        console.log(this.$route.params.id)
        let data = {
          "image_name": this.image_name
        }

        let data1 = {"image_name":"Ash11_0021_955_930.png"}

        const get_image_url = 'https://shafieelabdatalabeling.tk/get_image';

        // this.$route.params


        // this.sperm_image = axios.post(this.cors+get_image_url, data1, {headers: {
        //     'Content-Type': 'application/json','Access-Control-Allow-Origin': '*',
        //     'Access-Control-Allow-Headers': 'Origin, X-Requested-With, Content-Type, Accept'
        //
        //   }})
        //   .then(response => `data:${response.headers['content-type']};base64,${btoa(String.fromCharCode(...new Uint8Array(response.data)))}`).catch((error) => {
        //     this.resp= error
        //     console.error(error)
        //
        //     // dispatch({type: ERROR_FINDING_USER})
        //   });

        axios.post(this.cors+get_image_url,data, { responseType: 'arraybuffer', headers: {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': '*',
            'Access-Control-Allow-Headers': 'Origin, X-Requested-With, Content-Type, Accept'

          }})

          .then((response) => {


            this.sperm_image= this._imageEncode(response.data)

          })
          .catch((error) => {
            this.resp= error
            console.error(error)

          })


      },


      _imageEncode:function(arrayBuffer) {
        let u8 = new Uint8Array(arrayBuffer)
        let b64encoded = btoa([].reduce.call(new Uint8Array(arrayBuffer),function(p,c){return p+String.fromCharCode(c)},''))
        let mimetype="image/png"
        return "data:"+mimetype+";base64,"+b64encoded
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
