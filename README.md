### **📊 Projeto de Análise de Dados:**

#### **1\. Compreensão do Negócio (Business Understanding) 📈**

**Objetivo:**

Nesse projeto assumirei um trabalho em uma empresa de investimentos em startups que ajuda os clientes a investir seu dinheiro em ações. A ideia é extrair dados financeiros como histórico de preços e ações e relatórios de receita trimestrais de várias fontes. Depois realizar a criação de um painel para identificar padrões ou tendências. As ações trabalhadas serão da Apple, Tesla, Amazon, AMD e GameStop.  
Foi realizado as seguintes ações:

* **Extração de dados de ações das empresas**:  
  * Amazon;  
  * AMD;  
  * Apple;   
  * Tesla;  
  * GameStop

* **Extração de dados de receita das empresas:**  
  * Tesla;  
  * GameStop

* **Painel de controle de ações e receita da empresas:**  
  * Tesla;  
  * GameStop

#### **2\. Compreensão dos Dados (Data Understanding) 🧐**

Para realizar uma análise abrangente utilizamos duas fontes de dados: uma base extraída da API YFinance que fornece dados financeiros atualizados e duas páginas web que contêm dados de receitas das empresas Tesla e GameStop.

.

Dados de Ações Financeiras(Api YFinance):

* Data de Registro(Date): Data que os dados foram registrados;  
* Valor de Abertura(Open): Preço que ação tinha no início do período de negociação;  
* Valor Mais Alto(High): Preço máximo alcançado pela ação durante o período;  
* Valor Mais Baixo(Low): Preço mínimo alcançado pela ação durante o período;  
* Preço de Fechamento(Close): Preço que ação tinha ao fechar o periodo de negociação;  
* Volume: Número total de ações negociadas;  
* Dividendos (Dividends): Pagamentos feitos aos acionistas.  
* Desdobramentos de Ações (Stock Splits): Alterações na quantidade de ações em circulação.

**Amazon**:

