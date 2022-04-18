<template>
    <div>
        <Message :msg="msg" v-show="msg"/>
        <div>
            <form id="form" @submit="createNoodle">
                <div class="input-container">
                    <label for="Name">Client Name:</label>
                    <input type="text" id="name" name="name" v-model="name" placeholder="Insert Your Name">
                </div>
                <!-- input-container2 -->
                <div class="input-container">
                    <label for="Noodle">choose the dough</label>
                    <select name="Noodle" id="noodle" v-model="Noodle">
                        <option value="">choose the dough</option>
                        <option v-for="pasta in pastas" :key="pasta.id" :value="pasta.tipo">{{ pasta.tipo }}</option>
                    </select>
                    
                </div>
                <!-- input-container3 -->
                <div class="input-container">
                    <label for="Sauces">choose the sauce</label>
                    <select name="Sauces" id="sauces" v-model="Sauces">
                        <option value="">choose the sauce</option>
                        <option v-for="sauce in sauces" :key="sauce.id" :value="sauce.tipo">{{sauce.tipo}}</option>
                    </select>
                        
                    
                </div>
                <!-- input-container4 -->
                <div class="input-container" id="container-options">
                    <label id="title-options" for="options">choose the side dishes</label>
                    <div class="checkbox-container" v-for="options in optionsdata" :key="options.id">
                        <input type="checkbox" name="options" id="options" v-model="option" :value="options.tipo">
                        <span>{{options.tipo}}</span>
                    </div>
                    
                    
                </div>

                <!-- input submit -->
                <div class="input-container">
                    <input type="submit" class="btn-submit" value="assemble my noodles">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue'

export default {

    components:{
        Message
    },
 

    name: 'Form',
    data(){
        return{
            pastas: null,
            sauces: null,
            optionsdata: null,
            name: null,
            pasta: null,
            sauce: null,
            option: [],
            msg: null,
            noodle: null,
            Noodle: null,
            Sauces: null,
            
            

        }
    },
    methods:{
        async getIngredients(){
            const req = await fetch('http://localhost:3004/ingredients')
            const data = await req.json()

            this.pastas = data.pastas,
            this.sauces = data.sauces,
            this.optionsdata = data.options

        },
        async createNoodle(event){
            event.preventDefault()

            
            const data = {
                name: this.name,
                Pasta: this.Noodle,
                sauce: this.Sauces,
                options: Array.from(this.option),
                status: 'Requested'
                

            };

            const dataJson = JSON.stringify(data);

            const req = await fetch('http://localhost:3004/noodles', {
                method: "POST",
                headers: {"Content-Type": "application/json"},
                body: dataJson
            });

            const res = await req.json()

            const randomId = Math.floor(Math.random() * 100 )

            this.msg = `Pedido Nº ${randomId} Feito!`

            setTimeout(() => { this.msg='' }, 3000);
            
            this.name ='',
            this.Noodle='',
            this.Sauces='',
            this.option=''

        }
    },
    mounted(){
        this.getIngredients()
        

    }    
}
</script>

<style scoped>
    #form{
        max-width: 400px;
        margin: 0 auto;
        margin-left: 450px;
    }

    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label{
        font-weight: bold;
        margin-bottom: 15px;
        color: #43252c;
        padding: 5px 10px;
        border-left: 4px solid #ee9f07;
    }

    input, select{
        padding: 5px 10px;
        width: 300px;
    }

    #container-options{
        flex-direction: row;
        flex-wrap: wrap;
    }

    .checkbox-container{
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    #title-options{
        width: 100%;
    }

    .checkbox-container span,
    .checkbox-container input{
        width: auto;
    }

    .checkbox-container span{
        margin-left: 6px;
        font-weight: bold;
    }

    .btn-submit{
        color: #ba322b;
        background-color: #ee9f07;
        border: none;
        padding: 10px;
        font-weight: bold;
        text-transform: capitalize;
        font-size: 17px;
        border-radius: 4px;
        transition: 0.3s;
        cursor: pointer;
    }

    .btn-submit:hover{
         color:#ee9f07;
         background-color: #ba322b;
    }
</style>
    
