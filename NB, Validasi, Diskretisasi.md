
## Pada kasus ini, diskretisasi mampu meningkatkan akurasi


```R
# membaca data
carseat <- read.csv("Carseats.csv")

## melihat data teratas
head(carseat)
```


<table>
<thead><tr><th scope=col>Sales</th><th scope=col>CompPrice</th><th scope=col>Income</th><th scope=col>Advertising</th><th scope=col>Population</th><th scope=col>Price</th><th scope=col>ShelveLoc</th><th scope=col>Age</th><th scope=col>Education</th><th scope=col>Urban</th><th scope=col>US</th></tr></thead>
<tbody>
	<tr><td> 9.50 </td><td>138   </td><td> 73   </td><td>11    </td><td>276   </td><td>120   </td><td>Bad   </td><td>42    </td><td>17    </td><td>Yes   </td><td>Yes   </td></tr>
	<tr><td>11.22 </td><td>111   </td><td> 48   </td><td>16    </td><td>260   </td><td> 83   </td><td>Good  </td><td>65    </td><td>10    </td><td>Yes   </td><td>Yes   </td></tr>
	<tr><td>10.06 </td><td>113   </td><td> 35   </td><td>10    </td><td>269   </td><td> 80   </td><td>Medium</td><td>59    </td><td>12    </td><td>Yes   </td><td>Yes   </td></tr>
	<tr><td> 7.40 </td><td>117   </td><td>100   </td><td> 4    </td><td>466   </td><td> 97   </td><td>Medium</td><td>55    </td><td>14    </td><td>Yes   </td><td>Yes   </td></tr>
	<tr><td> 4.15 </td><td>141   </td><td> 64   </td><td> 3    </td><td>340   </td><td>128   </td><td>Bad   </td><td>38    </td><td>13    </td><td>Yes   </td><td>No    </td></tr>
	<tr><td>10.81 </td><td>124   </td><td>113   </td><td>13    </td><td>501   </td><td> 72   </td><td>Bad   </td><td>78    </td><td>16    </td><td>No    </td><td>Yes   </td></tr>
</tbody>
</table>




```R
# mengecek data hilang dan ringkasan data
summary(carseat)
```


         Sales          CompPrice       Income        Advertising    
     Min.   : 0.000   Min.   : 77   Min.   : 21.00   Min.   : 0.000  
     1st Qu.: 5.390   1st Qu.:115   1st Qu.: 42.75   1st Qu.: 0.000  
     Median : 7.490   Median :125   Median : 69.00   Median : 5.000  
     Mean   : 7.496   Mean   :125   Mean   : 68.66   Mean   : 6.635  
     3rd Qu.: 9.320   3rd Qu.:135   3rd Qu.: 91.00   3rd Qu.:12.000  
     Max.   :16.270   Max.   :175   Max.   :120.00   Max.   :29.000  
       Population        Price        ShelveLoc        Age          Education   
     Min.   : 10.0   Min.   : 24.0   Bad   : 96   Min.   :25.00   Min.   :10.0  
     1st Qu.:139.0   1st Qu.:100.0   Good  : 85   1st Qu.:39.75   1st Qu.:12.0  
     Median :272.0   Median :117.0   Medium:219   Median :54.50   Median :14.0  
     Mean   :264.8   Mean   :115.8                Mean   :53.32   Mean   :13.9  
     3rd Qu.:398.5   3rd Qu.:131.0                3rd Qu.:66.00   3rd Qu.:16.0  
     Max.   :509.0   Max.   :191.0                Max.   :80.00   Max.   :18.0  
     Urban       US     
     No :118   No :142  
     Yes:282   Yes:258  
                        
                        
                        
                        



```R
# mengecek struktur data
str(carseat)
```

    'data.frame':	400 obs. of  11 variables:
     $ Sales      : num  9.5 11.22 10.06 7.4 4.15 ...
     $ CompPrice  : int  138 111 113 117 141 124 115 136 132 132 ...
     $ Income     : int  73 48 35 100 64 113 105 81 110 113 ...
     $ Advertising: int  11 16 10 4 3 13 0 15 0 0 ...
     $ Population : int  276 260 269 466 340 501 45 425 108 131 ...
     $ Price      : int  120 83 80 97 128 72 108 120 124 124 ...
     $ ShelveLoc  : Factor w/ 3 levels "Bad","Good","Medium": 1 2 3 3 1 1 3 2 3 3 ...
     $ Age        : int  42 65 59 55 38 78 71 67 76 76 ...
     $ Education  : int  17 10 12 14 13 16 15 10 10 17 ...
     $ Urban      : Factor w/ 2 levels "No","Yes": 2 2 2 2 2 1 2 2 1 1 ...
     $ US         : Factor w/ 2 levels "No","Yes": 2 2 2 2 1 2 1 2 1 2 ...
    


