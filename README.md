# SeqSite: Seeking for ChIP-Seq Binding Sites

SeqSite is useful to identify transcription factor binding sites 
based on ChIP-seq data. It can pinpoint closely spaced binding sites
and isolated binding sites in detected binding regions at a 
high resolution. 

##  INSTALLATION

1. Clone the most updated SeqSite source code package

  `git clone https://github.com/sunlightwang/SeqSite.git`

2. Type 'make' to generate the binary file SeqSite.

  `make`

3. Type 'make install' to copy the executable file SeqSite 
to your directory for binary files: ~/bin 

   The default installing path is ~/bin. 
   Please specify BIN_DIR in Makefile, if you want to install 
   SeqSite to anywhere else.

  `make install`

4. Type 'SeqSite' to get the information how to run it.

  `SeqSite -h`


## RUN SeqSite NOW!

* Input files for SeqSite

    ChIP-seq tags: a BED file with 4 fields required: chrId, start, end, and strand
    Control tags:  a BED file with 4 fields required: chrId, start, end, and strand

    It is recommended to run SeqSite with control data, although it is 
    not required.

    Users can download PERL script provided on our website 
    http://bioinfo.au.tsinghua.edu.cn/seqsite/
    to convert other formats to BED. 


* Usage
```
    SeqSite [options] <input.bed> <output.bar> <output.bed>
        input.bed    ChIP-seq data in BED format (4 fields required: chrId, start, end, and strand)
        output.bar   BAR file containing binding sites identified
        output.bed   BED file containing binding regions detected
    Options: ( * advanced )
        -c <string>  control data in BED format (4 fields required) (default: not use)
        -g <int>     effective genome size (default: 2.4e+9 for the human genome)
        -d <int>     * tag clustering distance (default: 30)
        -n <int>     * min tag count in a tag cluster (default: 10)
        -S           * filter single-strand tag clusters (default: not filter)
        -l <double>  * average DNA fragment length (default: estimate from data)
        -t <int>     * top <int>% tag clusters for frag. length estimating (default: 5)
        -p <double>  p-value cutoff for binding region detection (default: 1e-3)
        -f <double>  FDR for binding region detection (default: 0.1)
        -s <int>     * arm length for smoothing tag signal (default: 20)
        -k <int>     * kernel density bandwidth for smoothing tag signal (default: use -s)
        -w <int>     * experimental motif width (default: 20)
        -F           * filter out the duplicate reads (default: FALSE)
        -q           quiet: no screen display (default: show progress)
    Help Options:
        -h           show this help message
        -v           show version information
        -a           about SeqSite
```

* Output files of SeqSite

    - BED file for binding regions

            Each column of the BED file represents:
            chr#, start, end, read-count|fold-change|p-value|q-value, score, strand(+)

    - BAR file for binding sites

            Each column of the BAR file represnets:
            chr#, position, p-value, fold-change, q-value, R-square, slope(normalized)

## EXAMPLES

We provide an example for a quick start.

1. Please download the following data files first:

    GABP ChIP-seq data: http://bioinfo.au.tsinghua.edu.cn/seqsite/files/GABP.bed.gz

    Control data:       http://bioinfo.au.tsinghua.edu.cn/seqsite/files/RX_noIP.bed.gz

2. Unzip the files
  
    `gunzip GABP.bed.gz`

    `gunzip RX_noIP.bed.gz`

3. Run SeqSite 

    `SeqSite -c ./RX_noIP.bed ./GABP.bed GABP.SeqSite.BS.bar GABP.SeqSite.BR.bed`


## BUGS and COMMENTS

Please return any bug reports and questions to 
Xi Wang ( xi dot wang at mdc-berlin dot de)

## CITATION 

[1] Xi Wang and Xuegong Zhang. (2011) Pinpointing Transcription Factor Binding Sites from ChIP-seq Data with SeqSite. BMC Systems Biology, 5(Suppl 2):S3. 

