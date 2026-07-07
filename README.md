# 🧬 Genen binnen de B-celreceptorsignaalroute vertonen een afwijkende expressie in synoviumbiopten van patiënten met reumatoïde artritis vergeleken met gezonde controles
<img width="1600" height="960" alt="image" src="https://github.com/user-attachments/assets/df82af55-4d98-4f65-a0b7-7c78584f9710" />

### 
#### 
## Introductie

Reumatoïde artritis (RA) is een chronische auto-immuunziekte die zorgt voor gewrichtsontstekingen, wat kan leiden tot ernstige boterosies en functieverlies (Almutairi et al., 2020). In 2020 leefden wereldwijd naar schattig 17,6 miljoen mensen met RA wereldwijd dit is een stijging van 14,1% sinds 1990.                Er wordt voorspeld dat er in 2050 31,7 miljoen mensen RA-patiënten zullen zijn (Black et al., 2023).                                                              De exacte oorzaak is nog niet bekend, maar genetische aanleg en omgevingsfactoren spelen een belangrijke rol (Gabriel, 2001). 

In dit onderzoek worden transcriptomicsgegevens van synoviumbiopten van RA-patiënten en gezonde controles geanalyseerd om genen en biologische processen te identificeren die betrokken zijn bij reumatoïde artritis. Met de focus op de B-celreceptorsignaalroute.                                                           Hierbij staat de vraag of de expressie van genen binnen de B-celreceptorsignaalroute verschilt tussen patiënten met reumatoïde artritis en gezonde controles centraal. Om deze vraag te beantwoorden wordt eerst onderzocht welke genen significant differentieel tot expressie worden gebracht tussen beide groepen. Vervolgens wordt bepaald welke biologische processen verrijkt zijn onder de differentieel tot expressie gebrachte genen. Ten slotte wordt specifiek gekeken welke genen binnen de B-celreceptorsignaalroute een verhoogde of verlaagde expressie vertonen bij RA-patiënten ten opzichte van gezonde controles. 

## 🔬 Methoden
In dit onderzoek werd de genexpressie van synoviumbiopten van patiënten met reumatoïde artritis (RA) vergeleken met gezonde controles, met de focus op de        B-celreceptorsignaalroute. De gebruikte RNA-seq dataset was afkomstig uit de studie van Platzer et al. (2020) en werd verkregen uit de NCBI Sequence Read Archive (SRA). De dataset bestond uit 8 synoviumbiopten: 4 gezonde controles (SRR4785819, SRR4785820, SRR4785828 en SRR4785831) en 4 patiënten met RA (SRR4785979, SRR4785980, SRR4785986 en SRR4785988) (tabel 1). 
De transcriptomische analyse werd uitgevoerd op al beschikbare ruwe sequencing reads. 

De RNA-seq data werden geanalyseerd in R met behulp van Bioconductor packages. Een index van het humane referentiegenoom hg38 (p14) werd gegenereerd met `Rsubread` [v2.26.0], waarna de paired-end reads werden uitgelijnd tegen het referentiegenoom met de functie *align()*. De resulterende BAM-bestanden werden gesorteerd en geïndexeerd met `Rsamtools` [v2.28.0] met de functie *lapply ()*. Vervolgens werd met de functie *featureCounts()* een countmatrix gemaakt op basis van de BAM-bestanden en het bijbehorende GTF annotatiebestand van het humane hg38 genoom.

Voor de differentiële genexpressie werd een DESeqDataSet gemaakt op basis van de countmatrix met behulp van de package `DESeq2` [v1.52.0].                        Genen met een p-waarde <0,05 en een log2FoldChange (log2FC) <-1 of >1 werden beschouwd als significant differentieel tot expressie gebracht. 
De resultaten van de differentiële expressieanalyse werden gevisualiseerd met een volcano plot, gegenereerd met `EnhancedVolcano` [v1.30.0]. 
Om de biologische betekenis van de differentieel tot expressie gebrachte genen te onderzoeken, werd een GO-analyse uitgevoerd volgens het stappenplan van Wu et al. (2021b) met aanvullende informatie uit de enrichGO documentatie (z.d.), gebruikmakend van `clusterProfiler` [v4.20.0] en `org.Hs.eg.db` [v3.23.1].            Gensymbolen werden geconverteerd naar Entrez-ID’s en p-waarden werden gecorrigeerd voor multiple testing volgens de Benjamin-Hochberg (BH) methode.           
Een gecorrigeerde p-waarde <0,05 werd gehanteerd als significantiedrempel. 
Op basis hiervan werd de KEGG pathway hsa04662 geanalyseerd en gevisualiseerd met `pathview` [v 1.52.0].      
Zie [Script](Script/) voor de uitwerking van de methode. 

*Tabel 1: Metadata van de gebruikte samples.*

<img width="661" height="250" alt="image" src="https://github.com/user-attachments/assets/ca3544ab-addb-4e9d-a227-b43d213c4a9a" />

<img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/e753f2b9-f560-453c-afe8-ec885d30967a" />
 
*Figuur 1: Workflow van de RNA-seq-data analyse.*

