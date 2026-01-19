# 📖 Metodologia Detalhada - Projeto Churn Telecom

## Sumário

1. [Visão Geral](#visão-geral)
2. [Preparação dos Dados](#preparação-dos-dados)
3. [Análise Exploratória](#análise-exploratória)
4. [Seleção de Modelos](#seleção-de-modelos)
5. [Validação Final](#validação-final)
6. [Interpretabilidade](#interpretabilidade)
7. [Deploy Simulado](#deploy-simulado)

---

## Visão Geral

Este documento detalha a metodologia completa utilizada no projeto de predição de churn, seguindo o roteiro acadêmico proposto na disciplina Fundamentos de Machine Learning.

### Ferramentas

- **Orange Data Mining 3.36+**
- **Extensão:** Orange3-Explain
- **Sistema:** Windows 11

### Pipeline Geral

```
Dados Brutos → Preparação → Análise → Modelagem → Validação → Interpretação → Deploy
```

---

## Preparação dos Dados

### 1. Carregamento

**Widget utilizado:** File

**Arquivo:** `telecom_churn_complete.xlsx` (fornecido pelo professor)

**Estrutura:**
- Linhas: Clientes da operadora de telecom
- Colunas: 11 (10 features + 1 target)

### 2. Definição da Target

**Widget utilizado:** Select Columns

**Configuração:**
- Target: `churn` (binário: yes/no)
- Features: Todas as demais variáveis

### 3. Verificação de Tipos

Orange detecta automaticamente os tipos de dados:
- Numéricos: account_age_weeks, data_usage_gb, customer_service_calls, day_minutes, day_calls, monthly_charge, overage_fee, roam_minutes
- Categóricos: contract_renewal, data_plan
- Target: churn (categórico binário)

### 4. Split Treino/Teste

**Widget utilizado:** Data Sampler

**Configuração:**
- **Treino:** 80% (utilizado para validação cruzada)
- **Teste:** 20% (hold-out set, não tocado até validação final)
- **Método:** Random sampling
- **Stratified:** Ativado (mantém proporção de classes)
- **Replicable:** Seed fixada para reprodutibilidade

**Justificativa do split 80/20:**
- Padrão da indústria para datasets de tamanho médio
- Balança quantidade de dados para treino vs. confiabilidade do teste
- Permite validação cruzada robusta no conjunto de treino

---

## Análise Exploratória

### Hipóteses Iniciais

Antes da modelagem, foram levantadas hipóteses sobre a importância de cada variável para prever churn, atribuindo notas de 0 (irrelevante) a 100 (muito importante).

**Critérios para atribuição de notas:**
1. Lógica de negócio (experiência em gestão)
2. Literatura sobre churn em telecomunicações
3. Intuição sobre comportamento do consumidor

**Resultado:** Documentado em `data/hipoteses_iniciais.xlsx`

### Objetivo da Análise Prévia

- Exercitar pensamento crítico antes de ver os dados
- Validar posteriormente se as hipóteses estavam corretas
- Demonstrar compreensão do domínio do problema

---

## Seleção de Modelos

### Validação Cruzada

**Widget utilizado:** Test & Score

**Configuração:**
- **Método:** Cross-validation (k-fold)
- **K:** 10 folds
- **Stratified:** Ativado
- **Shuffle:** Ativado

**Por que k=10?**
- Balança viés vs. variância
- Padrão amplamente aceito na literatura
- Usa 90% dos dados para treino em cada fold

### Algoritmos Testados

#### 1. Logistic Regression (4 modelos)

**Widget:** Logistic Regression

**Variações testadas:**
- **Lasso (C=0.1):** Regularização forte
- **Lasso (C=1.0):** Regularização moderada
- **Ridge (C=0.1):** Regularização forte
- **Ridge (C=1.0):** Regularização moderada

**Justificativa:**
- Baseline simples e interpretável
- Testou diferentes níveis de regularização
- Comparação Lasso (L1) vs Ridge (L2)

#### 2. Random Forest (4 modelos)

**Widget:** Random Forest

**Variações testadas:**
- **RF (300 trees, max_features=4)**
- **RF (300 trees, max_features=3)** ← **Modelo vencedor**
- **RF (100 trees, max_features=4)**
- **RF (100 trees, max_features=3)**

**Hiperparâmetros fixos:**
- min_samples_split: 2 (padrão)
- min_samples_leaf: 1 (padrão)
- bootstrap: True

**Justificativa:**
- Variou número de árvores (100 vs 300)
- Variou max_features (~1/3 das features, conforme recomendado)
- Mais árvores = maior estabilidade (mas computacionalmente mais caro)

#### 3. Gradient Boosting Machine (4 modelos)

**Widget:** Gradient Boosting

**Variações testadas:**
- **GBM (50 trees)**
- **GBM (100 trees)**
- **GBM (200 trees)**
- **GBM (300 trees)**

**Hiperparâmetros fixos:**
- learning_rate: 0.1 (padrão)
- max_depth: 3 (padrão)

**Justificativa:**
- Fixou outros parâmetros para isolar efeito do número de árvores
- GBM geralmente requer menos árvores que RF

#### 4. Neural Networks (4 modelos)

**Widget:** Neural Network

**Variações testadas:**
- **NN (50 neurons, 200 iterations)**
- **NN (50 neurons, 400 iterations)**
- **NN (100 neurons, 200 iterations)**
- **NN (100 neurons, 400 iterations)**

**Hiperparâmetros fixos:**
- Hidden layers: 1 camada
- Activation: ReLU
- Solver: Adam

**Justificativa:**
- Variou complexidade (neurônios) e tempo de treino (iterações)
- Manteve arquitetura simples (1 camada) para facilitar interpretação

### Métricas de Avaliação

**Métricas utilizadas:**
- **AUC-ROC:** Métrica principal (robusta a desbalanceamento)
- **Accuracy:** Performance geral
- **F1-Score:** Balança Precision e Recall
- **Precision:** Quantos churns previstos eram realmente churn
- **Recall:** Quantos churns reais foram identificados
- **MCC:** Matthews Correlation Coefficient (leva em conta todas as células da matriz de confusão)

**Por que AUC como métrica principal?**
- Invariante a threshold de classificação
- Robusta a desbalanceamento de classes
- Amplamente utilizada em problemas de churn

### Critérios de Seleção

**Modelo escolhido:** Random Forest (300 trees, max_features=3)

**Critérios:**
1. **AUC:** 0.905 (empatado com GBM-100 no topo)
2. **MCC:** 0.737 (superior ao GBM-100 que tinha 0.723)
3. **Estabilidade:** 300 árvores oferecem mais robustez que 100
4. **Interpretabilidade:** RF é mais fácil de explicar que GBM
5. **Adequação para produção:** Menor risco de overfitting

**Trade-off reconhecido:**
- RF (100 trees, 3 feats) tinha F1 e MCC ligeiramente superiores
- Decisão priorizou estabilidade para ambiente de produção

---

## Validação Final

### Teste em Hold-out Set

**Widget utilizado:** Predictions

**Procedimento:**
1. Treinar modelo vencedor com 100% do conjunto de treino (80% dos dados originais)
2. Aplicar modelo no conjunto de teste (20% nunca visto)
3. Avaliar métricas

### Análise de Overfitting

**Comparação:**

| Métrica | Cross-Val | Teste | Variação |
|---------|-----------|-------|----------|
| AUC | 0.905 | 0.880 | -2.8% |
| Accuracy | 93.9% | 92.3% | -1.7% |
| F1-Score | 0.936 | 0.919 | -1.8% |
| MCC | 0.737 | 0.667 | -9.5% |

**Interpretação:**
- Queda de AUC < 3% é considerada aceitável
- Todas as métricas permaneceram acima de 90% (exceto MCC)
- **Conclusão:** Modelo generaliza bem, sem overfitting significativo

---

## Interpretabilidade

### Permutation Feature Importance

**Widget utilizado:** Feature Importance (extensão Explain)

**Método:**
- Permutation Importance baseado em AUC
- Permuta aleatoriamente cada feature e mede queda no AUC
- Quanto maior a queda, mais importante a feature

**Configuração:**
- Score: AUC
- Permutations: 20 (padrão)
- Top features: 10 (todas as features)

### Comparação: Expectativa vs. Realidade

**Resultado:**
- **100% de alinhamento** nas 3 principais variáveis
- Top 3 esperado: monthly_charge, customer_service_calls, contract_renewal
- Top 3 real: monthly_charge, customer_service_calls, contract_renewal

**Insights:**
1. A análise conceitual estava correta
2. Preço (monthly_charge) é o fator mais determinante
3. Insatisfação (customer_service_calls) é forte preditor
4. Compromisso (contract_renewal) confirma intenção de permanência

---

## Deploy Simulado

### Previsão para Novo Cliente

**Dados de entrada:**
```python
{
    'account_age_weeks': 128,
    'contract_renewal': 1 (yes),
    'data_plan': 0 (no),
    'data_usage_gb': 0.0,
    'customer_service_calls': 4,
    'day_minutes': 265.1,
    'day_calls': 110,
    'monthly_charge': 45.0,
    'overage_fee': 10.5,
    'roam_minutes': 14.2
}
```

**Resultado:**
- Classe prevista: **NÃO CHURN**
- Probabilidade de permanência: **53%**
- Probabilidade de churn: **47%**

### Análise de Caso Limítrofe

Este cliente está na **fronteira de decisão** do modelo:
- Diferença de apenas 6 pontos percentuais
- Representa incerteza do modelo
- Requer atenção especial em produção

**Recomendação de negócio:**
- Monitoramento próximo
- Ação preventiva recomendada
- Incluir em programa de retenção

---

## Considerações Finais

### Pontos Fortes da Metodologia

1. ✅ Validação cruzada estratificada (k=10)
2. ✅ Hold-out set preservado até o fim
3. ✅ Múltiplos algoritmos testados (16+ configurações)
4. ✅ Hiperparâmetros variados sistematicamente
5. ✅ Interpretabilidade com Permutation Importance
6. ✅ Análise de casos limítrofes

### Limitações Reconhecidas

1. ⚠️ Ferramenta no-code (limitações de customização)
2. ⚠️ Dataset acadêmico (pode não refletir complexidade real)
3. ⚠️ Não testou técnicas de balanceamento (SMOTE, etc.)
4. ⚠️ Não realizou feature engineering avançado
5. ⚠️ Não avaliou impacto de diferentes thresholds

### Próximos Passos para Aprofundamento

- [ ] Reimplementar em Python (scikit-learn)
- [ ] Experimentar feature engineering
- [ ] Testar técnicas de balanceamento de classes
- [ ] Análise de curva Precision-Recall
- [ ] Otimização de threshold para negócio

---

## Referências Metodológicas

1. **Cross-Validation:**
   - Kohavi, R. (1995). "A study of cross-validation and bootstrap for accuracy estimation and model selection"

2. **Random Forest:**
   - Breiman, L. (2001). "Random Forests". Machine Learning, 45(1), 5-32.

3. **Permutation Importance:**
   - Breiman, L. (2001). "Random forests". Machine Learning, 45(1), 5-32.

4. **Model Evaluation:**
   - Davis, J., & Goadrich, M. (2006). "The relationship between Precision-Recall and ROC curves"

5. **Churn Prediction:**
   - Hadden, J., et al. (2007). "Computer assisted customer churn management: State-of-the-art and future trends"

---

*Documentação elaborada como parte do projeto acadêmico de Fundamentos de Machine Learning - MBA SENAC-RJ (2026)*
