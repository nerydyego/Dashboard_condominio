# Dicionário de Dados — Dashboard Financeiro de Condomínio

## 1. Tabela Fato: fReceitas

| Coluna | Tipo | Descrição |
|---|---|---|
| Data | Data | Data em que a receita foi registrada. |
| Cod_Receita | Número inteiro | Código identificador da receita, relacionado à tabela dimensão `dReceitas`. |
| Receita | Texto | Descrição original da receita extraída da administradora. |
| Tipo | Número inteiro | Código do tipo de movimentação, relacionado à tabela dimensão `dTipo`. |
| Valor | Decimal/Moeda | Valor financeiro da receita. |

---

## 2. Tabela Fato: fDespesas

| Coluna | Tipo | Descrição |
|---|---|---|
| Data | Data | Data em que a despesa foi registrada. |
| Descrição | Texto | Descrição original da despesa extraída da administradora. |
| Valor | Decimal/Moeda | Valor financeiro da despesa. |
| Tipo | Número inteiro | Código do tipo de movimentação, relacionado à tabela dimensão `dTipo`. |
| Cod_SubCateg | Número inteiro | Código da subcategoria da despesa, relacionado à tabela dimensão `dSubCategoria`. |
| Cod_Categoria | Número inteiro | Código da categoria da despesa, relacionado à tabela dimensão `dCategoria`. |

---

## 3. Tabela Dimensão: dCategoria

| Coluna | Tipo | Descrição |
|---|---|---|
| Cod_Categ | Número inteiro | Código único da categoria da despesa. |
| Categoria | Texto | Nome da categoria da despesa. Exemplo: manutenção, contratos, impostos, materiais, serviços etc. |

---

## 4. Tabela Dimensão: dSubCategoria

| Coluna | Tipo | Descrição |
|---|---|---|
| Cod_SubCat | Número inteiro | Código único da subcategoria da despesa. |
| SubCategoria | Texto | Nome detalhado da subcategoria da despesa. |

---

## 5. Tabela Dimensão: dTipo

| Coluna | Tipo | Descrição |
|---|---|---|
| Cod_tipo | Número inteiro | Código único do tipo de movimentação financeira. |
| Descrição | Texto | Descrição do tipo de movimentação. Exemplo: crédito, débito, transferência, ajuste etc. |

---

## 6. Tabela Dimensão: dReceitas

| Coluna | Tipo | Descrição |
|---|---|---|
| Cod_RE | Número inteiro | Código único da receita. |
| Receitas | Texto | Nome ou descrição padronizada da receita. |

---

## 7. Tabela Dimensão: dCalendario

| Coluna | Tipo | Descrição |
|---|---|---|
| Data | Data | Data base para relacionamento com as tabelas fato. |
| Ano | Número inteiro | Ano da data. |
| Mês | Texto | Nome do mês. |
| Mês Número | Número inteiro | Número do mês, usado para ordenação cronológica. |
| Ano-Mês | Texto | Combinação de ano e mês para análises mensais. |
| Trimestre | Texto | Trimestre correspondente à data. |

---

# Relacionamentos Esperados

| Tabela Fato | Coluna | Tabela Dimensão | Coluna | Cardinalidade |
|---|---|---|---|---|
| fDespesas | Cod_Categoria | dCategoria | Cod_Categ | Muitos para Um |
| fDespesas | Cod_SubCateg | dSubCategoria | Cod_SubCat | Muitos para Um |
| fDespesas | Tipo | dTipo | Cod_tipo | Muitos para Um |
| fReceitas | Cod_Receita | dReceitas | Cod_RE | Muitos para Um |
| fReceitas | Tipo | dTipo | Cod_tipo | Muitos para Um |
| fDespesas | Data | dCalendario | Data | Muitos para Um |
| fReceitas | Data | dCalendario | Data | Muitos para Um |

---

# Observações sobre Tratamento dos Dados

Os dados originais foram extraídos da plataforma da administradora do condomínio em formato XLS.

Após a extração, os dados foram migrados para uma nova planilha, onde passaram por processo de tratamento, padronização e organização.

As informações descritivas, como categorias, subcategorias, tipos e receitas, foram transformadas em tabelas dimensão, permitindo melhor estruturação do modelo de dados e maior eficiência na análise dentro do Power BI.

As tabelas de receitas e despesas foram mantidas separadas, pois representam naturezas financeiras diferentes. No dashboard, elas serão analisadas individualmente e também utilizadas em comparativos quando necessário.