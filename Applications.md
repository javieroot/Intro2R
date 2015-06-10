

INTRODUCCIÓN AL MANEJO DE DATOS Y PROGRAMACIÓN EN R
========================================================
width: 1366
height: 768
font-family: 'Serif'
author: Gustavo A. Ballen

Museu de Zoologia da Universidade de São Paulo

gaballench@gmail.com


=======================================================
# APLICACIONES DE R A PROBLEMAS DE INVESTIGACIÓN ICTIOLÓGICA

=======================================================
# Ecología de comunidades

Ecología de comunidades
=======================================================

* En 2014 se realizó un inventario rápido en la cuenca alta del río Cinaruco en Colombia
* Todos los análisis de ecología de comunidades fueron llevados a cabo en R
* Listas de especies, nuevos registros y especies esperadas fueron analizadas
* Riqueza
* Estructura
* Diversidad beta
* Reemplazo de especies
* Modelos de abundancia

Indicar el dir. de trabajo y cargar los datos
=======================================================


```r
## Set WD
setwd("/home/balleng/Dropbox/Consulting/Arauca Cinaruco 2014/Analysis/cinaruco")

## Load abundance data
dataset <- read.csv("juriepe.csv")
cNames <- as.character(dataset[, 1])
dataset <- dataset[, -1]
# Transpose table
dataset <- t(dataset)
colnames(dataset) <- cNames
rm(cNames)
```
Curva global de acumulación de especies
=======================================================


```r
library(iNEXT)
globalMargins <- apply(dataset, 2, sum)
names(globalMargins) <- NULL
globalMargins <- as.numeric(globalMargins)
globalanalyses <- iNEXT(globalMargins)
tiff(filename = "globalcurve.tiff", width = 480, height = 480, units = "px")
ggiNEXT(globalanalyses)
dev.off()
```

Listas de especies
=======================================================


```r
## Expected, observed, and new records
expected <- read.csv("esperadas.csv", header = FALSE)
expected <- as.character(expected[,1])
expected <-sort(expected)
observed <- as.character(colnames(dataset))
observed <- sort(observed)

newRecords <- setdiff(observed, expected)

# get rid of sps and affs
newToSpecies <- newRecords[-grep("*sp.",newRecords)]
newToSpecies <- newToSpecies[-grep("*aff.", newToSpecies)]

# get rid of new combinations/species/identifications
changes <- sort(c("Copella eigenmanni", "Hemigrammus analis", "Hemigrammus geisleri", 
             "Hyphessobrycon mavro", "Hemigrammus bleheri"))
newToSpecies <- setdiff(newToSpecies, changes)

rm(changes)
# rm(newRecords) # uncomment this line if total differences between observed and expected are desired
```

Info taxonómica y estructura (1)
=======================================================


```r
## Taxonomic info
taxoinfo <- read.csv("infotaxo.csv", header = TRUE)

# Species by order
specOrderGlobal <- table(taxoinfo[, 1])
tiff(filename = "specbyorder.tiff", width = 1000, height = 480, units = "px")
orderbar <- qplot(factor(taxoinfo[, 1], levels = names(sort(table(taxoinfo[, 1])))), main = "Numero de especies por orden", 
                   xlab = "Orden", ylab = "Riqueza", geom = "bar")
orderbar + theme(axis.text.x = element_text(angle = 90))
dev.off()

# Species by family
specFamilyGlobal <- table(taxoinfo[, 2])
numbers <- as.vector(specFamilyGlobal)
families <- names(specFamilyGlobal)
specFamilyGlobal <- data.frame(families, as.integer(numbers))
tiff(filename = "specbyfamily.tiff", width = 1000, height = 480, units = "px")
familybar <- qplot(factor(taxoinfo[, 2], levels = names(sort(table(taxoinfo[, 2])))), main = "Numero de especies por familia", 
        xlab = "Familia", ylab = "Riqueza", geom = "bar")
familybar + theme(axis.text.x = element_text(angle = 90))
dev.off()
```

Descripción de dieta
=======================================================


