Rota Inteligente: Otimização de Entregas com Algoritmos de IA



Este projeto implementa uma solução inteligente para otimizar rotas de entrega para a empresa "Sabor Express", utilizando algoritmos de Inteligência Artificial para encontrar os menores caminhos em um grafo e agrupar pontos de entrega geograficamente próximos.



\## 1. Descrição do Problema, Desafio Proposto e Objetivos



\### Descrição do Problema

A empresa "Sabor Express", um serviço de delivery de alimentos na região central da cidade, enfrenta sérios desafios durante horários de pico. As entregas são frequentemente atrasadas devido a rotas ineficientes, definidas manualmente com base apenas na experiência dos entregadores. Isso resulta em aumento de custos com combustível e, crucialmente, insatisfação dos clientes, ameaçando a competitividade da empresa.



\### Desafio Proposto

Desenvolver uma solução inteligente, utilizando algoritmos de Inteligência Artificial, para otimizar as rotas de entrega. A cidade será modelada como um grafo, onde nós representam locais de entrega e arestas representam ruas com pesos (distância/tempo). O objetivo é encontrar os menores caminhos entre múltiplos pontos de entrega e, em situações de alta demanda, agrupar entregas próximas utilizando algoritmos de clustering.



\### Objetivos

\*   Reduzir o tempo de entrega e o custo de combustível.

\*   Aumentar a satisfação dos clientes.

\*   Automatizar e otimizar o planejamento de rotas.

\*   Demonstrar a aplicação de algoritmos de busca em grafos (Dijkstra) e aprendizado não supervisionado (K-Means).



\## 2. Explicação Detalhada da Abordagem Adotada



A solução proposta divide-se em duas etapas principais:



\### Modelagem da Cidade como um Grafo e Busca do Menor Caminho:

\*   \*\*Representação:\*\* A cidade é modelada como um grafo utilizando a biblioteca `networkx` em Python. Cada local de entrega (bairro, restaurante, casa do cliente) é um nó do grafo, e as ruas que conectam esses locais são as arestas. Cada aresta possui um peso, que representa a distância ou o tempo estimado para percorrer aquela rua. Os dados do grafo são lidos de um arquivo CSV (`data/grafo\_cidade.csv`).

\*   \*\*Algoritmo de Busca:\*\* Para encontrar a rota mais eficiente entre dois pontos, utilizamos o algoritmo de Dijkstra (implementado via `networkx.dijkstra\_path`). Este algoritmo garante que o caminho encontrado entre um ponto de partida e um ponto de destino terá o menor peso acumulado (menor distância ou tempo).



\### Agrupamento de Entregas com K-Means (Clustering):

\*   \*\*Cenário:\*\* Em momentos de alta demanda, com muitos pedidos distribuídos pela cidade, torna-se ineficiente que cada entregador faça apenas uma entrega por vez.

\*   \*\*Algoritmo:\*\* Para otimizar o trabalho dos entregadores, aplicamos o algoritmo de K-Means (da biblioteca `scikit-learn`). O K-Means agrupa automaticamente os pontos de entrega (representados por suas coordenadas geográficas, lidas de `data/pontos\_entrega.csv`) em um número `K` de clusters (grupos), onde `K` pode ser o número de entregadores disponíveis ou o número ideal de rotas a serem geradas.

\*   \*\*Benefício:\*\* Cada cluster representa uma "zona" de entregas próximas. Um entregador pode então ser designado para um cluster e planejar sua rota para visitar todos os pontos dentro daquele grupo de forma eficiente, minimizando o deslocamento total.



\## 3. Algoritmos Utilizados



\*   \*\*Dijkstra:\*\* Algoritmo de busca de menor caminho em grafos ponderados, garantindo a rota mais eficiente entre dois pontos. É uma base fundamental para sistemas de GPS e otimização de rotas.

\*   \*\*K-Means:\*\* Algoritmo de clustering (aprendizado não supervisionado) que particiona N observações em K clusters, onde cada observação pertence ao cluster cujo centroide é o mais próximo. Ideal para agrupar pontos de entrega geograficamente próximos.



\## 4. Diagrama do Grafo/Modelo Usado na Solução



Aqui estão representações visuais do grafo utilizado para simular a cidade e o agrupamento de entregas, geradas pelo código.



\### Grafo da Cidade

!\[Grafo da Cidade](outputs/grafo\_visualizado.png)

