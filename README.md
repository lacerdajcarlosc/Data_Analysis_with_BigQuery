Análise de Dados com BigQuery
📌 Visão Geral

Este projeto realiza a extração, transformação e análise de dados do dataset público Chicago Taxi Trips disponível no Google BigQuery.

O objetivo é consultar, processar e salvar os dados em arquivos CSV para análises posteriores, como criação de dashboards e relatórios.

📂 Estrutura do Projeto
.
├── generate_csvs.py          # Script principal para consulta e geração dos CSVs
├── data/                     # Pasta onde os arquivos CSV serão salvos
│   ├── travells_per_year.csv     # Total de viagens por ano
│   ├── hour_weekday.csv         # Número de corridas por hora e dia da semana
│   └── taxi_trips_sample.csv    # Amostra de 5000 viagens para análises
├── README.md                # Documentação do projeto

🛠️ Tecnologias Utilizadas

Python 3.10+

Google BigQuery → Consulta de dados

Pandas → Manipulação e exportação dos dados

Google Cloud SDK → Autenticação no BigQuery

📥 Pré-requisitos
1. Criar um projeto no Google Cloud

Acesse https://console.cloud.google.com

Crie um novo projeto

Ative a API BigQuery

2. Configurar a autenticação

Gere uma chave de serviço no Google Cloud:

Vá para IAM & Admin → Service Accounts

Clique em Create Key

Escolha JSON

Baixe o arquivo.

Configure a variável de ambiente:

export GOOGLE_APPLICATION_CREDENTIALS="caminho/para/sua_chave.json"


No Windows (PowerShell):

setx GOOGLE_APPLICATION_CREDENTIALS "C:\caminho\para\sua_chave.json"

⚡ Como Rodar o Projeto
1. Criar um ambiente virtual
python -m venv venv
source venv/bin/activate      # Linux/Mac
venv\Scripts\activate         # Windows

2. Instalar as dependências
pip install --upgrade pip
pip install google-cloud-bigquery pandas

3. Rodar o script
python generate_csvs.py

📊 Funcionalidades do Script

O script generate_csvs.py executa três consultas principais:

1. Total de viagens por ano
SELECT 
    EXTRACT(YEAR FROM trip_start_timestamp) AS year,
    COUNT(*) AS num_trips
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
GROUP BY year
ORDER BY year;


📌 Salvo em: data/travells_per_year.csv

2. Corridas por hora e dia da semana
SELECT 
    EXTRACT(HOUR FROM trip_start_timestamp) AS hour,
    EXTRACT(DAYOFWEEK FROM trip_start_timestamp) AS weekday,
    COUNT(*) AS num_trips
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE trip_start_timestamp >= '2019-01-01'
GROUP BY hour, weekday
ORDER BY weekday, hour;


📌 Salvo em: data/hour_weekday.csv

3. Amostra de 5000 viagens
SELECT 
    trip_start_timestamp,
    trip_miles,
    fare
FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
WHERE fare IS NOT NULL
    AND trip_miles IS NOT NULL
LIMIT 5000;


📌 Salvo em: data/taxi_trips_sample.csv

📂 Saída Esperada

Após rodar o script, a pasta data/ será criada com os arquivos CSV:

data/
├── travells_per_year.csv
├── hour_weekday.csv
└── taxi_trips_sample.csv

🚀 Próximos Passos

Criar gráficos exploratórios usando Matplotlib e Seaborn

Desenvolver um dashboard interativo com Plotly Dash

Gerar relatórios automáticos em PDF

👨‍💻 Autor

Carlos Lacerda
📧 Email: [seu-email-aqui]
🔗 LinkedIn: [seu-linkedin-aqui]# Data_Analysis_with_BigQuery
