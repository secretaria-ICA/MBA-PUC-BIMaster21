<!-- antes de enviar a versão final, solicitamos que todos os comentários, colocados para orientação ao aluno, sejam removidos do arquivo -->
# Classificação de Imagens com Transfer Learning

#### Aluno: [Mauricio Pereira Rangel](https://github.com/link_do_github)
#### Orientador: [Felipe Borges](https://github.com/FelipeBorgesC) e [Nome Sobrenome](https://github.com/link_do_github).
#### Co-orientador(/a/es/as): [Nome Sobrenome](https://github.com/link_do_github) e [Nome Sobrenome](https://github.com/link_do_github). <!-- caso não aplicável, remover esta linha -->

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

<!-- para os links a seguir, caso os arquivos estejam no mesmo repositório que este README, não há necessidade de incluir o link completo: basta incluir o nome do arquivo, com extensão, que o GitHub completa o link corretamente -->
- [Link para o código](https://github.com/link_do_repositorio). <!-- caso não aplicável, remover esta linha -->

- [Link para a monografia](https://link_da_monografia.com). <!-- caso não aplicável, remover esta linha -->

- Trabalhos relacionados: <!-- caso não aplicável, remover estas linhas -->
    - [Nome do Trabalho 1](https://link_do_trabalho.com).
    - [Nome do Trabalho 2](https://link_do_trabalho.com).

---

### Resumo

<!-- trocar o texto abaixo pelo resumo do trabalho, em português -->

O presente estudo tem como escopo a análise comparativa da aplicação do conceito da técnica de transfer learning, em classificação de imagens, de quatro modelos de redes CNN. O objetivo é utilizar uma estrutura padrão de camadas em cada uma das redes CNN, em análise, e alterar um conjunto de parâmetros determinados, para avaliar o impacto dos mesmos no resultado de cada execução, de cada modelo de rede CNN. Com isso identificar se há relevância ou não, em cada uma dessas variações nos resultados coletados das execuções dos modelos, considerando um corte ideal para os valores das métricas de predição. Não faz parte do escopo atingir o máximo de performance no resultado de cada modelo.

### Abstract <!-- Opcional! Caso não aplicável, remover esta seção -->

<!-- trocar o texto abaixo pelo resumo do trabalho, em inglês -->

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin pulvinar nisl vestibulum tortor fringilla, eget imperdiet neque condimentum. Proin vitae augue in nulla vehicula porttitor sit amet quis sapien. Nam rutrum mollis ligula, et semper justo maximus accumsan. Integer scelerisque egestas arcu, ac laoreet odio aliquet at. Sed sed bibendum dolor. Vestibulum commodo sodales erat, ut placerat nulla vulputate eu. In hac habitasse platea dictumst. Cras interdum bibendum sapien a vehicula.

Proin feugiat nulla sem. Phasellus consequat tellus a ex aliquet, quis convallis turpis blandit. Quisque auctor condimentum justo vitae pulvinar. Donec in dictum purus. Vivamus vitae aliquam ligula, at suscipit ipsum. Quisque in dolor auctor tortor facilisis maximus. Donec dapibus leo sed tincidunt aliquam.

Donec molestie, ante quis tempus consequat, mauris ante fringilla elit, euismod hendrerit leo erat et felis. Mauris faucibus odio est, non sagittis urna maximus ut. Suspendisse blandit ligula pellentesque tincidunt malesuada. Sed at ornare ligula, et aliquam dui. Cras a lectus id turpis accumsan pellentesque ut eget metus. Pellentesque rhoncus pellentesque est et viverra. Pellentesque non risus velit. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.

### 1. Introdução

A base de dados para a realização do estudo analítico comparativo foi obtida do kaggle e contém 38 classes de tipos de plantas saudáveis ou com algum tipo de doença (fungo). Foi realizada uma análise da quantidade de ocorrências de imagens, em cada classe, e para adaptação a limites do ambiente de execução (processamento e consumo de GPU) foi necessário um corte reduzindo o escopo para 04 classes da categoria Uva, o que não afeta o objetivo do estudo. O processo para utillizar a técnica de transfer learming adotou a base de imagens da Imaginet e principalmente consultas em exemplos do Keras (keras.org), nesse contexto.  Após a análise e preparo da base de dados de imagens foram elaborados quatro notebooks python, um para cada rede CNN com transfer learning e realizadas oito execuções de cenários dos modelos, conservando uma estrutura commum de camadas e neurônios e variando determinados parâmetros comuns, para coleta e comparação dos valores das métricas de treino , vaidação e testes. As combinações dos parâmetros, em cada cenário, permite avaliar o impacto destas em cada rede CNN analisada.

### 2. Modelagem

O modelo proposto para a análise comparativa das redes CNN, com transfer learning, foi estruturado da seguinte forma:
Utilizar uma Base de dados de entrada com 03 classes de imagens de doenças em folhas de Uvas (Grape___healthy, Grape___Esca_(Black_Measles) e Grape___Black_rot). Uma classe foi descartada após análise da quantidade de imagens, na etapa de análise das frequências de imagens em cada classe. Construção de quatro códigos em python, padronizados, com utilização de tranfer learning, uso da Imagenet, e com base nos modelos CNN Resnet50, Xception, VGG19 e VGG16. Para que a análise comparativa ficasse preservada foi utilizada a mesma estrutura da camada dense e quantidade de neurônios, para cada modelo de rede CNN. Com base nesse padrão, condições e restriçõoes foram executados oito cenários, para cada modelo de rede CNN, com variação em combinações dos parâmetros Learning Rate, Early Stop, Dropout e BatchNormalization. O modelo não considerou a utilização da técncia de data augmentation, por estar fora desse escopo.

A codificaçãa de notebooks python, para cada modelo CNN, contém as seguintes etapas: Definição dos dados de treino, validação e testes; Contagens de cada classe e quantidade de imagens nas mesmas; Preparo de cada conjunto de dados de treino, validação e teste, com análise do formato das imagens e normalização dos dados de entrada; Análise da estrutura da rede CNN em questão; Análise da estrutura da rede CNN truncada; Análise das camadas do modelo final com transfer learning e camdas dense; Compilação do modelo; Treino e análise das métricas; Testes e Inferência;

O padrão de codificação facilitou a execução recursiva dos modelos e coleta das informação nos oito cenários. Sendo o oitavo cenário o ponto de corte para a análise comparativa final dos resultados.

Informações da base de dados:<br/>

a) Base de dados de entrada: Imagens de folhas de classes de vegetais saudáveis ou com algum tipo de doença. Utilizado um sbconjunto de 3 classes de de imagens de folhas de Uva. Fonte original da base de dados: https://www.kaggle.com/datasets/vipoooool/new-plant-diseases-dataset. <br/>
b) Total de umagens de treino: 4659 e total de imagens de validação: 1169. Para os testes de inferência foram utilizadas 10 imagens de cada classe.<br/>
c) Base de dados para utilização de transfer learning: Imagenet.

A estrutra padrão do modelo final a ser usado nas redes CNN, com transfer learning, foi a seguinte:

Camada | Neurônios | Ativação | Otimizador | Loss                  
------ | ----------|----------| ---------- | :----------------------
Dense1 | 128       |relu      |SGD         |categorical_crossentropy
Dense2 | 64        |relu      |SGD         |categorical_crossentropy
Dense3 | 3         |relu      |SGD         |categorical_crossentropy

Obs: As execuções dos cenários de 01 até 04, dos molelos, ainda considerou 4 classes na camada Dense3. Após a execução 04 uma classe foi descartada.

Os parâmetros submetidos ao estudo, em cada cenário de execução de treino, para os modelos CNN com transfer learning foram:

Parâmetro         | Execução 01 | Execução 02 | Execução 03 | Execução 04 | Execução 05 | Execução 05-i2 | Execução 06 | Execução 07 | Execução 08
----------------- | ----------- | ----------- | ----------- | ----------- | ----------- | -------------- | ----------- | ----------- | :-----------
LearningRate      | 0.5         | 0.5         | 0.1         | 0.5         | 0.01        | 0.01           | 0.03        |0.01         | 0.01          
EarlyStop         | 50          | 50          | 50          | 50          | 50          | 25             | 25          |25           | 25          
BatchNormalization| Não aplicado| Não aplicado| Não aplicado| Não aplicado| Não aplicado| Não aplicado   | Aplicado    |Aplicado     | Aplicado             
Dropout           | Não aplicado| 0.2 *       | Não aplicado| 0.5 *       | 0.2 *       | 0.2 **         | 0.2 *       |0.2 *        | 0.2 **           

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

A coleta dos resultados foi realizada para cada execução de cada cenário, como informado no tópico de modelagem. Os melhores resultados para as métricas selecionadas para cada rede CNN, nesse contexto, começarama ser observados a partir do cenário de execução 05, em diante. Foi percepetível que o parâmetro Learning Rate provocava uma melhora considerável ou piora considerável nas métricas e que nem todos os quatro modelos de rede CNN respondiam de forma idêntica ao conjunto de valores aplicados nos parâmetros analisados (Learning Rate, Early Stop, Dropout e BatchNormalized).

Os cenários x, y apresentaram ....
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin pulvinar nisl vestibulum tortor fringilla, eget imperdiet neque condimentum. Proin vitae augue in nulla vehicula porttitor sit amet quis sapien. Nam rutrum mollis ligula, et semper justo maximus accumsan. Integer scelerisque egestas arcu, ac laoreet odio aliquet at. Sed sed bibendum dolor. Vestibulum commodo sodales erat, ut placerat nulla vulputate eu. In hac habitasse platea dictumst. Cras interdum bibendum sapien a vehicula.

Proin feugiat nulla sem. Phasellus consequat tellus a ex aliquet, quis convallis turpis blandit. Quisque auctor condimentum justo vitae pulvinar. Donec in dictum purus. Vivamus vitae aliquam ligula, at suscipit ipsum. Quisque in dolor auctor tortor facilisis maximus. Donec dapibus leo sed tincidunt aliquam.

### 4. Conclusões

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin pulvinar nisl vestibulum tortor fringilla, eget imperdiet neque condimentum. Proin vitae augue in nulla vehicula porttitor sit amet quis sapien. Nam rutrum mollis ligula, et semper justo maximus accumsan. Integer scelerisque egestas arcu, ac laoreet odio aliquet at. Sed sed bibendum dolor. Vestibulum commodo sodales erat, ut placerat nulla vulputate eu. In hac habitasse platea dictumst. Cras interdum bibendum sapien a vehicula.

Proin feugiat nulla sem. Phasellus consequat tellus a ex aliquet, quis convallis turpis blandit. Quisque auctor condimentum justo vitae pulvinar. Donec in dictum purus. Vivamus vitae aliquam ligula, at suscipit ipsum. Quisque in dolor auctor tortor facilisis maximus. Donec dapibus leo sed tincidunt aliquam.

---

Matrícula: 123.456.789

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
