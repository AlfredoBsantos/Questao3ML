# Avaliação da Unidade 2 - Aprendizagem de Máquina

Este repositório contém a solução da **Questão 3** da avaliação da Unidade 2 da disciplina de Aprendizagem de Máquina.

* **Instituição:** Universidade Federal do Rio Grande do Norte (UFRN) - Escola Agrícola de Jundiaí 
* **Curso:** Análise e Desenvolvimento de Sistemas 
* **Docente:** Prof. Josenalde Oliveira 

## Sobre o Projeto

O objetivo deste projeto foi explorar o impacto da técnica de **Aumento de Dados (Data Augmentation)** na performance de um classificador linear simples (`SGDClassifier`) para um problema de classificação multiclasse, utilizando o dataset MNIST.

## Análise da Questão 3: Verificação de Requisitos

A seguir, é detalhado como cada item solicitado na Questão 3 foi cumprido pelo notebook `Untitled.ipynb` presente neste repositório.

#### 1. "escreva uma função que possa mover uma imagem do MNIST em qualquer direção" 
* **Status:** ✅ **Cumprido**
* **Implementação:** Na **Célula 3** do notebook, foi definida a função `mover_imagem(imagem, dx, dy)`. Esta função recebe uma imagem do MNIST (em formato de vetor), um deslocamento horizontal (`dx`) e um vertical (`dy`), e retorna a nova imagem deslocada.

#### 2. "considere usar o método shift() do módulo scipy.ndimage.interpolation" 
* **Status:** ✅ **Cumprido**
* **Implementação:** A função `mover_imagem` utiliza internamente o método `shift()`, conforme a documentação da biblioteca `scipy`, para realizar o deslocamento dos pixels da imagem de forma eficiente. A linha `imagem_deslocada = shift(imagem, [dy, dx], cval=0, mode='constant')` na **Célula 3** implementa esta sugestão.

#### 3. "Pode começar testando X=1 e as adicione ao conjunto de treinamento" 
* **Status:** ✅ **Cumprido**
* **Implementação:** Na **Célula 4**, foi implementado o processo de Aumento de Dados. Um laço `for` itera sobre cada imagem do conjunto de treino original. Para cada imagem, são geradas 4 novas versões, cada uma deslocada em **1 pixel** para cima, para baixo, para a esquerda e para a direita. Tanto as imagens originais quanto as novas imagens deslocadas foram adicionadas a um novo conjunto de treinamento (`X_train_aumentado`), que resultou em um total de 300.000 amostras.

#### 4. "Faça a classificação multiclasse com o SGD" 
* **Status:** ✅ **Cumprido**
* **Implementação:** A **Célula 5** do notebook é dedicada ao treinamento do modelo. Nela, um `SGDClassifier` do `scikit-learn` é instanciado e treinado (`.fit()`) utilizando o conjunto de dados aumentado (`X_train_aumentado` e `y_train_aumentado`).

#### 5. "veja se os resultados melhoraram em termos de confusão com os números" 
* **Status:** ✅ **Cumprido**
* **Implementação:** A **Célula 6** realiza a avaliação final. Após treinar o modelo, ele é usado para prever os resultados no conjunto de teste. Uma **Matriz de Confusão** é gerada e plotada com `seaborn`. A análise visual da matriz demonstra que os valores na diagonal principal (acertos) são muito superiores aos valores fora da diagonal (erros/confusões). Isso indica que a técnica de aumento de dados foi bem-sucedida em tornar o modelo mais robusto, diminuindo a confusão entre dígitos semelhantes, que era o objetivo central da questão. O modelo alcançou uma acurácia final de **88.26%**.

### Como Executar o Projeto

O ambiente de desenvolvimento foi configurado usando `conda`. Para recriar o ambiente e executar o notebook:

1.  Crie e ative um novo ambiente `conda` com todos os pacotes necessários:
    ```bash
    conda create --name ml_env python=3.11 numpy=1.26 scikit-learn pandas matplotlib seaborn notebook -y
    conda activate ml_env
    ```
2.  Navegue até a pasta do projeto e inicie o Jupyter Notebook:
    ```bash
    jupyter notebook
    ```
3.  Abra o arquivo `.ipynb` e execute as células em ordem.

### Tecnologias Utilizadas
* Python 3.11
* Jupyter Notebook
* Conda
* Scikit-learn
* NumPy
* SciPy
* Matplotlib
* Seaborn
