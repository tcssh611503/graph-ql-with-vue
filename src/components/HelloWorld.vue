<template>
  <div class="hello">
    <ul>
      <li v-for=" (person,index) in people" :key="index">
        {{person.id}}   {{person.firstname}}  {{person.lastname}}

      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios"
export default {
  name: 'HelloWorld',
  data(){
    return {
      people: []
    }
  },
  async mounted(){
    try{
      var result = await axios({
        method: "POST",
        url: "http://localhost:3000",
        data: {
          query: `{
            people{
              id,
              firstname,
              lastname
            }
          }`
        }

      });
      this.people = result.data.data.people;

    }catch(error){
      console.error(error);
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
