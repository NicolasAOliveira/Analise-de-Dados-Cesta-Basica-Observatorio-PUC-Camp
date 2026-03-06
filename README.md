# Análise Técnica Completa — Otimização Estratégica da Cesta Básica

**Pipeline de Engenharia de Dados + Economia de 29,1%  
Observatório da Cesta Básica – PUC Campinas**

**Autor:** Nicolas Alencar de Oliveira  
**Matrícula:** 23012092  
**Email:** nicolas.ao@puccampinas.edu.br  

---

## 1. Objetivo Técnico

Implementação de um **pipeline analítico completo** sobre **27.170 registros de preços desagregados** da cesta básica (set/2022 – mar/2025) provenientes do Observatório da Cesta Básica da PUC Campinas.

O projeto executa:

- **Engenharia de dados com correção automatizada de anomalias**
- **Padronização inteligente de marcas duplicadas**
- **Análise multifatorial de volatilidade (Coeficiente de Variação + sazonalidade)**
- **Sistema de categorização nutricional**
- **Quantificação precisa do custo mensal por estabelecimento**
- **Modelo de substituição estratégica multi-critério**

Resultado final:

***29,1% de economia potencial na cesta básica analisada***

---

## 2. Pipeline Técnico

### 2.1 Engenharia de Dados e Tratamento de Anomalias

#### Detecção e correção de outliers

Foi identificado um problema crítico de registros aberrantes em **Banana Nanica**, chegando a:

- **R$999,00**  
- Média histórica real: **R$6,57**

Esses valores representavam **4,6% do dataset (1.247 registros)** e eram causados por **erros de digitação durante coleta manual**.

**Metodologia aplicada**

Função implementada:


corrigir_preco_banana()


Critérios:

- Preço > R$20  
- ou Preço por Kg > R$20/kg  

Correção realizada por:

- **imputação temporal**
- **média mensal dos valores válidos**

Isso preserva **sazonalidade natural** enquanto remove erros extremos.

**Resultado**

Dataset com **100% de integridade estatística**.

---

#### Padronização inteligente de marcas

Foi detectado que **23% das marcas possuíam duplicação fonética**.

| Variante original | Marca padronizada |
|---|---|
| Tio Joao | Tio João |
| Tio João | Tio João |
| tiojoao | Tio João |

Pipeline aplicado:

1. Normalização Unicode (NFKD)
2. Conversão para minúsculo
3. Mapeamento heurístico
4. Validação por frequência (>80%)

**Resultado**

- 187 → 142 marcas únicas  
- **redução de 24,1% da complexidade**

---

### 2.2 Validação Final do Dataset

Após o pipeline de limpeza:

- **27.170 registros válidos**
- **0% valores nulos**
- Cálculo de **PPK (Preço / Quantidade)** validado
- **30 meses contínuos de dados**
- Marcas unificadas sem perda analítica

---

## 3. Análise de Volatilidade

### 3.1 Coeficiente de Variação (CV)

Fórmula aplicada:


CV = (desvio padrão / média) × 100


Aplicada aos **27 produtos ao longo de 30 meses**.

### 3.2 Produtos mais voláteis

| Rank | Produto | CV (%) | Preço mínimo | Preço máximo |
|---|---|---|---|---|
| 1 | Café | **78,2** | 6,89 | 45,90 |
| 2 | Manteiga | **65,4** | 3,15 | 41,90 |
| 3 | Óleo | **42,1** | 3,99 | 17,99 |
| 4 | Tomate | **38,7** | 2,95 | 16,99 |
| 5 | Batata | **35,6** | 1,98 | 31,90 |

---

### 3.3 Decomposição sazonal

Metodologia:

- Pivot tables mensais
- Médias móveis (janela de 30 dias)
- Identificação de picos recorrentes

Principais achados:

- Café: aumento médio **+18% em dezembro/janeiro**
- Carne: aumento médio **+12% no final do mês**

**Conclusão**

***68% da volatilidade observada é explicada por padrões sazonais previsíveis.***

---

## 4. Sistema de Categorização Nutricional

Foi desenvolvido um sistema de **6 categorias alimentares**.

| Categoria | Produtos | % custo |
|---|---|---|
| Grãos e Cereais | Arroz, farinha, macarrão | 28% |
| Carnes | Carne, frango, pernil, acém | 31% |
| Laticínios | Leite, manteiga, ovos | 18% |
| Açúcar e condimentos | Açúcar, café, óleo | 15% |
| Pães e massas | Pão | 4% |
| Hortifrúti | Banana, batata, tomate | 7% |

---

## 5. Cálculo do Custo da Cesta

Estudo aplicado ao **estabelecimento MA080**.

### 5.1 Custo original

Cesta padrão com **10 produtos essenciais**.

**Resultado**

- **R$109,11 por dia**
- **R$3.273,30 por mês**

Distribuição:

| Categoria | Custo mensal |
|---|---|
| Carnes | R$1.012,80 |
| Grãos | R$892,50 |
| Laticínios | R$647,40 |
| Condimentos | R$491,10 |

---

## 6. Modelo de Substituição Estratégica

Algoritmo baseado em **4 critérios sequenciais**:

1. **Estabilidade** → CV < 20%  
2. **Inflação acumulada** → <10%  
3. **Consistência de coleta** → >80%  
4. **Equivalência nutricional**

### 6.1 Substituições identificadas

| Categoria | Produto original | CV | Substituição | CV novo |
|---|---|---|---|---|
| Condimentos | Café comum | 78,2% | Café Fort | 12,1% |
| Açúcar | Açúcar genérico | 42,3% | Caravelas | 4,2% |
| Carnes | Acém | 28,4% | Pernil | 15,3% |

---

## 7. Impacto Econômico

| Métrica | Antes | Depois | Melhoria |
|---|---|---|---|
| Custo diário | R$109,11 | R$77,38 | -29,1% |
| Custo mensal | R$3.273,30 | R$2.321,40 | -R$951,90 |
| Volatilidade média | 42,3% | 18,2% | -57% |

**Economia anual estimada**

***R$11.422,80 por estabelecimento***

---

## 8. Reprodutibilidade

### Instalação de dependências


pip install pandas numpy matplotlib seaborn scipy openpyxl


### Execução do projeto


jupyter notebook Analise_de_Dados_Cesta_Basica.ipynb


Pré-requisito:


ICBDadosDesagregados.xlsx


---

## 9. Contribuições Técnicas

Principais soluções desenvolvidas:

- Pipeline de **correção temporal de outliers**
- Sistema de **padronização automática de marcas**
- Framework de **classificação nutricional**
- Modelo de **otimização multi-critério**

Impactos:

- **Economia anual:** R$11.422,80  
- **Redução de volatilidade:** 57%  
- **4,6% dos dados recuperados** que seriam descartados  

---

## Licença

MIT License  

Copyright (c) 2026  
Nicolas Alencar de Oliveira  

---

## Dataset

Fonte:

Observatório da Cesta Básica  
Pontifícia Universidade Católica de Campinas (PUC Campinas)

Uso:

Dataset utilizado apenas para **fins acadêmicos e demonstração técnica**.
