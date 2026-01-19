# 🎤 FAQ - Preparação para Entrevistas

## Guia de Perguntas e Respostas sobre o Projeto Churn Telecom

Este documento contém respostas estruturadas para perguntas comuns em entrevistas técnicas sobre este projeto.

---

## 📋 Perguntas Gerais sobre o Projeto

### 1. "Conte-me sobre este projeto de churn prediction."

**Resposta estruturada (método STAR):**

**Situação:** Durante o MBA em IA e Análise de Dados no SENAC-RJ, recebi um desafio acadêmico: desenvolver um modelo de Machine Learning para prever cancelamento de clientes em uma empresa de telecomunicações.

**Tarefa:** Precisava implementar um pipeline ML completo - desde análise exploratória até deploy simulado - utilizando Orange Data Mining, testando múltiplos algoritmos e validando rigorosamente o modelo final.

**Ação:** 
- Levantei hipóteses sobre importância das variáveis antes de ver os dados
- Testei 16+ configurações de modelos (Random Forest, GBM, Logistic Regression, Neural Networks)
- Utilizei validação cruzada estratificada (k=10) para selecionar o melhor modelo
- Validei em conjunto hold-out (20%) nunca visto
- Analisei interpretabilidade com Permutation Feature Importance
- Realizei deploy simulado para novo cliente

**Resultado:** 
- Modelo Random Forest atingiu AUC de 0.905 na validação cruzada e 0.880 no teste
- Queda de performance < 3%, indicando boa generalização
- As 3 variáveis mais importantes confirmaram minhas hipóteses iniciais
- Identifiquei um caso limítrofe (53% vs 47%) demonstrando compreensão de incerteza do modelo

---

## 🤖 Perguntas Técnicas sobre Machine Learning

### 2. "Por que você escolheu Random Forest?"

**Resposta:**

Testei 4 famílias de algoritmos com 16+ configurações diferentes. O Random Forest (300 árvores, 3 features por split) foi escolhido por três razões principais:

1. **Performance:** AUC de 0.905, empatado com GBM-100 no topo
2. **Robustez:** MCC de 0.737, superior ao GBM (0.723), indicando melhor equilíbrio entre todas as classes
3. **Produção:** 300 árvores oferecem maior estabilidade que 100, característica importante para deploy real

Além disso, Random Forest é mais interpretável que Gradient Boosting, facilitando extração de insights de negócio - importante para comunicar resultados a stakeholders não-técnicos.

**Trade-off reconhecido:** O RF (100 trees) tinha F1 e MCC ligeiramente superiores, mas priorizei estabilidade para ambiente de produção.

---

### 3. "Como você lidou com overfitting?"

**Resposta:**

Utilizei uma abordagem em camadas:

**1. Validação Cruzada Estratificada (k=10):**
- Testei o modelo em 10 partições diferentes dos dados de treino
- Estratificação manteve proporção de classes em cada fold
- Isso me deu uma estimativa robusta da performance esperada

**2. Hold-out Set Preservado:**
- Separei 20% dos dados no início e **não toquei** até a validação final
- Treinei o modelo vencedor em 100% do treino e testei no hold-out
- Queda de AUC foi de apenas 2.8% (0.905 → 0.880)

**3. Análise de Métricas Múltiplas:**
- Não me baseei apenas em accuracy
- Avaliei AUC, F1, MCC para ter visão completa
- Todas as métricas se mantiveram acima de 90% (exceto MCC)

**Conclusão:** A queda de performance < 3% indica que o modelo generaliza bem e não apresenta overfitting significativo.

---

### 4. "Explique o que é Permutation Feature Importance."

**Resposta:**

Permutation Feature Importance é uma técnica de interpretabilidade que mede a importância de uma variável **embaralhando aleatoriamente** seus valores e medindo o quanto a performance do modelo cai.

**Como funciona:**
1. Calcula-se a métrica base (AUC) com os dados originais
2. Para cada feature, seus valores são embaralhados aleatoriamente
3. Recalcula-se o AUC com a feature embaralhada
4. A queda no AUC indica a importância daquela feature

**Por que é útil:**
- Funciona com qualquer modelo (model-agnostic)
- Mais confiável que feature importance nativa do Random Forest
- Captura dependências não-lineares

**No meu projeto:** As 3 variáveis mais importantes foram monthly_charge, customer_service_calls e contract_renewal - exatamente as que eu havia previsto na análise prévia, validando minha compreensão do problema de negócio.

---

### 5. "O que você faria diferente se reimplementasse em Python?"

**Resposta:**

