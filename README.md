### **📊 Projeto de Análise de Dados:**

#### **1\. Compreensão do Negócio (Business Understanding) 📈**

**Objetivo:**

Neste projeto, assumirei a função de Cientista de Dados/Analista de Dados trabalhando para uma nova empresa de investimentos em startups que ajuda os clientes a investir seu dinheiro em ações. O objetivo do trabalho é extrair dados financeiros, como histórico de preços de ações e relatórios de receita trimestrais de várias fontes, usando bibliotecas Python e webscraping em ações populares. Depois de coletar esses dados, os visualiza em um painel para identificar padrões ou tendências. As ações com as quais trabalhamos são Tesla, Amazon, AMD e GameStop.

Ações Realizadas:

Extração de dados de ações das empresas:
Amazon
AMD
Tesla
GameStop
Extração de dados de receita das empresas:
Tesla
GameStop
Criação de um painel de controle de ações e receita das empresas:
Tesla
GameStop

* Criação de Painel de Controle:

	* Desenvolvemos um painel interativo para visualizar os dados coletados.
 	* O painel permite análises comparativas, identificação de tendências e tomada de decisões informadas.

#### **2\. Compreensão dos Dados (Data Understanding) 🧐**

Para realizar uma análise abrangente, utilizamos duas fontes de dados: a API YFinance, que fornece dados financeiros atualizados, e páginas web que contêm dados de receitas das empresas Tesla e GameStop.

Dados de Ações Financeiras(Api YFinance):

Data de Registro (Date): Data em que os dados foram registrados. É importante para contextualizar as informações adquiridas e entender o comportamento do mercado naquele determinado momento. Eventos macroeconômicos, notícias corporativas ou mudanças nas políticas podem gerar reações de mercado específicas que se refletem nos dados de cada dia. Compreender esse contexto ajuda a analisar as razões por trás das flutuações e tendências dos preços.

Valor de Abertura (Open): Preço da ação no início do período de negociação. Pode ser um indicativo de como estão os sentimentos do mercado naquele dia, ou seja, como os investidores estão reagindo a determinados eventos recentes. Comparado com o fechamento do dia anterior, pode identificar gaps (diferenças significativas), que podem representar oportunidades ou riscos, dependendo das estratégias adotadas.

Valor Mais Alto (High): Preço máximo alcançado pela ação durante o período. Esse valor pode identificar níveis de resistência (preços que impedem a ação de subir mais) e determinar a volatilidade do dia, além de identificar potenciais pontos de venda das ações.

Valor Mais Baixo (Low): Preço mínimo alcançado pela ação durante o período. Ajuda a identificar os níveis de suporte (preços que impedem a ação de cair mais), a determinar potenciais pontos de compra e também é útil para avaliar a volatilidade.

Preço de Fechamento (Close): Preço da ação ao fechar o período de negociação. É usado para calcular indicadores técnicos e é frequentemente comparado com o preço de abertura para identificar movimentos de alta ou baixa.

Volume: Número total de ações negociadas. É um indicador de liquidez e interesse do mercado. Volumes altos podem confirmar a força de uma tendência, enquanto volumes baixos indicam falta de interesse ou incertezas. O volume é essencial para analisar a oferta e a demanda, influenciando diretamente os preços.

Dividendos (Dividends): Pagamentos feitos aos acionistas. Podem influenciar o preço da ação, já que o valor do dividendo é geralmente descontado do preço da ação na data de ex-dividendo.

Desdobramentos de Ações (Stock Splits): Alterações na quantidade de ações em circulação. Podem influenciar a percepção dos investidores e, consequentemente, o preço da ação.


**Amazon**:

