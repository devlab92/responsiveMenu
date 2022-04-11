<template>
    <section>
        <div id="aboutMeBody">
            <div>
                <h1>Hello, world!</h1>
                <p>
                    Me chamo Luiz Augusto, 28 anos de idade. Desde crianca** sempre gostei muito de computadores e de desmontar as coisas, principalmente
                    eletronicos**. Nao demorou muito para que eu começasse a aprender o basico do funcionamento de um computador, de como formatar,
                    escolher pecas** e montar uma maquina do zero, etc. Em 2014 me matriculei** no Instituto Federal do Rio Grande do Sul (IFRS) para cursar
                    Analise e desenvolvimento de Sistemas (ADS) e entao** conheci o mundo da programacao.
                </p>
            </div>

            <div id="aboutMeImg">
                <!-- <img src="../assets/luiz_profile.jpg"/> -->
            </div>
        </div>
        
    </section>
</template>
<script>
export default {
    data() {
        return {};
    },
};
</script>

<style scoped>

#aboutMeBody{
    display: flex;
    flex-direction: row;
}

#aboutMeImg img{
    width: 100%;
    filter: grayscale(100%);
    transition: all 2s;
}

#aboutMeImg img:hover{
    filter: grayscale(0%);
    
}
</style>