Se fosse reimplementar em Python (scikit-learn), eu faria:

**Melhorias Técnicas:**
1. **Feature Engineering:** Criar variáveis derivadas (ex: razão overage_fee/monthly_charge, interação entre customer_service_calls e monthly_charge)
2. **Balanceamento de Classes:** Testar SMOTE ou class_weight para lidar com desbalanceamento
3. **Otimização de Hiperparâmetros:** Usar GridSearchCV ou RandomizedSearchCV para busca sistemática
4. **Ensemble:** Testar stacking de múltiplos modelos

**Análises Adicionais:**
5. **Curva Precision-Recall:** Avaliar diferentes thresholds
6. **Análise de Custo-Benefício:** Otimizar threshold baseado em custo de retenção vs. custo de churn
7. **SHAP Values:** Interpretabilidade mais detalhada por instância
8. **Análise de Erros:** Investigar características dos falsos positivos e falsos negativos

**Deploy:**
9. **API REST:** Criar endpoint com FastAPI para previsões em tempo real
10. **Dashboard:** Streamlit para visualização interativa de resultados

Mas reconheço que o Orange foi excelente para prototipagem rápida e aprendizado dos conceitos fundamentais.

---

## 🛠️ Perguntas sobre Ferramentas

### 6. "Por que você usou uma ferramenta no-code?"

**Resposta:**

**Contexto Acadêmico:** Este foi um projeto da disciplina de Fundamentos de Machine Learning no MBA, onde o professor escolheu Orange Data Mining como ferramenta pedagógica.

**Vantagens do Orange para Aprendizado:**
1. **Visualização do Pipeline:** Ver o workflow visualmente ajudou a consolidar conceitos
2. **Foco em Conceitos:** Menos tempo com sintaxe, mais tempo entendendo ML
3. **Prototipagem Rápida:** Testar 16+ modelos em minutos
4. **Validação de Aprendizado:** Forçou entender os algoritmos, não apenas copiar código

**Transição para Python:** Estou agora reimplementando projetos em Python/scikit-learn para desenvolver habilidades de programação. O Orange me deu uma base conceitual sólida que facilita essa transição.

**Ferramentas no-code têm espaço?** Sim! Em muitas empresas, analistas de negócio usam ferramentas como Orange, KNIME, ou Azure ML Studio. O importante é entender **o que** o algoritmo faz, não apenas **como** programá-lo.

---

### 7. "Qual foi o desafio técnico mais difícil?"

**Resposta:**

**Desafio:** Instalação da extensão "Explain" (necessária para Feature Importance) no Orange Data Mining.

**Problema:** Ao tentar instalar via Add-ons, recebia erro:
```
Command failed: python -m pip install --upgrade 
Orange3-Explain==0.6.10 exited with non zero status
```

**Processo de Resolução:**
1. **Pesquisa:** Investiguei fóruns e documentação
2. **Diagnóstico:** Descobri que o erro não informava claramente a causa raiz
3. **Solução:** Encontrei que era necessário instalar Microsoft Visual C++ Redistributable
4. **Implementação:** Download do C++ Redistributable + reinicialização do sistema
5. **Validação:** Extensão instalou corretamente após correção

**Aprendizado:**
- Importância de compreender dependências de sistema para bibliotecas Python
- Desenvolvimento de habilidades de troubleshooting
- Persistência e uso de recursos (IA, fóruns, documentação) para resolver problemas
- Mensagens de erro nem sempre são claras - preciso investigar a fundo

Esse desafio me ensinou mais do que simplesmente instalar uma extensão - aprendi sobre o ecossistema Python, dependências de sistema e resolução sistemática de problemas.

---

## 💼 Perguntas sobre Negócio

### 8. "Como você traduziria os resultados para um stakeholder não-técnico?"

**Resposta:**

**Para um CEO/Diretor de Retenção:**

"Desenvolvemos um sistema que identifica clientes com alto risco de cancelamento antes que eles saiam. O modelo acerta 92% das previsões e consegue identificar 9 em cada 10 clientes que realmente vão cancelar.

As 3 variáveis mais importantes são:
1. **Preço da mensalidade** - clientes com valores altos têm maior risco
2. **Ligações para o suporte** - muitas chamadas indicam insatisfação
3. **Renovação de contrato** - renovar demonstra compromisso

**Valor de Negócio:** Com este modelo, podemos:
- Priorizar ações de retenção nos clientes de maior risco
- Economizar recursos não gastando com clientes de baixo risco
- Reduzir churn em até 15% com intervenções proativas

