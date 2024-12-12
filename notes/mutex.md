# Mutexes
## contador.c
O valor do contador não é zero e muda a cada execução porque as threads estão acessando a variável compartilhada sem sincronização.
A solução é usar mutex (para implementar exclusão mútua) para sincronizar o acesso a variável compartilhada.
## Usando mutexes
O try_lock retorna 0 se conseguiu fazer o lock, e qualquer número diferente de 0 significa que ele não conseguiu.

## Para o Projeto
```
Variáveis de condição obrigatoriamente tem que ser usadas junto com um mutex.
```
Signal só acorda uma thread naquela variável de condição, mesmo se houver mais de uma. Broadcast acorda todas as threads naquela variável de condição. **No geral, Eduardo recomenda utilizar o Broadcast.**

## Produtor-Consumidor
**Empty** é usado quando há pelo menos 1 entrada vazia, e o **fill** quando tem pelo menos uma entrada preenchida do buffer.
O **join** faz com que a main espere pelas threads. Poderia ser usado wait.

Utilizamos **while** e não if em `try_lock.c` porque evita falsa sinalização (spurious wakeup), ou seja, o produtor/consumidor receber uma mensagem de que pode acordar, mas não ser o momento adequado.

# Barreiras
Técnica de sincronização de múltiplas threads, onde elas só são acordadas para executar quando todas threads alcançam a barreira (até lá, ficam esperando até todas chegarem). 
```
Necessário informar a quantidade de threads
```
Não pode ser de forma estática, só dinâmica.

Dependendo do compilador, usar o #define _XOPEN_SOURCE 600 ou usar -D_XOPEN_SOURCE=600.
```
gcc -D_XOPEN_SOURCE=600 {restante da execução}
```
