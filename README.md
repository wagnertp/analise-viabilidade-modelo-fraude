# Análise de viabilidade de modelo de fraude

## 📌 Visão Geral

Este projeto avalia a viabilidade financeira de um modelo antigo de detecção de fraude em transações. A partir do score gerado pelo modelo, simulamos diferentes pontos de corte (thresholds) e calculamos o ganho líquido de cada um, transformando a métrica técnica em impacto de negócio.

A técnica central é a escolha do threshold com base em custo financeiro, e não apenas em métricas estatísticas. A análise completa está no notebook [`notebooks/01_exploracao.ipynb`](notebooks/01_exploracao.ipynb).

## 💼 Entendimento do Negócio

Em uma operação de pagamentos, cada transação recebe um score de risco de fraude. Uma regra de threshold decide se a transação é aprovada ou reprovada. Os dois tipos de erro têm custos diferentes:

- **Falso positivo:** uma compra legítima é reprovada. A empresa deixa de ganhar a margem da venda, estimada em 10% do valor.
- **Falso negativo:** uma fraude é aprovada. A empresa perde o valor total da compra.

Um threshold baixo bloqueia muitas compras legítimas. Um threshold alto deixa passar fraudes. O melhor ponto de corte é o que maximiza o ganho líquido, e não o que maximiza a acurácia. Como a base tem apenas 5% de fraudes, a acurácia seria enganosa: um modelo que aprovasse tudo teria 95% de acerto.

**Tipos de análise realizados:**
- Exploração inicial e verificação da qualidade dos dados
- Análise da distribuição do score por classe de fraude
- Simulação do ganho líquido por threshold, de 0 a 100
- Refinamento do threshold entre 70 e 80

**Indicadores-chave:**
- Ganho líquido em reais, por threshold
- Quantidade de transações aprovadas
- Fraudes aprovadas (falsos negativos) e legítimas reprovadas (falsos positivos)
