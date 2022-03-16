
<template>
  <b-container fluid class="p-4 bg-dark" >
      <b-container fluid class="p-4 bg-dark">
          <b-container fluid class="p-4 bg-dark">
              <b-container fluid class="p-4 bg-dark" >
              <b-card align="center" bg-variant="warning">
                  <h2> FORM </h2>
              </b-card>
              </b-container>
                     <b-container> 
                        <b-form-group size="lg">
                        <label>İsim-Soyisim:</label>
                        <b-form-input v-model="name" :state="nameState" placeholder="İSİM GİRİNİZ.." trim></b-form-input>
                        Şifre:  <b-form-input v-model="sifre" placeholder="Şifre Giriniz..." type="password"></b-form-input>
                         Doğum Tarihi:<b-form-input v-model="tarih" placeholder="Tarih Giriniz..." type="date"></b-form-input>
                         Email: <b-form-input  v-model="email" placeholder="Email Giriniz..." type="email"></b-form-input>
                         Açık Adresiniz: 
                         <b-form-textarea v-model="textl" placeholder="Adres Giriniz.." rows="3" no-resize></b-form-textarea>
                         
                        <b-button v-if="!isEditing" @click="create" variant="secondary"> GÖNDER </b-button>     
                        <b-button v-else @click="updateTodo" variant="warning"> Update </b-button>  
                        </b-form-group>   
                        

                    <b-card>
                    <b-card-text>
                        <h3> GİRİLENLER </h3>
                    </b-card-text>
                    
                    <b-card-body>
                       <b-table-simple> 
                             <b-thead>
                                 <b-tr>
                        <b-td>AD</b-td>
                        <b-td>ŞİFRE</b-td>
                        <b-td>TARİH </b-td>
                        <b-td>EMAİL</b-td>
                        <b-td>ADRES </b-td> </b-tr> </b-thead> 
                    
                         <b-tr :key="todo.id" v-for="todo in todos" >  
                
                        <b-td>{{todo.name}}</b-td>
                        <b-td>{{todo.sifre}}</b-td>
                        <b-td>{{todo.tarih}}</b-td>
                        <b-td>{{todo.email}}</b-td>
                        <b-td>{{todo.textl}}</b-td>
                        <b-button variant="secondary" @click="deleteTodo(todo.id)" > DELETE</b-button> 
                        <b-button variant="warning"   @click="editTodo(todo)">EDİT</b-button> 
                          </b-tr>
                          
                       </b-table-simple>     
                     </b-card-body>
                     </b-card>
                     </b-container>
                     </b-container>
          </b-container>
          </b-container>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import axios from 'axios';
export default {
    data() {
        return {
         
            isEditing: false,
            counter:0,
            name:'',
            todos:[],
            selectedTodo: null,
            User:{ name:'', sifre:'',tarih:'',email:'',textl:''},
        }         
    },
    methods: {
        
        create(){
            let newUser = {
                id:this.counter++,
                name: this.name,
                completed: false,
                sifre:this.sifre,
                tarih:this.tarih,
                email:this.email,
                textl:this.textl
               
            }
            console.log(newUser);
    
        axios.post('http://localhost:/',newUser )
      
    .then(response => { 
	console.log(response)
})
.catch(error => {
    console.log(error.response)
});
        }, 
         deleteTodo (userId) {
             let index = this.todos.findIndex(todo => {
                 return todo.id == userId;
             });
                this.todos.splice(index,1)
        },
          updateTodo() {
              this.todos[this.selectedIndex].name = this.name;
              this.todos[this.selectedIndex].sifre = this.sifre;
              this.todos[this.selectedIndex].tarih = this.tarih;
              this.todos[this.selectedIndex].email = this.email;
              this.todos[this.selectedIndex].textl = this.textl;
              this.isEditing= false;

          },
              
          editTodo (todo) {
            console.log(todo.name);
                this.isEditing=true;
                  let index = this.todos.findIndex(todo => {
                 return todo.id == todo.id;  
             });
                this.selectedIndex=index;
        },

          }
          
    }

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
    background-color: rgb(189, 186, 186);
    
}



</style>

