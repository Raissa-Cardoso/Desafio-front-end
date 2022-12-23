<template>
    <main class="homePage">
        <div class="modal">
            <ModalComponent />
        </div> 
        <div class="mask">

        </div>       
        <div class="return">
            <img src='../assets/icons/return.png' alt="return icon" />
            <p>Minha conta</p>
        </div>
        <div class="path ">
            <p>Home /</p>
            <p>Minha conta /</p>
            <p>Bolsas favoritas</p>
        </div>
        <h1 id="principal">Bolsas Favoritas</h1>
        <h2>Adicione bolsas de cursos e faculdades do seu interesse e receba atualizações com as
            melhores ofertas disponíveis.</h2>
        <div class="semester ">
            <div>Todos os semestres</div>
            <div>2º semestre de 2019</div>
            <div>1º semestre de 2020</div>
        </div>
        <div class="card">
            <img src='../assets/icons/plus.png' alt="plus icon" v-on:click="showModal" />
            <p>Adicionar bolsa</p>
            <p>Clique para adicionar bolsas de cursos do seu interesse</p>
        </div>
    </main>
</template>
 
<script>
import ModalComponent from '../components/ModalComponent.vue'
export default {
    name: 'HomePage',
    data() {
        return {
            modal: "",
            main: "",
            card:""
        }
    },
    methods: {
        showModal: function () {
            this.modal = document.querySelector('.modal')
            this.modal.style.display = "block"                       
            this.mask=document.querySelector('.mask')
            this.mask.style.display = "block" 
         }
    },
    components: {
        ModalComponent
    }
}
</script>
 
<style scoped>
main{
    background-color: var(--color-background-main);    
       
}
.mask{
    display: none;
    width: 100%;  
    height: 100vh;      
    overflow: none;
    background-color: rgba(0,0,0,0.5);
    z-index: 1;
    position: absolute;
    top: 0;        
}

.modal {
    display: none;
    z-index: 100;
    width: 70vw;
    height: 70vh;
    border: solid 1px black;
    position: fixed;
    align-self: center;    
}

.return {
    color: var(--color-secondary-blue);
    font-weight: bold;
    font-size: var(--font-size-small);
    display: flex;
    flex-direction: row;
    padding: 20px;
}

.return img {
    height: 25px;
    margin-right: 10px;
}

.path {
    display: none;
}

h1 {
    margin-top: 20px;
}

h2 {
    padding: 20px;
    line-height: 40px;
}

h1,
h2,
.card p {
    color: var(--color-font-black);
}

.semester {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 20px;
    border-radius: 10px;
    border: solid 2px var(--color-secondary-blue);
}

.semester div {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: var(--font-size-small);
    font-weight: bold;
    height: 60px;
    width: 100%;
}

.semester :nth-child(1) {
    color: var(--color-font-white);
    background-color: var(--color-secondary-blue);
}

.semester :nth-child(2) {
    border-bottom: solid 2px var(--color-secondary-blue);
}

.semester :nth-child(2),
.semester :nth-child(3) {
    color: var(--color-secondary-blue);
}

.card {
    width: 95%;
    align-self: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    line-height: 40px;
    padding: 40px;
    border-radius: 10px;   
    background-color: #fff;
}

.card img {
    height: 80px;
    margin-bottom: 20px;
    cursor: pointer;
}

.card :nth-child(2) {
    font-weight: bold;
    font-size: var(--font-size-medium);
}

.card :nth-child(3) {
    font-size: var(--font-size-small);
}

@media (min-width:1178px) {
    .homePage{
        height: 76vh;
    }
    .mask{
        height: calc(100vh + 102px);
    }
    .return {
        display: none;
    }

    .path {
        display: block;
    }

    .path {
        margin: 20px;
        display: flex;
        flex-direction: row;
        font-size: var(--font-size-smallest);
    }

    .path :nth-child(1),
    .path :nth-child(2) {
        color: var(--color-secondary-blue);
        margin-right: 10px;
        font-weight: bold;
    }

    .path :nth-child(3) {
        color: var(--color-font-black);
    }

    h2 {
        font-weight: 200;
        font-size: var(--font-size-smaller);
        line-height: 0px;
    }

    .semester {
        flex-direction: row;
        align-self: flex-end;
        width: 40%;
        margin-right: 40px;
        height: 30px;
    }

    .semester div {
        height: 30px;
        font-size: var(--font-size-smallest);
        border-radius: 5px;
    }

    .semester :nth-child(2) {
        border-right: solid 1px var(--color-secondary-blue);
        border-radius: 0;
    }

    .card {
        width: 20%;
        height: 350px;
        align-self: flex-start;
        margin-left: 20px;
        line-height: 20px;

    }

    .card img {
        height: 60px;

    }

    .card :nth-child(2) {
        font-weight: bold;
        font-size: var(--font-size-smaller);
        margin-bottom: 20px;
    }

    .card :nth-child(3) {
        font-size: var(--font-size-smallest);
        text-align: center;

    }

}
</style>