FROM --platform=linux/amd64 ubuntu:20.04
RUN apt-get update && \
	apt-get install -y \
	python3-pip \
	git \
	wget \
	zip

# install HMMer 3.3.2 (used by BiG-SCAPE and GTDB-TK)
RUN wget https://s3.amazonaws.com/share.jgi-ga.org/satria/hmmer-3.3.2.tar.gz \
	&& tar zxf hmmer-3.3.2.tar.gz \
	&& cd hmmer-3.3.2 \
	&& ./configure --prefix / \
	&& make \
	&& make install

# install FastTree(MP) 2.1.11 
RUN wget https://s3.amazonaws.com/share.jgi-ga.org/satria/FastTree.c -P /bin/ \
	&& cd /bin \
	&& gcc -DOPENMP -fopenmp -O3 -finline-functions -funroll-loops -Wall -o FastTree FastTree.c -lm

# install pplacer
RUN wget https://s3.amazonaws.com/share.jgi-ga.org/satria/pplacer-linux-v1.1.alpha19.zip -P /bin/ \
	&& cd /bin \
	&& unzip pplacer-linux-v1.1.alpha19.zip

ENV PATH="$PATH:/bin/pplacer-Linux-v1.1.alpha19/"

# install FastANI
RUN wget https://s3.amazonaws.com/share.jgi-ga.org/satria/fastANI-Linux64-v1.33.zip -P /bin/ \
	&& cd /bin \
	&& unzip fastANI-Linux64-v1.33.zip

# install Mash
RUN wget https://s3.amazonaws.com/share.jgi-ga.org/satria/mash-Linux64-v2.3.tar -P /bin/ \
	&& cd /bin \
	&& tar xf mash-Linux64-v2.3.tar \
	&& ln -sf /bin/mash-Linux64-v2.3/mash /bin/

# install Prodigal 2.6.3
RUN wget https://s3.amazonaws.com/share.jgi-ga.org/satria/prodigal.v2.6.3.zip -P /bin \
	&& cd /bin \
	&& unzip prodigal.v2.6.3.zip \
	&& cd Prodigal-2.6.3 \
	&& make install \
	&& ln -sf /bin/Prodigal-2.6.3/prodigal /bin/

# install BiG-SCAPE 1.1.5
RUN wget https://s3.amazonaws.com/share.jgi-ga.org/satria/bigscape.v1.1.5.zip -P /bin/ \
	&& cd /bin \
	&& unzip bigscape.v1.1.5.zip \
	&& cd BiG-SCAPE-1.1.5 \
	&& pip install . \
	&& pip install numpy scipy scikit-learn biopython networkx pyhmmer \
	&& cd /usr/local/bin/ \
	&& wget https://s3.amazonaws.com/share.jgi-ga.org/satria/Pfam-A.v3.5.hmm.gz \
	&& gunzip Pfam-A.v3.5.hmm.gz \
	&& mv Pfam-A.v3.5.hmm Pfam-A.hmm \
	&& hmmpress Pfam-A.hmm \
	&& ln -sf /usr/local/lib/python3.8/dist-packages/BiG-SCAPE/html_template/ /usr/local/bin/ \
	&& ln -sf /usr/local/lib/python3.8/dist-packages/BiG-SCAPE/Annotated_MIBiG_reference /usr/local/bin/ \
	&& ln -sf /usr/local/lib/python3.8/dist-packages/BiG-SCAPE/anchor_domains.txt /usr/local/bin/ \
	&& ln -sf /usr/local/lib/python3.8/dist-packages/BiG-SCAPE/domain_includelist.txt /usr/local/bin/ \
	&& ln -sf /usr/local/lib/python3.8/dist-packages/BiG-SCAPE/domains_color_file.tsv /usr/local/bin/ \
	&& ln -sf /bin/FastTree /bin/fasttree

# install GTDB-TK
RUN wget https://s3.amazonaws.com/share.jgi-ga.org/satria/gtdbtk.2.1.1.zip -P /bin/ \
	&& cd /bin \
	&& unzip gtdbtk.2.1.1.zip \
	&& cd GTDBTk-2.1.1\
	&& pip install .

ENV GTDBTK_DATA_PATH="/data/gtdb_ref/release207_v2"

ENTRYPOINT bash
