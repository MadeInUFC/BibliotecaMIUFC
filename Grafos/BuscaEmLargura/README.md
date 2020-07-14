# **Busca em Largura**
Na teoria dos grafos, busca em largura (ou busca em amplitude, também conhecido em inglês por Breadth-First Search - BFS) é um algoritmo de busca em grafos utilizado para realizar uma busca ou travessia num grafo. Intuitivamente, você começa pelo vértice raiz e explora todos os vértices vizinhos. Então, para cada um desses vértices mais próximos, exploramos os seus vértices vizinhos inexplorados e assim por diante, até que ele encontre o alvo da busca.

## **Definição**
Formalmente, uma busca em largura é um método de busca não-informada (ou desinformada) que expande e examina sistematicamente todos os vértices de um grafo direcionado ou não-direcionado. Em outras palavras, podemos dizer que o algoritmo realiza uma busca exaustiva num grafo passando por todas as arestas e vértices do grafo. Sendo assim, o algoritmo deve garantir que nenhum vértice ou aresta será visitado mais de uma vez e, para isso, utiliza uma estrutura de dados fila para garantir a ordem de chegada dos vértices. Dessa maneira, as visitas aos vértices são realizadas através da ordem de chegada na estrutura fila e um vértice que já foi marcado não pode entrar novamente a esta estrutura.

### **Complexidade de tempo**
Considerando um grafo representado em listas de adjacência, o pior caso, aquele em que todos os vértices e arestas são explorados pelo algoritmo, a complexidade de tempo pode ser representada pela seguinte expressão O(|E|+|V|), onde |E| significa o tempo total gasto nas operações sobre todas as arestas do grafo onde cada operação requer um tempo constante O(1) sobre uma aresta, e |V| que significa o número de operações sobre todos os vértices que possui uma complexidade constante O(1) para cada vértice uma vez que todo vértice é enfileirado e desenfileirado uma unica vez.

### **Pseudocódigo**

    Algoritmo BuscaEmLargura(G, s)
      Para cada v ∈ V(G) faça       // inicializando a base dos dados
        cor[v] ← branco             // cor[] indica quais vertices foram visitados
        d[v] ← ∞                    // d[] guarda a distancia de s para todos os outros vertices
        π[v] ← null                 // π[j] guarda o pai de j, o vertice atravéz do qual j foi descoberto
      cor[s] ← cinza                // como s é a raiz, é o primeiro a ser visitado
      d[s] ← 0                      // distância de s para ele mesmo é 0
      Q ← Ø                         // criando uma fila
      Enfila(Q, s)                  // enfilando o vertice raiz
      Enquanto Q ≠ Ø faça           // enquanto houver vertices a visitar
        u ← Desenfila(Q)            // desenfilando um vertice u
        Para cada v ∈ Adj[u] faça   // visitando os vertices vizinhos/adjacentes ao recém desenfilado u
          Se cor[v] = branco        // se esse vizinho v ainda não foi visitado
            d[v] ← d[u] + 1         // a distância de v para a raiz será a distância de u mais 1
            π[v] ← u                // u será o pai de v
            cor[v] ← cinza          // marcando v como visitado
            Enfila(Q, v)            // enfilando v para visitar seus vizinhos ainda não visitados
        cor[u] ← preto              // informando que todos os vizinhos de u foram descobertos

### **Exemplo de implementação em C++**

    void BuscaEmLargura(Grafo *G, int raiz){
      int numV = G->NumVertices;                // obtendo o numero de vertices
      vector<bool> visitados(numV, false);      // inicializando com 0's o vetor que marca os vertices visitados
      vector<int> distancia(numV, 2147483647);  // inicializando o vetor de distâncias com um número para simular o infinito
      vector<int> pai(numV, -1);                // inicializando com -1 o vetor que marca os pais dos vertices descobertos

      visitados[raiz] = true;
      distancia[raiz] = 0;
      queue<int> fila;
      fila.push(raiz);

      while(!fila.empty()){
        int u = fila.front();                   // desenfilando o vertice
        fila.pop();                             // removendo o vertice da fila

        for(auto it = G->adj[u].begin(); it != G->adj[u].end(); it++){
          if(!visitados[*it]){
            distancia[*it] = distancia[u] + 1;  // setando a distancia
            pai[*it] = u;                       // setando o pai
            visitados[*it] = true;              // marca como visitado
            fila.push(*it);                     // insere na fila
          }
        }
      }
    }