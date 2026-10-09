# Desafio1_M-dulo5_DIO_PowerBI

Este repositório abriga um Dashboard Gerencial para Tomada de Decisão utilizando a Sample Financials do Power BI

# Desafio DIO - Atualizando Relatório Financeiro com Foco na Experiência do Usuário

Este repositório apresenta a resolução do desafio proposto pela DIO, utilizando o Power BI para aprimorar um relatório financeiro com foco na experiência do usuário, na organização visual e na análise dos dados.

O projeto utiliza a base **Financial Sample** e busca tornar as informações mais claras e acessíveis por meio da reorganização dos visuais, da utilização de filtros e da criação de elementos de navegação entre as páginas do relatório.

## Objetivos do desafio

O desafio consiste em atualizar o relatório financeiro desenvolvido durante o curso, considerando os seguintes aspectos:

- **Posicionamento:** organizar os elementos para facilitar a leitura e a interpretação das informações.
- **Contraste:** melhorar a diferenciação entre os elementos visuais.
- **Proporção áurea:** considerar proporções e distribuição dos elementos na composição do relatório.
- **Segmentação dos dados:** permitir a análise das informações por diferentes categorias e períodos.
- **Navegação:** implementar botões e menus para facilitar a movimentação entre as páginas.

## Estrutura do relatório

O relatório foi organizado em três páginas, cada uma com diferentes perspectivas de análise dos dados financeiros.

### 1. Sales Report

Página dedicada à análise das vendas, apresentando indicadores e gráficos para acompanhar o desempenho comercial.

Entre os elementos utilizados estão:

- Indicadores de vendas totais (*Sales*) e unidades vendidas (*Units Sold*).
- Gráfico de vendas por período.
- Segmentação por produto e outras categorias.
- Matriz com a descrição das vendas por ano, trimestre e canal de distribuição.
- Filtro de período para facilitar a análise temporal.

### 2. Profit Report

Página voltada à análise da lucratividade, permitindo observar o desempenho financeiro por localização geográfica e período.

Entre os elementos utilizados estão:

- Análise do lucro (*Profit*) por país.
- Comparação entre lucro e unidades vendidas por país.
- Análise do lucro mensal.
- Indicadores complementares para contextualizar os resultados.
- Filtros por ano para facilitar a comparação entre períodos.

### 3. Análises complementares

A terceira página reúne análises adicionais utilizando medidas DAX, permitindo explorar o desempenho dos produtos, dos segmentos e dos países.

Entre os elementos utilizados estão:

- Indicador de máximo de unidades vendidas.
- Análise dos três principais produtos.
- Comparação entre países com base nas unidades vendidas.
- Distribuição das unidades vendidas por produto.
- Análises complementares de vendas e lucro por mês.

## Medidas DAX

Além da organização visual do relatório, foram utilizadas medidas DAX para calcular indicadores e auxiliar na análise dos dados.

### Total Sales

```dax
Total Sales = SUMX(financials, financials[Sales])
```

A função `SUMX()` percorre as linhas da tabela `financials`, avalia o valor da coluna `Sales` em cada linha e soma os resultados.

Essa medida permite calcular o total de vendas, respeitando os filtros aplicados ao relatório, como período, produto e segmento.

### Máximo Sold

```dax
Máximo Sold = MAX(financials[Units Sold])
```

A função `MAX()` retorna o maior valor encontrado na coluna `Units Sold,` considerando o contexto de filtros aplicado.

Essa medida permite identificar o maior volume de unidades vendidas em determinado contexto de análise.

### Top 3 Product

```dax
Top 3 Product =
CALCULATE(
    [Total Sales],
    TOPN(
        3,
        ALL(financials[Product]),
        [Total Sales]
    ),
    VALUES(financials[Product])
)
```

A função `TOPN()` identifica os três produtos com os maiores valores de vendas, utilizando a medida `[Total Sales]` como critério de classificação.

A função `ALL()` remove os filtros existentes sobre a coluna `Product` durante a identificação dos principais produtos, enquanto `CALCULATE()` modifica o contexto de avaliação da medida.

Essa combinação permite destacar os produtos com maior participação nas vendas, facilitando a comparação de desempenho entre eles.

### Outlier

```dax
Outlier =
CALCULATE(
    [Total Sales],
    FILTER(
        VALUES(financials[Product]),
        COUNTROWS(
            FILTER(
                financials,
                [Total Sales] >= 150
            )
        ) > 0
    )
)
```

Essa medida utiliza `CALCULATE()`, `FILTER()`, `VALUES()` e `COUNTROWS()` para aplicar condições sobre os produtos e calcular as vendas dentro do contexto resultante.

A condição `> 0` verifica se existe pelo menos uma linha que atende ao critério definido no filtro interno.

**Observação:** embora o nome da medida seja `Outlier`, a expressão, por si só, não implementa um método estatístico completo de detecção de valores atípicos. O resultado depende do contexto de avaliação da medida `[Total Sales]` e da condição utilizada. Para identificar outliers estatísticos, seria necessário definir um critério específico.

## Recursos utilizados

- **Power BI Desktop:** desenvolvimento do relatório, criação de visuais, filtros e navegação.
- **DAX (Data Analysis Expressions):** criação de medidas e cálculos para análise dos dados.
- **Financial Sample:** base de dados utilizada no projeto.

## Resultado

O resultado é um relatório financeiro dividido em três páginas, com diferentes perspectivas de análise e recursos destinados a melhorar a experiência de navegação.

O projeto demonstra a aplicação de conceitos de visualização de dados, organização de dashboards e utilização de medidas DAX para transformar dados financeiros em informações úteis para análise e tomada de decisão.

## Aprendizados

A realização do desafio permitiu praticar:

- Organização e distribuição de elementos visuais em relatórios.
- Aplicação de princípios de design para melhorar a legibilidade.
- Utilização de filtros e segmentações para explorar os dados.
- Criação e aplicação de medidas DAX.
- Construção de botões e menus de navegação entre páginas.
- Desenvolvimento de relatórios com foco na experiência do usuário.

---

**Tecnologias:** Power BI Desktop e DAX.

**Projeto desenvolvido como parte dos desafios práticos da DIO.**
