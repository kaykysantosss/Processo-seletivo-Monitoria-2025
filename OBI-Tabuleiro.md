# Lista de exercícios OBI para Monitoria

Autor: Kayky Jerônimo Duarte dos Santos

## Problema OBI 2015 - Fase 2 - Torre

Dada uma matriz quadrada M de números naturais, o índice i de uma certa linha e o índice j de uma certa coluna, vamos definir o peso do cruzamento da linha i com a coluna j, como sendo a soma de todos os elementos que estejam na linha i ou na coluna j, mas não nas duas. Quer dizer, excluindo o elemento que está exatamente no cruzamento! Neste problema, você deve descobrir qual é o peso mínimo entre todos os possíveis cruzamentos da matriz!

No jogo de xadrez, a torre é uma peça que pode se mover para qualquer outra posição do tabuleiro na linha ou na coluna da posição que ela ocupa. O professor Paulo está tentando inventar um novo tipo de jogo de xadrez onde todas as peças são torres, o tabuleiro também é quadrado mas pode ter qualquer dimensão e cada posição do tabuleiro é anotada com um número inteiro positivo, como na figura abaixo.

<img src="https://olimpiada.ic.unicamp.br/static/img/task_images/2015f2p1_torre.png" alt="Texto alternativo" width="300">

Ele definiu o peso de uma posição (i,j) como sendo a soma de todos os números que estejam na linha i com todos os números da coluna j, mas sem somar o número que está exatamente na posição (i,j). Quer dizer, se uma torre estiver na posição (i,j), o peso da posição é a soma de todas as posições que essa torre poderia atacar.

O professor Paulo está solicitando a sua ajuda para implementar um programa que determine qual é o peso máximo entre todas as posições do tabuleiro.

No exemplo da figura acima, com um tabuleiro de dimensão seis (ou seja, seis linhas por seis colunas), o peso máximo é 67, referente à posição (4,4).

### Entrada:

A primeira linha da entrada contém um inteiro N, representando a dimensão do tabuleiro.
Cada uma das N linhas seguintes contém N inteiros positivos X_i, definindo os números em cada posição do tabuleiro.

### Saída:
Seu programa deve produzir uma única linha, contendo um único inteiro, o peso máximo entre todas as posições do tabuleiro.

### Restrições de Entrada

**3 ≤ N ≤ 1000**
**0 < X_i ≤ 100**

### Exemplo:
#### Entrada:

6
4 1 3 8 4 5
9 2 8 9 2 7
5 5 4 3 2 5
8 2 9 1 9 8
7 1 3 2 1 2
5 1 2 9 3 8

#### Saída:

67

## Resolução:

### Passo 1: Inclusão das bibliotecas

A biblioteca stdio.h permite realizar funções básicas de entradas e saídas.

```cpp
#include <stdio.h>

```
A biblioteca stdlib.h nos fornece funções utilitárias essencias para várias tarefas.

```cpp
#include <stdlib.h>

```

### Passo 2: Definição da função principal (main)

A função main é o ponto inicial fundamental de todo código em C. Toda a resolução está contida na funcão main.

```cpp
int main(){

}
```
### Passo 3: Criar as variáveis básicas

Aqui iremos definir as variáveis utilizadas no problema. **N** guardará um número inteiro que define a dimensão do tabuleiro, **somaL** irá armazenar a soma de determinada linha, **somaC** irá armazenar a soma de determinada coluna, **maiorPe** receberá posteriormente o maior peso possível e por fim **pesoAtual** guardará o peso atual.

```cpp
    int N;
	int i,j,q,r;
	int somaL = 0  ;
	int somaC = 0;
	int maiorPe = 0;
	int pesoAtual = 0;
```

#### Observação:

todas as variáveis, exceto N, são inicializadas com valor igual a 0.

### Passo 3: Atualização das váriaveis

Inicialmente damos entrada a variável N, para sabermos a dimensão do tabuleiro. Em seguida, criaremos uma nova variável, Tabuleiro, que representará a matriz envolvida no problema.

```cpp
    scanf("%d", &N);
	int tabuleiro[N][N];
```
Note que, tendo em vista ser um tabuleiro de formato quadrado, suas dimensões serão as mesmas em altura e largura.

### Passo 4: Lógica envolvida

Primeiramente precisamos saber qual o valor de todas coordenadas no tabuleiro, ou seja, daremos entrada em todas as posições do tabuleiro. Para isso usaremos dois laços de repetição (**For()**), um para percorrermos as linhas e um para percorrermos as colunas. Em seguida receberemos o valor de cada coordenada(i,j) da matriz do tabuleiro.