**Exemplo Real:** Analisamos um cliente novo e o modelo indicou 53% de probabilidade de permanecer vs. 47% de cancelar. Este é um caso **limítrofe** que merece atenção especial - como um sinal amarelo no semáforo."

**Visualizações que Prepararia:**
- Dashboard com ranking de clientes por risco
- Gráfico mostrando top 3 fatores de churn
- ROI estimado do programa de retenção

---

### 9. "Como você mediria o sucesso deste modelo em produção?"

**Resposta:**

**Métricas Técnicas (Monitoramento Contínuo):**
1. **AUC mensal:** Comparar com baseline de 0.880
2. **Precision/Recall:** Ajustar threshold se necessário
3. **Data Drift:** Monitorar se distribuição das variáveis mudou
4. **Concept Drift:** Verificar se relação features-target mudou

**Métricas de Negócio (KPIs):**
1. **Taxa de Churn:** Medir redução real após ações de retenção
2. **ROI do Programa:** (Receita retida - Custo das ações) / Custo das ações
3. **Taxa de Conversão:** % de clientes em risco que foram retidos após intervenção
4. **Precisão das Ações:** Se estamos focando nos clientes certos

**Experimento A/B (Ideal):**
- **Grupo A:** Recebe intervenções baseadas no modelo
- **Grupo B:** Intervenções aleatórias ou processo atual
- **Medida:** Comparar taxa de churn entre grupos após 3-6 meses

**Feedback Loop:**
- Coletar dados sobre sucesso/fracasso das intervenções
- Retreinar modelo periodicamente (ex: a cada trimestre)
- Incorporar novos padrões aprendidos

**Meta de Sucesso:**
- Redução de churn de pelo menos 10-15%
- ROI positivo dentro de 6 meses
- Modelo mantém AUC acima de 0.85

---

## 🎓 Perguntas sobre Aprendizado

### 10. "O que você aprendeu com este projeto?"

**Resposta:**

**Aprendizados Técnicos:**
1. **Pipeline ML Completo:** Entendi todas as etapas (prep, modelagem, validação, interpretação, deploy)
2. **Importância da Validação:** Validação cruzada + hold-out set são essenciais
3. **Trade-offs:** Nem sempre o modelo com melhores métricas é o melhor para produção
4. **Interpretabilidade:** Modelos precisam ser explicáveis para gerar confiança

**Aprendizados de Negócio:**
1. **Churn é Custoso:** Reter clientes é 5-25x mais barato que adquirir novos
2. **Incerteza é Real:** Casos limítrofes (53% vs 47%) mostram que ML não é magia
3. **Priorização:** Recursos limitados devem focar em clientes de alto risco

**Soft Skills:**
1. **Troubleshooting:** Resolvi problema complexo de dependências de sistema
2. **Documentação:** Escrever este README solidificou meu entendimento
3. **Humildade Intelectual:** Reconhecer limitações (ferramenta no-code, dataset acadêmico)
4. **Comunicação:** Traduzi conceitos técnicos para linguagem de negócio

**Meta-Aprendizado:**
Este projeto me mostrou que minha experiência de 20 anos em gestão de negócios é um **ativo**, não um passivo, na transição para tech. Consigo conectar análises técnicas com impacto real no negócio - habilidade valiosa para um Data Scientist.

---

## 🚀 Perguntas sobre Próximos Passos

### 11. "Onde você quer chegar profissionalmente?"

**Resposta:**

**Curto Prazo (6-12 meses):**
- Concluir MBA em IA e Análise de Dados (out/2026)
- Desenvolver portfólio robusto com projetos em Python
- Contribuir para projetos open-source relacionados a ML
- Conquistar primeira posição como Junior Data Scientist ou ML Engineer

**Médio Prazo (1-3 anos):**
- Aprofundar conhecimento em Deep Learning e NLP
- Certificações em Cloud (AWS Certified ML Specialty)
- Trabalhar em projetos com impacto mensurável de negócio
- Desenvolver especialização em um domínio (healthcare, fintech, ou telecom)

**Visão de Longo Prazo:**
Quero ser um **Data Scientist/ML Engineer** que conecta tecnologia com valor de negócio. Combinar minha experiência em gestão com habilidades técnicas avançadas para:
- Liderar projetos de IA do conceito ao deploy
- Mentorar outros profissionais em transição de carreira
- Contribuir para democratização da IA em empresas de médio porte

**Por que essa área?**
Estou genuinamente fascinado pela capacidade de **transformar dados em decisões** que impactam pessoas e negócios. Cada projeto de ML é um problema diferente a resolver - isso me mantém motivado e em constante aprendizado.

---