![Amazon](https://github.com/user-attachments/assets/e4a20b8f-9eea-4b74-b2af-c76b63e91718)


**AMD**:

![amd](https://github.com/user-attachments/assets/9f6bc064-e91f-4d49-91fe-8aa115303891)


**GameStop**:


![GameStop](https://github.com/user-attachments/assets/35b232e3-7663-456f-9636-4846b8b1255e)

**Tesla**:

![Tesla](https://github.com/user-attachments/assets/664864d5-7256-4e6c-a8b9-0cc5e8261cfd)


Dados de Receitas(Extraído da Web):

Além dos dados financeiros, extrai também informações das receitas das empresa, que incluem:

* Data de Registro(Date): Data que foi feito o registro da receita;  
* Receita(Revenue): Total de Receita gerada pela empresa em um determinado período

**GameStop:**


![GameStop](https://github.com/user-attachments/assets/e71a308e-ebc4-44fe-9dd3-d0acf72c9ef6)

**Tesla:**

![Tesla](https://github.com/user-attachments/assets/93593725-4a4d-486d-bce3-bb29841bd830)



#### **3\. Preparação dos Dados (Data Preparation) 🛠️**

Para a extração dos dados para analisar os dados financeiros, a linguagem Python.

Para extrair os dados de ações financeiras utiliza a api Yfinance e para extrair os dados na Web vamos utilizar a web scraping através do BeautifulSoup.

Código Utilizados:

Para acessar as informações das ações das empresas utiliza o ***Ticker*** e depois o código da empresa.

					x = yf.Ticker("codigo_empresa")

Os códigos de cada empresa são:

* Apple: “**APPL”**;  
* AMD: “**AMD”;**  
* Amazon**: “AMZN”;**  
* Tesla**: “TSLA”;**  
* GameStop**: “GME”**


Para pegar os históricos dos valores de cada empresa é utilizado o ***History*** e o “*period”* para pegar o período desejado, no caso, foi retirado pelo período máximo, desde o início.

					y = x.history( period=”max” )

**Extração de Dados da Web**

Através do endereço eletrônico  utilizo o “request” para solicitar as informações do HTTP.

					html_data = request.get(url).text 

O “*BeautifulSoup*” lê as informações do conteudo pego anteriormente, criando um objeto.

					soup = BeatigulSoup(html_data, ‘html.parser’)

Utiliza o “*find_all(‘table”)* para buscar todas as tabelas e guarda em tables.

					tables = soup.find_all(‘table’)

Para ser feito a análise, é necessário a criação de um DataFrame com as informações desejadas, com isso, utiliza o pandas para criar um DataFrame vazio:

					nome_revenue = pd.DataFrame(columns=[“Date”, “Revenue”])

O Data Frame tem as colunas Data(Date), Receita(Revenue).

Após isso é percorrido as tabelas guardadas no *tables* e busca a tabela com o nome *"GameStop Quarterly Revenue"*.

					for table in tables:

						if “GameStop Quarterly Revenue" in table.get_text():

Então é realizado o mapeamento do código html, e é buscado as colunas da tabela desejada e guardadas nas variáveis date e revenue.

					tbody = table.find(‘tbody’)

					for row in tbody.find_all(‘tr’):

					columns = row.find_all('td')**

						if columns:

							date = columns[0].get_text()

							revenue = columns[1].get_text()

E antes de guardar essas informações foi pedido para ser feito uma primeira limpeza, na qual, os cifrões e as vírgulas eram para retirar no dados de *revenue*, antes de adicionarmos ao DataFrame foi feito a limpeza utilizando o replace:

		 			revenue = revenue.replace(‘$’, ‘’).replace(“,” ,” ”)

Com os dados limpos é adicionado ao Data Frame:

					new_row = pd.DataFrame({“Date”}: [date], “Revenue”: [revenue]})

					nome_revenue* = pd.concat([gme_revenue, new_row], ignore_index=True)

O código completo ficou assim:

					html_data = request.get(url).text

					soup = BeatigulSoup(html_data, ‘html.parser’)

					tables = soup.find_all(‘table’)

					nome_revenue = pd.DataFrame(columns=[“Date”, “Revenue”])

					for table in tables:

						if “GameStop Quarterly Revenue" in table.get_text():

							tbody = table.find(‘tbody’)

							for row in tbody.find_all(‘tr’):

									columns = row.find_all('td')

										if columns:

											date = columns[0].get_text()

											revenue = columns[1].get_text()

 											revenue = revenue.replace(‘$’, ‘’).replace(“,” ,” ”)

											new_row = pd.DataFrame({“Date”}: [date], “Revenue”: [revenue]})

											nome_revenue = pd.concat([gme_revenue, new_row], ignore_index=True)

**Limpeza:**

Para garantir que os dados numéricos sejam manipulados corretamente em análises e cálculos, é essencial remover quaisquer caracteres não numéricos, como cifrões e vírgulas, que podem ser interpretados de forma errada por softwares de processamento de dados. A conversão de valores irá transformar valores monetários em numéricos, para ajudar em operações matemáticas sem erros.
Foi utilizado o “replace” para realizar essa conversão.

					revenue = revenue.replace(‘$’, ‘’).replace(“,” ,” ”)

A limpeza de dados é uma etapa fundamental no processo de análise de dados, pois dados imprecisos ou incompletos podem levar a conclusões errôneas e afetar negativamente as decisões empresariais. Remover valores nulos e vazios é essencial para manter a integridade dos dados, permitindo que futuramente façam algoritmos de aprendizado de máquina e modelos estatísticos que funcionem com a máxima eficiência. Este processo não só melhora a qualidade dos insights obtidos, mas também fortalece as estratégias de negócios ao se basear em informações confiáveis. Ao garantir que os dados estejam limpos e precisos, as organizações podem otimizar recursos, identificar oportunidades de mercado e mitigar riscos de forma mais eficaz.

					nome_revenue.dropna(inplace=True)

					nome_revenue = nome_revenue[nome_revenue[‘Revenue’] != “”]

Utilizo o **reset_index(inplace=True)** para redefinir o índice de um DataFrames para o padrão númerico, o que facilita diversas operações, como a concatenação de tabelas, filtros e outras transformações. Ao remover o índice baseado em data, você ganha mais flexibilidade para manipular os dados sem restrição.

					variavel.reset_index(inplace=True)

		

### **4\. Tecnologias, Linguagens de Programação e Bibliotecas 🔧**

Web Scraping: A técnica é utilizada para extração de informações de uma páginas webs, permitindo a coleta de dados para gerar insights poderosos. Neste projeto utilizou para a extração de informações em duas páginas webs distintas em HTML, conseguindo extrair as tabelas desejadas para análise.

Python: É utilizado devido à sua simplicidade e robustez, além da sua vasta gama de bibliotecas para análise de dados, permitindo ações de coleta, visualização e manipulação de dados, tornando o processo mais eficiente, acessível.

Plotly: É uma biblioteca Python feita para criação de gráficos, e foi utilizada para plotar os gráficos do projeto, facilitando a interpretação dos dados. Fazendo com que ao explorar os dados se torne intuitivo.

Pandas: É amplamente utilizado nas análises de dados, pois, tem uma gama de funcionalidades poderosíssimas para trabalhar com dados tabulares, como em planilhas e Banco de Dados. Facilitando o trabalho de manipulação, carregamento e análise de grandes volumes de dados, permitindo a extração de insights valiosíssimos.

Yfinance: API para acessar as informações financeiras atualizadas de diversas empresas.

Beautiful Soup: Biblioteca que facilita a extração de informações de páginas webs, com sua capacidade de analisar HTML e XML, permitindo navegar pelo código de forma eficiente e identificando e extraindo informações de forma precisa, otimizando o processo de coleta de dados.

Request: Biblioteca Python para fazer requisições HTTP. Essa funcionalidade é vital para integrar diversas fontes de dados e garantir que as informações estejam atualizadas.

Matplotlib: Usado para criar visualizações estatísticas interativas, para apresentar os dados de forma clara e envolvente. 

**5\. Resultados Finais e Insights 💡**

A análise financeira é uma ferramenta essencial para orientar decisões de investimento. Nesse contexto, desenvolvemos três gráficos detalhados para cada uma das seguintes empresas: Amazon, AMD, Apple, GameStop e Tesla. Esses gráficos exploram os dados financeiros até o momento, identificando padrões significativos que podem informar estratégias tanto a curto quanto a longo prazo.

Gráfico de Linha de Abertura

O gráfico de linha de abertura vai oferecer uma visão clara das trajetórias inicial dos preços das ações em um período, nesse caso, até o determinado momento. Este gráfico é útil para identificar tendências de abertura e padrões de comportamento dos ativos logo no início do pregão, podendo indicar como se comporta ao longo do dia.

Gráfico de Candlestick

Uma ferramenta essencial na análise técnica de mercados financeiros, como ações, moedas e commodities. Cada “candle” ou vela no gráfico representa os preços de abertura, fechamento, valor máximo e valor mínimo de um ativo, no caso do deste projeto até o atual momento, fornecendo uma visão detalhada da volatilidade do mercado e das tendências de preço. A cor e o tamanho do candle, oferecem pistas sobre a pressão de compra e venda e podem indicar reversões de tendências ou continuidade do movimento atual. A cor verde representa que as ações cresceram, já os candles de cor vermelha houve queda nas ações.

Gráfico de Área dos Preços de Ações(Area Chart)

Oferecem uma visualização clara da evolução dos preços dos preços ao longo do tempo, permitindo aos investidores identificar tendências e padrões no comportamento de mercado. Representa o preço do fechamento com um preenchimento em azul, o preço de abertura na cor amarela, na cor verde o valor máximo e na cor vermelha valor baixo, ajudando a destacar os volumes de negociações. Ajudando a discernir períodos de alta volatilidade e liquidez, fornecendo insights valiosos para decisão de compra e venda.


**Amazon**

![fechamento](https://github.com/user-attachments/assets/1adf259e-19ae-491a-b761-f80cedc66de3)

![Gráfico de Candlestick](https://github.com/user-attachments/assets/de489cc5-fa83-4210-9d50-82936184fdf9)

![Gráfico de Área dos Preços de Ações](https://github.com/user-attachments/assets/441460e4-4f53-421c-a701-5374ed900ac1)

A análise da Amazon revela uma tendência geral de alta, com crescimento acentuado iniciado após 2010. Este período é marcado por uma volatilidade crescente e oscilações diárias mais significativas, contratando com estabilidade observada antes de 2010. As correções de mercado após picos notáveis são cruciais para avaliar a sustentabilidade de tendência de alta. Em particular, o ano 2023 destaca-se por um pico seguido de uma correção acentuada, indicando uma possível resistência. Essas flutuações são indicativos importantes para compreender as dinâmicas do mercado e antecipar movimentações futuras.


**AMD**

![fechamento](https://github.com/user-attachments/assets/9e032a34-ae7f-4b0d-a590-ba256979cf36)

![Gráfico de Candlestick](https://github.com/user-attachments/assets/25c1f0da-ffbe-4868-9dac-4700c624874e)

![Gráfico de Área dos Preços de Ações](https://github.com/user-attachments/assets/76bb801c-f25e-481a-b0fc-f4ec34f2ab93)


AMD tem um período de estabilidade de 1995 até 2005, com variações mínimas, indicando um mercado menos volátil e mais previsível, a partir de 2005 a volatilidade aumentou significativamente, refletindo em possíveis mudanças no cenário econômico.
Após 2013 a volatilidade dos preços intensificou-se, com oscilações de altos e baixos, o que pode ser interpretado como uma resposta a eventos globais ou mudanças nas políticas monetárias.
A partir de 2016, nota-se uma tendência de alta nos preços de abertura das ações, culminando após 2020 com um valor máximo de 200. E depois uma oscilação constante.


**Gamestop**

![fechamento](https://github.com/user-attachments/assets/54221f8e-9f45-452b-8dd5-16135baf65c7)

![Gráfico de Candlestick](https://github.com/user-attachments/assets/a77ec2d7-816c-4a25-a389-8b5c69e5172d)


![Gráfico de Área dos Preços de Ações](https://github.com/user-attachments/assets/8ef5dc7e-f860-4451-b1c5-468298e010ad)


A GameStop entre 2005 e 2015, observou-se um período de estabilidade, com preços variando minimamente entre 0 e 20. Esta fase pode indicar um mercado equilibrado, sem grandes choques de oferta ou demanda. No entanto, a partir de 2015, começou-se a notar um aumento gradual. A situação se intensificou após 2018, com uma alta acentuada nos preços, atingindo um pico de 120 em 2020.. A volatilidade observada após 2020, com uma queda brusca nos preços, reforça a natureza imprevisível do mercado e a importância de uma análise contínua para entender as forças que o movem.


**Tesla**

![fechamento](https://github.com/user-attachments/assets/17387669-3cad-42eb-bba0-444cf5fe396e)

![Gráfico de Candlestick](https://github.com/user-attachments/assets/47481614-3d1f-417f-87dc-defb577d20ec)

![Gráfico de Área dos Preços de Ações](https://github.com/user-attachments/assets/f7cd0deb-3678-40b0-b635-c670937f856c)

Observa-se um período de estabilidade de preços entre 2010 a 2016, em seguida por um aumento gradual entre 2016 a 2018, com algumas flutuações notáveis. A partir de 2018, nota-se uma tendência de alta acentuada, culminando em um pico em 2020, onde os valores atingiram o máximo de 400.  Esses movimentos de preços podem refletir mudanças no mercado ou na economia que requerem uma análise mais aprofundada para compreender as causas subjacentes e as possíveis implicações para o futuro.

**Painéis**

Foi criado dois paineis para comparar as receitas com o valor de ações das empresas Tesla e GameStop

Tesla

![tesla](https://github.com/user-attachments/assets/ebc204b3-5489-4ee8-b3a6-d46fe41925b6)

O painel fornece uma análise da trajetória da Tesla, destacando a relação entre receita e valorização das ações. Essa correlação positiva indica que a empresa mantém uma trajetória de crescimento e que suas estratégias de negócios têm sido bem-sucedidas. Mostrando que aumentou seu valor de mercado e expandiu suas operações e receitas ao longo dos anos.

GameStop

![gamestop](https://github.com/user-attachments/assets/8029f453-7fc0-4425-95a0-382b4debbf96)

A trajetória da GameStop mostra uma estabilidade dos preços das ações seguindo por um aumento repentino, o que pode refletir uma mudança significativa na percepção do mercado ou na estratégia da empresa. Por outro lado, a receita já mostra um padrão mais consistente, sugerindo uma operação com fluxos de receitas mais previsíveis, apesar das flutuações do mercado.. Essa discrepância entre o preço das ações e a receita pode indicar oportunidades e riscos, e é por isso que uma análise aprofundada é essencial para os investidores que buscam tomar decisões informadas baseadas em dados históricos e tendências atuais.

**## Conclusão**

A análise das ações financeiras de cada empresa neste projeto é crucial para a criação de estratégias eficazes de compra e venda de ações, bem como estratégias de investimentos. Para isso, é fundamental contar com uma linha do tempo detalhada das ações da empresa, permitindo entender seu ao longo do tempo e em relação a eventos atuais. Isso oferece ao investidor uma visão contextualizada e é vital para a formulação de estratégias robustas.

Este projeto demonstra como realizar a coleta e análise de dados, usando a APIi no caso a Yfinnance e da técnia de WebScrapping, uma metodologia essencial para extrair informações de páginas web. Utilizando essas ferramentas, o projeto entrega insights valiosos por meio de gráficos e paineis comparativos. No entanto, é importante observar que este é um projeto de simulação, destinado a demonstrar o processo e os potenciais insights, não sendo uma recomendação direta de investimento.

A entrega de projetos que fornece informações precisas e atualizadas é crucial para capacitar investidores. Com acesso a dados relevantes, eles podem realizar análises mais profundas do mercado financeiro e assim tomar decisões e criar melhores estratégias.Essa prática traz mais confiança aos clientes da empresa, pois, terão estratégias criadas a partir de dados concretos e confiáveis.

A análise financeira é uma parte crucial do investimento em startups. Este projeto propostas não apenas fornecer uma solução técnica para a coleta e análise de dados, mas também equipar os investidores com as ferramentas necessárias para fazer escolhas informadas e estratégicas. Se desenvolvido, esta ferramenta contribuirá para a valorização do sucesso do investidor no mercado mutável e volúvel da startup.
