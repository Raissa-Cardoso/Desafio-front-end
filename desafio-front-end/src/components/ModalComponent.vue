<template>
    <main class="mainModal">
        <button class="closeModal" type="submit" v-on:click="closeModal">X</button>
        <p id="title">Adicionar Bolsa</p>
        <p id="subtitle">Filtre e adicione as bolsas do seu interesse.</p>
        <div class='cityCourse'>
            <div class="city">
                <label htmlFor="city">SELECIONE SUA CIDADE</label>
                <select id="city" v-on:change="changeCity">
                    <option value=""></option>
                    <option v-for="(city, index) in dbCityOrder" :key="index"> {{ city }}</option>
                </select>
            </div>
            <div class="course">
                <label htmlFor="course">SELECIONE O CURSO DE SUA PREFERÊNCIA</label>
                <select id="course" v-on:change="changeCourse">
                    <option value=""></option>
                    <option v-for="(course, index) in dbCourseOrder" :key="index"> {{ course }}</option>
                </select>
            </div>
        </div>
        <div class='kindPrice'>
            <div class="kindModal">
                <p>COMO VOCÊ QUER ESTUDAR?</p>
                <div class="kindModalOptions">
                    <input type="checkbox" class='kindCheck' name="kindCheck" value="presencial" id="kindPresencial"
                        v-on:click="changeKind('presencial')" />
                    <label htmlFor='kindPresencial' value="presencial">Presencial
                    </label>
                    <input type="checkbox" class='kindCheck' name="kindCheck" value="Ead" id="kindEad"
                        v-on:click="changeKind('ead')" />
                    <label htmlFor='kindEad' value="Ead">A distância
                    </label>
                </div>
            </div>
            <div class='priceModal'>
                <p>ATÉ QUANTO PODE PAGAR?</p>
                <p>R$ {{ this.priceChanged }}</p>
                <div class="priceBar">
                    <input type="range" name="" id="changePrice" min=0 max=10000 v-on:change="changePrice">
                </div>
            </div>
        </div>
        <div class="results">
            <div class='result'>
                <p>Resultado:</p>
            </div>
            <div class='order'>
                <p>Ordenar por </p>
                <select name="universityOp" id="universityOp">
                    <option value="Nome da faculdade">Nome da faculdade</option>
                    <option v-for="(university, index) in dbUniversityOrder" :key="index"> {{ university }}</option>
                </select>
            </div>
        </div>
        <div class="dividerModal"></div>
        <div class="universitiesModal">
            <div v-for="(offer, index) in dbFilter" :key="index">
                <div class='universityModal'>
                    <input type="checkbox" name="" id="" />
                    <img :src=offer.university.logo_url alt={{offer.university.logo_url}} />
                    <div class='courseModal'>
                        <p>{{ offer.course.name }}</p>
                        <p>{{ offer.course.level }}</p>
                    </div>
                    <div class='scholarshipModal'>
                        <div class='scholarshipModalPorcentage'>
                            <p>Bolsa de </p>
                            <p>{{ offer.discount_percentage }}%</p>
                        </div>
                        <p>R$ {{ offer.price_with_discount }} / mês</p>
                    </div>
                </div>
                <div class="dividerModal"></div>
            </div>
        </div>
    </main>
</template>
 
