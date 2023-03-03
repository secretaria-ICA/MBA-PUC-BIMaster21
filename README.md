<!-- antes de enviar a versão final, solicitamos que todos os comentários, colocados para orientação ao aluno, sejam removidos do arquivo -->
# Classificação de Imagens com Transfer Learning

#### Aluno: [Mauricio Pereira Rangel](https://github.com/link_do_github)
#### Orientador: [Felipe Borges](https://github.com/FelipeBorgesC).
#### Co-orientador(/a/es/as): [Manoela Kohler](https://github.com/link_do_github) 



Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

<!-- para os links a seguir, caso os arquivos estejam no mesmo repositório que este README, não há necessidade de incluir o link completo: basta incluir o nome do arquivo, com extensão, que o GitHub completa o link corretamente -->
- [Link para o código](https://github.com/mpr3735/MBA-PUC-BIMaster21/tree/main/Infer%C3%AAncia-Testes). <!-- caso não aplicável, remover esta linha -->

- Trabalhos relacionados: <!-- caso não aplicável, remover estas linhas -->
    - [Base dados Kaggle](https://www.kaggle.com/code/aryanml007/plant-disease-resnet50/notebook).
   
---

### Resumo

<!-- trocar o texto abaixo pelo resumo do trabalho, em português -->

O presente estudo tem como escopo a análise comparativa da aplicação do conceito da técnica de transfer learning, em classificação de imagens, de quatro modelos de redes CNN. O objetivo é utilizar uma estrutura padrão de camadas em cada uma das redes CNN, em análise, e alterar um conjunto de parâmetros específicos, para avaliar o impacto dos mesmos no resultado de cada execução de cada modelo de rede CNN. Com isso identificar se há relevância ou não, em cada uma dessas variações nos resultados coletados das execuções dos modelos, considerando um corte ideal para os valores das métricas de treino e validação. Não faz parte do escopo atingir o máximo de performance no resultado de cada modelo.

### Abstract <!-- Opcional! Caso não aplicável, remover esta seção -->

The current study has the aim  at analysing the comparative implementation of the concept of the learning transfer technique, in   image classification in the four different CNN models. The objective is to use a pattern of structure in each layer of the cnn networks, being analysed, and change a group of  specific parameters in order to assess the impact on the result of each execution of the CNN network model. Furthermore, identify if there is relevance or not, in each of these variations in the collected results and consider an ideal cutoff for the values of the measure of training and validation. This study  does not focus on achieving the maximum performance  in the result of each model.

### 1. Introdução

A base de dados para a realização do estudo analítico comparativo foi obtida do kaggle e contém 38 classes de tipos de plantas saudáveis ou com algum tipo de doença (fungo). Foi realizada uma análise da quantidade de ocorrências de imagens, em cada classe, e para adaptação a limites do ambiente de execução (processamento e consumo de GPU) foi necessário um corte reduzindo o escopo para 04 classes da categoria Uva, o que não afeta o objetivo do estudo. O processo para utillizar a técnica de transfer learming adotou a base de imagens da Imagenet e principalmente estrutras e consultas em exemplos do Keras (keras.org), nesse contexto.  Após a análise e preparo da base de dados de imagens foram elaborados quatro notebooks python, um para cada rede CNN com transfer learning e realizadas oito execuções de cenários dos modelos, conservando uma estrutura comum de camadas e neurônios e variando determinados parâmetros comuns, para coleta e comparação dos valores das métricas de treino , vaidação e testes. As combinações dos parâmetros, em cada cenário, permite avaliar o impacto destas em cada rede CNN analisada.

### 2. Modelagem

O modelo proposto para a análise comparativa das redes CNN, com transfer learning, foi estruturado da seguinte forma:
Utilizar uma Base de dados de entrada com 03 classes de imagens de doenças em folhas de Uvas (Grape___healthy, Grape___Esca_(Black_Measles) e Grape___Black_rot). Uma classe foi descartada, de um total de quatro, após análise da quantidade de imagens, na etapa de análise das frequências de imagens em cada classe. Construção de quatro códigos em python, padronizados, com utilização de tranfer learning, uso da Imagenet, e com base nos modelos CNN Resnet50, Xception, VGG19 e VGG16. Para que a análise comparativa ficasse preservada foi utilizada a mesma estrutura da camada dense e quantidade de neurônios, para cada modelo de rede CNN. Com base nesse padrão, condições e restriçõoes foram executados oito cenários, para cada modelo de rede CNN, com variação em combinações dos parâmetros Learning Rate, Early Stop, Dropout e BatchNormalization. O modelo não considerou a utilização da técncia de data augmentation, por estar fora desse escopo.

A codificaçãa de notebooks python, para cada modelo CNN, contém as seguintes etapas: Definição dos dados de treino, validação e testes; Contagens de cada classe e quantidade de imagens nas mesmas; Preparo de cada conjunto de dados de treino, validação e teste, com análise do formato das imagens e normalização dos dados de entrada; Análise da estrutura da rede CNN em questão; Análise da estrutura da rede CNN truncada; Análise das camadas do modelo final com transfer learning e camadas dense; Compilação do modelo; Treino e análise das métricas; Testes e Inferência;

O padrão de codificação facilitou a execução recursiva dos modelos e coleta das informação nos sete cenários. 
Informações da base de dados:<br/>

a) Base de dados de entrada: Imagens de folhas de classes de vegetais saudáveis ou com algum tipo de doença. Utilizado um suconjunto de 3 classes de de imagens de folhas de Uva. Fonte original da base de dados: (https://www.kaggle.com/datasets/vipoooool/new-plant-diseases-dataset). <br/>
b) Total de imagens de treino: 4659 e total de imagens de validação: 1169. Para os testes de inferência foram utilizadas 10 imagens de cada classe.<br/>
c) Base de dados para utilização de transfer learning: Imagenet.<br/>

