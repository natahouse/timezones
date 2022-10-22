# 🕒 💻 Configurando Timezone em Ambiente Linux

Há algumas formas de definir a timezone em um ambiente Linux. A seguir é descrito como verificar a TZ definida no sistema, bem como alterar para alguma TZ desejada.

## Conteúdos
- [Checar Timezone Definida no Sistema](#checar-timezone-definida-no-sistema)
- [Definir TZ Usando `timedatectl`](#definir-tz-usando-timedatectl)
- [Definir TZ Manualmente através de `/etc/localtime`](#definir-tz-manualmente-atrav%C3%A9s-de-etclocaltime)
- [Instalando Timezones através de `tzdata`](#instalando-timezones-atrav%C3%A9s-de-tzdata)
- [Definindo Timezone através da Variável de Ambiente TZ](#definindo-timezone-atrav%C3%A9s-da-vari%C3%A1vel-de-ambiente-tz)

## Checar Timezone Definida no Sistema

Para verificar a TZ usada no sistema, é possível usar o comando `date`. Esse comando informa a data, hora e TZ configurada.

**Informações de data com `date`:**
```bash
date
# Sat Oct 22 09:47:44 UTC 2022
```

No exemplo acima, a TZ definida no sistema é UTC (Coordinated Universal Time).

Também há casos em que é mostrado apenas o offset para a hora em UTC, como nesse exemplo, em que a timezone definida é UTC−3:

```bash
date
# Sun Oct 23 11:58:27 PM -03 2022
```

## Definir TZ Usando `timedatectl`

A forma mais simples de configurar TZ em um sistema Linux talvez seja usando `timedatectl`, que está disponível em muitas distribuições. Com ele é possível listar as timezones disponíveis e definir uma para o sistema. Além de outras operações relacionadas a horário, como definir a hora do sistema, e ativar ou desativar a sincronização de hora por NTP (Network Time Protocol).

**Listar timezones com `timedatectl`:**
```bash
timedatectl list-timezones
```

Com a lista de timezones disponíveis no sistema, é possível definir a TZ com o comando `set-timezone`, como por exemplo definir o sistema para o fuso de São Paulo:

**Definir uma timezone:**
```bash
timedatectl set-timezone America/Sao_Paulo
```

## Definir TZ Manualmente através de `/etc/localtime`

Caso não seja possível usar `timedatectl`, há uma forma mais tradicional para configurar a TZ do sistema, que é difinir um link simbólico no diretório `/etc/localtime` para um arquivo de timezone em `/usr/share/zoneinfo`.

Primeiro, é preciso localizar as timezones disponíveis no sistema, listando o conteúdo do diretório `/usr/share/zoneinfo`

**Listando timezones disponíveis no sistema:**
```bash
ls /usr/share/zoneinfo
```

Caso não exista timezones salvas, é possivel [Instalar através de tzdata](#instalando-timezones-atrav%C3%A9s-de-tzdata)

As timezones geralmente estão organizadas nesse diretório em regiões como continentes ou países

**Exemplo da TZ de São Paulo no Debian:**
```bash
ls /usr/share/zoneinfo/America/Sao_Paulo
```

Para definir a TZ no sistema dever ser criado um symbolic link no diretório `/etc/localtime`, apontando para algum arquivo de timezone em `/usr/share/zoneinfo`

Primeiramente é necessário remover o arquivo previamente salvo (caso exista)

**Removendo a TZ previamente salva:**
```bash
rm -rf /etc/localtime
```

Então pode ser criado um link simbólico para algum arquivo de TZ disponível no sistema

**Criando um symbolic link para TZ de São Paulo:**
```bash
ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
```

## Instalando Timezones através de `tzdata`

Em alguns ambientes específicos, como containers minificados, há a possibilidade de não haver arquivos de timezone pre instalados no sistema. Para resolver isso, é possível instalar o pacote `tzdata`. Esse pacote contém arquivos de regras para vários fusos do mundo, baseado na [Time Zone Database](https://www.iana.org/time-zones).

**Instalando `tzdata` no Alpine Linux:**
```bash
apk add tzdata
```

**Instalando `tzdata` no Ubuntu Server**
```bash
apt install tzdata
```

Com esse pacote instalado, é criado arquivos de TZ no diretório `/usr/share/zoneinfo/` e então é possível [definir uma timezone manualmente](#definir-tz-manualmente-atrav%C3%A9s-de-etclocaltime)

## Definindo Timezone através da Variável de Ambiente TZ

Se um sistema possui timezones disponíveis, é possível configurar a timezone do sistema através da variável de ambiente `TZ`, definindo para essa variável a timezone desejada.

No exemplo abaixo é definida a TZ de New York para um container Docker Debian.

**Subindo um container Debian com a TZ definida através de variável de ambiente**
```bash
docker container run -it -e TZ="America/New_York" debian
```

Dentro do container, com o comando `date`, temos a informação que foi definido o fuso EDT (Eastern Time Zone).

```bash
date
# Mon Oct 24 10:13:14 EDT 2022
```