## 📊 Resultaten
Om genen en biologische processen te identificeren die betrokken zijn bij reumatoïde artitis(RA), werden transcriptomicsgegevens van synoviumbiopten van RA-patiënten en gezonde controles geanalyseerd, met specifieke aandacht voor de B-celreceptorsignaalroute. 
Eerst werden de verschillen in genexpressie tussen beide groepen onderzocht. Vervolgens werden deze genen gebuikt voor functionele verrijkingsanalyse met gene ontology en voor analyse van de KEGG B-celreceptorsignaalroute.

### Differentiële genexpressie
Om verschillen in genexpressie tussen RA-patiënten en gezonde controles vast te stellen werden differentieel tot expressie gebrachte genen gevisualiseerd in een volcano plot. Zoals weergegeven in figuur 2 waren `ADAMDEC1`, `BCL2A1`en `SRGN` verhoogd tot expressie gebracht. In tegenstelling tot`ANKRD30BL`, `MT-ND6`en `ZNF598`die verlaagd tot expressie werden gebracht. 

<img width="851" height="617" alt="Volcano plot" src="https://github.com/user-attachments/assets/0b1a2dc2-3f7f-4930-a6b2-01a624abe1ab" />

*Figuur 2: Volcano plot van differentieel tot expressie gebrachte genen tussen RA-patiënten en gezonde controles*                     
Op de x-as staat de Log2FoldChange (verandering in genexpressie) en op de y-as de −log₁₀ (p-waarde), die de statische significantie weergeeft. In totaal werden 29407 genen geanalysseerd. Genen met een significante verandering in genexpressie en een significante p-waarde zijn rood gekleurd en gelabed. Genen die alleen voldoen aan de Log2FC drempel zijn groen gekleurd, de grijs gekleurde verschillen niet significant tussen de groepen. De stippellijn geeft de afkapwaarde voor significantie aan. 

### Gene Ontology analyse
Om inzicht te krijgen bij welke biologische processen de differentieel tot expressie komende genen betrokken waren werd een GO-analyse uitgevoerd.                In figuur 3 zijn immuungerelateerde processen zoals B-celgemedieerde immuniteit en leukocyt gemedieerde immuniteit verrijkt.                                      De lage aangepaste p-waarden wezen op een hoge statistische significantie. Op basis hiervan werd de B-celreceptorsignaalroute gekozen voor verdere analyse. 


<img width="1920" height="992" alt="image" src="https://github.com/user-attachments/assets/bfcb6883-a75c-4c7b-abf1-ac4a4ae9f329" />

*Figuur 3: GO-analyse barplot van significant differentieel tot expressie gebrachte genen bij RA-patiënten ten opzicht van gezonde controles*                    
De weergegeven biologische processen zijn de meest significant verrijkte GO-termen. De x-as toont het aantal genen per GO term. De kleur van de balken geeft de gecorrigeerde p-waarde weer, hoe roder de balk hoe statistisch significanter het resultaat. 

### KEGG pathway analyse
Om de betrokken signaalroutes van de differentieel tot expressie komende genen te onderzoeken, werd een pathway analyse uitgevoerd.                               De B-celreceptorsignaalroute bevatte op (o.a. PIR-B, CD22 en CD72) en neer (o.a. PI3K en AKT) gereguleerde genen in verschillende delen van de route (figuur 4). In tabel 2 zijn de functies van deze genen te zien gevonden via NCBI Gene (z.d.).  

<img width="1173" height="763" alt="B-cell receptor signaling pathview" src="https://github.com/user-attachments/assets/f9816b2a-4197-4017-a7e7-b0075df9eccb" />

*Figuur 4: KEGG pathway-analyse van de B-celreceptorsignaalroute bij RA-patiënten ten opzichte van gezonde controles*
Visualisatie van de KEGG B-cell receptor signaling pathway op basis van de differentiële genexpressieanalyse.  
De rode kleur duidt op een verhoogde expressie (opregulatie) en de groene kleur op een verlaagde expressie (neerregulatie) bij RA-patiënten t.o.v gezonde controles. 

*Tabel 2: Functie van op en neer gereguleerde genen binnen de B-celreceptorsignaalroute.*
<img width="772" height="257" alt="image" src="https://github.com/user-attachments/assets/e823900e-7328-4f7b-94b9-0946f6774c40" />


## Conclusie
In dit RNA-seq transcriptomics onderzoek zijn de verschillen in genexpressie van RA-patiënten en gezonde controles onderzocht, met de focus op de B-celreceptorsignaalroute.                                                                                                                                         De expressie van genen binnen deze route verschilde tussen beide groepen, wat blijkt uit significant differentieel tot expressie gebrachte genen (o.a. ADAMDEC1, BCL2A1 en SRGN) en verrijkte immuunprocessen zoals B-cel en leukocyt gemedieerde immuniteit. Dit sluit aan bij eerdere studies die aantonen dat B-cellen een belangrijke rol spelen bij de pathogenese van RA door hun betrokkenheid bij de regulatie van immuun responsen (Mauri & Ehrenstein, 2007).                         Daarnaast werd binnen de B-celreceptorsignaalroute verhoogde expressie van PIR-B, CD22 en CD72 en verlaagde expressie van PI3K en AKT waargenomen.               Omdat deze genen betrokken zijn bij de signaaloverdracht en regulatie van B-cellen, wijzen deze veranderingen op verstoringen in de B-celsignalering bij RA-patiënten. 
