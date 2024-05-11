# Downloading data from SRA

I tried several approaches but had issues. The one that worked in the end was to use wget to download the SRR file and then use fasterq-dump from the SRA toolkit to unpack this.
```
wget https://sra-pub-run-odp.s3.amazonaws.com/sra/SRR19560467/SRR19560467
```
```
#!/bin/sh
#SBATCH --job-name=fasterq-dump
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --time=8:00:00
#SBATCH --mem=32gb
#SBATCH --output=fasterq-dump.%J.out
#SBATCH --error=fasterq-dump.%J.err
#SBATCH --account=rrg-ben

module load StdEnv/2023  gcc/12.3 sra-toolkit/3.0.9
fasterq-dump ${1}
```


# scRNA tutorial

I'm using jupyter notebooks for this. In terminal type this:
```
jupyter notebook --notebook-dir=/Users/Shared/Previously\ Relocated\ Items/Security/benstuff/2024_grants/NSF_2024/single_cell/scRNAseq_best_practices/single-cell-tutorial/latest_notebook
```

# installing python modules on jupyter
```
!{sys.executable} -m pip install rpy2
```

# Downloading data
This is a good place to start:
https://statbiomed.github.io/SingleCell-Workshop-2021/preprocess.html
```
#!/bin/sh
#SBATCH --job-name=fasterq-dump
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --time=8:00:00
#SBATCH --mem=32gb
#SBATCH --output=fasterq-dump.%J.out
#SBATCH --error=fasterq-dump.%J.err
#SBATCH --account=rrg-ben

module load StdEnv/2023  gcc/12.3 sra-toolkit/3.0.9
# don't add a suffix to the SRA number:
# sbatch 2024_fasterq-dump.sh SRR19560456
fasterq-dump --split-files ${1}
```
