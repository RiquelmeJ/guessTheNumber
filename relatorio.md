**Universidade Federal do Cariri  
Bacharelado em Ciência da Computação  
Alunos: Karla Mikaelly Paz de Almeida e Riquelme Jatay Ribeiro S. Bezerra  
Professor: Ramon Santos Nepomuceno**
# Trabalho de Circuitos Digitais
Olá! Nesse documento, iremos explicar o funcionamento do projeto e como ocorreu a construção de cada um dos componentes.\
![visão geral do projeto](https://uploaddeimagens.com.br/images/004/590/419/full/projetoGeral1.png?1693230279 "visão geral do projeto")
## Sobre o jogo

O primeiro projeto da disciplina consiste em um jogo para dois jogadores construído na plataforma **Logisim**. O objetivo do jogo é adivinhar qual é o número secreto do sistema por meio de chutes e das dicas ao fim de cada rodada. Vencerá o o jogo aquele que adivinhar o número secreto primeiro. O sistema funciona da seguinte forma:
 - Para iniciar o jogo, há um botão "Jogar". Cada jogador, em sua vez, deve escolher um número e digitá-lo no sistema binário por meio de um conjunto de botões. Estes, por sua vez, estão ligados a um decodificador, que está ligado a um display de sete segmentos. Assim, a entrada do jogador é exibida no display no sistema hexadecimal;
 -   Logo após, é necessário indicar quem é o jogador da vez por meio do botão homônimo, e o multiplexador permitirá que apenas o palpite do jogador indicado seja analisado pelo comparador;
 - Então o comparador, como o nome sugere, comparará a entrada enviada pelo usuário com o número secreto (que está dentro deel) e indicará se o palpite foi errado (no caso, maior ou menor do que o número secreto) ou correto (igual ao número secreto) por meio de 3 saídas.
