# 📊 Análise de Aplicativos da Google Play Store

Este projeto tem como objetivo realizar uma análise exploratória dos aplicativos da Google Play Store, focando especialmente nas categorias **Educação** e **Produtividade**. A análise envolve a manipulação de dados, limpeza e visualização de informações para identificar padrões e insights relevantes.

## 📌 Tecnologias Utilizadas

- **Python**
- **Pandas**: Manipulação e limpeza de dados
- **NumPy**: Suporte para cálculos numéricos
- **Matplotlib**: Visualização de dados
- **Seaborn**: Gráficos estatísticos
- **Google Colab**: Execução do código na nuvem

## 📑 Etapas do Projeto

### 1. Carregamento dos Dados
O dataset `googleplaystore.csv` é carregado no ambiente do Google Colab e lido usando o Pandas.
```python
from google.colab import files
uploaded = files.upload()
df = pd.read_csv('googleplaystore.csv')
```

### 2. Exploração Inicial dos Dados
- Informações sobre o dataset
- Identificação de categorias
```python
df.info()
df.Category.unique()
df['Category'].value_counts(1)
```

### 3. Filtragem das Categorias de Interesse
Os aplicativos das categorias **Educação** e **Produtividade** são extraídos e processados para análise separadamente.
```python
df_educ = df[df.Category == 'EDUCATION']
df_product = df[df.Category == 'PRODUCTIVITY']
```

### 4. Limpeza e Tratamento dos Dados
- Conversão de tipos de dados
- Remoção de valores ausentes
- Tratamento da coluna `Installs`
```python
df_educ.Installs = df_educ.Installs.str.replace(',', '').str.replace('+', '').astype(int)
df_product.Installs = df_product.Installs.str.replace(',', '').str.replace('+', '').astype(int)
```

### 5. Análise Estatística
- Cálculo de médias e totais de avaliações
- Distribuição de instalações
```python
print(f"Média das avaliações de Educação: {df_educ.Rating.mean():.2f}")
print(f"Média das avaliações de Produtividade: {df_product.Rating.mean():.2f}")
```

### 6. Visualização dos Dados
Foram gerados diversos tipos de gráficos para interpretar melhor os dados:

- **Distribuição de aplicativos por categoria**
```python
sns.countplot(x='Category', data=df_educ_product)
```

- **Comparando aplicações gratuitas e pagas**
```python
sns.countplot(x='Type', data=df_educ_product, hue='Category')
```

- **Distribuição de notas dos aplicativos**
```python
sns.kdeplot(df_educ['Rating'], fill=True)
sns.kdeplot(df_product['Rating'], fill=True)
```

- **Correlação entre avaliações e downloads**
```python
sns.lmplot(y='Rating', x='Reviews', data=df_educ_product, hue='Category')
```

## ✅ Conclusões
- Aplicativos de **Educação** tendem a ter um número maior de avaliações, mas **Produtividade** tem maior número de instalações.
- A maioria dos aplicativos nas categorias analisadas são gratuitos.
- A média das avaliações para ambas as categorias está próxima de 4.0, sugerindo um bom desempenho geral.

## 🛠 Como Executar
1. **Fazer upload do dataset `googleplaystore.csv` no Google Colab**.
2. **Executar as células do notebook** para reproduzir a análise.
3. **Explorar os insights** a partir das visualizações geradas.

---

Este projeto possui apenas fins educacionais e analíticos.

