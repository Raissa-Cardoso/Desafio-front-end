<template>
    <main class="mainModal">
        <button class="closeModal" type="submit" v-on:click="closeModal">X</button>
        <p id="title">Adicionar Bolsa</p>
        <p id="subtitle">Filtre e adicione as bolsas do seu interesse.</p>
        <div class='cityCourse'>
            <div class="city">
                <label htmlFor="city">SELECIONE SUA CIDADE</label>
                <select id="city">
                    <option key="" value=""></option>
                </select>
            </div>
            <div class="course">
                <label htmlFor="course">SELECIONE O CURSO DE SUA PREFERÊNCIA</label>
                <select id="course">
                    <option key="" value=""></option>
                </select>
            </div>
        </div>
        <div class='kindPrice'>
            <div class="kindModal">
                <p>COMO VOCÊ QUER ESTUDAR?</p>
                <div class="kindModalOptions">
                    <input type="checkbox" class='kindCheck' name="kindCheck" value="presencial" id="kindPresencial" />
                    <label htmlFor='kindPresencial' value="presencial">Presencial
                    </label>
                    <input type="checkbox" class='kindCheck' name="kindCheck" value="adistancia" id="kindEad" />
                    <label htmlFor='kindEad' value="adistancia">A distância
                    </label>
                </div>
            </div>
            <div class='priceModal'>
                <p>ATÉ QUANTO PODE PAGAR?</p>
                <p>R$</p>
                <div class="progress">
                    <button></button>
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
                    <option key="" value=""></option>
                </select>
            </div>
        </div>
        <div class="dividerModal"></div>
        <div class="universitiesModal">
            <div class='universityModal' key="">
                <input type="checkbox" name="" id="" />
                <img src="" alt="" />
                <div class='courseModal'>
                    <p>Administração</p>
                    <p>Bacharelado</p>
                </div>
                <div class='scholarshipModal'>
                    <div class='scholarshipModalPorcentage'>
                        <p>Bolsa de </p>
                        <p> %</p>
                    </div>
                    <p>R$ / mês</p>
                </div>
            </div>
        </div>
        <div class="dividerModal"></div>
    </main>
</template>
 
<script>
export default {
    name: 'ModalComponent',
    methods: {
        closeModal: function () {
            this.modal = document.querySelector('.modal')
            this.modal.style.display = "none"
            this.mask = document.querySelector('.mask')
            this.mask.style.display = "none"
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
}

#title {
    font-size: var(--font-size-smaller);
    font-weight: bold;
}

#subtitle, .scholarshipModal {
    font-size: var(--font-size-smallest);
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
    width: 38%;
    height: 70px;
}

.dividerModal{
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
.order, .universityModal, .scholarshipModalPorcentage{
    display: flex;
    flex-direction: row;
    align-items: center;
   
}
.universityModal img{
    width: 30%;
}
.courseModal{
    width: 50%;    
}
.courseModal :nth-child(1){
    font-weight: bold;
    color: var(--color-secondary-blue);
}
.courseModal :nth-child(2){
    font-size: var(--font-size-smallest) ;
}
.scholarshipModal{    
    width: 20%; 
    margin-right: 40px;   
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
.universitiesModal{
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
