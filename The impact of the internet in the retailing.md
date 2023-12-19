## 1 PREPARATION
### 1.1 BUSINESS OBJECTIVE 
The advent of information and communication technologies (ICTs) has radically redefined human life, shaping new meanings and practices. This revolution has triggered significant changes at the political, social and economic levels, pushing toward a socio-economic restructuring of established behavioral patterns.
The heart of this thesis focuses on analyzing how businesses, in response to this scenario of change, have been directed and supported by the irruption of ICT in retailing. This transformation has led to the emergence of business models based entirely on these technologies. The revolution in the concept of "e-tailing" became firmly established in the late 1990s, outlining a process of selling goods and services that encompasses the entire interaction with the customer, from the initial stage to the conclusion of transactions, via the Internet.  
Retailing, originally associated with the distribution channel alone, has moved beyond its traditional definition to evolve into a business system based on digital platforms. A crucial element in this scenario is the affirmation of the value of data. Recognizing the potential richness inherent in information, businesses are called upon to develop targeted strategies for its collection and use. This process not only determines the information needed, but also helps shape the business value proposition, improving its performance and reducing the costs associated with investment. Through this thesis, we will explore the dynamics that have redefined the retailing landscape, focusing on the challenges and opportunities offered by ICT. With a close look at history and future prospects, we will analyze how businesses have adapted to this accelerated change, painting a comprehensive picture of the transformations that are redefining the world of retailing.

### 1.2 HOW TO GET THERE 
The basis of this research is established market data. We will begin with a general analysis of the global context in which the phenomenon has developed, and then gradually descend into detail, bringing the magnifying glass closer to a single sector and then to a specific company. The focus will be on the Appareal sector, with specific insight into the sportswear segment, particularly when we discuss Nike Inc.
The choice to focus on Nike Inc. was determined, first of all, by its adoption of a business plan that is a perfect concrete example for our study. Moreover, the company was selected because of its remarkable economic and, in part, social achievements in recent years. This decision allows us to go beyond simplistic general assumptions and base our answers on specific company data.

## 2 DATA USED 
### 2.1 DATA USED AND DATA LIMITATION
The fundamentals of this research draw market and sector data from Statista, a reliable source used for global market analysis. Statista already organizes and aggregates the data, ensuring, however, their reliability. The source and methodology are described in the reports, strengthening the reliability of the information. However, it should be noted that there is no direct access to sufficiently recent microdata (the least dated free data date back to 2007). This in my opinion for privacy reasons, therefore related to the purposes with which the data were collected by the company and, for this reason, not disclosed in an non-aggregate manner. Another reason, much more marked, concerns the economic value that these data assume. This limitation may be an obstacle to our research, but by analyzing it from a different point of view, it can become an argument in favor of our thesis. It represents how much the introduction of the internet has changed the economic and commercial scheme, transforming the same data in exchangeable assets and, consequently, a source of direct or indirect gain for the companies.
As for the data relating to Nike, I found them directly from the annual reports 10k published by the company itself, aimed at shareholders. This source offers a detailed insight into Nike’s financial performance. It should be noted that the data are divided into business years, starting in June and ending on May 31 of the following year.

### 2.2 DATA ORGANIZATION, VISUALIZATION AND AGGREGATION
Being taken from different datasets, the data are grouped in an excel file, later formatted to be best used in R Studio. The file was then imported and read using the readxl library.
Below the reference as file path and the code used in R.

```{r}
install.packages(c("tidyverse", "readxl"))
library(tidyverse)
library(readxl)

percorso_file <- "C:\\Users\\huawei\\OneDrive\\Documents\\xlxs_first_RF.xlsx"

nomi_fogli <- excel_sheets(percorso_file)

liste_tabelle <- setNames(
  lapply(nomi_fogli, function(nome_foglio) {
    read_excel(percorso_file, sheet = nome_foglio)
  }),
  nomi_fogli
)

lapply(nomi_fogli, function(nome_foglio) {
  cat("Tabella:", nome_foglio, "\n")
  print(head(liste_tabelle[[nome_foglio]]))
  cat("\n")
})

tables <- lapply(liste_tabelle, function(tabella) {
  na.omit(tabella)
})

print(head(tables))
```


