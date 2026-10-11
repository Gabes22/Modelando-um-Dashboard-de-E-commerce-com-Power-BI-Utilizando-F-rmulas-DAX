# Desafio de Projeto: Modelagem Dimensional com Power BI - Star Schema

Este repositório contém a resolução do desafio de projeto focado em transformar uma base de dados única (flat table) em um modelo relacional baseado nas boas práticas de Business Intelligence, utilizando o conceito de *Star Schema (Modelo Estrela)*.

## 📊 Estrutura do Modelo de Dados

O modelo foi reestruturado a partir de uma tabela de exemplo (financials), criando uma tabela fato central responsável pelas métricas de movimentação e tabelas dimensão responsáveis pelos contextos de filtros.

### Tabelas Criadas:
- *financials_origem:* Tabela oculta e com carga desabilitada utilizada como backup estrutural e origem para as demais referências.
- *F_Vendas (Tabela Fato):* Concentra as métricas financeiras cruciais como Sales, Profit, Gross Sales, quantidades de unidades vendidas (Units Sold), além das chaves estrangeiras para conexão.
- *D_Produtos (Tabela Dimensão):* Armazena o ID único do produto (ID_Produto) gerado via coluna condicional, o nome do produto e agregações estatísticas calculadas via Power Query (médias, valores máximos, mínimos e medianas de preço).
- *D_Produtos_Detalhes (Tabela Dimensão):* Detalhamento dos produtos contendo faixas de descontos (Discount Band), preço de venda, custo de fabricação e unidades vendidas.
- *D_Descontos (Tabela Dimensão):* Relacionamento de contexto focado em mapear os valores e faixas de desconto associados a cada ID de produto.

## 🛠️ Processo de ETL (Extração, Transformação e Carga) no Power Query

1. *Criação de Chaves Condicionais:* Criação da coluna ID_Produto mapeando de 0 a 5 cada produto da base para garantir relacionamentos íntegros baseados em chaves numéricas.
2. *Agrupamento de Dados (Group By):* Consolidação de dados estatísticos diretamente na dimensão de produtos para otimização da performance do relatório.
3. *Tratamento de Dados:* Correção de divergências textuais (case-sensitive) eliminando registros nulos (null) e garantindo consistência relacional.
4. *Otimização de Performance:* A tabela original (financials) teve sua carga desabilitada no modelo e foi oculta da visão de relatório, funcionando puramente como geradora de referências em segundo plano.

## 📐 Funções DAX Utilizadas

Para a criação da tabela de dimensão temporal dinâmica, foi utilizada a linguagem DAX através da função:
- *D_Calendário*: Estruturada com as funções ADDCOLUMNS, CALENDARAUTO, YEAR, MONTH, FORMAT e QUARTER para gerar automaticamente colunas de data, ano, número do mês, nome do mês e trimestre com base nos períodos existentes na tabela fato.

## 📐 Visualização do Modelo Relacional

![Modelo de Dados Star Schema](insira_aqui_o_link_do_print_da_sua_tela.png)

O modelo final apresenta cardinalidade de 1 para muitos (1:) com fluxo de filtragem direcionado das tabelas dimensão para a tabela fato.*

## 👨‍💻 Autor
Desenvolvido por **Gabriela Pereira das Neves** no âmbito da jornada de transição e especialização em Dados e Tecnologia.
