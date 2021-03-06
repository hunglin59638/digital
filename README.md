# Digital: A pipeline to annotate protein sequences  
## Introduction
Digital is a pipeline for annotation of proteins sequence. It could annoate with eggnog-mapper and align NR database with diamond.
## Requirements
+ linux
+ python >= 3.6
+ eggnog-mapper >= v2.1.2
+ diamond

## Installation

### git  
Running the `setup.py` will install [eggnog-mapper](https://github.com/eggnogdb/eggnog-mapper) and [diamond](https://github.com/bbuchfink/diamond) to `lib` directory.
If the software exists, the installation will be skipped.

```
git clone https://github.com/hunglin59638/digital.git
cd digital
./setup.py
./digital -h
```
`$root_dir` is the installation path of digital 
```
export PATH="$root_dir/digital:$root_dir/lib/eggnog-mapper:$root_dirdigital/lib:$PATH"
```
### docker
```
docker pull hunglin59638/digital:latest
docker run hunglin59638/digital digital -h
```

### Databases
+ diamond  (optional)  
Downloading NR database by diamond format or you can build by yourself  
paste the link (`https://docs.google.com/u/0/uc?export=download&confirm=aPno&id=1TnXJVYOiJ7vuCxSFdqfTwXKe6ov_jVDX`) to web browser and download file `nr.dmnd.gz`
```
gzip -d nr.dmnd.gz
```
+ eggnog-mapper (required)  
```
 download_eggnog_data.py -y --data_dir [eggnog_data_dir]
```
## Test
+ ubuntu 
```
digital --fasta test/test.faa --out_dir test/out --prefix test --data_dir [eggnog_data_dir]
```  
+ docker 
```
docker run -v [out_dir]:/data -v [eggnong_dir]:/opt/digital/db/eggnong  -v [nr_dmnd_dir]:/opt/digital/db/diamond hunglin59638/digital:latest digital --fasta /opt/digital/test/test.faa --out_dir [out_dir] --prefix test --data_dir /opt/digital/db/eggnong

```
## Usage
+ use diamond and emapper
```
digital --fasta [protein.fasta] --nr_dmnd [data_dir]/nr.dmnd --data_dir [eggnog_data_dir] --out_dir [out_dir]
```
+ skip diamond
  ```
  digital --fasta [protein.fasta] --out_dir [out_dir] --data_dir [eggnog_data_dir]
  ```
the results will output to [out_dir]

+ [prefix]_annotation.json  
annotation result
+ diamond.txt  
protein alingment file from diamond  
+ emmaper  
the directory contain files from emapper 

