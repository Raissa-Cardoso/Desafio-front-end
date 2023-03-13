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
                    <option v-for="(city, index) in dbCity" :key="index"> {{ city }}</option>
                </select>
            </div>
            <div class="course">
                <label htmlFor="course">SELECIONE O CURSO DE SUA PREFERÊNCIA</label>
                <select id="course" v-on:change="changeCourse">
                    <option value=""></option>
                    <option v-for="(course, index) in dbCourse" :key="index"> {{ course }}</option>
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
                <button v-on:click="universitiesOrder()">Nome da faculdade</button>
                <img src='../assets/icons/dropUniversities.png' alt="dropUniversitiesicon" />
            </div>
        </div>
        <div class="dividerModal"></div>
        <div class="universitiesModal">
            <div v-for="(offer, index) in dbFilter" :key="index">
                <div class='universityModal'>
                    <input type="checkbox" class="checkOffer" v-on:click="selectOffer(offer, index)" />
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
    <footer class="footerModal">
        <button id="buttonCancel">Cancelar</button>
        <button id="buttonAdd" v-on:click="addOffer"
            :class="{ buttonActived: isActive, buttonDesactived: !isActive }">Adicionar bolsa(s)</button>
    </footer>
</template>
<script>
import db from '../data/db.json'
export default {
    name: 'ModalComponent',
    emits: ["add"],        
    data() {
        return {
            db: db,
            dbFilter: [],
            dbFilterOrder: [],            
            filters:{},
            dbUniversity: [],            
            dbCity: [],            
            dbCourse: [],            
            offerSelected: [],
            priceChanged: 0,
            city: "",
            course: "",
            presencial: false,
            ead: false,
            order: false,
            isActive: false,
            indexSelected: []            
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
        this.dbCity= this.dbCity.sort()
        this.dbCourse = this.dbCourse.sort()
        this.dbUniversity = this.dbUniversity.sort()
        this.dbFilter = this.db                     
    },    
    methods: {
        closeModal: function () {
            this.modal = document.querySelector('.modal')
            this.modal.style.display = "none"
            this.mask = document.querySelector('.mask')
            this.mask.style.display = "none"
            if (this.offerSelected.length !== 0) {
                document.querySelector('.offerSelected').style.display = "flex"
            }
        },
        changePrice: function () {
            this.priceChanged = document.querySelector('#changePrice').value            
            this.filters.price_with_discount=this.priceChanged
            this.changeFilters()
        },
        changeCity: function () {
            this.city = document.querySelector('#city').value            
            this.filters.city=this.city
            this.changeFilters()
        },
        changeCourse: function () {
            this.course = document.querySelector('#course').value            
            this.filters.name=this.course
            this.changeFilters()
        },
        changeKind: function (kindSelected) {
            if (kindSelected == "presencial") {
                this.presencial = !this.presencial
            }
            if (kindSelected == "ead") {
                this.ead = !this.ead
            }
            this.filters.kind={Presencial:this.presencial,EaD:this.ead}
            this.changeFilters()           
        },
        changeFilters: function () { 
            if(this.dbFilter=='' || Object.values(this.filters).every(value=>value=='')){
                this.dbFilter=this.db 
            }              
            const campus=['city']
            const course=['name','kind']
            const offer=['price_with_discount']              
            Object.keys(this.filters).forEach((filter,index)=>{
                if(Object.values(this.filters)[index]!=''){
                    if(campus.indexOf(filter)!=-1){                    
                        this.filterCampus(filter)                    
                    }
                    if(course.indexOf(filter)!=-1){
                        this.filterCourse(filter)
                    }
                    if(offer.indexOf(filter)!=-1){
                        this.filterOffer(filter)
                    }
                }
            })
        },
        filterCampus:function(filter){
            if (this.dbFilter.filter(offer => offer.campus[filter] === this.city).length !== 0) {                
                this.dbFilter = this.dbFilter.filter(offer => offer.campus[filter] === this.city)                
            }else{
                this.clearFilter()                
            }
        },
        filterCourse:function(filter){
            if(filter=='name') this.filterNameCourse()
            if(filter=='kind') this.filterKind()
        },
        filterNameCourse:function(){
            if (this.dbFilter.filter(offer => offer.course.name === this.course).length !== 0) {                
                this.dbFilter = this.dbFilter.filter(offer => offer.course.name === this.course)                
            }else{
                this.clearFilter()
            }
        },
        filterKind(){    
            if(this.presencial==this.ead){
                this.dbFilter=this.db
                delete this.filters.kind                
                this.changeFilters()
            }else{
                if(this.presencial && (this.dbFilter.filter(offer => offer.course.kind === "Presencial").length !== 0)){                                  
                    this.dbFilter = this.dbFilter.filter(offer => offer.course.kind === "Presencial")                   
                }
                if(this.ead && (this.dbFilter.filter(offer => offer.course.kind === "EaD").length !== 0)){                                   
                    this.dbFilter = this.dbFilter.filter(offer => offer.course.kind === "EaD")
                }   
            }                     
        },
        filterOffer:function(filter){
            if (this.dbFilter.filter(offer => offer[filter] <= this.priceChanged).length !== 0) {               
                this.dbFilter = this.dbFilter.filter(offer => offer[filter] <= this.priceChanged)                
            }else{
                this.clearFilter()
            }
        },        
        clearFilter:function(){
            this.dbFilter=''
        },
        universitiesOrder: function () {
            this.order = !this.order
            if (this.order == true) {
                for (let i = 0; i < this.dbUniversity.length; i++) {
                    this.dbFilter.map(offer => {
                        if (offer.university.name.indexOf(this.dbUniversity[i]) !== -1) {
                            this.dbFilterOrder.push(offer)
                        }
                    })
                }
                this.dbFilter = this.dbFilterOrder
            }
        },
        selectOffer: function (offer, index) {
            this.indexSelected.push(index)
            let count = 0
            Object.values(this.indexSelected).reduce((value1, value2) => {
                if (value1 == value2) {
                    count++
                }
                return count
            })
            if (2 * count == Object.values(this.indexSelected).length) {
                this.isActive = false
            } else {
                this.isActive = true
                this.offerSelected.push([index, offer])
            }
        },
        addOffer: function () {           
            let count = 0
            let repeat = []
            for (let i = 0; i < this.offerSelected.length; i++) {
                if (this.offerSelected[0].indexOf(this.offerSelected[i][0]) !== -1) {
                    count++
                    repeat.push(this.offerSelected[i][0])
                }
            }
            if (count % 2 == 0) {
                for (let i = 0; i < repeat.length; i++) {
                    this.offerSelected.splice(this.offerSelected[0].indexOf(repeat[i]), 1)
                }
            }
            this.$emit('add', this.offerSelected)   
            this.closeModal() 
            this.clearModal()          
        },
        clearModal:function(){
            this.indexSelected=[] 
            this.offerSelected=[]                        
        }
    }
}
</script>

<style scoped>
.mainModal {
    background-color: var(--color-background-main);    
    width: 100vw;
    height: 150%;    
    padding: 40px 15vw;    
    line-height: 30px;
    box-sizing: border-box;
}

#title,
#subtitle {
    color: var(--color-font-black);    
}