## 💡 Perguntas sobre Uso de IA

### 12. "Você usou IA para fazer este projeto?"

**Resposta (Transparência Total):**

**Sim, com total transparência.** Utilizei ferramentas de IA generativa como **assistente técnico** em aspectos específicos:

**O que a IA ajudou:**
1. Revisão técnica de conceitos de ML que eu estava aprendendo
2. Estruturação da documentação (README, metodologia)
3. Brainstorming de formas de apresentar resultados

**O que EU fiz:**
1. **Todo o trabalho técnico:** Configurei modelos, executei validação cruzada, analisei resultados
2. **Todas as decisões:** Escolha do modelo, interpretação das métricas, conclusões
3. **Todo o aprendizado:** Estudei os conceitos, entendi os algoritmos, validei resultados

**Por que transparência importa:**
- Ética profissional: Honestidade sobre ferramentas usadas
- Educação moderna: IA como assistente é realidade do mercado
- Diferencial: Saber **quando** e **como** usar IA efetivamente

**Analogia:** Assim como um engenheiro usa CAD para desenhar mas precisa entender estruturas, eu usei IA para documentar mas preciso entender Machine Learning.

**Disclosure no Projeto:** Incluí declaração completa de uso de IA no README com referências acadêmicas sobre boas práticas (Princeton, ASU, AID Framework).

---

## 📌 Perguntas sobre Portfólio

### 13. "Por que devo contratar você como Junior Data Scientist?"

**Resposta:**

**Diferencial 1: Experiência de Negócio + Habilidades Técnicas**
- 20 anos em gestão (área veterinária) me ensinaram a resolver problemas reais
- Sei traduzir necessidades de negócio em soluções técnicas
- Entendo que ML é meio, não fim - o objetivo é gerar valor

**Diferencial 2: Aprendizado Estruturado e Proativo**
- MBA em IA e Análise de Dados (SENAC-RJ)
- Oracle Next Education (ONE) - Data Science
- AWS re/Start - Cloud Computing
- Portfolio com projetos documentados (não apenas código)

**Diferencial 3: Maturidade Profissional**
- Sei trabalhar em equipe (20 anos de experiência)
- Comunico tecnicamente (este README é evidência)
- Reconheço limitações e busco feedback
- Entrego projetos completos, não apenas "fazer funcionar"

**Diferencial 4: Motivação Genuína**
- Não estou apenas "mudando de área" - estou **construindo uma segunda carreira**
- Investi tempo e recursos significativos no MBA
- Criei portfolio para demonstrar aprendizado
- Estou comprometido com aprendizado contínuo

**O que ofereço:**
- Capacidade de aprender rápido (provado pela transição de carreira)
- Visão de negócio que muitos juniores não têm
- Ética de trabalho e profissionalismo
- Humildade para perguntar e buscar ajuda

**O que busco:**
- Oportunidade de aplicar conhecimento em problemas reais
- Mentoria de profissionais experientes
- Ambiente que valorize aprendizado e crescimento
- Time que me desafie tecnicamente

---

## 🎯 Dicas de Preparação

### Como Usar Este FAQ

1. **Leia em voz alta:** Pratique as respostas naturalmente
2. **Adapte ao contexto:** Use linguagem apropriada à empresa/vaga
3. **Seja autêntico:** Não decore - entenda e adapte ao seu estilo
4. **Demonstre entusiasmo:** Mostre paixão pelo projeto e pela área
5. **Prepare exemplos:** Tenha histórias concretas de aprendizado

### Estrutura STAR para Respostas

- **S**ituação: Contexto do desafio
- **T**arefa: O que precisava ser feito
- **A**ção: O que você fez especificamente
- **R**esultado: Impacto mensurável

### O Que Evitar

- ❌ Ser arrogante ou sabe-tudo
- ❌ Subestimar a ferramenta no-code
- ❌ Fingir que sabe algo que não sabe
- ❌ Não reconhecer limitações do projeto
- ❌ Focar apenas em técnica, ignorando negócio

### O Que Fazer

- ✅ Demonstrar pensamento crítico
- ✅ Conectar técnica com negócio
- ✅ Mostrar aprendizado contínuo
- ✅ Ser humilde mas confiante
- ✅ Perguntar sobre a empresa/time

---

**Lembre-se:** Entrevistas são conversas. Seja você mesmo, mostre curiosidade genuína e demonstre vontade de aprender. Seu diferencial não é saber tudo - é mostrar que você SABE APRENDER.

---

*Documento elaborado para preparação de entrevistas técnicas - Projeto Churn Telecom MBA SENAC-RJ*
