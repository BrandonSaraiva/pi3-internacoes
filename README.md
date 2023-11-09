# About
This project, developed by Arquimedes Aquides, Brandon Cardoso, Guilherme Rocha and Robson Ricardo, was part of the Data Science and AI course and focused on investigating the relationship between hospitalizations, length of hospital stay and mortality in Brazil.

# Data

The project used public data provided by the Brazilian Ministry of Health, through the DATASUS platform (SIH/SUS). The data consisted of three large databases: Hospital Information System (SIH), Hospitalizations per Procedure, Deaths per Procedure, and Average Duration of Hospitalization per Procedure.

The SIH database provided the number of hospitalizations by procedure subgroup in each of the Brazilian municipalities. The *"Admissions by Procedure"* database provided the number of hospitalizations for procedures, diagnoses, surgeries, actions related to organ and tissue transplants, among others. The *"Deaths by Procedure"* database provided the number of deaths by procedure subgroup in each Brazilian municipality. Finally, the Duration *"Average Hospitalization"* by Procedure database provided the average duration of hospitalization, in days, for each procedure subgroup in each municipality.

# Procedures

The CSV files were organized by year and quarter using the platform, and went through a data cleaning process, which included separating the IBGE code and the name of the municipality into different columns and replacing null values with zero. Then, the data was processed using the Python programming language, where it was loaded into Pandas data frames and organized by year and quarter. Three new columns were created for each data frame, and the data was concatenated into a single data frame and exported to a CSV file. This process was repeated for each of the three SUS databases. The results of data processing resulted in four CSV tables: Internacoes_Procedimento_Municipio, Media_Dias_Internacao, Obitos, and Municipios_IBGE_BR. These tables were loaded into the PostgreSQL database using SQL through TablePlus software. Example of table creation:
```
CREATE TABLE "public"."Internacoes_Procedimento_Municipio" (
     "Year" varchar NOT NULL,
     "Quarter" varchar NOT NULL,
     "UID" varchar NOT NULL PRIMARY KEY,
     "Codigo_Municipio" varchar NOT NULL,
     "Municipality_Name" text NOT NULL,
     "Material_Collection" int4,
     "Diagnostic_Endoscopy" int4,
     "Metodos_Diagnosticos_Specialties" int4,
     "Inquiries_Services_Follow-ups" int4,
     "Clinical_Treatments_Outras_Specialties" int4,
     "Treatment_Oncology" int4,
     "Treatment_Nephrology" int4,
     ...
     "Monitoring_Intercorrencias_Pre_Pos_Transplante" int4,
     CONSTRAINT "Internacoes_Procedimento_Municipio_19-22_Codigo_Municipio_fkey"
         FOREIGN KEY ("Codigo_Municipio") REFERENCES "public"."Municipios_IBGE_BR"("IBGE")
);
```

# Data period

The data used in the project corresponded to a period of four years, between 2019 and 2022, and were grouped by quarter to facilitate analysis.

# Data characteristics

The data was made available in CSV format, with a semicolon separator and Latin-1 encoding.

# Treatment and Analysis

Some additional treatments, such as changing the typing of some columns, were done using Python, more specifically on the Jupyter Notebook platform. The graphics were created using SAS software and also with Python, with the help of libraries such as matplotlib, seaborn, numpy, among others.

Below is an example of a graph that was transformed into a gif:

https://github.com/BrandonSaraiva/pi3-internacoes/assets/90096835/44b4669c-6fb9-44e6-b6e5-80e1388cd85a

# Conclusion

The results of this project can help healthcare professionals and policymakers better understand the relationship between hospitalizations, length of hospital stay and mortality in Brazil. The analysis showed that some procedures have a higher hospitalization rate, longer length of hospital stay, and higher mortality rates than others. These findings can support the development of more effective public health policies and improve health outcomes for the Brazilian population.