#title {
    font-size: var(--font-size-medium);
    font-weight: bold;
}

#subtitle,
.scholarshipModal {
    font-size: var(--font-size-small);
    margin-right: 40px;    
}

.scholarshipModal {
    margin-left: 60%;   
    display: flex;
    flex-direction: column;
    
}

.scholarshipModal :nth-child(2),
.scholarshipModal :nth-child(3) {
    font-weight: bold;
    color: var(--color-green);
    font-size: 16px;
}

.kindPrice{
    display: flex;
    flex-direction: column;
}
.results {
    display: flex;
    flex-direction: row;
    justify-content: space-between;      
    font-size: var(--font-size-smaller);    
}

.kindModal,
.priceModal {    
    height: 100px;    
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    font-size: var(--font-size-smaller);

}

.priceBar input {
    width: 100%; 

}

.kindModal p,
.priceModal :nth-child(1),
.results p {    
    font-weight: bold;    
    margin-right: 4vw;          
}

.kindModalOptions,
.universityModal,
.order,
.scholarshipModalPorcentage {
    display: flex;
    flex-direction: row;    
    align-items: center;
    font-size: var(--font-size-smaller);    
    flex-wrap: wrap;
}
.scholarshipModalPorcentage :nth-child(1) {
    margin-right: 5px;
}

.universitiesModal {
    overflow-x: scroll;
    display: flex;
    flex-direction: column;
}
.universityModal{      
    justify-content: space-between;      
}

