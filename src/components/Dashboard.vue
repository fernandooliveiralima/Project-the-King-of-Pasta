<template>
    <div class="table-dashboard">
        <div>
            <div id="table-dashboard-heading">
                <div class="order-id">#</div>
                <div>Client</div>
                <div>pasta</div>
                <div>sauces</div>
                <div>options</div>
                <div>actions</div>

            </div>

            <div id="table-dashboard-rows">
                <div class="table-dashboard-row" v-for="noodles in noodle" :key="noodles.id">
                    <div class="order-number">{{noodles.id}}</div>
                    <div>{{noodles.name}}</div>
                    <div>{{noodles.Pasta}}</div>
                    <div>{{noodles.sauce}}</div>
                    <div>
                        <ul>
                            <li v-for="(options, index) in noodles.options" :key="index">{{options}}</li>
                            
                        </ul>
                    </div>
                    <div>
                        <select name="status" class="status" @change="updateNoodle($event, noodles.id)">
                            <option value="">selecione</option>
                            <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="noodles.status === s.tipo">{{s.tipo}}</option>
                        </select>
                        <button @click="deleteNoodle(noodles.id)" class="delete-btn">Delete</button>
                    </div>
                </div>
                
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Dashboard',
    data(){
        return{
            
            noodle: null,
            noodle_id: null,
            status: []
        }
    },
    methods:{
        async getRequests(){
            const req = await fetch('http://localhost:3004/noodles');
            const data = await req.json()
            
            this.noodle = data;

            console.log(this.noodle);

            this.getStatus();
            
        },
        async getStatus(){
            const req = await fetch('http://localhost:3004/status');
            const data = await req.json()

            this.status = data;

            
        },
        async deleteNoodle(id){
            
            const req = await fetch(`http://localhost:3004/noodles/${id}`,{
                method: "DELETE"
            });

            const res = await req.json();

            this.getRequests()
        },
        async updateNoodle(event, id){
            const option = event.target.value;
            const dataJson = JSON.stringify({status: option});
            const req = await fetch(`http://localhost:3004/noodles/${id}`,
            {method: "PATCH",
            body: dataJson,
            headers: {"Content-Type": "application/json"}});
            

            const res = await req.json();

            console.log(res);
        },

        
    },
    mounted(){
        this.getRequests()
    }
}
</script>

<style scoped>
    .table-dashboard{
        max-width: 1200px;
        margin: 0 auto;

    }

    #table-dashboard-heading,
    #table-dashboard-rows,
    .table-dashboard-row{
        display: flex;
        flex-wrap: wrap;
    }

    #table-dashboard-heading{
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #43252c;
    }

    #table-dashboard-heading div,
    .table-dashboard-row div{
        width: 19%;
    }

    .table-dashboard-row{
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid brown;
    }

    #table-dashboard-heading .order-id,
    .table-dashboard-row .order-number{
        width: 5%;
    }

    select{
        padding: 12px 6px;
        margin-right: 12px;
    }

    .delete-btn{
        background-color: #ba322b;
        color: #ee9f07;
        border: none;
        padding: 10px;
        font-weight: bold;
        text-transform: capitalize;
        font-size: 17px;
        border-radius: 4px;
        transition: 0.3s;
        cursor: pointer;
    }

    .delete-btn:hover{
        color: #ba322b;
        background-color: #ee9f07;
    }
</style>