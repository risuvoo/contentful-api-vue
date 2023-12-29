<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3 style="color:red"><span style="color:black">This data providing me by contentful test api: </span>{{fromApi}}</h3>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
    data:()=>({
        fromApi:''
    }),
    mounted() {
        this.fetchData();
    },
    methods:{
      async fetchData(){
          await axios.get(`https://cdn.contentful.com/spaces/${process.env.VUE_APP_CONTENT_SPACE_ID}/entries?access_token=${process.env.VUE_APP_CONTENT_ACCESS_TOKEN}&content_type=test`).then((res)=>{
              if(res.status===200){
                  const {items}=res.data;
                  this.fromApi = items && items.length>0 && items[0].fields?.test

              }
          }).catch((err)=>{
              console.log(err)
          })
      }

    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
