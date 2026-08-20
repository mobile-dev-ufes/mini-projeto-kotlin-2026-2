# Mini-projeto Kotlin

**Programação para Dispositivos Móveis — 2025/2**

---

## Objetivo

O objetivo deste mini-projeto é colocar em prática os conhecimentos adquiridos na linguagem de programação Kotlin. O projeto foi elaborado para que você exercite, principalmente, os conceitos de **orientação a objetos** e **coleções** usando a linguagem. Além disso, este mini-projeto vai contar como **10% da nota final** da disciplina e deve ser feito de maneira **individual**.

## Descrição

Imagine que você foi contratado para construir um sistema de gerenciamento de uma **loja de artigos esportivos**. A loja possui diversos produtos classificados em três categorias: **vestuário**, **calçado** e **suplemento**. Independentemente da categoria, cada produto sempre deve possuir as seguintes informações:

- Nome do produto
- Preço pelo qual foi comprado para revender
- Preço pelo qual será vendido
- Código do produto

Dependendo da categoria, o produto possui outras informações.

**Se for um vestuário**, ele possui:

- Tipo: `CAMISA`, `BERMUDA`, `AGASALHO` ou `ACESSORIO`
- Tamanho: `PP`, `P`, `M`, `G`, `GG` ou `XG`
- Cor primária
- Cor secundária, caso exista

**Se for um calçado**, ele possui:

- Tipo: `CORRIDA`, `CAMINHADA`, `FUTEBOL` ou `CASUAL`
- Numeração (número inteiro, ex.: 42)
- Material: `COURO`, `SINTETICO`, `TECIDO` ou `MISTO`

**Se for um suplemento**, ele possui:

- Tipo: `PROTEINA`, `CREATINA`, `VITAMINA` ou `OUTROS`
- Sabor, caso exista
- Peso em gramas (número inteiro)
- Categoria do suplemento: `HIPERTROFIA`, `ENERGIA`, `SAUDE` ou `OUTROS`

O código do produto, que já é atribuído pelo fornecedor da loja, pode ser constituído por letras e números. Porém, para facilitar a visualização, o cliente deseja que você **acrescente ao código original a primeira letra da categoria principal, separada por hífen**. Portanto, se o código do produto for `CAM02` e ele pertencer à categoria vestuário, o sistema deve transformá-lo em `V-CAM02`. Os códigos estarão sempre em maiúsculo.

As iniciais são: **V**estuário → `V`, **C**alçado → `C`, **S**uplemento → `S`.

## Funcionalidades do programa

O programa de gerenciamento da loja possui 4 grandes funcionalidades: **gerenciamento de compra e venda de produtos**, **gerenciamento de estoque**, **balancete da loja** e **sistema de busca**. Cada item é detalhado na sequência. Junto com esta descrição é disponibilizado casos de teste completo, com entrada e saída.

### Gerenciamento de compra e venda

A primeira funcionalidade do seu programa é gerenciar a compra e a venda da loja. As compras e vendas serão obtidas através de dois arquivos `.csv`. O arquivo de compra (`compras.csv`) contém todas as informações do produto, além da quantidade que foi comprada. Já o arquivo de vendas (`vendas.csv`) possui apenas o código e a quantidade do produto vendido. Em ambos os casos, **cada linha do arquivo representa uma compra ou uma venda**.

Um mesmo produto (mesmo código) pode aparecer em mais de uma linha de compra; nesse caso, as quantidades se somam.

### Gerenciamento de estoque

Ao final de todas as operações de compra e venda, o programa precisa gerar um estoque consolidado da loja. Para isso, ele deve gerar dois arquivos chamados `estoque_geral.csv` e `estoque_categoria.csv`. O primeiro deve conter todo o estoque da loja com **um produto por linha**. Para simplificar, o produto é representado apenas pelo **código** (já formatado com a inicial da categoria), **nome** e **quantidade** atual em estoque. Porém, você deve manter o estoque completo em memória. O segundo arquivo é apenas uma consolidação por categoria, ou seja, cada linha vai ter a **categoria** e a **quantidade total de unidades em estoque** dessa categoria.

A quantidade em estoque de um produto é a quantidade comprada menos a quantidade vendida. Produtos cujo estoque chegou a zero **continuam aparecendo** no `estoque_geral.csv` com quantidade `0`.

### Balancete da loja

O programa também deve gerar um balancete geral da loja para consolidar as compras e vendas. Para isso, o programa deve gerar um arquivo chamado `balancete.csv` que contém, em uma única linha, o valor gasto em **compras**, o valor obtido em **vendas** e o **balancete**, que mostra o lucro ou prejuízo da loja. O balancete é `VENDAS − COMPRAS` (valor negativo indica prejuízo de caixa).

