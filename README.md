# datasciencecoursera
curso em R para machine learning
Como compartilhar dados com um estatístico
Este é um guia para quem precisa compartilhar dados com um estatístico ou cientista de dados. Os públicos-alvo que tenho em mente são:

Colaboradores que precisam de estatísticos ou cientistas de dados para analisar dados para eles
Estudantes ou pós-doutorandos em várias disciplinas à procura de consultoria
Estudantes de estatística júnior cujo trabalho é agrupar/limpar/organizar conjuntos de dados
Os objetivos deste guia são fornecer algumas instruções sobre a melhor maneira de compartilhar dados para evitar as armadilhas e fontes de atraso mais comuns na transição da coleta de dados para a análise de dados. O grupo Leek trabalha com um grande número de colaboradores e a principal fonte de variação na velocidade dos resultados é o status dos dados quando chegam ao grupo Leek. Com base em minhas conversas com outros estatísticos, isso é verdade quase universalmente.

Meu forte sentimento é que os estatísticos devem ser capazes de lidar com os dados em qualquer estado em que cheguem. É importante ver os dados brutos, entender as etapas no pipeline de processamento e ser capaz de incorporar fontes ocultas de variabilidade na análise de dados. Por outro lado, para muitos tipos de dados, as etapas de processamento são bem documentadas e padronizadas. Assim, o trabalho de converter os dados da forma bruta para a forma diretamente analisável pode ser realizado antes de chamar um estatístico. Isso pode acelerar drasticamente o tempo de resposta, já que o estatístico não precisa passar por todas as etapas de pré-processamento primeiro.

O que você deve entregar ao estatístico
Para facilitar a análise mais eficiente e oportuna, esta é a informação que você deve passar para um estatístico:

Os dados brutos.
Um conjunto de dados organizado
Um livro de códigos descrevendo cada variável e seus valores no conjunto de dados organizado.
Uma receita explícita e exata que você costumava ir de 1 -> 2,3
Vejamos cada parte do pacote de dados que você transferirá.

Os dados brutos
É fundamental que você inclua a forma mais bruta dos dados aos quais você tem acesso. Isso garante que a proveniência dos dados possa ser mantida em todo o fluxo de trabalho. Aqui estão alguns exemplos da forma bruta de dados:

O estranho arquivo binário que sua máquina de medição cospe
O arquivo Excel não formatado com 10 planilhas que a empresa que você contratou lhe enviou
Os dados JSON complicados que você obteve ao raspar a API do Twitter
Os números digitados à mão que você coletou olhando através de um microscópio
Você sabe que os dados brutos estão no formato correto se:

Não executou nenhum software nos dados
Não modificou nenhum dos valores de dados
Você não removeu nenhum dado do conjunto de dados
Você não resumiu os dados de forma alguma
Se você fez alguma modificação nos dados brutos, não é a forma bruta dos dados. Relatar dados modificados como dados brutos é uma maneira muito comum de retardar o processo de análise, pois o analista geralmente terá que fazer um estudo forense de seus dados para descobrir por que os dados brutos parecem estranhos. (Imagine também o que aconteceria se novos dados chegassem?)

O conjunto de dados organizado
Os princípios gerais de dados organizados são apresentados por Hadley Wickham neste artigo e neste vídeo . Embora tanto o artigo quanto o vídeo descrevam dados organizados usando R , os princípios são aplicáveis ​​de maneira mais geral:

Cada variável que você mede deve estar em uma coluna
Cada observação diferente dessa variável deve estar em uma linha diferente
Deve haver uma tabela para cada "tipo" de variável
Se você tiver várias tabelas, elas devem incluir uma coluna na tabela que permita que elas sejam unidas ou mescladas
Embora essas sejam as regras rígidas e rápidas, há várias outras coisas que tornarão seu conjunto de dados muito mais fácil de manusear. A primeira é incluir uma linha na parte superior de cada tabela/planilha de dados que contém os nomes completos das linhas. Portanto, se você medisse a idade no diagnóstico dos pacientes, encabeçaria essa coluna com o nome AgeAtDiagnosisem vez de algo como ADxou outra abreviação que pode ser difícil para outra pessoa entender.

