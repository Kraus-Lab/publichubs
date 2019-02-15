# publichubs
Kraus Lab data hub to visualize on UCSC Genome Browser:

#Kraus Lab Breast Bancer lncRNA track (pmid: 26236012)

Step1:
Download gtfToGenePred and then genePredToBigGenePred
For Linux:
wget http://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/gtfToGenePred 
wget http://hgdownload.soe.ucsc.edu/admin/exe/linux.x86_64/genePredToBigGenePred 
For MacOS:
wget http://hgdownload.soe.ucsc.edu/admin/exe/macOSX.x86_64/gtfToGenePred 
wget http://hgdownload.soe.ucsc.edu/admin/exe/macOSX.x86_64/genePredToBigGenePred

wget http://genome.ucsc.edu/goldenPath/help/examples/bigGenePred.as
wget http://hgdownload.soe.ucsc.edu/goldenPath/hg19/bigZips/hg19.chrom.sizes -O chrom.sizes
wget http://hgdownload.soe.ucsc.edu/admin/exe/macOSX.x86_64/bedToBigBed

Step2:
gtfToGenePred GSE63189_Catalog_of_lncRNAs_in_MCF-7cells.gtf GSE63189_Catalog_of_lncRNAs_in_MCF-7cells.genePred 
genePredToBigGenePred GSE63189_Catalog_of_lncRNAs_in_MCF-7cells.genePred GSE63189_Catalog_of_lncRNAs_in_MCF-7cells.bigGenePred 
#NOTE: The .bigGenePred file generated above does not have all the required columns.(https://genome.ucsc.edu/goldenpath/help/bigGenePred.html), and then convert it to a bigBed file. 

Step3:
cat GSE63189_Catalog_of_lncRNAs_in_MCF-7cells.bigGenePred | awk '{print $1,$2,$3,$4,$5,$6,$7,$8,$9,$10,$11,$12,$4,$13,$14,$15,$4,$4,$4,$16}' | sort -k1,1 -k2,2n > GSE63189_Catalog_of_lncRNAs_in_MCF-7cells.bigGenePred.txt

Step4:
bedToBigBed -as=bigGenePred.as -type=bed12+8 GSE63189_Catalog_of_lncRNAs_in_MCF-7cells.bigGenePred.txt chrom.sizes GSE63189_Catalog_of_lncRNAs_in_MCF-7cells.bigGenePred.bb

Step5:
Use the "Raw" text display for the link to hub to give the following URL https://raw.githubusercontent.com/Kraus-Lab/publichubs/master/breast_cancer_lncrna_pmid_26236012/hub.txt
