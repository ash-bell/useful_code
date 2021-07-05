```
module add MCL/14.137-intel-2016b
module avail

screen -S test --> make a screen called test
screen -r test --> go to the screen called test
screen -ls
screen -X -S <id> kill

#fastq to fasta with sed
unpigz -c <filename> | sed -n '1~4s/^@/>/p;2~4p' | pigz -c > <output_file>

#tab sep a file out in shell
column -t -s$'\t' checkm_output.txt

# trim a fasta file by X length
awk -v RS='>[^\n]+\n' 'length() >= 30 {printf "%s", prt $0} {prt = RT}' file

#remove files with less than 3 lines (remove echo when happy)
find . -type f -exec awk -v x=3 'NR==x{exit 1}' {} \; -exec echo rm -f {} \;

#covert multifasta to fasta
for i in *.faa; do grep -v "^>" $i | awk 'BEGIN { ORS=""; print ">REPLACE_ME\n"} {print}' | sed "s/^>REPLACE_ME/$(basename $i _Glimmer.faa)/g" > $(basename $i _Glimmer.faa)_condensed.faa; done

# change fasta header to basename
awk '/^>/ {gsub(/_condensed.fasta(sta)?$/,"",FILENAME);printf(">%s\n",FILENAME);next;} {print}' $i >> all_sag_and_ref_condensed.fna

#rename file based on prefix
mv 123456.freya.fq.gz $(echo 123456.freya.fq.gz | sed 's/.*5/abc/')

#create a sorted and indexed bam file one command
bbwrap.sh ref=AE1712_3_80m_1k_reformatted.fasta \
in=AE1712_3_interleaved_80m.qtrimmed.fq.gz,AE1712_3_interleaved_80m.merged.fq.gz \
nodisk=t out=mapped.bam append bs=bs.sh; sh bs.sh

#pass variables into .SLURM scripts
while read line; do sed "s/REPLACE_ME/$line/g" abc.SLURM > tmp.SLRUM; sbatch tmp.SLURM; done 

#split a multifasta by contig into new files
awk '{if (substr($0, 1, 1)==">") {filename=(substr($0,2) ".fa")} print $0 >filename}' file 

nice colours / new_colors = ['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728',
              '#9467bd', '#8c564b', '#e377c2', '#7f7f7f',
              '#bcbd22', '#17becf']

        clrs = ['#E8ECFB', '#D9CCE3', '#D1BBD7', '#CAACCB', '#BA8DB4',
                '#AE76A3', '#AA6F9E', '#994F88', '#882E72', '#1965B0',
                '#437DBF', '#5289C7', '#6195CF', '#7BAFDE', '#4EB265',
                '#90C987', '#CAE0AB', '#F7F056', '#F7CB45', '#F6C141',
                '#F4A736', '#F1932D', '#EE8026', '#E8601C', '#E65518',
                '#DC050C', '#A5170E', '#72190E', '#42150A']
#remove broken symlinks
find -L . -name . -o -type d -prune -o -type l -exec rm {} +
#remove symlinks
find -type l -delete

#chmod files
chmod 0644 #files
chmod 0755 #folders
chmod 0711 #folders no see

grep -o <only print exact matches to pattern>
  
cat test.fastq | paste - - - - | cut -f 2 | tr -d '\n' | wc -c #count bp in fastq

grep -Fxvf Run_accession_numbers.txt files.txt #find difference beween two files
```