```R
# membuat peubah baru
## membuat peubah High
carseat$High <- ifelse(carseat$Sales > 8, "ya", "tidak")

## merubah High menjadi bertipe factor
carseat$High <- as.factor(carseat$High)
```


```R
str(carseat)
```

    'data.frame':	400 obs. of  12 variables:
     $ Sales      : num  9.5 11.22 10.06 7.4 4.15 ...
     $ CompPrice  : int  138 111 113 117 141 124 115 136 132 132 ...
     $ Income     : int  73 48 35 100 64 113 105 81 110 113 ...
     $ Advertising: int  11 16 10 4 3 13 0 15 0 0 ...
     $ Population : int  276 260 269 466 340 501 45 425 108 131 ...
     $ Price      : int  120 83 80 97 128 72 108 120 124 124 ...
     $ ShelveLoc  : Factor w/ 3 levels "Bad","Good","Medium": 1 2 3 3 1 1 3 2 3 3 ...
     $ Age        : int  42 65 59 55 38 78 71 67 76 76 ...
     $ Education  : int  17 10 12 14 13 16 15 10 10 17 ...
     $ Urban      : Factor w/ 2 levels "No","Yes": 2 2 2 2 2 1 2 2 1 1 ...
     $ US         : Factor w/ 2 levels "No","Yes": 2 2 2 2 1 2 1 2 1 2 ...
     $ High       : Factor w/ 2 levels "tidak","ya": 2 2 2 1 1 2 1 2 1 1 ...
    


```R
barplot(xtabs(~High,data=carseat),main="Class of Sales \n ya=high  tidak=low",
       col=c("aquamarine","yellow"))
box()
```


![png](output_6_0.png)



```R
attach(carseat)
par(mfrow=c(2,4))
hist(Sales,main="Sales",col=adjustcolor("red",alpha.f=0.05))
hist(Sales[which(carseat$High=="ya")],col=adjustcolor("blue",alpha.f=0.7),add=TRUE)
hist(Sales[which(carseat$High=="tidak")],col=adjustcolor("yellow",alpha.f=0.5),add=TRUE)
box()

hist(CompPrice,main="CompPrice",col=rgb(1,0,0,1,alpha=0.05))
hist(CompPrice[which(carseat$High=="ya")],col=adjustcolor("blue",alpha.f=0.7),add=TRUE)
hist(CompPrice[which(carseat$High=="tidak")],col=adjustcolor("yellow",alpha.f=0.4),add=TRUE)
box()

hist(Income,main="Income",col=rgb(1,0,0,1,alpha=0.05))
hist(Income[which(carseat$High=="ya")],col=adjustcolor("blue",alpha.f=0.7),add=TRUE)
hist(Income[which(carseat$High=="tidak")],col=adjustcolor("yellow",alpha.f=0.4),add=TRUE)
box()

hist(Advertising,main="Advertising",col=rgb(1,0,0,1,alpha=0.05))
hist(Advertising[which(carseat$High=="ya")],col=adjustcolor("blue",alpha.f=0.7),add=TRUE)
hist(Advertising[which(carseat$High=="tidak")],col=adjustcolor("yellow",alpha.f=0.4),add=TRUE)
box()

hist(Population,main="Population",col=rgb(1,0,0,1,alpha=0.05))
hist(Population[which(carseat$High=="ya")],col=adjustcolor("blue",alpha.f=0.7),add=TRUE)
hist(Population[which(carseat$High=="tidak")],col=adjustcolor("yellow",alpha.f=0.4),add=TRUE)
box()

hist(Price,main="Price",col=rgb(1,0,0,1,alpha=0.05))
hist(Price[which(carseat$High=="ya")],col=adjustcolor("blue",alpha.f=0.7),add=TRUE)
hist(Price[which(carseat$High=="tidak")],col=adjustcolor("yellow",alpha.f=0.4),add=TRUE)
box()

hist(Age,main="Age",col=rgb(1,0,0,1,alpha=0.05))
hist(Age[which(carseat$High=="ya")],col=adjustcolor("blue",alpha.f=0.7),add=TRUE)
hist(Age[which(carseat$High=="tidak")],col=adjustcolor("yellow",alpha.f=0.4),add=TRUE)
box()

hist(Education,main="Education",col=rgb(1,0,0,1,alpha=0.05))
hist(Education[which(carseat$High=="ya")],col=adjustcolor("blue",alpha.f=0.7),add=TRUE)
hist(Education[which(carseat$High=="tidak")],col=adjustcolor("yellow",alpha.f=0.4),add=TRUE)
box()
```

    The following objects are masked from carseat (pos = 3):
    
        Advertising, Age, CompPrice, Education, High, Income, Population,
        Price, Sales, ShelveLoc, Urban, US
    
    


