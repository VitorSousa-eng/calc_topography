# Teste de Estresse (Stress Test) - Calculadora Topográfica

Este documento contém um conjunto de dados caóticos para testar a resiliência do script `calculadora_topografica.py`. O objetivo é provar que o código não "quebra" (crash) quando o usuário, no meio do campo e com pressa, digita entradas completamente fora do padrão.

Sinta-se à vontade para rodar o script e inserir os dados abaixo exatamente como estão escritos.

## 1. Tratamento de Espaços e Formatação (Menu 1)
O ambiente de campo é propício a erros de digitação (esbarrar no teclado do celular). Vamos testar como o interpretador lida com espaços duplos e formatação bizarra.

| O que você digita (Ângulo) | O que o programa deve fazer | Por que isso ocorre? |
| :--- | :--- | :--- |
| `  12     34    56   ` | **Sucesso:** Calcula normalmente. | O `.split()` remove todos os espaços excedentes automaticamente. |
| `12 34` | **Erro Tratado:** Pede 3 números. | Validação `len(partes) != 3` impede o cálculo incompleto. |
| `12 34 56 78` | **Erro Tratado:** Pede 3 números. | Evita que o programa tente processar um quarto valor inexistente. |
| `12 A 56` | **Erro Tratado:** Aviso de valor inválido. | O `try/except` com `ValueError` impede que letras quebrem o código. |

## 2. Abuso Trigonométrico e Modulo 360 (Menu 1 e 2)
Na pressa, o operador pode inserir valores absurdos no limbo do equipamento. O script deve ser capaz de normalizar esses ângulos utilizando a matemática do círculo trigonométrico.

| O que você digita | Operação | O que o programa deve fazer | Explicação Matemática |
| :--- | :--- | :--- | :--- |
| **Ang 1:** `400 00 00` | Subtrair de 360° | **Resultado:** `320° 00' 00"` | O Python entende que 360 - 400 = -40. A função normaliza `-40 % 360` resultando em 320°. |
| **Ang 1:** `0 150 3600` | Subtrair de 360° | **Resultado:** `356° 30' 00"` | Ele converte os minutos e segundos absurdos (150' e 3600") para 3,5 graus. 360 - 3.5 = 356.5°. |
| **Ang 1:** `10 00 00`<br>**Ang 2:** `30 00 00` | Subtração (`-`) | **Resultado:** `340° 00' 00"` | 10° - 30° = -20°. O script faz a manobra de "empréstimo" automaticamente, retornando ao quadrante correto (340°). |

## 3. Conversão de Distâncias e Float (Menu 3)
Cálculo de coordenadas exige extrema precisão. O script deve aceitar padrões brasileiros e americanos de pontuação, mas rejeitar lixo de texto.

| Azimute | Distância (Input) | O que o programa deve fazer | Explicação |
| :--- | :--- | :--- | :--- |
| `45 00 00` | `100,55` | **Sucesso:** Calcula X e Y. | O `.replace(',', '.')` atua antes da conversão, salvando o usuário brasileiro. |
| `45 00 00` | `100m` | **Erro Tratado:** Pede número válido. | Letras junto com a distância disparam o aviso de erro específico para distância. |
| `45 00 00` | `100,50,2` | **Erro Tratado:** Pede número válido. | Múltiplas vírgulas impedem a conversão para `float`. |
| `90 00 00` | `100` | **Sucesso:** `X = 100.000` / `Y = 0.000` | Testa o seno de 90 (1) e o cosseno de 90 (0). *Nota: Y pode aparecer como `0.000` ou um número ínfimo como `0.00000000000000006` devido à imprecisão de ponto flutuante do processador (IEEE 754).* |

## 4. Testes de Estresse de Interface (Menu Principal)
Testando a quebra do Loop `while True`.

| O que você digita no Menu | O que o programa deve fazer |
| :--- | :--- |
| `Enter` (vazio) | Mostra aviso de opção inválida e repete o menu. |
| `5` | Mostra aviso de opção inválida e repete o menu. |
| `abc` | Mostra aviso de opção inválida e repete o menu. |
| `0` | Encerra o programa pacificamente ("Bom trabalho em campo!"). |

> **Conclusão do Teste:** O script é *Fail-Safe* (à prova de falhas). Em nenhum dos cenários acima o programa sofre um crash fechando o terminal do usuário. Ele absorve o impacto do erro, instrui o operador e retorna ao estado funcional.
