# Calculadora Topográfica

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Licença MIT](https://img.shields.io/badge/Licen%C3%A7a-MIT-green?style=for-the-badge)
![Math](https://img.shields.io/badge/math-%23000000.svg?style=for-the-badge&logo=python&logoColor=white)

## Visão Geral
Este repositório fornece um script Python desenvolvido para automatizar os cálculos matemáticos fundamentais da disciplina de Topografia. O código foi arquitetado com um propósito estrito: **entregar estabilidade e precisão em ambientes de campo.**

## Objetivo Principal
A premissa deste projeto é a **resiliência operacional**. O software foi desenhado para ser operado sob pressão, evitando travamentos (crashes) e dependências de ambiente. Seus três pilares fundamentais são:

* **Independência de Ambiente (Zero Setup):** Construído exclusivamente com a biblioteca nativa `math`. Não há necessidade de gerenciadores de pacotes ou ambientes virtuais (`pip install`). O código roda "out-of-the-box" em qualquer dispositivo com Python instalado — desde servidores até IDEs de bolso em smartphones (como Pydroid 3 ou Pythonista).
* **Robustez e Prevenção de Falhas (Fail-Safe):** Operações em campo estão sujeitas a erros de digitação e formatações inconsistentes. O script implementa validações rigorosas e blocos `try/except` que interceptam caracteres inválidos, excesso de espaços e entradas ilógicas. O programa absorve a falha, alerta o operador e mantém a execução.
* **Integridade Matemática:** Rotinas automáticas de normalização trigonométrica garantem que qualquer anomalia angular (valores negativos, empréstimos incorretos de minutos/segundos ou giros além de 360°) seja rigorosamente corrigida para o quadrante e formato corretos antes da exibição ao usuário.

## Funcionalidades
1. **Inversão de Ângulos:** Subtração direta de ângulos em formato sexagesimal (GMS) por 360°.
2. **Aritmética Angular:** Soma e subtração de ângulos com ajuste automático de graus, minutos e segundos.
3. **Cálculo de Coordenadas Relativas (XY):** Conversão de Azimute e Distância Horizontal para o plano cartesiano, aceitando formatação numérica brasileira (vírgula) e internacional (ponto) de forma nativa.

## Como Executar
Nenhuma configuração prévia é necessária. Basta executar o script em seu interpretador Python de preferência para abrir o menu interativo:

```bash
python calculadora_topografica.py
