# 🫀 Predição de Risco Cardíaco com Explainable AI (SHAP)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Scikit-Learn](https://img.shields.io/badge/Library-Scikit--Learn-orange)
![SHAP](https://img.shields.io/badge/Explainability-SHAP-green)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 📄 Descrição do Projeto
Este projeto de Ciência de Dados visa desenvolver um modelo de Machine Learning capaz de identificar precocemente pacientes com alto risco de doenças cardiovasculares.

O diferencial técnico deste projeto é o foco na **prevenção de Data Leakage** (vazamento de dados) durante o pré-processamento e o uso de **SHAP (SHapley Additive exPlanations)** para garantir que o modelo não seja uma "caixa preta", explicando os fatores clínicos por trás de cada decisão.

---

## 💼 Contexto de Negócio & Métricas
Em diagnósticos médicos, o custo de um **Falso Negativo** (dizer que um doente está saudável) é muito maior do que um Falso Positivo. Um paciente não diagnosticado pode não receber o tratamento vital a tempo.

Por isso, este projeto priorizou a métrica de **Recall (Sensibilidade)**.
* **Objetivo:** Maximizar a detecção de casos positivos (Doença).
* **Meta Secundária:** Manter uma Acurácia global acima de 80%.

---

## 🛠️ Pipeline e Tecnologias
O projeto foi estruturado em um pipeline rigoroso para garantir a validade estatística:

1.  **Coleta de Dados:** Dataset *Heart Disease UCI* (Cleveland).
2.  **Limpeza e Mapeamento:** Padronização de variáveis categóricas e binarização do alvo.
3.  **Split de Dados:** Divisão Treino/Teste (80/20) com estratificação.
4.  **Engenharia de Atributos (Anti-Leakage):**
    * *Imputação de Nulos:* A mediana foi calculada **apenas nos dados de treino** e aplicada ao teste, simulando um cenário real de produção.
    * *Encoding:* Tratamento de variáveis categóricas (One-Hot Encoding).
    * *Escalonamento:* StandardScaler.
5.  **Modelagem:** Random Forest Classifier.
6.  **Explicabilidade:** Análise de features com SHAP.

---

## 📊 Resultados Obtidos

O modelo final atingiu os seguintes resultados nos dados de teste (nunca vistos pelo modelo):

| Métrica | Resultado | Significado |
| :--- | :--- | :--- |
| **Acurácia** | **~84%** | O modelo acerta a maioria dos diagnósticos gerais. |
| **Recall (Doença)** | **~83%** | O modelo detecta 83% de todos os doentes reais. |
| **Precisão (Doença)** | **~87%** | Quando o modelo diz que é doença, ele está certo 87% das vezes. |

> *Nota: Os valores podem variar ligeiramente dependendo da seed aleatória utilizada.*

---

## 🔍 Principais Insights (Análise SHAP)
Utilizando a biblioteca SHAP, identificamos que o modelo segue a intuição médica. As variáveis que mais impactam o risco de doença são:

1.  **Tipo de Dor no Peito (cp):** Pacientes assintomáticos ou com dores atípicas (classificação alta na escala) apresentam maior risco.
2.  **Talassemia (thal):** Defeitos reversíveis ou fixos aumentam drasticamente a probabilidade de doença.
3.  **Angina por Exercício (exang):** A presença de dor durante exercícios físicos é um divisor de águas para o diagnóstico positivo.
4.  **Depressão do Segmento ST (oldpeak):** Anomalias no eletrocardiograma são fortes preditores.

---

## 🚀 Como Executar o Projeto

### Pré-requisitos
```bash
pip install pandas numpy scikit-learn seaborn matplotlib shap
