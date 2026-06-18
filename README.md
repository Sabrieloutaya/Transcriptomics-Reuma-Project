# 🧬 Genen binnen de B-celreceptorsignaalroute vertonen een afwijkende expressie in synoviumbiopten van patiënten met reumatoïde artritis vergeleken met gezonde controles
<img width="1600" height="960" alt="image" src="https://github.com/user-attachments/assets/df82af55-4d98-4f65-a0b7-7c78584f9710" />

### 
#### 
## Introductie

Reumatoïde artritis (RA) is een chronische auto-immuunziekte die zorgt voor gewrichtsontstekingen, wat kan leiden tot ernstige boterosies en functieverlies (Almutairi et al., 2020). In 2020 leefden wereldwijd naar schattig 17,6 miljoen mensen met RA wereldwijd dit is een stijging van 14,1% sinds 1990.                Er wordt voorspeld dat er in 2050 31,7 miljoen mensen RA-patiënten zullen zijn (Black et al., 2023).                                                              De exacte oorzaak is nog niet bekend, maar genetische aanleg en omgevingsfactoren spelen een belangrijke rol (Gabriel, 2001). 

In dit onderzoek worden transcriptomicsgegevens van synoviumbiopten van RA-patiënten en gezonde controles geanalyseerd om genen en biologische processen te identificeren die betrokken zijn bij reumatoïde artritis. Met de focus op de B-celreceptorsignaalroute.                                                             Hierbij staat de vraag of de expressie van genen binnen de B-celreceptorsignaalroute verschilt tussen patiënten met reumatoïde artritis en gezonde controles centraal. Om deze vraag te beantwoorden wordt eerst onderzocht welke genen significant differentieel tot expressie worden gebracht tussen beide groepen. Vervolgens wordt bepaald welke biologische processen verrijkt zijn onder de differentieel tot expressie gebrachte genen. Ten slotte wordt specifiek gekeken welke genen binnen de B-celreceptorsignaalroute een verhoogde of verlaagde expressie vertonen bij RA-patiënten ten opzichte van gezonde controles. 

## 🔬 Methoden
In dit onderzoek werd de genexpressie van synoviumbiopten van patiënten met reumatoïde artritis (RA) vergeleken met gezonde controles, met de focus op de        B-celreceptorsignaalroute. De gebruikte RNA-seq dataset was afkomstig van Platzer et al. (2020) en werd verkregen uit de NCBI Sequence Read Archive (SRA).        De dataset bestond uit 8 synoviumbiopten: 4 gezonde controles (SRR4785819, SRR4785820, SRR4785828 en SRR4785831) en 4 patiënten met RA (SRR4785979, SRR4785980, SRR4785986 en SRR4785988) zie tabel 1. De analyse werd uitgevoerd op al beschikbare ruwe sequencing reads. 

De RNA-seq data werden geanalyseerd in R met behulp van Bioconductor packages. Volgens de Rsubread handleiding (hoofdstuk 4.2 stap 1) werd eerst een index van het humane referentiegenoom hg38 (p14) gemaakt met `Rsubread` [v2.26.0]. Waarna de paired-end reads werden uitgelijnd tegen het referentiegenoom met de functie align (hoofdstuk 4.2 stap 2). De verkregen BAM-bestanden werden gesorteerd en geïndexeerd met `Rsamtools` [v2.28.0] met de functie lapply ().                 Daarna werd met de functie featureCounts (hoofdstuk 6.2.10/6.4) een countmatrix gemaakt op basis van de BAM-bestanden en het bijbehorende GTF bestand van het humane hg38 genoom.

Voor de differentiële genexpressie werd een DESeqDataSet gemaakt op basis van de countmatrix met de package `DESeq2` [v1.52.0]. Genen met een p-waarde <0,05 en een log2FoldChange (log2FC) <-1 of >1 werden gezien als significant differentieel tot expressie gebracht. De resultaten werden gevisualiseerd met een volcano plot, gemaakt met `EnhancedVolcano` [v1.30.0]. Vervolgens werd een GO-analyse uitgevoerd met `clusterProfiler` [v4.20.0] en `org.Hs.eg.db` [v3.23.1].       Hierbij werden de gensymbolen veranderd naar Entrez-ID’s en werd voor correctie voor multiple testing de Benjamin-Hochberg (BH) methode gebruikt.           Waarbij een p-waarde cutoff van 0,05 werd gebruikt. Op basis hiervan werd de KEGG pathway hsa04662 geanalyseerd en gevisualiseerd met `pathview` [v 1.52.0].      Zie [Script](Script/) voor de uitwerking van de methode. 

## 📊 Resultaten
### Differentiële genexpressie
Om verschillen in genexpressie tussen RA-patiënten en gezonde controles vast te stellen werden differentieel tot expressie gebrachte genen gevisualiseerd in een volcano plot. Zoals weergegeven in figuur 1 waren `ADAMDEC1`, `BCL2A1`en `SRGN` verhoogd tot expressie gebracht. In tegenstelling tot`ANKRD30BL`, `MT-ND6`en `ZNF598`die verlaagd tot expressie werden gebracht. 

<img width="851" height="617" alt="Volcano plot" src="https://github.com/user-attachments/assets/0b1a2dc2-3f7f-4930-a6b2-01a624abe1ab" />


### Gene Ontology analyse
Om inzicht te krijgen bij welke biologische processen de differentieel tot expressie komende genen betrokken waren werd een GO-analyse uitgevoerd.                In figuur 2 zijn imuungerelateerde processen zoals B-celgemedieerde immuniteit en leukocyt gemedieerde immuniteit verrijkt.                                      De lage aangepaste p-waarden wezen op een hoge statistische significantie. Op basis hiervan werd de B-celreceptorsignaalroute gekozen voor verdere analyse. 

<img width="773" height="617" alt="GO-analyse barplot" src="https://github.com/user-attachments/assets/36e09a9b-5f99-4e5b-bfe9-4a44b6581db9" />

### KEGG pathway analyse
Om de betrokken signaalroutes van de differentieel tot expressie komende genen te onderzoeken, werd een pathway analyse uitgevoerd.                             De B-celreceptorsignaalroute bevatte op en neer gereguleerde genen in verschillende delen van de route (figuur 3), wat wijst op veranderingen in de B-celsignalering. 

<img width="1173" height="763" alt="B-cell receptor signaling pathview" src="https://github.com/user-attachments/assets/f9816b2a-4197-4017-a7e7-b0075df9eccb" />

## Conclusie
