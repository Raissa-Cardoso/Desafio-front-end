<template>
    <main class="mainCard">
        <img :src=this.offerSend.university.logo_url />
        <p id="universityName">{{ (this.offerSend.university.name).toUpperCase() }}</p>
        <p id="courseName">{{ this.offerSend.course.name }}</p>
        <div class="score">
            <p id="universityScore">{{ this.offerSend.university.score }}</p>
            <img v-if="this.offerSend.university.score < 3.6" src='../assets/icons/smallScore.png' />
            <img v-if="this.offerSend.university.score > 3.8 && this.offerSend.university.score < 4.4"
                src='../assets/icons/mediumScore.png' />
            <img v-if="this.offerSend.university.score > 4.4" src='../assets/icons/bigScore.png' />
        </div>
        <div class="dividerModal"></div>
        <p id="kindShift">{{ (this.offerSend.course.kind).toUpperCase() }} * {{
                (this.offerSend.course.shift).toUpperCase()
        }}</p>
        <p id="startDate">Início das aulas em: {{ this.offerSend.start_date }}</p>
        <div class="dividerModal"></div>
        <p id="titleBill">Mensalidade com o Quero Bolsa:</p>
        <p id="fullPrice"><s>R$ {{ this.offerSend.full_price }}</s></p>
        <div class="priceMonth">
            <p id="priceDiscount">R$ {{ this.offerSend.price_with_discount }}</p>
            <p id="month">/mês</p>
        </div>
        <div class="buttonsCard">
            <button id="buttonDelete" v-on:click="deleteOffer">Excluir</button>
            <button id="buttonViewOffer" v-if="this.offerSend.enabled == true" class="buttonActived">Ver oferta</button>
            <button id="buttonUnavailable" class="buttonDesactived" v-else>Indisponível</button>
        </div>

    </main>
</template>

<script>

export default {
    name: 'CardComponent',
    props: {
        offerSend: {}
    },
    methods: {
        deleteOffer: function () {
            document.querySelector('.mainCard').remove()
        }
    }
}
</script>

<style scoped>
.mainCard {
    background-color: #fff;
    border-radius: 10px;
    width: 100%;
    align-self: flex-start;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
    margin-bottom: 20px;
    display: flex;
    flex-direction: column;
    padding: 10px;
    align-items: center;
    line-height: 30px;
}

.mainCard img {
    width: 30vw;
    object-fit: contain;
}

.score {
    margin-top: 10px;
    display: flex;
    flex-direction: row;
    height: 25px;
    width: calc(100% - 20px);
    justify-content: center;
}

.score p {
    margin-right: 10px;
    align-self: flex-end;
}

.score img {
    height: 20px;
}

#universityName,
#universityScore,
#kindShift,
#titleBill {
    font-weight: bold;
    color: var(--color-font-black);
    font-size: var(--font-size-smaller);
}

#kindShift,
#titleBill {
    margin-top: 10px;
}

#courseName {
    color: var(--color-secondary-blue);
    font-weight: bold;
    font-size: var(--font-size-small);
}

.priceMonth {
    display: flex;
    flex-direction: row;
    font-size: var(--font-size-small);
}

#fullPrice,
#startDate,
#month {
    color: var(--color-font-black);
    font-size: var(--font-size-smaller);
}

#month {
    margin-left: 5px;
}

#priceDiscount {
    color: var(--color-green);
    font-weight: bold;
}

.buttonsCard {
    display: flex;
    flex-direction: row;
    margin-top: 20px;
    width: calc(100% - 20px);
    justify-content: space-between;
}

#buttonDelete,
#buttonViewOffer,
#buttonUnavailable {
    font-weight: bold;
    height: 40px;
    border-radius: 5px;
    font-size: var(--font-size-smaller);
}

#buttonViewOffer,
#buttonUnavailable {
    width: 120px;
}

#buttonDelete {
    background-color: #fff;
    color: var(--color-secondary-blue);
    border: solid 1px var(--color-secondary-blue);
    width: 80px;
    cursor: pointer;
}

@media (min-width:1178px) {
    .mainCard {
        width: 280px;
        height: 400px;
        margin-left: 20px;
    }

    .mainCard img {
        width: 140px;
        height: 50px;
    }

    #universityName,
    #universityScore,
    #kindShift,
    #titleBill {
        font-size: var(--font-size-smallest);
    }

    #courseName {
        font-size: var(--font-size-smaller);
    }

    .priceMonth {
        font-size: var(--font-size-smaller);
    }

    #fullPrice,
    #startDate,
    #month {
        font-size: var(--font-size-smallest);
    }

    #buttonDelete,
    #buttonViewOffer,
    #buttonUnavailable {
        font-size: var(--font-size-smallest);
    }
    .score img {
       align-self: center;
       margin-bottom: 10px;
    }
}
</style>