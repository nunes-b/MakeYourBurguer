<template>
<div>
    <p>component de mensagem</p>
    <div>
        <form id="burguer-form">
          <div class="input-container">
            <label for="nome">Nome do Cliente </label>
            <input type="text" name="nome" id="nome" v-model="nome" placeholder="Digite seu nome">
          </div>  
          <div class="input-container">
            <label for="pao">Escolha o seu pão </label>
            <select name="pao" id="pao" v-model="pao">
            <option value="">Selecione o seu pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
                {{pao.tipo}}</option>

        </select>
        
          </div>  

          <div class="input-container">
            <label for="carne">Escolha a carne para o seu hamburguer </label>
            <select name="carne" id="carne" v-model="carne">
            <option value="">Selecione uma opção</option>
            <option v-for="carne in carnes" :key="carne.id" value="carne.tipo">{{carne.tipo}}
            </option>

        </select>
        
          </div>  
          <div class="input-container">
            <label id="opcionais-title" for="opcionais">Selecione os opcionais: </label>
            <div class="checkbox-container">
                <input type="checkbox" name="opcionais" v-model="opcionais" value="couve">
                <span>Alface</span>
                <input type="checkbox" name="opcionais" v-model="opcionais" value="linguiceta">
                <span>Alface</span>
                <input type="checkbox" name="opcionais" v-model="opcionais" value="alface">
                <span>Alface</span>
            </div>        
          </div>  
          <div class="input-container">
           <input type="submit" class="submit-btn" value="Enviar meu pedido"> 
        </div>
        </form> 
    </div>
</div>

</template>

<script>
export default {
    name: 'BurguerForm',
    data(){
        return{
            paes:null,
            carnes:null,
            opcionaisdata: null,
            nome: null, 
            pao: null,
            carne: null, 
            opcionais: [],
            status: "Solicitado",
            msg: null, 
        }
    },
    methods:{
        async getIngredientes(){
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();
            
            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais
        }
    },
    mounted(){
        this.getIngredientes()
    }
}
</script>

<style scoped>
#burguer-form{
    max-width: 400px;
    margin: 0 auto;
}

.input-container{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label{
    font-weight: bold;
    margin-bottom: 15px;
    padding: 3px;
    color: rgb(24, 21, 24);
    border-left: 5px solid rgb(192, 12, 192);
}

input, select{
 padding: 5px 15px;
 width: 300px;
}

#opcionais-container{
    flex-direction: row;
    flex-wrap: wrap;
}
#opcionais-title{
    width: 100%;
}
.checkbox-container{
    padding: auto;
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkbox-container span, 
.checkbox-container input{
    width: auto;
}
.checkbox-container span{
    margin-left: 6px;
    font-weight: bold;
}

.submit-btn{
    background-color: purple;
    color: whitesmoke;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
}
.submit-btn:hover{
    background-color: whitesmoke;
    color: purple;
}
</style>