Aqui está um exemplo de como isso funcionaria a partir da genômica. Suponha que para 20 pessoas você coletou medidas de expressão gênica com sequenciamento de RNA. Você também coletou informações demográficas e clínicas sobre os pacientes, incluindo idade, tratamento e diagnóstico. Você teria uma tabela/planilha que contém as informações clínicas/demográficas. Teria quatro colunas (id do paciente, idade, tratamento, diagnóstico) e 21 linhas (uma linha com nomes de variáveis, depois uma linha para cada paciente). Você também teria uma planilha para os dados genômicos resumidos. Normalmente este tipo de dados é resumido ao nível do número de contagens por exão. Suponha que você tenha 100.000 exons, então você teria uma tabela/planilha com 21 linhas (uma linha para nomes de genes e uma linha para cada paciente) e 100.001 colunas (uma linha para ids de pacientes e uma linha para cada tipo de dados).

Se você estiver compartilhando seus dados com o colaborador no Excel, os dados organizados devem estar em um arquivo Excel por tabela. Eles não devem ter várias planilhas, nenhuma macro deve ser aplicada aos dados e nenhuma coluna/célula deve ser destacada. Como alternativa, compartilhe os dados em um arquivo de texto CSV ou delimitado por TAB . (Cuidado, no entanto, que a leitura de arquivos CSV no Excel às vezes pode levar ao manuseio não reproduzível de variáveis ​​de data e hora.)

O livro de códigos
Para quase qualquer conjunto de dados, as medidas que você calcular precisarão ser descritas com mais detalhes do que você pode ou deve entrar na planilha. O livro de códigos contém essas informações. No mínimo deve conter:

Informações sobre as variáveis ​​(incluindo unidades!) no conjunto de dados não contidas nos dados arrumados
Informações sobre as escolhas de resumo que você fez
Informações sobre o desenho do estudo experimental que você usou
Em nosso exemplo de genômica, o analista gostaria de saber qual é a unidade de medida para cada variável clínica/demográfica (idade em anos, tratamento por nome/dose, nível de diagnóstico e quão heterogêneo). Eles também gostariam de saber como você escolheu os exons usados ​​para resumir os dados genômicos (UCSC/Ensembl, etc.). Eles também gostariam de saber qualquer outra informação sobre como você fez a coleta de dados/desenho do estudo. Por exemplo, esses são os primeiros 20 pacientes que entraram na clínica? São 20 pacientes altamente selecionados por alguma característica como idade? Eles são randomizados para tratamentos?

Um formato comum para este documento é um arquivo do Word. Deve haver uma seção chamada "Design do estudo" que tenha uma descrição completa de como você coletou os dados. Existe uma seção chamada "Livro de códigos" que descreve cada variável e suas unidades.

Como codificar variáveis
Quando você coloca variáveis ​​em uma planilha, existem várias categorias principais que você encontrará dependendo do tipo de dados :

Contínuo
Ordinal
Categórico
Ausência de
Censurado
Variáveis ​​contínuas são qualquer coisa medida em uma escala quantitativa que pode ser qualquer número fracionário. Um exemplo seria algo como peso medido em kg. Dados ordinais são dados que têm um número fixo e pequeno (< 100) de níveis, mas são ordenados. Isso poderia ser, por exemplo, respostas de pesquisa em que as opções são: ruim, razoável, bom. Dados categóricos são dados em que há várias categorias, mas não são ordenados. Um exemplo seria o sexo: masculino ou feminino. Essa codificação é atraente porque é autodocumentada. Dados ausentes são dados que não são observados e você não conhece o mecanismo. Você deve codificar os valores ausentes como NA. Dados censuradossão dados em que você conhece o mecanismo de falta em algum nível. Exemplos comuns são uma medição abaixo do limite de detecção ou perda de seguimento de um paciente. Eles também devem ser codificados como NAquando você não tem os dados. Mas você também deve adicionar uma nova coluna aos seus dados organizados chamada "VariableNameCensored", que deve ter valores de TRUEse censurado e FALSEse não. No livro de códigos, você deve explicar por que esses valores estão ausentes. É absolutamente crítico relatar ao analista se houver uma razão que você sabe sobre a falta de alguns dados. Você também não deve imputar / inventar / jogar fora as observações que faltam.