.universityModal img{
    width: 50%;
    height: 55px;
    display: flex;    
    margin-top: 10%;
    object-fit: contain;     
}
.universityModal .checkOffer{
    width: 20px;
    height: 20px;
    margin-top: 10%;
}
.courseModal {
    width: 40%;       
}

.courseModal :nth-child(1) {
    font-weight: bold;
    color: var(--color-secondary-blue);
}

.courseModal :nth-child(2) {
    font-size: var(--font-size-smaller);    
}

.order button {
    color: var(--color-secondary-blue);
    font-weight: bold;
    height: 35px;
    align-self: center;
    margin-left: 10px;
    background-color: var(--color-background-main);
    border: none;
    cursor: pointer;
    font-size: var(--font-size-smaller);
}

.order img {       
    height: 3vh;
    width: 3vw;
}

.kindModalOptions input {
    margin-right: 10px;
}

#kindEad {
    margin-left: 20px;
}

.cityCourse {
    display: flex;
    flex-direction: column;  
    
}

.cityCourse select {
    width: 100%;
    height: 50px;
    margin-right: 6vw;
    border-radius: 10px;
    font-size: var(--font-size-smaller);
}

.city,
.course {
    display: flex;
    flex-direction: column;
    margin: 0;   
    padding: 10px 0px;
    
}
.city label, .course label{
    font-weight: bold;    
    font-size: var(--font-size-smaller);
    
}



.closeModal {
    top: -50px;
    right: 0;
    position: absolute;
    height: 50px;
    width: 50px;
    border: none;
    font-size: var(--font-size-medium);
    color: var(--color-font-white);
    background-color: rgba(31, 45, 48,0);
    cursor: pointer;
}

.footerModal {
    height: 10%;
    background-color: var(--color-background-main);
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    align-items: center;
}

.footerModal button {
    font-weight: bold;
    border-radius: 5px;
    margin-right: 20px;
    height: 40px;
}

#buttonCancel {
    width: 80px;
    border: solid 1px var(--color-primary-blue);
    color: var(--color-secondary-blue);
    background-color: var(--color-background-main);
}

#buttonAdd {
    width: 140px;
}

@media (min-width:1178px) {
    .mainModal {
        height: 90vh;
        width: calc(50vw - 1px);
        padding: 40px;
        
    }
    .closeModal { 
        top: -30px;  
        height: 20px;
        width: 20px;           
        font-size: var(--font-size-small); 
        align-self: right; 
            
    }

    
    #title {
        font-size: var(--font-size-smaller);
    }

    #subtitle,
    .scholarshipModal {
        font-size: var(--font-size-smallest);        
    }
    .scholarshipModal {
    
    margin-right: 5px;    
    margin-left: 4vw;   
    display: flex;
    flex-direction: column;
    
}

    .kindPrice,
    .results {
        align-items: center;
        justify-content: space-between;
        display: flex;
        flex-direction: row;
    }

    .kindModal,
    .priceModal {
        width: 20vw;           
    }

    .kindModal p,
    .cityCourse,
    .priceModal :nth-child(1)
    
     {
        font-size: var(--font-size-smallest2); 
    }
    .priceModal :nth-child(2)
    {
        font-size: var(--font-size-smallest); 
    }

    .kindModalOptions,
    .order,
    .universityModal,
    .scholarshipModalPorcentage,.results p {
        font-size: var(--font-size-smallest);
    }
    .universityModal{              
        flex-wrap: nowrap;
    }
   
    .universityModal img {
        width: 30%;
        height: 40px;
        margin-top: 0;
        object-fit: contain;             
    }
    .universityModal .checkOffer{
        width: 15px;
        height: 15px;
        margin-top: 0;
    }
    .courseModal{
        width: 30%;        
    }

    .courseModal :nth-child(2) {
               
        font-size: var(--font-size-smallest);
    }

    .order button {
        align-self: flex-end;
        margin-bottom: 3px;
        font-size: var(--font-size-smallest);
    }
    .order img {           
        height: 2vh;
        width: 1.5vw;
    }

    .cityCourse {
        justify-content: space-between;        
        flex-direction: row;
        font-size: var(--font-size-smaller);       
    }

    .cityCourse select {
        width: 20vw;
        height: 30px;        
        border-radius: 5px;
        font-size: var(--font-size-smallest);

    }

    .city,
    .course {
        width: 20vw;         
    }
    .city label, .course label{        
        font-size: var(--font-size-smallest2);
    }
}
</style>
