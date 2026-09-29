# Calculadora Binária de 5 Bits

Soma dois números de 5 bits (0 a 31) usando lógica digital pura. Construída no Logisim, começando por portas lógicas básicas até chegar numa cascata de somadores. Produz resultado de 5 bits + carry de estouro.

## Por que eu fiz isso

Queria entender como um processador soma de verdade, descendo até o nível das portas lógicas. Comecei montando o XOR na mão com OR + AND + NOT e terminei com a calculadora funcionando no Logisim.

## Como funciona

O circuito é construído em três camadas. Cada uma usa a anterior como bloco de construção.

### 1. Half Adder — soma 2 bits

Soma A + B e produz dois sinais:

- **Soma** = A XOR B
- **Carry** = A AND B

### 2. Full Adder — soma 3 bits

Junta dois Half Adders e um OR. Soma A + B + Cin:

- HA1 soma A + B → Soma1, Carry1
- HA2 soma Soma1 + Cin → Soma final, Carry2
- OR junta Carry1 + Carry2 → Carry out

### 3. Cascata — soma 5 bits

Cinco Full Adders em série. O carry que sai de um vira o carry que entra no próximo. É essa propagação que permite somar números maiores que 1 bit.

    Bit 0 (LSB):  A0 + B0 + Cin=0  →  S0, C1
    Bit 1:        A1 + B1 + C1     →  S1, C2
    Bit 2:        A2 + B2 + C2     →  S2, C3
    Bit 3:        A3 + B3 + C3     →  S3, C4
    Bit 4 (MSB):  A4 + B4 + C4     →  S4, C5 (carry final)

## Estrutura do projeto

    circuits/
      half-adder.circ          # 2 bits: A + B
      full-adder.circ          # 3 bits: A + B + Cin
      calculadora-5bits.circ   # 5 bits: resultado de 0 a 31

    images/
      half-adder.png
      full-adder.png
      calculadora.png

## Como rodar

Não precisa instalar nada. Duas opções:

**Opção 1 — Web (mais rápido):**

1. Acessa logisim.app
2. File → Open → escolhe o .circ desejado
3. Clica no ícone ▶ pra ativar a simulação
4. Seleciona a ferramenta de mão (Poke Tool)
5. Clica nos Input Pins pra alternar 0 e 1

**Opção 2 — Desktop:**

Baixa o Logisim Evolution e abre os mesmos arquivos.

### Lendo o resultado

Os outputs estão em ordem crescente (S0 à esquerda, S4 à direita). Pra ler o valor, soma os LEDs acesos:

| Output | Valor |
|:------:|:-----:|
| S0     | 1     |
| S1     | 2     |
| S2     | 4     |
| S3     | 8     |
| S4     | 16    |

Exemplo: S0 e S2 acesos = 1 + 4 = **5**.

## Testes validados

| A | B | Resultado |
|:-:|:-:|:---------:|
| 0 | 0 | 0         |
| 2 | 0 | 2         |
| 4 | 0 | 4         |
| 1 | 2 | 3         |
| 2 | 2 | 4         |
| 2 | 3 | 5         |

## Limitações

- Só faz **soma**. Subtração, multiplicação e divisão não estão implementadas.
- Se a soma estourar 31, o resultado precisa ser lido como 6 bits (S0–S4 + carry final).
- Não tem display de 7 segmentos. O resultado é lido direto nos LEDs.

## Próximos passos

- Display de 7 segmentos pra mostrar o valor em decimal
- Subtração via complemento de dois
- Registrador pra armazenar o último resultado

## Autor

Rafael Nunes — [@Rafaelnunes-alt2](https://github.com/Rafaelnunes-alt2)