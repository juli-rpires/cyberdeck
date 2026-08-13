# 🖥️ Cyberdeck

> Computador portátil construído a partir de sucata eletrônica.

Projeto de construção de um computador portátil funcional utilizando componentes eletrônicos reaproveitados e materiais disponíveis em casa. A proposta une eletrônica, montagem física e programação em um projeto prático de reaproveitamento tecnológico e computação de baixo custo.

## 🎯 Objetivo

Projetar e construir um computador portátil (**cyberdeck**) funcional a partir de componentes de sucata eletrônica.

### Objetivos específicos

- ♻️ Reaproveitar um smartphone Android como unidade central de processamento;
- ⌨️ Integrar um mini teclado Bluetooth com touchpad;
- 📦 Construir um invólucro/caixa para acomodar e proteger os componentes;
- 🐧 Instalar um ambiente Linux sobre o Android através do Termux;
- 💻 Testar o conjunto para tarefas básicas de computação;
- 📸 Documentar todo o processo de montagem e os resultados.

## 🧩 Conceito

A versão inicial utiliza um **Motorola Moto G54** como núcleo de processamento, memória, tela e sistema operacional.

O conjunto é formado por:

- 📱 Motorola Moto G54 reaproveitado;
- ⌨️ Mini teclado Bluetooth com touchpad;
- 📦 Caixa, maleta ou outro invólucro reaproveitado;
- 🔋 Power bank para alimentação;
- 🔌 Cabos e conectores necessários;
- 🐧 Ambiente Linux instalado através do Termux.

A ideia é transformar o smartphone em um computador portátil de uso geral, mantendo o projeto acessível e baseado em reaproveitamento eletrônico.

## 🛠️ Montagem física

O projeto inicial prevê:

1. Seleção dos componentes disponíveis;
2. Teste individual do celular e do teclado;
3. Planejamento do layout interno da caixa/maleta;
4. Adaptação do invólucro;
5. Fixação do smartphone, teclado e power bank;
6. Testes de digitação, navegação, autonomia e conforto;
7. Ajustes finais e registro fotográfico.

## 🐧 Linux via Termux

O projeto prevê a instalação de um ambiente Linux completo sobre o Android utilizando o Termux.

O script utilizado no projeto possui suporte aos ambientes:

| Ambiente | Perfil |
|---|---|
| XFCE4 | ⚖️ Equilíbrio entre desempenho e funcionalidade |
| LXQt | 🪶 Mais leve, indicado para dispositivos antigos |
| MATE | 🧩 Alternativa estável |
| KDE | 🖥️ Mais pesado, indicado para dispositivos mais potentes |

### Requisitos previstos

- Android 5.0 ou superior;
- Termux instalado via F-Droid;
- Termux:X11;
- Aproximadamente 2 GB de espaço livre;
- Conexão com a internet.

A documentação detalhada da configuração está em [`docs/linux-termux.md`](docs/linux-termux.md).

## 📸 Processo

As fotos e registros da montagem serão adicionados nesta pasta:

[`imagens/`](imagens/)

### Protótipo

*Fotos da montagem serão adicionadas conforme o projeto avançar.*

## 🔭 Possíveis evoluções

O conceito do Cyberdeck pode evoluir para outras plataformas, incluindo:

- Monitor LCD reaproveitado + SBC;
- Placa-mãe de PC/notebook;
- ESP32;
- TV Box;
- Raspberry Pi;
- Orange Pi;
- Banana Pi.

Essas alternativas mantêm o conceito de um computador portátil reaproveitado, mas podem alterar o nível de processamento, alimentação, tamanho e complexidade.

## 📚 Documentação

- [`docs/projeto.md`](docs/projeto.md) — descrição do projeto, objetivos, materiais e metodologia;
- [`docs/montagem.md`](docs/montagem.md) — roteiro da montagem física;
- [`docs/linux-termux.md`](docs/linux-termux.md) — configuração do ambiente Linux via Termux;
- [`docs/Projeto_Cyberdeck.pdf`](docs/Projeto_Cyberdeck.pdf) — proposta original do projeto.

## 🌱 Resultados esperados

Espera-se obter um dispositivo portátil funcional para tarefas básicas de computação e, com o ambiente Linux via Termux, ampliar as possibilidades de uso do smartphone como computador.

Além do dispositivo, o projeto pretende gerar uma documentação do processo de montagem, servindo como material de estudo sobre reaproveitamento eletrônico e montagem de hardware.

---

**Projeto Cyberdeck**  
Autora: Jiulia Ramos Pires  
Professor: Maximiano Correia Martins
