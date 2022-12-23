<template>
    <footer>
        <div class="footerTel">
            <img src='../assets/icons/whatsapp.png' alt="whatsapp icon" />
            <div>
                <p>0800 123 2222</p>
                <p>Seg - Sex 8h-22h</p>
            </div>
        </div>
        <div class="footerOthers">
            <div class="footerChat">
                <img src='../assets/icons/chat.png' alt="chat icon" />
                <p id="chat">Chat</p>
                <div class="chatLive">
                    <p>Chat ao vivo</p>
                    <p>Seg - Sex 8h-22h</p>
                </div>
            </div>
            <div class="footerEmail">
                <img src='../assets/icons/email.png' alt="email icon" />
                <p id="email">E-mail</p>
                <div class="sendEmail">
                    <p>Mande um e-mail</p>
                    <p>Respondemos rapidinho</p>
                </div>
            </div>
            <div class="footerInfo">
                <img src='../assets/icons/infoBlue.png' alt="info icon" />
                <p id="help">Ajuda</p>
                <div class="helpCentral">
                    <p>Central de ajuda</p>
                    <p>Encontre todas as respostas</p>
                </div>
            </div>
        </div>
        <div class="footerSignature">
            <p>Feito com <img src='../assets/icons/heart.png' alt="heart icon" /> pela Quero Educação</p>
        </div>
    </footer>
</template>

<script>
export default {
    name: 'FooterComponent'
}
</script>

<style scoped>
footer {
    background-color: var(--color-primary-blue);
    display: flex;
    flex-direction: column;
    color: var(--color-font-white);
    font-size: var(--font-size-small);    
}

.footerTel,
.footerEmail div {
    background-color: var(--color-secondary-blue); 
    
    
}

.footerSignature,
.footerTel,
.footerOthers {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    height: 130px;            
}

.footerEmail,
.footerChat,
.footerInfo {
    width: 33%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-color: var(--color-secondary-blue);
}

.chatLive,
.sendEmail,
.helpCentral {
    display: none;
}

.footerEmail {
    margin-left: 10px;
    margin-right: 10px;
}

.footerTel img,
.footerEmail img,
.footerChat img,
.footerInfo img {
    height: 80px;

}

.footerSignature img {
    height: 40px;
}

@media (min-width:1178px) {
    footer {
        flex-direction: row;
        flex-wrap: wrap;
        font-size: var(--font-size-smallest);
    }

    .chatLive,
    .sendEmail,
    .helpCentral {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    .chatLive p,
    .sendEmail p,
    .helpCentral p {
        width: 100%;
    }

    #chat,
    #email,
    #help {
        display: none;
    }

    .chat {

        border: solid 1px purple;
    }

    .chat img {
        border: solid 1px green;
    }

    .footerSignature,
    .footerTel,
    .footerOthers {
        height: 80px;
    }

    .footerTel {
        width: 25%;
    }

    .footerOthers {
        width: 75%;
        background-color: var(--color-secondary-blue);
    }

    .footerTel,
    .footerOthers {
        font-weight: bold;
    }

    .footerEmail,
    .footerChat,
    .footerInfo {
        margin-right: 0;
        height: 100%;
        flex-direction: row;
    }

    .footerEmail {
        margin-left: 0px;
        margin-right: 0px;
    }


    .footerSignature {
        width: 100%;
    }

    .footerSignature img {
        height: 20px;
    }

    .footerTel img,
    .footerOthers img {
        height: 40px;
    }
}
</style>