```r
## Diet
diet <- read.csv("diet.csv", header = TRUE)
dietByOrder <- table(responseName = diet$Diet, diet$Order)
dietByOrderSum <- apply(dietByOrder, 1, FUN = sum)
dietByFamily <-table(responseName = diet$Diet, diet$Family)
dietByFamilySum <- apply(dietByFamily, 1, FUN = sum)

# Pie charts
tiff(filename = "dietpiechart.tiff", width = 1000, height = 480, units = "px")
pie <- ggplot(diet, aes(x = factor(1), fill = factor(Diet))) + geom_bar(width = 1)
pie + coord_polar(theta = "y")
dev.off()
##### Analysis by waterbody #####
samples <- rownames(dataset)
localities <- c(rep("ARA-01", 3), "ARA-02", "ARA-01", "ARA-02", rep("ARA-03", 9), 
                "ARA-04", "ARA-05", rep("ARA-04", 2), "ARA-01", "ARA-03", 
                "ARA-05", "ARA-04")
samplesLocs <- cbind(samples, localities)

rm(samples, localities)
```

Riqueza en Caño Juriepe
=======================================================


```r
# Caño Juriepe:
juriepeSamples <- samplesLocs[which(samplesLocs[, 2] == "ARA-01"), 1]
juriepeSamples <- c(juriepeSamples, samplesLocs[which(samplesLocs[, 2] == "ARA-02"), 1])
juriepeSamples <- c(juriepeSamples, samplesLocs[which(samplesLocs[, 2] == "ARA-03"), 1])
juriepeSamples <- sort(juriepeSamples)
juriepe <- dataset[juriepeSamples, ]

rm(juriepeSamples)

juriepeMargins <- apply(juriepe, 2, sum)
names(juriepeMargins) <- NULL
juriepeMargins <- as.numeric(juriepeMargins)
juriepeAnalyses <- iNEXT(juriepeMargins)
tiff(filename = "juriepecurve.tiff", width = 480, height = 480, units = "px")
ggiNEXT(juriepeAnalyses)
dev.off()

juriepeSpecies <- colnames(juriepe[, which(juriepeMargins > 0)])
```

Riqueza Morichal La Calandria
=======================================================


```r
# Morichal La Calandria:
calandriaSamples <- samplesLocs[which(samplesLocs[, 2] == "ARA-05"), 1]
calandria <- dataset[calandriaSamples, ]

rm(calandriaSamples)

calandriaMargins <- apply(calandria, 2, sum)
names(calandriaMargins) <- NULL
calandriaMargins <- as.numeric(calandriaMargins)
calandriaAnalyses <- iNEXT(calandriaMargins)
tiff(filename = "calandriacurve.tiff", width = 480, height = 480, units = "px")
ggiNEXT(calandriaAnalyses)
dev.off()

calandriaSpecies <- colnames(calandria[, which(calandriaMargins > 0)])
```

Riqueza Caño Seco
=======================================================


```r
# Caño Seco:
secoSamples <- samplesLocs[which(samplesLocs[, 2] == "ARA-04"), 1]
seco <- dataset[secoSamples, ]

rm(secoSamples)

secoMargins <- apply(seco, 2, sum)
names(secoMargins) <- NULL
secoMargins <- as.numeric(secoMargins)
secoAnalyses <- iNEXT(secoMargins)
tiff(filename = "secocurve.tiff", width = 480, height = 480, units = "px")
ggiNEXT(secoAnalyses)
dev.off()

secoSpecies <- colnames(seco[, which(secoMargins > 0)])
```

Diversidad beta
=======================================================


