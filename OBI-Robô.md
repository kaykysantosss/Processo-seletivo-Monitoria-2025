#  Lista de exercícios OBI para Monitoria

Autor: Kayky Jerônimo Duarte dos Santos

## Problema OBI 2021 - Fase 2 - Robô

Um fazendeiro comprou um robô-espantalho para espantar os pássaros de sua plantação de milho. O robô se move ao longo de um caminho que circunda a plantação. No caminho há N estações numeradas sequencialmente, a partir de 1, no sentido horário. A figura abaixo mostra um exemplo com oito estações.

<img src="https://olimpiada.ic.unicamp.br/static/img/task_images/2021f2pj_robo.png" alt="Texto alternativo" width="500">

O robô inicia cada dia na estação número 1, e então obedece a uma sequência de comandos. Os comandos são gerados por um algoritmo de aprendizagem de máquina que coleta informações através de sensores espalhados na plantação, para garantir uma cobertura de vigia máxima. Cada comando faz com que o robô se mova para outra estação, vizinha à estação em que ele se encontra, ou no sentido horário ou no sentido anti-horário. O robô permanece nessa nova estação até receber um novo comando.

Apesar da promessa de que o robô protegeria a plantação, ao final de um determinado dia o fazendeiro notou que parte de sua plantação estava devastada por pássaros. O fazendeiro agora quer entender melhor o que aconteceu.
Dados o número da estação mais próxima à área devastada e a sequência de comandos que o robô obedeceu naquele dia, escreva um programa para determinar quantas vezes o robô permaneceu na estação mais próxima à àrea devastada.

### Entrada:

A primeira linha contém três inteiros N, C e S, representando respectivamente o número de estações, o número de comandos e o número da estação mais próxima à área devastada. A segunda linha contém C inteiros X1, X2, …, XC, representando a sequência de comandos recebidos pelo robô. Para i = 1, 2, …, C, se Xi é 1 então o i-ésimo comando significa "mova-se para a próxima estação no sentido horário", enquanto se Xi é -1 então o i-ésimo comando significa "mova-se para a próxima estação no sentido anti-horário". O robô sempre inicia na estação número 1.

### Saída:

Seu programa deve produzir uma única linha, contendo um único inteiro, o número de vezes que o robô permaneceu na estação número S durante o dia.

### Restrições de Entrada

**2 ≤ N ≤ 100**

**1 ≤ C ≤ 1000**

### Exemplo:

#### Entrada:

8 8 3

1 -1 1 1 1 -1 1 1

#### Saída:

2

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

Aqui definiremos variaveis que serão utilizadas na resolução do problema. **N** irá guardar a quantidade de estações envolvidas no trajeto, **C** guardará a quantidade de comandos a serem realizados, **S** informará a estação mais próxima a área devastada, a variável **comandos** irá guardar todas as sequências de comandos recebidos (podendo ser elas 1,para sentido horário e -1, para sentido anti-horário) e por fim a variável **estacao** guardará a estação atual do robô.

```cpp
int main(){
    int N,C,S;
	int i;
 	int contador = 0;
 	int comandos;
 	int estacao = 1;
}
```
#### Observação:

Podemos notar que as váriaveis **contador** e **estacao** são inicializadas. **contador** tera seu valor inicial igual a 0, já a **estação** será inicada com valor = 1, pois o problema nos diz que o robô sempre inicia na estação 1.

### Passo 4: Atualização das váriaveis

Rebemos a entrada das 3 variáveis iniciais.

```cpp
  scanf("%d %d %d",&N,&C,&S);
```

### Passo 5: Lógica envolvida

Inicialmente, antes de analisarmos cada situação, devemos realizar uma condição inicial de um caso isolado. Caso a estação mais próxima a área devastada(S) seja igual ao valor da estação inicial(1), nosso contador somará + 1. Ao realizar essa condição forçamos o robô a verificar a estação inicial antes de seguir para a próxima.

```cpp
    if(S == 1){
		contador++;
	}
```
Em seguida criaremos um laço de repetição **(For())**. Este laço é fundamental para analisarmos todos os comandos(**C**) que foram dados ao nosso robô. Sua estrutura inicia com um valor i ( recebido anteriormente), inicialmente igual a 0, que irá se repetir **enquanto i for menor que C**.

```cpp
    	for(i = 0; i < C; i++){

        }
```
Dentro deste laço de repetição daremos entrada aos comandos recebidos.


```cpp
    	for(i = 0; i < C; i++){
            scanf("%d",&comandos);
        }
```

Em seguida dizemos que a estação irá guardar o valor da estação mais o comando recebido, podendo ser eles 1 (avance) ou -1 (Volte).

```cpp
    	estacao += comandos;
```

Agora analisaremos duas possíveis situações. Primeiramente, o problema nos fornece a informação de que o trajeto é um circuito fechado, logo ao chegar a ultima estação, o trajeto recomeça da estação inicial. Para que esse caso aconteça precisamos implementar uma condição que nos diz: Se a estação atual for maior que o número de estações, ou seja, chegamos a última estação e estamos seguindo para a próxima, o valor de estação retornará a estação inicial().

```cpp
	 	if(estacao > N){
			 estacao = 1;
		 }
```

O contrário também deve ser considerado. Se a estação atual for menor que a estação inicial, ou seja, caso retornarmos 1 estação anterior a inicial, estaremos na última estação,Logo, a variável estação guardará N.

```cpp
	 	if(estacao < 1 ){
			 estacao = N;
		 }
```

Por fim temos a condicional mais importante do problema, que irá guardar quantas vezes o robô passou pela área devastada. Se a estação atual for igual a estação mais próxima a área devastada, nosso contador somará + 1;

```cpp
if(estacao == S ){
			contador++;
		 }	
```
```cpp

Por fim fecharemos o laço de repetição e em seguida exibiremos o contador na tela.

for(i = 0; i < C; i++){
		scanf("%d",&comandos);
	 	estacao= estacao + comandos;
	 	
	 	if(estacao > N){
			 estacao = 1;
		 }
		 if( estacao < 1){
			 estacao = N;
		 }
		 if(estacao == S ){
			contador++;
		 }			 
	}
	
	printf("%d", contador);
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
	
	int N,C,S;
	int i;
 	int contador = 0;
 	int comandos;
 	int estacao = 1;
	scanf("%d%d %d",&N,&C,&S);
	if(S == 1){
		contador++;
	}
	
	for(i = 0; i < C; i++){
		scanf("%d",&comandos);
	 	estacao += comandos;
	 	
	 	if(estacao > N){
			 estacao = 1;
		 }
		 if( estacao < 1){
			 estacao = N;
		 }
		 if(estacao == S ){
			contador++;
		 }		
		 
		 
	}
	
	printf("%d", contador);
	
	return 0;
}
```
