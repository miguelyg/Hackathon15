<template>
    <section class="section">
    <div class="container">
      <h1 class="title has-text-primary-light">
        Contact
      </h1>
        <div class="columns is-multiline is-centered">
            <div class="column is-6 is-narrow">
                <div class="card">
                    <div class="card-content">
                        <div class="media">
                            <div class="media-left">
                                <figure class="image is-128x128">
                                <img src="../assets/contact.png" alt="Placeholder image">
                                </figure>
                            </div>
                            <div class="media-content">      
                                <form @submit.prevent="createContact()">
                                    <div class="field">
                                        <input type="text" class="input is-rounded"  v-model="contact.name">
                                    </div>
                                    <div class="field">
                                        <input type="text" class="input is-rounded"  v-model="contact.email">
                                    </div>
                                    <div class="field">
                                        <input type="text" class="input is-rounded"  v-model="contact.job">
                                    </div>  
                                    <div class="level">
                                        <div class="buttons level-item has-text-centered">
                                            <input type="submit" class="button is-primary" value="Crear">
                                            <router-link class="button is-danger" :to="`/contacts`">Cancelar</router-link>
                                        </div>  
                                    </div>                      
                                </form>                                                                                                                                                                 
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
            message: 'Editar',
            contact: {},
        };
    },

    methods: {
        async createContact(){
        const id = `${this.$route.params.id}`;
            const body = {
                    name: this.contact.name,
                    job: this.contact.job,
                    email: this.contact.email,
            };

            const data = await fetch(`http://localhost:3000/contacts`,{method:'POST',body:JSON.stringify(body), headers: { 'Content-Type': 'application/json' }});
            const info = await data.json();
            this.goContacts();
        },
        goContacts(){
            this.$router.push({ name: 'Contacts' });
        },
    },

    created(){
        console.log('metodo creado');
    },
};
</script>

<style scoped>

</style>