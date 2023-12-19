## STRUCTURE
- 1 PREPARATION
    - 1.1 BUSINESS OBJECTIVE
    - 1.2 HOW TO GET THERE
- 2 DATA USED
    - 2.1 DATA USED AND DATA LIMITATION
    - 2.2 DATA ORGANIZATION, VISUALIZATION AND AGGREGATION
- 3 METHODOLOGY
- 4 ANALYSIS
    - 4.1 APPAREL REVENUES
    - 4.2 KEY PLAYERS
    - 4.3 CHANGE IN INVESTEMTS
    - 4.4 NIKE SUCCESS
- 5 CONCLUSION

## 1 PREPARATION
### 1.1 BUSINESS OBJECTIVE 
The advent of information and communication technologies (ICTs) has radically redefined human life, shaping new meanings and practices. This revolution has triggered significant changes at the political, social and economic levels, pushing toward a socio-economic restructuring of established behavioral patterns.
The heart of this thesis focuses on analyzing how businesses, in response to this scenario of change, have been directed and supported by the irruption of ICT in retailing. This transformation has led to the emergence of business models based entirely on these technologies. The revolution in the concept of "e-tailing" became firmly established in the late 1990s, outlining a process of selling goods and services that encompasses the entire interaction with the customer, from the initial stage to the conclusion of transactions, via the Internet.  
Retailing, originally associated with the distribution channel alone, has moved beyond its traditional definition to evolve into a business system based on digital platforms. A crucial element in this scenario is the affirmation of the value of data. Through this thesis, we will explore the dynamics that have redefined the retailing landscape, focusing on the challenges and opportunities offered by ICT. With a close look at history and future prospects, we will analyze how businesses have adapted to this accelerated change, painting a comprehensive picture of the transformations that are redefining the world of retailing.

### 1.2 HOW TO GET THERE 
The basis of this research is established market data. We will begin with a general analysis of the global context in which the phenomenon has developed, and then gradually descend into detail, bringing the magnifying glass closer to a single sector and then to a specific company. The focus will be on the Appareal sector, with specific insight into the sportswear segment, particularly when we discuss Nike Inc.
The choice to focus on Nike Inc. was determined, first of all, by its adoption of a business plan that is a perfect concrete example for our study. Moreover, the company was selected because of its remarkable economic and, in part, social achievements in recent years. This decision allows us to go beyond simplistic general assumptions and base our answers on specific company data.

## 2 DATA USED 
### 2.1 DATA USED AND DATA LIMITATION
The fundamentals of this research draw market and sector data from Statista, a reliable source used for global market analysis. Statista already organizes and aggregates the data, ensuring, however, their reliability. The source and methodology are described in the reports, strengthening the reliability of the information. However, it should be noted that there is no direct access to sufficiently recent microdata (the least dated "free-data" dates back to 2007). This is for privacy reasons, therefore related to the purposes with which the data were collected by the company and so not disclosed in an non-aggregate manner. Another reason, much more marked, concerns the economic value that these data assume. This limitation may be an obstacle to our research, but by analyzing it from a different point of view, it can become an argument in favor of our thesis. It represents how much the introduction of the internet has changed the economic and commercial scheme, transforming the same data in exchangeable assets and, consequently, a source of direct or indirect gain for the companies.
As for the data relating to Nike, I retrieved them directly from the annual reports 10k published by the company itself, aimed at shareholders. This source offers a detailed insight into Nike’s financial performance. It should be noted that the data are divided into business years, starting in June and ending on May 31 of the following year.

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

An example of what the data will loke like in the R environment: 

```{r}

$Revenue
# A tibble: 5 × 13
  Class              `2017` `2018` `2019` `2020` `2021` `2022` `2023` `2024` `2025` `2026` `2027` `2028`
  <chr>               <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>
1 Children's Apparel   26.2   32.2   37.2   46.9   55.4   51.1   55.7   63.2   71.6   75.8   80.8   85.7
2 Men's Apparel        55.6   66.9   76.6   96.8  117    107.   117.   133.   150.   158.   168.   177. 
3 Other Apparel        15.6   19.3   22.2   28.4   34.0   35.8   38.3   43.3   48.9   52.3   56.1   59.8
4 Women's Apparel      95.2  114.   130.   162.   197.   179    196.   222.   251    265.   282    298. 
5 Total               193.   232.   266.   334.   404.   372.   408.   461.   522.   551.   586.   621. 

$RCh_percent
# A tibble: 5 × 12
  RCh_percent        `2018` `2019` `2020` `2021` `2022` `2023` `2024` `2025` `2026` `2027` `2028`
  <chr>               <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>
1 Children's Apparel   22.8   15.2   26.3   18.1  -7.86   9.01   13.4   13.3   5.93   6.58   6.02
2 Men's Apparel        20.2   14.5   26.4   21.0  -8.95   9.85   13.4   13.3   5.22   5.99   5.42
3 Other Apparel        23.9   14.8   28.2   19.9   5.28   6.85   13.0   12.9   7.01   7.23   6.6 
4 Women's Apparel      19.8   13.6   25.3   21.5  -9.27   9.74   13.1   13.0   5.64   6.35   5.83
5 Total                20.7   14.2   26.0   20.7  -7.75   9.39   13.2   13.1   5.69   6.36   5.81


```


