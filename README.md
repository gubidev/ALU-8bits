# ALU 8-bits

Fala galera! Esse repositório guarda a minha ALU (Arithmetic Logic Unit) de 8 bits. Esse projeto foi desenvolvido para uma atividade do curso de Engenharia da Computação do Inteli. 

A ideia aqui não foi usar "caixas pretas" ou blocos prontos que fazem a matemática por você. Cada soma, multiplicação e divisão foi construída no nível dos transistores, juntando porta lógica por porta lógica.

Aqui esta o video onde eu explico o projeto: [Video Explicativo](https://drive.google.com/file/d/15fg-e287JZY6VHjWE1TchTIG7yuPIzob/view?usp=sharing)

## O que essa ALU faz?
Ela recebe dois números de 8 bits (A e B) e, dependendo do "canal" que você escolher no Seletor (OPCODE), ela faz uma das seguintes operações:

* **Soma & Subtração:** Usando uma cascata de Somadores Completos (Full Adders).
* **NAND & XOR:** Operações lógicas bit a bit.
* **Shift Lógico (Esquerda e Direita):** Deslocamento de bits feito fisicamente entortando os fios, sem usar portas lógicas extras.
* **Multiplicação:** A parte mais hardcore. Feita com uma matriz de portas AND gerando produtos parciais, que depois são somados em uma árvore de somadores de 16 bits.
* **Divisão:** Feita usando o algoritmo de *Divisão com Restauração* (Restoring Division), testando a subtração bit a bit e restaurando o valor quando a conta dá negativo.

## Como a Arquitetura funciona?
Como a gente tá lidando com 8 bits, algumas contas (tipo multiplicar 255 x 255) geram números muito grandes que não cabem em 8 fios. Para resolver isso, a arquitetura usa dois "cofres" principais para guardar as respostas:

1. **AC (Acumulador):** É o painel principal. Ele mostra o resultado das contas normais (Soma, Lógicas, Shifts). 
   * Na **Multiplicação**, ele guarda a metade "baixa" do número (os 8 bits menos significativos). 
   * Na **Divisão**, ele guarda o **Resto** da conta.
2. **MQ (Multiplicador/Quociente):** É o painel auxiliar.
   * Na **Multiplicação**, ele acende para mostrar a metade "alta" do número (os 8 bits mais significativos) quando a conta transborda.
   * Na **Divisão**, ele guarda o **Quociente** (o resultado principal de quantas vezes um número coube no outro).

Toda essa organização passa por um **Multiplexador (MUX) de 8 canais**, que atua como um guarda de trânsito deixando só a resposta certa passar para o painel final. No final de tudo, a resposta é salva de verdade usando um **Registrador** acionado por um pulso de Clock.

## Como rodar o projeto
1. Você vai precisar do simulador lógico **[Digital](https://github.com/hneemann/Digital)** instalado no seu PC (roda em Windows e Linux).
2. Baixe todos os arquivos `.dig` na sua pasta de documentos.
3. Abra o arquivo principal (`ALU.dig`) dentro do programa.
4. Dê o Play na simulação lá no topo.
5. Coloque os valores nas entradas `A` e `B`, escolha a operação no botão de `OPCODE` e dê um pulso no botão de `Clock` para salvar o resultado no Acumulador!
6. Qualquer duvida veja o [Video Explicativo](https://drive.google.com/file/d/15fg-e287JZY6VHjWE1TchTIG7yuPIzob/view?usp=sharing) ou entre em contato.