<script>
import db from '../data/db.json'
export default {
    name: 'ModalComponent',
    data() {
        return {
            db: db,
            dbFilter: [],
            filters: ["","","","",""],
            dbCity: [],
            dbCityOrder: [],
            dbCourse: [],
            dbCourseOrder: [],
            dbUniversity: [],
            dbUniversityOrder: [],
            priceChanged: 0,
            city: "",
            course: "",
            presencial: false,
            ead: false
        }
    },
    mounted() {
        for (let i = 0; i < db.length; i++) {
            if (this.dbCity.indexOf(this.db[i].campus.city) == -1) {
                this.dbCity.push(db[i].campus.city)
            }
            if (this.dbCourse.indexOf(this.db[i].course.name) == -1) {
                this.dbCourse.push(db[i].course.name)
            }
            if (this.dbUniversity.indexOf(this.db[i].university.name) == -1) {
                this.dbUniversity.push(db[i].university.name)
            }
        }
        this.dbCityOrder = this.dbCity.sort()
        this.dbCourseOrder = this.dbCourse.sort()
        this.dbUniversityOrder = this.dbUniversity.sort()
        this.dbFilter = this.db

    },
    methods: {
        closeModal: function () {
            this.modal = document.querySelector('.modal')
            this.modal.style.display = "none"
            this.mask = document.querySelector('.mask')
            this.mask.style.display = "none"
        },
        changePrice: function () {
            this.priceChanged = document.querySelector('#changePrice').value
            this.filters[4] = this.priceChanged
            this.changeFilters()
        },
        changeCity: function () {
            this.city = document.querySelector('#city').value
            this.filters[0] = this.city
            this.changeFilters()

        },
        changeCourse: function () {
            this.course = document.querySelector('#course').value
            this.filters[1] = this.course
            this.changeFilters()

        },
        changeKind: function (kindSelected) {
            if (kindSelected == "presencial") {
                this.presencial = !this.presencial
                if (this.presencial == true) {
                    this.filters[2] = this.presencial
                    this.changeFilters()
                }
            }
            if (kindSelected == "ead") {                
                this.ead = !this.ead
                if (this.ead == true) {
                    this.filters[3] = this.ead
                    this.changeFilters()
                }
            }
        },
        changeFilters: function () {            
            if(this.dbFilter.length==0||(this.filters[0] == ""&&this.filters[1] == "")){
                this.dbFilter=this.db
            }
            if (this.filters[0] !== "") {
               this.dbFilter = this.dbFilter.filter(offer => offer.campus.city === this.city)               
            }
            if (this.filters[1] !== "") {
                this.dbFilter = this.dbFilter.filter(offer => offer.course.name === this.course)                
            }
            if(this.filters[2]!==""){
                this.dbFilter = this.db.filter(offer => offer.course.kind === "Presencial")
            }
            if(this.filters[3]!==""){
                this.dbFilter = this.db.filter(offer => offer.course.kind === "EaD")
            }
            if(this.filters[4]!==""){
                this.dbFilter = this.db.filter(offer => offer.price_with_discount <= this.priceChanged)
            }
            
        }

    }
}
</script>
 
<style scoped>
.mainModal {
    background-color: var(--color-background-main);
    height: 100%;
    padding: 20px;
    line-height: 30px;
}

#title,
#subtitle {
    color: var(--color-font-black);
    width: 30%;
}

#title {
    font-size: var(--font-size-smaller);
    font-weight: bold;
}

#subtitle,
.scholarshipModal {
    font-size: var(--font-size-smallest);
    margin-right: 40px;
}

.scholarshipModal {
    width: 20%;
}

.scholarshipModal :nth-child(2),
.scholarshipModal :nth-child(3) {
    font-weight: bold;
    color: var(--color-green);
}

.kindPrice,
.results {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin-right: 40px;
}

.kindModal,
.priceModal {
    width: 35%;
    height: 120px;
}

.priceBar input {
    width: 100%;
}

.dividerModal {
    height: 1px;
    width: 97%;
    background-color: var(--color-primary-blue);
    opacity: 0.5;
}

.kindModal p,
.cityCourse,
.priceModal :nth-child(1),
.results p {
    font-size: var(--font-size-smallest);
    font-weight: bold;
    margin-top: 10px;
}

.kindModalOptions,
.order,
.universityModal,
.scholarshipModalPorcentage {
    display: flex;
    flex-direction: row;
    align-items: center;
}

.scholarshipModalPorcentage :nth-child(1) {
    margin-right: 5px;
}

.universitiesModal {
    overflow-x: scroll;
}

.universityModal img {
    width: 30%;
    height: 35px;
    object-fit: contain;
}

.courseModal {
    width: 50%;
}

.courseModal :nth-child(1) {
    font-weight: bold;
    color: var(--color-secondary-blue);
}

.courseModal :nth-child(2) {
    font-size: var(--font-size-smallest);
}

.order p {
    align-self: center;
    margin-right: 10px;
}

.order select {
    color: var(--color-secondary-blue);
    font-weight: bold;
    height: 25px;
}

.kindModalOptions input {
    margin-right: 10px;
}

#kindEad {
    margin-left: 20px;
}

.cityCourse {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    margin-right: 40px;
}

.cityCourse select {
    width: 350px;
    height: 30px;
}

.city,
.course {
    display: flex;
    flex-direction: column;
}

.universitiesModal {
    display: flex;
    flex-direction: column;
}

.closeModal {
    top: -30px;
    right: 0;
    position: absolute;
    height: 30px;
    width: 30px;
}
</style>
