# Análise e Comparação de Eficiência com Algoritmos de Ordenação em C++

###### Artigo escrito em markdown por meio do Github Gist

###### Tempo médio de leitura: 18 minutos

###### Autores: Guilherme Gomes de Medeiros e Jamily Kelly Silva Gomes

## Introdução

Durante a disciplina de estrutura de dados ministrada no 3° período do curso de Tecnologia em Sistemas para Internet (TSI) foi proposto que implementássemos os algoritmos de ordenação apresentados em sala, e que apartir deles fosse realizada uma análise e comparação acerca do tempo de execução de cada um, de forma que se torne possivel visualizar de forma mais clara a discrepância de eficiência entre de cada algoritmo.

### Algoritmos de Ordenação

Os Algoritmos de ordenação são uma parte fundamental da ciência da computação, eles permitem que os programadores organizem e classifiquem grandes quantidades de dados de forma rápida e eficiente. Dentre os muitos algoritmos de ordenação disponíveis, este artigo irá tratar sobre alguns dos mais comuns, que incluem: o Bubble Sort, Selection Sort, Insertion Sort, Shell Sort, Quick Sort e Merge Sort.
Caso se interesse, você poderá acessar o código detalhado de cada algoritmo aqui: [Link do repositório](https://github.com/Guilherme-07062002/EstruturaDeDados.git)

Abaixo examinar cada um desses algoritmos em detalhes:

* Bubble Sort - O Bubble Sort é um algoritmo simples de ordenação que funciona comparando elementos adjacentes em uma lista, realizando a comparação do elemento atual com o seu sucessor e trocando os valores caso o antecessor seja maior que o que vem em seguida. Ele continua fazendo essas substituições até que toda a lista esteja em ordem, embora seja fácil de entender e implementar, o Bubble Sort tem uma complexidade de tempo de O(n²), o que significa que seu desempenho pode ser bastante lento em listas grandes.

* Selection Sort - Este começa encontrando o menor elemento em uma lista e colocando-o na primeira posição, em seguida, ele encontra o próximo menor elemento e o coloca na segunda posição, e assim por diante até que toda a lista esteja ordenada. Como o Bubble Sort, o Selection Sort também tem uma complexidade de tempo de O(n²), o que o torna ineficiente em listas muito grandes.  

* Insertion Sort - É de certa forma semelhante ao Bubble Sort, a diferença é que ele realiza comparações consecutivas, checando se o valor atual é menor que cada elemento anterior a ele na lista. Ele começa com o primeiro elemento e o compara com seus antecessores, realizando o "swap" caso necessário. Em seguida, ele pega o próximo elemento e o insere na posição correta, ordenando os valores progressivamente. Esse processo continua sendo feito para cada elemento subsequente até que toda a lista esteja em ordem. O Insertion Sort tem uma complexidade de tempo média de O(n²), mas é mais rápido do que o Bubble Sort e o Selection Sort em listas pequenas.

* Shell Sort - O Shell Sort é um algoritmo de ordenação que tem um desempenho melhor que o Insertion Sort. Primeiramente é obtido o 'gap', que consiste em (n / 2), aonde n é o tamanho do array, em seguida é realizado a comparação entre o elemento atual e o elemento que está a um gap de distância do mesmo, depois que essa checagem é feita em toda a lista, reinicia-se novamente o processo dividindo novamente o valor de gap por 2 dessa forma gap = ((n / 2) / 2) ou (n / 4), esse processo é repetido quantas vezes for necessário até que em determinado momento "gap" seja 1, e a lista esteja ordenada. Portanto aos poucos ele reduz a distância entre os elementos  nos subgrupos e repete o processo. O Shell Sort tem uma complexidade de tempo média de O(n log n), o que o torna mais rápido do que o Bubble Sort, o Selection Sort e o Insertion Sort em listas maiores.

* Quick Sort - Utiliza a abordagem "dividir e conquistar", ele divide a lista em dois subconjuntos menores, um com elementos maiores do que um valor escolhido (pivô) e outro com elementos menores. Em seguida, ele ordena recursivamente cada subconjunto e os une para produzir uma lista ordenada completa. O Quick Sort é um dos algoritmos de ordenação mais eficientes, com uma complexidade de tempo média de O(n log n), mas pode ser mais lento em listas quase ordenadas.

* Merge Sort - De forma similar ao Quick Sort, o Merge Sort divide a lista em subconjuntos menores recursivamente, até que o agrupamento de valores seja reduzida a apenas um elemento. Em seguida, ele junta esses subgrupos, ordenando-os, até que a lista original esteja completamente organizada. Esse processo de "dividir e conquistar" permite que o Merge Sort alcance uma complexidade de tempo média de O(n log n). O processo de junção dos subconjuntos é chamado de "merge", ele basicamente se consiste em comparar os primeiros elementos de cada subconjunto e colocar o menor deles na lista de saída, dessa forma O processo é repetido até que todos os elementos dos subconjuntos tenham sido adicionados à lista de saída.

## Metodologia

### Automatização com shell script

Após criado o repositório no github para armazenar os códigos de cada algoritmo, foi necessário pensar em como realizariamos a análise.

Antes de tudo, criamos na pasta do projeto um script em shell que automatiza a execução de cada algoritmo, por meio do comando `./cmd`.

###### Saída do terminal que fornece interação com o usuário

![print1](./imgs/print1.png)

Dessa forma caso o programador deseje testar um único algoritmo não é necessário que a cada alteração o usuário tenha que executar o comando `g++ <nome-do-arquivo> -o executavel` para compilar o código, pois o script automatiza esse processo, resumindo a compilação e execução de todos os algoritmos a um único comando.

No entanto, para a comparação, criamos um arquivo main.cpp que contém todas as funções que executam cada algoritmo, ele cria um único array com valores aleatórios e passa ele como paramêtro para cada método, por fim, exibe no terminal o tempo que foi necessário para as ordenações em segundos e milissegundos.

###### Trecho da saída no terminal, exibindo os tempos de execução para cada algoritmo

![print2](./imgs/print2.png)

### Bibliotecas auxiliares

A linguagem de programação C++ oferece muitas bibliotecas padrão que fornecem recursos poderosos e flexíveis para manipulação de dados, geração de números aleatórios e medição de tempo. Neste artigo, falaremos sobre as bibliotecas que utilizamos neste projeto:

* Vector -
    A biblioteca vector é usada para criar vetores dinâmicos ou seja, coleções de elementos de tamanho variável que podem ser adicionados ou removidos facilmente. Um vetor dinâmico é essencialmente um array que pode mudar de tamanho durante a execução do programa.

```C++
   #include <vector>
   
   int valor = 5;
   
   // Declaraçao do array
   vector<int> vetor;
   
   // Inserção dinâmica de elementos por meio do push_back
   vetor.push_back(valor);
```

* Random -
    É usada para a geração de números aleatórios em C++, ela oferece vários tipos de distribuição, como a distribuição uniforme, a distribuição normal e a distribuição de Poisson, Além disso possui diferentes motores de geração de números aleatórios, que são usados para produzir diferentes sequências de valores.

```C++
    #include <iostream>
    #include <vector>
    #include <random>
    
    
    // Gerador de números aleatórios utilizando um valor de semente fixo
    std::mt19937 rng(1234);

    // Criação de uma distribuição uniforme no intervalo de 0 a 99
    std::uniform_int_distribution<int> dist(0, 99);

    // Declaração do vetor dinâmico com <vector>
    vector<int> lista;

    // Obtendo do usuário o tamanho do vetor
    int tamanho;
    cout << "Tamanho do array: ";
    cin >> tamanho;

    // Preenchendo vetor com números aleatórios 
    for (int i = 0; i < tamanho; i++)
    {
        int rand_num = dist(rng);
        // Com o push_back, insere cada valor no fim do vetor
        lista.push_back(rand_num);
    }
```

* Chrono -
    É usada para lidar com tempo e medir a duração de um programa. Ela fornece um conjunto de classes para lidar com diferentes unidades de medição e realizar operações com elas.

Abaixo um exemplo de como coletamos o tempo de execução das funções:

```C++
   #include <chrono>
   
   
   // marca o tempo de início
   auto start = std::chrono::high_resolution_clock::now(); 
   
   // executa o algoritmo que queremos medir o tempo
   bubbleSort(lista); 
   
   // marca o tempo de término
   auto end = std::chrono::high_resolution_clock::now(); 
   
   // calcula o intervalo de tempo
   std::chrono::duration<double, std::milli> diff = end - start; 
   
   // exibe o tempo de execução em segundos e milissegundos
   cout << "\nPara um array aleatório de tamanho " << tamanho << endl;
   cout << "Tempo de execucao do Bubble Sort: \n"
        << diff.count() / 1000 << " segundos \n"
        << fmod(diff.count(), 1000) << " milissegundos\n"; 
```

Dessa forma o algoritmo realiza a cada execução a ordenação de um vetor de números aleatórios com a quantidade de elementos que o usuário informar.

Na execução do código de cada algoritmo, o usuário informa a quantidade de elementos do vetor que será ordenado, esse array é preenchido por meio de um loop for com números aleatórios entre 0 a 99.

Para que fosse possivel inserirmos dinâmicamente os elementos do array a cada repetição do laço, utilizamos a biblioteca `vector` por meio do método push_back() que adiciona cada valor ao fim do array. Dentro do parametro da função é passado o número aleatório armazenado, este que é gerado graças a importação do `random`.

Além disso para obtermos o tempo de execução de cada algoritmo, utilizamos o `chrono`, aonde por meio deste delimitamos o trecho específico de código em que o tempo seria capturado, marcando o ponto de início e fim da execução do algoritmo.

Após isso, é realizado o cálculo da diferença entre o intervalo cronometrado, exibindo na tela a quantidade de tempo necessária para a execução do algoritmo em segundos e milissegundos.

## Resultados

O arquivo main do repositório, possui o código com as funções equivalentes a cada um dos algoritmo de ordenação citados acima neste artigo, lá é criado um único vetor com elementos ordenados aleatoriamente, a cada ordenação a lista é restaurada para seu estado original, por meio de outro array que armazena uma cópia dos valores iniciais da lista, dessa forma dessa forma foi possivel realizar os testes com cada algoritmo ordenando o mesmo array, armazenando em uma planilha o tempo necessário em milissegundos de cada execução para vetores com 1000(Mil), 10.000(Dez mil) e 100.000(Cem mil) elementos.

###### Tabela com os dados coletados

|                | Mil   | Dez Mil | Cem Mil |
| -------------- | ----- | ------- | ------- |
| Bubble Sort    | 13.1  | 873.2   | 851.44  |
| Selection Sort | 5.294 | 262.964 | 307.99  |
| Insertion Sort | 2.719 | 175.022 | 277.44  |
| Shell Sort     | 0.257 | 2.555   | 29.362  |
| Quick Sort     | 0.905 | 35.203  | 156.006 |
| Merge Sort     | 0.798 | 6.111   | 64.970  |

### Visualização e análise dos dados

Para a análise, utilizamos a linguagem Python devido a sua versatilidade e o fato de que ela ser utilizada em diversas aplicações, e uma dessas é a visualização de dados, em que bibliotecas como o pandas e o matplotlib se destacam.

* pandas -
   O pandas é uma biblioteca de código aberto que fornece estruturas de dados flexíveis e de alto desempenho para análise de dados. Com ele, é possível manipular e analisar facilmente dados em tabelas, incluindo operações de filtragem, agregação e pivotagem.

* matplotlib -
   Já o matplotlib é uma biblioteca de visualização de dados 2D que produz gráficos de alta qualidade em vários formatos, é possível criar gráficos de vários tipos, como o de linhas, barras e dispersão, além de poder personalizar completamente a aparência dos mesmos.

```python
   import pandas as pd
   import matplotlib.pyplot as plt
   %matplotlib inline

   data = {
       'Algoritmo': ['Bubble Sort', 'Selection Sort', 'Insertion Sort', 'Shell Sort', 'Quick Sort', 'Merge Sort'],
       '1,000(Mil) elementos': [13.1, 5.29, 2.71, 0.257, 0.90, 0.79],
       '10,000(Dez mil) elementos': [873.2, 262.9, 175.0, 2.55, 0.16, 2.8],
       '100,000(Cem mil) elementos': [851.44, 307.99, 277.44, 29.3, 6.888, 1.58]
   }

   df = pd.DataFrame(data)

   # Gráfico para 1,000(Mil) elementos
   df.plot(kind='line', x='Algoritmo', y='1,000(Mil) elementos',
           title='Tempo de Execução dos Algoritmos - 1,000(Mil) elementos')
   plt.ylabel('Tempo (ms)')

   # Gráfico para 10,000(Dez mil) elementos
   df.plot(kind='line', x='Algoritmo', y='10,000(Dez mil) elementos',
           title='Tempo de Execução dos Algoritmos - 10,000(Dez mil) elementos')
   plt.ylabel('Tempo (ms)')

   # Gráfico para 100,000(Cem mil) elementos
   df.plot(kind='line', x='Algoritmo', y='100,000(Cem mil) elementos',
           title='Tempo de Execução dos Algoritmos - 100,000(Cem mil) elementos')
   plt.ylabel('Tempo (ms)')

   plt.show()

```

Utilizando essas duas bibliotecas em conjunto, criamos os gráficos mostrados abaixo para uma melhor visualização dos dados coletados.

###### Gráfico 1 -

![mil](./imgs/mil.png)

###### Gráfico 2 -

![dezMil](./imgs/dezMil.png)

###### Gráfico 3 -

![cemMil](./imgs/cemMil.png)

Da esquerda para a direita estão sendo exibidos os algoritmos considerados mais eficientes em ordenação.

Nesta análise, temos os tempos de execução, em milissegundos, de seis diferentes algoritmos de ordenação (Bubble Sort, Selection Sort, Insertion Sort, Shell Sort, Quick Sort e Merge Sort) para três tamanhos de listas diferentes (1.000, 10.000 e 100.000 elementos).

Em cada gráfico é possivel observar a diferença entre o tempo de execução de cada um e o quanto isso depende do tamanho da entrada, alguns algoritmos possuem uma eficiência significativa em vetores maiores, porém tem uma menor eficácia em conjuntos com número menor de elementos, e o oposto também acontece.

Analisando os resultados, podemos observar que o Bubble Sort é o algoritmo de ordenação mais lento em todos os casos, apresentando um tempo de execução muito maior do que os outros algoritmos, mesmo em listas com apenas 1.000 elementos, o tempo de execução do Bubble Sort já é significativamente maior do que os outros algoritmos.

Já o Selection Sort, Insertion Sort, Shell Sort e Quick Sort apresentam tempos de execução semelhantes em listas com 1.000 elementos, mas a diferença começa a se destacar em listas maiores, também é notável que o Quick Sort se mostra muito eficiente em listas de 10.000 e 100.000 elementos, apresentando tempos de execução significativamente menores do que os outros algoritmos, o Shell Sort apresenta um bom desempenho em listas grandes, mas é superado pelo Quick Sort.

Por fim, temos o Merge Sort, que se destaca por apresentar tempos de execução menores em listas com 100.000 elementos em comparação com os outros algoritmos, exceto pelo Quick Sort. O Merge Sort é um algoritmo muito eficiente para lidar com listas grandes, mas pode não ser a melhor opção em listas menores.

## Conclusão

Em resumo, esta análise reforça a importância de escolher um algoritmo de ordenação adequado para o tamanho da lista a ser ordenada, em listas menores, a diferença de tempo de execução entre os algoritmos não é tão notável e pode não ter um impacto significativo, mas em listas maiores, a escolha do algoritmo certo pode fazer uma grande diferença na eficiência da execução. O Quick Sort se mostra como uma opção muito eficiente em geral, mas é importante avaliar o tamanho da lista a ser ordenada e considerar outras opções como o Merge Sort para listas maiores.

No entanto, vale ressaltar que os dados deste trabalho foram coletados e analisados com a finalidade de realizar esse estudo, os tempos de execução podem variar dependendo do hardware utilizado para a execução dos algoritmos, da linguagem de programação que está sendo usada, e do próprio algoritmo em si. Portanto, é importante considerar esses fatores ao interpretar os resultados.

## Referências

Documentação C++ - <https://devdocs.io/cpp/>

Documentação pandas - <https://pandas.pydata.org/docs/>

Documentação matplotlib - <https://matplotlib.org/stable/users/index.html>
