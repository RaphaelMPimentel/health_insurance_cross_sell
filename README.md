# Health Insurance Cross-Sell

## Este projeto tem como objetivo priorizar uma lista de clientes potenciais por pontuação de propensão, com base na probabilidade de compra de um novo produto de seguro de automóvel.

### 1. Business Problem
A empresa de seguros oferece seguros de saúde para uma base de clientes que já pagam anualmente pelo serviço. Agora, o time de produtos deseja lançar um novo produto: um seguro de carros. No entanto, antes de investir no lançamento do produto, a empresa precisa entender a viabilidade dessa oferta, identificar o potencial de receita e determinar para quais clientes ela deve oferecer o novo produto.

O desafio é que uma pesquisa foi realizada apenas com um subconjunto de clientes existentes, perguntando se comprariam ou não o seguro de carro. Com base nessas respostas, é necessário prever, por meio de um classificador, quais clientes (que não participaram da pesquisa) têm maior probabilidade de comprar o seguro de carro. O time comercial tem um limite de 2.000 ligações para prospectar, enquanto a base total de clientes possui 127.000 registros. O objetivo é priorizar as 2.000 pessoas com maior propensão para comprar o novo produto.

### 2. Business Assumptions
- Os dados fornecidos são representativos dos clientes da base e a segmentação do público-alvo pode ser extrapolada para novos clientes.
- As variáveis presentes na base de dados têm uma relação significativa com a probabilidade de compra do seguro de automóvel.
- O modelo de classificação será suficiente para gerar uma lista priorizada que ajude a maximizar a conversão do time comercial.

### 3. Solution Strategy
Minha estratégia para resolver este desafio foi:

**Step 01. Data Description:**
A base de dados contém informações sobre os clientes, incluindo características como idade, gênero, histórico de seguro de saúde, entre outros. A variável alvo é a resposta à pesquisa sobre a compra do seguro de carro.

**Step 02. Feature Engineering:**
A partir das variáveis brutas, foram realizadas transformações como:
- Conversão de variáveis categóricas (como "vehicle_damage" e "vehicle_age") em variáveis binárias ou dummies.
- Codificação de variáveis como "gender", "region_code" e "policy_sales_channel" utilizando técnicas de Target Encoding e One-Hot Encoding.

**Step 03. Data Filtering:**
Filtragem de dados foi realizada para garantir que as variáveis relevantes fossem mantidas para o modelo de classificação, como "annual_premium", "vintage", "age", "region_code", "vehicle_damage", entre outras.

**Step 04. Exploratory Data Analysis (EDA):**
Uma análise exploratória dos dados foi realizada para identificar padrões, outliers e a distribuição das variáveis. Isso ajudou a entender melhor o comportamento dos clientes e a identificar tendências relevantes.

**Step 05. Data Preparation:**
A preparação dos dados envolveu a normalização de algumas variáveis, como "annual_premium", "age" e "vintage", utilizando scalers apropriados. Além disso, foi realizada a transformação das variáveis categóricas em formatos utilizáveis para o modelo.

**Step 06. Feature Selection:**
Foi realizada uma seleção de características com base na relevância das variáveis para o modelo de previsão. As variáveis selecionadas foram: "annual_premium", "vintage", "age", "region_code", "vehicle_damage", "previously_insured" e "policy_sales_channel".

**Step 07. Machine Learning Modelling:**
O modelo utilizado foi uma **Regressão Logística** para prever a probabilidade de um cliente comprar o seguro de automóvel com base nas características fornecidas. A probabilidade foi convertida em uma pontuação que foi usada para priorizar as ligações comerciais.

**Step 08. Model Evaluation:**
A performance do modelo foi avaliada utilizando as seguintes métricas:
- **Top-k Accuracy Score**: mede a taxa de acerto considerando os top-k clientes com maior probabilidade de conversão.
- **Commutative Curve**: curva que visualiza a evolução das previsões à medida que mais clientes são classificados.
- **Lift Curve**: curva que avalia a melhoria da precisão ao priorizar os clientes com maior probabilidade.
- **ROI Curve**: curva que relaciona o retorno sobre o investimento à medida que as ações comerciais são feitas com base na priorização.

**Step 09. Convert Model Performance to Business Values:**
A performance do modelo foi traduzida em valores de negócios, priorizando as 2.000 pessoas com maior probabilidade de conversão para serem contactadas pelo time comercial.

**Step 10. Deploy Model to Production:**
O modelo foi integrado a um script no Google Sheets, que calcula o **Propensity Score** de cada cliente. Com isso, é possível gerar uma lista ordenada dos clientes com maior potencial de compra, facilitando o trabalho do time comercial, que pode utilizá-la diretamente para priorizar as ligações.

![Demonstração do meu projeto](images/health_insurance_sheets.gif)

### 4. Top 3 Data Insights
1. **Clientes com idade entre 30 e 50 anos** apresentam maior propensão a comprar o seguro de automóvel.
2. **Clientes com histórico de "veículo danificado"** (indicando maior interesse em seguros) têm uma probabilidade significativamente maior de adquirir o novo produto.
3. **A variável "policy_sales_channel"** mostrou forte correlação com a decisão de compra, sugerindo que canais específicos têm mais sucesso em converter clientes.

### 5. Machine Learning Model Applied
O modelo utilizado foi uma **Regressão Linear**, que foi treinada para prever a probabilidade de um cliente comprar o seguro de automóvel com base nas características fornecidas. A probabilidade foi utilizada para classificar os clientes em ordem de prioridade para o time comercial.

### 6. Machine Learning Model Performance
O modelo foi avaliado utilizando as seguintes métricas:
- **Top-k Accuracy Score**: taxa de acerto ao priorizar os top-k clientes.
- **Commutative Curve**: mostra como a performance do modelo melhora conforme o número de clientes aumentam na lista de priorização.
- **Lift Curve**: quantifica a melhoria nas taxas de conversão à medida que priorizamos os clientes com maior pontuação.
- **ROI Curve**: avalia o retorno sobre o investimento da campanha de vendas conforme o time comercial realiza ligações baseadas nas previsões do modelo.

Essas métricas ajudaram a validar a eficácia do modelo na priorização dos 2.000 clientes com maior chance de conversão.

### 7. Business Results
- A lista de 2.000 clientes com maior probabilidade de conversão foi gerada com sucesso.
- Espera-se que a campanha de vendas atinja uma taxa de conversão de 10% ou mais, resultando em uma adição significativa à receita da empresa.

### 8. Conclusions
- A utilização de aprendizado de máquina para priorizar as ligações do time comercial aumentará a eficiência das campanhas de vendas.
- A segmentação de clientes com base nas características de comportamento e demográficas pode melhorar a eficácia das vendas do novo produto.
  
### 9. Lessons Learned
- A qualidade das variáveis de entrada é crucial para a performance do modelo. Variáveis mal processadas ou irrelevantes podem prejudicar os resultados.
- O modelo precisou ser ajustado várias vezes para otimizar as métricas de avaliação e melhorar a acurácia nas previsões.

### 10. Next Steps to Improve
- **Ajuste do modelo**: Testar diferentes algoritmos de aprendizado de máquina (como XGBoost ou Redes Neurais) para melhorar a precisão da previsão.
- **Expansão de dados**: Incorporar dados adicionais (por exemplo, comportamento de navegação no site ou histórico de interações com o time de vendas) para melhorar a segmentação.
- **Otimização de campanhas**: Utilizar as previsões do modelo para ajustar as campanhas em tempo real e aumentar a taxa de conversão.

### LICENSE
MIT License.
