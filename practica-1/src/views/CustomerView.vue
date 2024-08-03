<template>
  <div>
    <h1>{{ title }}</h1>
    <!-- <p >Filtro :<input v-model="searchQuery" placeholder="Buscar..."> </p> -->

    <div class="filtro">
        Filtro:  <input type="search" v-model="textoBusar"  placeholder="Buscar..." />
    </div>


    <table>
            <thead>
                <tr>
                    <th>Id</th>
                    <th>Name</th>
                    <th>Email</th>
                    <th>address</th>
                    <th>Phone</th>
                    <th>country</th>
                    <th>city</th>
                    <th></th>
                </tr>
                <tr>
                    <th><input type="text" v-model="customerNew.id"></th>
                    <th><input type="text" v-model="customerNew.name"></th>
                    <th><input type="text" v-model="customerNew.email"></th>
                    <th><input type="text" v-model="customerNew.address"></th>
                    <th><input type="text" v-model="customerNew.phone"></th>
                    <th><input type="text" v-model="customerNew.country"></th>
                    <th><input type="text" v-model="customerNew.city"></th>
                    <th><button @click="save()">Nuevo</button></th>
                </tr>
                <tr v-if="indexToEdit !== null">
                    <th><input type="text" v-model="customerEdit.id"></th>
                    <th><input type="text" v-model="customerEdit.name"></th>
                    <th><input type="text" v-model="customerEdit.email"></th>
                    <th><input type="text" v-model="customerEdit.address"></th>
                    <th><input type="text" v-model="customerEdit.phone"></th>
                    <th><input type="text" v-model="customerEdit.country"></th>
                    <th><input type="text" v-model="customerEdit.city"></th>
                    <th><button @click="saveEdit()">Guardar</button></th>
                </tr> 
            </thead>
            <tbody>
                <tr v-for="(customer, index) in listCustomerComputada" :key="customer.id">
                    <td>{{customer.id}}</td>
                    <td>{{customer.name}}</td>
                    <td>{{customer.email}}</td>
                    <td>{{customer.address}}</td>
                    <td>{{customer.phone}}</td>
                    <td>{{customer.country}}</td>
                    <td>{{customer.city}}</td>
                    <td>
                        <button @click="deleteCustomer(index)">Eliminar </button> <span> | </span>
                        <button @click="edit(customer, index)">Editar</button> 
                    </td>
                </tr>
            </tbody>
        </table>
  </div>
</template>

<script>
import { ref, computed } from 'vue';
export default {
  name: 'MiComponente',
  data() {
    return {
        title: 'Register Customer',
        textoBusar: '',
        customerNew:{ id:"", name:"", email:"", address: "", phone: "", country: "", city:"" },
        customerEdit:{id:"", name:"", email:"", address: "", phone: "", country: "", city:"" },
        customersCopy:{id:"", name:"", email:"", address: "", phone: "", country: "", city:"" },
        indexToEdit:null, 
        searchQuery: null,
        customers: [
	        { id: "1", name:"Raul Flores", email:"raul@gmail.com", address:"Av Central nro 652", phone:"700-26531", country:"Bolivia", city:"Santa Cruz"},
	        { id: "2", name:"Miran Caseres", email:"mirian@gmail.com", address:"Av Bolivar", phone:"602-23562", country:"Bolivia", city:"Sucre"},
            { id: "3", name:"Ximena Vargas", email:"xvargas@gmail.com", address:"Av Iral nro 65", phone:"660-75251", country:"Bolivia", city:"Santa Cruz" },
	        { id: "4", name:"Fernanda Lopez", email:"fernanda@gmail.com", address:"Av Avaroa 452", phone:"600-00252", country:"Bolivia", city:"La Paz" },
	        { id: "5", name:"Alexander Carrillo", email:"a_carrillo@gmail.com", address:"Av Rosas 652", phone:"602-56244", country:"Bolivia", city:"Tarija"},
        ],
    }
  },
  components: {
    // Registro de componentes que se utilizaran.
  },
  methods: {
    // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
    save(){
        this.customers.push(Object.assign({}, this.customerNew));
    },
    deleteCustomer(index){
        this.customers.splice(index,1);
    },
    saveEdit(){
        this.customers[this.indexToEdit] = Object.assign({}, this.customerEdit)
        this.indexToEdit = null;
    },
    edit(customer, index){
        this.indexToEdit = index;
        this.customerEdit = Object.assign({},customer);
    },

  },
  computed: {
    // propiedades computadas que dependen de otras propiedades reactivas
    listCustomerComputada(){
        return this.customers.filter(item => item.name.toLowerCase().includes(this.textoBusar.toLowerCase())||item.id.toLowerCase().includes(this.textoBusar.toLowerCase()));
    } 
  },
  props: {
    // propiedades que el componente puede recibir.
  },
  emits: [] // los eventos personalizados que el componente puede emitir.
}
</script>

<style scope>
h1 {
    color: #42b983;
}
table {
    width: 100%;
    border-collapse: collapse;
}
th, td {
    border: 1px solid #ddd;
    padding: 8px;
}
th {
    background-color: #f2f2f2;
    text-align: left;
}
p{
    text-align: left;
}
</style>