![png](output_7_1.png)



```R
barplot(xtabs(~High,data=carseat),col="aquamarine")
barplot(xtabs(~High,data=train),col="pink",add=T)
legend("topright",inset=0.01,c("Semua","Train"),col=c("aquamarine","pink"),fill=c("aquamarine","pink"),
       cex=1,title="Keterangan", text.font=4, bg="white")
box()
```


    Error in terms.formula(formula, data = data): object 'train' not found
    Traceback:
    

    1. barplot(xtabs(~High, data = train), col = "pink", add = T)

    2. xtabs(~High, data = train)

    3. terms(formula, data = data)

    4. terms.formula(formula, data = data)



![png](output_8_1.png)



```R
cor(carseat[,-c(7,10,11,12)])
```


<table>
<thead><tr><th></th><th scope=col>Sales</th><th scope=col>CompPrice</th><th scope=col>Income</th><th scope=col>Advertising</th><th scope=col>Population</th><th scope=col>Price</th><th scope=col>Age</th><th scope=col>Education</th></tr></thead>
<tbody>
	<tr><th scope=row>Sales</th><td> 1.00000000 </td><td> 0.06407873 </td><td> 0.151950979</td><td> 0.269506781</td><td> 0.050470984</td><td>-0.44495073 </td><td>-0.231815440</td><td>-0.051955242</td></tr>
	<tr><th scope=row>CompPrice</th><td> 0.06407873 </td><td> 1.00000000 </td><td>-0.080653423</td><td>-0.024198788</td><td>-0.094706516</td><td> 0.58484777 </td><td>-0.100238817</td><td> 0.025197050</td></tr>
	<tr><th scope=row>Income</th><td> 0.15195098 </td><td>-0.08065342 </td><td> 1.000000000</td><td> 0.058994706</td><td>-0.007876994</td><td>-0.05669820 </td><td>-0.004670094</td><td>-0.056855422</td></tr>
	<tr><th scope=row>Advertising</th><td> 0.26950678 </td><td>-0.02419879 </td><td> 0.058994706</td><td> 1.000000000</td><td> 0.265652145</td><td> 0.04453687 </td><td>-0.004557497</td><td>-0.033594307</td></tr>
	<tr><th scope=row>Population</th><td> 0.05047098 </td><td>-0.09470652 </td><td>-0.007876994</td><td> 0.265652145</td><td> 1.000000000</td><td>-0.01214362 </td><td>-0.042663355</td><td>-0.106378231</td></tr>
	<tr><th scope=row>Price</th><td>-0.44495073 </td><td> 0.58484777 </td><td>-0.056698202</td><td> 0.044536874</td><td>-0.012143620</td><td> 1.00000000 </td><td>-0.102176839</td><td> 0.011746599</td></tr>
	<tr><th scope=row>Age</th><td>-0.23181544 </td><td>-0.10023882 </td><td>-0.004670094</td><td>-0.004557497</td><td>-0.042663355</td><td>-0.10217684 </td><td> 1.000000000</td><td> 0.006488032</td></tr>
	<tr><th scope=row>Education</th><td>-0.05195524 </td><td> 0.02519705 </td><td>-0.056855422</td><td>-0.033594307</td><td>-0.106378231</td><td> 0.01174660 </td><td> 0.006488032</td><td> 1.000000000</td></tr>
</tbody>
</table>




```R
# membagi data
library(caret)
## train
set.seed(1993)
index_train <- createDataPartition(1:length(carseat$High),times=1,p=0.8,list=FALSE)
train <- carseat[index_train,-1]

## test
test <- carseat[-index_train,-1]
dim(train)
dim(test)
```

    Loading required package: lattice
    Loading required package: ggplot2
    


