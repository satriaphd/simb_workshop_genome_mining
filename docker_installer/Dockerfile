FROM ubuntu:20.04
RUN apt-get update && \
	apt-get install -y \
	python3-pip \
	git \
	wget \
	zip

# install HMMer 3.3.2 (used by BiG-SCAPE and GTDB-TK)
RUN wget http://eddylab.org/software/hmmer/hmmer.tar.gz \
	&& tar zxf hmmer.tar.gz \
	&& cd hmmer-3.3.2 \
	&& ./configure --prefix / \
	&& make \
	&& make install

# install FastTree(MP) 2.1.11 
RUN wget http://www.microbesonline.org/fasttree/FastTree.c -P /bin/ \
	&& cd /bin \
	&& gcc -DOPENMP -fopenmp -O3 -finline-functions -funroll-loops -Wall -o FastTree FastTree.c -lm

# install pplacer
RUN wget https://github.com/matsen/pplacer/releases/download/v1.1.alpha19/pplacer-linux-v1.1.alpha19.zip -P /bin/ \
	&& cd /bin \
	&& unzip pplacer-linux-v1.1.alpha19.zip

ENV PATH="$PATH:/bin/pplacer-Linux-v1.1.alpha19/"

# install FastANI
RUN wget https://github.com/ParBLiSS/FastANI/releases/download/v1.33/fastANI-Linux64-v1.33.zip -P /bin/ \
	&& cd /bin \
	&& unzip fastANI-Linux64-v1.33.zip

# install Mash
RUN wget https://github.com/marbl/Mash/releases/download/v2.3/mash-Linux64-v2.3.tar -P /bin/ \
	&& cd /bin \
	&& tar xf mash-Linux64-v2.3.tar \
	&& ln -sf /bin/mash-Linux64-v2.3/mash /bin/

# install Prodigal 2.6.3
RUN wget https://github.com/hyattpd/Prodigal/archive/refs/tags/v2.6.3.zip -P /bin \
	&& cd /bin \
	&& unzip v2.6.3.zip \
	&& cd Prodigal-2.6.3 \
	&& make install \
	&& ln -sf /bin/Prodigal-2.6.3/prodigal /bin/

# install BiG-SCAPE 1.1.5
RUN wget https://github.com/medema-group/BiG-SCAPE/archive/refs/tags/v1.1.5.zip -P /bin/ \
	&& cd /bin \
	&& unzip v1.1.5.zip \
	&& cd BiG-SCAPE-1.1.5 \
	&& pip install . \
	&& pip install -r requirements.txt \
	&& pip install scikit-learn \
	&& cd /usr/local/bin/ \
	&& wget https://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.hmm.gz \
	&& gunzip Pfam-A.hmm.gz \
	&& hmmpress Pfam-A.hmm

# install GTDB-TK
RUN wget https://github.com/Ecogenomics/GTDBTk/archive/refs/tags/2.1.1.zip -P /bin/ \
	&& cd /bin \
	&& unzip 2.1.1.zip \
	&& cd GTDBTk-2.1.1\
	&& pip install .

ENV GTDBTK_DATA_PATH="/data/gtdb_ref/release207_v2"

ENTRYPOINT bash
