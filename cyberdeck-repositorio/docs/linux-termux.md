# 🐧 Linux via Termux

A proposta do Cyberdeck utiliza o Termux para instalar e executar um ambiente Linux completo sobre o Android.

## Script

O projeto descrito na proposta utiliza um script de configuração automatizada com:

- detecção automática do dispositivo e da GPU;
- suporte a XFCE4, LXQt, MATE e KDE;
- otimização gráfica por GPU;
- instalação simplificada;
- compatibilidade com smartphones e tablets.

Repositório mencionado na proposta original:

`https://github.com/lucasaguiar-la/linux-android`

## Requisitos

- Android 5.0 ou superior;
- Termux instalado via F-Droid;
- Termux:X11 instalado;
- aproximadamente 2 GB de espaço livre;
- conexão com a internet.

## Instalação prevista

### 1. Preparar o Termux

Instalar o Termux e conceder acesso ao armazenamento:

```bash
termux-setup-storage
```

### 2. Preparar o aparelho

Ativar o modo Desenvolvedor e desabilitar:

`Desativar restrições de processos filhos`

ou:

`Disable child process restrictions`

### 3. Instalar Git

```bash
pkg install git
```

### 4. Clonar o script

```bash
git clone https://github.com/lucasaguiar-la/linux-android.git
cd linux-android
```

### 5. Permitir execução

```bash
chmod +X script-termux.sh
```

### 6. Executar

```bash
./script-termux.sh
```

### 7. Escolher o desktop

O script permite selecionar:

- XFCE4;
- LXQt;
- MATE;
- KDE.

### 8. Inicializar

Após a instalação:

```bash
cd
./start-linux.sh
```

### 9. Interface gráfica

Abrir o Termux:X11 para acessar o ambiente desktop Linux.

## ⚠️ Registro de alterações

Os comandos acima reproduzem o procedimento descrito na proposta original. Este arquivo deverá ser atualizado conforme os testes reais do Cyberdeck forem realizados.
