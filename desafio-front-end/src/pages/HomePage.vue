<template>
    <main class="homePage">
        <div class="modal">
            <ModalComponent v-on:add="addOffers" />
        </div>
        <div class="mask"></div>
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
            <button id="allSemesters" class="buttonSelected" v-on:click="buttonChecked('allSemesters')">Todos os
                semestres</button>
            <button id="2019.2" class="buttonUnselected" v-on:click="buttonChecked('2019.2')">2º semestre de 2019</button>
            <button id="2020.1" class="buttonUnselected" v-on:click="buttonChecked('2020.1')">1º semestre de 2020</button>
        </div>
        <div class="cards">
            <div class="card">
                <img src='../assets/icons/plus.png' alt="plus icon" v-on:click="showModal" />
                <p>Adicionar bolsa</p>
                <p>Clique para adicionar bolsas de cursos do seu interesse</p>
            </div>
            <div class="offerSelected">
                <div v-for="(offer, index) in offersFilter" :key="index">
                    <CardComponent :offerSend="offer" v-on:delete="deleteOffers(index)" />
                </div>
            </div>
        </div>
    </main>
</template>
<script>
import ModalComponent from '../components/ModalComponent.vue'
import CardComponent from '@/components/CardComponent.vue'
export default {
    name: 'HomePage',
    data() {
        return {
            modal: "",
            mask: "",
            offers: [],
            offersFilter: []
        }
    },
    methods: {
        showModal: function () {
            this.modal = document.querySelector('.modal')
            this.modal.style.display = "block"
            this.mask = document.querySelector('.mask')
            this.mask.style.display = "block"
        },
        addOffers: function (offersModal) {
            for (let i = 0; i < offersModal.length; i++) {
                this.offers.push(offersModal[i][1])
            }
            this.offersFilter = this.offers
        },
        deleteOffers: function (index) {
            document.querySelectorAll('.mainCard').length != 1 ? document.querySelectorAll('.mainCard').item(index).remove() : document.querySelector('.mainCard').remove()
        },
        buttonChecked: function (id) {
            document.querySelectorAll('.semester button').forEach(element => {
                if (element.classList == 'buttonSelected') {
                    element.classList.remove('buttonSelected')
                    element.classList.add('buttonUnselected')
                }
            })
            document.getElementById(id).classList.remove('buttonUnselected')
            document.getElementById(id).classList.add('buttonSelected')
            if (id !== 'allSemesters') {
                this.offersFilter = []
                this.offers.forEach(offer => {
                    if (offer.enrollment_semester == id) {
                        this.offersFilter.push(offer)
                    }
                })
            } else {
                this.offersFilter = this.offers
            }
        }
    },
    components: {
        ModalComponent,
        CardComponent
    }
}
</script>

<style scoped>
.homePage {
    background-color: var(--color-background-main);
}

.mask {
    display: none;
    width: 100%;
    height: calc(100% + 500px);
    overflow: none;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 1;
    position: fixed;
    top: 0;
    left: 0;
}

.modal {
    display: none;
    z-index: 100;
    width: 100vw;
    height: 100vh;
    border: solid 1px black;
    position: absolute;
    align-self: center;
    box-sizing: border-box;
}

.offerSelected {
    display: none;
    flex-direction: column;
    flex-wrap: wrap;
    width: 100%;
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
    height: 160px;
    border: solid 2px var(--color-secondary-blue);
}

.semester button {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: var(--font-size-smaller);
    font-weight: bold;
    height: 100%;
    width: 100%;
    border: none;
    cursor: pointer;
}

.semester :nth-child(1) {
    border-top-left-radius: 10px;
    border-right: solid 1px var(--color-secondary-blue);
}

.semester :nth-child(3) {
    border-bottom-right-radius: 10px;
    border-top-right-radius: 10px;
}

.cards {
    display: flex;
    flex-direction: column;
    width: 95%;
    margin-bottom: 20px;
    margin-left: 20px;
}

.card {
    height: 100%;
    width: 100%;
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
    text-align: center;
}

@media (min-width:1178px) {

    .mask {
        height: calc(100vh + 230px);
    }

    .cards,
    .offerSelected {
        flex-direction: row;
    }

    .offerSelected {
        width: 80%;
        margin-right: 0;
    }

    .cards {
        width: 95%;
        margin-bottom: 20px;
        margin-left: 20px;
    }

    .card {
        width: 280px;
        height: 400px;
    }

    .return {
        display: none;
    }

    .modal {
        width: 50vw;
        height: 80vh;
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

    .semester :nth-child(1) {
        border-top-left-radius: 8px;
        border-bottom-left-radius: 8px;
    }

    .semester :nth-child(2) {
        border-right: solid 1px var(--color-secondary-blue);
        border-radius: 0;
    }

    .semester :nth-child(3) {
        border-top-right-radius: 8px;
        border-bottom-right-radius: 8px;
    }

    .semester button {
        font-size: var(--font-size-smallest);
    }

    .card {
        width: 280px;
        height: 400px;
        align-self: flex-start;
        margin-left: 20px;
        line-height: 20px;
    }

    .card img {
        height: 60px;
    }

    .card :nth-child(2) {
        font-size: var(--font-size-smaller);
        margin-bottom: 20px;
    }

    .card :nth-child(3) {
        font-size: var(--font-size-smallest);
        text-align: center;
    }
}
</style>