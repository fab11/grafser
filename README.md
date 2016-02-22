# grafser
##impor
library(foreign)
require(foreign)
baseinegi<-read.dbf("C:\\Users\\SALA-C25\\Downloads\\sdemt205\\sdemt205.dbf")
table(baseinegi$CD_A)
table(baseinegi$CLASE1)
sd<-read.dbf("C:\\Users\\SALA-C25\\Downloads\\sdemt205\\sdemt205.dbf")
baseinegi$R_DEF1 <- as.numeric(as.character(baseinegi$R_DEF))
baseinegi$C_RES1 <- as.numeric(as.character(baseinegi$C_RES))
baseinegi$EDA1 <- as.numeric(as.character(baseinegi$EDA))##primer argumento mandamos llamar la base

precod <-subset (baseinegi, ((R_DEF1 == 0) & (C_RES1 == 1 |C_RES1 == 3) & (EDA1 >= 15 & EDA1 <=98 )))
table (precod$R_DEF1)##lo ponemos en la base precod por que es en donde estamos haciendo las restricciones
table (precod$C_RES1)
table (precod$EDA1)
precod <-subset (baseinegi, ((R_DEF1 == 0) & (C_RES1 == 1 |C_RES1 == 3) & (EDA1 >= 15 & EDA1 <=98 )),select = c(EDA,SEX,HRSOCUP, CLASE2, CLASE1, CLASE3))
table (precod$R_DEF1)
table (precod$C_RES1)
table (precod$EDA1)

attach(precod)
CLASE2V1 <-table(CLASE2)
CLASE2V1
hist (CLASE2,)
hist(CLASE2, main="Grafica 1, Distribucion de la
     población de 15 años o mas, 2015",
     xlab ="Tipo de ocupada", ylab ="Poblacion miles",
     xlim = c (1,4), ylim = c(0,200000), border = T, pch=18,
     col = c("orange","green","purple","pink"))
sd1<-subset(sd,CLASE2==1, select =c(EDA,SEX,HRSOCUP, CLASE2, CLASE3, EDA5C,IMSSISSSTE))
frec<-table(sd1$IMSSISSSTE)
frec
help(pie)
pie(frec)
#LABELS LE PONEMOS LA ETIQUETA DEBE SER VECTOR
pie(frec, labels=c("imss", "issste", "otra", "norecibe", "noespecificado"), main="institucion de atención de atención medica")
pie(frec, labels=c("imss", "issste", "otra", "norecibe", "noespecificado"), main="institucion de atención de atención medica", col=c("green","pink","blue", "red","yellow", "gray"))

## graficas de barras 
### sacamos frecuencia de las variables que vamos a utilizar
frec1<-table(sd1$EDA5C)
barplot(frec1, main="grafica 1 cinco grupos de edad", col=c("green","red","blue","gray", "yellow", "brown"), names.arg = c("menor","14 a 24", "25 a 44","45 a 64", "65 y mas", "n.e"), xlab = "edad",ylab = "población", ylim = c(0,85000))
