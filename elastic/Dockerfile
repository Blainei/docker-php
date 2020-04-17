FROM docker.elastic.co/elasticsearch/elasticsearch:7.6.2@sha256:59342c577e2b7082b819654d119f42514ddf47f0699c8b54dc1f0150250ce7aa
RUN  yum install -y wget
WORKDIR /usr/share/elasticsearch/plugins
RUN wget -O analysis-ik.zip https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v7.6.2/elasticsearch-analysis-ik-7.6.2.zip \
    && mkdir analysis-ik \
    && unzip analysis-ik.zip -d analysis-ik \
    && rm -rf analysis-ik.zip
