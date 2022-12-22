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
            <div>
                <img src='../assets/icons/chat.png' alt="chat icon" />
                <p>Chat</p>
            </div>
            <div class="footerEmail">
                <img src='../assets/icons/email.png' alt="email icon" />
                <p>E-mail</p>
            </div>
            <div>
                <img src='../assets/icons/infoBlue.png' alt="info icon" />
                <p>Ajuda</p>
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
     footer{
         background-color: var(--color-primary-blue);          
         display: flex;       
         flex-direction: column;
         color: var(--color-font-white);
         font-size: var(--font-size-small);
     }
     .footerTel, .footerOthers div{
        background-color: var(--color-secondary-blue);   
        margin-bottom: 2px;
     }
     .footerSignature, .footerTel, .footerOthers{
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        height: 130px;
     }
     .footerOthers div{
        width: 33%;        
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
     }
     .footerEmail{
        margin-left: 10px;
        margin-right: 10px;        
     }
     .footerTel img, .footerOthers img{
        height: 80px;        
    }
    .footerSignature img{
        height: 40px;
    }
     
 </style>