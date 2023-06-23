
# Análise dos charts do YouTube Brasil das últimas 71 semanas.

## Introdução

Este repo foi desenvolvido como teste técnico para um processo seletivo para vaga de analista.

Deixei meus notebooks de exploração anexados junto ao projeto para que meu processo de pensamento seja visualizado pelos avaliadores, porém, nem todos os gráficos estão na entrega final, que deve ser a considerada.

Os relatórios finais se encontram no diretório `reports`, sob formato de [texto](reports/YouTube%20BR%20charts_textreport.pdf), [slide em pdf](reports/YouTube%20BR%20charts_slide.pdf) e [slide em ppt](reports/YouTube%20BR%20charts_slide.pptx).

Abaixo, as instruções para o desafio:

1 - **Montar base de dados com as top 100 faixas semanais de 07/02/22 até 02/06/23 do [Youtube Brasil](https://charts.youtube.com/charts/TopSongs/br?hl=pt)**.

2 - **Classificações**:
- Frontline: As faixas com menos de 42 meses de lançamento são consideradas `frontline`.
- Catálogo: São as faixas com 42 meses ou mais de lançamento.

3 - Análises:
As respostas deverão ser respondidas em um relatório em formato de email ou powerpoint. Foi optado formato .pdf/email.

- PERGUNTA 1: Qual o artista que mais teve faixas no Top 100 ao longo desses anos?

- PERGUNTA 2: Qual a posição mais alta que uma faixa atingiu na semana de seu lançamento? E qual foi a faixa? - ver published date

- PERGUNTA 3: Qual o ano teve o maior número de views no chart? E qual foi sua taxa de crescimento em relação ao ano anterior?

- PERGUNTA 4: Existe alguma tendência de crescimento ou queda do frontline no chart ao longo dos anos?

- PERGUNTA 5: Nossa impressão é que o tempo que as faixas permanecem no chart está diminuindo e com isso, mais faixas diferentes estão passando pelo chart. Com os dados extraídos, é possível comprovar essa afirmativa?

## Resultados

Os resultados estão expostos no arquivo `relatorio.pdf`, com as devidas visualizações e explicações. O notebook `3_data_analysis.ipynb` mostra o racional e o caminho para chegar nas respostas.

As respostas para as perguntas individuais são

1:  Henrique e Juliano, com 24 faixas.

2: A posição mais elevada é o primeiro lugar no ranking. Quem atingiu foi Zé Felipe e Mc Mari

3: Apresentamos duas métricas. Uma apresenta uma queda de -11,38% e outra um minúsculo crescimento de 0,10% de 2022 para 2023. Estão apresentadas nos relatórios.

4: Existe uma *levíssima* tendência de alta identificada por meio de uma linha de regressão linear.

5: Existe uma sutil tendência de queda no tempo que as faixas permanecem nos charts, com 1 semana a menos em 2023 em relação a 2022.

## Como rodar

1. Clone este repositório em sua máquina.
2. Reproduza o ambiente de execução em sua máquina:
	- Opção 1: certifique-se de ter o `python` e o gerenciador de pacotes `pip` instalados. Crie um ambiente `python -m venv <myenv>`, ative-o e reproduza o ambiente com o comando `pip install -r requirements.txt` em seu terminal.
	- Opção 2: instale o gerenciador de ambientes Conda em sua máquina. Recrie o ambiente com o comando `conda env create --file requirements.yml`. Ative o ambiente criado.
3. Configurando segredos:
	- Opção 1: Insira as variáveis `CHROME_DRIVER_PATH` e `DOWNLOAD_CHARTS_PATH` no `PATH` do windows. Eles deverão receber, respectivamente, o caminho do `webdriver.exe` e o caminho para a pasta de download dos arquivos.
	- Opção 2: Configure um arquivo `.env` com os caminhos `CHROME_DRIVER_PATH=` e `DOWNLOAD_CHARTS_PATH=` dentro deste diretório. Eles deverão receber, respectivamente, o caminho do `webdriver/`, diretório contido neste projeto, e o caminho para a pasta de download dos arquivos brutos `raw/`.
		- Se o `script` for executado dentro da pasta, o `.env` será executado automaticamente.
		- Caso opte por rodá-lo em `.py`, como nesse diretório, é necessário instalar a biblioteca `dotenv`. Digite `pip install python-dotenv` no terminal de seu ambiente de execução.
4. Abra a pasta de `notebooks` e insira, no `2_data_wrangling.ipynb`, a sua chave de acesso à `api` do `YouTube Data v3`. Saiba como gerar a sua [neste link](https://developers.google.com/youtube/registering_an_application?hl=pt-br). Após, remova a formatação `docstring` da célula.
	- Alternativamente, ignore esse passo e utilize os dados já capturados na pasta `raw`.
5. Inicie o script de raspagem `youtube_weekly_charts_scrapper.py` e rode os notebooks na pasta `notebooks` em ordem.



## Organização dos arquivos

```
.
├── data
│   ├── raw
│   ├── trusted
│   └── refined
├── notebooks
├── scripts
├── output
│   ├── tableau
│   └── images
├── webdriver
└── .env
└── requirements
│   ├── requirements.txt
│   └── environment.yml
└── reports
	├── YouTube BR charts_slide.pdf
	├── YouTube BR charts_slide.ppt
	└── YouTube BR charts_textreport.pdf
```

- **data**:
	- **raw**: Diretório para os arquivos baixados com o script de `scraping`
	- **trusted**: Diretório para os arquivos que compõem a base de dados.
	- **refined**: Diretório para a base de dados pronta para análise.
- **notebooks**:
	- `1_data_cleansing.ipynb`: notebook que recebe os arquivos `.csv` da pasta `raw` e os organiza em um dataset.
	- `2_data_wrangling.ipynb`: notebook que consome a `api` do YouTube `YouTube Data v3` para construir uma segunda base de dados e monta a base de dados para análise `refined.csv`
	- `3_data_analysis.ipynb`: notebook que busca responder as perguntas levantadas pelos `business` por meio de estatística descritiva e análise de dados.
- **output**:
	- **refined_for_tableau**: arquivos .`xlsx` para construir visualizações específicas no tableau
	- **imagens**: imagens de gráficos para serem exportadas para o report.pdf
- **webdriver**: diretório que armazena o `chromedriver.exe` para execução do `scrap`. O webdriver é uma ferramenta que permite automatização de tarefas a serem executadas em um navegador. Ele é compatível com google chrome.
- **requirements:** arquivos com lista de dependências em `.txt` para `pip` e `.yml` para o gerenciador de ambientes `conda`
	- requirements.txt
	- requirements.yml
- **reference_dates.json**: arquivo `.json` retirado da aba `networks` do `developer tools` da página que será raspada. Ele possui chaves `id`, `startTime` e `endTime`, que são usadas para filtrar os charts mostrados na página.
- **youtube_weekly_charts_scrapper.py**: arquivo que executa o `script` de `scraping`. O script utiliza a biblioteca `selenium` para navegar pelas diferentes `urls` dos charts e baixar os `.csvs` brutos que permitirão a análise. A página possui um objeto javascript filtrado por semana e por número de views. A diferença das `urls` são as datas, que são compostas pela data de abertura e a data de fechamento da semana em formato YYYY-MM-DD. O script identifica o botão de douwnload e baixa um arquivo `.csv`. Após o download, o arquivo é lido com a biblioteca pandas, adiciona uma coluna numérica para referenciar a semana (`week_ref`), uma contendo a data de abertura da semana (`week_open`) e outra contendo a data de fechamento (`week_close`). Ao final, o script imprime seu tempo de execução, a quantidade de arquivos baixados e o tempo médio de execução por arquivo baixado.