FROM sagemathinc/cocalc-kubernetes-project

USER root

# Add current R version
RUN add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/' &&\
 apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
RUN apt update && apt install libboost-all-dev libxml2-dev r-base-y
RUN umask 022 \
  && echo "install.packages(c('readr', 'tidyr', 'stringr', 'data.table', 'ggplot2', 'readxl', 'kableExtra', 'VGAM', 'OneR', 'multgee', 'ordinal', 'effects'));" | R --no-save

USER user

ENTRYPOINT ["/cocalc/bin/tini", "--"]
CMD ["sh", "-c", "env -i /cocalc/init/init.sh $COCALC_PROJECT_ID"]
