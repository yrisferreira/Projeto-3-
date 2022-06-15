# Projeto-3-
const prompt = require("prompt-sync")();

console.log(`         JOGO DA VELHA 
O Jogador 1 jogará com X e o Jogador 2 com O `);
prompt("Vamos começar? Aperte ENTER para jogar!");

let nomes = nomeJogador();

let arrTTT = [
  ["0:0", "0:1", "0:2"],
  ["1:0", "1:1", "1:2"],
  ["2:0", "2:1", "2:2"]
];

let controleGeral = true;
jogo(controleGeral, nomes, arrTTT);

function jogo(controle, nomeJogador, array){
  let controleTurno = 0;
  while (controle) {
    let rodadas
    let verificador = true;
  
    do{
      console.log("Qual será o número de rodadas?");
      rodadas = +prompt(": ");
      try{
        if(isNaN(rodadas) || undefined) throw 'Digite um número!';
        if(rodadas > 0 && typeof rodadas == 'number') verificador = false;
      }catch(e){
        console.clear();
        console.log('ERROR: ' + e);
      }
    }while(verificador);
    
    console.log(`RODADAS = ${rodadas}`);
    let vitoria = [0, 0];
  
    while (rodadas > 0) {
      let verificaVitoria = false;
  
      marcarTabela(array, nomeJogador, controleTurno);
      console.clear();

      verificaVitoria = verificarVitoria(array, nomeJogador, controleTurno, vitoria);

      if(verificaVitoria == 1){
          console.table(array);
          rodadas--;
          array = [
            ["0:0", "0:1", "0:2"],
            ["1:0", "1:1", "1:2"],
            ["2:0", "2:1", "2:2"],
          ];
          if (rodadas <= 0) break;
          prompt("PRESSIONE ENTER PARA PRÓXIMA RODADA!");
      }
      controleTurno++;
    }
