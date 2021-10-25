<template>

<div>
  <Navigation />
  
  <div class="container my-12 mx-auto px-4 md:px-12">
   
<section class="grid gap-6 my-6 md:grid-cols-3">
            <div class="p-6 bg-white shadow rounded-2xl">
                <dl class="space-y-2">
                    <dt class="text-sm font-medium text-gray-500">Tickets </dt>

                    <dd class="text-2xl font-light md:text-6xl">{{tickets.length}} tickets</dd>

                    <dd class="flex items-center space-x-1 text-sm font-medium text-green-500">
                        <span>3% increase</span>

                        <svg class="w-7 h-7" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
  <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M17.25 15.25V6.75H8.75"/>
  <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M17 7L6.75 17.25"/>
</svg>                    </dd>
                </dl>
            </div>

            <div class="p-6 bg-white shadow rounded-2xl">
                <dl class="space-y-2">
                    <dt class="text-sm font-medium text-gray-500">Resolved tickets</dt>

                    <dd class="text-5xl font-light md:text-6xl">0 tickets </dd>

                    <dd class="flex items-center space-x-1 text-sm font-medium text-red-500">
                        <span>7% decrease</span>

                        <svg class="w-7 h-7" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
  <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M17.25 8.75V17.25H8.75"/>
  <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M17 17L6.75 6.75"/>
</svg>                    </dd>
                </dl>
            </div>

            <div class="p-6 bg-white shadow rounded-2xl">
                <dl class="space-y-2">
                    <dt class="text-sm font-medium text-gray-500">Ticket resolution Score</dt>

                    <dd class="text-5xl font-light md:text-6xl">21%</dd>

                    <dd class="flex items-center space-x-1 text-sm font-medium text-green-500">
                        <span>2% increase</span>

                        <svg class="w-7 h-7" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
  <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M17.25 15.25V6.75H8.75"/>
  <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M17 7L6.75 17.25"/>
</svg>                    </dd>
                </dl>
            </div>
            
        </section>
        <!-- Column -->
        <div class="my-1 px-1 w-full md:w-1/2 lg:my-4 lg:px-4 lg:w-1/3">
        </div>
   
   <div class="flex items-center">
    <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6 mr-2 text-dark-600" fill="none" viewBox="0 0 24 24"
        stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
            d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
    </svg>
    <input type="text"  v-model="code" name="search" placeholder="search by ticket code"
        class="w-1/2 py-2 border-b-2 border-blue-400 outline-none focus:border-green-400">
