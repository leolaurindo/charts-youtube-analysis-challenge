
# Análise dos charts do YouTube Brasil das últimas 71 semanas.

## Introdução

Este repo foi desenvolvido como teste técnico para um processo seletivo para vaga de analista júnior.

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

## Como rodar

1. Clone este repositório em sua máquina.
2. Reproduza o ambiente de execução em sua máquina:
	- Opção 1: certifique-se de ter o `python` e o gerenciador de pacotes `pip` instalados. Crie um ambiente `python -m venv myenv`, ative-o e reproduza o ambiente com o comando `pip install -r requirements.txt` em seu terminal.
	- Opção 2: instale o gerenciador de ambientes Conda em sua máquina. Recrie o ambiente com o comando `conda env create --file requirements.yml`. Ative o ambiente criado.
3. Configurando segredos:
	- Opção 1: Insira as variáveis `CHROME_DRIVER_PATH` e `DOWNLOAD_CHARTS_PATH` no `PATH` do windows. Eles deverão receber, respectivamente, o caminho do `webdriver` e o caminho para a paste de download dos arquivos.
	- Opção 2: Configure um arquivo `.env` com os caminhos `CHROME_DRIVER_PATH=` e `DOWNLOAD_CHARTS_PATH=` dentre deste diretório. Eles deverão receber, respectivamente, o caminho do `webdriver` e o caminho para a paste de download dos arquivos.
		- Se o `script` for executado dentro da pasta, o `.env` será executado automatica.
		- Caso opte por rodá-lo em `.py`, como nesse diretório, é necessário instalar a biblioteca `dotenv`. Digite `pip install python-dotenv` no terminal de seu ambiente de execução.
4. Abra a pasta de `notebooks` e insira, no `2_data_wrangling.ipynb`, a sua chave de acesso à `api` do `YouTube Data v3`. Saiba como gerar a sua [neste link](https://developers.google.com/youtube/registering_an_application?hl=pt-br). Após, remova a formatação `docstring` da célula.
	- Alternativamente, ignore esse passo e utilize os dados já capturados na pasta `raw`.



## Organização dos arquivos

```
.
├── data
│   ├── raw
│   ├── processed
│   └── external
├── notebooks
├── scripts
├── output
│   ├── tableau
│   └── images
├── webdriver
└── .env
└── requirements
│   ├── requirements.txt
│   └── requirements.yml

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
- **webdriver**: diretório que armazena o `webdriver` para execução do `scrap`
- **requirements:** arquivos com lista de dependências em `.txt` para `pip` e `.yml` para o gerenciador de ambientes `conda`
	- requirements.txt
	- requirements.yml
- **reference_dates.json**: arquivo `.json` retirado da aba `networks` do `developer tools` da página que será raspada. Ele possui chaves `id`, `startTime` e `endTime`, que são usadas para filtrar os charts mostrados na página.