```r
##### Beta Diversity #####

# barplot with 95%CI
tiff(filename = "betadiversity.tiff", width = 480, height = 480, units = "px")

entropies <- c(ChaoEntropy(globalMargins, datatype="abundance")[1, 2], 
               ChaoEntropy(juriepeMargins, datatype="abundance")[1, 2], 
               ChaoEntropy(calandriaMargins, datatype="abundance")[1, 2], 
               ChaoEntropy(secoMargins, datatype="abundance")[1, 2])
mp <- barplot(entropies, axes=FALSE, axisnames=FALSE, ylim=c(0, 3), 
              main = "Entropía de Shannon", xlab = "Global y Estaciones", 
              ylab = "H")
axis(1, labels=c("Cinaruco (Global)", "Cñ. Juriepe", "Mr. Calandria", "Cñ. Seco"), 
     at = mp)
axis(2, at=seq(0 , 3, by=0.5))
box()
upper <- matrix(c(ChaoEntropy(globalMargins, datatype="abundance")[1, 5], 
                  ChaoEntropy(juriepeMargins, datatype="abundance")[1, 5], 
                  ChaoEntropy(calandriaMargins, datatype="abundance")[1, 5], 
                  ChaoEntropy(secoMargins, datatype="abundance")[1, 5]), 2)
lower<- matrix(c(ChaoEntropy(globalMargins, datatype="abundance")[1, 4], 
                 ChaoEntropy(juriepeMargins, datatype="abundance")[1, 4], 
                 ChaoEntropy(calandriaMargins, datatype="abundance")[1, 4], 
                 ChaoEntropy(secoMargins, datatype="abundance")[1, 4]), 2)
segments(mp, lower, mp, upper, lwd=2)
segments(mp - 0.1, lower, mp + 0.1, lower, lwd=2)
segments(mp - 0.1, upper, mp + 0.1, upper, lwd=2)
dev.off()
```

Reemplazo de especies
=======================================================


```r
##### Species replacement #####

library(vegan)
siteSpecies <- rbind(juriepeMargins, calandriaMargins, secoMargins)
rownames(siteSpecies) <- c("Juriepe", "Calandria", "Seco")
colnames(siteSpecies) <- colnames(dataset)
distMatrix <- vegdist(siteSpecies, method="bray")
cluster <- hclust(distMatrix)
tiff(filename = "replacement.tiff", width = 480, height = 480, units = "px")
plot(cluster, hang = -1)
dev.off()
```

Modelos de abundancia
=======================================================


```r
##### RAD plot for anaysis of structure #####
# Global best fit by locality
RAD <- radfit(siteSpecies)
tiff(filename = "RAD.tiff", width = 480, height = 480, units = "px")
plot(RAD)
dev.off()

# Fit all models and use AIC for best fit for each site
RADjuriepe <- radfit(siteSpecies[1, ])
tiff(filename = "RADjuriepe.tiff", width = 480, height = 480, units = "px")
radlattice(RADjuriepe)
dev.off()
RADcalandria <- radfit(siteSpecies[2, ])
tiff(filename = "RADcalandria.tiff", width = 480, height = 480, units = "px")
radlattice(RADcalandria)
dev.off()
RADseco <- radfit(siteSpecies[3, ])
tiff(filename = "RADseco.tiff", width = 480, height = 480, units = "px")
radlattice(RADseco)
dev.off()
```

=======================================================
# Limnología de la represa Guarapiranga, Sao Paulo

Limnología de Guarapiranga
=======================================================

* Con un total de 151 líneas de código se desarrolló la v.1 que es totalmente funcional

<center><img src="seminario-figure/script.png"
        height="500px"/></center>
***

* Básicamente lee el formato html de una página web, identifica links a archivos pdf, los descarga, convierte los pdfs a csvs, corrige errores de formato, y genera archivos listos para ser cargados en R

Paquetes necesarios
=======================================================


```r
# Uso práctico de direcciones http 
library(httr)
# Funciones para vectorización y modificación simple de strings
library(stringr)
# Facilitador de descargas
library(downloader)
```

Local da maquina e pastas de execução do tabula
=======================================================

```r
# Set Syslocale
Sys.setlocale('LC_ALL','C') 

# Tell R to look for tabula in its respective path. Each time a session starts
# it is necessary to run these lines as the effects are not global but temporary

Sys.setenv(PATH=paste(Sys.getenv("PATH"),
                      "/home/balleng/jruby-1.7.16.1/bin/",sep=":"))
Sys.setenv(PATH=paste(Sys.getenv("PATH"),
                      "/opt/jruby/bin/",sep=":"))
```

Nossa pasta de trabalho
=======================================================


```r
# setwd("./guarapiranga")
setwd("PATH")
dir.create("datasets")
```

URL da Sabesp, lendo a info da internet
=======================================================

<small style="font-size:.8em">

