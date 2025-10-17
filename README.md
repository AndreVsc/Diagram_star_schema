# Modelagem Dimensional - Análise de Atividade Docente

## Visão Geral

[cite_start]Este projeto documenta a conversão de um modelo de dados relacional de uma universidade para um modelo dimensional no formato **Star Schema**[cite: 3]. [cite_start]O objetivo é criar uma estrutura de dados otimizada para análise de BI (Business Intelligence), com foco principal nas atividades dos professores[cite: 5, 6].

## Objetivo do Projeto

[cite_start]O desafio consiste em criar um diagrama dimensional a partir de um esquema relacional existente[cite: 3]. [cite_start]A análise deve ser centrada nos professores, o que significa que a tabela fato precisa consolidar informações sobre os cursos que eles ministram e os departamentos aos quais pertencem[cite: 5, 6, 7].

[cite_start]Conforme as regras do desafio, os dados referentes aos alunos não foram incluídos no modelo dimensional[cite: 8].

## Estrutura do Star Schema

[cite_start]O modelo é composto por uma tabela fato central, que armazena as métricas, e tabelas de dimensão, que fornecem o contexto descritivo[cite: 10, 11].

### Tabela Fato

-   [cite_start]**`Fato_Atividade_Docente`**: Tabela central que registra a ocorrência de um professor lecionando uma disciplina em um determinado curso, departamento e período[cite: 7, 10]. Suas colunas são majoritariamente chaves estrangeiras que se conectam às dimensões.

### Tabelas de Dimensão

-   [cite_start]**`Dim_Professor`**: Armazena os detalhes dos professores[cite: 11].
-   **`Dim_Disciplina`**: Contém as informações sobre as disciplinas ministradas.
-   **`Dim_Curso`**: Descreve os cursos da universidade.
-   **`Dim_Departamento`**: Detalha os departamentos e seus respectivos campus.
-   [cite_start]**`Dim_Tempo`**: Uma dimensão de data foi criada, conforme solicitado, para permitir análises temporais (por exemplo, por ano ou semestre de oferta das disciplinas)[cite: 12, 13, 14].

## Diagrama do Modelo

O código abaixo pode ser utilizado em qualquer editor compatível com a linguagem Mermaid (como o Mermaid Live Editor) para gerar a representação visual do Star Schema.

```mermaid
erDiagram
    Dim_Professor {
        int SK_Professor PK "Chave Surrogada"
        int ID_Professor
        varchar Nome_Professor
    }
    Dim_Disciplina {
        int SK_Disciplina PK "Chave Surrogada"
        int ID_Disciplina
        varchar Nome_Disciplina
    }
    Dim_Curso {
        int SK_Curso PK "Chave Surrogada"
        int ID_Curso
        varchar Nome_Curso
    }
    Dim_Departamento {
        int SK_Departamento PK "Chave Surrogada"
        int ID_Departamento
        varchar Nome_Departamento
    }
    Dim_Tempo {
        int SK_Tempo PK "Chave Surrogada"
        date Data_Completa
        int Ano
        int Semestre
    }
    Fato_Atividade_Docente {
        int SK_Professor FK
        int SK_Disciplina FK
        int SK_Curso FK
        int SK_Departamento FK
        int SK_Tempo FK
        int Qtd_Disciplinas_Ministradas
    }

    Dim_Professor      ||--o{ Fato_Atividade_Docente : "relaciona-se com"
    Dim_Disciplina     ||--o{ Fato_Atividade_Docente : "relaciona-se com"
    Dim_Curso          ||--o{ Fato_Atividade_Docente : "relaciona-se com"
    Dim_Departamento   ||--o{ Fato_Atividade_Docente : "relaciona-se com"
    Dim_Tempo          ||--o{ Fato_Atividade_Docente : "relaciona-se com"
