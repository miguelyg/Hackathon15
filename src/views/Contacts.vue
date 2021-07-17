<template>
    <section class="section">
    <div class="container">
      <h1 class="title has-text-primary-light">
        Contacts <router-link class="button is-warning" :to="`/crear/`">Agregar </router-link>
      </h1>
        <div class="columns is-multiline is-centered">
            <div class="column is-6 is-narrow" v-for="(usuario, index) in contacts" :key="index">
                <div class="card box has-background-info-light">
                    <div class="card-content">
                        <div class="media">
                            <div class="media-left">
                                <figure class="image is-128x128">
                                <img src="../assets/contact.png" alt="Placeholder image">
                                </figure>
                            </div>
                            <div class="media-content">
                                <p class="title is-4">{{usuario.name}}</p>
                                <p class="subtitle is-6">{{usuario.email}}</p>
                                <p class="subtitle is-6">{{usuario.job}}</p>
                                <div class="level">
                                    <div class="buttons level-item has-text-centered">
                                        <router-link class="button is-warning" :to="`/contacts/${usuario.id}`">Editar </router-link>
                                        <button class="button is-danger" @click="deleteContact(usuario.id)"> Eliminar </button>
                                    </div>  
                                </div>                               
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
  </section>
</template>
<script>
export default {
    data(){
        return{
            message: 'Listar',
            contacts: [],
        };
    },

    methods: {
        async getContacts(){
            const data = await fetch('http://localhost:3000/contacts');
            const info = await data.json();
            this.contacts = info;
        },
        async deleteContact(id){
            const data = await fetch(`http://localhost:3000/contacts/${id}`,{method:'DELETE'});
            const info = await data.json();
            this.contacts = info;
            this.getContacts();
        }
    },

    created(){
        this.getContacts();
        console.log('metodo creado');
    },
};
</script>

<style scoped>

</style>