Estrutura das Imagens (shapes):<br/>

Rede CNN | Shape Imagem | Batch Size Utilizado
-------- | ------------ | :-------------------
Resnet50 | 224,224,3    | 32
Xception | 299,299,3    | 32
VGG19    | 224,224,3    | 32
VGG16    | 224,224,3    | 32

A estrutra padrão do modelo final a ser usado nas redes CNN, com transfer learning, foi a seguinte:

Camada | Neurônios | Ativação | Otimizador | Loss                    | Pooling                 
------ | ----------|----------| ---------- | ----------------------  | :-----------------------
Poolig | xxxxxxxxx | xxxxxxxx | xxxxxxxxxx | xxxxxxxxxxxxxxxxxxxxxxx | Global_average_pooling2D
Dense1 | 128       |relu      |Adam        |categorical_crossentropy | xxxxxxxxxxxxxxxxxxxxxxxx
Dense2 | 64        |relu      |Adam        |categorical_crossentropy | xxxxxxxxxxxxxxxxxxxxxxxx
Dense3 | 3         |sofmax    |Adam        |categorical_crossentropy | xxxxxxxxxxxxxxxxxxxxxxxx

Obs: Após análise das frequências de classes uma delas foi descartada por não conter imagens.

Os parâmetros submetidos ao estudo, em cada cenário de execução de treino, para os modelos CNN com transfer learning foram:

Parâmetro         | Execução 01| Execução 02 | Execução 03 | Execução 04 | Execução 04-i2 | Execução 05 | Execução 06 | Execução 07
----------------- | ----------- | ----------- | ----------- | ----------- | -------------- | ----------- | ----------- | :-----------
LearningRate      | 0.5         | 0.5         | 0.1         | 0.01        | 0.01           | 0.03        |0.01         | 0.01          
EarlyStop         | 50          | 50          | 50          | 50          | 25             | 25          |25           | 25          
BatchNormalization| Não aplicado| Não aplicado| Não aplicado| Não aplicado| Não aplicado   | Aplicado    |Aplicado     | Aplicado             
Dropout           | Não aplicado| 0.2 *       | Não aplicado| 0.2 *       | 0.2 **         | 0.2 *       |0.2 *        | 0.2 **           

Dropout inserido antes da camanda pooling (asterístico).<br/>
Dropout inserido após a camanda pooling (asterístico duplo).<br/>
Obs: Detalhes sobre a coleta dos resultados, dessas execuções, devem ser consultados nas pastas e arquivos sobre cada execução.

Métricas analisadas no treino e validação do modelo final, em cada cenário executado:
Treino   | Validação
-------- | :--------
loss     | val_loss
accuracy | val_accuracy
precision| val_precision
recall   | val_recall
auc      | val_auc

Obs: Para ponto de corte na coleta dos valores das métricas no estudo comparativo foi considerada uma acurácia acima de 90%, durante o treino.

### 3. Resultados

