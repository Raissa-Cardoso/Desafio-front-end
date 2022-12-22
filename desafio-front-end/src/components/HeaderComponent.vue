<template>
    <header>
        <div class="info">
            <img src='../assets/icons/info.png' alt="info icon" />
            <p>Ajuda</p>
            <p>Como funciona</p>
        </div>
        <div class="infoTel">
            <img src='../assets/icons/whatsappGreen.png' alt="whatsapp logo" />
            <div>
                <p>0800 123 2222</p>
                <p>Envie mensagem ou ligue</p>
            </div>
            
        </div>
        <img src='../assets/icons/divider.png' alt="divider icon" />
        <div class="quero-logo">
            <img src='../assets/quero-Logo.jpg' alt="quero logo" />
        </div>
        <img src='../assets/icons/divider.png' alt="divider icon" />
        <div class="login">
            <img src='../assets/icons/login.png' alt="login icon" />
            <p>Conta</p>
        </div>
    </header>
    <nav class="navHeader">
        <p>Minha conta</p>
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

header img{
    height: 90%;
}

header p {
    color: var(--color-secondary-blue);
    font-weight: bold;
    font-size: var(--font-size-small);
}
.info :nth-child(3), .infoTel{
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
.navHeader ul{
    list-style: none;
    display: flex;
    flex-direction: row;    
}
.navHeader ul li{
    padding-right: 10px;
}
@media (min-width:700px){
        
        header div{
            flex-direction: row;
        }
         .info :nth-child(2){
           display: none;
         }
         .info :nth-child(3), .infoTel{
           display: block;
         }
         .infoTel{
            display: flex;
            flex-direction: row;
            align-items: center;
            justify-content: center;
         }
         .infoTel div{
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
         }
         .infoTel img{
            height: 70px;            
         }
}
</style>