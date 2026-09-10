# Phantom Process Killer — Android 12+

## Objetivo

Esta documentação apresenta o problema do **Phantom Process Killer** em dispositivos Android 12 ou superiores e as possíveis configurações para reduzir a interrupção de processos utilizados pelo ambiente Linux do Cyberdeck.

O problema é especialmente relevante quando o projeto utiliza **Termux**, **Termux:X11** e **XFCE4**.

---

## 1. O problema

A partir do Android 12, o sistema passou a aplicar mecanismos mais agressivos de gerenciamento de processos em segundo plano.

Entre eles está o mecanismo conhecido como **Phantom Process Killer**, que pode encerrar processos filhos executados por aplicativos como o Termux.

No Cyberdeck, isso pode causar a interrupção de componentes necessários para manter o ambiente Linux e sua interface gráfica funcionando.

Os componentes potencialmente afetados incluem:

- Termux;
- ambiente Linux executado pelo Termux;
- Termux:X11;
- XFCE4;
- servidores e outros processos executados em segundo plano.

---

## 2. Sintoma

Durante a configuração do Cyberdeck, o problema pode apresentar o seguinte comportamento:

1. O Termux é iniciado normalmente.
2. O ambiente Linux é iniciado.
3. O servidor gráfico X11 é executado.
4. O XFCE4 é iniciado.
5. A interface gráfica funciona inicialmente.
6. Depois de algum tempo, o Android pode encerrar processos filhos.
7. O servidor X11, XFCE4 ou outro serviço pode deixar de funcionar.

O comportamento pode variar de acordo com:

- versão do Android;
- fabricante do dispositivo;
- ROM utilizada;
- gerenciamento de bateria;
- versão do Termux;
- versão do Termux:X11;
- configurações do próprio dispositivo.

---

# 3. Solução 1 — Opções do desenvolvedor

Antes de utilizar ADB, algumas configurações do Android podem ajudar a reduzir o encerramento de processos em segundo plano.

### Ativar as opções do desenvolvedor

No Android, acesse:

**Configurações → Sobre o telefone**

Localize:

**Número da versão**

Toque aproximadamente 7 vezes em **Número da versão** até que o Android informe que as opções do desenvolvedor foram ativadas.

Depois acesse:

**Configurações → Sistema → Opções do desenvolvedor**

A localização e o nome dessas opções podem variar de acordo com o fabricante e a versão do Android.

### Não manter atividades

Caso essa opção esteja disponível, deixe:

**Desativada**

Essa configuração evita que atividades sejam destruídas imediatamente quando o usuário deixa uma aplicação.

### Limite de processos em segundo plano

Caso essa configuração esteja disponível, evite utilizar um limite muito baixo de processos.

Uma configuração possível para testes é:

**4 processos ou mais**

### Observação

Essas configurações podem reduzir alguns problemas relacionados ao gerenciamento de processos, mas **não garantem que o Android deixe de encerrar processos filhos do Termux**.

Para uma configuração mais específica, pode ser utilizado o ADB.

---

# 4. Solução 2 — ADB

O **Android Debug Bridge (ADB)** permite executar comandos no dispositivo Android a partir de um computador.

Essa é uma alternativa para modificar a configuração relacionada ao limite de processos fantasmas.

## Requisitos

É necessário possuir:

- computador com ADB instalado;
- dispositivo Android compatível;
- Depuração USB ou Depuração sem fio habilitada;
- dispositivo autorizado para comunicação com o computador.

---

## 5. Habilitar a depuração USB

No dispositivo Android:

**Configurações → Sistema → Opções do desenvolvedor**

Procure por:

**Depuração USB**

Ative a opção.

Conecte o dispositivo ao computador.

Caso apareça uma mensagem perguntando se deseja permitir a depuração USB, autorize o computador.

---

# 6. Aplicar a configuração via ADB

No computador, abra o terminal ou Prompt de Comando e execute:

```bash
adb shell "/system/bin/device_config set_sync_disabled_for_tests persistent"
```

Depois execute:

```bash
adb shell "/system/bin/device_config put activity_manager max_phantom_processes 2147483647"
```