Diagrama ilustrando os bairros (nós) e as ruas (arestas) com seus respectivos pesos (distância/tempo).



\### Menor Caminho Encontrado

!\[Menor Caminho](outputs/grafo\_menor\_caminho.png)

Visualização de um exemplo de menor caminho entre dois pontos no grafo, destacado em verde.



\### Agrupamento de Entregas (K-Means)

!\[Agrupamento de K-Means](outputs/agrupamento\_kmeans.png)

Gráfico mostrando pontos de entrega agrupados em 3 clusters distintos pelo algoritmo K-Means. Os "X" pretos indicam os centroides de cada cluster, e as diferentes cores representam os grupos de entregas próximas.



\## 5. Análise dos Resultados, Eficiência da Solução, Limitações Encontradas e Sugestões de Melhoria



\### Análise dos Resultados

A aplicação do algoritmo de Dijkstra demonstrou a capacidade de identificar o caminho mais curto/rápido entre quaisquer dois pontos no grafo, o que é crucial para otimizar viagens individuais. O K-Means conseguiu agrupar de forma eficaz os pontos de entrega geograficamente próximos, o que permite a criação de rotas otimizadas para múltiplos entregadores, reduzindo a distância total percorrida e o tempo de entrega.



\### Eficiência da Solução

A combinação de grafos, Dijkstra e K-Means oferece uma base robusta para a otimização de rotas. Ambos os algoritmos são eficientes para suas respectivas tarefas, proporcionando uma melhoria significativa em relação ao planejamento manual, resultando em:

\*   Redução de custos operacionais (combustível).

\*   Maior agilidade nas entregas.

\*   Melhora na satisfação do cliente.



\### Limitações Encontradas

\*   \*\*Dados Estáticos:\*\* A implementação atual utiliza um grafo estático e coordenadas fixas. Em um cenário real, os dados de tráfego (pesos das arestas) são dinâmicos e mudam constantemente.

\*   \*\*Problema do Caixeiro Viajante (TSP) dentro dos Clusters:\*\* Após o agrupamento, a otimização da rota dentro de cada cluster para visitar todos os pontos uma única vez na ordem mais eficiente é um problema do Caixeiro Viajante (TSP), que é NP-Hard (muito difícil de resolver de forma ótima para muitos pontos). Nossa solução atual não implementa uma heurística TSP avançada para esta fase.

\*   \*\*Capacidade dos Entregadores:\*\* Não foram consideradas restrições de capacidade dos entregadores (ex: quantos pedidos podem levar, tempo máximo de rota).

\*   \*\*Modelo Simplificado:\*\* O grafo atual é pequeno e idealizado. Cidades reais são muito mais complexas.



\### Sugestões de Melhoria

\*   \*\*Dados em Tempo Real:\*\* Integrar APIs de mapas (Google Maps, OpenStreetMap) para obter dados de tráfego em tempo real e atualizar dinamicamente os pesos das arestas.

\*   \*\*Heurísticas TSP:\*\* Implementar algoritmos heurísticos ou meta-heurísticos (ex: algoritmo genético, simulated annealing, busca tabu) para resolver o problema do Caixeiro Viajante de forma aproximada dentro de cada cluster, otimizando a sequência de entregas.

\*   \*\*Algoritmo A\\\*:\*\* Para grafos muito grandes, substituir Dijkstra por A\\\* para maior eficiência na busca do menor caminho, utilizando uma função heurística (ex: distância euclidiana até o destino).

\*   \*\*Restrições de Negócio:\*\* Adicionar lógica para considerar capacidade dos veículos, janelas de tempo de entrega, e prioridades de pedidos.

\*   \*\*Interface Gráfica:\*\* Desenvolver uma interface gráfica para os entregadores visualizarem suas rotas otimizadas diretamente em um mapa.

\*   \*\*Outros Algoritmos de Clustering:\*\* Explorar outros algoritmos de clustering como DBSCAN para comparar a qualidade dos agrupamentos.



\## 6. Instruções para Execução do Projeto



Para executar este projeto localmente no seu computador, siga os passos abaixo:



\*\*Pré-requisitos:\*\*

\*   Python 3.x instalado

\*   Pip (gerenciador de pacotes do Python)

\*   Git (para clonar o repositório)



\*\*Passo a passo:\*\*



1\.  \*\*Clone o Repositório:\*\*

&nbsp;   Abra o terminal (ou prompt de comando) e clone este repositório para o seu computador. Navegue para a pasta `rota\_inteligente\_ia`:

