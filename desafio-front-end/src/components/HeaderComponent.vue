<template>
    <header>
        <div class="info">
            <img src='../assets/icons/info.png' alt="info icon" />
            <p id="infoHelp">Ajuda</p>
            <p id="infoHowWorks">Como funciona</p>
        </div>
        <img class="divider" src='../assets/icons/divider.png' alt="divider icon" />
        <div class="infoTel">
            <img src='../assets/icons/whatsappGreen.png' alt="whatsapp logo" />
            <div>
                <p>0800 123 2222</p>
                <p>Envie mensagem ou ligue</p>
            </div>
        </div>
        <img class="divider" src='../assets/icons/divider.png' alt="divider icon" />
        <div class="queroLogo">
            <img src='../assets/quero-Logo.jpg' alt="quero logo" />
        </div>
        <img src='../assets/icons/divider.png' alt="divider icon" />
        <div class="login">
            <p>Nome Sobrenome</p>
            <img src='../assets/icons/login.png' alt="login icon" />
            <p>Conta</p>
        </div>
    </header>
    <nav class="navHeader">
        <p>Minha conta</p>
        <p>Pré-matrículas</p>
        <p>Bolsas favoritas</p>
        <ul>
            <li>Menu</li>
            <li> <img src='../assets/icons/dropMenu.png' alt="dropMenu icon" /></li>
        </ul>
    </nav>
</template>

<script>
export default {
    name: 'HeaderComponent'
}
</script>

<style scoped>
header {
    background-color: var(--color-background-header);
    margin: 2px;
    display: flex;
    align-items: center;
    justify-content: space-around;
}

header div {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

header img {
    height: 90%;
}

header p {
    color: var(--color-secondary-blue);
    font-weight: bold;
    font-size: var(--font-size-small);
}

.login :nth-child(2),
#infoHelp {
    display: block;
}

#infoHowWorks,
.infoTel,
header :nth-child(2),
.login :nth-child(1),
.navHeader p:nth-child(2),
.navHeader :nth-child(3) {
    display: none;
}

.navHeader {
    height: 80px;
    background-color: var(--color-primary-blue);
    color: var(--color-font-white);
    font-weight: bold;
    font-size: var(--font-size-medium);
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 0 30px;
    align-items: center;
}

.navHeader ul {
    list-style: none;
    display: flex;
    flex-direction: row;
}

.navHeader ul li {
    padding-right: 10px;
}

@media (min-width:1178px) {
    header {
        height: 80px;
    }

    .info,
    .infoTel,
    .queroLogo,
    .login {
        flex-direction: row;
        width: 25%;
    }

    header p {
        font-size: var(--font-size-smaller);
    }

    #infoHelp,
    header :nth-child(4),
    header :nth-child(6),
    .login :nth-child(3),
    .navHeader :nth-child(4) {
        display: none;
    }

    #infoHowWorks,
    .infoTel,
    header :nth-child(2),
    .login :nth-child(1),
    .navHeader :nth-child(2),
    .navHeader :nth-child(3) {
        display: block;
    }

    .navHeader :nth-child(2),
    .navHeader :nth-child(3) {
        font-weight: 200;
    }

    .infoTel {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
    }

    .infoTel div {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
    }

    .infoTel img {
        margin-right: 20px;
    }

    .infoTel img,
    .login img,
    .info img,
    .queroLogo img {
        height: 40px;
    }

    .navHeader {
        height: 40px;
        font-size: var(--font-size-smallest);
        justify-content: flex-start;
    }

    .navHeader p {
        height: 100%;
        padding: 10px 20px;
    }

    .navHeader :nth-child(3) {
        background-color: var(--color-secondary-blue);
    }
}
</style>