</div>
   <br>
    <!-- This example requires Tailwind CSS v2.0+ -->
    <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
      <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
        <div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
          <table class="min-w-full divide-y divide-gray-200">
            <thead class="bg-white">
              <tr>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  CODE
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  STATUS
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  TITLE
                </th>
                <!-- <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  CONTENT
                </th> -->
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  USERS
                </th>
                 <!-- <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  ASSIGNED TO
                </th> -->
                 <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  TIMESTAMPS
                </th>
                 <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  ACTION
                </th>
                <th scope="col" class="relative px-6 py-3">
                  <span class="sr-only">Edit</span>
                </th>
              </tr>
            </thead>
            <tbody class="bg-white divide-y divide-gray-200">
              <tr v-for="ticket of filteredTickets" :key="ticket.id">
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="flex items-center">
                    <div class="flex-shrink-0 h-10 w-10">
                      <img class="h-10 w-10 rounded-full" src="../assets/tkt.svg" alt="">
                    </div>
                    <div class="ml-4">
                      <div v-if="ticket.status==='Resolved'" class="text-sm line-through font-medium text-green-900">
                        {{ticket.code}}
                      </div>
                      <div v-else class="text-sm  font-medium text-gray-900">
                        {{ticket.code}}
                      </div>
                      <div v-if="ticket.priority ==='High'" class="text-sm text-red-500">
                      {{ticket.priority}}
                      </div>
                      <div v-if="ticket.priority ==='Medium'" class="text-sm text-purple-500">
                      {{ticket.priority}}
                      </div>
                      <div v-if="ticket.priority ==='Low'" class="text-sm text-yellow-900">
                      {{ticket.priority}}
                      </div>
                    </div>
                  </div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap">
                  <span v-if="ticket.status !='Resolved'" class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-pink-100 text-pink-800">
                    {{ticket.status}}
                  </span>
                   <span v-else class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">
                    {{ticket.status}}
                  </span>
                  <!-- <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-red-100 text-red-800">
                    NOT PAID {{entry.room.monthly_rent}}
                  </span> -->
                </td>
                <td class="px-6 py-4 ">
                  <div class="text-sm text-gray-900"> {{ticket.title}}</div>
                  <div class="text-sm text-gray-500">{{ticket.content}}</div>
                </td>
                <!-- <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                   {{ticket.content}}
                </td> -->
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="text-sm text-gray-900"><small>CREATED BY</small> {{ticket.created_by.first_name}}</div>
                  <div class="text-sm text-gray-900"><small>ASSIGNED TO</small> {{ticket.assigned_to.first_name}}</div>
                  <!-- <div v-if="ticket.status ==='Resolved'" class="text-sm text-green-900"><small>RESOLVED BY</small> {{ticket.created_by.first_name}}</div> -->
                </td>
                <!-- <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                   {{ticket.assigned_to.first_name}}
                </td> -->
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="text-sm text-gray-900"><small>CREATED</small> {{ticket.created_at | formatDate }}</div>
                   <div v-if="ticket.status ==='Resolved'" class="text-sm text-gray-900"><small>RESOLVED</small> {{ticket.resolved_at | formatDate }}</div>
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                  <a v-if="ticket.status!='Resolved'" @click="resolveTicket(ticket.id)" class="text-green-600 hover:text-green-900">Resolve</a>
                 <a v-if="ticket.status==='Resolved'" @click="reopenTicket(ticket.id)" class="text-yellow-600 hover:text-yellow-900">Reopen</a>
               |  <a @click="deleteTicket(ticket.id)" class="text-red-600 hover:text-red-900">Delete</a>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  
</div>
<br>

</div>
</template>
<script>
import Navigation from '@/components/Navigation.vue'
import axios from 'axios'
export default {
  components:{Navigation},
  data(){
    return{
      code: '',
      user:null,
      tickets:[],
      currentTicket:null,
    }
  },
  computed: {
    filteredTickets() {
      return this.tickets.filter((ticket) => {
        return ticket.code.toLowerCase().includes(this.code.toLowerCase());
      });
    },
  },
  methods:{
    getTickets(){
      return axios.get('http://3.21.27.168/tickets').then(res=>{
        console.log(res)
        this.tickets=res.data
      }).catch(error=>{
        console.log(error)
      })
    },
    resolveTicket(id){
      
      return axios.get(`http://3.21.27.168/tickets/${id}/`).then(res=>{
        let assigned_to=res.data['assigned_to'].id
        let created_by=res.data['created_by'].id
        this.currentTicket=res.data
        this.currentTicket['status']='Resolved'
        this.currentTicket['created_by']=created_by
        this.currentTicket['assigned_to']=assigned_to
        this.currentTicket['resolved_by']=this.user.id
        this.currentTicket['resolved_at']=new Date()
        console.log(this.currentTicket)
        axios.put(`http://3.21.27.168/tickets/${id}/`, this.currentTicket).then(res=>{
          this.getTickets()
        }).catch(error=>{
          console.log(error)
        })
        // this.getTickets()
      })
    },
    reopenTicket(id){
      
      return axios.get(`http://3.21.27.168/tickets/${id}/`).then(res=>{
        let assigned_to=res.data['assigned_to'].id
        let created_by=res.data['created_by'].id
        this.currentTicket=res.data
        this.currentTicket['created_by']=created_by
        this.currentTicket['assigned_to']=assigned_to
        this.currentTicket['status']='Open'
        console.log(this.currentTicket)
        axios.put(`http://3.21.27.168/tickets/${id}/`, this.currentTicket).then(res=>{
          this.getTickets()
        })
        // this.getTickets()
      })
    },
    deleteTicket(id){
      return axios.delete(`http://3.21.27.168/tickets/${id}/`).then(res=>{
        this.getTickets()
      })
    }
  },
  created(){
    this.getTickets()
    this.user =JSON.parse(localStorage.getItem('loggedUser'))
  }
}
</script>