```cpp
    for(i = 0; i < N; i++){
		 for(j = 0; j < N; j++){
		 	scanf("%d", &tabuleiro[i][j]);
		 }
	}
```

Em seguida iremos percorrer o tabuleiro novamente. O problema nos diz que temos que descobrir o peso máximo entre todas as posições do tabuleiro e que esse peso máximo é dado pela soma entre a maior soma de linhas do tabuleiro e a maior soma de colunas no tabuleiro, a posição que a torre se encontra não deve ser considerada. 

Para realizarmos a soma das linhas, teremos de percorrer o tabuleiro novamente, analisando somente as linhas. Note que para isso a variável das colunas deverá ser constante. Podemos escrever assim:

```cpp
for(q = 0; q < N; q++){
		somaL += tabuleiro[q][j];
 }
```
Devemos fazer o mesmo com as colunas, seguindo a mesma ideia, mas desta vez a variável das linhas deverá ser constante.

```cpp
for(r = 0; r < N; r++){
		somaC += tabuleiro[i][r];
 }
```
Após realizar ambas as somas, podemos determinar o peso atual. Esse peso pode ser descrito da seguinte forma:

```cpp
pesoAtual = (somaC + somaL) - 2*tabuleiro[i][j];
```
#### Observação:

No problema é dito, que a posição que a torre está não deve ser considerada, por isso subtraimos a posição(i,j). Mas note que a subtraimos duas vezes, pois seguindo a técnica que utilizamos para a contagem, determinada posição seria contada 1 vez a mais que o necessário.

Em seguida após definirmos o peso atual, devemos resetar as variáveis da soma das linhas e da soma das colunas, assim cada coordenada percorrida terá seu próprio peso, sem interferência da anterior.

```cpp
 somaL = 0;
 somaC = 0;

```
Em seguida há apenas uma condicional que irá atualizar o valor do maior peso a cada loop do código. Para isso devemos apenas verificar se o peso atual é maior que o maior peso (inicialmente 0), caso seja verdadeiro o valor do maior peso será atualizado para o valor atual.

```cpp
 if(pesoAtual > maiorPe){
	  maiorPe = pesoAtual;
 }
```
Em seguidas fechamos o laço de repetição inicial, e printamos o valor do maior peso na tela.

```cpp
	for(i = 0; i < N; i++){
		 for(j = 0; j < N; j++){
		 	for(q = 0; q < N; q++){
				 somaL += tabuleiro[q][j];
			 }
			 for(r = 0; r < N; r++){
				 somaC += tabuleiro[i][r];
			 }
			 pesoAtual = (somaC + somaL) - 2*tabuleiro[i][j];
			 
			 somaL = 0;
			 somaC = 0;
		  	 
		  	 if(pesoAtual > maiorPe){
				   maiorPe = pesoAtual;
			   }
		 }
	}
	
	printf("%d", maiorPe);

```

### Passo 6: Finalização do programa

 Por último a função deverá nos retornar um valor inteiro. Para indicarmos que a função não teve erros, retornamos a mesma a 0.

```cpp
 	return 0;
    }
```
## Código Completo

Seguindo o passo a passo acima conseguimos resolver de forma objetiva o problema apresentado.

```cpp
 	#include <stdio.h>
    #include <stdlib.h>

    int main(){
        
        int N;
        int i,j,q,r;
        int somaL = 0  ;
        int somaC = 0;
        int maiorPe = 0;
        int pesoAtual = 0;
        scanf("%d", &N);
        int tabuleiro[N][N];

        for(i = 0; i < N; i++){
            for(j = 0; j < N; j++){
                scanf("%d", &tabuleiro[i][j]);
            }
        }
        
        for(i = 0; i < N; i++){
            for(j = 0; j < N; j++){
                for(q = 0; q < N; q++){
                    somaL += tabuleiro[q][j];
                }
                for(r = 0; r < N; r++){
                    somaC += tabuleiro[i][r];
                }
                pesoAtual = (somaC + somaL) - 2*tabuleiro[i][j];
                
                somaL = 0;
                somaC = 0;
                
                if(pesoAtual > maiorPe){
                    maiorPe = pesoAtual;
                }
            }
        }
        
        printf("%d", maiorPe);
        
        
        return 0;
    }
 ```   


