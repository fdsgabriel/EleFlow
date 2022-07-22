- Descrever qual estratégia você usaria para ingerir estes dados de forma incremental caso precise capturar esses dados a cada mes?
    Utilizaria uma ferramenta de orquestração (Airflow) para realizar o ETL mensalmente, e faria um APPEND nas tabelas. Checaria qual foi a data da última atualização e permitiria apenas datapoints que tenham datas posteriores a ela.
    Ingeriria os cados primários para um datalake (S3), trataria-os de modo a serem úteis e lançaria-os em um DW.

- Justifique em cada etapa sobre a escalabilidade da tecnologia utilizada.
    Ao ingerir os dados para o S3, o montante futuro pode aumentar bastante, o que é ótimo para a escalabilidade. O processamento desses dados pode perder desempenho com o aumento do volume de dados, o que requeriria a um processamento paralelo (Spark). E o Airflow manteria o ritmo da ETL.

- Justifique as camadas utilizadas durante o processo de ingestão até a disponibilização dos dados.
    Trata-se de uma camada maior com um montante de dados dentro de um datalake, informação disponível, seguida por uma "entre-camada" que aponta alguns documentos prioritários onde ocorre o tratamento dessas infomações escolhidas. Por fim, uma camada menor com dados tratados e úteis para análises.