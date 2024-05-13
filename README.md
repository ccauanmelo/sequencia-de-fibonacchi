# sequencia-de-fibonacchi
Nesse projeto temos como objetivo a implementação de um uso prático para o cálculo exato de qualquer termo existente na sequência de Fibonacchi, utilizando como base o Risc-V v1.0 que criamos durante o estudo sobre arquitetura de sistemas digitais.

A primeira etapa necessária para a realização desse projeto é a atualização do risc-V v1.0 para incluir as instruções: jal, jalr, bne, andi e ori que serão precisos para o programa que irá calcular os termos da sequência de Fibonacchi, as modificações feitas no código base foram:

1 - Atualização da unidade de controle adicionando as entradas e saidas respectivas de todas as instruções para o funcionamento apropriado de cada arquivo dentro do mod_teste( dessa forma já teremos o andi e ori funcionando corretamente )

2 - Modificação da extensão para incluir o tipo-j de saída de constante na chave de seleção "11" importante para a instrução jal

3 - Alteração do mux 2x1 no final do código para um mux 4x2, pois será necessário na chave de seleção "11" o mux receba o valor presente no "PCtarget" importante para as instruções jal e jalr 

4 - Inclusão de um mux 2x1 que irá controlar se no "PCtarget" ele receberá "rd1" ou "PC", que diferencia se o programa vai realizar jal ou jalr

5 - Para o funcionamento apropriado do comando bne precisamos que antes do "PCSrc" tenhamos uma porta xor com o "Zero" e "funct3" para que o programa diferencie entre o comando bne e beq

Após essas modificações serem feitas no risc-V v1.0 teremos todo o necessário para a inclusão do sequinte código na instrução de memória:

"lb x2, 0xFF(x0)

addi x3, zero, 1

addi x5, zero, 1

beq x2, x5, done

while:

beq x3, x2, end

jal x1, fib

addi x3, x3, 1

jal x0, while


end:

addi x6, x6, 0

jal x0, fim 


done:

addi x6, x5, 0

jal x0, fim


fib:
add x6, x5, x4

addi x4, x5, 0

addi x5, x6, 0

jalr zero, ra, 0

fim: "

Sendo as chaves SW[7:0] que irá determinar o exato termo da sequência de Fibonacchi que você deseja