In order to operate on the data I had to modify the dataset tables after importing them from Excel. 
Being double entry tables with historical series I had to use the function of the package tidyverse "pivot_longer"  that converts the format of the data from "wide" to "long". It basically transforms the imported dataframe columns into new rows of a new dataframe.
Here an example

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
As you can see Women’s Apparel holds the record for revenue compared to the others, followed by Men’s apparel. Other Apparel includes, among others, skorts, outerwear, and clothing accessories such as bandanas, handkerchiefs, and tie clips.


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

line_graph <- ggplot(data_long, aes(x = Anno, y = Valori, group = RCh_percent, color = RCh_percent)) +
  geom_line(size = 1) +
  geom_point(size = 2) +
  labs(title = "Revenue Change",
       x = "Anno",
       y = "Valori",
       color = "Class") +
  theme_minimal() +
  scale_color_brewer(palette = "PuRd")

print(line_graph)

```
![image](https://github.com/Paolaloi/e-Tailing/assets/147175173/ec4c6284-ef10-402a-9190-52d234751caf)




### 4.2 KEY PLAYERS 
The growth and profitability of this market in e-commerce has brought new names in the ranking of leading companies. I’ll show you below with a tree map based on everyone’s share of the market, created by using a new library: "plotly". 
As you can see the main player is Amazon, an entirely online platform. 
I would like to draw the attention to the percentage of Nike Inc, third place in 2022. For reference, in 2016 Nike did not reach any significant share, after that year it began investments in e-commerce and direct sales with a new business strategy called "Triple double" based on the development of a new online marketplace. 


```{r}

install.packages("plotly")
library(plotly)
library(RColorBrewer)

data4 <- readxl::read_excel(percorso_file, sheet = "Key_Players")
palette_colori <- c(brewer.pal(nrow(data), "Greens"), "orange")

treemap <- plot_ly(
  labels = as.character(data4$B_S_percent),
  parents = "",
  values = data4$`2022`,
  type = "treemap",
  hoverinfo = "label+value+percent parent",
  marker = list(
    colors = palette_colori,
    line = list(color = "white", width = 0.5)
  )
)

print(layout)

```
![image](https://github.com/Paolaloi/e-Tailing/assets/147175173/d3c1e397-c76c-4fee-9aeb-0609e08377fa)



### 4.3 CHANGE IN INVESTEMTS 
Like Nike, the rest of the market has had to adapt to this trend of digital growth. 
I organized the data on companies in four categories based on the investments made in e-commerce and digital programming. I’m drawing it in a bar chart. The companies that have made significant investments are 57%, a sign of the recognition of the importance of the changes that trade is going through. 
Only 1% of the companies did not make any investments. The data are updated to May 2022. 

```{r}
library(tidyr)

data_d2ci <- readxl::read_excel(percorso_file, sheet = "D2C_Investment")

colnames(data_d2ci) <- c("Categoria", "Percentuali")

data_d2ci$Percentuali <- as.numeric(sub("%", "", data_d2ci$Percentuali))

d2c_graph <- ggplot(data_d2ci, aes(x = factor(1), y = Percentuali, fill = Categoria)) +
  geom_bar(stat = "identity", position = "dodge", width = 0.7) +
  labs(title = "Investments",
       x = NULL,  
       y = "Percentage") +
  theme_minimal() +
  theme(legend.position = "top") +  
  scale_fill_brewer(palette = "PuBu")  

print(d2c_graph)

```
![image](https://github.com/Paolaloi/e-Tailing/assets/147175173/b4913857-d12a-4bf9-b373-a80b5adc32ef)


However, the investments must be analysed with a view to profitability, to see if the large investments are justified. 
Take Nike as an example. Starting from the balance sheet data we observe Total equity and Net debt in the years 2017-2022. 

```{r}

print(liste_tabelle$Nike_DE)

 A tibble: 2 × 7
  NIKEde       `2017` `2018` `2019` `2020` `2021` `2022`
  <chr>         <dbl>  <dbl>  <dbl>  <dbl>  <dbl>  <dbl>
1 Total Equity  12407   9812   9040   8055  12767  15281
2 Net Dept      -2377  -1360   -810   4228   -663   -370

```


I reorganized the data in R to calculate its ratio

```{r}
data_linee_stacked <- readxl::read_excel(percorso_file, sheet = "Nike_DE")

data_linee_stacked_long <- data_linee_stacked %>%
  pivot_longer(cols = -NIKEde, names_to = "Anno", values_to = "Valori")

```

I divided the Net Debt by the Total Equity and asked for the absolut value.

```{r}
data_linee_stacked <- readxl::read_excel(percorso_file, sheet = "Nike_DE")

data_linee_stacked_long <- data_linee_stacked %>%
  pivot_longer(cols = -NIKEde, names_to = "Anno", values_to = "Valori")
