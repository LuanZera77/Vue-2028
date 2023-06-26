<template>
    <div id="sobre">
            
            <h1>
                <img class="logo" src="/img/logo-Marvel.webp" alt="logo" width="200px">
            </h1>

            <hr>

            <div class="container">
          

                <div class="row justify-content-center">
                    <span class="col-3" v-for="personagem in personagens" :key="personagem.id">
                        
                            <div class="card ">
                            <img :src="personagem.thumbnail.path+'.'+ personagem.thumbnail.extension" class="card-img-top" alt="...">
                            <div class="card-body">
                                <h5 class="card-title">{{personagem.name}}</h5>
                                <div class="card-text">

                                    <!-- Button trigger modal -->
                                    <button type="button" class="btn btn-outline-primary " data-bs-toggle="modal" :data-bs-target="'#modal_'+personagem.id">
                                    Descrição
                                    </button>

                                    <!-- Modal -->
                                    <div class="modal fade" :id="'modal_'+personagem.id" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                                    <div class="modal-dialog">
                                        <div class="modal-content">
                                        <div class="modal-header">
                                            <h5 class="modal-title" id="exampleModalLabel">Descrição</h5>
                                            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                                        </div>
                                        <div class="modal-body">
                                            
                                           <p class="card-text">
                                                 {{personagem.description}}
                                           </p> 

                                        </div>
                                        <div class="modal-footer">
                                            <button type="button" class="btn btn-danger" data-bs-dismiss="modal">Close</button>
                                        </div>
                                        </div>
                                    </div>
                                    
                                    </div>
                               
                                    
                                </div>
                            </div>
                            </div>
                    </span>                      
                </div>

                <div class="card">

                </div>

            

            </div>
    </div>  
</template>
<script>
import md5 from 'md5'
import axios from 'axios'
export default {
    name: 'sobre-view',
    data(){
        return{
            ts: Date.now(),
            chave_publica:'ea04dcaffcf71dfc5dfc0c68ff9059c5',
            chave_privada: '68b917818cbfac09399c17b7e7769e05fd9216a2',
            hash: md5(this.ts + this.chave_privada + this.chave_publica),
            personagens: []
        }
    },
    mounted(){
        axios.get("http://gateway.marvel.com/v1/public/characters?ts="+this.ts+"&apikey="+ this.chave_publica +
        "&hash="+ md5(this.ts + this.chave_privada + this.chave_publica)).then(res => {
            console.log(res)
            this.personagens = res.data.data.results})
    }
}

</script>
