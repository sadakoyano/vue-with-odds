<template>
  <div id="app">
      <form @submit.prevent="onSubmit">
        <div>
        <label for="mtype">type</label>
        <input id="mtype" name="type" type="text" v-model="mform.type">
        </div>

        <div>
        <label for="desc">description</label>
        <input id="desc" type="text" v-model="mform.description">
        </div>

        <div>
        <label for="fine">fine</label>
        <input id="fine" type="text" v-model="mform.fine">
        </div>

        <!-- <div>
        <label for="ispaid">paid</label>
        <input id="ispaid" type="text" v-model="mform.ispaid">
        </div>        -->

        <button>{{btnName}}</button>

          

      </form>

      <ul>
        <li v-for="(ticket,index) in tickets" :key="index">
         {{ticket.type}} {{ticket.description}} {{ticket.fine}} {{ticket.ispaid}}
         <button @click="onPaidClick(index)">paid</button>
          <button @click="onDeleteClick(index)">delete</button>
          <button @click="onEditClick(ticket, index)">edit</button>
        </li>
      </ul>
  </div>

  
</template>

<script>
export default {
  name: 'App',
  data() {
      return{
        editId:-1,
        mform:{
          type:'',
          decription:'',
          fine:'',
          ispaid:false
        },
        tickets:[
          // {type:'sss', decription:'ddd', fine:'500', ispaid:false},
          // {type:'aaa', decription:'aaa', fine:'500', ispaid:false},
        ],
        
        
      }
  },
  methods:{
    onSubmit()
    {

          if(this.editId < 0 ) {
            let ticket = {...this.mform}
            this.tickets = [...this.tickets, ticket]
          } else {
            let editTicket = {...this.mform}
            this.tickets[this.editId] = editTicket
            this.tickets.push()

            this.editId = -1
          }
          this.resetForm()

    },
    resetForm(){
        this.mform.type = '',
        this.mform.description='',
        this.mform.fine=''
    },
    onPaidClick(index){
      let mTicket = this.tickets[index]
      mTicket.ispaid = !mTicket.ispaid
      this.tickets[index = mTicket]
      this.tickets.push()
    },
    onEditClick(ticket,index){
      this.editId = index
      this.mform.type = ticket.type
      this.mform.description = ticket.description
      this.mform.fine=ticket.fine
      this.mform.ispaid=ticket.ispaid
    },
    onDeleteClick(index){
        this.tickets.splice(index,1)
    }
    
  } ,
  computed:{
    btnName() { return this.editId < 0 ? "Submit" : "Update"}
      
  
  }
}
</script>

<style>
</style>