<ol class=list-inline>
	<li>320</li>
	<li>11</li>
</ol>




<ol class=list-inline>
	<li>80</li>
	<li>11</li>
</ol>




```R
str(train)
```

    'data.frame':	320 obs. of  11 variables:
     $ CompPrice  : int  111 113 141 124 136 132 121 117 122 115 ...
     $ Income     : int  48 35 64 113 81 110 78 94 35 28 ...
     $ Advertising: int  16 10 3 13 15 0 9 4 2 11 ...
     $ Population : int  260 269 340 501 425 108 150 503 393 29 ...
     $ Price      : int  83 80 128 72 120 124 100 94 136 86 ...
     $ ShelveLoc  : Factor w/ 3 levels "Bad","Good","Medium": 2 3 1 1 2 3 1 2 3 2 ...
     $ Age        : int  65 59 38 78 67 76 26 50 62 53 ...
     $ Education  : int  10 12 13 16 10 10 10 13 18 18 ...
     $ Urban      : Factor w/ 2 levels "No","Yes": 2 2 2 1 2 1 1 2 2 2 ...
     $ US         : Factor w/ 2 levels "No","Yes": 2 2 1 2 2 1 2 2 1 2 ...
     $ High       : Factor w/ 2 levels "tidak","ya": 2 2 1 2 2 1 2 2 1 2 ...
    


```R
# diskretisasi
library(classInt)

## equal width TRAIN
eqwid_CompPrice <- cut(train$CompPrice,classIntervals((train$CompPrice), 4, style = 'equal')$brks,include.lowest=TRUE)
eqwid_Income <- cut(train$Income,classIntervals((train$Income), 4, style = 'equal')$brks,include.lowest=TRUE)
eqwid_Advertising <- cut(train$Advertising,classIntervals((train$Advertising), 4, style = 'equal')$brks,include.lowest=TRUE)
eqwid_Population <- cut(train$Population,classIntervals((train$Population), 4, style = 'equal')$brks,include.lowest=TRUE)
eqwid_Price <- cut(train$Price,classIntervals((train$Price), 4, style = 'equal')$brks,include.lowest=TRUE)
eqwid_Age <- cut(train$Age,classIntervals((train$Age), 4, style = 'equal')$brks,include.lowest=TRUE)
eqwid_Education <- cut(train$Education,classIntervals((train$Education), 4, style = 'equal')$brks,include.lowest=TRUE)
```

    Warning message:
    "package 'classInt' was built under R version 3.5.2"


```R
train_eqwid <- data.frame(eqwid_CompPrice,eqwid_Income,eqwid_Advertising,eqwid_Population,eqwid_Price,eqwid_Age,
                          eqwid_Education,High=train$High)
summary(train_eqwid)
```


      eqwid_CompPrice      eqwid_Income   eqwid_Advertising  eqwid_Population
     [77,102] : 22    [21,45.8]  :79    [0,7.25]   :181     [12,136] :76     
     (102,126]:150    (45.8,70.5]:80    (7.25,14.5]: 91     (136,260]:74     
     (126,150]:135    (70.5,95.2]:92    (14.5,21.8]: 40     (260,385]:85     
     (150,175]: 13    (95.2,120] :69    (21.8,29]  :  8     (385,509]:85     
         eqwid_Price        eqwid_Age  eqwid_Education    High    
     [24,65.8] :  5   [25,38.8]  :77   [10,12]:123     tidak:187  
     (65.8,108]:114   (38.8,52.5]:75   (12,14]: 66     ya   :133  
     (108,149] :175   (52.5,66.2]:90   (14,16]: 65                
     (149,191] : 26   (66.2,80]  :78   (16,18]: 66                



```R
test_eqwid <- NULL
test_eqwid$eqwid_CompPrice <- ifelse(test$CompPrice<=102,1,ifelse(test$CompPrice<=126,2,ifelse(test$CompPrice<=150,3,4)))
test_eqwid$eqwid_Income <- ifelse(test$Income<=45.8,1,ifelse(test$Income<=70.5,2,ifelse(test$Income<=95.2,3,4)))
test_eqwid$eqwid_Advertising <- ifelse(test$Advertising<=7.25,1,ifelse(test$Advertising<=14.5,2,
                                ifelse(test$Advertising<=21.8,3,4)))
test_eqwid$eqwid_Population <- ifelse(test$Population<=136,1,ifelse(test$Population<=260,2,
                               ifelse(test$Population<=385,3,4)))
test_eqwid$eqwid_Price <- ifelse(test$Price<=65.8,1,ifelse(test$Price<=114,2,ifelse(test$Price<=175,3,4)))
test_eqwid$eqwid_Age <- ifelse(test$Age<=38.8,1,ifelse(test$Age<=75,2,ifelse(test$Age<=90,3,4)))
test_eqwid$eqwid_Education <- ifelse(test$Education<=12,1,ifelse(test$Education<=14,2,ifelse(test$Education<=16,3,4)))
```