print(data_linee_stacked_long)

ratio_tibble <- data_linee_stacked_long %>%
  group_by(Anno) %>%
  summarise(Ratio_DE = abs(sum(Valori[NIKEde == "Net Dept"]) / sum(Valori[NIKEde == "Total Equity"])))

```
Down below I show the result in a graph. 

```{r}

DE_graph <- ggplot(ratio_tibble, aes(x = Anno, y = Ratio_DE, group = 1)) +
  geom_line() +
  geom_point(shape = 16, size = 3, color = "orange") +
  labs(title = "Net Dept / Total Equity Ratio",
       x = "Anno",
       y = "Ratio DE") +
  theme_minimal() +
  scale_color_brewer(palette = "OrRd")

print(DE_graph)

```

![image](https://github.com/Paolaloi/e-Tailing/assets/147175173/f969d43c-71ff-44d2-b511-8cb296d08f60)

The company has proven to be able to finance the total capital by more than 75% with own funds in the observed period, thus being less exposed to financial debts and, therefore, to the risk of fluctuations in interest rates. The exception is fiscal year 2020 when the value rose to 0.52, indicating a 52% livelihood from financial debts.
While not dependent on its operational performance, Nike’s autonomy index values report asset stability, giving investment margins and growth opportunities. 

### 4.4 NIKE SUCCESS 
Given what has been said so far about Nike, we want to link its success and increased revenues to the actual use of online distribution channels. To do this I will start from the revenues of Nike, but doing a quartile analysis (range of three months) of the fiscal year, to observe the data more closely. 
We also observe the number of accesses to the Nike.com site and its extensions (mobile applications) in the same period of time. 
The data of the revenues are in billions of dollars, while the accesses are to be considered in millions. For this reason we display the data in two different graphs.

```{r}

library(ggplot2)

dati <- data.frame(
  Colonna1 = c("'20 Q4", "'21 Q1", "'21 Q2", "'21 Q3", "'21 Q4", "'22 Q1", "'22 Q2", "'22 Q3", "'22 Q4"),
  REVENUE = c(6.3, 10.6, 11.2, 10.4, 12.3, 12.2, 11.4, 10.9, 12.2),
  `.com_VISITS` = c(260, 279, 355, 279, 352, 368, 387, 407, 444)
)

revenue_graph <- ggplot(dati, aes(x = as.factor(seq_along(Colonna1)), y = REVENUE)) +
  geom_line(size = 1, aes(color = "REVENUE", group = 1)) +
  labs(title = "REVENUE",
       x = "Quarters",
       y = "REVENUE") +
  theme_minimal() +
  scale_color_brewer(palette = "RdBu")

com_visits_graph <- ggplot(dati, aes(x = as.factor(seq_along(Colonna1)), y = `.com_VISITS`)) +
  geom_line(size = 1, aes(color = ".com_VISITS", group = 1)) +
  labs(title = ".com_VISITS",
       x = "Quarters",
       y = ".com_VISITS") +
  theme_minimal() +
  scale_color_brewer(palette = "PuBu")

print(revenue_graph)
print(com_visits_graph)

```

![image](https://github.com/Paolaloi/e-Tailing/assets/147175173/acf0ec3f-bb4d-4705-a361-0b0851aa018c)

![image](https://github.com/Paolaloi/e-Tailing/assets/147175173/03cb0d67-461a-46d2-bcc1-732183859b11)


Although looking at the graphs you could already see similarity in the historical trend, I transformed the data into numerics and calculated the correlation coefficient between the two data. In this way I also overcame the problem of the difference in unit of measurement. 

```{r}

dati$REVENUE <- as.numeric(dati$REVENUE)
dati$.com_VISITS <- as.numeric(dati$.com_VISITS)

correlation_coefficient <- cor(dati$REVENUE, dati$.com_VISITS, use = "complete.obs")

cat("The correlation coefficient between REVENUE and .com VISITS is:", correlation_coefficient, "\n")

```

The correlation coefficient between REVENUE and .com VISITS is: 0.6850819, showing a strong positive relationship between the two variables analysed. Note, for example, that a peak of access to the site between September and November 2020 (Q2 '21) corresponds to an increase in revenues in the same period; in the following quarter there is a decrease in login to the online site and a corresponding decrease in revenues. Analyzing data from fiscal year 2022 assumes that it is not a relationship in which the independent variable explains the dependent variable totally(as per a linear cause-and-effect relationship), but there is sufficient empirical evidence to confirm the influence of the online market on business results.


## 5 CONCLUSION 
The growth of the online retail apparel industry has led to significant changes in the business landscape, highlighted by industry analysis. In response to the challenges, companies have adapted and invested massively in e-commerce. Nike, for example, has completely transformed its strategy and radically changed the corporate structure. Many other companies have started from its success. The classification of companies according to the investments made shows a widespread recognition of the dynamics of change in trade.  
Nike’s revenue and online access analysis shows a strong correlation, underlining the importance of online distribution channels. Overall, flexibility in adapting to digital growth and investment strategy seem essential for success and sustainability in the retailing market. 
