# 🕒 💻 Configurando Timezone em Ambiente Linux

## Definir TZ Usando `timedatectl`
Há algumas formas de definir a timezone em um ambiente Linux. A mais simples talvez seja usando `timedatectl`, que está disponível em muitas distribuições. Com ele é possível listar as timezones disponíveis e definir uma para o sistema. Além de outras operações relacionadas a horário, como definir a hora do sistema, e ativar ou desativar a sincrnização de hora por NTP (Network Time Protocol).

**Listar timezones:**
```bash
timedatectl list-timezones
```

Com a lista de timezones disponíveis no sistema, é possível definir a TZ com o comando `set-timezone`, como por exemplo definir o sistema para o fuso de São Paulo:

**Definir uma timezones:**
```bash
timedatectl set-timezone America/Sao_Paulo
```