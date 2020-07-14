# **Busca em Profundidade**
Na teoria dos grafos, busca em profundidade (também conhecido em inglês por Depth-First Search - DFS) é um algoritmo usado para realizar uma busca ou travessia em um grafo. Intuitivamente, o algoritmo começa num nó raiz e explora tanto quanto possível cada um dos seus ramos, antes de retroceder(backtracking).

## **Definição**
Formalmente, um algoritmo de busca em profundidade realiza uma busca não-informada que progride através da expansão do primeiro nó filho da árvore de busca, e se aprofunda cada vez mais, até que o alvo da busca seja encontrado ou até que ele se depare com um nó que não possui filhos (nó folha). Então a busca retrocede (backtrack) e começa no próximo nó. Numa implementação não-recursiva, todos os nós expandidos recentemente são adicionados a uma pilha, para realizar a exploração.

### **Complexidade de tempo**
A complexidade do algoritmo é proporcional ao número de vértices n somados ao número de arestas m do grafo ao qual ele atravessa, O(m + n).

### **Pseudocódigo**
    Algoritmo BuscaEmProfundidade(G)
      Para cada u ∈ V(G) faça       // inicializando a base dos dados
        cor[u] ← branco             // cor[] indica quais vertices foram visitados
        π[u] ← nulo                 // π[j] guarda o pai de j, o vertice atravéz do qual j foi descoberto
      tempo ← 0
      Para cada u ∈ V(G) faça       // visitando todos os vertices
        Se cor[u] = branco
          DFS-visita(u)
    
    Algoritmo DFS-visita(u)
      cor[u] ← cinza
      tempo ← tempo + 1
      d[u] ← tempo                  // d[u]: passo em que u é descoberto 
      Para cada v ∈ Adj[u] faça
        Se cor[v] = branco então
          π[v] ← u
          DFS-visita(v)
      cor[u] ← preto
      tempo ← tempo + 1
      f[u] ← tempo                  // f[u]: passo em que u tem sua visita concluida
    

### **Exemplo de implementação em C++**

    int tempo = 0;
    void BuscaEmProfundidade(G){
      int numV = G->NumVertices;            // obtendo o numero de vertices
      vector<bool> visitados(numV, false);
      vector<int> pai(numV, -1);
      vector<int> d(numV, 0);               // d[u]: passo em que u é descoberto 
      vector<int> f(numV, 0);               // f[u]: passo em que u tem sua visita concluida

      for(int i = 0; i < numV; i++){
        if(visitados[i] == false){
          DFSvisita(i, G, visitados, pai, d, f);
        }
      }
    }

    void DFSvisita(u, G, visitados, pai, d, f){
      visitados[u] = true;
      tempo++;
      d[u] = tempo;
      for(auto it = G->adj[u].begin(); it != G->adj[u].end(); it++){
        if(!visitados[*it]){
          pai[*it] = u;
          DFSvisita(*it);
        }
      }
      visitados[u] = true;
      tempo++;
      f[u] = tempo;
    }