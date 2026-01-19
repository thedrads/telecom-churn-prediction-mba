# 📊 Previsão de Churn em Telecomunicações - Projeto Acadêmico MBA

[![Orange Data Mining](https://img.shields.io/badge/Orange-Data%20Mining-orange)](https://orangedatamining.com/)
[![Machine Learning](https://img.shields.io/badge/ML-Random%20Forest-green)](https://github.com/thedrads/telecom-churn-prediction-mba)
[![Academic Project](https://img.shields.io/badge/Project-MBA%20SENAC--RJ-blue)](https://github.com/thedrads/telecom-churn-prediction-mba)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> **Projeto acadêmico de Machine Learning** desenvolvido durante o MBA em Inteligência Artificial e Análise de Dados aplicados a Negócios (SENAC-RJ). Este trabalho demonstra a aplicação prática de técnicas de ML para resolver um problema real de negócio: **predição de cancelamento de clientes (churn)** em empresas de telecomunicações.

---

## 🎯 Sobre o Projeto

Este é um projeto de **aprendizado prático** que implementa um pipeline completo de Machine Learning usando **Orange Data Mining**, uma ferramenta visual para prototipagem rápida. O objetivo foi desenvolver um modelo capaz de identificar clientes com alto risco de cancelamento, permitindo ações preventivas de retenção.

### 📚 Contexto Acadêmico

- **Disciplina:** Fundamentos de Machine Learning
- **Instituição:** SENAC-RJ (MBA em IA & Análise de Dados)
- **Professor:** Jorge Junio Moreira Antunes
- **Data:** Janeiro/2026
- **Aluno:** Fábio Ferreira de Andrade

### 🎓 Objetivo de Aprendizado

Este projeto foi desenvolvido como parte da minha jornada de **transição para a área de tecnologia**, após 20 anos de experiência em gestão de negócios. O trabalho demonstra:

- Compreensão de conceitos fundamentais de Machine Learning
- Capacidade de executar um pipeline ML completo (preparação, modelagem, validação, deploy)
- Aplicação prática de validação cruzada e técnicas de prevenção de overfitting
- Interpretação de modelos e extração de insights de negócio
- Comunicação técnica através de documentação estruturada

---

## 🔍 Problema de Negócio

**Churn (cancelamento de clientes)** é um dos maiores desafios em telecomunicações. Estudos mostram que:

- 📉 Adquirir um novo cliente custa **5-25x mais** do que reter um existente
- 💰 Empresas de telecom perdem **US$ 65 bilhões/ano** devido ao churn
- 🎯 Modelos preditivos podem **reduzir churn em até 15%** com ações preventivas

Este projeto simula um cenário real onde uma operadora contrata um cientista de dados para desenvolver um sistema de predição de churn.

---

## 🛠️ Tecnologias Utilizadas

### Ferramenta Principal
- **[Orange Data Mining 3.36](https://orangedatamining.com/)** - Plataforma visual para Machine Learning (no-code)
  - Extensão: Orange3-Explain (para interpretabilidade)

### Algoritmos Testados
- **Random Forest** (escolhido como modelo final)
- Gradient Boosting Machine (GBM)
- Logistic Regression (Ridge e Lasso)
- Neural Networks

### Ambiente
- **Sistema Operacional:** Windows 11
- **Dependências:** Microsoft Visual C++ Redistributable (necessário para extensão Explain)

---

## 📊 Metodologia

O projeto seguiu um pipeline estruturado de Machine Learning:

### 1️⃣ **Análise Exploratória e Hipóteses**
- Levantamento de hipóteses sobre importância das variáveis
- Atribuição de notas de relevância (0-100) para cada feature
- Análise conceitual baseada em lógica de negócio

### 2️⃣ **Preparação dos Dados**
- Base de dados: `telecom_churn_complete.xlsx` (fornecida pelo professor)
- **10 variáveis preditoras:** account_age_weeks, contract_renewal, data_plan, data_usage_gb, customer_service_calls, day_minutes, day_calls, monthly_charge, overage_fee, roam_minutes
- **Target:** churn (binário: sim/não)
- Split: 80% treino / 20% teste (hold-out)

### 3️⃣ **Seleção de Modelos**
- Teste de **16+ configurações** de modelos
- Validação cruzada estratificada (k-fold, k=10)
- Comparação baseada em múltiplas métricas (AUC, Accuracy, F1, MCC)

### 4️⃣ **Validação Final**
- Teste em conjunto hold-out (20% não visto)
- Análise de overfitting
- Avaliação de generalização

### 5️⃣ **Interpretabilidade**
- Permutation Feature Importance (baseado em AUC)
- Comparação entre importância esperada vs. real
- Validação de hipóteses iniciais

### 6️⃣ **Deploy Simulado**
- Previsão em novo cliente (dados fornecidos)
- Recomendações de negócio
- Análise de casos limítrofes

---

## 🏆 Resultados Principais

### 🥇 Modelo Vencedor: Random Forest

**Configuração:**
- 300 árvores
- 3 variáveis por divisão (max_features)
- Bootstrap ativado

### 📈 Performance

| Métrica | Validação Cruzada (10-fold) | Teste (20% hold-out) | Variação |
|---------|----------------------------|----------------------|----------|
| **AUC** | 0.905 | 0.880 | -2.8% |
| **Accuracy** | 93.9% | 92.3% | -1.7% |
| **F1-Score** | 0.936 | 0.919 | -1.8% |
| **Precision** | 0.937 | 0.919 | -1.9% |
| **Recall** | 0.939 | 0.923 | -1.7% |
| **MCC** | 0.737 | 0.667 | -9.5% |

### ✅ Análise de Overfitting

A queda de performance entre validação cruzada e teste foi **inferior a 3% no AUC**, indicando:
- ✅ Boa capacidade de generalização
- ✅ Ausência de overfitting significativo
- ✅ Modelo adequado para produção

### 🔑 Top 5 Variáveis Mais Importantes

| Ranking | Variável | Nota Esperada | Alinhamento |
|---------|----------|---------------|-------------|
| 🥇 1º | monthly_charge | 95 | ✅ Confirmado |
| 🥈 2º | customer_service_calls | 90 | ✅ Confirmado |
| 🥉 3º | contract_renewal | 95 | ✅ Confirmado |
| 4º | day_minutes | 80 | ✅ Confirmado |
| 5º | roam_minutes | 60 | ✅ Confirmado |

**Insight:** A análise prévia foi extremamente precisa, com **100% de alinhamento** entre expectativa e realidade nas 3 principais variáveis. Isso demonstra que a compreensão conceitual do problema foi sólida.

---

## 💼 Caso de Uso Real: Previsão para Novo Cliente

**Perfil do Cliente:**
- Tempo de conta: 128 semanas
- Renovação de contrato: Sim
- Plano de dados: Não
- Chamadas ao suporte: 4
- Mensalidade: $45.00

**Resultado da Previsão:**
- ⚠️ **Classe Prevista:** NÃO CHURN (cliente deve permanecer)
- 📊 **Probabilidade de permanência:** 53%
- 📊 **Probabilidade de cancelamento:** 47%

**Interpretação:**
Este é um **caso limítrofe** (diferença de apenas 6 pontos percentuais). O cliente está na fronteira de decisão do modelo e representa **risco moderado-alto**, merecendo atenção especial da equipe de retenção.

**Recomendações de Negócio:**
1. 📞 Contato proativo do time de retenção
2. 🎁 Ofertas personalizadas ou revisão de plano
3. 💰 Redução de cobranças extras ou ajustes contratuais

---

## 📁 Estrutura do Repositório

```
telecom-churn-prediction-mba/
├── README.md                          # Documentação principal (este arquivo)
├── LICENSE                            # Licença MIT
├── data/                              # Dados do projeto
│   ├── cliente_novo.xlsx             # Novo cliente para previsão
│   └── hipoteses_iniciais.xlsx       # Análise prévia de variáveis
├── models/                            # Modelos treinados
│   └── modelo_final_RF.pkcls         # Random Forest (300 trees)
├── workflow/                          # Arquivos Orange Data Mining
│   ├── workflow_completo.ows         # Pipeline ML completo
│   └── workflow_diagram.png          # Diagrama visual do workflow
├── docs/                              # Documentação detalhada
│   ├── relatorio_completo.pdf        # Relatório acadêmico oficial
│   └── metodologia.md                # Detalhamento da metodologia
├── results/                           # Resultados e análises
│   ├── feature_importance.png        # Gráfico de importância
│   ├── model_comparison.png          # Comparação de modelos
│   └── predictions_sample.png        # Exemplo de previsões
└── images/                            # Imagens para documentação
    ├── workflow_overview.png
    ├── cross_validation_results.png
    └── test_predictions.png
```

---

## 🚀 Como Reproduzir

### Pré-requisitos

1. **Instalar Orange Data Mining:**
   ```bash
   # Download: https://orangedatamining.com/download/
   # Versão recomendada: 3.36+
   ```

2. **Instalar dependências do Windows (se necessário):**
   - Microsoft Visual C++ Redistributable
   - Necessário para extensão Orange3-Explain

3. **Instalar extensão Explain:**
   - Orange → Options → Add-ons → Procurar "Explain" → Install

### Passo a Passo

1. **Clone este repositório:**
   ```bash
   git clone https://github.com/thedrads/telecom-churn-prediction-mba.git
   cd telecom-churn-prediction-mba
   ```

2. **Abra o workflow no Orange:**
   ```
   Orange Data Mining → File → Open → Selecionar "workflow/workflow_completo.ows"
   ```

3. **Execute o pipeline:**
   - O workflow está pré-configurado e pronto para rodar
   - Todos os widgets estão conectados corretamente
   - Os dados já estão incluídos

4. **Explore os resultados:**
   - Visualize as métricas no widget "Test & Score"
   - Analise a importância das variáveis em "Feature Importance"
   - Teste previsões no widget "Predictions"

---

## 🎓 Aprendizados e Reflexões

### 🔧 Desafios Técnicos Enfrentados

**1. Instalação da Extensão Explain**
- **Problema:** Erro ao instalar Orange3-Explain devido a dependências do Python
- **Mensagem:** `Command failed: python -m pip install --upgrade exited with non zero status`
- **Causa Raiz:** Falta do Microsoft Visual C++ Redistributable no Windows
- **Solução:** Download e instalação do C++ Redistributable + reinicialização do sistema
- **Aprendizado:** Importância de compreender dependências de sistema para ferramentas Python

**2. Escolha do Modelo Final**
- **Dilema:** RF (100 trees) tinha F1 e MCC ligeiramente superiores ao RF (300 trees)
- **Decisão:** Escolher RF (300 trees) pela maior **estabilidade e robustez** em produção
- **Aprendizado:** Nem sempre o modelo com melhores métricas é o melhor para deploy real

### 💡 Principais Takeaways

1. **Validação Cruzada é Essencial:** Sem k-fold, não teria detectado a consistência do modelo
2. **Interpretabilidade Importa:** Permutation Feature Importance validou hipóteses iniciais
3. **Casos Limítrofes Existem:** Cliente com 53% vs 47% mostra que ML não é magia - é probabilidade
4. **Documentação é Aprendizado:** Escrever este README solidificou meu entendimento do projeto

### 🎯 Próximos Passos

Como este é um projeto de aprendizado contínuo, planejo:

- [ ] Reimplementar o modelo em Python (scikit-learn) para comparação
- [ ] Experimentar técnicas de balanceamento de classes (SMOTE)
- [ ] Implementar um dashboard interativo (Streamlit)
- [ ] Aplicar feature engineering mais avançado
- [ ] Testar outros algoritmos (XGBoost, LightGBM)

---

## 📚 Recursos e Referências

### Documentação Orange Data Mining
- [Orange Documentation](https://orange-data-mining-library.readthedocs.io/)
- [Orange3-Explain Extension](https://github.com/biolab/orange3-explain)

### Artigos sobre Churn Prediction
- Hadden, J., et al. (2007). "Computer assisted customer churn management: State-of-the-art and future trends"
- Coussement, K., & Van den Poel, D. (2008). "Churn prediction in subscription services"

### Material de Estudo ML
- Hastie, T., Tibshirani, R., & Friedman, J. (2009). "The Elements of Statistical Learning"
- Müller, A. C., & Guido, S. (2016). "Introduction to Machine Learning with Python"

---

## ⚖️ Declaração de Uso de IA

Este projeto foi desenvolvido com apoio de **ferramentas de Inteligência Artificial generativa**, utilizadas como **assistente técnico** para:

- 📝 Organização de ideias e estruturação de documentação
- 🔍 Revisão técnica de conceitos de Machine Learning
- 💡 Apoio conceitual em interpretação de métricas
- 📊 Formatação e apresentação de resultados

### Responsabilidade

Todo o **conteúdo final, análises, insights, decisões técnicas e conclusões** foram integralmente **revisados, validados e aprovados** pelo autor. A inteligência artificial foi utilizada como ferramenta de apoio ao desenvolvimento, **complementando** o trabalho intelectual do autor, **não o substituindo**.

### Referências sobre Uso Ético de IA em Contextos Acadêmicos

- [Princeton University - Disclosing the Use of AI](https://writing.princeton.edu/owp/ai-policies)
- [Arizona State University - Acknowledging AI Usage](https://provost.asu.edu/ai-guidance)
- [AID Framework - AI Disclosure](https://www.aidisclosure.org/)

O uso de IA neste projeto seguiu princípios éticos e educacionais, priorizando transparência e aprendizado genuíno.

---

## 🤝 Sobre o Autor

**Fábio Ferreira de Andrade**

Profissional em **transição para tecnologia** com 20 anos de experiência em gestão de negócios (área veterinária). Atualmente cursando **MBA em Inteligência Artificial e Análise de Dados** aplicados a Negócios no SENAC-RJ, com conclusão prevista para outubro/2026.

**Motivação:** Combinar experiência em negócios com novas habilidades técnicas em Data Science e Machine Learning para resolver problemas reais com dados.

### 📫 Contato

- **GitHub:** [@thedrads](https://github.com/thedrads)
- **LinkedIn:** [Fábio Ferreira de Andrade](https://linkedin.com/in/fabio-andrade) *(ajuste o link)*
- **Portfolio:** [thedrads.github.io](https://thedrads.github.io)

### 🎯 Interesses Profissionais

- 📊 Data Science & Machine Learning
- 🤖 Inteligência Artificial aplicada a Negócios
- 📈 Analytics & Business Intelligence
- ☁️ Cloud Computing (AWS)

---

## 📄 Licença

Este projeto está licenciado sob a **MIT License** - veja o arquivo [LICENSE](LICENSE) para detalhes.

```
MIT License

Copyright (c) 2026 Fábio Ferreira de Andrade

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

---

## 🏷️ Tags

`machine-learning` `churn-prediction` `random-forest` `orange-data-mining` `data-science` `mba-project` `academic-project` `telecommunications` `customer-retention` `predictive-analytics` `classification` `cross-validation` `feature-importance` `model-interpretability` `business-analytics` `senac-rj` `portfolio-project`

---

## ⭐ Agradecimentos

- **Prof. Jorge Junio Moreira Antunes** - Pela orientação na disciplina de Fundamentos de Machine Learning
- **SENAC-RJ** - Pela estrutura e qualidade do MBA
- **Comunidade Orange Data Mining** - Pela ferramenta open-source excepcional
- **Colegas de turma** - Pelas discussões e troca de conhecimento

---

<div align="center">

**Se este projeto foi útil para você, considere dar uma ⭐!**

*Desenvolvido com 💙 e muito aprendizado por [Fábio Andrade](https://github.com/thedrads)*

</div>
