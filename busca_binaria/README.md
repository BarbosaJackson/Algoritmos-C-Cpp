# Motivação
Qual o melhor jeito possivel de se fazer uma busca em um array que esteja *ordenado*?

# Problema da busca binária
Mesmo sendo muito eficiente, essa busca só funciona para array que estejam ordenados previamente, ou seja, para alguns casos será necessário primeiro ordenar o array para depois fazer a busca.

# Como funciona?

Diferente da busca linear, a busca binária não vai olhar para o array sequencialmente, mas sim, fazendo questionamentos e com a resposta obtida eliminar metade do array restante para a busca.
A busca consiste em fixar um pivô em alguma posição de um array ordenado e a partir do valor dele decidir o que fazer, aqui definiremos que o pivô será sempre o elemento do meio do array, seguindo o passo a passo abaixo:

  1. O inicio do subarray que estou olhando é maior que o final?
  	- Se sim, o elemento não existe no array
  2. O pivô é quem estou buscando?
    - Se sim, retorne a posição, você achou o elemento
  3. Senão é quem estou buscando o pivô é menor que o valor que estou buscando?
    - Se sim, passe a procurar no array com inicio *meio + 1* e final do subarray anterior
    - Volte para o passo 1
  4. Senão for nenhum dos dois anteriores
    - busque no subarray com o inicio do subarray anterior e final em *meio - 1*
    - Volte para o passo 1

# O código

## Maneira iterativa

```C
#include <stdio.h>

int main() {
	int array[1000000], i, valor_busca, qtd_comp, inicio, meio, fim;
	// apenas inicializa o array com valores para cada posição
	for(i = 0; i < 1000000; i++) {
		array[i] = i + 1;
	}
	while(1) {
		flag = 0;
		// pega o valor da busca ou de encerramento do programa
		printf("Digite o valor que deseja buscar(-1 encerra o programa): ");
		scanf("%d", &valor_busca);
		// se for digitado -1 como informado no print, o programa é encerrado
		if(valor_busca == -1) {
			return 0;
		}
		inicio = 0;
		fim = 1000000;
		qtd_comp = 0;
		while(inicio <= fim) {
			qtd_comp++;
			meio = (inicio + fim) / 2; // pega o pivô que é a posição central
			if(array[meio] == valor_busca) {
				printf("%d esta na posicao: %d\nForam necessarias %d comparacoes para encontra-lo\n", valor_busca, meio, qtd_comp);
				break;
			} else if(array[meio] < valor_busca) {
				inicio = meio + 1;
			} else {
				fim = meio - 1;
			}
		}
		if(inicio > fim) {
			printf("%d nao encontrado\nForam feitas %d comparacoes para chegar a isso\n", valor_busca, qtd_comp);
		}
	}

	return 0;
}
```

## Maneira recursiva

```C
#include <stdio.h>

int busca_binaria(int *array, int inicio, int fim, int valor_busca, int *qtd_comp) {
	int meio = (inicio + fim) / 2;
	*qtd_comp += 1;
	if(inicio > fim) {
		return -1;
	}
	if(array[meio] == valor_busca) {
		return meio;
	} else if(array[meio] < valor_busca) {
		return busca_binaria(array, meio + 1, fim, valor_busca);
	} else {
		return busca_binaria(array, inicio, meio - 1, valor_busca);
	}
}

int main() {
	int array[1000000], i, valor_busca, qtd_comp;
	// apenas inicializa o array com valores para cada posição
	for(i = 0; i < 1000000; i++) {
		array[i] = i + 1;
	}
	while(1) {
		flag = 0;
		// pega o valor da busca ou de encerramento do programa
		printf("Digite o valor que deseja buscar(-1 encerra o programa): ");
		scanf("%d", &valor_busca);
		// se for digitado -1 como informado no print, o programa é encerrado
		if(valor_busca == -1) {
			return 0;
		}
		qtd_comp = 0;
		int pos = busca_binaria(array, 0, 1000000, valor_busca, &qtd_comp);
		if(pos == -1) {
			printf("%d nao encontrado\nForam feitas %d comparacoes para chegar a isso\n", valor_busca, qtd_comp);
		} else{ 
			printf("%d esta na posicao: %d\nForam necessarias %d comparacoes para encontra-lo\n", valor_busca, pos, qtd_comp);
		}
	}

	return 0;
}
```

# Veja abaixo uma comparação entre a busca linear e a busca binária:
![Comparação entre busca binária e busca linear](comp.gif)
