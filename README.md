# Resumo sobre Listas Dinâmicas

## 1️⃣ Introdução às Listas Dinâmicas

### Definição de lista dinâmica
Uma lista dinâmica é uma estrutura de dados que armazena elementos de forma não contígua na memória, utilizando ponteiros para ligar os elementos entre si. Diferente dos arrays, que possuem tamanho fixo, as listas dinâmicas podem crescer ou diminuir conforme necessário.

### Comparação entre listas estáticas (arrays) e listas dinâmicas
| Característica | Arrays (Listas Estáticas) | Listas Dinâmicas |
|--------------|--------------------|----------------|
| Alocação de Memória | Pré-definida, tamanho fixo | Alocação dinâmica, cresce conforme necessário |
| Acesso aos Elementos | Direto (índices) | Sequencial (através de ponteiros) |
| Uso de Memória | Pode desperdiçar espaço se subutilizado | Usa apenas a memória necessária |
| Tempo de Acesso | Rápido (O(1)) | Mais lento (O(n)) |
| Inserção/Remoção | Custosa, pois exige realocação | Mais eficiente, sem necessidade de deslocamento |

### Vantagens e desvantagens
**Vantagens das listas dinâmicas:**
- Permitem um uso mais eficiente da memória.
- Facilitam inserções e remoções sem necessidade de deslocamento.

**Desvantagens:**
- O tempo de acesso é mais lento em comparação a arrays.
- Requer gerenciamento de memória manual com `malloc()` e `free()`.

## 2️⃣ Estrutura de uma Lista Dinâmica
Uma lista dinâmica em C geralmente é implementada como uma **lista encadeada**, onde cada nó contém:
- Um **valor**.
- Um **ponteiro** para o próximo nó da lista.

Exemplo de estrutura para um nó de lista encadeada em C:
```c
struct Node {
    int dado;
    struct Node* proximo;
};
```

## 3️⃣ Operações Básicas

### Criação e Inicialização
Para iniciar uma lista dinâmica, declaramos um ponteiro do tipo `struct Node*`, inicialmente apontando para `NULL`.
```c
struct Node* inicio = NULL;
```

### Inserção
Para inserir um novo nó no início da lista:
```c
struct Node* novoNo = (struct Node*) malloc(sizeof(struct Node));
novoNo->dado = valor;
novoNo->proximo = inicio;
inicio = novoNo;
```

### Remoção
Para remover o primeiro elemento da lista:
```c
struct Node* temp = inicio;
inicio = inicio->proximo;
free(temp);
```

## 4️⃣ Implementação em C
Aqui está uma implementação completa de uma lista encadeada em C, incluindo inserção e remoção:
```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int dado;
    struct Node* proximo;
};

void inserir(struct Node** inicio, int valor) {
    struct Node* novoNo = (struct Node*) malloc(sizeof(struct Node));
    novoNo->dado = valor;
    novoNo->proximo = *inicio;
    *inicio = novoNo;
}

void remover(struct Node** inicio) {
    if (*inicio == NULL) return;
    struct Node* temp = *inicio;
    *inicio = (*inicio)->proximo;
    free(temp);
}

void imprimir(struct Node* inicio) {
    while (inicio != NULL) {
        printf("%d -> ", inicio->dado);
        inicio = inicio->proximo;
    }
    printf("NULL\n");
}

int main() {
    struct Node* lista = NULL;
    inserir(&lista, 10);
    inserir(&lista, 20);
    inserir(&lista, 30);
    imprimir(lista);
    remover(&lista);
    imprimir(lista);
    return 0;
}
```

## 5️⃣ Referências
Brian W. Kernighan, Dennis M. Ritchie - *C: A Linguagem de Programação - Padrão ANSI*, Capítulos 5 e 6.
