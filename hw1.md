1.
iowa.df<-read.csv("data/iowa.csv",sep=';',header=T)
dim<-dim(iowa.df)
cat("行",dim[1],"\n")
cat("列",dim[2],"\n")
colname<-colnames(iowa.df)
cat("列名",colname,"\n")
r5c7<-iowa.df[5,7]
cat("第5行第7列的值",r5c7,"\n")
r2<-iowa.df[2,]
cat("第二行:\n")
print(r2)
2.
print("max不会报错，max基于字典顺序比较，7为最大值，所以返回7.")
print("sort不会报错，sort基于字典顺序排序,为12，32，5，7")
print("sum报错，因为sum是数值类而不是字符向量")
print("会报错，因为vector2为一个字符向量，无法进行数值加法运算")
print("不会报错，结果为19，这二者分别都是数值7和12，可以进行数值加法运算")
print("不会报错，list4[2]和list4[4]分别是数值42和126，可以进行数值加法运算，结果为168")
print("会报错，list4[2]和list4[4]是包含单元素列表而不是数值，无法进行加法运算")
3.
seq1<-seq(from=1,to=10000,by=372)
print(seq1)
seq2<-seq(from=1,to=10000,length.out=50)
print(seq2)
print("times参数会重复整个向量指定的次数，在这种情况下，1：3整个向量会被重复三次，结果为1 2 3 1 2 3 1 2 3，而each则是对每个元素分别重复指定的次数，结果为1 1 1 2 2 2 3 3 3")
4.
library(DAAG)
data(orings)
head(orings)
sr<-orings[c(1,2,4,11,13),]
print(sr)
plot(sr$Temperature,sr$Incidents,
xlab="Temperature",
ylab="Incidents",
main="Incidents vs Temperature (sr)")
plot(orings$Temperature,orings$Incidents,
xlab="Temperature",
ylab="Incidents",
main="Incidents vs Temperature (Fs)")
5.
library(DAAG)
data(ais)
head(ais)
str(ais)
library(dplyr)
library(tidyr)
sgc<-ais %>%
group_by(sport,sex) %>%
summarise(count = n())
sport_gender_table<-sgc %>%
pivot_wider(names_from = sex, values_from = count, names_prefix = "num_")
sport_gender_table<-sport_gender_table %>%
mutate(ratio = num_m / num_f)
print(sport_gender_table[order(-sport_gender_table$ratio),])
imbalanced_sports<-sport_gender_table %>%
filter(ratio>2|ratio<0.5)
print(imbalanced_sports)
6.
Manitoba.lakes <- data.frame(
elevation = c(217, 254, 248, 254, 253, 227, 178, 207, 217),
area = c(24387, 5374, 4624, 2247, 1353, 1223, 1151, 755, 657),
row.names = c("Winnipeg", "Winnipegosis", "Manitoba","SouthernIndian", "Cedar", "Island", "Gods", "Cross", "Playgreen")
)
attach(Manitoba.lakes)
plot(log2(area)~elevation, pch=16, xlim=c(170,280))
text(log2(area)~elevation, labels=row.names(Manitoba.lakes), pos=4)
text(log2(area) ~ elevation, labels = area, pos = 2)
title("Manitoba's Largest Lakes")
plot(area~elevation, pch=16, xlim=c(170,280), ylog=T)
text(area~elevation, labels=row.names(Manitoba.lakes), pos=4, ylog=T)
text(area~elevation, labels=area, pos=2, ylog=T)
title("Manitoba's Largest Lakes")
7.
dotchart(Manitoba.lakes$area, main = "马尼托巴省湖泊面积线性", xlab = "面积（平方公里）")
dotchart(log2(Manitoba.lakes$area), main = "马尼托巴省湖泊面积对数", xlab = "log2(面积，平方公里)")
8.
lowerboundarea<-sum(Manitoba.lakes$area)
print(lowerboundarea)