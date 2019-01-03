# Motivação
Como encontrar um número que esteja em um array de maneira simples?

# Maneira corriqueira
Uma buscas consiste em simplesmente percorrer todo o array até encontrar o elemento. a depender do tamanho do array o custo para isso pode ser muito grande, pois o elemento buscado pode estar muito longe no array(pra um array de 1.000.000 de posições, se o elemento estiver na ultima posição, serão necessárias 1.000.000 de comparações para obter-se onde o elemento está).

### Veja abaixo um exemplo de uma busca sequencial em C

```C
#include<stdio.h>

int main() {
	int array[1000000], i, valor_busca, flag;
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
		// faz a busca comparando valor a valor até encontrar o valor desejado
		for(i = 0; i < 1000000; i++) {
			if(valor_busca == array[i]) {
				printf("%d esta na posicao: %d\nForam necessarias %d comparacoes para encontra-lo\n", valor_busca, i, i + 1);
				flag = 1;
				break;
			}
		}
		if(!flag) {
			printf("%d nao encontrado\nForam feitas 1000000 comparacoes para chegar a isso\n", valor_busca);
		}
	}
	return 0;
}
```