![Amazon](https://github.com/user-attachments/assets/e4a20b8f-9eea-4b74-b2af-c76b63e91718)


**AMD**:

![amd](https://github.com/user-attachments/assets/9f6bc064-e91f-4d49-91fe-8aa115303891)


**Apple**:

![apple](https://github.com/user-attachments/assets/bde47363-8578-4650-adf9-4623e9c1aa21)


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

 Para extrair os dados de ações financeiras utiliza a  api Yfinance e para extrair os dados na Web vamos utilizar o web scraping através do BeautifulSoup.

Código Utilizados:

Para acessar as informações das ações das empresas utiliza o ***Ticker*** e depois o código da empresa.

		***x \= yf.Ticker("codigo\_empresa")***

Os códigos de cada empresa são:

* Apple: “**APPL”**;  
* AMD: “**AMD”;**  
* Amazon**: “AMZN”;**  
* Tesla**: “TSLA”;**  
* GameStop**: “GME”**


Para pegar os históricos dos valores de cada empresa é utilizado o ***History*** e o “*period”* para pegar o período desejado, no caso, foi retirado pelo período máximo, desde o início.

		**y \= x.history( period=”max” )**

**Extração de Dados da Web**

Através do endereço eletronico utilizo o “request” para solicitar as informações do HTTP.

		***html\_data \= request.get(url).text*** 

O “*BeautifulSoup*” lê as informações do conteudo pego anteriormente, criando um objeto.

		***soup \= BeatigulSoup(html\_data, ‘html.parser’)***

Utiliza o “*find\_all(‘table”)* para buscar todas as tabelas e guarda em tables.

		***tables \= soup.find\_all(‘table’)***

Para ser feito a análise, é necessário a criação de um DataFrame com as informações desejadas, com isso, utiliza o pandas para criar um DataFrame vazio:

		***nome\_revenue \= pd.DataFrame(columns=\[“Date”, “Revenue”\])***

O Data Frame tem as colunas Data(Date), Receita(Revenue).

Após isso é percorrido as tabelas que foram guardadas no *tables* e busca a tabela com o nome *"GameStop Quarterly Revenue"*.

		**for table in tables:**

			**if “*GameStop Quarterly Revenue"* in table.get\_text():**

Então é realizado o mapeamento do código html, e é buscado as colunas da tabela desejada e guardadas nas variáveis date e revenue.

			**tbody \= table.find(‘tbody’)**

			**for row in tbody.find\_all(‘tr’):**

			**columns \= row.find\_all('td')**

				**if columns:**

					**date \= columns\[0\].get\_text()**

					**revenue \= columns\[1\].get\_text()**

E antes de guardar essas informações foi pedido para ser feito uma primeira limpeza, na qual, os cifrões e as vírgulas eram para ser retirados no dados de *revenue*, antes de adicionarmos ao DataFrame foi feito a limpeza utilizando o replace:

		 **revenue \= revenue.replace(‘$’, ‘’).replace(“,” ,” ”)**

Com os dados limpos é adicionado ao Data Frame:

			**new\_row \= pd.DataFrame({“Date”}: \[date\], “Revenue”: \[revenue\]})**

			***nome\_revenue* \= pd.concat(\[gme\_revenue, new\_row\], ignore\_index=True)**

O código completo ficou assim:

		***html\_data \= request.get(url).text*** 

***soup \= BeatigulSoup(html\_data, ‘html.parser’)***

***tables \= soup.find\_all(‘table’)***

***nome\_revenue \= pd.DataFrame(columns=\[“Date”, “Revenue”\])***

**for table in tables:**

**if “*GameStop Quarterly Revenue"* in table.get\_text():**

**tbody \= table.find(‘tbody’)**

				**for row in tbody.find\_all(‘tr’):**

					**columns \= row.find\_all('td')**

**if columns:**

						**date \= columns\[0\].get\_text()**

						**revenue \= columns\[1\].get\_text()**

 						**revenue \= revenue.replace(‘$’, ‘’).replace(“,” ,” ”)**

**new\_row \= pd.DataFrame({“Date”}: \[date\], “Revenue”: \[revenue\]})**

						***nome\_revenue* \= pd.concat(\[gme\_revenue, new\_row\], ignore\_index=True)**

Limpeza:

Além da limpeza mostrada no item acima para a retirada do cifrão e vírgulas:

		**revenue \= revenue.replace(‘$’, ‘’).replace(“,” ,” ”)**

foi retirado também os valores nulos e vazios.

		**nome\_revenue.dropna(inplace=True)**

		**nome\_revenue \= nome\_revenue\[nome\_revenue\[‘Revenue’\] \!= “”\]**

Foi realizado também o reset do index das tabelas de ações, que vinha com a data como index, o que atrapalha na hora de fazer alguma manipulação, usando o **reset\_index(inplace=True)**

		**variavel.reset\_index(inplace=True)**

		

### **4\. Tecnologias, Linguagens de Programação e Bibliotecas 🔧**

Web Scraping: A técnica é utilizada para extração de informações de uma páginas Web, permitindo a coleta de dados para gerar insights poderosos.Neste projeto utilizou para a extração de informações em duas páginas Web distintas em HTML, conseguindo extrair as tabelas desejadas para análise.

Python: É utilizado por causa da sua simplicidade e robustez, além da sua vasta gama de bibliotecas para análise de dados, permitindo ações de coleta, visualização e manipulação de dados, tornando o processo mais eficiente, acessível..

Plotly: É uma biblioteca Python feita para criação de gráficos, e foi utilizada para plotar os gráficos do projeto, facilitando a interpretação dos dados. Fazendo com que ao explorar os dados se torne intuitivo.

Pandas: É amplamente utilizado nas análises de dados, pois, tem uma gama de funcionalidades poderosíssimas para trabalhar com dados tabulares, como em planilhas e Banco de Dados. Facilitando o trabalho de manipulação, carregamento e análise de grandes volumes de dados, permitindo a extração de insights valiosíssimos.

Yfinance: Api para acessar as informações financeiras atualizadas de diversas empresas.

Beautiful Soup: Biblioteca que facilita a extração de informações de páginas Web, com sua capacidade de analisar HTML e XML, permitindo navegar pelo código de forma eficiente e identificando e extraindo informações de forma precisa, otimizando o processo de coleta de dados.

Request: Biblioteca Python para fazer requisições HTTP. Essa funcionalidade é vital para integrar diversas fontes de dados e garantir que as informações estejam atualizadas.

Matplotlib: Usado para criar visualizações estatísticas interativas, para apresentar os dados de forma clara e envolvente. 

**5\. Resultados Finais e Insights 💡**

Foi desenvolvido 3 gráficos para cada empresa(Amazon, AMD, Apple, GameStop, Tesla), analisando os dados financeiros até o presente momento. 

* O gráfico de fechamento   
  * Mostra o fechamento das ações ao longo do tempo;  
  * Útil para identificar tendência de alta

**Apple**

**![][image8]**

**AMD**

**![][image9]**

**Amazon**

**![][image10]**

**Gamestop**

**![][image11]**

**Tesla**

![][image12]

* Gráfico de Candlestick   
  * Ideal para identificar padrões de reversão ou continuação de tendência;  
  * Utiliza dados de .preço de abertura, fechamento, máxima e mínima das ações;  
  * Cada “candle” (candelabro) representa um período (por exemplo, um dia) e mostra visualmente as variações.

Apple

![][image13]  
Amazon  
![][image14]  
AMD  
![][image15]

GameStop  
![][image16]  
Tesla  
![][image17]

* Gráfico de Área dos Preços de Ações(Area Chart):  
  * Destaca a variação dos preços das ações com base nos valores de abertura, fechamento, preço mais alto e preço mais baixo;  
  * É uma maneira eficaz de visualizar como esses valores se relacionam ao longo do tempo.

Apple  
![][image18]

Amazon

![][image19]  
AMD

![][image20]

GameStop

![][image21]

Tesla

![][image22]

Foi criado dois paineis para comparar as receitas com o valor de ações das empresas Tesla e GameStop

Tesla

![][image23]

GameStop

![][image24]

