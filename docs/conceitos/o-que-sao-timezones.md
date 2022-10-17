# Introdução

Muitas vezes, durante o desenvolvimento de aplicações, os desenvolvedores se deparam com uma função ou serviço que utiliza o conceito de tempo. De forma quase geral, grande parte das linguagens de programação já dispõem de bibliotecas que fazem a maior parte do trabalho para nós, lidando com as datas, suas formatações e muitas coisas que podem acabar trazendo um pouco de dor de cabeça para os devs.

Timezones, por outro lado, são um pouco mais complexas de se lidar (por isso que criamos um repositório inteiro dedicado a esse tema, inclusive). Nesse conteúdo, vamos conhecer alguns conceitos básicos sobre timezones que irão facilitar sua compreensão sobre o tema.

# O que são timezones?

O termo "timezone", traduzido de forma literal significaria "zona de tempo", normalmente se refere ao tempo local de uma região ou país. Muitas pessoas também usam o termo "fuso-horário" para se referir as timezones. O tempo local de uma timezone é definido pela sua diferença do UTC (Tempo Universal Coordinado), que é o padrão internacional.

Normalmente os fuso-horários seguem a fronteira entre os países, e não a longitude, já que é mais útil que locais que se comuniquem com frequência usem a mesma timezone. Lugares que tem a latitude alta costumam usar o conhecido (e falecido) horário de verão por metade do ano, adicionando uma hora no tempo local pra economizar energia.

A primeira pessoa a propor o uso de timezones foi o engenheiro canadense Sir Sanford Fleming em 1878 (um baita tempo atrás!). Como a terra rotaciona 15 graus a cada hora (ou seja, 360 graus em um dia), ele propôs dividir o mundo em 24 timezones com 15 graus de longitude de diferença entre elas. Esse modelo é utilizado até hoje, e vale lembrar que essa é uma explicação um pouco mais simplificada.

As timezones são utilizadas em todos os propositos sociais, comerciais e legais de uma região.

# Qual a importância para os projetos?

Digamos que você está desenvolvendo um aplicativo que deve implementar um calendário, relógio ou qualquer outra coisa que envolva manipulação de dados de tempo. O motivo pelo qual devemos levar as timezones em consideração é: se dois usuários que moram em lugares diferentes do mundo utilizassem o aplicativo, o mesmo deve se adaptar para o fuso-horário de cada um.

Muitas vezes é bem confuso e complicado tentar implementar funções que utilizam timezones do zero, por isso que já existem diversas bibliotecas que já fazem esse trabalho pelo dev. Muitos serviços de banco de dados também já armazenam os dados com suas respectivas timezones para facilitar as conversões nos aplicativos.

É válido dizer que todo desenvolvedor quer que seu aplicativo seja utilizado no mundo inteiro, por diversas pessoas diferentes. Então, pra que isso seja possível, é sempre importante ter as timezones em mente durante o desenvolvimento dos seus projetos.

**Gostou do conteúdo? Tem alguma dúvida ou encontrou algum erro? [Cria uma issue e avisa pra gente!](https://github.com/natahouse/timezones/issues/new/choose)**

# Referências

- https://en.wikipedia.org/wiki/Time_zone
- https://geojango.com/blogs/explore-your-world/history-of-time-zones#:~:text=Sir%20Sanford%20Fleming%2C%20a%20Canadian,360%20degrees%20in%2024%20hours.
- https://www.ticwatches.co.uk/time-zones-explained-i14