- `COMPRAS` = soma de `preço de compra × quantidade` de cada linha de `compras.csv`.
- `VENDAS` = soma de `preço de venda × quantidade` de cada linha de `vendas.csv` (o preço de venda é o do produto cadastrado nas compras).

### Sistema de busca

Por fim, o programa permite que sejam realizadas buscas no estoque virtual da loja. Para realizar a busca, o programa vai receber um arquivo chamado `busca.csv` que contém as informações que devem ser buscadas no estoque. Realizada a busca, seu programa deve gerar um arquivo chamado `resultado_busca.csv` que contém a **quantidade em estoque** correspondente a cada uma das buscas solicitadas (vide exemplo para melhor compreensão).

Cada linha de `busca.csv` é uma consulta. A **categoria é sempre informada**; os demais campos podem conter um valor (a ser casado) ou o tracinho `-` (ignorado). Um produto satisfaz a consulta se pertence à categoria informada **e** casa com **todos** os campos preenchidos (diferentes de `-`). A quantidade retornada é a **soma das quantidades em estoque** de todos os produtos que satisfazem a consulta.

## Funcionamento do programa

O seu programa deve receber, como argumentos de entrada padrão, os caminhos completos para as pastas de **entrada** e de **saída** de dados, respeitando essa ordem: o primeiro argumento é a string que representa a pasta de entrada e o segundo, a pasta de saída. Todos os arquivos `.csv` de entrada citados nesta descrição estarão disponíveis no caminho indicado.

Após a leitura dos caminhos, seu programa deve executar o gerenciamento de compra e venda. Na sequência, realiza o gerenciamento de estoque e o balancete da loja. O sistema de busca é **opcional**: ele só ocorre se, na pasta de entrada, existir o arquivo `busca.csv`. Todos os arquivos `.csv` de saída devem ser escritos dentro da pasta de saída informada como parâmetro.

## Formato dos arquivos

Todos os arquivos usam **vírgula** como separador, **ponto** como separador decimal e possuem uma **linha de cabeçalho** (que deve ser ignorada na leitura e reescrita na saída). Todos os dados são tratados em **maiúsculo, sem acentos**. Informações inexistentes são representadas por tracinho (`-`).

### Entrada

**`compras.csv`**
```
CATEGORIA,CODIGO,NOME,PRECO_COMPRA,PRECO_VENDA,QUANTIDADE,ATRIB1,ATRIB2,ATRIB3,ATRIB4
```

**`vendas.csv`** (o código é o código original do fornecedor, sem a inicial da categoria)
```
CODIGO,QUANTIDADE
```

**`busca.csv`** (opcional)
```
CATEGORIA,CODIGO,NOME,ATRIB1,ATRIB2,ATRIB3,ATRIB4
```

Os quatro atributos `ATRIB1..ATRIB4` têm significado dependente da categoria:

| Categoria    | ATRIB1 | ATRIB2    | ATRIB3        | ATRIB4          |
|--------------|--------|-----------|---------------|-----------------|
| `VESTUARIO`  | tipo   | tamanho   | cor primária  | cor secundária  |
| `CALCADO`    | tipo   | numeração | material      | (sempre `-`)    |
| `SUPLEMENTO` | tipo   | sabor     | peso (g)      | categoria supl. |

### Saída

**`estoque_geral.csv`** — um produto por linha, na mesma ordem em que aparece pela primeira vez em `compras.csv`:
```
CODIGO,NOME,QUANTIDADE
```

**`estoque_categoria.csv`** — categorias na ordem de primeira aparição em `compras.csv`:
```
CATEGORIA,QUANTIDADE
```

**`balancete.csv`**
```
COMPRAS,VENDAS,BALANCETE
```

**`resultado_busca.csv`** — ecoa a consulta e acrescenta a quantidade encontrada, na mesma ordem de `busca.csv`:
```
CATEGORIA,CODIGO,NOME,ATRIB1,ATRIB2,ATRIB3,ATRIB4,QUANTIDADE
```

## Exemplo

**Entrada — `compras.csv`**
```
CATEGORIA,CODIGO,NOME,PRECO_COMPRA,PRECO_VENDA,QUANTIDADE,ATRIB1,ATRIB2,ATRIB3,ATRIB4
VESTUARIO,CAM01,CAMISA BRASIL,45.00,89.90,10,CAMISA,M,VERDE,AMARELO
CALCADO,TEN05,TENIS CORRIDA,120.00,249.90,5,CORRIDA,42,SINTETICO,-
SUPLEMENTO,WHEY1,WHEY CHOCOLATE,80.00,159.90,8,PROTEINA,CHOCOLATE,900,HIPERTROFIA
```

