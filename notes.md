


Magic python notebook:

https://kscprod-bio4.esr.cri.nz/NGS/active/VIR/SARS-CoV2/covid_postassembly.ipynb



Most data livese here: `/NGS/active/VIR/SARS-CoV2/analysis/BIdownload/microreact/`

Table 1:
/NGS/active/VIR/SARS-CoV2/analysis/alignment_clustering/clean_dataset/report_table.tsv 


```python
%%bash  -s "$KSC_RUN_ID" "$MASC_RUN_ID" "$CSC_RUN_ID"
echo "Runs KSC=$1, MASC=$2, CSC=$3"
KSCRUN_DIR=$(echo "/NGS/active/VIR/SARS-CoV2/analysis/GridIon_assemblies/$1_analysis")
MASCRUN_DIR=$(echo "/NGS/active/VIR/SARS-CoV2/analysis/MASC/$2_analysis/")
CSCRUN_DIR=$(echo "/NGS/active/VIR/SARS-CoV2/analysis/CSC/$3_analysis/")
cat $KSCRUN_DIR/*/isolate_to_barcode.csv $MASCRUN_DIR/*/isolate_to_barcode.csv $CSCRUN_DIR/*/isolate_to_barcode.csv | \
awk 'BEGIN {​FS=","}​ {​print $1}​' | \
xargs -I {​}​ grep {​}​ /NGS/active/VIR/SARS-CoV2/analysis/alignment_clustering/clean_dataset/clean_samples.txt | \
xargs -I {​}​ grep {​}​ /NGS/active/VIR/SARS-CoV2/analysis/BIdownload/BI_epi.tsv | awk 'BEGIN {​FS="\t"}​ {​OFS="\t"}​ {​print $2, $3, $4, $28}​' | uniq > report_isolates.tsv
cat $KSCRUN_DIR/*/isolate_to_barcode.csv $MASCRUN_DIR/*/isolate_to_barcode.csv $CSCRUN_DIR/*/isolate_to_barcode.csv | \
awk 'BEGIN {​FS=","}​ {​print $1}​' | \
xargs -I {​}​ grep {​}​ /NGS/active/VIR/SARS-CoV2/analysis/alignment_clustering/clean_dataset/clean_samples.txt | \
xargs -I {​}​ grep {​}​ /NGS/active/VIR/SARS-CoV2/analysis/BIdownload/microreact/microreact_new.tsv | awk 'BEGIN {​FS="\t";OFS="\t"}​ {​print $7, $18, $28}​' | paste report_isolates.tsv - | \
awk 'BEGIN {​FS="\t"}​ {​OFS="\t"}​ {​print $1, $2, $5, $6, $4, $3, $7}​' | uniq > report_table.tsv
```

