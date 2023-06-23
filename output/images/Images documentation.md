Arquivo: `top_10_by_track_uniques.png`
Descrição: Gráfico de barras com os 10 artistas com mais faixas nos charts do período analisado
Base de dados: `top_10_artists_by_track.xlsx`
Processo:
1. `artist_names` como linha, `track_name` como coluna `medido` com `count distinct` (`CNTD(track_name)`)
2. `sort` pela coluna de contagem de `track_name`
3. `filter` `artist_names` por `top 10` por `track_name count distinct`
3. adição de paleta de cores, tamanho e ajuste de labels
4. Marcas: 
    - Cor: `CTND(Track_name)`
    - Label: ``CNTD(Track_name)`

---

Arquivo: `first_week_charts.png`
Base de dados: `refined.csv`
Processo documentado na heading `B` do [terceiro notebook](/notebooks/3_data_analysis.ipynb)
Descrição: Gráfico de barras com as top 10 faixas da semana entre 17 de junho de 2022 e 23 de junho de 2022.

---

Arquivo: `week_release_views.png`
Base de dados: `refined_with_first_week_release.xlsx`
Descrição: gráfico de círculos com as 25 músicas com mais views na semana de lançamento.
Processo: 
1. Filtro: Track Name, top 25, by views.
2. Filtro: Released in first week, True
3. Marks:
    - Label: 
        - Track name
        - SUM(views)
    - Color: SUM(views)
    - Size: SUM(views)

---

Arquivo: `yearly_views.png`
Base de dados: `yearly_data.xlsx`
Descrição: gráfico de barras "side-by-side" que mostra a média de visualizações por mês de cada ano e a soma de visualizações entre os mesmos meses (de fevereiro a junho)
Processo:
1. Coluna: Measure Values
2. Linha: Measure names, Year(Year)
3. Filtro: Measure Names
4. Marcas: Cor: Year(Year)
5. Measure Values:
    - SUM(Same Months)
    - SUM(Avg)

---
Arquivo: `frontlines_trend.png`
Base de dados: `refined.csv`
Descrição: Scatterplot com linha de regressão mostrando tendência para a quantidade de frontlines nos charts ao longo das semanas.
Processo: Processo documentado na heading `D` do [terceiro notebook](/notebooks/3_data_analysis.ipynb)

---