A coleta de resultados foi realizada após a execução dos códigos python, de cada cenário de Treino e Validação, considerando
as variações envolvendo os valores de Learning Rate, Early Stop (evitar overfitting), inclusão ou não de Dropout(reduzir efeito de overfiting em CNN profundas), antes ou depois da etapa de polling,e a inclusão ou não de Bacth Normalization (analisar a relação com Learning Rate e melhorar a generalização). Cada cenário pode ser consultado em documento no formato pdf na pasta Coleta de Resultados (https://github.com/mpr3735/MBA-PUC-BIMaster21/tree/main/Coleta%20de%20Resultados).<br/>

Resultado da Execução do Treino e Validação: <br/>

Os valores coletados referem-se a úlima época de cada execução, para efeito comparativo entre os modelos.<br/>
Os cenários 01 e 02 não apresentaram valores satisfatórios para as métricas analisadas e uma taxa da métrica "Loss" ainda relativamente alta, e foi
estabelecida a diferença entre os dois, somente com a inclusão do recurso de Dropout, sem outras alterações, mantendo o valor de Learning Rate em 0.5.<br/>

O cenário 03 foi retirado o recurso de Dropout e relizada somente uma variação do valor de Learning Rate de 0.5 para 0.1. Nesse contexto a Rede
CNN Xception apresentou um bom valor para as métricas, com acurácia acima de 95%, porém as outras redes (Resnet50, VGG19 e VGG16) mantiveram os
valores próximos ao cenário 01 e 02, assim sendo classificados como não satisfatórios. <br/>

O cenário 04 o experimento foi reduzir de forma considerável o valor de Learning Rate para 0.01 e retornar com o recurso de Dropout (0.2), antes da etapa de polling.A métricas dos modelos CNN Xception, VGG19 e VGG16 apresentaram valores satisfatórios para as métricas, porém a rede Resnet50, nesse contexto, apresentou grande evolução, mas não acima de 90%.<br/>

** Uma variação do cenário 04 (04-i2) alterou a etapa de Dropout (0.2) para após a etapa de polling, mantendo o valor de Learning Rate e Early Stop. Em termos de treino e validação não foi observada uma variação considerável nas métricas dos quato modelos CNN.<br/>

O cenário 05 retomou as condições do cenário 04, com um pequena variação para maior no valor de Learning Rate, de 0,01 para 0,03 e o valor de 
Early Stop de 50 para 25. Nesse contexto as Redes CNN Xception, VGG19, Resnet50 e VGG16 tiveram uma redução nos valores das métricas para treino e validação, de forma não satisfatória para superar a meta de 90%. Assim esse cenário não foi considerado satisfatório e a variação do valor de Learning Rate confirmou a sensibilidade para os resultados dos modelos. Uma outra possível variação desse cenário poderia ser incluir uma etapa de Batch Normalization, uma vez que houve um aumento do valor de Learning Rate e observar o resultado dessa modificação.<br/>

O cenário 06, é muito próximo ao cenário 04, com a inserção do recurso de Batch Normalization, com um valor reduzido para Learning Rate (0,01), e manteve a boa perfomance das métricas das redes CNN Xception, VGG19 e VGG16 acima de 95%, no treino e validação, e ainda apontou uma melhoria de perfomance das métricas para a rede CNN Resnet50. O números de épocas executadas reduziu para os quatro modelos de rede CNN, com Batch Normalization. Não foi observada uma relação direta entre o dois cenários em relação ao tempo de execução de cada rede CNN, mas para a Resnet50 houve uma redução. Sendo assim um candidato para realização das inferências de testes.<br/>

O cenário 07 apresenta como diferença, em relação ao cenário 06, somente a camada de Dropout posicionada antes da etapa de polling, e os valores das métricas das quatro redes CNN, de treino e validação não apresentaram grande variação. Sendo assim um cenário também favorável para realização de inferências de testes.<br/>

Para efeito comparativo na etapa de inferência, ou seja, teste do modelo com as imagens de testes foram selecionados os modelos dos seguintes cenários:<br/>

Caso de Teste 01: Avaliar o resultado dos testes da Rede Xception do cenário 04 (cenário base).
                  Certificar de que não há overfitting.<br/>

Caso de Teste 02: Comparar o resultados dos testes da Rede Resnet50 do cenário 05 com cenário 06.
                  Avaliar o efeito da variação do Learning Rate no contexto dos cenários.<br/>

Caso de Teste 03: Comparar o resultado do cenário 04 (variação i2) dos testes da Rede Resnet50 com o cenário 06.
                  Avaliar o efeito da utilização de Batch Normalization. <br/>

Caso de Teste 04: Comparar o resultado do cenário 06 dos testes da Rede VGG19 com o cenário 07.
                  Identificar possibilidade de overfitting e avaliar o efeito da posição do Dropout no modelo.<br/>
                  
 Resultado da Inferência e Testes:<br/>
 Foram utilizadas 10 imagens de cada tipo de estado da folha, que não estavam na base de dados de treino e validação.<br/>
 Tabela Score: <br/>
 Caso de Testes | Prever        |Folhas Healphy | Folhas com Black-Hot | Folhas com Black-Measles | CNN
 -------------- | --------------| --------------| -------------------- | ------------------------ |:------------
 01 (cenário 04)| Black-Measles | 0.00000       | 0.00000              | 1.00000                  | Xception
 01             | Healphy       | 1.00000       | 0.00000              | 0.00000                  | 
 01             | Black-Hot     | 0.00000       | 0.99998              | 0.00002                  | 
 02 (cenário 05)| Healphy       | 0.33496       | 0.45708              | 0.20797                  | Resnet50
 02             | Black-Hot     | 0.33496       | 0.45708              | 0.20797                  | 
 02             | Black-Measles | 0.33496       | 0.45708              | 0.20797                  | 
 02 (cenário 06)| Healphy       | 1.00000       | 0.00000              | 0.00000                  | Resnet50
 02             | Black-Hot     | 0.00000       | 0.01496              | 0.98504                  | 
 02             | Black-Measles | 0.00000       | 0.07631              | 0.92369                  | 
 03 (cen. 04-i2)| Healphy       | 0.99975       | 0.00022              | 0.00003                  | Resnet50
 03             | Black-Hot     | 0.00003       | 0.35394              | 0.64603                  | 
 03             | Black-Measles | 0.00001       | 0.20186              | 0.79813                  | 
 04 (cenário 06)| Healphy       | 1.00000       | 0.00000              | 0.00000                  | VGG19
 04             | Black-Hot     | 0.00000       | 0.00006              | 0.99994                  | 
 04             | Black-Measles | 0.00000       | 0.00000              | 1.00000                  | 
 04 (cenário 07)| Healphy       | 1.00000       | 0.00000              | 0.00000                  | VGG19
 04             | Black-Hot     | 0.02010       | 0.58840              | 0.39149                  | 
 04             | Black-Measles | 0.00000       | 0.00001              | 0.99999                  | 
 
 

### 4. Conclusões

Após as execuções de todos os cenários para cada modelo de rede CNN com a utilização de transfer learning, no contexto dessa base de dados de imagens, foi observado que a variação dos valores dos parâmetros, no escopo desse estudo, provacam resultados diferentes (exemplo na coleta de resultados do cenário 03) em cada modelo de rede CNN, assim como a combinação desses parâmetros em cada um dos cenários. A sensibilidade do Learning Rate deve ser sempre observada, uma vez que foi a que mais provocou variações consideráveis nas métricas dos modelos na etapa de treino e validação, quando aplicado em valores reduzidos, sendo assim, observou-se que o objetivo do estudo, em seu escopo,  foi atingido. 

Em relação aos resultados dos dos casos de testes selecionados , após a execução de cada teste verificou-se que o cenário 04 no caso de teste 01 não presentou overfitting , pois o modelo conseguiu classificar bem as imagens de testes. No caso de teste 02 o cenário 06 para a CNN Resnet conseguiu uma melhor classificação, porém com dificuldades para classificar as classes Black-Hot e Black-Measles, e nesse caso uma opção poderia ser aplicar data augmentation na classe Black-Hot e observar o resultado. O mesmo caso ocorre com o cenário 04-i2, pois a classe Healphy obteve bom resultado, mas a classe Black-Hot parace ser classificada como Black-Measle.<br/>

O caso de teste 03 no cenário 04-i2 distribuiu melhor a classificação entrea as classes Black-Hot e Black-Measle, mas ainda persistindo o problema do caso de teste 02, e como opçao a aplicação de data augmentation nessas duas classes pode ser uma opção para melhorar a taxa de acerto nos testes.<br/>

O caso de uso 04 o modelo conseguiu classificar o que é doença ou não, como nos cenários anteriores, mas ainda persistiu a dificuldade para classificar o tipo de doença, não sendo observada alguma alteração em função da camada Dropout. 

---

Matrícula: 123.456.789

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
