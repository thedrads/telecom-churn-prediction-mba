# 📊 Previsão de Churn em Telecomunicações
### 🎓 Projeto acadêmico | MBA em IA & Análise de Dados – SENAC-RJ

---

[![Orange Data Mining](https://img.shields.io/badge/Orange-Data%20Mining-E9782D?style=for-the-badge)](https://orangedatamining.com/)
[![Machine Learning](https://img.shields.io/badge/ML-Random%20Forest-228B22?style=for-the-badge)](https://github.com/thedrads/telecom-churn-prediction-mba)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge)]()

> **Projeto acadêmico de Machine Learning** desenvolvido durante o MBA em Inteligência Artificial e Análise de Dados aplicados a Negócios (SENAC-RJ). Este trabalho demonstra a aplicação prática de técnicas de ML para resolver um problema real de negócio: **predição de cancelamento de clientes (churn)** em empresas de telecomunicações.

---

## 📑 Sumário

- [Sobre o Projeto](#-sobre-o-projeto)
- [Minha Jornada](#-minha-jornada)
- [Problema de Negócio](#-problema-de-negócio)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Metodologia](#-metodologia)
- [Resultados Principais](#-resultados-principais)
- [Caso de Simulação](#-caso-de-simulação-previsão-para-novo-cliente)
- [Estrutura do Repositório](#-estrutura-do-repositório)
- [Como Reproduzir](#-como-reproduzir)
- [Aprendizados e Reflexões](#-aprendizados-e-reflexões)
- [Recursos e Referências](#-recursos-e-referências)
- [Declaração de Uso de IA](#-declaração-de-uso-de-ia)
- [Autor](#-autor)
- [Licença](#-licença)

---

## 🎯 Sobre o Projeto

Este é um projeto de **aprendizado prático** que implementa um pipeline completo de Machine Learning usando **Orange Data Mining**, uma ferramenta visual para prototipagem rápida. O objetivo foi desenvolver um modelo capaz de identificar clientes com alto risco de cancelamento, permitindo ações preventivas de retenção.

### 📚 Contexto Acadêmico

| Informação | Detalhe |
|------------|---------|
| **Disciplina** | Fundamentos de Machine Learning |
| **Instituição** | SENAC-RJ |
| **Curso** | MBA em IA & Análise de Dados aplicados a Negócios |
| **Professor** | Jorge Antunes |
| **Data** | Janeiro/2026 |

---

## 🚀 Minha Jornada

Sou gestor financeiro com 20 anos de experiência em gestão empresarial, atualmente em transição de carreira para Data Science e Cloud Computing. Este projeto faz parte da minha formação no **MBA em IA & Análise de Dados (SENAC-RJ)** e complementa meus estudos no programa **Oracle Next Education (ONE)**.

### 🎓 Objetivo de Aprendizado

Este projeto demonstra:

- Compreensão de conceitos fundamentais de Machine Learning
- Capacidade de executar um pipeline ML completo (preparação, modelagem, validação, deploy)
- Aplicação prática de validação cruzada e técnicas de prevenção de overfitting
- Interpretação de modelos e extração de insights de negócio
- Comunicação técnica através de documentação estruturada

Como iniciante em programação e ML, busco aprender continuamente e trocar conhecimento com a comunidade. Este repositório representa um passo concreto na construção do meu portfólio técnico, com transparência sobre meu nível atual e compromisso com a evolução constante.

---

## 🔍 Problema de Negócio

**Churn (cancelamento de clientes)** é um dos maiores desafios em telecomunicações. Estudos mostram que:

- 📉 Adquirir um novo cliente custa **5-25x mais** do que reter um existente
- 💰 Empresas de telecom perdem **US$ 65 bilhões/ano** devido ao churn
- 🎯 Modelos preditivos podem **reduzir churn em até 15%** com ações preventivas

Este projeto simula um cenário real onde uma operadora contrata um cientista de dados para desenvolver um sistema de predição de churn.

### Perspectiva de Negócio

Com base na minha experiência em gestão, destaco que o churn não representa apenas perda de receita recorrente, mas também **desperdício do CAC (Customer Acquisition Cost)** investido. Em telecomunicações, recuperar um cliente perdido custa significativamente mais do que prevenir o cancelamento, o que justifica o investimento em modelos preditivos como ferramenta estratégica de retenção.

---

## 🧰 Tecnologias Utilizadas

### Ferramenta Principal

| Tecnologia | Versão | Uso |
|------------|--------|-----|
| [Orange Data Mining](https://orangedatamining.com/) | 3.40+ | Plataforma visual para ML (no-code) |
| Orange3-Explain | - | Extensão para interpretabilidade |

### Algoritmos Testados

| Algoritmo | Status |
|-----------|--------|
| **Random Forest** | ✅ Modelo final (300 árvores) |
| Gradient Boosting Machine (GBM) | Testado |
| Logistic Regression (Ridge/Lasso) | Testado |
| Neural Networks | Testado |

### Ambiente

- **Sistema Operacional:** Windows 10
- **Dependências:** Microsoft Visual C++ Redistributable (necessário para extensão Explain)

---

## 📊 Metodologia

O projeto seguiu um pipeline estruturado de Machine Learning:

### 1️⃣ Análise Exploratória e Hipóteses

- Levantamento de hipóteses sobre importância das variáveis
- Atribuição de notas de relevância (0-100) para cada feature
- Análise conceitual baseada em lógica de negócio

### 2️⃣ Preparação dos Dados

- **Base de dados:** `telecom_churn_complete.xlsx` (fornecida pelo professor)
- **10 variáveis preditoras:** account_age_weeks, contract_renewal, data_plan, data_usage_gb, customer_service_calls, day_minutes, day_calls, monthly_charge, overage_fee, roam_minutes
- **Target:** churn (binário: sim/não)
- **Split:** 80% treino / 20% teste (hold-out)

### 3️⃣ Seleção de Modelos

- Teste de **16+ configurações** de modelos
- Validação cruzada estratificada (k-fold, k=10)
- Comparação baseada em múltiplas métricas (AUC, Accuracy, F1, MCC)

### 4️⃣ Validação Final

- Teste em conjunto hold-out (20% não visto)
- Análise de overfitting
- Avaliação de generalização

### 5️⃣ Interpretabilidade

- Permutation Feature Importance (baseado em AUC)
- Comparação entre importância esperada vs. real
- Validação de hipóteses iniciais

### 6️⃣ Deploy Simulado

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

## 💼 Caso de Simulação: Previsão para Novo Cliente

**Perfil do Cliente:**

| Atributo | Valor |
|----------|-------|
| Tempo de conta | 128 semanas |
| Renovação de contrato | Sim |
| Plano de dados | Não |
| Chamadas ao suporte | 4 |
| Mensalidade | $45.00 |

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
├── README.md                          # Documentação principal
├── LICENSE                            # Licença MIT
├── data/                              # Dados do projeto
│   ├── cliente_novo.xlsx              # Novo cliente para previsão
│   └── hipoteses_iniciais.xlsx        # Análise prévia de variáveis
├── models/                            # Modelos treinados
│   └── modelo_final_RF.pkcls          # Random Forest (300 trees)
├── workflow/                          # Arquivos Orange Data Mining
│   ├── workflow_completo.ows          # Pipeline ML completo
│   └── workflow_diagram.png           # Diagrama visual do workflow
├── docs/                              # Documentação detalhada
│   ├── relatorio_completo.pdf         # Relatório acadêmico oficial
│   └── metodologia.md                 # Detalhamento da metodologia
├── results/                           # Resultados e análises
│   ├── feature_importance.png         # Gráfico de importância
│   ├── model_comparison.png           # Comparação de modelos
│   └── predictions_sample.png         # Exemplo de previsões
└── images/                            # Imagens para documentação
    ├── workflow_overview.png
    ├── cross_validation_results.png
    └── test_predictions.png
```

---

## 🚀 Como Reproduzir

### Pré-requisitos

1. **Instalar Orange Data Mining:**
   - Download: [https://orangedatamining.com/download/](https://orangedatamining.com/download/)
   - Versão recomendada: 3.40+

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
3. **Casos Limítrofes Existem:** Cliente com 53% vs 47% mostra que ML não é magia — é probabilidade
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

### Artigos Científicos sobre Churn Prediction

- Hadden, J., Tiwari, A., Roy, R., & Ruta, D. (2007). [Computer assisted customer churn management: State-of-the-art and future trends](https://www.sciencedirect.com/science/article/abs/pii/S0305054805003503). *Computers & Operations Research*, 34(10), 2902-2917.

- Coussement, K., & Van den Poel, D. (2008). [Churn prediction in subscription services: An application of support vector machines while comparing two parameter-selection techniques](https://www.sciencedirect.com/science/article/abs/pii/S0957417406002806). *Expert Systems with Applications*, 34(1), 313-327.

### Documentação Orange Data Mining

- [Orange Data Mining - Documentação Oficial](https://orange-data-mining-library.readthedocs.io/)
- [Orange3-Explain Extension](https://github.com/biolab/orange3-explain)

---

## 🤖 Declaração de Uso de IA

Este projeto foi desenvolvido com assistência de **Inteligência Artificial Generativa**.

### Escopo de Utilização

- 📝 Organização de ideias e estruturação de documentação
- 🔍 Revisão técnica de conceitos de Machine Learning
- 💡 Apoio conceitual em interpretação de métricas
- 📊 Formatação e apresentação de resultados

### Responsabilidade

Todo o conteúdo final — análises, insights, decisões técnicas e conclusões foram **integralmente revisados, validados e aprovados pelo autor**. A IA foi utilizada como ferramenta de apoio ao desenvolvimento, complementando o trabalho intelectual, não o substituindo.

### Referências sobre Disclosure de IA

- [Princeton University - Disclosing the Use of AI](https://libguides.princeton.edu/generativeAI/disclosure)
- [Arizona State University - Acknowledging AI Usage](https://libguides.asu.edu/generativeai/acknowledgement)
- [AID Framework - AI Disclosure](https://crln.acrl.org/index.php/crlnews/article/view/26548)

> Este projeto está alinhado à minha formação contínua em IA aplicada aos negócios, incluindo cursos como [IA Aplicada aos Negócios – FGV](https://educacao-executiva.fgv.br/cursos/live/curta-media-duracao-live/inteligencia-artificial-aplicada-aos-negocios-2) e [Generative AI for Productivity – Cornell](https://ecornell.cornell.edu/certificates/technology/generative-ai-for-productivity/).

---

## ⭐ Agradecimentos

- **Prof. Jorge Antunes** — Pela orientação na disciplina de Fundamentos de Machine Learning
- **SENAC-RJ** — Pela estrutura e qualidade do MBA
- **Comunidade Orange Data Mining** — Pela ferramenta open-source excepcional
- **Colegas de turma** — Pelas discussões e troca de conhecimento

---

## 👤 Autor

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/thedrads">
        <img src="https://github.com/thedrads.png" width="100px;" alt="Fábio Andrade"/><br>
        <sub><b>Fábio Andrade</b></sub>
      </a>
    </td>
  </tr>
</table>

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/fabioandradegf/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/thedrads)

**Programa:** MBA em IA & Análise de Dados – SENAC-RJ  
**Previsão de conclusão:** Outubro/2026

---

## 📄 Licença

Este projeto está sob a licença MIT — consulte [LICENSE](LICENSE) para detalhes.

---

<p align="center">
  Desenvolvido por <a href="https://github.com/thedrads">Fábio Andrade</a> | Aberto a feedbacks e contribuições
</p>
