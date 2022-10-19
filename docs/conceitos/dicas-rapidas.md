# ✅ Boas Práticas

**Observação:** O formato utilizado nesta seção foi fortemente insipirado neste [repositório](https://github.com/testjavascript/nodejs-integration-tests-best-practices), que faz um EXCELENTE trabalho explicando boas práticas de Testes de Integracão em Node. Recomendo fortemente para todos que trabalham com essa tecnologia.

<br/>

### ⚪️ &nbsp; 1. Data e Hora são uma coisa só

🏷 &nbsp; **Tags:** `#boaspraticas`

✅ &nbsp; **O que fazer:** Sua aplicação nunca deverá lidar com data separada de hora ou hora separada de data. Mesmo que para um caso de uso específico você precise apenas de uma das duas informações, sua vida ficará muito mais simples se você lidar apenas com variáveis de datahora (datetimes). Isso significa que qualquer definição formal dentro do seu sistema como colunas de banco de dados, propriedades de classes, parâmetros de funções e etc devem ser do tipo datahora e conter ambas as partes desta informação.

<br/>

👀 &nbsp; **Alternativas:** Definir variáveis que armazenam apenas a data de forma a simplificar algumas das suas operações, mas a custo de perda de flexibilidade e manutenabilidade já que qualquer pequena mudança de requisitos (ex: instituir internacionalização no sistema) pode fazer com que seja necessário grande volume de reescrita de código ❌;  

<br/>

### ⚪️ &nbsp; 2. Armazenar em UTC

🏷 &nbsp; **Tags:** `#boaspraticas`

✅ &nbsp; **O que fazer:** As datahoras do seu sistema devem ser armazenadas no seu back-end em formato UTC. É importante que todas as datahoras usem a mesma timezone para manter a consistência e facilitar os cálculos, e dado que podem haver modificações de fuso horário devido a novos tipos de usuários ou novas features, usar UTC prepara o sistema para operar de uma forma mais robusta e adaptável para qualquer contexto. Se feito corretamente, utilizar UTC não deve dificultar o desenvolvimento.

<br/>

👀 &nbsp; **Alternativas:** Usar algum fuso horário em particular para as datas armazenadas. Não recomendado pois torna o sistema muito frágil e abre brecha para problemas de funcionamento advindos de pessoas utilizando seu sistema de áreas inesperadas (com diferentes fusos), ou coisas do tipo. ❌; 

<br/>

### ⚪️ &nbsp; 3. Converter para fuso horário local via código front-end

🏷 &nbsp; **Tags:** `#boaspraticas`

✅ &nbsp; **O que fazer:** Dado que as datahoras estarão num formato padronizado UTC armazenadas no back-end (dica #2), ao receber esses dados a nossa aplicação cliente (front-end) deve realizar uma conversão dessa data UTC para o fuso horário local do usuário antes de exibir a informação. Ao enviar requisições para o back-end, seu front deverá enviar a data local, seguindo um padrão pré-definido (ver dica #4) que estiver sendo usado, e será responsabilidade do back-end realizar a conversão de volta para o formato UTC antes de realizar quaisquer tipos de operação com os dados recebidos.

<br/>

👀 &nbsp; **Alternativas:** Converter para os horários locais antes de retornar ao front-end. Pode ser muito mais difícil devido a dificuldade do servidor de saber com certeza em qual zona temporal cada cliente se encontra.
 ❌; 

<br/>

### ⚪️ &nbsp; 4. Definir algum formato de exibicão padrão.

🏷 &nbsp; **Tags:** `#boaspraticas`

✅ &nbsp; **O que fazer:** Além de utilizar o formato UTC exclusivamente no back-end, precisamos definir algum formato padrão (ex: ISO 8601) a ser seguido para a exibição de datas no front-end. Essa decisão deve ser feita com a maior antecedência possível, e documentada de forma clara e fácil de ser consultada pelas pessoas desenvolvedoras do projeto.

<br/>

👀 &nbsp; **Alternativas:** Permitir que os próprios desenvolvedores tentem acertar qual é o formato correto ❌; 

<br/>