**Entrada — `vendas.csv`**
```
CODIGO,QUANTIDADE
CAM01,3
TEN05,2
```

**Entrada — `busca.csv`**
```
CATEGORIA,CODIGO,NOME,ATRIB1,ATRIB2,ATRIB3,ATRIB4
VESTUARIO,-,-,CAMISA,-,-,-
SUPLEMENTO,-,-,PROTEINA,-,900,-
```

**Saída — `estoque_geral.csv`**
```
CODIGO,NOME,QUANTIDADE
V-CAM01,CAMISA BRASIL,7
C-TEN05,TENIS CORRIDA,3
S-WHEY1,WHEY CHOCOLATE,8
```

**Saída — `estoque_categoria.csv`**
```
CATEGORIA,QUANTIDADE
VESTUARIO,7
CALCADO,3
SUPLEMENTO,8
```

**Saída — `balancete.csv`**
```
COMPRAS,VENDAS,BALANCETE
1690.00,769.50,-920.50
```
> `COMPRAS = 45,00×10 + 120,00×5 + 80,00×8 = 1690,00` · `VENDAS = 89,90×3 + 249,90×2 = 769,50` · `BALANCETE = 769,50 − 1690,00 = −920,50`.

**Saída — `resultado_busca.csv`**
```
CATEGORIA,CODIGO,NOME,ATRIB1,ATRIB2,ATRIB3,ATRIB4,QUANTIDADE
VESTUARIO,-,-,CAMISA,-,-,-,7
SUPLEMENTO,-,-,PROTEINA,-,900,-,8
```

> **Importante:** o exemplo deve ser sempre utilizado como referência principal.

Veja a pasta de testes disponível nesta descrição.

## Correção do mini-projeto

Para permitir a correção automatizada, o seu projeto deve permitir a criação de um arquivo com extensão `.jar` chamado `miniprojeto.jar`. Para isso, crie o projeto seguindo as [instruções disponibilizadas na documentação do IntelliJ](https://www.jetbrains.com/help/idea/create-your-first-kotlin-app.html).

Além disso, o projeto deve ser criado utilizando a versão do `open-jdk` disponível no Labgrad.

> **Importante:** se você não seguir essas instruções, você não vai conseguir gerar o `.jar`.


Os testes de correção serão automatizados e executarão o seu projeto de acordo com os seguintes passos:

1. Executar o script `./gradlew jar`, que é gerado automaticamente dentro da pasta do projeto.
2. Executar o arquivo `miniprojeto.jar` da seguinte forma:
   ```
   java -jar miniprojeto.jar <path_completo_pasta_entrada> <path_completo_pasta_saida>
   ```

Ao final da execução, é esperado que seu programa tenha gerado a pasta de saída com os resultados corretos para cada um dos casos de teste.

## Prazo e submissão

A submissão do projeto será realizada utilizando a organização da disciplina no GitHub (se você não foi convidado, entre em contato com o professor). Para isso, siga as instruções:

- Crie um repositório **privado** dentro da organização.
- O nome do repositório deve seguir o padrão: `2026-2-mini-proj-kotlin-<nome>-<sobrenome>`.
  - Exemplo: `2026-2-mini-proj-kotlin-andre-pacheco`.
- Siga todas as instruções corretamente; caso contrário, seu repositório não será encontrado.

O prazo do último *commit* no repositório é definido no Google Classroom. Qualquer *commit* fora do prazo será considerado entrega em atraso e desconsiderado.

## Regras gerais

Para todos os casos, adote as seguintes regras:

- Transforme todas as entradas para maiúsculo. Todas as saídas devem estar em maiúsculo.
- Ignore acentos.
- Se um dado produto não possui uma informação, ela é representada por tracinho (`-`).
- A mesma notação é utilizada na busca. Utilize apenas as informações úteis, ou seja, diferentes do tracinho.
- As entradas seguirão sempre o mesmo padrão, inclusive nos nomes dos arquivos de entrada e de saída.
- Os dados de saída devem ser processados na mesma sequência em que aparecem no arquivo de compras.
- Possíveis plágios não serão tolerados. Todos os trabalhos serão testados com software de análise de plágio.

---

Possíveis problemas nesta descrição serão solucionados em sala de aula e comunicados a todos. Qualquer dúvida, faça um post no Google Classroom. **Don't Panic!**
