<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=df5f2e&height=120&section=header"/>

[![Typing SVG](https://readme-typing-svg.herokuapp.com/?color=df5f2e&size=35&center=true&vCenter=true&width=1000&lines=Bem+vindo,+faça+sua+consulta)](https://git.io/typing-svg)
-----

## 📑 Sumário

  - [Visão Geral](#visão-geral)
  - [Estrutura e Tópicos](#estrutura-e-tópicos)
  - [Coleta e Geração de Dados](#coleta-e-geração-de-dados)
  - [Limpeza e Preparação de Dados](#limpeza-e-preparação-de-dados)
  - [Engenharia de Recursos](#engenharia-de-recursos)
  - [Análise Estatística](#análise-estatística)
  - [Transformação de Variáveis](transformacao-de-variáveis)
  - [Visualização de Dados](#visualização-de-dados)
  - [Boas Práticas](#boas-práticas)
  - [Autor](#autor)

-----

## Visão Geral

Este **Caderno de Anotações** é um guia rápido e prático sobre os fundamentos da **Análise Exploratória de Dados (AED)**, cobrindo todo o ciclo de vida de um projeto de análise. O material foca nas operações essenciais e boas práticas, utilizando as bibliotecas mais importantes do ecossistema Python: **Pandas**, **Matplotlib**, **Seaborn** e **Plotly**.

A estrutura do caderno é projetada para ser um ponto de referência rápido e objetivo, ideal para consulta diária.

## Estrutura e Tópicos

O caderno está organizado em seções que seguem um fluxo de trabalho lógico de análise de dados. Cada seção detalha as funções, seu propósito, biblioteca utilizada e exemplos práticos.

### Coleta e Geração de Dados

| Função | O que é | Para que serve | Biblioteca | Requisitos |
| :--- | :--- | :--- | :--- | :--- |
| **`requests.get()`** | Faz uma requisição HTTP. | Coletar o conteúdo HTML de uma página web estática. | `requests` | URL da página. |
| **`BeautifulSoup()`** | Analisa o HTML. | Navegar e extrair informações específicas da estrutura da página. | `BeautifulSoup` | Conteúdo HTML (do `requests.get()`). |
| **`webdriver.Chrome()`** | Inicia um navegador automatizado. | Extrair conteúdo de páginas que carregam dinamicamente via JavaScript. | `selenium` | Chromedriver instalado e configurado. |
| **`pd.read_html()`** | Extrai tabelas diretamente do HTML. | Converter tabelas HTML em um DataFrame do Pandas. | `pandas` | Conteúdo HTML com tabelas. |
| **`Faker()`** | Cria um gerador de dados falsos. | Gerar dados sintéticos que simulam características reais. | `Faker` | Não há. |
| **`pd.read_csv()`** | Lê dados de um arquivo CSV. | Carregar um conjunto de dados existente em um DataFrame. | `pandas` | Arquivo CSV local. |

**Comentários:**

  * Para **Web Scraping Dinâmico**, o `selenium` é essencial para lidar com sites que exigem interação ou que carregam conteúdo com atraso. O `time.sleep()` é usado para dar tempo ao navegador para renderizar a página.
  * A geração de **dados sintéticos** é útil para testar códigos, demonstrar funcionalidades ou trabalhar em projetos sem dados reais. A biblioteca `Faker` oferece uma variedade de geradores localizados (ex: `pt-BR`).
  * Para o carregamento de arquivos, a função `os.chdir()` pode ser usada para alterar o diretório de trabalho e facilitar a leitura do arquivo.

-----

### Limpeza e Preparação de Dados

| Função | O que é | Para que serve | Biblioteca | Requisitos |
| :--- | :--- | :--- | :--- | :--- |
| **`pd.to_numeric()`** | Converte uma coluna para tipo numérico. | Permitir cálculos e análises em colunas que foram importadas como texto. | `pandas` | Coluna do DataFrame. |
| **`.isnull().sum()`** | Conta valores nulos. | Identificar a quantidade de dados faltantes por coluna. | `pandas` | DataFrame. |
| **`.fillna()`** | Preenche valores nulos. | Lidar com dados faltantes substituindo-os por um valor ou método. | `pandas` | DataFrame com valores nulos. |
| **`.dropna()`** | Remove linhas/colunas com nulos. | Remover dados faltantes quando a substituição não é a melhor opção. | `pandas` | DataFrame com valores nulos. |
| **`.str.strip()`** | Remove espaços em branco. | Padronizar nomes de colunas ou valores de texto para evitar erros. | `pandas` | Nomes de colunas ou coluna de texto. |

**Exemplos e Comentários:**

  * Ao usar `pd.to_numeric(errors='coerce')`, os valores que não podem ser convertidos para números são transformados em `NaN` (nulos), o que permite o tratamento posterior.
  * A filtragem de dados é uma operação fundamental. Por exemplo, `df[(df['Coluna'] != 0) & (df['Coluna'].notna())]` combina duas condições para selecionar linhas que não têm valor zero e não são nulas.

-----

### Engenharia de Recursos (Feature Engineering Básico)

| Função | O que é | Para que serve | Biblioteca | Requisitos |
| :--- | :--- | :--- | :--- | :--- |
| **Cálculo Direto** | Cria uma nova coluna a partir de colunas existentes. | Derivar métricas mais relevantes para sua análise (ex: `preço_total = preço_unitario * quantidade`). | `pandas` | Duas ou mais colunas numéricas. |
| **`.str.extract()`** | Captura informações de texto com Regex. | Extrair padrões específicos de strings para criar novas colunas. | `pandas` | Coluna de texto e uma expressão regular (Regex). |
| **`np.random.uniform()`** | Gera números aleatórios. | Simular cenários, como a criação de uma coluna de descontos ou taxas. | `numpy` | Faixa de valores (`min`, `max`) e tamanho da amostra (`size`). |

**Comentários:**

  * A Engenharia de Recursos é a arte de criar novas variáveis a partir das existentes para melhorar o desempenho de modelos de Machine Learning.
  * O uso de Expressões Regulares (Regex) com `.str.extract()` é poderoso para estruturar dados que estão em formato de texto livre.

-----

### Análise Estatística e Agregação

| Função | O que é | Para que serve | Biblioteca | Requisitos |
| :--- | :--- | :--- | :--- | :--- |
| **`.nunique()`** | Conta valores únicos. | Entender a cardinalidade das variáveis (quão diversas são). | `pandas` | DataFrame. |
| **`.value_counts()`** | Conta a frequência de valores. | Entender a distribuição de categorias em uma coluna. | `pandas` | Coluna do DataFrame. |
| **`.groupby()`** | Agrupa dados por categoria. | Calcular métricas por grupo (ex: média de salário por profissão). | `pandas` | Coluna categórica para agrupar. |
| **`.agg()`** | Aplica funções de agregação. | Calcular múltiplas métricas em diferentes colunas dentro de um grupo. | `pandas` | DataFrame agrupado. |
| **`.mean()`, `.median()`, `.mode()`** | Medidas de tendência central. | Resumir o "centro" de um conjunto de dados. | `pandas` | Coluna numérica. |
| **`.std()`** | Desvio Padrão. | Medir a variabilidade ou dispersão dos dados. | `pandas` | Coluna numérica. |

**Exemplos e Comentários:**

  * O método `value_counts(normalize=True)` é útil para obter a proporção percentual de cada categoria.
  * A cadeia de operações `df.groupby(...).agg(...).reset_index().sort_values(...)` é um padrão comum para realizar análises de agrupamento complexas e apresentar o resultado de forma clara.

-----

### Transformação de Variáveis (Pré-processamento) 🔄

Esta etapa é crucial para preparar dados para modelos de Machine Learning.

| Função | O que é | Para que serve | Biblioteca | Requisitos |
| :--- | :--- | :--- | :--- | :--- |
| **`MinMaxScaler()`** | Normaliza dados para um intervalo [0, 1]. | Evitar que variáveis com grandes ranges dominem o modelo. | `sklearn` | Coluna numérica. |
| **`StandardScaler()`** | Padroniza dados para média 0 e desvio 1. | Útil para algoritmos que assumem uma distribuição normal. | `sklearn` | Coluna numérica. |
| **`LabelEncoder()`** | Codifica categorias em números inteiros. | Converter variáveis categóricas ordinais em um formato numérico. | `sklearn` | Coluna categórica. |
| **`pd.get_dummies()`** | Cria variáveis *dummy* (One-Hot). | Converter variáveis categóricas nominais para um formato binário, evitando que o modelo assuma uma ordem. | `pandas` | Coluna categórica. |

**Comentários:**

  * A escolha entre Normalização e Padronização depende da distribuição dos seus dados e do algoritmo de Machine Learning que você irá usar.
  * A codificação de variáveis categóricas é obrigatória para a maioria dos modelos de ML. `LabelEncoder` é ideal para variáveis ordinais, enquanto `pd.get_dummies` (One-Hot Encoding) é preferível para variáveis nominais.

-----

### Visualização de Dados Essenciais (Resumo)

Para detalhes mais profundos e exemplos, consulte o "Caderno de Anotações: Visualização de Dados".

| Função | Para que serve | Biblioteca | Requisitos |
| :--- | :--- | :--- | :--- |
| **Gráfico de Barras** | Comparar quantidades entre categorias. | `matplotlib`, `seaborn`, `plotly` | Variável categórica e uma numérica. |
| **Gráfico de Dispersão** | Mostrar a relação entre duas variáveis numéricas. | `matplotlib`, `plotly` | Duas variáveis numéricas. |
| **Mapa de Calor** | Visualizar correlações entre múltiplas variáveis. | `seaborn`, `plotly` | Matriz de correlação. |
| **Boxplot** | Visualizar a distribuição, assimetria e outliers. | `matplotlib`, `plotly` | Variável numérica. |
| **Gráfico de Densidade** | Visualizar a distribuição suave de uma variável. | `seaborn` | Variável numérica. |
| **Gráfico Treemap** | Visualizar proporções em dados hierárquicos. | `plotly` | Variáveis hierárquicas. |

**Comentários:**

  * As bibliotecas `Matplotlib` e `Seaborn` são excelentes para gráficos estáticos, enquanto `Plotly` se destaca por suas visualizações interativas.
  * A escolha do gráfico certo é fundamental para comunicar insights de forma clara e eficaz.

-----

### Boas Práticas e Modularização 

| Função/Prática | O que é | Para que serve | Biblioteca | Requisitos |
| :--- | :--- | :--- | :--- | :--- |
| **Organização em Funções** | Agrupar código em blocos reutilizáveis. | Reusabilidade, modularidade e legibilidade. | `python` | Nenhum. |
| **`pathlib`** | Manipula caminhos de arquivo de forma segura. | Compatibilidade entre sistemas operacionais (Windows, Linux, macOS). | `pathlib` | Nenhum. |
| **`try-except`** | Tratamento de erros. | Tornar o código mais robusto e fornecer feedback claro em caso de problemas. | `python` | Nenhum. |
| **Exportação de Gráficos** | Salvar visualizações em arquivos. | Compartilhar visualizações interativas ou estáticas em relatórios. | `plotly`, `matplotlib` | Para `plotly`, `kaleido` pode ser necessário. |

**Exemplos e Comentários:**

  * A criação de funções como `load_and_clean_data()` encapsula o processo inicial de preparação dos dados, tornando o código principal mais limpo.
  * O uso de `pathlib.Path()` substitui a concatenação de strings para caminhos de arquivo, eliminando problemas com barras (`/` ou `\`).
  * Tratar erros com `try-except` e `raise` permite que o programa se recupere de falhas ou avise o usuário sobre um problema de forma clara.

-----
### Autor 
**Johnny Sorato Martins Fernandes**  
Business Consultant | Data & Visualization Specialist | Executive Director at Tutoreanos — Primavera do Leste Unit

-----

## 🔖 Tags

`data-analysis`, `data-science`, `data-cleaning`, `web-scraping`, `feature-engineering`, `descriptive-statistics`, `data-visualization`, `python`, `pandas`, `matplotlib`, `seaborn`, `plotly`
