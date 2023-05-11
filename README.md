Este projeto, desenvolvido por Arquimedes Aquides, Brandon Cardoso, Guilherme Rocha e Robson Ricardo, fez parte do curso de Ciência de Dados e IA e teve como foco investigar a relação entre internações, duração da estadia hospitalar e mortalidade no Brasil.

**Dados**

O projeto utilizou dados públicos fornecidos pelo Ministério da Saúde do Brasil, por meio da plataforma DATASUS (SIH/SUS). Os dados consistiam em três grandes bancos de dados: Sistema de Informações Hospitalares (SIH), Internações por Procedimento, Mortes por Procedimento e Duração Média da Hospitalização por Procedimento.

O banco de dados SIH forneceu o número de internações por subgrupo de procedimento em cada um dos municípios brasileiros. O banco de dados *"Internações por Procedimento"* forneceu o número de internações para procedimentos, diagnósticos, cirurgias, ações relacionadas a transplantes de órgãos e tecidos, entre outros. O banco de dados *"Mortes por Procedimento"* forneceu o número de mortes por subgrupo de procedimento em cada município brasileiro. Por fim, o banco de dados Duração *"Média da Hospitalização"* por Procedimento forneceu a duração média da hospitalização, em dias, para cada subgrupo de procedimento em cada município.

**Procedimentos**

Os arquivos CSV foram organizados por ano e trimestre utilizando a plataforma, e passaram por um processo de limpeza de dados, que incluiu a separação do código IBGE e do nome do município em colunas distintas e a substituição dos valores nulos por zero. Em seguida, os dados foram tratados usando a linguagem de programação Python, onde foram carregados em data frames do Pandas e organizados por ano e trimestre. Foram criadas três novas colunas para cada data frame, e os dados foram concatenados em um único data frame e exportados para um arquivo CSV. Esse processo foi repetido para cada uma das três bases de dados do SUS. Os resultados do tratamento dos dados resultaram em quatro tabelas em CSV: Internacoes_Procedimento_Municipio, Media_Dias_Internacao, Obitos, e Municipios_IBGE_BR. Essas tabelas foram carregadas no banco de dados PostgreSQL usando SQL através do software TablePlus. Exemplo de criação da tabela:
`CREATE TABLE "public"."Internacoes_Procedimento_Municipio" (
"Ano" varchar NOT NULL,
"Trimestre" varchar NOT NULL,
"UID" varchar NOT NULL PRIMARY KEY
,
"Codigo_Municipio" varchar NOT NULL,
"Nome_Municipio" text NOT NULL,
"Coleta_Material" int4
,
"Diagnostico_Endoscopia" int4
,
"Metodos_Diagnosticos_Especialidades" int4
,
"Consultas_Atendimentos_Acompanhamentos" int4
,
"Tratamentos_Clinicos_Outras_Especialidades" int4
,
"Tratamento_Oncologia" int4
,
"Tratamento_Nefrologia" int4
,
...
"Acompanhamento_Intercorrencias_Pre_Pos_Transplante" int4
,
CONSTRAINT "Internacoes_Procedimento_Municipio_19
-22_Codigo_Municipio_fkey"
FOREIGN KEY ("Codigo_Municipio") REFERENCES "public"."Municipios_IBGE_BR"("IBGE")
);`

**Período dos dados**

Os dados utilizados no projeto correspondiam a um período de quatro anos, entre 2019 e 2022, e foram agrupados por trimestre para facilitar a análise.

Características dos dados

Os dados foram disponibilizados em formato CSV, com separador de ponto e vírgula e codificação Latin-1. As tabelas foram organizadas por municípios brasileiros (linhas) e por subgrupos de procedimentos hospitalares (colunas).

Tratamento e Carregamento

O processo de limpeza dos dados envolveu a remoção do cabeçalho e rodapé que continham informações do arquivo e a atribuição da fonte de dados. O nome dos procedimentos hospitalares também foi modificado para facilitar a legibilidade e remover os códigos internos do SUS.

Após a limpeza, os dados foram carregados em data frames do pandas e organizados por ano e trimestre. Três novas colunas foram criadas para cada data frame para melhorar a análise. Por fim, os data frames foram concatenados para facilitar uma análise abrangente.

Conclusão

Os resultados deste projeto ajudarão profissionais de saúde e formuladores de políticas a entender melhor a relação entre internações, duração da estadia hospitalar e mortalidade no Brasil. A análise mostrou que alguns procedimentos têm uma taxa de internação mais alta, duração de estadia hospitalar mais longa e taxas de mortalidade mais altas do que outros. Essas descobertas podem apoiar o desenvolvimento de políticas de saúde pública mais eficazes e melhorar os resultados de saúde para a população brasileira.
