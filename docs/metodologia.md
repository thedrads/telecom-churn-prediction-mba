## Visão Geral

Este documento detalha a metodologia completa aplicada no projeto de **Previsão de Churn em Telecomunicações**, desde a preparação dos dados até a avaliação final dos modelos de Machine Learning.

---

## 1. Preparação e Exploração dos Dados

### 1.1 Carregamento do Dataset
- **Fonte:** Conjunto de dados de churn em telecomunicações
- **Ferramenta:** Orange Data Mining
- **Widget utilizado:** File
- **Formato:** CSV/Excel
- **Registros:** Aproximadamente 3.333 clientes

### 1.2 Análise Exploratória Inicial
- **Widget:** Data Table + Data Info
- **Objetivos:**
  - Verificar tipos de dados (numérico, categórico, texto)
  - Identificar valores ausentes
  - Analisar distribuição da variável target (Churn)
  - Verificar balanceamento das classes

### 1.3 Tratamento de Dados
- **Valores ausentes:** Verificação e tratamento quando necessário
- **Tipos de variáveis:** Conversão apropriada (categórica vs. numérica)
- **Variável target:** "Churn" definida como target no widget Select Columns

---

## 2. Divisão dos Dados (Data Sampling)

### 2.1 Estratégia de Divisão
- **Widget:** Data Sampler
- **Método:** Fixed Proportion
- **Configuração:**
  - **Treino:** 70% dos dados
  - **Teste:** 30% dos dados
- **Estratificação:** Ativada (Stratified)
  - Garante proporção similar de Churn/Não-Churn em ambos os conjuntos
- **Reprodutibilidade:** Seed fixo para garantir resultados reproduzíveis

### 2.2 Justificativa Técnica
A divisão 70/30 é um padrão amplamente aceito que:
- Fornece dados suficientes para treinamento (70%)
- Mantém conjunto de teste representativo (30%)
- Permite validação confiável do modelo final

---

## 3. Seleção e Treinamento de Modelos

### 3.1 Algoritmos Avaliados

#### 3.1.1 Árvore de Decisão (Tree)
- **Tipo:** Modelo baseado em regras
- **Vantagens:** Interpretabilidade alta, visualização clara
- **Parâmetros default:** Profundidade não limitada

#### 3.1.2 Random Forest
- **Tipo:** Ensemble de árvores de decisão
- **Vantagens:** Robusto, reduz overfitting, captura relações complexas
- **Configurações testadas:**
  - **RF (10/3):** 10 árvores, profundidade máxima 3
  - **RF (100/3):** 100 árvores, profundidade máxima 3
  - **RF (100/5):** 100 árvores, profundidade máxima 5

#### 3.1.3 Naive Bayes
- **Tipo:** Modelo probabilístico
- **Vantagens:** Rápido, eficiente com poucos dados
- **Base:** Teorema de Bayes com premissa de independência

### 3.2 Justificativa da Seleção
- **Diversidade de abordagens:** Regras, ensemble, probabilístico
- **Complexidade variada:** De simples (Tree) a complexo (RF)
- **Benchmarking:** Comparação justa entre diferentes paradigmas

---

## 4. Validação Cruzada (Cross-Validation)

### 4.1 Configuração do Test & Score
- **Widget:** Test & Score
- **Método:** Cross-validation (k-fold)
- **Número de folds:** 10
- **Estratificação:** Ativada
- **Dados utilizados:** Conjunto de treino (70%)

### 4.2 Metodologia do k-Fold Estratificado
1. Dataset de treino dividido em 10 subconjuntos (folds)
2. Cada fold mantém proporção similar de Churn/Não-Churn
3. Modelo treinado 10 vezes, cada vez usando:
   - 9 folds para treino
   - 1 fold para validação
4. Métricas calculadas como média das 10 iterações

### 4.3 Métricas Avaliadas
- **AUC (Area Under the Curve):** Capacidade de discriminação
- **CA (Classification Accuracy):** Acurácia geral
- **F1:** Média harmônica entre Precisão e Recall
- **Precision:** Taxa de verdadeiros positivos
- **Recall:** Cobertura dos casos positivos

### 4.4 Critério de Seleção do Melhor Modelo
- **Métrica principal:** AUC (foco em discriminação)
- **Métricas secundárias:** F1, Precision, Recall
- **Modelo vencedor:** Random Forest (100/3)
  - AUC: 0.926
  - F1: 0.835
  - Melhor equilíbrio entre performance e complexidade