Em geral, tente evitar codificar variáveis ​​categóricas ou ordinais como números. Quando você insere o valor para sexo nos dados arrumados, deve ser "masculino" ou "feminino". Os valores ordinais no conjunto de dados devem ser "ruim", "regular" e "bom" e não 1, 2 ,3. Isso evitará possíveis confusões sobre a direção dos efeitos e ajudará a identificar erros de codificação.

Sempre codifique cada informação sobre suas observações usando texto. Por exemplo, se você estiver armazenando dados no Excel e usar uma forma de texto colorido ou formatação de fundo de célula para indicar informações sobre uma observação ("entradas de variáveis ​​vermelhas foram observadas no experimento 1"), essas informações não serão exportadas (e serão ser perdido!) quando os dados são exportados como texto bruto. Cada pedaço de dados deve ser codificado como texto real que pode ser exportado.

A lista de instruções/script
Você pode ter ouvido isso antes, mas a reprodutibilidade é um grande negócio na ciência computacional . Isso significa que, quando você envia seu artigo, os revisores e o resto do mundo devem ser capazes de replicar exatamente as análises dos dados brutos até os resultados finais. Se você estiver tentando ser eficiente, provavelmente executará algumas etapas de resumo/análise de dados antes que os dados possam ser considerados organizados.

O ideal para você fazer ao realizar a sumarização é criar um script de computador (em R, Python, ou qualquer outra coisa) que receba os dados brutos como entrada e produza os dados organizados que você está compartilhando como saída. Você pode tentar executar seu script algumas vezes e ver se o código produz a mesma saída.

Em muitos casos, a pessoa que coletou os dados tem incentivo para deixá-los organizados para que um estatístico acelere o processo de colaboração. Eles podem não saber como codificar em uma linguagem de script. Nesse caso, o que você deve fornecer ao estatístico é algo chamado pseudocódigo . Deve ser algo como:

Etapa 1 - pegue o arquivo bruto, execute a versão 3.1.2 do software de resumo com os parâmetros a=1, b=2, c=3
Etapa 2 - execute o software separadamente para cada amostra
Etapa 3 - pegue a coluna três de outputfile.out para cada amostra e essa é a linha correspondente no conjunto de dados de saída
Você também deve incluir informações sobre em qual sistema (Mac/Windows/Linux) você usou o software e se você tentou mais de uma vez para confirmar que deu os mesmos resultados. Idealmente, você executará isso por um colega/colega de laboratório para confirmar que eles podem obter o mesmo arquivo de saída que você obteve.

O que você deve esperar do analista
Quando você entrega um conjunto de dados devidamente organizado, diminui drasticamente a carga de trabalho do estatístico. Então, espero que eles voltem para você muito mais cedo. Mas os estatísticos mais cuidadosos verificarão sua receita, farão perguntas sobre as etapas que você executou e tentarão confirmar se podem obter os mesmos dados organizados que você obteve com, no mínimo, verificações pontuais.

Você deve então esperar do estatístico:

Um script de análise que executa cada uma das análises (não apenas instruções)
O código de computador exato que eles usaram para executar a análise
Todos os arquivos/figuras de saída que eles geraram.
Esta é a informação que você usará no suplemento para estabelecer a reprodutibilidade e precisão de seus resultados. Cada uma das etapas da análise deve ser claramente explicada e você deve fazer perguntas quando não entender o que o analista fez. É responsabilidade do estatístico e do cientista entender a análise estatística. Você pode não ser capaz de realizar as análises exatas sem o código do estatístico, mas deve ser capaz de explicar por que o estatístico executou cada etapa para um colega de laboratório/seu investigador principal.

Contribuintes
Jeff Leek - Escreveu a versão inicial.
L. Collado-Torres - Erros de digitação corrigidos, links adicionados.
Nick Reich - Adicionadas dicas sobre como armazenar dados como texto.
Nick Horton - Pequenas sugestões de redação.
