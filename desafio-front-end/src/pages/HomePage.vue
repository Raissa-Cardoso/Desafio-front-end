<template>
    <main>
        <div class="return">
            <img src='../assets/icons/return.png' alt="return icon" />
            <p>Minha conta</p>
        </div>
        <h1 id="principal">Bolsas Favoritas</h1>
        <h2>Adicione bolsas de cursos e faculdades do seu interesse e receba atualizações com as
            melhores ofertas disponíveis.</h2>
        <div class="semester">
            <div>Todos os semestres</div>
            <div>2º semestre de 2019</div>
            <div>1º semestre de 2020</div>
        </div>
        <div class="card">
            <img src='../assets/icons/plus.png' alt="plus icon" />
            <p>Adicionar bolsa</p>
            <p>Clique para adicionar bolsas de cursos do seu interesse</p>

        </div>
    </main>
</template>
 
<script>
export default {
    name: 'HomePage'
}
</script>
 
<style scoped>
main {
    background-color: var(--color-background-main);
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
    margin-bottom: 80px;
    background-color: #fff;
}

.card img {
    height: 80px;
    margin-bottom: 20px;
}

.card :nth-child(2) {
    font-weight: bold;
    font-size: var(--font-size-medium);
}

.card :nth-child(3) {
    font-size: var(--font-size-small);
}
</style>