---

## 5. Avaliação Final no Conjunto de Teste

### 5.1 Configuração do Teste Final
- **Widget:** Test & Score (segunda instância)
- **Método:** Test on test data
- **Modelo:** Random Forest (100/3) pré-treinado
- **Dados:** Conjunto de teste (30% separado no início)

### 5.2 Objetivo da Avaliação Final
- Simular performance em dados nunca vistos
- Validar generalização do modelo
- Confirmar ausência de overfitting
- Obter estimativa realista de performance em produção

### 5.3 Resultados do Teste Final
- **AUC:** 0.916
- **CA:** 0.839
- **F1:** 0.829
- **Precision:** 0.783
- **Recall:** 0.882

### 5.4 Interpretação dos Resultados
- Performance consistente com cross-validation (AUC 0.926 → 0.916)
- Diferença mínima indica boa generalização
- Recall alto (88.2%) essencial para detecção de churn
- Modelo pronto para implementação

---

## 6. Análise de Importância de Features

### 6.1 Método Utilizado
- **Widget:** Explain Model (Orange3-Explain)
- **Algoritmo:** SHAP (SHapley Additive exPlanations)
- **Modelo base:** Random Forest (100/3)

### 6.2 Interpretação SHAP
- Valores SHAP indicam contribuição de cada feature
- Features com maior impacto na predição de churn
- Visualização via gráfico de barras

### 6.3 Top 5 Features Mais Importantes
1. **Total day charge**
2. **Customer service calls**
3. **Total intl calls**
4. **International plan**
5. **Voice mail plan**

---

## 7. Validação e Boas Práticas Aplicadas

### ✅ **Reprodutibilidade**
- Seed fixo no Data Sampler
- Workflow salvo (.ows) versionado no GitHub

### ✅ **Prevenção de Data Leakage**
- Divisão treino/teste ANTES de qualquer processamento
- Conjunto de teste isolado até avaliação final
- Validação cruzada apenas no conjunto de treino

### ✅ **Validação Rigorosa**
- Cross-validation estratificado (10-fold)
- Teste final em dados completamente independentes
- Múltiplas métricas avaliadas

### ✅ **Comparação Justa**
- Todos os modelos treinados com mesma divisão de dados
- Mesma metodologia de avaliação
- Mesmas métricas calculadas

### ✅ **Interpretabilidade**
- Análise SHAP para explicação do modelo
- Feature importance documentada
- Workflow visual (Orange) facilita compreensão

---

## 8. Limitações e Trabalhos Futuros

### Limitações Conhecidas
- Dataset relativamente pequeno (~3.3k registros)
- Número limitado de features (21 variáveis)
- Ausência de validação temporal (dados cross-sectional)

### Próximos Passos
1. **Otimização de hiperparâmetros:** Grid search para RF
2. **Feature engineering:** Criar variáveis derivadas
3. **Ensemble avançado:** Stacking/Blending de modelos
4. **Deploy:** Containerização e API REST
5. **Monitoramento:** Tracking de performance em produção

---

## Referências Técnicas

- **Orange Data Mining Documentation:** [https://orangedatamining.com/docs/](https://orangedatamining.com/docs/)
- **SHAP:** Lundberg, S. M., & Lee, S. I. (2017). A unified approach to interpreting model predictions. *NIPS*.
- **Random Forest:** Breiman, L. (2001). Random forests. *Machine learning*, 45(1), 5-32.
- **Cross-Validation:** Kohavi, R. (1995). A study of cross-validation and bootstrap for accuracy estimation and model selection. *IJCAI*.

---

## Conclusão Metodológica

A metodologia aplicada segue rigorosamente as melhores práticas de Machine Learning:
- Divisão apropriada dos dados
- Validação robusta (cross-validation + teste final)
- Comparação justa entre múltiplos modelos
- Interpretabilidade via SHAP
- Reprodutibilidade garantida

O Random Forest (100/3) demonstrou ser a escolha ideal, equilibrando performance (AUC 0.916), interpretabilidade e eficiência computacional.

---

**Autor:** Fábio Andrade  
**Projeto:** MBA em Inteligência Artificial e Análise de Dados - SENAC-RJ  
**Data:** Fevereiro 2025  
**Licença:** MIT