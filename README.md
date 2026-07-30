# Modelo-Preditivo-Clinica-Medica

# 🏥 Previsão de Absenteísmo Médico (No-Show) com Machine Learning

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F6993F?style=for-the-badge&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-111111?style=for-the-badge&logo=xgboost)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen?style=for-the-badge)

## 📌 Visão Geral do Projeto

O absenteísmo de pacientes em consultas agendadas (*No-Show*) gera ineficiência operacional, ociosidade do corpo médico e perdas financeiras significativas em clínicas e hospitais. 

Este projeto desenvolve uma **solução preditiva de aprendizado de máquina** em Python para identificar, com antecedência, agendamentos com alto risco de não comparecimento. A metodologia foi construída seguindo as melhores práticas de Engenharia de Machine Learning e MLOps presentes nas obras de **Aurélien Géron** (*Hands-On Machine Learning*) e **Chip Huyen** (*Designing Machine Learning Systems*).

---

## 🎯 Objetivos de Negócio

1. **Prever Faltas**: Identificar a probabilidade de um paciente faltar à consulta no momento do agendamento ou dias antes do atendimento.
2. **Identificar Alavancas de Negócio**: Entender quais variáveis (tempo de espera, canal de contacto, especialidade) mais influenciam o comportamento do paciente.
3. **Ações Preventivas**: Subsidiar a equipa de atendimento com dados para aplicação de réguas de comunicação dinâmicas (WhatsApp/SMS) e gestão inteligente de *overbooking*.

---

## 📂 Estrutura dos Dados

A base de dados de suporte (`base_clinica_tratada.csv`) contém o histórico de agendamentos e consultas médicas com as seguintes variáveis principais:

| Variável | Descrição |
| :--- | :--- |
| `Data_Agendamento` | Data e hora em que a consulta foi marcada |
| `Data_Consulta` | Data e hora agendada para o atendimento |
| `Especialidade` | Especialidade médica da consulta |
| `Convenio` | Tipo de plano de saúde ou Particular |
| `Valor_Consulta` | Valor financeiro do procedimento |
| `Dias_Espera` | Dias decorridos entre o agendamento e a consulta |
| `Flag_No_Show` | **Target**: `1` (Não compareceu) / `0` (Compareceu) |

---

## 🛠️ Metodologia e Arquitetura da Solução

O pipeline de dados e modelo foi estruturado em 7 etapas principais:

[Dados Brutos] ➔ [Tratamento/Limpeza] ➔ [Feature Engineering] ➔ [Pipeline Scikit-Learn] ➔ [Treinamento] ➔ [Avaliação ROC-AUC] ➔ [Insights de Negócio]
1. **Análise Exploratória & Limpeza**: Padronização de datas, tratamento de valores ausentes e identificação de incoerências cadastrais (ex.: registos sem telefone válido).
2. **Engenharia de Features**:
   * Cálculo de dias de espera (`Dias_Espera`).
   * Extração de dia da semana (`Dia_Semana_Consulta`) e hora do atendimento (`Hora_Consulta`).
   * Indicador de ausência de contacto direto (`Flag_Sem_Telefone`).
3. **Pré-processamento com Pipelines**:
   * **Variáveis Numéricas**: Imputação pela mediana + `StandardScaler`.
   * **Variáveis Categóricas**: Imputação pelo valor mais frequente + `OneHotEncoder`.
4. **Modelagem Preditiva**: Treinamento comparativo de múltiplos algoritmos:
   * Regressão Logística
   * Random Forest Classifier
   * **XGBoost Classifier** *(Melhor Desempenho)*

---

## 🚀 Como Executar o Projeto

### Pré-requisitos
* Python 3.10+
* Git

### Passos para Instalação

1. **Clonar o repositório:**
   ```bash
   git clone [https://github.com/seu-usuario/previsao-noshow-clinica.git](https://github.com/seu-usuario/previsao-noshow-clinica.git)
   cd previsao-noshow-clinica
Criar e ativar um ambiente virtual (recomendado):Bashpython -m venv venv
# No Windows:
venv\Scripts\activate
# No Linux/Mac:
source venv/bin/activate
Instalar as dependências:Bashpip install -r requirements.txt
Executar o script do modelo:Bashpython src/predict_noshow.py
📈 Resultados e Conclusões Recomendadas💡 Principais AchadosJanela de Espera: Agendamentos com mais de 15 a 20 dias de antecedência apresentam a maior taxa de abandono sem aviso prévio.Canal de Comunicação: A ausência de um número de telefone móvel válido aumenta substancialmente a probabilidade de No-Show.Consultas Particulares vs. Convénio: Consultas particulares possuem menor taxa de falta não avisada.📌 Recomendações Estratégicas para a ClínicaLembretes Automatizados: Implementação de notificações via WhatsApp acionadas 72h, 48h e 24h antes para pacientes classificados com probabilidade de falta $> 40\%$.Políticas de Encaixe: Criação de lista de espera para preenchimento automático em especialidades com maior índice histórico de faltas.Saneamento Cadastral: Torna obrigatório o preenchimento de telefone/WhatsApp no momento do agendamento.💻 AutorDesenvolvido por Marcelo Rodrigues Data Scientist & Senior Data Analyst
---

### 💡 Dica de organização de pastas no GitHub:
Para deixar o seu repositório ainda mais profissional, pode estruturar os ficheiros da seguinte forma:

```text
├── data/
│   └── base_clinica_tratada.csv
├── src/
│   └── predict_noshow.py
├── requirements.txt
└── README.md
