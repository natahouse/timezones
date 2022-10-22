# 🕒 💻 Configurando Timezone em Ambiente Linux

Há algumas formas de definir a timezone em um ambiente Linux. A seguir é descrito como verificar a TZ definida no sistema, bem como alterar para alguma TZ desejada.

## Checar Timezone Definida no Sistema

Para verificar a TZ usada no sistema, é possível usar o comando `date`. Esse comando informa a data, hora e TZ configurada

**Informações de data com `date`:**
```bash
date
# Sat Oct 22 09:47:44 UTC 2022
```

No exemplo acima, a TZ definida no sistema é UTC (Coordinated Universal Time)

Também há casos em que é mostrado apenas o offset para a hora em UTC, como nesse exemplo:

```bash
date
# Sun Oct 23 11:58:27 PM -03 2022
```

Nesse exemplo, a TZ definida é UTC−3

## Definir TZ Usando `timedatectl`
Há algumas formas de definir a timezone em um ambiente Linux. A mais simples talvez seja usando `timedatectl`, que está disponível em muitas distribuições. Com ele é possível listar as timezones disponíveis e definir uma para o sistema. Além de outras operações relacionadas a horário, como definir a hora do sistema, e ativar ou desativar a sincrnização de hora por NTP (Network Time Protocol).

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