&nbsp;   ```bash

&nbsp;   git clone \[LINK\_DO\_SEU\_REPOSITORIO\_GITHUB]

&nbsp;   cd rota\_inteligente\_ia

&nbsp;   ```

&nbsp;   (Substitua `\[LINK\_DO\_SEU\_REPOSITORIO\_GITHUB]` pelo link real do seu repositório quando ele estiver no GitHub.)



2\.  \*\*Crie e Ative um Ambiente Virtual (Opcional, mas Recomendado):\*\*

&nbsp;   É uma boa prática para isolar as dependências do projeto. Execute estes comandos na raiz da pasta `rota\_inteligente\_ia`:

&nbsp;   ```bash

&nbsp;   python -m venv venv

&nbsp;   # No Windows (PowerShell):

&nbsp;   .\\venv\\Scripts\\Activate

&nbsp;   # No Windows (Command Prompt):

&nbsp;   .\\venv\\Scripts\\activate.bat

&nbsp;   # No macOS/Linux:

&nbsp;   source venv/bin/activate

&nbsp;   ```



3\.  \*\*Instale as Dependências:\*\*

&nbsp;   Com o ambiente virtual ativado, instale todas as bibliotecas necessárias usando o `requirements.txt`:

&nbsp;   ```bash

&nbsp;   pip install -r requirements.txt

&nbsp;   ```



4\.  \*\*Execute o Notebook no Jupyter:\*\*

&nbsp;   Este projeto foi desenvolvido como um Jupyter Notebook. Para executá-lo:

&nbsp;   \*   Garanta que você tenha o Jupyter instalado (geralmente vem com a instalação das dependências, ou instale com `pip install jupyter`).

&nbsp;   \*   Na raiz do projeto (`rota\_inteligente\_ia`), execute o Jupyter Notebook:

&nbsp;       ```bash

&nbsp;       jupyter notebook

&nbsp;       ```

&nbsp;   \*   Seu navegador abrirá uma interface do Jupyter. Navegue até a pasta `src/` e clique em `rota\_inteligente.ipynb` para abri-lo.

&nbsp;   \*   Execute cada célula do notebook em sequência (clicando no botão "Run" ou `Shift + Enter`).



5\.  \*\*Verifique os Resultados:\*\*

&nbsp;   Após a execução de todas as células do notebook, as imagens geradas (`grafo\_visualizado.png`, `grafo\_menor\_caminho.png`, `agrupamento\_kmeans.png`) serão salvas na pasta `outputs/` dentro do seu projeto. Além disso, as informações sobre o grafo, menor caminho e clusters serão impressas nas células de saída do notebook.



\## 7. Referências (Fontes de Pesquisa)



\*   \*\*Estudo de caso da UPS – ORION:\*\* A gigante logística utiliza o sistema ORION (On‑Road Integrated Optimization and Navigation), que combina heurísticas e dados de tráfego em tempo real para reduzir milhões de milhas percorridas e economizar aproximadamente US$ 30 milhões ao ano.

&nbsp;   \*   `cdotimes.com`

&nbsp;   \*   `wired.com`

&nbsp;   \*   `jsaer.com`

\*   \*\*Medium – “Optimizing Logistics: Clustering e MILP”:\*\* Caso de aplicação de K‑Means, DBSCAN e Programação Linear Inteira Mista (MILP) para agrupar entregas e minimizar distância total percorrida.

&nbsp;   \*   `medium.com`

\*   \*\*ResearchGate – AI‑Powered Route Optimization:\*\* Artigo que explora integração de IA, sensores IoT, algoritmos heurísticos (como genéticos e RL) para roteamento dinâmico em tempo real, focado em redução de custos e aumento da eficiência das entregas.

&nbsp;   \*   `nickmccullum.com`

&nbsp;   \*   `levelup.gitconnected.com`

&nbsp;   \*   `youtube.com`

&nbsp;   \*   `diva-portal.org`

&nbsp;   \*   `researchgate.net`

&nbsp;   \*   `jsaer.com`

\*   \*\*Kardinal.ai – Case Study “Fresh Product Delivery”:\*\* Demonstra o uso de otimização contínua de rotas, análise de território e planejamento dinâmico para entregas de alimentos frescos, com resultados concretos em eficiência operacional.

&nbsp;   \*   `kardinal.ai`

&nbsp;   \*   `digitaldefynd.com`