```r
urlSabesp <- "http://site.sabesp.com.br/site/interna/Default.aspx?secaoId=43"

linesSabesp <- readLines(urlSabesp)

monitIndex <- grep("monitoramento", linesSabesp, ignore.case = TRUE, value = FALSE)
pdfIndex <- grep("pdf", linesSabesp, ignore.case = TRUE, value = FALSE)

compl <- c(monitIndex, pdfIndex)

linesSabesp[compl[duplicated(compl)]] # Cases for which only pdf lines from the 
# monitoramento folder

linesSabesp <- linesSabesp[compl[duplicated(compl)]] # Reduced to pdf urls
```
</small>

Gerando as URLs finais
=======================================================


```r
pdfUrls <- vector()
range <- vector(length = 2)
for(i in seq_along(linesSabesp)) {
	range[1] <- str_locate(linesSabesp[i], "/uploads/file/monitoramento")[1]
	range[2] <- str_locate(linesSabesp[i], ".pdf")[2]
	pdfUrls <- c(pdfUrls, str_sub(linesSabesp[i], start = range[1], end = range[2]))
}
```

Obtendo os nomes de arquivo com base nas URLs
=======================================================


```r
pdfFilenames <- vector()

for(i in seq_along(pdfUrls)) {
	filename <- strsplit(pdfUrls[i], "/")[[1]][length(strsplit(pdfUrls[i], "/")[[1]])]
	pdfFilenames <- c(pdfFilenames, filename)
}

dir.create("sabespDatasets")
```

Preparando os URLS dos pdfs
=======================================================


```r
urlPrefix <- "http://site.sabesp.com.br"

for(i in seq_along(pdfUrls)) {
	download(url = paste(urlPrefix, pdfUrls[i], sep = ""), 
		destfile = paste(getwd(), "/sabespDatasets/", i, ".pdf", sep = ""))
}
```

Passando os nomes dos pdfs pra os futuros csvs
=======================================================


```r
pdfDownloads <- list.files("sabespDatasets", recursive = TRUE, full.names = FALSE)

csvNames <- vector()

for(i in seq_along(pdfDownloads)) {
	name <- str_sub(pdfDownloads[i], start = 1, end = (str_length(pdfDownloads[i])-4))
	csvNames <- c(csvNames, name)
}

setwd("sabespDatasets")
```

Converção do pdf pra o csv
=======================================================

O processo leva por conta de uma hora pra 176 arquivos

```r
for(i in seq_along(pdfDownloads)) {
	system(paste("tabula --pages all -o ", csvNames[i], ".csv ", pdfDownloads[i], sep = ""))
}
# t1 <- Sys.time(); expr{}; t2 <- Sys.time(); print(t2-t1) 
# for only two files had this output:
# [1] Time difference of 40.14474 secs
# This means that for a total of 176 files it would take:
# 40.14474s/2 = 20.07237s; 20.07237s*176 = 3532.737s/60s*m^-1 = 58.87895m
csvNames <- grep(".csv", dir(), value = TRUE)
```

Modificando erros de conversão em formato
=======================================================


```r
# Call the replacer.sh bash script in order to format the csv files
system("cd ..; cd ..; cp analyses/replacer.sh datasets/sabespDatasets")
system("sh replacer.sh")
```

O script replacer.sh
=======================================================

```{bash}
#!/bin/bash
for i in `ls *.csv`
do
sed -ri 's/,"//g' $i
sed -ri 's/",//g' $i
sed -ri 's/"//g' $i
sed -ri 's/ ,/ /g' $i
sed -ri 's/,/\./g' $i
sed -ri 's/ /\,/g' $i
sed -ri 's/^,//g' $i
sed -ri 's/,,/,/g' $i
done
```

=======================================================
# Resultados graficos

Site da Sabesp
=======================================================

<center><img src="seminario-figure/sitesabesp.png"
        height="500px"/></center>

Estrutura HTML
=======================================================

<center><img src="seminario-figure/html.png"
        height="500px"/></center>

Baixando os arquivos pdf
=======================================================

<center><img src="seminario-figure/pdfs.png"
        height="500px"/></center>

O que tém o pdf dentro?
=======================================================

<center><img src="seminario-figure/pdfdentro.png"
        height="500px"/></center>

Após conversão: csv
=======================================================

<center><img src="seminario-figure/csvs.png"
        height="500px"/></center>

O que tém o csv dentro?
=======================================================

<center><img src="seminario-figure/csvdentro.png"
        height="500px"/></center>|
