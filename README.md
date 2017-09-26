# musical-waffle
#!/bin/bash
j=N1-1
##mkdir intermediate #store the intermediate files
##for i in N1-2 N2 N3 H1 H2
##do
#       awk 'BEGIN{FS=OFS="\t"}{if ($0!~/^#/) print $1,$2,$2,$4,$5}' ../$i\.filted.SNP.vcf > ../$i\.filted.SNP.bed #already get these files

##      intersectBed -a ../N1-1.filted.SNP.bed -b ../$i\.filted.SNP.bed -wao > intermediate/N1-1vs$i\.filter.SNP.bed
##      awk 'BEGIN{FS=OFS="\t"}NR<=FNR{id=$1"\t"$2; a[id]}NR>FNR{pos=$1"\t"$2; if (!(pos in a)) print $0"\t.\t-1\t-1\t.\t.\t0"}' ../N1-1.filted.SNP.bed ../$i\.filted.SNP.bed >> intermediate/N1-1vs$i\.filter.SNP.bed
##      sort -n -k 1 -k 2 intermediate/N1-1vs$i\.filter.SNP.bed -o intermediate/N1-1vs$i\.filter.SNP.bed

##      perl bin_identity.pl -i intermediate/N1-1vs$i\.filter.SNP.bed -o N1-1vs$i\.filter_1M.SNP.bin -b 1000000 -x 5 -y 10
##done


cat > $j\_IS_1M.txt << EOF
Group   chromosome      floor   ceiling total   identity        rate    Rate    Chromosome_position
EOF

for n in tmp*bin
do
        group=${n%%.*}
        grep '^[1-9]' $n > intermediate/$group\_1M.tmp
        awk 'BEGIN{FS=OFS="\t"}{print $group"\t"$0"\t"($6*100)"\t"($2/1000000)}' intermediate/$group\_1M.tmp >> $j\_IS_1M.txt
done