```R
test_eqwid <- lapply(test_eqwid,function(x) as.factor(x))
test_eqwid <- as.data.frame(test_eqwid)
head(test_eqwid)
```


<table>
<thead><tr><th scope=col>eqwid_CompPrice</th><th scope=col>eqwid_Income</th><th scope=col>eqwid_Advertising</th><th scope=col>eqwid_Population</th><th scope=col>eqwid_Price</th><th scope=col>eqwid_Age</th><th scope=col>eqwid_Education</th></tr></thead>
<tbody>
	<tr><td>3</td><td>3</td><td>2</td><td>3</td><td>3</td><td>2</td><td>4</td></tr>
	<tr><td>2</td><td>4</td><td>1</td><td>4</td><td>2</td><td>2</td><td>2</td></tr>
	<tr><td>2</td><td>4</td><td>1</td><td>1</td><td>2</td><td>2</td><td>3</td></tr>
	<tr><td>3</td><td>4</td><td>1</td><td>1</td><td>3</td><td>3</td><td>4</td></tr>
	<tr><td>3</td><td>3</td><td>1</td><td>4</td><td>3</td><td>3</td><td>4</td></tr>
	<tr><td>2</td><td>1</td><td>1</td><td>3</td><td>2</td><td>2</td><td>2</td></tr>
</tbody>
</table>




```R
str(train_eqwid)
```

    'data.frame':	320 obs. of  8 variables:
     $ eqwid_CompPrice  : Factor w/ 4 levels "[77,102]","(102,126]",..: 2 2 3 2 3 3 2 2 2 2 ...
     $ eqwid_Income     : Factor w/ 4 levels "[21,45.8]","(45.8,70.5]",..: 2 1 2 4 3 4 3 3 1 1 ...
     $ eqwid_Advertising: Factor w/ 4 levels "[0,7.25]","(7.25,14.5]",..: 3 2 1 2 3 1 2 1 1 2 ...
     $ eqwid_Population : Factor w/ 4 levels "[12,136]","(136,260]",..: 2 3 3 4 4 1 2 4 4 1 ...
     $ eqwid_Price      : Factor w/ 4 levels "[24,65.8]","(65.8,108]",..: 2 2 3 2 3 3 2 2 3 2 ...
     $ eqwid_Age        : Factor w/ 4 levels "[25,38.8]","(38.8,52.5]",..: 3 3 1 4 4 4 1 2 3 3 ...
     $ eqwid_Education  : Factor w/ 4 levels "[10,12]","(12,14]",..: 1 1 2 3 1 1 1 2 4 4 ...
     $ High             : Factor w/ 2 levels "tidak","ya": 2 2 1 2 2 1 2 2 1 2 ...
    


```R
str(test_eqwid)
```

    'data.frame':	80 obs. of  7 variables:
     $ eqwid_CompPrice  : Factor w/ 4 levels "1","2","3","4": 3 2 2 3 3 2 3 2 3 2 ...
     $ eqwid_Income     : Factor w/ 4 levels "1","2","3","4": 3 4 4 4 3 1 1 3 3 3 ...
     $ eqwid_Advertising: Factor w/ 3 levels "1","2","3": 2 1 1 1 1 1 1 1 2 1 ...
     $ eqwid_Population : Factor w/ 4 levels "1","2","3","4": 3 4 1 1 4 3 2 3 1 2 ...
     $ eqwid_Price      : Factor w/ 3 levels "1","2","3": 3 2 2 3 3 2 2 2 2 2 ...
     $ eqwid_Age        : Factor w/ 3 levels "1","2","3": 2 2 2 3 3 2 2 2 2 2 ...
     $ eqwid_Education  : Factor w/ 4 levels "1","2","3","4": 4 2 3 4 4 2 1 1 3 3 ...
    


