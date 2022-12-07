<script setup lang="ts">
</script>
<template >
    <section  v-on:load="usr()">
    <div>

<form class="form-floating" method="POST"  >
        
            <div class="modal-body">
                <label class="p-2">nom</label>
                <input type="text" class="form-control" nom="nom" id="nom" v-model="nom" placeholder="nom">
        
                <label class="p-2">prenom</label>
                <input type="text" class="form-control" nom="prenom" id="prenom" placeholder="prenom" v-model="prenom">
                <label class="p-2">email</label>
                <input type="email" class="form-control" nom="email" id="email" placeholder="email" v-model="email">
                <br>
        
                <div class="modal-footer m-2">
                    <button type="reset" class="btn btn-danger" data-bs-dismiss="modal">Annuler</button>
                    <button type="button" v-on:click="update(nom,prenom,email)" class="btn btn-success" id="submit">modifier</button>
                </div>
            </div>
        
        </form>
    </div>
    </section>
</template>
<script>
import axios from "axios";

const baseURL = 'http://127.0.0.1:8000/api/personne/';

export default {
    nom: "Liste",
    data() {
        return {
            todos: [],
            nom: "",
            prenom: "",
            email: "",
            id: this.$route.params.id,
        };
        
    },
   
    async created() {
        try {
            const res = await axios.get(baseURL);

            this.todos = res.data;
        } catch (e) {
            console.error(e);
        }

    },
    methods: 
    {
       
        async usr() {
            const res = await axios.get('http://127.0.0.1:8000/api/personne/' +this.id);
            this.todos = res.data;

        },
        async supp(id) {
            //    let resp= await axios.get('http://localhost:3000/user/1');
            //    console.log(resp.data);
            axios.delete('http://127.0.0.1:8000/api/personne/' + id);
            const res = await axios.get(baseURL);

            this.todos = res.data;


        },

      





        async update(nom,prenom,email) {
            
                let res = await axios.put(baseURL+this.id, { nom: nom, prenom: prenom, email: email });


                
               
        
            window.location.href = "/"
        }

    }
};
</script>



        
    