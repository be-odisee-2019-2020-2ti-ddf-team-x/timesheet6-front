<template>
  <div id="timesheet">
    <form @submit.prevent="getIdToLookup">
        <input type="text" placeholder="id?" v-model="idToLookup" name="idToLookup">
    </form>

      <br/>

    <div v-if=" info == 'error' ">
        Unfortunately, something went wrong<br/><br/>
    </div>
    <div v-else  >
        We have read the <strong>entry with id </strong> {{ info.id }} from the backend:
        <ul>
          <li v-if="info.project"><strong>User:</strong>
            {{ info.project.user.firstName }}
            {{ info.project.user.lastName }}
          </li>
          <li v-if="info.project"><strong>Category:</strong> {{ info.project.category.name }}</li>
          <li v-if="info.project"><strong>Project:</strong> {{ info.project.name }}</li>
          <li><strong>DateTime From:</strong> {{ info.dateTimeFrom }}</li>
          <li><strong>DateTime To:</strong> {{ info.dateTimeTo }}</li>
          <li><strong>Description:</strong> {{ info.description }}</li>
        </ul>
    </div>
    <div>
      <strong>Status: </strong> {{ status }}
    </div>
    <div v-if= " info == 'error' " >
      <strong>Error: </strong> {{ error }}
    </div>
  </div>
</template>

<script>
    import * as axios from "axios";

    export default {
        name: "Timesheet",
        data () {
            return {
                idToLookup: '',
                theUrl: '',
                info: null,
                status: null,
                error: null
            }
        },
        mounted () {
            this.idToLookup = '1'
            this.getIdToLookup()
        },
        methods: {
            getIdToLookup() {
                this.theUrl = 'http://localhost:8080/timesheetrest/' + this.idToLookup
                axios
                    .get(this.theUrl)
                    .then(response => (this.info = response.data,
                                        this.status = response.status) )
                    .catch(error => (this.info = "error",
                                        this.status = error.response.status,
                                        this.error = error.response.data.message ) )
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
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