In order to operate on the data I had to modify the dataset tables after importing them from Excel. 
Being double entry tables with historical series I had to use the function of the package tidyverse "pivot_longer"  that converts the format of the data from "wide" to "long". It basically transforms the imported dataframe columns into new rows of a new dataframe.

```{r}
data3 <- read_excel(percorso_file, sheet = "ARPR")

data_long <- data3 %>%
  pivot_longer(cols = -ARPR, names_to = "Anno", values_to = "Valori")
print(data_long)
```


## 3 METHODOLOGY 
The conclusions and assumptions made in this study derive from an analysis of the imported data, using a graphical representation to evaluate the trend over time and significant changes. 
The data are also compared with each other through formulas of statistical inference, in particular in the forecasting phases. 
Disclaimer. The forecast analysis of the data collected by Statista is done by the company itself, as they take into account numerous factors including analysis of market trends outside of our expertise. Below is the reference link containing the report with all the phases of the analysis of the years 2024 to 2027, considered into account in this study.


https://cdn.statcdn.com/static/img/outlook/methodology/methodology-en.pdf_


The specific data of the market and the company Nike were chosen after a personal analysis of the company budgets, reporting in this study only the data necessary to answer our questions.
Among the various numerical analyses carried out are also the calculation of correlation coefficients, differences in historical series and the calculation of percentages from data provided by companies. 



## 4 ANALYSIS
In order to draw conclusions from the data we have, we shift the focus from the global retail market to the specific appareal retail sector. This is because it is the largest category in Fashion eCommerce with a revenue of US$425.5 billion at 2023.


This sector is divided into four subcategories, among them different in target, characteristics and profit. 

- Children's Apparel
- Men's Apparel
- Women's Apparel
- Other Apparel

### 4.1 APPAREL REVENUES 
As you can see Women’s Apparel holds the record for revenue compared to the others, followed by Men’s apparel. Other Apparel includes, among others, skorts, outerwear, and clothing accessories such as bandanas, handkerchiefs, and tie clips
Data are to be considered in billions of US$.

```{r}

library(tidyverse)
library(readxl)

data1<- read_excel(percorso_file, sheet = "Revenue")

data_graph1 <- data1%>%
  pivot_longer(cols = -Class, names_to = "Anno", values_to = "Valori")

graph_1 <- ggplot(data_graph1, aes(x = Valori, y = Anno, fill = Class)) +
  geom_col(position = "stack") +
  labs(title = "Apparel",
       x = "Classificazione",
       y = "Valori",
       fill = "Anno") +
  theme_minimal() +
  scale_fill_brewer(palette = "PuRd")

print(graph_1)

```

![image](https://github.com/Paolaloi/e-Tailing/assets/147175173/20818be1-5bb6-4776-bb8b-362d52d7ef11)

The analysis of the data provided on revenue change percentage in the online retail apparel market highlights some significant trends. In 2020, many sectors recorded a contraction in revenues, largely attributable to the impacts of the pandemic from COVID-19. Sectors such as Men’s Apparel and Women’s Apparel have fallen significantly, by 9.0% and 9.3% respectively. However, in 2021, a recovery is observed with an increase of 21.0% in Men’s Apparel and 21.5% in Women’s Apparel.Important also the impact that the war in Ukraine and the difficult relations with Russia have had on the market

The Other Apparel category shows steady growth. Turning to revenues in billions of dollars, Women’s Apparel emerges as the most profitable, indicating strong demand. For the period 2024-2028, despite the uncertainties related to COVID-19, the forecast shows a constant growth in all categories, signalling a positive outlook for online fashion retail.


```{r}
data2<- read_excel(percorso_file, sheet = "RCh_percent")

data_long <- data2 %>%
  pivot_longer(cols = -RCh_percent, names_to = "Anno", values_to = "Valori")

grafico_linee <- ggplot(data_long, aes(x = Anno, y = Valori, group = RCh_percent, color = RCh_percent)) +
  geom_line(size = 1) +
  geom_point(size = 2) +
  labs(title = "Revenue Change",
       x = "Anno",
       y = "Valori",
       color = "Class") +
  theme_minimal() +
  scale_color_brewer(palette = "PuRd")

print(grafico_linee)

```
![image](https://github.com/Paolaloi/e-Tailing/assets/147175173/ec4c6284-ef10-402a-9190-52d234751caf)