A configuração aumenta o limite de processos fantasmas para um valor muito alto, reduzindo a possibilidade de que o Android encerre os processos utilizados pelo ambiente do Cyberdeck.

---

# 7. Verificar se a configuração foi aplicada

Execute:

```bash
adb shell "/system/bin/device_config get activity_manager max_phantom_processes"
```

Se a configuração estiver aplicada, deverá aparecer:

```text
2147483647
```

Caso outro valor seja retornado, a configuração pode não ter sido aplicada conforme esperado.

---

# 8. ADB sem cabo — Depuração sem fio

Em dispositivos Android compatíveis, é possível utilizar o ADB sem conectar um cabo USB.

No Android, acesse:

**Configurações → Sistema → Opções do desenvolvedor**

Procure por:

**Depuração sem fio**

Ative a função.

O Android exibirá informações de pareamento.

No computador, execute:

```bash
adb pair IP:PORTA
```

Substitua `IP:PORTA` pelas informações apresentadas pelo dispositivo.

Depois de realizar o pareamento, conecte-se ao dispositivo:

```bash
adb connect IP:PORTA
```

Após a conexão, os comandos ADB apresentados anteriormente podem ser executados normalmente.

---

# 9. Verificar a conexão ADB

Para verificar se o computador reconheceu o dispositivo, execute:

```bash
adb devices
```

O dispositivo deverá aparecer na lista de dispositivos conectados.

Exemplo:

```text
List of devices attached
XXXXXXXX    device
```

Se aparecer como `unauthorized`, verifique a tela do dispositivo Android e autorize a conexão.

---

# 10. Reverter a configuração

Caso seja necessário remover a alteração realizada anteriormente, execute:

```bash
adb shell "/system/bin/device_config set_sync_disabled_for_tests none"
```

Depois:

```bash
adb shell "/system/bin/device_config delete activity_manager max_phantom_processes"
```

Após isso, o comportamento volta a depender da configuração padrão do sistema.

---

# 11. Dispositivo com root

Em dispositivos com acesso root, a configuração também pode ser realizada diretamente pelo Termux.

Execute:

```bash
su -c "device_config put activity_manager max_phantom_processes 2147483647"
```

Essa alternativa exige acesso root e, portanto, **não é necessária para dispositivos sem root**.

---

# 12. Relação com o Cyberdeck

O problema é relevante para o Cyberdeck porque o projeto utiliza o Android como plataforma de processamento e o Termux como ambiente para execução do Linux.

A arquitetura atual do ambiente pode ser representada da seguinte forma:

```text
┌───────────────────────────┐
│          Android          │
│       Moto G54            │
└─────────────┬─────────────┘
              │
              ▼
┌───────────────────────────┐
│          Termux           │
└─────────────┬─────────────┘
              │
              ▼
┌───────────────────────────┐
│      Ambiente Linux       │
└─────────────┬─────────────┘
              │
       ┌──────┴───────┐
       ▼              ▼
┌────────────┐   ┌────────────┐
│ Termux:X11 │   │   XFCE4    │
└────────────┘   └────────────┘
       │              │
       └──────┬───────┘
              ▼
┌───────────────────────────┐
│ Interface gráfica do      │
│        Cyberdeck          │
└───────────────────────────┘
```

O Android pode interromper processos dessa cadeia quando considera que eles estão sendo executados em segundo plano.

Por esse motivo, o gerenciamento de processos deve ser considerado durante a configuração e os testes do Cyberdeck.

---

# 13. Procedimento recomendado para o Cyberdeck

Para o desenvolvimento do projeto, recomenda-se seguir esta ordem:

### Etapa 1

Configurar as **Opções do desenvolvedor** do dispositivo.

### Etapa 2

Instalar e configurar o Termux.

### Etapa 3

Configurar o ambiente Linux.

### Etapa 4

Instalar e configurar o Termux:X11.

### Etapa 5

Instalar e configurar o XFCE4.

### Etapa 6

Testar a estabilidade do ambiente.

### Etapa 7

Caso ocorram encerramentos inesperados de processos, utilizar o ADB para aplicar a configuração do Phantom Process Killer.

### Etapa 8

Testar novamente o ambiente gráfico durante um período prolongado.