```R
# Model Naive Bayes
library(klaR)
nb_model <- NaiveBayes(High~ ., data=train_eqwid)
summary(nb_model)
```

    Warning message:
    "package 'klaR' was built under R version 3.5.2"Loading required package: MASS
    


              Length Class      Mode     
    apriori   2      table      numeric  
    tables    7      -none-     list     
    levels    2      -none-     character
    call      3      -none-     call     
    x         7      data.frame list     
    usekernel 1      -none-     logical  
    varnames  7      -none-     character



```R
klasifikasi <- predict(nb_model,newdata=test_eqwid)
```


```R
confusionMatrix(test$High,klasifikasi$class,positive='ya')
```


    Confusion Matrix and Statistics
    
              Reference
    Prediction tidak ya
         tidak    40  9
         ya       11 20
                                              
                   Accuracy : 0.75            
                     95% CI : (0.6406, 0.8401)
        No Information Rate : 0.6375          
        P-Value [Acc > NIR] : 0.02184         
                                              
                      Kappa : 0.467           
     Mcnemar's Test P-Value : 0.82306         
                                              
                Sensitivity : 0.6897          
                Specificity : 0.7843          
             Pos Pred Value : 0.6452          
             Neg Pred Value : 0.8163          
                 Prevalence : 0.3625          
             Detection Rate : 0.2500          
       Detection Prevalence : 0.3875          
          Balanced Accuracy : 0.7370          
                                              
           'Positive' Class : ya              
                                              


## tanpa diskretisasi


```R
nb_model2 <- NaiveBayes(High~.,data=train[,-c(6,9,10)])
klasifikasi2 <- predict(nb_model2,newdata=test[,-c(6,9,10,11)])
```

    Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 1"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 2"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 3"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 4"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 5"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 6"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 7"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 8"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 9"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 10"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 11"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 12"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 13"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 14"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 15"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 16"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 17"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 18"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 19"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 20"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 21"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 22"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 23"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 24"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 25"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 26"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 27"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 28"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 29"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 30"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 31"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 32"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 33"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 34"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 35"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 36"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 37"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 38"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 39"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 40"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 41"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 42"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 43"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 44"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 45"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 46"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 47"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 48"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 49"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 50"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 51"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 52"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 53"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 54"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 55"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 56"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 57"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 58"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 59"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 60"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 61"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 62"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 63"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 64"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 65"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 66"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 67"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 68"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 69"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 70"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 71"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 72"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 73"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 74"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 75"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 76"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 77"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 78"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 79"Warning message in FUN(X[[i]], ...):
    "Numerical 0 probability for all classes with observation 80"


```R
confusionMatrix(test$High,klasifikasi2$class)
```


    Confusion Matrix and Statistics
    
              Reference
    Prediction tidak ya
         tidak    44  5
         ya       16 15
                                              
                   Accuracy : 0.7375          
                     95% CI : (0.6271, 0.8296)
        No Information Rate : 0.75            
        P-Value [Acc > NIR] : 0.6574          
                                              
                      Kappa : 0.4085          
     Mcnemar's Test P-Value : 0.0291          
                                              
                Sensitivity : 0.7333          
                Specificity : 0.7500          
             Pos Pred Value : 0.8980          
             Neg Pred Value : 0.4839          
                 Prevalence : 0.7500          
             Detection Rate : 0.5500          
       Detection Prevalence : 0.6125          
          Balanced Accuracy : 0.7417          
                                              
           'Positive' Class : tidak           
                                              


## Diskretisasi tanpa CompPrice


```R
nb_model3 <- NaiveBayes(High~ ., data=train_eqwid[,-1])
```


```R
klasifikasi3 <- predict(nb_model3,newdata=test_eqwid[,-1])
```


```R
confusionMatrix(test$High,klasifikasi3$class,positive='ya')
```


    Confusion Matrix and Statistics
    
              Reference
    Prediction tidak ya
         tidak    37 12
         ya       11 20
                                              
                   Accuracy : 0.7125          
                     95% CI : (0.6005, 0.8082)
        No Information Rate : 0.6             
        P-Value [Acc > NIR] : 0.02453         
                                              
                      Kappa : 0.3979          
     Mcnemar's Test P-Value : 1.00000         
                                              
                Sensitivity : 0.6250          
                Specificity : 0.7708          
             Pos Pred Value : 0.6452          
             Neg Pred Value : 0.7551          
                 Prevalence : 0.4000          
             Detection Rate : 0.2500          
       Detection Prevalence : 0.3875          
          Balanced Accuracy : 0.6979          
                                              
           'Positive' Class : ya              
                                              

